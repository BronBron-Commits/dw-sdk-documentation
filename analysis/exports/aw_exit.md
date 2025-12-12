# aw_exit

## Signature
int aw_exit(void);

## Role
World exit function. Requests exit from the current world or instance using the active session/connection.

## Preconditions
- aw_init must have been called
- SDK must be initialized
- A valid session/connection handle must exist

## Behavior
- Reads the thread-local SDK context
- Verifies initialized flag (TLS +0x7E0)
- Verifies presence of active session/connection handle (TLS +0x7E4)
- Delegates exit request to an internal handler bound to the active connection
- Passes a null/zero flag to the internal handler

## State Effects
- No direct TLS field modification observed
- Triggers transition out of world/instance state via internal logic

## Return Values
- 0x1BC if SDK is not initialized
- 0x1BD if no session/connection handle is present
- Otherwise returns result from internal exit handler

## Side Effects
- Initiates network activity related to world exit
- No memory allocation observed at this level
- No thread creation observed

## Call Order Role
- Transition / teardown function
- Used to leave a world or instance
- Typically followed by aw_enter, aw_term, or connection teardown

## Notes
- Does not destroy the connection itself
- Connection/session remains valid after exit unless explicitly terminated
