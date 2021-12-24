[PF Server](../README.md) / data/types/Root

# Module: data/types/Root

## Table of contents

### Variables

- [Root](data_types_Root.md#root)

## Variables

### Root

• **Root**: ``"\n\t# The dummy queries and mutations are necessary because\n\t# graphql-js cannot have empty root types and we only extend\n\t# these types later on\n\t# Ref: apollographql/graphql-tools#293\n\ttype Query {\n\t\tdummy: String\n\t}\n\n\ttype Mutation {\n\t\tdummy: String\n\t}\n\n\ttype Subscription {\n\t\tdummy: String\n\t}\n\n\tschema {\n\t\tquery: Query\n\t\tmutation: Mutation\n\t\tsubscription: Subscription\n\t}\n"``

#### Defined in

[src/data/types/Root.ts:1](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/types/Root.ts#lines-1)
