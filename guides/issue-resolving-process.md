---
description: >-
  Below is a step-by-step guideline I suggest developers follow when resolving
  an issue.
---

# Issue-resolving process

The procedure has two parts: researching (steps 1 to 3) and coding (steps 4 to 6). At the end of the first part, developers need to submit [this Google form](https://docs.google.com/forms/d/e/1FAIpQLSc8IcTnfy\_6Y92hScpEwUMpfWXQengWYQtxPXiXPbmStBWilw/viewform) that states the result of the first three steps before continuing to the second part.

## 1. Understanding the issue first

Some developers start coding as soon as they receive an issue. This behavior might lead to misunderstanding the problem and less effective solutions.

It will be better if developers step back to see an overview of the problem first. Then, look closer to find out details from different points of view. If anything is not clear, developers need to clarify it with stakeholders.

There are different ways to understand a problem. However, to form a complete understanding of a problem, splitting the problem into several pieces is a good way to follow.

The process of understanding a problem can be split into four steps: _**define the problem**_, _**analyze the problem**_, _**frame the problem**_, and _**evaluate the problem**_.

The [5W + H method](https://www.google.com/search?q=5W%2BH+method) (who, what, when, where, why, and how) can help _**define the problem**_ clearly and precisely and avoid confusion, ambiguity, and irrelevant information.

Analyzing the problem and identifying its root causes will help you understand why the problem exists and what factors contribute to it. To _**analyze the problem**_, you can use [the 5 Whys method](https://www.google.com/search?q=5+Whys+method).

Focusing on the most relevant and important aspects of the problem and avoiding distractions and biases by framing the problem and defining its scope and boundaries. Making the problem statement specific, measurable, achievable, relevant, and time-bound ([the SMART method](https://www.google.com/search?q=the+SMART+method)) can help _**frame the problem**_.

The final step is evaluating the problem and assessing its complexity and feasibility. You need to determine how challenging the problem is and how realistic your expectations are. To _**evaluate the problem**_, you can use [the ICE method](https://www.google.com/search?q=the+ice+method): rate the problem according to its impact, confidence, and ease.

When an issue for implementing a new feature is assigned to a developer, usually, that issue is already researched thoroughly by the design team. So, understanding the issue is much easier. Most of the time, understanding the issue is understanding the designed UI, interactions, and individual use cases.

Issues for fixing bugs are vice versa. When fixing a bug, developers should use the four steps stated above to find the root cause to be able to fix the bug thoroughly.

## 2. Find at least 2 solutions

After understanding the problem, some developers start coding the very first idea flashing in their minds. Most of the time, it’s not the best solution.

Developers should find as many solutions as possible before writing the first line of code. If the time is limited, try to find at least two solutions.

Regarding finding solutions, usually, people make decisions based on facts. This way is called convergent thinking which involves finding one solution that is usually based on logic and linear thinking.

In the opposite of convergent thinking, by looking at a situation from a unique perspective we may experience a “light-bulb” moment that inspires a unique solution. This can lead to a simple fix to a simple problem like using a coin to tighten a screw. This way is called _**divergent thinking**_.

<figure><img src="https://lh7-us.googleusercontent.com/lW7qNkcsTlrzQTfypcdKbyelQV9-cknHHTLdNu7WTaB97eLiRqQ-3D5bFIbzljUZHES7jcEWAGgHb6uoDwDDfJMwGYRl4vrbdkqOkvZyP8ZWXPei9hT0fnJhb0EwzdRnkaFTrOLaeBjV8-JL1YpEXbw" alt=""><figcaption><p>Divergent Vs Convergent Thinking (<a href="https://helpfulprofessor.com/divergent-thinking-examples/">15 Divergent Thinking Examples</a>)</p></figcaption></figure>

Look at the image above, the concept of divergent thinking is to ask questions first and then find ideas to solve the questions. Brainstorming is a group activity designed to generate multiple ideas regarding a specific problem. It’s divergent thinking as a group, which helps unlock even more possibilities.

## 3. Choose the simplest solution

In software development, a simple solution can save a lot of coding, understanding, and debugging hours. Not only for the developer who implements it but also for another developer who maintains it later.

When developing a new feature, I would suggest the simplest solution is a solution that is independent, reusable, and does not affect other functionalities of the application.

When fixing a bug, the simplest solution must ensure a thorough fix without creating unnecessary new structures or mechanisms and not generating similar new code in different places.

Remember the image that compares divergent thinking with convergent thinking included in step 3. Now it’s time to use _**convergent thinking**_. Use facts such as simplicity, modularity, reusable, and “do no harm” to make the final decision.

If you see more than one simple solution, estimate the total number of lines of code. A solution that requires fewer lines of code is the better solution.

If you cannot make a final decision, don't be afraid to discuss it with your teammates for more points of view. Remember that you're not alone!

## 4. Write automated tests

At this step, developers need to write automated tests for every case that might occur. Sure, the test will fail immediately because the code is not written yet. The purpose of test-driven development is to write code to pass each designed test case until all is done.

When resolving an issue for implementing a new feature, normally, the feature already has UI, common interactions, and individual use cases. In this circumstance, you can write tests for visible things (UI, interactions, special use cases, etc.) first. After that, let's write skeletons for classes, functions, variables, etc. that need to be created then write unit tests for them before adding detailed code.

Fixing bugs is different, writing automated tests is only needed if not already exist or missing the cases that cause bugs to occur.

Fail soon, fix soon, no bugs slip out. So, smile when it fails!

## 5. Start coding

**Important**: Make sure you setup your branch properly by following this [guideline](https://app.gitbook.com/o/-LALY4wpRdbiKWEAUz1H/s/4dRlrcbGMohh9Je45HcP/\~/changes/100/guides/resolving-issues-guidelines/create-your-first-good-pull-request)

It's time to feel free to write code. However, don't rely on automatic formatting. Instead, write each line of code yourself that complies with the coding standards. It shows your seriousness. When you are serious, bugs are more likely to be seen as soon as you write code. The [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript) is a good coding standard to follow.

When coding your solution, it is important to pay attention to the three aspects _**Separation of concerns (SoC)**_, _**Keep it simple, stupid (KISS)**_, and _**Don’t Repeat Yourself (DRY)**_ as described below.

_**Separation of concerns (SoC)**_ is a concept that each component or module should be _**independent**_ and responsible for a single part of the functionality. It does not mean you need one component or module for each function. The intention is to ensure that you don’t have universal objects that do everything and, hence, are sensitive to change.

Let's take a simple webpage as an example:

```html
<!DOCTYPE html>
<html>
   <head>
       <style>
           body {background-color: gray;}
           h1 {color: blue;}
           p {color: red;}
       </style>
   </head>
   <body>
       <h1>This is a heading</h1>
       <p>This is a paragraph.</p>
   </body>
   <script>
       console.log("hello world")
   </script>
</html>
```

This is a perfectly working page, but the issue is that if we ever want to add more stuff to our webpage then things would get messy, mainly because our structure, style, and logic layers are close together. A better approach would look like this:

```html
<!-- index.html -->
<!DOCTYPE html>
<html>
   <head>
       <link rel="stylesheet" href="styles.css">
   </head>
   <body>
       <h1>This is a heading</h1>
       <p>This is a paragraph.</p>
   </body>
   <script src="logic.js"></script>
</html>
```

```javascript
// logic.js
console.log("hello world")
```

```css
/* styles.css */
body {background-color: gray;}
h1 {color: blue;}
p {color: red;}
```

Our code is much cleaner now as we separated them into three files for different layers. This is a really simple example but it can be applied on a bigger scale.

Below is another simple example of applying the separation of concerns concept. The object is a source code file of the PageFly app.

{% tabs %}
{% tab title="Don't" %}
```javascript
/**
* File: api/client.ts
*/

// Import necessary constants, types, functions, etc.

const client = apolloClientWithSessionToken('/api/graphql')

export async function updatePageFlyMeta(pageflyMeta = {}) {
 // Code that updates PageFly metadata for a shop.
}

export function updatePageConfig(id: string, configs: any): Promise<any> {
 // Code that updates configuration for a page.
}

export function duplicatePageById(id: string): Promise<any> {
 // Code that duplicates the specified page.
}

export async function saveData(
 data: IPageData = { _id: globalConfig.id },
 publish = false,
 imported: boolean = false,
 abortController?: AbortController
) {
 // Code that saves data for a page.
}

export function deletePage(id: any): Promise<any> {
 // Code that deletes a page.
}

export function saveShopFavoriteFonts(favoriteFonts) {
 // Code that saves the favorite Google fonts for a shop.
}

export function saveShopFavoriteCustomFonts(favoriteCustomFonts) {
 // Code that saves the favorite custom fonts for a shop.
}
```
{% endtab %}

{% tab title="Do" %}
```javascript
/**
* File: api/client.ts
*/

// Import necessary constants, types, functions, etc.

export const client = apolloClientWithSessionToken('/api/graphql')

// -------------------------------------------------------------------- //

/**
* File: api/shop.ts
*/

// Import necessary constants, types, functions, etc.
import { client } from '/path/to/api/client'

export async function updateShopPageFlyMeta(pageflyMeta = {}) {
 // Code that updates PageFly metadata for a shop.
}

export function saveShopFavoriteFonts(favoriteFonts) {
 // Code that saves the favorite Google fonts for a shop.
}

export function saveShopFavoriteCustomFonts(favoriteCustomFonts) {
 // Code that saves the favorite custom fonts for a shop.
}

// -------------------------------------------------------------------- //

/**
* File: api/page.ts
*/

// Import necessary constants, types, functions, etc.
import { client } from '/path/to/api/client'

export async function savePageData(
 data: IPageData = { _id: globalConfig.id },
 publish = false,
 imported: boolean = false,
 abortController?: AbortController
) {
 // Code that saves data for a page.
}

export function updatePageConfig(id: string, configs: any): Promise<any> {
 // Code that updates configuration for a page.
}

export function duplicatePageById(id: string): Promise<any> {
 // Code that duplicates the specified page.
}

export function deletePage(id: any): Promise<any> {
 // Code that deletes a page.
}
```
{% endtab %}
{% endtabs %}

For more details about the separation of concerns concept, I recommend you read the following articles: [Separation of Concerns The Simple Way](https://dev.to/tamerlang/separation-of-concerns-the-simple-way-4jp2), [Separation of Concerns in Node.js](https://www.infoq.com/articles/separation-concerns-nodejs/)

_**Keep it simple, stupid (KISS)**_ is a design principle that states that designs or systems should be as _**simple**_ as possible. Simplicity guarantees acceptance and usability. Simplicity also prevents unwanted side effects or potential bugs.

Developers should write code as simply as possible. A line of code using nested ternaries or more than two operators, conditions, or function calls becomes complex. It should be split into multiple lines of code.

{% tabs %}
{% tab title="Don't" %}
```javascript
const listOptionsIcon = !filters.includes('recently used')
   ? filteredByCategories
   : [recentlyUsedIcons, ...filteredByCategories]
```
{% endtab %}

{% tab title="Do" %}
```javascript
// Do not use the logical not operator when not necessary to avoid adding
 // one more layer of thinking. This will help code more readable and avoid
 // confusion.
 const listOptionsIcon = filters.includes('recently used')
   ? [recentlyUsedIcons, ...filteredByCategories]
   : filteredByCategories
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Don't" %}
```javascript
export async function countPublishedPage(options) {
 try {
   return (
     (
       await ShopifyPage.aggregate([
         /* Pipeline stages for querying a list of published pages */
         { $count: 'total' },
       ])
     )[0]?.total || 0
   )
 } catch (e) {
   console.error('Failed to count published pages.', e)
 }
}
```
{% endtab %}

{% tab title="Do" %}
```javascript
export async function countPublishedPage(options) {
 let result = 0

 // Avoid using the combination of multiple unrelated operations.
 try {
   // Count the number of published pages.
   result = await ShopifyPage.aggregate([
     /* Pipeline stages for querying a list of published pages */
     { $count: 'total' },
   ])

   if (result.length > 0) {
     result = result[0].total
   }
 } catch (e) {
   console.error('Failed to count published pages.', e)
 }

 return result
}
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Don't" %}
```javascript
export const cleanupData = async (req: any, res) => {
 /* Code that initiates cleanedPages and cleanedRevision variables */

 res.json({
   cleanedPages: cleanedPages.map(p => {
     return {
       id: p._id,
       title: p.title,
       shopDomain: p.shopDomain,
       deletedAt: p.deletedAt,
     }
   }),
   cleanedRevision:
     cleanedRevision &&
     cleanedRevision.map(p => {
       return {
         id: p._id,
         pageId: p.pageId,
         shopDomain: p.shopDomain,
         createdAt: p.createdAt,
       }
     }),
 })
}
```
{% endtab %}

{% tab title="Do" %}
```javascript
export const cleanupData = async (req: Request, res: Response) => {
 /* Code that initiates cleanedPages and cleanedRevision variables */

 // Refine the list of outdated pages to keep only needed properties.
 cleanedPages = cleanedPages.map(p => ({
   id: p._id,
   title: p.title,
   shopDomain: p.shopDomain,
   deletedAt: p.deletedAt,
 }))

 // Refine the list of deleted page revisions to keep only needed properties.
 if (cleanedRevision) {
   cleanedRevision = cleanedRevision.map(p => ({
     id: p._id,
     pageId: p.pageId,
     shopDomain: p.shopDomain,
     createdAt: p.createdAt,
   }))
 }

 // Send a response to the client.
 res.json({
   cleanedPages,
   cleanedRevision: cleanedRevision || []
 })
}
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Don't" %}
```javascript
function GroupContent() {
 /**
  * Code that initiates the following variables:
  * loading
  * filters
  * filteredByCategories
  * listOptionsIcon
  * recentlyUsedIcons
  */

 return <Box>
   {!loading ? (
     filteredByCategories?.length || filters?.includes('recently used') ? (
       <div>
         {!!listOptionsIcon.length &&
           listOptionsIcon.map((item, index) => {
             return (
               <Box key={item.label}>
                 {(filters.length === 0 || filters.includes('recently used')) && index === 0 && (
                   <Text as="p" fontWeight="medium">
                     {t(recentlyUsedIcons.label)}
                   </Text>
                 )}
               </Box>
             )
           })}
       </div>
     ) : (
       <Box padding={'32'}>
         <EmptySearchResult heading={t('EMPTY_RESULTS_ICONS')} />
       </Box>
     )
   ) : (
     <LoadingIframe />
   )}
 </Box>
}
```
{% endtab %}

{% tab title="Do" %}
```javascript
function GroupContent() {
 /**
  * Code that initiates the following variables:
  * loading
  * filters
  * filteredByCategories
  * listOptionsIcon
  * recentlyUsedIcons
  */

 // Nested ternaries should be split into multiple control statements.
 if (loading) {
   return <Box>
     <LoadingIframe />
   </Box>
 }

 const isFilterByCategoriesOrRecentlyUsed =
   filteredByCategories?.length || filters?.includes('recently used')

 if (!isFilterByCategoriesOrRecentlyUsed) {
   return <Box>
     <Box padding={'32'}>
       <EmptySearchResult heading={t('EMPTY_RESULTS_ICONS')} />
     </Box>
   </Box>
 }

 // Simplify complex conditions used inline when rendering.
 const showRecentlyUsedIconLabel =
   filters.length === 0 || filters.includes('recently used')

 return <Box>
   <div>
     {listOptionsIcon?.map((item, index) => (
       <Box key={item.label}>
         {showRecentlyUsedIconLabel && index === 0 && (
           <Text as="p" fontWeight="medium">
             {t(recentlyUsedIcons.label)}
           </Text>
         )}
       </Box>
     ))}
   </div>
 </Box>
}
```
{% endtab %}
{% endtabs %}

Additionally, unless some special cases such as defining a list of properties for an object, developers should frequently use blank lines to separate code blocks for easy reading. More than three continuous lines of code without a blank line should be avoided.

{% tabs %}
{% tab title="Don't" %}
```javascript
export const loadModelViewer = ($master, src, poster, alt) => {
 const modelViewer = $master.querySelector('model-viewer')
 if (modelViewer) {
   modelViewer.setAttribute('poster', poster)
   modelViewer.setAttribute('src', src)
   modelViewer.setAttribute('alt', alt)
   modelViewer.classList.remove('pf-hidden')
 } else {
   const modelViewer: any = document.createElement('model-viewer')
   modelViewer.loading = 'eager'
   modelViewer.setAttribute('camera-controls', '')
   modelViewer.setAttribute('poster', poster)
   modelViewer.setAttribute('src', src)
   modelViewer.setAttribute('alt', alt)
   modelViewer.classList.add('featured-media')
   $master.prepend(modelViewer)
 }
}
```
{% endtab %}

{% tab title="Do" %}
```javascript
export const loadModelViewer = ($master, src, poster, alt) => {
 const modelViewer = $master.querySelector('model-viewer')

 // Always put a blank line above code blocks (control statements, loop
 // statements, function declarations, a group of similar code,...) unless
 // it is the first code block inside a file or another code block.
 if (modelViewer) {
   // Group only similar lines of code.
   modelViewer.setAttribute('poster', poster)
   modelViewer.setAttribute('src', src)
   modelViewer.setAttribute('alt', alt)

   // Separate unsimilar lines of code.
   modelViewer.classList.remove('pf-hidden')
 } else {
   // Group only similar lines of code.
   const modelViewer: any = document.createElement('model-viewer')
   modelViewer.loading = 'eager'

   // Group only similar lines of code.
   modelViewer.setAttribute('camera-controls', '')
   modelViewer.setAttribute('poster', poster)
   modelViewer.setAttribute('src', src)
   modelViewer.setAttribute('alt', alt)

   // Separate unsimilar lines of code.
   modelViewer.classList.add('featured-media')

   // Separate unsimilar lines of code.
   $master.prepend(modelViewer)
 }
}
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Don't" %}
```javascript
export const useCustomCodeEditor = () => {
 const [, forceUpdate] = useState(null)
 const elementStore = useInspectorContext(allStyleKeys)
 const {
   styleStore: { getGlobalStyle, getCurrentStyle, updateStyle },
   data: { classGlobalStyling },
 } = elementStore
 const {
   state: { device },
 } = useSubscription(workspaceSubscription, ['device'])
 const globalStyles = classGlobalStyling ? getGlobalStyle(`.__pf .${classGlobalStyling}`) : undefined
 const currentStyle = getCurrentStyle(device)
 const cssApplied = currentStyle?.cssText || ''
 const getValueCustomCode = val => {
   const value = val && globalStyles ? val + globalStyles.cssText : globalStyles ? globalStyles.cssText + val : val
   return value.replace(/;\s?/gm, ';').trim()
 }
 const handleUpdateStyle = valueStyle => {
   updateStyle({ cssText: valueStyle })
 }
 return { forceUpdate, updateStyle, cssApplied, getValueCustomCode, handleUpdateStyle }
}
```
{% endtab %}

{% tab title="Do" %}
```javascript
export const useCustomCodeEditor = () => {
 const [, forceUpdate] = useState(null)
 const elementStore = useInspectorContext(allStyleKeys)

 // An assignment statement that spread across multiple lines should be considered
 // a block of code and should be separated by putting blank lines around it.
 const {
   styleStore: { getGlobalStyle, getCurrentStyle, updateStyle },
   data: { classGlobalStyling },
 } = elementStore

 const {
   state: { device },
 } = useSubscription(workspaceSubscription, ['device'])

 const globalStyles = classGlobalStyling ? getGlobalStyle(`.__pf .${classGlobalStyling}`) : undefined
 const currentStyle = getCurrentStyle(device)
 const cssApplied = currentStyle?.cssText || ''

 // Blocks of code such as function declarations, control statements, loop statements, a
 // group of similar lines of code, etc. should be surrounded by blank lines.
 const getValueCustomCode = val => {
   const value = val && globalStyles ? val + globalStyles.cssText : globalStyles ? globalStyles.cssText + val : val
   return value.replace(/;\s?/gm, ';').trim()
 }

 const handleUpdateStyle = valueStyle => {
   updateStyle({ cssText: valueStyle })
 }

 return { forceUpdate, updateStyle, cssApplied, getValueCustomCode, handleUpdateStyle }
}
```
{% endtab %}
{% endtabs %}

For more details about simplicity in programming, I recommend you read the following articles: [The Power of Simplicity in Code](https://www.audero.it/blog/2016/08/03/power-simplicity-code/), [Simplify Your Code: The Power of the KISS Principle in JavaScript](https://medium.com/@ksekwamote/keep-it-simple-stupid-how-it-applies-in-javascript-113b1c4e77a8)

_**Don’t Repeat Yourself (DRY)**_ is about _**modularity**_ and _**reusable**_. Code repeats in more than two places, even only one line, should be converted to a reusable function. You might see it as a waste of time and unnecessary. However, imagine if that line of code needs to be updated. If you convert it to a reusable function, you can alter it in just one place. It will save time and help prevent bugs.

{% tabs %}
{% tab title="Don't" %}
```javascript
function ColorPicker({ value, onChange, onClear }) {
 return <Input
   value={value}
   onChange={onChange}
   onClear={onClear}
 />
}

function BackgroundColor({ data, setData }) {
 return (
   <ColorPicker
     value={data.filterColor}
     onChange={v => setData({ filterColor: v })}
     onClear={() => setData({ filterColor: '' })}
   />
 )
}

function LineColor({ data, setData }) {
 return (
   <ColorPicker
     value={data.filterColor}
     onChange={v => setData({ filterColor: v })}
     onClear={() => setData({ filterColor: '' })}
   />
 )
}

function ShadowColor({ data, setData }) {
 return (
   <ColorPicker
     value={data.filterColor}
     onChange={v => updateStyle({
       boxShadow: `${v} ${hOffset}px ${vOffset}px ${blur}px`,
       notPushHistory: false,
     })}
     onClear={() => updateStyle({
       boxShadow: `${''} ${hOffset}px ${vOffset}px ${blur} px`,
       notPushHistory: false,
     })}
   />
 )
}
```
{% endtab %}

{% tab title="Do" %}
```javascript
function ColorPicker({ data, setData, onChange, onClear }) {
 const handleChange = typeof onChange === 'function'
   ? onChange
   : useCallback(v => setData({ filterColor: v }), [setData])

 const handleClear = typeof onClear === 'function'
   ? onClear
   : useCallback(() => handleChange(''), [handleChange])

 return <Input
   value={data?.filterColor || ''}
   onChange={handleChange}
   onClear={handleClear}
 />
}

function BackgroundColor({ data, setData }) {
 return (
   <ColorPicker
     data={data}
     setData={setData}
   />
 )
}

const LineColor = BackgroundColor

function ShadowColor({ data, setData }) {
 return (
   <ColorPicker
     data={data}
     onChange={v => updateStyle({
       boxShadow: `${v} ${hOffset}px ${vOffset}px ${blur}px`,
       notPushHistory: false,
     })}
   />
 )
}
```
{% endtab %}
{% endtabs %}

For more details about modularity and reusable, I recommend you read the following article: [JavaScript Modules – Explained with Examples](https://www.freecodecamp.org/news/javascript-modules-explained-with-examples/)

## ~~6. Do user testing~~

~~Sometimes, users use the product not in the way the software was designed, even in a way not considered when designing the software. This behavior can cause errors that developers did not expect before.~~

~~Once coding is complete, developers should perform user testing before passing it to QA. User testing does not focus on technicalities but on usability. So, let the people involved in a test do what they want. You can introduce something about what you have done but let users use it their way.~~

~~Developers should record all actions users make when using the software so potential errors are not missed.~~

## Side notes

<mark style="color:purple;">If you can not fix the bug</mark> <mark style="color:purple;"></mark><mark style="color:purple;">**before the due date**</mark><mark style="color:purple;">, your issue will be delegated to other team member and your KPI will not be recorded</mark>
