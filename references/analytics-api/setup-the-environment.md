# Setup the environment

After following the instruction in Getting Started / Setup the environment article, follow the steps below for running pf-analytic-server project

* Update .env file in pfserver project:

```
HOST=[ngrok link]
PF_ANALYTICS_SERVER=[ngrok link]/api/analytics-server
PAGEFLY_SECRET=[secret key]
```

Run <mark style="color:red;">yarn && yarn shopify</mark>

* update .env file in pf-analytic-server project:

```
PF_SERVER_URL=http://localhost:8080
PAGEFLY_SECRET=[secret key]
```

Run <mark style="color:red;">yarn && yarn watch</mark>
