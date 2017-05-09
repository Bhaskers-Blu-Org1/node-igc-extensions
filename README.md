# README

<!-- Generated by documentation.js. Update this documentation by updating the source code. -->

## ibm-igc-extensions

Re-usable functions for extending IBM Information Governance Catalog (i.e. OpenIGC)

**Meta**

-   **license**: Apache-2.0

## AssetHandler

AssetHandler class -- for handling IGC Flow Documents (XML) with the purpose of creating or updating asset instances

**Examples**

```javascript
// create an XML flow document with a new asset instance
var igcext = require('ibm-igc-extensions');
var ah = new igcext.AssetHandler();
ah.addAsset('$MyBundle-ClassName', 'AssetInstanceName', '123', {
   "short_description": "This is a short description of my asset",
   "$newField": "This is the value for a field that only exists in this bundle (and class)"
});
```

### parseXML

Parses an XML flow document

**Parameters**

-   `xml` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** 

### getAssetName

Gets the name of an asset

**Parameters**

-   `asset` **Asset** 

Returns **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** 

### getAssetRID

Gets the RID of an asset

**Parameters**

-   `asset` **Asset** 

Returns **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** 

### getAssetById

Gets an asset by its unique flow XML ID (not RID)

**Parameters**

-   `id` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** 

Returns **Asset** 

### getAssetNameById

Gets the name of an asset based on its unique flow XML ID (not RID)

**Parameters**

-   `id` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** 

Returns **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** 

### getParentAssetId

Gets the ID of the parent (reference) of the provided asset

**Parameters**

-   `asset` **Asset** 

Returns **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** 

### getTableIdentity

Gets the identity string (externalID) for the provided database table

**Parameters**

-   `tblName` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** the name of the database table
-   `schemaId` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** the ID of the parent database schema

Returns **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** 

### getColumnIdentity

Gets the identity string (externalID) for the provided database column

**Parameters**

-   `colName` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** the name of the database column
-   `tableId` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** the ID of the parent database table

Returns **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** 

### getColumnIdentityFromTableIdentity

Gets the database column identity string (externalID) from an existing database table identity string

**Parameters**

-   `colName` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** the name of the database column
-   `tableIdentity` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** the identity string (externalID) of the parent database table

Returns **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** 

### addAsset

Adds an asset to the flow XML

**Parameters**

-   `className` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** the classname of the data type of the asset (e.g. ASCLModel.DatabaseField)
-   `name` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** the name of the asset
-   `xmlId` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** the unique ID of the asset within the XML flow document
-   `objAttrs` **[Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)** the attributes to set on this asset
-   `parentType` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)?** the classname of the asset's parent data type (e.g. ASCLModel.DatabaseTable)
-   `parentId` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)?** the unique ID of the asset's parent within the XML flow document

### addImportAction

Adds an import action to the flow XML (to actually create the assets)

**Parameters**

-   `completeAssetIDs` **[Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)>** an array of asset IDs that should be created & replaced (if they already exist)
-   `partialAssetIDs` **[Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)>?** an array of asset IDs that should be created if they do not exist; otherwise should be updated (i.e. children added)

### getCustomisedXML

Retrieves the flow XML, including any modifications that have been made (added assets)

Returns **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** the full XML of the flow document

## BundleHandler

BundleHandler class -- for handling IGC Bundle definitions with the purpose of creating or updating asset type definitions

**Examples**

```javascript
// create an OpenIGC bundle with a new asset type definition
var igcext = require('ibm-igc-extensions');
var bh = new igcext.BundleHandler('.../ibm-igc-x-json');
bh.createBundleZip(function(err, pathToZip) {
  console.log("The bundle zip file is here: " + pathToZip);
});
```

### constructor

Retrieves the flow XML, including any modifications that have been made (added assets)

**Parameters**

-   `basePath` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** the base path of the bundle to create (i.e. directory containing 'asset_type_descriptor.xml')

### generateLabels

Generates the default labels based on all of the default locale descriptions provided in the asset definition

### validateBundle

Does some basic validation of the bundle (e.g. ensuring all classes have icons and label translations)

**Parameters**

-   `logIssues` **[boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)** if true, any issues identified are console.log'd

Returns **[boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)** true if all checks pass, false otherwise

### createBundleZip

Retrieves the flow XML, including any modifications that have been made (added assets)

**Parameters**

-   `callback` **[bundleCallback](#bundlecallback)** callback that is invoked once ZIP file is created

## bundleCallback

This callback is invoked as the result of a bundle ZIP file being created, providing the path to the file.

Type: [Function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)

**Parameters**

-   `errorMessage` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** any error message, or null if no errors
-   `path` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** the file system path in which the ZIP file was created
