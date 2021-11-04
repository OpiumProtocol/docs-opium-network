# Opium swaps (TMtm)

In financial markets, traders often combine orders to take or reduce exposure in multiple positions at the same time. This was our motivation for designing the TMtm mechanism. It enables a variety of operations such as buying, selling, swapping and creating spreads in simple, but also complex ways.

The swap function executes TMtm-swaps:

{% hint style="info" %}
_**TMtm swap:**_** **user requests to provide {T amount of Opium Tokens + M amount of ERC-20 margin} in exchange for {T amount of Opium Tokens + M amount of ERC-20 margin}
{% endhint %}

With this standard protocol request, it is possible to sell, buy and exchange tokens or spreads. For example:&#x20;

> {4xFuture, 0, 0, 6xUSDT} is a sell order of 4 Futures for 6 USDT Tokens.
>
> {0, 5xDAI, 10xOptions, 0} is a buy order of 10 Options for 5 DAI  Tokens.
>
> {4xFuture, 6xUSDT, 10xOptions, 0} is a combined sell order for \[10 Options - 4 Futures] spread with a price to pay of 6 USDT coins.
>
> {4xFutureA, 0, 8xFutureB, 0} is a buy order of 8 FutureB with paying of 4 FutureA
>
> {1xPortfolio, 0, 0, 1200xDAI} is a sell order of user Portfolio for 1200 DAI coins

Orders are signed by the user and allow the Opium Network to withdraw funds needed to execute the order. &#x20;
