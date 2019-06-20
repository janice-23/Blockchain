# Consensus Protocols: Simple Comparison of POW vs RAFT

Janice Ng, November 2018



## Blockchain Consensus: 

Blockchain Consensus Mechanisms are crucial for blockchain in order to function effectively. On a blockchain, anyone can add anything, thus, it is necessary that all transactions are constantly checked by nodes. Without a good consensus mechanism, the blockchain is at risk of being attacked. In general, a consensus mechanism involves servers agreeing on certain values. In order to get a consensus, all nodes must be synchronised with one another and agree on the legitimate transaction before it is added onto the blockchain.

## Proof of Work (POW):

One of the most used consensus mechanisms is Proof of Work (POW), which is used by Bitcoin. POW is an algorithm used to confirm transactions which is then added as a new block to the chain. With POW, miners, who compete against each other, must use mining and computational work to solve mathematical problems to authenticate transactions. The unique concept about POW is that it does not require all miners to submit a conclusion in order for a consensus to be reached. Rather, it uses encrypted transactions in a block, which are hash functions, to create a circumstance where one miner within the network share their conclusion, while other miners verify the conclusion. If the conclusion is verified, the new block is formed.

POW has many advantages, mostly in security. POW has a defense against DoS (Distributed Denial of Service) attacks as in order to efficiently attack the network, a lot of computational power is required to do the calculations. Thus, an attack is possible but is useless since the costs are too high. However, the disadvantage of POW is the huge energy costs of computing as it consumes a lot of electricity.

## RAFT:

An alternate consensus mechanism is Raft (based on Paxos), it takes on a leader-based approach. Raft deconstructs consensus into three individual subproblems. First, one server acts as a leader and is assumed to always be correct. The leader is elected when the algorithm begins and sends ‘heartbeats’ to other nodes. If the other nodes do not receive a ‘heartbeat’, a new election cycle will begin to select a new leader. The other nodes replicate the entries proposed by the leader. If the leader crashes, the remainder of the network will elect a new leader and the network will continue to function. Secondly, log replication. The leader accepts commands from clients, replicates the log to other nodes and ensures all nodes have followed the request. Thirdly, the logs must be consistent and up-to-date ignorer to ensure safety. 

Raft has evident advantages in speed of block time as it does not mint empty blocks. Mint, in this case, means using calculating energy to generate a block. Thus, Raft allows storage space to be saved and gives a faster block time. However, Raft’s disadvantage is that there is no protection from attacks. If the leader wants to create a fake transaction, other nodes will generate this transaction. In my opinion, Raft should only be used in consortium blockchain unless there are improvements to ensure protection from attacks. 