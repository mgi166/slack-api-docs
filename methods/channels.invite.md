This method is used to invite a user to a channel. The calling user must be a member of the channel.

## Arguments

This method has the URL `https://slack.com/api/channels.invite` and follows the [Slack Web API calling conventions](/web#basics).

| Argument | Example | Required | Description |
| --- | --- | --- | --- |
| `token` | `xxxx-xxxxxxxxx-xxxx` | Required | Authentication token (Requires scope: `post`) |
| `channel` | `C1234567890` | Required | Channel to invite user to. |
| `user` | `U1234567890` | Required | User to invite to channel. |

## Response

```
{
    "ok": true,
    "channel": {
        "id": "C024BE91L",
        "name": "fun",
        "created": 1360782804,
        "creator": "U024BE7LH",
        "is_archived": false,
        "is_member": true,
        "is_general": false,
        "last_read": "1401383885.000061",
        "latest": { … },
        "unread_count": 0,
        "unread_count_display": 0,
        "members": […],
        "topic": {
            "value": "Fun times",
            "creator": "U024BE7LV",
            "last_set": 1369677212
        },
        "purpose": {
            "value": "This channel is for fun",
            "creator": "U024BE7LH",
            "last_set": 1360782804
        }
    }
}
```

## Errors

This table lists the expected errors that this method will return. However, other errors can be returned in the case where the service is down or other unexpected factors affect processing. Callers should _always_ check the value of the `ok` params in the response.

| Error | Description |
| --- | --- |
| `channel_not_found` | Value passed for `channel` was invalid. |
| `user_not_found` | Value passed for `user` was invalid. |
| `cant_invite_self` | Authenticated user cannot invite themselves to a channel. |
| `not_in_channel` | Authenticated user is not in the channel. |
| `already_in_channel` | Invited user is already in the channel. |
| `is_archived` | Channel has been archived. |
| `cant_invite` | User cannot be invited to this channel. |
| `not_authed` | No authentication token provided. |
| `invalid_auth` | Invalid authentication token. |
| `account_inactive` | Authentication token is for a deleted user or team. |
| `user_is_bot` | This method cannot be called by a bot user. |
| `user_is_ultra_restricted` | This method cannot be called by a single channel guest. |

