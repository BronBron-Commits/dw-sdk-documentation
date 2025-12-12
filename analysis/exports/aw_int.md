# aw_int / aw_int_set

## Status
Behavior locked via Ghidra analysis.

## Threading Model
- Uses thread-local storage (TLS)
- TLS slot:
  *(ThreadLocalStoragePointer + _tls_index * 4)

## Required TLS State
The following fields must be valid in the thread-local context:

Offset   Description
0x7E0    Initialized / valid flag
0x7E4    Pointer to active StateObject

If either is invalid, the call fails deterministically.

---

## aw_int

Signature (as observed):
  int aw_int(uint32_t property_id);

Behavior
- Retrieves an integer property from the active StateObject
- Reads from the StateObject property bag at (state + 4)
- Returns 0 if:
  - SDK is not initialized for the calling thread
  - No active StateObject is bound

Notes
- property_id is a logical property identifier, not an array index
- Read-only accessor
- Thread-local; values do not cross threads

---

## aw_int_set

Signature (as observed):
  int aw_int_set(uint32_t property_id, int value);

Behavior
- Sets an integer property on the active StateObject
- Writes into the same property bag consumed by other aw_* calls

Error Codes
Code    Meaning
0x1BC   SDK not initialized for this thread
0x1BD   No active StateObject bound
0x1C3   Property exists but is read-only or locked

Notes
- Serves as a parameter transport mechanism for many other SDK calls
- Overwrites existing value for the same property_id
- Thread-local; must be called from the same thread as the consumer call

---

## Internal Calls
- StateObject_GetIntProperty(state + 4, property_id)
- StateObject_SetIntProperty(state + 4, property_id, value)
