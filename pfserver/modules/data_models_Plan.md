[PF Server](../README.md) / data/models/Plan

# Module: data/models/Plan

## Table of contents

### References

- [default](data_models_Plan.md#default)

### Variables

- [PlanModel](data_models_Plan.md#planmodel)

### Functions

- [getPlanByShop](data_models_Plan.md#getplanbyshop)
- [updatePlan](data_models_Plan.md#updateplan)

## References

### default

Renames and re-exports [PlanModel](data_models_Plan.md#planmodel)

## Variables

### PlanModel

• **PlanModel**: `Model`<[`PlanModelType`](data_models_types.md#planmodeltype), {}, {}, {}\>

#### Defined in

[src/data/models/Plan.ts:31](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Plan.ts#lines-31)

## Functions

### getPlanByShop

▸ **getPlanByShop**(`shopDomain`): `Promise`<[`IPlan`](../interfaces/data_models_types.IPlan.md)\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `shopDomain` | `any` |

#### Returns

`Promise`<[`IPlan`](../interfaces/data_models_types.IPlan.md)\>

#### Defined in

[src/data/models/Plan.ts:34](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Plan.ts#lines-34)

___

### updatePlan

▸ **updatePlan**(`shopDomain`, `plan?`): `Promise`<[`IPlan`](../interfaces/data_models_types.IPlan.md)\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `shopDomain` | `any` |
| `plan` | `Object` |

#### Returns

`Promise`<[`IPlan`](../interfaces/data_models_types.IPlan.md)\>

#### Defined in

[src/data/models/Plan.ts:49](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Plan.ts#lines-49)
