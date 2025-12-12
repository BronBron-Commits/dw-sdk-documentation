# aw_world_attribute_set

## Signature
int aw_world_attribute_set(uint attribute, const char *value);

## Role
Sets a world attribute if it is not already defined.

## Preconditions
- aw_init must have been called
- SDK must be initialized
- A valid session/connection handle must exist
- Caller must have appropriate world permissions

## Behavior
- Verifies SDK initialized flag (TLS +0x7E0)
- Verifies presence of active session/connection handle (TLS +0x7E4)
- Validates value length does not exceed 255 bytes
- Checks internal string encoding mode (TLS +0x7E8)
- Converts value to internal Unicode representation if required
- Delegates attribute assignment to internal property setter
- Attribute is only set if not already defined

## State Effects
- May modify world attribute state on the server
- No local TLS modification observed

## Return Values
- 0 on success
- 0x1BC if SDK is not initialized
- 0x1BD if no session/connection handle is present
- 0x1C2 if value exceeds maximum length
- Other error codes as defined by internal setter

## Side Effects
- Initiates network activity related to world configuration
- Temporary memory allocation for string conversion

## Call Order Role
- World configuration function
- Used during world setup or initialization

## Notes
- Does not overwrite existing attributes
- Attribute identifiers and semantics are protocol-defined
