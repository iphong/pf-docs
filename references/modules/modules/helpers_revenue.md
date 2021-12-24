[PF Server](../README.md) / helpers/revenue

# Module: helpers/revenue

## Table of contents

### Functions

- [getOrderList](helpers_revenue.md#getorderlist)
- [getRevenueDataByShop](helpers_revenue.md#getrevenuedatabyshop)

## Functions

### getOrderList

▸ **getOrderList**(`shop`, `startDate`, `endDate`, `timezoneOffset?`): `Promise`<`IOrder`[]\>

#### Parameters

| Name | Type | Default value |
| :------ | :------ | :------ |
| `shop` | `any` | `undefined` |
| `startDate` | `any` | `undefined` |
| `endDate` | `any` | `undefined` |
| `timezoneOffset` | `any` | `'7'` |

#### Returns

`Promise`<`IOrder`[]\>

#### Defined in

[src/helpers/revenue.ts:65](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/revenue.ts#lines-65)

___

### getRevenueDataByShop

▸ **getRevenueDataByShop**(`shop`, `startDate`, `endDate`, `timezoneOffset`): `Promise`<{ `pageId`: `any` ; `revenue`: `any` ; `totals`: `any`  }[]\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `shop` | `any` |
| `startDate` | `any` |
| `endDate` | `any` |
| `timezoneOffset` | `any` |

#### Returns

`Promise`<{ `pageId`: `any` ; `revenue`: `any` ; `totals`: `any`  }[]\>

#### Defined in

[src/helpers/revenue.ts:94](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/revenue.ts#lines-94)
