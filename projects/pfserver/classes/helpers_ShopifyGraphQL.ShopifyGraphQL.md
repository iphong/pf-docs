[PF Server](../README.md) / [helpers/ShopifyGraphQL](../modules/helpers_ShopifyGraphQL.md) / ShopifyGraphQL

# Class: ShopifyGraphQL

[helpers/ShopifyGraphQL](../modules/helpers_ShopifyGraphQL.md).ShopifyGraphQL

## Table of contents

### Constructors

- [constructor](helpers_ShopifyGraphQL.ShopifyGraphQL.md#constructor)

### Properties

- [accessToken](helpers_ShopifyGraphQL.ShopifyGraphQL.md#accesstoken)
- [baseUrl](helpers_ShopifyGraphQL.ShopifyGraphQL.md#baseurl)
- [options](helpers_ShopifyGraphQL.ShopifyGraphQL.md#options)
- [shopDomain](helpers_ShopifyGraphQL.ShopifyGraphQL.md#shopdomain)
- [version](helpers_ShopifyGraphQL.ShopifyGraphQL.md#version)

### Methods

- [createAppSubscription](helpers_ShopifyGraphQL.ShopifyGraphQL.md#createappsubscription)
- [requestGraphQL](helpers_ShopifyGraphQL.ShopifyGraphQL.md#requestgraphql)

## Constructors

### constructor

• **new ShopifyGraphQL**(`options`)

#### Parameters

| Name | Type |
| :------ | :------ |
| `options` | [`IShopifyGraphQLOptions`](../interfaces/helpers_ShopifyGraphQL._internal_.IShopifyGraphQLOptions.md) |

#### Defined in

[src/helpers/ShopifyGraphQL.ts:32](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/ShopifyGraphQL.ts#lines-32)

## Properties

### accessToken

• **accessToken**: `string`

#### Defined in

[src/helpers/ShopifyGraphQL.ts:24](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/ShopifyGraphQL.ts#lines-24)

___

### baseUrl

• **baseUrl**: `Object` = `{}`

#### Defined in

[src/helpers/ShopifyGraphQL.ts:28](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/ShopifyGraphQL.ts#lines-28)

___

### options

• **options**: [`IShopifyGraphQLOptions`](../interfaces/helpers_ShopifyGraphQL._internal_.IShopifyGraphQLOptions.md)

#### Defined in

[src/helpers/ShopifyGraphQL.ts:25](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/ShopifyGraphQL.ts#lines-25)

___

### shopDomain

• **shopDomain**: `any`

#### Defined in

[src/helpers/ShopifyGraphQL.ts:29](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/ShopifyGraphQL.ts#lines-29)

___

### version

• **version**: `string` = `shopifyAPIVersion`

#### Defined in

[src/helpers/ShopifyGraphQL.ts:30](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/ShopifyGraphQL.ts#lines-30)

## Methods

### createAppSubscription

▸ **createAppSubscription**(`planData`): `Promise`<`any`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `planData` | [`IGraphQLCharge`](../interfaces/helpers_ShopifyGraphQL.IGraphQLCharge.md) |

#### Returns

`Promise`<`any`\>

#### Defined in

[src/helpers/ShopifyGraphQL.ts:88](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/ShopifyGraphQL.ts#lines-88)

___

### requestGraphQL

▸ **requestGraphQL**(`body`): `Promise`<`any`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `body` | `Object` |
| `body.query?` | `string` |
| `body.variables?` | `any` |

#### Returns

`Promise`<`any`\>

#### Defined in

[src/helpers/ShopifyGraphQL.ts:63](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/ShopifyGraphQL.ts#lines-63)
