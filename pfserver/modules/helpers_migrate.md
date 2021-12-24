[PF Server](../README.md) / helpers/migrate

# Module: helpers/migrate

## Table of contents

### Variables

- [oldAppUrl](helpers_migrate.md#oldappurl)

### Functions

- [generateNewPageFromOld](helpers_migrate.md#generatenewpagefromold)
- [importOldPages](helpers_migrate.md#importoldpages)
- [queryOldApp](helpers_migrate.md#queryoldapp)
- [updateOldPageToDatabase](helpers_migrate.md#updateoldpagetodatabase)

## Variables

### oldAppUrl

• **oldAppUrl**: `string`

#### Defined in

[src/helpers/migrate.ts:9](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/migrate.ts#lines-9)

## Functions

### generateNewPageFromOld

▸ **generateNewPageFromOld**(`page`): `Promise`<`any`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `page` | `any` |

#### Returns

`Promise`<`any`\>

#### Defined in

[src/helpers/migrate.ts:30](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/migrate.ts#lines-30)

___

### importOldPages

▸ **importOldPages**(`req`, `res`): `Promise`<`void`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `any` |
| `res` | `any` |

#### Returns

`Promise`<`void`\>

#### Defined in

[src/helpers/migrate.ts:135](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/migrate.ts#lines-135)

___

### queryOldApp

▸ **queryOldApp**(`query`): `Promise`<`any`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `query` | `any` |

#### Returns

`Promise`<`any`\>

#### Defined in

[src/helpers/migrate.ts:12](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/migrate.ts#lines-12)

___

### updateOldPageToDatabase

▸ **updateOldPageToDatabase**(`data`): `Promise`<`void`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `data` | `any` |

#### Returns

`Promise`<`void`\>

#### Defined in

[src/helpers/migrate.ts:115](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/migrate.ts#lines-115)
