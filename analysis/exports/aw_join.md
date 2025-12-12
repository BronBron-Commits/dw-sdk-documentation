# aw_join

## Signature
int aw_join(int target);

## Role
Join request function. Initiates a join operation using the active session/connection.

## Preconditions
- aw_init must have been called
- SDK must be initialized
- A valid session/connection handle must exist

## Behavior
- Reads the thread-local SDK context
- Verifies initialized flag (TLS +0x7E0)
- Verifies presence of active session/connection handle (TLS +0x7E4)
- Delegates join request to an internal handler bound to the active connection
- Passes the provided target parameter directly to the handler

## State Effects
- No direct TLS field modification observed
- Causes a join transition via internal connection/session logic

## Return Values
- 0x1BC if SDK is not initialized
- 0x1BD if no session/connection handle is present
- Otherwise returns result from internal join handler

## Side Effects
- Initiates network activity related to joining
- No memory allocation observed at this level
- No thread creation observed

## Call Order Role
- Transition function
- Must be called after successful login
- Typically follows aw_enter or is paired with a join-reply mechanism

## Notes
- aw_join does not validate the target parameter
- Semantics of the target value are defined by the server protocol
