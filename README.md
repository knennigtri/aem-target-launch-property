<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Contents**

- [Example launch API for target tutorial](#example-launch-api-for-target-tutorial)
  - [Prerequisites](#prerequisites)
  - [How to use](#how-to-use)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Example launch API for target tutorial
This is an example postman project for using the Adobe Experience Platform Launch API. The example property created is based on the Experience League tutorial: https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/target/overview.html?lang=en.

This automates the creation of the final launch property for adding target onto an AEM website. 

> Note Adobe Experience Platform **Launch** has been rebranded to Adobe Experience Platform **Tags**. These terms may be used interchangably throughout this documentation.



## Prerequisites

* Have access to Adobe Experience Platform Tags (Launch)
* [Postman](https://www.postman.com/downloads/) is installed
* You will need to create is a postman environment with the [example.postman_environment.json](example.postman_environment.json). Directions to create this  file can be found in  [create-environment.md](create-environment.md).

## How to use

1. [Import](https://learning.postman.com/docs/getting-started/importing-and-exporting-data/#importing-data-into-postman) into Postman:
   1. postman_environment.json. If you don't have this file created, see the prerequisites.
   2. [example-launch-api-for-target-tutorial.postman_collection.json](example-launch-api-for-target-tutorial.postman_collection.json)
   3. [Run](https://learning.postman.com/docs/running-collections/intro-to-collection-runs/) the imported collection
2. If you would like to complete the entire usecase from the [Experience League tutorial]( https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/target/overview.html?lang=en) you will need to use the tutorial to:
   1. Create an AEM author/publish environment with the [WKND project](https://github.com/adobe/aem-guides-wknd) installed
   2. Create an IMS configuration for Launch in AEM (if you're using Cloud Service, this is auto created)
   3. Create a Launch configuration with the tag property created from this project
   4. Test the tag property on the publish environment website.