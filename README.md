# BasicSwitchConfig


 Basic Switch Configration Homelab
 Objectives
 
 ● Simulate a console connection to a switch using Packet Tracer.
 ● Understand and configure basic switch settings.
 ● Learnto configure hostname, IP addresses, MOTD and passwords.
 ● Practice using show commands to verify switch configurations.
 
 Software Requirements:
CISCO Packet Tracer
 
 Lab Setup
 Part 1: Simulating the Console Connection Using Packet Tracer
 1.
 2.
 3.
 
 
 Open Cisco Packet Tracer and Create a Topology
 ○ LaunchPacketTracer.
 ○ Addthefollowing devices to your workspace:
 
 ■ OneCisco2960Switch.
 ■ OnePC.
 ■ OneConsoleCable.
 
 Connect the PC to the Switch Using a Console Cable
 ○ InPacketTracer, select the Console Cable from the cable options.
 ○ ClickonthePCandconnect the cable to the RS-232 port (also known as the console
 port).
 ○ ClickontheSwitch and connect the other end to the Console Port.
 Access the Switch via the Terminal on the PC
 ○ ClickonthePC.
 ○ GototheDesktoptab and click on the Terminal application.
 ○ Configure the terminal settings (leave the default settings: 9600 Baud rate, 8 data bits, no
 parity, 1 stop bit).
 ○ Youshouldnowhaveaccess to the switch’s CLI (Command Line Interface).

Part 2: Verify the default switch configuration.
 In this step, you will examine the default switch settings, such as current switch configuration, IOS
 information, interface properties, VLAN information, and flash memory.
 Switch> enable
 This command allows you to access Privileged EXEC Mode, where you can execute higher-level
 commands. By default, the switch starts in User EXEC Mode with limited access.
 I.
 II.
 III.
 IV.
 V.

 Examine the current running configuration file.
 Switch# show running-config
 Examine the startup configuration file in NVRAM.
 Switch# show startup-config
 Examine the Cisco IOS version information of the switch.
 Switch# show version
 Examine the default VLAN settings of the switch.
 Switch# show vlan
 Examine flash memory.
 Switch# show flash
 Configure Basic Network Device Settings
 
 Configure basic switch settings including hostname, local passwords and MOTD banner.
 I.
 II.
 III.
 IV.
 V.
 
 Assign the switch hostname.
 Switch(config)# hostname Switch01
 Configure password encryption.
 Switch01(config)# service password-encryption
 Assign class as the secret password for privileged EXEC mode access.
 Switch01(config)# enable secret class
 This sets an encrypted password for accessing Privileged EXEC Mode. Encrypting the password
 adds a layer of security.
 Prevent unwanted DNS lookups.
 Switch01(config)# no ip domain-lookup
 Configure a MOTD banner.
 Switch01(config)# banner motd #
 Enter Text message. End with the character ‘#’.
 Unauthorized access is strictly prohibited. #


 Console port access should also be restricted. The default configuration is to allow all console
 connections with no password needed. To prevent console messages from interrupting
 commands, use the logging synchronous option.
 Switch01(config)# line con 0
 Switch01(config-line)# password cisco
 Switch01(config-line)# login
 Switch01(config-line)# logging synchronous
 Switch01(config-line)# exit
 Switch01(config)#
 Configure an IP Address on VLAN 1
 Switch01(config)# interface vlan 1
 Switch01(config-if)# ip address 192.168.1.5 255.255.255.0
 Switch01(config-if)# no shutdown
 VLAN 1 is the default VLAN on most switches. Assigning an IP address to VLAN 1 allows you to
 remotely manage the switch. The no shutdown command ensures the interface is activated.
 Configure a Default Gateway
 Switch(config)# ip default-gateway 192.168.1.1
 The default gateway allows the switch to communicate with devices outside its local network,
 enabling remote management from different subnets.
 Enable Remote Management SSH (more secure):
 Enable SSH for remote access
 Create a local user
 Switch01(config)#username admin privilege 15 secret cisco
 Create a domain name
 Switch01(config)#ip domain-name eastcharmer.com
EAST CHARMER youtube.com/eastcharmer | www.eastcharmer.com
 Generate RSA keys for SSH
 Switch01(config)#crypto key generate rsa
 The name for the keys will be: Switch01.eastcharmer.com
 Choose the size of the key modulus in the range of 360 to 2048 for your
 General Purpose Keys. Choosing a key modulus greater than 512 may take a few minutes.
 How many bits in the modulus [512]: 1024
 %Generating 1024 bit RSA keys, keys will be non-exportable...[OK]
 Enable SSH for remote access:
 Switch01(config)#ip ssh version 2
 Switch01(config)#line vty 0 15
 Switch01(config-line)#transport input ssh
 Switch01(config-line)#login local
 Test Remote Access for SSH
 Open the Command Prompt on the PC and type:
 PC> ssh-l admin 192.168.1.5
 Enter the password to access the switch securely via SSH.
 Verification commands:
 Switch# show ip interface brief
 Switch# show run
