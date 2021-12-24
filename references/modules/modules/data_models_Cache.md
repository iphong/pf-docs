[PF Server](../README.md) / data/models/Cache

# Module: data/models/Cache

## Table of contents

### Namespaces

- [&lt;internal\&gt;](data_models_Cache._internal_.md)

### Variables

- [CacheModel](data_models_Cache.md#cachemodel)

### Functions

- [getCacheByQueryString](data_models_Cache.md#getcachebyquerystring)
- [setCache](data_models_Cache.md#setcache)

## Variables

### CacheModel

• **CacheModel**: `Model`<[`CacheDocument`](../interfaces/data_models_Cache._internal_.CacheDocument.md), {}, {}, {}\>

#### Defined in

[src/data/models/Cache.ts:18](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Cache.ts#lines-18)

## Functions

### getCacheByQueryString

▸ `Const` **getCacheByQueryString**(`query`): `Promise`<[`CacheDocument`](../interfaces/data_models_Cache._internal_.CacheDocument.md)\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `query` | `string` |

#### Returns

`Promise`<[`CacheDocument`](../interfaces/data_models_Cache._internal_.CacheDocument.md)\>

#### Defined in

[src/data/models/Cache.ts:21](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Cache.ts#lines-21)

___

### setCache

▸ `Const` **setCache**(`query`, `data`): `Promise`<`unknown`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `query` | `string` |
| `data` | `any` |

#### Returns

`Promise`<`unknown`\>

#### Defined in

[src/data/models/Cache.ts:33](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Cache.ts#lines-33)
