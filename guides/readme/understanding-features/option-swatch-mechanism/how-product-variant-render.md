---
cover: >-
  https://studio.uxpincdn.com/studio/wp-content/uploads/2023/03/reactjs-websites.png.webp
coverY: 0
---

# How Product variant render?

### Editor

* With Combined options turned off, render the default option swatch with 2 types: dropdown menu and radio buttons.
* With Combined options turned on, render the option swatch configured on the Extra functions screen.

### Live view

First, let's discuss the server-side setup. In the `saveAll` function, we make an API call to Shopify to store metafield values related to swatch options, using the key `pfVariantSwatchesV2`. When rendering the live view, we utilize the Liquid object API to fetch data from the metafield with that key. Subsequently, we render the styles for each pre-configured swatch option based on the retrieved data.

![](<../../../../.gitbook/assets/image (5).png>)![](<../../../../.gitbook/assets/image (6).png>)



