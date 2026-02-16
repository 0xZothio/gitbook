# Oracle and Attestation Security

#### <mark style="color:$info;">Decentralized Attestation Network</mark>

USDZe's value depends critically on accurate NAV reporting from the decentralized attestation network. To ensure oracle integrity, the protocol implements multiple security layers around the attestation process:

Each zTOKEN vault has a designated fund administrator who serves as the primary attestor, independently calculating and verifying vault NAV based on direct access to portfolio positions and pricing sources. These fund administrators are regulated entities subject to industry oversight and professional standards, importing traditional fund industry accountability mechanisms into the blockchain environment.

In addition to vault-specific administrators, an independent attestor provides secondary verification of NAV calculations, creating redundancy and reducing single-point-of-failure risks in price reporting. This multi-attestor model requires consensus before NAV updates are accepted on-chain, preventing unilateral manipulation or error propagation.

Attestor Liability and Governance Oversight

Attestors bear direct financial liability for losses resulting from incorrect NAV reporting. This economic accountability creates powerful incentives for diligent verification and conservative reporting practices. In cases where attestation errors cause user losses, affected attestors are contractually obligated to compensate users, with recourse mechanisms built into attestor service agreements.

Beyond direct attestor liability, ZOTH token holders retain governance rights to challenge NAV attestations they believe to be inaccurate. This community oversight layer adds a third verification mechanism, enabling distributed stakeholders to identify and contest suspicious attestations before they impact users. Successful governance challenges can trigger attestor penalties and forced NAV corrections, creating accountability beyond bilateral contractual relationships.

#### <mark style="color:$info;">Fallback Mechanisms and Tolerance Bounds</mark>

NAV updates can only be submitted through authorized off-chain calls by fund administrators or the Zoth entity, with multiple validation checks preventing unauthorized oracle manipulation. The system implements tolerance bounds that define acceptable ranges for NAV updates based on historical volatility and expected return distributions. Updates falling outside tolerance bounds are automatically flagged for manual review before acceptance.

In scenarios where fund administrators cannot provide timely attestations due to operational issues, market disruptions, or technical failures, the Zoth entity maintains independently calculated NAV data that can serve as a fallback pricing source. This backup mechanism ensures that oracle functionality continues even during attestor outages, preventing protocol disruption from temporary attestation failures.

The biweekly attestation cadence balances the need for current pricing with operational efficiency and cost management. However, in periods of extreme market volatility or when vault positions experience rapid value changes, attestation frequency can be increased to ensure that on-chain prices remain synchronized with underlying asset values.
