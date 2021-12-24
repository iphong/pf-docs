[PF Server](../README.md) / [handlers/shopify](../modules/handlers_shopify.md) / PageFlyShopifyHandler

# Class: PageFlyShopifyHandler

[handlers/shopify](../modules/handlers_shopify.md).PageFlyShopifyHandler

## Table of contents

### Constructors

- [constructor](handlers_shopify.PageFlyShopifyHandler.md#constructor)

### Properties

- [app](handlers_shopify.PageFlyShopifyHandler.md#app)
- [sessionStore](handlers_shopify.PageFlyShopifyHandler.md#sessionstore)

### Methods

- [authWithShopify](handlers_shopify.PageFlyShopifyHandler.md#authwithshopify)
- [handleAfterAuthEffect](handlers_shopify.PageFlyShopifyHandler.md#handleafterautheffect)
- [handleShopifyAuthCallback](handlers_shopify.PageFlyShopifyHandler.md#handleshopifyauthcallback)
- [handleWebhook](handlers_shopify.PageFlyShopifyHandler.md#handlewebhook)
- [initRouting](handlers_shopify.PageFlyShopifyHandler.md#initrouting)
- [initShopifyContext](handlers_shopify.PageFlyShopifyHandler.md#initshopifycontext)

## Constructors

### constructor

• **new PageFlyShopifyHandler**(`app`, `sessionStore`)

#### Parameters

| Name | Type |
| :------ | :------ |
| `app` | `Express` |
| `sessionStore` | `any` |

#### Defined in

[src/handlers/shopify.ts:117](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/handlers/shopify.ts#lines-117)

## Properties

### app

• **app**: `Express`

#### Defined in

[src/handlers/shopify.ts:114](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/handlers/shopify.ts#lines-114)

___

### sessionStore

• **sessionStore**: `any`

#### Defined in

[src/handlers/shopify.ts:115](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/handlers/shopify.ts#lines-115)

## Methods

### authWithShopify

▸ **authWithShopify**(`request`, `response`): `Promise`<`void`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `request` | `any` |
| `response` | `any` |

#### Returns

`Promise`<`void`\>

#### Defined in

[src/handlers/shopify.ts:146](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/handlers/shopify.ts#lines-146)

___

### handleAfterAuthEffect

▸ **handleAfterAuthEffect**(`req`, `res`): `Promise`<`void`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `any` |
| `res` | `any` |

#### Returns

`Promise`<`void`\>

#### Defined in

[src/handlers/shopify.ts:254](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/handlers/shopify.ts#lines-254)

___

### handleShopifyAuthCallback

▸ **handleShopifyAuthCallback**(`req`, `res`): `Promise`<`any`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `any` |
| `res` | `any` |

#### Returns

`Promise`<`any`\>

#### Defined in

[src/handlers/shopify.ts:171](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/handlers/shopify.ts#lines-171)

___

### handleWebhook

▸ **handleWebhook**(`topic`, `shop`, `webhookRequestBody`): `Promise`<`void`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `topic` | `string` |
| `shop` | `string` |
| `webhookRequestBody` | `string` |

#### Returns

`Promise`<`void`\>

#### Defined in

[src/handlers/shopify.ts:326](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/handlers/shopify.ts#lines-326)

___

### initRouting

▸ **initRouting**(): `void`

#### Returns

`void`

#### Defined in

[src/handlers/shopify.ts:210](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/handlers/shopify.ts#lines-210)

___

### initShopifyContext

▸ **initShopifyContext**(): `void`

#### Returns

`void`

#### Defined in

[src/handlers/shopify.ts:124](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/handlers/shopify.ts#lines-124)
