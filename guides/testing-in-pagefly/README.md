---
description: >-
  In order to sustain a stable product and have the best deliveries to our
  customers, since 2022, we integrate the testing process into the development
  in an official way.
---

# Testing in PageFly

### Types of tests

We long for a great product so basically we aim at the maximum number of tests. And within an affordable time frame, we successfully adopted 2 main test types which are **Unit Tests** and **Automation Tests**. The grand total of tests at the time that this guideline is being documented is approximately 100.&#x20;

### Getting started

After successfully configuring `pfcore` and `pfserver` projects, you may try running `yarn test` to execute Unit Tests and `yarn uitest` for Automation Tests.

_There is an extra step if you're playing around with Automation Tests related to MacOS permission, make sure you grant that to your IDE. Also, your mouse will be controlled by the Automation so do not use it._
