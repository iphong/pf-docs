[PF Server](../README.md) / data/models/ShopifyPage

# Module: data/models/ShopifyPage

## Table of contents

### Variables

- [ShopifyPage](data_models_ShopifyPage.md#shopifypage)

### Functions

- [addShopifyPage](data_models_ShopifyPage.md#addshopifypage)
- [cleanUpOutDatePages](data_models_ShopifyPage.md#cleanupoutdatepages)
- [countPage](data_models_ShopifyPage.md#countpage)
- [countPublishedPage](data_models_ShopifyPage.md#countpublishedpage)
- [findAndUpdatePage](data_models_ShopifyPage.md#findandupdatepage)
- [findExistPage](data_models_ShopifyPage.md#findexistpage)
- [findPageAndUpdateConfigs](data_models_ShopifyPage.md#findpageandupdateconfigs)
- [generatePageDataToJsonFile](data_models_ShopifyPage.md#generatepagedatatojsonfile)
- [getExpiredPage](data_models_ShopifyPage.md#getexpiredpage)
- [getFilteredPageListByShopDomain](data_models_ShopifyPage.md#getfilteredpagelistbyshopdomain)
- [getPageByID](data_models_ShopifyPage.md#getpagebyid)
- [getPageByShopDomain](data_models_ShopifyPage.md#getpagebyshopdomain)
- [getPageListByShopDomain](data_models_ShopifyPage.md#getpagelistbyshopdomain)
- [getPageVersion](data_models_ShopifyPage.md#getpageversion)
- [getPagesByIds](data_models_ShopifyPage.md#getpagesbyids)
- [getUnlockedPagesID](data_models_ShopifyPage.md#getunlockedpagesid)
- [lockAllPageByShop](data_models_ShopifyPage.md#lockallpagebyshop)
- [removeAllDataByShop](data_models_ShopifyPage.md#removealldatabyshop)
- [removePageAnalyticData](data_models_ShopifyPage.md#removepageanalyticdata)
- [removePageFromDB](data_models_ShopifyPage.md#removepagefromdb)
- [savePageData](data_models_ShopifyPage.md#savepagedata)
- [searchPage](data_models_ShopifyPage.md#searchpage)
- [updateShopifyPage](data_models_ShopifyPage.md#updateshopifypage)
- [updateShopifyPageByID](data_models_ShopifyPage.md#updateshopifypagebyid)

## Variables

### ShopifyPage

• **ShopifyPage**: `Model`<[`PageModelType`](data_models_types.md#pagemodeltype), {}, {}, {}\>

#### Defined in

[src/data/models/ShopifyPage.ts:58](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/ShopifyPage.ts#lines-58)

## Functions

### addShopifyPage

▸ **addShopifyPage**(`input`): `Promise`<`any`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `input` | `any` |

#### Returns

`Promise`<`any`\>

#### Defined in

[src/data/models/ShopifyPage.ts:266](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/ShopifyPage.ts#lines-266)

___

### cleanUpOutDatePages

▸ **cleanUpOutDatePages**(`limitPage?`, `pageTimeRange?`): `Promise`<`any`\>

#### Parameters

| Name | Type | Default value |
| :------ | :------ | :------ |
| `limitPage` | `number` | `10` |
| `pageTimeRange` | `number` | `30` |

#### Returns

`Promise`<`any`\>

#### Defined in

[src/data/models/ShopifyPage.ts:460](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/ShopifyPage.ts#lines-460)

___

### countPage

▸ **countPage**(`options`): `Promise`<`number`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `options` | `any` |

#### Returns

`Promise`<`number`\>

#### Defined in

[src/data/models/ShopifyPage.ts:353](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/ShopifyPage.ts#lines-353)

___

### countPublishedPage

▸ **countPublishedPage**(`options`): `Promise`<`unknown`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `options` | `any` |

#### Returns

`Promise`<`unknown`\>

#### Defined in

[src/data/models/ShopifyPage.ts:365](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/ShopifyPage.ts#lines-365)

___

### findAndUpdatePage

▸ **findAndUpdatePage**(`conditions`, `input`): `Promise`<[`IShopifyPage`](../interfaces/data_models_types.IShopifyPage.md)\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `conditions` | `any` |
| `input` | `any` |

#### Returns

`Promise`<[`IShopifyPage`](../interfaces/data_models_types.IShopifyPage.md)\>

#### Defined in

[src/data/models/ShopifyPage.ts:295](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/ShopifyPage.ts#lines-295)

___

### findExistPage

▸ **findExistPage**(`type`, `shopifyPage`): `Promise`<[`IShopifyPage`](../interfaces/data_models_types.IShopifyPage.md)\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `type` | `any` |
| `shopifyPage` | `any` |

#### Returns

`Promise`<[`IShopifyPage`](../interfaces/data_models_types.IShopifyPage.md)\>

#### Defined in

[src/data/models/ShopifyPage.ts:325](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/ShopifyPage.ts#lines-325)

___

### findPageAndUpdateConfigs

▸ **findPageAndUpdateConfigs**(`query`, `configs`): `Promise`<`unknown`[]\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `query` | `any` |
| `configs` | `any` |

#### Returns

`Promise`<`unknown`[]\>

#### Defined in

[src/data/models/ShopifyPage.ts:310](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/ShopifyPage.ts#lines-310)

___

### generatePageDataToJsonFile

▸ **generatePageDataToJsonFile**(`page`, `shop`, `prefix?`): `string`

#### Parameters

| Name | Type | Default value |
| :------ | :------ | :------ |
| `page` | `any` | `undefined` |
| `shop` | `any` | `undefined` |
| `prefix` | `string` | `''` |

#### Returns

`string`

#### Defined in

[src/data/models/ShopifyPage.ts:88](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/ShopifyPage.ts#lines-88)

___

### getExpiredPage

▸ **getExpiredPage**(`limitPage?`, `pageTimeRange?`): `Promise`<[`IShopifyPage`](../interfaces/data_models_types.IShopifyPage.md)[]\>

#### Parameters

| Name | Type | Default value |
| :------ | :------ | :------ |
| `limitPage` | `number` | `10` |
| `pageTimeRange` | `number` | `30` |

#### Returns

`Promise`<[`IShopifyPage`](../interfaces/data_models_types.IShopifyPage.md)[]\>

#### Defined in

[src/data/models/ShopifyPage.ts:445](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/ShopifyPage.ts#lines-445)

___

### getFilteredPageListByShopDomain

▸ **getFilteredPageListByShopDomain**(`clientQuery`, `handleQuery?`): `Promise`<[`IShopifyPage`](../interfaces/data_models_types.IShopifyPage.md)[]\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `clientQuery` | `Object` |
| `clientQuery.page` | `any` |
| `clientQuery.perPage` | `any` |
| `clientQuery.query` | `any` |
| `clientQuery.sortData` | `any` |
| `clientQuery.status?` | `any` |
| `handleQuery?` | `Object` |
| `handleQuery.allTemplatesWithThisType` | `any` |
| `handleQuery.fetchMore` | `any` |
| `handleQuery.limit` | `any` |
| `handleQuery.result` | `any` |
| `handleQuery.skip` | `any` |

#### Returns

`Promise`<[`IShopifyPage`](../interfaces/data_models_types.IShopifyPage.md)[]\>

#### Defined in

[src/data/models/ShopifyPage.ts:190](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/ShopifyPage.ts#lines-190)

___

### getPageByID

▸ **getPageByID**(`id`): `Promise`<[`IShopifyPage`](../interfaces/data_models_types.IShopifyPage.md)\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `id` | `any` |

#### Returns

`Promise`<[`IShopifyPage`](../interfaces/data_models_types.IShopifyPage.md)\>

#### Defined in

[src/data/models/ShopifyPage.ts:60](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/ShopifyPage.ts#lines-60)

___

### getPageByShopDomain

▸ **getPageByShopDomain**(`shopDomain`, `type?`): `Promise`<[`PageModelType`](data_models_types.md#pagemodeltype)[]\>

#### Parameters

| Name | Type | Default value |
| :------ | :------ | :------ |
| `shopDomain` | `string` | `undefined` |
| `type` | `string` | `null` |

#### Returns

`Promise`<[`PageModelType`](data_models_types.md#pagemodeltype)[]\>

#### Defined in

[src/data/models/ShopifyPage.ts:115](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/ShopifyPage.ts#lines-115)

___

### getPageListByShopDomain

▸ **getPageListByShopDomain**(`query`, `limit?`, `skip?`, `sortData?`, `result?`, `_allThemeTemplatesWithThisType?`): `Promise`<[`IShopifyPage`](../interfaces/data_models_types.IShopifyPage.md)[]\>

#### Parameters

| Name | Type | Default value |
| :------ | :------ | :------ |
| `query` | `any` | `undefined` |
| `limit` | `number` | `20` |
| `skip` | `number` | `0` |
| `sortData` | `Object` | `{}` |
| `result` | `any`[] | `[]` |
| `_allThemeTemplatesWithThisType` | `any`[] | `[]` |

#### Returns

`Promise`<[`IShopifyPage`](../interfaces/data_models_types.IShopifyPage.md)[]\>

#### Defined in

[src/data/models/ShopifyPage.ts:157](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/ShopifyPage.ts#lines-157)

___

### getPageVersion

▸ **getPageVersion**(`pageId`): `Promise`<[`PageModelType`](data_models_types.md#pagemodeltype)\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `pageId` | `any` |

#### Returns

`Promise`<[`PageModelType`](data_models_types.md#pagemodeltype)\>

#### Defined in

[src/data/models/ShopifyPage.ts:76](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/ShopifyPage.ts#lines-76)

___

### getPagesByIds

▸ **getPagesByIds**(`_ids`): `Promise`<[`IShopifyPage`](../interfaces/data_models_types.IShopifyPage.md)[]\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `_ids` | `string`[] |

#### Returns

`Promise`<[`IShopifyPage`](../interfaces/data_models_types.IShopifyPage.md)[]\>

#### Defined in

[src/data/models/ShopifyPage.ts:482](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/ShopifyPage.ts#lines-482)

___

### getUnlockedPagesID

▸ **getUnlockedPagesID**(`shopDomain`, `type`): `Promise`<[`IShopifyPage`](../interfaces/data_models_types.IShopifyPage.md)[]\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `shopDomain` | `any` |
| `type` | `any` |

#### Returns

`Promise`<[`IShopifyPage`](../interfaces/data_models_types.IShopifyPage.md)[]\>

#### Defined in

[src/data/models/ShopifyPage.ts:378](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/ShopifyPage.ts#lines-378)

___

### lockAllPageByShop

▸ **lockAllPageByShop**(`shopDomain`): `Promise`<`unknown`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `shopDomain` | `any` |

#### Returns

`Promise`<`unknown`\>

#### Defined in

[src/data/models/ShopifyPage.ts:390](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/ShopifyPage.ts#lines-390)

___

### removeAllDataByShop

▸ **removeAllDataByShop**(`shopDomain`): `Promise`<`unknown`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `shopDomain` | `any` |

#### Returns

`Promise`<`unknown`\>

#### Defined in

[src/data/models/ShopifyPage.ts:493](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/ShopifyPage.ts#lines-493)

___

### removePageAnalyticData

▸ **removePageAnalyticData**(`pageId`): `CancelableRequest`<`Response`<`string`\>\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `pageId` | `any` |

#### Returns

`CancelableRequest`<`Response`<`string`\>\>

#### Defined in

[src/data/models/ShopifyPage.ts:477](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/ShopifyPage.ts#lines-477)

___

### removePageFromDB

▸ **removePageFromDB**(`page`): `Promise`<`boolean`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `page` | `any` |

#### Returns

`Promise`<`boolean`\>

#### Defined in

[src/data/models/ShopifyPage.ts:418](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/ShopifyPage.ts#lines-418)

___

### savePageData

▸ **savePageData**(`data`): `Promise`<[`IShopifyPage`](../interfaces/data_models_types.IShopifyPage.md)\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `data` | `any` |

#### Returns

`Promise`<[`IShopifyPage`](../interfaces/data_models_types.IShopifyPage.md)\>

#### Defined in

[src/data/models/ShopifyPage.ts:403](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/ShopifyPage.ts#lines-403)

___

### searchPage

▸ **searchPage**(`options`): `Promise`<[`IShopifyPage`](../interfaces/data_models_types.IShopifyPage.md)[]\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `options` | `any` |

#### Returns

`Promise`<[`IShopifyPage`](../interfaces/data_models_types.IShopifyPage.md)[]\>

#### Defined in

[src/data/models/ShopifyPage.ts:341](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/ShopifyPage.ts#lines-341)

___

### updateShopifyPage

▸ **updateShopifyPage**(`input`): `Promise`<[`IShopifyPage`](../interfaces/data_models_types.IShopifyPage.md)\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `input` | `any` |

#### Returns

`Promise`<[`IShopifyPage`](../interfaces/data_models_types.IShopifyPage.md)\>

#### Defined in

[src/data/models/ShopifyPage.ts:279](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/ShopifyPage.ts#lines-279)

___

### updateShopifyPageByID

▸ **updateShopifyPageByID**(`id`, `input`): `Promise`<[`IShopifyPage`](../interfaces/data_models_types.IShopifyPage.md)\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `id` | `any` |
| `input` | `any` |

#### Returns

`Promise`<[`IShopifyPage`](../interfaces/data_models_types.IShopifyPage.md)\>

#### Defined in

[src/data/models/ShopifyPage.ts:253](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/ShopifyPage.ts#lines-253)
