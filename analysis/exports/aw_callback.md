# aw_callback

## Signature
int aw_callback(uint callback_id);

## Role
Retrieves or dispatches a callback for a given callback ID, depending on connection state.

## Preconditions
- aw_init must have been called
- SDK must be initialized
- callback_id must be less than 0x36

## Behavior
- Reads the thread-local SDK context
- Verifies initialized flag (TLS +0x7E0)
- Validates callback_id range (0–0x35)
- If no active session/connection handle exists:
  - Returns the callback pointer stored in the TLS callback table
- If an active session/connection handle exists:
  - Delegates callback retrieval/dispatch to an internal handler bound to the connection

## State Effects
- None
- Pure query or delegation based on connection state

## Return Values
- Returns callback pointer or handler result on success
- Returns 0 if SDK is not initialized
- Returns 0 if callback_id is out of range

## Side Effects
- No networking at this level
- No memory allocation
- May indirectly trigger callback dispatch via internal handler

## Call Order Role
- Callback access / dispatch function
- Used internally or by clients to retrieve or invoke callbacks
- Works in conjunction with aw_callback_set

## Notes
- Behavior differs based on whether a session/connection is active
- Callback storage resides in TLS at offset +0x10
