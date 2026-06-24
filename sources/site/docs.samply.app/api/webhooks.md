# Source: https://docs.samply.app/api/webhooks.html

# Webhooks [​](https://docs.samply.app/#webhooks)

Webhooks let you receive real-time updates when certain actions happen in your Samply account—like when an upload finishes or a comment is added. When one of your subscribed events occurs, Samply sends an HTTP POST request to the URL you provide with a [JSON payload](https://docs.samply.app/#example-payload) describing the event.

## Create a webhook [​](https://docs.samply.app/#create-a-webhook)

This endpoint creates a webhook and returns a [webhook object](https://docs.samply.app/#webhook-object).

Request type `POST`

Endpoint `/webhooks`

### Attributes [​](https://docs.samply.app/#attributes)

js

```
{
  label: string,
  url: string,
  events: string[],
}
```

---

#### label string

A name to help you identify the webhook.

---

#### url string

The endpoint URL where Samply will send event payloads.

---

#### events string array

One or more event types to subscribe to. See available events below.

## Delete a webhook [​](https://docs.samply.app/#delete-a-webhook)

This endpoint deletes a webhook by id.

Request type `DELETE`

Endpoint `/webhooks/:webhookid`

## Available events [​](https://docs.samply.app/#available-events)

| Event type | Description |
| --- | --- |
| `player.created` | A new player is created |
| `player.updated` | An existing player is modified |
| `project.created` | A new project is created |
| `project.updated` | An existing project is modified |
| `comment.created` | A new comment is posted |
| `upload.started` | A file begins uploading |
| `upload.completed` | A file has finished uploading |
| `upload.failed` | A file upload fails due to an error |

## Webhook object [​](https://docs.samply.app/#webhook-object)

All webhook actions return a webhook object with the following structure.

js

```
{
  id: string,
  label: string,
  events: string[],
  url: string,
  timeCreated: number,
  timeModified: number,
}
```

---

#### id string readonly

Webhook id.

---

#### label string readonly

Webhook label.

---

#### events string array readonly

Subscribed event types.

---

#### url string readonly

Destination URL.

---

#### timeCreated number readonly

Time created in millis since Unix epoch.

---

#### timeModified number readonly

Time modified in millis since Unix epoch.

## Example payload [​](https://docs.samply.app/#example-payload)

json

```
{
  "id": "a459f855-da9f-4dfc-9181-35da2badfdcc",
  "type": "comment.created",
  "object": "event",
  "projectid": "mSg4Nu5vAch9pkCEcgDP",
  "boxid": "cd01f0c1-f1b3-4bc9-95c3-e14e5b01fbe1",
  "boxName": "Mystery Machine",
  "commentid": "uDXE192QibaDfK51eTTN",
  "data": {
    "after": {
      "id": "uDXE192QibaDfK51eTTN",
      "object": "comment",
      "message": "<p>Scooby Doo Where Are You?</p>",
      "creator": {
        "displayName": "eschirtz",
        "email": null,
        "photoURL": null,
        "uid": "TlYYwlHzZohpleC8a2Vo1SYY1902"
      },
      "isReply": false,
      "timeCreated": 1750041281427,
      "timeModified": 1750041281427
    }
  },
  "timeCreated": 1750041281427,
  "uid": "zklUx8RcjHZTqqi4mWoQNoBMsU03"
}
```

## Tips [​](https://docs.samply.app/#tips)

- Test your endpoint with a tool like [Webhook.site](https://webhook.site) before going live.
- Use webhooks alongside tools like [Zapier](https://zapier.com/apps/samply/integrations) or [Make](https://www.make.com) to trigger automations.
- You can delete or update webhooks at any time from your [Samply preferences](https://samply.app/preferences/api).

Need help? Contact support or check out our integration guides.