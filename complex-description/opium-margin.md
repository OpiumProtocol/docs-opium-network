# Opium margin

To create a derivative contract, participants need to provide collateral \(margin\) that will be used to pay the counterparty if a position is liable. Within this margin, the position payout is guaranteed for the counterparty. In general, the maximum amount of profit to be earned is known for both counterparties. Depending on how derivative recipes are structured, insurance products can be connected to guarantee payouts above the placed margins by counterparties.

{% hint style="info" %}
In the Opium protocol we define margin as any ERC-20 token. 
{% endhint %}

Users can choose their desired token as a margin and create the corresponding contract. Specifications of the derivative contract include the type and amount of margin token, so participants can assess the risks connected to this contract and know what is the maximum delivery of which amount of tokens. As an example, USDT and DAI are both stable coins pegged to the US Dollar but carry inherently different risks. The Opium Protocol is unbiased towards the usage of margin tokens. Users can choose themselves which tokens they use as collateral.

![Any ERC-20 token can be used as collateral](../.gitbook/assets/image%20%282%29.png)



  


   

