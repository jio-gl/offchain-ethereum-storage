# offchain-ethereum-storage
 
 ## Storage on IPFS
 
 Using a Merkle B-tree implemented on a decentralized public (and free) storage (like this implementation https://www.npmjs.com/package/merkle-btree) we satisfy the requirement of have a free and fast storage for the dataset. Now the problem remains who can update the root of this Merkle tree, that is the administrator.
 
 ## Smart Contract Admin
 
 Now the database will be administered by an Ethereum smart contract. Then we can have, for example, and open database where anyone can add elements but only the owner of the smart contract can remove data. Or we can have a group of administrators that can add or delete elements from the database. In the standard Ethereum-type blockchain, everything is public, so anyone can read the database if is in plain-text. If you use an encrypted database you can have that too.
 
 In the smart contract, at least you need to store the root of the Merkle B-tree, and anyone update the database/table will have to update the root of the tree on the smart contract.
 
 ## Checking immutability
 
 Maintaining immutability of the database accross transactions is a property that we want to move from Ethereum into our off-chain storage. For this, we use Merkle Proofs (https://medium.com/crypto-0-nite/merkle-proofs-explained-6dd429623dc5). We store in the smart contract of the database, only one Merkle Proof per database, and only a new valid Merkle Proof that is a valid successor of the previous Merkle Proof can replace the previous one. Regarding ordering or transactions, if we have two concurrent transactions on the database on the same block, only the first one will be applied effectively in the database. The other transaction will not be applied because now the Merkle Proof will be invalid as the tree will have changed.
 
 
