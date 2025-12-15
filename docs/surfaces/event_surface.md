# \# Event Surface (SdkCore\_EventId)

# 

# This document enumerates all valid SdkCore\_EventId values accepted by the Classic SDK.

# These values are validated by Enum\_\_IsDefinedPrimitive<UInt32> during aw\_event\_set

# and define the complete event surface a client may register.

# 

# Any client behavior outside this surface is rejected by the SDK runtime.

# 

# \## Enumeration

# 

# | ID | Name |

# |----|------|

# | 0 | AvatarAdd |

# | 1 | AvatarChange |

# | 2 | AvatarDelete |

# | 3 | CellBegin |

# | 4 | CellObject |

# | 5 | CellEnd |

# | 6 | Chat |

# | 7 | ObjectAdd |

# | 8 | ObjectDelete |

# | 9 | UniverseAttributes |

# | 10 | UniverseDisconnect |

# | 11 | WorldAttributes |

# | 12 | WorldInfo |

# | 13 | WorldDisconnect |

# | 14 | SendFile |

# | 15 | ContactState |

# | 16 | Telegram |

# | 17 | Join |

# | 18 | ObjectClick |

# | 19 | ObjectSelect |

# | 20 | AvatarClick |

# | 21 | Url |

# | 22 | UrlClick |

# | 23 | Teleport |

# | 24 | AdminWorldInfo |

# | 25 | AdminWorldDelete |

# | 26 | TerrainBegin |

# | 27 | TerrainData |

# | 28 | TerrainEnd |

# | 29 | ConsoleMessage |

# | 30 | TerrainChanged |

# | 31 | Botgram |

# | 32 | ToolbarClick |

# | 33 | UserInfo |

# | 34 | VoipData |

# | 35 | Noise |

# | 36 | Camera |

# | 37 | Botmenu |

# | 38 | ObjectBump |

# | 39 | EntityAdd |

# | 40 | EntityChange |

# | 41 | EntityDelete |

# | 42 | EntityRiderAdd |

# | 43 | EntityRiderDelete |

# | 44 | EntityRiderChange |

# | 45 | AvatarReload |

# | 46 | EntityLinks |

# | 47 | HudClick |

# | 48 | HudCreate |

# | 49 | HudDestroy |

# | 50 | HudClear |

# | 51 | CavDefinitionChange |

# | 52 | WorldCavDefinitionChange |

# | 53 | XferDisconnect |

# | 54 | XferOffer |

# | 55 | XferReply |

# | 56 | XferSend |

# | 57 | XferRequest |

# | 58 | XferCancel |

# | 59 | LaserBeam |

# | 60 | XferQuery |

# | 61 | CavTemplateChange |

# | 62 | PurchaseOffer |

# | 63 | Dialog |

# | 64 | DialogAnswer |

# | 65 | TelegramPending |

# | 66 | TelegramJournal |

# | 67 | TelegramJournalGet |

# 

# \## Behavioral Notes

# 

# \- aw\_event\_set validates EventId using Enum\_\_IsDefinedPrimitive<UInt32>.

# \- Valid registrations update the world event mask.

# \- Event mask is recomputed and transmitted immediately to the server.

# \- Missing required events lead to incomplete world synchronization.

# 

# This list represents the full and final event surface for Classic SDK clients.

# 

