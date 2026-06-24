# Source: https://docs.samply.app/api/introduction.html

# API Reference [​](https://docs.samply.app/#api-reference)

The Samply API provides a CRUD interface to operate on Samply primitives, including Projects, Players, and Files. These simple primitives, along with OAuth and custom webhook support allow you to build infinite integrations.

This API follows the [REST](http://en.wikipedia.org/wiki/Representational_State_Transfer) architectual style. Our API has predictable resource-oriented URLs, returns [JSON-encoded](http://www.json.org) responses, and uses standard HTTP response codes, authentication, and verbs.

All documentation examples use the [web fetch api](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API). Of course, you can use any tool that allows https requests (cURL, Zapier, Postman, etc).

js

```
const baseUrl = "https://samply.app/api/v0";
const token = "MY-UNIQUE-TOKEN"

// Create a player
const response = await fetch(`${baseUrl}/players`, {
  method: "POST"
  body: JSON.stringify({
    name: "Hello World Player",
    options: {        
      downloads: false,
      comments: true,
      stacks: true,        
    }
  }),
  headers: {
    Authorization: `Bearer ${token}`,
    "Content-Type": "application/json"
  }
});

const jsonResponse = await response.json();
```

Let's get started!