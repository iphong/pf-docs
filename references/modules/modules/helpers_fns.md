[PF Server](../README.md) / helpers/fns

# Module: helpers/fns

## Table of contents

### Functions

- [customHandleAuthCallback](helpers_fns.md#customhandleauthcallback)
- [generateAnalyticsDates](helpers_fns.md#generateanalyticsdates)
- [generateLocalHmac](helpers_fns.md#generatelocalhmac)
- [generateNewItemStyleId](helpers_fns.md#generatenewitemstyleid)
- [generatePreview](helpers_fns.md#generatepreview)
- [mergeAnalyticsData](helpers_fns.md#mergeanalyticsdata)
- [redirectToInstall](helpers_fns.md#redirecttoinstall)
- [renderIndexHtml](helpers_fns.md#renderindexhtml)
- [safeCompare](helpers_fns.md#safecompare)
- [stringifyQuery](helpers_fns.md#stringifyquery)
- [updateTitle](helpers_fns.md#updatetitle)
- [validateHmac](helpers_fns.md#validatehmac)
- [validateMicroService](helpers_fns.md#validatemicroservice)
- [validateShop](helpers_fns.md#validateshop)
- [verifyHMAC](helpers_fns.md#verifyhmac)

## Functions

### customHandleAuthCallback

▸ **customHandleAuthCallback**(`request`): `Promise`<{ `accessToken`: `any` ; `shop`: `any`  }\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `request` | `any` |

#### Returns

`Promise`<{ `accessToken`: `any` ; `shop`: `any`  }\>

#### Defined in

[src/helpers/fns.ts:233](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/fns.ts#lines-233)

___

### generateAnalyticsDates

▸ **generateAnalyticsDates**(`startDate`, `endDate`): `any`[]

#### Parameters

| Name | Type |
| :------ | :------ |
| `startDate` | `any` |
| `endDate` | `any` |

#### Returns

`any`[]

#### Defined in

[src/helpers/fns.ts:11](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/fns.ts#lines-11)

___

### generateLocalHmac

▸ **generateLocalHmac**(`__namedParameters`): `string`

#### Parameters

| Name | Type |
| :------ | :------ |
| `__namedParameters` | `AuthQuery` |

#### Returns

`string`

#### Defined in

[src/helpers/fns.ts:188](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/fns.ts#lines-188)

___

### generateNewItemStyleId

▸ **generateNewItemStyleId**(`__namedParameters`): `Object`

#### Parameters

| Name | Type |
| :------ | :------ |
| `__namedParameters` | `Object` |

#### Returns

`Object`

| Name | Type |
| :------ | :------ |
| `items` | `any`[] |
| `styles` | `any`[] |

#### Defined in

[src/helpers/fns.ts:82](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/fns.ts#lines-82)

___

### generatePreview

▸ **generatePreview**(`html`, `content?`, `tag?`): `any`

#### Parameters

| Name | Type | Default value |
| :------ | :------ | :------ |
| `html` | `any` | `undefined` |
| `content` | `string` | `''` |
| `tag` | `string` | `'main'` |

#### Returns

`any`

#### Defined in

[src/helpers/fns.ts:62](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/fns.ts#lines-62)

___

### mergeAnalyticsData

▸ **mergeAnalyticsData**(`analytics?`, `revenue?`): `any`[]

#### Parameters

| Name | Type | Default value |
| :------ | :------ | :------ |
| `analytics` | `any`[] | `[]` |
| `revenue` | `any`[] | `[]` |

#### Returns

`any`[]

#### Defined in

[src/helpers/fns.ts:27](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/fns.ts#lines-27)

___

### redirectToInstall

▸ `Const` **redirectToInstall**(`req`, `res`): `void`

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `any` |
| `res` | `any` |

#### Returns

`void`

#### Defined in

[src/helpers/fns.ts:289](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/fns.ts#lines-289)

___

### renderIndexHtml

▸ **renderIndexHtml**(`req`): `Promise`<`unknown`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `any` |

#### Returns

`Promise`<`unknown`\>

#### Defined in

[src/helpers/fns.ts:135](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/fns.ts#lines-135)

___

### safeCompare

▸ **safeCompare**(`strA`, `strB`): `boolean`

#### Parameters

| Name | Type |
| :------ | :------ |
| `strA` | `string` \| `string`[] \| `number`[] \| `Record`<`string`, `string`\> |
| `strB` | `string` \| `string`[] \| `number`[] \| `Record`<`string`, `string`\> |

#### Returns

`boolean`

#### Defined in

[src/helpers/fns.ts:153](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/fns.ts#lines-153)

___

### stringifyQuery

▸ **stringifyQuery**(`query`): `string`

#### Parameters

| Name | Type |
| :------ | :------ |
| `query` | `AuthQuery` |

#### Returns

`string`

#### Defined in

[src/helpers/fns.ts:178](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/fns.ts#lines-178)

___

### updateTitle

▸ **updateTitle**(`html`, `title`): `any`

#### Parameters

| Name | Type |
| :------ | :------ |
| `html` | `any` |
| `title` | `any` |

#### Returns

`any`

#### Defined in

[src/helpers/fns.ts:72](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/fns.ts#lines-72)

___

### validateHmac

▸ **validateHmac**(`query`): `boolean`

#### Parameters

| Name | Type |
| :------ | :------ |
| `query` | `any` |

#### Returns

`boolean`

#### Defined in

[src/helpers/fns.ts:223](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/fns.ts#lines-223)

___

### validateMicroService

▸ **validateMicroService**(`req`, `res`, `next`): `any`

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `any` |
| `res` | `any` |
| `next` | `any` |

#### Returns

`any`

#### Defined in

[src/helpers/fns.ts:280](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/fns.ts#lines-280)

___

### validateShop

▸ **validateShop**(`req`, `res`, `next`): `void`

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `any` |
| `res` | `any` |
| `next` | `any` |

#### Returns

`void`

#### Defined in

[src/helpers/fns.ts:45](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/fns.ts#lines-45)

___

### verifyHMAC

▸ **verifyHMAC**(`request`): `boolean`

#### Parameters

| Name | Type |
| :------ | :------ |
| `request` | `any` |

#### Returns

`boolean`

#### Defined in

[src/helpers/fns.ts:203](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/fns.ts#lines-203)
