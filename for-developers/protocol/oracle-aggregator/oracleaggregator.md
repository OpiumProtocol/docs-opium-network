---
description: Methods overview
---

# OracleAggregator

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
