<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Contents**

- [Tag property for Target tutorial using APIs](#tag-property-for-target-tutorial-using-apis)
  - [Helpful resources](#helpful-resources)
  - [Prerequisites](#prerequisites)
  - [How to use](#how-to-use)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Tag property for Target tutorial using APIs
This is an postman project to build the tag property created in [Adobe Experience League Target tutorial](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/target/overview.html?lang=en) using the Launch API. This automates the creation of the final launch property for adding target onto an AEM website. 

> This process has been reimaged as a generic import/export process for any launch property and **this project will no longer be updated.** The new import/export tool can be found in the [launch-api-automations](https://github.com/knennigtri/launch-api-automation) project. This git project can still be used as a POC for creating various requests using the Launch API.

> Note: Adobe Experience Platform **Launch** has been rebranded to Adobe Experience Platform **Tags**. These terms may be used interchangably throughout this documentation.

## Helpful resources
 * Checkout [requests-and-tips.md](requests-and-tips.md) to learn more about each of the requests and their caveats.
 * Use the [Helper Requests.postman_collection.json](Helper%20Requests.postman_collection.json) to run GET requests to list properties, data elements, rules, extensions, and more.
 * [Reactor (Tags) API](https://developer.adobelaunch.com/api/) reference

## Prerequisites

* Have access to Adobe Experience Platform Tags (Launch)
* [Postman](https://www.postman.com/downloads/) is installed
* You will need to create is a postman environment with the [example.postman_environment.json](example.postman_environment.json). Directions to create this  file can be found in  [create-environment.md](create-environment.md).

## How to use

1. [Import](https://learning.postman.com/docs/getting-started/importing-and-exporting-data/#importing-data-into-postman) into Postman:
   1. postman_environment.json. If you don't have this file created, see the prerequisites.
   2. [Tag property for Target tutorial using APIs.postman_collection.json](Tag%20property%20for%20Target%20tutorial%20using%20APIs.postman_collection.json)
   3. [Run](https://learning.postman.com/docs/running-collections/intro-to-collection-runs/) the imported collection
2. If you would like to complete the entire usecase from the [Experience League tutorial]( https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/target/overview.html?lang=en) you will need to use the tutorial to:
   1. Create an AEM author/publish environment with the [WKND project](https://github.com/adobe/aem-guides-wknd) installed
   2. Create an IMS configuration for Launch in AEM (if you're using Cloud Service, this is auto created)
   3. Create a Launch configuration with the tag property created from this project
   4. Test the tag property on the publish environment website.