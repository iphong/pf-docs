# Core API

From any node.js modules imported in our current pfserver application. Add these to existing code. &#x20;

```javascript
import events from 'handlers/events'

// LISTEN TO REALTIME EVENTS
events.on('page_publish', (shop, page_id) => {
    // Do something when a page is published
})
events.on('page_change', (shop, page_id) => {
    // Do something when a page is edited
})
events.on('some_custom_event', (shop, page_id) => {
    // Do something when custom event is triggerd
})

// BROADCAST EVENTS
events.send('iphong.myshopify.com', 'some_custom_event', { foo: 'bar' })

```
