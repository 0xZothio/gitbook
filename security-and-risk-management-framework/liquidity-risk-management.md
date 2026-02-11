# Liquidity Risk Management

#### Multi-Tier Liquidity Architecture&#x20;

ZEUSD and individual zTOKEN vaults implement sophisticated liquidity management frameworks designed to accommodate both routine redemptions and stress scenarios without forcing destabilizing liquidations or creating unfair treatment among users.

Each vault maintains a recommended liquidity buffer of approximately 10% of assets under management held in liquid stablecoins. This buffer enables instant atomic redemptions for typical withdrawal requests without requiring fund managers to liquidate deployed positions. Buffer sizing reflects the specific liquidity profile of each vault's strategy, with more liquid DeFi strategies potentially maintaining smaller buffers and less-liquid RWA strategies holding larger reserves.

At the ZEUSD protocol level, an additional liquidity buffer provides a second layer of redemption capacity. This ZEUSD-level buffer allows users to withdraw even when individual underlying zTOKEN vaults have depleted their own liquidity reserves, creating system-wide resilience against correlated redemption demand across multiple vaults.

#### Queue-Based Stress Management

When redemption requests exceed available liquidity buffer capacity, the protocol automatically transitions to first-in-first-out (FIFO) queue-based processing. This orderly withdrawal mechanism prevents bank-run dynamics where sophisticated actors gain advantage through faster transaction execution or larger gas payments.

An automated bot sequentially processes queued redemption requests as fund managers provide liquidity in response to withdrawal notices. The queue system maintains fairness and transparency throughout stress periods, with users able to monitor their queue position and expected settlement timing through protocol interfaces.

Fund managers face contractual obligations to provide requested liquidity within T+2 (for ZEUSD) or T+3 (for direct zTOKEN vault redemptions) settlement windows. These timeframes align with traditional financial market conventions while providing sufficient time for orderly position unwinding without fire-sale execution. Managers who repeatedly fail to meet settlement obligations face penalties and potential removal from the protocol through governance action.<br>

#### Real-Time Monitoring and Indexing

Zoth indexes all on-chain activity and maintains real-time subgraph infrastructure that provides continuous visibility into liquidity positions, withdrawal queue status, buffer depletion rates, and aggregate redemption demand. This monitoring infrastructure enables proactive liquidity management, allowing fund managers and protocol operators to identify developing liquidity stress before buffers are fully depleted.

The real-time indexing also powers user-facing dashboards that display current liquidity availability, estimated redemption timing, and queue positions, creating transparency that helps users make informed decisions during periods of elevated withdrawal activity.
