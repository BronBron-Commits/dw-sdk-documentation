# aw_join_reply

## Signature
int aw_join_reply(int request_id, int response);

## Role
Join reply handler. Sends a response to a prior join request using the active session/connection.

## Preconditions
- aw_init must have been called
- SDK must be initialized
- A valid session/connection handle must exist

## Behavior
- Reads the thread-local SDK context
- Verifies initialized flag (TLS +0x7E0)
- Verifies presence of active session/connection handle (TLS +0x7E4)
- Delegates join reply handling to an internal handler bound to the active connection
- Passes both parameters directly to the internal handler

## State Effects
- No direct TLS field modification observed
- Affects join state via internal connection/session logic

## Return Values
- 0x1BC if SDK is not initialized
- 0x1BD if no session/connection handle is present
- Otherwise returns result from internal join-reply handler

## Side Effects
- Initiates network activity related to join reply handling
- No memory allocation observed at this level
- No thread creation observed

## Call Order Role
- Transition / response function
- Used in response to aw_join or server-issued join requests
- Part of join handshake sequence

## Notes
- Parameter semantics are protocol-defined
- Function does not perform validation on parameters
