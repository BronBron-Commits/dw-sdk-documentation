# aw_callback_set

## Signature
int aw_callback_set(uint callback_id, void *callback);

## Role
Registers a callback function for a specific callback ID and propagates it to all active instances.

## Preconditions
- aw_init must have been called
- SDK must be initialized

## Behavior
- Verifies SDK initialized flag (TLS +0x7E0)
- Validates callback_id is within allowed range (0–0x35)
- Stores callback pointer in TLS callback table (TLS +0x10 + callback_id * 4)
- Iterates over all known instances and applies the callback pointer to each via internal setter

## State Effects
- Updates per-thread callback table entry
- Updates callback bindings for all active instances

## Return Values
- 0 on success
- 0x1BC if SDK is not initialized
- 0x1C0 if callback_id is out of range

## Side Effects
- No networking
- No memory allocation
- Updates internal instance callback bindings

## Call Order Role
- Configuration function
- Must be called before events relying on the specified callback
- Typically used during setup prior to entering a world or instance

## Notes
- Callback registration is global to the thread context
- Changes are propagated immediately to all instances
