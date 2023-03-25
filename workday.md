# How to connect to Workday

To create a connection with Workday, you have to complete 2 steps.

1. [Create Integration System User](#1-create-integration-system-user-isu)
2. [Vault Connection Setup](#2-vault-connection-setup)

## 1. Create Integration System User (ISU)

The first step is to set up an Integration System User (ISU) in Workday. This way, your Apideck usage will be logged as one user. This also allows you to limit permissions to Apideck. Select only the required permissions for your integration use case.

If you encounter 403 errors when using Unify, ensure your ISU has enough permissions.

### Create a Security Group

Navigate to the **Create Security Group** task in Workday and create an Integration System Security Group.

### Grant permissions to the Security Group

The next step is to grant permissions to your newly created security group.

For each domain you want to grant access to:

1. Navigate to the **View Domain** report and find the domains listed below
2. Click **Domain > Edit Security Policy Permissions**
3. Add the security group you just created, and grant permissions for GET, POST and PUT.

Required domains for the Workday HRIS integration:

- Job Requisition Data
- Person Data: Personal Data
- Person Data: Home Contact Information
- Person Data: Work Contact Information
- Worker Data: Compensation
- Worker Data: Workers
- Worker Data: All Positions
- Worker Data: Current Staffing Information
- Worker Data: Public Worker Reports
- Worker Data: Employment Data
- Worker Data: Organization Information
- Worker Data: Time Off

Also, grant access to the following security policies:

- Integration Build
- Integration Process
- Integration Debug
- Integration Event

Lastly, activate these permissions by navigating to the **Activate Pending Security Policy Changes** task.

### Create Integration System User (ISU)

Navigate to the **Create Integration System User** task and configure a Workday user for Apideck.

![Workday Create ISU Form](https://res.cloudinary.com/apideck/image/upload/v1665490331/docs/connectors/workday/create_isu.png)

Set the Session Timeout Minutes to 0 to prevent session expiration.

Navigate to the **Maintain Password Rules** task and add the ISU to the System Users exempt from a password expiration.

Optionally, enable the **Do Not Allow UI Sessions** checkbox to block the ISU from logging in through the Workday UI.

### Link Security Group to ISU

After creating the ISU, select **Security Profile > Assign Integration System Security Groups**. Select the security group you created previously.

Navigate to the **View Integration System** report and access the Connector or Studio integration. Click **Workday Account > Edit** and select the ISU.

## 2. Vault Connection Setup

Now that you've created an ISU, you're ready to fill out your credentials in Vault.

![Workday Vault Form](https://res.cloudinary.com/apideck/image/upload/v1665491823/docs/connectors/workday/vault.jpg)

| Field                | Description                                                                                                                                                                                                                                                                                                  |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Username (required)  | The username of your Workday Integration Services User (ISU) created in step 1                                                                                                                                                                                                                               |
| Password (required)  | The password of your Workday Integration Services User (ISU) created in step 1                                                                                                                                                                                                                               |
| Tenant ID (required) | The Tenant ID is found in the URL when you are logged into Workday. For example, if the URL of your Workday UI is https://impl.workday.com/sample_company/d/home.html, your tenant ID is sample_company                                                                                                      |
| WSDL URL (required)  | The Workday WSDL URL is used as the base URL for every API request. Find your WSDL URL here: https://community.workday.com/articles/6120#endpoint. If you are unsure, use https://wd2-impl-services1.workday.com/ccx/service/                                                                                |
| Client ID            | Reserved for future use; leave empty for now. Follow the steps on https://community.workday.com/rest/oauth to create an OAuth client                                                                                                                                                                         |
| Client Secret        | Reserved for future use; leave empty for now. Follow the steps on https://community.workday.com/rest/oauth to create an OAuth client                                                                                                                                                                         |
| API Domain           | Reserved for future use; leave empty for now. The API domain is found after creating your OAuth client in Workday. Look for \"Workday REST API Endpoint\". For example, if the REST endpoint is https://wd2-impl-services1.workday.com/ccx/api/my_company, your API domain is wd2-impl-services1.workday.com |

Click **Save** after completing the form. Your Workday account is now connected.
