# aw_address

## Signature
int aw_address(uint32_t address);

## Preconditions
- aw_init must have been called
- SDK must be initialized
- A valid session/connection handle must exist

## Behavior
- Checks TLS initialized flag
- Verifies presence of active session/connection handle
- Passes the provided address value to an internal handler bound to the session
- Returns the result of the internal handler

## State Effects
- No direct TLS field modification observed
- Uses existing session/connection state

## Return Values
- 0x1BC if SDK is not initialized
- 0x1BD if no session/connection handle is present
- Otherwise returns result from internal address handler

## Side Effects
- Likely updates or queries address-related state via the active connection
- No memory allocation observed at this level

## Call Order Role
- Configuration / query function
- Requires prior initialization and session setup
- Callable during connected/login phase

## Notes
- Function delegates all semantics to an internal handler
- Address parameter likely represents network or world addressing information
