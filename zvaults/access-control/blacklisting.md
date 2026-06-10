# Blacklisting

### Why a zVault Implements Blacklisting

The blacklist is the protocol-controlled blocklist that extends protection beyond the automated sanctions gate. The sanctions oracle only covers OFAC-sanctioned addresses, a narrow set; it does not flag wallets for risk exposure such as mixer interactions, darknet-market association, or links to high-risk venues, and it cannot act on a wallet that has been compromised. Blacklisting lets the protocol restrict a specific address from interacting with the vault, which protects the remaining holders, maintains the vault's AML and sanctions posture, and prevents a flagged actor from continuing to transact. Because the check also runs on token transfers, a flagged wallet cannot move its tokens to a clean address to escape the restriction.

### When an Address Is Blacklisted

Blacklisting is a deliberate, manually executed action, distinct from the automated sanctions gate. The intended triggers are addresses the sanctions oracle does not catch but that present unacceptable risk:

| Trigger category                | Example                                                       |
| ------------------------------- | ------------------------------------------------------------- |
| High-risk counterparty exposure | Significant flow to or from sanctioned or high-risk exchanges |
| Illicit-source association      | Mixer or tumbler interactions, darknet-market links           |
| Compromise or malicious use     | A wallet known to be compromised or acting against the vault  |
| Legal or regulatory order       | An address subject to a court or regulatory directive         |

The precise risk thresholds that move an address from flagged to blacklisted, the role authorized to execute it, and the review and appeal process are governed by a screening policy that is being finalized. Until that policy is set, the blacklist trigger is not yet codified, and this is a known open item rather than a shipped rule.

### What Happens When an Address Is Blacklisted

A blacklisted address fails the blacklist gate, so any operation it attempts reverts before executing. It cannot deposit, cannot redeem through any path, and cannot transfer its tokens. The tokens are not seized: they remain in the wallet but are frozen from movement for as long as the address holds blacklisted status. The restriction is on the address, not the vault, so all other holders continue to transact normally.

### Redemption While Blacklisted

Because the blacklist gate reverts every standard operation, a blacklisted address has no self-service, on-chain route to redeem. It cannot even submit a redemption request, because the request call itself runs the compliance check and reverts.

Recovery, where permitted, is handled off-chain and case by case, not by the contract. Two cases separate cleanly. For a genuine sanctions match, funds cannot be returned, because doing so would itself breach sanctions law, and the freeze stands. For a risk-based blacklist, particularly a wrongly flagged legitimate user, the path back is a manual review; on a satisfactory outcome the address is removed from the blacklist by the authorized operator, after which the standard redemption flow becomes available again, or the team processes an administered redemption to the verified user. The review and appeal mechanics are part of the screening policy still being finalized.
