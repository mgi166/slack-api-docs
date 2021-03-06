This method starts a Real Time Messaging API session. Refer to the [RTM API documentation](/rtm) for full details on how to use the RTM API.

## Arguments

This method has the URL `https://slack.com/api/rtm.start` and follows the [Slack Web API calling conventions](/web#basics).

| Argument | Example | Required | Description |
| --- | --- | --- | --- |
| `token` | `xxxx-xxxxxxxxx-xxxx` | Required | Authentication token (Requires scope: `client`) |

## Response

This method returns lots of data about the current state of a team, along with a WebSocket Message Server URL:

```
{
    "ok": true,
    "url": "wss:\/\/ms9.slack-msgs.com\/websocket\/7I5yBpcvk",

    "self": {
        "id": "U023BECGF",
        "name": "bobby",
        "prefs": {
            …
        },
        "created": 1402463766,
        "manual_presence": "active"
    },
    "team": {
        "id": "T024BE7LD",
        "name": "Example Team",
        "email_domain": "",
        "domain": "example",
        "msg_edit_window_mins": -1,
        "over_storage_limit": false
        "prefs": {
            …
        },
        "plan": "std"
    },
    "users": […],

    "channels": […],
    "groups": […],
    "ims": […],

    "bots": […],
}
```

The `url` property contains a WebSocket Message Server URL. Connecting to this URL will initiate a Real Time Messaging session. These URLs are only valid for 30 seconds, so connect quickly!

The `self` property contains details on the authenticated user.

The `team` property contains details on the authenticated user's team. The`users` property contains a list of [user objects](/types/user), one for every member of the team.

The `channels` property is a list of [channel objects](/types/channel), one for every channel visible to the authenticated user. For regular or administrator accounts this list will include every team channel. The`is_member` property indicates if the user is a member of this channel. If true then the channel object will also include the topic, purpose, member list and read-state related information.

The `groups` property is a list of [group objects](/types/group), one for every group the authenticated user is in.

The `ims` property is a list of [IM objects](/types/im), one for every direct message channel visible to the authenticated user.

The `bots` property gives details of the integrations set up on this team.

## Errors

This table lists the expected errors that this method will return. However, other errors can be returned in the case where the service is down or other unexpected factors affect processing. Callers should _always_ check the value of the `ok` params in the response.

| Error | Description |
| --- | --- |
| `migration_in_progress` | Team is being migrated between servers. See [the `team_migration_started` event documentation](/events/team_migration_started) for details. |
| `not_authed` | No authentication token provided. |
| `invalid_auth` | Invalid authentication token. |
| `account_inactive` | Authentication token is for a deleted user or team. |

