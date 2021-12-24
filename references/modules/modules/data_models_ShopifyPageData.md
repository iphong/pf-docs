[PF Server](../README.md) / data/models/ShopifyPageData

# Module: data/models/ShopifyPageData

## Table of contents

### References

- [default](data_models_ShopifyPageData.md#default)

### Variables

- [ShopifyPageData](data_models_ShopifyPageData.md#shopifypagedata)

### Functions

- [getPageDataById](data_models_ShopifyPageData.md#getpagedatabyid)
- [getShopifyPageDataById](data_models_ShopifyPageData.md#getshopifypagedatabyid)
- [removeShopifyPageDataById](data_models_ShopifyPageData.md#removeshopifypagedatabyid)
- [updateShopifyPageData](data_models_ShopifyPageData.md#updateshopifypagedata)

## References

### default

Renames and re-exports [ShopifyPageData](data_models_ShopifyPageData.md#shopifypagedata)

## Variables

### ShopifyPageData

• **ShopifyPageData**: `Model`<`any`, {}, {}, {}\>

#### Defined in

[src/data/models/ShopifyPageData.ts:32](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/ShopifyPageData.ts#lines-32)

## Functions

### getPageDataById

▸ **getPageDataById**(`_id`): `Promise`<`any`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `_id` | `any` |

#### Returns

`Promise`<`any`\>

#### Defined in

[src/data/models/ShopifyPageData.ts:78](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/ShopifyPageData.ts#lines-78)

___

### getShopifyPageDataById

▸ **getShopifyPageDataById**(`id`): `Promise`<[`IPageData`](../interfaces/data_models_types.IPageData.md)\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `id` | `any` |

#### Returns

`Promise`<[`IPageData`](../interfaces/data_models_types.IPageData.md)\>

#### Defined in

[src/data/models/ShopifyPageData.ts:51](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/ShopifyPageData.ts#lines-51)

___

### removeShopifyPageDataById

▸ **removeShopifyPageDataById**(`id`): `Promise`<`boolean`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `id` | `any` |

#### Returns

`Promise`<`boolean`\>

#### Defined in

[src/data/models/ShopifyPageData.ts:63](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/ShopifyPageData.ts#lines-63)

___

### updateShopifyPageData

▸ **updateShopifyPageData**(`input`): `Promise`<[`PageDataType`](data_models_types.md#pagedatatype)\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `input` | `any` |

#### Returns

`Promise`<[`PageDataType`](data_models_types.md#pagedatatype)\>

#### Defined in

[src/data/models/ShopifyPageData.ts:35](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/ShopifyPageData.ts#lines-35)
