# Core

It is the main contract of the Opium Protocol. It exposes most of the user-facing functions that a user or a contract need to use in order to interact with the Opium Protocol, such as the creation of new financial products or their executions. &#x20;

The Core contract is responsible for processing the data encoded in a derivative recipe and for fetching the data from a specified oracle recipe for the purpose of calculating payouts, validating a financial product’s specs.

### Contract functions description

**`create(Derivative memory _derivative, uint256 _quantity, address[2] memory _addresses) public`**

If the derivative recipe is valid and the `msg.sender` calling core.create is providing a collateral allowance that matches the margin requirements specified in the derivative recipe, it transfers the collateral from the user via the `TokenSpender` contract and subsequently it mints a **LONG** and a **SHORT** `ERC721O` tokens for the given derivative recipe via the `TokenMinter` and transfers them respectively to the specified buyer and seller. As an argument it accepts `LibDerivative.derivative,` `uint256` quantity as the number of positions that the `TokenMinter` shall mint and a tuple of addresses - respectively the buyer and the seller- that shall be the recipients of the minted positions.

**`execute(uint256 _tokenId, uint256 _quantity, Derivative memory _derivative)`**

`msg.sender` executes a single derivative position type with a specified quantity. The position type being executed is represented by its unique `ERC721O` `tokenId`. Internally the function performs the required validation - such as checking whether the derivative associated to the `tokenId` is expired, the `OracleAggregator` has already provided the necessary data to settle the derivative and `msg.sender` is allowed to execute the given position. If all the validations are passed successfully, then it checks whether the provided `tokenId` belongs to a **LONG** or **SHORT** position and then proceeds to computing the payout logic according to the specifications encoded in the derivative recipe - specifically the `getExecutionPayout` specified in `IDerivativeLogic`- and the outcome cached in the OracleAggregator from the given derivative’s oracle recipe. After calculating the buyer’s and seller’s payouts, it finally forwards the payout to the winning party and,  if specified, it calculates the commission of the derivative’s author. As an argument it accepts the `uint256` `_tokenId` unique `tokenId` of the position to be executed, `uint256` \_quantity the number of positions to be executed, and `LibDerivative.Derivative` the derivative recipe associated with the given `tokenId`.

**`execute(uint256[] _tokenId, uint256[] _quantity, Derivative[] memory _derivative)`**

`msg.sender` executes a batch of derivatives’ positions with a specified quantity. The high-level logic introduced for `execute(uint256 _tokenId, uint256 _quantity, Derivative memory _derivative)` is applied to each provided position by looping through their array.&#x20;

**`execute(address _tokenOwner, uint256 _tokenId, uint256 _quantity, Derivative memory _derivative)`**

`msg.sender` executes a single derivative’s position type on behalf of `_tokenOwner`. An additional check is required in cases where a third-party requests the execution of a derivative’s position type owned by another account. Internally it checks whether the derivative recipe contract implementing the `IDerivativeLogic` interface allows the execution from third-parties by calling the `IDerivativeLogic` function `thirdPartyExecutionAllowed`, which returns a boolean. If true, the remaining high-level logic is identical to `execute(uint256 _tokenId, uint256 _quantity, Derivative memory _derivative)`

**`execute(address _tokenOwner, uint256[] memory  _tokenId, uint256[] memory _quantity, Derivative[] memory _derivative)`**

`msg.sender` executes a batch of derivatives’ positions on behalf of `_tokenOwner`. The logic being performed on each position is identical to `execute(address _tokenOwner, uint256 _tokenId, uint256 _quantity, Derivative memory _derivative)`but applied on each element of the supplied arrays.

**`cancel(uint256 _tokenId, uint256 _quantity, Derivative memory _derivative)`**

It allows the cancellation of the execution of a derivative if no data was provided to perform its settlement after 2 weeks from its maturity. If the execution is canceled, then all the allocated margins are returned to the respective position's owners. More importantly, once a position is canceled, it won’t be possible to execute it even if the oracle data will finally arrive at a later time.

**`cancel(uint256[] memory _tokenId, uint256[] memory _quantity, Derivative[] memory _derivative)`**

It allows the cancellation of a batch of derivatives if no data was provided to perform their settlement after 2 weeks for each of their maturity. The logic is identical to `cancel(uint256 _tokenId, uint256 _quantity, Derivative memory _derivative)` but it is applied to each of the derivatives’ positions array in a loop.

**`withdrawFee(address _tokenAddress) public`**

Allows the author of a derivative to withdraw the fees that were specified in the related derivative recipe as a commission for the author of said financial product. As an address it accepts the ERC20 address of the token with which the derivative author will be compensated - generally it is the ERC20 token used as a margin for the derivative itself.
