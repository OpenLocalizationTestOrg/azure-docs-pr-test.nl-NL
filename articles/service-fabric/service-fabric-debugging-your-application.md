---
title: aaaDebug uw toepassing in Visual Studio | Microsoft Docs
description: Hallo-betrouwbaarheid en prestaties van uw services verbeteren door te ontwikkelen en ze op een lokaal ontwikkelcluster foutopsporing in Visual Studio.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: cb888532-bcdb-4e47-95e4-bfbb1f644da4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: vturecek;mikhegn
ms.openlocfilehash: 8d08689e82195d09f57b462631ad04fd237bc4fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-service-fabric-application-by-using-visual-studio"></a>Fouten opsporen in uw Service Fabric-toepassing met behulp van Visual Studio
> [!div class="op_single_selector"]
> * [Visual Studio/CSharp](service-fabric-debugging-your-application.md) 
> * [Eclipse/Java](service-fabric-debugging-your-application-java.md)
>


## <a name="debug-a-local-service-fabric-application"></a>Fouten opsporen in een lokale Service Fabric-toepassing
U kunt tijd en geld besparen door te implementeren en foutopsporing van uw Azure Service Fabric-toepassing in een cluster van de ontwikkeling van lokale computer. Visual Studio 2017 of Visual Studio 2015 Hallo toepassing toohello lokale cluster implementeren en automatisch verbinding Hallo foutopsporingsprogramma tooall exemplaren van uw toepassing.

1. Een lokaal ontwikkelcluster starten door de stappen te volgen Hallo in [instellen van uw ontwikkelomgeving Service Fabric](service-fabric-get-started.md).
2. Druk op **F5** of klik op **Debug** > **foutopsporing starten**.
   
    ![Foutopsporing van een toepassing starten][startdebugging]
3. Onderbrekingspunten instellen in uw code en de toepassing hello stap voor stap door te klikken op de opdrachten in Hallo **Debug** menu.
   
   > [!NOTE]
   > Visual Studio koppelt tooall exemplaren van uw toepassing. Terwijl u de code hebt doorlopen, kunnen onderbrekingspunten ophalen geraakt door meerdere processen, wat resulteert in gelijktijdige sessies. Probeer Hallo onderbrekingspunten uitschakelen nadat ze zijn bereikt door middel van elke onderbrekingspunt voorwaardelijke op Hallo thread-ID of met behulp van diagnostische gebeurtenissen.
   > 
   > 
4. Hallo **diagnostische gebeurtenissen** venster wordt automatisch geopend zodat u de diagnostische gebeurtenissen in realtime kunt bekijken.
   
    ![Diagnostische gebeurtenissen in realtime weergeven][diagnosticevents]
5. U kunt ook openen Hallo **diagnostische gebeurtenissen** venster in de Cloud Explorer.  Onder **Service Fabric**, met de rechtermuisknop op een willekeurig knooppunt en kiest u **weergave Streaming traceringen**.
   
    ![Open Hallo diagnostische gebeurtenissen venster][viewdiagnosticevents]
   
    Als u toofilter uw traceringen tooa specifieke service of toepassing wilt, schakel gewoon streaming traces op die specifieke service of toepassing.
6. Hallo diagnostische gebeurtenissen worden weergegeven in Hallo automatisch gegenereerd **ServiceEventSource.cs** bestand en worden aangeroepen vanuit de toepassingscode.
   
    ```csharp
    ServiceEventSource.Current.ServiceMessage(this, "My ServiceMessage with a parameter {0}", result.Value.ToString());
    ```
7. Hallo **diagnostische gebeurtenissen** venster biedt ondersteuning voor filteren, onderbreken en gebeurtenissen in realtime te bekijken.  Hallo-filter is een eenvoudige tekenreeks zoekactie van Hallo gebeurtenisbericht, met inbegrip van de inhoud ervan.
   
    ![Filteren, onderbreken en hervatten of gebeurtenissen in realtime controleren][diagnosticeventsactions]
8. Services-foutopsporing is vergelijkbaar met een andere toepassing voor foutopsporing. U wordt normaal gesproken onderbrekingspunten met Visual Studio voor het opsporen van eenvoudige instellen. Hoewel betrouwbare verzamelingen over meerdere knooppunten repliceren, ze nog steeds IEnumerable is geïmplementeerd. Dit betekent dat u Hallo resultaten weergeven in Visual Studio gebruiken kunt tijdens het opsporen van toosee wat u hebt opgeslagen in. Gewoon een onderbrekingspunt instellen overal in uw code.
   
    ![Foutopsporing van een toepassing starten][breakpoint]

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="debug-a-remote-service-fabric-application"></a>Fouten opsporen in een externe Service Fabric-toepassing
Als uw Service Fabric-toepassingen worden uitgevoerd op een Service Fabric-cluster in Azure, u zich tooremotely fouten opsporen in deze rechtstreeks vanuit Visual Studio.

> [!NOTE]
> Hallo-onderdeel vereist [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) en [Azure SDK voor .NET 2.9](https://azure.microsoft.com/downloads/).    
> 
> 

<!-- -->
> [!WARNING]
> Foutopsporing op afstand is bedoeld voor ontwikkel-/ Testscenario's en niet toobe gebruikt in een productieomgeving vanwege Hallo impact op Hallo uitvoeren van toepassingen.
> 
> 

1. Navigeer tooyour cluster in **Cloud Explorer**, klik met de rechtermuisknop en kies **foutopsporing inschakelen**
   
    ![Foutopsporing op afstand inschakelen][enableremotedebugging]
   
    Dit wordt ere van Hallo proces van het Hallo-extensie op uw clusterknooppunten foutopsporing op afstand inschakelen, evenals netwerkconfiguraties vereist.
2. Klik met de rechtermuisknop Hallo clusterknooppunt in **Cloud Explorer**, en kies **foutopsporingsprogramma koppelen**
   
    ![Foutopsporingsprogramma koppelen][attachdebugger]
3. In Hallo **koppelen tooprocess** dialoogvenster Kies Hallo proces u toodebug wilt en klikt u op **koppelen**
   
    ![Kies proces][chooseprocess]
   
    de naam van de Hallo Hallo proces dat u wilt dat tooattach aan, gelijk is aan de naam van het assembly-naam van uw service-project Hallo.
   
    Hallo-foutopsporingsprogramma koppelt tooall knooppunten Hallo process uitgevoerd.
   
   * In geval van Hallo waar u fouten een stateless service opspoort, uitmaken alle exemplaren van Hallo-service op alle knooppunten deel van Hallo foutopsporingssessie.
   * Als u fouten een stateful service opspoort, worden alleen Hallo primaire replica van een partitie actief en daarom bijgewerkt door Hallo foutopsporingsprogramma. Als de primaire replica Hallo tijdens de foutopsporingssessie hello verplaatst, wordt Hallo verwerking van die replica nog steeds deel uitmaken van Hallo foutopsporingssessie.
   * In de volgorde tooonly catch relevante partities of verschillende exemplaren van een bepaalde service, kunt u voorwaardelijke onderbrekingspunten tooonly einde een specifieke partitie of het exemplaar.
     
     ![Voorwaardelijke onderbrekingspunt][conditionalbreakpoint]
     
     > [!NOTE]
     > Momenteel wij bieden geen ondersteuning voor foutopsporing van een Service Fabric-cluster met meerdere exemplaren van Hallo dezelfde uitvoerbare service-naam.
     > 
     > 
4. Nadat u fouten opspoort in uw toepassing hebt, kunt u Hallo externe foutopsporing uitbreiding uitschakelen door met de rechtermuisknop op Hallo-cluster in **Cloud Explorer** en kies **foutopsporing uitschakelen**
   
    ![Foutopsporing op afstand uitschakelen][disableremotedebugging]

## <a name="streaming-traces-from-a-remote-cluster-node"></a>Streaming traceringen vanaf een externe clusterknooppunt
Bent u ook kunnen toostream traceringen rechtstreeks vanuit een externe cluster knooppunt tooVisual Studio. Deze functie kunt u toostream ETW-traceringsgebeurtenissen, op het knooppunt van een Service Fabric-cluster geproduceerd.

> [!NOTE]
> Dit onderdeel vereist [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) en [Azure SDK voor .NET 2.9](https://azure.microsoft.com/downloads/).
> Deze functie ondersteunt alleen clusters die worden uitgevoerd in Azure.
> 
> 

<!-- -->
> [!WARNING]
> Streaming traceringen is bedoeld voor ontwikkel-/ Testscenario's en niet toobe gebruikt in een productieomgeving vanwege Hallo impact op Hallo uitvoeren van toepassingen.
> In een productiescenario verstandig doorsturen van gebeurtenissen met behulp van Azure Diagnostics.
> 
> 

1. Navigeer tooyour cluster in **Cloud Explorer**, klik met de rechtermuisknop en kies **Streaming traceringen inschakelen**
   
    ![Externe streaming traceringen inschakelen][enablestreamingtraces]
   
    Dit wordt ere van Hallo proces van het inschakelen van Hallo streaming traceringen-extensie op uw clusterknooppunten, evenals netwerkconfiguraties vereist.
2. Vouw Hallo **knooppunten** -element in **Cloud Explorer**, klik met de rechtermuisknop Hallo knooppunt gewenste toostream traceringen uit en kies **weergave Streaming traceringen**
   
    ![Externe streaming traceringen weergeven][viewremotestreamingtraces]
   
    Herhaal stap 2 voor zoveel knooppunten gewenste toosee traceringen uit. Elke stroom knooppunten wordt in een speciale venster weergegeven.
   
    U bent nu kunnen toosee Hallo traceringen verzonden door het Service Fabric en uw services. Als u een specifieke toepassing toofilter Hallo gebeurtenissen tooonly weergeven wilt, typ gewoon in Hallo-naam van de toepassing hello in Hallo filter.
   
    ![Streaming traceringen weergeven][viewingstreamingtraces]
3. Wanneer u klaar bent streaming traceringen van uw cluster, kunt u externe streaming traceringen, uitschakelen met de rechtermuisknop op Hallo-cluster in **Cloud Explorer** en kies **Streaming traceringen uitschakelen**
   
    ![Externe streaming traceringen uitschakelen][disablestreamingtraces]

## <a name="next-steps"></a>Volgende stappen
* [Een Service Fabric-service testen](service-fabric-testability-overview.md).
* [Beheren van uw Service Fabric-toepassingen in Visual Studio](service-fabric-manage-application-in-visual-studio.md).

<!--Image references-->
[startdebugging]: ./media/service-fabric-debugging-your-application/startdebugging.png
[diagnosticevents]: ./media/service-fabric-debugging-your-application/diagnosticevents.png
[viewdiagnosticevents]: ./media/service-fabric-debugging-your-application/viewdiagnosticevents.png
[diagnosticeventsactions]: ./media/service-fabric-debugging-your-application/diagnosticeventsactions.png
[breakpoint]: ./media/service-fabric-debugging-your-application/breakpoint.png
[enableremotedebugging]: ./media/service-fabric-debugging-your-application/enableremotedebugging.png
[attachdebugger]: ./media/service-fabric-debugging-your-application/attachdebugger.png
[chooseprocess]: ./media/service-fabric-debugging-your-application/chooseprocess.png
[conditionalbreakpoint]: ./media/service-fabric-debugging-your-application/conditionalbreakpoint.png
[disableremotedebugging]: ./media/service-fabric-debugging-your-application/disableremotedebugging.png
[enablestreamingtraces]: ./media/service-fabric-debugging-your-application/enablestreamingtraces.png
[viewingstreamingtraces]: ./media/service-fabric-debugging-your-application/viewingstreamingtraces.png
[viewremotestreamingtraces]: ./media/service-fabric-debugging-your-application/viewremotestreamingtraces.png
[disablestreamingtraces]: ./media/service-fabric-debugging-your-application/disablestreamingtraces.png
