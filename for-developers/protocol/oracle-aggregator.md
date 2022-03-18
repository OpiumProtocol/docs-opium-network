# OracleAggregator

It is the data layer of the Opium Protocol.

&#x20;The OracleAggregator is the contract responsible for providing the necessary data to settle a financial product in the Opium Protocol.&#x20;

It does not implement any specific oracle logic as it is designed to be more oracle-agnostic. This grants developers the freedom to choose the data source of their application - be it any oracle of their choosing or an off-chain API.

### Contract functions description

**`__callback(uint256 timestamp, uint256 data) public`**

The main OracleAggregator function that users and consumer contracts will use the most. It receives and caches the data from msg.sender based on the oracleId address and the provided timestamp - be it an oracle or an off-chain data source- so that it can be provided to the Core contract for the settlement of its related financial product. It takes as an argument the address of the oracle recipe’s oracleId and the uint256 timestamp

**`getData(address oracleId, uint256 timestamp) public view returns(uint256 dataResult)`**

If present, it returns the cached data associated with a given oracleId and timestamp. t takes as an argument the address of the oracle recipe’s oracleId and the uint256 timestamp

**`hasData(address oracleId, uint256 timestamp) public view returns(bool result)`**

It checks whether the OracleAggregator has already been provided with data for a given address oracleId and uint256 timestamp key pair

**`calculateFetchPrice(address oracleId) public returns(uint256 fetchPrice)`**

deprecated

**`registerQuery(address oracleId, uint256 timestamp)`**

deprecated

**`fetchData(address oracleId, uint256 timestamp) public`**

deprecated

**`recursivelyFetchData(address oracleId, uint256 timestamp, uint256 period, uint256 times) public`**

deprecated
