[PF Server](../README.md) / helpers/customerio

# Module: helpers/customerio

## Table of contents

### Functions

- [checkFirstVistPricingPage](helpers_customerio.md#checkfirstvistpricingpage)
- [checkLastAccessWithin3months](helpers_customerio.md#checklastaccesswithin3months)
- [postAnonymousEventCustomerIo](helpers_customerio.md#postanonymouseventcustomerio)
- [postEventToCustomerIo](helpers_customerio.md#posteventtocustomerio)
- [requestCustomerIoApi](helpers_customerio.md#requestcustomerioapi)
- [requestCustomerIoBetaApi](helpers_customerio.md#requestcustomeriobetaapi)
- [syncUserDataToCustomerIo](helpers_customerio.md#syncuserdatatocustomerio)

## Functions

### checkFirstVistPricingPage

▸ `Const` **checkFirstVistPricingPage**(`req`, `res`): `Promise`<`void`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `any` |
| `res` | `any` |

#### Returns

`Promise`<`void`\>

#### Defined in

[src/helpers/customerio.ts:491](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/customerio.ts#lines-491)

___

### checkLastAccessWithin3months

▸ `Const` **checkLastAccessWithin3months**(`shopData`): `boolean`

#### Parameters

| Name | Type |
| :------ | :------ |
| `shopData` | `any` |

#### Returns

`boolean`

#### Defined in

[src/helpers/customerio.ts:504](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/customerio.ts#lines-504)

___

### postAnonymousEventCustomerIo

▸ `Const` **postAnonymousEventCustomerIo**(`eventName`, `shopData`, `eventData`): `Promise`<`unknown`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `eventName` | `any` |
| `shopData` | `any` |
| `eventData` | `any` |

#### Returns

`Promise`<`unknown`\>

#### Defined in

[src/helpers/customerio.ts:474](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/customerio.ts#lines-474)

___

### postEventToCustomerIo

▸ `Const` **postEventToCustomerIo**(`eventName`, `shopData`, `eventData?`): `Promise`<`unknown`\>

Method that posts an event to customer.io

#### Parameters

| Name | Type |
| :------ | :------ |
| `eventName` | `any` |
| `shopData` | `any` |
| `eventData` | `Object` |

#### Returns

`Promise`<`unknown`\>

Promise

#### Defined in

[src/helpers/customerio.ts:386](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/customerio.ts#lines-386)

___

### requestCustomerIoApi

▸ **requestCustomerIoApi**(`endPoint`, `method?`, `postData?`): `Promise`<`unknown`\>

Method that sends a request to customer.io API.

#### Parameters

| Name | Type | Default value |
| :------ | :------ | :------ |
| `endPoint` | `any` | `undefined` |
| `method` | `string` | `'get'` |
| `postData` | `any` | `undefined` |

#### Returns

`Promise`<`unknown`\>

Promise

#### Defined in

[src/helpers/customerio.ts:29](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/customerio.ts#lines-29)

___

### requestCustomerIoBetaApi

▸ **requestCustomerIoBetaApi**(`endPoint`, `queryString?`, `method?`, `postData?`): `Promise`<`unknown`\>

Method that sends a request to the Beta API of customer.io

#### Parameters

| Name | Type | Default value |
| :------ | :------ | :------ |
| `endPoint` | `any` | `undefined` |
| `queryString` | `string` | `''` |
| `method` | `string` | `'get'` |
| `postData` | `any` | `undefined` |

#### Returns

`Promise`<`unknown`\>

Promise

#### Defined in

[src/helpers/customerio.ts:66](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/customerio.ts#lines-66)

___

### syncUserDataToCustomerIo

▸ `Const` **syncUserDataToCustomerIo**(`email`, `customAttrs?`): `Promise`<`unknown`\>

Method that synchronizes user data to email profile at customer.io

#### Parameters

| Name | Type |
| :------ | :------ |
| `email` | `any` |
| `customAttrs` | `Object` |

#### Returns

`Promise`<`unknown`\>

Promise

#### Defined in

[src/helpers/customerio.ts:99](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/customerio.ts#lines-99)
