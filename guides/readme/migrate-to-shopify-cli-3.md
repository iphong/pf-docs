---
description: Updated version currently on development branch only
---

# Migrate to Shopify CLI 3

### TLDR;

#### Step 1

Pull the latest code from `pfserver` `development` branch and run `yarn install` to install Shopify CLI libs

#### Step 2

* Install `ngrok`&#x20;
* Open terminal and run `ngrok http 3000`, **copy** the https url. It should look **like** this [https://0481-1-53-240-22.ngrok.io](https://0481-1-53-240-22.ngrok.io)

#### Step 3

Under `pfserver` root folder

Run `yarn dev-shopify --tunnel-url {YOUR_NGROK_URL}:3000` to start the backend. An example of the full command is `yarn dev-shopify --tunnel-url` [`https://0481-1-53-240-22.ngrok.io:3000`](https://0481-1-53-240-22.ngrok.io)

That's it

### Details

Shopify has leveraged their CLI to version 3 with some major changes. Notable updates are

* Shopify CLI is now a project-scoped lib which means you are no longer able to run command `shopify` any more
  * We then have to update `package.json`
* Requires configuration files: `shopify.app.toml` and `shopify.web.toml`
  * Add 2 files above with proper configurations
* Requires Shopify app to strictly follow the app structure. With dual-process app (like ours), it's compulsory that we merge both projects (`pfcore` and `pfserver`) into one
  * The ultimate purpose of this merge, as investigated, is to enable the port transfer. Shopify CLI automatically decide the port which frontend runs (like 54671 and this will randomly change, ours is 3000). They do provide the configuration for the port provided that we follow the app structure which we don't want to because this will affect our current dev flow and not recommend.
  * We have digged deeper and found 2 solutions
    * Solution 1 (Basic): Manually run ngrok
      * **Pros**: Shopify CLI natively supports this (custom tunnel url)
      * **Cons**: We need to do it every time we start the `pfcore` project. You can mitigate this by not stopping the ngrok
    * Solution 2 (Advanced): Modify the CLI code to add our port (3000)
      * **Pros**: This modification is minor, 2 lines, just an update regards the port and the updated urls. Do one time and or the time you upgrade shopify-cli
      * **Cons**: Shopify CLI does not officially support this
* It depends on your understanding level of Shopify to choose your favorite solution, I've updated the guideline following the solution 1 as I think it's easier and require less actions.

For more details, visit here [https://shopify.dev/apps/tools/cli](https://shopify.dev/apps/tools/cli/migrate)

