[PF Server](../README.md) / util/p-throttle

# Module: util/p-throttle

## Table of contents

### Functions

- [asyncThrottle](util_p_throttle.md#asyncthrottle)
- [delay](util_p_throttle.md#delay)

## Functions

### asyncThrottle

▸ `Const` **asyncThrottle**<`Argument`, `ReturnValue`\>(`function_`): `ThrottledFunction`<`Argument`, `ReturnValue`\>

#### Type parameters

| Name | Type |
| :------ | :------ |
| `Argument` | extends readonly `unknown`[] |
| `ReturnValue` | `ReturnValue` |

#### Parameters

| Name | Type |
| :------ | :------ |
| `function_` | (...`arguments`: `Argument`) => `ReturnValue` |

#### Returns

`ThrottledFunction`<`Argument`, `ReturnValue`\>

#### Defined in

[src/util/p-throttle.ts:3](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/util/p-throttle.ts#lines-3)

___

### delay

▸ `Const` **delay**(`time?`): `Promise`<`unknown`\>

#### Parameters

| Name | Type | Default value |
| :------ | :------ | :------ |
| `time` | `number` | `100` |

#### Returns

`Promise`<`unknown`\>

#### Defined in

[src/util/p-throttle.ts:8](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/util/p-throttle.ts#lines-8)
