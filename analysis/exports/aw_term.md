# aw_term

## Signature
void aw_term(void);

## Role
SDK teardown / cleanup function. Inverse of aw_init.

## Preconditions
- May be called after aw_init
- Safe to call even if partially initialized
- Operates on thread-local SDK context

## Behavior
- Drains internal work queue until empty
- Processes and frees queued internal items
- Releases owned secondary resource handles
- Clears per-thread SDK state

## State Effects
- Frees queued internal objects
- Releases session/connection-related handle (if present)
- Clears TLS fields:
  - initialized flag
  - error/handle field
  - SDK mode/version

## Side Effects
- Memory deallocation
- Internal queue processing
- No networking
- No file I/O
- No thread creation

## Call Order Role
- Teardown
- Returns SDK to uninitialized state
- aw_init must be called again before further SDK use

## Notes
- Ensures no pending internal work remains after return
- Designed to be idempotent per thread
