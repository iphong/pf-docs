[PF Server](../README.md) / data/mutations/shopify-page-mutation

# Module: data/mutations/shopify-page-mutation

## Table of contents

### Properties

- [default](data_mutations_shopify_page_mutation.md#default)

### Functions

- [handleShopifyPage](data_mutations_shopify_page_mutation.md#handleshopifypage)
- [mergePageData](data_mutations_shopify_page_mutation.md#mergepagedata)
- [updateShopifyPage](data_mutations_shopify_page_mutation.md#updateshopifypage)

## Properties

### default

• **default**: `Object`

#### Type declaration

| Name | Type |
| :------ | :------ |
| `Mutation` | `Object` |
| `Mutation.deletePage` | (`obj`: `any`, `args`: `any`, `context`: `any`, `info`: `any`) => `any` |
| `Mutation.duplicatePage` | (`obj`: `any`, `args`: `any`, `context`: `any`, `info`: `any`) => `any` |
| `Mutation.updatePageConfig` | (`obj`: `any`, `args`: `any`, `context`: `any`, `info`: `any`) => `any` |
| `Mutation.updateShopifyPage` | (`obj`: `any`, `args`: `any`, `context`: `any`, `info`: `any`) => `any` |

## Functions

### handleShopifyPage

▸ **handleShopifyPage**(`Shop`, `input`, `oldPageData`): `Promise`<`any`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `Shop` | [`PFShop`](../classes/data_models_Shop.PFShop.md) |
| `input` | `any` |
| `oldPageData` | `any` |

#### Returns

`Promise`<`any`\>

#### Defined in

[src/data/mutations/shopify-page-mutation.ts:106](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/mutations/shopify-page-mutation.ts#lines-106)

___

### mergePageData

▸ **mergePageData**(`oldData`, `newData`): [`IShopifyPage`](../interfaces/data_models_types.IShopifyPage.md)

#### Parameters

| Name | Type |
| :------ | :------ |
| `oldData` | `any` |
| `newData` | `any` |

#### Returns

[`IShopifyPage`](../interfaces/data_models_types.IShopifyPage.md)

#### Defined in

[src/data/mutations/shopify-page-mutation.ts:93](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/mutations/shopify-page-mutation.ts#lines-93)

___

### updateShopifyPage

▸ **updateShopifyPage**(`__namedParameters`, `__namedParameters`): `Promise`<[`IShopifyPage`](../interfaces/data_models_types.IShopifyPage.md) \| { `error`: `any`  }\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `__namedParameters` | `Object` |
| `__namedParameters` | `Object` |

#### Returns

`Promise`<[`IShopifyPage`](../interfaces/data_models_types.IShopifyPage.md) \| { `error`: `any`  }\>

#### Defined in

[src/data/mutations/shopify-page-mutation.ts:188](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/mutations/shopify-page-mutation.ts#lines-188)
