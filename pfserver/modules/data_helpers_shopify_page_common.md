[PF Server](../README.md) / data/helpers/shopify-page/common

# Module: data/helpers/shopify-page/common

## Table of contents

### Functions

- [findThemeFileAndDelete](data_helpers_shopify_page_common.md#findthemefileanddelete)
- [generateJSONTemplate](data_helpers_shopify_page_common.md#generatejsontemplate)
- [generateTemplateSuffix](data_helpers_shopify_page_common.md#generatetemplatesuffix)
- [removeThemeAssetsByKey](data_helpers_shopify_page_common.md#removethemeassetsbykey)

## Functions

### findThemeFileAndDelete

▸ `Const` **findThemeFileAndDelete**(`Shop`, `keys`, `except?`): `Promise`<`void`\>

#### Parameters

| Name | Type | Default value |
| :------ | :------ | :------ |
| `Shop` | [`PFShop`](../classes/data_models_Shop.PFShop.md) | `undefined` |
| `keys` | `string`[] | `undefined` |
| `except` | `any` | `null` |

#### Returns

`Promise`<`void`\>

#### Defined in

[src/data/helpers/shopify-page/common.ts:23](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/helpers/shopify-page/common.ts#lines-23)

___

### generateJSONTemplate

▸ **generateJSONTemplate**(`Shop`, `sectionKey`, `templateAssetKey`, `hideHeaderFooter?`, `oldTemplateAssetKey?`): `Promise`<`string`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `Shop` | [`PFShop`](../classes/data_models_Shop.PFShop.md) |
| `sectionKey` | `any` |
| `templateAssetKey` | `any` |
| `hideHeaderFooter?` | `any` |
| `oldTemplateAssetKey?` | `any` |

#### Returns

`Promise`<`string`\>

#### Defined in

[src/data/helpers/shopify-page/common.ts:39](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/helpers/shopify-page/common.ts#lines-39)

___

### generateTemplateSuffix

▸ `Const` **generateTemplateSuffix**(`id`): `string`

#### Parameters

| Name | Type |
| :------ | :------ |
| `id` | `any` |

#### Returns

`string`

#### Defined in

[src/data/helpers/shopify-page/common.ts:18](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/helpers/shopify-page/common.ts#lines-18)

___

### removeThemeAssetsByKey

▸ `Const` **removeThemeAssetsByKey**(`Shop`, `key`): `Promise`<`void`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `Shop` | [`PFShop`](../classes/data_models_Shop.PFShop.md) |
| `key` | `any` |

#### Returns

`Promise`<`void`\>

#### Defined in

[src/data/helpers/shopify-page/common.ts:4](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/helpers/shopify-page/common.ts#lines-4)
