# aw_has_world_right_all

## Signature
bool aw_has_world_right_all(int right_id);

## Role
Checks whether the current session has a specific right across all worlds.

## Preconditions
- aw_init must have been called
- SDK must be initialized
- A valid session/connection handle must exist

## Behavior
- Verifies SDK initialized flag (TLS +0x7E0)
- Verifies presence of active session/connection handle (TLS +0x7E4)
- Delegates global world-right evaluation to an internal handler

## State Effects
- None
- Pure permission query

## Return Values
- 1 if the specified right is granted for all worlds
- 0 otherwise or if preconditions are not met

## Side Effects
- No networking
- No memory allocation

## Call Order Role
- Global world authority query
- Used to verify elevated or administrative permissions

## Notes
- Requires an active session context
