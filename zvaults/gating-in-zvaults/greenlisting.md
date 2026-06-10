# Greenlisting

Greenlisting is a per-vault access toggle. With the greenlist off, the gate is skipped entirely and any wallet can transact, so the vault operates permissionlessly. With it on, only addresses holding greenlisted status can deposit or redeem, and every other wallet's operation reverts. The same contracts support both modes through a single setting, so a vault's access posture follows its strategy rather than being hardcoded.

This is an address allowlist, not identity verification. Greenlisting records which wallet addresses may transact with a vault; it does not require or imply KYC. A vault can run fully permissionless with the greenlist disabled, which is the intended posture for open retail vaults, or run with it enabled where a specific strategy or jurisdiction requires participation to be limited to a known set of addresses, such as during a controlled beta or for a restricted institutional vault.

Greenlisted status is granted and revoked by a dedicated screening operator, held in a separate wallet from the protocol's admin and price-update authorities so that access decisions cannot be made from a single concentrated key.
