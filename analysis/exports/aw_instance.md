# aw_instance

## Signature
int aw_instance(void);

## Role
Query function that returns the current instance-related handle or identifier from the SDK context.

## Preconditions
- aw_init must have been called
- SDK must be initialized

## Behavior
- Reads the thread-local SDK context
- Returns the value stored at TLS offset +0x7E4
- Does not perform validation or side effects

## State Effects
- None
- Pure read of TLS state

## Return Value
- Returns the current instance or session handle
- A return value of 0 indicates no active instance/session

## Side Effects
- None
- No networking
- No memory allocation

## Call Order Role
- Query / inspection function
- Safe to call anytime after aw_init
- Used to retrieve the active instance handle

## Notes
- Shares the same underlying handle as connection/session-related functions
- Does not distinguish between connection and instance semantics internally
