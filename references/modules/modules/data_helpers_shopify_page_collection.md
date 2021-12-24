[PF Server](../README.md) / data/helpers/shopify-page/collection

# Module: data/helpers/shopify-page/collection

## Table of contents

### Functions

- [handleRemoveCollectionTemplate](data_helpers_shopify_page_collection.md#handleremovecollectiontemplate)
- [handleSetAllCollection](data_helpers_shopify_page_collection.md#handlesetallcollection)
- [revertBackupCollectionTemplate](data_helpers_shopify_page_collection.md#revertbackupcollectiontemplate)
- [updateCollectionPageToShopify](data_helpers_shopify_page_collection.md#updatecollectionpagetoshopify)
- [updateCollectionPageToTheme](data_helpers_shopify_page_collection.md#updatecollectionpagetotheme)

## Functions

### handleRemoveCollectionTemplate

▸ `Const` **handleRemoveCollectionTemplate**(`Shop`, `page`): `Promise`<`void`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `Shop` | [`PFShop`](../classes/data_models_Shop.PFShop.md) |
| `page` | [`IShopifyPage`](../interfaces/data_models_types.IShopifyPage.md) |

#### Returns

`Promise`<`void`\>

#### Defined in

[src/data/helpers/shopify-page/collection.ts:273](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/helpers/shopify-page/collection.ts#lines-273)

___

### handleSetAllCollection

▸ **handleSetAllCollection**(`Shop`, `input`): `Promise`<`void`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `Shop` | [`PFShop`](../classes/data_models_Shop.PFShop.md) |
| `input` | `any` |

#### Returns

`Promise`<`void`\>

#### Defined in

[src/data/helpers/shopify-page/collection.ts:152](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/helpers/shopify-page/collection.ts#lines-152)

___

### revertBackupCollectionTemplate

▸ **revertBackupCollectionTemplate**(`Shop`): `Promise`<`any`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `Shop` | [`PFShop`](../classes/data_models_Shop.PFShop.md) |

#### Returns

`Promise`<`any`\>

#### Defined in

[src/data/helpers/shopify-page/collection.ts:118](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/helpers/shopify-page/collection.ts#lines-118)

___

### updateCollectionPageToShopify

▸ **updateCollectionPageToShopify**(`Shop`, `input`, `oldPageData`): `Promise`<`ICollection`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `Shop` | [`PFShop`](../classes/data_models_Shop.PFShop.md) |
| `input` | `any` |
| `oldPageData` | `any` |

#### Returns

`Promise`<`ICollection`\>

#### Defined in

[src/data/helpers/shopify-page/collection.ts:210](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/helpers/shopify-page/collection.ts#lines-210)

___

### updateCollectionPageToTheme

▸ **updateCollectionPageToTheme**(`Shop`, `input`): `Promise`<`string`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `Shop` | [`PFShop`](../classes/data_models_Shop.PFShop.md) |
| `input` | [`IShopifyPage`](../interfaces/data_models_types.IShopifyPage.md) |

#### Returns

`Promise`<`string`\>

#### Defined in

[src/data/helpers/shopify-page/collection.ts:17](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/helpers/shopify-page/collection.ts#lines-17)
