[PF Server](../README.md) / controllers/shop

# Module: controllers/shop

## Table of contents

### Functions

- [addShopReferral](controllers_shop.md#addshopreferral)
- [cleanupData](controllers_shop.md#cleanupdata)
- [ejectThemeAssets](controllers_shop.md#ejectthemeassets)
- [generateShopifyConfig](controllers_shop.md#generateshopifyconfig)
- [getChargeInfo](controllers_shop.md#getchargeinfo)
- [getShopInfo](controllers_shop.md#getshopinfo)
- [getShopifyConfig](controllers_shop.md#getshopifyconfig)
- [handleAllRemainingRoute](controllers_shop.md#handleallremainingroute)
- [handleChangeTheme](controllers_shop.md#handlechangetheme)
- [handleCustomerDataRequest](controllers_shop.md#handlecustomerdatarequest)
- [handleCustomerRedact](controllers_shop.md#handlecustomerredact)
- [handleDeleteThemeWebhook](controllers_shop.md#handledeletethemewebhook)
- [handleShopRedact](controllers_shop.md#handleshopredact)
- [handleShopUpdateWebhook](controllers_shop.md#handleshopupdatewebhook)
- [handleUninstallApp](controllers_shop.md#handleuninstallapp)
- [logoutApp](controllers_shop.md#logoutapp)
- [logoutShop](controllers_shop.md#logoutshop)
- [rePublishAllPages](controllers_shop.md#republishallpages)
- [removeShopAnalyticData](controllers_shop.md#removeshopanalyticdata)
- [removeShopReferral](controllers_shop.md#removeshopreferral)
- [runNewThemePublishTask](controllers_shop.md#runnewthemepublishtask)
- [switchPageFlyVersion](controllers_shop.md#switchpageflyversion)
- [uninstallOrCloseShop](controllers_shop.md#uninstallorcloseshop)
- [uploadToMainTheme](controllers_shop.md#uploadtomaintheme)
- [uploadToShopifyPFTheme](controllers_shop.md#uploadtoshopifypftheme)

## Functions

### addShopReferral

▸ **addShopReferral**(`Shop`, `currentCharge`): `Promise`<`void`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `Shop` | [`PFShop`](../classes/data_models_Shop.PFShop.md) |
| `currentCharge` | `any` |

#### Returns

`Promise`<`void`\>

#### Defined in

[src/controllers/shop.ts:54](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/controllers/shop.ts#lines-54)

___

### cleanupData

▸ `Const` **cleanupData**(`req`, `res`): `Promise`<`void`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `any` |
| `res` | `any` |

#### Returns

`Promise`<`void`\>

#### Defined in

[src/controllers/shop.ts:537](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/controllers/shop.ts#lines-537)

___

### ejectThemeAssets

▸ `Const` **ejectThemeAssets**(`req`, `res`): `Promise`<`void`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `any` |
| `res` | `any` |

#### Returns

`Promise`<`void`\>

#### Defined in

[src/controllers/shop.ts:394](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/controllers/shop.ts#lines-394)

___

### generateShopifyConfig

▸ **generateShopifyConfig**(`Shop`): `Promise`<`any`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `Shop` | [`PFShop`](../classes/data_models_Shop.PFShop.md) |

#### Returns

`Promise`<`any`\>

#### Defined in

[src/controllers/shop.ts:493](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/controllers/shop.ts#lines-493)

___

### getChargeInfo

▸ `Const` **getChargeInfo**(`req`, `res`): `Promise`<`any`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `any` |
| `res` | `any` |

#### Returns

`Promise`<`any`\>

#### Defined in

[src/controllers/shop.ts:349](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/controllers/shop.ts#lines-349)

___

### getShopInfo

▸ `Const` **getShopInfo**(`req`, `res`): `Promise`<`any`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `any` |
| `res` | `any` |

#### Returns

`Promise`<`any`\>

#### Defined in

[src/controllers/shop.ts:409](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/controllers/shop.ts#lines-409)

___

### getShopifyConfig

▸ **getShopifyConfig**(`req`, `res`): `Promise`<`any`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `any` |
| `res` | `any` |

#### Returns

`Promise`<`any`\>

#### Defined in

[src/controllers/shop.ts:515](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/controllers/shop.ts#lines-515)

___

### handleAllRemainingRoute

▸ `Const` **handleAllRemainingRoute**(`req`, `res`): `Promise`<`any`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `any` |
| `res` | `any` |

#### Returns

`Promise`<`any`\>

#### Defined in

[src/controllers/shop.ts:435](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/controllers/shop.ts#lines-435)

___

### handleChangeTheme

▸ **handleChangeTheme**(`req`, `res`): `Promise`<`any`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `any` |
| `res` | `any` |

#### Returns

`Promise`<`any`\>

#### Defined in

[src/controllers/shop.ts:318](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/controllers/shop.ts#lines-318)

___

### handleCustomerDataRequest

▸ **handleCustomerDataRequest**(`req`, `res`): `Promise`<`any`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `any` |
| `res` | `any` |

#### Returns

`Promise`<`any`\>

#### Defined in

[src/controllers/shop.ts:140](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/controllers/shop.ts#lines-140)

___

### handleCustomerRedact

▸ **handleCustomerRedact**(`req`, `res`): `void`

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `any` |
| `res` | `any` |

#### Returns

`void`

#### Defined in

[src/controllers/shop.ts:162](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/controllers/shop.ts#lines-162)

___

### handleDeleteThemeWebhook

▸ **handleDeleteThemeWebhook**(`req`, `res`): `Promise`<`any`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `any` |
| `res` | `any` |

#### Returns

`Promise`<`any`\>

#### Defined in

[src/controllers/shop.ts:338](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/controllers/shop.ts#lines-338)

___

### handleShopRedact

▸ **handleShopRedact**(`req`, `res`): `Promise`<`any`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `any` |
| `res` | `any` |

#### Returns

`Promise`<`any`\>

#### Defined in

[src/controllers/shop.ts:170](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/controllers/shop.ts#lines-170)

___

### handleShopUpdateWebhook

▸ **handleShopUpdateWebhook**(`req`, `res`): `Promise`<`any`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `any` |
| `res` | `any` |

#### Returns

`Promise`<`any`\>

#### Defined in

[src/controllers/shop.ts:203](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/controllers/shop.ts#lines-203)

___

### handleUninstallApp

▸ **handleUninstallApp**(`req`, `res`): `Promise`<`any`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `any` |
| `res` | `any` |

#### Returns

`Promise`<`any`\>

#### Defined in

[src/controllers/shop.ts:116](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/controllers/shop.ts#lines-116)

___

### logoutApp

▸ `Const` **logoutApp**(`req`, `res`): `Promise`<`void`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `any` |
| `res` | `any` |

#### Returns

`Promise`<`void`\>

#### Defined in

[src/controllers/shop.ts:418](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/controllers/shop.ts#lines-418)

___

### logoutShop

▸ `Const` **logoutShop**(`shop`, `removeAccessToken?`): `Promise`<`void`\>

#### Parameters

| Name | Type | Default value |
| :------ | :------ | :------ |
| `shop` | `any` | `undefined` |
| `removeAccessToken` | `boolean` | `true` |

#### Returns

`Promise`<`void`\>

#### Defined in

[src/controllers/shop.ts:425](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/controllers/shop.ts#lines-425)

___

### rePublishAllPages

▸ `Const` **rePublishAllPages**(`req`, `res`): `Promise`<`void`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `any` |
| `res` | `any` |

#### Returns

`Promise`<`void`\>

#### Defined in

[src/controllers/shop.ts:370](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/controllers/shop.ts#lines-370)

___

### removeShopAnalyticData

▸ **removeShopAnalyticData**(`shopDomain`): `CancelableRequest`<`Response`<`string`\>\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `shopDomain` | `any` |

#### Returns

`CancelableRequest`<`Response`<`string`\>\>

#### Defined in

[src/controllers/shop.ts:198](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/controllers/shop.ts#lines-198)

___

### removeShopReferral

▸ **removeShopReferral**(`Shop`): `Promise`<`unknown`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `Shop` | [`PFShop`](../classes/data_models_Shop.PFShop.md) |

#### Returns

`Promise`<`unknown`\>

#### Defined in

[src/controllers/shop.ts:39](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/controllers/shop.ts#lines-39)

___

### runNewThemePublishTask

▸ `Const` **runNewThemePublishTask**(`Shop`): `Promise`<`void`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `Shop` | [`PFShop`](../classes/data_models_Shop.PFShop.md) |

#### Returns

`Promise`<`void`\>

#### Defined in

[src/controllers/shop.ts:280](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/controllers/shop.ts#lines-280)

___

### switchPageFlyVersion

▸ `Const` **switchPageFlyVersion**(`req`, `res`): `void`

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `any` |
| `res` | `any` |

#### Returns

`void`

#### Defined in

[src/controllers/shop.ts:455](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/controllers/shop.ts#lines-455)

___

### uninstallOrCloseShop

▸ **uninstallOrCloseShop**(`Shop`): `Promise`<`void`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `Shop` | [`PFShop`](../classes/data_models_Shop.PFShop.md) |

#### Returns

`Promise`<`void`\>

#### Defined in

[src/controllers/shop.ts:74](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/controllers/shop.ts#lines-74)

___

### uploadToMainTheme

▸ `Const` **uploadToMainTheme**(`req`, `res`): `Promise`<`void`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `any` |
| `res` | `any` |

#### Returns

`Promise`<`void`\>

#### Defined in

[src/controllers/shop.ts:440](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/controllers/shop.ts#lines-440)

___

### uploadToShopifyPFTheme

▸ `Const` **uploadToShopifyPFTheme**(`req`, `res`): `Promise`<`void`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `any` |
| `res` | `any` |

#### Returns

`Promise`<`void`\>

#### Defined in

[src/controllers/shop.ts:447](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/controllers/shop.ts#lines-447)
