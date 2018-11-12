# dtickets
## Intro
This ticket sale project is inspired by a Consensys Academy final project called [dtickets](https://github.com/pacoard/dtickets)

In that project, some Solidity smart contracts were developed to allow anyone to start the sale of tickets to an event in the form of ERC721 tokens. These tokens are non-fungible, like baseball cards, so they are ideal to use as tickets to enter any event, whether it is a paid ticket or just a from of RSVPing.

Example: a band wants to sell tickets for a concert, but wants to avoid the high middle-man fees when distributing them... They can just hire a blockchain engineer to deploy the dtickets smart contract configuring price, max number of tickets, name of the event and any other metadata in a file that can be uploaded to IPFS. Once that is done, a function call will start the sale and the clients can purchase tickets through a web3-frontend. The smart contract stores who owns what tickets as a distributed source of truth.

## Smart contracts
- **ERC165.sol**: indicate which interfaces our smart contracts implement
- **ERC721.sol**: ERC721 interface, with functions to transfer, approve transfers and other useful and common functions to interact with tokens
- **TicketSale.sol**: (is Ownable) logic of the ticket sale, with a state-machine design pattern. It initializes the parameters and lets the owner manipulate them
- **TicketOwnership.sol**: (is ERC165, ERC721, TicketSale) last contract that inherits all the rest and therefore deployed. It adds the necessary ERC721 logic to implement its interface.

Although the implementation of these contracts was pretty thorough, it doesn't consider security risks very much and it costs about 0.28 ETH to deploy (tested with Ganache). That seems very fixable...

## Frontend
Implemented with Web3, React and a [Bootswatch](https://bootswatch.com/) template, it enables users to enter the ticket sale contract address and buy tickets. AND THAT IS IT.

The frontend would probably have to get done from scratch, as it was done in probably two nights and it poorly uses ethjs instead of web3. The UI is too simple and not intuitive at all, as it doesn't show any instructions on what to do. It does check and show the state of web3 (enabled? which address is being used?).