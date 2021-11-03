---
description: >-
  This is a detailed procedure on how to define a PageFly element and start
  developing it.
---

# Write your first element

{% hint style="info" %}
In this instruction we are going to create an element named "Demo"
{% endhint %}

## Define Component View

Component view is rendered on page. In editor view, user can click to select, drag and drop it into other elements on page.

Create a new folder called Demo then add a index.tsx in `/src/next/elements/base/`

```js
import { IPFElementProps } from '@t/index';
import React from 'react'
import { StyledDemo } from './styled';
import t from '@/language'

export interface IDemoProps extends IPFElementProps {
	foo: string
	bar: boolean
	name?: string
}

Demo.defaultProps = {
	foo: 'Foo Value',
	bar: true,
	name: t('DEMO')
}

export default function Demo(props:IDemoProps) {
	const { foo, bar } = props
	return <StyledDemo>
		This is a demo component: "{foo}"
	</StyledDemo>
}
```

next we need to register this component to the element registry. To do so, add the following line in the `/src/next/elements/index.tsx`

```js
...
import Demo from '@/elements/base/Demo'
...
...
const elementComponents: {
	[type: string]: FunctionComponent<IPFElementProps>
} = {
	Demo, // <------------ Add the following line
	Slide2,
	Slider2,
	Carousel: Slide,
	Slide,
	Slider,
	Button,
...
```

## Define Element Styling

Component can have variable styling defined using styled component. Create a file styled.ts in the Demo folder just created.

```js
import styled from 'styled-components'

export const StyledDemo = styled.div<any>`
	background: red;
`
```

## &#x20;Define Inspector View

An inspector view show selected element settings and configurations.

Create a file called demo.tsx inside `/src/next/modules/inspector/elements/base`

```js
import { InspectorContext } from "@/constants"
import { useContext } from "react"

export function DemoInspector() {
    const store = useContext(InspectorContext)
    const {styleStore: {updateStyle, getCurrentStyle}} = store
	console.log(store)
    return  <div>
		aloha
		<input type="text" defaultValue={store.state.data.foo} onChange={(e) => { console.log(e) }} />
	</div>
}
```

Then in the file `/src/next/modules/inspector/group.ts` add the following object in the inspectors array

In this example, we create an inspector group called "DemoContent", mapping the component \<DemoInspector> we created above

```js
...
import { DemoInspector } from './elements/base/demo'
...


const inspectors = [
	/**
	 * Demo element
	 */
	{
		Component: DemoInspector,
		tab: 'general',
		group: 'DemoContent',
		groupHeader: 'DEMO',
		keyword: [t('DEMO')]
	}
	....
	....
]
```

This inspector should show up when element is selected.

## Define Catalog Registry

Finally we need to add this element to the catalog so user can drag it from the left panel to add the element on to page.

First create a file called Demo.ts in `/src/next/modules/catalog/data/normalcatalog/` with the following content

```js
import {imageDir} from '@/constants/image-dir'
import t from '@/language'

export const DemoCatalog = {
	Demo: [
		{
			name: t('DEMO'),
			items: [
				{
					type: 'Demo',
					id: 0
				}
			],
			icon: imageDir + 'catalog/core-elements/button/1.svg'
		}
	]
}
```

then in the file `/src/next/modules/catalog/data/index.ts` add the following lines

```js
...
import {DemoCatalog} from '@/modules/catalog/data/normalcatalog/Demo'
...
...
export const catalogData = {
	Elements: {
		Containers: {
			...layoutCatalog,
			...tabsCatalog,
			...accordionsCatalog,
			...slider2Catalog
		},
		Basic: {
			...DemoCatalog, // <-------------- Add this line
			...headingCatalog,
			...paragraphCatalog,
			...buttonCatalog,
			...listCatalog,
			...htmlliquidCatalog
		},
		Media: {
			...mediaCatalog,
			...dividerCatalog
		},
		Social: {
			...socialCatalog
		},
...
```

Now your component should show up in the left panel. Drag your element on to page and test if everything is working.
