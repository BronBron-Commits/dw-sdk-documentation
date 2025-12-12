# aw_avatar_location

## Signature
int aw_avatar_location(int avatar_id, int flags, char **location);

## Role
Requests or updates the location information for an avatar in the active world or instance.

## Preconditions
- aw_init must have been called
- SDK must be initialized
- A valid session/connection handle must exist
- Client must be inside a world/instance

## Behavior
- Verifies SDK initialized flag (TLS +0x7E0)
- Verifies presence of active session/connection handle (TLS +0x7E4)
- Checks internal string encoding mode (TLS +0x7E8)
- If internal encoding is Unicode:
  - Passes parameters directly to the internal handler
- If internal encoding is non-Unicode:
  - Converts provided location string to wide-character format
  - Passes converted string to the internal handler
- Delegates avatar location handling to an internal function bound to the active connection

## State Effects
- No direct TLS field modification observed
- Updates or queries avatar location via internal avatar management logic

## Return Values
- 0x1BC if SDK is not initialized
- 0x1BD if no session/connection handle is present
- Otherwise returns result from internal avatar-location handler

## Side Effects
- Initiates network activity related to avatar location update or query
- Allocates temporary buffers for string conversion when required
- No thread creation observed

## Call Order Role
- Avatar state function
- Used after successful world entry
- Required for avatar positioning and tracking

## Notes
- Location string encoding depends on internal SDK mode
- Actual semantics of avatar_id and flags are protocol-defined
