[PF Server](../README.md) / data/helpers/media

# Module: data/helpers/media

## Table of contents

### Interfaces

- [IMedia](../interfaces/data_helpers_media.IMedia.md)

### Functions

- [deleteMedia](data_helpers_media.md#deletemedia)
- [getMediaData](data_helpers_media.md#getmediadata)
- [sortByDate](data_helpers_media.md#sortbydate)
- [updateMediaData](data_helpers_media.md#updatemediadata)
- [uploadMedia](data_helpers_media.md#uploadmedia)

## Functions

### deleteMedia

▸ **deleteMedia**(`Shop`, `key`): `Promise`<`IAsset`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `Shop` | [`PFShop`](../classes/data_models_Shop.PFShop.md) |
| `key` | `any` |

#### Returns

`Promise`<`IAsset`\>

#### Defined in

[src/data/helpers/media.ts:120](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/helpers/media.ts#lines-120)

___

### getMediaData

▸ **getMediaData**(`Shop`): `Promise`<`IAsset`[]\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `Shop` | [`PFShop`](../classes/data_models_Shop.PFShop.md) |

#### Returns

`Promise`<`IAsset`[]\>

#### Defined in

[src/data/helpers/media.ts:91](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/helpers/media.ts#lines-91)

___

### sortByDate

▸ **sortByDate**(`arr?`): `any`[]

#### Parameters

| Name | Type | Default value |
| :------ | :------ | :------ |
| `arr` | `any`[] | `[]` |

#### Returns

`any`[]

#### Defined in

[src/data/helpers/media.ts:81](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/helpers/media.ts#lines-81)

___

### updateMediaData

▸ **updateMediaData**(`Shop`, `data`): `Promise`<`void`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `Shop` | [`PFShop`](../classes/data_models_Shop.PFShop.md) |
| `data` | `any` |

#### Returns

`Promise`<`void`\>

#### Defined in

[src/data/helpers/media.ts:111](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/helpers/media.ts#lines-111)

___

### uploadMedia

▸ **uploadMedia**(`Shop`, `asset`): `Promise`<`IAsset`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `Shop` | [`PFShop`](../classes/data_models_Shop.PFShop.md) |
| `asset` | `any` |

#### Returns

`Promise`<`IAsset`\>

#### Defined in

[src/data/helpers/media.ts:105](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/helpers/media.ts#lines-105)
