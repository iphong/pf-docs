[PF Server](../README.md) / data/types/Item

# Module: data/types/Item

## Table of contents

### Variables

- [ItemsType](data_types_Item.md#itemstype)

## Variables

### ItemsType

• **ItemsType**: ``"\n\ttype Item {\n\t\t_id: String!\n        type: String!\n        children: [String]\n        styles: [String]\n        data: JSON\n        options: JSON\n\t}\n\n\tinput ItemInput {\n\t    _id: String!\n\t    roomId: String\n\t    type: String!\n\t    children: [String]\n\t    styles: [String]\n\t    data: JSON\n\t    options: JSON\n\t}\n\n\textend type Query {\n        getItem(id: String): Item\n\t}\n\n\textend type Mutation {\n\t\tupdateItem(input: ItemInput!): Item\n\t}\n\n"``

#### Defined in

[src/data/types/Item.ts:1](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/types/Item.ts#lines-1)
