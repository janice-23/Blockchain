# Distributed Hash Tables 

Janice Ng, April 2019

## **General Overview on Distributed Hash Tables (DHT)**

**Library Analogy** 

Imagine all of mankind’s knowledge is written down in books, and the books are stored in a network of libraries all across the world. There’s a few reasons why we would do this: there’s too many books to store them all in one library, and nobody should need to travel across countries to reach a book. Ideally, though, no one authority is controlling which libraries store which books, as that could open the door for censorship. We’re trying to design a protocol for assigning books to libraries. 

One of the libraries would be one node in the network, while the knowledge is the data stored across many nodes that enter and leave the system. 

**Hash Tables** 

Hash tables are key value stores where the key is hashed to identify the node containing its value. Hash functions, hash values and routing algorithms are key elements of a Hash Table. The hash function must be deterministic, which means that there is a one-to-one mapping between an input and output. The Hash Table allows you to insert, lookup, and delete objects with keys. 

**Distributed Hash Tables (DHT)** 

DHT is a distributed database that can store and retrieve information associated with a key in a network of peer nodes that can join and leave the network at any time. The DHT protocol determines how data is distributed among nodes, ensuring that they can be easily searched for and retrieved. It consists of two functions:  *store(k, v)*  and *r*  *etrieve(k)* . Nodes coordinate, among themselves, to balance and store data in the network without any central coordinating party. In order to scale a large number of nodes, the mapping from key to value is maintained in its distribution among the nodes. A change in the set of participants causes a minimal amount of disruption. 

**Main Properties of a DHT**

1. Autonomy and Distributed
Without any centralization, all nodes coordinate to form the system. Any one node can
coordinate with a few other nodes, with a certain distance, in the system.
2. Fault Tolerance
Although nodes join, leaves, and fails, DHT must be reliable and secure against malicious
participants.
3. Scalability
The system should be efficientin scaling as the number of nodes scales. This deals with more
traditional distributed system issues such as: load balancing, data integrity, and performance.



## **General Overlook on Structure of DHT**

**Structure of Keys** 

As DHTs require that information be evenly distributed across the network, consistent hashing is used. Consistent Hashing is an abstract notion of the distance between keys: k1 and k2, and employs a function  δ*(k1, k2)*.  The distance has nothing to do with geographical distance or network latency. Rather, each node is assigned a single key: identifier (ID). A node ID *i*  *x*  owns all the keys *k*  *c* f  or which  *ix* i  s the closest ID; this is measured according to the function  δ*(kx, ic)*.  To ensure that each node in the DHT network has equal chance of being chosen to store Key/Value Pair, key goes through a hash function to form a hash. 

**Routing and Lookup Cost** 

DHT nodes only store a portion of data, thus, there is a routing layer for any node to locate the node that stores a particular key. It must be noted that mechanisms and details of how routing table is maintained as nodes join and leaves the network is what differentiates DHT algorithms. In general, when a node joins the network, routing information is disseminated to a small number of peers. Since each node only contains a portion of the routing table, the process of finding or storing a Key-Value Pair requires contacting multiple nodes. The number of nodes that need to be contacted is affected by the amount of routing information each node stores. A common lookup complexity is O(log n), where  *n*  is the number of nodes in the network. For example, in a network of one million nodes, only 20 nodes would need to be found. 

**Iterative and Recursive Lookup**

**1. Iterative** 

Iterative lookups are less efficient than recursive lookups. Iterative lookups require a requesting node to query another node asking for Key-Value pair, if it is not responsible for it. If the node 

does not have Key, then it will return one or more nodes that are closer. This process is repeated until either Key-Value pair is found and returned, or it will return an error from the last queried node that the Key cannot be found. 

**2. Recursive** 

Recursive lookups require the first requesting node to query the next closest node, which then queries the next closest node until the Key-Value pair wanted is found. The data is then passed back along the chain of requests to the requestor. 



## **Application: DHT and Healthcare**

DHT is efficient in Key-Value lookups but not joins. Joins, in this case, is the protocol of multiple Key-Value pairs needed to be looked up in order to retrieve information wanted. In Healthcare, Electronic Health Records (EHT) can be stored as a single Key-Value Pair, which reduces lookup time for a single record of a patient. However, patient records are large as there are multiple of records - this will take a significant network bandwidth and time to download the 

entire file. However, this can be solved by making a key that stores a list of keys to other records. The key can act as a search index for a patient’s record, where the record is broken up and each component is stored under its own Key-Value pair. This acts as a solution as it allows a requestor to only download records they want while being evenly distributing data across the network, and effectively increasing data durability and availability. 

**Blockchain vs DHT in EHR** 

The reason for why Blockchain is not used for EHR records is due to multiple of reasons. Firstly, Blockchain nodes need to store the entire database in order to maintain their security guarantees. It is not practical to store the patient’s record directly on the Blockchain as a huge amount of data would be stored and is cost prohibitive. Secondly, even if the Blockchain is optimized to store compressed amount of data, the security risk would still be significant. In general, the only safe way to store private information on a Blockchain is to encrypt data. However, for EHR, it is inconvenient to encrypt data as it limits the overall usefulness of storing information to ultimately be shared in an emergency or even in general. 



## **Evolution of DHT**

**Napster** 

Napster used a central indexing server to provide a “host list” of users who were logged into the system at the time. When a user searched for a file using *N*  *apster Client,*  the server would look through the host list and their files to see who had them and provide requester with a list of hosts who had their file. To apply this to an analogy, this would be similar to having a central library responsible for storing the location of each book at all libraries that it has interacted with it. If a client wants to retrieve a book, they would need to contact the central library first and retrieve the information of the library where the book was held and contact specific library to get the book. In this case, Napster is the *c*  *entral library and*  users contact Napster and is redirected to a  *host*  (specific library) who has their file. 



## **In-Depth Case of DHT: Kademlia**

**General Overview** 

Kademlia is one of the most popular decentralized P2P DHT; it is used in BitTorrent and IPFS. In Kademlia, configuration information such as nodes and neighboring nodes on the network are spread automatically as a side effect of *k*  *ey lookups;* n  odes  *are* k  nowledgeable  *of* o  ther nodes. 

**Node Search** 

Kademlia is represented in the form of a binary tree where nodes are the leaves. Each node is identified by a Node ID, which is used to locate values that are hashes. The key, 160-bit, associated with the value being searched for must be known in order to search for its location. From the node’s location in the tree, it traverses down to find the particular node wanted. Nodes that are closer to the key are found at each step until the contacted node returns the value being searched for, or no more closer nodes are found. Searching for ‘n’ nodes in the system takes  *O(log(n))* t  ime - which is very efficient. 

**Membership Changes** 

In Kademlia, each node consists of a list of triples: IP Address, UDP Port, and a Node ID, and a routingtablethatcomposesofabinarytreewhoseleavesarek-buckets.*K*  *-buckets* arealistof routing addresses of other nodes in the network, which are maintained by each node. The node only keeps a list of nodes of distance 2i and 2i + 1 from itself, which will be stored in its binary tree as the node will know the set of nodes from each of its subtrees. When a node receives any messages, request or reply, from another node, it updates appropriate k-buckets for the sender’s Node ID. 

When updating k-buckets, there are three different possibilities that must be taken into consideration. Firstly, if the sending node already exists in the recipient’s k-bucket, the recipient moves it to the tail of the list. Secondly, if the node is not in the appropriate k-bucket and the bucket has fewer than k entries, then the recipient has to insert the new sender at the tail of the 

list. Thirdly, if the k-bucket is full, the recipient pings the k-bucket’s most least recently seen node to decide what to do. In this case, if the least recently seen node fails to respond, it is evicted from the k-bucket and the new sender is inserted at the tail. On the other hand, if the least-recently seen node responds, it moves to the tail of the list and the new sender’s contact is discarded. 

There are two main advantages of Kademlia’s use of k-buckets. Firstly, k-buckets implement a least-recently seen eviction policy where only live nodes are not removed from the list. By keeping the live and oldest nodes, the k-buckets maximizes the probability that the nodes they contain remain online. Secondly, it provides resistance to certain DoS attacks as Kademlia nodes will only insert nodes in the k-buckets when old inactive nodes leave the system. This increases the number of known valid nodes and provides for a more stable network. 

**Routing** 

To find a Key-Value pairs, the node starts by performing a lookup to the find the k nodes with IDs closest to the key, which is done through Kademlia’s recursive lookup algorithm. The lookup algorithm is the procedure by which a node locates the k closest nodes to some given key. The process begins with a lookup initiator where α nodes are picked from its closest non-empty k-buckets. The initiator then sends parallel, asynchronous FIND_NODE RPCs to the α nodes it has chosen. FIND_NODE is a protocol message where the recipient of the request will return the k nodes in its own k-bucket that are the closest to the requested key. In the recursive step, the initiator resends the FIND_NODE to nodes it has learned from previous RPCs. From the k nodes the initiator has seen that are closest to the target, it picks α that it has not queried yet and resends the FIND_NODE RPC to them. If a node fails to respond quickly, they are removed from being considered. If a round of find nodes fails to return a node any closer than the closest already seen, the initiator resends the find node to all of the k-closest nodes it has not queried. The lookup terminates when the initiator has queried and receives responses from the k-closest nodes it has seen. The best k nodes in the resulting list are the ones in the network that are closest to the desired key. 

To accelerate lookups, Kademlia uses a X-OR metric, which is unidirectional, to define distance. Two node ID’s or a node ID and a key are X-OR-ed, and the result is the distance between them. Each Kademlia node has a 160-bit NodeID and key of every data is also a 160-bit identifier. In order to decide which node a Key-Value pair should be stored, Kademlia uses the notion of distance between the 2 identifiers. This is done through X-OR-ing the two 160-bit identifiers, and can capture the notion of distance implicit to the binary tree sketch of the system. For example, the distance between 0011 and 1001 would be: 0011 ⊕ 1001 = 1010. 