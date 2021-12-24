# Create Charge

![](<../../.gitbook/assets/Screen Shot 2021-11-22 at 10.34.18.png>)

### Function: \`createCharge\`

After Select the plan and click continue, use the function `createCharge` to start creating a charge.

#### Parameters:

* `planId`: Number -  The ID of the plan, for example: `20001`
* `addOns`: Array\<AddOnName> - Array of additional Add on, for example: `['BLOG_ADDON']`
* coupon: String - The coupon code, for example: `PFXXXXXXXX`

``

#### Return data:

Sample:

```json
{
    "status": "success",
    "data": {
        "appSubscriptionCreate": {
            "appSubscription": {
                "id": "gid://shopify/AppSubscription/22090481734"
            },
            "confirmationUrl": "https://minhpt4.myshopify.com/admin/charges/1837151/22090481734/RecurringApplicationCharge/confirm_recurring_application_charge?signature=BAh7BzoHaWRsKwhGALIkBQA6EmF1dG9fYWN0aXZhdGVU--c21cba2049f8f82d657bcd570e961c9ec14d1430",
            "userErrors": []
        }
    }
}
```

After getting `confirmationUrl` from the result, redirect the app to that URL. You will be redirected to Shopify's Confirmation page.

