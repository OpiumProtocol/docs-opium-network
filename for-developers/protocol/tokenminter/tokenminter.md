---
description: Methods overview
---

# TokenMinter



**`mint(address _buyer, address _seller, bytes32 _derivativeHash, uint256 _quantity) external`**

Wrapper around `ERC7210BackwardCompatible` `_mint`. It mints **LONG** and **SHORT** `ERC721O` tokens according to the specified quantity respectively to the buyer and the seller. The `tokenId` of the **LONG** and **SHORT** position token is computed based on the provided `_derivativeHash`. The access to the function is restricted by the `onlyCore` modifier which grants its usage only to the `Core` contract.&#x20;

**`mint(address _buyer, bytes32 _derivativeHash, uint256 _quantity)`**

only for pooled

**`burn(address _tokenOwner, uint256 _tokenId, uint256 _quantity) external`**

Wrapper around ERC7210BackwardCompatible `_burn`. It burns a specified `tokenId` position on behalf of a `_tokenOwner`. The access to the function is restricted by the `onlyCore` modifier which grants its usage only to the `Core` contract.&#x20;

**`name() external view returns(string memory)`**

It returns a common name for all the position tokens.

**`symbol() external external view returns(string memory)`**

It returns a common symbol for all the position tokens.

**`isApprovedOrOwner(address _spender, address _owner, uint256 _tokenId) public view returns(bool)`**

**`isOpiumSpender(address _spender) public view returns(bool)`**
