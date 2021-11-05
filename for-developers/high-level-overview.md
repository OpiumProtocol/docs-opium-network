# High-level overview

The Opium Protocol is an oracle-agnostic smart escrow that allows to build and trade fully customizable financial products in a trustless fashion.

The two building blocks of the Opium Protocol are derivative recipes and oracle recipes. A derivative recipe encodes the financial specifications that describe a product whereas an oracle recipe specifies what data source should be used to settle a product upon its expiry.

![](https://lh5.googleusercontent.com/xnPdBzlfeBb\_fEbGLPQCEnzvwUb7VpHgWOv9RiMh\_12UOBiArmYkXa9Jik2fuCPHW-9gwA0\_DMx91AahOyP\_YPTFp8eCJA-ct5altEKpO5TzkJfU3T-dBOu9U\_8I8SYBJQj6zVpI=s0)

### Development life cycle  of a derivative:

From a developer perspective, the main steps to develop a financial product on top of the Opium Protocol can be broken down into a few simple steps:

1\) Creation of an oracle

2\) Creation of a derivative recipe

3\) Provision of the oracle data upon the derivative’s maturity in order to perform its settlement

4\) Execution\


Let’s go through them step by step.\


Each financial instrument built on top of the Opium Protocol needs to be associated with an oracle whose responsibility is to provide the necessary data for its settlement. An oracle can be either an on-chain or an off-chain data source.&#x20;

From the Opium Protocol’s perspective, what matters is that the OracleAggregator - the data layer of the protocol- receives a derivative recipe’s required data within a specific time frame after its maturity. As such, off-chain data sources, although not in line with the spirit of decentralization, can be used if a derivative author wishes to do so, further decreasing the development burden placed required to craft financial instruments on Opium. \


Moving on to the second step, once a ‘source of truth’ for a financial instrument has been established, it is immediately possible to create a derivative recipe - hence mint LONG/SHORT positions for it. Derivative recipes can be created both by contracts or off-chain with the usage of a client library (web3.js, ethers.js, web3.py etc.) or SDK. All that is required is to understand the schema of a derivative in the Opium Protocol.

The core structure of a derivative product built on Opium needs to implement the following schema:

* **`uint256 margin`**

The reference collateral requirement of the given derivative product

* **`uint256 endTime`**

The expiry date of the given derivative product -  namely the date after which the parties involved in the product life-cycle will be allowed to call its execution and settlement

* **`uint256[] params`**

An array of arbitrary parameters, the first of which is the strike price of the derivative product

* **`address oracleId`**

The address of the account - either EOA (externally owned account) or contract account- that will be responsible to provide the data necessary for the settlement of the derivative

* **`address token`**

The ERC20 token to be used as a margin for the product.

* **`address syntheticId`**

The address of the derivative recipe.

The specifications encoded in a derivative structure are then packed and hashed to generate a footprint of a financial product which can be used within the Opium Protocol for the creation and execution of new positions.\


Once a derivative has been created, a derivative author must ensure that the selected oracle will provide the Opium Protocol with the required data within a specific time window (currently two weeks) after its maturity. Failing to do so will invalidate the derivative and will result in all the allocated capital being returned to the respective owners.\


Finally, if the third step has been performed successfully, the derivative’s positions can be executed. A position can be executed either by its owner or by a third-party if the respective position’s owner has enabled such a feature. A position owner can be either an EOA - externally owned account- or a contract account.\


And that’s it!

As you can see, since it’s possible to rely on ready-to-use third-party oracles and a derivative can be executed by its respective owners - hence, it doesn’t require a derivative’s author to take care of its programmatic execution-, the only step that is actually fundamental is to have a proper understanding of the financial instruments’ data schema adopted by the Opium Protocol - as described in the second step.

As a result, the creation of financial instruments on Opium is, by design, accessible to developers and non-developers, alike - but, at the same time, it allows for a high degree of customization for more development-intensive use-cases.\
****
