# TokenMinter

Its main responsibility is to perform actions on tokens representing the **LONG** and **SHORT** positions of a financial product.&#x20;

As the Opium Protocol makes use of its own token standard `ERC721O`, the `TokenMinter` exposes a set of functions to work with it.&#x20;

Its main consumer in the Opium Protocol is the Core contract, which makes use of the `TokenMinter` to mint **LONG**/**SHORT** positions upon the creation of a new financial product and burn them after the successful execution of the said financial product.&#x20;
