# Test-driven development (TDD)

### Introduction

I tended to write a detailed introduction about test-driven development (TDD) methodology. However, after googling "test-driven development" I see about 664,000,000 results. So, writing a new introduction about it is unnecessary.

Let me shorten it for you by an image and a short description.

<figure><img src="../.gitbook/assets/card.png" alt=""><figcaption><p>Credited by <a href="https://martinfowler.com/bliki/TestDrivenDevelopment.html">martinfowler.com</a></p></figcaption></figure>

{% hint style="info" %}
Test-driven development (TDD) focuses on an iterative development cycle where the emphasis is placed on writing test cases before the actual feature or function is written.

TDD usually follows the "Red-Green-Refactor" cycle:

1. Add a test to the test suite
2. <mark style="color:red;">**Red**</mark>: Run all the tests to ensure the new test fails
3. <mark style="color:green;">**Green**</mark>: Write just enough code to get that single test to pass
4. Run all tests
5. <mark style="color:orange;">**Refactor**</mark>: Improve the initial code while keeping the tests green
6. Repeat
{% endhint %}

### Test-driven development cycle

The following sequence is based on the book [_Test-Driven Development by Example_](https://www.google.com.vn/books/edition/Test\_Driven\_Development/zNnPEAAAQBAJ).

1.  **Create a list of test cases:**

    This initial step is to list all the expected variants in the requirements, such as “There’s the basic case & then what if this service times out & what if the key isn’t in the database yet &…”. You can discover these specifications by asking about use cases and user stories. A key benefit of test-driven development is that it makes the developer focus on requirements _before_ writing code.
2.  **Add one test from the list:**

    Write an automated test that passes if the variant in the requirements is met.
3.  **Run all tests, the new test **_**should fail**_** for the expected reasons:**

    This shows that new code is needed for the desired function or feature. It validates that the test harness is working correctly. It rules out the possibility that the new test is flawed and will always pass.
4.  **Write the simplest code that passes the new test:**

    Inelegant or hard code is acceptable as long as it passes the test. The code will be honed anyway in step 6. No code should be added beyond the tested functionality.
5.  **All tests should now pass:**

    If any fail, the new code must be revised until they pass. This ensures the new code meets the test requirements and does not break existing functions or features.
6.  **Refactor to standards, testing after each refactor to ensure functionality is preserved:**

    The code is refactored for readability and maintainability. In particular, hard-coded test data should be removed. Running the test suite after each refactor helps ensure that no existing functionality is broken.

    * Examples of refactoring:
      * Moving code to where it most logically belongs.
      * Removing duplicate code.
      * Making names self-documenting.
      * Splitting methods into smaller pieces.
      * Re-arranging inheritance hierarchies.
7. **Add the next test on the list:**\
   Repeat steps from 2 to 6 for each test on the list of test cases until all tests are implemented and passed.

The cycle above is repeated for each new piece of functionality. Tests should be small and incremental, and code should be committed often. Doing that, if new code fails some tests, you can undo or revert rather than debug excessively.

### Best practices

In [an article](https://www.browserstack.com/guide/what-is-test-driven-development) published on the BrowserStack website, Jash Unadkat recommends the following best practices when applying TDD.

1. **Start with a clear understanding of the requirements:**\
   Begin by understanding the requirements or specifications of the feature you are developing. This will help you write focused and relevant tests.
2. **Write atomic tests:**\
   Each test should focus on a specific behavior or functionality. Keep your tests small and focused, addressing a single aspect of the code. This improves test readability, and maintainability, and allows for easier debugging.
3. **Write the simplest test case first:**\
   Begin by writing the simplest possible test case that will fail. This helps you focus on the immediate task and avoids overwhelming yourself with complex scenarios upfront.
4. **Write tests for edge cases:**\
   Consider boundary conditions and edge cases when designing your tests. They are inputs or scenarios that lie at the extremes of the input domain and often reveal potential bugs or unexpected behavior.
5. **Refactor regularly:**\
   After a test passes, take time to refactor the code and improve its design without changing its behavior. This helps maintain clean and maintainable code as the project progresses.
6. **Maintain a fast feedback loop:**\
   Your test suite should execute quickly so that you can receive immediate feedback on the health of your code. Fast feedback allows for faster development iterations and catches issues early on.
7. **Automate your tests:**\
   Utilize test automation frameworks and tools to automate the execution of your tests. This enables you to run tests frequently and ensure consistent and reliable test results.
8. **Follow the Red-Green-Refactor cycle:**\
   Commit to the core TDD cycle of writing a failing test (**Red**), implementing the minimum code to pass the test (**Green**), and then refactoring the code to improve its design (**Refactor**). Repeat this cycle for each new function, behavior, or feature.
9. **Maintain a comprehensive test suite:**\
   Aim to achieve a good balance between unit tests, integration tests, and acceptance tests. Each test type serves a different purpose and provides different confidence levels of the code.
10. **Continuously run tests:**\
    Integrate your test suite with your development environment and set up continuous integration (CI) pipelines to automatically execute tests whenever code changes are made. This ensures that tests are run consistently and helps catch regressions early.
11. **Test failures should guide development:**\
    When a test fails, it should guide your development efforts. Analyze the failure, identify the cause, and fix the code to address the issue. Test failures are valuable feedback for improving code quality.

Delivering quality products requires debugging and optimization in the development process. When incorporated correctly, the TDD approach provides numerous benefits, particularly in bringing cost-efficiency in the long run and delivering true value to businesses.

### Set things up

Currently, the `pfserver` project is not fully settled for automated tests. Thus, we will do the necessary setup to make the `pfserver` project fully testable.

First, we need to install some modules to support automated tests. Open the terminal and run the following command.

```sh
npm i jest supertest cross-env --save-dev
```

The config file for the `jest` module has already been created for some unit tests before but needs to be updated as follows.

<details>

<summary>[pfserver] jest.config.js</summary>

```javascript
// ...
-  testEnvironment: 'jsdom',
+  testEnvironment: 'node',
// ...
```

</details>

Because the `pfserver` project requires a connection to MongoDB for querying and storing data, we need to test it on another database to prevent damaging the official database. Let's open the file `.env` and add the following directive to it.

```
MONGODB_URI_FOR_AUTOMATED_TESTS=mongodb://localhost:27017/test
```

Additionally, the PageFly server requires authentication when requesting its API endpoints. Hence, we need to update the function `validateShopAPI` to disable the authorization process when the server runs in the `test` environment.

<details>

<summary>[pfserver] src/helpers/middleware.ts</summary>

```typescript
// ...
export async function validateShopAPI(req, res, next?): Promise<void> {
+  // Support automated testing API endpoints.
+  if (process.env.NODE_ENV === 'test') {
+    req.session.shop = req.query.shop || req.body.shop
+
+    return next && next()
+  }
// ...
```

</details>

Finally, we need to update some files that initialize the server to skip some tasks when the server runs in the `test` environment.

<details>

<summary>[pfserver] src/server.ts</summary>

```typescript
// ...
  async connectMongoose(): Promise<string> {
-    for (const uri of MONGODB_URI_ARR) {
+    const mongoServers =
+      process.env.NODE_ENV === 'test' ? [process.env.MONGODB_URI_FOR_AUTOMATED_TESTS] : MONGODB_URI_ARR
+
+    for (const uri of mongoServers) {
      if (!this.mongoConnected) {
// ...
+      if (process.env.NODE_ENV === 'test') {
+        return
+      }
+
      mongoose.connection.on('error', e => {
// ...
  async runApp() {
+    // Do not run Express server in the `test` environment.
+    // We will use the `supertest` module to emulate a server.
+    if (NODE_ENV === 'test') {
+      return
+    }
+
    // Remove `X-Powered-By: Express` response header.
// ...
-new PageFlyServer()
+if (process.env.NODE_ENV !== 'test') {
+  new PageFlyServer()
+}
+
+// We need to export the initialization class to make the pfserver project testable.
+export {PageFlyServer}
```

</details>

<details>

<summary>[pfserver] src/handlers/shopify.ts</summary>

```typescript
// ...
-    this.initShopifyContext()
+    if (process.env.NODE_ENV !== 'test') {
+      this.initShopifyContext()
+    }
// ...
```

</details>

<details>

<summary>[pfserver] src/helpers/fns.ts</summary>

```typescript
// ...
-        html = fs.readFileSync(publicPath + '/index.html').toString()
+        try {
+          html = fs.readFileSync(publicPath + '/index.html').toString()
+        } catch (e) {
+          html = ''
+        }
// ...
```

</details>

The `pfserver` project is fully settled for automated tests now. Open the terminal and run the following command to start an automated test session.

```sh
yarn cross-env NODE_ENV=test jest --testTimeout=5000 --watchAll --detectOpenHandles
```

Let's create a new test file to verify if the automated test session works as expected.

<details>

<summary>[pfserver] src/__<strong>tests__</strong>/routers/api/page.test.ts</summary>

```typescript
import 'dotenv/config'
import request from 'supertest'
import mongoose from 'mongoose'
import {randomUUID} from 'crypto'
import {PageFlyServer} from '../../../server'
import ShopifyPage from '../../../data/models/ShopifyPage'
import PageFlyShopifyHandler from '../../../handlers/shopify'

describe('Test the server endpoint /api/page/[id]', () => {
  let server, handler, agent

  beforeAll(async () => {
    // Connect Mongoose to MongoDB.
    await mongoose.connect(process.env.MONGODB_URI_FOR_AUTOMATED_TESTS, { keepAlive: true })

    // Fake some environment variables.
    process.env.CATALOG_DATA_IMPORTED = 'yes'

    // Init PageFly server.
    server = new PageFlyServer()
    handler = new PageFlyShopifyHandler(server.app, null)

    handler.initRouting()

    // Init an agent for testing.
    agent = request.agent(server.app)
  })

  afterAll(async () => {
    // Clear mock data.
    await ShopifyPage.deleteMany({})

    // Disconnect from MongoDB.
    await mongoose.connection.close()
  })

  it('Should return correct page data for the specified page ID', async () => {
    // Create a page in the database for testing.
    const page = await ShopifyPage.create({
      _id: randomUUID(),
      title: 'Test page 1',
      shopDomain: 'cuongnm-dev-store.myshopify.com',
    })

    // Send a GET request to the API endpoint.
    const res = await agent.get(`/api/page/${page._id}?shop=cuongnm-dev-store.myshopify.com`)

    expect(res.body._id).toBe(page._id)
    expect(res.body.shopDomain).toBe('cuongnm-dev-store.myshopify.com')
  })
})
```

</details>

Now, you can save the file and switch to the terminal where you started the automated test session to see how it works yourself.

### References

* [Performing NodeJS Unit testing using Jest](https://www.browserstack.com/guide/unit-testing-for-nodejs-using-jest)
* [Watch and rerun Jest JS tests](https://stackoverflow.com/questions/25472665/watch-and-rerun-jest-js-tests)
* [How to Test Your Express.js and Mongoose Apps with Jest and SuperTest](https://www.freecodecamp.org/news/how-to-test-in-express-and-mongoose-apps/)
