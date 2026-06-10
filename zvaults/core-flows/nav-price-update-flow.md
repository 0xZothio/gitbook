# NAV Price Update Flow

A `zTOKEN` is priced against the vault NAV, which is refreshed on a fixed cadence by a dedicated update multisig. The figure is sourced one of two ways: off-chain from the vault's strategy or fund administrator, or on-chain from an independently verified oracle service. Each submission is then gated by the tolerance and staleness bounds described under Price Manipulation Protection, so deposits and redemptions never execute against an outdated or manipulated NAV. The result is a price holders can verify on-chain rather than take on trust.
