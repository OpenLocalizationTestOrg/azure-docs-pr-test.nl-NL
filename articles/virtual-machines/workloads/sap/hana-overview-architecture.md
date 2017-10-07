---
title: aaaOverview en architectuur van SAP HANA in Azure (grote exemplaren) | Microsoft Docs
description: Overzicht van de architectuur van het tooDeploy SAP HANA in Azure (grote exemplaren).
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e3ee6864af37ac322635eaef43e3c20101e3a769
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-large-instances-overview-and-architecture-on-azure"></a>Overzicht van de SAP HANA (grote exemplaren) en architectuur op Azure

## <a name="what-is-sap-hana-on-azure-large-instances"></a>Wat is een SAP HANA in Azure (grote exemplaren)?

SAP HANA in Azure (grote exemplaar) is een unieke oplossing tooAzure. Bovendien tooproviding Azure Virtual Machines Hallo doel te implementeren en uitvoeren van SAP HANA, Azure biedt u Hallo mogelijkheid toorun en SAP HANA implementeren op bare metal-servers die toegewezen tooyou als een klant zijn. Hallo SAP HANA in Azure (grote exemplaren)-oplossing is gebaseerd op niet-gedeelde/hostserver bare-metal hardware die tooyou als een klant is toegewezen. Hallo serverhardware is ingesloten in grotere stempels die compute/server-, netwerk- en opslaginfrastructuur bevatten. Dit, als een combinatie HANA TDI gecertificeerd is. Hallo-service-aanbieding voor SAP HANA in Azure (grote exemplaren) biedt verschillende SKU's van andere server of grootten vanaf eenheden die 72 CPU's hebben en 768 GB geheugen toounits waarvoor 960 CPU's en 20 TB geheugen.

Hallo klant isolatielaag binnen Hallo infrastructuur stempel moet worden uitgevoerd in de tenants die in details ziet eruit als:

- Netwerken: Isolatie van klanten in de infrastructuur-stack via virtuele netwerken per klant toegewezen tenant. Een tenant wordt één klant tooa toegewezen. Een klant kan meerdere tenants hebben. Hallo netwerkisolatie van tenants verbiedt netwerkcommunicatie tussen de tenants op Hallo infrastructuur stempel niveau. Zelfs als tenants toohello behoren dezelfde klant.
- Opslagonderdelen: isolatie door middel van opslag virtuele machines met opslagvolumes tooit toegewezen. Opslagvolumes worden tooone opslag virtuele machine alleen toegewezen. Een virtuele machine van opslag is één tenant uitsluitend tooone in Hallo SAP HANA TDI gecertificeerde infrastructuur stack toegewezen. Als gevolg hiervan kunnen opslagvolumes toegewezen tooa opslag virtuele machine worden geopend in een specifieke en verwante tenant alleen. En zijn niet zichtbaar tussen verschillende geïmplementeerde tenants Hallo.
- Server- of host: een eenheid server- of host wordt niet gedeeld tussen klanten of tenants. Een server of de host tooa klant geïmplementeerd, is een atomic bare-metal compute-eenheid die één tenant tooone is toegewezen. **Geen** hardware partitioneren of soft partitioneren wordt gebruikt die kunnen leiden tot u, als een klant, delen van een host of een server met een andere klant. Opslagvolumes die zijn toegewezen toohello opslag virtuele machine van de specifieke Hallo-tenant zijn gekoppeld toosuch een server. Een tenant kan één toomany server eenheden van verschillende SKU's exclusief toegewezen hebben.
- Binnen een SAP HANA op Azure (grote exemplaar) infrastructuur stempel, zijn veel verschillende tenants geïmplementeerd en ten opzichte van elkaar geïsoleerd door Hallo tenant concepten op niveau van netwerken, opslag en berekeningen. 


Deze eenheden bare metal-server worden ondersteund op toorun SAP HANA alleen. Hallo SAP toepassingslaag of werkbelasting middleware-laag wordt uitgevoerd in Microsoft Azure Virtual Machines. Hallo infrastructuur stempels Hallo SAP HANA uitgevoerd op Azure (grote exemplaar) zijn eenheden verbonden toohello Azure Network wervels, dus die lage latentie connectiviteit tussen SAP HANA op Azure (grote exemplaar) eenheden en virtuele Machines van Azure wordt geleverd.

Dit document is een van vijf documenten die betrekking hebben op Hallo onderwerp van het SAP HANA in Azure (grote exemplaar). In dit document gaan we basisarchitectuur hello, verantwoordelijkheden, services die worden geleverd en op een hoog niveau met behulp van de functionaliteit van Hallo-oplossing. Voor de meeste Hallo gebieden, zoals netwerken en verbindingen, hello andere vier documenten zijn die betrekking hebben op meer informatie en omlaag keuzelijsten. Hallo-documentatie voor SAP HANA in Azure (grote exemplaar) wordt niet uitgelegd aspecten van SAP NetWeaver-installatie of implementaties van SAP NetWeaver in Azure VM's. In dit onderwerp wordt beschreven in afzonderlijke documentatie gevonden in Hallo dezelfde container documentatie. 


Hallo vijf onderdelen van deze handleiding Hallo volgende onderwerpen te omvatten:

- [Overzicht van de SAP HANA (grote exemplaar) en architectuur op Azure](hana-overview-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Infrastructuur voor SAP HANA (grote exemplaren) en de verbindingen van Azure](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Hoe tooinstall en SAP HANA (grote exemplaren) configureren in Azure](hana-installation.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [SAP HANA (grote exemplaren) hoge beschikbaarheid en herstel na noodgevallen op Azure](hana-overview-high-availability-disaster-recovery.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Probleemoplossing voor SAP HANA (grote exemplaren) en de controle op Azure](troubleshooting-monitoring.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="definitions"></a>Definities

Verschillende gemeenschappelijke definities worden veel gebruikt in Hallo architectuur en technische Deployment Guide. Hallo opmerking na de voorwaarden en hun betekenis:

- **IaaS:** infrastructuur als een Service
- **PaaS:** Platform as a Service
- **SaaS:** Software als een Service
- **SAP-onderdeel:** een afzonderlijke SAP-toepassing, zoals ECC, BW, oplossing Manager of EP is geplaatst. SAP-onderdelen kunnen worden gebaseerd op traditionele ABAP of Java-technologieën of een NetWeaver op basis van toepassing zoals zakelijke objecten.
- **SAP-omgeving:** een of meer onderdelen voor SAP tooperform een business-functie, zoals ontwikkeling, QAS, Training, DR of productie logisch zijn gegroepeerd.
- **SAP liggend:** toohello gehele SAP activa in uw IT-liggend verwijst. Hallo SAP liggend bevat alle productie en niet-productieve omgevingen.
- **SAP-systeem:** Hallo combinatie van laag DBMS en toepassingslaag van een SAP ERP-ontwikkelsysteem, SAP BW testsysteem, productiesysteem SAP CRM, enzovoort. Implementaties van Azure bieden geen ondersteuning voor het delen van deze twee lagen tussen on-premises en Azure. Betekent een SAP-systeem is geïmplementeerde on-premises of deze is geïmplementeerd in Azure. U kunt echter verschillende systemen Hallo van een liggend SAP in Azure of on-premises implementeren. Bijvoorbeeld, kan u Hallo SAP CRM ontwikkeling en tests systemen implementeren in Azure, tijdens de implementatie van Hallo SAP CRM productie system lokale. Het is voor SAP HANA in Azure (grote exemplaren), dat u Hallo SAP toepassingslaag van SAP-systemen in Azure VM's host en bijbehorende SAP HANA-exemplaar op een eenheid in Hallo HANA grote exemplaar stempel Hallo bedoeld.
- **Grote exemplaar stempel:** een hardware-infrastructuur stack die SAP HANA TDI gecertificeerd en specifiek toorun SAP HANA-exemplaren in Azure.
- **SAP HANA in Azure (grote exemplaren):** officiële taal voor de aanbieding Hallo in Azure toorun HANA-exemplaren in op SAP HANA TDI gecertificeerde hardware die wordt geïmplementeerd in grote exemplaar stempels in verschillende Azure-regio's. Hallo gerelateerde term **HANA grote exemplaar** kort voor SAP HANA in Azure (grote exemplaren) is en veel deze technische handleiding gebruikt.
- **Cross-Premises:** beschrijft een scenario waarin VM's zijn geïmplementeerde tooan Azure-abonnement met site-naar-site meerdere locaties of ExpressRoute-verbinding tussen Hallo lokale clientresources en Azure. Gemeenschappelijk Azure-documentatie, dit soort implementaties worden ook beschreven als Cross-Premises scenario's. Hallo reden voor Hallo verbinding is tooextend on-premises domeinen, on-premises Active Directory/OpenLDAP, en lokale DNS in Azure. Hallo lokale liggend is uitgebreide toohello Azure activa Hallo Azure-abonnementen. Met deze uitbreiding, kan Hallo VMs deel uitmaken van Hallo lokaal domein. Domeingebruikers van Hallo lokale domein hebben toegang tot Hallo-servers en services kunnen uitvoeren op de virtuele machines (zoals DBMS services). Communicatie en naamomzetting tussen de geïmplementeerde virtuele machines on-premises en geïmplementeerde virtuele machines in Azure is mogelijk. Dergelijke is Hallo typisch scenario in waarop de meeste SAP activa zijn geïmplementeerd. Zie Hallo hulplijnen van [Planning en ontwerp voor VPN-Gateway](../../../vpn-gateway/vpn-gateway-plan-design.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) en [maken van een VNet met een Site-naar-Site-verbinding met hello Azure-portal](../../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) voor meer informatie gedetailleerde.
- **Tenant:** een klant die is geïmplementeerd in grote exemplaren HANA stempel opgehaald geïsoleerd in een 'tenant'. Een tenant is geïsoleerd in Hallo netwerken, opslag en berekeningslaag van andere tenants. Ja, dat opslagruimte en rekencapaciteit eenheden toegewezen toohello verschillende tenants niet zien elkaar of met elkaar communiceren op Hallo tijdstempel HANA grote exemplaar niveau. Een klant kunt toohave implementaties in verschillende tenants. Er is zelfs dan geen communicatie tussen de tenants op Hallo HANA grote stempel instantieniveau.

Er zijn tal van aanvullende bronnen die zijn gepubliceerd op Hallo onderwerp van het implementeren van SAP-werkbelasting op Microsoft Azure openbare cloud. Het is raadzaam dat iedereen plannen en uitvoeren van een SAP HANA-implementatie in Azure ervaren en op de hoogte van Hallo principals van Azure IaaS en Hallo-implementatie van de SAP-werkbelastingen op Azure IaaS is. Hallo volgende bronnen geven informatie en moeten worden verwezen voordat u verdergaat:


- [SAP-oplossingen gebruiken op Microsoft Azure virtuele machines](get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="certification"></a>Certificering

Afgezien van hello NetWeaver certificering, vereist SAP een speciale certificaat voor SAP HANA toosupport SAP HANA op bepaalde infrastructuren, zoals Azure IaaS.

Hallo Core SAP-notitie op NetWeaver en tooa mate SAP HANA-certificering, [SAP-notitie #1928533 – SAP-toepassingen in Azure: typen ondersteunde producten en de virtuele machine van Azure](https://launchpad.support.sap.com/#/notes/1928533).

Dit [SAP Opmerking #2316233 - SAP HANA op Microsoft Azure (grote exemplaren)](https://launchpad.support.sap.com/#/notes/2316233/E) is ook belangrijk. Er wordt aangegeven Hallo-oplossing in deze handleiding beschreven. Daarnaast bent u ondersteunde toorun SAP HANA in het type van de Hallo GS5 VM van Azure. [Informatie voor deze aanvraag is gepubliceerd op Hallo SAP website](http://global.sap.com/community/ebook/2014-09-02-hana-hardware/enEN/iaas.html).

Hallo SAP HANA in Azure (grote exemplaren)-oplossing bedoelde tooin SAP-notitie #2316233 Microsoft biedt en SAP-klanten de mogelijkheid toodeploy Hallo grote SAP Business Suite, SAP Business Warehouse (BW), S/4 HANA, BW/4HANA of andere werkbelastingen SAP HANA in Azure. Hallo-oplossing is gebaseerd op Hallo SAP-HANA gecertificeerd van specifieke hardware stempel ([SAP HANA aangepast Datacenter integratie – TDI](https://scn.sap.com/docs/DOC-63140)). Wordt uitgevoerd als een SAP HANA TDI biedt geconfigureerde oplossing u Hallo vertrouwen van weten dat alle SAP HANA-toepassingen (inclusief SAP Business Suite van SAP HANA en SAP Business Warehouse (BW) voor SAP HANA, S4/HANA en BW4/HANA) toowork op Hallo gaat hardware-infrastructuur.

Een voordeel ten opzichte toorunning SAP HANA in Azure Virtual Machines deze oplossing heeft: het zorgt voor veel grotere volumes van geheugen. Als u deze oplossing tooenable wilt, zijn er enkele belangrijke aspecten toounderstand:

- Hallo SAP toepassingslaag en niet-SAP-toepassingen worden uitgevoerd in Azure Virtual Machines (VM's) die worden gehost in Hallo gebruikelijke Azure hardware stempels.
- Klant on-premises infrastructuur, datacenters en implementaties van toepassingen zijn verbonden toohello cloudplatform van Microsoft Azure via Azure ExpressRoute (aanbevolen) of virtuele particuliere netwerk (VPN). Active Directory (AD) en DNS ook worden uitgebreid naar Azure.
- Hallo SAP HANA-database-exemplaar voor HANA werkbelasting wordt uitgevoerd op een SAP HANA in Azure (grote exemplaren). Hallo grote exemplaar stempel is verbonden in Azure-netwerken, zodat de software die wordt uitgevoerd in Azure VM's kan communiceren met de Hallo HANA-exemplaar in grote HANA-exemplaren.
- Hardware van de SAP HANA in Azure (grote exemplaren) is specifieke hardware die zijn opgegeven in een infrastructuur als een Service (IaaS) met SUSE Linux Enterprise Server of Red Hat Enterprise Linux, vooraf is geïnstalleerd. Is uw verantwoordelijkheid zoals met Azure Virtual Machines verdere updates en onderhoud toohello-besturingssysteem.
- Installatie van HANA of eventuele extra onderdelen nodig toorun SAP HANA op eenheden HANA grote exemplaren van is uw verantwoordelijkheid, evenals alle respectieve conflicterende bewerkingen worden uitgevoerd en administraties van SAP HANA op Azure.
- Bovendien toohello oplossingen die hier worden beschreven, u kunt andere onderdelen installeren op uw Azure-abonnement dat verbinding tooSAP HANA in Azure (grote exemplaren maakt).  Bijvoorbeeld, de onderdelen waarmee de communicatie met en/of rechtstreeks toohello SAP HANA-database (korte inleiding-servers, RDP-servers, SAP HANA Studio SAP Data Services voor SAP BI-scenario's of bewakingsoplossingen netwerk).
- Als in Azure bieden HANA grote exemplaren ondersteunende functionaliteit voor hoge beschikbaarheid en herstel na noodgevallen.

## <a name="architecture"></a>Architectuur

Op een hoog niveau heeft hello SAP HANA in Azure (grote exemplaren)-oplossing Hallo SAP toepassingslaag die zich in de Azure VM's en Hallo databaselaag op SAP TDI geconfigureerd hardware zich in een grote exemplaar stempel in dezelfde Azure-regio die is verbonden Hallo tooAzure IaaS.

> [!NOTE]
> U moet toodeploy Hallo SAP toepassingslaag in Hallo hetzelfde Azure-gebied als Hallo SAP DBMS laag. Deze regel is goed gedocumenteerd in gepubliceerde informatie over SAP werkbelasting op Azure. 

Hallo biedt algehele architectuur van SAP HANA in Azure (grote exemplaren) een SAP TDI gecertificeerde hardware-configuratie (niet-gevirtualiseerde, bare metal, hoge prestaties server voor SAP HANA-database Hallo), en Hallo mogelijkheid en flexibiliteit van Azure tooscale bronnen voor Hallo SAP application layer toomeet uw behoeften.

![Overzicht van de architectuur van SAP HANA in Azure (grote exemplaren)](./media/hana-overview-architecture/image1-architecture.png)

Hallo-architectuur weergegeven is onderverdeeld in drie secties:

- **Rechts:** een on-premises infrastructuur met verschillende toepassingen in datacenters met eindgebruikers die LOB-toepassingen (zoals SAP) openen. In het ideale geval dit lokale infrastructuur is vervolgens verbonden tooAzure met Azure [ExpressRoute](https://azure.microsoft.com/services/expressroute/).

- **Center:** toont Azure IaaS en, in dit geval wordt het gebruik van Azure Virtual machines toohost SAP of andere toepassingen die gebruikmaken van SAP HANA als een DBMS-systeem. Kleinere HANA-exemplaren die functie met Hallo geheugen Azure VM's bieden zijn samen met hun toepassingslaag in virtuele Azure-machines geïmplementeerd. Meer informatie over [virtuele Machines](https://azure.microsoft.com/services/virtual-machines/).
<br />Azure-netwerken wordt gebruikt toogroup SAP-systemen samen met andere toepassingen in Azure virtuele netwerken (vnet's). Deze VNets verbinden tooon-premises systemen, evenals tooSAP HANA in Azure (grote exemplaren).
<br />Voor SAP NetWeaver toepassingen en databases die worden ondersteund toorun in Microsoft Azure, Zie [SAP ondersteuning Opmerking #1928533 – SAP-toepassingen in Azure: typen ondersteunde producten en de virtuele machine van Azure](https://launchpad.support.sap.com/#/notes/1928533). Controleer voor documentatie over het implementeren van SAP-oplossingen in Azure:

  -  [SAP gebruiken op Windows virtuele machines (VM's)](../../virtual-machines-windows-sap-get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
  -  [SAP-oplossingen gebruiken op Microsoft Azure virtuele machines](get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

- **Links:** toont Hallo SAP HANA TDI gecertificeerde hardware in hello Azure grote exemplaar stempel. Hallo HANA grote exemplaar eenheden zijn verbonden toohello Azure VNets van uw abonnement met Hallo dezelfde technologie als Hallo verbinding tussen lokale in Azure.

Hello Azure grote exemplaar stempel zelf combineert Hallo volgende onderdelen:

- **Berekeningen:** Servers die zijn gebaseerd op Intel Xeon E7-8890v3 of Intel Xeon E7-8890v4 processors die Hallo nodig IT de mogelijkheid en SAP HANA gecertificeerd.
- **Netwerk:** A unified snel netwerk-fabric die Hallo berekenings-, opslag- en LAN-onderdelen met elkaar verbindt.
- **Opslag:** een opslaginfrastructuur die toegankelijk is via een netwerk-infrastructuur. Specifieke opslagcapaciteit is opgegeven, afhankelijk van Hallo specifieke SAP HANA van Azure (grote exemplaren)-configuratie wordt geïmplementeerd (meer opslagcapaciteit is beschikbaar op een extra maandelijkse kosten).

In de multitenant-infrastructuur Hallo van Hallo grote exemplaar stempel, klanten geïmplementeerd als geïsoleerde tenants. Aan de implementatie van Hallo-tenant moet u tooname een Azure-abonnement binnen uw Azure-inschrijving. Dit gaat toobe hello Azure-abonnement, Hallo HANA grote exemplaren gaat toobe kosten in rekening gebracht tegen. Deze tenants hebben een relatie 1:1 toohello Azure-abonnement. Netwerk verstandig dat mogelijke tooaccess HANA grote exemplaar eenheid is geïmplementeerd in een tenant in een Azure-regio in verschillende Azure VNets die deel uitmaken van toodifferent Azure-abonnementen. Hoewel deze Azure-abonnementen toobelong toohello moeten dezelfde Azure-inschrijving. 

Net als bij Azure Virtual machines, wordt SAP HANA in Azure (grote exemplaren) aangeboden in meerdere Azure-regio's. U kunt in de volgorde toooffer herstel na noodgevallen mogelijkheden tooopt in. Andere grote exemplaar stempels binnen één geografisch politieke regio zijn verbonden tooeach andere. Bijvoorbeeld, zijn HANA grote exemplaar stempels in VS-West en VS-Oost verbonden via een speciaal netwerkkoppeling Hallo doel DR-replicatie. 

Net zoals u tussen verschillende VM typen met Azure Virtual Machines kiezen kunt, kunt u kiezen uit verschillende SKU's van HANA grote exemplaren die speciaal voor de werkbelasting van de verschillende soorten SAP HANA geschikt zijn. SAP geheugen tooprocessor socket ratio's voor verschillende werkbelastingen op basis van Hallo Intel processor generaties geldt: Er zijn vier verschillende SKU-typen die worden aangeboden:

SAP HANA in Azure (grote exemplaren) is vanaf juli 2017 beschikbaar in verschillende configuraties in hello Azure-regio's van VS-West, VS-Oost, Australië-Oost, Australië-Zuidoost, West-Europa en Noord-Europa:

| SAP-oplossing | CPU | Geheugen | Storage | Beschikbaarheid |
| --- | --- | --- | --- | --- |
| Geoptimaliseerd voor OLAP-: SAP BW, BW/4HANA<br /> of SAP HANA voor algemene OLAP-werkbelasting | SAP HANA op Azure S72<br /> – 2 x Intel Xeon®-Processor E7 8890 v3<br /> 36 CPU-kernen en 72 CPU threads |  768 GB |  3 TB | Beschikbaar |
| --- | SAP HANA op Azure S144<br /> – 4 x Intel Xeon®-Processor E7 8890 v3<br /> 72 CPU-kernen en 144 CPU threads |  1,5 TB |  6 TB | Niet beschikbaar meer |
| --- | SAP HANA op Azure S192<br /> – 4 x Intel Xeon®-Processor E7 8890 v4<br /> 96 CPU-kernen en 192 CPU threads |  2.0 TB |  8 TB | Beschikbaar |
| --- | SAP HANA op Azure S384<br /> – 8 x Intel Xeon®-Processor E7 8890 v4<br /> 192 CPU-kernen en 384 CPU threads |  4.0 TB |  16 TB | Gereed tooOrder |
| Geoptimaliseerd voor OLTP: SAP Business Suite<br /> voor SAP HANA of S/4HANA (OLTP)<br /> algemene OLTP | SAP HANA op Azure S72m<br /> – 2 x Intel Xeon®-Processor E7 8890 v3<br /> 36 CPU-kernen en 72 CPU threads |  1,5 TB |  6 TB | Beschikbaar |
|---| SAP HANA op Azure S144m<br /> – 4 x Intel Xeon®-Processor E7 8890 v3<br /> 72 CPU-kernen en 144 CPU threads |  3.0 TB |  12 TB | Niet beschikbaar meer |
|---| SAP HANA op Azure S192m<br /> – 4 x Intel Xeon®-Processor E7 8890 v4<br /> 96 CPU-kernen en 192 CPU threads  |  4.0 TB |  16 TB | Beschikbaar |
|---| SAP HANA op Azure S384m<br /> – 8 x Intel Xeon®-Processor E7 8890 v4<br /> 192 CPU-kernen en 384 CPU threads |  6.0 TB |  18 TB | Gereed tooOrder |
|---| SAP HANA op Azure S384xm<br /> – 8 x Intel Xeon®-Processor E7 8890 v4<br /> 192 CPU-kernen en 384 CPU threads |  8.0 TB |  22 TB |  Gereed tooOrder |
|---| SAP HANA op Azure S576<br /> – 12 x Intel Xeon®-Processor E7 8890 v4<br /> 288 CPU-kernen en 576 CPU threads |  12.0 TB |  28 TB | Gereed tooOrder |
|---| SAP HANA op Azure S768<br /> – 16 x Intel Xeon®-Processor E7 8890 v4<br /> 384 CPU-kernen en 768 CPU threads |  16,0 TB |  36 TB | Gereed tooOrder |
|---| SAP HANA op Azure S960<br /> – 20 x Intel Xeon®-Processor E7 8890 v4<br /> 480 CPU-kernen en 960 CPU threads |  20,0 TB |  46 TB | Gereed tooOrder |

- CPU-kernen = de som van de CPU-kernen niet-hyper-threaded van sum Hallo Hallo processors van Hallo server eenheid.
- CPU-threads = de som van de compute-threads geleverd door de CPU-kernen hyper-threaded van sum Hallo Hallo processors van Hallo server eenheid. Alle eenheden worden geconfigureerd door standaard toouse Hyper-Threading.


Hallo verschillende configuraties bovenstaande die beschikbaar zijn of zijn 'niet beschikbaar voor meer' zijn waarnaar wordt verwezen in [SAP ondersteuning Opmerking #2316233 – SAP HANA op Microsoft Azure (grote exemplaren)](https://launchpad.support.sap.com/#/notes/2316233/E). Hallo-configuraties die zijn gemarkeerd als 'Gereed tooOrder' vindt binnenkomst in Hallo SAP-notitie snel. Maar kan deze exemplaar SKU's worden besteld al voor Hallo zes verschillende Azure-regio's Hallo HANA grote exemplaar service beschikbaar is.

Hallo specifieke configuraties gekozen zijn afhankelijk van de werkbelasting, CPU-bronnen en gewenste geheugen. Het is mogelijk voor OLTP werkbelasting tooleverage Hallo SKU's die zijn geoptimaliseerd voor OLAP-werkbelasting. 

Hallo hardware voor alle Hallo aanbiedingen zijn SAP HANA TDI gecertificeerd. Echter, wordt onderscheid gemaakt tussen twee verschillende soorten hardware die wordt gedeeld Hallo-SKU's in:

- S72, S72m S144, S144m, S192 en S192m die we tooas Hallo 'Type ik klasse' verwijzen van SKU's.
- S384, S384m S384xm, S576, S768 en S960 die we verwijzen tooas Hallo Type II klasse van SKU's.

Het is belangrijk toonote dat een stempel met volledige HANA grote exemplaar uitsluitend niet is toegewezen voor één klant &#39; s gebruik. Dit feit geldt toohello rekken van berekenings- en bronnen die verbonden zijn via een netwerk fabric ook geïmplementeerd in Azure. Grote exemplaren HANA-infrastructuur, zoals Azure, implementeert u verschillende klanten &quot;tenants&quot; die zijn geïsoleerd van elkaar in Hallo na drie niveaus:

- : Netwerkisolatie via virtuele netwerken in Hallo HANA grote exemplaar stempel.
- Opslag: Isolatie door middel van opslag virtuele machines die opslagvolumes hebt toegewezen en isoleren opslagvolumes tussen de tenants.
- COMPUTE: Speciale toewijzing van de server eenheden tooa één tenant. Geen vaste of zachte partitionering van eenheden van de server. Er is geen delen van een enkele server of de hostnaam eenheid tussen de tenants. 

Als zodanig zijn Hallo implementaties van eenheden tussen verschillende tenants HANA grote instanties niet zichtbaar tooeach andere. Noch HANA grote exemplaar eenheden is geïmplementeerd in verschillende tenants kan communiceren direct met elkaar op Hallo HANA grote stempel instantieniveau. Alleen HANA grote exemplaar eenheden binnen één tenant kunnen tooeach andere op Hallo HANA grote stempel instantieniveau communiceren.
Een geïmplementeerde tenant in Hallo grote exemplaar stempel toegewezen facturering verstandig tooone Azure-abonnement. Echter, Hallo netwerk wijzen toegankelijk vanuit Azure VNets van andere Azure-abonnementen binnen dezelfde Azure-inschrijving. Als u met een andere Azure-abonnement in Hallo dezelfde implementeert Azure-regio, u kunt ook kiezen tooask voor een gescheiden grote exemplaar HANA-tenant.

Er zijn belangrijke verschillen tussen actieve SAP HANA op grote HANA-exemplaren en SAP HANA uitgevoerd op Azure Virtual machines die zijn geïmplementeerd in Azure:

- Er is geen virtualisatielaag voor SAP HANA in Azure (grote exemplaren). U ophalen Hallo prestaties van de onderliggende bare-metal hardware Hallo.
- In tegenstelling tot Azure is Hallo SAP HANA op Azure (grote exemplaren)-server toegewezen tooa specifieke klant. Er is geen mogelijkheid om een server-eenheid of de host moeilijk of soft gepartitioneerd is. Als gevolg hiervan wordt een grote HANA-exemplaar gebruikt als een hele tooa-tenant en met die tooyou als een klant die is toegewezen. Een opnieuw opstarten of afsluiten van Hallo-server leidt niet automatisch toohello-besturingssysteem en SAP HANA wordt geïmplementeerd op een andere server. (Voor het Type ik SKU's klasse, Hallo enige uitzondering hierop is als een server problemen optreden kan en opnieuw implementeren gaande toobe uitgevoerd op een andere server moet.)
- In tegenstelling tot Azure, waarmee host processortypen worden geselecteerd voor de beste prijs/prestaties verhouding Hallo, worden de typen processors Hallo gekozen voor SAP HANA in Azure (grote exemplaren) Hallo hoogste uitvoeren op de regel voor Hallo Intel E7v3 en E7v4 processor.


### <a name="running-multiple-sap-hana-instances-on-one-hana-large-instance-unit"></a>Meerdere exemplaren van de SAP HANA uitgevoerd op één grote exemplaar HANA-eenheid
Het is mogelijk toohost meer dan één actieve SAP HANA-exemplaar op Hallo HANA grote exemplaar eenheden. In volgorde bieden toostill Hallo-mogelijkheden van opslag-momentopnamen en herstel na noodgevallen in een dergelijke configuratie vereist een volume per exemplaar instellen. Vanaf nu worden Hallo HANA grote exemplaar eenheden als volgt ingedeeld:

- S72, S72m, S144, S192: In stappen van 256 GB 256 GB Hello kleinste starten eenheid. Verschillende stappen zoals 256 GB, 512 GB, enzovoort, kunnen worden gecombineerd toohello maximaal geheugen Hallo van Hallo-eenheid.
- S144m en S192m: In stappen van 256 GB met de kleinste 512 GB Hallo-eenheid. Verschillende stappen zoals 512 GB, 768 GB, enzovoort, kunnen worden gecombineerd toohello maximaal geheugen Hallo van Hallo-eenheid.
- Typ de klasse II: In stappen van 512 GB Hello kleinste eenheid van 2 TB wordt gestart. Verschillende stappen zoals 512 GB, 1 TB, 1,5 TB, enzovoort kunnen worden gecombineerd toohello maximaal geheugen Hallo van Hallo-eenheid.

Enkele voorbeelden van meerdere instanties voor SAP HANA kunnen eruitzien als:

| SKU | Geheugengrootte | Opslaggrootte | Grootten met meerdere databases |
| --- | --- | --- | --- |
| S72 | 768 GB | 3 TB | 1 x 768 GB HANA exemplaar<br /> of 1 x 512 GB exemplaar + 1 x 256 GB-exemplaar<br /> of 3 x 256 GB exemplaren | 
| S72m | 768 GB | 3 TB | 3x512GB HANA exemplaren<br />of 1 x 512 GB exemplaar + 1 x 1 TB exemplaar<br />of 6 x 256 GB exemplaren<br />of 1x1.5 TB exemplaar | 
| S192m | 4 TB | 16 TB | 8 x 512 GB exemplaren<br />of 4 x 1 TB exemplaren<br />of exemplaren van 4 x 512 GB + 2 x 1 TB exemplaren<br />of exemplaren van 4 x 768 GB + 2 x 512 GB exemplaren<br />of 1 x 4 TB-exemplaar |
| S384xm | 8 TB | 22 TB | 4 x 2 TB exemplaren<br />of 2 x 4 TB exemplaren<br />of 2 x 3 TB exemplaren + 1 x 2 TB exemplaren<br />of 2x2.5 TB exemplaren + 1 x 3 TB exemplaren<br />of 1 x 8 TB exemplaar |


U Hallo idee te krijgen. Er zijn veel andere variaties ook. 


## <a name="operations-model-and-responsibilities"></a>Operations-model en verantwoordelijkheden

Hallo-service van SAP HANA in Azure (grote exemplaren) wordt uitgelijnd met Azure IaaS-services. Krijgt u een grote exemplaren HANA-exemplaar met een geïnstalleerde besturingssysteem die is geoptimaliseerd voor SAP HANA. Is uw verantwoordelijkheid met Azure IaaS VM's, taken Hallo beperking Hallo OS, installeert aanvullende software die u nodig hebt, HANA, installeren van de meeste besturingssystemen Hallo OS en HANA en bijwerken van Hallo OS en HANA. Microsoft biedt geen OS-updates of updates HANA afdwingen op u.

![De verantwoordelijkheden van SAP HANA in Azure (grote exemplaren)](./media/hana-overview-architecture/image2-responsibilities.png)

Zoals u in de bovenstaande Hallo diagram zien kunt, is SAP HANA in Azure (grote exemplaren) een multitenant infrastructuur als een Service-aanbieding. En als gevolg hiervan Hallo-divisie van verantwoordelijkheid is op Hallo OS-infrastructuur grens voor Hallo meeste onderdeel. Microsoft is verantwoordelijk voor alle aspecten van de service onder Hallo-regel van het besturingssysteem Hallo Hallo en u bent zelf verantwoordelijk hierboven Hallo-regel, inclusief Hallo-besturingssysteem. Meest recente lokale methoden u kan worden om voor naleving, beveiliging, toepassingsbeheer, basis en OS-management kunnen dus doorgaan met toobe gebruikt. Hallo-systemen worden weergegeven alsof ze zich in uw netwerk ten opzichte van alle.

Deze service is echter wel geoptimaliseerd voor SAP HANA zodat er gebieden waar u en Microsoft toowork samen toouse Hallo onderliggende infrastructuurmogelijkheden nodig voor de beste resultaten.

Hallo volgende lijst biedt meer details over elk van de lagen Hallo en uw verantwoordelijkheden:

**Netwerken:** alle interne netwerken voor Hallo grote exemplaar stempel SAP HANA, de opslag van de toohello toegang connectiviteit tussen Hallo-exemplaren (voor scale-out en andere functies), verbinding toohello liggend en connectiviteit met Hallo tooAzure waar Hallo SAP toepassingslaag in Azure Virtual Machines wordt gehost. Dit omvat ook WAN-verbinding tussen Azure-datacenters voor herstel na noodgevallen doeleinden replicatie. Alle netwerken zijn gepartitioneerd door Hallo-tenant en QOS hebt toegepast.

**Opslag:** Hallo gevirtualiseerde gepartitioneerde opslag voor alle volumes die door Hallo SAP HANA-servers nodig, evenals voor momentopnamen. 

**Servers:** Hallo toegewezen fysieke servers toorun Hallo SAP HANA-databases tootenants toegewezen. Hallo servers Hallo Type ik klasse van SKU's zijn gescheiden hardware. Met deze typen servers, Hallo-serverconfiguratie worden verzameld en onderhouden in profielen die kunnen worden verplaatst van één fysieke hardware tooanother fysieke hardware. (Dergelijke een handmatig) verplaatsen van een profiel door bewerkingen iets kan worden vergeleken tooAzure Service herstel. Hallo servers Hallo Type II klasse SKU's zijn niet zoals een mogelijkheid bieden.

**SDDC:** Hallo-beheersoftware gebruikte toomanage gegevens wordt gecentreerd als software-gedefinieerde entiteiten. Kunt u Microsoft toopool resources voor schaal, beschikbaarheid en prestaties.

**Besturingssysteem:** Hallo OS gewenst (SUSE Linux of Red Hat Linux) die wordt uitgevoerd op Hallo-servers. Hallo OS-installatiekopieën die u zijn opgegeven door Hallo afzonderlijke Linux leverancier tooMicrosoft voor het doel van het uitvoeren van SAP HANA Hallo Hallo-installatiekopieën. U staat op het vereiste toohave een abonnement met Hallo Linux leverancier voor Hallo specifieke geoptimaliseerd voor SAP HANA-installatiekopie. Uw verantwoordelijkheden zijn Hallo afbeeldingen met Hallo OS leverancier registreren. Vanaf het punt Hallo van overdracht door Microsoft bent u ook verantwoordelijk voor eventuele verdere patchen van Hallo Linux-besturingssysteem. Deze patchen ook extra pakketten die mogelijk nodig is voor een geslaagde installatie van de SAP HANA bevat (Zie SAP-opmerkingen en documentatie voor de installatie HANA van tooSAP) en die niet zijn opgenomen Hallo leverancier met betrekking tot een specifiek Linux in hun SAP HANA installatiekopieën van het besturingssysteem wordt geoptimaliseerd. Hallo verantwoordelijkheid van de klant Hallo tevens patchen van Hallo OS gerelateerde toomalfunction/optimalisatie van Hallo OS en de stuurprogramma's gerelateerde toohello specifieke serverhardware. Of een beveiligings- of functioneel patchen van Hallo OS. De verantwoordelijkheid van klant is ook bewakings- en capaciteitsplanning van:

- Resource-CPU-verbruik
- Geheugengebruik
- Schijfruimte volumes gerelateerde toofree IOPS en latentie
- Volume van netwerkverkeer tussen HANA grote exemplaar en de toepassingslaag SAP

de onderliggende infrastructuur Hallo HANA grote exemplaren van biedt functionaliteit voor back-up en herstel van Hallo OS volume. Deze functionaliteit is ook uw eigen verantwoordelijkheid.

**Middleware:** SAP HANA-exemplaar, voornamelijk Hallo. Bent u verantwoordelijk voor beheer, bewerkingen en controle. Er is functionaliteit opgegeven waarmee u opslag-momentopnamen toouse voor back-up/herstel en herstel na noodgevallen doeleinden. Deze mogelijkheden worden geleverd door het Hallo-infrastructuur. Uw verantwoordelijkheden zijn echter ook hoge beschikbaarheid of herstel na noodgevallen ontwerpen met deze mogelijkheden, gebruik van deze, en de bewaking dat opslag-momentopnamen met succes uitgevoerd.

**Gegevens:** uw gegevens worden beheerd door een SAP HANA en andere gegevens zoals back-ups van bestanden op volumes of bestand deelt. Uw verantwoordelijkheden zijn vrije schijfruimte controleren en beheren van inhoud op Hallo volumes Hallo en de bewaking van Hallo geslaagde uitvoering van back-ups van volumes op schijven en opslag-momentopnamen. Voltooiing van uitvoering van de gegevens replicatie tooDR sites is echter Hallo verantwoordelijkheid van Microsoft.

**Toepassingen:** Hallo SAP toepassingsexemplaren of, in geval van een niet-SAP-toepassingen, de toepassingslaag Hallo van deze toepassingen. Uw verantwoordelijkheden zijn implementatie, beheer, bewerkingen en bewaking van deze toepassingen gerelateerd toocapacity planning van het verbruik van CPU, geheugengebruik, Azure Storage-verbruik en netwerkbandbreedte in Azure VNets en naar Azure VNets tooSAP HANA in Azure (grote exemplaren).

**WAN:** Hallo verbindingen u tot stand van on-premises tooAzure implementaties voor werkbelastingen brengen. Onze klanten met grote exemplaren HANA gebruik Azure ExpressRoute voor connectiviteit. Deze verbinding maakt geen deel uit van Hallo SAP HANA in Azure (grote exemplaren)-oplossing, zodat u zelf verantwoordelijk voor het Hallo-installatie van deze verbinding bent.

**Archief:** u liever met tooarchive kopieën van gegevens met behulp van uw eigen methoden in opslagaccounts. Archiveren vereist management, naleving, kosten en bewerkingen. U bent zelf verantwoordelijk voor het archiveren kopieert en back-ups op Azure genereren en opslaan in een compatibele manier.

Zie Hallo [SLA voor SAP HANA in Azure (grote exemplaren)](https://azure.microsoft.com/support/legal/sla/sap-hana-large/v1_0/).

## <a name="sizing"></a>Schaling

Sizing voor HANA grote exemplaren gaat niet anders dan in het algemeen voor HANA formaat. Voor bestaande en systemen, geïmplementeerd gewenste toomove van andere tooHANA RDBMS, SAP biedt een aantal rapporten die worden uitgevoerd op uw bestaande SAP-systemen. Als Hallo-database verplaatst tooHANA is, worden deze rapporten Hallo gegevens controleren en geheugenvereisten voor Hallo HANA exemplaar berekenen. Hallo volgende opmerkingen bij de SAP tooget meer informatie over hoe toorun deze rapporten en lezen en hoe tooobtain hun meest recente patches/versies:

- [SAP-notitie #1793345 - formaat voor SAP-Suite op HANA](https://launchpad.support.sap.com/#/notes/1793345)
- [SAP-notitie #1872170 - Suite op HANA en S/4 HANA sizing rapport](https://launchpad.support.sap.com/#/notes/1872170)
- [SAP-notitie #2121330 - Veelgestelde vragen over: SAP BW op HANA Sizing rapport](https://launchpad.support.sap.com/#/notes/2121330)
- [SAP-notitie #1736976 - schaling rapport voor BW op HANA](https://launchpad.support.sap.com/#/notes/1736976)
- [SAP-notitie #2296290 - nieuw rapport voor schaling voor BW op HANA](https://launchpad.support.sap.com/#/notes/2296290)

Voor implementaties van groen veld is snelle Sizer SAP beschikbaar toocalculate geheugenvereisten van Hallo-implementatie van SAP software bovenop HANA.

Geheugenvereisten voor HANA evenredig wanneer gegevensvolume groeit, zodat u toobe op de hoogte van Hallo geheugenverbruik nu wilt en kunnen toopredict worden wat is momenteel toobe in toekomstige Hallo. Op basis van de geheugenvereisten hello, u kunt vervolgens toe te wijzen uw vraag een Hallo HANA grote exemplaar SKU's.

## <a name="requirements"></a>Vereisten

Deze lijst samengevoegd naast de vereisten voor SAP HANA uitgevoerd op Azure (grotere exemplaren).

**Microsoft Azure:**

- Een Azure-abonnement dat kan worden gekoppeld tooSAP HANA in Azure (grote exemplaren).
- Microsoft Premier Support-Contract. Zie [SAP ondersteuning Opmerking #2015553 – SAP op Microsoft Azure: ondersteuning vereisten](https://launchpad.support.sap.com/#/notes/2015553) voor specifieke informatie gerelateerd toorunning SAP in Azure. HANA grote exemplaar eenheden met 384 en meer CPU's gebruikt, moet u ook tooextend Hallo Premier Support-contract tooinclude Azure snelle reactie (ARR).
- Bewustzijn van Hallo HANA grote exemplaren SKU's u moet na het uitvoeren van een sizing oefenen met SAP.

**Netwerkverbinding:**

- Azure ExpressRoute tussen lokale tooAzure: tooconnect uw lokale datacentrum tooAzure, zorg ervoor dat tooorder ten minste 1 Gbps verbinding van uw Internetprovider. 

**Besturingssysteem:**

- Licenties voor SUSE Linux Enterprise Server 12 voor SAP-toepassingen.

> [!NOTE] 
> Hallo besturingssysteem geleverd door Microsoft is niet geregistreerd bij SUSE, noch het met een SMT-exemplaar is verbonden.

- SUSE Linux abonnement Management Tool (SMT) geïmplementeerd in Azure op een Azure VM. Dit biedt Hallo mogelijkheid voor SAP HANA op Azure (grote exemplaren) toobe registreren en respectievelijk bijwerken door SUSE (zoals er geen internettoegang binnen grote exemplaren HANA datacenter is). 
- Licenties voor Red Hat Enterprise Linux 6.7 of 7.2 voor SAP HANA.

> [!NOTE]
> Hallo besturingssysteem geleverd door Microsoft is niet geregistreerd bij Red Hat, evenmin als it verbonden tooa Red Hat abonnement Manager-instantie.

- Red Hat abonnement Manager is geïmplementeerd in Azure op een Azure VM. Hallo Red Hat abonnement Manager biedt Hallo mogelijkheid voor SAP HANA op Azure (grote exemplaren) toobe geregistreerd en respectievelijk op Red Hat bijgewerkt (zoals er geen directe toegang tot internet vanaf binnen Hallo tenant op Hallo grote exemplaar van Azure stempel geïmplementeerd is).
- SAP, moet u toohave ondersteuning voor een contract met uw Linux-provider. Deze vereiste is niet gewist door Hallo-oplossing van grote HANA-exemplaren of Hallo fact die uw Linux uitvoeren in Azure. In tegenstelling tot met enkele van installatiekopieën van Hallo Linux Azure-galerie, is servicekosten Hallo niet opgenomen in Hallo oplossing aanbieding van grote HANA-exemplaren. Het is voor u als een klant toofulfill Hallo vereisten van SAP met betrekking tot ondersteuningscontracten met Hallo Linux distributor.   
   - Opzoeken voor SUSE Linux Hallo vereisten van ondersteuning in contract [SAP Opmerking #1984787 - SUSE LINUX Enterprise Server 12: opmerkingen bij de installatie](https://launchpad.support.sap.com/#/notes/1984787) en [SAP Opmerking #1056161 - SUSE prioriteit ondersteuning voor SAP-toepassingen](https://launchpad.support.sap.com/#/notes/1056161).
   - Red Hat Linux moet u toohave Hallo juiste abonnement niveaus met ondersteuning en service (toohello besturingssystemen HANA grote exemplaren van updates. Red Hat raadt aan om een 'RHEL voor SAP Business-toepassingen' abonnement ophalen. Controleren met betrekking tot ondersteuning en services [SAP Opmerking #2002167 - Red Hat Enterprise Linux 7.x: installatie en Upgrade](https://launchpad.support.sap.com/#/notes/2002167) en [SAP Opmerking #1496410 - Red Hat Enterprise Linux 6.x: installatie en Upgrade](https://launchpad.support.sap.com/#/notes/1496410) voor meer informatie.

**Database:**

- Licenties en software-installatie van onderdelen voor SAP HANA (platform of enterprise edition).

**Toepassingen:**

- Licenties en software-installatie van onderdelen voor alle toepassingen SAP HANA tooSAP verbinden en gerelateerde SAP ondersteuning voor contracten.
- Licenties en software-installatie-onderdelen voor alle toepassingen die niet SAP gebruikt in relatie tooSAP HANA op Azure (grote exemplaren)-omgeving en gerelateerde support-contract.

**Vaardigheden:**

- Ervaring en kennis op Azure IaaS en de bijbehorende onderdelen.
- Ervaring en kennis over het implementeren van de werkbelasting SAP in Azure.
- Gecertificeerd persoonlijke SAP HANA-installatie.
- SAP architect vaardigheden toodesign hoge beschikbaarheid en herstel na noodgevallen rond SAP HANA.

**SAP:**

- Verwachting is dat u een SAP-klant bent en een hebben contract met SAP
- Met name voor implementaties op Hallo Type II klasse van HANA grote exemplaar SKU's, is het raadzaam tooconsult met SAP op versies van SAP HANA en uiteindelijke-configuraties van groot formaat omhoog schalen-hardware.


## <a name="storage"></a>Storage

Hallo opslagindeling voor SAP HANA in Azure (grote exemplaren) wordt geconfigureerd SAP HANA op Azure Service Management via SAP aanbevolen richtlijnen, gedocumenteerd in Hallo [opslagvereisten voor SAP HANA](http://go.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html) witboek.

Hallo HANA grote exemplaren van Hallo Type ik klasse worden geleverd met vier keer Hallo geheugen volume als opslagvolume. Hallo type II klasse van grote exemplaar HANA eenheden gaat Hallo opslag niet toobe vier keer meer. Hallo eenheden worden geleverd met een volume dat bestemd is voor het opslaan van HANA transactielogboekback-ups. Meer informatie in [hoe tooinstall en SAP HANA (grote exemplaren) configureren in Azure](hana-installation.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Zie de tabel in termen van Opslagtoewijzing Hallo. Hallo tabel bevat ongeveer Hallo capaciteit voor Hallo andere volumes Hallo verschillende HANA grote exemplaar eenheden voorzien.

| HANA grote exemplaar SKU | Hana/gegevens | Hana/logboek | Hana/gedeeld | Hana/log/back-up |
| --- | --- | --- | --- | --- |
| S72 | 1280 GB | 512 GB | 768 GB | 512 GB |
| S72m | 3328 GB | 768 GB |1280 GB | 768 GB |
| S192 | 4608 GB | 1.024 GB | 1536 GB | 1.024 GB |
| S192m | 11,520 GB | 1536 GB | 1792 GB | 1536 GB |
| S384 | 11,520 GB | 1536 GB | 1792 GB | 1536 GB |
| S384m | 12.000 GB | 2050 GB | 2050 GB | 2040 GB |
| S384xm | 16.000 GB | 2050 GB | 2050 GB | 2040 GB |
| S576 | 20.000 GB | 3100 GB | 2050 GB | 3100 GB |
| S768 | 28.000 GB | 3100 GB | 2050 GB | 3100 GB |
| S960 | 36.000 GB | 4100 GB | 2050 GB | 4100 GB |


Werkelijke geïmplementeerde volumes mogelijk iets op basis van de implementatie en het hulpprogramma dat wordt gebruikt tooshow hello volumegrootten variëren.

Als u een exemplaar van HANA groot SKU onderverdelen, wordt een paar voorbeelden van mogelijke deling stukken eruit als:

| Geheugenpartitie in GB | Hana/gegevens | Hana/logboek | Hana/gedeeld | Hana/log/back-up |
| --- | --- | --- | --- | --- |
| 256 | 400 GB | 160 GB | 304 GB | 160 GB |
| 512 | 768 GB | 384 GB | 512 GB | 384 GB |
| 768 | 1280 GB | 512 GB | 768 GB | 512 GB |
| 1024 | 1792 GB | 640 GB | 1.024 GB | 640 GB |
| 1536 | 3328 GB | 768 GB | 1280 GB | 768 GB |


Deze grootten zijn ruwe volume cijfers die enigszins verschillen op basis van de implementatie verschillen kan en hulpprogramma's gebruikt toolook op Hallo volumes. Er zijn ook andere partitiegrootten thinkable zoals 2,5 TB. Deze maximale grootten zou worden berekend met een vergelijkbare formule als gebruikt voor Hallo partities hierboven. Hallo term 'partitions' betekent niet dat Hallo-besturingssysteem, geheugen of CPU-bronnen worden op elke manier gepartitioneerd. Het zojuist geeft aan dat opslag partities voor Hallo verschillende HANA exemplaren kunt u toodeploy op een enkel HANA grote exemplaar exemplaar. 

Als een klant wellicht moet u voor meer opslagruimte, hebt u Hallo mogelijkheid tooadd opslag toopurchase extra opslagruimte in eenheden van 1 TB. Deze extra opslagruimte kan worden toegevoegd als extra volume of gebruikte tooextend een of meer van de bestaande volumes Hallo kan zijn. Het is niet mogelijk toodecrease Hallo grootten van Hallo volumes zoals oorspronkelijk geïmplementeerd en voornamelijk door Hallo tabel(len) hierboven beschreven. Het is ook niet mogelijk toochange Hallo namen van Hallo volumes of mount-namen. zoals hierboven beschreven zijn Hallo opslagvolumes gekoppelde toohello HANA grote exemplaar eenheden als NFS4 volumes.

Als een klant kunt u toouse opslag-momentopnamen voor back-up/herstel en noodherstel hersteldoeleinden. Meer informatie over dit onderwerp worden beschreven in [SAP HANA (grote exemplaren) hoge beschikbaarheid en herstel na noodgevallen op Azure](hana-overview-high-availability-disaster-recovery.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

### <a name="encryption-of-data-at-rest"></a>Versleuteling van data-at-rest
Hallo-opslag gebruikt voor grote HANA-exemplaren kunnen een transparante versleuteling van Hallo gegevens zoals deze is opgeslagen op Hallo schijven. Tijdens de implementatie van een exemplaar van HANA grote eenheid hebt Hallo optie toohave dit soort versleuteling ingeschakeld. U kunt ook toochange tooencrypted volumes na al Hallo-implementatie. Hallo verplaatsen van niet-versleutelde tooencrypted volumes is transparant en vereist geen een uitvaltijd. 

Hello Type ik klasse SKU's, Hallo volume Hallo opstarten LUN is opgeslagen, worden versleuteld. In geval van een Hallo type II klasse van SKU's van HANA grote exemplaren moet u tooencrypt Hallo boot LUN met OS-methoden. 


## <a name="networking"></a>Netwerken

Hallo-architectuur van de Azure-netwerken is een belangrijk onderdeel toosuccessful-implementatie van SAP-toepassingen op grote HANA-exemplaren. SAP HANA in implementaties van Azure (grote exemplaren) hebben doorgaans een groter SAP Liggend met verschillende andere SAP-oplossingen met verschillende grootten van databases, verbruik van CPU en geheugengebruik. Waarschijnlijk zijn niet alle die SAP-systemen gebaseerd op SAP HANA, zodat uw SAP-liggend is waarschijnlijk een hybride die gebruikmaakt van:

- SAP systemen lokale geïmplementeerd. Vervaldatum tootheir grootte en kunnen niet deze systemen die momenteel worden gehost in Azure. een voorbeeld van een klassieke zou een SAP ERP productiesysteem waarop Microsoft SQL Server (als de database Hallo) waarvoor meer CPU of geheugenbronnen Azure VM's kunnen opgeven.
- SAP SAP HANA gebaseerde systemen lokale geïmplementeerd.
- Geïmplementeerde SAP-systemen in Azure VM's. Deze systemen kunnen ontwikkeling, testen, sandbox, of productie instanties voor een Hallo SAP NetWeaver gebaseerde toepassingen die met succes in Azure (op VM's) implementeren kunnen, op basis van gebruiks- en behoefte aan bronnen. Deze systemen ook kunnen worden gebaseerd op zoals SQL Server-databases (Zie [SAP ondersteuning Opmerking #1928533 – SAP-toepassingen in Azure: typen ondersteunde producten en de virtuele machine van Azure](https://launchpad.support.sap.com/#/notes/1928533/E)) of SAP HANA (Zie [SAP HANA gecertificeerd IaaS Platforms](http://global.sap.com/community/ebook/2014-09-02-hana-hardware/enEN/iaas.html)).
- SAP toepassingsservers in Azure (op VM's) die gebruikmaken van de SAP HANA in Azure (grote exemplaar) in Azure grote exemplaar stempels geïmplementeerd.

Een hybride SAP liggend (met vier of meer verschillende implementatiescenario's) is typerend, maar er zijn veel aanvragen van de klant van volledige SAP Liggend in Azure wordt uitgevoerd. Als Microsoft Azure VM's worden steeds krachtiger, wordt Hallo aantal alle oplossingen voor hun SAP verplaatst naar een Azure-klanten verhogen.

Azure-netwerken in de context Hallo van SAP-systemen die zijn geïmplementeerd in Azure is niet ingewikkeld. Deze is gebaseerd op Hallo principes van de volgende:

- Virtuele netwerken van Azure (vnet's) moeten toobe verbonden toohello Azure ExpressRoute-circuit dat tooon-premises netwerk verbindt.
- Een ExpressRoute-circuit meestal verbinding maken met on-premises tooAzure moet een bandbreedte van 1 Gbps of hoger hebben. Deze minimale bandbreedte kunt voldoende bandbreedte voor de gegevensoverdracht tussen on-premises systemen en systemen die worden uitgevoerd op Azure Virtual machines (evenals verbinding tooAzure systemen van eindgebruikers on-premises).
- Alle SAP-systemen in Azure nodig toobe instellen in toocommunicate Azure VNets met elkaar.
- Active Directory en DNS gehost lokale van on-premises worden uitgebreid naar Azure via ExpressRoute.


> [!NOTE] 
> Vanuit het facturering oogpunt alleen Eén Azure-abonnement kan één tenant alleen tooone in een grote exemplaar stempel in een specifieke Azure-regio worden gekoppeld, en als u daarentegen een enkele grote exemplaar stempel tenant kan worden gekoppeld tooone alleen Azure-abonnement. Dit is geen andere tooany andere factureerbare objecten in Azure

U implementeert SAP HANA in Azure (grote exemplaren) in meerdere verschillende Azure-regio's, resulteert in een afzonderlijke tenant toobe geïmplementeerd in Hallo grote exemplaar stempel. U kunt echter uitvoeren beide onder Hallo hetzelfde Azure-abonnement zolang deze instanties deel uitmaken van Hallo dezelfde SAP Liggend. 

> [!IMPORTANT] 
> Alleen Azure Resource Management-implementatie wordt ondersteund met SAP HANA in Azure (grote exemplaren).

 

### <a name="additional-azure-vnet-information"></a>Aanvullende informatie voor Azure VNet

In de volgorde tooconnect een Azure VNet tooExpressRoute, een Azure-gateway moet worden gemaakt (Zie [over virtuele netwerkgateways voor ExpressRoute](../../../expressroute/expressroute-about-virtual-network-gateways.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Een Azure-gateway kan worden gebruikt met ExpressRoute tooan infrastructuur buiten Azure (of tooan Azure grote exemplaar stempel) of tooconnect tussen Azure VNets (Zie [een VNet-naar-VNet-verbinding configureren voor Resource Manager, met behulp van PowerShell ](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). U kunt hello Azure-gateway tooa maximaal vier verschillende ExpressRoute-verbindingen kunt verbinden, zolang deze verbindingen afkomstig zijn uit verschillende MS Enterprise randen (MSEE)-routers.  Zie voor meer informatie [SAP HANA (grote exemplaren)-infrastructuur en de verbindingen van Azure](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 

> [!NOTE] 
> Hallo doorvoer een Azure-gateway biedt verschilt voor beide gevallen gebruikt (Zie [over VPN-Gateway](../../../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). de maximale doorvoer Hallo die we met een VNet-gateway bereiken kunt is 10 Gbps, met behulp van een ExpressRoute-verbinding. Houd er rekening mee dat het kopiëren van bestanden tussen een Azure-virtuele machine die zich in een Azure VNet en een systeem lokale (als een stream met één exemplaar) biedt Hallo volledige doorvoer van Hallo verschillende gateway-SKU's niet bereiken. tooleverage hello volledige bandbreedte van Hallo VNet gateway, moet u meerdere streams of andere bestanden kopiëren in parallelle stromen van één bestand.


### <a name="networking-architecture-for-hana-large-instances"></a>Architectuur van de netwerken voor grote HANA-exemplaren
Hallo architectuur voor grote exemplaren HANA netwerken kan zoals hieronder aangegeven, worden gescheiden in vier verschillende onderdelen:

- On-premises netwerken en een ExpressRoute-verbinding tooAzure. Dit gedeelte is Hallo klanten domein en de verbonden tooAzure via ExpressRoute. Dit is onderdeel van de Hallo Hallo rechtsonder Hallo afbeeldingen hieronder in.
- Azure Networking zo kort hierboven besproken met Azure VNets waarvoor opnieuw gateways. Dit is een gebied waar u nodig hebt toofind Hallo juiste ontwerpen voor uw vereisten voor toepassingen, beveiligings- en nalevingsvereisten. Met grote HANA-instanties is een ander punt van overweging in termen van het aantal vnet's en Azure-gateway-SKU's toochoose uit. Dit is onderdeel in de rechterbovenhoek Hallo Hallo afbeeldingen Hallo.
- Connectiviteit van grote exemplaren HANA via ExpressRoute technologie in Azure. Dit onderdeel is geïmplementeerd en uitgevoerd door Microsoft. U hoeft toodo wanneer een klant tooprovide bepaalde IP-adresbereiken worden en na de implementatie van uw assets HANA grote exemplaren verbinding Hallo Hallo ExpressRoute circuit toohello Azure VNet(s) (Zie [SAP HANA (grote exemplaren)-infrastructuur en connectiviteit op Azure](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). 
- Netwerken in grote exemplaren HANA, die voornamelijk transparant is voor u als klant.

![Azure VNet verbonden tooSAP HANA op Azure (grote exemplaren) en on-premises](./media/hana-overview-architecture/image3-on-premises-infrastructure.png)

Hallo feit dat u grote HANA exemplaren Hallo vereiste tooget uw on-premises assets die zijn verbonden via ExpressRoute tooAzure niet gewijzigd. Deze wordt ook niet Hallo vereiste voor een of meerdere VNets met hello Azure Virtual machines welke host Hallo toepassingslaag die verbinding toohello HANA exemplaren die worden gehost in grote exemplaar HANA eenheden maakt met gewijzigd. 

Hallo verschil tooSAP implementaties in pure Azure, wordt geleverd met Hallo feiten die:

- Hallo HANA grote exemplaar eenheden van de tenant van uw klant zijn verbonden via een ander ExpressRoute-circuit in uw Azure-VNet(s). In de volgorde tooseparate belastingsvoorwaarden, Hallo Hallo on-premises tooAzure VNets ExpressRoute en koppelingen tussen Azure VNets en grote HANA exemplaren delen niet dezelfde routers.
- Hallo werkbelasting profiel tussen Hallo SAP toepassingslaag en Hallo HANA exemplaar is een andere aard van veel kleine aanvragen en burst zoals gegevens (resultaatsets) vanaf SAP HANA in Hallo toepassingslaag worden overgedragen.
- Hallo SAP toepassingsarchitectuur is gevoeliger toonetwork latentie dan typische scenario's waarbij gegevens opgehaald uitgewisseld tussen on-premises en Azure.
- Hallo VNet gateway heeft ten minste twee ExpressRoute-verbindingen en beide verbindingen delen Hallo maximale bandbreedte voor binnenkomende gegevens van Hallo VNet gateway.

Hallo netwerklatentie tussen Azure VM's en grote HANA exemplaar eenheden ervaren kan hoger zijn dan een typische round trip latentie van de VM-VM-netwerk. Afhankelijk van hello Azure-regio, gemeten Hallo-waarden kunnen overschrijden Hallo 0,7 ms round trip latentie geclassificeerd zoals hieronder gemiddelde in [SAP Opmerking #1100926 - Veelgestelde vragen over: prestaties van het netwerk](https://launchpad.support.sap.com/#/notes/1100926/E). Niettemin klanten geïmplementeerd op basis van een SAP HANA SAP productietoepassingen zeer uitgevoerd op grote SAP HANA-exemplaren. Hallo-klanten die geïmplementeerd gerapporteerd verbeterd door het uitvoeren van hun SAP-toepassingen op SAP HANA HANA grote exemplaar eenheden wilt gebruiken. Niettemin moet u uw bedrijfsprocessen grondig testen in Azure HANA grote exemplaren.
 
In de volgorde tooprovide deterministische netwerklatentie tussen Azure VM's en grote exemplaar HANA is Hallo gekozen hello Azure VNet Gateway-SKU essentieel. In tegenstelling tot verkeerspatronen Hallo tussen on-premises en Azure VM's, kunt Hallo verkeer patroon tussen Azure VM's en grote exemplaren HANA kleine maar groot bursts aanvragen en-gegevens volumes toobe verzonden ontwikkelen. In de volgorde toohave dergelijke bursts verwerkt, sterk aangeraden gebruik Hallo Hallo UltraPerformance Gateway-SKU. Voor Hallo Type II klasse HANA grote exemplaar SKU, Hallo van Hallo UltraPerformance gateway SKU als Azure VNet Gateway verplicht is.  

> [!IMPORTANT] 
> Gegeven Hallo Hallo algehele netwerkverkeer tussen Hallo SAP-toepassing en lagen van de database, alleen HighPerformance of UltraPerformance gateway-SKU's voor VNets wordt ondersteund voor het verbinden van tooSAP HANA in Azure (grote exemplaren). Voor grote HANA exemplaar Type II SKU's, wordt alleen Hallo UltraPerformance Gateway-SKU als Azure VNet Gateway ondersteund.



### <a name="single-sap-system"></a>Eenmalige SAP-systeem

Hallo on-premises infrastructuur hierboven is verbonden via ExpressRoute in Azure en Hallo ExpressRoute-circuit verbindt in een Microsoft Enterprise Edge Router (MSEE) (Zie [technisch overzicht van ExpressRoute](../../../expressroute/expressroute-introduction.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Zodra die route verbinding tot stand gebracht, in de Microsoft Azure-backbone Hallo en alle Azure-regio's toegankelijk zijn.

> [!NOTE] 
> SAP landschappen in Azure wordt uitgevoerd, verbinding maken toohello MSEE dichtstbijzijnde toohello Hallo SAP liggend Azure-regio. Azure grote exemplaar stempels zijn verbonden via speciale MSEE apparaten toominimize-netwerklatentie tussen Azure-machines in Azure IaaS en grote exemplaar stempels.

Hallo VNet gateway voor hello Azure VM's die als host fungeert voor SAP toepassingsexemplaren, verbonden toothat ExpressRoute-circuit is en hello hetzelfde VNet verbonden tooa afzonderlijke MSEE Router toegewezen tooconnecting tooLarge exemplaar stempels.

Dit is een eenvoudig voorbeeld van een enkel SAP-systeem, waarbij wordt hello SAP toepassingslaag gehost in Azure en Hallo SAP HANA-database wordt uitgevoerd op SAP HANA in Azure (grote exemplaren). Hallo verondersteld wordt dat Hallo VNet gateway bandbreedte van 2 Gbps of doorvoer van 10 Gbps vertegenwoordigt een knelpunt.

### <a name="multiple-sap-systems-or-large-sap-systems"></a>Meerdere SAP-systemen of grote SAP-systemen

Als er meerdere SAP-systemen of grote SAP-systemen worden geïmplementeerd verbinden tooSAP HANA op Azure (grote exemplaren), &#39; vormen s redelijke tooassume Hallo doorvoer van Hallo VNet gateway een knelpunt. In dat geval moet u toosplit Hallo toepassingslagen in meerdere Azure VNets. Ook kan het zijn recommendable toocreate speciale VNets die verbinding maken met tooHANA grote exemplaren voor gevallen, zoals:

- NFS-shares uitvoeren van back-ups rechtstreeks vanuit Hallo HANA exemplaren in grote exemplaren HANA tooa virtuele machine in Azure die als host fungeert
- Back-ups van grote of andere bestanden kopiëren van grote exemplaar HANA eenheden toodisk ruimte die wordt beheerd in Azure.

Met behulp van afzonderlijke VNets dat host virtuele machines die Hallo opslag te beheren op het milieu op grote bestanden voorkomt of gegevensoverdracht van grote exemplaren HANA tooAzure op Hallo VNet-Gateway die Hallo virtuele machines met Hallo SAP toepassingslaag fungeert. 

Voor een meer schaalbare netwerkarchitectuur:

- Maak gebruik van meerdere Azure VNets voor een enkele, grotere SAP toepassingslaag.
- Implementeren van een afzonderlijke Azure VNet voor elk SAP-systeem geïmplementeerd, vergeleken toocombining de SAP-systemen in afzonderlijke subnetten onder Hallo hetzelfde VNet.

 Een meer schaalbare netwerkarchitectuur voor SAP HANA in Azure (grote exemplaren):

![SAP toepassingslaag over meerdere Azure VNets wordt geïmplementeerd](./media/hana-overview-architecture/image4-networking-architecture.png)

Hallo SAP toepassingslaag of onderdelen, over meerdere Azure VNets zoals hierboven, wordt geïmplementeerd onvermijdelijke latentie overhead die is opgetreden tijdens de communicatie tussen Hallo toepassingen die worden gehost in de Azure VNets geïntroduceerd. Standaard zich Hallo netwerkverkeer tussen virtuele Azure-machines in verschillende VNets doorsturen via Hallo MSEE-routers in deze configuratie. Echter sinds September 2016 kan deze routering worden geoptimaliseerd. Hallo manier toooptimize en terugdringen Hallo latentie in de communicatie tussen de twee VNets is door de peering Azure VNets binnen Hallo dezelfde regio. Zelfs als de VNets die tot verschillende abonnementen behoren. Met behulp van Azure VNet-peering, Hallo communicatie tussen VM's in twee verschillende Azure VNets kan gebruik hello Azure-netwerk-backbone toodirectly met elkaar communiceren. Waardoor gelijksoortige latentie weergeeft als Hallo virtuele machines in zou worden Hallo hetzelfde VNet. Terwijl het verkeer, IP-adresbereiken die zijn verbonden via hello Azure VNet-gateway, adressering doorgestuurd via Hallo afzonderlijke VNet gateway Hallo VNet. Krijgt u meer informatie over Azure VNet-peering in Hallo artikel [VNet-peering](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview).


### <a name="routing-in-azure"></a>Routering in Azure

Er zijn twee belangrijke netwerk aandachtspunten voor routering voor SAP HANA in Azure (grote exemplaren):

1. SAP HANA in Azure (grote exemplaren) zijn alleen toegankelijk voor virtuele Azure-machines in Hallo toegewezen ExpressRoute-verbinding. niet rechtstreeks vanuit een on-premises. Bepaalde beheerclients en alle toepassingen die directe toegang zoals SAP oplossing Manager on-premises uitgevoerd kan geen verbinding maken toohello SAP HANA-database.

2. SAP HANA op Azure (grote exemplaren) eenheden hebben een toegewezen IP-adres van Hallo servergroep IP-adres u als Hallo klant ingediende liggen (Zie [SAP HANA (grote exemplaren)-infrastructuur en de verbindingen van Azure](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) voor meer informatie).  Dit IP-adres is toegankelijk via hello Azure-abonnementen en ExpressRoute die verbinding Azure VNets tooHANA in Azure (grote exemplaren maakt). Hallo IP-adres toegewezen buiten die Server IP-adresgroepbereik rechtstreeks toohello hardware-eenheid is toegewezen en is niet NAT'ed meer dit was Hallo geval Hallo eerste implementaties van deze oplossing. 

> [!NOTE] 
> Als u tooconnect tooSAP HANA in Azure (grote exemplaren) moet een _datawarehouse_ scenario, waarin toepassingen en/of eindgebruikers moet tooconnect toohello SAP HANA-database (rechtstreeks worden uitgevoerd), moet een ander onderdeel toegang gebruikt: een reverse proxy tooroute gegevens, tooand uit. Zoals F5 BIG-IP, NGINX met Traffic Manager, geïmplementeerd in Azure als virtuele firewall/verkeer routering oplossing.

### <a name="internet-connectivity-of-hana-large-instances"></a>Verbinding met Internet van grote HANA-exemplaren
Grote exemplaren HANA hoeft geen directe verbinding met internet. Dit is uw mogelijkheden, bijvoorbeeld bij worden geregistreerd installatiekopie van het besturingssysteem Hallo rechtstreeks Hallo OS leverancier beperken. Daarom moet u mogelijk toowork bij lokale SLES SMT-server of RHEL abonnement Manager

### <a name="data-encryption-between-azure-vms-and-hana-large-instances"></a>Versleuteling van gegevens tussen Azure VM's en grote HANA-exemplaren
Gegevens die overgedragen tussen HANA grote exemplaren en Azure VM's is niet versleuteld. Alleen voor Hallo exchange tussen hello HANA DBMS kant- en op basis van ODBC-en JDBC toepassingen kunt u codering van het verkeer inschakelen. Verwijzing [deze documentatie door SAP](http://help-legacy.sap.com/saphelp_hanaplatform/helpdata/en/db/d3d887bb571014bf05ca887f897b99/content.htm?frameset=/en/dd/a2ae94bb571014a48fc3b22f8e919e/frameset.htm&current_toc=/en/de/ec02ebbb57101483bdf3194c301d2e/plain.htm&node_id=20&show_children=false)

### <a name="using-hana-large-instance-units-in-multiple-regions"></a>Gebruik HANA grote exemplaar eenheden in meerdere regio 's

U hebt mogelijk andere redenen toodeploy SAP HANA in Azure (grote exemplaren) in meerdere Azure-regio's, naast het herstel na noodgevallen. Misschien wilt u tooaccess HANA grote exemplaren van elk van de Hallo virtuele machines die zijn geïmplementeerd in Hallo verschillende VNets in Hallo regio's. Aangezien Hallo IP-adressen toegewezen toohello andere grote exemplaren HANA eenheden worden niet doorgegeven naar boven hello Azure VNets (die rechtstreeks zijn verbonden via hun toohello gatewayexemplaren), er is een kleine wijzigen toohello VNet ontwerp die hierboven zijn geïntroduceerd: een Azure VNet-gateway kan verwerken vier verschillende ExpressRoute-circuits buiten verschillende msee's en elk VNet dat is verbonden tooone Hallo grote exemplaar stempels mag verbonden toohello grote exemplaar stempel in een andere Azure-regio.

![Azure VNets verbonden tooAzure grote exemplaar stempels in verschillende Azure-regio 's](./media/hana-overview-architecture/image8-multiple-regions.png)

Hallo bovenstaande afbeelding toont hoe verschillende Azure VNets in beide Hallo gebieden zijn verbonden tootwo ander ExpressRoute-circuits die gebruikt tooconnect tooSAP HANA in Azure (grote exemplaren) in beide Azure-regio's zijn. Hallo onlangs geïntroduceerd verbindingen zijn Hallo rechthoekige rode lijnen. Met deze verbindingen buiten hello Azure VNets, Hallo VM's worden uitgevoerd in een van deze VNets toegang tot elk Hallo verschillende HANA grote exemplaren eenheden in twee gebieden Hallo geïmplementeerd. Zoals u in de bovenstaande Hallo van afbeeldingen ziet, wordt ervan uitgegaan dat u twee ExpressRoute-verbindingen van lokale toohello twee Azure-regio's hebt; aanbevolen voor herstel na noodgevallen redenen.

> [!IMPORTANT] 
> Als u meerdere ExpressRoute-circuits gebruikt, moet lokale voorkeur BGP-instellingen en AS-padtoevoeging gebruikte tooensure juiste routering van netwerkverkeer.


