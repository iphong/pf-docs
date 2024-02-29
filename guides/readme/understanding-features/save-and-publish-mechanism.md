# Save and Publish Mechanism

### Frontend

#### Save mechanism

When you click the Save button on the HeaderBar, there are a bunch of things that have been done. In this case, I just introduce you to the `handleSavePage` function because ehhhhhhhh, you know, I think that is the most important part in the FrontEnd of this mechanism.

I will skip all the check conditions to focus on the main.&#x20;

<figure><img src="../../../.gitbook/assets/1.png" alt=""><figcaption><p>Find this keyword if you need to do something with it</p></figcaption></figure>

Because the function here is Save, so the parameter `publish` will be false.

<figure><img src="../../../.gitbook/assets/2.png" alt=""><figcaption><p>If the conditions above are valid, then run the function menubarSavePage.</p></figcaption></figure>

<figure><img src="../../../.gitbook/assets/3.png" alt=""><figcaption><p>3 parameters, publish or save, silent: is autoSave or manualSave, abortController</p></figcaption></figure>

menubarSavePage shows toast and UI changes, the main action in this function is `savePageData`

<figure><img src="../../../.gitbook/assets/4.png" alt=""><figcaption><p>savePageData function</p></figcaption></figure>

savePageData is a function that summarizes all general data like id, HTML, or CSS of the page/section. Then, all page data will be standardized, and prepared to send to the server. Here, we use the `prepareSaveData` function. The data contains lots of parameters, like `HTML`, `css`, `fonts`,  `elements`, `configs`, ....

<figure><img src="../../../.gitbook/assets/5.png" alt=""><figcaption><p>data is standardized and prepared to send to the server.</p></figcaption></figure>

After the preparation is completed, the next step will be to run `saveData`

<figure><img src="../../../.gitbook/assets/6.png" alt=""><figcaption><p>saveData function with its params</p></figcaption></figure>

This `saveData` is the final step on the FrontEnd side its mission is to send all summarized data to the server.

<figure><img src="../../../.gitbook/assets/7.png" alt=""><figcaption><p>Send all data to the server.</p></figcaption></figure>

#### Publish mechanism

The publish mechanism also has the same flow as the save mechanism, but it will include some conditions like slot usage check, ...

### Backend

After receiving the request from the client, the server will continue the rest of the work.

<figure><img src="../../../.gitbook/assets/8.png" alt=""><figcaption><p>function updateShopifyPage in shopify-page-mutation.ts</p></figcaption></figure>

####

&#x20;The server will receive the data from the request and validate all of them

<figure><img src="../../../.gitbook/assets/9.png" alt=""><figcaption><p>validate data input</p></figcaption></figure>

After confirming that all the data are valid, if the page has been published before and the page type has been changed, the server will send a request to Shopify to remove that page from the theme.

<figure><img src="../../../.gitbook/assets/10.png" alt=""><figcaption><p>remove the current page and clean all data on that page</p></figcaption></figure>

After the delete process is complete, the server will continue to create a new page with the validated data above, and send it to the Shopify theme to store. For each page type, there is a specific function to publish. For more details, please check the function `handleShopifyPage`

<figure><img src="../../../.gitbook/assets/12.png" alt=""><figcaption><p>function handleShopifyPage to create a page on the Shopify theme</p></figcaption></figure>

After being published successfully, we store the page data in our database.

<figure><img src="../../../.gitbook/assets/11.png" alt=""><figcaption><p>store page data to our database </p></figcaption></figure>

If the type is section, update that section to the Shopify Theme

<figure><img src="../../../.gitbook/assets/13.png" alt=""><figcaption><p>Update PageFly section list on the Shopify theme</p></figcaption></figure>

That's it. All the information I gave you above is the whole of Save and Publish Mechanism. If you have any consider, please don't hesitate to ask and discuss together. Thank you.
