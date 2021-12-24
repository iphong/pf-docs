[PF Server](../README.md) / data/helpers/shopify-helper

# Module: data/helpers/shopify-helper

## Table of contents

### Functions

- [cancelCurrentActiveCharge](data_helpers_shopify_helper.md#cancelcurrentactivecharge)
- [generateSchema](data_helpers_shopify_helper.md#generateschema)
- [generateTemplateHtml](data_helpers_shopify_helper.md#generatetemplatehtml)
- [getMainCss](data_helpers_shopify_helper.md#getmaincss)
- [getMaximumPageCreateCount](data_helpers_shopify_helper.md#getmaximumpagecreatecount)
- [getMaximumPageEditCount](data_helpers_shopify_helper.md#getmaximumpageeditcount)
- [getMaximumSavedSectionCount](data_helpers_shopify_helper.md#getmaximumsavedsectioncount)
- [getShopifyActiveCharge](data_helpers_shopify_helper.md#getshopifyactivecharge)
- [initPageFlyTheme](data_helpers_shopify_helper.md#initpageflytheme)
- [migratePageToTheme](data_helpers_shopify_helper.md#migratepagetotheme)
- [minifyCss](data_helpers_shopify_helper.md#minifycss)
- [purgeAndMinifyCss](data_helpers_shopify_helper.md#purgeandminifycss)
- [removeRedundancyItemsStyles](data_helpers_shopify_helper.md#removeredundancyitemsstyles)
- [updateItemsAndStylesToDatabase](data_helpers_shopify_helper.md#updateitemsandstylestodatabase)
- [uploadToShopify](data_helpers_shopify_helper.md#uploadtoshopify)
- [validatePageInput](data_helpers_shopify_helper.md#validatepageinput)

## Functions

### cancelCurrentActiveCharge

▸ **cancelCurrentActiveCharge**(`Shop`): `Promise`<`void`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `Shop` | [`PFShop`](../classes/data_models_Shop.PFShop.md) |

#### Returns

`Promise`<`void`\>

#### Defined in

[src/data/helpers/shopify-helper.ts:285](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/helpers/shopify-helper.ts#lines-285)

___

### generateSchema

▸ `Const` **generateSchema**(`page`, `showInThemeSection?`, `allowAppBlock?`): `string`

#### Parameters

| Name | Type | Default value |
| :------ | :------ | :------ |
| `page` | `any` | `undefined` |
| `showInThemeSection` | `boolean` | `false` |
| `allowAppBlock` | `boolean` | `false` |

#### Returns

`string`

#### Defined in

[src/data/helpers/shopify-helper.ts:69](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/helpers/shopify-helper.ts#lines-69)

___

### generateTemplateHtml

▸ **generateTemplateHtml**(`input`, `Shop`): `Promise`<`string`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `input` | [`IShopifyPage`](../interfaces/data_models_types.IShopifyPage.md) |
| `Shop` | [`PFShop`](../classes/data_models_Shop.PFShop.md) |

#### Returns

`Promise`<`string`\>

#### Defined in

[src/data/helpers/shopify-helper.ts:123](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/helpers/shopify-helper.ts#lines-123)

___

### getMainCss

▸ `Const` **getMainCss**(): `Promise`<`unknown`\>

#### Returns

`Promise`<`unknown`\>

#### Defined in

[src/data/helpers/shopify-helper.ts:102](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/helpers/shopify-helper.ts#lines-102)

___

### getMaximumPageCreateCount

▸ `Const` **getMaximumPageCreateCount**(`plan`, `pageType`): `number`

#### Parameters

| Name | Type |
| :------ | :------ |
| `plan` | [`IPFPlan`](../interfaces/data_models_types.IPFPlan.md) |
| `pageType` | `any` |

#### Returns

`number`

#### Defined in

[src/data/helpers/shopify-helper.ts:293](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/helpers/shopify-helper.ts#lines-293)

___

### getMaximumPageEditCount

▸ `Const` **getMaximumPageEditCount**(`plan`, `pageType`): `number`

#### Parameters

| Name | Type |
| :------ | :------ |
| `plan` | [`IPFPlan`](../interfaces/data_models_types.IPFPlan.md) |
| `pageType` | `any` |

#### Returns

`number`

#### Defined in

[src/data/helpers/shopify-helper.ts:299](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/helpers/shopify-helper.ts#lines-299)

___

### getMaximumSavedSectionCount

▸ `Const` **getMaximumSavedSectionCount**(`plan`): `number`

#### Parameters

| Name | Type |
| :------ | :------ |
| `plan` | [`IPFPlan`](../interfaces/data_models_types.IPFPlan.md) |

#### Returns

`number`

#### Defined in

[src/data/helpers/shopify-helper.ts:306](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/helpers/shopify-helper.ts#lines-306)

___

### getShopifyActiveCharge

▸ **getShopifyActiveCharge**(`Shop`): `Promise`<`IRecurringApplicationCharge`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `Shop` | [`PFShop`](../classes/data_models_Shop.PFShop.md) |

#### Returns

`Promise`<`IRecurringApplicationCharge`\>

#### Defined in

[src/data/helpers/shopify-helper.ts:269](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/helpers/shopify-helper.ts#lines-269)

___

### initPageFlyTheme

▸ **initPageFlyTheme**(`deprecated_ShopifyClient`): `Promise`<`number`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `deprecated_ShopifyClient` | `any` |

#### Returns

`Promise`<`number`\>

#### Defined in

[src/data/helpers/shopify-helper.ts:201](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/helpers/shopify-helper.ts#lines-201)

___

### migratePageToTheme

▸ **migratePageToTheme**(`Shop`, `i`): `Promise`<`any`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `Shop` | [`PFShop`](../classes/data_models_Shop.PFShop.md) |
| `i` | [`IShopifyPage`](../interfaces/data_models_types.IShopifyPage.md) |

#### Returns

`Promise`<`any`\>

#### Defined in

[src/data/helpers/shopify-helper.ts:142](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/helpers/shopify-helper.ts#lines-142)

___

### minifyCss

▸ `Const` **minifyCss**(`css`): `string`

#### Parameters

| Name | Type |
| :------ | :------ |
| `css` | `string` |

#### Returns

`string`

#### Defined in

[src/data/helpers/shopify-helper.ts:26](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/helpers/shopify-helper.ts#lines-26)

___

### purgeAndMinifyCss

▸ **purgeAndMinifyCss**(`css`, `html`): `Promise`<`string`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `css` | `any` |
| `html` | `any` |

#### Returns

`Promise`<`string`\>

#### Defined in

[src/data/helpers/shopify-helper.ts:41](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/helpers/shopify-helper.ts#lines-41)

___

### removeRedundancyItemsStyles

▸ **removeRedundancyItemsStyles**(`oldPageData`): `Promise`<`void`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `oldPageData` | `any` |

#### Returns

`Promise`<`void`\>

#### Defined in

[src/data/helpers/shopify-helper.ts:185](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/helpers/shopify-helper.ts#lines-185)

___

### updateItemsAndStylesToDatabase

▸ **updateItemsAndStylesToDatabase**(`pageId`, `items`, `styles`): `void`

#### Parameters

| Name | Type |
| :------ | :------ |
| `pageId` | `any` |
| `items` | `any` |
| `styles` | `any` |

#### Returns

`void`

#### Defined in

[src/data/helpers/shopify-helper.ts:172](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/helpers/shopify-helper.ts#lines-172)

___

### uploadToShopify

▸ **uploadToShopify**(`req`, `main?`): `Promise`<`IAsset`\>

#### Parameters

| Name | Type | Default value |
| :------ | :------ | :------ |
| `req` | `any` | `undefined` |
| `main` | `boolean` | `false` |

#### Returns

`Promise`<`IAsset`\>

#### Defined in

[src/data/helpers/shopify-helper.ts:238](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/helpers/shopify-helper.ts#lines-238)

___

### validatePageInput

▸ **validatePageInput**(`input`): `void`

#### Parameters

| Name | Type |
| :------ | :------ |
| `input` | `any` |

#### Returns

`void`

#### Defined in

[src/data/helpers/shopify-helper.ts:194](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/helpers/shopify-helper.ts#lines-194)
