---
id: databricks
title: Databricks
---

Databricks is a cloud-based platform for data processing, analytics, and machine learning. ToolJet connects to Databricks, allowing your applications to access and update your data in your Databricks Warehouses directly using SQL queries.

<div style={{textAlign: 'center'}}>
    <img style={{ border:'0', borderRadius:'5px', boxShadow: '0px 1px 3px rgba(0, 0, 0, 0.2)' }} className="screenshot-full" src="/img/datasource-reference/databricks/install.gif" alt="Install Databricks" />
</div>

<div style={{paddingTop:'24px'}}>

## Configuration

ToolJet's Databricks integration relies on a configuration form that supports the following parameters:

#### Required Parameters

- **Server hostname**: The server hostname or the IP address of your Databricks Warehouse. For example, `62596234423488486.6.gcp.databricks.com`.
- **HTTP Path**: The API endpoint path for the Databricks resource you want to access. For example, `/sql/1.0/warehouses/44899g7346c19m95`.
- **Personal access token**: Personal access tokens are used for secure authentication to the Databricks API instead of passwords. For example, `dapi783c7d155d138d8cf14`.

#### Optional Parameters

- **Port**: The port number of your Databricks Warehouse. The default port number is `443`.
- **Default Catalog**: The default catalog to use for the connection.
- **Default Schema**: The default schema to use for the connection.

### Setup

- Navigate to your Databricks workspace, select the desired SQL Warehouse, and find **Server Hostname** and **HTTP Path** within the connection details tab.

<img style={{ border:'0', borderRadius:'5px', boxShadow: '0px 1px 3px rgba(0, 0, 0, 0.2)' }} className="screenshot-full" src="/img/datasource-reference/databricks/connection-details.png" alt="Databricks: Connection Details" />

- To generate a personal access token, access your Databricks User Settings, select the Developer tab, click Manage under Access Tokens, and then click on the **Generate New Token** button.

<img style={{ border:'0', borderRadius:'5px', boxShadow: '0px 1px 3px rgba(0, 0, 0, 0.2)' }} className="screenshot-full" src="/img/datasource-reference/databricks/generate-token.png" alt="Databricks: Access Tokens" />

- Navigate to the Databricks datasource configuration form in ToolJet, fill in the required parameters, and click the **Save** button. You can test the connection by clicking the **Test Connection** button.

<img style={{ border:'0', borderRadius:'5px', boxShadow: '0px 1px 3px rgba(0, 0, 0, 0.2)' }} className="screenshot-full" src="/img/datasource-reference/databricks/setup-parameters.png" alt="Databricks: Setup Paramaters" />

</div>

<div style={{paddingTop:'24px'}}>

## Querying Databricks

1. Click on + Add button of the query manager at the bottom panel of the editor.
2. Select the **Databricks** datasource added in previous step.
3. Select the **SQL Mode** from the dropdown. (ToolJet currently supports only SQL mode for Databricks interactions.)
4. Click on the **Preview** button to preview the output or Click on the **Run** button to create and trigger the query.

<div style={{textAlign: 'center'}}>

<img className="screenshot-full" src="/img/datasource-reference/databricks/add-query.gif" alt="Databricks: Query Setup" />

</div>

:::tip
You can apply transformations to the query results. Refer to our transformations documentation for more information: [link](/docs/beta/app-builder/custom-code/transform-data)
:::

</div>

<div style={{paddingTop:'24px'}}>

## Supported Queries

Databricks supports standard SQL commands for data manipulation tasks.

### Read Data

The following example demonstrates how to read data from a table. The query selects all the columns from the _customers_ table.

```sql
SELECT * FROM customers
```

<img className="screenshot-full" src="/img/datasource-reference/databricks/readData.png" alt="Databricks: Read Data Query" style={{marginBottom:'15px'}}/>

### Write Data

The following example demonstrates how to write data to a table. The query inserts a new row into the _customers_ table.

```sql
INSERT INTO customers (
    customer_id,
    first_name,
    last_name,
    email,
    phone,
    city,
    state,
    zip_code,
    country
) VALUES (
    '1001'
    'Tom',
    'Hudson',
    'tom.hudson@example.com',
    '50493552',
    'San Clemente',
    'CA',
    '92673',
    'USA'
);
```

<img className="screenshot-full" src="/img/datasource-reference/databricks/writeData.png" alt="Databricks: Write Data Query" style={{marginBottom:'15px'}}/>

### Update Data

The following example demonstrates how to update data in a table. The query updates the _first_name_ and _email_ column of the _customers_ table.

```sql
UPDATE customer
SET first_name = 'John',
    email = 'john.hudson@example.com'
WHERE customer_id = 1001;
```

<img className="screenshot-full" src="/img/datasource-reference/databricks/updateData.png" alt="Databricks: Update Data Query" style={{marginBottom:'15px'}}/>

### Delete Data

The following example demonstrates how to delete data from a table. The query deletes a row from the _customers_ table.

```sql
DELETE FROM customer
WHERE customer_id = 1001;
```

<img className="screenshot-full" src="/img/datasource-reference/databricks/deleteData.png" alt="Databricks: Delete Data Query" style={{marginBottom:'15px'}}/>

</div>
