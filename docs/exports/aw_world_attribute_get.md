# aw_world_attribute_get

## Signature
void aw_world_attribute_get(uint attribute, uint *type, char *value);

## Role
Retrieves the value of a world attribute for the active world/session.

## Preconditions
- aw_init must have been called
- SDK must be initialized
- A valid session/connection handle must exist
- Caller must provide a writable buffer for value

## Behavior
- Verifies SDK initialized flag (TLS +0x7E0)
- Verifies presence of active session/connection handle (TLS +0x7E4)
- Checks internal string encoding mode (TLS +0x7E8)
- If Unicode mode:
  - Passes output buffer directly to internal handler
- If non-Unicode mode:
  - Retrieves value into an internal wide-character buffer
  - Converts the result into the caller-provided ANSI buffer
- Writes attribute type to the provided type pointer

## State Effects
- None
- Pure query against world state

## Return Values
- None (void)
- Failure results in no modification of output buffers

## Side Effects
- No networking initiated at this level
- Temporary stack buffer usage for string conversion

## Call Order Role
- World data query function
- Used to inspect world metadata and configuration

## Notes
- Caller is responsible for buffer size
- Attribute identifiers are protocol-defined
