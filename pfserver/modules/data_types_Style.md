[PF Server](../README.md) / data/types/Style

# Module: data/types/Style

## Table of contents

### Variables

- [StylesType](data_types_Style.md#stylestype)

## Variables

### StylesType

• **StylesType**: ``"\n\ttype Style {\n\t\t_id: String!,\n        type: String!,\n        styles: JSON!,\n\t}\n\n\tinput StyleInput {\n\t    _id: String!\n\t    type: String!\n\t    styles: JSON!\n\t}\n\n\textend type Query {\n        getStyle(id: String): Style\n\t}\n\n\textend type Mutation {\n\t\tupdateStyle(input: StyleInput!): Style\n\t}\n\n"``

#### Defined in

[src/data/types/Style.ts:1](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/types/Style.ts#lines-1)
