---
layout: default
title: Bearer Token Authentication
parent: API
nav_order: 1
---

## Bearer Token Authentication

To get a Bearer token for authenticating your API calls, you must first request a valid LEADx API Client ID and secret from LEADx support.

Then get a LEADx code by going to:

`https://app.leadx.org/oauth/authorize?client_id=REPLACE_THIS_WITH_YOUR_LEADX_CLIENT_ID&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob&response_type=code&scope=leadx`

Finally, you must convert the code given to you at that URL into a Bearer token by running a command like this:

```bash
LEADX_CLIENT_ID=...
LEADX_CLIENT_SECRET=...
LEADX_CODE=...

curl -F grant_type=authorization_code -F client_id=$LEADX_CLIENT_ID -F client_secret=$LEADX_CLIENT_SECRET -F code=$LEADX_CODE -F redirect_uri=urn:ietf:wg:oauth:2.0:oob -X POST https://app.leadx.org/oauth/token
```

That command will return a value like this:

```json
{"access_token":"vQnHwxNg_IUnd384hf34hfBafn70m5i","token_type":"Bearer","expires_in":7199,"refresh_token":"65Ztwj18_2JsdfsdfsdfGqOA1UoXzDlViWkn2MGYio","scope":"leadx","created_at":1593111170}
```

The access_token is your Bearer token, which you can use to authenticate any of the API calls below like this:

```bash
LEADX_BEARER_TOKEN=vQnHwxNg_IUnd384hf34hfBafn70m5i

curl -X GET https://app.leadx.org/api/v1/academy/courses -H "accept: application/json" -H "Authorization: Bearer $LEADX_BEARER_TOKEN"
```

NOTE: The above Bearer token will not work, it is just an example for illustrative purposes.

