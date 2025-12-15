Delta Worlds — Event Surface Analysis



This document records the actual event surface used by the Classic Delta Worlds SDK to define a valid, real client.



All information here is derived from static analysis (Ghidra) of the Classic SDK and related Core libraries — not Wireshark inference.



WHY EVENTS MATTER



Delta Worlds does not treat clients as stateless packet senders.



Instead, the server evaluates:



• Which events the client claims to support

• When those events are registered

• Whether the event mask matches expectations



This is enforced server-side during and after login.



KEY OBSERVATIONS (CONFIRED)



Events are validated against SdkCore\_EventId



Inside aw\_event\_set:



Event IDs are checked using System.Enum.IsDefined(SdkCore\_EventId)



Invalid or unknown IDs are rejected before registration.



This means only known EventIds are accepted. Arbitrary IDs do nothing.



Event registration directly affects server state



After an event is registered, the SDK calls:



ClassicSdk\_WorldSession\_\_SendEventMask



This sends a bitmask representing supported events to the server.



If this mask is incomplete or unexpected, the server may:



• Accept login but stall

• Drop the connection later

• Never deliver world bootstrap packets



Event IDs are offset internally



From aw\_event and aw\_event\_set:



Event IDs are mapped internally as eventId + 2000



This offset is consistent across:



• aw\_event

• aw\_event\_set

• Event dictionary lookups



This strongly suggests a fixed internal event namespace.



CONFIRMED SDK FUNCTIONS INVOLVED



aw\_event

Query current event handler



aw\_event\_set

Register event handler



ClassicSdk\_WorldSession\_\_SendEventMask

Send event capability mask



System.Enum.IsDefined(SdkCore\_EventId)

Validate event ID



EVENT MASK SERIALIZATION



From ClassicSdk\_WorldSession\_\_SendEventMask:



• PacketWriter is created with type 0x99

• Event mask is written using field 0x106

• Packet is serialized and sent over the active connection



This confirms:



• Event mask is explicitly transmitted

• Server logic depends on it



IMPLICATION FOR CUSTOM CLIENTS (ARM / NON-SDK)



A client that:



• Logs in correctly

• Sends heartbeats

• Sends ticks



But does not send a correct event mask will still be treated as non-real and disconnected.



Reproducing the event surface is mandatory.



NEXT REQUIRED WORK



Extract the full SdkCore\_EventId enum



Categorize events:

• Login

• World

• Avatar

• Chat

• Tick / Timing



Identify which events are required before world bootstrap



Replicate event registration order in non-SDK clients



EVIDENCE SOURCES



• Ghidra analysis of aw\_event

• aw\_event\_set

• ClassicSdk\_WorldSession\_\_SendEventMask

• SdkCore\_SdkCore\_Connection\_\_WaitForPacketAsync



• Runtime logging from ConsoleHarness

• SDK callback behavior during aw\_wait

