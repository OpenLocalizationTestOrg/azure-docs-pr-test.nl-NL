Hallo oudere (oude) VPN-gateway SKU's zijn:

* Basic
* Standard
* HighPerformance

VPN-Gateway gebruikt geen Hallo UltraPerformance gateway-SKU. Zie voor informatie over Hallo UltraPerformance SKU Hallo [ExpressRoute](../articles/expressroute/expressroute-about-virtual-network-gateways.md) documentatie.

Als u werkt met Hallo verouderde SKU's, houd rekening met de volgende Hallo:

* Als u toouse een PolicyBased VPN-type wilt, moet u Hallo basis-SKU. PolicyBased VPN-verbindingen (voorheen statische routering) worden niet ondersteund op andere SKU's.
* BGP wordt niet ondersteund op Hallo basis-SKU.
* ExpressRoute-VPN-Gateway worden gecombineerd configuraties worden niet ondersteund op Hallo basis-SKU.
* Actieve S2S-VPN-gatewayverbindingen kunnen worden geconfigureerd op alleen Hallo HighPerformance SKU.
