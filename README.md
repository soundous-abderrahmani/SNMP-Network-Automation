# SNMP Network Monitoring Lab

## About This Project
This lab shows how to use SNMP (Simple Network Management Protocol) to monitor and configure network devices remotely. I set up a Cisco router as an SNMP agent and used Packet Tracer's MIB Browser to read and change router settings.

## What I Did

### 1. Router Configuration
I configured the router (R1) with SNMP using these commands:
```cisco
snmp-server community public RO    # Read-only access
snmp-server community private RW   # Read-write access
```

*Note: The `snmp-server location` and `snmp-server contact` commands didn't work in Packet Tracer, so I set these values using SNMP SET operations instead.*

### 2. SNMP Operations
Using the MIB Browser on PC1, I performed these operations:

**GET Operations (Read):**
- Got the system name: `Router`
- Retrieved IP routing table information

**SET Operations (Write):**
- Changed system name from "Router" to "R1"
- Set system location to "ServerRoom" using OID `1.3.6.1.2.1.1.6.0`
- Set system contact to "admin@lab.com" using OID `1.3.6.1.2.1.1.4.0`

### 3. Simulation Analysis
I used Packet Tracer's simulation mode to watch the SNMP packets:
- **GET** uses UDP port 161 with community "public"
- **SET** uses UDP port 161 with community "private"
- Saw 6 SNMP messages exchanged for GET operation

## Key Learnings
- SNMP has 4 main components: Manager, Agent, MIB, and Protocol
- UDP port 161 for normal SNMP, port 162 for traps
- MIB is like a dictionary that organizes device information with OIDs
- Different community strings control access levels
- Some configurations can be done via CLI, others via SNMP SET operations

## Files
- `Lab1AN3.pkt` - Main Packet Tracer file with all configurations

## How to Test
1. Open `Lab1AN3.pkt` in Packet Tracer
2. Click on PC1 → Desktop → MIB Browser
3. Set address to 192.168.1.1
4. Use community "public" for reading, "private" for writing
5. Try these OIDs:
   - `1.3.6.1.2.1.1.5.0` - Get system name
   - `1.3.6.1.2.1.1.6.0` - Set system location
   - `1.3.6.1.2.1.1.4.0` - Set system contact
