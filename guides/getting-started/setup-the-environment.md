# Setup the environment

## Frontend App

{% hint style="info" %}
Make sure you have **NodeJS** and **NPM** installed on your machine before continue
{% endhint %}

{% embed url="https://nodejs.org/en/download" %}

**Clone project source code**

```bash
git clone git@bitbucket.org:bravebits/pfcore.git
```

#### Then install the dependencies

```bash
cd pfcore
yarn install
```

#### Finally start the dev server

```bash
yarn start
```

## Backend Server

{% hint style="info" %}
The backend server requires **Redis** and **MongoDB** services and the **Shopify CLI** command line tool so make sure they are up and running on your local system.
{% endhint %}

{% embed url="https://docs.docker.com/desktop/mac/install" %}

**Clone project source code**

```bash
git clone git@bitbucket.org:bravebits/pfcore.git
```

**Start mongodb and redis with docker-compose**

```bash
sudo docker compose up -d
```

**Copy the .env.example to .env**

```bash
cp .env.example .env
```

**Install the Shopify CLI and make sure it in the newest version:**

```bash
brew tap shopify/shopify
brew install shopify-cli
shopify version
```

**Update the .env file**

```bash
SHOPIFY_API_KEY=
SHOPIFY_API_SECRET=
SHOP=your-shop.myshopify.com
```

**Install the dependencies and run `yarn shopify` command.**

```bash
yarn && yarn shopify
```

**Start the pfcore:**

```bash
    yarn && yarn start
```

## Update your account

Update new PageFly plan into database by go to: [http://localhost:3000/api/seed-plan-db](http://localhost:3000/api/seed-plan-db)

Next, in `pfcore/config`, copy `proxySetup.example.js` to `proxySetup.js` After that update the proxy information if needed.

Now, <mark style="background-color:green;">`yarn start`</mark> in pfcore and you will get our app running in [http://localhost:3000](http://localhost:3000)

## **Use missing lang tool**

```
# run in terminal
yarn check-trans
# enter test case and source file/folder (optional)
# add ignore key and ignore path in folder /script/check-trans-tool
```

**Update translate key in Spreadsheet(data will save in public/languages/v3):**

```
- First, login app by go to: 'https://pf-translating.herokuapp.com/login'

- Update new translate in Spreadsheet

- Then, update new data trans : 'https://pf-translating.herokuapp.com/update-data-trans'

- Wait a second, and run 'yarn trans' in pfcore
```

#### Restore all sheet in spreadsheet: - Clone project pf-translating

```
- Run ngrok and update new uri in GCP Pagefly, BASE_URL in .env (pf-translating), uri in function updatedSpreadSheet AppScript

- Update new data json in folder Lang (pf-translating)

- Go to: 'https://pf-translating.herokuapp.com/update-spreadsheet'
```

**Enable Preview via Shopify Proxy:**

* Go to you app set up in Shopify Partner > Extensions > Online Store > Manage App Proxy
* Update your proxy like follow: https://apps.pagefly.io/api/public/preview
* Set your own custom path/subpath. Example: /a/pf\_preview
* Update your backend .env: SHOPIFY\_PROXY\_PATH=/apps/pagefly
* Save and restart the app
* Set your own custom path/subpath. Example: /a/pf\_preview
* Update your backend .env: SHOPIFY\_PROXY\_PATH=/apps/pagefly
* Save and restart the app
