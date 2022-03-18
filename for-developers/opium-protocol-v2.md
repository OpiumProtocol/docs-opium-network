# Opium Protocol V2

## Introduction

Opium v2 is a permissionless smart financial escrow protocol that allows its users to create fully customizable financial products. Its primary use-case is the management of derivatives, which are represented as a pair of LONG and SHORT ERC20 Opium position tokens. As a financial engineer, you can easily create a derivative contract with Opium v2 and be rewarded a portion of the reserves accrued by the protocol for each successful settlement of your own financial products. As a seller and buyer, you can partake in (for example) PUT or CALL options on an underlying by holding a specific Opium position token, you can exchange them on an AMM, exercise them at expiry or redeem them for initial margin if you hold an equal amount of LONG and SHORT positions. The focus of the design is to be as lean as possible as to enable the greatest flexibility and interoperability with other financial primitives.

## **Changelog from Opium Protocol v1**

1. Completely removed `pooled derivative` logic
2. Changed `ERC721o` to `ERC20`: `LONG` and `SHORT` position tokens and removed `TokenMinter` contract
3. Removed all Matching contracts, as ERC20 positions are compatible with protocols like `1inch Limit Order Protocol` and `0x`
4. Changed Solidity version to latest with best practices refactoring
5. Changed `create` to support `amounts` instead of `quantities` (fractional derivatives)
6. Separated `create` process into `create` and `mint` to reduce gas costs
7. Changed `execute` to support `amounts` instead of `quantities` (fractional derivatives)
8. Added `redeem` derivatives function to burn `LONG` + `SHORT` in return of `initial margin`
9. Added upgradability
10. Added emergency mechanisms
11. Added governance and roles
12. Performed additional refactoring and optimizations

## Core protocol modules

![](../.gitbook/assets/Brainstorms.jpeg)

{% content-ref url="opium-protocol-v2/core.md" %}
[core.md](opium-protocol-v2/core.md)
{% endcontent-ref %}

{% content-ref url="opium-protocol-v2/registry.md" %}
[registry.md](opium-protocol-v2/registry.md)
{% endcontent-ref %}

{% content-ref url="opium-protocol-v2/syntheticaggregator.md" %}
[syntheticaggregator.md](opium-protocol-v2/syntheticaggregator.md)
{% endcontent-ref %}

{% content-ref url="opium-protocol-v2/oracleaggregator.md" %}
[oracleaggregator.md](opium-protocol-v2/oracleaggregator.md)
{% endcontent-ref %}

{% content-ref url="opium-protocol-v2/opiumproxyfactory.md" %}
[opiumproxyfactory.md](opium-protocol-v2/opiumproxyfactory.md)
{% endcontent-ref %}

{% content-ref url="opium-protocol-v2/opiumpositiontoken.md" %}
[opiumpositiontoken.md](opium-protocol-v2/opiumpositiontoken.md)
{% endcontent-ref %}

## **Derivative author fees and protocol reserves**

### **Execution**

Derivatives authors can set a fee (limited) on the profit that trades make from execution. Part of this fee goes to protocol execution reserves and the rest goes to the derivative author.

Example:

| Name                                       | Value     |
| ------------------------------------------ | --------- |
| _\[input] Execution profit_                | _100 ETH_ |
| _\[input] Derivative author fee_           | _5%_      |
| _\[input] Protocol execution reserve part_ | _10%_     |
| \[output] Total reserve                    | 5 ETH     |
| \[output] Protocol execution reserve       | 0.5 ETH   |
| \[output] Derivative author reserve        | 4.5 ETH   |

### Redemption

| Name                                         | Value      |
| -------------------------------------------- | ---------- |
| _\[input] Initial margin_                    | _1000 ETH_ |
| _\[input] Derivative author redemption part_ | _0.1%_     |
| _\[input] Protocol redemption preserve part_ | _10%_      |
| \[output] Total reserve                      | 1 ETH      |
| \[output] Protocol redemption reserve        | 0.1 ETH    |
| \[output] Derivative author reserve          | 0.9 ETH    |

## Security measures

### Derivative data cache

Since all syntheticId’s (derivative logic contracts) are third party contracts that are being consumed by the protocol, protocol MUST consider them as potentially malicious and act accordingly. This is why all data consumption calls (except derivative parameters validation) are only made once and are stored in cache thereafter.

### P2P Vaults

As an additional security measure there was introduced a so-called “P2P Vault”, which’s only purpose is a bookkeeping of cash flows for each particular derivative (ticker). It’s being increased on every incoming cash flow and deceased on every outcoming cash flow. It’s decreasing by greater value that it counts at the moment will result in transaction’s reverting.

This bookkeeping helps to prevent any potentially (not yet known) malicious derivatives from stealing funds withheld for other derivatives settlement.

## ACL

### Upgradability

All the core contracts of the Opium Protocol are upgradeable. The upgradeability is ensured by the openzeppelin’s “@openzeppelin/contracts-upgradeable” library which uses the unstructured storage proxies pattern and it is assumed that it safely protects from storage clashes between the proxy contract and the implementation contract. However, in order to avoid storage layout collisions between different implementation contract versions we have added a fixed length uint256 array (with 50 as length everywhere except for the OpiumPositionToken) which is assumed that will allow up to 50 storage slots (or 30 storage slots for the OpiumPositionToken) to add new variable/modify the contract without shifting down the storage layout and cause clashes.

### Roles

| Category  | ID | Role                                                  | Description                                                                                                                                                                                                                                                                     |
| --------- | -- | ----------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Setup     | 0  | DEFAULT\_ADMIN                                        | Special role set by default by the OpenZeppelin AccessControl library. It has the highest privilege level and can manage all the other roles (assign a role, revoke a role)                                                                                                     |
| Setup     | 1  | PROTOCOL\_ADDRESSES\_SETTER\_ROLE                     | Role responsible for updating the Opium Protocol core contracts' addresses                                                                                                                                                                                                      |
| Setup     | 5  | NO\_DATA\_CANCELLATION\_PERIOD\_SETTER\_ROLE          | Role responsible for updating the RegistryEntities.ProtocolParametersArgs.noDataCancellationPeriod                                                                                                                                                                              |
| Setup     | 7  | WHITELISTER\_ROLE                                     | Role responsible for managing (adding and removing accounts) the whitelist                                                                                                                                                                                                      |
| Setup     | 10 | REGISTRY\_MANAGER\_ROLE                               | Role responsible for updating the Registry address itself stored in the Opium Protocol core contracts that consume the Registry                                                                                                                                                 |
| Setup     | 18 | CORE\_CONFIGURATION\_UPDATER\_ROLE                    | Role responsible for updating (applying) new core configuration if it was changed in the registry                                                                                                                                                                               |
| Reserve   | 2  | EXECUTION\_RESERVE\_CLAIMER\_ADDRESS\_SETTER\_ROLE    | Role responsible for updating the reserve recipient's address of the profitable execution of derivatives positions                                                                                                                                                              |
| Reserve   | 3  | REDEMPTION\_RESERVE\_CLAIMER\_ADDRESS\_SETTER\_ROLE   | Role responsible for updating the reserve recipient's address of the redemption of market neutral positions                                                                                                                                                                     |
| Reserve   | 4  | EXECUTION\_RESERVE\_PART\_SETTER\_ROLE                | Role responsible for updating the fixed part (percentage) of the derivative author fees that goes to the protocol execution reserve                                                                                                                                             |
| Reserve   | 8  | DERIVATIVE\_AUTHOR\_EXECUTION\_FEE\_CAP\_SETTER\_ROLE | Role responsible for updating the maximum fee that a derivative author can set as a commission originated from the profitable execution of derivatives positions                                                                                                                |
| Reserve   | 9  | REDEMPTION\_RESERVE\_PART\_SETTER\_ROLE               | Role responsible for updating the fixed part (percentage) of the initial margin that will be deducted to the reserves during redemption of market neutral positions. Also sets fixed part (percentage) of this redemption reserves that goes to the protocol redemption reserve |
| Emergency | 6  | GUARDIAN\_ROLE                                        | Role responsible for globally pausing the protocol                                                                                                                                                                                                                              |
| Emergency | 11 | PARTIAL\_CREATE\_PAUSE\_ROLE                          | Role responsible for pausing Core.create                                                                                                                                                                                                                                        |
| Emergency | 12 | PARTIAL\_MINT\_PAUSE\_ROLE                            | Role responsible for pausing Core.mint                                                                                                                                                                                                                                          |
| Emergency | 13 | PARTIAL\_REDEEM\_PAUSE\_ROLE                          | Role responsible for pausing Core.redeem                                                                                                                                                                                                                                        |
| Emergency | 14 | PARTIAL\_EXECUTE\_PAUSE\_ROLE                         | Role responsible for pausing Core.execute                                                                                                                                                                                                                                       |
| Emergency | 15 | PARTIAL\_CANCEL\_PAUSE\_ROLE                          | Role responsible for pausing Core.cancel                                                                                                                                                                                                                                        |
| Emergency | 16 | PARTIAL\_CLAIM\_RESERVE\_PAUSE\_ROLE                  | Role responsible for pausing Core.claimReserve                                                                                                                                                                                                                                  |
| Emergency | 17 | PROTOCOL\_UNPAUSER\_ROLE                              | Role responsible for globally unpausing the protocol                                                                                                                                                                                                                            |

