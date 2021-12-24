[PF Server](../README.md) / [data/models/Shop](../modules/data_models_Shop.md) / PFShop

# Class: PFShop

[data/models/Shop](../modules/data_models_Shop.md).PFShop

## Table of contents

### Constructors

- [constructor](data_models_Shop.PFShop.md#constructor)

### Properties

- [$graphqlClient](data_models_Shop.PFShop.md#$graphqlclient)
- [$restClient](data_models_Shop.PFShop.md#$restclient)
- [accessToken](data_models_Shop.PFShop.md#accesstoken)
- [deprecated\_ShopifyClient](data_models_Shop.PFShop.md#deprecated_shopifyclient)
- [mainTheme](data_models_Shop.PFShop.md#maintheme)
- [shopData](data_models_Shop.PFShop.md#shopdata)
- [shopDomain](data_models_Shop.PFShop.md#shopdomain)

### Methods

- [checkPageTypeUseJsonTemplate](data_models_Shop.PFShop.md#checkpagetypeusejsontemplate)
- [convertPlan](data_models_Shop.PFShop.md#convertplan)
- [getAllThemeAssets](data_models_Shop.PFShop.md#getallthemeassets)
- [getCurrentActiveCharge](data_models_Shop.PFShop.md#getcurrentactivecharge)
- [getLicense](data_models_Shop.PFShop.md#getlicense)
- [getMainTheme](data_models_Shop.PFShop.md#getmaintheme)
- [getPlan](data_models_Shop.PFShop.md#getplan)
- [getRemainingPageCount](data_models_Shop.PFShop.md#getremainingpagecount)
- [getShopData](data_models_Shop.PFShop.md#getshopdata)
- [getShopMetaFromAPI](data_models_Shop.PFShop.md#getshopmetafromapi)
- [getShopPlanData](data_models_Shop.PFShop.md#getshopplandata)
- [getStoreUserData](data_models_Shop.PFShop.md#getstoreuserdata)
- [getThemeAssetsData](data_models_Shop.PFShop.md#getthemeassetsdata)
- [getThemeList](data_models_Shop.PFShop.md#getthemelist)
- [initDefaultPlan](data_models_Shop.PFShop.md#initdefaultplan)
- [initOfflineAccess](data_models_Shop.PFShop.md#initofflineaccess)
- [updatePageFlyMetaData](data_models_Shop.PFShop.md#updatepageflymetadata)
- [updatePlan](data_models_Shop.PFShop.md#updateplan)
- [updateShopMetaData](data_models_Shop.PFShop.md#updateshopmetadata)
- [updateShopPlan](data_models_Shop.PFShop.md#updateshopplan)
- [updateStore](data_models_Shop.PFShop.md#updatestore)
- [updateThemeAssetData](data_models_Shop.PFShop.md#updatethemeassetdata)

## Constructors

### constructor

• **new PFShop**(`__namedParameters`)

If don't have access token yet, load offline access by using this.initOfflineAccess(shopDomain)

#### Parameters

| Name | Type |
| :------ | :------ |
| `__namedParameters` | `Object` |

#### Defined in

[src/data/models/Shop.ts:143](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Shop.ts#lines-143)

## Properties

### $graphqlClient

• **$graphqlClient**: `any`

#### Defined in

[src/data/models/Shop.ts:132](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Shop.ts#lines-132)

___

### $restClient

• **$restClient**: `any`

#### Defined in

[src/data/models/Shop.ts:131](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Shop.ts#lines-131)

___

### accessToken

• **accessToken**: `string` = `''`

#### Defined in

[src/data/models/Shop.ts:129](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Shop.ts#lines-129)

___

### deprecated\_ShopifyClient

• **deprecated\_ShopifyClient**: `Shopify` = `null`

**`deprecated`** please migrate/use $graphqlClient instead

#### Defined in

[src/data/models/Shop.ts:136](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Shop.ts#lines-136)

___

### mainTheme

• **mainTheme**: `ITheme`

#### Defined in

[src/data/models/Shop.ts:130](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Shop.ts#lines-130)

___

### shopData

• **shopData**: [`IShopType`](../interfaces/data_models_types.IShopType.md) = `null`

#### Defined in

[src/data/models/Shop.ts:127](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Shop.ts#lines-127)

___

### shopDomain

• **shopDomain**: `string` = `''`

#### Defined in

[src/data/models/Shop.ts:128](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Shop.ts#lines-128)

## Methods

### checkPageTypeUseJsonTemplate

▸ **checkPageTypeUseJsonTemplate**(`templateKey`): `Promise`<`boolean`\>

https://shopify.dev/apps/online-store/verify-support

#### Parameters

| Name | Type |
| :------ | :------ |
| `templateKey` | `any` |

#### Returns

`Promise`<`boolean`\>

#### Defined in

[src/data/models/Shop.ts:210](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Shop.ts#lines-210)

___

### convertPlan

▸ **convertPlan**<`P`\>(`chargeData`): `P`

#### Type parameters

| Name | Type |
| :------ | :------ |
| `P` | extends [`PFChargeType`](../modules/data_models_types.md#pfchargetype) |

#### Parameters

| Name | Type |
| :------ | :------ |
| `chargeData` | `P` |

#### Returns

`P`

#### Defined in

[src/data/models/Shop.ts:321](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Shop.ts#lines-321)

___

### getAllThemeAssets

▸ **getAllThemeAssets**(): `Promise`<`any`\>

#### Returns

`Promise`<`any`\>

#### Defined in

[src/data/models/Shop.ts:200](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Shop.ts#lines-200)

___

### getCurrentActiveCharge

▸ **getCurrentActiveCharge**(): `Promise`<[`IPFPlan`](../interfaces/data_models_types.IPFPlan.md)\>

#### Returns

`Promise`<[`IPFPlan`](../interfaces/data_models_types.IPFPlan.md)\>

#### Defined in

[src/data/models/Shop.ts:379](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Shop.ts#lines-379)

___

### getLicense

▸ **getLicense**(`forceUpdate?`): `Promise`<[`ILicense`](../interfaces/data_models_types.ILicense.md)\>

#### Parameters

| Name | Type | Default value |
| :------ | :------ | :------ |
| `forceUpdate` | `boolean` | `false` |

#### Returns

`Promise`<[`ILicense`](../interfaces/data_models_types.ILicense.md)\>

#### Defined in

[src/data/models/Shop.ts:384](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Shop.ts#lines-384)

___

### getMainTheme

▸ **getMainTheme**(): `Promise`<`ITheme`\>

#### Returns

`Promise`<`ITheme`\>

#### Defined in

[src/data/models/Shop.ts:179](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Shop.ts#lines-179)

___

### getPlan

▸ **getPlan**(): `Promise`<[`IPlan`](../interfaces/data_models_types.IPlan.md)\>

#### Returns

`Promise`<[`IPlan`](../interfaces/data_models_types.IPlan.md)\>

#### Defined in

[src/data/models/Shop.ts:334](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Shop.ts#lines-334)

___

### getRemainingPageCount

▸ **getRemainingPageCount**(`type`): `Promise`<`number`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `type` | `any` |

#### Returns

`Promise`<`number`\>

#### Defined in

[src/data/models/Shop.ts:495](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Shop.ts#lines-495)

___

### getShopData

▸ **getShopData**(): `Promise`<[`IShopType`](../interfaces/data_models_types.IShopType.md)\>

#### Returns

`Promise`<[`IShopType`](../interfaces/data_models_types.IShopType.md)\>

#### Defined in

[src/data/models/Shop.ts:239](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Shop.ts#lines-239)

___

### getShopMetaFromAPI

▸ **getShopMetaFromAPI**(): `Promise`<`IShop`\>

#### Returns

`Promise`<`IShop`\>

#### Defined in

[src/data/models/Shop.ts:235](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Shop.ts#lines-235)

___

### getShopPlanData

▸ **getShopPlanData**(): `Promise`<`any`\>

#### Returns

`Promise`<`any`\>

#### Defined in

[src/data/models/Shop.ts:338](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Shop.ts#lines-338)

___

### getStoreUserData

▸ **getStoreUserData**(): `Promise`<`unknown`\>

#### Returns

`Promise`<`unknown`\>

#### Defined in

[src/data/models/Shop.ts:306](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Shop.ts#lines-306)

___

### getThemeAssetsData

▸ **getThemeAssetsData**(`key`): `Promise`<`any`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `key` | `any` |

#### Returns

`Promise`<`any`\>

#### Defined in

[src/data/models/Shop.ts:221](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Shop.ts#lines-221)

___

### getThemeList

▸ **getThemeList**(): `Promise`<`any`\>

#### Returns

`Promise`<`any`\>

#### Defined in

[src/data/models/Shop.ts:189](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Shop.ts#lines-189)

___

### initDefaultPlan

▸ **initDefaultPlan**(): `Promise`<[`IPlan`](../interfaces/data_models_types.IPlan.md)\>

#### Returns

`Promise`<[`IPlan`](../interfaces/data_models_types.IPlan.md)\>

#### Defined in

[src/data/models/Shop.ts:283](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Shop.ts#lines-283)

___

### initOfflineAccess

▸ **initOfflineAccess**(): `Promise`<[`IShopType`](../interfaces/data_models_types.IShopType.md)\>

#### Returns

`Promise`<[`IShopType`](../interfaces/data_models_types.IShopType.md)\>

#### Defined in

[src/data/models/Shop.ts:163](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Shop.ts#lines-163)

___

### updatePageFlyMetaData

▸ **updatePageFlyMetaData**(`data?`): `Promise`<[`IShopMeta`](../interfaces/data_models_types.IShopMeta.md)\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `data` | `Object` |

#### Returns

`Promise`<[`IShopMeta`](../interfaces/data_models_types.IShopMeta.md)\>

#### Defined in

[src/data/models/Shop.ts:267](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Shop.ts#lines-267)

___

### updatePlan

▸ **updatePlan**(`planData`): `Promise`<[`IPlan`](../interfaces/data_models_types.IPlan.md)\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `planData` | [`IPlan`](../interfaces/data_models_types.IPlan.md) |

#### Returns

`Promise`<[`IPlan`](../interfaces/data_models_types.IPlan.md)\>

#### Defined in

[src/data/models/Shop.ts:317](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Shop.ts#lines-317)

___

### updateShopMetaData

▸ **updateShopMetaData**(): `Promise`<[`IShopType`](../interfaces/data_models_types.IShopType.md)\>

#### Returns

`Promise`<[`IShopType`](../interfaces/data_models_types.IShopType.md)\>

#### Defined in

[src/data/models/Shop.ts:251](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Shop.ts#lines-251)

___

### updateShopPlan

▸ **updateShopPlan**(): `Promise`<`void`\>

#### Returns

`Promise`<`void`\>

#### Defined in

[src/data/models/Shop.ts:271](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Shop.ts#lines-271)

___

### updateStore

▸ **updateStore**(`data?`): `Promise`<[`IShopType`](../interfaces/data_models_types.IShopType.md)\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `data` | `Object` |

#### Returns

`Promise`<[`IShopType`](../interfaces/data_models_types.IShopType.md)\>

#### Defined in

[src/data/models/Shop.ts:247](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Shop.ts#lines-247)

___

### updateThemeAssetData

▸ **updateThemeAssetData**(`key`, `value`): `Promise`<`IAsset`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `key` | `any` |
| `value` | `any` |

#### Returns

`Promise`<`IAsset`\>

#### Defined in

[src/data/models/Shop.ts:227](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Shop.ts#lines-227)
