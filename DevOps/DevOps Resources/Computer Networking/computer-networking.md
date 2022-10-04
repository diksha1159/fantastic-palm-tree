<h1 align="center"><b> Computer Networks </b></h1>

## Introduction

  Computer Network simply means computers connected to each other creating an connection that can share information or data through each other. This sharing of data is done through many processes, protocols and methods which we would see further in this documentation.

  Protocols are some regulars under which data is exchanged between computers. For example : TCP/IP protocol, UDP protocol and more.

## How does a computer network work?

Nodes and links are the basic building blocks in computer networking. A network node may be data communication equipment (DCE) such as a modem, hub or, switch, or data terminal equipment (DTE) such as two or more computers and printers. A link refers to the transmission media connecting two nodes. Links may be physical, like cable wires or optical fibers, or free space used by wireless networks.

In a working computer network, nodes follow a set of rules or protocols that define how to send and receive electronic data via the links. The computer network architecture defines the design of these physical and logical components. It provides the specifications for the network’s physical components, functional organization, protocols, and procedures.

## OSI Model

 OSI Model is a standard model which shows transfer of data between computer through different layers with different functionings.

![image](https://user-images.githubusercontent.com/38884247/193452058-e6de244a-c27b-45d2-8a65-b8ab943eb92e.png)

### Different Layers in OSI Model

- Application Layer
- Presentation Layer
- Session Layer
- Transport Layer
- Network Layer
- Data Link Layer
- Physical Layer

`<br><br>`

#### Application Layer :

Application layer is the layer which interact with the user and it is presented on the devices.
`<br>`

#### Presentation Layer :

Presentation Layer is responsible for recieving data from application layer and manipulate it as per the required format for transmistting over the network.
`<br>`

#### Session Layer :

Session layer allows different machines to establish active communications sessions between them, It is responsible for establishing, maintaining, synchronizing, terminating sessions between end-user applications.
`<br>`

#### Transport Layer :

Transport Layer is an end-to-end layer used to deliver messages to a host. It is termed an end-to-end layer because it provides a point-to-point connection rather than hop-to- hop, between the source host and destination host to deliver the services reliably.
`<br>`

#### Network Layer :

The network layer works for the transmission of data from one host to the other located in different networks. It also takes care of packet routing i.e. selection of the shortest path to transmit the packet, from the number of routes available. The sender & receiver’s IP addresses are placed in the header by the network layer.
`<br>`

#### Data Link Layer :

The data link layer is responsible for the node-to-node delivery of the message. The main function of this layer is to make sure data transfer is error-free from one node to another, over the physical layer. When a packet arrives in a network, it is the responsibility of Data Link Layer to transmit it to the Host using its MAC address.
`<br>`

#### Physical Layer :

The lowest layer of the OSI reference model is the physical layer. It is responsible for the actual physical connection between the devices. The physical layer contains information in the form of bits. It is responsible for transmitting individual bits from one node to the next.
`<br> `


## TCP/IP Reference Model

The TCP/IP which stands for Transmission Control Protocol/Internet Protocol is the set of communication protocols used in the internet and similar computer networks. It provides end-to-end data communication. It specifies all the processes involved in end-to-end data communication which includes packetizing, addressing, routing, transmission. It contains four layers and all the functionalities are organized in these four layers. The four layers are shown in the diagram below.

![](https://wat-user-images.s3.amazonaws.com/1642488809573%2FJELDIpR18x%2FOSI_diag.png)

TCP/IP is a layered server architecture system in which each layer is defined according to a specific function to perform. All these four TCP IP layers work collaboratively to transmit the data from one layer to another.


## Network Architectures

Computer network design falls under two broad categories:

- Client-Server Architecture
- Peer-to-Peer Architecture

<br>
<br>

### Client Server Architecture :

Simply understanding : A server is the one who provides requested services and Clients are the ones who request services.

![image](https://user-images.githubusercontent.com/38884247/193465363-cabd0898-eb05-4f6a-86e3-0c5abf13f3bf.png)

### Peer-to-Peer Architecture :

A peer-to-peer network is a simple network of computers. It first came into existence in the late 1970s. Here each computer acts as a node for file sharing within the formed network. Here each node acts as a server and thus there is no central server in the network. This allows the sharing of a huge amount of data.

![image](https://user-images.githubusercontent.com/38884247/193465421-7b2929d0-f048-4356-8108-c972498026fb.png)

## What is network topology?

Network Topology is the schematic description of a network arrangement, connecting various nodes(sender and receiver) through lines of connection.They can be configured in different ways to get different outcomes. Some types of network topologies are:

##### BUS Topology

Bus topology is a network type in which every computer and network device is connected to single cable. When it has exactly two endpoints, then it is called  **Linear Bus topology** .

##### Ring topology

Each node is linked to two other nodes, forming a ring. Data can flow bi-directionally. However,single node failure can bring down the entire network.


#### Tree Topology

Tree topology is the topology in which the nodes are connected hierarchically, with all the nodes connected to the topmost node or root node.


#### **MESH Topology**

It is a point-to-point connection to other nodes or devices. All the network nodes are connected to each other. Mesh has `n(n-1)/2` physical channels to link `n` devices.

There are two techniques to transmit data over the Mesh topology, they are :

1. Routing
2. Flooding `<br><br>`

### Star topology

A central server node is linked to multiple client network devices. This topology performs better as data doesn’t have to go through each node. It is also more reliable.
