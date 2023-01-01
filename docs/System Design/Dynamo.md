# Dynamo

1. Distributed key-value store
   - available
   - scalable
   - decentralised
2. AP type of system under CAP theorem.
   - designed for high availibility and partition tolerance at cost of strong consistency
3. Uses Consistent Hashing to distribute data among nodes.
4. Gossip protocol
5. Hinted handoff

## Data Partitioning

#### Problems with normal hashing

- finding correct node where data is present.
- resolving in consistency upon addign removing nodes.

Solution: Consistent Hashing.

Steps to store data:

- Apply MD5 hashing algo on key.
- check which range the hash lies.
- insert data in the particular node.

- Uses concept of virtual node.
  Each node is furthur subdivided into smaller sub nodes for duplication of data.

# [WIP]