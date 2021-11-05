# OracleId examples

As the Opium Protocol OracleAggregator is designed to be data source agnostic, it is up to the developer to implement what kind of on-chain or off-chain mechanism is the most suitable to their application.



As it was explained in the previous chapter, in the Opium protocol a financial instrument is defined by two separate entities:

* Derivative recipe
* Oracle recipe

For the purpose of sharing a common vocabulary, we refer to the contract entity implementing the oracle recipe as OracleId.&#x20;

In fact, the OracleAggregator itself uses the same terminology. In the OracleAggregator we have a nested mapping that maps the address of an OracleId to a mapping that maps the timestamp when the OracleId provided data to the OracleAggregator to the numerical value provided.

The OracleId’s value is therefore cached and made available to the Opium Protocol Core contract for the execution of the related derivative’s positions (see below):(.

```
mapping(address => mapping(uint256 => uint256)) private dataCache;
```



A possible pattern for the development of OracleIds is to split their logic in an OracleId and an OracleSubId. This allows to reason more clearly on the oracle logic and enforce a better separation of concerns and [single responsibility principle](https://en.wikipedia.org/wiki/Single-responsibility\_principle).

The OracleId is responsible for pushing data into the OracleAggregator contract by calling the OracleAggregator callback function and the OracleSubId is responsible for implementing the oracle-specific logic. The OracleSubId logic can be implemented using Chainlink, UMA etc..

As the most popular oracle solution in the Ethereum space thus far is Chainlink, in the following example we showcase how to implement the OracleId/OracleSubId pattern:

```
interface IChainlinkOracle {
    function getLatestPrice() external returns(int);
}

contract OracleIdar is IOracleId, Ownable {
    IOracleAggregator oracleAggregator;
    uint256 public result;

    constructor(address _registry) public {
        IRegistry registry = IRegistry(_registry);
        oracleAggregator = IOracleAggregator(registry.getOracleAggregator());
    }
    /// @notice Wrapper around Opium oracleAggregator.__callback to push the data related to the underlying's market price
    /// @param _oracleSubId address of the oracleSubId - the data source whose result is being pushed into the OracleAggregator
    /// @param _timestamp uint256 unix timestamp of when the data is being pushed
    function __callback(address _oracleSubId, uint256 _timestamp) external onlyOwner {
        require(
            !oracleAggregator.hasData(address(this), _timestamp) && _timestamp < now,
            "Only when no data and after timestamp allowed"
        );
        uint256 data = uint256(IChainlinkOracle(_oracleSubId).getLatestPrice());
        result = data;

        oracleAggregator.__callback(_timestamp, result);
    }

    function fetchData(uint256 timestamp) external payable {}

    function recursivelyFetchData(
        uint256 timestamp,
        uint256 period,
        uint256 times
    ) external payable {}

    function calculateFetchPrice() external returns (uint256 fetchPrice) {}
}
```

In the above code snippet, the contract implements the OracleId interface. In the OracleId \_\_callback function, the contract fetches the required data from the OracleSubId and provides it to the OracleAggregator.

The OracleSubId is a basic implementation of a Chainlink pricefeed:

```
contract OracleSubId {
    AggregatorV3Interface internal priceFeed;

    /**
        AAVE/ETH price feed (8 decimals)
     */
    constructor() public {
        priceFeed = AggregatorV3Interface(0x6Df09E975c830ECae5bd4eD9d90f3A95a4f88012);
    }

    function getLatestPrice() public view returns(int) {
        (
            uint80 roundId,
            int price,
            uint startedAt,
            uint timeStamp,
            uint80 answeredInRound
        ) = priceFeed.latestRoundData();
        return price;
    }

}
```
