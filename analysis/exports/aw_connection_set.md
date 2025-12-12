# aw_connection_set

## Signature
int aw_connection_set(int connection);

## Role
Sets the current connection identifier or handle in the SDK context.

## Preconditions
- aw_init must have been called
- SDK must be initialized
- Caller is responsible for providing a valid connection value

## Behavior
- Writes the provided value into the thread-local SDK context
- Stores the value at TLS offset +0x7F4
- Does not perform validation

## State Effects
- Updates the per-thread connection field
- Overwrites any previously stored connection value

## Return Value
- Always returns 0

## Side Effects
- None
- No networking
- No memory allocation

## Call Order Role
- Configuration function
- Must be called before aw_login and other connection-dependent calls
- Typically paired with aw_connection for query

## Notes
- This function does not establish a network connection
- It only records a connection identifier used by other SDK functions
