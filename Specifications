--[[General Project Overview:
 
 
 
        --[[Final Goals:
               
                Implement TCP/IPv4 over Ethernet into ComputerCraft, following the OSI & TCP/IP Models, as close to reality as possible.
                This will include Routing & Switching of data across the network(s) and common network services and applications such as:
                       
                        DHCP
                        TELNET/SSH
                        ICMPv4
                        DNS
                        NTP
                       
               
               
                --[[Specific Technologies:
                       
                        RFC 793 TCP/IP
                        IEEE 802.3 Ethernet
                       
                        --[[OnBuilt-Protocols:
                       
                                Routing:
                               
                                        RIPv2
                                        OSPF
                                        BGP
                                        MPLS
                                       
                                Switching:
                                       
                                        VLAN
                                        Spanning-Tree
                                        MST
                                        EtherChannel
                                        Cut-Thru switching method
                                       
                                Services:
                                       
                                        DHCP
                                        SMTP/POP3
                                        DNS
                                        NTP
                               
                                Applications:
                               
                                        Telnet
                                        SSH
                                        ICMPv4
                                        Email-Messenger
                                       
                                General_Technologies:
                               
                                        VRRP
                        ]]
                ]]
        ]]
 
 
]]
 
--[[Detailed Project Specifications:
 
                -------------------------
           |    Technology Models    |
                -------------------------
                -----                    --------
           | OSI |                      | TCP/IP |
            -----                        --------
               
        Application<--|---->Application
        Presentation<-|
        Session<------|
       
        Transport<--------->Transport
       
        Network<----------->Network
       
        Data Link<-|------->Interface
        Physical<--|
       
       
       
        --[[Ethernet:
       
                Physical:  Defines the physical entities capable of being used in this technology.
                Data Link: Defines the logical identifiers for the physical peripherals.
               
                Physical:
                        Ethernet defines that all data must be serialized when transmitted over the medium.
                        In a copper twisted pair cable there is a transmit pair, and a receive pair.
                        The transmit pair is used to send data over the medium while the receive pair
                        is used to accept an incoming transmission.
                       
                Data Link:
                        Ethernet defines that a Physical entity must have a logical identifier that is
                        solely unique to that entity. This ID is bound to the physical device and represents
                        a label for other Data Link layer devices as well as to allow higher layer devices to identify
                        this entity at the Data Link layer. The format used is in 6 octets or 48bits
                        and is in Hexadecimal format. This identifier is called the Media Access Control Address
                        or MAC Address for short. At this layer is also defined the types of addresses, they are as follows:
                       
                                Unicast -   Used to identify a single device
                                Multicast - Used to identify a group of devices with a single address
                                Broadcast - Used to identify all devices with a single address
                               
                        At the Data Link layer is a sole Broadcast address: FFFF.FFFF.FFFF
                       
                        Unicast and Multicast addresses can be in the range of 0000.0000.0000 to FFFF.FFFF.FFFG
        ]]
       
        --[[TCP/IP:
               
                For our implementation we will pick up TCP/IP at Layer 2 as it is running over Ethernet
               
                Data Link: Implements Ethernet Data Link Layer.
                Network: Defines higher logical identifiers for the Data Link layer.
                Transport: Controls aspects of the protocol such as data timings, control methods, etc.
               
                Network:
                        The Network layer defines a second logical identifier that is not bound to a single entity.
                        This identifier can be used many times on various systems granted that the same identifier
                        is not used multiple times in the same network. This layer is represented in the format of
                        4 octets or 32bits and is in Decimal format. This identifier is called the Internet Protocol Address
                        or IP Address for short. At this layer is also defined two new types of addresses, they are as follows:
                       
                                Public - Is a purchased address from the country's Public IP Space Management Company.
                                Private - Used to identify a host on a local network.
                               
                        Public IP Range - 1.0.0.0 - 191.0.0.0
                        Private IP Range - 192.0.0.0 - 255.255.255.254
       
        ]]
       
]]
