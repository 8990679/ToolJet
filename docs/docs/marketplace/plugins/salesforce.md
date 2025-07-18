---
id: marketplace-plugin-salesforce
title: Salesforce
---

# Salesforce

ToolJet connects to your Salesforce account, allowing you to directly interact with your Salesforce connected app from within your ToolJet application.

:::info
**NOTE:** **Before following this guide, it is assumed that you have already completed the process of [Using Marketplace plugins](/docs/marketplace/marketplace-overview#using-marketplace-plugins)**.
:::

## Connection

- To connect to Salesforce, you need to have the following credentials:
  - **Client ID** - The consumer key of your Salesforce connected app.
  - **Client Secret** - The consumer secret of your Salesforce connected app.
  <img className="screenshot-full img-full" style={{ marginTop: '15px' }} src="/img/marketplace/plugins/salesforce/api_settings.png" alt="Salesforce Connected App API Settings" />
- Establish a connection to Salesforce by either clicking `+Add new Data source` on the query panel or navigating to the [Data Sources](/docs/data-sources/overview/) page from the ToolJet dashboard.
- Select the API version from the dropdown, enter your Client ID and Client Secret into their designated fields.
- Copy the **Redirect URL** and paste it into the OAuth **Callback URL** field in your Salesforce connected app settings.
- Click the **Connect to salesforce** button to authenticate your Salesforce account.
- Once authenticated, click **Save data source** to store the data source.
    <img className="screenshot-full img-full" style={{ marginTop: '15px' }} src="/img/marketplace/plugins/salesforce/setup.png" alt="Salesforece Install" />

## Querying Salesforce

- To perform queries on Salesforce in ToolJet, click the **+Add** button in the [query manager](/docs/app-builder/query-panel/#query-manager) located at the bottom panel of the editor.
- Select the previously configured Salesforce datasource from the **Data Source** dropdown.
- In the Operation dropdown, select the desired operation type. ToolJet supports two operation types for Salesforce interactions:
  - **[SOQL Query](#soql-query)** - SOQL (Salesforce Object Query Language) is used to search your organization’s Salesforce data for specific information.
  - **[CRUD Action](#crud-actions)** - CRUD (Create, Retrieve/Read, Update, Delete) actions are used to interact with Salesforce objects.

## SOQL Query

- To perform a SOQL query, select the **SOQL Query** operation from the dropdown.
- Enter the SOQL query in the **Query** field.
- Click **Run** to execute the query.
    <img className="screenshot-full img-full" style={{ marginTop: '15px' }} src="/img/marketplace/plugins/salesforce/soql-query.png" alt="SOQL Query" />

:::info
Query results can be transformed using transformations. Read our [transformations documentation](/docs/beta/app-builder/custom-code/transform-data).
:::

## CRUD Actions

To perform CRUD actions on Salesforce, select the **CRUD Action** operation from the dropdown. The following CRUD actions are supported:

### Create

#### Required parameters:

- **Resource Name** - The name of the Salesforce object you want to create. By default, Account is selected.
- **Resource Body** - The data you want to insert into the Salesforce object.
    <img className="screenshot-full img-full" style={{ marginTop: '15px' }} src="/img/marketplace/plugins/salesforce/action-create.png" alt="Create" />

### Retrieve(Read)

#### Required parameters:

- **Resource Name** - The name of the Salesforce object you want to create. By default, Account is selected.
- **Resource ID** - The ID of the Salesforce object you want to retrieve.
    <img className="screenshot-full img-full" style={{ marginTop: '15px' }} src="/img/marketplace/plugins/salesforce/action-read.png" alt="Read" />

### Update

#### Required parameters:

- **Resource Name** - The name of the Salesforce object you want to create. By default, Account is selected.
- **Resource Body** - The data you want to update in the Salesforce object. The resource body should contain the ID of the Salesforce object you want to update.
    <img className="screenshot-full img-full" style={{ marginTop: '15px' }} src="/img/marketplace/plugins/salesforce/action-update.png" alt="Update" />

### Delete

#### Required parameters:

- **Resource Name** - The name of the Salesforce object you want to create. By default, Account is selected.
- **Resource ID** - The ID of the Salesforce object you want to delete.
    <img className="screenshot-full img-full" style={{ marginTop: '15px' }} src="/img/marketplace/plugins/salesforce/action-delete.png" alt="Delete" />
