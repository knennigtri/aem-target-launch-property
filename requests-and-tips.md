# Launch API requests used and tips for use

The collection [Tag property for Target tutorial using APIs.postman_collection.json](Tag property for Target tutorial using APIs.postman_collection.json) is made up of 6 groupings of requests. Each collection folder represents a grouping of typical actions that might need to be performed when creating different items within a tag property. These groupings include:
- [Adobe IO Token](#adobe-io-token)
- [Create Property](#create-property)
- [Add Extensions](#add-extensions)
- [Add Elements](#add-elements)
- [Add Rule - Target](#add-rule---target)
- [Publish Library](#publish-library)

## Collection Variables

[Collection variables](https://learning.postman.com/docs/sending-requests/variables/) are used to keep auto-generated values in scope of this collection. You will notice throughout the pre-request scripts and tests that these two methods are used to set/get the collection variables:

``` javascript
//setter and getter
pm.collectionVariables.set("variable_key", "variable_value");
pm.collectionVariables.get("variable_key");

//Itergate over all collection variables
var varObject = pm.collectionVariables.toObject()
for (var key in varObject){
	console.log(varObject[key]);
}
```

## Adobe IO Token

This folder generates an access_token to use for all subsequent requests. Alternatively this access key could be created by uploading the private.key to the Adobe IO project under the JWT credentials tab. The `access_token` is stored as a collection variable. 



## Create Property

TBD



## Add Extensions

TBD



## Add Elements

TBD



## Add Rule - Target

TBD



## Publish Library

TBD