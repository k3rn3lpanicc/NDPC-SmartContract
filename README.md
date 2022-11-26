# Storage Space needs

- cep78_metadatas : `Map<token_id => token_metadata>`
- publishers : `List<account-hash>`
- producers : `List<account-hash>`
- total_supply : ?


# EntryPoints (Functions)

- mint (`meta_data`, `number_of_copies`) : Only Producers can mint NFTs and it will be minted to their account

- approve (`token_ids?`, `publisher_account_hash`, `amount_of_tokens`) : approves for the publisher to sell specific amount of NFTs of the producer
- add_producer (`producer_account_hash`) : add a new producer to `producers` list

- remove_producer (`producer_account_hash`) : remove the producer from list

- get_metadata(`token_id`) : returns the metadata (as `String`) of the NFT token
- balance_of (`owner : Key` , `token_id`)

- owner_of (`token_id`) : returns the `Account-Hash` that owns that token

- total_supply() : returns total number of minted NFTs untill now

- transfer_from (`sender` , `reciver` , `token_id`  , `count`)




# Groups

## Producer

Producers are the companies which produce products (that will be digitized as NFT's in their account)

We need a `add_producer` entry_point which will add an producer's account-hash (or public-key) to our `producers`

## Publisher

Two possible things :

    1)Publishers are the actual sellers of the NFTs, they can transfer an NFT (that has been approved for them by producers) to another account (user or maybe smart contract)
    2)Publishers are the ones who can sell NFTs on side of producers, but *Users* (or contracts) are the actual ones who request a NFT token and buy it from publishers (with tokens)
    

# Definitions

- Producer : mentioned above
- Publisher : mentioned above
- approve : let another account (publisher) sell our product for us
- disallow : get back the approvment from a publisher (ban them from selling Producers)
-

# Challenges and TODOs

- How to transfer money (token) with smart contract on casper network
- Build this SC(Smart Contract) with minimum amount of calculations and storage usage
- Mint high amount of NFTs with low cost
- Find a way to put the actual data representation (not metadata) on a p2p file storage and link it to the actual product (should we support multiple services?)
- Find a way to test contract without multiple deploys (It's pain in A:) )
- Find the documentation related to gas price in casper
- Revert the mint request if the metadata was not valid (in cep47 format)

# Questions (Issues)
- Are publishers the ones who transfer NFTs or are users who request to transfer the nft by publishers? I think the second one is more rational
- Can the producers sell their product themselves ? 
- Companies should be able to monitor which one ?
    - Each token is owned by who (list of accounts) OR
    - Each token is owned by how many accounts ?

# Done So far
- Created Structs `NFTHolder`, `NFTMetadata`, `ApprovedNFT` , `MetadataHash` and functionalities (like finding hash of metadata and represent it as string (hexadecimal)) and implemented `to_bytes` and `from_bytes` for them to be able to put them in dictionaries and read them after wards
- Tested above functionalities in testnet and optimized the code
- Created the storage and functionalities model(blueprint) in draw.io (the file is in this repo). I'm trying to fulfill all the needs with smallest amount of storage and calculations needed. (This part is not done completely yet)
- Tested session/contract code for transfering tokens from contract purse to account and vice versa.
