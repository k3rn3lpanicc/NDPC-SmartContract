# Storage Space needs



# EntryPoints (Functions)

- mint (`meta_data`, `number_of_copies`) : Only Producers can mint NFTs and it will be minted to their account

- approve (`token_id?`, `publisher_id or publisher_address`, `amount_of_tokens`) : approves for the publisher to sell specific amount of NFTs of the producer




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

# Challenges

- How to transfer money (token) with smart contract on casper network
- Build this SC(Smart Contract) with minimum amount of calculations and storage usage
- Mint high amount of NFTs with low cost
- Find a way to put the actual data representation (not metadata) on a p2p file storage and link it to the actual product (should we support multiple services?)
- Find a way to test contract without multiple deploys (It's pain in A:) )


# Questions (Issues)
- Are publishers the ones who transfer NFTs or are users who request to transfer the nft by publishers? I think the second one is more rational


# Done So far
