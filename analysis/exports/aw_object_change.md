# aw_object_change

## Signature
int aw_object_change(void);

## Role
Applies property changes to the currently selected or pending object in the active world or instance.

## Preconditions
- aw_init must have been called
- SDK must be initialized
- A valid session/connection handle must exist
- An object must be in a modifiable state (e.g., recently added or selected)

## Behavior
- Verifies SDK initialized flag (TLS +0x7E0)
- Verifies presence of active session/connection handle (TLS +0x7E4)
- Delegates object change operation to an internal handler bound to the active connection

## State Effects
- No direct TLS field modification observed
- Updates object state via internal object management logic

## Return Values
- 0x1BC if SDK is not initialized
- 0x1BD if no session/connection handle is present
- Otherwise returns result from internal object-change handler

## Side Effects
- Initiates network activity related to object property updates
- May modify server-side object state

## Call Order Role
- World modification function
- Typically follows aw_object_add or aw_object_select
- Used to finalize or update object properties

## Notes
- Actual property data is assumed to be staged prior to this call
