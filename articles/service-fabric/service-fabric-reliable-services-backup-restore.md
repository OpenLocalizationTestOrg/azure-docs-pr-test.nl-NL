---
title: aaaService Fabric back-up en herstel | Microsoft Docs
description: Conceptuele documentatie voor Service Fabric-back-up en herstel
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: subramar,jessebenson
ms.assetid: 91ea6ca4-cc2a-4155-9823-dcbd0b996349
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: mcoskun
ms.openlocfilehash: e502b59c84999c3fe825167383f00a5ebd70c9b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-and-restore-reliable-services-and-reliable-actors"></a>Back-up en herstel Reliable Services en Reliable Actors
Azure Service Fabric is een hoge beschikbaarheid-platform die zijn gerepliceerd Hallo status over meerdere knooppunten toomaintain deze hoge beschikbaarheid.  Dus zelfs als een knooppunt in het Hallo-cluster is mislukt, Hallo services kunnen blijven toobe beschikbaar. Bij deze ingebouwde redundantie geleverd door Hallo platform is mogelijk niet voldoende is voor sommige, in bepaalde gevallen is het wenselijk voor Hallo service tooback van gegevens (tooan externe store).

> [!NOTE]
> Het is essentieel toobackup en herstellen van uw gegevens (en de test werkt zoals verwacht) zodat u vanaf gegevensverlies herstellen kunt.
> 
> 

Bijvoorbeeld, kunt een service tooback van gegevens in de volgorde tooprotect van Hallo volgen scenario's:

- In de gebeurtenis Hallo van Hallo permanent verlies van een volledige Service Fabric-cluster.
- Permanent verlies van een meerderheid van Hallo replica's van de partitie van een service
- Administratieve fouten waarbij Hallo status per ongeluk wordt verwijderd of beschadigd. Dit kan bijvoorbeeld gebeuren als een beheerder met voldoende bevoegdheden ten onrechte Hallo-service worden verwijderd.
- Fouten in Hallo-service die leiden gegevensbeschadiging van tot. Dit kan bijvoorbeeld gebeuren wanneer een code-upgrade van service wordt gestart met het schrijven van beschadigde gegevens tooa betrouwbare verzameling. In dat geval beide code Hallo en Hallo gegevens mogelijk toobe tooan teruggezet eerdere status.
- De gegevensverwerking is offline. Handige toohave offline verwerking van gegevens voor business intelligence die plaatsvindt afzonderlijk uit Hallo-service die Hallo gegevens genereert mogelijk.

Hallo Backup/Restore-functie kunt services is gebaseerd op Hallo betrouwbare Services API toocreate en terugzetten van back-ups. Hallo toestaan back-API's die worden geleverd door Hallo platform backup(s) van status van een service-partitie, zonder blokkerende lees- of schrijfbewerkingen. Hallo-API's van de partitie van een service status toobe hersteld op basis van een gekozen back-up maken terugzetten.

## <a name="types-of-backup"></a>Typen back-ups
Er zijn twee opties voor back-up: volledige en incrementele.
Een volledige back-up is een back-up waarin alle Hallo gegevens die nodig zijn toorecreate Hallo status van replica Hallo: controlepunten en alle records in het logboek.
Omdat het Hallo controlepunten en Hallo logboekbestanden heeft, kan een volledige back-up kan worden hersteld door zelf.

Hallo probleem met volledige back-ups ontstaat wanneer Hallo controlepunten groot zijn.
Een replica met 16 GB status heeft bijvoorbeeld controlepunten die ongeveer too16 GB samen.
Als we een beoogd herstelpunt van vijf minuten hebt, moet Hallo replica toobe een back-up om de vijf minuten.
Telkens wanneer er een back-up moet toocopy 16 GB van controlepunten Daarnaast too50 MB (met behulp van configureerbare `CheckpointThresholdInMB`) aan logboeken.

![Voorbeeld van de volledige back-up.](media/service-fabric-reliable-services-backup-restore/FullBackupExample.PNG)

Hallo oplossing toothis probleem is incrementele back-ups wanneer back-up bevat alleen logboekrecords Hallo gewijzigd sinds de laatste back-up Hallo.

![Incrementele back-voorbeeld.](media/service-fabric-reliable-services-backup-restore/IncrementalBackupExample.PNG)

Aangezien incrementele back-ups worden enkel wijzigingen sinds Hallo laatste back-up (omvat geen controlepunten Hallo), ze toobe sneller vaak maar ze kunnen niet worden teruggezet op hun eigen.
toorestore een incrementele back-up, Hallo volledige back-keten is vereist.
Een back-keten is een keten van back-ups die beginnen met een volledige back-up en gevolgd door een aantal aaneengesloten incrementele back-ups.

## <a name="backup-reliable-services"></a>Back-Reliable Services
Hallo service auteur heeft volledig beheer van wanneer toomake back-ups en waar back-ups worden opgeslagen.

een back-up toostart, Hallo-service moet tooinvoke Hallo overgenomen lidfunctie `BackupAsync`.  
Back-ups kunnen alleen vanaf de primaire replica's worden gemaakt, en ze vereisen schrijven status toobe verleend.

Zoals hieronder aangegeven, `BackupAsync` wordt in een `BackupDescription` object, een waar een volledige of incrementele back-up, evenals een callback-functie opgeven kunt, `Func<< BackupInfo, CancellationToken, Task<bool>>>` die wordt geactiveerd wanneer de back-upmap Hallo lokaal is gemaakt en is klaar toobe verplaatst uit toosome externe opslag.

```csharp

BackupDescription myBackupDescription = new BackupDescription(backupOption.Incremental,this.BackupCallbackAsync);

await this.BackupAsync(myBackupDescription);

```

Aanvraag tootake met een incrementele back-up mislukken `FabricMissingFullBackupException`. Deze uitzondering geeft aan dat er een van de volgende dingen Hallo gebeurt:

- Hallo replica is nooit gemaakt van een volledige back-up nadat primaire geworden,
- aantal Hallo logboekregistratie records sinds de laatste back-up Hallo is afgekapt of
- replica Hallo doorgegeven `MaxAccumulatedBackupLogSizeInMB` limiet.

Gebruikers kunnen verhogen Hallo kans kunnen toodo incrementele back-ups wordt door het configureren van `MinLogSizeInMB` of `TruncationThresholdFactor`.
Houd er rekening mee dat deze waarden, Hallo per replica schijfgebruik verhoogt.
Zie voor meer informatie [betrouwbare configuratie van Services](service-fabric-reliable-services-configuration.md)

`BackupInfo`bevat informatie over Hallo back-up, inclusief locatie Hallo Hallo map Hallo runtime Hallo back-up opgeslagen (`BackupInfo.Directory`). Hallo-callback-functie kunt verplaatsen Hallo `BackupInfo.Directory` tooan externe winkel of een andere locatie.  Deze functie wordt ook een Boole-waarde die aangeeft of het kunnen toosuccessfully verplaatsen Hallo back-upmap tooits target-locatie.

Hallo volgende code laat zien hoe Hallo `BackupCallbackAsync` methode gebruikte tooupload Hallo back-tooAzure opslag kan zijn:

```csharp
private async Task<bool> BackupCallbackAsync(BackupInfo backupInfo, CancellationToken cancellationToken)
{
    var backupId = Guid.NewGuid();

    await externalBackupStore.UploadBackupFolderAsync(backupInfo.Directory, backupId, cancellationToken);

    return true;
}
```

In Hallo voorgaande voorbeeld `ExternalBackupStore` is Hallo voorbeeldklasse die is gebruikt toointerface met Azure Blob storage en `UploadBackupFolderAsync` is Hallo-methode die comprimeert Hallo-map en plaatst het in hello Azure Blob-opslag.

Opmerking:

  - Er mag slechts één back-upbewerking onderweg per replica op elk moment. Meer dan één `BackupAsync` aanroep tegelijk genereert `FabricBackupInProgressException` toolimit inflight back-ups tooone.
  - Als een replica mislukt via tijdens een back-up uitgevoerd wordt, kan Hallo back-up niet zijn voltooid. Zodra het Hallo-failover is voltooid, het is dus Hallo-service verantwoordelijkheid toorestart Hallo back-up door aan te roepen `BackupAsync` indien nodig.

## <a name="restore-reliable-services"></a>Reliable Services herstellen
In het algemeen Hallo gevallen wanneer u tooperform een herstelbewerking moet mogelijk worden onderverdeeld in een van deze categorieën:

  - Hallo service partitioneren gegevens verloren gaan. Hallo-schijf voor twee van de drie replica's voor een partitie (met inbegrip van de primaire replica Hallo) opgehaald bijvoorbeeld beschadigd of gewist. de nieuwe primaire Hallo wellicht toorestore gegevens uit een back-up.
  - de hele service Hallo gaat verloren. Bijvoorbeeld, een beheerder Hallo hele service verwijdert en dus Hallo-service en Hallo gegevens moet toobe hersteld.
  - Hallo service gerepliceerd beschadigd toepassingsgegevens (bijv, vanwege een fout van toepassing). In dit geval Hallo-service heeft toobe bijgewerkt of teruggekeerde tooremove Hallo oorzaak van het Hallo-beschadiging en gegevens die niet beschadigd toobe hersteld.

Hoewel veel manieren mogelijk, bieden we enkele voorbeelden voor het gebruik van `RestoreAsync` toorecover van Hallo bovenstaande scenario's.

## <a name="partition-data-loss-in-reliable-services"></a>Partitie gegevensverlies in Reliable Services
In dit geval Hallo runtime automatisch zou gegevensverlies Hallo detecteren en aanroepen Hallo `OnDataLossAsync` API.

Hallo service auteur moet tooperform hello toorecover te volgen:

  - Hallo virtuele basisklassenmethode overschrijven `OnDataLossAsync`.
  - Hallo meest recente back-ups vinden in Hallo een externe locatie op waarin back-ups Hallo-service.
  - Download de meest recente back-up hello (en decomprimeren Hallo back-up naar back-upmap Hallo als het is gecomprimeerd).
  - Hallo `OnDataLossAsync` methode biedt een `RestoreContext`. Hallo aanroepen `RestoreAsync` API op Hallo opgegeven `RestoreContext`.
  - Retourneert waar als de Hallo herstelbewerking is gelukt.

Hieronder volgt een voorbeeld van de implementatie van Hallo `OnDataLossAsync` methode:

```csharp
protected override async Task<bool> OnDataLossAsync(RestoreContext restoreCtx, CancellationToken cancellationToken)
{
    var backupFolder = await this.externalBackupStore.DownloadLastBackupAsync(cancellationToken);

    var restoreDescription = new RestoreDescription(backupFolder);

    await restoreCtx.RestoreAsync(restoreDescription);

    return true;
}
```

`RestoreDescription`doorgegeven toohello `RestoreContext.RestoreAsync` aanroep van een lid genaamd bevat `BackupFolderPath`.
Bij het herstellen van een eenmalige volledige back-up, dit `BackupFolderPath` toohello lokale pad van Hallo map waarin uw volledige back-up moet worden ingesteld.
Bij het herstellen van een volledige back-up en een aantal incrementele back-ups `BackupFolderPath` toohello lokale pad van Hallo map waarin niet alleen volledige back-up hello, maar ook alle Hallo incrementele back-ups moet worden ingesteld.
`RestoreAsync`aanroep kunt throw `FabricMissingFullBackupException` als hello `BackupFolderPath` opgegeven bevat geen een volledige back-up.
Het kan ook de throw `ArgumentException` als `BackupFolderPath` heeft een verbroken keten van incrementele back-ups.
Als het Hallo volledige back-up bevat, bijvoorbeeld Hallo eerst incrementele en Hallo derde incrementele back-up, maar er is geen Hallo tweede incrementele back-up.

> [!NOTE]
> Hallo RestorePolicy is tooSafe standaard ingesteld.  Dit betekent dat Hallo `RestoreAsync` API met ArgumentException mislukken als er die back-upmap Hallo bevat een staat die ouder zijn dan of gelijk zijn toohello status van deze replica wordt gedetecteerd.  `RestorePolicy.Force`kan worden gebruikt tooskip deze veiligheidscontrole. Dit is opgegeven als onderdeel van `RestoreDescription`.
> 

## <a name="deleted-or-lost-service"></a>Verwijderde of verloren-service
Als een service wordt verwijderd, moet u eerst opnieuw maken Hallo service voordat Hallo gegevens kunnen worden hersteld.  Het is belangrijk toocreate Hallo service Hello dezelfde configuratie, bijvoorbeeld partitieschema, zodat die gegevens Hallo naadloos kan worden hersteld.  Zodra het Hallo-service is, Hallo API toorestore gegevens (`OnDataLossAsync` hierboven) heeft toobe aangeroepen voor elke partitie van deze service. Een manier om dat te bereiken dit is met behulp van `[FabricClient.TestManagementClient.StartPartitionDataLossAsync](https://msdn.microsoft.com/library/mt693569.aspx)` op elke partitie.  

Vanaf dit punt is de implementatie Hallo hetzelfde als Hallo bovenstaande scenario. Elke partitie moet toorestore Hallo laatste relevante back-up van Hallo externe winkel. Een voorbehoud is deze ID is mogelijk nu gewijzigd, omdat Hallo runtime partitie-id dynamisch maakt Hallo-partitie. Hallo-service moet dus toostore Hallo juiste partitiegegevens en service naam tooidentify Hallo juist meest recente back-toorestore uit voor elke partitie.

> [!NOTE]
> Het wordt niet aangeraden toouse `FabricClient.ServiceManager.InvokeDataLossAsync` op elke partitie toorestore Hallo hele service, omdat dat de clusterstatus mogelijk beschadigd.
> 

## <a name="replication-of-corrupt-application-data"></a>Replicatie van gegevens beschadigd toepassing
Als de upgrade van de toepassing hello zojuist is geïmplementeerd, heeft een fout, die mogelijk leiden tot beschadiging van gegevens. Bijvoorbeeld, een upgrade van de toepassing mogelijk gaan tooupdate elke telefoon nummer record in een betrouwbare woordenlijst met een ongeldige netnummer.  In dit geval worden Hallo ongeldige telefoonnummers gerepliceerd sinds de Service Fabric is niet bekend met Hallo aard van Hallo-gegevens die worden opgeslagen.

Hallo eerst te beginnen toodo nadat u deze een egregious fout die ervoor zorgt gegevensbeschadiging dat detecteren toofreeze Hallo service is op toepassingsniveau Hallo en, indien mogelijk toohello versie van Hallo toepassingscode die geen Hallo bug niet bijwerken.  Zelfs nadat het Hallo-servicecode is opgelost, Hallo gegevens zijn mogelijk nog steeds beschadigd en gegevens moet daarom mogelijk toobe hersteld.  In dergelijke gevallen niet mogelijk voldoende toorestore Hallo meest recente back-up, sinds de meest recente back-ups Hallo ook mogelijk beschadigd.  U hebt dus toofind Hallo laatste back-up die is gemaakt voordat het Hallo-gegevens zijn beschadigd.

Als u niet zeker welke back-ups zijn beschadigd weet, kan u een nieuwe Service Fabric-cluster implementeren en herstel van Hallo back-ups van betrokken partities net als Hallo hierboven 'Deleted of verloren service' scenario.  Voor elke partitie terug te zetten van Hallo back-ups van de meest recente toohello Hallo minste. Als u een back-up die geen Hallo beschadiging heeft gevonden, verplaatsen en verwijderen alle back-ups van deze partitie die recenter (dan back-up waren). Herhaal dit proces voor elke partitie. Nu als `OnDataLossAsync` wordt aangeroepen op Hallo partitie in een productiecluster Hallo Hallo laatste back-up gevonden in Hallo externe store Hallo een verzameld door Hallo hierboven proces zijn.

Nu Hallo stappen voor het Hallo 'Deleted of verloren service' sectie kan worden gebruikt toorestore Hallo status van de servicestatus toohello Hallo voordat Hallo buggy code beschadigd Hallo status.

Opmerking:

  - Wanneer u herstelt, is er is een kans dat Hallo back-up wordt hersteld ouder dan Hallo status van Hallo partitie voordat Hallo gegevens verloren gegaan. Daarom moet u weer alleen als een laatste toevlucht toorecover zo veel mogelijk gegevens mogelijk.
  - Hallo tekenreeks met Hallo back-upmap pad en hello paden van bestanden in de back-upmap Hallo kunnen niet groter zijn dan 255 tekens, afhankelijk van Hallo FabricDataRoot pad en de lengte van de naam van het toepassingstype. Hierdoor kunnen sommige .NET-methoden zoals `Directory.Move`, toothrow hello `PathTooLongException` uitzondering. Er is een oplossing toodirectly aanroepen kan kernel32-API's, zoals `CopyFile`.

## <a name="backup-and-restore-reliable-actors"></a>Back-up en herstel Reliable Actors


Betrouwbare actoren Framework is ingebouwd in Reliable Services. Hallo ActorService die als host fungeert voor Hallo actor(s) is een stateful betrouwbare service. Daarom alle Hallo back-up en herstel functionaliteit beschikbaar zijn in Reliable Services is ook beschikbaar tooReliable actoren (met uitzondering van het gedrag dat specifieke state-provider zijn). Sinds de back-ups zullen worden uitgevoerd op basis van de per-partitie, statussen voor alle actoren in de betreffende partitie, worden back-up (en herstel lijkt en gebeurt op basis van per partitie). tooperform back-up/herstel, Hallo service-eigenaar moet een aangepaste actor serviceklasse die is afgeleid van klasse ActorService maken en vervolgens back-up/herstel vergelijkbare tooReliable Services zoals hierboven is beschreven in de vorige secties.

```csharp
class MyCustomActorService : ActorService
{
     public MyCustomActorService(StatefulServiceContext context, ActorTypeInformation actorTypeInfo)
            : base(context, actorTypeInfo)
     {                  
     }
    
    //
   // Method overrides and other code.
    //
}
```

Wanneer u een aangepaste actor serviceklasse maakt, moet u tooregister dat ook bij het registreren van Hallo actor.

```csharp
ActorRuntime.RegisterActorAsync<MyActor>(
   (context, typeInfo) => new MyCustomActorService(context, typeInfo)).GetAwaiter().GetResult();
```

Hallo standaard state-provider voor Reliable Actors is `KvsActorStateProvider`. Incrementele back-up is niet standaard ingeschakeld voor `KvsActorStateProvider`. U kunt de incrementele back-up inschakelen door het maken van `KvsActorStateProvider` met Hallo de desbetreffende instelling in de constructor en vervolgens doorgeeft tooActorService constructor zoals weergegeven in het volgende codefragment:

```csharp
class MyCustomActorService : ActorService
{
     public MyCustomActorService(StatefulServiceContext context, ActorTypeInformation actorTypeInfo)
            : base(context, actorTypeInfo, null, null, new KvsActorStateProvider(true)) // Enable incremental backup
     {                  
     }
    
    //
   // Method overrides and other code.
    //
}
```

Nadat de incrementele back-up is ingeschakeld, duurt een incrementele back-up voor een van de volgende redenen mislukken met FabricMissingFullBackupException en moet u tootake een volledige back-up voordat u incrementele backup(s):

  - Hallo replica heeft nooit genomen voor een volledige back-up nadat primaire werd.
  - Aantal logboekrecords Hallo zijn afgebroken sinds laatste back-up is gemaakt.

Wanneer incrementele back-up is ingeschakeld, `KvsActorStateProvider` gebruikt geen circulaire buffer toomanage het logboek vastgelegd en regelmatig worden afgekapt. Als geen back-up wordt gemaakt door gebruiker gedurende een periode van 45 minuten, wordt in Hallo systeem automatisch wordt afgekapt Hallo logboekrecords. Dit interval kan worden geconfigureerd door op te geven `logTrunctationIntervalInMinutes` in `KvsActorStateProvider` constructor (vergelijkbaar toowhen incrementele back-up inschakelen). Hallo logboekrecords kunnen ook ophalen afgekapt als primaire replica moet toobuild aan een andere replica door te sturen alle bijbehorende gegevens.

Bij het uitvoeren van herstel van een back-keten vergelijkbare tooReliable Services moet Hallo BackupFolderPath submappen met een submap met de volledige back-up en anderen submappen met incrementele backup(s) bevatten. Hallo terugzetten API genereert FabricException met het bijbehorende bericht als Hallo upketen validatie mislukt. 

> [!NOTE]
> `KvsActorStateProvider`momenteel worden Hallo optie RestorePolicy.Safe genegeerd. Ondersteuning voor deze functie is in een toekomstige release gepland.
> 

## <a name="testing-backup-and-restore"></a>Testen van back-up en herstel
Het is belangrijk tooensure die kritieke gegevens worden back-up en kan worden hersteld vanuit. Dit kan worden gedaan door aan te roepen Hallo `Start-ServiceFabricPartitionDataLoss` cmdlet in PowerShell die verlies van gegevens in een bepaalde partitie tootest veroorzaken kan of Hallo gegevens back-up en herstel functionaliteit voor uw service werkt zoals verwacht.  Het is ook mogelijk tooprogrammatically aanroepen verlies van gegevens en herstel van die gebeurtenis ook.

> [!NOTE]
> U vindt een Voorbeeldimplementatie van back-up en herstel functionaliteit in Hallo Reference-Web-App op GitHub. Zie Hallo `Inventory.Service` service voor meer informatie.
> 
> 

## <a name="under-hello-hood-more-details-on-backup-and-restore"></a>Achter de schermen Hallo: meer informatie over back-up en herstel
Hier volgt een aantal meer informatie over back-up en herstel.

### <a name="backup"></a>Back-up
Hallo betrouwbare status Manager biedt Hallo mogelijkheid toocreate consistent back-ups zonder blokkering van een lees- of schrijfbewerkingen. toodo dus hierbij wordt gebruikgemaakt van een mechanisme controlepunt- en logboekbestanden.  Hallo betrouwbare statusbeheer fuzzy (lightweight) controlepunten bij bepaalde punten toorelieve druk uit Hallo transactionele logboek neemt en hersteltijden te verbeteren.  Wanneer `BackupAsync` wordt aangeroepen, Hallo betrouwbare statusbeheer Hiermee geeft u alle objecten van betrouwbare toocopy hun meest recente controlepunt bestanden tooa lokale back-upmap.  Hallo betrouwbare status Manager kopieert vervolgens alle logboekrecords Hallo 'start aanwijzer' toohello nieuwste logboekrecord vanaf in Hallo back-upmap.  Aangezien alle Hallo logboekrecords van de meest recente logboekrecord toohello zijn opgenomen in Hallo back-up en Hallo betrouwbare statusbeheer vooraf geschreven logboekregistratie behoudt, Hallo betrouwbare status Manager zorgt ervoor dat alle transacties die toegewezen zijn (`CommitAsync` heeft geretourneerd met succes) zijn opgenomen in Hallo back-up.

De transactie die na doorvoeren `BackupAsync` mei is aangeroepen of mogelijk niet in Hallo back-up.  Zodra het Hallo lokale back-upmap is gevuld door Hallo platform (dat wil zeggen, lokale back-up is voltooid door de runtime Hallo), back-callback Hallo-service is aangeroepen.  Deze retouraanroep is verantwoordelijk voor het verplaatsen van Hallo back-upmap tooan externe locatie bevindt, zoals Azure Storage.

### <a name="restore"></a>Herstellen
Hallo betrouwbare status Manager biedt Hallo mogelijkheid toorestore vanuit een back-up met behulp van Hallo `RestoreAsync` API.  
Hallo `RestoreAsync` methode op `RestoreContext` kunnen worden aangeroepen alleen Hallo `OnDataLossAsync` methode.
Hallo bool geretourneerd door `OnDataLossAsync` geeft aan of Hallo-service de status van een externe bron hersteld.
Als hello `OnDataLossAsync` true retourneert, Service Fabric alle andere replica's van deze primaire opnieuw opgebouwd. Service Fabric zorgt ervoor dat replica's die worden ontvangen `OnDataLossAsync` aanroepen van eerste overgang toohello primaire rol, maar zijn niet verleend status lezen of schrijven status.
Dit houdt in dat voor StatefulService implementeerders, `RunAsync` wordt niet aangeroepen tot `OnDataLossAsync` met succes wordt voltooid.
Vervolgens `OnDataLossAsync` wordt aangeroepen op de nieuwe primaire Hallo.
Totdat een service deze API is (met retourneert true of false voltooit) en relevante Hallo-herconfiguratie is voltooid, wordt Hallo API behouden wordt aangeroepen één tegelijk.

`RestoreAsync`alle bestaande status in Hallo primaire replica die is aangeroepen op eerst verwijderd.  
Hallo betrouwbare statusbeheer maakt vervolgens alle Hallo betrouwbare objecten die zijn opgenomen in de back-upmap Hallo.  
Hallo betrouwbare objecten zijn vervolgens gebruiksaanwijzing toorestore uit hun controlepunten in de back-upmap Hallo.  
Ten slotte Hallo betrouwbare status Manager een eigen staat vanuit Hallo logboekrecords in de back-upmap Hallo herstelt en wordt een herstelbewerking uitgevoerd.  
Als onderdeel van het herstelproces Hallo zijn vanaf Hallo 'beginpunt' bewerkingen waarvoor logboekrecords doorvoeren in de back-upmap Hallo herhaald toohello betrouwbare objecten.  
Deze stap zorgt ervoor dat Hallo herstelde status consistent is.

## <a name="next-steps"></a>Volgende stappen
  - [Betrouwbare verzamelingen](service-fabric-work-with-reliable-collections.md)
  - [Betrouwbare Services snel starten](service-fabric-reliable-services-quick-start.md)
  - [Betrouwbare Services meldingen](service-fabric-reliable-services-notifications.md)
  - [Configuratie van betrouwbare Services](service-fabric-reliable-services-configuration.md)
  - [Referentie voor ontwikkelaars voor betrouwbare verzamelingen](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

