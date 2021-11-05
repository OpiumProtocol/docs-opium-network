# Core

**`ERROR_CORE_TICKER_WAS_CANCELLED`**

The error is triggered when an account tries to either create or execute a previously canceled derivative.

**`ERROR_CORE_SYNTHETIC_VALIDATION_ERROR`**

The error is triggered at the moment of a derivative’s positions creation if the provided LibDerivative.Derivative schema includes invalid parameters

**`ERROR_CORE_NOT_ENOUGH_TOKEN_ALLOWANCE`**

The error is triggered when an account tries to create a derivative’s positions without providing an amount of margin that matches the amount of collateral specified in the derivative recipe.

**`ERROR_CORE_TOKEN_IDS_AND_QUANTITIES_LENGTH_DOES_NOT_MATCH`**

The error is triggered when an account tries to either execute or cancel an array of positions represented by their tokenIds but provides a mismatching array of quantities - as every element in the array of quantities is the amount of positions that the account wishes to execute or cancel

**`ERROR_CORE_TOKEN_IDS_AND_DERIVATIVES_LENGTH_DOES_NOT_MATCH`**

The error is triggered when an account tries to either execute or cancel an array of positions represented by their tokenIds but provides a mismatching array of derivatives - as every element in the array of tokenIds is associated to a derivative in the array of derivatives

**`ERROR_CORE_EXECUTION_BEFORE_MATURITY_NOT_ALLOWED`**

The error is triggered when an account tries to execute a derivative before its maturity as specified in the endTime field of the derivative structure

**`ERROR_CORE_SYNTHETIC_EXECUTION_WAS_NOT_ALLOWED`**

The error is triggered when an account tries to execute a derivative that does not enable third-party execution without being its creator&#x20;

**`ERROR_CORE_CANCELLATION_IS_NOT_ALLOWED`**

The error is triggered when an account tries to cancel a derivative sooner than two weeks since its maturity in case no data was provided to the OracleAggregator

**`ERROR_CORE_UNKNOWN_POSITION_TYPE`**

The error is triggered in case the provided tokenId is not recognized by the Opium protocol\
