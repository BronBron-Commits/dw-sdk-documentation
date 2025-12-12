# aw_object_camera

## Signature
int aw_object_camera(int *camera_info);

## Role
Queries or retrieves camera-related information associated with an object.

## Preconditions
- aw_init must have been called
- SDK must be initialized
- A valid session/connection handle must exist

## Behavior
- Verifies SDK initialized flag (TLS +0x7E0)
- Verifies presence of active session/connection handle (TLS +0x7E4)
- Delegates object camera query to an internal handler bound to the active connection

## State Effects
- No direct TLS field modification observed
- Populates camera information via internal logic

## Return Values
- Returns result from internal object-camera handler
- Returns 0 if SDK is not initialized or no connection exists

## Side Effects
- No networking beyond query signaling
- No memory allocation observed at this level

## Call Order Role
- Query / inspection function
- Used to retrieve camera parameters tied to an object

## Notes
- Structure and semantics of camera_info are protocol-defined
