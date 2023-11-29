---
description: >-
  Below is a step-by-step guideline I suggest developers follow when resolving
  an issue.
---

# Resolving issues guidelines

## General

The procedure can be split into two parts: researching (steps 1 to 3) and coding (steps 4 to 6). At the end of the first part, I think it will be better if developers submit a Google form that states the result of the first three steps before continuing to the second part.

## Understanding the issue first

Some developers start coding as soon as they receive an issue. This behavior might lead to misunderstanding the problem and less effective solutions.

It will be better if developers step back to see an overview of the problem first. Then, look closer to find out details from different points of view. If anything is not clear, developers need to clarify it with stakeholders.

## Find at least 2 solutions

After understanding the problem, some developers start coding the very first idea flashing in their minds. Most of the time, it’s not the best solution.

Developers should find as many solutions as possible before writing the first line of code. If the time is limited, try to find at least two solutions.

## Choose the simplest solution

In software development, a simple solution can save a lot of coding, understanding, and debugging hours. Not only for the developer who implements it but also for another developer who maintains it later.

When developing a new feature, I would suggest the simplest solution is a solution that is independent, reusable, and does not affect other functionalities of the application.

When fixing a bug, the simplest solution must ensure a thorough fix without creating unnecessary new structures or mechanisms and not generating similar new code in different places.

If you see more than one simple solution, estimate the total number of lines of code. A solution that requires fewer lines of code is the better solution.

If you’re still confused after analyzing every solution, don't be afraid to discuss it with your teammates for more points of view. Remember that you're not alone!

## Write automated tests

At this step, developers need to write automated tests for every case that might occur. Sure, the test will fail immediately because the code is not written yet. The purpose of test-driven development is to write code to pass each designed test case until all is done.

Fail soon, fix soon, no bugs slip out. So, smile when it fails!

## Start coding

It's time to feel free to write code. However, don't rely on automatic formatting. Instead, write each line of code yourself that complies with the coding standards. It shows your seriousness. When you are serious, bugs are more likely to be seen as soon as you write code. The [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript) is a good coding standard to follow.

When coding your solution, it is important to pay attention to the three aspects described below.

Separation of concerns is a concept that each component or module should be independent and responsible for a single part of the functionality. It does not mean you need one component or module for each function. The intention is to ensure that you don’t have universal objects that do everything and, hence, are sensitive to change.

Keep it simple, stupid (KISS) is a design principle that states that designs or systems should be as simple as possible. Simplicity guarantees acceptance and usability. Simplicity also prevents unwanted side effects or potential bugs.

Developers should write code as simply as possible. A line of code using nested ternaries or more than two operators, conditions, or function calls becomes complex. It should be split into multiple lines of code.

Additionally, unless a list of import statements, developers should frequently use blank lines to separate code blocks for easy reading. More than three continuous lines of code without a blank line should be avoided.

Don’t Repeat Yourself (DRY) is about modularity and reusable. Code repeats in more than two places, even only one line, should be converted to a reusable function. You might see it as a waste of time and unnecessary. However, imagine if that line of code needs to be updated. If you convert it to a reusable function, you can alter it in just one place. It will save time and help prevent bugs.

## Do user testing

Sometimes, users use the product not in the way the software was designed, even in a way not considered when designing the software. This behavior can cause errors that developers did not expect before.

Once coding is complete, developers should perform user testing before passing it to QA. User testing does not focus on technicalities but on usability. So, let the people involved in a test do what they want. You can introduce something about what you have done but let users use it their way.

Developers should record all actions users make when using the software so potential errors are not missed.

## Side notes

<mark style="color:purple;">If you can not fix the bug</mark> <mark style="color:purple;"></mark><mark style="color:purple;">**before the due date**</mark><mark style="color:purple;">, your issue will be delegated to other team member and your KPI will not be recorded</mark>
