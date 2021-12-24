[PF Server](../README.md) / data/types/Block

# Module: data/types/Block

## Table of contents

### Variables

- [BlockType](data_types_Block.md#blocktype)

## Variables

### BlockType

• **BlockType**: ``"\ntype Block {\n  id: ID\n  html: String\n  css: String\n  js: String\n}\n\ninput BlockInput {\n  html: String!\n  css: String!\n  js: String!\n}\n\nextend type Query {\n  getBlock(id: ID): Block\n  fetchBlocks(query: JSON): [Block]\n}\n\nextend type Mutation {\n  createBlock(block: BlockInput): Block\n  updateBlock(id: ID, block: BlockInput): Block\n  removeBlock(id: ID): Block\n  deleteBlock(id: ID): Block\n}\n"``

#### Defined in

[src/data/types/Block.ts:1](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/types/Block.ts#lines-1)
