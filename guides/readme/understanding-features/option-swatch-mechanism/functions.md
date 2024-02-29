---
cover: https://insidescientific.com/wp-content/uploads/2020/08/Function-logo-600.jpg
coverY: 0
layout:
  cover:
    visible: true
    size: full
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Functions

### Front end

#### Get data

1. `getVariantOptions`: In this function, we initiate a BulkOperation mutation to retrieve all variant options from Shopify in the form of a JSON link. Subsequently, we organize this data by grouping it based on the option name key.
2. `fetchUserDefinedData`: This function retrieves data that the user previously edited from the PF database.
3. After having data from the above two functions, compare and update them to the global state is `VariantOptionStoreEmbed`

#### Update data

1. `standardizeDataBeforeSendingToServer, standardizeSomeDataBeforeSendingToServer`: Standardize user-defined data before transmitting it to the server by eliminating all deleted options and swatches. Additionally, restore the ID for variant options that may have been previously deleted.&#x20;
2. `saveAllData`: Update data standardized to the database.
3. `onAddedOptionName`: Define default values ​​for added options and add them to the database.
4. `onDeletedOptionName`: Delete the option swatch added to the database.
5. `syncDataOptionsFromShopify`: Compare the server's data with Shopify's data. Add status to each option swatch and each value of this option swatch.
6.  `getLastChosenValue, saveLastChosenValue, updateWebStorageFromServer`: Implement a caching mechanism to retain the last selected value of users, ensuring data preservation in case of sudden disconnection or when switching swatch types. This is achieved by maintaining an ARRAY named "preserve", which records user actions when altering a value. The use of this ARRAY serves as an efficient means to save and preserve data, contributing to optimization. Moreover, this data structure facilitates seamless integration with undo and redo functionalities.

    **Expected results**: When they change a value A (original value) to value B (last value) of a swatch, a record will be put to (the head of) preserve array. When users switch swatch to display, all swatch C values will be set to empty. If the user has the last value B of that swatch C, we return B, else we return the default value. When users reload the page, always return value A.

### Back end

1. `addSwatch`: Add once option swatch to the database.
2. `updateSwatch`: Update one option swatch to the database.
3. `deleteSwatch`: Delete one option swatch to the database.
4. `saveAll`: One-way sync, all changes locally will be applied to the server. First, find elements that are not included in client data anymore and remove them. Second, add and update all option swatches. Then call API to Shopify to update metafield with the key is `pfVariantSwatchesV2.`
