[PF Server](../README.md) / [handlers/events](../modules/handlers_events.md) / [<internal\>](../modules/handlers_events._internal_.md) / EventsBus

# Class: EventsBus

[handlers/events](../modules/handlers_events.md).[<internal>](../modules/handlers_events._internal_.md).EventsBus

## Hierarchy

- `EventEmitter`

  ↳ **`EventsBus`**

## Table of contents

### Constructors

- [constructor](handlers_events._internal_.EventsBus.md#constructor)

### Properties

- [clients](handlers_events._internal_.EventsBus.md#clients)
- [counter](handlers_events._internal_.EventsBus.md#counter)

### Methods

- [middleware](handlers_events._internal_.EventsBus.md#middleware)
- [send](handlers_events._internal_.EventsBus.md#send)

## Constructors

### constructor

• **new EventsBus**(`options?`)

#### Parameters

| Name | Type |
| :------ | :------ |
| `options?` | `EventEmitterOptions` |

#### Inherited from

EventEmitter.constructor

#### Defined in

node_modules/@types/node/events.d.ts:19

## Properties

### clients

• **clients**: `Map`<`string`, `Map`<`Request`<`ParamsDictionary`, `any`, `any`, `ParsedQs`, `Record`<`string`, `any`\>\>, `Response`<`any`, `Record`<`string`, `any`\>\>\>\>

#### Defined in

[src/handlers/events.ts:7](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/handlers/events.ts#lines-7)

___

### counter

• **counter**: `number` = `0`

#### Defined in

[src/handlers/events.ts:6](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/handlers/events.ts#lines-6)

## Methods

### middleware

▸ **middleware**(`req`, `res`): `void`

#### Parameters

| Name | Type |
| :------ | :------ |
| `req` | `Request`<`ParamsDictionary`, `any`, `any`, `ParsedQs`, `Record`<`string`, `any`\>\> |
| `res` | `Response`<`any`, `Record`<`string`, `any`\>\> |

#### Returns

`void`

#### Defined in

[src/handlers/events.ts:9](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/handlers/events.ts#lines-9)

___

### send

▸ **send**(`shop`, `event`, `data`): `void`

#### Parameters

| Name | Type |
| :------ | :------ |
| `shop` | `string` |
| `event` | `string` |
| `data` | `any` |

#### Returns

`void`

#### Defined in

[src/handlers/events.ts:33](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/handlers/events.ts#lines-33)
