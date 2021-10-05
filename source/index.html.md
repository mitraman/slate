---
title: BaaS API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - javascript
  
toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>

includes:
  - accounts
  - lending
  - customer_onboarding
  - balances
  - transactions
  - pfm
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the Banking as a Service Starter API
---

# Introduction


Introduction text.

# Authentication

TBD

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here" \
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
```

> Make sure to replace `meowmeowmeow` with your API key.

Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

# Message Structure

Request messages look like this

`json
{

}
`

# Pagination

TBD

