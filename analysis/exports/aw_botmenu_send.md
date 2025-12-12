# aw_botmenu_send

## Signature
int aw_botmenu_send(void);

## Role
Sends a bot menu request or update using the active session/connection.

## Preconditions
- aw_init must have been called
- SDK must be initialized
- A valid session/connection handle must exist

## Behavior
- Reads the thread-local SDK context
- Verifies initialized flag (TLS +0x7E0)
- Verifies presence of active session/connection handle (TLS +0x7E4)
- Delegates bot menu send operation to an internal handler bound to the active connection

## State Effects
- No direct TLS field modification observed
- Relies on existing session/connection state

## Return Values
- 0x1BC if SDK is not initialized
- 0x1BD if no session/connection handle is present
- Otherwise returns result from internal bot menu send handler

## Side Effects
- Initiates network activity related to bot menu transmission
- No memory allocation observed at this level
- No thread creation observed

## Call Order Role
- Action / messaging function
- Callable after successful login and world/instance entry
- Used by bots or automated agents to present menu options

## Notes
- Function takes no parameters; menu content is assumed to be preconfigured
- Semantics of bot menu handling are defined by server protocol
