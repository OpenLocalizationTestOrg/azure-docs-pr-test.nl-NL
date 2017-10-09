## <a name="load-balancer-differences"></a>Verschillen in Load Balancer

Er zijn verschillende opties toodistribute-netwerkverkeer met Microsoft Azure. Deze opties werken verschillend. Ze hebben een eigen functieset en ondersteunen verschillende scenario's. Ze kunnen elk afzonderlijk worden gebruikt, maar ook worden gecombineerd.

* **Azure Load Balancer** werkt op Hallo transportlaag (laag 4 in Hallo OSI-netwerkstack verwijzing). Het biedt op netwerkniveau distributie van verkeer voor exemplaren van een toepassing die wordt uitgevoerd in Hallo hetzelfde Azure-Datacenter.
* **Toepassingsgateway** werkt op laag van de toepassing hello (laag 7 in Hallo OSI-netwerkstack verwijzing). Het fungeert als een reverse proxy-service wordt beëindigd Hallo clientverbinding en doorsturen van aanvragen tooback-end-eindpunten.
* **Traffic Manager** werkt op Hallo DNS-niveau.  DNS-antwoorden toodirect eindgebruiker verkeer gedistribueerd tooglobally eindpunten wordt gebruikt. Clients vervolgens rechtstreeks verbinding gemaakt toothose eindpunten.

Hallo volgende tabel geeft een overzicht van Hallo-functies die worden aangeboden door elke service:

| Service | Azure Load Balancer | Application Gateway | Traffic Manager |
| --- | --- | --- | --- |
| Technologie |Transportniveau (laag 4) |Toepassingsniveau (laag 7) |DNS-niveau |
| Ondersteunde toepassingsprotocollen |Alle |HTTP, HTTPS en WebSockets |Alle (voor eindpuntbewaking is een HTTP-eindpunt vereist) |
| Eindpunten |Azure-VM's en Cloud Services-rolinstanties |Intern Azure-IP-adres, openbaar internet-IP-adres, Azure-VM of Azure Cloud Service |Azure-VM's, Cloud Services, Azure-web-apps en externe eindpunten |
| VNet-ondersteuning |Kan worden gebruikt voor internetgerichte en interne (VNet-)toepassingen |Kan worden gebruikt voor internetgerichte en interne (VNet-)toepassingen |Ondersteunt alleen internetgerichte toepassingen |
| Eindpuntbewaking |Ondersteund via tests |Ondersteund via tests |Ondersteund via HTTP/HTTPS GET |

Azure Load Balancer en network-verkeer tooendpoints voor Application Gateway route, maar ze hebben verschillende scenario's toowhich verkeer toohandle. Hallo helpt onderstaande tabel understanding Hallo verschil tussen de twee netwerktaakverdelers Hallo:

| Type | Azure Load Balancer | Application Gateway |
| --- | --- | --- |
| Protocollen |UDP/TCP |HTTP, HTTPS en WebSockets |
| IP-reservering |Ondersteund |Niet ondersteund |
| Load balancing-modus |5-tuple (bron-IP, bronpoort, doel-IP, doelpoort, protocoltype) |Round robin<br>Routering op basis van URL |
| Load balancing-modus (bron-IP/vergrendelde sessies) |2-tuple (bron-IP en doel-IP), 3-tuple (bron-IP, doel-IP en poort). Kan omhoog of omlaag schalen op basis van het aantal virtuele machines Hallo |Affiniteit op basis van cookies<br>Routering op basis van URL |
| Statuscontroles |Standaard: testinterval - 15 seconden. Uit rotatie gehaald: 2 doorlopende fouten. Ondersteunt door de gebruiker gedefinieerde tests |Inactieve testinterval - 30 seconden. Eruit gehaald na 5 opeenvolgende live verkeersfouten of het mislukken van één test in de inactieve modus. Ondersteunt door de gebruiker gedefinieerde tests |
| SSL-offloading |Niet ondersteund |Ondersteund |
| URL-gebaseerde routering | Niet ondersteund | Ondersteund|
| SSL-beleid | Niet ondersteund | Ondersteund|
