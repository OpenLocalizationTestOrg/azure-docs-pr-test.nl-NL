---
title: aaaSQL patronen voor Server-toepassing op virtuele machines | Microsoft Docs
description: In dit artikel bevat informatie over application patronen voor SQL Server op Azure Virtual machines. Biedt oplossingsarchitecten en ontwikkelaars een basis voor goede toepassingsarchitectuur en het ontwerp.
services: virtual-machines-windows
documentationcenter: na
author: ninarn
manager: jhubbard
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 41863c8d-f3a3-4584-ad86-b95094365e05
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/31/2017
ms.author: ninarn
ms.openlocfilehash: e18597598fdf9fe534ed07331d6f531d4dca0601
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="application-patterns-and-development-strategies-for-sql-server-in-azure-virtual-machines"></a>Toepassingspatronen en ontwikkelingsstrategieën voor SQL Server in Azure Virtual Machines
[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="summary"></a>Overzicht:
Te bepalen welke toepassing patroon of patronen toouse voor uw toepassingen op basis van SQL-Server in Azure-omgeving is een belangrijk ontwerpbeslissing en vereist een goed begrip van hoe SQL Server en elk onderdeel van de infrastructuur van Azure samenwerken . Met SQL Server in Azure Infrastructure Services, kunt u gemakkelijk migreren, onderhouden en controleren van uw bestaande SQL Server-toepassingen gebouwd op Windows Server toovirtual machines in Azure.

Hallo-doel van dit artikel is tooprovide oplossingsarchitecten en ontwikkelaars een basis voor de goed toepassingsarchitectuur en het ontwerp, dat ze na kunnen bij het migreren van bestaande toepassingen tooAzure als goed als ontwikkelen van nieuwe toepassingen in Azure.

Voor elk patroon toepassing vindt u een lokale scenario, de respectievelijke cloud-oplossing, en Hallo gerelateerde technische aanbevelingen. Bovendien orde Hallo strategieën voor het ontwikkelen van Azure-specifieke zodat u uw toepassingen goed kunt ontwerpen. Vervaldatum toohello veel mogelijke toepassing patronen, het raadzaam dat architecten en ontwikkelaars de meest geschikte patroon Hallo voor hun toepassingen en gebruikers moeten kiezen.

**Medewerkers aan technische:** Luis Jeroen Vargas haring, Madhan Arumugam Ramakrishnan

**Technische controleurs:** Corey schuurmachines, Drew McDaniel, Narayan Annamalai, Nir Mashkowski, Sanjay Mishra, Silvano Coriani, Stefan Schackow, Tim Hickey, Tim Wieman, Xin Jin

## <a name="introduction"></a>Inleiding
Door te scheiden Hallo onderdelen van verschillende toepassingslagen Hallo op verschillende computers ook als in afzonderlijke onderdelen, kunt u verschillende soorten toepassingen n-aantal lagen ontwikkelen. Bijvoorbeeld, kunt u de clienttoepassing Hallo plaatsen en bedrijfsregels onderdelen op één computer, front-endweblaag en laag voor gegevenstoegang in een andere computer en een laag van de back-end-database in een andere computer. Dit soort structureren helpt elke laag van elkaar isoleren. Als u waar gegevens vandaan wijzigt, kunt u niet nodig toochange Hallo client of web application maar alleen Hallo-laag voor gegevenstoegang.

Een typische *n-aantal lagen* toepassing bevat presentatielaag hello, Hallo bedrijfslaag en Hallo gegevenslaag:

| Laag | Beschrijving |
| --- | --- |
| **Presentatie** |Hallo *presentatielaag* (weblaag, front-laag) Hallo laag waarin gebruikers met een toepassing werken is. |
| **Bedrijven** |Hallo *bedrijfslaag* (middelste laag) is laag Hallo die Hallo presentatie-laag en Hallo gegevens laag gebruik toocommunicate met elkaar en omvat Kernfunctionaliteit Hallo van Hallo systeem. |
| **Gegevens** |Hallo *gegevenslaag* is in feite Hallo-server die een toepassing gegevens worden opgeslagen (bijvoorbeeld een server met SQL Server). |

Toepassingslagen beschrijven Hallo logische groeperingen van Hallo functies en onderdelen in een toepassing. terwijl lagen Hallo fysieke distributie van Hallo functies en onderdelen op afzonderlijke fysieke servers, computers, netwerken of externe locaties beschrijft. Hallo lagen van een toepassing kunnen zich bevinden op Hallo dezelfde fysieke computer (Hallo dezelfde laag) of kan worden verdeeld over de afzonderlijke computers (n-laag) en Hallo componenten in elke laag communiceren met andere lagen via goed gedefinieerde interfaces-onderdelen. U kunt zien van Hallo term laag als verwijzingen toophysical distributiepatronen, zoals twee lagen en drie lagen n-aantal lagen. Een **2-tier application-patroon** bevat twee toepassingslagen: application server en database-server. Hallo rechtstreekse communicatie gebeurt tussen Hallo-toepassingsserver en Hallo-databaseserver. Hallo-toepassingsserver bevat zowel-weblaag en bedrijfslaag onderdelen. In **3-laagse toepassing patroon**, er zijn drie toepassingslagen: webserver, toepassingsserver, die Hallo zakelijke logicalaag en/of business-laag voor gegevenstoegang bevat en Hallo-databaseserver. Hallo-communicatie tussen webserver Hallo en Hallo databaseserver gebeurt via Hallo-toepassingsserver. Zie voor gedetailleerde informatie over toepassingslagen en lagen [Microsoft toepassing Architecture Guide](https://msdn.microsoft.com/library/ff650706.aspx).

Voordat u dit artikel leest, moet u informatie gegeven over de basisconcepten van SQL Server en Azure Hallo hebben. Zie voor informatie [SQL Server Books Online](https://msdn.microsoft.com/library/bb545450.aspx), [SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md) en [Azure.com](https://azure.microsoft.com/).

In dit artikel beschrijft enkele toepassing patronen die geschikt is voor uw eenvoudige toepassingen evenals Hallo zeer complexe zakelijke toepassingen kunnen zijn. Voordat u met gedetailleerde informatie over elk patroon, het is raadzaam dat u moet vertrouwd raken met Hallo beschikbare gegevens storage-services in Azure, zoals [Azure Storage](../../../storage/common/storage-introduction.md), [Azure SQL Database](../../../sql-database/sql-database-technical-overview.md), en [ SQL Server in Azure een virtuele Machine](virtual-machines-windows-sql-server-iaas-overview.md). toomake hello in de regel best ontwerpbeslissingen voor uw toepassingen begrijpen wanneer toouse welke gegevensopslag duidelijk service.

### <a name="choose-sql-server-in-an-azure-virtual-machine-when"></a>SQL Server in Azure een virtuele Machine, kiezen als:
* U moet een besturingselement in SQL Server en Windows. Dit kan bijvoorbeeld Hallo SQL Server-versie, speciale hotfixes, prestaties, configuratie, enzovoort bevatten.
* U moet een volledige compatibiliteit met SQL Server on-premises en bestaande toepassingen tooAzure als toomove wilt-is.
* U wilt tooleverage Hallo mogelijkheden van Azure-omgeving Hallo maar Azure SQL Database biedt geen ondersteuning voor alle Hallo-functies die vereist zijn voor uw toepassing. Het kan hierbij gaan Hallo gebieden te volgen:
  
  * **Databasegrootte**: gelijktijdig Hallo dit artikel is bijgewerkt, SQL Database ondersteunt een database met up too1 TB aan gegevens. Als uw toepassing meer dan 1 TB aan gegevens vereist en u niet dat tooimplement aangepaste sharding-oplossingen wilt, het raadzaam dat u SQL Server in een virtuele Machine van Azure. Zie voor de meest recente informatie Hallo [schalen uit Azure SQL-Databases](https://msdn.microsoft.com/library/azure/dn495641.aspx) en [Azure SQL Database servicecategorieën en prestatieniveaus](../../../sql-database/sql-database-service-tiers.md).
  * **HIPAA naleving**: gezondheidszorg klanten en onafhankelijke softwareleveranciers (ISV's) kunt [SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md) in plaats van [Azure SQL Database](../../../sql-database/sql-database-technical-overview.md) omdat SQL Server in een virtuele Machine van Azure is gedekt door HIPAA Business koppelen overeenkomst (BAA). Zie voor informatie over naleving, [Microsoft Azure Trust Center: naleving](https://azure.microsoft.com/support/trust-center/compliance/).
  * **Instantieniveau functies**: op dit moment functies die live buiten Hallo database biedt geen ondersteuning voor SQL-Database (zoals gekoppelde Servers Agent taken, FileStream, Service Broker, enz.). Zie voor meer informatie [Azure SQL Database richtlijnen en beperkingen](https://msdn.microsoft.com/library/azure/ff394102.aspx).

## <a name="1-tier-simple-single-virtual-machine"></a>1-laag (eenvoudig): één virtuele machine
In dit patroon toepassing implementeert u uw SQL Server-toepassing en de database tooa zelfstandige virtuele machine in Azure. Hallo bevat dezelfde virtuele machine uw client-/ webtoepassing, bedrijfsonderdelen, gegevenstoegangslaag en Hallo-databaseserver. Hallo-presentatie, zakelijke en gegevens toegangscode logisch van elkaar worden gescheiden, maar zich fysiek bevinden in een machine met één server. De meeste klanten beginnen met het patroon van deze toepassing en vervolgens zij zich uitbreiden door meer web rollen of virtuele machines tootheir system toe te voegen.

Dit patroon van toepassing is handig wanneer:

* U wilt een eenvoudige migratie tooAzure platform tooevaluate tooperform of Hallo platform van uw toepassing vereisten of niet beantwoordt.
* U wilt dat alle toepassingslagen gehost Hallo tookeep in Hallo dezelfde virtuele machine in Hallo dezelfde Azure-datacentrum tooreduce Hallo latentie tussen lagen.
* U wilt tooquickly inrichten ontwikkeling en tests omgevingen gedurende korte perioden.
* Wilt u tooperform stress testen voor verschillende werkbelastingniveaus, maar op hetzelfde moment u niet wilt tooown en onderhouden van veel fysieke machines alle Hallo tijd Hallo.

Hallo ziet volgende diagram u een eenvoudige on-premises scenario en hoe u de cloudoplossing ingeschakeld in een enkele virtuele machine in Azure kunt implementeren.

![1-tier application-patroon](./media/virtual-machines-windows-sql-server-app-patterns-dev-strategies/IC728008.png)

Hallo business laag (bedrijfslogica en data access-onderdelen) implementeren op Hallo dezelfde fysieke laag als Hallo presentatie laag kunt toepassingsprestaties, maximaliseren, tenzij u moet een afzonderlijke laag vanwege problemen tooscalability of beveiliging.

Aangezien dit een zeer gangbaar patroon toostart met, ziet u wellicht Hallo volgende artikel op de migratie is nuttig voor het verplaatsen van uw gegevens tooyour SQL Server-VM: [migreren van een Database tooSQL Server op een Azure VM](virtual-machines-windows-migrate-sql.md).

## <a name="3-tier-simple-multiple-virtual-machines"></a>3-laagse (eenvoudig): meerdere virtuele machines
In dit patroon toepassing implementeert u een 3-laagse toepassing in Azure door het plaatsen van elke toepassingslaag in een andere virtuele machine. Dit biedt een flexibele omgeving voor een eenvoudig scenario's voor scale-up en scale-out. Wanneer een virtuele machine uw client-/ webtoepassing bevat, Hallo andere als host fungeert voor de bedrijfsonderdelen van uw en andere databaseserver voor één hosts Hallo Hallo.

Dit patroon van toepassing is handig wanneer:

* Wilt u tooperform een migratie van de database voor complexe toepassingen tooAzure virtuele Machines.
* Wilt u verschillende groepen van toepassingen lagen toobe gehost in verschillende regio's. Bijvoorbeeld, kunt u gedeelde databases die geïmplementeerd toomultiple regio's zijn voor rapportagedoeleinden.
* Wilt u de bedrijfstoepassingen toomove on-premises gevirtualiseerde platforms tooAzure virtuele Machines. Zie voor een gedetailleerde bespreking van de zakelijke toepassingen, [wat is er een zakelijke toepassing](https://msdn.microsoft.com/library/aa267045.aspx).
* U wilt tooquickly inrichten ontwikkeling en tests omgevingen gedurende korte perioden.
* Wilt u tooperform stress testen voor verschillende werkbelastingniveaus, maar op hetzelfde moment u niet wilt tooown en onderhouden van veel fysieke machines alle Hallo tijd Hallo.

Hallo volgende diagram laat zien hoe u een eenvoudige 3-laagse toepassing in Azure kunt plaatsen door het plaatsen van elke toepassingslaag in een andere virtuele machine.

![3-laagse toepassing patroon](./media/virtual-machines-windows-sql-server-app-patterns-dev-strategies/IC728009.png)

In dit patroon toepassing is er slechts één virtuele machine (VM) in elke laag. Als u meerdere virtuele machines in Azure hebt, raden wij aan dat u een virtueel netwerk instellen. [Azure Virtual Network](../../../virtual-network/virtual-networks-overview.md) maakt een beveiligingsgrens vertrouwde en kunt u ook virtuele machines toocommunicate onderling via Hallo privé IP-adres. Bovendien altijd Zorg ervoor dat alle internetverbindingen alleen toohello presentatielaag gaan. Wanneer dit patroon van een toepassing te volgen, Hallo network security regels toocontrol groepstoegang beheren. Zie voor meer informatie [toestaan externe toegang tooyour virtuele machine met behulp van Azure-portal Hallo](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

In het Hallo-diagram zijn Internet-protocollen TCP, UDP, HTTP of HTTPS.

> [!NOTE]
> Instellen van een virtueel netwerk in Azure is gratis. Echter, u in rekening worden gebracht voor Hallo VPN-gateway die tooon-premises verbindt. Deze kosten is gebaseerd op Hallo hoeveelheid tijd die de verbinding ingericht en beschikbaar is.
> 
> 

## <a name="2-tier-and-3-tier-with-presentation-tier-scale-out"></a>laag 2 en 3-laagse met presentatie laag scale-out
In dit patroon toepassing kunt u database laag 2 of 3-laagse toepassing tooAzure virtuele Machines implementeren door het plaatsen van elke toepassingslaag in een andere virtuele machine. Bovendien uitschalen u Hallo presentatielaag vanwege tooincreased volume van binnenkomende aanvragen van clients.

Dit patroon van toepassing is handig wanneer:

* Wilt u de bedrijfstoepassingen toomove on-premises gevirtualiseerde platforms tooAzure virtuele Machines.
* Wilt u tooscale uit de presentatielaag Hallo vanwege tooincreased volume van binnenkomende aanvragen van clients.
* U wilt tooquickly inrichten ontwikkeling en tests omgevingen gedurende korte perioden.
* Wilt u tooperform stress testen voor verschillende werkbelastingniveaus, maar op hetzelfde moment u niet wilt tooown en onderhouden van veel fysieke machines alle Hallo tijd Hallo.
* Wilt u tooown een infrastructuur-omgeving die omhoog en omlaag op aanvraag kan worden geschaald.

Hallo volgende diagram laat zien hoe u Hallo toepassingslagen kunt plaatsen in meerdere virtuele machines in Azure door het uitbreiden van de presentatielaag Hallo vanwege tooincreased volume van binnenkomende aanvragen van clients. Zoals in Hallo diagram kunt zien, is Azure Load Balancer verantwoordelijk voor het distribueren van verkeer over meerdere virtuele machines en ook bepalen welke tooconnect web server op. Met meerdere exemplaren van de webservers Hallo achter een load balancer zorgt Hallo hoge beschikbaarheid van presentatielaag Hallo.

![Patroon toepassing - presentatie laag scale-out](./media/virtual-machines-windows-sql-server-app-patterns-dev-strategies/IC728010.png)

### <a name="best-practices-for-2-tier-3-tier-or-n-tier-patterns-that-have-multiple-vms-in-one-tier"></a>Aanbevolen procedures voor laag 2, 3-laagse of n-aantal lagen patronen die meerdere virtuele machines hebben met één laag
Het raadzaam dat u Hallo virtuele machines die deel uitmaken van dezelfde laag in Hallo dezelfde cloudservice en in dezelfde Hallo toohello plaatst Hallo beschikbaarheidsset. Bijvoorbeeld, plaatst u een reeks webservers in **CloudService1** en **AvailabilitySet1** en een set van databaseservers in **CloudService2** en **AvailabilitySet2**. Beschikbaarheidsset in Azure, kunt u tooplace Hallo hoge beschikbaarheid knooppunten in domeinen met afzonderlijke fouten en upgradedomeinen.

tooleverage meerdere VM-exemplaren van een laag, hoeft u Azure Load Balancer tooconfigure tussen de toepassingslagen. tooconfigure Load Balancer in elke laag worden afzonderlijk een eindpunt taakverdeling op virtuele machines voor elke laag maken. Voor een specifieke laag, moet u eerst virtuele machines maken in Hallo dezelfde cloudservice. Dit zorgt ervoor dat ze Hallo dezelfde openbare virtuele IP-adres. Maak vervolgens een eindpunt op een van de Hallo virtuele machines op die laag. Vervolgens Hallo toewijzen dezelfde eindpunt toohello andere virtuele machines in die laag voor taakverdeling. Door het maken van een set met gelijke taakverdeling verkeer verdelen over meerdere virtuele machines en ook de mogelijkheid Hallo Load Balancer toodetermine welke tooconnect knooppunt als een back-end-VM-knooppunt is mislukt. Bijvoorbeeld, met meerdere exemplaren van de webservers Hallo achter een load balancer zorgt u ervoor Hallo hoge beschikbaarheid van Hallo presentatielaag.

Als een best practice altijd Zorg dat alle internetverbindingen eerst toohello presentatielaag gaan. Hallo presentatie laag toegang heeft tot Hallo bedrijfslaag en benadert bedrijfslaag Hallo Hallo gegevenslaag. Zie voor meer informatie over hoe tooallow toegang krijgen tot toohello presentatie laag, [toestaan externe toegang tooyour virtuele machine met behulp van Azure-portal Hallo](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Houd er rekening mee dat Hallo Load Balancer in Azure vergelijkbare tooload balancers werkt in een on-premises omgeving. Zie voor meer informatie [taakverdeling voor Azure-infrastructuurservices](../tutorial-load-balancer.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Bovendien is het raadzaam dat u een particulier netwerk instellen voor uw virtuele machines met behulp van Azure Virtual Network. Hierdoor kunnen ze toocommunicate onderling via Hallo privé IP-adres. Zie voor meer informatie [Azure Virtual Network](../../../virtual-network/virtual-networks-overview.md).

## <a name="2-tier-and-3-tier-with-business-tier-scale-out"></a>laag 2 en 3-laagse met business laag scale-out
In dit patroon toepassing kunt u database laag 2 of 3-laagse toepassing tooAzure virtuele Machines implementeren door het plaatsen van elke toepassingslaag in een andere virtuele machine. U kunt bovendien toodistribute Hallo application server-onderdelen toomultiple virtuele machines vanwege de complexiteit van uw toepassing toohello.

Dit patroon van toepassing is handig wanneer:

* Wilt u de bedrijfstoepassingen toomove on-premises gevirtualiseerde platforms tooAzure virtuele Machines.
* U wilt toodistribute Hallo application server-onderdelen toomultiple virtuele machines vanwege toohello complexiteit van uw toepassing.
* Wilt u toomove zakelijke logica zware lokale LOB (line-of-business) toepassingen tooAzure virtuele Machines. LOB-toepassingen bestaan uit een set van essentiële toepassingen die zijn essentieel toorunning een bedrijf, zoals accounting, human resources (uur), salaris, geef keten management en resourceplanning toepassingen.
* U wilt tooquickly inrichten ontwikkeling en tests omgevingen gedurende korte perioden.
* Wilt u tooperform stress testen voor verschillende werkbelastingniveaus, maar op hetzelfde moment u niet wilt tooown en onderhouden van veel fysieke machines alle Hallo tijd Hallo.
* Wilt u tooown een infrastructuur-omgeving die omhoog en omlaag op aanvraag kan worden geschaald.

Hallo volgende diagram laat zien een lokale scenario en de cloudoplossing ingeschakeld. In dit scenario kunt u Hallo toepassingslagen in meerdere virtuele machines in Azure plaatsen door Hallo bedrijfslaag, waarin Hallo zakelijke logicalaag en data access-componenten uitbreiden. Zoals in Hallo diagram kunt zien, is Azure Load Balancer verantwoordelijk voor het distribueren van verkeer over meerdere virtuele machines en ook bepalen welke tooconnect web server op. Met meerdere exemplaren van de toepassingsservers Hallo achter een load balancer zorgt Hallo hoge beschikbaarheid van Hallo bedrijfslaag. Zie voor meer informatie [aanbevolen procedures voor laag 2, 3-laagse of n-tier application-patronen die meerdere virtuele machines hebben met één laag](#best-practices-for-2-tier-3-tier-or-n-tier-patterns-that-have-multiple-vms-in-one-tier).

![Patroon toepassing met business laag scale-out](./media/virtual-machines-windows-sql-server-app-patterns-dev-strategies/IC728011.png)

## <a name="2-tier-and-3-tier-with-presentation-and-business-tiers-scale-out-and-hadr"></a>laag 2 en 3-laagse met presentatie en zakelijke lagen scale-out en HADR
In dit patroon toepassing database laag 2 of 3-laagse toepassing tooAzure virtuele Machines implementeren met het distribueren van presentatielaag hello (webserver) en Hallo business-laag (toepassingsserver) onderdelen toomultiple virtuele machines. U kunt bovendien oplossingen voor hoge beschikbaarheid en noodherstel herstel implementeren voor uw databases in virtuele machines in Azure.

Dit patroon van toepassing is handig wanneer:

* Wilt u de bedrijfstoepassingen toomove van gevirtualiseerde platforms lokale tooAzure door het implementeren van SQL Server hoge beschikbaarheid en noodherstel herstelfuncties.
* Wilt u tooscale Hallo presentatielaag en de bedrijfslaag Hallo vervaldatum tooincreased volume van binnenkomende aanvragen van clients en complexiteit van uw toepassing hello.
* U wilt tooquickly inrichten ontwikkeling en tests omgevingen gedurende korte perioden.
* Wilt u tooperform stress testen voor verschillende werkbelastingniveaus, maar op hetzelfde moment u niet wilt tooown en onderhouden van veel fysieke machines alle Hallo tijd Hallo.
* Wilt u tooown een infrastructuur-omgeving die omhoog en omlaag op aanvraag kan worden geschaald.

Hallo volgende diagram laat zien een lokale scenario en de cloudoplossing ingeschakeld. In dit scenario dat u uitschalen Hallo presentatielaag en Hallo bedrijfsonderdelen laag in meerdere virtuele machines in Azure. U kunt bovendien hoge beschikbaarheid en disaster recovery (HADR) technieken voor SQL Server-databases implementeren in Azure.

Virtuele machines Zorg met meerdere exemplaren van een toepassing in verschillende ervoor dat u aanvragen voor taakverdeling over ze. Wanneer u meerdere virtuele machines hebt, moet u ervoor dat alle virtuele machines toegankelijk zijn en worden uitgevoerd op een punt in tijd toomake. Als u taakverdeling configureert, wordt Azure Load Balancer houdt Hallo status van virtuele machines en binnenkomende oproepen toohello goed functionerende VM knooppunten goed stuurt. Voor informatie over het tooset van taakverdeling van Hallo virtuele machines, Zie [taakverdeling voor Azure-infrastructuurservices](../tutorial-load-balancer.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Met meerdere exemplaren van web- en toepassingsservers achter een load balancer zorgt ervoor dat hoge beschikbaarheid Hallo Hallo presentatie en lagen.

![Scale-out en hoge beschikbaarheid](./media/virtual-machines-windows-sql-server-app-patterns-dev-strategies/IC728012.png)

### <a name="best-practices-for-application-patterns-requiring-sql-hadr"></a>Aanbevolen procedures voor de toepassing patronen SQL HADR vereisen
Bij het instellen van hoge beschikbaarheid van SQL Server en oplossingen voor herstel na noodgevallen in Azure Virtual Machines, instellen van een virtueel netwerk voor uw virtuele machines met [Azure Virtual Network](../../../virtual-network/virtual-networks-overview.md) is verplicht.  Virtuele machines binnen een virtueel netwerk heeft een stabiele privé IP-adres ook na de uitvaltijd van een service, dus u kunt voorkomen dat Hallo updatetijd die nodig is voor DNS-naamomzetting. Bovendien Hallo virtueel netwerk kunt u tooextend uw on-premises netwerk tooAzure en maakt een beveiligingsgrens vertrouwd. Bijvoorbeeld, als uw toepassing heeft bedrijfsdomein beperkingen (zoals Windows-verificatie, Active Directory), instellen van [Azure Virtual Network](../../../virtual-network/virtual-networks-overview.md) nodig is.

De meeste klanten productiecode op Azure uitvoert, worden behouden van primaire en secundaire replica's in Azure.

Zie voor uitgebreide informatie en zelfstudies voor hoge beschikbaarheid en disaster recovery technieken [hoge beschikbaarheid en herstel na noodgevallen voor SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-high-availability-dr.md).

## <a name="2-tier-and-3-tier-using-azure-vms-and-cloud-services"></a>laag 2 en 3-laagse met behulp van Azure VM's en Cloudservices
In dit patroon toepassing u laag 2 of 3-laagse toepassing tooAzure implementeren met behulp van beide [Azure Cloud Services](../../../cloud-services/cloud-services-choose-me.md#tellmecs) (web- en werkrollen rollen - Platform als een Service (PaaS)) en [Azure Virtual Machines](../overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) () Infrastructuur als een Service (IaaS)). Met behulp van [Azure Cloud Services](https://azure.microsoft.com/documentation/services/cloud-services/) voor Hallo laag/business presentatielaag en SQL Server in [Azure Virtual Machines](../overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) voor Hallo gegevens laag is nuttig voor de meeste toepassingen die worden uitgevoerd op Azure. Hallo reden is dat met een compute-exemplaar met Cloud-Services biedt een eenvoudig beheer, implementatie, bewaking en scale-out.

Met Cloud Services Azure onderhoudt Hallo infrastructuur voor u, voert routineonderhoud, patches Hallo-besturingssystemen en probeert toorecover van service-en hardwarefouten. Als uw toepassing moet de scale-out, is automatische en handmatige scale-out-opties zijn beschikbaar voor uw cloudserviceproject door te verhogen of verlagen Hallo-exemplaren of virtuele machines die worden gebruikt door uw toepassing. Bovendien kunt u lokale Visual Studio toodeploy uw cloudserviceproject tooa toepassing in Azure.

Als u niet veel beheertaken tooown voor Hallo presentatie/bedrijfslaag wilt en complexe configuratie van software of Hallo besturingssysteem niet wordt vereist door uw toepassing, gebruikt u Kortom, Azure Cloud Services. Als Azure SQL Database biedt geen ondersteuning voor alle Hallo-functies die u zoekt, SQL Server gebruiken in een virtuele Machine van Azure voor Hallo gegevenslaag. Een toepassing uitvoeren op Azure Cloud Services en opslaan van gegevens in Azure Virtual Machines combineert Hallo voordelen van beide services. Zie voor een gedetailleerde vergelijking Hallo-sectie in dit onderwerp op [vergelijken ontwikkelingsstrategieën in Azure](#comparing-web-development-strategies-in-azure).

In dit patroon toepassing bevat presentatielaag Hallo een Webrol, dit is een onderdeel Cloudservices in hello Azure omgeving uitgevoerd en deze kan worden aangepast voor het programmeren van web application ondersteund door IIS en ASP.NET. Hallo-laag voor zakelijke of back-end omvat een werkrol die is een onderdeel Cloudservices in hello Azure omgeving uitgevoerd en het is nuttig voor algemene ontwikkeling en achtergrondverwerking kan uitvoeren voor een Webrol. Hallo databaselaag bevindt zich in een virtuele machine van SQL Server in Azure. Hallo communicatie tussen de presentatielaag Hallo en Hallo databaselaag gebeurt rechtstreeks of via Hallo bedrijfslaag – onderdelen voor worker-rol.

Dit patroon van toepassing is handig wanneer:

* Wilt u de bedrijfstoepassingen toomove van gevirtualiseerde platforms lokale tooAzure door het implementeren van SQL Server hoge beschikbaarheid en noodherstel herstelfuncties.
* Wilt u tooown een infrastructuur-omgeving die omhoog en omlaag op aanvraag kan worden geschaald.
* Azure SQL Database biedt geen ondersteuning voor alle Hallo-functies die uw toepassing of de database moet.
* Wilt u tooperform stress testen voor verschillende werkbelastingniveaus, maar op hetzelfde moment u niet wilt tooown en onderhouden van veel fysieke machines alle Hallo tijd Hallo.

Hallo volgende diagram laat zien een lokale scenario en de cloudoplossing ingeschakeld. In dit scenario plaatsen u Hallo presentatielaag in web-rollen, Hallo bedrijfslaag in werkrollen, maar de gegevenslaag Hallo in virtuele machines in Azure. Meerdere exemplaren van presentatielaag Hallo uitgevoerd in verschillende webrollen, zorgt u ervoor van aanvragen verdelen over tooload ertussen. Wanneer u Azure Cloud Services met Azure Virtual Machines combineert, raden we aan dat u instelt [Azure Virtual Network](../../../virtual-network/virtual-networks-overview.md) ook. Met [Azure Virtual Network](../../../virtual-network/virtual-networks-overview.md), kunt u stabiel en permanente privé IP-adressen binnen dezelfde cloudservice in Hallo Hallo cloud. Nadat u een virtueel netwerk voor uw virtuele machines definiëren en cloud services, kunnen ze starten onderling communiceren via Hallo privé IP-adres. Bovendien hebben virtuele machines en rollen in Azure web/worker Hallo dezelfde [Azure Virtual Network](../../../virtual-network/virtual-networks-overview.md) lage latentie en veiliger connectiviteit. Zie voor meer informatie [wat is een cloudservice](../../../cloud-services/cloud-services-choose-me.md).

Zoals u in het diagram hello, Azure Load Balancer wordt verkeer over meerdere virtuele machines en bepaalt ook welke webserver of toepassingsserver tooconnect aan. Met meerdere exemplaren van de web- en toepassingsservers Hallo achter een load balancer zorgt Hallo hoge beschikbaarheid van Hallo presentatielaag en de bedrijfslaag Hallo. Zie voor meer informatie [Best practices voor toepassing vereisen SQL HADR patronen](#best-practices-for-application-patterns-requiring-sql-hadr).

![Toepassing van patronen met Cloudservices](./media/virtual-machines-windows-sql-server-app-patterns-dev-strategies/IC728013.png)

Een andere benadering tooimplement dit patroon van toepassing is een geconsolideerde Webrol die bevat presentatielaag en laag bedrijfsonderdelen, zoals wordt weergegeven in de volgende Hallo toouse diagram. Dit patroon van toepassing is nuttig voor toepassingen waarvoor stateful ontwerp. Omdat Azure staatloze rekenknooppunten voor web-en werkrollen bevat, het is raadzaam dat u een logische toostore sessiestatus met behulp van een van de volgende technologieën Hallo implementeren: [Azure Caching](https://azure.microsoft.com/documentation/services/redis-cache/), [Azure Table Storage](../../../cosmos-db/table-storage-how-to-use-dotnet.md) of [Azure SQL Database](../../../sql-database/sql-database-technical-overview.md).

![Toepassing van patronen met Cloudservices](./media/virtual-machines-windows-sql-server-app-patterns-dev-strategies/IC728014.png)

## <a name="pattern-with-azure-vms-azure-sql-database-and-azure-app-service-web-apps"></a>Patroon met virtuele machines in Azure, Azure SQL Database en -Azure App Service (Web-Apps)
Hallo voornaamste doel van dit patroon van toepassing is tooshow u hoe toocombine Azure-infrastructuur als een service (IaaS)-onderdelen met Azure-platform as a service onderdelen (PaaS) in uw oplossing. Dit patroon is gericht op Azure SQL Database voor relationele gegevensopslag. Dit omvat geen SQL Server in Azure een virtuele machine, die deel uitmaakt van hello Azure-infrastructuur als een serviceaanbieding.

In dit patroon toepassing implementeren van een toepassing database tooAzure door het plaatsen van Hallo presentatie en bedrijfstiers in Hallo dezelfde virtuele machine en een database in Azure SQL Database (SQL Database)-servers te openen. U kunt Hallo presentatielaag implementeren met behulp van de traditionele IIS-webservices-oplossingen. Of u kunt een samengevoegde presentatie en de bedrijfslaag implementeren met behulp van [Azure Web Apps](https://azure.microsoft.com/documentation/services/app-service/web/).

Dit patroon van toepassing is handig wanneer:

* U hebt al een bestaande SQL-Database-server geconfigureerd in Azure en u wilt tootest uw toepassing snel.
* Wilt u tootest Hallo mogelijkheden van Azure-omgeving.
* U wilt tooquickly inrichten ontwikkeling en tests omgevingen gedurende korte perioden.
* Van uw zakelijke logica en gegevens die de onderdelen van de toegang kunnen worden ingesloten in een webtoepassing.

Hallo volgende diagram laat zien een lokale scenario en de cloudoplossing ingeschakeld. In dit scenario moet u de toepassingslagen Hallo in één virtuele machine in Azure en toegang tot gegevens in Azure SQL Database plaatsen.

![Patroon van gemengde toepassing](./media/virtual-machines-windows-sql-server-app-patterns-dev-strategies/IC728015.png)

Als u ervoor kiest tooimplement een gecombineerde web- en laag met behulp van Azure Web Apps, we adviseren dat u de middelste laag of een toepassing laag Hallo als dynamic link libraries (DLL's) in de context van een webtoepassing Hallo.

Bovendien Bekijk Hallo aanbevelingen gegeven in Hallo [strategieën voor web-ontwikkeling in Azure vergelijken](#comparing-web-development-strategies-in-azure) sectie aan Hallo einde van dit artikel toolearn meer over het programmeren van technieken.

## <a name="n-tier-hybrid-application-pattern"></a>N-aantal lagen hybride toepassing patroon
In hybride n-tier application patroon, moet u uw toepassing met meerdere lagen die zijn gedistribueerd tussen on-premises en Azure implementeren. Daarom maakt u een flexibele en herbruikbare hybride-systeem die u kunt wijzigen of toevoegen zonder bepaalde laag Hallo andere laag. tooextend uw bedrijfsnetwerk toohello cloud, gebruikt u [Azure Virtual Network](../../../virtual-network/virtual-networks-overview.md) service.

Dit patroon van de toepassing hybride is handig wanneer:

* Wilt u toobuild toepassingen die deels in de cloud Hallo worden uitgevoerd en deels on-premises.
* Wilt u toomigrate enkele of alle elementen van een bestaande lokale toepassing toohello cloud.
* Wilt u de bedrijfstoepassingen toomove van lokale gevirtualiseerd platforms tooAzure.
* Wilt u tooown een infrastructuur-omgeving die omhoog en omlaag op aanvraag kan worden geschaald.
* U wilt tooquickly inrichten ontwikkeling en tests omgevingen gedurende korte perioden.
* U wilt een goedkope manier tootake back-ups voor bedrijfstoepassingen in de database.

Hallo volgende diagram ziet u een patroon met lagen hybride toepassing die zich over on-premises en Azure. Zoals u in het diagram hello, lokale infrastructuur omvat [Active Directory Domain Services](https://technet.microsoft.com/library/hh831484.aspx) domain controller toosupport gebruikersverificatie en autorisatie. Houd er rekening mee dat Hallo diagram toont een scenario waarin bepaalde onderdelen van de gegevenslaag Hallo bevinden zich in een on-premises datacenter dat sommige onderdelen van de gegevenslaag Hallo live in Azure. Afhankelijk van de behoeften van uw toepassing, kunt u verschillende andere hybride scenario's implementeren. U kan bijvoorbeeld Hallo presentatielaag en de bedrijfslaag Hallo bewaren in een lokale omgeving maar Hallo gegevenslaag in Azure.

![N-tier application-patroon](./media/virtual-machines-windows-sql-server-app-patterns-dev-strategies/IC728016.png)

In Azure, kunt u Active Directory gebruiken als een zelfstandige cloud-map voor uw organisatie, of u kunt ook integreren met bestaande op de lokale Active Directory met [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/). Zoals u in het diagram hello, Hallo laag bedrijfsonderdelen kunnen toegang krijgen tot toomultiple gegevensbronnen, zoals te[SQL-Server in Azure](virtual-machines-windows-sql-server-iaas-overview.md) via persoonlijke interne IP-adres, tooon lokale SQL Server via [Azure Virtual Network](../../../virtual-network/virtual-networks-overview.md), of te[SQL-Database](../../../sql-database/sql-database-technical-overview.md) met behulp van Hallo .NET Framework data provider-technologieën. In dit diagram is Azure SQL Database een optionele gegevens storage-service.

In hybride n-tier application patroon, kunt u Hallo werkstroom in de opgegeven Hallo volgorde na implementeren:

1. Enterprise databasetoepassingen die toobe verplaatst van toocloud moeten met behulp van Hallo identificeren [Microsoft Assessment and Planning (MAP) Toolkit](http://microsoft.com/map). Hallo MAP Toolkit verzamelt inventaris-en prestatiegegevens van computers die u voor virtualisatie overweegt en aanbevelingen biedt over capaciteit en evaluatie planning.
2. Plan Hallo resources en de configuratie is vereist in hello Azure-platform, zoals virtuele machines en opslagaccounts.
3. Instellen van de netwerkverbinding tussen Hallo bedrijfsnetwerk on-premises en [Azure Virtual Network](../../../virtual-network/virtual-networks-overview.md). tooset Hallo-verbinding tussen Hallo bedrijfsnetwerk on-premises en een virtuele machine in Azure, een van de volgende twee methoden hello gebruiken:
   
   1. Verbinding maken tussen on-premises en Azure via openbare eindpunten op een virtuele machine in Azure. Deze methode biedt een eenvoudige installatie en kunt u toouse SQL Server-verificatie in de virtuele machine. Bovendien instellen van uw netwerk beveiliging groep regels toocontrol openbaar verkeer toohello VM. Zie voor meer informatie [toestaan externe toegang tooyour virtuele machine met behulp van Azure-portal Hallo](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
   2. Verbinding maken tussen on-premises en Azure via Azure virtueel particulier netwerk (VPN)-tunnel. Deze methode kunt u tooextend domein beleid tooa virtuele machine in Azure. U kunt bovendien firewallregels instellen en gebruiken van Windows-verificatie in de virtuele machine. Op dit moment ondersteunt Azure beveiligde site-naar-site VPN- en punt-naar-site VPN-verbindingen:
      
      * Met beveiligde site-naar-site-verbinding, kunt u geen netwerkverbinding tussen uw on-premises netwerk en het virtuele netwerk in Azure. Het wordt aanbevolen voor het verbinden van uw lokale gegevens center omgeving tooAzure.
      * U kunt de netwerkverbinding tussen het virtuele netwerk in Azure en de afzonderlijke computers waarop het overal maken met beveiligde punt-naar-site-verbinding. Dit is vooral aanbevolen voor ontwikkelings- en testdoeleinden.
      
      Voor meer informatie over tooconnect tooSQL-Server in Azure, Zie [verbinding maken met virtuele Machine van SQL Server op Azure tooa](virtual-machines-windows-sql-connect.md).
4. Geplande taken en waarschuwingen die back-up on-premises gegevens op een schijf van de virtuele machine in Azure instellen. Zie voor meer informatie [SQL Server-back-up en herstel met Azure Blob Storage-Service](https://msdn.microsoft.com/library/jj919148.aspx) en [back-up en herstel voor SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).
5. Afhankelijk van de behoeften van uw toepassing, kunt u een van drie gangbare scenario's te volgen Hallo implementeren:
   
   1. U kunt uw webserver, toepassingsserver en hoofdlettergevoelig gegevens in een databaseserver in Azure houden terwijl u Hallo gevoelige gegevens op de lokale behouden.
   2. U kunt uw webserver houden en toepassingsserver on-premises terwijl Hallo databaseserver in een virtuele machine in Azure.
   3. U kunt houden van uw database-server, webserver, en toepassingsserver on-premises terwijl u Databasereplica's Hallo in virtuele machines in Azure bewaren. Deze instelling kan Hallo on-premises webservers of reporting toepassingen tooaccess Hallo Databasereplica's in Azure. U kunt daarom toolower Hallo werkbelasting in een on-premises database bereiken. Het is raadzaam dat u dit scenario voor zware implementeren gelezen werkbelastingen en ontwikkeling doeleinden. Zie voor informatie over het maken van databasereplica's in Azure AlwaysOn Availability Groups op [hoge beschikbaarheid en herstel na noodgevallen voor SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-high-availability-dr.md).

## <a name="comparing-web-development-strategies-in-azure"></a>Vergelijking van strategieën voor web-ontwikkeling in Azure
tooimplement en een meerlaagse op basis van SQL Server-toepassing in Azure implementeert, kunt u een van de volgende twee methoden voor programming hello gebruiken:

* Een traditionele webserver (IIS - Internet Information Services) instellen in Azure en access-databases in SQL Server in Azure Virtual Machines.
* Implementeren en te gebruiken van een cloud service tooAzure. Controleer vervolgens of deze cloudservice toegankelijk databases in SQL Server op Azure Virtual machines. Een cloudservice kan meerdere web- en werkrollen functies bevatten.

Hallo volgende tabel bevat een vergelijking van traditionele websites ontwikkelen met Azure Cloud Services en Azure Web Apps met opzicht tooSQL Server in Azure Virtual Machines. Hallo tabel bevat Azure Web Apps, omdat deze mogelijk toouse SQL-Server in Azure VM als gegevensbron voor Azure-Web-Apps via de openbare virtuele IP-adres of de DNS-naam.

|  | Traditionele webontwikkeling in Azure Virtual Machines | Cloudservices in Azure | Webhosting met Azure-Web-Apps |
| --- | --- | --- | --- |
| **Toepassingsmigratie van on-premises** |Bestaande toepassingen als-is. |Toepassingen moeten web-en werkrollen. |Bestaande toepassingen, zoals-maar geschikt is voor ingesloten webtoepassingen en webservices waarvoor snelle schaalbaarheid. |
| **Ontwikkeling en implementatie** |Visual Studio, WebMatrix, Visual Web Developer, Web Deploy, FTP, TFS, IIS-beheer, PowerShell. |Visual Studio, Azure SDK, TFS, PowerShell. Elke cloudservice heeft twee omgevingen toowhich implementeren van uw servicepakket en -configuratie: fasering en productie. U kunt een cloud service toohello staging-omgeving tootest implementeren voordat u deze tooproduction promoveert. |Visual Studio, WebMatrix, Visual Web Developer, FTP, GIT, BitBucket, CodePlex, DropBox, GitHub, volgt, TFS, Web implementeert, PowerShell. |
| **Beheer en Setup** |U bent zelf verantwoordelijk voor beheertaken op Hallo toepassing, gegevens, firewall-regels, virtueel netwerk en besturingssysteem. |U bent zelf verantwoordelijk voor beheertaken op Hallo toepassing, gegevens, firewall-regels en virtueel netwerk. |U bent zelf verantwoordelijk voor beheertaken op Hallo toepassings- en alleen. |
| **Hoge beschikbaarheid en herstel na noodgevallen (HADR)** |Het is raadzaam plaats te maken van virtuele machines in Hallo dezelfde beschikbaarheid instellen en Hallo in dezelfde cloudservice. Behouden van uw virtuele machines in dezelfde Hallo beschikbaarheidsset kan Azure tooplace Hallo hoge beschikbaarheid knooppunten in domeinen met afzonderlijke fouten en upgradedomeinen. Op deze manier te houden van uw virtuele machines in Hallo dezelfde cloudservice maakt taakverdeling en virtuele machines met elkaar kunnen communiceren via lokale netwerk Hallo binnen een Azure-Datacenter.<br/><br/>U bent zelf verantwoordelijk voor het implementeren van een hoge beschikbaarheid en noodherstel hersteloplossing voor SQL Server in Azure Virtual Machines tooavoid uitvaltijd. Zie voor ondersteunde HADR technologieën, [hoge beschikbaarheid en herstel na noodgevallen voor SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-high-availability-dr.md).<br/><br/>U bent zelf verantwoordelijk voor het back-ups van uw eigen gegevens en toepassingen.<br/><br/>Azure kan uw virtuele machines kunt verplaatsen als Hallo hostmachine in het datacenter Hallo vanwege toohardware problemen mislukt. Bovendien kan er geplande uitvaltijd van uw virtuele machine wanneer Hallo hostmachine wordt bijgewerkt voor beveiliging of software updates. Daarom raden we u ten minste twee virtuele machines bijhouden in elke laag tooensure Hallo continue beschikbaarheid van toepassingen. Azure biedt geen SLA voor één virtuele machine. Zie voor meer informatie [technische richtlijnen voor Azure tolerantie](../../../resiliency/resiliency-technical-guidance.md). |Hallo fouten ten gevolge van Hallo onderliggende hardware of besturingssysteem software wordt beheerd door Azure. Het is raadzaam dat u meerdere exemplaren van een web- of worker-rol tooensure Hallo hoge beschikbaarheid van uw toepassing implementeren. Zie voor informatie [Cloudservices, virtuele Machines en virtuele netwerk Service Level Agreement](http://www.microsoft.com/download/details.aspx?id=38427) en [herstel na noodgevallen en hoge beschikbaarheid voor Azure-toepassingen](../../../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md)<br/><br/>U bent zelf verantwoordelijk voor het back-ups van uw eigen gegevens en toepassingen.<br/><br/>Voor de databases die zich in een SQL Server-database in een virtuele machine in Azure, bent u verantwoordelijk voor het implementeren van een hoge beschikbaarheid en noodherstel herstel oplossing tooavoid uitvaltijd. Zie voor ondersteunde HDAR technologieën, hoge beschikbaarheid en herstel na noodgevallen voor SQL Server in Azure Virtual Machines.<br/><br/>**SQL Server Database Mirroring**: gebruik met Azure Cloud Services (web/werkrollen). SQL Server-VM's en een cloudserviceproject kunnen worden in Hallo hetzelfde virtuele Azure-netwerk. Als SQL Server VM bevindt zich niet in hetzelfde virtuele netwerk hello, moet u toocreate een exemplaar van SQL Server-Alias tooroute communicatie toohello van SQL Server. Bovendien Hallo SQL Server-naam moet overeenkomen met de aliasnaam Hallo. |Hoge beschikbaarheid is overgenomen van de Azure-werkrollen, Azure blob-opslag en Azure SQL Database. Azure Storage heeft bijvoorbeeld drie replica's van alle blob, table en queue-gegevens. Op elk gewenst moment houdt Azure SQL Database drie replica's van gegevens die worden uitgevoerd: één primaire replica en twee secundaire replica's. Zie voor meer informatie [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) en [Azure SQL Database](../../../sql-database/sql-database-technical-overview.md).<br/><br/>Wanneer u SQL Server in Azure VM als gegevensbron voor Azure Web Apps, houd er rekening mee Azure Web Apps biedt geen ondersteuning voor Azure Virtual Network. Met andere woorden, moeten alle verbindingen van Azure Web Apps tooSQL Server virtuele machines in Azure gaan via openbare eindpunten van virtuele machines. Dit kan enkele beperkingen voor hoge beschikbaarheid en herstel na noodgevallen veroorzaken. Bijvoorbeeld, zou Hallo-clienttoepassing op Azure Web Apps die gebruikmaken van tooSQL Server-VM met databasespiegeling niet kunnen tooconnect toohello nieuwe primaire server als databasespiegeling vereist het instellen van Azure Virtual Network tussen SQL Server-host-VM's in Azure. Daarom kan het gebruik **SQL Server Database Mirroring** met Azure-Web-Apps wordt momenteel niet ondersteund.<br/><br/>**SQL Server AlwaysOn-beschikbaarheidsgroepen**: U kunt AlwaysOn Availability Groups instellen bij het gebruik van Azure Web Apps met SQL Server-VM's in Azure. Maar u moet tooconfigure AlwaysOn beschikbaarheidsgroep-Listener tooroute Hallo communicatie toohello primaire replica via openbare eindpunten voor taakverdeling. |
| **cross-premises connectiviteit** |U kunt Azure Virtual Network tooconnect tooon-premises gebruiken. |U kunt Azure Virtual Network tooconnect tooon-premises gebruiken. |Virtuele Azure-netwerk wordt ondersteund. Zie voor meer informatie [Web Apps virtuele netwerkintegratie](https://azure.microsoft.com/blog/2014/09/15/azure-websites-virtual-network-integration/). |
| **Schaalbaarheid** |Scale-up is beschikbaar door de grootte van de virtuele machines Hallo verhogen of meer schijven toe te voegen. Zie voor meer informatie over de grootte van virtuele machines, [grootten van virtuele machines voor Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).<br/><br/>**Voor de databaseserver**: Scale-out is beschikbaar via de partitionering technieken database en SQL Server AlwaysOn-beschikbaarheidsgroepen.<br/><br/>Voor werkbelastingen met zware gelezen, kunt u [AlwaysOn Availability Groups](https://msdn.microsoft.com/library/hh510230.aspx) op meerdere secundaire knooppunten, evenals een SQL Server-replicatie.<br/><br/>Voor werkbelastingen zware schrijven, kunt u horizontale partitionering gegevens over meerdere fysieke servers tooprovide toepassing scale-out implementeren.<br/><br/>Bovendien kunt u een scale-out implementeren met behulp van [SQL-Server met gegevensafhankelijke routering](https://technet.microsoft.com/library/cc966448.aspx). Met gegevens afhankelijke routering (DDR), hoeft u tooimplement Hallo mechanisme in Hallo clienttoepassing, doorgaans in Hallo business laag laag partitioneren, tooroute Hallo database aanvragen toomultiple SQL Server-knooppunten. Hallo bedrijfslaag toewijzingen bevat toohow Hallo gegevens zijn gepartitioneerd en welk knooppunt Hallo gegevens bevat.<br/><br/>Toepassingen die virtuele machines worden uitgevoerd, kunnen worden geschaald. Zie voor meer informatie [hoe een toepassing tooScale](../../../cloud-services/cloud-services-how-to-scale.md).<br/><br/>**Belangrijke opmerking**: Hallo **automatisch schalen** functie in Azure kunt u tooautomatically vergroten of verkleinen van virtuele Machines die worden gebruikt door uw toepassing hello. Deze functie zorgt ervoor dat Hallo eindgebruikerservaring wordt niet negatief beïnvloed tijdens de piekuren en virtuele machines worden afgesloten wanneer Hallo-aanvraag laag is. Het verdient aanbeveling ingesteld Hallo voor automatisch schalen die optie niet voor uw cloudservice als het SQL Server-VM's bevat. Hallo is reden dat deze functie voor automatisch schalen hello Azure tooturn op een virtuele machine kunt wanneer hello CPU-gebruik in die virtuele machine is hoger dan enkele drempelwaarde en tooturn uit een virtuele machine Hallo CPU-gebruik lager is dan het gaat. Hallo-functie voor automatisch schalen is nuttig voor de staatloze toepassingen, zoals webservers, waar elke VM Hallo werkbelasting zonder eventuele verwijzingen tooany eerdere status kunt beheren. Hallo-functie voor automatisch schalen is echter niet handig voor stateful toepassingen, zoals SQL Server, waarbij slechts één exemplaar kunt toohello database schrijven. |Scale-up is beschikbaar via meerdere web- en werkrollen functies. Zie voor meer informatie over de grootte van virtuele machines voor webrollen en werkrollen [grootten configureren voor Cloud Services](../../../cloud-services/cloud-services-sizes-specs.md).<br/><br/>Wanneer u **Cloudservices**, kunt u meerdere rollen toodistribute verwerking definiëren en ook bereiken flexibel schalen van uw toepassing. Elke service in de cloud bevat een of meer webrollen en/of werkrollen, elk met een eigen toepassingsbestanden en de configuratie. Als u scale-up een cloudservice doordat Hallo aantal rolexemplaren (virtuele machines) geïmplementeerd voor een rol en omlaag schalen een cloudservice door te verlagen van het aantal rolinstanties Hallo. Zie voor gedetailleerde informatie [Azure uitvoering modellen](../../../cloud-services/cloud-services-choose-me.md).<br/><br/>Scale-out is beschikbaar via de ingebouwde Azure hoge beschikbaarheid ondersteuning via [Cloudservices, virtuele Machines en virtuele netwerk Service Level Agreement](http://www.microsoft.com/download/details.aspx?id=38427) en Load Balancer.<br/><br/>Voor een toepassing met meerdere lagen, wordt u aangeraden dat u verbinding web/worker rollen toodatabase toepassingsserver VM's via Azure Virtual Network maakt. Bovendien Azure zorgt voor taakverdeling voor virtuele machines in Hallo dezelfde cloudservice, gebruikersaanvragen verspreid over ze. Virtuele machines verbonden op deze manier kunnen rechtstreeks met elkaar communiceren via lokale netwerk Hallo binnen een Azure-Datacenter.<br/><br/>U kunt instellen **automatisch schalen** op Hallo Azure-portal, evenals Hallo planning tijden. Zie voor meer informatie [hoe tooconfigure automatisch schalen voor een Cloudservice in de portal Hallo](../../../cloud-services/cloud-services-how-to-scale-portal.md). |**Omhoog en omlaag geschaald**: U kunt vergroten/verkleinen Hallo grootte van Hallo-instantie (VM) gereserveerd voor uw website.<br/><br/>Scale-out: U kunt meer gereserveerde exemplaren (VM's) toevoegen voor uw website.<br/><br/>U kunt instellen **automatisch schalen** op Hallo-portal, evenals Hallo planning tijden. Zie voor meer informatie [hoe tooScale Web-Apps](../../../app-service-web/web-sites-scale.md). |

Zie voor meer informatie over het kiezen tussen deze programming methoden [Azure Web Apps, Cloud Services en virtuele machines: wanneer toouse die](../../../app-service-web/choose-web-site-cloud-service-vm.md).

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over het uitvoeren van SQL Server op Azure Virtual machines [SQL Server op Azure Virtual Machines Overview](virtual-machines-windows-sql-server-iaas-overview.md).

