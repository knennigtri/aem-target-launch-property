# Postman Environments
These allow for connection and configuration of a experience cloud product or service.

## Create an IO project
 1. Go to https://console.adobe.io/home
 2. Create a new project. Name the project unique to this connection so that it's easy to understand what it's used for.
 3. Click **Add to Project > API**
 4. Under Adobe Experience Platform, select **Experience Platform Launch API** and **Next**
 5. Select Option 1 **Generate a key pair**
> It's worth noting that in the long term, all Adobe IO credentials could use the same keypair credentials.
 5. Generate the keypair and download
 6. **Next**
 7. Select the **Launch - Everything** profile
 4. Go to the Credentials > Service Account (JWT)

## Create the postman environment JSON
 1. Copy the example.postman_environment.json  file in this folder.
 2. Rename it so it's unique to the AEC organization
 3. From The **Credentials details** screen, copy the following values into their respective values in the environment JSON:
    1. CLIENT_ID (Client ID)
    2. CLIENT_SECRET (Client Secret)
    3. TECHNICAL_ACCOUNT (Technical Account ID)
    4. ORG_ID (Organization ID)
 4. Next, open the private key you downloaded earlier in a text editor. Copy the entire text.
    1. In the environment JSON paste the private key value into the **PRIVATE_KEY** value
 5. Save

## Upload the environment JSON to Postman
https://testfully.io/blog/import-from-postman/#import-postman-environments 
