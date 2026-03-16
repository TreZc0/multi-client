# OoTMM Multi-Client

A middleware client that connects OoTMM emulators to the multiworld server for item sync.

## Features

- **Dual emulator support**: Project64 (PJ64) and Ares
- **Item synchronization**: Items found by one player appear for others

## Requirements

- **Emulator**: Project64 or Ares with debug/GDB stub enabled
  - PJ64: Listening on `localhost:13249`
  - Ares: Listening on `localhost:9123`
- **Server**: Connects to `multi.ootmm.com:13248` by default

## Building

### Windows (Visual Studio)
```bash
mkdir build
cd build
cmake .. -A x64
cmake --build . --config Release
```

### Windows (MinGW)
```bash
mkdir build
cd build
cmake .. -G "MinGW Makefiles"
cmake --build . --config Release
```

The executable will be in `build/bin/Release/MultiClient.exe`

## Usage

```bash
MultiClient.exe [server_host] [server_port]
```

**Examples:**
```bash
# Connect to default server
MultiClient.exe

# Connect to custom server
MultiClient.exe example.com 13248

# Connect to localhost server
MultiClient.exe localhost 13248
```

## Logging

The client provides detailed logging for debugging and monitoring:

### Outgoing Items
```
ITEM OUT - FROM: 1, TO: 2, GAME: 0, KEY: 1A3F, GI: 0053, FLAGS: 0004
ITEM OUT - FROM: 1, TO: 2, GAME: 0, KEY: 2B7E, GI: 0012, FLAGS: 0000 [ALREADY SENT]
```

### Incoming Items
```
LEDGER APPLY #4216 - from: Player 2, to: Player 1
```

**Log Fields:**
- **FROM/TO**: Player IDs
- **GAME**: Game instance ID
- **KEY**: Location check identifier (hex)
- **GI**: GetItem ID (hex)
- **FLAGS**: Item flags (hex)
- **[ALREADY SENT]**: Indicates duplicate send attempt
