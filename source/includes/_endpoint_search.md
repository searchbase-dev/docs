# Search Endpoint

The `/search` endpoint is the primary way to perform searches within your indexed data. This section covers the endpoint's usage, including request structure, available filters, and response handling.

## Making a Search Request

```js
const fetch = require('node-fetch');

const query = {
  index: 'products',
  filters: [
    { field: 'category', op: 'EQUAL', value: 'electronics' },
    { field: 'price', op: 'GTE', value: 100 }
  ],
  select: ['name', 'price', 'description'],
  limit: 10
};

const headers = {
  'Content-Type': 'application/json',
  'x-searchbase-token': 'YourAPITokenHere'
};

fetch('https://api.searchbase.dev/search', {
  method: 'POST',
  headers: headers,
  body: JSON.stringify({ query: query })
})
.then(response => response.json())
.then(data => console.log(data))
.catch(error => console.error('Error:', error));
```

### HTTP Request

`POST https://api.searchbase.dev/search`

### Request Headers

- `Content-Type`: `application/json`
- `x-searchbase-token`: `<Your API token>`

### Request Body Structure

The body of a search request includes the following parameters:

- `index`: Name of the index to search.
- `filters`: (Optional) Array of filter objects to refine the search.
- `select`: (Optional) Fields to be included in the search results.
- `limit`: (Optional) Maximum number of results to return.
- `offset`: (Optional) Number of results to skip (for pagination).

### Filter Object

Each filter object within the `filters` array can have the following properties:

- `field`: The name of the field to filter on.
- `op`: The operation to apply. Supported operations include `EQUAL`, `NOT_EQUAL`, `IN`, `NOT_IN`, `GTE`, `LTE`, etc.
- `value`: The value to use for the operation.



## Response Structure

```json
{
  "results": [
    {
      "id": "1",
      "name": "Smartphone",
      "price": 299,
      "description": "Latest model with high-resolution camera"
    },
    ...
  ],
  "total": 150,
  "limit": 10,
  "offset": 0
}
```

A successful search request returns a JSON object containing the following keys:

- `results`: An array of matching documents.
- `total`: Total number of documents matching the query.
- `limit`: The `limit` value from the request.
- `offset`: The `offset` value from the request.
