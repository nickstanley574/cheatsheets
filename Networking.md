# Networking

* **Default Gateway** - The device that passes traffic from the local subnet to devices on other subnets.
* **Subnet Mask** - a number that defines a range of IP addresses that can be used in a network
* **Subnetting** - The process of dividing a network into smaller network sections. This can be useful for many different purposes and helps isolate groups of hosts together and deal with them easily.
* **Netmask** -  a 32-bit mask used to divide an IP address into subnets and specify the network's available hosts.
* **CIDR Notation (Classless Inter-Domain Routing)** - CIDR notation is a compact representation of an IP address and its associated routing prefix. The notation is constructed from an IP address, a slash ('/') character, and a decimal number. The number is the count of leading 1 bits in the routing mask, traditionally called the network mask. The IP address is expressed according to the standards of IPv4 or IPv6.
* The term **octet** string refers to a collection of any number of related octets


```
8           .16             .24             .32         
[ octet ]   .[ octet ]      .[ octet ]      .[ octet ]

192         .168            .0              .15              
1100 0000   .1010 1000      .0000 0000      .0000 1111

255         .255            .255            .0
1111 1111   .1111 1111      .1111 1111      .0000 0000          # Any bit that is a "1" is the "network bit field" and "0" is the "rest bit field"

---- above is the same has the below ----

192         .168            .0              .15         /24     # This means that the first 24 bits of the IP address given are considered significant for the network routing.
```


Binary: 
```
128     64      32      16      8       4       2       1
2^7     2^6     2^5     2^4     2^3     2^2     2^1     2^0    

Example: 

128 64  32  16  8   4   2   1 . 128 64  32  16  8   4   2   1 . 128 64  32  16  8   4   2   1 . 128 64  32  16  8   4   2   1    
1   1   0   0   0   0   0   0 . 1   0   1   0   1   0   0   0 . 0   0   0   0   0   0   0   0 . 0   0   0   0   1   1   1   1 
128+64 = 192                    128 + 32 + 8 = 168              = 0                             8 + 4 + 2 + 1 = 15 
192                           . 168                            . 0                             . 15

```

| Class | Leading bits | Size of network number bit field | Size of rest bit field | Number of networks | Addresses per network | Total addresses in class | Start address | End address   | subnet mask dot-decimal notation | CIDR |
|-------|--------------|----------------------------------|------------------------|--------------------|-----------------------|--------------------------|---------------|---------------|----------------------------------|------|
| A     | 0            | 8                                | 24                     | 128 (2^7)          | 16,777,216 (2^24)     | 2,147,483,648 (2^31)     | 0.0.0.0       | 127.0.0.0     | 255.0.0.0                        | /8   | 
| B     | 10           | 16                               | 16                     | 16,384 (2^14)      | 65,536 (2^16)         | 1,073,741,824 (2^30)	   | 128.0.0.0     | 191.255.0.0   | 255.255.0.0	                  | /16  | 
| C     | 110          | 24                               | 8                      | 2,097,152 (2^21)   | 256 (2^8)     	    | 536,870,912   (2^29)	   | 192.0.0.0	   | 223.255.255.0 | 255.255.255.0                    | /24  | 
	

* Class A: NNNNNNNN.HHHHHHHH.HHHHHHHH.HHHHHHHH (less networks, more hosts)
* Class B: NNNNNNNN.NNNNNNNN.HHHHHHHH.HHHHHHHH (more networks, less hosts)
* Class C: NNNNNNNN.NNNNNNNN.NNNNNNNN.HHHHHHHH (even more networks, even less hosts)


## AWS Networking


* **VPC A virtual private cloud** - a private network space in which you can run your infrastructure. It has an address space (CIDR range) which you choose e.g. `10.0.0.0/16`. This determines how many IP addresses you can assign within the VPC. The `10.0.0.0/16` address space can use the addresses from `10.0.0.0` to `10.0.255.255`, which is 65,536 IP addresses.
* **Subnets** - A subnet is a section of your VPC, with its own CIDR range and rules on how traffic can flow. Its CIDR range has to be a subset of the VPC’s, for example `10.0.1.0/24` which would allow for IPs from `10.0.1.0` to `10.0.1.255` giving 256 possible IP addresses. 
* **Availability Zones** -  is an isolated location inside a region, at least one zone should be able to operate, even if others suffer outages 
* **Routing Tables** - contains rules about how IP packets in the subnets can travel to different IP addresses. 
* **Internet Gateways** - The routing table which makes a subnet public needs to reference an Internet gateway to allow the flow of external IP packets into and out of the VPC. 
* **NAT Gateways** - sits in the public subnets, accepts any IP packets bound for the Internet coming from the private subnets, sends those packets on to their destination and then sends the returning packets back to the source.
* **Security Groups** - specifies ingress (inbound) and egress (outbound) traffic rules, limiting them to certain sources (inbound) and destinations (outbound). They are associated with EC2 instances rather than subnets.


## References 
* https://www.digitalocean.com/community/tutorials/understanding-ip-addresses-subnets-and-cidr-notation-for-networking
* https://www.lifewire.com/what-is-octet-818391
* https://www.dummies.com/programming/networking/cisco/network-basics-ip-network-classes/
* https://en.wikipedia.org/wiki/Classful_network
* https://grahamlyons.com/article/everything-you-need-to-know-about-networking-on-aws