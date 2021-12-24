# WebSocket API

## Using WebSocket API <a href="#websocket-api" id="websocket-api"></a>

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
