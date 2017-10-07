---
title: aaaMonitor een live ASP.NET web-app met Azure Application Insights | Microsoft Docs
description: Bewaak de prestaties van een website zonder de website opnieuw te implementeren. Werkt met ASP.NET-web-apps die on-premises worden gehost, die in virtuele machines worden gehost en die via Azure worden gehost.
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 769a5ea4-a8c6-4c18-b46c-657e864e24de
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: 0d53f0a59974f40767fae681bafc4f358d1283a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="instrument-web-apps-at-runtime-with-application-insights"></a>Web-apps tijdens runtime instrumenteren met Application Insights


U kunt een live web-app met Azure Application Insights, zonder toomodify softwareontwikkelaars of implementeren van uw code. Als uw apps worden gehost op een on-premises IIS-server, installeert u Status Monitor. Als ze nu Azure-web-apps of in een virtuele machine in Azure worden uitgevoerd, kunt u overschakelen op de bewaking van Application Insights in hello Azure het Configuratiescherm. (Er zijn ook afzonderlijke artikelen over het instrumenteren van [live J2EE-web-apps](app-insights-java-live.md) en [Azure Cloud Services](app-insights-cloudservices.md).) U hebt een [Microsoft Azure](http://azure.com)-abonnement nodig.

![voorbeeldgrafieken](./media/app-insights-monitor-performance-live-website-now/10-intro.png)

Hebt u een keuze uit drie routes tooapply Application Insights tooyour .NET-webtoepassingen:

* **Bouwen:** [Hallo Add Application Insights-SDK] [ greenbrown] tooyour web-app-code.
* **Uitvoeringstijd:** Instrumenteren van uw web-app op Hallo van server, zoals hieronder, zonder opnieuw te bouwen en opnieuw distribueren Hallo code wordt beschreven.
* **Beide:** Hallo SDK bouwen in uw web-app-code en ook van toepassing hello runtime-extensies. Hallo beste van beide opties worden opgehaald.

Hier volgt een samenvatting van wat elke route u biedt:

|  | Tijdens het bouwen | Tijdens het gebruik |
| --- | --- | --- |
| Aanvragen en uitzonderingen |Ja |Ja |
| [Meer gedetailleerde uitzonderingen](app-insights-asp-net-exceptions.md) | |Ja |
| [Diagnostische gegevens over afhankelijkheid](app-insights-asp-net-dependencies.md) |Op .NET 4.6+, maar minder details |Ja, volledige details: resultaatcodes, SQL-opdrachttekst, HTTP-woord|
| [Systeemprestatiemeteritems](app-insights-performance-counters.md) |Ja |Ja |
| [API voor aangepaste telemetrie][api] |Ja |Nee |
| [Integratie traceerlogboeken](app-insights-asp-net-trace-logs.md) |Ja |Nee |
| [Paginaweergave en gebruikersgegevens](app-insights-javascript.md) |Ja |Nee |
| Toorebuild code nodig |Ja | Nee |


## <a name="monitor-a-live-azure-web-app"></a>Een live Azure-web-app bewaken

Als uw toepassing wordt uitgevoerd als een Azure-web-service, hier van hoe tooswitch over het controleren van:

* Selecteer Application Insights in het Configuratiescherm Hallo-app in Azure.

    ![Application Insights instellen voor een Azure-web-app](./media/app-insights-monitor-performance-live-website-now/azure-web-setup.png)
* Wanneer Hallo Application Insights-overzichtspagina wordt geopend, klikt u op Hallo koppeling Hallo onder tooopen Hallo volledige Application Insights-resource.

    ![Klik door tooApplication Insights](./media/app-insights-monitor-performance-live-website-now/azure-web-view-more.png)

[Cloud- en VM-apps bewaken](app-insights-azure.md).

### <a name="enable-client-side-monitoring-in-azure"></a>Bewaking aan clientzijde in Azure inschakelen

Als u Application Insights in Azure hebt ingeschakeld, kunt u de paginaweergave en gebruikerstelemetrie toevoegen.

1. Selecteer Instellingen > Toepassingsinstellingen
2.  Voeg een nieuw sleutelwaardepaar toe bij App-instellingen: 
   
    Sleutel: `APPINSIGHTS_JAVASCRIPT_ENABLED` 
    
    Waarde:`true`
3. **Sla** Hallo instellingen en **opnieuw** uw app.

Hallo Application Insights JavaScript SDK is nu opgenomen in elke webpagina.

## <a name="monitor-a-live-iis-web-app"></a>Een live IIS-web-app bewaken

Als uw app wordt gehost op een IIS-server, kunt u Application Insights inschakelen met Status Monitor.

1. Meld u op uw IIS-webserver aan met beheerdersreferenties.
2. Als de Application Insights Status Monitor nog niet is geïnstalleerd, downloaden en uitvoeren van Hallo [Status Monitor-installatieprogramma](http://go.microsoft.com/fwlink/?LinkId=506648) (of uit te voeren [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) en zoekt u in het Application Insights Status Monitor).
3. Selecteer in de Status Monitor Hallo geïnstalleerd webtoepassing of website die u toomonitor wilt. Meld u aan met uw Azure-referenties.

    Hallo-resource waar u toosee Hallo resulteert in Application Insights-portal hello wilt configureren. (Normaal gesproken het is aanbevolen toocreate een nieuwe resource. Selecteer een bestaande resource als u al [webtests][availability] of [clientbewaking][client] hebt voor deze app.) 

    ![Kies een app en een resource.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-configAIC.png)

4. Start IIS opnieuw.

    ![Opnieuw opstarten boven Hallo van Hallo dialoogvenster kiezen.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-restart.png)

    Uw webservice wordt enkele ogenblikken onderbroken.

## <a name="customize-monitoring-options"></a>Bewakingsopties aanpassen

Application Insights inschakelen voegt dll's en ApplicationInsights.config tooyour web-app. U kunt [Hallo .config-bestand bewerken](app-insights-configuration-with-applicationinsights-config.md) toochange aantal Hallo-opties.

## <a name="when-you-re-publish-your-app-re-enable-application-insights"></a>Wanneer u uw app opnieuw publiceert, schakelt u Application Insights opnieuw in

Voordat u uw app opnieuw publiceert, rekening houden met [Application Insights toohello code toe te voegen in Visual Studio][greenbrown]. U krijgt meer gedetailleerde Telemetrie en Hallo mogelijkheid toowrite aangepaste telemetrie.

Als u wilt dat toore-publiceren zonder Application Insights toohello code toe te voegen, houd er rekening mee dat implementatieproces Hallo Hallo dll-bestanden te verwijderen en ApplicationInsights.config van Hallo website gepubliceerd. Daarom:

1. Als u ApplicationInsights.config hebt bewerkt, maakt u er een kopie van voordat u de app opnieuw publiceert.
2. Publiceer uw app opnieuw.
3. Schakel Application Insights-bewaking opnieuw in. (Gebruik de juiste methode Hallo: hello Azure-web-app van het Configuratiescherm of Hallo Status Monitor op een IIS-host.)
4. Alle bewerkingen die u hebt uitgevoerd op Hallo .config-bestand opnieuw.


## <a name="troubleshooting-runtime-configuration-of-application-insights"></a>Problemen met de runtimeconfiguratie van Application Insights oplossen

### <a name="cant-connect-no-telemetry"></a>Kunt u geen verbinding maken? Geen telemetrie?

* Open [Hallo nodig uitgaande poorten](app-insights-ip-addresses.md#outgoing-ports) in uw server firewall tooallow Status Monitor toowork.

* Open Status Monitor en selecteer in het linkerdeelvenster uw toepassing. Controleer of er diagnostische meldingen voor deze toepassing in de sectie 'Configuration notifications' hello zijn:

  ![Open Hallo prestaties blade toosee aanvraag, reactietijden, afhankelijkheden en andere gegevens](./media/app-insights-monitor-performance-live-website-now/appinsights-status-monitor-diagnostics-message.png)
* Op Hallo van server, als er een bericht over 'onvoldoende machtigingen', voer een Hallo volgende:
  * In de IIS-beheer, selecteer uw groep van toepassingen, open **geavanceerde instellingen**, en klikt u onder **procesmodel** Noteer Hallo identiteit.
  * In het Configuratiescherm voor Computerbeheer, voeg deze identiteit toohello Prestatiemetergebruikers.
* Als op uw server MMA/SCOM (Systems Center Operations Manager) is geïnstalleerd, kan er een conflict optreden met sommige versies. Verwijder zowel SCOM als Status Monitor en installeer opnieuw de meest recente versies Hallo.
* Zie [Probleemoplossing][qna].

## <a name="system-requirements"></a>Systeemvereisten
Ondersteuning van het besturingssysteem voor Application Insights Status Monitor op de server:

* Windows Server 2008
* Windows Server 2008 R2
* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

met het nieuwste SP en .NET-framework 4.5

Aan de clientzijde Hallo: Windows 7, 8, 8.1 en 10, opnieuw met .NET Framework 4.5

Ondersteuning voor IIS is: IIS 7, 7.5, 8, 8.5 (IIS is vereist)

## <a name="automation-with-powershell"></a>Automatisering met PowerShell
Met PowerShell kunt u de bewaking op de IIS-server starten en stoppen.

Eerst Hallo Application Insights-module importeren:

`Import-Module 'C:\Program Files\Microsoft Application Insights\Status Monitor\PowerShell\Microsoft.Diagnostics.Agent.StatusMonitor.PowerShell.dll'`

Controleer welke apps worden bewaakt:

`Get-ApplicationInsightsMonitoringStatus [-Name appName]`

* `-Name`(Optioneel) Hallo-naam van een web-app.
* Geeft Hallo Application Insights-bewakingsstatus voor elke web-app (of met de naam app Hallo) in deze IIS-server.
* Retourneert `ApplicationInsightsApplication` voor elke app:

  * `SdkState==EnabledAfterDeployment`: De app wordt bewaakt en is tijdens de uitvoering geïnstrumenteerd door hulpprogramma Hallo-Status Monitor of door `Start-ApplicationInsightsMonitoring`.
  * `SdkState==Disabled`: Hallo app is niet geïnstrumenteerd voor Application Insights. Deze App is niet geïnstrumenteerd, hetzij runtime-controle is uitgeschakeld met hulpprogramma voor Hallo Status Monitor of met `Stop-ApplicationInsightsMonitoring`.
  * `SdkState==EnabledByCodeInstrumentation`: Hallo app is geïnstrumenteerd door Hallo SDK toohello broncode toe te voegen. De SDK kan niet worden bijgewerkt of gestopt.
  * `SdkVersion`Hallo versie bevat gebruikt voor het bewaken van deze app.
  * `LatestAvailableSdkVersion`bevat Hallo-versie die momenteel beschikbaar op Hallo NuGet-galerie. tooupgrade hello app toothis versie, gebruik `Update-ApplicationInsightsMonitoring`.

`Start-ApplicationInsightsMonitoring -Name appName -InstrumentationKey 00000000-000-000-000-0000000`

* `-Name`Hallo-naam van Hallo-app in IIS
* `-InstrumentationKey`Hallo ikey Hallo Application Insights-resource waar u Hallo resultaten toobe weergegeven.
* Deze cmdlet geldt alleen voor apps die niet al zijn geïnstrumenteerd, dus SdkState==NotInstrumented.

    Hallo-cmdlet heeft geen invloed op een app die al zijn geïnstrumenteerd. Het niet belangrijk te weten dat het Hallo-app is geïnstrumenteerd build gelijktijdig door Hallo SDK toohello code toevoegen of tijdens runtime met gebruik van deze cmdlet.

    Hallo SDK versie die wordt gebruikt tooinstrument Hallo-app is Hallo-versie die het laatst toothis server hebt gedownload.

    meest recente versie toodownload hello, Update-ApplicationInsightsVersion gebruiken.
* Retourneert `ApplicationInsightsApplication` wanneer het is gelukt. Als dit mislukt, wordt een toostderr trace gelogd.

          Name                      : Default Web Site/WebApp1
          InstrumentationKey        : 00000000-0000-0000-0000-000000000000
          ProfilerState             : ApplicationInsights
          SdkState                  : EnabledAfterDeployment
          SdkVersion                : 1.2.1
          LatestAvailableSdkVersion : 1.2.3

`Stop-ApplicationInsightsMonitoring [-Name appName | -All]`

* `-Name`Hallo-naam van een app in IIS
* `-All` Stopt het bewaken van alle apps op deze IIS-server waarvoor `SdkState==EnabledAfterDeployment`
* Stopt de bewaking van Hallo opgegeven apps en verwijdert instrumentatie. Deze functie werkt alleen voor apps die op het gebruik van de runtime-zijn geïnstrumenteerd Hallo hulpprogramma Status of Start-ApplicationInsightsApplication. (`SdkState==EnabledAfterDeployment`)
* Retourneert ApplicationInsightsApplication.

`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]

* `-Name`: Hallo-naam van een web-app in IIS.
* `-InstrumentationKey` (Optioneel.) Gebruik die deze toochange Hallo resource toowhich Hallo van app telemetrie wordt verzonden.
* Deze cmdlet:
  * Upgrades Hallo app toohello-versie van Hallo SDK met de naam gedownload meest recent toothis machine. (Werkt alleen als `SdkState==EnabledAfterDeployment`)
  * Als u een instrumentatiesleutel opgeeft, is met de naam app Hallo opnieuw geconfigureerde toosend telemetrie toohello bron met die sleutel. (Werkt als `SdkState != Disabled`)

`Update-ApplicationInsightsVersion`

* Hallo nieuwste Application Insights-SDK toohello server downloadt.

## <a name="questions"></a>Vragen over Status Monitor

### <a name="what-is-status-monitor"></a>Wat is Status Monitor?

Een bureaubladtoepassing die u op uw IIS-webserver kunt installeren. Hiermee kunt u web-apps instrumenteren en configureren. 

### <a name="when-do-i-use-status-monitor"></a>Wanneer maak ik gebruik van Status Monitor?

* tooinstrument een web-app die wordt uitgevoerd op uw IIS-server - zelfs als het al wordt uitgevoerd.
* aanvullende telemetrie voor web-apps die zijn tooenable [gebouwd met Application Insights-SDK Hallo](app-insights-asp-net.md) tijdens de compilatie. 

### <a name="can-i-close-it-after-it-runs"></a>Kan ik de applicatie sluiten nadat deze is uitgevoerd?

Ja. Nadat deze is geïnstrumenteerd Hallo websites die u selecteert, kunt u deze sluiten.

Status Monitor verzamelt niet zelf telemetrie. Gewoon configureert Hallo web-apps en sommige machtigingen ingesteld.

### <a name="what-does-status-monitor-do"></a>Wat doet Status Monitor?

Wanneer u een web-app voor statuscontrole tooinstrument selecteren:

* Downloadt en plaatst Hallo Application Insights-assembly's en .config-bestand in map met binaire Hallo van web-app.
* Hiermee wijzigt u `web.config` tooadd Hallo Application Insights HTTP bijhouden-module.
* Kan CLR toocollect afhankelijkheidsaanroepen profilering.

### <a name="do-i-need-toorun-status-monitor-whenever-i-update-hello-app"></a>Moet ik toorun Status Monitor wanneer ik Hallo app bijwerken?

Niet als u deze stapsgewijs opnieuw implementeert. 

Als u optie Hallo 'delete bestaande bestanden' in hello proces publiceren, moet u toore-run Status Monitor tooconfigure Application Insights.

### <a name="what-telemetry-is-collected"></a>Welke telemetrie wordt verzameld?

Voor toepassingen die u met behulp van de Status Monitor bij het uitvoeren instrumenteert:

* HTTP-aanvragen
* Aanroepen toodependencies
* Uitzonderingen
* Prestatiemeteritems

Voor toepassingen die bij het compileren al zijn geïnstrumenteerd:

 * Procestellers.
 * Afhankelijkheidsaanroepen (.NET 4.5); retourwaarden in afhankelijkheidsaanroepen (.NET 4.6).
 * Stack-tracewaarden van uitzonderingen.

[Meer informatie](http://apmtips.com/blog/2016/11/18/how-application-insights-status-monitor-not-monitors-dependencies/)

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next"></a>Volgende stappen

Uw telemetrie weergeven:

* [Verkennen van metrische gegevens](app-insights-metrics-explorer.md) toomonitor prestaties en gebruik
* [Zoek naar gebeurtenissen en logboeken] [ diagnostic] toodiagnose problemen
* [Gebruik analyses](app-insights-analytics.md) voor meer geavanceerde query's
* [Maak dashboards](app-insights-dashboards.md)

Meer telemetrie toevoegen:

* [Maak webtests] [ availability] toomake zorgen dat uw site actief blijft.
* [Voeg telemetrie van de webclient] [ usage] toosee uitzonderingen op de webpagina code en toolet u invoegen aanroepen traceren.
* [Application Insights-SDK tooyour code toevoegen] [ greenbrown] zodat u kunt trace invoegen en meld u aanroepen

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[availability]: app-insights-monitor-web-app-availability.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[roles]: app-insights-resources-roles-access-control.md
[usage]: app-insights-javascript.md
