---
title: 5 reasons to test first
---

From 'The Clean Coder'

## 1 Change Certainty

Whenever you make a change and your tests pass you can be almost certain that you didn't break anything.

## 2 Lower Defect Injection Rate

High test coverage catches more breaking changes, resulting in a lower defect injection rate.

## 3 Courage

Why don't people fix bad code? Because they worry it will break something and they will get blamed. Fast high coverage tests means you know you haven't broken anything.
This means you lose fear of making changes, and changes can be made faster and more often to clean up the code.
Clean code is easier to understand, easier to change, and easier to extend. Clean code is less likely to contain defects because it is simpler.

## 4 Documentation 

High coverage means you have documentation for every meaningful way a function can be called, and its expected responses.

## 5 Design

In order to test code you must isolate it, and to isolate it you must decouple it from the rest of the code. To decouple it you must design it well. Testing first improves the design of the code, testing afterwards doesn't affect the design unless you rewrite all of the code.

