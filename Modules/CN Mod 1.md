>What is Computer Networks?
  Interconnected collection of autonomous computers


## Computer Networks VS Distributed Networks
A computer network is a set of interconnected devices that can communicate and share resources, while a distributed system is a network of interconnected computers that work together to achieve a common goal, often sharing both computation and data.
## Advantages and Disadvantages
- Enhances communication
- Allows convenient resource sharing 
- Highly flexible

- Security risk
- Lacks independence
- Not robust

## Social Issues
- Privacy concerns
- Security 
- Online bullying and harassment
- Legal issues such as copyright, net neutrality,

## Types of networks

- PAN
- LAN (*WLAN*)
- MAN 
- WAN 

## Protocol Hierarchies
![[Images/Pasted image 20231020191503.png]]

## Design Issues for the Layers 
- Reliability
	- Error detection
	- Error correction
	- Routing
- Evolution of the network
	- protocol layering
- Addressing or naming
- Internetworking
- Scalability
- Statistical multiplexing
- Flow control
- Congestion control
- Quality of service
	- Real time delivery
- Secure the network
	- Confidentiality
	- Authentication
	- Integrity
## OSI MODEL

| LAYER              | USE                                       | DESC                                                                                                                                                                      |
| ------------------ | ----------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Application layer  |     Protocols                                      |        Highest Layer in the OSI Model, which is Incharge of dealing with the protocol used by applications and ensuring the work properly                                                                                                                                                                   |
| Presentation Layer |     Syntax and Semantics                                      |    The layer  deals with the data translation, encryption, and compression.
| Session Layer      |    Manage Session, Synchronization                                       |      The session layer is in-charge of maintaining the communication between devices keeping tab of sessions so that data is in context during data transfers                                                                                                                                                                     |
| Transport Layer    |  Ensure package Transfer                                         |          The transport layer is responsible for data segmentation and ensures data integrity                                                                                                                                                                 |
| Network Layer      |   Manges Subnet, Routing, Congestion Control                                        | The network layer is in-charge of  performing network routing                                                                                                             | 
| Data Link Layer    | Error Control , Flow Control              | The data link layer is responsible for error handling of the data transferred from two physical computers, It is also responsible for the flow control of the information |
| Physical Layer     | Mechanical, Electrical, Timing Interfaces | The physical layer makes use of 1's and 0's to transfer data from one place to the other usually                                                                          |

## Service Primitives

```
LISTEN 
CONNECT 
RECIVE
DISCONNECT
```

## Modes of Communication
- Simplex
- Half Duplex
- Full Duplex