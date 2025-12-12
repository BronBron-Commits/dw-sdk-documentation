# aw_object_select

## Signature
int aw_object_select(void);

## Role
Selects or targets an object for subsequent object-related operations.

## Preconditions
- aw_init must have been called
- SDK must be initialized
- A valid session/connection handle must exist

## Behavior
- Verifies SDK initialized flag (TLS +0x7E0)
- Verifies presence of active session/connection handle (TLS +0x7E4)
- Delegates object selection logic to an internal handler bound to the active connection

## State Effects
- No direct TLS field modification observed
- Updates internal object selection state

## Return Values
- 0x1BC if SDK is not initialized
- 0x1BD if no session/connection handle is present
- Otherwise returns result from internal object-select handler

## Side Effects
- No direct networking beyond selection signaling
- No memory allocation observed at this level

## Call Order Role
- Selection / targeting function
- Used before aw_object_change or aw_object_delete

## Notes
- Selection context is maintained internally
- Object identity is implied by prior operations or server state
