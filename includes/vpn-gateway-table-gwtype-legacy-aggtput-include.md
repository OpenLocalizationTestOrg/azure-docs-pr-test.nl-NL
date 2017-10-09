Hallo volgende tabel toont Hallo gatewaytypen en Hallo geschatte geaggregeerde doorvoer door de gateway-SKU. Deze tabel is van toepassing toohello Resource Manager en de klassieke implementatiemodellen. 

De prijzen zijn afhankelijk van de gateway-SKU's. Zie [Prijzen van VPN Gateway](https://azure.microsoft.com/pricing/details/vpn-gateway) voor meer informatie.

Houd er rekening mee dat Hallo UltraPerformance gateway-SKU niet in deze tabel weergegeven wordt. Zie voor informatie over Hallo UltraPerformance SKU Hallo [ExpressRoute](../articles/expressroute/expressroute-about-virtual-network-gateways.md) documentatie.

|  | **Doorvoer VPN-gateway (1)** | **Max. IPsec-tunnels VPN-gateway (2)** | **Doorvoer ExpressRoute-gateway** | **VPN-gateway en ExpressRoute bestaan tegelijk** |
| --- | --- | --- | --- | --- |
| **Basic SKU (3)(5)(6)** |100 Mbps |10 |500 Mbps (6) |Nee |
| **Standaard SKU (4)(5)** |100 Mbps |10 |1000 Mbps |Ja |
| **High Performance SKU (4)** |200 Mbps |30 |2000 Mbps |Ja |


(1) Hallo VPN-doorvoer is een ruwe schatting op basis van metingen tussen vnet's in Hallo Hallo dezelfde Azure-regio. Het is niet een gegarandeerde doorvoer voor cross-premises verbindingen via Internet Hallo. Is het Hallo maximale doorvoer van mogelijke meting.

(2) het aantal tunnels hello Raadpleeg tooRouteBased VPN-verbindingen. Een op beleid gebaseerde VPN biedt alleen ondersteuning voor één site-naar-site VPN-tunnel.

(3) BGP wordt niet ondersteund voor Hallo basis-SKU.

(4) Op beleid gebaseerde VPN-verbindingen worden niet ondersteund voor deze SKU. Ze worden ondersteund voor basis-SKU Hallo alleen.

(5) Actief-actief S2S VPN-gatewayverbindingen worden niet ondersteund voor deze SKU. Actieve wordt op Hallo HighPerformance SKU alleen ondersteund.

(6) het basis-SKU is voor gebruik met ExpressRoute afgeschaft.
