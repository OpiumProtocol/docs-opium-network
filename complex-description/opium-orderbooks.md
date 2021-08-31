# Opium order books

The Opium Network transfers the clearing, settlement and trading functions from centralized agents to the blockchain, with support of relayers. Core and sensitive functions are stored on-chain and all computational intense processes are run on the overlay of relayers but verified on-chain. Relayers are motivated by commission fees and can also carry out arbitrage functions between different orders, markets, and ecosystems.

The Opium Protocol is unbiased towards how matched orders are broadcasted to the blockchain and how order books are presented to users. What matters for the protocol is that TMtm interfaces are used and orders are matched correctly. 

Orders can be broadcasted to the blockchain by anyone. Though, relayers might require the user to state ‘senderAddress’ - the only Ethereum address that is allowed to broadcast the orders to the blockchain. This prevents frontrunning and order collision and enhances the trading experience.

Relayers can set up order books that are quoted in any base margin currency and are free to benefit from arbitrage opportunities by matching orders in different order books, making a free profit whilst providing liquidity to the system. TMtm order models can be used for simple trades, but also allow users to set up complex orders.

