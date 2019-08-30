**dWeb: The Protocol For Web 4.0**
***By: Jared Rice Sr.***
Created On: August 26th, 2019 
***(Revised On: August 28th, 2019)***

# ABSTRACT
dWeb is a protocol designed for syncing folders that typically contain websites and web applications, along with the data that's usually associated with their usage, between peers on a decentralized peer-to-peer network, even if these folders are substantial in size or frequently updated. Synced and distributed folders over the protocol are referred to as **"dWeb repositories"** or **"dPacks"** for short. dWeb's protocol utilizes a cryptographically secure log of updates to validate whether or not the dPack is truly distributed. A byte range of any file's version can be efficiently broadcasted via a dWeb-based repository to other peers utilizing the dWeb protocol, from any network connection. dWeb's protocol uses public key cryptography to encrypt all traffic over a dWeb-based network. A dWeb peer-to-peer network is essentially a group of peers, also referred to as a **"flock"**, that ultimately connect with each other to exchange dPacks. A dWeb peer-to-peer network can be established as a public or private network and an infinite number of networks can co-exist at once, utilizing the same protocol.

# BACKGROUND
The need for a decentralized internet, during a time where the web has become over-centralized, has become obvious to many who avidly use the internet and have witnessed the constant violation of many internet user's human, civil and constitutional rights. The influx of countries and their governments whom use the internet to spy on their citizens has gotten way out of control. The lack of privacy is truly alarming and so are the security issues, where even central banks are still unable to protect our money, after over twenty years of trying to secure their own networks. Now social networks and search engines want to get involved in politics, control what we find or view on their networks and will delete our entire digital existence over a policy violation. Big tech firms and tyrannical governments know that software developers are building ways around their control and are using policies, as well as regulators to scare off innovators in an attempt to maintain their power and keep their usual control mechanisms in place. Developers and innovators alike need a better protocol to build upon, rather than HTTP. Developers as well as the users of their software and websites, deserve a completely decentralized web, where a developer's hard work can never be destroyed or shutdown by fearful organizations and where users of the web can experience true privacy, freedom, security and transparency for the first time since the inception of the web itself. Isn't that what the web was created for? dWeb's protocol makes all of this a reality and presents a better and safer alternative to HTTP.

# 1. DWEB PROTOCOL
dWeb is a website, web application and dataset (dPack) synchronization protocol that does not assume that the dPack is static or that the complete dPack will be downloaded in full.

***A reference implementation is provided in JavaScript via our private NPM repository:*** 
```http://npm.dwebs.io```

***Once connected to our private repository via the NPM CLI, you can install the dPack CLI with the following command:***
```npm install @dpack/cli -g```

dWeb has no idea what form of transport is being used, nor does it matter what underlying transport the protocol will ultimately use to connect to the outside world. This means dWeb is completely transport agnostic. This section (1.x) covers dWeb's protocol design, as well as the following critical properties:

**1.1 - Website, Web Application & Content Integrity** - ***Websites, web applications, as well as their publisher's integrity are verified through signed hashes of the content itself.***
----
**1.2 - Peer Revelation & The Flock** - ***Peers on a dWeb network are able to find each other through a process known as "peer revelation", where they form groups around dPacks on a dWeb-based network, known as a flock.***
----
**1.3 - User-Controlled Privacy & E2E Encrypted Transport** - ***dWeb's protocol includes many advantages when it comes to security, as well as privacy -- including end-to-end encryption.***
----
**1.4 - dPack Syncing & Distributed File Versioning** - ***dWeb's ability to utilize a cryptographically secure log to reference a dPack's different versions and metadata, gives it the added ability of syncing new dPack updates to other peers within a dPack's flock, right when updates are distributed from a dPack's publisher.***
---
**1.5 - A Decentralized Web At Global Scale** - ***dWeb can easily transport massive file hierarchies and datasets while doing so at global scale. The restrictions brought about by web host-related resource limits are no longer a limitation placed on developers, considering dWeb's protocol is based entirely around a distributed peer-to-peer network architecture.***

## 1.1 WEBSITE, WEB APPLICATION & CONTENT INTEGRITY
It's important that the dPack you receive, is the exact version of the dPack you requested. Malicious peers on a distributed network, could in fact send information that is entirely different than the information you had originally requested. dWeb's protocol places the importance of integrity, as it applies to files and content, above anything that's distributed over the protocol itself. Being able to verify that you're receiving exactly what you requested is paramount in a protocol that's based around distributed systems, like dWeb. This starts with a consumer being able to reference specific versions of a website, web application or file, by way of a hash, that should ultimately derive from the content of the website or web application itself. 

For example, when using the HTTP protocol, if you had downloaded the dWeb whitepaper ***(https://dwebs.io/whitepaper.pdf)*** last week, there would have been no way for you to check and see if it was updated today, without having to download the entire PDF file again and checking the file's metadata to see when it was last updated. The dWeb protocol refers to files within a dPack, by the hash of its content. This is called content-addressability, which allows a consumer of a protocol to verify that the data they're receiving is precisely the data they originally requested and also lets consumers cite specific versions of a dPack or files within a dPack that are specifically needed, by referencing a specific hash. 

When addressing dPacks, the dWeb protocol utilizes BLAKE2b ***(Aumasson et. al. 2013)*** cryptographically secure hashes, where these hashes are arranged in a Merkle tree ***(Mykeltun, Narasimha and Tsudik et. al. 2003)***, ***"a Merkle tree where each non-leaf node is the hash of all child nodes" (credit: Mykeltun)***. Leaf nodes contain pieces of a dPack. In other words, due to how a cryptographic hash is formed, the "top hash" within the Merkle tree can only be found if all the content below it is a precise match. If two Merkle trees have "top hashes" that are a precise match, you can guarantee that all other leaf nodes within that Merkle tree will be a precise match as well. In the case of the dWeb protocol, this is how the protocol confirms whether or not a dPack has been synced by a flock of dPack peers, who are simultaneously seeding the dPack itself. dWeb works efficiently over a network connection due to its Merkle tree-based data structure (primary), which allows for the protocol to efficiently access subsets of a dPack's metadata. 

## dWeb Addresses
dWeb addresses are Ed25519 public keys ***(32 bytes and 64 characters when Hex encoded)***. dWeb addresses or links take on the following formats:

dWeb Key:
```8e1b9399n7d3jd18d2dk382928109394817239a9```

Using the dWeb protocol prefix:
```dweb://8e1b9399n7d3jd18d2dk382928109394817239a9```

Via a TXT dDNS record, where a dWeb key is accessed over a dTLD:
```dweb://dtest.dcom or https://test.dcom```

Over the HTTP protocol:
```https://dpacks.io/8e1b9399n7d3jd18d2dj382928109394817239a9```

All messages that are transported over the dWeb protocol are end-to-end encrypted and digitally signed using the dPack's public key (the dWeb addresses), during the transport process. If you are unaware of the public key of a dPack, then you will not be able to **"revelate"** or communicate with any publisher or seeder within that dPack's flock. On the other hand, anyone who has the dPack's public key can verify that data within a dPack derived from the publisher (the owner of the private key). This is because every dPack (dWeb repository) has a private key that directly corresponds with it. A dPack's private key is kept in the original dPack's folder, on the publisher's device that originally created the dPack itself.

dWeb's protocol will never expose the public or private key of a dPack over a public network of any kind. This is made possible through the **"revelation protocol"** where a BLAKE2b hash is taken of the dWeb address (public key) and is ultimately used as the **"revelation key"**. In other words, the original key is impossible to find unless of course you have shared this key publicly or have attached it to a dTLD. Most websites, web applications and their dWeb keys will be exposed publicly, just as they are over HTTP. Although, there are dPacks that will remain private and should always remain private. For example, dPacks that hold a dSiteDB (Decentralized DBMS) with a stream of messages between two users of a messenger dApp, may want to keep messages between themselves inside a private room, where it is broadcasted over a dWeb address that purposely remains private (if the dApp had private rooms, where dWeb addresses remained private and has no exposure of any kind). This is so the conversation between these two users always remains private between them (unless of course they expose the dWeb address to the public at a later time). As you can see, there are many use-cases for dWeb addresses and it's ultimately up to the developers and consumers on whether they want to publicize them or not. Privacy will always remain one of the most important design elements of the protocol itself. 

### dCass and dDBMS Layers
dWeb's decentralized content-addressable storage ***(dCass)*** layer and networking protocols are implemented through one of dWeb's three onboard dDBMS's, known as dDatabase. dPack integrity protocols are also implemented at the dDBMS layer.

**NOTE:** ***We won't dive into the dDatabase framework within this whitepaper, since it has its own whitepaper but will explain some basics surrounding the dDBMS layer and the dDatabase framework, so you can understand how dDatabase-based update logs work.***

Just like dWeb's protocol is transport agnostic, dDatabase is format agnostic, meaning it will accept any kind of input data. Therefore it is important to note that it will continue to function with any sort of streamed binary data. While the dWeb protocol uses dDatabase for versioning, it uses an onboard dCass called dDrive as a **"file system"** layer, that sits directly on top of the dDBMS layer. The dCass layer is used for syncing dPacks between dWeb peers. The art of the dDBMS layer is to allow consumers of the dDBMS to have full control over how they input data or how they ultimately design their decentralized database. A great example of this, is how dDrive utilizes dDatabase to create a file system that is synchronized and ultimately distributed between peers. 

dDatabase-based binary append-only update logs are a crucial component of the dWeb protocol. Each binary-based entry is cryptographically hashed, signed and can be verified by any consumer who holds the public key of the dPack itself. A publisher of a dPack can be verified through the exact same means. dWeb's protocol uses two logs known as **"content"** and **"metadata"**, where the content log contains the files within a dPack, while the metadata log contains the name, size, last modified time and other file-related metadata. This ultimately creates an entire file system structure. These update logs are no different than a digital ledger. The only difference in this form of a decentralized digital ledger and blockchain-based digital ledgers is the fact that the data within a dDatabase or a dPack is only verified by those who want to utilize it, whereas, depending on the consensus algorithm used in accordance with a blockchain software, all data generated on a blockchain-based network is propagated to all participants of the network. Both the content and metadata logs are replicated when syncing between dWeb peers within a dPack's flock. Lastly, versioning control and the process of replicating dPacks between peers is made possible through file fragmentation. When files are appended to a dPack, each file is fragmented into a randomized amount of fragments, where these fragments are then arranged into a Merkle tree, where versioning and the replication process can be successfully validated.

## 1.2 DECENTRALIZED PEER REVELATION & THE FLOCK
dWeb is a protocol designed to sync and distributed fragments of a dPack amongst a flock of dWeb-based peers. Peers on a dWeb network who acquire the initial fragments of a dPack, by design, can become a **"partial seeder"** for that particular dPack. If another dWeb peer, gathering fragments from the flock, is looking for a particular fragment that is held by a partial seeder, the partial seeder can elect to sync these fragments with that particular peer. Fragments are downloaded from multiple partial seeders in parallel, so that dPack fragments are downloaded and synchronized in harmony with one another. 

### Peer Revelation
---------------------
The most crucial aspect of a dPack's synchronization and distribution protocol is known as **"peer revelation"**, which encompasses the processes involved with peers finding each other on a dWeb-based network. Peer revelation involves finding the IP address and port number of a peer that is syncing the dPack a peer is performing a lookup for. Once a lookup is successful, the peer connects and the **"seeder"** or partial seeder begins distributing a dPack or dPack fragment(s) to the requesting peer. This peer revelation process allows for dPacks to be found, even when the original dPack publisher is no longer a peer or the original dPack distributor is no longer syncing the dPack on a related revelation network that utilizes the dWeb protocol. 

The following actions are involved in peer revelation:

1. **connect(dWebKey, port)** - ***Every 5 seconds (or on a customized interval) by default, a dWeb client (like dPack CLI or dBrowser) performs peer lookups for a specific dWebKey. A port can be specified, if the peer performing the lookup would like to seed the dPack that is found, over a specific port.***

2. **success(dWebKey, ip, port)** - ***This action is called when a dPack peer is successfully located during a lookup.***

3. **terminate(dWebKey, port)** - ***After starting the interval-lookups for a dWebKey, a peer can terminate the lookups and include a port that will terminate the seeding of that same dWebKey over that particular port.***

***These peer revelation-related actions current occur on four different types of revelation networks:***

- **DNS** - A globally used method for resolving keys to addresses.
- **dDNS** - A decentralized version of the globally used DNS method.
- **MultiCast DNS** - Peer revelation in a near-field or local network scenario.
- **Kademlia Mainline DHT** - Increases the likelihood that a dPack can be found, even if DNS servers are not found, although dDNS is always accessible considering dDNS exists on several separate P2P networks at once.

Considering the dWeb protocol is agnostic to the type of network revelation methods that are utilized, such as DNS, new implementations can be created over time to expand the current types of network revelation methods that are compatible with the protocol itself. The four methods above give the dWeb protocol a great set of peer revelation methods to ensure peers could (most likely) find each other on the network, in order to ultimately exchange dPacks with one another, therefore accomplishing the general use-case for the dWeb protocol. Another important aspect we should note is that all four methods of network revelation are used simultaneously, to increase the likelihood that a peer is found in a short period of time. Although, peer revelation can be ran in a "single-method" mode, where dPacks are simply broadcasted over the HTTP protocol instead, where it can be found via ```http://``` rather than being found through peer revelation methods that are only used to find a dPack over ```dweb://```. In a single-method mode, a server or network of servers (for example), that broadcast a dPack via HTTP, are considered to be the only peer(s).

### dWeb Peer Connections

**Note:** ***dWeb is not designed to replace HTTP, since it can be layered on top of HTTP. HTTP is supported for compatibility with static file servers and web browser clients.***

After peer revelation has taken place, the protocol process has gathered a list of potential dWeb peers syncing the dPack being requested. From here, the protocol will attempt to make contact with peers on this list. While dWeb's protocol is transport agnostic, HTTP, TCP and UTP methods are used in the JavaScript implementation mentioned earlier in this whitepaper (dPack CLI). The current implementation will prefer HTTP over the other protocols. If HTTP is not mentioned then the protocol will utilize the TCP or UTP protocols (in the current implementation). If one protocol method connects first, dWeb's protocol is designed to terminate other potential protocol connections. If no connections are successfully made, dWeb's protocol will decide that the peer is offline and will terminate the connection(s). In the event an internet connection is lost, dWeb's protocol maintains a list of known sources for a dPack, within the dPack's file system (dDrive), so it can reconnect to this list of good and known sources immediately. If the protocol is dealing with many known peers, it will only utilize a handful of peers to connect and save the others for use later, in case it needs more sources at a future time. 

### Duplex Binary Connections & dWeb Channels
Once a duplex binary connection to a remote dPack peer has been successfully established and opened, dWeb's protocol places a P2P messaging protocol layer (dAmp) on top of the dDBMS protocol layer (dDatabase in this instance), allowing two dWeb peers to communicate over separate and stateless "dWeb channels". This is where dPack fragments are requested and ultimately exchanged between the two peers. In the situation where there are more than two peers, separate dWeb channels are opened with many peers at once, where clients can simultaneously download and sync dPack fragments across the entire group of peers within a dPack's flock.

## 1.3 END-TO-END ENCRYPTED TRAFFIC 
Web 2.0 and 3.0 provided us with the ability  to encrypt traffic from a consumer's computer to a particular server or group of servers that they were exchanging data with, by utilizing what is known as the Secure Sockets Layer (SSL). This guaranteed that all data exchanged between a consumer's device and server(s) the consumer was connecting with, remained private, as long as a hacker hadn't infiltrated the server(s) and had access to the consumer's logs. Even if a hacker simply intercepted the traffic between a consumer's device and the server(s), the hacker would be unable to read the HTTP traffic exchanged between the two, if SSL was being used. This requires the client to trust the server it  is attempting to connect to which is pretty problematic. With the recent hacks of Capital One's servers, where a former AWS employee had published the personal information of many Capital One customers, servers are no longer a trustable source to connect with for clients, if the providers and employees can no longer be trusted. This is because the model just mentioned, requires the client to trust the server it's connecting to and this trust has deteriorated over time. While the dWeb eliminates the need for servers, web hosting companies or web infrastructure services like Amazon's AWS, it is not "perfectly secure". It's actually in the hands of developers and publishers to keep their dWeb address (public key) a secret, if data within a dPack is to remain private. 
There is an obvious tradeoff in P2P networks, like a dWeb-based network between peer revelation and consumer privacy. The more dWeb peers you lookup and exchange data with, the more peers you have to trust with the data being exchanged. Remember a dPack can remain private and will never be found  by attackers, even if it's privately shared with a group of peers over a dWeb-based network, because a revelation key (a BLAKE2b hash of the dWeb address) is used instead of the dWeb address (public key). Although, if that key were to be shared publicly, attackers could access the data within it at will. Therefore the protocol is designed for developers to design their own privacy guidelines and make their own privacy decisions as it pertains to their own dSites (decentralized websites) and dApps (decentralized applications). This also means developers can choose which network revelation providers to integrate with (e.g. BitTorrent). Although a developer should only integrate with revelation networks they trust, like the old client/server model mentioned above. With dWeb's protocol, privacy is now in the hands of the consumer, instead of the provider and traffic is always encrypted from one end to the other.

## 1.4 LIVE DPACK SYNCING & DISTRIBUTED FILE VERSIONING
dWeb's protocol is designed to take streaming binary data through the following process, in order to enable dWeb's "replication protocol":

***1. Split the binary stream into fragments or "packets"***
***2. Creates a hash from each fragment or "packet"***
***3. Arranges the fragment hashes into a Merkle tree***

It is important to note that dWeb's protocol is also able to fully or partially sync streaming binary data (dWeb streams), in a distributed system, even if the dWeb stream is being appended to. This is accomplished by utilizing a P2P messaging protocol (dAmp) to traverse the Merkle tree of remote dWeb peers and to fetch the strategic set of leaf nodes. Due to the low-level, message oriented design of the replication protocol, different node traversal strategies can be implemented. 

Two types of dPack versioning strategies take place automatically over the dWeb protocol. dPack metadata is kept in the root folder inside of every dPack, called ```.dweb``` and normal data is stored as normal files within the dPack file system which expands out from the root level as well. 

### Metadata Versioning
If you have ever used the file transfer protocol (FTP), when uploading files or a web page, you probably remember the protocol catching whether or not a file existed or not. In this case, it would have asked you to overwrite it. This happens because the filename you are updating already exists. What FTP-based clients cannot do, on the other hand, is tell the consumer of the protocol with absolute certainty whether the file on a server and the file being transferred to the server, have any true differences in content. Of course, it can see the file on the server was uploaded at a different time and may differ in size but there aren't many other forms of metadata that FTP can use to determine if anything has changed. dWeb's protocol no only keeps of record of all historical file-related metadata, it can also keep a copy of every single iteration of a file, from the moment it was created. 

When uploading a file over the dWeb protocol, the protocol is designed to use a sorted, depth-first recursion to list all the files in the file system tree. For each file the protocol finds, it fetches the dCass-based file system metadata (filename, Stat object, etc) and performs a check if a filename with the precise metadata within ".dweb" exists. If it does exist and is deemed to be the newest possible version of the file, then the file is effectively skipped and the previous version will remain the newest and most current version of the file. If the metadata is different then the metadata currently held within ".dweb", then a new metadata entry will be appended to the update log within ".dweb", as the new "latest" version of this file. 

### File Versioning
While dWeb's protocol is designed to store metadata by keeping a historical record of a dCass-based system, files can also be stored via a version-controlled method. dDrive stores files, as files, which means dDrive does not store past versions of files (like has been seen with protocols like GIT) by default. If dDrive did store all files (past & present) within the ".dweb" directory" as GIT does the ".git" directory, it would risk taking up a dWeb user's entire hard drive, when seeding a website (for example), that has a plethora of different renditions (updates). For this reason, dDrive utilizes multiple storage modes. The dDatabase-based update log includes an optional "data" file that stores all file-related data. In dWeb only the "metadata.data" file is used, while the "content.data" file is not used. By default, dDrive will store files as files, as mentioned previously but **"dWeb Vault"** nodes can be ran that keep all previous versions, by setting the protocol to use **"content.data"** instead of **"metadata.data"**, where every single file is kept, from the time a dPack is created.

### Merkle Trees
dWeb's protocol uses a custom encoding method, when laying out dDatabase-based update logs into a Merkle tree. This particular encoding method positions hashes in a scheme called **"binary in-order interval numbering"** or just **"bin"** numbering for short. This is a deterministic method of positioning leaf-nodes in a Merkle tree. 

***A Merkle tree with seven leaf nodes will always be laid out like this:***

```
0L
      1L
2L
           3L
4L
      5L
6L
```

dWeb's protocol ensures that the hashes related to the fragments of files within a dPack or dDrive are always even numbers, at the wide end of the Merkle tree. 

***The Merkle tree example above had four leaf nodes that became even numbers.***

```
fragment0 -> 0
fragment2 -> 2
fragment4 -> 4 
fragment6 -> 6
```

***In this example the even and odd leaf nodes of the Merkle tree store differentiating data:***

**- Even Leaf Nodes -** List of fragment hashes (fragment0, fragment 1, fragment 2...)
**- Odd Leaf Nodes -** List of Merkle hashes (hash of child even nodes) [h0, h1, h2, ...)

These two lists are intertwined into a single update log, so that the indexes (position) in the update log, are the same as the bin numbers from the Merkle tree. All odd fragment hashes are derived by hashing the two child leaf nodes.

The following example shows how odd and even hashes are calculated:

**Evens:**
```
h0 = h(fragment0)
h2 = h(fragment1)
```

**Odds:**
```
h1 = h(h0 + h2)
```
***An update log with two entries would look like this:***
```
0. h(fragment0)
1. h(h(fragment0) + h(fragment1))
2. h(fragment1)
```
***(Where h = hash)***

#### Multiple Merkle Roots 
It is also possible for a Merkle tree under the "bin" to have two or more roots. A root can be defined as a parent leaf node that can have its own child leaf nodes, within a Merkle tree. 

***This Merkle tree has 2 roots (parent nodes) [ 1 and 4 in this example are roots ]:***
```
0L
       1L
2L

4L
```
***This Merkle tree has 1 root (3 in this example is a root):***
```
0L
       1L
2L
             3L
4L
       5L
6L
```
***This Merkle tree has 1 root (1 in this example is a root):***
```
0L
       1L
2L
```

### dPack Replication Example

This section is meant to describe how dPacks are replicated over the dWeb protocol. The easiest way to describe how dPack replication works is through a series of pseudocode-based examples.

Let's say you have a folder on your computer that contains two PNG images:
- jefferson.png
- trump.png

If you want to send these files to another device using the dWeb protocol, you would first have to add them to a dPack which would split them into fragments and would ultimately construct a data file that represents the fragments and the related dDrive's file system metadata.

Assuming jefferson.png and trump.png both split into three fragments apiece, that each equate to a file size of 124KB. A dWeb-based network would then create a representation of the fragmented files and their metadata. 

***These eight fragments are placed in a list like this:***
```
jefferson-1.png
jefferson-2.png
jefferson-3.png
trump-1.png
trump-2.png
trump-3.png
```

***These fragments of the two image files, each get hashed and those hashes are organized into a Merkle tree, like the example below:***

```
0L                  - h(jefferson-1)
       1L           - h(0L+2L)
2L                  - h(jefferson-2)
            3L      - h(1L+5L)
4L                  - h(jefferson-3)
       5L           - h(4L+6L)
6L                  - h(trump-1)
8L                  - h(trump-2)
       9L           - h(8L+10L)
10L                - h(trump-3)
```
***(Where h = hash) and (L = Mt leaf node)***

The next part of the process is to calculate the root hashes of our Merkle tree which are 3L and 9L then hash the number that derives from that and lastly, cryptographically sign the hash (sH). The signed hash is utilized to validate all other leaf nodes (parent/child) within the tree and the signature proves it was published by. 

The pseudo-tree above is for the hashes that derive from the fragments of our two photos. A second Merkle tree is generated as a representation of the files and their metadata, known as the "metadata log".

***An example of a metadata log-based Merkle tree is below:***
```
0L - h(contentLog: {'4f21f567...'})
1L - h(0+2)
2L - h({"jefferson.png", first: 0, length: 3})
4L - h({"trump.png", first: 3, length: 3})
```

***(Where h=hash) and (L = Mt leaf node)***

**A few notes about the above pseudo-representation of the metadata log's Merkle tree:**
- The 1st entry in this log is the metadata entry pointing to the dWeb key of the second log (the contentLog that the first Merkle tree represented).
- Notice that the 3rd leaf node is not included in the above representation. That's because 3 is the hash of 1+5 and 5 does not exist yet, so it will be written at a later update.

All that's left in the replication process is to send the metadata to the other device (peer). The replicating P2P low-level messaging protocol is tasked with communicating between peers over a dWeb channel, as was described earlier in the whitepaper. Below is a play-by-play of the communications between both peers, where you are Bob and the other device is Alice.:

- Bob sends the first message, known as the "Announce" message, that includes the revelation key that was generated from the public dWeb key of this dPack.
- Alice sends Bob an "Ask" message, signaling that Alice wants all leaf nodes in the metadata log of the dPack that Bob is announcing.
- Alice sends three "Pull" messages, one for each leaf node (0,2,4)
- Bob sends back 3 "Data" messages:
-- The data messages contain the "contentLog" key, the hash of the sibling which in this case is (2), the hash of the uncle root (4), as well as the signature for the root hashes (in this case 1,4).
- Alice can validate the integrity of the first data message by hashing the metadata received for the contentLog metadata to produce the hash for fragment0. They then hash the leaf node 0, with the hash 2 that was included to reproduce hash 1 and hashes 1 with the value of 4. Lastly, the digital signature that was received, is used in order to verify it was the same dPack that was originally requested.
- When the next "Data" message is received, a similar replication process to the one shown above, is performed to verify the content of the dPack again. Alice now has a full list of the files in the dPack and can choose which ones she wants to download. 

## 1.5 A DECENTRALIZED WEB AT GLOBAL SCALE
-----------------------------------------------------------
Being that a dPack and dDrive can support millions of cryptographically validated and versioned files, in a single repository that is ultimately synchronized, distributed and exchanged between peers of a secure peer-to-peer network, without the need for a data center or any central hosting providers, means any network that is based around the dWeb protocol is a decentralized intranet that can operate at global scale. In other words, the more people who join a dWeb-based network, only add to its network resources, rather than diminish its resources, because data is shared between users and not shared via a central location, with centralized infrastructure. That data is also secure, because it's cryptographically validated and versioned, where it can always be verified back to the original publisher. 

### Peer-To-Peer Web Hosting
---------------------------------
Due to the way websites and web applications, distributed via dPacks and/or dDrives, are exchanged between peers over a network, instead of being shared via a centralized server, the need for web hosting has been eliminated. Developing websites or web applications with programming languages like PHP, which only works alongside centralized DBMS's, are only designed to develop applications for a centralized architecture. This is why dWeb embraces the JavaScript programming language and all current DBMS's designed for the protocol are written in JavaScript. This allows developers to build "host-less" websites and applications that scale to the global resources of the network without a single central point of failure, as long as dTLDs (decentralized top-level domain names) are used for resolving websites and web applications, rather than centralized TLDs that can be seized or lost.

# 2. STATE OF THE PROTOCOL
------------------------------------
dWeb's protocol has already been implemented into a series of decentralize software projects and is even being used by blockchain networks for its many off-chain resources. Below are a list of dApps, dSites and developer tools that already use the dWeb protocol and dWeb's dDBMS frameworks. We will continue to update this section of the whitepaper, as more projects adopt the protocol. Below, is the current state of the dWeb:

**NOTE:** ***This list is constantly growing and will continually update***

## 2.1 dApps
- dPress - Decentralized CMS (Content Management System) for creating dWeb-ready dSites, using a drag-and-drop UI. 
- dHosting - Purchase seeds for dSites and dApps (Under development).
- dBrowser - dWeb-ready web borwser. Browse over dweb:// and http://. For MacOSX, Windows and Linux.
- dStatus - dWeb and dSiteDB-based social network, similar to Twitter.

### 2.2 dSites
- dWeb - The official dWeb site is available over the dWeb at dweb://dwebs.io and dweb://dweb.link
(we are currently compiling a long list of dSites that are available and will be revising this section of the whitepaper soon).

### 2.3 Developer Tools 
- dPack CLI - Official CLI for interacting with the dWeb, creating and distributing dPacks across the network and a variety of other things. 
- dDatabase (dDBMS) - JavaScript-based dDBMS framework built for use over the dWeb protocol. 
- dSiteDB (dDBMS) - JavaScript-based dDBMS framework built for use over the dWeb protocol.
- dAppDB (dDBMS) - JavaScript-based dDBMS framework built for use over the dWeb protocol.
- dDrive CLI - Official CLI for dDrive, so developers can easily create and distribute dDrives across a dWeb network.
- dPack Core JS Library - JavaScript API for interacting with dWeb-based networks.
- dWeb University - Official site for dWeb-based documentation.
- dPack Forever - CLI for keeping dSites and dApps syncing "forever".
- Dr. Satoshi - CLI for checking dWeb's network health.
- Bootstrap DHT Bootstrap CLI - Bootstrap a BitTorrent DHT server.
- Revelation CLI - CLI for bootstrapping your own dWeb revelation server. 
- dDNS Lookup CLI - CLI for performing dDNS lookups and Multicast DNS lookups.
- dWeb Tower CLI - CLI for launching dWeb announcement/broadcast towers.
- dDNS Server CLI - CLI for launching dDNS servers.
- dBrowser's dPack Client API - JavaScript API that dBrowser uses to interact with dPacks.
- dPack JS Client API - JavaScript API for interacting with dPacks.
- dWeb Vault Client API - JavaScript API for interacting with dPacks in "vault" storage mode.
