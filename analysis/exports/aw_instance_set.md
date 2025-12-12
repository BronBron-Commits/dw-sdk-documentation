# aw_instance_set

## Signature
int aw_instance_set(int instance);

## Role
Sets the active instance handle in the SDK context after validating it against known instances.

## Preconditions
- aw_init must have been called
- SDK must be initialized

## Behavior
- Reads the thread-local SDK context
- Verifies initialized flag (TLS +0x7E0)
- If instance parameter is non-zero:
  - Iterates over internal instance list
  - Compares provided value against known instance identifiers
  - If a match is found, stores the instance in TLS offset +0x7E4 and returns success
  - If no match is found, returns an error
- If instance parameter is zero:
  - Clears the active instance field (TLS +0x7E4)
  - Returns success

## State Effects
- Updates or clears the active instance handle in TLS
- Does not modify other SDK state

## Return Values
- 0 on success
- 0x1BC if SDK is not initialized
- 0x1BD if provided instance value is invalid or not found

## Side Effects
- No networking
- No memory allocation
- Iterates over internal instance registry

## Call Order Role
- Configuration / transition function
- Used to select an active instance after instance discovery
- Required before instance-specific operations

## Notes
- Instance validation relies on internal instance enumeration functions
- Passing 0 explicitly clears the current instance selection
