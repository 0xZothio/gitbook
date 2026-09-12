# zFX calculator

\---

description: >-

&#x20; zFX Calculator shows the live local currency amount a recipient receives for

&#x20; any USDC payout, at one stated rate with no hidden FX markup. Free to use and

&#x20; embeddable on any website.

icon: calculator

\---

\# zFX Calculator

The zFX Calculator is a free stablecoin cross-border payout calculator. Enter a USDC amount, select a destination currency, and the calculator returns the exact local currency amount the recipient receives, at one stated rate with no hidden FX markup. It runs as a hosted page and as an embeddable widget for any website.

\{% hint style="info" %\}

Open the live calculator at \[zfx.web.app/calculator]\(https://zfx.web.app/calculator.html). Supported currencies are listed live on that page and on the \[Global FX Rates board]\(https://zfx.web.app/rates.html).

\{% endhint %\}<br>

\## How it works

\`\`\`mermaid

flowchart LR

&#x20;   A\["Enter USDC amount"] --> B\["Select payout currency"]

&#x20;   B --> C\["Live zFX rate and recipient amount"]

&#x20;   C --> D\["Initiate Payout"]

&#x20;   D --> E\["zPayments team settles"]

\`\`\`

\| Field | What it does |

\| ----- | ------------ |

\| \*\*You Send\*\* | Enter the USDC amount. USDC is the only send currency |

\| \*\*Recipient Gets\*\* | Select the payout currency. The recipient amount calculates live |

\| \*\*Rate line\*\* | Shows the zFX rate applied to the payout |

\| \*\*Initiate Payout\*\* | Opens contact with the zPayments team at \[zpayments@zoth.io]\(mailto:zpayments@zoth.io) |<br>

\## What the rate includes

\- One stated rate, quoted before the payout is initiated

\- No FX markup buried inside the rate

\- The figure under \*\*Recipient Gets\*\* is the amount that lands in the beneficiary bank account

\- Rates stream live and move with the market, so the quote is current at the moment it is shown<br>

\## Why a dedicated stablecoin payout calculator

Standard FX converters quote a mid-market rate that no payment provider actually delivers. The gap between that rate and the settled amount is where margin usually sits. zFX quotes the payout rate itself, so the number on screen is the number the recipient receives.<br>

\## Supported currencies

Send currency is USDC. Destination currencies are listed live on the \[calculator page]\(https://zfx.web.app/calculator.html) and change as corridors are added.<br>

\## Embedding the calculator

Add the calculator to any site with a single iframe. No script, no API key, no account.

\{% code title="zFX widget embed" overflow="wrap" %\}

\`\`\`html

\<iframe src="https://zfx.web.app/calculator.html" width="100%" height="580" style="border:none; border-radius:24px; max-width:440px;" title="zFX Calculator">\</iframe>

\`\`\`

\{% endcode %\}<br>

\{% tabs %\}

\{% tab title="WordPress" %\}

Open the page editor, add a \*\*Custom HTML\*\* block, paste the snippet, publish.

\{% endtab %\}<br>

\{% tab title="Wix / Squarespace" %\}

Open the page editor, add an \*\*Embed HTML\*\* element, paste the snippet, publish.

\{% endtab %\}<br>

\{% tab title="Custom site" %\}

Paste the snippet into the page HTML where the calculator should render.

\{% endtab %\}

\{% endtabs %\}<br>

\*\*Specifications:\*\* width 100 percent to a 440px maximum, height 580px, no border, 24px corner radius, no dependencies.<br>

\{% hint style="warning" %\}

Keep the height at 580px. Lower values crop the rate line and the payout control.

\{% endhint %\}<br>

\## Frequently asked questions<br>

\### How does zFX calculate the payout rate?<br>

The rate streams from live corridor pricing and already carries the cost of settlement. It is the rate applied to the payout, not a mid-market reference rate.<br>

\### Is the calculator free to use?<br>

Yes. The calculator and the embeddable widget are free, with no account or API key required.<br>

\### Is zFX an offramp?<br>

No. zFX supports a payout rail that settles stablecoin into a beneficiary bank account in local currency. The sender never handles the local currency leg.<br>

\### Which currencies can I calculate?<br>

Send currency is USDC. The destination list is live on the calculator page and grows as corridors are added.<br>

\### How long does settlement take?<br>

Settlement is real time on priority corridors and next business day where local rails require it.<br>

\### Who operates zFX?<br>

zFX is a product of Zoth Payments Limited, a money services business registered with FINTRAC in Canada.<br>

\## Talk to the payouts team<br>

For corridor coverage, volume pricing, and onboarding, contact \[zpayments@zoth.io]\(mailto:zpayments@zoth.io).<br>

{% embed url="https://zfx.web.app" %}
