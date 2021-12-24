# EventSource API

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
