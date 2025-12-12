# aw_init

## Purpose
Initializes the DeltaWorlds SDK state machine for the current thread.
This function establishes the root SDK state and must be called before
any other aw_* API (except aw_init_bind).

This is the **state zero** of the SDK.

---

## Signature
undefined4 aw_init(int param_1)

---

## Preconditions
- param_1 must be in the ASCII range:
  - 0x41 ('A') through 0x65
- If the parameter is invalid, initialization fails

---

## Behavior

1. Calls aw_term() to reset any existing SDK state
2. Acquires the thread-local SDK context (TLS slot)
3. Captures the current aw_tick() value and stores it as the time origin
4. Clears internal tables:
   - Event callback table (offset 0xE8, size 0xF8)
   - SDK callback table (offset 0x10, size 0xD8)
5. Seeds internal PRNG using:
   - Current process ID
   - Current time
   - rand()
6. Stores param_1 as the SDK "instance / universe selector"
7. Clears active world pointer
8. Sets the SDK initialized flag

---

## State Changes

- SDK.Initialized = true
- SDK.ActiveWorld = null
- SDK.InstanceId = param_1
- SDK.TimeOrigin = aw_tick() at init

This transitions the SDK from:
UNINITIALIZED → INITIALIZED

---

## Return Values

- 0 on success
- 0x1C6 if param_1 is outside the valid range

---

## Side Effects

- Resets all prior SDK state
- Resets callback registrations
- Reseeds internal randomness
- Thread-local only (no global shared state)

---

## Notes

- aw_init is idempotent only via aw_term
- Every aw_* function checks the Initialized flag set here
- This function defines the guard rails for the entire SDK

---

# aw_init_bind

## Signature
void aw_init_bind(int param_1, undefined4 param_2)

---

## Behavior

1. Registers an initialization callback or binding via FUN_10025a80
2. Immediately invokes aw_init(param_1)

---

## Notes

- aw_init_bind is a convenience wrapper
- Used when initialization must be coupled with a host-provided binding
- Does not alter aw_init semantics

---

## State Machine Role

aw_init is the **root constructor** of the DeltaWorlds SDK state machine.
All later states (world entry, events, rights, objects, avatars) are
illegal unless this function has completed successfully.

