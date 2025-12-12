# aw_check_right_allW

## Signature
bool aw_check_right_allW(const wchar_t *right);

## Role
Wide-character variant of aw_check_right_all. Checks a right using a Unicode string.

## Preconditions
- SDK instance list must be initialized
- At least one instance must exist

## Behavior
- Verifies at least one instance exists
- Converts provided wide-character string into internal string representation
- Delegates rights evaluation to the same internal handler as aw_check_right_all

## State Effects
- None
- Pure query against internal rights system

## Return Values
- 1 if the specified right is granted
- 0 otherwise

## Side Effects
- No networking
- Temporary memory usage for string handling only

## Call Order Role
- Authority / permission query function
- Functionally equivalent to aw_check_right_all

## Notes
- Unicode variant bypasses codepage-based conversion
