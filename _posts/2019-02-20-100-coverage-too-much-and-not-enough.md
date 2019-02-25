

Code coverage percentage is a controversial subject: some will tell you that you get diminishing returns after 70-80% and it's not worth bothering, others will say that 100% is not enough. The underlying problem is often the approach taken to testing:

## 100% coverage as a goal is counterproductive
Code coverage tools tell you how much of your code has been tested, not how well that code has been tested.
* Code coverage only applies to the code you have written, and doesn't highlight the features you've forgotten to implement.
* Achieving high code coverage with low quality is relatively simple, but only results in the code being run, not being tested. It's possible to hit 100% code coverage with 0 assertions!

No assertions:
![A test that doesnt test anything](/assetts/img/no-assertions.png)
But our tool is happy!
![100% coverage](/assetts/img/full-coverage.png)
[(code on github)](https://github.com/kraftman/coverage-example/tree/100-percent-coverage)

If features drive your testing, you are more likely to find missing code paths, and to write assertions for the features. If coverage drives your testing, your are likely to write low quality, brittle tests that satisfy the coverage tool - missing assertions and missing omissions in your logic. This is a problem because:

* Your customer doesn't care about your coverage, hitting 100% doesn't help them if your code is still full of bugs. Tests should focus on surfacing bugs, not satisfying tool output.
* You lose insight into the areas that need to be more thoroughly tested: when 100% of your code is covered by low quality tests, your code coverage tool becomes useless.

## 100% unit test coverage != 100% test coverage
When looking at the test pyramid, it's easy to assume that if you're aiming for 100% test coverage, that means you should be hitting 100% coverage with your unit tests, ~60% with component tests, ~30% with integration tests etc. This misses the point of the tests pyramid: that each layer higher in the test pyramid performs a different function to the layer below, and should fill in the gaps that the layer below wasn't able to cover.

Unit testing glue-code with tonnes of mocks is possible, but the effort to value ratio is pretty bad: you'll end up duplicating the same tests at a higher level anyway, and then have more tests to fix when you change that code later.

## Not all code is equal
Some code is much more important than other code. Your focus should be on testing the important code thoroughly, not in wasting effort setting up mocks for the less important code.

Some projects have more risk than others. Are you writing banking software for millions of paying users, or a side project for fun? Scale your testing time appropriately.

Conclusion
Use your product requirements to drive testing. Use the risk factors of your product to determine how thorough your tests need to be. Use your code coverage tool as a tool, to tell you where best to spend your limited amount of time, not as a goal to give you a false sense of security.

Related reading:

https://martinfowler.com/bliki/TestCoverage.html
http://www.exampler.com/testing-com/writings/coverage.pdf



