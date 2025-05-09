JAMII COMPANY - RIP
Overview
This topology represents an enterprise network segmented by VLANs across different floors and departments, connected to a branch office. RIP v2 is used for dynamic routing between the Main Router, Branch Router, and Cloud Router.
 
Core Components
•	Main Router (2911) – Central router for the enterprise network.
•	Main L3 Switch (3560-24PS) – Handles VLAN routing within the main site.
•	Branch Router (2911) – Connects the branch site to the main site.
•	Branch L3 Switch (3560-24PS) – VLAN routing at the branch site.
•	Cloud Router (2911) – Connects to an external email server.

Routing Protocol
RIP v2 Configuration:
•	Used between: Main Router, Branch Router, and Cloud Router.
•	RIP networks advertised:
o	10.10.10.0/30 (Main ↔ Branch)
o	10.10.10.4/30 (Main ↔ Cloud)
o	All internal subnets are summarized at the Main Router.

VLAN Segmentation
Router	Role	Connections
Main Router	Inter-VLAN Routing + RIP	Trunk to Main Switch, Branch, Cloud
Branch Router	RIP Peer	Branch Switch, Main Router
Cloud Router	External Connectivity	Email Server, Main Router

VLAN	Department	Subnet	Router Sub interface IP
10	ADMIN	192.168.1.0/24	192.168.1.1
20	HR	192.168.2.0/24	192.168.2.1
30	FINANCE	192.168.3.0/24	192.168.3.1
40	BUSINESS	192.168.4.0/24	192.168.4.1
50	E&C	192.168.5.0/24	192.168.5.1
60	A&D	192.168.6.0/24	192.168.6.1
70	LABS	192.168.7.0/24	192.168.7.1
80	IT	192.168.8.0/24	192.168.8.1

Branch Network VLANs
VLAN	Name	Subnet	Router IP
90	STAFF	192.168.9.0/24	192.168.9.1
100	GUEST	192.168.10.0/24	192.168.10.1
The branch router also uses sub-interfaces (e.g., Gig0/0.90, Gig0/0.100) for inter-VLAN routing.
Server Roles
Server	VLAN	IP Address	Role
EMAIL	N/A	20.0.0.2	External Email
WEB SERVER	80	192.168.8.3	Web Hosting
FTP SERVER	80	192.168.8.4	File Storage

Interconnection IPs
Link	Subnet	IPs
Main ↔ Cloud	10.10.10.4/30	Main: .5, Cloud: .6
Main ↔ Branch	10.10.10.0/30	Main: .1, Branch: .2

Security and Access
•	VLANs separate departmental traffic.
•	RIP does not support authentication by default; recommend MD5 authentication if supported on devices.
•	Implement ACLs for restricting access between sensitive VLANs (e.g., Guest ↔ Finance).
•	Security enhancements like RIP authentication, ACLs, and DHCP snooping are recommended for production.
Notes
•	Each floor switch is a Layer 2 switch; the L3 switch handles inter-VLAN routing.
•	RIP may not be optimal for larger networks—consider OSPF or EIGRP for future scalability.
•	Trunking must be properly configured between routers and switches.


