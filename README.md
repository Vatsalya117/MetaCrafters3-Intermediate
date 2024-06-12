# Auction House Contract
The AuctionHouse is a Solidity smart contract that allows users to create auctions, bid on items, and view the highest bidder. It includes functionality for creating new auctions, placing bids, closing auctions, and viewing auction results.

## Features
### Auction Creation:
Users can create new auctions with a specified item and starting price.
#### Bidding: 
Users can place bids on open auctions, with the highest bidder being updated in real-time.
#### Auction Closure: 
Auctions can be closed, and the highest bidder declared the winner.
#### Auction Results: 
The contract provides a way to view the results of closed auctions, including the winning bidder and bid amount.
#### Error Handling: 
Demonstrates the use of require() and modifier for safety checks and error handling.
## Events

#### NewAuction: Emitted when a new auction is created.
``auctionId: The ID of the new auction.
item: The item being auctioned.
startPrice: The starting price of the auction.
BidPlaced: Emitted when a bid is placed on an auction.
``
#### bidder: The address of the bidder.
``auctionId: The ID of the auction being bid on.
bid: The amount of the bid.
AuctionResult: Emitted when an auction is closed.
``
#### auctionId: The ID of the closed auction.
``winner: The address of the winning bidder.
winningBid: The winning bid amount.
``
### Functions
#### Constructor
``solidity
constructor() {
    auctionCount = 0;
}
``
### Create Auction
``function
    auctionCount++;
    auctions[auctionCount] = Auction(item, startPrice, 0, address(0), true);
    emit NewAuction(auctionCount, item, startPrice);
}``` 

Allows users to create new auctions with a specified item and starting price.

### Place Bid
``function
    require(bid > auctions[auctionId].highestBid, "Bid must be higher than the current highest bid");
    auctions[auctionId].highestBid = bid;
    auctions[auctionId].highestBidder = msg.sender;
    bidderBids[msg.sender] = auctionId;
    emit BidPlaced(msg.sender, auctionId, bid);
}
``

Allows users to place bids on open auctions, with the highest bidder being updated in real-time.

### Close Auction
``function
    auctions[auctionId].isOpen = false;
    emit AuctionResult(auctionId, auctions[auctionId].highestBidder, auctions[auctionId].highestBid);
}
``

Allows users to close auctions, declaring the highest bidder the winner.

### View Auction Results
``function
    return (auctions[auctionId].highestBidder, auctions[auctionId].highestBid);
}
``

Allows users to view the results of closed auctions, including the winning bidder and bid amount.

## Usage
Deploy the AuctionHouse contract to an Ethereum-compatible blockchain.

Interact with the contract using a web3-enabled browser or a dApp interface.

Use the createAuction function to create new auctions.

Use the placeBid function to bid on open auctions.

Use the closeAuction function to close auctions and declare winners.

Use the viewAuctionResult function to view the results of closed auctions.

## Help
If you encounter any issues or have questions, please refer to the documentation or contact the contributors:

## Authors
Vatsalya Mishra

https://github.com/Vatsalya117
