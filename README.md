# TCP SYN Flood Tool

A Python-based TCP SYN flood tool designed for educational purposes and network security research. This tool demonstrates how SYN flood attacks work by sending raw TCP SYN packets to a target server.

## ⚠️ DISCLAIMER

**THIS TOOL IS FOR EDUCATIONAL AND AUTHORIZED TESTING PURPOSES ONLY**

- Only use this tool on networks and systems you own or have explicit written permission to test
- Unauthorized use of this tool may violate local, state, and federal laws
- The authors are not responsible for any misuse or damage caused by this tool
- Always ensure you have proper authorization before conducting any security testing

## Features

- **Raw Packet Construction**: Builds custom IP and TCP headers from scratch
- **IP Spoofing**: Optional source IP spoofing capability
- **Multi-threading**: Configurable number of threads for increased packet rate
- **Rate Control**: Adjustable packets per second (PPS) rate
- **Response Monitoring**: Captures and displays SYN-ACK responses to verify connectivity
- **Connectivity Testing**: Sends initial test packet to verify target reachability

## Requirements

### System Requirements

- Linux operating system (required for raw socket support)
- Root/administrator privileges (required for raw socket creation)
- Python 3.6 or higher

### Python Dependencies

- No external dependencies required (uses only Python standard library)

## Installation

1. Clone or download this repository:

```bash
git clone https://github.com/ArnabDeyKabya/TCP-SYN-Food-DoS_Attack.git
cd TCP-SYN-Food-DoS_Attack
```

2. Ensure you have Python 3 installed:

```bash
python3 --version
```

3. Make the script executable (optional):

```bash
chmod +x attacker.py
```

## Usage

### Basic Usage

Run the tool with root privileges:

```bash
sudo python3 gpt.py
```

The tool will prompt you for the following parameters:

1. **Target IP**: IP address of the target server
2. **Target Port**: Port number to target (e.g., 80 for HTTP, 443 for HTTPS)
3. **Packets per second**: Rate of packet transmission
4. **Number of threads**: Number of concurrent threads for sending packets
5. **IP spoofing**: Whether to use random source IP addresses (y/n)

### Example Session

```
Target IP           : 192.168.1.100
Target Port         : 80
Packets per sec     : 1000
Number of threads   : 4
Use IP spoofing? (y/n): y
[*] Local IP: 192.168.1.50
[*] Sending test SYN (no spoof)...
[+] SYN-ACK from 192.168.1.100:80 (connectivity OK)
[*] Flooding 192.168.1.100:80 @ 1000pps across 4 threads (spoof=true)
[*] Thread 1 started (@ 250pps, spoof=True)
[*] Thread 2 started (@ 250pps, spoof=True)
[*] Thread 3 started (@ 250pps, spoof=True)
[*] Thread 4 started (@ 250pps, spoof=True)
```

To stop the tool, press `Ctrl+C`.

## Technical Details

### How It Works

1. **Packet Construction**: The tool builds raw IP and TCP packets with proper headers and checksums
2. **SYN Flood**: Sends TCP SYN packets without completing the three-way handshake
3. **Resource Exhaustion**: Causes the target server to maintain half-open connections, potentially exhausting resources
4. **Monitoring**: Captures incoming SYN-ACK responses to monitor the attack effectiveness

### Code Structure

- `checksum()`: Computes Internet checksum for packet headers
- `IPPacket`: Class for building IP headers
- `TCPPacket`: Class for building TCP headers with SYN flag
- `send_syn()`: Sends a single SYN packet
- `sniff_responses()`: Monitors incoming SYN-ACK responses
- `flood_worker()`: Worker thread function for continuous packet sending

### IP Spoofing

When IP spoofing is enabled:

- Random source IP addresses are generated for each packet
- Makes the attack harder to trace and block
- Bypasses simple IP-based filtering

When disabled:

- Uses the local machine's IP address
- Easier to detect and block
- May receive RST packets from the target

## Ethical Considerations

This tool should only be used for:

- Educational purposes to understand network security
- Authorized penetration testing with proper documentation
- Research in controlled environments
- Testing your own network infrastructure's resilience

## Legal Notice

- Ensure compliance with local laws and regulations
- Obtain proper authorization before testing any network
- Document all testing activities appropriately
- Consider the impact on network availability and users

## Limitations

- Requires root privileges for raw socket access
- Limited to Linux systems
- May be detected by modern DDoS protection systems
- Effectiveness depends on target system configuration

## Defense Mechanisms

Common defenses against SYN flood attacks include:

- SYN cookies
- Rate limiting
- Firewall rules
- Load balancers with DDoS protection
- Connection timeouts

## Contributing

This is an educational project. If you find bugs or have improvements, please ensure any contributions maintain the educational focus and include appropriate warnings about responsible use.

## License

This project is provided for educational purposes only. Use at your own risk and ensure compliance with all applicable laws and regulations.
