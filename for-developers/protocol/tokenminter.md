# TokenMinter

Its main responsibility is to perform actions on tokens representing the **LONG** and **SHORT** positions of a financial product.&#x20;

As the Opium Protocol makes use of its own token standard `ERC721O`, the `TokenMinter` exposes a set of functions to work with it.&#x20;

Its main consumer in the Opium Protocol is the Core contract, which makes use of the `TokenMinter` to mint **LONG**/**SHORT** positions upon the creation of a new financial product and burn them after the successful execution of the said financial product.&#x20;

### Contract functions description



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
