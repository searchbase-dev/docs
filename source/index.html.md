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
