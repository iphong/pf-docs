[PF Server](../README.md) / data/models/Notification

# Module: data/models/Notification

## Table of contents

### Namespaces

- [&lt;internal\&gt;](data_models_Notification._internal_.md)

### Variables

- [Notification](data_models_Notification.md#notification)

### Functions

- [addNotification](data_models_Notification.md#addnotification)
- [getNotiById](data_models_Notification.md#getnotibyid)
- [getNotiByShop](data_models_Notification.md#getnotibyshop)
- [getNotiByTypeAndShop](data_models_Notification.md#getnotibytypeandshop)

## Variables

### Notification

• **Notification**: `Model`<[`INotificationSchema`](../interfaces/data_models_Notification._internal_.INotificationSchema.md), {}, {}, {}\>

#### Defined in

[src/data/models/Notification.ts:18](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Notification.ts#lines-18)

## Functions

### addNotification

▸ **addNotification**(`notificationData`): `Promise`<`void` \| [`INotificationSchema`](../interfaces/data_models_Notification._internal_.INotificationSchema.md) & {}\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `notificationData` | `any` |

#### Returns

`Promise`<`void` \| [`INotificationSchema`](../interfaces/data_models_Notification._internal_.INotificationSchema.md) & {}\>

#### Defined in

[src/data/models/Notification.ts:56](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Notification.ts#lines-56)

___

### getNotiById

▸ **getNotiById**(`id`): `Promise`<`unknown`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `id` | `any` |

#### Returns

`Promise`<`unknown`\>

#### Defined in

[src/data/models/Notification.ts:20](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Notification.ts#lines-20)

___

### getNotiByShop

▸ **getNotiByShop**(`shopDomain`): `Promise`<`unknown`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `shopDomain` | `any` |

#### Returns

`Promise`<`unknown`\>

#### Defined in

[src/data/models/Notification.ts:44](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Notification.ts#lines-44)

___

### getNotiByTypeAndShop

▸ **getNotiByTypeAndShop**(`type`, `shopDomain`): `Promise`<`unknown`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `type` | `any` |
| `shopDomain` | `any` |

#### Returns

`Promise`<`unknown`\>

#### Defined in

[src/data/models/Notification.ts:32](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/models/Notification.ts#lines-32)
