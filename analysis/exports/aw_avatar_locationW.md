# aw_avatar_locationW

## Signature
int aw_avatar_locationW(int avatar_id, int flags, const wchar_t *location);

## Role
Wide-character variant of aw_avatar_location. Requests or updates avatar location using a Unicode string.

## Preconditions
- aw_init must have been called
- SDK must be initialized
- A valid session/connection handle must exist
- Client must be inside a world or instance

## Behavior
- Verifies SDK initialized flag (TLS +0x7E0)
- Verifies presence of active session/connection handle (TLS +0x7E4)
- Converts provided wide-character string into internal string representation
- Delegates avatar location handling to the same internal handler used by aw_avatar_location

## State Effects
- No direct TLS field modification observed
- Updates or queries avatar location via internal avatar management logic

## Return Values
- 0x1BC if SDK is not initialized
- 0x1BD if no session/connection handle is present
- Otherwise returns result from internal avatar-location handler

## Side Effects
- Initiates network activity related to avatar location update or query
- Allocates temporary buffers for internal string handling
- No thread creation observed

## Call Order Role
- Avatar state function
- Used after world entry
- Functionally equivalent to aw_avatar_location with Unicode input

## Notes
- aw_avatar_location and aw_avatar_locationW share identical internal logic
- The W variant bypasses codepage-based string conversion
