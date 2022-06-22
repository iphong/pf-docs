---
description: This covers unit level of your implementation
---

# Unit Tests

Testing is not a very popular topic generally as nowadays it has been shocking to see that it seems like everybody does not need a single test for their application. PageFly has been roughly through that ancient time and suffered quite a lot, also, our customers also have to.

### First thing first, what to test

The main purpose of this is safeguarding your code so that when a new change is applied, it won't easily affect your master piece. So the level of testing this time really **depends** on the complication of your own implementation. While reviewing, if the main reviewer may require a few extra tests, you may need to add them later.

If you have programmed a good new feature and are required to add tests for it, don't hurriedly go pack all your files to the test space. Indeed, you would need to be very mindful on which is needed to have tests. In most cases, you will need your very core functions to be well tested. However it's not necessarily useless if you also have your components rendering tested.

For example, while implementing the new Analytics feature, we have a pricing modal including the `custom-dragger` shown up when it's required to upgrade and a core function that calculates the time zone which is essentially core. So basically we have one component and a function needed to be safeguarded. And that's totally fine.



