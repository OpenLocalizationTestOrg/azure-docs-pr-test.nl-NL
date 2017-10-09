

Er zijn twee niveaus van taakverdeling beschikbaar voor Azure-infrastructuurservices:

* **DNS-niveau**: taakverdeling voor verkeer toodifferent cloud-services zich in verschillende data centers, toodifferent Azure websites zich in verschillende datacenters of tooexternal eindpunten. Dit wordt gedaan met Azure Traffic Manager en Hallo Round-Robin taakverdelingsmethode.
* **Netwerk-niveau**: Load balancing van binnenkomende Internet verkeer toodifferent virtuele machines van een cloudservice of taakverdeling van verkeer tussen virtuele machines in een cloudservice of het virtuele netwerk. Dit wordt gedaan met hello Azure load balancer.

## <a name="traffic-manager-load-balancing-for-cloud-services-and-websites"></a>Traffic Manager taakverdeling voor cloudservices en websites
Traffic Manager kunt u toocontrol Hallo distributie van de gebruiker verkeer tooendpoints, waaronder cloudservices, websites, externe sites en andere Traffic Manager-profielen. Traffic Manager werkt door het toepassen van een intelligente beleid engine tooDomain Name System (DNS)-query's voor domeinnamen op Hallo van uw Internet-bronnen. Uw cloudservices of websites kunnen worden uitgevoerd in verschillende datacenters over Hallo wereld.

U moet externe eindpunten met tooconfigure REST of Windows PowerShell of Traffic Manager-profielen als eindpunten gebruiken.

Traffic Manager maakt gebruik van drie methoden toodistribute verkeer taakverdeling:

* **Failover**: Gebruik deze methode als u wilt dat een primaire eindpunt toouse voor al het verkeer, maar back-ups bieden geval Hallo primaire wegvalt.
* **Prestaties**: Gebruik deze methode wanneer u eindpunten op verschillende geografische locaties en u wilt dat clients toouse Hallo 'dichtstbijzijnde' eindpunt in termen van de laagste latentie Hallo aanvraagt.
* **Round Robin:** gebruik van deze methode als u wilt laden toodistribute over een set van cloud-services in Hallo dezelfde datacenter of in de cloud-services of websites in verschillende datacenters.

Zie voor meer informatie [over Traffic Manager Load Balancing methoden](../articles/traffic-manager/traffic-manager-routing-methods.md).

Hallo volgende diagram toont een voorbeeld van Hallo Round-Robin load balancing-methode voor het distribueren van verkeer tussen verschillende cloud-services.

![loadbalancing](./media/virtual-machines-common-load-balance/TMSummary.png)

Hallo basisproces verloopt Hallo volgende:

1. Een internetclient query op een domein naam bijbehorende tooa webservice.
2. DNS verzendt Hallo naam query aanvraag tooTraffic Manager.
3. Traffic Manager Hallo volgende cloudservice kiest in de lijst van Round-Robin Hallo en verzendt terug Hallo DNS-naam. Hallo internetclient DNS-server wordt omgezet Hallo naam tooan IP-adres en verzendt deze toohello internetclient.
4. Hallo internetclient verbinding met de cloudservice Hallo gekozen door Traffic Manager.

Zie voor meer informatie [Traffic Manager](../articles/traffic-manager/traffic-manager-overview.md).

## <a name="azure-load-balancing-for-virtual-machines"></a>Azure load balancer voor virtuele machines
Virtuele machines in dezelfde cloudservice Hallo of virtueel netwerk kan communiceren met elkaar via hun persoonlijke IP-adressen. Computers en services buiten Hallo cloudservice of virtuele netwerk kan alleen communiceren met virtuele machines in een service in de cloud of een virtueel netwerk met een geconfigureerde eindpunt. Een eindpunt is een toewijzing van een openbaar IP-adres en poort toothat privé IP-adres en poort van een virtuele machine of de Webrol in een Azure-cloud-service.

Hello Azure Load Balancer verdeelt willekeurig een specifiek type binnenkomend verkeer over meerdere virtuele machines of services in een configuratie met een set met gelijke taakverdeling genoemd. Bijvoorbeeld, kunt u Hallo belasting van de aanvraag webverkeer spreiden meerdere webservers of web-rollen.

Hallo toont volgende diagram een eindpunt met gelijke taakverdeling voor standaard (niet-versleutelde) internetverkeer die wordt gedeeld door drie virtuele machines voor Hallo openbare en persoonlijke TCP-poort 80. Deze drie virtuele machines zijn in een set met gelijke taakverdeling.

![loadbalancing](./media/virtual-machines-common-load-balance/LoadBalancing.png)

Zie voor meer informatie [Azure Load Balancer](../articles/load-balancer/load-balancer-overview.md). Zie voor Hallo stappen toocreate uit een set met gelijke taakverdeling, [een set met gelijke taakverdeling configureren](../articles/load-balancer/load-balancer-get-started-internet-arm-ps.md).

Taakverdeling binnen een cloudservice of een virtueel netwerk worden ook toegepast op Azure. Dit staat bekend als interne load balancing en kan worden gebruikt in de volgende manieren Hallo:

* tooload balans tussen servers in verschillende lagen van een toepassing met meerdere lagen (bijvoorbeeld tussen web- en databaselagen).
* tooload saldo van LOB-toepassingen (LOB) gehost in Azure, zonder dat extra load balancer-hardware of software.
* tooinclude lokale servers in Hallo set computers waarvan het verkeer gelijkmatig verdeeld wordt.

Vergelijkbare tooAzure taakverdeling, interne load balancing wordt vergemakkelijkt door een interne set met gelijke taakverdeling configureren.

Hallo volgende diagram toont een voorbeeld van een intern eindpunt van de taakverdeling voor een line-of-business (LOB)-toepassing die wordt gedeeld door drie virtuele machines in een virtueel netwerk met cross-premises.

![loadbalancing](./media/virtual-machines-common-load-balance/LOBServers.png)

## <a name="load-balancer-considerations"></a>Load balancer-overwegingen
Een load balancer is standaard geconfigureerd tootimeout een niet-actieve sessie in vier minuten. Als uw toepassing achter een load balancer een verbinding inactief voor meer dan vier minuten verlaat en geen een Keep-Alive configuratie heeft, Hallo verbinding verwijderd. Hallo load balancer gedrag tooallow kunt u een [langere time-outinstelling voor Azure load balancer](../articles/load-balancer/load-balancer-tcp-idle-timeout.md).

Andere overweging is Hallo type distributiepunt modus wordt ondersteund door Azure Load Balancer. U kunt de bron-IP-affiniteit (bron-IP, doel-IP) of bron-IP-protocol (bron-IP, doel-IP en -protocol) configureren. Bekijk [Azure Load Balancer-distributie-modus (bron-IP-affiniteit)](../articles/load-balancer/load-balancer-distribution-mode.md) voor meer informatie.

## <a name="next-steps"></a>Volgende stappen
Zie voor Hallo stappen toocreate uit een set met gelijke taakverdeling, [configureren van een interne set met gelijke taakverdeling](../articles/load-balancer/load-balancer-get-started-ilb-arm-ps.md).

Zie voor meer informatie over de load balancer [interne load balancing](../articles/load-balancer/load-balancer-internal-overview.md).

