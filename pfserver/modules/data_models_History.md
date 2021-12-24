[PF Server](../README.md) / data/models/History

# Module: data/models/History

## Table of contents

### Functions

- [addHistoryToDB](data_models_History.md#addhistorytodb)
- [deleteHistoryById](data_models_History.md#deletehistorybyid)
- [deleteHistoryOlderThanOneYear](data_models_History.md#deletehistoryolderthanoneyear)
- [getHistoryById](data_models_History.md#gethistorybyid)
- [getHistoryByPageId](data_models_History.md#gethistorybypageid)
- [removeHistoryByPageId](data_models_History.md#removehistorybypageid)

## Functions

### addHistoryToDB

▸ **addHistoryToDB**(`data`): `Promise`<[`HistoryType`](data_models_types.md#historytype)\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `data` | [`IHistory`](../interfaces/data_models_types.IHistory.md) |

#### Returns

`Promise`<[`HistoryType`](data_models_types.md#historytype)\>

#### Defined in

[src/data/models/History.ts:19](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/History.ts#lines-19)

___

### deleteHistoryById

▸ **deleteHistoryById**(`_id`): `Promise`<`boolean`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `_id` | `string` |

#### Returns

`Promise`<`boolean`\>

#### Defined in

[src/data/models/History.ts:99](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/History.ts#lines-99)

___

### deleteHistoryOlderThanOneYear

▸ **deleteHistoryOlderThanOneYear**(`limitHistory?`, `historyTimeRange?`): `Promise`<[`HistoryType`](data_models_types.md#historytype)[]\>

#### Parameters

| Name | Type | Default value |
| :------ | :------ | :------ |
| `limitHistory` | `number` | `200` |
| `historyTimeRange` | `number` | `365` |

#### Returns

`Promise`<[`HistoryType`](data_models_types.md#historytype)[]\>

#### Defined in

[src/data/models/History.ts:32](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/History.ts#lines-32)

___

### getHistoryById

▸ **getHistoryById**(`_id`): `Promise`<[`IHistory`](../interfaces/data_models_types.IHistory.md)\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `_id` | `string` |

#### Returns

`Promise`<[`IHistory`](../interfaces/data_models_types.IHistory.md)\>

#### Defined in

[src/data/models/History.ts:87](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/History.ts#lines-87)

___

### getHistoryByPageId

▸ **getHistoryByPageId**(`pageId`): `Promise`<[`HistoryType`](data_models_types.md#historytype)[]\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `pageId` | `any` |

#### Returns

`Promise`<[`HistoryType`](data_models_types.md#historytype)[]\>

#### Defined in

[src/data/models/History.ts:72](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/History.ts#lines-72)

___

### removeHistoryByPageId

▸ **removeHistoryByPageId**(`pageId`): `Promise`<`boolean`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `pageId` | `any` |

#### Returns

`Promise`<`boolean`\>

#### Defined in

[src/data/models/History.ts:111](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/History.ts#lines-111)
