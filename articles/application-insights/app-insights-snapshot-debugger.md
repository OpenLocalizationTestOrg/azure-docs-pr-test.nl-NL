---
title: aaaAzure Application Insights momentopname foutopsporingsprogramma voor .NET-toepassingen | Microsoft Docs
description: Fouten opsporen in momentopnamen worden automatisch verzameld wanneer uitzonderingen worden veroorzaakt in productie .NET-toepassingen
services: application-insights
documentationcenter: 
author: qubitron
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: bwren
ms.openlocfilehash: f0173a752b5795d934fbab1bd53eb077433edc90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="debug-snapshots-on-exceptions-in-net-apps"></a>Fouten opsporen in momentopnamen op uitzonderingen in .NET-toepassingen

Wanneer er een uitzondering optreedt, kunt u automatisch een debug-momentopname verzamelen van uw live-webtoepassing. Hallo momentopname toont Hallo status van de broncode en variabelen op Hallo momenteel Hallo uitzondering is opgetreden. Hallo momentopname foutopsporingsprogramma (preview) in [Azure Application Insights](app-insights-overview.md) uitzonderingstelemetrie van uw web-app wordt bewaakt. Deze verzamelt momentopnamen op uw eerste ArgumentOutOfRangeException uitzonderingen zodat u Hallo-informatie die u toodiagnose problemen in productie nodig hebt. Hallo omvatten [momentopname collector NuGet-pakket](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) in uw toepassing, en desgewenst verzameling parameters in configureren [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Momentopnamen worden weergegeven op [uitzonderingen](app-insights-asp-net-exceptions.md) in Hallo Application Insights-portal.

U kunt momentopnamen voor foutopsporing weergeven in Hallo portal toosee Hallo aanroepstack en variabelen op elke aanroepstackframe controleren. een krachtigere foutopsporing ervaring met broncode, open momentopnamen met Visual Studio 2017 Enterprise door tooget [Hallo momentopname Debugger-extensie voor Visual Studio downloaden](https://aka.ms/snapshotdebugger).

Verzameling van de momentopname is beschikbaar voor:
* .NET framework en ASP.NET-toepassingen met .NET Framework 4.5 of hoger.
* .NET core 2.0 en ASP.NET Core 2.0-toepassingen worden uitgevoerd op Windows.

### <a name="configure-snapshot-collection-for-aspnet-applications"></a>Momentopname verzamelen voor ASP.NET-toepassingen configureren

1. [Application Insights inschakelen in uw web-app](app-insights-asp-net.md), als u dit nog niet hebt gedaan.

2. Hallo omvatten [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet-pakket in uw app. 

3. Hallo standaardopties die Hallo pakket toegevoegd te bekijken[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):

    ```xml
    <TelemetryProcessors>
        <Add Type="Microsoft.ApplicationInsights.SnapshotCollector.SnapshotCollectorTelemetryProcessor, Microsoft.ApplicationInsights.SnapshotCollector">
        <!-- hello default is true, but you can disable Snapshot Debugging by setting it toofalse -->
        <IsEnabled>true</IsEnabled>
        <!-- Snapshot Debugging is usually disabled in developer mode, but you can enable it by setting this tootrue. -->
        <!-- DeveloperMode is a property on hello active TelemetryChannel. -->
        <IsEnabledInDeveloperMode>false</IsEnabledInDeveloperMode>
        <!-- How many times we need toosee an exception before we ask for snapshots. -->
        <ThresholdForSnapshotting>5</ThresholdForSnapshotting>
        <!-- hello maximum number of examples we create for a single problem. -->
        <MaximumSnapshotsRequired>3</MaximumSnapshotsRequired>
        <!-- hello maximum number of problems that we can be tracking at any time. -->
        <MaximumCollectionPlanSize>50</MaximumCollectionPlanSize>
        <!-- How often tooreset problem counters. -->
        <ProblemCounterResetInterval>06:00:00</ProblemCounterResetInterval>
        <!-- hello maximum number of snapshots allowed in one minute. -->
        <SnapshotsPerMinuteLimit>2</SnapshotsPerMinuteLimit>
        <!-- hello maximum number of snapshots allowed per day. -->
        <SnapshotsPerDayLimit>50</SnapshotsPerDayLimit>
        </Add>
    </TelemetryProcessors>
    ```

4. Momentopnamen worden verzameld alleen op uitzonderingen die gemeld tooApplication Insights worden. In sommige gevallen (bijvoorbeeld oudere versies van .NET-platform Hallo), moet u wellicht te[uitzondering verzamelen configureren](app-insights-asp-net-exceptions.md#exceptions) toosee uitzonderingen met momentopnamen in Hallo-portal.


### <a name="configure-snapshot-collection-for-aspnet-core-20-applications"></a>Momentopname verzamelen voor ASP.NET Core 2.0-toepassingen configureren

1. [Application Insights inschakelen in uw web-app van ASP.NET Core](app-insights-asp-net-core.md), als u dit nog niet hebt gedaan.

2. Hallo omvatten [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet-pakket in uw app.

3. Hallo wijzigen `ConfigureServices` methode in uw toepassing `Startup` tooadd Hallo momentopname van Collector telemetrie processor klasse. Hallo-code die moet worden toegevoegd, is afhankelijk van Hallo waarnaar wordt verwezen versie Hallo Microsoft.ApplicationInsights.ASPNETCore NuGet-pakket.

   Voeg voor Microsoft.ApplicationInsights.AspNetCore 2.1.0 toe:
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       // This method is called by hello runtime. Use it tooadd services toohello container.
       public void ConfigureServices(IServiceCollection services)
       {
           services.AddSingleton<Func<ITelemetryProcessor, ITelemetryProcessor>>(next => new SnapshotCollectorTelemetryProcessor(next));
           // TODO: Add any other services your application needs here.
       }
   }
   ```

   Voeg voor Microsoft.ApplicationInsights.AspNetCore 2.1.1 toe:
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       private class SnapshotCollectorTelemetryProcessorFactory : ITelemetryProcessorFactory
       {
           public ITelemetryProcessor Create(ITelemetryProcessor next) =>
               new SnapshotCollectorTelemetryProcessor(next);
       }

       // This method is called by hello runtime. Use it tooadd services toohello container.
       public void ConfigureServices(IServiceCollection services)
       {
            services.AddSingleton<ITelemetryProcessorFactory>(new SnapshotCollectorTelemetryProcessorFactory());
           // TODO: Add any other services your application needs here.
       }
   }
   ```

### <a name="configure-snapshot-collection-for-other-net-applications"></a>Momentopname verzamelen voor andere .NET-toepassingen configureren

1. Als uw toepassing is niet al zijn geïnstrumenteerd met Application Insights, aan de slag door [inschakelen van Application Insights en instelling Hallo instrumentatiesleutel](app-insights-windows-desktop.md).

2. Hallo toevoegen [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet-pakket in uw app.

3. Momentopnamen worden verzameld alleen op uitzonderingen die gemeld tooApplication Insights worden. Mogelijk moet u toomodify uw code tooreport ze. Hallo uitzonderingsverwerking-code is afhankelijk van Hallo-structuur van uw toepassing, maar een voorbeeld lager is dan:
    ```C#
   TelemetryClient _telemetryClient = new TelemetryClient();

   void ExampleRequest()
   {
        try
        {
            // TODO: Handle hello request.
        }
        catch (Exception ex)
        {
            // Report hello exception tooApplication Insights.
            _telemetryClient.TrackException(ex);

            // TODO: Rethrow hello exception if desired.
        }
   }
    ```
    
## <a name="grant-permissions"></a>Machtigingen toekennen

Eigenaren van hello Azure-abonnement kunnen inspecteren momentopnamen. Andere gebruikers moet machtiging worden verleend door een eigenaar.

toogrant machtiging toewijzen Hallo `Application Insights Snapshot Debugger` rol toousers die momentopnamen inspecteert. Deze rol kan worden toegewezen tooindividual gebruikers of groepen door abonnementseigenaren voor Hallo doel Application Insights-resource of de resourcegroep of abonnement.

1. Hallo Access Control (IAM) blade geopend.
1. Klik op Hallo + knop toevoegen.
1. Selecteer Application Insights momentopname foutopsporingsprogramma van Hallo rollen vervolgkeuzelijst.
1. Zoeken en geef een naam voor Hallo gebruiker tooadd.
1. Klik op Hallo opslaan knop tooadd hello toohello gebruikersrol.


[!IMPORTANT]
    Momentopnamen kunnen mogelijk persoonlijke en andere gevoelige gegevens in waarden van variabelen en parameter bevatten.

## <a name="debug-snapshots-in-hello-application-insights-portal"></a>Fouten opsporen in momentopnamen in Hallo Application Insights-portal

Als een momentopname beschikbaar voor een bepaalde uitzondering of een probleem-ID is, een **fouten opsporen in momentopname openen** knop wordt weergegeven op Hallo [uitzondering](app-insights-asp-net-exceptions.md) in Hallo Application Insights-portal.

![De knop openen fouten opsporen in momentopname op uitzondering](./media/app-insights-snapshot-debugger/snapshot-on-exception.png)

In de weergave fouten opsporen in momentopname hello ziet u een aanroepstack en een deelvenster Variabelen. Wanneer u selecteert frames van Hallo aanroep op Hallo call stack deelvenster geplaatst, kunt u lokale variabelen weergeven en parameters voor die functie-aanroep in Hallo variabelen deelvenster.

![Weergave fouten opsporen in momentopname in Hallo-portal](./media/app-insights-snapshot-debugger/open-snapshot-portal.png)

Momentopnamen kunnen gevoelige gegevens bevatten, en ze zijn standaard niet zichtbaar. tooview momentopnamen, moet u Hallo hebben `Application Insights Snapshot Debugger` tooyou rol die is toegewezen.

## <a name="debug-snapshots-with-visual-studio-2017-enterprise"></a>Fouten opsporen in momentopnamen met Visual Studio 2017 Enterprise
1. Klik op Hallo **momentopname downloaden** knop toodownload een `.diagsession` bestand, dat kan worden geopend door Visual Studio 2017 Enterprise. 

2. Hallo tooopen `.diagsession` -bestand, moet u eerst [downloaden en installeren van Hallo momentopname Debugger-extensie voor Visual Studio](https://aka.ms/snapshotdebugger).

3. Nadat u Hallo momentopnamebestand opent, Hallo Minidump foutopsporing pagina in Visual Studio geopend. Klik op **fouten opsporen in beheerde Code** toostart Hallo momentopname foutopsporing. Hallo momentopname wordt geopend toohello coderegel waar Hallo uitzondering is opgetreden, zodat u fouten Hallo huidige status van het Hallo-proces opsporen kunt.

    ![Weergave foutopsporing momentopname in Visual Studio](./media/app-insights-snapshot-debugger/open-snapshot-visualstudio.png)

Hallo gedownloade momentopname bevat symboolbestanden die zijn gevonden op de webserver van de toepassing. Deze symboolbestanden zijn vereiste tooassociate momentopnamegegevens met broncode. Voor App Service-apps, zorg ervoor dat tooenable symbool implementatie wanneer u uw web-apps publiceren.

## <a name="how-snapshots-work"></a>De werking van momentopnamen

Wanneer uw toepassing wordt gestart, moet op een afzonderlijke momentopname uploader proces dat uw toepassing voor aanvragen van de momentopname bewaakt wordt gemaakt. Wanneer een momentopname wordt aangevraagd, wordt een schaduwkopie van Hallo process uitgevoerd aangebracht in ongeveer 10 too20 minuten. Hallo shadow proces vervolgens wordt geanalyseerd en een momentopname wordt gemaakt terwijl de Hallo hoofdproces nog steeds toorun en verkeer toousers fungeren. Hallo momentopname is vervolgens geüploade tooApplication Insights samen met eventuele relevante (.pdb)-symboolbestanden die zijn vereist tooview Hallo momentopname.

## <a name="current-limitations"></a>Huidige beperkingen

### <a name="publish-symbols"></a>Symbolen publiceren
Hallo momentopname foutopsporingsprogramma vereist symboolbestanden op Hallo productie-toodecode servervariabelen en tooprovide een foutopsporing ervaring in Visual Studio. Hallo 15.2 versie van Visual Studio 2017 publiceert symbolen voor release builds standaard, wanneer het tooApp Service publiceert. In eerdere versies, moet u tooadd Hallo volgende regel tooyour publicatieprofiel `.pubxml` zodat symbolen zijn gepubliceerd in de releasemodus bestand:

```xml
    <ExcludeGeneratedDebugSymbol>False</ExcludeGeneratedDebugSymbol>
```

Voor Azure Compute en andere typen ervoor te zorgen dat de symboolbestanden Hallo Hallo dezelfde map van Hallo hoofdtoepassing .dll (meestal `wwwroot/bin`) of op het huidige pad Hallo beschikbaar zijn.

### <a name="optimized-builds"></a>Geoptimaliseerde builds
In sommige gevallen kunnen geen lokale variabelen worden weergegeven in de release builds vanwege optimalisaties die worden toegepast tijdens het maken van een Hallo.

## <a name="troubleshooting"></a>Problemen oplossen

De volgende tips helpen u problemen oplossen met Hallo momentopname foutopsporingsprogramma.

### <a name="verify-hello-instrumentation-key"></a>Controleer of de instrumentatiesleutel Hallo

Zorg ervoor dat u de juiste instrumentatiesleutel Hallo in uw gepubliceerde toepassing. Application Insights leest meestal Hallo instrumentatiesleutel van Hallo ApplicationInsights.config-bestand. Controleer of dat Hallo waarde dezelfde is Hallo als Hallo instrumentatiesleutel voor Hallo Application Insights-resource dat u in Hallo-portal ziet.

### <a name="check-hello-uploader-logs"></a>Hallo uploader logboeken controleren

Nadat een momentopname is gemaakt, wordt een bestand met Mini-geheugendump (dmp) op schijf gemaakt. Een afzonderlijke uploader proces duurt dat minidump-bestand en uploadt, samen met eventuele bijbehorende-PDB-bestanden, tooApplication Insights momentopname foutopsporingsprogramma opslag. Nadat het Hallo minidump heeft geüpload, wordt deze verwijderd van de schijf. Hallo-logboekbestanden voor Hallo minidump uploader worden bewaard op de schijf. In een App Service-omgeving vindt u deze logboeken in `D:\Home\LogFiles\Uploader_*.log`. Gebruik Hallo Kudu management site voor App Service-toofind deze logboekbestanden.

1. Open uw App Service-toepassing hello Azure-portal.

2. Selecteer Hallo **geavanceerde hulpmiddelen** blade of zoeken naar **Kudu**.
3. Klik op **gaat**.
4. In Hallo **-console voor foutopsporing** vervolgkeuzelijst de optie **CMD**.
5. Klik op **logboekbestanden**.

Er is ten minste één bestand met een naam die met begint `Uploader_` en een `.log` extensie. Klik op Hallo juiste pictogram toodownload alle logboekbestanden of in een browser openen.
Hallo-bestandsnaam bevat Hallo machine-naam. Als uw App Service-exemplaar wordt gehost op meer dan één computer, moet u er aparte logboekbestanden voor elke computer zijn. Wanneer Hallo uploader een nieuw minidump-bestand detecteert, vastgelegd in het logboekbestand Hallo. Hier volgt een voorbeeld van een geslaagde upload:

```
MinidumpUploader.exe Information: 0 : Dump available 139e411a23934dc0b9ea08a626db16c5.dmp
    DateTime=2017-05-25T14:25:08.0349846Z
MinidumpUploader.exe Information: 0 : Uploading D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp, 329.12 MB
    DateTime=2017-05-25T14:25:16.0145444Z
MinidumpUploader.exe Information: 0 : Upload successful.
    DateTime=2017-05-25T14:25:42.9164120Z
MinidumpUploader.exe Information: 0 : Extracting PDB info from D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp.
    DateTime=2017-05-25T14:25:42.9164120Z
MinidumpUploader.exe Information: 0 : Matched 2 PDB(s) with local files.
    DateTime=2017-05-25T14:25:44.2310982Z
MinidumpUploader.exe Information: 0 : Stamp does not want any of our matched PDBs.
    DateTime=2017-05-25T14:25:44.5435948Z
MinidumpUploader.exe Information: 0 : Deleted D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp
    DateTime=2017-05-25T14:25:44.6095821Z
```

In het vorige voorbeeld Hallo Hallo instrumentatiesleutel is `c12a605e73c44346a984e00000000000`. Deze waarde moet overeenkomen met de instrumentatiesleutel Hallo voor uw toepassing.
Hallo minidump is gekoppeld aan een momentopname met de ID Hallo `139e411a23934dc0b9ea08a626db16c5`. U kunt deze ID hoger toolocate Hallo uitzonderingstelemetrie in Application Insights Analytics die is gekoppeld.

Hallo uploader scant op nieuwe-PDB-bestanden over om de 15 minuten. Hier volgt een voorbeeld:

```
MinidumpUploader.exe Information: 0 : PDB rescan requested.
    DateTime=2017-05-25T15:11:38.8003886Z
MinidumpUploader.exe Information: 0 : Scanning D:\home\site\wwwroot\ for local PDBs.
    DateTime=2017-05-25T15:11:38.8003886Z
MinidumpUploader.exe Information: 0 : Scanning D:\local\Temporary ASP.NET Files\root\a6554c94\e3ad6f22\assembly\dl3\81d5008b\00b93cc8_dec5d201 for local PDBs.
    DateTime=2017-05-25T15:11:38.8160276Z
MinidumpUploader.exe Information: 0 : Local PDB scan complete. Found 2 PDB(s).
    DateTime=2017-05-25T15:11:38.8316450Z
MinidumpUploader.exe Information: 0 : Deleted PDB scan marker D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\.pdbscan.
    DateTime=2017-05-25T15:11:38.8316450Z
```

Voor toepassingen die zijn _niet_ Hallo uploader logboeken worden gehost in App Service, in Hallo dezelfde map als Hallo minidumps: `%TEMP%\Dumps\<ikey>` (waarbij `<ikey>` is uw instrumentatiesleutel).

### <a name="use-application-insights-search-toofind-exceptions-with-snapshots"></a>Gebruik Application Insights zoeken toofind uitzonderingen met momentopnamen

Wanneer een momentopname wordt gemaakt, is er uitzondering is opgetreden Hallo gecodeerd met een momentopname-ID. Wanneer Hallo-uitzonderingstelemetrie gemelde tooApplication inzichten, is die momentopname-ID opgenomen als een aangepaste eigenschap. Hallo Search-blade met in Application Insights kunt u alle telemetrie Hello vinden `ai.snapshot.id` aangepaste eigenschap.

1. Blader tooyour Application Insights-resource in hello Azure-portal.
2. Klik op **Search**.
3. Type `ai.snapshot.id` in Hallo zoekvak en druk op Enter.

![Zoeken naar telemetrie met een momentopname-ID in Hallo-portal](./media/app-insights-snapshot-debugger/search-snapshot-portal.png)

Als deze zoekopdracht geen resultaten oplevert, zijn er zijn geen momentopnamen gemelde tooApplication inzichten voor uw toepassing in het tijdsbereik Hallo geselecteerd.

die ID toosearch voor een specifieke momentopname-ID van Hallo Uploader Logboeken, typ in het zoekvak Hallo. Als u geen telemetrie voor een momentopname waarvan u weet dat is geüpload vinden, voert u de volgende stappen uit:

1. Controleer dat u hello rechts Application Insights-resource bekijkt door Hallo instrumentatiesleutel te verifiëren.

2. Met tijdstempel Hallo uit Hallo Uploader logboek, aanpassen Hallo tijdsbereik filter van Hallo zoeken toocover die tijdsbereik.

Als u een uitzondering met die ID momentopname niet ziet, niet-uitzonderingstelemetrie Hallo gemelde tooApplication Insights. Deze situatie kan zich voordoen als uw toepassing is vastgelopen na het heeft geduurd Hallo momentopname maar voordat het Hallo-uitzonderingstelemetrie gerapporteerd. In dit geval controleren Hallo App Service-Logboeken onder `Diagnose and solve problems` toosee als er onverwacht opnieuw wordt opgestart of onverwerkte uitzonderingen.

## <a name="next-steps"></a>Volgende stappen

* [Snappoints instellen in uw code](https://azure.microsoft.com/blog/snapshot-debugger-for-azure/) tooget momentopnamen zonder te wachten op een uitzondering.
* [Diagnose van uitzonderingen in uw web-apps](app-insights-asp-net-exceptions.md) wordt uitgelegd hoe toomake meer uitzonderingen zichtbaar tooApplication Insights. 
* [Detectie van smartcard](app-insights-proactive-diagnostics.md) detecteert automatisch afwijkingen.
