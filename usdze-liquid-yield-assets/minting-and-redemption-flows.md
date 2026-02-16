# Minting & Redemption Flows

### Minting Process

Users can mint USDZe at any time without restriction or delay. Upon deposit of accepted collateral (typically stablecoins), the allocator contract automatically distributes the incoming capital to appropriate vaults according to current governance-approved allocation weights. This automated distribution ensures that new deposits immediately begin generating yield and that the protocol's overall allocation remains consistent with established risk parameters.

The minting process occurs on-chain in a single transaction, with users receiving USDZe tokens that immediately begin accruing value based on the aggregate performance of underlying vaults. There are no minimum deposit requirements, lock-up periods, or minting fees beyond standard blockchain transaction costs.

### Redemption Process

USDZe redemptions operate through a two-tier system designed to balance immediate liquidity with capital efficiency. Under normal operating conditions, users can redeem USDZe at any time, receiving stablecoins from the liquidity buffer in atomic transactions. This instant redemption capability ensures that USDZe maintains functional parity with traditional stablecoins during routine operations.

When redemption requests exceed available liquidity buffer capacity, the protocol automatically transitions to queue-based processing. Redemption requests are placed in a FIFO queue and submitted to relevant fund managers, who are obligated to provide liquidity within a T+2 (two business day) settlement window. The protocol does not impose per-user withdrawal limits during queue periods, ensuring that users maintain unrestricted access to their capital subject only to the orderly processing timeframe.

Fund managers bear contractual liability for meeting T+2 settlement obligations. Failure to provide committed liquidity within the specified timeframe exposes fund managers to potential penalties and governance actions, creating strong incentives for maintaining appropriate liquidity levels and risk management practices.

The redemption value of USDZe is determined by oracle-reported vault NAVs, updated biweekly, ensuring that users receive fair value reflecting the current aggregate value of underlying positions. Yield accrues through appreciation of USDZe's value rather than through rebasing or separate claim mechanisms, meaning that yield is automatically compounded into the token's redemption value based on attestor-verified vault performance.

<figure><img src="../.gitbook/assets/Instant deposit and redemption flow.png" alt=""><figcaption></figcaption></figure>
