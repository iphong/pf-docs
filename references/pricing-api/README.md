# Pricing API

## Migrating from the old API

The old pricing model contains four main plans: Free, Silver, Gold, Platinum. Since the new pricing model is entirely different, we need to do version checking and migration when users switch to the new pricing model.

#### Seed the new pricing plan to database:

Go to `https://your-app-url.ngrok.io/api/seed-plan-db`

#### Check whether users are using the old pricing plan or not:

The function should be:

```tsx
let isOldPricing = ['pro', 'premuim', 'silver', 'gold', 'platinum'].includes(globalConfig.license
```

## API References

{% content-ref url="get-list-plan.md" %}
[get-list-plan.md](get-list-plan.md)
{% endcontent-ref %}

{% content-ref url="get-list-add-ons.md" %}
[get-list-add-ons.md](get-list-add-ons.md)
{% endcontent-ref %}

{% content-ref url="create-charge.md" %}
[create-charge.md](create-charge.md)
{% endcontent-ref %}

{% content-ref url="calculate-analytic-usage.md" %}
[calculate-analytic-usage.md](calculate-analytic-usage.md)
{% endcontent-ref %}

{% content-ref url="purchase-analytic-session-packages.md" %}
[purchase-analytic-session-packages.md](purchase-analytic-session-packages.md)
{% endcontent-ref %}
