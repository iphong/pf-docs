# Events Bus

## Core Concept

&#x20;Allow services to communicate with each other using events and actions via simple messages.

## &#x20;Intergrations

### Using pfserver core API

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

### Using EventSource API

Subscribe to events from any javascript clients such as browsers, service workers and mobile apps.

```javascript
const events = new EventSource(`https://apps.pagefly.com/events?shop=iphong.myshopify.com`);

// LISTEN TO REALTIME EVENTS
events.addEventListener('page_change', (e: { data: page_id }) => {
    // Do something when the page data is changed
})
events.addEventListener('some_custom_event', (e: { data: message }) => {
    // Do something when custom event is triggerd
})
```

{% embed url="https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events/Using_server-sent_events" %}
Click here to learn more about Server-Sent-Events (SSE)
{% endembed %}

### Using WebSocket API

From any applications and services running remotely written in any programing language that has  network layer access to TCP/IP protocol.

```javascript
const ws = new WebSocket(`ws://apps.pagefly.io/events?shop=iphong.myshopify.com`)

// LISTEN TO REALTIME EVENTS
ws.addEventListener('message', ({ event, data }) => {
    switch (event) {
        case 'page_change':
            // Do something when the page data is changed
            break
        case 'some_custom_event':
            // Do something when custom event is triggerd
            break
    }
})

// BROADCAST EVENTS
events.send('iphong.myshopify.com', 'some_custom_event', { foo: 'bar' })

```

{% embed url="https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API/Writing_WebSocket_client_applications" %}
Click here to learn more about writing applications using websocket
{% endembed %}

```
// Some code
```
