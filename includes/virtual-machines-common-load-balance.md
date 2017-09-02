

Er zijn twee niveaus van taakverdeling beschikbaar voor Azure-infrastructuurservices:

* **DNS-niveau**: taakverdeling voor verkeer naar een andere cloud-services zich in verschillende data centers naar verschillende Azure websites zich in verschillende datacenters, of op externe eindpunten. Dit wordt gedaan met Azure Traffic Manager en de Round-Robin load balancing-methode.
* **Netwerk-niveau**: Load balancing van binnenkomende internetverkeer naar verschillende virtuele machines van een cloudservice of taakverdeling van verkeer tussen virtuele machines in een cloudservice of het virtuele netwerk. Dit wordt gedaan met de Azure load balancer.

## <a name="traffic-manager-load-balancing-for-cloud-services-and-websites"></a>Traffic Manager taakverdeling voor cloudservices en websites
Traffic Manager kunt u de distributie van gebruikersverkeer naar eindpunten, waaronder cloudservices, websites, externe sites en andere Traffic Manager-profielen te beheren. Traffic Manager werkt door het toepassen van een intelligente beleidsengine voor Domain Name System (DNS)-query's voor de domeinnamen van uw Internet-bronnen. Uw cloudservices of websites kunnen worden uitgevoerd in verschillende datacenters over de hele wereld.

U moet een REST- of Windows PowerShell gebruiken voor het configureren van externe eindpunten of Traffic Manager-profielen als eindpunten.

Traffic Manager maakt gebruik van drie methoden voor taakverdeling voor het distribueren van verkeer:

* **Failover**: Gebruik deze methode als u wilt gebruiken van een primaire eindpunt voor al het verkeer, maar bieden back-ups als de primaire niet beschikbaar.
* **Prestaties**: Gebruik deze methode wanneer u eindpunten op verschillende geografische locaties en u wilt dat clients die aanvragen indienen het eindpunt 'dichtstbijzijnde' in termen van de laagste latentie te gebruiken.
* **Round Robin:** Gebruik deze methode als u wilt verdelen over een set van cloud-services in hetzelfde datacenter of in de cloud-services of websites in verschillende datacenters.

Zie voor meer informatie [over Traffic Manager Load Balancing methoden](../articles/traffic-manager/traffic-manager-routing-methods.md).

Het volgende diagram toont een voorbeeld van de taakverdelingsmethode van Round Robin voor het distribueren van verkeer tussen verschillende cloud-services.

![loadbalancing](./media/virtual-machines-common-load-balance/TMSummary.png)

Het basisproces is het volgende:

1. Een internetclient vraagt een domeinnaam die overeenkomt met een webservice.
2. DNS stuurt de aanvraag van de query naam aan Traffic Manager.
3. Traffic Manager de volgende cloudservice kiest in de lijst Round Robin en stuurt terug de DNS-naam. De client Internet DNS-server wordt de naam omgezet in een IP-adres en verzendt het naar de client via Internet.
4. De client via Internet verbinding met de gekozen door Traffic Manager-cloudservice.

Zie voor meer informatie [Traffic Manager](../articles/traffic-manager/traffic-manager-overview.md).

## <a name="azure-load-balancing-for-virtual-machines"></a>Azure load balancer voor virtuele machines
Virtuele machines in dezelfde cloudservice of virtuele netwerk kan communiceren met elkaar rechtstreeks met hun persoonlijke IP-adressen. Computers en services buiten de service in de cloud of een virtueel netwerk kunnen communiceren alleen met virtuele machines in een service in de cloud of een virtueel netwerk met een geconfigureerde eindpunt. Een eindpunt is een toewijzing van een openbaar IP-adres en poort op die privé IP-adres en poort van een virtuele machine of de Webrol in een Azure-cloud-service.

De Azure Load Balancer verdeelt willekeurig een specifiek type binnenkomend verkeer over meerdere virtuele machines of services in een configuratie met een set met gelijke taakverdeling genoemd. Bijvoorbeeld, kunt u het laden van de aanvraag webverkeer spreiden meerdere webservers of web-rollen.

Het volgende diagram toont een eindpunt met gelijke taakverdeling voor standaard (niet-versleutelde) internetverkeer die wordt gedeeld door drie virtuele machines voor de openbare en persoonlijke TCP-poort 80. Deze drie virtuele machines zijn in een set met gelijke taakverdeling.

![loadbalancing](./media/virtual-machines-common-load-balance/LoadBalancing.png)

Zie voor meer informatie [Azure Load Balancer](../articles/load-balancer/load-balancer-overview.md). Zie voor de stappen voor het maken van een set met gelijke taakverdeling [een set met gelijke taakverdeling configureren](../articles/load-balancer/load-balancer-get-started-internet-arm-ps.md).

Taakverdeling binnen een cloudservice of een virtueel netwerk worden ook toegepast op Azure. Dit staat bekend als interne load balancing en kan worden gebruikt in de volgende manieren:

* Om taken te verdelen tussen servers in verschillende lagen van een toepassing met meerdere lagen (bijvoorbeeld tussen web- en databaselagen).
* Laden verdelen over line-of-business (LOB) toepassingen die worden gehost in Azure zonder dat extra load balancer-hardware of software.
* Voor het opnemen van lokale servers in de set van computers waarvan het verkeer is de belasting met taakverdeling.

Vergelijkbaar met Azure load balancing, interne load balancer proces wordt vergemakkelijkt door een interne set met gelijke taakverdeling configureren.

Het volgende diagram toont een voorbeeld van een intern eindpunt van de taakverdeling voor een line-of-business (LOB)-toepassing die wordt gedeeld door drie virtuele machines in een virtueel netwerk met cross-premises.

![loadbalancing](./media/virtual-machines-common-load-balance/LOBServers.png)

## <a name="load-balancer-considerations"></a>Load balancer-overwegingen
Een load balancer is standaard geconfigureerd voor time-out voor een niet-actieve sessie in vier minuten. Als uw toepassing achter een load balancer een verbinding inactief voor meer dan vier minuten verlaat en geen een Keep-Alive configuratie heeft, is de verbinding wordt verbroken. Kunt u het gedrag van de load balancer om toe te staan een [langere time-outinstelling voor Azure load balancer](../articles/load-balancer/load-balancer-tcp-idle-timeout.md).

Andere overweging is het type van de distributie-modus wordt ondersteund door Azure Load Balancer. U kunt de bron-IP-affiniteit (bron-IP, doel-IP) of bron-IP-protocol (bron-IP, doel-IP en -protocol) configureren. Bekijk [Azure Load Balancer-distributie-modus (bron-IP-affiniteit)](../articles/load-balancer/load-balancer-distribution-mode.md) voor meer informatie.

## <a name="next-steps"></a>Volgende stappen
Zie voor de stappen voor het maken van een set met gelijke taakverdeling [configureren van een interne set met gelijke taakverdeling](../articles/load-balancer/load-balancer-get-started-ilb-arm-ps.md).

Zie voor meer informatie over de load balancer [interne load balancing](../articles/load-balancer/load-balancer-internal-overview.md).

