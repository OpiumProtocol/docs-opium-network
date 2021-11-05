# OracleAggregator

**`ERROR_ORACLE_AGGREGATOR_DATA_DOESNT_EXIST`**

The exception is triggered when the OracleAggregator `getData` function is called and the requested data for a given oracleId and timestamp has not yet been cached.

**`ERROR_ORACLE_AGGREGATOR_DATA_ALREADY_EXIST`**

The exception is triggered when an OracleId tries to push data twice with the same timestamp to the OracleAggregator - which would result in overriding the previously cached result.

**`ERROR_ORACLE_AGGREGATOR_NOT_ENOUGH_ETHER`**

deprecated

**`ERROR_ORACLE_AGGREGATOR_QUERY_WAS_ALREADY_MADE`**

deprecated
