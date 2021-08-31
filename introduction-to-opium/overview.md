# Opium Network

The Opium Network is a complete, consistent and learning ecosystem to create, settle and trade virtually all derivatives in a trustless way.

![The 6 qualities of the Opium Network](../.gitbook/assets/image%20%285%29.png)

**Creation**

The creation of a new derivative recipe is as simple as deploying a smart contract in the Ethereum network. The contract has to contain Opium required functions with standard interfaces to provide the data about specific details of a new derivative type: initial margin sizes for participant, immediate payout of a premium, if the execution is possible before the maturity date, functions that are based on oracle calculations and reporting of margin re-distribution after expiration.

Derivative recipes are crucial for the repayments, so they should be checked by auditors before one considers to allocate money there. Most of the users will not check derivative recipes' open-source code themselves, but they may see the author of the derivative logic or the status of the community audit. It is possible to sign the deployment of a derivative recipe with your signature connected to an ETH domain name.

#### Trading

Opium is a gas efficient trading protocol that provides off-chain matching of orders and on-chain execution. Each order is signed by a user and allows Opium to execute the desired trade. Orders can be constructed conveniently so that combined orders for tokens or portfolios \(including classical trading orders as spread trades, swaps, and rolls\) can be carried out.

The Opium network can execute create and swap functions. Both functions receive matched requests from the relayer with signed orders attached. The functions require margin allowance from both counterparties and mints tokens as a result of the deal. 

#### Settlement 

The settlement of all transactions, minting, and burning of tokens and execution of the derivatives are all done in the Opium Network. External logic is limited to the feeding of the data about the derivative logic and its features. In other words, all derivatives within the Opium Network are treated the same and the differences are described by creators and are located in external contracts with Opium interfaces.

#### Learning

Once derivative and oracle recipes with desired logic are deployed, the Opium Network “knows” the corresponding logic of such derivatives. They can be settled and traded in any quantity and it can be used by the ecosystem to create any product.

#### Consistency

All tokens in the ecosystem are interchangeable and have the same process logic \(margin inputs/outputs\). Moreover, they can be wrapped into portfolios processed within the Opium Protocol with the general TMtm request format. Opium derivatives and oracles can be underlying assets for other Opium derivatives or oracles. That's why we say that the ecosystem is consistent.

#### Completeness

The definition of Opium derivatives covers most of the financial derivatives and goes even broader to some interesting non-financial applications.

Margin requirements and distribution formulas have Turing complete logic, thanks to the Solidity programming language. Moreover, derivative recipe formulas are triggered by oracle recipes or other derivative recipes, so one derivative recipe can have another derivative recipe as an input. This means that a derivative can be made on a derivative or underlying oracle feed.  


  




