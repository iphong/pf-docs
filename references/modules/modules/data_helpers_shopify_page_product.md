[PF Server](../README.md) / data/helpers/shopify-page/product

# Module: data/helpers/shopify-page/product

## Table of contents

### Functions

- [handleRemoveProductTemplate](data_helpers_shopify_page_product.md#handleremoveproducttemplate)
- [revertBackupProductTemplate](data_helpers_shopify_page_product.md#revertbackupproducttemplate)
- [updateProductPageToShopify](data_helpers_shopify_page_product.md#updateproductpagetoshopify)
- [updateProductPageToTheme](data_helpers_shopify_page_product.md#updateproductpagetotheme)

## Functions

### handleRemoveProductTemplate

▸ `Const` **handleRemoveProductTemplate**(`Shop`, `page`): `Promise`<`void`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `Shop` | [`PFShop`](../classes/data_models_Shop.PFShop.md) |
| `page` | `any` |

#### Returns

`Promise`<`void`\>

#### Defined in

[src/data/helpers/shopify-page/product.ts:247](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/helpers/shopify-page/product.ts#lines-247)

___

### revertBackupProductTemplate

▸ **revertBackupProductTemplate**(`Shop`): `Promise`<`IAsset`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `Shop` | [`PFShop`](../classes/data_models_Shop.PFShop.md) |

#### Returns

`Promise`<`IAsset`\>

#### Defined in

[src/data/helpers/shopify-page/product.ts:34](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/helpers/shopify-page/product.ts#lines-34)

___

### updateProductPageToShopify

▸ **updateProductPageToShopify**(`Shop`, `input`, `oldPageData`): `Promise`<`IProduct`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `Shop` | [`PFShop`](../classes/data_models_Shop.PFShop.md) |
| `input` | `any` |
| `oldPageData` | `any` |

#### Returns

`Promise`<`IProduct`\>

#### Defined in

[src/data/helpers/shopify-page/product.ts:132](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/helpers/shopify-page/product.ts#lines-132)

___

### updateProductPageToTheme

▸ **updateProductPageToTheme**(`Shop`, `input`): `Promise`<`string`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `Shop` | [`PFShop`](../classes/data_models_Shop.PFShop.md) |
| `input` | [`IShopifyPage`](../interfaces/data_models_types.IShopifyPage.md) |

#### Returns

`Promise`<`string`\>

#### Defined in

[src/data/helpers/shopify-page/product.ts:185](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/helpers/shopify-page/product.ts#lines-185)
