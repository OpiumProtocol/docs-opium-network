# TokenSpender

It is the ‘asset manager’ of the Opium Protocol. Its core responsibility is to manage the transfer of ERC20 and `ERC721O` tokens.&#x20;

Its only consumer contract in the Opium Protocol is the Core contract, which makes use of the `TokenSpender` for actions such as receiving the required margin (collateral) from a user upon a financial product’s creation and transferring the said margin upon a financial product’s execution according to the payout and the outcome fetched at expiry from the `OracleAggregator`.
