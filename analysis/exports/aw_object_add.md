# aw_object_add

## Signature
int aw_object_add(void);

## Role
Requests creation of a new object in the current world or instance using the active session/connection.

## Preconditions
- aw_init must have been called
- SDK must be initialized
- A valid session/connection handle must exist
- Client must be inside a world/instance

## Behavior
- Reads the thread-local SDK context
- Verifies initialized flag (TLS +0x7E0)
- Verifies presence of active session/connection handle (TLS +0x7E4)
- Delegates object creation request to an internal handler bound to the active connection

## State Effects
- No direct TLS field modification observed
- Triggers object creation via internal world/object management logic

## Return Values
- 0x1BC if SDK is not initialized
- 0x1BD if no session/connection handle is present
- Otherwise returns result from internal object-add handler

## Side Effects
- Initiates network activity related to object creation
- May allocate internal object tracking structures
- No thread creation observed at this level

## Call Order Role
- Action / world modification function
- Must be called after successful world entry
- Precedes object configuration functions such as aw_object_change

## Notes
- Object properties are likely set via subsequent calls
- Object ID assignment is handled internally by the server
