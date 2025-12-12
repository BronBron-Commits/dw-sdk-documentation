# aw_enter / aw_enterW

## Signatures
int aw_enter(char **world_name);
int aw_enterW(const wchar_t *world_name);

## Role
World entry function. Requests entry into a world instance using the active session/connection.

## Preconditions
- aw_init must have been called
- SDK must be initialized
- A valid session/connection handle must exist

## Behavior
- Verifies SDK initialized flag
- Verifies presence of active session/connection handle (TLS +0x7E4)
- Determines string handling mode based on internal encoding flag (TLS +0x7E8)
- Reads boolean flag via aw_bool(0x148) to influence entry behavior
- Converts world name to internal wide-string representation if required
- Delegates world entry request to internal handler bound to the active connection

## State Effects
- No direct TLS field modification observed
- Triggers transition into world-entry state via internal handler

## Return Values
- 0x1BC if SDK is not initialized
- 0x1BD if no session/connection handle is present
- Otherwise returns result from internal world-entry handler

## Side Effects
- Initiates network request to enter a world
- Allocates temporary string conversion buffers
- No thread creation observed

## Call Order Role
- Transition function
- Must be called after successful login/session setup
- Required before object, avatar, or world interaction APIs

## Notes
- aw_enter and aw_enterW share identical semantics
- ANSI version conditionally converts to wide string based on internal encoding state
- Boolean flag 0x148 likely controls optional entry behavior or feature gating
