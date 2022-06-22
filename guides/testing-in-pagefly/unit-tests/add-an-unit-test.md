---
description: >-
  The whole project has been already setup, mocked, configured so that you just
  need to add your own test
---

# Add an Unit Test

We use `jest` test library so let's take a quick look on this [docs](https://jestjs.io/docs/getting-started) for syntax and basic test cases

### Create the file

Place it inside `__test__` folder

It's recommended to have your test file named as follow rule `your-test-file-name.test.ts` If your test is at the component level, named the file ends with `tsx` instead.

### 3 basic test cases

In order to have the most real life like data, 3 cases of tests below are recommended

#### Case 0

Have at least one test case when given data is `null` or `undefined`

#### Case 1

Another test case for regular expectation with an average amount of data

#### Case Many

One last case for extremely large amount of data to spot out performance issue if any

### One last step

Run `yarn test` or follow [this](https://jestjs.io/docs/cli#--testnamepatternregex) to run only your test

_You may refer to some already written tests in the project to have more info_

