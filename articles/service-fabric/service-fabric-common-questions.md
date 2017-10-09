---
title: aaaCommon vragen over Microsoft Azure Service Fabric | Microsoft Docs
description: Veelgestelde vragen over Service Fabric en hun antwoorden
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: 
ms.assetid: 5a179703-ff0c-4b8e-98cd-377253295d12
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: chackdan
ms.openlocfilehash: 4cbe92d2a03f7a1ea5d077807fdc982288220a7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="commonly-asked-service-fabric-questions"></a>Veelgestelde vragen over Service Fabric

Er zijn veel Veelgestelde vragen over wat Service Fabric kan doen en hoe moet worden gebruikt. Dit document bevat informatie over veel van deze Veelgestelde vragen en antwoorden.

## <a name="cluster-setup-and-management"></a>Installatie en beheer

### <a name="can-i-create-a-cluster-that-spans-multiple-azure-regions-or-my-own-datacenters"></a>Kan ik een cluster die meerdere Azure-regio's of mijn eigen datacenters omvat maken?

Ja. 

Hallo core Service Fabric-clustertechnologie mag gebruikte toocombine-machines met een willekeurige plaats in Hallo wereld zolang ze network connectivity tooeach andere hebben. Bouwen en uitvoeren van deze clusters kunnen echter wel ingewikkeld.

Als u geïnteresseerd in dit scenario bent, raden we u contact op met tooget via Hallo [Service Fabric Github lijst](https://github.com/azure/service-fabric-issues) of via uw ondersteuningsmedewerker in volgorde tooobtain aanvullende richtlijnen. Hallo Service Fabric-team werkt tooprovide extra informatie, richtlijnen en aanbevelingen in dit scenario. 

Sommige tooconsider dingen: 

1. Hallo Service Fabric-cluster-bron in Azure is vandaag de dag regionaal, omdat Hallo virtuele-machineschaalsets dat cluster Hallo is gebouwd op. Dit betekent dat in geval van een regionale fout Hallo u mogelijk Hallo mogelijkheid toomanage Hallo cluster via hello Azure Resource Manager verliezen of hello Azure-Portal. Dit kan gebeuren Hoewel Hallo cluster actief blijft en u zou kunnen toointeract ermee rechtstreeks. Bovendien biedt Azure vandaag geen Hallo mogelijkheid toohave één virtueel netwerk dat kan worden gebruikt tussen regio's. Dit betekent dat een cluster met meerdere regio in Azure een vereist [openbare IP-adressen voor elke virtuele machine in Hallo VM-Schaalsets](../virtual-machine-scale-sets/virtual-machine-scale-sets-networking.md#public-ipv4-per-virtual-machine) of [Azure VPN-Gateways](../vpn-gateway/vpn-gateway-about-vpngateways.md). Deze netwerken keuzes worden verschillende gevolgen hebben voor de kosten, prestaties en toosome mate toepassingsontwerp, dus zorgvuldig analyse en planning is vereist voordat de positie van een dergelijke omgeving.
2. Hallo onderhoud, beheer en bewaking van deze virtuele machines kunnen worden ingewikkeld, vooral wanneer spanned over verschillende _typen_ omgevingen, zoals tussen verschillende cloudproviders of tussen lokale bronnen en Azure . Wees voorzichtig tooensure dat bijwerkt, bewaking, management en diagnostische gegevens voor zowel Hallo-cluster en Hallo toepassingen voordat productieworkloads wordt uitgevoerd in een dergelijke omgeving zijn begrepen. Als u al veel ervaring voor het oplossen van deze problemen in Azure of in uw eigen datacenters, is het waarschijnlijk dat deze dezelfde oplossingen kunnen worden toegepast als samenstellen uit of uw Service Fabric-cluster wordt uitgevoerd. 

### <a name="do-service-fabric-nodes-automatically-receive-os-updates"></a>Ontvang Service Fabric-knooppunten automatisch updates voor het besturingssysteem?

Geen vandaag, maar dit is een algemene aanvraag dat Azure voornemen toodeliver heeft.

In tijdelijke hello, hebben we [opgegeven van een toepassing](service-fabric-patch-orchestration-application.md) dat besturingssystemen Hallo onder uw Service Fabric-knooppunten patches en omhoog in toodate blijven.

Hallo uitdaging met updates voor het besturingssysteem is dat ze moeten doorgaans Hallo-computer, wat tot verlies van beschikbaarheid van tijdelijke leidt opnieuw worden opgestart. Zelfstandig gebruikt, dat is niet een probleem voordoet, omdat de Service Fabric worden automatisch omgeleid verkeer voor deze services tooother knooppunten. Als updates voor het besturingssysteem niet over Hallo-cluster worden gecoördineerd, is er echter Hallo kans dat veel knooppunten tegelijk uitvallen. Dergelijke gelijktijdige herstarts kunnen leiden tot volledige beschikbaarheid verlies voor een service of op minimaal gedurende een specifieke partitie (voor een stateful service).

In toekomstige hello plant we updatebeleid toosupport een besturingssysteem die is volledig geautomatiseerd en gecoördineerd in meerdere domeinen, update, waarbij u ervoor zorgt dat beschikbaarheid behouden ondanks opnieuw wordt opgestart en andere onverwachte fouten blijft.

### <a name="can-i-use-large-virtual-machine-scale-sets-in-my-sf-cluster"></a>Kan ik grote virtuele-Machineschaalsets in mijn SF-cluster gebruiken? 

**Korte antwoord** : Nee. 

**Lang antwoord** : hoewel Hallo grote virtuele-Machineschaalsets u tooscale kunt een virtuele-machineschaalset ingesteld maximaal 1000 VM-instanties, gebeurt dat Hallo gebruik van de plaatsing groepen (PGs). Domeinen met fouten (FDs) en upgradedomeinen (UDs) zijn alleen consistent binnen een plaatsing groep Service fabric gebruikt FDs en UDs toomake plaatsing beslissingen van uw service-replica's / Service-exemplaren. Aangezien Hallo FDs en UDs vergelijkbaar zijn alleen binnen een groep plaatsing SF niet gebruiken. Bijvoorbeeld, als VM1 in PG1 een topologie van FD heeft = 0 en VM9 in PG2 heeft een topologie van FD = 4, het betekent niet dat VM1 en VM2 zich op twee verschillende Hardware rekken, daarom SF Hallo FD waarden in dit geval toomake plaatsing besluiten niet gebruiken.

Momenteel andere problemen met een grote virtuele machine-schaalsets, zoals Hallo gebrek aan niveau 4 Load balancing ondersteuning. Raadpleeg toofor [details op grote schaal sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-placement-groups.md)



### <a name="what-is-hello-minimum-size-of-a-service-fabric-cluster-why-cant-it-be-smaller"></a>Wat is de minimale grootte Hallo van een Service Fabric-cluster? Waarom kan deze niet kleiner zijn?

Hallo minimale ondersteunde grootte voor een productie-workloads met Service Fabric-cluster is vijf knooppunten. Wij ondersteunen drie clusters met knooppunten voor scenario's met ontwikkelen en testen.

Deze alle minimumwaarden bestaan omdat Hallo Service Fabric-cluster een reeks stateful systeemservices voert, waaronder de naamgevingsservice Hallo en Hallo failover manager. Deze services, bijhouden welke services zijn geïmplementeerd toohello cluster en waar ze zijn momenteel wordt gehost, afhankelijk van sterke consistentie. Hallo mogelijkheid tooacquire die sterke consistentie op zijn beurt afhankelijk een *quorum* voor een bepaalde update toohello status van die services, waarbij een quorum vertegenwoordigt een strikte meerderheid van Hallo replica's (N/2 + 1) voor een bepaalde service.

Met deze achtergrond behandeld sommige clusterconfiguraties mogelijk:

**Eén knooppunt**: deze optie biedt geen hoge beschikbaarheid, aangezien Hallo verlies van één knooppunt om welke reden Hallo Hallo verlies van het hele cluster Hallo betekent.

**Twee knooppunten**: een quorum voor een service die is geïmplementeerd op twee knooppunten (N = 2) 2 (2/2 + 1 = 2). Wanneer een enkele replica verloren gegaan is, is het onmogelijk toocreate een quorum. Omdat u een service-upgrade uitvoert tijdelijk duurt omlaag een replica vereist, maar dit is geen configuratie van een handig.

**Drie knooppunten**: met drie knooppunten (N = 3), Hallo vereiste toocreate een quorum is nog steeds twee knooppunten (3/2 + 1 = 2). Dit betekent dat u kunt een afzonderlijke knooppunten verliezen en nog steeds quorum onderhouden.

drie knooppunt Hallo-clusterconfiguratie wordt ondersteund voor ontwikkeling en testen omdat kunt u veilig uitvoeren van upgrades en fouten voor afzonderlijke knooppunten, blijven bewaard, zolang ze niet tegelijkertijd uitgevoerd. Voor productieworkloads moet u robuuste toosuch geen gelijktijdige foutstatus dus vijf knooppunten vereist zijn.

### <a name="can-i-turn-off-my-cluster-at-nightweekends-toosave-costs"></a>Kan ik mijn cluster nacht/weekends toosave kosten uitschakelen?

In het algemeen niet. Service Fabric opgeslagen status op lokale tijdelijke schijven, wat betekent dat als Hallo virtuele machine verplaatst tooa andere host is, Hallo gegevens verplaatst geen aan. In de normale werking die is niet een probleem als nieuw knooppunt Hallo toodate wordt opgeroepen door andere knooppunten. Als u alle knooppunten stoppen en deze later opnieuw opstarten, is er echter een aanzienlijke kans dat de meeste Hallo knooppunten op de nieuwe hosts starten en Hallo system niet kan toorecover.

Als u toocreate clusters dat wilt voor uw toepassing testen voordat deze is geïmplementeerd, raden wij aan dat u deze clusters dynamisch als onderdeel van maken uw [continue integratie/continue implementatie pijplijn](service-fabric-set-up-continuous-integration.md).


### <a name="how-do-i-upgrade-my-operating-system-for-example-from-windows-server-2012-toowindows-server-2016"></a>Hoe voer ik een upgrade het besturingssysteem (bijvoorbeeld van Windows Server 2012 tooWindows Server 2016)?

Terwijl we op een betere ervaring vandaag werkt, bent u verantwoordelijk voor het Hallo-upgrade. U moet upgraden Hallo OS-installatiekopie op Hallo virtuele machines Hallo één VM-cluster tegelijk. 

## <a name="container-support"></a>Container-ondersteuning

### <a name="why-are-my-containers-that-are-deployed-toosf-unable-tooresolve-dns-addresses"></a>Waarom wordt mijn containers die geïmplementeerd tooSF niet kan tooresolve DNS zijn-adressen?

Dit probleem is gerapporteerd op clusters die zich op 5.6.204.9494 versie 

**Risicobeperking** : Volg [dit document](service-fabric-dnsservice.md) tooenable Hallo DNS-service fabric-service in uw cluster.

**Los** : Upgrade tooa ondersteund cluster versie die hoger is dan 5.6.204.9494, wanneer deze beschikbaar is. Als uw cluster is ingesteld tooautomatic upgrades, wordt vervolgens Hallo cluster automatisch bijwerken toohello versie waarvoor dit probleem is opgelost.

  
## <a name="application-design"></a>Het ontwerp van toepassing

### <a name="whats-hello-best-way-tooquery-data-across-partitions-of-a-reliable-collection"></a>Wat is Hallo aanbevolen manier tooquery gegevens meerdere partities van een betrouwbare verzameling?

Betrouwbare verzamelingen zijn meestal [gepartitioneerde](service-fabric-concepts-partitioning.md) tooenable scale-out voor hogere prestaties en doorvoer. Dat betekent dat staat voor een bepaalde service Hallo kan worden verdeeld over per 10 of 100s machines. tooperform bewerkingen via die volledige gegevensset, hebt u een aantal opties:

- Maken van een service waarmee een query op alle partities van een andere service toopull in gegevens Hallo vereist.
- Maken van een service die u gegevens van alle partities van een andere service ontvangen kunt.
- Push-gegevens periodiek uit elke service tooan externe store. Deze aanpak is alleen van toepassing als Hallo-query's die u uitvoert geen deel uitmaken van uw bedrijfslogica core.


### <a name="whats-hello-best-way-tooquery-data-across-my-actors"></a>Wat is Hallo aanbevolen manier tooquery gegevens over mijn actoren?

Actors zijn ontworpen toobe onafhankelijke eenheden van de status en compute-, dus niet aanbevolen tooperform algemene query's van de actorstatus tijdens runtime. Als u een tooquery nodig over de volledige set actorstatus hello hebt, moet u overwegen een:

- Vervangen door uw actorservices betrouwbare stateful services zodat Hallo netwerk aantal aanvragen toogather voor alle gegevens van Hallo aantal actoren toohello aantal partities in uw service.
- Het ontwerpen van uw actoren tooperiodically push hun status tooan externe winkel eenvoudiger query's. Als is hierboven, deze benadering alleen levensvatbaar als Hallo-query's die u uitvoert, niet vereist voor uw runtimegedrag zijn.

### <a name="how-much-data-can-i-store-in-a-reliable-collection"></a>Hoeveel gegevens kan ik opslaan in een betrouwbare verzameling?

Betrouwbare services worden doorgaans gepartitioneerd, Hallo bedrag die kunt u opslaan wordt alleen beperkt door het aantal machines hebt u in de cluster Hallo Hallo en Hallo hoeveelheid beschikbaar geheugen op deze computers.

Stel bijvoorbeeld dat u hebt een betrouwbare verzameling in een service met 100 partities en 3 replica's voor het opslaan van objecten die 1kb groot gemiddelde. Stel nu dat u een machinecluster 10 met 16gb geheugen per computer hebt. Voor eenvoud en toobe zeer conservatief wordt ervan uitgegaan dat Hallo-besturingssystemen en systeemservices, Hallo Service Fabric-runtime en uw services 6gb, 10gb beschikbare per computer of 100gb verlaten voor Hallo-cluster gebruiken.

Houd in gedachten dat elk object moet worden opgeslagen drie tijden (een primaire en twee replica's), hebt u voldoende geheugen voor ongeveer 35 miljoen objecten in uw verzameling indien de volledige capaciteit. We raden echter aan robuuste toohello gelijktijdige verlies van een domein is mislukt en een upgradedomein, die ongeveer 1/3 capaciteit vertegenwoordigt en sneller een Hallo nummer tooroughly 23 miljoen wordt.

Houd er rekening mee dat deze berekening ook wordt ervan uitgegaan dat:

- Dat Hallo distributie van gegevens over Hallo partities min of meer uniform is of dat u load metrische gegevens toohello Cluster Resource Manager rapporteert. Standaard wordt de Service Fabric saldo op basis van het aantal replica's geladen. In het bovenstaande voorbeeld zou die 10 primaire replica's en 20 secundaire replica's op elk knooppunt in Hallo cluster plaatsen. Die geschikt is voor belasting die evenredig verdeeld over Hallo partities. Als er geen load zelfs is, moet u load melden zodat hello Resource Manager kunt pack kleinere replica's samen en grotere replica's tooconsume meer geheugen op een afzonderlijke knooppunten.

- Hallo betrouwbare service in kwestie is Hallo slechts één opslag status in Hallo-cluster. Aangezien u meerdere services tooa cluster implementeren kunt, moet u toobe Houd ook rekening met de Hallo resources dat elk toorun nodig hebt en de status te beheren.

- Hallo cluster zelf is niet groeiende of verkleinen. Als u meer machines toevoegt, Service Fabric wordt opnieuw verdelen uw replica's tooleverage Hallo extra capaciteit totdat het aantal machines Hallo overschrijdt Hallo aantal partities in uw service, omdat de replica van een afzonderlijke niet meerdere machines omvatten. Daarentegen als u Hallo Hallo cluster verkleinen door het verwijderen van computers, replica's veiliger worden ingepakt en minder algehele capaciteit.

### <a name="how-much-data-can-i-store-in-an-actor"></a>Hoeveel gegevens kan ik opslaan in een actor

Net als bij betrouwbare services wordt Hallo hoeveelheid gegevens die u kunt opslaan in een actor-service alleen beperkt door Hallo totale schijfruimte vrij en beschikbaar geheugen op Hallo-knooppunten in het cluster. Afzonderlijke actoren zijn echter meest effectief wanneer ze gebruikte tooencapsulate een kleine hoeveelheid systeemstatus- en bijbehorende bedrijfsregels in te schakelen zijn. Als in het algemeen moet een afzonderlijke actor staat dat wordt gemeten in kilobytes hebben.

## <a name="other-questions"></a>Andere vragen

### <a name="how-does-service-fabric-relate-toocontainers"></a>Service Fabric relatie toocontainers?

Containers bieden een eenvoudige manier toopackage services en de bijbehorende afhankelijkheden, zodat ze consistent worden uitgevoerd in alle omgevingen en kunnen worden uitgevoerd in een geïsoleerde wijze op een enkele computer. Service Fabric biedt een manier toodeploy en beheren van services, waaronder [services die in een container verpakt zijn](service-fabric-containers-overview.md).

### <a name="are-you-planning-tooopen-source-service-fabric"></a>Bent u van plan tooopen bron Service Fabric?

We tooopen bron Hallo reliable services en betrouwbare actoren frameworks op GitHub van plan bent en community bijdragen toothose projecten worden geaccepteerd. Volg Hallo [Service Fabric-blog](https://blogs.msdn.microsoft.com/azureservicefabric/) voor meer informatie, zoals deze wordt vermeld.

Hallo zijn momenteel geen plannen tooopen bron Hallo Service Fabric-runtime.

## <a name="next-steps"></a>Volgende stappen

- [Meer informatie over Service Fabric-kernconcepten en best practices](https://mva.microsoft.com/en-us/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tbuZM46yC_5206218965)
