\# ClassicSdk Driver SetEvent Behavior



\## Function

ClassicSdk\_ClassicSdk\_Driver\_\_SetEvent(EventId, Callback)



\## Purpose

Maintains the runtime mapping between SdkCore\_EventId values and their

registered managed delegates. This function does NOT assign event mask bits.



\## Storage

Event registrations are stored in:



Driver::\_\_GCSTATICS + 0x78  

Type: ConcurrentDictionary<EventId, Delegate>



\## Behavior



\### Callback Removal

If Callback == NULL:

\- The EventId entry is removed from the dictionary using TryRemove

\- The event will no longer participate in event mask generation



\### Callback Registration

If Callback != NULL:

\- The unmanaged function pointer is wrapped into a managed delegate

\- The dictionary is updated using AddOrUpdate(EventId, Delegate)



No event mask bits are computed or modified here.



\## Event Mask Relationship

SetEvent does not determine which bit corresponds to an event.



Event mask bits are derived later by:

\- WorldSession.GetEventMask()

\- Iterating session-owned OrderedDictionary entries

\- OR-ing per-entry mask values when a corresponding EventId exists in the Driver dictionary



\## Implications

\- SdkCore\_EventId numeric values do not map directly to mask bits

\- Mask bit positions are determined by session state and registration order

\- This design preserves backward compatibility across protocol versions



