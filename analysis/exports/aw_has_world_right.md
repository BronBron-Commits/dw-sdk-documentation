# aw_has_world_right

## Signature
bool aw_has_world_right(int world_id, int right_id);

## Role
Checks whether the current session has a specific right within a given world.

## Preconditions
- aw_init must have been called
- SDK must be initialized
- A valid session/connection handle must exist

## Behavior
- Verifies SDK initialized flag (TLS +0x7E0)
- Verifies presence of active session/connection handle (TLS +0x7E4)
- Delegates world-right evaluation to an internal handler

## State Effects
- None
- Pure permission query

## Return Values
- 1 if the specified world right is granted
- 0 otherwise or if preconditions are not met

## Side Effects
- No networking
- No memory allocation

## Call Order Role
- World authority / permission query
- Used to gate world-scoped operations

## Notes
- Requires an active world/session context
