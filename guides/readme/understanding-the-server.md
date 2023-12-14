# Understanding the server

The server app of PageFly has the following folder structure which groups source code files by purpose.

```
src
 |_ controllers
 |_ data
 |_ handlers
 |_ helpers
 |_ includes
 |_ middleware
 |_ routers
 |_ types
 |_ util
```

The `controllers` directory contains files that declare controllers for manipulating data and producing responses for all HTTP requests.

A controller function will be passed 3 arguments when called: the request object, the response object, and the next function provided by the Express app.

Depending on different purposes, a controller function should end by calling the following methods of the response object: `json`, `text`, `send`, `end`, or `redirect`.

If any error occurs while processing a request, the controller function should call the next function and pass the error object to it to let the Express app finish the request.

Below is a sample controller file.

```javascript
export function sayHello(req, res, next) {
    res.end(`Hello ${req.query.name || 'Unknown'}!`)
}
```

The `data` directory contains anything related to data including files that either define constants, declare data types, or provide methods for manipulating data.

The `handlers` directory contains files that handle integration with Shopify including authentication, authorization, and proxying Shopify Admin API and GraphQL API requests.

The `helpers` and `includes` directories contain files that provide helper functions and static data for inclusion when needed.

The `middleware` directory contains a file named `router.ts` and a folder named `hooks`. The `router.ts` file provides methods for loading handlers from the `routers` directory based on the request path for HTTP requests. The `hooks` directory contains files that declare event listeners to be executed when appropriate events are triggered by request handlers. Hooks will be loaded automatically based on the request path. For example, hooks for the request path `/api/config` will be loaded from the file `hooks/api/config.ts`.

The `routers` directory contains files that declare request handlers and will be used for path-based routings without the need to register endpoints with the Express app. Request handlers should import controllers from the `controllers` directory to process the request.

There are 2 types of request handlers: static and dynamic.

A static request handler should be used when declaring an end-point that provides data that can be retrieved without any parameter. For example, `/api/config`. To declare a static request handler, create a file in the `routers` directory with the file name the same as the request path. In the example above, the file that declares request handler(s) for the request path `/api/config` should be `routers/api/config.ts`.

Dynamic request handlers should be used when declaring an end-point that provides data that can only be retrieved with a certain parameter. For example, `/api/pages/[ID]`. To declare a dynamic request handler, create a file in the `routers` directory with the file name starting with a `[` character and ending with a `]` character. In the example above, the file that declares request handler(s) for the request path `/api/pages/[ID]` should be `routers/api/pages/[id].ts`. When a dynamic request handler is executed, it can access the parameter via the `params` property of the request object provided by the Express app. Again, in the example above, the request `[ID]` can be accessed via `req.params.id`.

A request handler file must export a default function to handle all types of request methods or must export either of the following functions to handle different types of request methods individually: `handleGet`, `handlePut`, `handlePost`, `handlePatch`, or `handleDelete`.

```javascript
// Handle all types of request method
export default function (req, res, next) {
    try {
        // If this is a dynamic request handler declared in a file named `[id].ts`,
        // then the required parameter can be accessed from `req.params.id`
        const {id} = req.params

        // Do something to get the requested data
        const data = {}

        // Send a response back to the client
        res.json(data)
    } catch (e) {
        next(e)
    }
}

```

```javascript
// Handle GET request method
export function handleGet(req, res, next) {
    try {
        // If this is a dynamic request handler declared in a file named `[id].ts`,
        // then the required parameter can be accessed from `req.params.id`
        const {id} = req.params

        // Do something to get the requested data
        const data = {}

        // Send a response back to the client
        res.json(data)
    } catch (e) {
        next(e)
    }
}

// Handle PUT request method
export function handlePut(req, res, next) {
    try {
        // If this is a dynamic request handler declared in a file named `[id].ts`,
        // then the required parameter can be accessed from `req.params.id`
        const {id} = req.params

        // Send a response back to the client
        res.json(data)
    } catch (e) {
        next(e)
    }
}

// Handle POST request method
export function handlePost(req, res, next) {
    try {
        // If this is a dynamic request handler declared in a file named `[id].ts`,
        // then the required parameter can be accessed from `req.params.id`
        const {id} = req.params

        // Do something to get the requested data
        const data = {}

        // Send a response back to the client
        res.json(data)
    } catch (e) {
        next(e)
    }
}

// Handle PATCH request method
export function handlePatch(req, res, next) {
    try {
        // If this is a dynamic request handler declared in a file named `[id].ts`,
        // then the required parameter can be accessed from `req.params.id`
        const {id} = req.params

        // Do something to get the requested data
        const data = {}

        // Send a response back to the client
        res.json(data)
    } catch (e) {
        next(e)
    }
}

// Handle DELETE request method
export function handleDelete(req, res, next) {
    try {
        // If this is a dynamic request handler declared in a file named `[id].ts`,
        // then the required parameter can be accessed from `req.params.id`
        const {id} = req.params

        // Do something to get the requested data
        const data = {}

        // Send a response back to the client
        res.json(data)
    } catch (e) {
        next(e)
    }
}

```

The `types` and the `util` directories contain files that declare variable types and common functions that can be imported to use when needed.
