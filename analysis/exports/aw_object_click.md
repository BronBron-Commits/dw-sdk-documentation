# aw_object_click

## Signature
int aw_object_click(void);

## Role
Sends an object click interaction event for the currently targeted object.

## Preconditions
- aw_init must have been called
- SDK must be initialized
- A valid session/connection handle must exist

## Behavior
- Verifies SDK initialized flag (TLS +0x7E0)
- Verifies presence of active session/connection handle (TLS +0x7E4)
- Delegates object click handling to an internal handler bound to the active connection

## State Effects
- No direct TLS field modification observed
- Triggers object interaction logic internally

## Return Values
- 0x1BC if SDK is not initialized
- 0x1BD if no session/connection handle is present
- Otherwise returns result from internal object-click handler

## Side Effects
- Initiates network activity related to object interaction
- May trigger server-side scripts or events

## Call Order Role
- Object interaction function
- Used during active world participation

## Notes
- Object identity is implied by current selection or server context
