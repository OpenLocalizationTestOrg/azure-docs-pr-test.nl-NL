---
title: aangepaste Service Fabric-statusrapporten aaaAdd | Microsoft Docs
description: Hierin wordt beschreven hoe toosend aangepaste systeemstatusrapporten tooAzure Service Fabric health entiteiten. Geeft aanbevelingen voor het ontwerpen en implementeren van statusrapporten kwaliteit.
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: 0a00a7d2-510e-47d0-8aa8-24c851ea847f
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: oanapl
ms.openlocfilehash: 12c9f664e2a457b4e1e8f340873ca60ebcefb097
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-custom-service-fabric-health-reports"></a>Aangepaste statusrapporten van Service Fabric toevoegen
Azure Service Fabric introduceert een [statusmodel](service-fabric-health-introduction.md) ontworpen tooflag slecht cluster en de voorwaarden van toepassing op specifieke entiteiten. Hallo-statusmodel gebruikt **health rapporteurs** (onderdelen van het systeem en watchdogs). Hallo-doel is snel en gemakkelijk diagnose en herstel. Schrijvers van de service moeten toothink tevoren over status. Een voorwaarde die van invloed kan status moet worden gerapporteerd, vooral als vlag problemen sluiten toohello root kunt u. Hallo statusgegevens kunt tijd en moeite besparen op onderzoek naar en het opsporen van fouten. Hallo nut vooral duidelijk is wanneer het Hallo-service actief is op de gewenste schaal in de cloud Hallo (particulier of Azure).

Hallo Service Fabric-rapporteurs monitor geïdentificeerd voorwaarden van belang. Ze een rapport over deze voorwaarden op basis van hun lokale weergave. Hallo [health store](service-fabric-health-introduction.md#health-store) aggregeert statusgegevens verzonden door alle rapporteurs toodetermine of entiteiten globaal in orde zijn. Hallo-model is beoogde toobe uitgebreide, flexibele en eenvoudige toouse. Hallo kwaliteit van statusrapporten Hallo bepaalt Hallo nauwkeurig Hallo health weergave van Hallo-cluster. Fout-positieven waarin ten onrechte slecht problemen weergegeven kunnen nadelig upgrades of andere services die gebruikmaken van statusgegevens. Voorbeelden van dergelijke services zijn reparatie en waarschuwen mechanismen. Voorzichtig is daarom benodigde tooprovide rapporten die voorwaarden van interesse in Hallo vastleggen best mogelijke manier.

toodesign en implementeer health reporting, watchdogs en systeemonderdelen moeten:

* Hallo-voorwaarde die in kwestie definiëren, Hallo manier waarop die deze wordt bewaakt en Hallo van invloed op Hallo cluster- of -functionaliteit. Bepaal op basis van deze informatie, op Hallo rapport eigenschap en health status.
* Hallo bepalen [entiteit](service-fabric-health-introduction.md#health-entities-and-hierarchy) Hallo rapport is van toepassing op.
* Bepalen waar Hallo rapportage gebeurt, Hallo vanuit de service of van een interne of externe watchdog.
* Een bron gebruikt tooidentify hello Rapportagefout definiëren.
* Kies een reporting strategie periodiek of op overgangen. Hallo aanbevolen manier is periodiek, omdat deze eenvoudiger code vereist en minder gevoelig tooerrors is.
* Bepalen hoe lang Hallo-rapport voor slechte voorwaarden in Hallo health store blijven moeten en hoe moet worden gewist. Met deze informatie kunt bepalen van het rapport Hallo time toolive en verwijderen op vervaldatum gedrag.

Zoals gezegd, rapportage kunt u doen vanaf:

* Hallo bewaakt replica voor Service Fabric-service.
* Interne watchdogs geïmplementeerd als een Service Fabric-service (bijvoorbeeld een Service Fabric staatloze service dat wordt bewaakt voorwaarden en rapporten). Hallo watchdogs kunnen worden geïmplementeerd een alle knooppunten of stelt toohello bewaakte service kan zijn.
* Interne watchdogs die worden uitgevoerd op Hallo Service Fabric-knooppunten maar *niet* geïmplementeerd als een Service Fabric-services.
* Externe watchdogs die resource test Hallo van *buiten* Hallo Service Fabric-cluster (bijvoorbeeld bewaking service zoals Gomez).

> [!NOTE]
> Hallo-cluster is out of box hello gevuld met statusrapporten dat is verzonden door de onderdelen van het systeem Hallo. Meer informatie op [rapporten system health gebruiken voor het oplossen van](service-fabric-understand-and-troubleshoot-with-system-health-reports.md). Hallo Gebruikersrapporten moeten worden verzonden op [de statusentiteiten](service-fabric-health-introduction.md#health-entities-and-hierarchy) die al zijn gemaakt door Hallo-systeem.
> 
> 

Eenmaal hello health reporting ontwerp is duidelijk, statusrapporten eenvoudig kunnen worden verzonden. U kunt [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) tooreport health als Hallo-cluster niet is [beveiligde](service-fabric-cluster-security.md) of als Hallo fabric-client beheerdersbevoegdheden heeft. Rapportage kan worden uitgevoerd via Hallo API door met [FabricClient.HealthManager.ReportHealth](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.reporthealth), via PowerShell of via REST. Configuratie knoppen batch-rapporten voor betere prestaties.

> [!NOTE]
> De status van het rapport is synchrone en het Hallo validatie werkt alleen op de client Hallo vertegenwoordigt. Hallo wordt dat rapport Hallo geaccepteerd door Hallo health client of Hallo `Partition` of `CodePackageActivationContext` objecten betekent niet dat in de winkel hello wordt toegepast. Het is asynchroon worden verzonden en mogelijk met andere rapporten batch verwerkt. Hallo verwerking op de server Hallo mogelijk nog steeds: Hallo volgnummer is mogelijk verlopen, Hallo-entiteit op welke Hallo rapport moet worden toegepast is verwijderd, enzovoort.
> 
> 

## <a name="health-client"></a>Health-client
Hallo statusrapporten worden toohello health store via een health-client, die zich in de fabric-client Hallo verzonden. Hallo health client kan worden geconfigureerd met Hallo volgende instellingen:

* **HealthReportSendInterval**: Hallo vertraging tussen Hallo tijd Hallo rapport is toegevoegd toohello client en Hallo tijd deze toohello health store wordt verzonden. Gebruikte toobatch rapporten in een enkel bericht, in plaats van verzenden een bericht voor elk rapport. Hallo batchverwerking verbetert de prestaties. Standaardwaarde: 30 seconden.
* **HealthReportRetrySendInterval**: hello-interval opnieuw op welke Hallo Samengevoegde health verzendt de client health rapporten toohello health store. Standaardwaarde: 30 seconden.
* **HealthOperationTimeout**: Hallo time-outperiode voor een rapportbericht verzonden toohello health store. Als er is een time-out opgetreden voor een bericht, opnieuw Hallo health client het totdat Hallo health store bevestigt dat Hallo rapport is verwerkt. Standaardwaarde: twee minuten.

> [!NOTE]
> Wanneer het Hallo-rapporten in batch worden opgenomen, Hallo fabric-client moet worden behouden voor ten minste Hallo HealthReportSendInterval tooensure dat ze worden verzonden. Als het Hallo-bericht verloren gegaan is of Hallo health store niet vanwege tootransient fouten toepassen, Hallo fabric-client moet worden bewaard alive langer toogive er een kans tooretry.
> 
> 

Hallo buffer op Hallo client neemt Hallo Uniekheid van Hallo rapporten in aanmerking. Bijvoorbeeld, als een bepaalde slechte Rapportagefout 100 rapport is rapporten per seconde op Hallo dezelfde eigenschap Hallo Hallo rapporten zijn vervangen door de laatste versie Hallo dezelfde entiteit. Maximaal één zo'n rapport bestaat in Hallo client wachtrij. Als batchverwerking is geconfigureerd, verzonden hello aantal rapporten toohello health store is slechts een interval dat verzenden. Dit rapport is Hallo laatste toegevoegde rapport, dat overeenkomt met de meest actuele status Hallo van Hallo entiteit.
Geef configuratieparameters wanneer `FabricClient` wordt gemaakt door het doorgeven van [FabricClientSettings](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclientsettings) Hello de gewenste waarden voor de health-gerelateerde vermeldingen.

Hallo volgende voorbeeld wordt een fabric-client en geeft aan dat Hallo rapporten moeten worden verzonden wanneer ze worden toegevoegd. Nieuwe pogingen gebeuren voor time-outs en fouten die kunnen opnieuw worden geprobeerd, elke 40 seconden.

```csharp
var clientSettings = new FabricClientSettings()
{
    HealthOperationTimeout = TimeSpan.FromSeconds(120),
    HealthReportSendInterval = TimeSpan.FromSeconds(0),
    HealthReportRetrySendInterval = TimeSpan.FromSeconds(40),
};
var fabricClient = new FabricClient(clientSettings);
```

We raden u Hallo standaard fabric-clientinstellingen, die ingesteld `HealthReportSendInterval` too30 seconden. Deze instelling zorgt u voor optimale prestaties vanwege toobatching. Gebruik voor kritieke rapporten die zo snel mogelijk moeten worden verzonden, `HealthReportSendOptions` met direct `true` in [FabricClient.HealthClient.ReportHealth](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.reporthealth) API. Onmiddellijke rapporten overslaan Hallo batchverwerking interval. Gebruik deze vlag zorgvuldig; We willen tootake profiteren van Hallo health client batchverwerking indien mogelijk. Onmiddellijke verzenden is ook nuttig bij het afsluiten van Hallo fabric-client (bijvoorbeeld Hallo proces heeft ongeldige status vastgesteld en moet tooshut omlaag tooprevent bijwerkingen). Hiermee zorgt u ervoor een best-effort verzenden van rapporten Hallo verzameld. Wanneer een rapport met onmiddellijke vlag wordt toegevoegd, batches Hallo health client alle Hallo cumulatieve rapporten sinds de laatste verzenden.

Dezelfde parameters kunnen worden opgegeven wanneer een verbinding tooa cluster wordt gemaakt via PowerShell. Hallo volgende voorbeeld wordt een verbinding tooa lokaal cluster gestart:

```powershell
PS C:\> Connect-ServiceFabricCluster -HealthOperationTimeoutInSec 120 -HealthReportSendIntervalInSec 0 -HealthReportRetrySendIntervalInSec 40
True

ConnectionEndpoint   :
FabricClientSettings : {
                       ClientFriendlyName                   : PowerShell-1944858a-4c6d-465f-89c7-9021c12ac0bb
                       PartitionLocationCacheLimit          : 100000
                       PartitionLocationCacheBucketCount    : 1024
                       ServiceChangePollInterval            : 00:02:00
                       ConnectionInitializationTimeout      : 00:00:02
                       KeepAliveInterval                    : 00:00:20
                       HealthOperationTimeout               : 00:02:00
                       HealthReportSendInterval             : 00:00:00
                       HealthReportRetrySendInterval        : 00:00:40
                       NotificationGatewayConnectionTimeout : 00:00:00
                       NotificationCacheUpdateTimeout       : 00:00:00
                       }
GatewayInformation   : {
                       NodeAddress                          : localhost:19000
                       NodeId                               : 1880ec88a3187766a6da323399721f53
                       NodeInstanceId                       : 130729063464981219
                       NodeName                             : Node.1
                       }
```

Op dezelfde manier tooAPI, rapporten kunnen worden verzonden met behulp van `-Immediate` toobe onmiddellijk verzonden ongeacht Hallo overschakelen `HealthReportSendInterval` waarde.

Hallo-rapporten worden voor REST, toohello Service Fabric-gateway een interne fabric-client is worden verzonden. Standaard is deze client geconfigureerde toosend rapporten batch verwerkt elke 30 seconden. U kunt hello batch-interval wijzigen met Hallo cluster configuratie-instelling `HttpGatewayHealthReportSendInterval` op `HttpGateway`. Zoals gezegd, een betere optie toosend Hallo rapporten met is `Immediate` true. 

> [!NOTE]
> tooensure dat services onbevoegde kan niet rapporteren health configureren tegen Hallo entiteiten in de cluster hello, Hallo serveraanvragen tooaccept alleen van beveiligde clients. Hallo `FabricClient` gebruikt voor het melden van de beveiliging is ingeschakeld kunnen toocommunicate toobe met Hallo-cluster (bijvoorbeeld met Kerberos of certificaten verificatie). Lees meer over [beveiliging cluster](service-fabric-cluster-security.md).
> 
> 

## <a name="report-from-within-low-privilege-services"></a>Rapport van binnen services met beperkte bevoegdheden
Als de Service Fabric-services geen beheerder toegang toohello cluster hebt, kunt u health rapporteren op entiteiten van de huidige context Hallo via `Partition` of `CodePackageActivationContext`.

* Gebruik voor stateless services [IStatelessServicePartition.ReportInstanceHealth](https://docs.microsoft.com/dotnet/api/system.fabric.istatelessservicepartition.reportinstancehealth) tooreport op Hallo huidige service-exemplaar.
* Gebruik voor stateful services [IStatefulServicePartition.ReportReplicaHealth](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition.reportreplicahealth) tooreport voor de huidige replica.
* Gebruik [IServicePartition.ReportPartitionHealth](https://docs.microsoft.com/dotnet/api/system.fabric.iservicepartition.reportpartitionhealth) tooreport op Hallo huidige partitie entiteit.
* Gebruik [CodePackageActivationContext.ReportApplicationHealth](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext.reportapplicationhealth) tooreport op de huidige toepassing.
* Gebruik [CodePackageActivationContext.ReportDeployedApplicationHealth](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext.reportdeployedapplicationhealth) tooreport op Hallo van de huidige toepassing geïmplementeerd op het huidige knooppunt Hallo.
* Gebruik [CodePackageActivationContext.ReportDeployedServicePackageHealth](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext.reportdeployedservicepackagehealth) tooreport op een servicepakket voor geïmplementeerd op het huidige knooppunt Hallo Hallo-toepassing.

> [!NOTE]
> Intern Hallo `Partition` en Hallo `CodePackageActivationContext` houdt een health-client met standaardinstellingen geconfigureerd. Zoals uitgelegd voor Hallo [health client](service-fabric-report-health.md#health-client), rapporten zijn batch verwerkt en verzonden via een timer. Hallo-objecten moeten worden bewaard alive toohave een kans toosend Hallo-rapport.
> 
> 

U kunt opgeven `HealthReportSendOptions` bij het verzenden van rapporten via `Partition` en `CodePackageActivationContext` health API's. Als er kritieke rapporten die zo snel mogelijk moeten worden verzonden, gebruikt u `HealthReportSendOptions` met direct `true`. Onmiddellijke rapporten overslaan Hallo batchverwerking interval van Hallo interne health client. Zoals al eerder vermeld, gebruikt u deze vlag zorgvuldig; We willen tootake profiteren van Hallo health client batchverwerking indien mogelijk.

## <a name="design-health-reporting"></a>Health reporting ontwerpen
Hallo wordt eerste stap bij het genereren van rapporten van hoge kwaliteit identificeren Hallo voorwaarden die invloed op Hallo status van Hallo-service hebben kunnen. Elke voorwaarde kunt vlag problemen bij het Hallo-service of het cluster wanneer deze wordt-- of zelfs beter voordat er een probleem voordoet--kan mogelijk miljarden bedragen opslaan. Hallo voordelen zijn minder uitvaltijd, uren minder 's nachts besteed aan het onderzoeken en oplossen van problemen en hogere klanttevredenheid.

Nadat Hallo voorwaarden worden geïdentificeerd, moeten watchdog schrijvers toofigure uit Hallo aanbevolen manier toomonitor ze voor balans tussen overhead en bruikbaarheid. Neem bijvoorbeeld een service die complexe berekeningen die gebruikmaken van een aantal tijdelijke bestanden op een share heeft. Hallo share tooensure dat voldoende ruimte beschikbaar is, kan een watchdog controleren. Het kan luisteren voor meldingen van bestand of map wijzigingen. Dit kan een waarschuwing worden gerapporteerd als een vooraf drempelwaarde is bereikt en een fout gemeld als Hallo share vol is. Op een waarschuwing kan een reparatie-systeem gestart opschonen van oudere bestanden op Hallo share. Op een fout optreedt, kan een systeem herstellen Hallo service replica tooanother knooppunt verplaatsen. Houd er rekening mee hoe Hallo voorwaarde statussen worden beschreven in termen van health: Hallo status van Hallo voorwaarde die kan worden overwogen in orde (ok) of slecht (waarschuwing of fout).

Zodra Hallo bewaking details zijn ingesteld, moet een schrijver watchdog toofigure uit hoe tooimplement watchdog Hallo. Als Hallo voorwaarden kunnen worden bepaald uit in de service hello, kan Hallo watchdog deel uitmaken van Hallo bewaakt service zelf. Hallo-servicecode kan bijvoorbeeld Controleer Hallo share gebruik en vervolgens rapporteren telkens wanneer wordt geprobeerd een bestand toowrite. Hallo voordeel van deze benadering is dat reporting eenvoudig is. Wees voorzichtig tooprevent watchdog bugs Hallo service functionaliteit beïnvloeden.

Rapportage van binnen Hallo bewaakt service is niet altijd een optie. Een watchdog binnen Hallo-service mogelijk niet kunnen toodetect Hallo voorwaarden. Het mag geen Hallo logica of gegevens toomake Hallo bepaling hebben. Hallo-overhead van bewaking Hallo voorwaarden mogelijk te hoog. Hallo voorwaarden kunnen ook niet worden specifieke tooa service, maar in plaats daarvan invloed hebben op de interacties tussen services. Een andere optie is toohave watchdogs in Hallo cluster als afzonderlijke processen. Hallo watchdogs bewaken Hallo voorwaarden en rapport zonder Hallo belangrijkste services op een manier. Deze watchdogs kunnen bijvoorbeeld worden geïmplementeerd als stateless services in Hallo dezelfde toepassing geïmplementeerd op alle knooppunten of op Hallo dezelfde knooppunten als Hallo-service.

Soms is een watchdog in Hallo cluster wordt uitgevoerd geen optie ofwel. Als Hallo bewaakt voorwaarde is Hallo beschikbaarheid of functionaliteit van Hallo-service, zoals gebruikers deze zien, is het aanbevolen toohave hello watchdogs in Hallo dezelfde als Hallo gebruiker clients plaatsen. Daar ze Hallo bewerkingen kunnen testen in Hallo dezelfde manier waarop gebruikers ze aanroept. U kunt bijvoorbeeld een watchdog die woont buiten Hallo-cluster, aanvragen toohello service uitgeeft en controleert Hallo latentie en de juistheid van Hallo resultaat hebben. (Voor een service Rekenmachine bijvoorbeeld 2 + 2 retourneert 4 binnen redelijke tijd?)

Zodra het Hallo watchdog details hebt is voltooid, moet u bepalen van een bron-ID die uniek wordt geïdentificeerd. Als meerdere watchdogs van hetzelfde type zijn dat in Hallo hello cluster, moeten ze rapporteren over verschillende entiteiten of, als ze een rapport over Hallo dezelfde entiteit, gebruik verschillende bron-ID of eigenschap. Op deze manier hun rapporten kunnen worden gecombineerd. Hallo-eigenschap van het statusrapport Hallo moet Hallo bewaakt voorwaarde vastleggen. (Bijvoorbeeld Hallo bovenstaande Hallo-eigenschap kan worden **ShareSize**.) Als meerdere rapporten toohello toepast dezelfde voorwaarde hello eigenschap moet een aantal dynamische informatie waarmee u rapporten toocoexist bevatten. Bijvoorbeeld, als meerdere shares toobe bewaakt moeten, Hallo eigenschapsnaam mag **ShareSize sharename**.

> [!NOTE]
> Voer *niet* gebruik Hallo health store tookeep-statusinformatie. Alleen door de health-gerelateerde informatie moet worden gerapporteerd als health als deze informatie effecten Hallo health evaluatie van een entiteit. Hallo health store is niet ontworpen als een algemene archief. Wordt gebruikt health evaluatie logica tooaggregate alle gegevens in het Hallo-status. Verzenden gegevens niet-verwante toohealth (zoals rapportage over de status met een status van OK) heeft geen invloed op Hallo samengevoegd status, maar het Hallo-prestaties van Hallo health store negatief kan beïnvloeden.
> 
> 

de volgende beslissingspunt Hallo is welke tooreport entiteit op. Meestal Hallo Hallo voorwaarde duidelijk Hallo idetifies entiteit. Hallo-entiteit met best mogelijke granulatie kiezen. Als een voorwaarde heeft gevolgen voor alle replica's in een partitie, een rapport over Hallo-partitie, niet op Hallo-service. Er zijn hoek gevallen waar meer gedachte is vereist, hoewel. Als Hallo voorwaarde geldt voor een entiteit, zoals een replica, maar Hallo desire toohave Hallo voorwaarde gemarkeerd voor meer dan Hallo duur van de replica-levensduur en vervolgens op Hallo partitie moet worden gemeld. Anders wanneer Hallo replica wordt verwijderd, ruimt Hallo health store de rapporten ervan. Watchdog schrijvers moeten Denk na over Hallo levensduur van Hallo entiteit en Hallo-rapport. Het moet wissen wanneer een rapport moet worden opgeruimd in een store (bijvoorbeeld wanneer een fout gerapporteerd voor een entiteit wordt niet langer van toepassing).

Bekijk een voorbeeld waarin plaatst samen Hallo punten die ik beschreven. U kunt dat een Service Fabric-toepassing bestaat uit een stateful permanente service master en secundaire stateless services die zijn geïmplementeerd op alle knooppunten (één secundaire servicetype voor elk type taak). Hallo-master heeft een wachtrij voor verwerking die opdrachten toobe uitgevoerd door de secundaire replica's bevat. Hallo secundaire replica's uitvoeren Hallo inkomende aanvragen en signalen back bevestiging verzenden. Een voorwaarde die kan worden bewaakt is Hallo lengte van master Hallo-verwerkingswachtrij. Als de master wachtrijlengte Hallo een drempel bereikt, wordt een waarschuwing wordt gerapporteerd. Hallo waarschuwing geeft aan dat secundaire replica's Hallo Hallo werklast kunnen verwerken. Als Hallo wachtrij bereikt Hallo maximumlengte en opdrachten worden verwijderd, wordt een fout gerapporteerd, als Hallo service kan niet worden hersteld. Hallo kunnen rapporten worden op Hallo eigenschap **QueueStatus**. Hallo watchdog woont binnen Hallo-service en deze regelmatig op Hallo master primaire replica wordt verzonden. Hallo tijd toolive is twee minuten en periodiek elke 30 seconden verzonden. Als primaire Hallo uitvalt, wordt Hallo rapport automatisch opgeschoond vanuit de store. Als Hallo service replica actief is, maar dit is een impasse of er andere problemen Hallo verloopt rapport Hallo health store. In dit geval wordt Hallo entiteit geëvalueerd op fout.

Nog een voorwaarde die kan worden gecontroleerd is uitvoeringstijd van de taak. Hallo master distribueert taken toohello secundaire replica's op basis van het taaktype Hallo. Afhankelijk van het ontwerp voor Hallo kan Hallo master Hallo secundaire replica's voor de taakstatus pollen. Het kan ook wachten voor secundaire replica's toosend back bevestiging opgeven wanneer ze klaar bent. In het tweede geval Hallo moet nauwkeurig toodetect situaties waarbij secundaire replica's die of berichten gaan verloren. Een optie is voor Hallo master toosend een ping-aanvraag toohello dezelfde secundaire, waarmee de status ervan terug wordt verzonden. Als geen status wordt ontvangen, een storing acht Hallo hoofd- en Hallo taak opnieuw gepland. Dit gedrag wordt ervan uitgegaan dat Hallo taken idempotent zijn.

Hallo bewaakt voorwaarde kan worden omgezet als een waarschuwing als het Hallo-taak is niet uitgevoerd in een bepaalde tijd (**t1**, bijvoorbeeld 10 minuten). Als Hallo-taak is niet voltooid in de tijd (**t2**, bijvoorbeeld 20 minuten), Hallo bewaakt voorwaarde als fout kan worden omgezet. Deze rapportage kunt op verschillende manieren doen:

* Hallo master primaire replica rapporten periodiek op zichzelf. U kunt één eigenschap voor alle in behandeling zijnde taken in de wachtrij Hallo hebben. Als ten minste één taak duurt langer, Hallo rapportstatus op Hallo eigenschap **PendingTasks** een waarschuwing of fout naar gelang van toepassing is. Als er geen taken in behandeling zijn of heeft de uitvoering van alle taken gestart, is Hallo rapportstatus in orde. Hallo-taken zijn permanent. Als primaire Hallo uitvalt, verder Hallo zojuist gepromoveerd primaire tooreport goed.
* Een ander watchdog proces (in Hallo cloud of extern) controleert taken hello (van buiten, op basis van gewenst Hallo Taakresultaat) toosee als ze zijn voltooid. Als ze bieden geen ondersteuning voor Hallo drempelwaarden, wordt een rapport op Hallo hoofd-service verzonden. Een rapport wordt ook op elke taak met taak-id op Hallo, zoals verzonden **PendingTask + taskId**. Rapporten moeten alleen op slecht statussen worden verzonden. Stel toolive tooa tijd enkele minuten en Hallo rapporten toobe verwijderd wanneer deze tooensure Schijfopruiming verlopen markeren.
* Hallo secundaire dat een taak wordt uitgevoerd rapporten wanneer het duurt langer dan verwacht toorun deze. Bevat informatie over service-exemplaar op Hallo eigenschap Hallo **PendingTasks**. Hallo rapport lokaliseert Hallo service-exemplaar die problemen heeft, maar het Hallo situatie waarbij Hallo exemplaar matrijzen niet vastleggen. Hallo rapporten worden vervolgens opgeschoond. Dit kan een rapport over Hallo secundaire service. Als secundaire Hallo Hallo taken is voltooid, wist secundaire exemplaar Hallo Hallo rapport uit Hallo store. Hallo-rapport vastleggen niet Hallo situatie waarin bevestiging het Hallo-bericht is verloren gegaan en Hallo-taak niet uit het oogpunt van Hallo model is beëindigd.

Maar Hallo rapportage gebeurt in Hallo gevallen die hierboven worden beschreven, worden rapporten Hallo vastgelegd in toepassingsstatus health wordt geëvalueerd.

## <a name="report-periodically-vs-on-transition"></a>Rapport regelmatig versus op overgang
Met behulp van Hallo health model reporting kunt watchdogs periodiek of overgangen rapporten verzenden. Hallo aanbevolen watchdog reporting wordt regelmatig omdat Hallo code veel eenvoudiger en minder gevoelig tooerrors is. Hallo watchdogs moeten streven ernaar toobe zo eenvoudig mogelijk tooavoid bugs die onjuiste rapporten activeren. Onjuiste *slecht* rapporten gevolgen hebben voor health-beoordelingen en scenario's op basis van status, met inbegrip van upgrades. Onjuiste *orde* rapporten problemen in Hallo-cluster niet verbergen.

Voor periodieke rapportage kan Hallo watchdog worden geïmplementeerd met een timer. Op een retouraanroep timer Hallo watchdog Hallo status controleren en een rapport op basis van de huidige status Hallo verzenden. Er is geen noodzaak toosee welke rapport eerder is verzonden of maken van alle optimalisaties in termen van berichten. Hallo health client heeft batchverwerking logica toohelp met prestaties. Tijdens het Hallo-health-client wordt gehouden actief is, het opnieuw probeert intern totdat Hallo rapport is bevestigd door Hallo health store of Hallo watchdog een nieuwere rapport met Hallo genereert dezelfde entiteit, eigenschap en bron.

Rapportage over overgangen vereist zorgvuldige verwerking van de status. Hallo watchdog bewaakt een aantal voorwaarden en rapporten alleen als Hallo voorwaarden wijzigen. Hallo opwaartse van deze benadering is dat er minder rapporten nodig zijn. Hallo nadeel is dat Hallo logica van Hallo watchdog complexe. Hallo watchdog moet onderhouden Hallo voorwaarden of Hallo rapporten, zodat ze domeinen toodetermine statuswijzigingen worden kunnen. Failover, Wees voorzichtig met rapporten is toegevoegd, maar nog niet verzonden toohello health store. Hallo volgnummer moet steeds groter wordende. Als dat niet het geval is, Hallo rapporten als verlopen worden afgewezen. In Hallo zeldzame gevallen waarin het verlies van gegevens is gemaakt, zijn mogelijk tussen Hallo status van Hallo Rapportagefout en status van Hallo health store Hallo synchronisatie vereist.

Rapportage over overgangen zinvol is voor services die worden gerapporteerd met betrekking tot zelf, via `Partition` of `CodePackageActivationContext`. Wanneer Hallo lokaal object (replica of geïmplementeerd servicepakket / toepassing is geïmplementeerd) is verwijderd, worden de rapporten ervan ook verwijderd. Deze automatisch opschonen worden Hallo nodig voor de synchronisatie tussen Rapportagefout en health store. Als Hallo rapport voor de bovenliggende partitie of de bovenliggende toepassing, moet nauwkeurig in failover tooavoid verlopen rapporten op Hallo health store. Logica moet worden toegevoegd toomaintain Hallo juiste status en wissen Hallo rapport uit de store wanneer het niet meer nodig hebt.

## <a name="implement-health-reporting"></a>Health reporting implementeren
Als de entiteit en in het rapport details zijn hello wissen, kan statusrapporten verzenden worden gedaan via Hallo API, PowerShell of REST.

### <a name="api"></a>API
tooreport via Hallo API, moet u toocreate een health specifieke toohello entiteit rapporttype hij of zij wil tooreport op. Geeft Hallo rapport tooa health client. U kunt ook een statusgegevens maken en geef dit toocorrect rapportagemethoden op `Partition` of `CodePackageActivationContext` tooreport op huidige entiteiten.

Hallo ziet volgende voorbeeld periodieke rapportage vanuit een watchdog binnen Hallo-cluster. Hallo watchdog controleert of een externe resource vanuit een knooppunt kan worden benaderd. Hallo resource nodig is voor een servicemanifest in Hallo-toepassing. Als het Hallo-bron niet beschikbaar is, hello andere services binnen de toepassing hello kunnen nog steeds naar behoren. Daarom Hallo rapport wordt verzonden op Hallo geïmplementeerd service pakket entiteit elke 30 seconden.

```csharp
private static Uri ApplicationName = new Uri("fabric:/WordCount");
private static string ServiceManifestName = "WordCount.Service";
private static string NodeName = FabricRuntime.GetNodeContext().NodeName;
private static Timer ReportTimer = new Timer(new TimerCallback(SendReport), null, 30 * 1000, 30 * 1000);
private static FabricClient Client = new FabricClient(new FabricClientSettings() { HealthReportSendInterval = TimeSpan.FromSeconds(0) });

public static void SendReport(object obj)
{
    // Test whether hello resource can be accessed from hello node
    HealthState healthState = this.TestConnectivityToExternalResource();

    // Send report on deployed service package, as hello connectivity is needed by hello specific service manifest
    // and can be different on different nodes
    var deployedServicePackageHealthReport = new DeployedServicePackageHealthReport(
        ApplicationName,
        ServiceManifestName,
        NodeName,
        new HealthInformation("ExternalSourceWatcher", "Connectivity", healthState));

    // TODO: handle exception. Code omitted for snippet brevity.
    // Possible exceptions: FabricException with error codes
    // FabricHealthStaleReport (non-retryable, hello report is already queued on hello health client),
    // FabricHealthMaxReportsReached (retryable; user should retry with exponential delay until hello report is accepted).
    Client.HealthManager.ReportHealth(deployedServicePackageHealthReport);
}
```

### <a name="powershell"></a>PowerShell
Verzenden van statusrapporten met  **verzenden ServiceFabric*EntityType*HealthReport **.

Hallo ziet volgende voorbeeld periodieke rapportage over CPU-waarden op een knooppunt. Hallo rapporten elke 30 seconden moeten worden verzonden en een periode van twee minuten toolive hebben. Als ze zijn verlopen, heeft Hallo Rapportagefout problemen, zodat het Hallo-knooppunt wordt geëvalueerd op fout. Wanneer Hallo CPU hoger dan een drempelwaarde is, heeft Hallo rapport een status van de waarschuwing. Wanneer Hallo CPU boven een drempelwaarde komt meer dan de tijd Hallo geconfigureerd blijft, wordt als een fout gerapporteerd. Anders verzendt Hallo Rapportagefout een status OK.

```powershell
PS C:\> Send-ServiceFabricNodeHealthReport -NodeName Node.1 -HealthState Warning -SourceId PowershellWatcher -HealthProperty CPU -Description "CPU is above 80% threshold" -TimeToLiveSec 120

PS C:\> Get-ServiceFabricNodeHealth -NodeName Node.1
NodeName              : Node.1
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='PowershellWatcher', Property='CPU', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 5
                        SentAt                : 4/21/2015 8:01:17 AM
                        ReceivedAt            : 4/21/2015 8:02:12 AM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/21/2015 8:02:12 AM

                        SourceId              : PowershellWatcher
                        Property              : CPU
                        HealthState           : Warning
                        SequenceNumber        : 130741236814913394
                        SentAt                : 4/21/2015 9:01:21 PM
                        ReceivedAt            : 4/21/2015 9:01:21 PM
                        TTL                   : 00:02:00
                        Description           : CPU is above 80% threshold
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Warning = 4/21/2015 9:01:21 PM
```

Hallo volgende voorbeeld wordt een tijdelijke waarschuwing op een replica. Het eerst opgehaald Hallo partitie-ID en vervolgens Hallo replica-ID voor deze is geïnteresseerd in Hallo-service. Verzendt vervolgens een rapport van **PowershellWatcher** op Hallo eigenschap **ResourceDependency**. Hallo-rapport is van belang zijn voor slechts twee minuten en wordt deze verwijderd uit de store Hallo automatisch.

```powershell
PS C:\> $partitionId = (Get-ServiceFabricPartition -ServiceName fabric:/WordCount/WordCount.Service).PartitionId

PS C:\> $replicaId = (Get-ServiceFabricReplica -PartitionId $partitionId | where {$_.ReplicaRole -eq "Primary"}).ReplicaId

PS C:\> Send-ServiceFabricReplicaHealthReport -PartitionId $partitionId -ReplicaId $replicaId -HealthState Warning -SourceId PowershellWatcher -HealthProperty ResourceDependency -Description "hello external resource that hello primary is using has been rebooted at 4/21/2015 9:01:21 PM. Expect processing delays for a few minutes." -TimeToLiveSec 120 -RemoveWhenExpired

PS C:\> Get-ServiceFabricReplicaHealth  -PartitionId $partitionId -ReplicaOrInstanceId $replicaId


PartitionId           : 8f82daff-eb68-4fd9-b631-7a37629e08c0
ReplicaId             : 130740415594605869
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='PowershellWatcher', Property='ResourceDependency', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 130740768777734943
                        SentAt                : 4/21/2015 8:01:17 AM
                        ReceivedAt            : 4/21/2015 8:02:12 AM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/21/2015 8:02:12 AM

                        SourceId              : PowershellWatcher
                        Property              : ResourceDependency
                        HealthState           : Warning
                        SequenceNumber        : 130741243777723555
                        SentAt                : 4/21/2015 9:12:57 PM
                        ReceivedAt            : 4/21/2015 9:12:57 PM
                        TTL                   : 00:02:00
                        Description           : hello external resource that hello primary is using has been rebooted at 4/21/2015 9:01:21 PM. Expect processing delays for a few minutes.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : ->Warning = 4/21/2015 9:12:32 PM
```

### <a name="rest"></a>REST
Statusrapporten met REST met POST-aanvragen die gaat u toohello gewenst entiteit en in Hallo hoofdtekst Hallo health Rapportbeschrijving verzenden. Zie bijvoorbeeld hoe REST-toosend [cluster statusrapporten](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-cluster) of [service statusrapporten](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service). Alle entiteiten worden ondersteund.

## <a name="next-steps"></a>Volgende stappen
Op basis van de statusgegevens hello, kunnen schrijvers van de service en cluster/toepassing beheerders van manieren tooconsume Hallo informatie zien. Ze kunnen bijvoorbeeld waarschuwingen op basis van status status toocatch ernstige problemen voordat ze leiden uitval tot instellen. Beheerders kunnen ook reparatie systemen toofix problemen automatisch ingesteld.

[Inleiding tooService Fabric health Monitoring](service-fabric-health-introduction.md)

[Service Fabric-statusrapporten weergeven](service-fabric-view-entities-aggregated-health.md)

[Hoe tooreport en controleer health service](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[Systeemstatusrapporten gebruiken voor het oplossen van problemen](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[Controle en diagnose van lokaal services](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Upgrade van de service Fabric-toepassing](service-fabric-application-upgrade.md)

