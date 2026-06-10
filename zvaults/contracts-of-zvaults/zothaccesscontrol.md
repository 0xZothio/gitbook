# ZothAccessControl

Central role store for the entire protocol. All other contracts call `hasRole()` against this contract. A role granted here is immediately effective in every contract without redeployment.

| Function                              | Access        | Description                                                                                    |
| ------------------------------------- | ------------- | ---------------------------------------------------------------------------------------------- |
| `initialize()`                        | Once (deploy) | Sets up initial roles for the deployer. Must be called exactly once via the proxy initializer. |
| `grantRole(role, account)`            | Role admin    | Assign a role to an address.                                                                   |
| `revokeRole(role, account)`           | Role admin    | Remove a role from an address.                                                                 |
| `grantRoleMult(roles[], accounts[])`  | Role admin    | Bulk role assignment. Useful during deployment setup.                                          |
| `revokeRoleMult(roles[], accounts[])` | Role admin    | Bulk role removal. Used to decommission the deployer key.                                      |
| `hasRole(role, account)`              | View (public) | Returns true or false. Called by all other contracts on every guarded action.                  |
