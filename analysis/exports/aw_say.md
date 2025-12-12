# aw_say

## Signature
int aw_say(char **message);

## Role
Sends a public chat message from the active avatar in the current world or instance.

## Preconditions
- aw_init must have been called
- SDK must be initialized
- A valid session/connection handle must exist
- Client must be inside a world or instance

## Behavior
- Verifies SDK initialized flag (TLS +0x7E0)
- Verifies presence of active session/connection handle (TLS +0x7E4)
- Checks internal string encoding mode (TLS +0x7E8)
- If internal encoding is Unicode:
  - Passes message directly to internal handler
- If internal encoding is non-Unicode:
  - Converts message string to wide-character format
  - Passes converted string to internal handler
- Delegates chat send operation to an internal handler bound to the active connection

## State Effects
- No direct TLS field modification observed
- Triggers server-side broadcast of chat message

## Return Values
- 0x1BC if SDK is not initialized
- 0x1BD if no session/connection handle is present
- Otherwise returns result from internal chat handler

## Side Effects
- Initiates network activity related to chat messaging
- Allocates temporary buffers for string conversion when required
- Chat delivery occurs asynchronously via events

## Call Order Role
- Messaging function
- Used during active world participation
- Requires event/callback system to receive chat responses

## Notes
- Message length and formatting constraints are enforced server-side
- Unicode and ANSI behavior mirrors aw_enter and aw_avatar_location
