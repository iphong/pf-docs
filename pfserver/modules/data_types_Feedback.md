[PF Server](../README.md) / data/types/Feedback

# Module: data/types/Feedback

## Table of contents

### Variables

- [FeedbackType](data_types_Feedback.md#feedbacktype)

## Variables

### FeedbackType

• **FeedbackType**: ``"\n\ttype Feedback {\n\t\t_id: ID\n\t\tshopDomain: String\n\t\ttype: String\n\t\tstatus: String\n\t\tcreatedAt: Date\n\t\tupdatedAt: Date\n\t\tdescription: String\n\t\tcontent: String\n\t}\n\t\n\tinput FeedbackInput {\n\t\tshopDomain: String\n\t\ttype: String\n\t\tstatus: String\n\t\tcreatedAt: Date\n\t\tupdatedAt: Date\n\t\tdescription: String\n\t\tcontent: String\n\t}\n\n\textend type Mutation {\n\t    addFeedback(feedbackInput: FeedbackInput!): Feedback\n\t}\n\textend type Query {\n\t    getFeedbackByShop(shopDomain: String): [Feedback]\n\t}\n"``

#### Defined in

[src/data/types/Feedback.ts:1](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/types/Feedback.ts#lines-1)
