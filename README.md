iPerf3
Introduction

iPerf3 is an open-source network performance testing tool designed to measure bandwidth, throughput, latency-related performance characteristics, and data transfer efficiency between two network endpoints. It is widely used by network administrators, system engineers, DevOps specialists, and IT infrastructure teams to diagnose network connectivity issues, evaluate network capacity, and verify the performance of wired and wireless connections. Available for Linux, Windows, macOS, and other Unix-like operating systems, iPerf3 supports both IPv4 and IPv6, making it suitable for testing modern network environments.

The application operates using a client-server architecture. One system runs in server mode and listens for incoming test connections, while another system acts as a client and initiates network performance tests. This approach allows administrators to measure TCP throughput, UDP bandwidth, packet loss, and jitter under different network conditions. Tests can be performed across local area networks (LAN), wide area networks (WAN), virtual private networks (VPN), data centers, and cloud infrastructure.

Key features include configurable test duration, adjustable TCP and UDP parameters, parallel data streams, bidirectional testing, reverse mode, and detailed performance statistics. Users can also specify network interfaces, ports, buffer sizes, maximum transmission units indirectly through socket settings, and reporting intervals to investigate specific network conditions.

iPerf3 is particularly useful for troubleshooting slow network connections, validating bandwidth between servers, testing firewall and routing configurations, and identifying throughput limitations. Its command-line interface makes it suitable for automated network diagnostics, infrastructure monitoring workflows, and repeatable performance benchmarking. By providing measurable network throughput results, the utility helps IT professionals distinguish application-level performance problems from underlying network limitations.

How to Install and Configure iPerf3 for Network Performance Testing

Installing iPerf3 requires selecting a compatible package for the operating system and making the executable available through the system command line. On Linux, the utility can typically be installed using the distribution's package manager. On Debian-based systems, for example, run sudo apt install iperf3. On Windows, download or install a compatible executable and launch it from PowerShell or Command Prompt. macOS users can install the application through a supported package manager.

The testing process requires two endpoints with network connectivity. Start the server on the remote machine using:

iperf3 -s

By default, the server listens on TCP port 5201. If a different port is required, specify it with the -p option:

iperf3 -s -p 5001

On the client machine, initiate a TCP throughput test by specifying the server address:

iperf3 -c 192.168.1.100

To run a test for 30 seconds, use -t 30. The -i 5 option configures five-second reporting intervals, while -P 4 creates four parallel client streams. For example:

iperf3 -c 192.168.1.100 -t 30 -i 5 -P 4

Network administrators can also test UDP performance using -u and specify the target bandwidth with -b:

iperf3 -c 192.168.1.100 -u -b 100M -t 30

Firewall rules must allow the selected test port and protocol. For standard operation, TCP port 5201 is required, while UDP testing also requires the corresponding UDP traffic to reach the server. Correct endpoint addressing, routing, and firewall configuration are essential for reliable network bandwidth measurements.

How to Measure TCP Throughput, UDP Bandwidth, Packet Loss, and Jitter

iPerf3 provides several testing modes for evaluating network performance under different traffic conditions. TCP throughput testing measures the amount of data successfully transferred between endpoints over a given period. It is useful for assessing available network bandwidth, identifying bottlenecks, and comparing performance across network paths.

For reverse TCP testing, where the server sends data to the client, use:

iperf3 -c 192.168.1.100 -R

This is particularly useful when investigating asymmetric network performance, where download and upload speeds differ significantly. Bidirectional testing can be performed with:

iperf3 -c 192.168.1.100 --bidir

UDP testing provides additional information about packet delivery quality. Unlike TCP, UDP does not automatically retransmit lost packets or regulate transmission rates through congestion control. A UDP test can therefore reveal packet loss and jitter under a specified traffic load:

iperf3 -c 192.168.1.100 -u -b 50M -t 30

The results include the configured transmission rate, achieved throughput, datagram counts, packet loss percentage, and jitter. Jitter represents variations in packet arrival timing and is particularly relevant to VoIP, video conferencing, and real-time communication systems.

For more detailed diagnostics, use -J to generate JSON output:

iperf3 -c 192.168.1.100 -t 30 -J

Structured results can be processed by scripts, monitoring platforms, and automated benchmarking pipelines. IT specialists should perform multiple tests, compare reverse and standard modes, and evaluate different parallel stream counts. Measurements should also account for CPU utilization, network interface capacity, routing, and background traffic. A single throughput result does not necessarily represent the maximum capacity or typical performance of a network connection.
