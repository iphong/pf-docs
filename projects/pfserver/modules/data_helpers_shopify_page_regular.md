[PF Server](../README.md) / data/helpers/shopify-page/regular

# Module: data/helpers/shopify-page/regular

## Table of contents

### Functions

- [addPageToShopify](data_helpers_shopify_page_regular.md#addpagetoshopify)
- [handleRemoveShopifyRegularPage](data_helpers_shopify_page_regular.md#handleremoveshopifyregularpage)
- [updatePageToShopify](data_helpers_shopify_page_regular.md#updatepagetoshopify)
- [updatePageToShopifyTheme](data_helpers_shopify_page_regular.md#updatepagetoshopifytheme)

## Functions

### addPageToShopify

▸ **addPageToShopify**(`input`, `deprecated_ShopifyClient`, `templateSuffix`): `Promise`<`IPage`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `input` | `any` |
| `deprecated_ShopifyClient` | `any` |
| `templateSuffix` | `any` |

#### Returns

`Promise`<`IPage`\>

#### Defined in

[src/data/helpers/shopify-page/regular.ts:44](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/helpers/shopify-page/regular.ts#lines-44)

___

### handleRemoveShopifyRegularPage

▸ `Const` **handleRemoveShopifyRegularPage**(`Shop`, `page`): `Promise`<`void`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `Shop` | [`PFShop`](../classes/data_models_Shop.PFShop.md) |
| `page` | `any` |

#### Returns

`Promise`<`void`\>

#### Defined in

[src/data/helpers/shopify-page/regular.ts:126](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/helpers/shopify-page/regular.ts#lines-126)

___

### updatePageToShopify

▸ **updatePageToShopify**(`Shop`, `input`, `oldPageData`): `Promise`<`IPage`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `Shop` | [`PFShop`](../classes/data_models_Shop.PFShop.md) |
| `input` | `any` |
| `oldPageData` | `any` |

#### Returns

`Promise`<`IPage`\>

#### Defined in

[src/data/helpers/shopify-page/regular.ts:77](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/helpers/shopify-page/regular.ts#lines-77)

___

### updatePageToShopifyTheme

▸ **updatePageToShopifyTheme**(`Shop`, `input`): `Promise`<`string`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `Shop` | [`PFShop`](../classes/data_models_Shop.PFShop.md) |
| `input` | [`IShopifyPage`](../interfaces/data_models_types.IShopifyPage.md) |

#### Returns

`Promise`<`string`\>

#### Defined in

[src/data/helpers/shopify-page/regular.ts:10](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/helpers/shopify-page/regular.ts#lines-10)
