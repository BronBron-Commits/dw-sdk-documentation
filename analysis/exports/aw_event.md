# aw_event / aw_event_set

## Summary
Defines and queries event handler bindings for the DeltaWorlds SDK.
These functions form the core of the SDK's event-dispatch layer and
are fundamental to the runtime state machine.

---

## aw_event

### Prototype
undefined4 aw_event(uint event_id)

### Description
Returns the currently registered event handler for a given event ID.

If an instance context exists, the handler is queried from the instance.
Otherwise, the handler is read from the global SDK event table.

### Preconditions
- SDK must be initialized
- event_id < 0x3E (62)

### Behavior
- If SDK not initialized: returns 0
- If no active instance:
  - Reads handler from global event table at offset 0xE8
- If instance exists:
  - Delegates lookup to instance-specific event table

### Return Value
- Event handler pointer if present
- 0 otherwise

### Notes
- Does not trigger or invoke the event
- Pure lookup function
- No memory allocation
- No networking

---

## aw_event_set

### Prototype
undefined4 aw_event_set(uint event_id, undefined4 handler)

### Description
Registers an event handler for a given event ID.
Updates both the global SDK state and all active instances.

### Preconditions
- SDK must be initialized
- event_id <= 0x3D (61)

### Behavior
- Stores handler in global event table at offset 0xE8
- Iterates all active instances
- Propagates handler into each instance's event table

### Return Values
- 0 on success
- 0x1BC if SDK not initialized
- 0x1C0 if event_id out of range

### Side Effects
- Mutates global SDK state
- Mutates per-instance event state
- No immediate event execution

---

## State Machine Role

- Defines allowable transitions via event bindings
- Separates event declaration from execution
- Enables deterministic event routing
- Supports both global and instance-scoped behavior

---

## Observations

- Event ID space is fixed and bounded
- Handlers are function pointers
- Design enforces explicit event registration
- Strong indicator of a deterministic, table-driven state machine

