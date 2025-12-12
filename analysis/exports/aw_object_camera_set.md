# aw_object_camera_set

## Signature
int aw_object_camera_set(uint16_t mode, int target, char *flags);

## Role
Sets or updates object-relative camera parameters for the active session.

## Preconditions
- aw_init must have been called
- SDK must be initialized
- A valid session/connection handle must exist

## Behavior
- Verifies SDK initialized flag (TLS +0x7E0)
- Verifies presence of active session/connection handle (TLS +0x7E4)
- Delegates object camera configuration to an internal handler bound to the active connection
- Passes mode, target, and flag parameters directly to the handler

## State Effects
- No direct TLS field modification observed
- Updates object-relative camera state internally

## Return Values
- 0x1BC if SDK is not initialized
- 0x1BD if no session/connection handle is present
- Otherwise returns result from internal handler

## Side Effects
- Initiates network activity related to camera configuration
- Affects client view relative to objects

## Call Order Role
- View / interaction configuration function
- Used during active world participation

## Notes
- Parameter semantics are defined by server protocol
