[PF Server](../README.md) / data/queries/ShopifyPage

# Module: data/queries/ShopifyPage

## Table of contents

### Properties

- [default](data_queries_ShopifyPage.md#default)

### Functions

- [deletePagePermanently](data_queries_ShopifyPage.md#deletepagepermanently)
- [getDeletedPage](data_queries_ShopifyPage.md#getdeletedpage)
- [getPageCount](data_queries_ShopifyPage.md#getpagecount)
- [getPageData](data_queries_ShopifyPage.md#getpagedata)
- [getPageList2](data_queries_ShopifyPage.md#getpagelist2)
- [getPageListData](data_queries_ShopifyPage.md#getpagelistdata)
- [getPageListInfo](data_queries_ShopifyPage.md#getpagelistinfo)
- [getPublishedPageCount](data_queries_ShopifyPage.md#getpublishedpagecount)
- [queryPage](data_queries_ShopifyPage.md#querypage)
- [recoverPageById](data_queries_ShopifyPage.md#recoverpagebyid)

## Properties

### default

• **default**: `Object`

#### Type declaration

| Name | Type |
| :------ | :------ |
| `Query` | `Object` |
| `Query.pageData` | (`obj`: `any`, `args`: `any`, `context`: `any`, `info`: `any`) => `any` |
| `Query.pageList` | (`obj`: `any`, `args`: `any`, `context`: `any`, `info`: `any`) => `any` |
| `Query.pageListByType` | (`obj`: `any`, `args`: `any`, `context`: `any`, `info`: `any`) => `any` |

## Functions

### deletePagePermanently

▸ `Const` **deletePagePermanently**(`req`, `res`): `void`

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `any` |
| `res` | `any` |

#### Returns

`void`

#### Defined in

[src/data/queries/ShopifyPage.ts:188](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/queries/ShopifyPage.ts#lines-188)

___

### getDeletedPage

▸ `Const` **getDeletedPage**(`req`, `res`): `Promise`<`void`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `any` |
| `res` | `any` |

#### Returns

`Promise`<`void`\>

#### Defined in

[src/data/queries/ShopifyPage.ts:161](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/queries/ShopifyPage.ts#lines-161)

___

### getPageCount

▸ `Const` **getPageCount**(`req`, `res`): `Promise`<`any`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `any` |
| `res` | `any` |

#### Returns

`Promise`<`any`\>

#### Defined in

[src/data/queries/ShopifyPage.ts:90](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/queries/ShopifyPage.ts#lines-90)

___

### getPageData

▸ **getPageData**(`req`, `res`): `Promise`<`any`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `any` |
| `res` | `any` |

#### Returns

`Promise`<`any`\>

#### Defined in

[src/data/queries/ShopifyPage.ts:17](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/queries/ShopifyPage.ts#lines-17)

___

### getPageList2

▸ `Const` **getPageList2**(`req`, `res`): `Promise`<`any`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `any` |
| `res` | `any` |

#### Returns

`Promise`<`any`\>

#### Defined in

[src/data/queries/ShopifyPage.ts:77](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/queries/ShopifyPage.ts#lines-77)

___

### getPageListData

▸ `Const` **getPageListData**(`req`, `res`): `Promise`<`any`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `any` |
| `res` | `any` |

#### Returns

`Promise`<`any`\>

#### Defined in

[src/data/queries/ShopifyPage.ts:118](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/queries/ShopifyPage.ts#lines-118)

___

### getPageListInfo

▸ `Const` **getPageListInfo**(`req`, `res`): `Promise`<`any`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `any` |
| `res` | `any` |

#### Returns

`Promise`<`any`\>

#### Defined in

[src/data/queries/ShopifyPage.ts:140](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/queries/ShopifyPage.ts#lines-140)

___

### getPublishedPageCount

▸ `Const` **getPublishedPageCount**(`req`, `res`): `Promise`<`any`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `any` |
| `res` | `any` |

#### Returns

`Promise`<`any`\>

#### Defined in

[src/data/queries/ShopifyPage.ts:109](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/queries/ShopifyPage.ts#lines-109)

___

### queryPage

▸ `Const` **queryPage**(`__namedParameters`, `type?`, `title?`, `sort?`, `limit?`, `skip?`, `status?`): `Promise`<[`IShopifyPage`](../interfaces/data_models_types.IShopifyPage.md)[]\>

#### Parameters

| Name | Type | Default value |
| :------ | :------ | :------ |
| `__namedParameters` | `Object` | `undefined` |
| `type` | `string` | `'page'` |
| `title` | `string` | `''` |
| `sort` | `any` | `null` |
| `limit` | `number` | `20` |
| `skip` | `number` | `0` |
| `status` | `any` | `null` |

#### Returns

`Promise`<[`IShopifyPage`](../interfaces/data_models_types.IShopifyPage.md)[]\>

#### Defined in

[src/data/queries/ShopifyPage.ts:40](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/queries/ShopifyPage.ts#lines-40)

___

### recoverPageById

▸ `Const` **recoverPageById**(`req`, `res`): `void`

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `any` |
| `res` | `any` |

#### Returns

`void`

#### Defined in

[src/data/queries/ShopifyPage.ts:178](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/queries/ShopifyPage.ts#lines-178)
