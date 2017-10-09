---
title: Service Fabric-noodherstel aaaAzure | Microsoft Docs
description: Azure Service Fabric biedt Hallo mogelijkheden nodig toodeal met alle soorten noodsituaties. Dit artikel wordt beschreven Hallo typen noodsituaties die zich kunnen voordoen en hoe toodeal mee.
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 04b8348fb63e8a1c76a8f722c4c8255b339908e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-in-azure-service-fabric"></a>Herstel na noodgevallen in Azure Service Fabric
Een belangrijk onderdeel van het leveren van hoge beschikbaarheid is ervoor te zorgen dat alle soorten fouten meer services kunnen doorstaan. Dit is vooral belangrijk voor fouten die niet-geplande zijn en buiten uw beheer. Dit artikel worden enkele algemene fout modi die mogelijk noodsituaties als dat niet het gemodelleerd en correct worden beheerd. Deze oplossingen en acties tootake Bespreek ook als er een ramp toch opgetreden. Hallo-doel is toolimit of Hallo risico uitvaltijd of gegevensverlies te voorkomen wanneer ze, fouten optreden, gepland of anders optreden.

## <a name="avoiding-disaster"></a>Noodherstel voorkomen
Het voornaamste doel van de service Fabric is toohelp u zowel uw omgeving en uw services zodanig dat algemene fout typen niet noodsituaties zijn model. 

In het algemeen zijn er twee soorten na noodgevallen/mislukte scenario's:

1. Hardware of software-fouten
2. Operationele fouten

### <a name="hardware-and-software-faults"></a>Hardware en software-fouten
Hardware en software fouten zijn onvoorspelbaar. Hallo gemakkelijkste manier toosurvive fouten kan meer exemplaren van Hallo service omspannen buiten de grenzen van de fout hardware of software wordt uitgevoerd. Bijvoorbeeld, als uw service alleen op een bepaalde computer wordt uitgevoerd, is klikt u vervolgens hello mislukte van die één machine een noodgeval voor de service. Hallo op eenvoudige wijze tooavoid deze noodherstel is tooensure die Hallo service daadwerkelijk wordt uitgevoerd op meerdere machines. Testen is ook nodig tooensure Hallo uitvallen van één machine Hallo waarop service wordt uitgevoerd niet verstoren. Plannen van capaciteit zorgt ervoor dat het exemplaar van een vervanging kan worden gemaakt elders en dat vermindering van de capaciteit Hallo resterende services biedt geen overbelasting. Hallo hetzelfde patroon werkt ongeacht wat u tooavoid Hallo mislukt probeert. Bijvoorbeeld. Als u zich zorgen over Hallo falen van een SAN maakt, loopt u over meerdere SAN's. Als u zich zorgen over Hallo verlies van een rek met servers maakt, voert u via meerdere rekken. Als u Hallo verlies van datacenters twijfelt, moet uw service uitvoeren op meerdere Azure-regio's of datacenters. 

Wanneer in deze modus wordt uitgevoerd, u nog steeds onderwerp toosome typen gelijktijdige storingen, maar één en zelfs meerdere van een bepaald type (bijvoorbeeld: een enkele virtuele machine of netwerk koppeling mislukken) automatisch worden verwerkt (en dus niet langer een 'noodgeval'). Service Fabric bevat veel mechanismen voor het uitbreiden van Hallo-cluster en ingangen knooppunten en services terug te brengen. Service Fabric kunnen ook met veel exemplaren van uw services in volgorde tooavoid deze typen niet-geplande storingen uit te schakelen in echte noodsituaties.

Mogelijk zijn er redenen waarom een groot genoeg toospan implementatie uitgevoerd gedurende fouten niet haalbaar is. Bijvoorbeeld, duurt het meer hardwarebronnen dan je niet bereid toopay voor relatieve toohello kans van de fout. Tijdens het afhandelen van gedistribueerde toepassingen, kan het zijn dat aanvullende communicatie hops of status replicatie over geografische afstanden oorzaken onaanvaardbaar latentie kost. Waar deze regel wordt getekend verschilt voor elke toepassing. Voor softwarefouten in het bijzonder Hallo veroorzaakt mogelijk Hallo service dat u tooscale probeert. In dit geval voorkomen niet meer exemplaren Hallo na noodgevallen, omdat Hallo fouttoestand worden gecorreleerd over alle Hallo-exemplaren.

### <a name="operational-faults"></a>Operationele fouten
Zelfs als uw service Hallo wereld met veel redundantie upset, kan deze nog steeds rampzalig zijn gebeurtenissen optreden. Bijvoorbeeld als iemand per ongeluk Hallo DNS-naam voor de service Hallo geconfigureerd of deze rechtstreekse wordt verwijderd. Stel bijvoorbeeld moest u een stateful Service Fabric-service en iemand die service per ongeluk hebt verwijderd. Tenzij er een aantal andere risicobeperking, of de service en alle Hallo status die deze had is nu voltooid. Dit type operationele noodsituaties vereist ('Oeps') verschillende oplossingen en stappen voor herstel dan gewone niet-geplande storingen. 

Hallo aanbevolen manieren tooavoid deze typen operationele storingen zijn aan
1. operationele toegang toohello omgeving beperken
2. strikt gevaarlijke bewerkingen controleren
3. automation leggen, te voorkomen dat handmatige of buiten band wijzigingen en specifieke wijzigingen tegen Hallo werkelijke omgeving valideren voordat ze vast te stellen
4. Zorg ervoor dat destructieve operations 'soft'. Voorlopig bewerkingen onmiddellijk van kracht niet of kunnen in sommige tijdvenster ongedaan worden gemaakt

Service Fabric bevat enkele mechanismen tooprevent operationele fouten, zoals bieden [op basis van rollen](service-fabric-cluster-security-roles.md) toegangsbeheer voor bewerkingen voor een cluster. De meeste van deze operationele storingen vereisen echter organisatie inspanningen en andere systemen. Service Fabric bieden een mechanisme voor functionerende operationele fouten, met name back-up en herstel voor stateful services.

## <a name="managing-failures"></a>Het beheren van fouten
Hallo-doel van de Service Fabric is bijna altijd automatisch beheer van fouten. Echter, in volgorde toohandle bepaalde typen fouten, services moeten aanvullende code hebben. Andere typen van fouten moeten _niet_ worden automatisch opgelost redenen veiligheid en zakelijke continuïteit. 

### <a name="handling-single-failures"></a>Afhandeling van één fouten
Meerdere computers kunnen om allerlei redenen mislukken. Sommige van deze zijn oorzaken van hardware, zoals voedingen en netwerken hardwarefouten. Andere fouten zijn in software. Het gaat hierbij om fouten van Hallo van het besturingssysteem en het Hallo-service zelf. Service Fabric detecteert automatisch dergelijke fouten, met inbegrip van gevallen waarin Hallo machine geïsoleerd van andere machines vanwege toonetwork problemen wordt.

Ongeacht Hallo-type van de service, één exemplaar resultaten in uitgevoerd uitvaltijd voor de service als dat één exemplaar van Hallo code om welke reden mislukt. 

In de volgorde toohandle één enkele storing Hallo eenvoudigste wat die u kunt doen is tooensure die uw services worden uitgevoerd op meer dan één knooppunt standaard. Voor stateless services, kan dit worden bereikt door een `InstanceCount` groter is dan 1. Voor stateful services Hallo minimale aanbeveling is altijd een `TargetReplicaSetSize` en `MinReplicaSetSize` van ten minste 3. Meer kopieën van uw servicecode wordt uitgevoerd, zorgt u ervoor dat uw service automatisch één enkele storing kan verwerken. 

### <a name="handling-coordinated-failures"></a>Verwerking gecoördineerd fouten
Gecoördineerde fouten kunnen gebeuren in een cluster vervaldatum tooeither gepland of niet-geplande infrastructuur fouten en wijzigingen of wijzigingen in de geplande software. Service Fabric modellen infrastructuur-zones die gecoördineerde fouten als domeinen met fouten optreden. Gebieden die gecoördineerde softwarewijzigingen merken zijn gemodelleerd als domeinen upgraden. Meer informatie over probleem- en upgrade domeinen zich in [dit document](service-fabric-cluster-resource-manager-cluster-description.md) die beschrijft clustertopologie en definitie.

Standaard beschouwt Service Fabric-fout- en upgrade-domeinen bij het plannen waar uw services moeten worden uitgevoerd. Standaard probeert de Service Fabric tooensure die uw services worden uitgevoerd in verschillende domeinen voor probleem- en dus als gepland of ongepland wijzigingen per ongeluk uw services beschikbaar blijven. 

Stel dat dat falen van een stroombron zorgt ervoor een rek met machines toofail tegelijk dat. Hiermee schakelt u in een ander voorbeeld van een storing voor een bepaalde service met meerdere exemplaren van Hallo-service Hallo verlies van veel computers in een domein-fout veroorzaakt. Dit is daarom essentieel tooensuring hoge beschikbaarheid van uw services beheren domeinen met fouten is. Wanneer het Service Fabric in Azure wordt uitgevoerd, worden foutdomeinen automatisch beheerd. In andere omgevingen ze mogelijk niet. Als u uw eigen clusters on-premises maakt, ervoor toomap en uw domein veroorzaakt indeling onjuist plant.

Upgradedomeinen zijn handig voor het modelleren gebieden waar software gaat toobe bijgewerkt op Hallo dezelfde tijd. Als gevolg hiervan definiëren domeinen upgraden ook vaak Hallo grenzen waar software wordt offline gezet tijdens geplande upgrades. Upgrades van zowel Service Fabric en uw services Volg Hallo hetzelfde model. Zie voor meer informatie over upgrades, upgradedomeinen en Hallo Service Fabric-statusmodel die voorkomt dat onbedoelde wijzigingen die invloed hebben op Hallo-cluster en uw service rolling deze documenten:

 - [Upgrade van de toepassing](service-fabric-application-upgrade.md)
 - [Zelfstudie over Upgrade](service-fabric-application-upgrade-tutorial.md)
 - [Service Fabric-statusmodel](service-fabric-health-introduction.md)

U kunt visualiseren Hallo-indeling van het cluster met behulp van Hallo clustertoewijzing opgegeven in [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md):

<center>
![Knooppunten die zijn verdeeld over de domeinen met fouten in Service Fabric Explorer][sfx-cluster-map]
</center>

> [!NOTE]
> Modeling gebieden mislukt, rolling upgrades met veel exemplaren van uw servicecode en status, plaatsing regels tooensure uw services uitvoeren in domeinen met fouten en upgrade, en de ingebouwde statuscontrole NET **sommige** Hallo functies die Service Fabric in de volgorde tookeep normale operationele problemen en fouten uit te schakelen in noodsituaties bevat. 
>

### <a name="handling-simultaneous-hardware-or-software-failures"></a>Verwerking van gelijktijdige hardware of software-fouten
Hierboven besproken we enkele fouten. Zoals u ziet, zijn eenvoudig toohandle voor zowel stateless als stateful services alleen doordat meer exemplaren van het Hallo-code (en de status) uitvoert via domeinen met fouten en upgradedomeinen. Meerdere gelijktijdige willekeurige fouten kunnen ook gebeuren. Dit zijn vaker toolead tooan de werkelijke na noodgevallen.


### <a name="random-failures-leading-tooservice-failures"></a>Willekeurige fouten voorloopspaties tooservice fouten
Stel dat Hallo-service heeft een `InstanceCount` van 5 en verschillende knooppunten die exemplaren met alle mislukte op Hallo dezelfde tijd. Service Fabric reageert automatisch vervangen door exemplaren te maken op andere knooppunten. Vervangingen maken totdat het Hallo-service is weer terug tooits gewenst aantal exemplaren wordt voortgezet. Een ander voorbeeld: Stel dat er is een staatloze service met een `InstanceCount`van -1, wat betekent dat deze wordt uitgevoerd op alle geldige knooppunten in het Hallo-cluster. Stel dat een aantal van deze exemplaren toofail waren. In dit geval merkt Service Fabric Hallo-service is niet in de gewenste status en probeert toocreate Hallo-exemplaren op Hallo knooppunten waar ze ontbreekt zijn. 

Voor stateful services Hallo situatie is afhankelijk van of Hallo-service heeft gehandhaafd status of niet. Deze ook afhankelijk van hoeveel replica's Hallo-service heeft en hoeveel is mislukt. Bepalen of een noodgeval is opgetreden voor een stateful service bevat en het beheren van deze drie fasen:

1. Bepalen of er quorumverlies of niet is
 - Een quorumverlies is elk gewenst moment een meerderheid van Hallo replica's van een stateful service lopen Hallo hetzelfde moment, met inbegrip van Hallo primaire.
2. Bepalen of Hallo quorumverlies permanente of niet is
 - De meeste tijd hello, zijn fouten tijdelijke. Processen opnieuw zijn opgestart, opnieuw worden opgestart, virtuele machines zijn uitgebracht, retoucheren netwerkpartities. Fouten zijn soms echter permanent. 
    - Voor services zonder permanente status, een storing van een quorum of meer van de resultaten van de replica's _onmiddellijk_ permanente quorum verloren gaan. Wanneer het Service Fabric quorumverlies in een stateful service voor niet-permanente detecteert, loopt hij onmiddellijk dataloss toostep 3 door te declareren (potentiële). Procedure toodataloss zin omdat Service Fabric weet dat er geen punt in afwachting Hallo replica's toocome vorige, omdat zelfs als ze zijn hersteld, deze leeg zijn zou.
    - Een storing van een quorum of meer van de replica's voor permanente stateful services zorgt ervoor dat Service Fabric-toostart wacht op Hallo replica's toocome terug en terugzetten quorum. Dit resulteert in een onderbreking van deze service voor een _schrijft_ toohello van invloed op een partitie (of 'replicaset') van Hallo-service. Leesbewerkingen kunnen echter nog wel worden mogelijk met verminderde consistentie wordt gegarandeerd. Hallo standaardhoeveelheid tijd dat het Service Fabric quorum toobe hersteld wacht is oneindig, omdat u doorgaat een (mogelijke) dataloss gebeurtenis en andere risico's uitvoert. Hallo standaard overschrijven `QuorumLossWaitDuration` waarde is mogelijk, maar wordt niet aanbevolen. In plaats daarvan op dit moment moeten alle pogingen worden aangebracht toorestore Hallo omlaag replica's. Hiervoor moet het Hallo-knooppunten die omlaag back up te brengen, en ervoor te zorgen dat ze opnieuw kunnen koppelen Hallo stations waar ze Hallo lokale permanente status opgeslagen. Hallo quorumverlies wordt veroorzaakt door een fout, Service Fabric automatisch probeert toorecreate Hallo processen als Hallo replica's in deze opnieuw. Als dit mislukt, wordt in Service Fabric health fouten rapporteert. Als deze omgezet worden kunnen Ga Hallo replica's gewoonlijk dan terug. Soms echter niet kunnen Hallo replica's worden teruggebracht. Bijvoorbeeld, Hallo stations mogelijk alle is mislukt of Hallo machines fysiek vernietigd enigszins. In dergelijke gevallen hebben we nu een permanente quorum verlies-gebeurtenis. tootell Service Fabric toostop wachten op Hallo omlaag replica's toocome terug, Clusterbeheerder moet bepalen welke partities die services worden beïnvloed en roep Hallo `Repair-ServiceFabricPartition -PartitionId` of ` System.Fabric.FabricClient.ClusterManagementClient.RecoverPartitionAsync(Guid partitionId)` API.  Deze API kunt u opgeven Hallo partitie toomove buiten QuorumLoss en potentiële dataloss Hallo-ID.

> [!NOTE]
> Het is _nooit_ veilige toouse deze API anders dan in een bepaalde manier tegen specifieke partities. 
>

3. Bepalen of er sprake is van feitelijke gegevens verloren gaan en het terugzetten van back-ups
  - Wanneer het Service Fabric Hallo aangeroepen `OnDataLossAsync` methode altijd omdat is _vermoed_ dataloss. Service Fabric zorgt ervoor dat deze aanroep toohello wordt geleverd _aanbevolen_ resterende replica. Dit is de replica voortgang is Hallo meeste. Hallo reden we altijd spreken _vermoed_ dataloss is dat het is mogelijk alle dezelfde staat die Hallo resterende replica daadwerkelijk heeft als Hallo primaire was voordat deze werd afgesloten. Echter, zonder dat toocompare staat het, is er geen goede manier voor Service Fabric of operators tooknow controleren. Op dit moment Service Fabric weet ook Hallo andere replica's zijn niet terugkomen. Dat was Hallo beslissingen bij het wachten op Hallo quorum verlies tooresolve zelf is gestopt. Hallo oplossing komen voor Hallo-service is meestal toofreeze en wacht tot specifieke interventie van een beheerder. Dus de betekenis van een typische implementatie van Hallo `OnDataLossAsync` methode doen?
  - Meld u eerst die `OnDataLossAsync` is geactiveerd en eventuele benodigde beheerdersrechten waarschuwingen starten.
   - Meestal op dit moment toopause en wacht voor verdere beslissingen en handmatige acties toobe genomen. Dit is omdat ook als back-ups beschikbaar toobe voorbereid moeten. Bijvoorbeeld, als twee verschillende services coördineren van gegevens, mogelijk deze back-ups toobe gewijzigd in de volgorde tooensure die zodra Hallo terugzetten Hallo informatie die twee services belang gebeurt bij consistent is. 
  - Vaak is ook andere telemetrie of uitlaatgas van Hallo-service. Deze metagegevens kan zijn opgenomen in de andere services of in Logboeken. Deze informatie kan gebruikte benodigde toodetermine zijn als er aanroepen ontvangen en verwerkt op primaire Hallo niet aanwezig zijn in bepaalde Hallo back-up of gerepliceerde toothis-replica zijn. Deze wellicht toobe herhaald of toegevoegde toohello back-up voordat de herstelbewerking haalbaar is.  
   - Vergelijkingen van Hallo resterende van replica de status toothat opgenomen in alle back-ups die beschikbaar zijn. Als met betrouwbare Service Fabric-verzamelingen hello wordt er zijn extra en beschikbaar verwerkt om te doen, dat wordt beschreven in [in dit artikel](service-fabric-reliable-services-backup-restore.md). Hallo-doel is toosee als Hallo status binnen Hallo replica voldoende is of ook welke Hallo back-up ontbreekt mogelijk.
  - Eenmaal Hallo vergelijking wordt uitgevoerd, en als de benodigde Hallo terugzetten is voltooid, Hallo servicecode moet true wordt geretourneerd als er wijzigingen zijn aangebracht. Retourneert onwaar als de replica Hallo vastgesteld dat het was Hallo beste beschikbaar exemplaar van Hallo status heeft en er zijn geen wijzigingen aangebracht. Waar geeft aan dat elke _andere_ resterende replica's nu mogelijk niet door deze gegevensset. Ze zullen worden verwijderd en opnieuw opgebouwd uit deze replica. Drempelwaarde.ONWAAR geeft aan dat er geen statuswijzigingen doorgevoerd, dus Hallo andere replica's kunnen houden wat ze hebben. 

Het is zeer belangrijk dat service auteurs potentiële dataloss en scenario's fouten oefenen voordat services ooit worden geïmplementeerd in de productieomgeving. tooprotect tegen dataloss Hallo mogelijkheid is het belangrijk tooperiodically [back-up Hallo status](service-fabric-reliable-services-backup-restore.md) van elk van uw stateful services tooa geografisch redundante opslag. U moet ook voor zorgen dat er Hallo mogelijkheid toorestore deze. Aangezien de back-ups van veel verschillende services worden uitgevoerd op verschillende tijdstippen, moet u tooensure dat de uw services na een herstelbewerking een consistente weergave van elkaar hebben. Neem bijvoorbeeld een situatie waarin een service een aantal genereert en opgeslagen en vervolgens verzendt het tooanother-service waarmee gegevens worden ook opgeslagen. Na een herstelbewerking mogelijk ontdekt u dat tweede Hallo-service Hallo nummer heeft maar Hallo eerst niet bestaat, omdat de back-up die voor deze bewerking niet bevatten.

Als u dat Hallo resterende ontdekken replica's zijn onvoldoende toocontinue uit in een scenario dataloss en u kan geen servicestatus van telemetrie of uitlaatgas Reconstrueer, de best mogelijke beoogd herstelpunt (RPO) wordt bepaald door Hallo frequentie van uw back-ups . Service Fabric bevat veel hulpprogramma's voor het testen van verschillende scenario's voor mislukt, met inbegrip van permanente quorum en dataloss herstel vanaf een back-up vereisen. Deze scenario's zijn opgenomen als onderdeel van de Service Fabric testbaarheid-hulpprogramma's worden beheerd door Hallo veroorzaakt Analysis Services. Meer informatie over deze hulpprogramma's en patronen [hier](service-fabric-testability-overview.md). 

> [!NOTE]
> Systeemservices kunnen ook quorum verloren zijn gegaan, Hallo gevolgen wordt specifieke toohello service betrokken afnemen. Bijvoorbeeld quorumverlies in Hallo naamgevingsservice heeft gevolgen voor naamomzetting, terwijl quorumverlies in Hallo failover manager service maken van nieuwe services en failovers geblokkeerd. Tijdens het Hallo Service Fabric-systeemservices volgen hetzelfde patroon als uw services voor statusbeheer hello, dit wordt niet aanbevolen dat u toomove moet proberen ze buiten Quorumverlies en potentiële dataloss. Hallo-aanbeveling is in plaats daarvan te[ondersteuning zoeken](service-fabric-support.md) toodetermine een oplossing die is gericht tooyour specifieke situatie.  Meestal is het beter toosimply wacht tot Hallo omlaag replica's retourneren.
>

## <a name="availability-of-hello-service-fabric-cluster"></a>Beschikbaarheid van Hallo Service Fabric-cluster
Hallo Service Fabric-cluster zichzelf is over het algemeen een sterk gedistribueerde omgeving met geen enkele storingspunten. Een storing van een willekeurig knooppunt leidt niet tot de beschikbaarheid of betrouwbaarheidsproblemen voor Hallo-cluster, voornamelijk omdat Hallo Service Fabric-systeemservices Volg Hallo dezelfde richtlijnen die eerder is verkregen: ze altijd uitgevoerd met drie of meer replica's standaard en die systeemservices die staatloze zijn uitgevoerd op alle knooppunten. Hallo onderliggende Service Fabric-netwerken en fout detectie lagen worden volledig gedistribueerd. De meeste systeemservices van metagegevens in Hallo cluster kan worden gemaakt of weten hoe tooresynchronize hun status vanuit andere locaties. Hallo-beschikbaarheid van Hallo cluster kan niet meer betrouwbaar als systeemservices quorum verlies situaties zoals deze beschreven bovenstaande krijgen. In dergelijke gevallen niet mogelijk kunnen tooperform bepaalde bewerkingen op Hallo-cluster dat begint met een upgrade of implementeren van nieuwe services, maar het Hallo-cluster zelf nog steeds actief is. Services op het al wordt uitgevoerd blijft actief in deze voorwaarden, tenzij ze nodig schrijfbewerkingen toohello system services toocontinue werkt hebben. Bijvoorbeeld als Hallo Failover Manager is sprake van quorumverlies alle services toorun wordt voortgezet, maar kunnen services die niet voldoen aan zich niet kunnen tooautomatically opnieuw wordt opgestart, omdat dit Hallo betrokkenheid van Hallo Failover Manager vereist. 

### <a name="failures-of-a-datacenter-or-azure-region"></a>Fouten van een datacenter of een Azure-regio
In zeldzame gevallen, een fysieke datacenter zijn tijdelijk niet beschikbaar vanwege tooloss van power of netwerkverbinding. In deze gevallen is is de Service Fabric-clusters en -services in het desbetreffende datacenter of een Azure-regio niet beschikbaar. Echter, _uw gegevens behouden blijven_. Voor clusters worden uitgevoerd in Azure, kunt u updates bekijken op storingen op Hallo [pagina Azure status][azure-status-dashboard]. Zeer onwaarschijnlijk gebeurtenis die een fysieke datacenter is volledig of gedeeltelijk vernietigd, alle Service Fabric-clusters die er worden gehost in Hallo of Hallo-services in deze verloren kunnen gaan. Dit omvat geen status die niet een back-up buiten het datacenter of de regio.

Er is twee verschillende strategieën voor functionerende hallo permanente of volgehouden falen van een enkele datacenter of regio. 

1. Afzonderlijke Service Fabric-clusters worden uitgevoerd in meerdere dergelijke regio's en gebruikmaken van een mechanisme voor failover en failback tussen deze omgevingen. De sortering van meerdere actief-actief of actief / passief clustermodel vereist aanvullende code voor beheer van en bewerkingen. Dit is ook vereist coördinatie van de back-ups van Hallo-services in een datacenter of regio zodat ze beschikbaar zijn in andere datacenters of de regio's wanneer een mislukt. 
2. Voer één Service Fabric-cluster die meerdere datacenters of regio's omvat. Hallo minimale ondersteunde configuratie voor deze is drie datacenters of regio's. Hallo aanbevolen aantal regio's of datacenters is vijf. Hiervoor moet een complexere clustertopologie. Hallo is voordeel van dit model echter dat falen van een datacenter of regio na een noodgeval is geconverteerd naar een normale fout. Deze fouten kunnen worden verwerkt door het Hallo-mechanismen die werken voor clusters binnen één regio. Zorg ervoor werkbelastingen worden gedistribueerd, zodat ze normaal fouten tolereren domeinen met fouten en upgradedomeinen regels voor de plaatsing van de Service Fabric. Voor meer informatie over beleidsregels die kunnen helpen bij het gebruiken van services in dit type cluster Lees informatie over [plaatsingsbeleid](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md)

### <a name="random-failures-leading-toocluster-failures"></a>Willekeurige fouten voorloopspaties toocluster fouten
Service Fabric heeft Hallo concept van Seed-knooppunten. Dit zijn de knooppunten die de beschikbaarheid van de onderliggende cluster Hallo Hallo onderhouden. Deze knooppunten te up maken van tooensure Hallo cluster blijft door tot stand brengen van leases met andere knooppunten en fungeren als tiebreakers tijdens bepaalde soorten netwerkfouten. Als willekeurige fouten een meerderheid van Hallo seed-knooppunten in cluster Hallo verwijderen en ze niet worden toegevoegd, Hallo cluster automatisch afgesloten. In Azure, Seed-knooppunten automatisch worden beheerd: ze worden gedistribueerd via Hallo beschikbaar fouten en upgradedomeinen en als een enkel seed-knooppunt wordt verwijderd uit Hallo cluster een andere naam in plaats daarvan wordt gemaakt. 

In zelfstandige Service Fabric-clusters en Azure is Hallo 'Primaire knooppunttype' hello die Hallo zaden wordt uitgevoerd. Bij het definiëren van een primaire knooppunttype Service Fabric, automatisch profiteren van het aantal knooppunten dat is geleverd door het maken van too9 seed-knooppunten en 9 replica's van elk van de systeemservices Hallo Hallo. Als een set van willekeurige fouten tegelijkertijd uit een meerderheid van die replica van de service system duurt, Voer Hallo systeemservices quorum verloren zijn gegaan, zoals hierboven is beschreven. Als een meerderheid van Hallo seed-knooppunten verloren gaan, Hallo cluster snel na afgesloten.

## <a name="next-steps"></a>Volgende stappen
- Meer informatie over hoe toosimulate diverse fouten met Hallo [testbaarheid framework](service-fabric-testability-overview.md)
- Lezen van andere bronnen voor herstel na noodgevallen en hoge beschikbaarheid. Microsoft heeft een grote hoeveelheid informatie over deze onderwerpen worden gepubliceerd. Terwijl sommige van deze documenten toospecific technieken voor gebruik in andere producten verwijzen, bevatten ze veel algemene aanbevolen procedures die u in Hallo Service Fabric-context ook toepassen kunt:
  - [Beschikbaarheidscontrolelijst](../best-practices-availability-checklist.md)
  - [Uitvoeren van een herstel na noodgevallen detailanalyse](../sql-database/sql-database-disaster-recovery-drills.md)
  - [Herstel na noodgevallen en hoge beschikbaarheid voor Azure-toepassingen][dr-ha-guide]
- Meer informatie over [ondersteuningsopties voor Service Fabric](service-fabric-support.md)

<!-- External links -->

[repair-partition-ps]: https://msdn.microsoft.com/library/mt163522.aspx
[azure-status-dashboard]:https://azure.microsoft.com/status/
[azure-regions]: https://azure.microsoft.com/regions/
[dr-ha-guide]: https://msdn.microsoft.com/library/azure/dn251004.aspx


<!-- Images -->

[sfx-cluster-map]: ./media/service-fabric-disaster-recovery/sfx-clustermap.png
