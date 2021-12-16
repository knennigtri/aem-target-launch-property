# Launch API requests used and tips for use

The collection [Tag property for Target tutorial using APIs.postman_collection.json](Tag property for Target tutorial using APIs.postman_collection.json) is made up of 6 groupings of requests. Each collection folder represents a grouping of typical actions that might need to be performed when creating different items within a tag property. These groupings include:
- [Adobe IO Token](#adobe-io-token)
- [Create Property](#create-property)
- [Add Extensions](#add-extensions)
- [Add Elements](#add-elements)
- [Add Rule - Target](#add-rule---target)
- [Publish Library](#publish-library)

# Header Variables

All requests in this collection use the same headers for authentication and use the values specified from the Postman environment.

```
Authorization:bearer {{access_token}}
x-api-key:{{CLIENT_ID}}
X-Gw-Ims-Org-Id:{{ORG_ID}}
Content-Type:application/vnd.api+json
Accept:application/vnd.api+json;revision=1
```

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

This folder creates the bare minimum of a tag property. Most of this folder is boilerplate objects for a property. 

### Properties

When you create a property using the API, it will be completely empty except for the `core` extension. 

**Request:**

```HTTP
POST {{HOST}}/companies/{{companyID}}/properties
```

**Required input vars:** `HOST`, `companyID`

**Saved vars after request:** `propID`

**Sample Body**: See the [Properties API](https://developer.adobelaunch.com/api/reference/1.0/properties/create/)

If you would like the tag to have a specific name, you will need to update the `body` in the **Create/Save property**:

``` JSON
{

  "data": {

    "attributes": {

      "name": "Launch with Target *{{PROPERTY_COUNT}}*",

      "domains": [

        "example.com"

      ],

      "platform": "web"

    },

    "type": "properties"

  }

}
```

> Note: {{PROPERTY_COUNT}} is  a simple counter to force a creation of a new property each time this request is run. See the  **pre-request Script** to see how it's implemented.

### Host

**Request:**

```HTTP
POST {{HOST}}/properties/{{propID}}/hosts
```

**Required input vars:** `HOST`, `propID`

**Saved vars after request:** `hostID`

**Sample Body**: See the [Hosts API](https://developer.adobelaunch.com/api/reference/1.0/hosts/create/)

### Environments

You can have 0 to many environments for a tag property. The bare minimum to publish your tag is 2: development and production.

**Request:**

```HTTP
POST {{HOST}}/properties/{{propID}}/environments
```

**Required input vars:** `HOST`, `propID`

**Saved vars after request:** `envID_<name>`

**Sample Body**: See the [Environments API](https://developer.adobelaunch.com/api/reference/1.0/environments/create/)



## Add Extensions

The `core` extension is the only extension that is created with the property. This means you need to add any other extensions you want to use. In order to do this though, you will need to know that extensions **extension package ID**. 

### Extension Packages

The **Get Extension Packages** request returns all installable packages and the **Tests** of the request saves the desired extension package IDs. If you are unsure what the data.attribute.name in **Tests** you can run the request first and search for the desired extension to get the correct name to save.

**Request:**

```HTTP
GET {{HOST}}/extension_packages?page[size]=999&sort=display_name&filter[platform]=EQ%20web,EQ%20null&max_availability=private
```

**Required input vars:** `HOST`

**Saved vars after request:** desired `extID` variables

**Sample Body**: See the [Extension Packages API](https://developer.adobelaunch.com/api/reference/1.0/extension_packages/list/)

### Extensions

>  **Golden rule:** The easiest way to create a request is to create it first in the UI and then do a GET request (see [Helper Requests.postman_collection.json](Helper Requests.postman_collection.json)) to see the `delegate_descriptor_id` and `settings` values.

**Request:**

```HTTP
POST {{HOST}}/properties/{{propID}}/extensions
```

**Required input vars:** `HOST`, `propID`, related `EXT_PACKAGE_ID` variables

**Saved vars after request:** `extID_<name>`

**Sample Body**: See the [Extensions API](https://developer.adobelaunch.com/api/reference/1.0/extensions/create/)


## Add Data Elements

>  **Golden rule:** The easiest way to create a request is to create it first in the UI and then do a GET request (see [Helper Requests.postman_collection.json](Helper Requests.postman_collection.json)) to see the `delegate_descriptor_id` and `settings` values.

**Request:**

```HTTP
POST {{HOST}}/properties/{{propID}}/data_elements
```

**Required input vars:** `HOST`, `propID`, related `extID` variables

**Saved vars after request:** `dataElementID_<name>`

**Sample Body**: See the [Data Elements API](https://developer.adobelaunch.com/api/reference/1.0/data_elements/create/)

### Escaping custom scripts

If you follow the golden rule, you might end up with a `settings` like

```json
"settings": "{\"source\":\"if(event \&\& event.id) {\\n    return event.id;\\n}\"}"
```

and you'll notice that it isn't valid JSON. To fix this, simply double escape the `&` symbol.
```json
"settings": "{\"source\":\"if(event \\&\\& event.id) {\\n    return event.id;\\n}\"}"
```

## Add Rule - Target

> **Golden rule:** The easiest way to create a request is to create it first in the UI and then do a GET request (see [Helper Requests.postman_collection.json](Helper Requests.postman_collection.json)) to see the `delegate_descriptor_id` and `settings` values.

A rule object is composed of 0 to many rule component objects. This means that after you create the rule object, you will need to create (and order) rule components to be related to the rule object. The **Rule - Target** request saves the ruleID so that the rule components can be related to the rule object.

**Request**:

```HTTP
POST {{HOST}}/properties/{{propID}}/rules
```

**Required input vars:** `HOST`, `propID`

**Saved vars after request:**`ruleID_Target`

**Sample Body**: See the [Rule API](https://developer.adobelaunch.com/api/reference/1.0/rules/create/)

### Rule Components

Rule components require a relationship to a ruleID and also the extensionID that the rule component is based on. The Events, Conditions, and Actions will occur based on the `order` value.

**Request**:

```HTTP
POST {{HOST}}/properties/{{propID}}/rule_components
```

**Required input vars:** `HOST`, `propID`, `ruleID_Target`, related `extID` variables

**Saved vars after request:** none

**Sample Body**: See the [Rule Components API](https://developer.adobelaunch.com/api/reference/1.0/rule_components/create/)



## Publish Library

The first request in this folder is by far the most complex of all the requests in this collection. The **Create Library** request dynamically builds the `body` to include all data elements, rules, and extensions in the create library request. This cuts down on a number of requests to add all objects to the library for publishing. The **pre-request Script** contains all the logic for dynamically building the body:

```javascript
var data_data_elements = [];
var data_rules = [];
var data_extensions = [];
// envVariables = pm.environment.toObject();
envVariables = pm.collectionVariables.toObject();

//Find all data elements, rules, and extensions in this property so they can be added to the Library
for (var key in envVariables){
    if(envVariables.hasOwnProperty(key)){
        if(key.includes("dataElementID")){
                var dEObj_data = new Object();
                dEObj_data.id = envVariables[key];
                dEObj_data.type = "data_elements";
                dEObj_data.meta = {};
                dEObj_data.meta.action = "revise";
                data_data_elements.push(JSON.stringify(dEObj_data));
        }
        if(key.includes("ruleID")){
                var ruleObj_data = new Object();
                ruleObj_data.id = envVariables[key];
                ruleObj_data.type = "rules";
                ruleObj_data.meta = {};
                ruleObj_data.meta.action = "revise";
                data_rules.push(JSON.stringify(ruleObj_data));
        }
        if(key.includes("extID")){
                var extObj_data = new Object();
                extObj_data.id = envVariables[key];
                extObj_data.type = "extensions";
                extObj_data.meta = {};
                extObj_data.meta.action = "revise";
                data_extensions.push(JSON.stringify(extObj_data));
        }
    }
}
//If there are data elements, create a JSON entry for them
var data_elementsObj = "";
if(data_data_elements.length != 0){
    data_elementsObj = `"data_elements": {
          "data": [`
            +data_data_elements+
          `]
        },`;
}
//If there are rules, create a JSON entry for them
var rulesObj = "";
if(data_rules.length != 0){
    rulesObj = `"rules": {
          "data": [`
            +data_rules+
          `]
        },`;
}
//If there are extensions, create a JSON entry for them
var extensionsObj = "";
if(data_extensions.length != 0){
    extensionsObj = `"extensions": {
          "data": [`
            +data_extensions+
          `]
        },`;
}
pm.globals.set("data_data_elements", data_elementsObj);
pm.globals.set("data_rules", rulesObj);
pm.globals.set("data_extensions", extensionsObj);
```

**Requests**

This request chain follows the simplest path to publishing a tag into production. These steps are documented in the [Library Transitions API](https://developer.adobelaunch.com/api/reference/1.0/libraries/transition/#)

1. Create the Library

```HTTP
POST {{HOST}}/properties/{{propID}}/libraries
```
2. Build the library into the dev environment

```HTTP
POST {{HOST}}/libraries/{{libraryID}}/builds
```
3. Submit the  library
```HTTP
PATCH {{HOST}}/libraries/{{libraryID}}
```
4. Approve the library
```HTTP
PATCH {{HOST}}/libraries/{{libraryID}}
```
5. Move the library to production
```HTTP
POST {{HOST}}/libraries/{{libraryID}}/relationships/environment
```
6. Publish the library
```HTTP
POST {{HOST}}/libraries/{{libraryID}}/builds
```

**Required input vars:** `HOST`, `propID`, `libraryID`, related `envID` variables, all `dataElementIDs`, `ruleIDs`, and `extensionIDs`

**Saved vars after request:** none

**Sample Body**: See the [Library API](https://developer.adobelaunch.com/api/reference/1.0/libraries/create/0)

