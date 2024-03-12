# API Access Key

## **ADMIN ONLY**

Only the administrator can generate the API key and secret. The steps for doing this is as follows.

Keycloak console will be available at `https://<host-name>/auth`.  The admin will log in using the username and password secret.

### Step 1: Import Realm (If not already done)

1. Open the Keycloak console
2. Near the top-left corner in the realm drop down menu, select **Add Realm**.
3. Select the [ifix-realm.json](https://github.com/egovernments/iFix-Dev/blob/develop/core/keycloak/ifix-realm.json) file.
4. After the realm gets created, select the `ifix` realm from the drop-down near the top-left corner.

### Creating Clients

1. Remember to select the `ifix` realm from the Keycloak console before proceeding.
2. From the Clients section of Keycloak Admin Console, create a client.
3. Provide a unique username for the client.
4. Go to the client's settings
5. Change Access Type to **confidential**
6. Turn on **Service Account Enabled**
7. In the **Valid Redirect URIs** field provide the root URL of the iFIX Instance. (Not important for our purposes but need to set it because it is mandatory)
8. And Save these changes
9. In the **Service Account Roles** tab, assign the role "fiscal-event-producer"
10. In the **Mappers** tab, create a new mapper to associate the client with a tenantId
    1. Select `Mapper Type` to be "Hardcoded claim"
    2. In `Token Claim Name`, write "tenantId"
    3. In `Claim value`, write the under which the client is being created. (For example, "pb")
    4. Set `Name` same as `Token Claim Name` i.e. "tenantId"
    5. Select `Claim Json Type` to be "String"

Now you can get the credentials from the **Credentials** tab and configure them in the client's system.
