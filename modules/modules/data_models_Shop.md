[PF Server](../README.md) / data/models/Shop

# Module: data/models/Shop

## Table of contents

### Classes

- [PFShop](../classes/data_models_Shop.PFShop.md)

### Variables

- [ShopModel](data_models_Shop.md#shopmodel)

### Functions

- [createShop](data_models_Shop.md#createshop)
- [getFilterShopData](data_models_Shop.md#getfiltershopdata)
- [getShopByDomain](data_models_Shop.md#getshopbydomain)
- [updatePageFlyShopMeta](data_models_Shop.md#updatepageflyshopmeta)
- [updateShopByShopDomain](data_models_Shop.md#updateshopbyshopdomain)

## Variables

### ShopModel

• **ShopModel**: `Model`<[`IShopType`](../interfaces/data_models_types.IShopType.md), {}, {}, {}\>

#### Defined in

[src/data/models/Shop.ts:57](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Shop.ts#lines-57)

## Functions

### createShop

▸ **createShop**(`shopDomain`, `data?`): `Promise`<[`IShopType`](../interfaces/data_models_types.IShopType.md)\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `shopDomain` | `any` |
| `data` | `Object` |

#### Returns

`Promise`<[`IShopType`](../interfaces/data_models_types.IShopType.md)\>

#### Defined in

[src/data/models/Shop.ts:72](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Shop.ts#lines-72)

___

### getFilterShopData

▸ **getFilterShopData**(`req`, `res`): `Promise`<`void`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `any` |
| `res` | `any` |

#### Returns

`Promise`<`void`\>

#### Defined in

[src/data/models/Shop.ts:107](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Shop.ts#lines-107)

___

### getShopByDomain

▸ **getShopByDomain**(`shopDomain`): `Promise`<[`IShopType`](../interfaces/data_models_types.IShopType.md)\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `shopDomain` | `any` |

#### Returns

`Promise`<[`IShopType`](../interfaces/data_models_types.IShopType.md)\>

#### Defined in

[src/data/models/Shop.ts:60](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Shop.ts#lines-60)

___

### updatePageFlyShopMeta

▸ **updatePageFlyShopMeta**(`shopDomain`, `meta?`): `Promise`<[`IShopMeta`](../interfaces/data_models_types.IShopMeta.md)\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `shopDomain` | `any` |
| `meta` | `Object` |

#### Returns

`Promise`<[`IShopMeta`](../interfaces/data_models_types.IShopMeta.md)\>

#### Defined in

[src/data/models/Shop.ts:100](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Shop.ts#lines-100)

___

### updateShopByShopDomain

▸ **updateShopByShopDomain**(`shopDomain`, `data`): `Promise`<[`IShopType`](../interfaces/data_models_types.IShopType.md)\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `shopDomain` | `any` |
| `data` | `any` |

#### Returns

`Promise`<[`IShopType`](../interfaces/data_models_types.IShopType.md)\>

#### Defined in

[src/data/models/Shop.ts:88](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Shop.ts#lines-88)
