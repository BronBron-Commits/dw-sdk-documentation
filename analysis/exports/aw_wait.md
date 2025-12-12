# aw_wait

## Signature
int aw_wait(int timeout);

## Role
Waits for SDK events or internal processing to complete, optionally with a timeout.

## Preconditions
- aw_init must have been called
- SDK must be initialized

## Behavior
- Verifies SDK initialized flag (TLS +0x7E0)
- If timeout is non-zero:
  - Calculates an absolute end time using aw_tick
  - If timeout is negative, waits indefinitely
  - Enters a loop that:
    - Calls internal wait/dispatch function
    - Sleeps briefly (Sleep(1)) between iterations
    - Continues until an event is processed or timeout expires
  - Returns success after loop exits
- If timeout is zero:
  - Calls internal wait/dispatch function once
  - Returns its result directly

## State Effects
- None
- Does not modify TLS state

## Return Values
- 0 on successful wait or completion
- 0x1BC if SDK is not initialized
- For timeout == 0, returns value from internal wait/dispatch function

## Side Effects
- May block the calling thread
- Processes internal event and callback dispatch
- No direct networking initiated at this level

## Call Order Role
- Synchronization / pump function
- Intended to be called regularly in a client main loop
- Required to drive event and callback delivery

## Notes
- aw_wait is effectively the SDK event pump
- Clients must call this periodically to receive events
- Negative timeout value indicates infinite wait
