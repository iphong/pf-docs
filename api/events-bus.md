# Events Bus

## Core Concept

&#x20;Allow services to communicate with each other using events and actions via simple messages.

## &#x20;Intergrations

```javascript
import events from 'handlers/events'

events.on('page_publish', (shop, page_id) => {
    // Do something when a page is published
})

events.on('page_change', (shop, page_id) => {
    // Do something when a page is edited
})

events.on('shop_config', (shop, page_id) => {
    // Do something when shop settings changed
})
```
