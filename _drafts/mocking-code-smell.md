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
    const burgerData = {
      totalScore: burger.meatScore + burger.bunScore,
      meatScore: burger.meatScore,
      bunScore: burger.bunScore,
      id: uuidv4()
    }
    const pipeline = redis.pipeline();
    pipeline.hset({burgerData});
    pipeline.zadd(burgerData.totalScore, burgerData.id);
    await pipeline.exec();
    return res
    .code(200)
    .header('Content-Type', 'application/json; charset=utf-8')
    .send({ hello: 'world' })
  })
}

```

First we break 