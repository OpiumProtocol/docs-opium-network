# Glossary

**Margin token:** any ERC-20 token that is specified in the contract and used for collateral and payout of the position.&#x20;

**Opium position token:** after the creation of a contract, tokens that are minted by the Opium minter represent a short or long position that consists of information of a derivative and oracle recipe and a prepaid margin. Opium derivative tokens can easily be composed into portfolios and traded in any ecosystem that supports the ERC-721 token standard.\
\
**Opium portfolio token:** multiple Opium derivative tokens can be composed into an Opium portfolio token and traded as one. Portfolios can be recomposed by taking out or adding Opium derivative tokens from the portfolio. At any time, portfolios can also be decomposed, turning the whole portfolio back into Opium derivative tokens.

**Opium derivative:** a **** financial agreement where parties downpay specified margins that will be redistributed after maturity according to the specified oracle and derivative logic. Every derivative also differs according to parameters, such as maturity and required margin.&#x20;

**Derivative recipe:** a derivative recipe is a set of logic that defines how certain margin input is recalculated into a payout at the end of a contract. The derivative recipe needs data input to come to an exact number**.** This data is fed by the oracle recipe. As derivative recipes are Turing complete, almost any financial product can be created.

**Derivative register:** the derivative register keeps track of all the underlying margins behind each ticker and oracle ID to make sure that there is always enough margin in the system, even if a third party derivative recipe is corrupted.

**Oracle recipe:** An oracle recipe describes how data will be fetched from an off-chain or on-chain source, which data exactly will be fetched, and how this data will be processed. As oracle recipes are Turing complete, it allows for very specific data input. Besides price data, it also supports event and status data.&#x20;

**Oracle register:** the Oracle Register stores all the data, supplied by oracle recipes, that was ever requested by the system. In this way, data only has to be transferred once to the blockchain and all other contracts using the same data can use this without paying fees for transferring the data.

**Opium swaps (TMtm):** in order, a user signs how much of what he wants to receive, and how much of what he is willing to give in return. This can comprise very complex swaps built up from multiple components such as assets, tokens, and derivatives and gives a professional trading experience.

**Opium relayer:** an Opium relayer matches users' orders and broadcasts them to the blockchain. He is incentivized by a relay fee and possible arbitrage opportunities that he can find between different markets and platforms.

**Opium affiliate:** an affiliate looks for the best prices in the market and redirects users' orders to the relayer that offers the best price. An affiliate does not broadcast orders to the blockchain himself. For his services, an affiliate will most likely demand an affiliate fee. \
\
**Opium minter:** after the creation of a contract, the Opium minter mints long and short derivative tokens to the respective owners of the positions. The Opium minter is also responsible for composing and recomposing portfolio tokens and burning position tokens after a contract has matured and paid out.

**Ticker:** a ticker is made up of the derivative and oracle recipes and the parameters (such as maturity, margin and strike price) that make up the agreement.

**TokenID:** besides the information that a ticker shows, a tokenID also specifies if someone owns the long or short token of an agreement.&#x20;
