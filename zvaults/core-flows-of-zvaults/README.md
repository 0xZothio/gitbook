# Core Flows

The protocol exposes a small set of core flows: depositing stablecoins to mint a `zTOKEN`, redeeming a `zTOKEN` to exit, and updating the NAV the token is priced against. Every flow runs through the compliance sequence and the price safety bounds described elsewhere in this document; the descriptions below cover the operational path of each.

{% content-ref url="deposit-flow.md" %}
[deposit-flow.md](deposit-flow.md)
{% endcontent-ref %}

{% content-ref url="redemption-flow.md" %}
[redemption-flow.md](redemption-flow.md)
{% endcontent-ref %}

{% content-ref url="nav-price-update-flow.md" %}
[nav-price-update-flow.md](nav-price-update-flow.md)
{% endcontent-ref %}
