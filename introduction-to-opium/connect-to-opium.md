# Connect to Opium

The Opium Network is an **attempt** to transfer the financial market and its participants' functions to the blockchain. A certain part of the financial market has automatic stabilizers or is driven by market mechanisms. 

It is impossible and also not needed to try to program these functions on the blockchain. Instead, there are several participants \(acting in economical interest\) that ensure the market is efficient:

* Relayers
* Affiliates
* Market makers
* Arbitrageurs
* Executors of contracts
* Data suppliers
* Product designers

**Connect as a relayer**

A relayer can participate in the network and earn relay-fees for collecting orders, matching them in the best possible way and broadcasting them to Opium for settlement. Users sign their orders with their private key, which allows the Opium Network to withdraw funds from their balance that are needed to execute the order. Note that users' funds can never be stolen by the relayer!

**Connect as an affiliate**

An affiliate will participate by looking for the best prices in the market at other relayers and redirecting users' orders to the relayer that offers the best price. An affiliate does not broadcast orders to the blockchain himself though, he is an aggregator of order books. An affiliate will charge an affiliate fee to the users he redirects, and if he sees fit, he can also act as an arbitrageur.

**Connect as a market maker**

Market makers are incentivized to participate in the network by creating markets and charging their prices for a certain risk or asset, aiming to earn a profit premium. We expect that eventually, the most popular markets will not need market makers, but less liquid markets will always give opportunities for market makers to step in.

**Connect as an arbitrageur**

Arbitrage opportunities will arise in low liquidity or dispersed markets and can come from various sources. Arbitrage in its simplest form is buying and selling a single product that is traded for different prices in different places. In more complex forms, arbitrageurs might step in if a futures market is in contango, go long on single assets and short the index token or playout option prices against each other. These profit opportunities eventually create an efficient market for traders.

**Connect as a data supplier**

Oracles often request data from off-chain sources, and this can be supplied in various ways \(see Oracle and derivative recipes section\). Suppliers of data, that bridge the blockchain with the real-world, will charge a fee for their service. Often, the charged fee is calculated according to security needs.

**Connect as a product designer**

Product designers can participate in the Opium Network in two ways: by combining existing products into one new product and by designing a new derivative recipe. By combining existing products into 1 new product \(such as notes, spreads, and portfolios\), product designers can earn a risk-free profit. If a product designer decides to connect a new derivative recipe to the Opium Network, he can charge a fee to everyone that uses his derivative recipe in their contracts.

