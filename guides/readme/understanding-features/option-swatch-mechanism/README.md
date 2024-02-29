# Option Swatch Mechanism

### Overview

|                              |                                                                                                                                                                                                                                                                                                                              |
| ---------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|                              |                                                                                                                                                                                                                                                                                                                              |
| Specs                        | [https://www.figma.com/file/8DVP2p5fqq2ImHPMh0oQk4/Design-proposal-for-PageFly-embedded-app?type=design\&node-id=417-53179\&mode=design\&t=I8KQOqpSlcbiW6xC-0](https://www.figma.com/file/8DVP2p5fqq2ImHPMh0oQk4/Design-proposal-for-PageFly-embedded-app?type=design\&node-id=417-53179\&mode=design\&t=I8KQOqpSlcbiW6xC-0) |
| Contributors you can contact | Aiya                                                                                                                                                                                                                                                                                                                         |

### Mechanism

#### Get data

1. `getVariantOptions`: In this function, we run a BulkOperation mutation to get all the variant options from Shopify as a JSON link. Then we group this data by key is the option name.
2. `fetchUserDefinedData`: This function retrieves data that the user previously edited from the PF database.
3. After having data from the above two functions, compare and update them to the global state is `VariantOptionStoreEmbed`

#### Update data

1. `standardizeDataBeforeSendingToServer, standardizeSomeDataBeforeSendingToServer`: Standardize user-defined data before sending it to the server. Remove all deleted options and swatches. Add the ID back for the variant option that might have been deleted.&#x20;
2. `saveAllData`: Update data standardized to the database.
3. `onAddedOptionName`: Define default values ​​for added options and add them to the database.
4. `onDeletedOptionName`: Delete the option swatch added to the database.
5. `syncDataOptionsFromShopify`: Compare the server's data with Shopify's data. Add status to each option swatch and each value of this option swatch.
6.  `getLastChosenValue, saveLastChosenValue, updateWebStorageFromServer`: Cache the last value selection of users so that when they suddenly lose connection or switch swatch type, data is preserved. We create an ARRAY of preserve which represents the actions of users when they change a value. We use ARRAY to save and preserve data for optimizing purposes. Further, we can better integrate undo redo with this data structure.&#x20;

    **Expected results**: When they change a value A (original value) to value B (last value) of a swatch, a record will be put to (the head of) preserve array. When users switch swatch to display, all swatch C values will be set to empty. If the user has the last value B of that swatch C, we return B, else we return the default value. When users reload the page, always return value A.

