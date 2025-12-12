# aw_avatar_set

## Signature
int aw_avatar_set(int avatar_id);

## Role
Selects or sets the active avatar for the current session within the active world or instance.

## Preconditions
- aw_init must have been called
- SDK must be initialized
- A valid session/connection handle must exist
- Client must be inside a world or instance

## Behavior
- Verifies SDK initialized flag (TLS +0x7E0)
- Verifies presence of active session/connection handle (TLS +0x7E4)
- Delegates avatar selection logic to an internal handler bound to the active connection
- Passes the avatar identifier directly to the internal handler

## State Effects
- No direct TLS field modification observed
- Updates internal avatar selection state

## Return Values
- 0x1BC if SDK is not initialized
- 0x1BD if no session/connection handle is present
- Otherwise returns result from internal avatar-set handler

## Side Effects
- Initiates network activity related to avatar selection
- May affect subsequent avatar-related queries and updates
- No memory allocation observed at this level

## Call Order Role
- Avatar configuration function
- Must be called after world entry
- Typically precedes avatar movement, location updates, or interactions

## Notes
- Avatar identity and validity are enforced by server-side logic
- Function does not perform local validation on avatar_id
