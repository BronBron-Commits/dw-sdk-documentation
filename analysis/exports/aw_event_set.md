# aw_event_set

## Signature
int aw_event_set(uint event_id, void *handler);

## Role
Registers an event handler for a specific event ID and propagates it to all active instances.

## Preconditions
- aw_init must have been called
- SDK must be initialized

## Behavior
- Reads the thread-local SDK context
- Verifies initialized flag (TLS +0x7E0)
- Validates event_id is within allowed range (0–0x3D)
- Stores event handler pointer in TLS event table (TLS +0xE8 + event_id * 4)
- Iterates over all known instances and applies the event handler to each via internal setter

## State Effects
- Updates per-thread event handler table entry
- Updates event bindings for all active instances

## Return Values
- 0 on success
- 0x1BC if SDK is not initialized
- 0x1C0 if event_id is out of range

## Side Effects
- No networking
- No memory allocation
- Updates internal instance event bindings

## Call Order Role
- Configuration function
- Must be called before events of the specified type are expected
- Typically used during setup prior to or immediately after instance creation

## Notes
- Event handler registration is global to the thread context
- Changes are propagated immediately to all instances
