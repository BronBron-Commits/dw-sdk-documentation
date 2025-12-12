# aw_avatar_reload

## Signature
int aw_avatar_reload(int avatar_id, int flags);

## Role
Requests a reload or refresh of an avatar’s data or appearance in the active world or instance.

## Preconditions
- aw_init must have been called
- SDK must be initialized
- A valid session/connection handle must exist
- Client must be inside a world or instance

## Behavior
- Verifies SDK initialized flag (TLS +0x7E0)
- Verifies presence of active session/connection handle (TLS +0x7E4)
- Delegates avatar reload operation to an internal handler bound to the active connection
- Passes avatar identifier and flags directly to the internal handler

## State Effects
- No direct TLS field modification observed
- Triggers internal avatar refresh logic

## Return Values
- 0x1BC if SDK is not initialized
- 0x1BD if no session/connection handle is present
- Otherwise returns result from internal avatar-reload handler

## Side Effects
- Initiates network activity related to avatar reload
- May cause avatar state to be re-sent or re-applied
- No memory allocation observed at this level

## Call Order Role
- Avatar management function
- Used after avatar selection or when avatar state must be refreshed
- Can be invoked while inside a world or instance

## Notes
- Exact semantics of flags parameter are protocol-defined
- Reload behavior is enforced server-side
