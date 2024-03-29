---
title: Mocking is a code smell
---


- take example code
- show how to unit test with stubs
- extract the bl
- show how to unit test without stubs

## The three types of code

### Business logic
Business logic is the code that actually manipulates your data based on your business rules. Examples:

- Perform calculations on retrieved data
- Combine data
- Set defaults for data

### Data access

- Read/write data from a database
- Make external calls to other services (http calls, etc)

### Plumbing
- Orchestrate the above code by connecting the outputs of functions to inputs of other functions.


Lets start with some *bad code*:

```javascript
const homeRouter = async (fastify) => {
  fastify.post('/burger', async (req, res) => {
    const burger = req.body;
    // Validation
    if (!burger.meatScore) {
      return
    }
    if (!burger.bunScore) {
      return
    }
    // Transformation
    const burgerData = {
      meatScore: burger.meatScore,
      bunScore: burger.bunScore,
      id: uuidv4()
    }
    // Business Logic
    burgerData.totalScore = burgerData.meatScore + burgerData.bunScore

    // Data Access
    const pipeline = redis.pipeline();
    pipeline.hset({burgerData});
    pipeline.zadd(burgerData.totalScore, burgerData.id);
    await pipeline.exec();

    //Response formatting
    return res
    .code(200)
    .header('Content-Type', 'application/json; charset=utf-8')
    .send({ hello: 'world' })
  })
}

```

Let's quickly talk about why this is bad code. In general, whre possible, a peice of code should have a single purpose, 
or a single reason to change. This is called the single responsbility principal. A peice of code that has a single reason to change should in theory have a single, or at least simple, way to break. A peice of code that has multiple reasons to change will have multiple reasons to break: it is complex. Complex code means that we have to understand it more to modify it without breaking it, which is hard for humans to do.

So how many reasons to change does this code have? At least 5. Either the validation, transformation, data access, or response logic could change.

First let's do the obvious, which is how most apps are structured, and pull out the data access 


```javascript
// validation.js
const validate = (burgerData) {
  if (!burger.meatScore) {
    throw new Error('no meat score!')
  }
  if (!burger.bunScore) {
    throw new Error('no burger score!')
  }
  // etc...
}
module.exports = { validate }

// bl/burger.js

const createBurger = (burger) => {
  const burgerData = {
    totalScore: burger.meatScore + burger.bunScore,
    meatScore: burger.meatScore,
    bunScore: burger.bunScore,
    id: uuidv4()
  }
  return burgerData;
}

// dal/burgerDAL.js

const writeBurger = async (burger) => {
  const pipeline = redis.pipeline();
    pipeline.hset({burgerData});
    pipeline.zadd(burgerData.totalScore, burgerData.id);
    await pipeline.exec();
}

// routes.js

const { validate } = require('validation.js');
const burgerBl = require('bl/burger.js');
const burgerDAL = require('dal/burgerDAL.js');

const homeRouter = async (fastify) => {
  fastify.post('/burger', async (req, res) => {
    const burgerData = req.body;
    
    const burger = burgerBL.createBurger(burgerData);
    
    return res
    .code(200)
    .header('Content-Type', 'application/json; charset=utf-8')
    .send(burgerData)
  })
}

```





Now we want to test this code, burger.js has no dependencies, so there is nothing to mock. We can just test it directly.
To unit test routes.js we would need to mock out validation.js, burger.js, and burgerDAL.js, all of which could be fairly complex mocks in the real world.
Once we've done this, what can we actually test? What changes can we make to routes.js that would break the tests? We could change the order of the functions, or the names of the functions, but that's about it. We can't change the logic of the functions without breaking the tests. This is a code smell. We have to mock out so much code to test this code that we can't actually test anything.

The bike: an anology.
Another way to think about this is to think about testing a bike. you can test certain features of a bike individually, like the thickness of the tires, the size of the wheels, but the best way to test 
that the bike will slow down when you apply the breaks isnt to create an aparatus for testing the friction of every single break pad, its to test the bike as a whole. 

Ways to change

Our goal with testing is to be able to allow the code under test to be as flexible as possible while still passing the test. If you cant refactor the code without it breaking your test, you have a brittle test
which means you will have to spend more time fixing tests than you should. The better your abstraction, the better your code. In the bike example, you can easily remove the wheel of a bike and replace it with any other wheel without an issue, there is a single interface, the dropout, which has defined standards about size.