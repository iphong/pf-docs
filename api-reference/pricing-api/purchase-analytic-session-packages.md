# Purchase Analytic Session Packages

![](<../../.gitbook/assets/Screen Shot 2021-11-23 at 10.32.09.jpg>)

### Function: `purchaseSessionPackage`

#### Params:&#x20;

* `amount`: number - number of session package (min: 1, max: 20)

Usage:&#x20;

Same as the Create Charge function, after execute the `purchaseSessionPackage,` it will return a JSON data including the `confirmationUrl`. Next, redirect the app to that `confirmationUrl` then let users confirm the onetime charge.



