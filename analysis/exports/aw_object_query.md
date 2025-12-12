# aw_object_query

## Signature
int aw_object_query(void);

## Role
Queries information about objects in the active world or instance.

## Preconditions
- aw_init must have been called
- SDK must be initialized
- A valid session/connection handle must exist

## Behavior
- Verifies SDK initialized flag (TLS +0x7E0)
- Verifies presence of active session/connection handle (TLS +0x7E4)
- Delegates object query operation to an internal handler bound to the active connection

## State Effects
- No direct TLS field modification observed
- Retrieves object state or metadata via internal logic

## Return Values
- 0x1BC if SDK is not initialized
- 0x1BD if no session/connection handle is present
- Otherwise returns result from internal object-query handler

## Side Effects
- Initiates network activity related to object state retrieval
- No memory allocation observed at this level

## Call Order Role
- Query / inspection function
- Used to inspect object state after creation or modification

## Notes
- Query results are delivered via events or callbacks
