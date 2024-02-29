---
description: >-
  You've done with finding solutions, it's time for actual collaborating with
  team via pull requests
---

# How to create a good Pull Request

## General

* Join the **git channel** on Slack to get updates
* Include the issue key if you are doing it

## Do not overlook the description

PR description is **compulsory**, do not use the generated description, this helps give the reviewers a quick look on how you solve the problem

* <mark style="color:blue;">Submit the proposal for your work</mark>
* Add a checklist of cases that you have tested on your development environment
  * For example: a pull request that fix the slideshow won't work should have a list of test cases like this
    * Check slideshow in product media
    * Check slideshow elements in section
    * ...

## Setup your main branch

Depending on the release schedule, your implementation may be checked out from `staging` or `development` Add a prefix for your main branch following the below format

**`feat`**`-abc` or **`fix`**`-desktop-view`

Please create a PR from your main branch to the designated branch like so `feat-abc` to `development` Doing this will help all devs know which features are being implemented and keep them up-to-date if conflicts are araised.

_Note: Make sure your branches or the main branch have no upper case letter_

## Do not push code directly to your main branch as you might not work alone

You and every member in your team should have separated branches (eg: `feat-abc-by-silver`). Daily PR to the main branch is recommended.&#x20;

## Do not merge the PRs

Let the seniors review first then they shall merge them into the main branch, not you

You should resolve your issue if you're done with all the work on the main branch, no need to wait for the code is merged to `development` or `staging` .

### Avoid conflicts

**Which branch to starts?**

* Work with PM if it’s unclear when your implementation will be released and starts checkout from the appropriate branch
* Communicate with Tech Lead to know if someone else will also working on the same area of your work
  * If yes, work with that teammate and cherrypick their commits if needed

**Syncing with main branches**

* Always create your PR with no commits behind the destination branch (Reviewer will check at the moment your PR is created)

<figure><img src="../../.gitbook/assets/Screenshot 2023-11-12 at 16.38.42.png" alt=""><figcaption></figcaption></figure>

**Mindset**

* You’ve just created a PR, it’s not done yet
  * Keep watching your PRs and update them regularly

### When your PR is requested changes

Not necessarily from the main reviewer, if you get **at least one request changes** (though other members might have already approved), follow the steps below

* Read the comments and make sure you understand why it is requested changes
* If you failed to update the PR within **4 hours**, it will be **declined** and the reviewer will reopen your issue
