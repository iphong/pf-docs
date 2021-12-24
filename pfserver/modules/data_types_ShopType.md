[PF Server](../README.md) / data/types/ShopType

# Module: data/types/ShopType

## Table of contents

### Variables

- [ShopType](data_types_ShopType.md#shoptype)

## Variables

### ShopType

• **ShopType**: ``"\n\ttype Shop {\n\t\t_id: ID!\n\t\tshopDomain: String!\n\t\taccessToken: String!\n\t\tcreatedAt: Date\n\t\tlastAccess: Date\n\t\tuninstallAt: Date\n\t\tclosedStore: Boolean\n\t\tfavoriteFonts: [String]\n\t\tmetadata: JSON\n\t\tpageflyMeta: JSON\n\t}\n\ttype ShopScriptTags {\n\t\tid: ID!\n\t}\n\textend type Query {\n        shop: Shop\n\t}\n\tinput ShopInput {\n\t\tcreatedAt: Date\n\t\tlastAccess: Date\n\t\tuninstallAt: Date\n\t\tclosedStore: Boolean\n\t\tfavoriteFonts: [String]\n\t}\n\n\tinput PageFlyMetaInput {\n\t    visits: String\n\t    dashboardVisits: String\n\t\tstorefrontPassword: String\n\t\tacceptGDPR: Boolean\n\t\tacceptTracking: Boolean\n\t\tforceRemoveData: Boolean\n\t\treferralCode: String\n\t\tlandingPage: String\n\t\tpercentageDiscount: String\n\t\taffectedPlans: JSON\n\t\tcouponCode: String\n\t\tacceptGATracking: Boolean\n\t\tacceptCrisp: Boolean\n\t\tacceptCookies: Boolean\n\t}\n\n\ttype PageFlyMeta {\n\t    visits: String\n\t    dashboardVisits: String\n\t\tstorefrontPassword: String\n\t\tacceptGDPR: Boolean\n\t\tacceptTracking: Boolean\n\t\tforceRemoveData: Boolean\n\t\tacceptGATracking: Boolean\n\t\tacceptCrisp: Boolean\n\t\tacceptCookies: Boolean\n\t}\n\n\textend type Mutation {\n\t    updateShop(shopInput: ShopInput!): Shop\n\t    updatePageFlyMeta(pageflyMeta: PageFlyMetaInput!): PageFlyMeta\n\t}\n"``

#### Defined in

[src/data/types/ShopType.ts:1](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/data/types/ShopType.ts#lines-1)
