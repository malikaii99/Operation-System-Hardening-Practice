# Operation-System-Hardening-Practice
<h1>Description</h1>
I examined DNS and ICMP traffic in transit by utilizing data from a network protocol analysis tool. My goal was to determine the specific network protocol involved in evaluating the cybersecurity incident.
Within the Internet layer of the TCP/IP model, IP takes data packets and structures them into IP datagrams. The content within these datagrams of an IP packet offered security analysts valuable information about potentially suspicious data packets as they traveled through the network.
I became proficient in recognizing potentially harmful network traffic, which is crucial for cybersecurity analyst. It enables me to evaluate security threats within the network and enhance overall network security

<h2>Scenario</h2>
Review the scenario below. 

You are a cybersecurity analyst working at a company that specializes in providing IT consultant services. Several customers contacted your company to report that they were not able to access the company website www.yummyrecipesforme.com, and saw the error “destination port unreachable” after waiting for the page to load. 
You are tasked with analyzing the situation and determining which network protocol was affected during this incident. To start, you visit the website and you also receive the error “destination port unreachable.” Next, you load your network analyzer tool, tcpdump, and load the webpage again. This time, you receive a lot of packets in your network analyzer. The analyzer shows that when you send UDP packets and receive an ICMP response returned to your host, the results contain an error message: “udp port 53 unreachable.” 

13:24:32.192571 IP 192.51.52444 > 203.0.113.2.domain: 35084+ A? yummyrecipesforme.com (24)

13:24:36.098564 IP 203.0.113.2 > 192.51.100.15: ICMP 203.0.113.2 udp port 53 unreachable length 254

13:26:32.192571 IP 192.51.52444 > 203.0.113.2.domain: 35084+ A? yummyrecipesforme.com (24)

13:27:15.934126 IP 203.0.113.2 > 192.51.100.15: ICMP 203.0.113.2 udp port 53 unreachable length 320

13:28:32.192571 IP 192.51.52444 > 203.0.113.2.domain: 35084+ A? yummyrecipesforme.com (24)

13:28:50.022967 IP 203.0.113.2 > 192.51.100.15: ICMP 203.0.113.2 udp port 53 unreachable length 150


- <a> In the DNS and ICMP logs, you will find the following information: </a>
    -  In the first two lines of the log file, you see the initial outgoing request from your computer to the DNS server requesting the IP address of yummyrecipesforme.com. This request is sent in a UDP packet.
    -  Next, you find timestamps that indicate when the event happened. In the log, this is the first sequence of numbers displayed. For example: 13:24:32.192571. This displays the time 1:24 p.m., 32.192571 seconds.
    -  The source and destination IP address is next. In the error log, this information is displayed as: 192.51.100.15.52444 > 203.0.113.2.domain. The IP address to the left of the greater than (>) symbol is the source address. In this example, the source is your computer’s IP address. The IP address to the right of the greater than (>) symbol is the destination IP address. In this case, it is the IP address for the DNS server: 203.0.113.2.domain
    -  The second and third lines of the log show the response to your initial ICMP request packet. In this case, the ICMP 203.0.113.2 line is the start of the error message indicating that the ICMP packet was undeliverable to the port of the DNS server.
    -  Next are the protocol and port number, which displays which protocol was used to handle communications and which port it was delivered to. In the error log, this appears as: udp port 53 unreachable. This means that the UDP protocol was used to request a domain name resolution using the address of the DNS server over port 53. Port 53, which aligns to the .domain extension in 203.0.113.2.domain, is a well-known port for DNS service. The word “unreachable” in the message indicates the message did not go through to the DNS server. Your browser was not able to obtain the IP address for yummyrecipesforme.com, which it needs to access the website because no service was listening on the receiving DNS port as indicated by the ICMP error message “udp port 53 unreachable.”
    -  The remaining lines in the log indicate that ICMP packets were sent two more times, but the same delivery error was received both times. 


Now that you have captured data packets using a network analyzer tool, it is your job to identify which network protocol and service were impacted by this incident. Then, you will need to write a follow-up report.
As an analyst, you can inspect network traffic and network data to determine what is causing network-related issues during cybersecurity incidents. Later in this course, you will demonstrate how to manage and resolve incidents. For now, you only need to analyze the situation. 


<h3>Part 1: Provide a summary of the problem found in the DNS and ICMP traffic log</h3>
The UDP protocol reveals that the DNS was unreachable; could not retrieve the IP address. This is based on the results of the network analysis, which show that the ICMP echo reply returned the error message: udp port 53 is unreachable. The port noted in the error message is used for DNS service. The most likely issue is that DNS was unable to pick up the service, which led to the error message.
<h3>Part 2: Explain your analysis of the data and provide at least one cause of the incident</h3>
The incident occurred at 1:23 p.m. Customers were trying to access the website but were unable to, so they reported the incident, indicating that an error “destination port unreachable” was the outcome after the loading process. During the investigation, the IT department first tried to access the website and received the same error, then used a network packet analyzer: ICMP which provided details about the incident. There was no service being picked up by the receiving DNS port, as indicated by the ICMP error message “udp port 53 unreachable. The DNS server might be down due to a successful Denial of Service attack or a misconfiguration.
