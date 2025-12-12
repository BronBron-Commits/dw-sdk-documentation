# aw_camera_set

## Signature
int aw_camera_set(int camera_mode);

## Role
Sets the active camera mode or viewpoint for the client in the current world or instance.

## Preconditions
- aw_init must have been called
- SDK must be initialized
- A valid session/connection handle must exist

## Behavior
- Verifies SDK initialized flag (TLS +0x7E0)
- Verifies presence of active session/connection handle (TLS +0x7E4)
- Delegates camera mode handling to an internal handler bound to the active connection

## State Effects
- No direct TLS field modification observed
- Updates camera/view state internally

## Return Values
- 0x1BC if SDK is not initialized
- 0x1BD if no session/connection handle is present
- Otherwise returns result from internal camera-set handler

## Side Effects
- Initiates network activity related to camera/view updates
- Affects subsequent rendering and viewpoint behavior

## Call Order Role
- View configuration function
- Used during active world participation

## Notes
- Camera mode semantics are protocol-defined
