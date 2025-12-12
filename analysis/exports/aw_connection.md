# aw_connection

## Signature
int aw_connection(void);

## Role
Query function that returns the current connection identifier or state value.

## Preconditions
- aw_init must have been called
- SDK must be initialized

## Behavior
- Reads the thread-local SDK context
- Returns the value stored at TLS offset +0x7F4
- Does not perform validation or side effects

## State Effects
- None
- Pure read of TLS state

## Return Value
- Returns the current connection value from the SDK context
- Value is likely set by aw_connection_set or connection setup routines

## Side Effects
- None
- No networking
- No memory allocation

## Call Order Role
- Query / inspection function
- Safe to call anytime after aw_init
- Used to check connection status or identifier

## Notes
- aw_connection does not create or modify a connection
- A return value of 0 likely indicates no active connection
