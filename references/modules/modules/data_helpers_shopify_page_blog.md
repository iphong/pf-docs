[PF Server](../README.md) / data/helpers/shopify-page/blog

# Module: data/helpers/shopify-page/blog

## Table of contents

### Functions

- [handleRemoveBlogPost](data_helpers_shopify_page_blog.md#handleremoveblogpost)
- [updateBlogPageToShopify](data_helpers_shopify_page_blog.md#updateblogpagetoshopify)
- [updateBlogPageToTheme](data_helpers_shopify_page_blog.md#updateblogpagetotheme)

## Functions

### handleRemoveBlogPost

▸ `Const` **handleRemoveBlogPost**(`Shop`, `page`): `Promise`<`void`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `Shop` | [`PFShop`](../classes/data_models_Shop.PFShop.md) |
| `page` | [`IShopifyPage`](../interfaces/data_models_types.IShopifyPage.md) |

#### Returns

`Promise`<`void`\>

#### Defined in

[src/data/helpers/shopify-page/blog.ts:108](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/helpers/shopify-page/blog.ts#lines-108)

___

### updateBlogPageToShopify

▸ **updateBlogPageToShopify**(`Shop`, `input`): `Promise`<`any`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `Shop` | [`PFShop`](../classes/data_models_Shop.PFShop.md) |
| `input` | [`IShopifyPage`](../interfaces/data_models_types.IShopifyPage.md) |

#### Returns

`Promise`<`any`\>

#### Defined in

[src/data/helpers/shopify-page/blog.ts:10](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/helpers/shopify-page/blog.ts#lines-10)

___

### updateBlogPageToTheme

▸ **updateBlogPageToTheme**(`Shop`, `input`): `Promise`<`string`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `Shop` | [`PFShop`](../classes/data_models_Shop.PFShop.md) |
| `input` | `any` |

#### Returns

`Promise`<`string`\>

#### Defined in

[src/data/helpers/shopify-page/blog.ts:72](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/helpers/shopify-page/blog.ts#lines-72)
