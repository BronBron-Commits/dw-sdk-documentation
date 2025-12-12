# aw_check_right

## Signature
bool aw_check_right(int target, const char *right);

## Role
Checks whether a specific right is granted for a given target entity.

## Preconditions
- SDK instance list must be initialized
- At least one instance must exist
- Does not require aw_enter, but requires instance availability

## Behavior
- Retrieves thread-local SDK context
- Verifies at least one instance exists via internal instance enumeration
- Uses the first available instance for rights checking
- Checks internal string encoding mode (TLS +0x7E8)
- If Unicode mode:
  - Passes parameters directly to internal rights checker
- If non-Unicode mode:
  - Converts right string to wide-character format
  - Passes converted string to internal rights checker

## State Effects
- None
- Pure query against internal rights system

## Return Values
- 1 if the specified right is granted
- 0 if the right is not granted or prerequisites are not met

## Side Effects
- No networking initiated at this level
- No memory allocation beyond temporary string conversion

## Call Order Role
- Authority / permission query function
- Used to gate object, world, and avatar operations

## Notes
- Rights are evaluated against the active or first instance
- Target parameter semantics are protocol-defined
