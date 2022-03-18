# TokenSpender

It is the ‘asset manager’ of the Opium Protocol. Its core responsibility is to manage the transfer of ERC20 and `ERC721O` tokens.&#x20;

Its only consumer contract in the Opium Protocol is the Core contract, which makes use of the `TokenSpender` for actions such as receiving the required margin (collateral) from a user upon a financial product’s creation and transferring the said margin upon a financial product’s execution according to the payout and the outcome fetched at expiry from the `OracleAggregator`.

### Contract functions description

**`claimTokens(IERC20 token, address from, address to, uint256 amount) external onlyWhitelisted`**

As an argument it takes an ERC20 address, the address of the sender from, the address of the recipient to and the `uint256 amount` to be managed. Its main responsibility is to transfer the money from the sender to the recipient with the specified quantity. The function’s usage is restricted by the modifier `onlyWhitelisted`, which allows only a set of whitelisted contracts to call a function to which it is applied. The whitelist of the allowed contracts is managed by the Opium Protocol’s governance contracts.

**`claimPositions(IERC721O token, address from, address to, uint256 tokenId, uint256 amount) onlyWhitelisted`**

As an argument it takes an `ERC721O` address, the address of the sender from, the address of the recipient to and the uint256 amount to be managed. Its main responsibility is to transfer the money from the sender to the recipient with the specified quantity. The function’s usage is restricted by the modifier `onlyWhitelisted`, which allows only a set of whitelisted contracts to call a function to which it is applied. The whitelist of the allowed contracts is managed by the Opium Protocol’s governance contracts.
