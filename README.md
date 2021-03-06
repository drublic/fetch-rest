# REST-API caller using fetch

[![Build Status](https://travis-ci.org/drublic/fetch-rest-connect.svg?branch=master)](https://travis-ci.org/drublic/fetch-rest-connect)
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2Fdrublic%2Ffetch-rest-connect.svg?type=shield)](https://app.fossa.io/projects/git%2Bgithub.com%2Fdrublic%2Ffetch-rest-connect?ref=badge_shield)

Call any REST-API in the browser.

## How to use

### Install

You can install this package via NPM

    npm install --save fetch-rest-connect

Using yarn

    yarn add fetch-rest-connect

### Usage

All methods used provided by the package are asynchronous.

```javascript
import Fetcher from 'fetch-rest-connect'
const CONTENT_ENDPOINT = 'content'

const fetcher = new Fetcher({
  apiUrl: `/api`,
  endpoints: {
    [CONTENT_ENDPOINT]: '/content/',
  },
  options: { // optional
    credentials: 'include',
  }
})

const getContent = async () => {
  try {
    const data = await fetcher.getAll(CONTENT_ENDPOINT)

    return data
  } catch (error) {
    throw new Error(error)
  }
}
```

Your API endpoints can also hold any kind of variable:

```javascript
const endpoints = {
  [CONTENT_ENDPOINT]: '/article/:articleId/content/'
}
```

When calling the fetcher you can now pass `uriParams` to fill the vars in the
route.

```javascript
const articleId = `foo`;
const uriParams = {
  articleId,
};
const data = await fetcher.getAll(CONTENT_ENDPOINT, uriParams)
```

### Methods

All methods build upon the main method `fetch`:

* `fetch`, Fetch entry point
  * `action: string`, Action or endpoint you want to call, required
  * `id: String`, If you want to call a specific ID of an endpoint, you can use this field
  * `uriParams: Object`, If the endpoint has variables in it you can use this object to fill them
  * `additionalQueryParams: object`, Pass get parameters for the request
  * `data: Object`, Data you want to send with the request
  * `method: ENUM('GET' | 'PUT' | 'POST' | 'DELETE') = 'GET'`, Specific method you want for your call
  * `headers: Object`, additional headers for request

Params are the same as above

* `get(action, id, uriParams, additionalQueryParams, headers)`
* `getAll(action, uriParams, additionalQueryParams, headers)`
* `create(action, data, uriParams, additionalQueryParams, headers)`
* `update(action, id, data, uriParams, additionalQueryParams, headers)`
* `upsert(action, id, data, uriParams, additionalQueryParams, headers)`
* `delete(action, id, uriParams, additionalQueryParams, headers)`

## License

This library is licensed under [MIT](./LICENSE)

[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2Fdrublic%2Ffetch-rest-connect.svg?type=large)](https://app.fossa.io/projects/git%2Bgithub.com%2Fdrublic%2Ffetch-rest-connect?ref=badge_large)
