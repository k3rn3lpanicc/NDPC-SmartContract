# Record Merch
## Front-end Part
We should form a Metadata of the product, it can be anything formed as a json object, for example :
```!bash
{
    "color" : "Black",
    "size"  : "44",
    "ProductID" : 1234,
    "ProductName" : Nike Shoes
}
```
Obviously you can form it in another way (as you want)

We have a `recordMerch.js` script in front, which exports a function named `record_merch` which's inputs is like this : (metadata (that we discussed before), account_information (which we fetch from user's wallet when they log in), Product_title(string), price(number), amount(number)).

You should pass these information to the `record_merch` function, it will automatically upload the metadata to IPFS and gets the address of it, creates a deploy which calls the mint entrypoint of the contract, request the user's signature (pops up a sign request in user's wallet), and when the user signed that deploy, it will return its signature back.

So by calling this function you would get a signed deploy, but is still needs to be deployed, front-end needs to send this deploy object to Back-end where it actually will be deployed on casper.

## Back-end Part

We have a `recordCasper` function in `recordMerchback.js` which takes the signed deploy from the front-end and deploys that transaction into the casper network, then grabs its deploy-hash and returns it. then you should send this deploy hash to `Queue-Server` which checks each event in casper network, and calls a call-back when it found that deploy hash in events of casper network, or it timed out (around 5 minutes). backend will also inform the front-end when it got that call back so front-end can update it's UI based on it.

## Queue-Server Part

The `deploy-hash` which was output of the `recordCasper` function will be sent to this server using a API call, it holds all the deploy-hashes in the database (so when something went wrong, it could load back the data on a restart), and when a event arrived from the casper-network, it checks it with all the deploy hashes in the database and if it was one of them, it'll change the state of that deploy hash in database to checked, and calls the call-back function to inform backend whether it was successful or not (user had not enough casper-tokens in it's wallet to call mint function). Also each deploy hash's state would change to Timedout when 5 minutes after it recived that deploy-hash, no events gets emitted from the casper related to that hash, and it will also call the callback function to inform backend about it.