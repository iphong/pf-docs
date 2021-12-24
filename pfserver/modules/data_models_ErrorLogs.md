[PF Server](../README.md) / data/models/ErrorLogs

# Module: data/models/ErrorLogs

## Table of contents

### Variables

- [ErrorLogModel](data_models_ErrorLogs.md#errorlogmodel)

### Functions

- [addErrorFeedback](data_models_ErrorLogs.md#adderrorfeedback)

## Variables

### ErrorLogModel

• **ErrorLogModel**: `Model`<`any`, {}, {}, {}\>

#### Defined in

[src/data/models/ErrorLogs.ts:13](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/ErrorLogs.ts#lines-13)

## Functions

### addErrorFeedback

▸ **addErrorFeedback**(`type`, `content`, `shopDomain?`, `description?`, `status?`): `void`

#### Parameters

| Name | Type | Default value |
| :------ | :------ | :------ |
| `type` | `any` | `undefined` |
| `content` | `any` | `undefined` |
| `shopDomain` | `string` | `'anonymous'` |
| `description` | `string` | `''` |
| `status` | `string` | `'active'` |

#### Returns

`void`

#### Defined in

[src/data/models/ErrorLogs.ts:16](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/ErrorLogs.ts#lines-16)
