# traceroute

My Python networking project uses low-level ICMP **ping** and **traceroute** style behavior using raw sockets.

## What this project is

This repository contains a single Python module (`traceroute.py`) with an `IcmpHelperLibrary` class that:

- Builds ICMP Echo Request packets manually (type, code, checksum, identifier, sequence number).
- Sends packets using raw sockets.
- Receives and parses ICMP replies (Echo Reply, Time Exceeded, Destination Unreachable).
- Validates reply fields from the original request.
- Provides two workflows:
  - `sendPing(host)` for ping-style RTT/loss stats.
  - `traceRoute(host)` for hop-by-hop path probing by incrementing TTL.

## Tech used

- **Language:** Python 3
- **Networking APIs:** `socket`, `select`
- **Packet packing/parsing:** `struct`
- **Timing:** `time`
- **OS/process metadata:** `os`
- **Protocol focus:** ICMP over IPv4 (raw socket `IPPROTO_ICMP`)

## Skills demonstrated

Practical networking and software-engineering skills, including:

- Software engineering
- Systems programming
- Networking
- Backend engineering
- Infrastructure and platform work
- Technical security work
- Binary protocol construction and parsing.
- Checksum computation for ICMP packets.
- Socket programming with timeout/select handling.
- RTT measurement and ping statistics (min/avg/max and loss).
- Traceroute logic by controlled TTL increments.
- OOP structure with nested packet/reply classes.
- Defensive response validation (identifier, sequence number, payload checks).

## How to use

> Raw ICMP sockets usually require administrator/root privileges.

1. Make sure Python 3 is installed.
2. Run the script (often with elevated permissions):

```bash
sudo python3 traceroute.py
```

3. Open `main()` in `traceroute.py` and choose behavior by uncommenting one call:

- `icmpHelperPing.sendPing("www.google.com")`
- `icmpHelperPing.traceRoute("www.google.com")`

4. Replace the host/IP as needed.

## Output you can expect

- **Ping mode:** per-request RTT lines plus packet loss and min/avg/max summary.
- **Traceroute mode:** per-TTL responses showing hop behavior until destination reached or timeout limit hit.

## Notes and limitations

- Current `main()` is configured for ping by default.
- Because this uses live network conditions and ICMP handling via intermediate routers, output may vary by host, route, firewall policy, and platform permissions.
- This implementation targets educational understanding of ICMP internals and route discovery mechanics.
