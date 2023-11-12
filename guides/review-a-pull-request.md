---
description: >-
  This describes how a pull request should be handled for both reviewers and
  reviewee
---

# Review a pull request

### General

* Join the **git channel** on Slack to get updates
* Include the issue key if you are doing it
* PR description is **compulsory**, do not use the generated description, this helps give the reviewers a quick look on how you solve the problem
  * <mark style="color:blue;">If it's a bug, add reasons and solutions</mark>
* Add tests where necessary

### <mark style="color:blue;">Avoid conflicts</mark>

<mark style="color:blue;">**Which branch to starts?**</mark>

* <mark style="color:blue;">Work with PM if it’s unclear when your implementation will be released and starts checkout from the appropriate branch</mark>
* <mark style="color:blue;">Communicate with Tech Lead to know if someone else will also working on the same area of your work</mark>
  * <mark style="color:blue;">If yes, work with that teammate and cherrypick their commits if needed</mark>

<mark style="color:blue;">**Syncing with main branches**</mark>

* <mark style="color:blue;">Always create your PR with no commits behind the destination branch (Reviewer will check at the moment your PR is created)</mark>

<figure><img src="../.gitbook/assets/Screenshot 2023-11-12 at 16.38.42.png" alt=""><figcaption></figcaption></figure>

<mark style="color:blue;">**Mindset**</mark>

* <mark style="color:blue;">You’ve just created a PR, it’s not done yet</mark>
  * <mark style="color:blue;">Keep watching your PRs and update them regularly</mark>

### Reviewing a PR

* Mr. Silver will be the **main reviewer**
* Within 2 hours (in working hours) since the time the PR is created, there should be an update
* If a PR takes a long time to handle, there will be a comment of **reviewing** from the main reviewer
* Sometimes, other core members (Dung, Duong and Kevin) will be added to review your code
* If the PR is good, it will be approved

### When a PR needs a review session

* <mark style="color:blue;">Silver</mark> <mark style="color:blue;"></mark><mark style="color:blue;">**has a review session everyday**</mark><mark style="color:blue;">, check our calendar and come join him if needed or being asked</mark>
* If a PR needs a demo, or more detailed explanation, **a review session** is needed then PR owner shall proactively come to the lab ASAP to have the PR reviewed.&#x20;
* It will be marked **requested changes** and all steps of handling a requested change PR will be applied

### When a PR is ready to be merged

* One (the other does not raise a request changes) or all reviewers approve

### When you are assigned to be a reviewer in a PR

* Review and update the PR within 2 hours
* If you have a comment, tag the PR owner so that they know and update their PR

### When your PR is requested changes

Not necessarily from the main reviewer, if you get **at least one request changes** (though other members might have already approved), follow the steps below

* Read the comments and make sure you understand why it is requested changes
* If you failed to update the PR within **4 hours**, it will be **declined** and the reviewer will reopen your issue

