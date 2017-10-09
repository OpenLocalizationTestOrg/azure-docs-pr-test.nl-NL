Wanneer u een virtuele netwerkgateway maakt, moet u toospecify Hallo gateway SKU die u toouse wilt. Selecteer Hallo-SKU's die voldoen aan uw behoeften op basis van Hallo typen werkbelastingen, doorvoercapaciteit, functies en sla's.

[!INCLUDE [classic SKU](./vpn-gateway-classic-sku-support-include.md)]

[!INCLUDE [Aggregated throughput by SKU](./vpn-gateway-table-gwtype-aggtput-include.md)]

###  <a name="workloads"></a>Productie *vs.* werkbelastingen voor ontwikkelen en testen

Vervaldatum toohello verschillen in de sla en functiesets, wordt aangeraden Hallo SKU's voor productie na *versus* dev-test:

| **Workload**                       | **SKU's**               |
| ---                                | ---                    |
| **Productie, kritieke werkbelastingen** | VpnGw1, VpnGw2, VpnGw3 |
| **Ontwikkelen en testen of conceptontwerpen**   | Basic                  |
|                                    |                        |

Als u oude hello, SKU's, Hallo productie SKU aanbevelingen zijn Standard en HighPerformance SKU's. Zie voor informatie over Hallo oude SKU's, [Gateway-SKU's (verouderde SKU's)](../articles/vpn-gateway/vpn-gateway-about-skus-legacy.md).

###  <a name="feature"></a>Gateway-SKU-functiesets

Hallo nieuwe gateway-SKU's stroomlijnen Hallo functiesets aangeboden op Hallo gateways:

| **SKU**| **Functies**|
| ---    | ---         |
|**Basic**   | **Op route gebaseerd VPN**: 10 tunnels met P2S<br><br>**Op beleid gebaseerd VPN**: (IKEv1): 1 tunnel; geen P2S|
| **VpnGw1, VpnGw2 en VpnGw3** | **Route gebaseerde VPN-**: too30 tunnels (*), P2S, BGP, actieve, aangepaste IPsec/IKE-beleid, naast elkaar bestaan ExpressRoute/VPN |
|        |             |

(*) U kunt 'PolicyBasedTrafficSelectors' tooconnect een op route gebaseerde VPN-gateway (VpnGw1, VpnGw2, VpnGw3) toomultiple on-premises firewall op beleid gebaseerde apparaten configureren. Raadpleeg te[verbinding maken met VPN-gateways toomultiple on-premises op beleid gebaseerde VPN-apparaten met behulp van PowerShell](../articles/vpn-gateway/vpn-gateway-connect-multiple-policybased-rm-ps.md) voor meer informatie.

###  <a name="resize"></a>Het formaat van gateway-SKU's wijzigen

1. U kunt wisselen tussen VpnGw1-, VpnGw2- en VpnGw3-SKU's.
2. Als u werkt met Hallo oude gateway-SKU's, kunt u het formaat van tussen Basic, Standard en HighPerformance SKU's.
2. U **kan niet** vergroten of verkleinen van standaard-Basic/HighPerformance SKU's toohello nieuwe VpnGw2-VpnGw1/VpnGw3-SKU's. U moet in plaats daarvan [migreren](#migrate) toohello nieuwe SKU's.

###  <a name="migrate"></a>Migreren van oude SKU's toohello nieuwe SKU's

[!INCLUDE [Migrate SKU](./vpn-gateway-migrate-legacy-sku-include.md)]
