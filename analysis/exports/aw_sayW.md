# aw_sayW

## Signature
int aw_sayW(const wchar_t *message);

## Role
Wide-character variant of aw_say. Sends a public chat message using a Unicode string.

## Preconditions
- aw_init must have been called
- SDK must be initialized
- A valid session/connection handle must exist
- Client must be inside a world or instance

## Behavior
- Verifies SDK initialized flag (TLS +0x7E0)
- Verifies presence of active session/connection handle (TLS +0x7E4)
- Converts provided wide-character string into internal string representation
- Delegates chat send operation to the same internal handler used by aw_say

## State Effects
- No direct TLS field modification observed
- Triggers server-side broadcast of chat message

## Return Values
- 0x1BC if SDK is not initialized
- 0x1BD if no session/connection handle is present
- Otherwise returns result from internal chat handler

## Side Effects
- Initiates network activity related to chat messaging
- Allocates temporary buffers for internal string handling
- Chat delivery occurs asynchronously via events

## Call Order Role
- Messaging function
- Used during active world participation
- Functionally equivalent to aw_say with Unicode input

## Notes
- aw_say and aw_sayW share identical internal logic
- Unicode variant bypasses codepage-based conversion
