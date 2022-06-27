---
description: >-
  We embed puppeteer so if you have familiar with it, this should not take you
  long to get started.
---

# Add an automation test

### General notes

The configuration is minimal and the starting procedure is somewhat easy to follow. However, you do need to carry these notes while writing automation tests

* Import and export is pure, you need to `modules.export` and `const abc = require`
* Puppeteer built-in `page.mouse.dragAndDrop` does not work, we have reimplemented this function and geared it with a more powerful capability - selectors.&#x20;
* Automation test will actually move your mouse cursor so do not use it

### Getting started

#### Step 0, Prerequisites

* Close Chrome and start the debug mode by running this in terminal app
  * `/Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --remote-debugging-port=9222`&#x20;
  * `get the ws id and replace the value below`&#x20;
  * `const wsChromeEndpointUrl = 'ws://127.0.0.1:9222/devtools/browser/72466de8-3e60-4500-924b-487158db1d77'`
* Start `pfserver` and `pfcore`
* Create the file namely format like `your-test-name.test.js` inside the `/instrumental` folder
* This must be `js` file because it's not transpiled by babel and webpack. It's shipped with pure JS

#### Step 1, Setting things up

* Add a test as usual with `it` or `test`

```
it('A simple test that ensure the app is running', () => {})
```

* The mouse moving function has a fixed variable between the puppeteer mouse and the actual mouse
* The viewport is standard and needed to be exactly the same

```
  const browser = await puppeteer.connect({
      browserWSEndpoint: wsChromeEndpointUrl,
      defaultViewport: null,
      slowMo: 300,
  });
  const page = await browser.newPage()

  // Installs the helper to the page. Mouse will be visible in the subsequent navigation.
  await installMouseHelper(page)
  page.setViewport({
    width: 1366,
    height: 768,
  })
```

#### Step 2, visit the page

```
await page.goto(
    'https://wip.pagefly.io/editor?id=8af35425-007f-4968-b9b5-0d316eb2a782',
    {waitUntil: 'load', timeout: 0}
  )
```

#### Step 3, perform life-like actions

```
  await page.waitForSelector('[data-testid="basic-element-catalog"]')
  await page.click('[data-testid="basic-element-catalog"]')
  await page.waitForSelector('[id$="Layout-popup"] [data-testid="catalog-item-1"]')
  await dragAndDropWithSelector(page,'[id$="Layout-popup"] [data-testid="catalog-item-1"]', '--iframe-- #editor-dnd-wrapper')
  await page.click('[data-testid="basic-element-catalog"]')
  await page.waitForSelector('[data-testid="submenu-Heading"]')
  await page.click('[data-testid="submenu-Heading"]')
  await page.waitForSelector('[id$="Heading-popup"] [data-testid="catalog-item-1"]')
  await dragAndDropWithSelector(page,'[id$="Heading-popup"] [data-testid="catalog-item-1"]', '--iframe-- .pf-4_')
  await dragAndDropWithSelector(page, '--iframe-- [data-pf-type="Heading"]', '--iframe-- [data-pf-type="Column"]')
```

* `dragAndDropWithSelector` will move the queried element to the targeted queried position
* If you query inside an iframe, there will be more steps needed but we have done it for you, just add `--iframe--` anywhere inside the query selector string
* For example, if you drag and drop from the catalog, the first query will not have `--iframe--` but the second selector will need it as we drag it into an iframe. Btw, if you move an element inside the iframe, both selector must include `--iframe--`&#x20;

#### Step 4, assertion

```
const result = await page.evaluate(
    () => {
      return document
      .querySelector('iframe')
      .contentDocument.querySelector('[data-pf-type="Column"]')
      .innerHTML.indexOf('This is your heading text.') >= 0
    }   
  )
  expect(result).toBe(true)
```

You query DOM inside the page and return the result through `page.evaluate`&#x20;

#### Step 5, one last step

Run `yarn uitest` to execute your code

\---

And that's it, you may have a look at the file `basic-dnd.test.js`

Demo [here](https://www.loom.com/share/2190d8a85bde4f3286a95372934a9c20)
