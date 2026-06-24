# Source: https://docs.samply.app/api/authentication.html

# Authentication [​](https://docs.samply.app/#authentication)

The Samply API uses personal access tokens to authenticate requests.

Your Access Tokens carry many privileges, so be sure to keep them secure. Don't share your tokens in publicly accessible places like GitHub or client-side code.

Authentication to the API is performed with [HTTP Token Auth](https://developer.mozilla.org/en-US/docs/Web/HTTP/Authentication#bearer). Provide your token as a parameter in the Authorization header with "auth-scheme" set to Bearer.

```
Authorization: Bearer <Your Token>
```

Create and manage your tokens here: [samply.app/preferences/api](https://samply.app/preferences/api)

INFO

Our API is currently availble on [team plans](https://samply.app/plans) & upon request. We can work with you to create custom solutions and expand the API wherever necessary.

## OAuth Support [​](https://docs.samply.app/#oauth-support)

If you're interested in building a Samply integration through your service, you'll need a way to connect a Samply token with your user's Samply account. [OAuth](https://en.wikipedia.org/wiki/OAuth) is an open standard that offers a secure way for users to grant applications access to their information.

Currently, Samply offers OAuth support directly. If you're interested in implementing OAuth in your integration, please reach out to our lead software engineer at [matt@samplyaudio.com](mailto:matt@samplyaudio.com).

## OAuth Implementation [​](https://docs.samply.app/#oauth-implementation)

Once you've worked with our team and received a `CLIENT_ID` and `CLIENT_SECRET`, you'll need to implement OAuth in your application. Below, we've provided a general example of that implementation.

### Authorization request [​](https://docs.samply.app/#authorization-request)

First, your application will need to redirect the user to Samply so the user may authorize the connection between your service and Samply. In the request, you must provide the `CLIENT_ID` ans `redirect_uri`. All other parameters are optional.

```
https://samply.app/oauth/yourservice?client_id=MYCLIENT_ID&redirect_uri=REDIRECT_URI&error_uri=ERROR_URI&state=STATE.
```

---

#### client\_id query parameter

CLIENT\_ID as provided to your service by the Samply team.

---

#### redirect\_uri query parameter

Redirect URI back to your service. User will be redirected here after successfully authorizing the OAuth request.

---

#### error\_uri query parameter optional

Error URI back to your service. User will be redirected here after an unsuccessful authorization request.

---

#### state query parameter optional

Optional state parameter. This value will be passed back to your service after a successful or unsuccessful authorization request.

### Authorization grant [​](https://docs.samply.app/#authorization-grant)

If the user declined authorization or another error occurred, Samply will redirect to the `error_uri` with an `error` and `error_description`. You can read more information on error handling [here](https://docs.samply.app/./authentication.html#error-handling).

If the user successfully granted authorization, Samply will redirect to the `redirect_uri`. with a `code` and `state` (if it was provided).

### Request token [​](https://docs.samply.app/#request-token)

Now that the user has authorized the request, your server may request a token from the `auth-token` endpoint on behalf of that user.

Request type `POST`

Endpoint `/auth-token`

js

```
{
  client_id: string,
  client_secret: string,
  code: string,
}
```

---

#### client\_id string

CLIENT\_ID as provided to your service by the Samply team.

---

#### client\_secret string

CLIENT\_SECRET as provided to your service by the Samply team. Never expose this value in publicly available code.

---

#### code string

The code provided to your server from Samply after user authorization.

Assuming `CLIENT_ID`, `CLIENT_SECRET`, and `code` were all valid, a `200` response will be sent containing that user's access token.

js

```
{
  access_token: string
}
```

Now that you have a user's access token, you're ready to build an integration that makes calls on their behalf!

### Error handling [​](https://docs.samply.app/#error-handling)

When a user declines authorization or another error occurs, Samply will redirect to the provided `error_uri` and provide additional `error` and `error_description` query parameters that can be read on your server. Those values are outlined below. If `state` was provided in the initial request, it will be provided in the error redirect as well.

---

#### error query parameter readonly

Error code with the following possible values:

###### Values

---

#### access\_denied

User denied authorization.

---

#### server\_error

Something went wrong on Samply's server during authorization.

---

#### error\_description query parameter readonly

A human readable, URI-encoded description of the error that occurred.