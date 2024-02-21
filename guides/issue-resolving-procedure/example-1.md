---
description: >-
  Display a survey to PageFly users to collect their needs for the Black Friday
  campaign.
---

# Example 1

### 1. Understand the issue

#### 1.1. Define the issue

Although the requirement is straightforward, we should still use the 5W1H method to define the request to _“display a survey to PageFly users to collect their needs for the Black Friday campaign”_.

{% hint style="success" %}
**Topic:** Collect the needs of PageFly users for their Black Friday campaign.

**What:** To understand the real needs of PageFly users for their Black Friday campaign.

**Who:** Marketing, design, and dev team.

**Where:** Regions where the Black Friday event will occur.

**When:** Before the Black Friday event occurs.

**Why:** Fulfilling users’ needs for their Black Friday campaign.

**How:** Display a survey on the dashboard and maybe other pages of PageFly to users who live in regions where the Black Friday event will occur.
{% endhint %}

By answering the 5W1H questions, we understand that the primary purpose of the issue is _**to understand users’ needs to make PageFly fulfill exactly what users need for their Black Friday campaign**_.

#### 1.2. Analyze the issue

We can use the 5 Whys method to analyze the request to _“display a survey to PageFly users to collect their needs for the Black Friday campaign”_ as follows.

{% hint style="success" %}
**Why do we need to collect the needs of PageFly users for their Black Friday campaign?**

\=> To understand the users’ needs.

**Why do we need to understand the users’ needs?**

\=> To fulfill users’ needs.

**Why do we need to fulfill users’ needs?**

\=> To keep them using the app.

**Why do we need to keep users using the app?**

\=> If users use the app frequently, they will likely upgrade to a higher plan and pay us more.

**Why don’t we collect users’ needs on other events to keep them using the app more frequently?**

\=> We will also collect users’ needs at other times if needed.
{% endhint %}

Answering the 5 Whys, we know that the root cause for the issue is _**to keep users using PageFly and using it frequently by exactly fulfilling their needs at any specified time**_.

#### 1.3. Frame the issue

We will use the SMART method to frame the request to _“display a survey to PageFly users to collect their needs for the Black Friday campaign”_ as follows.

{% hint style="success" %}
**Specific:** We will collect users’ needs.

**Measurable:** We will collect users’ needs for their Black Friday campaign, and there might be other events.

**Achievable:** We will collect users’ needs for their Black Friday campaign, and there might be other events, to understand what users need at a specified time.

**Relevant:** We will collect users’ needs for their Black Friday campaign, and there might be other events, to understand what users need at a specified time. Based on the users’ needs, our design team can create new features or update existing features for our app to serve users better, and our marketing team can create campaigns that are appropriate to users’ needs.

**Time-bound:** Before Black Friday occurs, and maybe at other times before some specific events, we will collect users’ needs for their sales campaign to understand what users need at a specified time. Based on the users’ needs, our design team can create new features or update existing features for our app to serve users better, and our marketing team can create campaigns that are appropriate to users’ needs.
{% endhint %}

Using the SMART method, we find that we will need _**to implement a solution that can flexibly collect users’ needs during a period and allow non-technical stakeholders to update the survey and see the results**_.

{% content-ref url="processes/1.-understand-the-issue.md" %}
[1.-understand-the-issue.md](processes/1.-understand-the-issue.md)
{% endcontent-ref %}

### 2. Find at least two solutions

Let’s continue with the request to _“display a survey to PageFly users to collect their needs for the Black Friday campaign”_.

We understand that the purpose of this request is _to understand users’ needs to make PageFly fulfill exactly what users need for their Black Friday campaign_ ([step 1.1](example-1.md#id-1.1.-define-the-issue)) _to keep users using PageFly and using it frequently by exactly fulfilling their needs at any specified time_ ([step 1.2](example-1.md#id-1.2.-analyze-the-issue)) _and we will need to implement a solution that can flexibly collect users’ needs during a period and allow non-technical stakeholders to update the survey and see the results_ ([step 1.3](example-1.md#id-1.3.-frame-the-issue)).

{% hint style="success" %}
We need to allow non-technical stakeholders to see the results of the survey, so every solution needs to create an endpoint in the `pfserver` project. Responses from PageFly users will be sent to this endpoint to save to a dedicated collection in the database. Then, we need to create a screen in AC2 to display the user responses to non-technical stakeholders.
{% endhint %}

Now, let’s find solutions for _displaying a survey to PageFly users to collect their needs for the Black Friday campaign_.

We can start from the most direct way to implement the most basic requirements. In this example, after defining the issue, we need _to understand users’ needs to make PageFly fulfill exactly what users need for their Black Friday campaign_ ([step 1.1](example-1.md#id-1.1.-define-the-issue)). Thus, the most direct way to implement this requirement is to code a stand-alone component that directly displays the predefined survey in the `pfcore` project and place it where the survey needs to show.

{% hint style="info" %}
The first solution is to code a stand-alone component that directly displays the predefined survey in the `pfcore` project and place it where the survey needs to show.
{% endhint %}

However, this solution only addresses the display of the predefined survey. Complying with the deeper requirement _to keep users using PageFly and using it frequently by exactly fulfilling their needs at any specified time_ ([step 1.2](example-1.md#id-1.2.-analyze-the-issue)), if stakeholders need to edit or delete existing surveys or create new surveys, this solution will need to manually update the component and redistribute it to the live app server.

Therefore, we should not write the survey content directly in the component that displays the survey. Instead, we should define the survey content as a constant so that changing, deleting, and creating new ones can be done easier.

{% hint style="info" %}
The second solution is defining surveys and their lifetime as a constant in the `pfserver` project and including the active survey in the global configuration. Then, code a stand-alone component in the `pfcore` project and place it where the survey needs to show. The component will look for any survey included in the global configuration and display it.
{% endhint %}

Although this solution is more flexible, each time surveys need to be changed, it still requires updating the constant and redistributing it to the live app server. This action does not comply with the deepest requirement _to implement a solution that can flexibly collect users’ needs during a period and allow non-technical stakeholders to update the survey and see the results_ ([step 1.3](example-1.md#id-1.3.-frame-the-issue)).

To solve this problem, we can move the storage of survey content from the code base to the database. We can then create a tool in AC2 for stakeholders to proactively change, delete, and create new surveys.

{% hint style="info" %}
The third solution is creating a dedicated collection in the database for saving surveys and their lifetime. Then, we will create an endpoint in the `pfserver` project for returning the survey content that should be shown at the current time (active survey). Finally, code a stand-alone component in the `pfcore` project and place it where the survey needs to show. The component will automatically request the endpoint for an active survey and display it if available.
{% endhint %}

There might be more solutions but will mostly be similar. So, we can stop here and continue to the next step to evaluate each solution.

{% content-ref url="processes/2.-find-at-least-two-solutions.md" %}
[2.-find-at-least-two-solutions.md](processes/2.-find-at-least-two-solutions.md)
{% endcontent-ref %}

### 3. Choose the simplest and most effective solution

Let’s resume the request to _“display a survey to PageFly users to collect their needs for the Black Friday campaign”_. We will evaluate and score each solution we found in [step 2](example-1.md#id-2.-find-at-least-two-solutions) by **impact**, **confidence**, and **ease**.

#### 3.1. Evaluate the first solution

{% hint style="info" %}
The first solution is to code a stand-alone component that directly displays the predefined survey in the `pfcore` project and place it where the survey needs to show.
{% endhint %}

Although this solution can resolve the issue, it is not flexible and not reusable because the survey content is hard-coded. In case the survey content needs to be updated or the stakeholders need to create new surveys, we will need to update the hard-coded survey in the `pfcore` project and redistribute the code to the live app environment.

<img src="../../.gitbook/assets/file.excalidraw.svg" alt="" class="gitbook-drawing">

{% hint style="success" %}
For this solution, we can:

* &#x20;_**Score 2 for the impact factor**_ because the solution can resolve only a specific case.
* _**Score 4 for the confidence factor**_ because the solution requires updating the frontend component and redistributing it if the survey content needs to be updated.
* _**Score 8 for the ease factor**_ because the implementation of the solution can be rapid.
{% endhint %}

#### 3.2. Evaluate the second solution

{% hint style="info" %}
The second solution is defining surveys and their lifetime as a constant in the `pfserver` project and including the active survey in the global configuration. Then, code a stand-alone component in the `pfcore` project and place it where the survey needs to show. The component will look for any survey included in the global configuration and display it.
{% endhint %}

This solution is flexible because updating or removing a survey and creating new surveys is easy. However, it still needs to update the constant defined in the `pfserver` project and redistribute it to the live app environment.

<img src="../../.gitbook/assets/file.excalidraw (1).svg" alt="" class="gitbook-drawing">

{% hint style="success" %}
For this solution, we can:

* _**Score 6 for the impact factor**_ because the solution can resolve multiple cases, but changes need time to appear.
* _**Score 6 for the confidence factor**_ because the solution requires updating the constant definition and redistributing it if the survey content needs to be updated.
* _**Score 6 for the ease factor**_ because the implementation of the solution can be fast.
{% endhint %}

#### 3.3. Evaluate the third solution

{% hint style="info" %}
The third solution is creating a dedicated collection in the database for saving surveys and their lifetime. Then, we will create an endpoint in the `pfserver` project for returning the survey content that should be shown at the current time (active survey). Finally, code a stand-alone component in the `pfcore` project and place it where the survey needs to show. The component will automatically request the endpoint for an active survey and display it if available.
{% endhint %}

With this **overall** solution, we only need to code **once** and use it for **a long time**. After distributing the code, all survey-related actions can be done in the database without the need for code redistribution. This behavior allows a survey to be updated or removed instantly. Creating new surveys is also easy and instant.

<img src="../../.gitbook/assets/file.excalidraw (2).svg" alt="" class="gitbook-drawing">

{% hint style="success" %}
For this solution, we can:

* _**Score 10 for the impact factor**_ because the solution can resolve multiple cases, and changes can appear instantly.
* _**Score 10 for the confidence factor**_ because inserting new surveys into the database or updating existing surveys can be done easily without risks.
* _**Score 4 for the ease factor**_ because the implementation of the solution needs more time than the other solutions.
{% endhint %}

#### 3.4. Conclusion

After scoring all solutions, we can conclude that the third solution should be the simplest and most effective solution with the highest ICE score of 24 (the second solution and the first solution have ICE scores of 18 and 14).

Suppose the due date of the Jira issue to _“display a survey to PageFly users to collect their needs for the Black Friday campaign”_ is the same day you receive the issue. We should choose the first solution (which has the shortest implementation time) to ensure the distribution of the feature in time. But, after releasing the feature to the live app environment, you should ask the owner of the issue to create another Jira issue for you to implement the long-term solution (the third solution).

Similarly, suppose the due date of the Jira issue is the next day. In that case, we should choose the second solution (slightly better than the first one) to ensure the feature will be distributed in time and create another Jira issue to implement the long-term solution.

On the other hand, if the time-to-market is not too close, implement only the third solution, which is the simplest and most effective solution.

{% content-ref url="processes/3.-choose-the-simplest-and-most-effective-solution.md" %}
[3.-choose-the-simplest-and-most-effective-solution.md](processes/3.-choose-the-simplest-and-most-effective-solution.md)
{% endcontent-ref %}

### 4. Write automated tests

Resuming the request to _“display a survey to PageFly users to collect their needs for the Black Friday campaign”_, regardless of which solution you choose in [step 3](example-1.md#id-3.-choose-the-simplest-and-most-effective-solution), we will need to create a stand-alone component and place it where the survey needs to show. The component will display the survey in the UI provided by the design team.

Because we already have the UI, we can create a test file that renders the component using the `mountWithApp` function and then use the `getByText` or other similar functions combined with the `toBeInTheDocument` or other similar functions to verify whether the survey and its content are displayed correctly.

{% content-ref url="processes/4.-write-automated-tests.md" %}
[4.-write-automated-tests.md](processes/4.-write-automated-tests.md)
{% endcontent-ref %}

### 5. Start coding

Suppose that the time-to-market of the request to _“display a survey to PageFly users to collect their needs for the Black Friday campaign”_ is not too close, which allows having enough time to implement the simplest and most effective solution ([the third solution](example-1.md#id-3.3.-evaluate-the-third-solution)).

First, we will declare schemas for two collections, one for saving surveys and the other for saving user responses. Because we have to pay the MongoDB cloud service for the amount of stored data, let's make the data structure as lean as possible by keeping the relationship between documents and collections straightforward and avoiding data duplication.

{% tabs %}
{% tab title="Data structure for saving surveys" %}
```typescript
import mongoose, {Document} from 'mongoose'

// Define document type.
export SurveyType = Document & {
  _id: string
  title: string
  description: string
  questions: [{
    _id: string
    type: 'text' | 'radio' | 'checkbox'
    question: string
    // Predefined answers are only required if the `type` is not 'text'.
    answers?: [{
      _id: string
      answer: string
    }]
  }]
  status: 'active' | 'inactive'
  // If both `startTime` and `endTime` are undefined, the survey will
  // always be visible until its `status` is set to 'inactive'.
  startTime?: Date
  endTime?: Date
}

// Define model schema.
const surveySchema = new mongoose.Schema({
  _id: {
    type: mongoose.Schema.Types.ObjectId,
    required: true,
    index: true,
  },
  title: {
    type: String,
    required: true,
    index: true,
  },
  description: String,
  questions: [{
    _id: {
      type: mongoose.Schema.Types.ObjectId,
      required: true,
      index: true,
    },
    type: {
      type: String,
      enum: ['text', 'radio', 'checkbox'],
      default: 'text',
      index: true,
    },
    question: {
      type: String,
      required: true,
      index: true,
    },
    // Predefined answers are only required if the `type` is not 'text'.
    answers: [{
      _id: {
        type: mongoose.Schema.Types.ObjectId,
        required: true,
        index: true,
      },
      answer: {
        type: String,
        required: true,
        index: true,
      },
    }],
    status: {
      type: String,
      enum: ['active', 'inactive'],
      default: 'inactive',
      index: true,
    },
    // If both `startTime` and `endTime` are undefined, the survey will
    // always be visible until its `status` is set to 'inactive'.
    startTime: Date,
    endTime: Date,
  }]
})

export const SurveyModel = mongoose.model<SurveyType>('Survey', surveySchema)
```
{% endtab %}

{% tab title="Data structure for saving user responses" %}
```typescript
import mongoose, {Document} from 'mongoose'

// Define document type.
export SurveyResponseType = Document & {
  _id: string
  surveyId: string
  shopDomain: string
  answers: [{
    questionId: string
    // Answer ID is only available if the question `type` is not 'text'.
    answerId?: string[]
    // Text answer is only available if the question `type` is 'text'.
    textAnswer?: string
  }]
}

// Define model schema.
const surveyResponseSchema = new mongoose.Schema({
  _id: {
    type: mongoose.Schema.Types.ObjectId,
    required: true,
    index: true,
  },
  surveyId: {
    type: mongoose.Schema.Types.ObjectId,
    required: true,
    index: true,
    ref: 'Survey',
  },
  shopDomain: {
    type: String,
    required: true,
    index: true,
    ref: 'Shop',
  },
  answers: [{
    questionId: {
      type: mongoose.Schema.Types.ObjectId,
      required: true,
      index: true,
    },
    // Answer ID is only available if the question `type` is not 'text'.
    answerId: [{
      type: mongoose.Schema.Types.ObjectId,
      required: true,
      index: true,
    }],
    // Text answer is only available if the question `type` is 'text'.
    textAnswer: String,
  }],
})

export const SurveyResponseModel = mongoose.model<SurveyResponseType>('SurveyResponse', surveyResponseSchema)
```
{% endtab %}
{% endtabs %}

{% content-ref url="processes/5.-start-coding.md" %}
[5.-start-coding.md](processes/5.-start-coding.md)
{% endcontent-ref %}
