# SyntheticId examples

The financial logic of a product built on top of the Opium Protocol is encoded in a SyntheticId.



A SyntheticId must inherit the IDerivativeLogic interface as the Opium Protocol SyntheticAggregator expects to call some of the functions defined in the IDerivativeLogic contract throughout the lifecycle of the derivative. Specifically, these core functions are:

* validateInput
* getMargin
* getExecutionPayout
* getAuthorAddress
* getAuthorCommission
* thirdPartyExecutionAllowed
* allowThirdPartyExecution\


The core function of a SyntheticId is the getExecutionPayout. It allows a SyntheticId author to describe the payout logic of their financial product. Hence, whether a financial product is a traditional call option or put option, a CDO or some more exotic derivative, that’s the function where the logic needs to be encoded.

The following is an example of a getExecutionPayout implementation for a CALL option:

```
function getExecutionPayout(Derivative memory _derivative, uint256 _result)
        public
        view
        returns (uint256 buyerPayout, uint256 sellerPayout)
    {
        uint256 ppt;

        uint256 strikePrice = _derivative.params[0];

        if (_derivative.params.length == 2) {
            ppt = _derivative.params[1];
        } else {
            ppt = BASE_PPT;
        }

        if (_result > strikePrice) {
            uint256 profit = _result.sub(strikePrice);
            profit = profit.mul(ppt).div(BASE_PPT);

            if (profit < _derivative.margin) {
                buyerPayout = profit;
                sellerPayout = _derivative.margin.sub(profit);
            } else {
                buyerPayout = _derivative.margin;
                sellerPayout = 0;
            }
        } else {
            buyerPayout = 0;
            sellerPayout = _derivative.margin;
        }
    }
```

In the above example, in case the option is in the money and its intrinsic value is greater than the allocated margin, then the difference between the underlying's market price and the strike price represents the buyer's profit and the seller's loss. However, if the option is in the money and the profit is greater than the allocated collateral, then the buyer's profit is equal to the entire margin.

Conversely, the following is an example of a PUT option:

```
function getExecutionPayout(LibDerivative.Derivative memory _derivative, uint256 _result)
        public
        view
        override
        returns (uint256 buyerPayout, uint256 sellerPayout)
    {
        uint256 ppt;

        uint256 strikePrice = _derivative.params[0];

        if (_derivative.params.length == 2) {
            ppt = _derivative.params[1];
        } else {
            ppt = BASE_PPT;
        }

        if (_result < strikePrice) {
            uint256 profit = strikePrice.sub(_result);
            profit = profit.mul(ppt).div(BASE_PPT);

            if (profit < _derivative.margin) {
                buyerPayout = profit;
                sellerPayout = _derivative.margin.sub(profit);
            } else {
                buyerPayout = _derivative.margin;
                sellerPayout = 0;
            }
        } else {
            buyerPayout = 0;
            sellerPayout = _derivative.margin;
        }
    }
```
