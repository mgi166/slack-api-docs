This method lets you find out information about a user's presence. [Consult the presence documentation](/docs/presence) for more details.

## Arguments

This method has the URL `https://slack.com/api/users.getPresence` and follows the [Slack Web API calling conventions](/web#basics).

| Argument | Example | Required | Description |
| --- | --- | --- | --- |
| `token` | `xxxx-xxxxxxxxx-xxxx` | Required | Authentication token (Requires scope: `read`) |
| `user` | `U1234567890` | Required | User to get presence info on. Defaults to the authed user. |

## Response

When requesting information for a different user, this method just returns the current presence (either `active` or `away`):

```
{
    "ok": true,
    "presence": "active",
}
```

If you are requesting presence information for the authed user, this method returns the current presence, along with details on how it was calculated:

```
{
    "ok": true,
    "presence": "active",
    "online": true,
    "auto_away": false,
    "manual_away": false,
    "connection_count": 1,
    "last_activity": 1419027078
}
```

`presence` indicates the user's overall presence, it will either be `active` or `away`.

`online` will be true if they have a client currently connected to Slack. `auto_away` will be true if our servers haven't detected any activity from the user in the last 30 minutes. `manual_away` will be true if the user has manually set their presence to `away`.

`connection_count` gives a count of total connections.

`last_activity` indicates the last activity seen by our servers. If a user has no connected clients then this property will be absent.

## Errors

This table lists the expected errors that this method will return. However, other errors can be returned in the case where the service is down or other unexpected factors affect processing. Callers should _always_ check the value of the `ok` params in the response.

| Error | Description |
| --- | --- |
| `not_authed` | No authentication token provided. |
| `invalid_auth` | Invalid authentication token. |
| `account_inactive` | Authentication token is for a deleted user or team. |

