# Oracle and derivative registers

Oracle and derivative recipes should be registered at either their respective Oracle or Derivative register to connect to the Opium Network. Registers store data about the qualities of a recipe and secure the Opium Network against hacks. Once data is supplied to the register, it cannot be changed.

The derivative register stores how much margin was placed at the creation of a contract. The Opium core uses this data to determine payouts when one of the counterparties uses the withdrawal function. Counterparties can never receive more from the contract than initially was put up as collateral. This means that even if a third party derivative recipe is corrupted, it will never be able to steal money from the system. In this way, it is guaranteed that there is always enough margin in the system for all the outstanding positions in the Opium Network.  
  
The oracle register stores all the data, supplied by oracle recipes, that was ever requested by the system. In this way, data only has to be transferred once to the blockchain and all other contracts using the same data can use this without paying fees for transferring the data to the blockchain.  
  
This means that if after maturity one contract is executed, all the other contracts with the same specifics are technically also matured. Users just have to withdraw their part of the margin by using the withdrawal function. If after 2 weeks contracts have not been executed, because the oracle recipe was unable to deliver data, both parties can withdraw their initially placed margin from the derivative register.   
  
The oracle register also stores which publicKey queried the data, and before fetching checks if there was enough Ether supplied to finish the fetching function.

![Registers store data and secure the system against hacks.](../.gitbook/assets/image%20%286%29.png)





