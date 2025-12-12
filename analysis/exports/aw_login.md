# aw_login

## Signature
int aw_login(void);

## Preconditions
- aw_init must have been called
- SDK must be in initialized state
- A valid session/connection handle must exist

## Behavior
- Checks TLS initialized flag
- Verifies presence of active session/connection handle
- Invokes internal login routine using existing handle
- Returns result of login attempt

## State Effects
- No direct TLS field modification observed
- Relies on existing session/connection state

## Return Values
- 0x1BC if SDK is not initialized
- 0x1BD if no session/connection handle is present
- Otherwise returns result from internal login handler

## Side Effects
- Likely performs network login via existing connection
- No memory allocation observed at this level

## Call Order Role
- Transition function
- Must be called after aw_init and connection/session setup
- Required before world entry or active interaction

## Notes
- aw_login does not create a connection; it assumes one already exists
- Login semantics are delegated to internal handler
