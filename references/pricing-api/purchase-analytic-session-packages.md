# Purchase Analytic Session Packages

![](<../../.gitbook/assets/Screen Shot 2021-11-23 at 10.32.09.jpg>)

### Function: `purchaseSessionPackage`

#### Params:&#x20;

* `amount`: number - number of session package (min: 1, max: 20)

Usage:&#x20;

Same as the Create Charge function, after executing the `purchaseSessionPackage` function, it will return JSON data including the `confirmationUrl`. Next, redirect the app to that `confirmationUrl` then let users confirm the one-time charge.

After confirming the charge, you will see the data like this in `globalConfig.license`

![](<../../.gitbook/assets/Screen Shot 2022-01-24 at 11.11.26.png>)





### Function `getAnalyticMonthToDateUsage`&#x20;

Get the amount of session usage for this month.
