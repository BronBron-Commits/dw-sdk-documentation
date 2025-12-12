# aw_object_delete

## Signature
int aw_object_delete(void);

## Role
Deletes the currently selected object from the active world or instance.

## Preconditions
- aw_init must have been called
- SDK must be initialized
- A valid session/connection handle must exist
- An object must be selected or implicitly targeted

## Behavior
- Verifies SDK initialized flag (TLS +0x7E0)
- Verifies presence of active session/connection handle (TLS +0x7E4)
- Delegates object deletion request to an internal handler bound to the active connection

## State Effects
- No direct TLS field modification observed
- Removes object via internal object lifecycle logic

## Return Values
- 0x1BC if SDK is not initialized
- 0x1BD if no session/connection handle is present
- Otherwise returns result from internal object-delete handler

## Side Effects
- Initiates network activity related to object removal
- Frees server-side object resources

## Call Order Role
- World modification / teardown function
- Used after object creation and selection
- Completes object lifecycle

## Notes
- Object selection semantics are handled internally
