[PF Server](../README.md) / controllers/page

# Module: controllers/page

## Table of contents

### Variables

- [debounceHandleShopifyPage](controllers_page.md#debouncehandleshopifypage)

### Functions

- [cleanUpData](controllers_page.md#cleanupdata)
- [exportMultiplePage](controllers_page.md#exportmultiplepage)
- [exportPage](controllers_page.md#exportpage)
- [getPageListToSearch](controllers_page.md#getpagelisttosearch)
- [getTemplateUsageData](controllers_page.md#gettemplateusagedata)
- [getUnlockedPage](controllers_page.md#getunlockedpage)
- [handlePreviewPage](controllers_page.md#handlepreviewpage)
- [handlePreviewPageInEditor](controllers_page.md#handlepreviewpageineditor)
- [recoverAllPages](controllers_page.md#recoverallpages)
- [unlockAllPages](controllers_page.md#unlockallpages)
- [unlockPageAPI](controllers_page.md#unlockpageapi)

## Variables

### debounceHandleShopifyPage

• **debounceHandleShopifyPage**: `ThrottledFunction`<[page: any, Shop: any], `Promise`<`void`\>\>

#### Defined in

[src/controllers/page.ts:68](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/controllers/page.ts#lines-68)

## Functions

### cleanUpData

▸ **cleanUpData**(`__namedParameters`): `Promise`<{ `cleanedPages`: `any` ; `cleanedRevision`: `void` \| [`HistoryType`](data_models_types.md#historytype)[]  }\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `__namedParameters` | `Object` |

#### Returns

`Promise`<{ `cleanedPages`: `any` ; `cleanedRevision`: `void` \| [`HistoryType`](data_models_types.md#historytype)[]  }\>

#### Defined in

[src/controllers/page.ts:253](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/controllers/page.ts#lines-253)

___

### exportMultiplePage

▸ `Const` **exportMultiplePage**(`req`, `res`): `Promise`<`any`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `any` |
| `res` | `any` |

#### Returns

`Promise`<`any`\>

#### Defined in

[src/controllers/page.ts:319](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/controllers/page.ts#lines-319)

___

### exportPage

▸ `Const` **exportPage**(`req`, `res`): `Promise`<`any`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `any` |
| `res` | `any` |

#### Returns

`Promise`<`any`\>

#### Defined in

[src/controllers/page.ts:291](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/controllers/page.ts#lines-291)

___

### getPageListToSearch

▸ `Const` **getPageListToSearch**(`req`, `res`): `void`

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `any` |
| `res` | `any` |

#### Returns

`void`

#### Defined in

[src/controllers/page.ts:428](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/controllers/page.ts#lines-428)

___

### getTemplateUsageData

▸ **getTemplateUsageData**(): `Promise`<`any`\>

#### Returns

`Promise`<`any`\>

#### Defined in

[src/controllers/page.ts:275](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/controllers/page.ts#lines-275)

___

### getUnlockedPage

▸ `Const` **getUnlockedPage**(`req`, `res`): `void`

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `any` |
| `res` | `any` |

#### Returns

`void`

#### Defined in

[src/controllers/page.ts:361](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/controllers/page.ts#lines-361)

___

### handlePreviewPage

▸ `Const` **handlePreviewPage**(`req`, `res`): `Promise`<`any`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `any` |
| `res` | `any` |

#### Returns

`Promise`<`any`\>

#### Defined in

[src/controllers/page.ts:183](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/controllers/page.ts#lines-183)

___

### handlePreviewPageInEditor

▸ `Const` **handlePreviewPageInEditor**(`req`, `res`): `Promise`<`any`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `any` |
| `res` | `any` |

#### Returns

`Promise`<`any`\>

#### Defined in

[src/controllers/page.ts:72](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/controllers/page.ts#lines-72)

___

### recoverAllPages

▸ `Const` **recoverAllPages**(`req`, `res`): `void`

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `any` |
| `res` | `any` |

#### Returns

`void`

#### Defined in

[src/controllers/page.ts:408](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/controllers/page.ts#lines-408)

___

### unlockAllPages

▸ `Const` **unlockAllPages**(`req`, `res`): `Promise`<`void`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `any` |
| `res` | `any` |

#### Returns

`Promise`<`void`\>

#### Defined in

[src/controllers/page.ts:385](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/controllers/page.ts#lines-385)

___

### unlockPageAPI

▸ `Const` **unlockPageAPI**(`req`, `res`): `Promise`<`void`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `any` |
| `res` | `any` |

#### Returns

`Promise`<`void`\>

#### Defined in

[src/controllers/page.ts:369](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/controllers/page.ts#lines-369)
