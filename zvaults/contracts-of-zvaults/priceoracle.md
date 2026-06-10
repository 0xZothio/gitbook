# PriceOracle

Stores and validates the current NAV price for the `zTOKEN`. Non-upgradeable to maximize trust. Price is expressed in configurable decimal units (default: cents) and normalized to base-18 when read by vault contracts.

| Function                     | Access             | Description                                                                                                                     |
| ---------------------------- | ------------------ | ------------------------------------------------------------------------------------------------------------------------------- |
| `setPrice(price)`            | `PRICE_ADMIN_ROLE` | Submit a new NAV price. Runs the tolerance check. Reverts with `ToleranceExceeded` if the deviation is too large.               |
| `getDataInBase18()`          | View (public)      | Returns the current price normalized to 18 decimals. Reverts with `StalePrice` if the last update is older than `maxStaleness`. |
| `setTolerancePercent(bps)`   | `CONFIG_ROLE`      | Update the maximum allowed price deviation in basis points.                                                                     |
| `setPriceDecimals(decimals)` | `CONFIG_ROLE`      | Update the input decimal precision (must be 18 or fewer).                                                                       |
| `setMaxStaleness(seconds)`   | `CONFIG_ROLE`      | Update the maximum age of a valid price in seconds.                                                                             |
| `getPriceAge()`              | View (public)      | Returns seconds elapsed since the last price update.                                                                            |
| `isPriceStale(maxAge)`       | View (public)      | Returns true if `getPriceAge()` is greater than maxAge.                                                                         |
