# Architecture of zVaults

A zVault is a layered smart-contract system, not a single contract. Responsibilities are split across distinct contracts so that each does one job and the boundaries between them are auditable. The architecture is deployment-agnostic: every vault launched on the protocol reuses the same contract set, regardless of its underlying strategy. The design separates what must stay open and transparent (the token, the price feed) from what must stay tightly controlled (role administration, upgrades, custody authority).
