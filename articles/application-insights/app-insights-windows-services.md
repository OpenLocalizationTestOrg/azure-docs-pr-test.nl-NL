---
title: aaaAzure Application Insights voor Windows server- en werkrollen rollen | Microsoft Docs
description: Handmatig toevoegen Hallo Application Insights-SDK tooyour ASP.NET-toepassing tooanalyze gebruik, beschikbaarheid en prestaties.
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 106ba99b-b57a-43b8-8866-e02f626c8190
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: 64643ef637195d10f87fc6020a77169bca66c1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manually-configure-application-insights-for-net-applications"></a>Application Insights handmatig configureren voor .NET-toepassingen

U kunt configureren [Application Insights](app-insights-overview.md) toomonitor tal van toepassingen of toepassing functies, onderdelen of microservices. Voor web-apps en services biedt Visual Studio [configuratie in één stap](app-insights-asp-net.md). Voor andere typen .NET-toepassingen, zoals back-end-serverfuncties of -desktoptoepassingen, kunt u Application Insights handmatig configureren.

![Voorbeeld van grafieken met prestatiebewaking](./media/app-insights-windows-services/10-perf.png)

#### <a name="before-you-start"></a>Voordat u begint

U hebt de volgende zaken nodig:

* Een abonnement te[Microsoft Azure](http://azure.com). Als uw team of organisatie een Azure-abonnement heeft, Hallo kan eigenaar u toevoegen tooit, met behulp van uw [Microsoft-account](http://live.com).
* Visual Studio 2013 of later.

## <a name="add"></a>1. Een Application Insights-resource kiezen

Hallo 'resource' is waar uw gegevens worden verzameld en weergegeven in hello Azure-portal. Moet u toodecide of toocreate een nieuwe, of een bestaande bestandsshare.

### <a name="part-of-a-larger-app-use-existing-resource"></a>Onderdeel van een grotere app: bestaande resource gebruiken

Als uw webtoepassing verschillende onderdelen - bijvoorbeeld een front-web-app en een of meer back-end-services heeft - er moet voor het verzenden van telemetrie vanaf alle Hallo onderdelen toohello dezelfde resource. Dit wordt deze weergegeven op een enkele toepassing kaart toobe inschakelen en maken het mogelijk tootrace een aanvraag van een onderdeel tooanother.

Dus als u bent al andere onderdelen van deze app bewaken, klikt u vervolgens alleen gebruik Hallo dezelfde resource.

Hallo-resource openen in Hallo [Azure-portal](https://portal.azure.com/). 

### <a name="self-contained-app-create-a-new-resource"></a>Zelfstandige app: nieuwe resource maken

Als nieuwe Hallo-app niet van belang tooother toepassingen is, moet dit een eigen resource hebben.

Meld u aan toohello [Azure-portal](https://portal.azure.com/), en maak een nieuwe Application Insights-resource. Kies ASP.NET als Hallo toepassingstype.

![Klik op Nieuw > Application Insights](./media/app-insights-windows-services/01-new-asp.png)

Hallo gekozen toepassingstype wordt de Standaardinhoud Hallo van Hallo resourceblades.

## <a name="2-copy-hello-instrumentation-key"></a>2. Hallo Instrumentatiesleutel kopiëren
Hallo sleutel identificeert Hallo resource. U hebt deze snel installeren in Hallo SDK, in volgorde toodirect gegevens toohello resource.

![Klik op eigenschappen en druk op ctrl + C Hallo sleutel selecteren](./media/app-insights-windows-services/02-props-asp.png)

## <a name="sdk"></a>3. Hallo Application Insights-pakket installeren in uw toepassing
Installeren en configureren van Hallo Application Insights wordt pakket varieert afhankelijk van Hallo platform waarmee u werkt. 

1. Klik in Visual Studio met de rechtermuisknop op het project en kies **NuGet-pakketten beheren**.
   
    ![Met de rechtermuisknop op het Hallo-project en selecteer Nuget-pakketten beheren](./media/app-insights-windows-services/03-nuget.png)
2. Application Insights-pakket voor Windows server-apps, 'Microsoft.ApplicationInsights.WindowsServer.' hello installeren
   
    ![Naar Application Insights zoeken](./media/app-insights-windows-services/04-ai-nuget.png)
   
    *Welke versie?*

    Controleer **Include prerelease** desgewenst tootry onze nieuwste functies. Hallo relevante documenten of blogs opmerking of u een prerelease-versie moet.
    
    *Kan ik andere pakketten gebruiken?*
   
    Ja. Kies 'Microsoft.ApplicationInsights' als u wilt dat alleen toouse Hallo API toosend uw eigen telemetrie. Hallo-pakket voor Windows Server omvat Hallo API plus een aantal andere pakketten zoals het verzamelen van prestatiemeteritems en bewaking van afhankelijkheid. 

### <a name="tooupgrade-toofuture-package-versions"></a>tooupgrade toofuture pakketversies
Brengen we een nieuwe versie van Hallo SDK van tijd tootime.

tooupgrade tooa [nieuwe release van Hallo pakket](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/), opent u NuGet-Pakketbeheer opnieuw en filtert u op geïnstalleerde pakketten. Selecteer **Microsoft.ApplicationInsights.WindowsServer** en kies **Upgraden**.

Als u alle aanpassingen tooApplicationInsights.config genomen, een kopie van deze opslaan voordat u bijwerken en vervolgens uw wijzigingen in de nieuwe versie Hallo samen.

## <a name="4-send-telemetry"></a>4. Telemetrie verzenden
**Als u alleen Hallo API-pakket geïnstalleerd:**

* De instrumentatiesleutel Hallo in code, bijvoorbeeld ingesteld in `main()`: 
  
    `TelemetryConfiguration.Active.InstrumentationKey = "` *uw sleutel* `";` 
* [Uw eigen telemetrie met Hallo API schrijven](app-insights-api-custom-events-metrics.md#ikey).

**Als u andere pakketten Application Insights geïnstalleerd** kunt, als u liever, u Hallo .config-bestand tooset hello instrumentatiesleutel:

* Bewerk ApplicationInsights.config (die is toegevoegd door Hallo NuGet installeren). Voeg dit vlak vóór Hallo afsluitcode:
  
    `<InstrumentationKey>`*Hallo-instrumentatiesleutel die u hebt gekopieerd*`</InstrumentationKey>`
* Zorg ervoor dat de eigenschappen van ApplicationInsights.config in Solution Explorer hello te worden ingesteld**Build Action = inhoud, kopie tooOutput Directory = kopiëren**.

Het is nuttig tooset hello instrumentatiesleutel in de code als u wilt dat te[switch Hallo sleutel voor ander buildnummer configuraties](app-insights-separate-resources.md). Als u Hallo-sleutel in de code hebt ingesteld, hebt u niet tooset in Hallo `.config` bestand.

## <a name="run"></a> Uw project uitvoeren
Gebruik Hallo **F5** toorun uw toepassing en probeer deze uit: open verschillende pagina's toogenerate telemetrie.

In Visual Studio ziet u een aantal Hallo-gebeurtenissen die zijn verzonden.

![Het aantal gebeurtenissen in Visual Studio](./media/app-insights-windows-services/appinsights-09eventcount.png)

## <a name="monitor"></a> Uw telemetrie weergeven
Retourneren van toohello [Azure-portal](https://portal.azure.com/) en blader tooyour Application Insights-resource.

Zoek naar gegevens in de overzichtsgrafieken Hallo. Aanvankelijk ziet u slechts één of twee punten. Bijvoorbeeld:

![Klik door toomore gegevens](./media/app-insights-windows-services/12-first-perf.png)

Klik op via een grafiek toosee gedetailleerdere metrische gegevens. [Meer informatie over metrische gegevens.](app-insights-web-monitor-performance.md)

### <a name="no-data"></a>Zijn er geen gegevens?
* Gebruik Hallo toepassing om verschillende pagina's te openen zodat er telemetrie wordt gegenereerd.
* Open Hallo [Search](app-insights-diagnostic-search.md) tegel, toosee afzonderlijke gebeurtenissen. Het duurt soms een beetje terwijl langer tooget via Hallo metrische gegevens pipeline gebeurtenissen.
* Wacht een paar seconden en klik op **Vernieuwen**. Grafieken worden regelmatig vernieuwd, maar u kunt handmatig vernieuwen als u voor sommige gegevens tooshow up wacht.
* Zie [Probleemoplossing](app-insights-troubleshoot-faq.md).

## <a name="publish-your-app"></a>Uw app publiceren
Nu uw toepassing tooyour server implementeren of tooAzure en bekijk Hallo-gegevens worden verzameld.

![Visual Studio toopublish uw app gebruiken](./media/app-insights-windows-services/15-publish.png)

Wanneer u in de foutopsporingsmodus uitvoert, wordt de telemetrie direct via Hallo pipeline, zodat u gegevens ziet verschijnen binnen enkele seconden. Wanneer u uw app in de Release-configuratie implementeert, duurt het langer om gegevens te verzamelen.

### <a name="no-data-after-you-publish-tooyour-server"></a>Er zijn geen gegevens nadat u tooyour server hebt gepubliceerd?
Open poorten voor uitgaand verkeer in de firewall van uw server. Zie [deze pagina](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses) voor Hallo lijst met vereiste adressen 

### <a name="trouble-on-your-build-server"></a>Problemen op uw buildserver?
Raadpleeg dit artikel voor [Probleemoplossing](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild).

> [!NOTE]
> Als uw app veel telemetrie genereert, beperkt Hallo adaptieve steekproeven module automatisch Hallo volume dat toohello portal wordt verzonden door alleen een representatieve fractie van gebeurtenissen verzenden. Gebeurtenissen die zijn echter gerelateerde toohello dezelfde aanvraag worden geselecteerd of gedeselecteerd als groep, zodat u tussen gerelateerde gebeurtenissen kunt navigeren. 
> [Meer informatie over steekproeven](app-insights-sampling.md).
> 
> 

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Volgende stappen
* [Voeg meer telemetrie](app-insights-asp-net-more.md) tooget Hallo 360-graden weergave van uw toepassing.

