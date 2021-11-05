---
description: Methods overview
---

# TokenSpender

**`claimTokens(IERC20 token, address from, address to, uint256 amount) external onlyWhitelisted`**

As an argument it takes an ERC20 address, the address of the sender from, the address of the recipient to and the `uint256 amount` to be managed. Its main responsibility is to transfer the money from the sender to the recipient with the specified quantity. The function’s usage is restricted by the modifier `onlyWhitelisted`, which allows only a set of whitelisted contracts to call a function to which it is applied. The whitelist of the allowed contracts is managed by the Opium Protocol’s governance contracts.

**`claimPositions(IERC721O token, address from, address to, uint256 tokenId, uint256 amount) onlyWhitelisted`**

As an argument it takes an `ERC721O` address, the address of the sender from, the address of the recipient to and the uint256 amount to be managed. Its main responsibility is to transfer the money from the sender to the recipient with the specified quantity. The function’s usage is restricted by the modifier `onlyWhitelisted`, which allows only a set of whitelisted contracts to call a function to which it is applied. The whitelist of the allowed contracts is managed by the Opium Protocol’s governance contracts.
