# aw_avatar_click

## Signature
int aw_avatar_click(int avatar_id);

## Role
Sends an avatar click interaction event for the specified avatar in the active world or instance.

## Preconditions
- aw_init must have been called
- SDK must be initialized
- A valid session/connection handle must exist
- Client must be inside a world or instance

## Behavior
- Verifies SDK initialized flag (TLS +0x7E0)
- Verifies presence of active session/connection handle (TLS +0x7E4)
- Delegates avatar click handling to an internal handler bound to the active connection
- Passes the avatar identifier directly to the internal handler

## State Effects
- No direct TLS field modification observed
- Triggers avatar interaction logic internally

## Return Values
- 0x1BC if SDK is not initialized
- 0x1BD if no session/connection handle is present
- Otherwise returns result from internal avatar-click handler

## Side Effects
- Initiates network activity related to avatar interaction
- May trigger server-side events or callbacks
- No memory allocation observed at this level

## Call Order Role
- Avatar interaction function
- Used during active world or instance participation
- Can trigger scripted or interactive avatar behaviors

## Notes
- Semantics of avatar click handling are defined by server-side logic
- Often paired with avatar-related callbacks or events
