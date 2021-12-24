[PF Server](../README.md) / data/models/Section

# Module: data/models/Section

## Table of contents

### Namespaces

- [&lt;internal\&gt;](data_models_Section._internal_.md)

### Variables

- [Section](data_models_Section.md#section)

### Functions

- [createSection](data_models_Section.md#createsection)
- [fetchSections](data_models_Section.md#fetchsections)
- [getSection](data_models_Section.md#getsection)
- [removeSection](data_models_Section.md#removesection)
- [updateSectionName](data_models_Section.md#updatesectionname)

## Variables

### Section

• **Section**: `Model`<`any`, {}, {}, {}\>

#### Defined in

[src/data/models/Section.ts:32](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Section.ts#lines-32)

## Functions

### createSection

▸ **createSection**(`section`, `request`): `Promise`<`unknown`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `section` | [`SectionType`](../interfaces/data_models_Section._internal_.SectionType.md) |
| `request` | `any` |

#### Returns

`Promise`<`unknown`\>

#### Defined in

[src/data/models/Section.ts:35](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Section.ts#lines-35)

___

### fetchSections

▸ **fetchSections**(`request`): `Promise`<`unknown`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `request` | `any` |

#### Returns

`Promise`<`unknown`\>

#### Defined in

[src/data/models/Section.ts:63](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Section.ts#lines-63)

___

### getSection

▸ **getSection**(`id`): `Promise`<`unknown`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `id` | `string` |

#### Returns

`Promise`<`unknown`\>

#### Defined in

[src/data/models/Section.ts:79](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Section.ts#lines-79)

___

### removeSection

▸ **removeSection**(`id`): `Promise`<`unknown`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `id` | `string` |

#### Returns

`Promise`<`unknown`\>

#### Defined in

[src/data/models/Section.ts:104](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Section.ts#lines-104)

___

### updateSectionName

▸ **updateSectionName**(`id`, `name`): `Promise`<`unknown`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `id` | `any` |
| `name` | `any` |

#### Returns

`Promise`<`unknown`\>

#### Defined in

[src/data/models/Section.ts:91](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Section.ts#lines-91)
