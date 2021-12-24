[PF Server](../README.md) / data/types/Section

# Module: data/types/Section

## Table of contents

### Variables

- [SectionType](data_types_Section.md#sectiontype)

## Variables

### SectionType

• **SectionType**: ``"\n  type Section {\n    id: ID\n    name: String!\n    image: String!\n    shopDomain: String!\n    selectedFonts: JSON\n    data: [JSON]\n    isOld: Boolean\n  }\n\n  input SectionInput {\n    name: String!\n    image: String!\n    shopDomain: String!\n    data: [JSON]\n    selectedFonts: JSON\n  }\n\n  extend type Query {\n    getSection(id: ID): Section\n    fetchSections(shopDomain: String): [Section]\n  }\n\n  extend type Mutation {\n    createSection(section: SectionInput): Section\n    updateSectionName(id: ID, name: String): Section\n    removeSection(id: ID): Section\n  }\n"``

#### Defined in

[src/data/types/Section.ts:1](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/types/Section.ts#lines-1)
