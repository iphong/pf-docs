# Setup the environment

### The Frontend App

{% hint style="info" %}
Make sure you have **NodeJS** and **NPM** installed on your machine before continue

* [Click here to download NodeJS](https://nodejs.org/en/download/)
{% endhint %}

```bash
# clone this repo with SSH
# make sure you setup the SSH in bitbucket setting
git clone git@bitbucket.org:bravebits/pfcore.git

# go to cloned pfcore folder
cd pfcore

# install the dependencies
yarn install

# if you failed to install and the console is throwing permission issue, please chmod the node_modules:
sudo chmod -R 777 node_modules
# then yarn install again.

# Start the app in port 3000
yarn start
```

### The Backend Server

{% hint style="info" %}
The backend server requires **Redis** and **MongoDB** services and the **Shopify CLI** command line tool so make sure they are up and running on your local system. Read the following guide on how to set them up:
{% endhint %}

* [Install and config Redis on Mac OS X via HomeBrew](https://medium.com/@petehouston/install-and-config-redis-on-mac-os-x-via-homebrew-eb8df9a4f298)
* [Install MongoDB Community Edition on macOS](https://medium.com/@petehouston/install-and-config-redis-on-mac-os-x-via-homebrew-eb8df9a4f298)
* [Install the Shopify CLI command line tool](https://shopify.dev/apps/tools/cli/installation)

> If you are having troubles starting redis and mongodb on M1 mac
>
> ```
> /redis-server --daemonize yes
> mongod --dbpath ~/Workspace/mongo-data --fork --logpath ~/Workspace/mongo-data/log.txt
> ```

#### Clone the source codes and start the dev server

```bash
# Clone the backend project
git clone git@bitbucket.org:bravebits/pfserver.git

# go to backend source
cd pfserver

# create .env file from .env.example file
cp .env.example .env

# Remember to update all config behind that

# login to Shopify:
shopify login

# install dependencies and start
yarn && yarn shopify

# or just yarn start if you don't need to update backend code.

# now your backend project is live in http://localhost:8080
```

Update new PageFly plan into database by go to: [http://localhost:3000/api/update-pf-plan](http://localhost:3000/api/update-pf-plan)

Next, in `pfcore/config`, copy `proxySetup.example.js` to `proxySetup.js` After that update the proxy information if needed.

Now, <mark style="background-color:green;">`yarn start`</mark> in pfcore and you will get our app running in [http://localhost:3000](http://localhost:3000)

### **Use missing lang tool**

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
