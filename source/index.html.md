---
title: Searchbase API Reference

language_tabs:
  - shell
  - ruby
  - python
  - javascript

toc_footers:
  - <a href='https://app.searchbase.dev/signup'>Sign Up for a Developer Key</a>


includes:
  - endpoint_search

search: true

code_clipboard: true

meta:
  - name: description
    content: Searchbase API documentation provides comprehensive guides and interactive examples to help you integrate powerful search functionalities in your applications.
---

# Introduction

Welcome to the Searchbase API documentation. Here, you will find all the information needed to integrate our powerful search functionalities into your applications. Our API supports a wide range of search capabilities, including full-text and semantic searches, to provide flexible and efficient search experiences.

This documentation is intended for developers looking to integrate Searchbase's search capabilities into their applications and covers everything from authentication to making complex search queries.


# Setup
When setting up your Searchbase account, you'll be asked to provide authentication specifications for your database, whether it's PostgreSQL or Firebase. These credentials are critical to ensure secure communication between Searchbase and your database, allowing for seamless search functionality within your application.

## PostgreSQL Credentials

To securely access your PostgreSQL database, you'll need to create authentication credentials that grant limited, read-only access. This ensures that the Searchbase integration can query your data without risking unauthorized modifications.

### Steps to Create Read-Only Credentials in PostgreSQL

1. **Log into your PostgreSQL server**: Use a PostgreSQL client or terminal. If you're using `psql`, you can connect with `psql -U username dbname`.

2. **Create a read-only role**: Execute the SQL command to create a new role. Replace `readonly_user` with your desired username.

   ```sql
   CREATE ROLE readonly_user WITH LOGIN PASSWORD 'your_strong_password';
   ```

3. **Grant usage on your schema**: Usually, the schema is `public`, but replace `your_schema` if you're using a different one.

   ```sql
   GRANT USAGE ON SCHEMA your_schema TO readonly_user;
   ```

4. **Grant select permission**: This allows the read-only user to perform select queries.

   ```sql
   GRANT SELECT ON ALL TABLES IN SCHEMA your_schema TO readonly_user;
   ```

5. **Set default privileges**: Ensure that future tables are also accessible to the read-only user.

   ```sql
   ALTER DEFAULT PRIVILEGES IN SCHEMA your_schema GRANT SELECT ON TABLES TO readonly_user;
   ```

### Steps to Test Read-Only Account

After creating your read-only user, you can test it with this one-liner in your PostgreSQL client:

```sh
psql 'dbname=your_database_name user=readonly_user password=your_strong_password host=your_database_host' -c 'SELECT * FROM your_table LIMIT 1;'
```

Replace `your_database_name`, `readonly_user`, `your_strong_password`, `your_database_host`, and `your_table` with your actual database name, read-only username, password, host, and a table name, respectively.

### Generating Connection String

Now you can compile your connection string like with this template:

`postgres://readonly_user:your_strong_password@your_database_host:5432/your_database_name`

Input this connection string on Searchbase when prompted under the Postgres connection string field.

### Using the Credentials

When integrating with Searchbase, ensure your application or service uses the `readonly_user` credentials. This provides Searchbase with the necessary permissions to perform search queries without the ability to alter the database.

## Firebase Credentials

For Firebase, creating a read-only access involves setting up a new role with restricted permissions in your Firebase project and generating a private key associated with that role.


### Creating a Role with Read-Only Access

To set up Firebase, navigate to `cloud.google.com`, access `IAM & Admin` from the left sidebar, and follow these steps:

1.  Click on `Roles`.

2.  Select `Create Role`.

3.  Name the role "FirestoreReadAccess".

4.  Add the following permissions to the role:

    -   `datastore.databases.get`
    -   `datastore.databases.getMetadata`
    -   `datastore.databases.list`
    -   `datastore.entities.get`
    -   `datastore.entities.list`
    -   `datastore.indexes.get`
    -   `datastore.indexes.list`
    -   `datastore.namespaces.get`
    -   `datastore.namespaces.list`
    -   `datastore.statistics.get`
    -   `datastore.statistics.list`


### Creating a Service Account

Then, create a service account with this role:

1.  Go to `Service Accounts` in the sidebar.
2.  Click on `Create new service account`.
3.  Assign the "FirestoreReadAccess" role to this account.

### Downloading the Service Account Key

After creating the service account:

1.  Navigate to the service account you created.
2.  Click on `Keys`.
3.  Choose `Add Key`, then `Create new key`.
4.  Select `JSON` as the key type, which will prompt the download of the key file.

Use this downloaded JSON key file to authenticate your Firebase instance with Searchbase by uploading it when prompted for Firebase credentials.

After these steps, you'll be able to download a JSON file with your service account's credentials. Use these credentials in Searchbase by uploading the JSON file when prompted for Firebase credentials.

### Using the Credentials

In your application integration with Searchbase, use the service account JSON file to authenticate with Firebase. This setup ensures that Searchbase queries your Firebase database using the read-only permissions, safeguarding your data integrity.

By following these steps, you create secure, read-only access credentials for both PostgreSQL and Firebase, allowing safe integration with the Searchbase API.

# Authentication

## Obtaining Your API Token

Before you can start using the Searchbase API, you need to obtain an API token. This token is necessary for all your API requests to be authenticated and authorized.

### Steps to Obtain an API Token

1. [Sign up for a developer account](https://app.searchbase.dev/signup)
2. Once logged in, navigate to the API section.
3. Generate a new API token from the dashboard.

Keep your API token secure and ensure it is not exposed publicly in your applications.

## Using the API Token

```shell
curl "https://api.searchbase.dev/search" \
  -H "Content-Type: application/json" \
  -H "x-searchbase-token: YourAPITokenHere" \
  -d '{...}'
```

To authenticate your API requests, include your API token in the request headers as follows:

Replace `YourAPITokenHere` with your actual API token.
