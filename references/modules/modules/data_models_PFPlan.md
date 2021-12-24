[PF Server](../README.md) / data/models/PFPlan

# Module: data/models/PFPlan

## Table of contents

### Type aliases

- [IPFPlanModel](data_models_PFPlan.md#ipfplanmodel)

### Variables

- [PFDefaultPlans](data_models_PFPlan.md#pfdefaultplans)
- [PFPlanModel](data_models_PFPlan.md#pfplanmodel)

### Functions

- [findPFPlan](data_models_PFPlan.md#findpfplan)
- [getListPFPlan](data_models_PFPlan.md#getlistpfplan)
- [getPFPlanByPlanID](data_models_PFPlan.md#getpfplanbyplanid)
- [saveDefaultPlanDataToDB](data_models_PFPlan.md#savedefaultplandatatodb)
- [updateDefaultPlanData](data_models_PFPlan.md#updatedefaultplandata)
- [updateDiscount](data_models_PFPlan.md#updatediscount)

## Type aliases

### IPFPlanModel

Ƭ **IPFPlanModel**: [`IPFPlan`](../interfaces/data_models_types.IPFPlan.md) & `Document`

#### Defined in

[src/data/models/PFPlan.ts:4](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/PFPlan.ts#lines-4)

## Variables

### PFDefaultPlans

• **PFDefaultPlans**: [`IPFPlan`](../interfaces/data_models_types.IPFPlan.md)[]

#### Defined in

[src/data/models/PFPlan.ts:31](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/PFPlan.ts#lines-31)

___

### PFPlanModel

• **PFPlanModel**: `Model`<[`IPFPlanModel`](data_models_PFPlan.md#ipfplanmodel), {}, {}, {}\>

#### Defined in

[src/data/models/PFPlan.ts:29](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/PFPlan.ts#lines-29)

## Functions

### findPFPlan

▸ **findPFPlan**(`condition`): `Promise`<[`IPFPlan`](../interfaces/data_models_types.IPFPlan.md)\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `condition` | `any` |

#### Returns

`Promise`<[`IPFPlan`](../interfaces/data_models_types.IPFPlan.md)\>

#### Defined in

[src/data/models/PFPlan.ts:179](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/PFPlan.ts#lines-179)

___

### getListPFPlan

▸ **getListPFPlan**(): `Promise`<[`IPFPlan`](../interfaces/data_models_types.IPFPlan.md)[]\>

#### Returns

`Promise`<[`IPFPlan`](../interfaces/data_models_types.IPFPlan.md)[]\>

#### Defined in

[src/data/models/PFPlan.ts:144](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/PFPlan.ts#lines-144)

___

### getPFPlanByPlanID

▸ **getPFPlanByPlanID**(`planId`): `Promise`<[`IPFPlan`](../interfaces/data_models_types.IPFPlan.md)\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `planId` | `any` |

#### Returns

`Promise`<[`IPFPlan`](../interfaces/data_models_types.IPFPlan.md)\>

#### Defined in

[src/data/models/PFPlan.ts:156](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/PFPlan.ts#lines-156)

___

### saveDefaultPlanDataToDB

▸ **saveDefaultPlanDataToDB**(): `Promise`<`void`\>

#### Returns

`Promise`<`void`\>

#### Defined in

[src/data/models/PFPlan.ts:129](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/PFPlan.ts#lines-129)

___

### updateDefaultPlanData

▸ **updateDefaultPlanData**(`req`, `res`): `void`

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `any` |
| `res` | `any` |

#### Returns

`void`

#### Defined in

[src/data/models/PFPlan.ts:168](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/PFPlan.ts#lines-168)

___

### updateDiscount

▸ `Const` **updateDiscount**(`planId`, `shop`): `Promise`<`unknown`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `planId` | `any` |
| `shop` | `any` |

#### Returns

`Promise`<`unknown`\>

#### Defined in

[src/data/models/PFPlan.ts:192](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/PFPlan.ts#lines-192)
