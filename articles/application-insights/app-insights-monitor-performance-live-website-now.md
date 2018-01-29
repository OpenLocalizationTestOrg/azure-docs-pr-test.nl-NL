---
title: Een live ASP.NET-web-app bewaken met Azure Application Insights | Microsoft Docs
description: Bewaak de prestaties van een website zonder de website opnieuw te implementeren. Werkt met ASP.NET-web-apps die on-premises worden gehost, die in virtuele machines worden gehost en die via Azure worden gehost.
services: application-insights
documentationcenter: .net
author: mrbullwinkle
manager: carmonm
ms.assetid: 769a5ea4-a8c6-4c18-b46c-657e864e24de
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: mbullwin
ms.openlocfilehash: 869ea96072b1492db929c16cfb1e22b0c96bca7d
ms.sourcegitcommit: e462e5cca2424ce36423f9eff3a0cf250ac146ad
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 11/01/2017
---
# <a name="instrument-web-apps-at-runtime-with-application-insights"></a>Web-apps tijdens runtime instrumenteren met Application Insights


U kunt een live web-app instrumenteren met Azure Application Insights, zonder dat u de code hoeft te wijzigen of opnieuw hoeft te implementeren. Als uw apps worden gehost op een on-premises IIS-server, installeert u Status Monitor. Als uw apps Azure-web-apps zijn of worden uitgevoerd op een virtuele Azure-machine, kunt u Application Insights-bewaking inschakelen in het configuratiescherm van Azure. (Er zijn ook afzonderlijke artikelen over het instrumenteren van [live J2EE-web-apps](app-insights-java-live.md) en [Azure Cloud Services](app-insights-cloudservices.md).) U hebt een [Microsoft Azure](http://azure.com)-abonnement nodig.

![voorbeeldgrafieken](./media/app-insights-monitor-performance-live-website-now/10-intro.png)

U kunt kiezen uit drie routes om Application Insights toe te passen op uw .NET-webtoepassingen:

* **Tijdens het bouwen:** [voeg de Application Insights-SDK][greenbrown] toe aan uw web-app-code.
* **Tijdens het gebruik:** Instrumenteer uw web-app op de server, zoals hieronder wordt beschreven, zonder deze opnieuw op te bouwen en de code opnieuw te implementeren.
* **Beide:** bouw de SDK in de code van uw web-app in en pas ook de runtime-extensies toe. Zo profiteert u van het beste van beide opties.

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
| Code moet worden herbouwd |Ja | Nee |


## <a name="monitor-a-live-azure-web-app"></a>Een live Azure-web-app bewaken

Als uw toepassing wordt uitgevoerd als Azure-webservice, leest u hier hoe u bewaking inschakelt:

* Selecteer Application Insights in het configuratiescherm van de app in Azure.

    ![Application Insights instellen voor een Azure-web-app](./media/app-insights-monitor-performance-live-website-now/azure-web-setup.png)
* Wanneer de Application Insights-overzichtspagina wordt geopend, klikt u op de koppeling onderaan om de volledige Application Insights-resource te openen.

    ![Klik door naar Application Insights](./media/app-insights-monitor-performance-live-website-now/azure-web-view-more.png)

[Cloud- en VM-apps bewaken](app-insights-azure.md).

### <a name="enable-client-side-monitoring-in-azure"></a>Bewaking aan clientzijde in Azure inschakelen

Als u Application Insights in Azure hebt ingeschakeld, kunt u de paginaweergave en gebruikerstelemetrie toevoegen.

1. Selecteer Instellingen > Toepassingsinstellingen
2.  Voeg een nieuw sleutelwaardepaar toe bij App-instellingen: 
   
    Sleutel: `APPINSIGHTS_JAVASCRIPT_ENABLED` 
    
    Waarde:`true`
3. Sla de instellingen op met **Opslaan** en start de app opnieuw met **Opnieuw opstarten**.

De Application Insights JavaScript-SDK is nu opgenomen in elke webpagina.

## <a name="monitor-a-live-iis-web-app"></a>Een live IIS-web-app bewaken

Als uw app wordt gehost op een IIS-server, kunt u Application Insights inschakelen met Status Monitor.

1. Meld u op uw IIS-webserver aan met beheerdersreferenties.
2. Als Application Insights Status Monitor nog niet is geïnstalleerd, downloadt u het [Status Monitor-installatieprogramma](http://go.microsoft.com/fwlink/?LinkId=506648) en voert u deze uit. (Of u kunt het [Webplatforminstallatieprogramma](https://www.microsoft.com/web/downloads/platform.aspx) uitvoeren en hierin zoeken naar Application Insights Status Monitor).
3. In Status Monitor selecteert u de geïnstalleerde web-app of website die u wilt bewaken. Meld u aan met uw Azure-referenties.

    Configureer de resource waarvan u de resultaten wilt weergeven in de Application Insights-portal. (Normaal gesproken is het het beste om een nieuwe resource te maken. Selecteer een bestaande resource als u al [webtests][availability] of [clientbewaking][client] hebt voor deze app.) 

    ![Kies een app en een resource.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-configAIC.png)

4. Start IIS opnieuw.

    ![Klik boven in het dialoogvenster op Restart.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-restart.png)

    Uw webservice wordt enkele ogenblikken onderbroken.

## <a name="customize-monitoring-options"></a>Bewakingsopties aanpassen

Als u Application Insights inschakelt, worden ddl-bestanden en het bestand ApplicationInsights.config toegevoegd aan uw web-app. U kunt [het bestand .config bewerken](app-insights-configuration-with-applicationinsights-config.md) om enkele van de opties te wijzigen.

## <a name="when-you-re-publish-your-app-re-enable-application-insights"></a>Wanneer u uw app opnieuw publiceert, schakelt u Application Insights opnieuw in

Voordat u uw app opnieuw publiceert, overweegt u om [Application Insights toe te voegen aan de code in Visual Studio][greenbrown]. U krijgt dan meer gedetailleerde telemetrie en de mogelijkheid om aangepaste telemetrie te schrijven.

Als u opnieuw wilt publiceren zonder Application Insights toe te voegen aan de code, moet u zich realiseren dat tijdens het implementatieproces de ddl-bestanden en het bestand ApplicationInsights.config mogelijk worden verwijderd van de gepubliceerde website. Daarom:

1. Als u ApplicationInsights.config hebt bewerkt, maakt u er een kopie van voordat u de app opnieuw publiceert.
2. Publiceer uw app opnieuw.
3. Schakel Application Insights-bewaking opnieuw in. (Gebruik de juiste methode: het configuratiescherm van de Azure-web-app of Status Monitor op een IIS-host.)
4. Voer alle wijzigingen die u hebt doorgevoerd in het .config-bestand opnieuw door.


## <a name="troubleshooting-runtime-configuration-of-application-insights"></a>Problemen met de runtimeconfiguratie van Application Insights oplossen

### <a name="cant-connect-no-telemetry"></a>Kunt u geen verbinding maken? Geen telemetrie?

* Open [de benodigde uitgaande poorten](app-insights-ip-addresses.md#outgoing-ports) in de firewall van uw server om Status Monitor uit te voeren.

* Open Status Monitor en selecteer in het linkerdeelvenster uw toepassing. Controleer in het gedeelte Configuration notifications of er diagnostische meldingen zijn voor de toepassing:

  ![Open de blade Performance om aanvragen, reactietijden, afhankelijkheden en andere gegevens te bekijken](./media/app-insights-monitor-performance-live-website-now/appinsights-status-monitor-diagnostics-message.png)
* Als u op de server een bericht over 'insufficient permissions' (onvoldoende machtigingen) ziet, probeert u het volgende:
  * Selecteer in IIS Manager uw groep met toepassingen, open **Advanced Settings** en noteer de identiteit onder **Proces Model**.
  * Voeg in het configuratiescherm voor computerbeheer deze identiteit toe aan de groep Prestatiemetergebruikers.
* Als op uw server MMA/SCOM (Systems Center Operations Manager) is geïnstalleerd, kan er een conflict optreden met sommige versies. Verwijder zowel SCOM als Status Monitor en installeer de meest recente versies.
* Zie [Probleemoplossing][qna].

## <a name="system-requirements"></a>Systeemvereisten
Ondersteuning van het besturingssysteem voor Application Insights Status Monitor op de server:

* Windows Server 2008
* Windows Server 2008 R2
* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

met het nieuwste SP en .NET-framework 4.5

Aan de clientzijde: Windows 7, 8, 8.1 en 10, eveneens met .NET Framework 4.5

Ondersteuning voor IIS is: IIS 7, 7.5, 8, 8.5 (IIS is vereist)

## <a name="automation-with-powershell"></a>Automatisering met PowerShell
Met PowerShell kunt u de bewaking op de IIS-server starten en stoppen.

Importeer eerst de module Application Insights:

`Import-Module 'C:\Program Files\Microsoft Application Insights\Status Monitor\PowerShell\Microsoft.Diagnostics.Agent.StatusMonitor.PowerShell.dll'`

Controleer welke apps worden bewaakt:

`Get-ApplicationInsightsMonitoringStatus [-Name appName]`

* `-Name` (Optioneel) De naam van een web-app.
* Geeft de Application Insights-bewakingsstatus voor elke web-app (of de benoemde app) op deze IIS-server.
* Retourneert `ApplicationInsightsApplication` voor elke app:

  * `Start-ApplicationInsightsMonitoring`: de app wordt bewaakt en was in runtime geïnstrumenteerd, door het hulpprogramma Status Monitor of door `SdkState==EnabledAfterDeployment`.
  * `SdkState==Disabled` : de app is niet geïnstrumenteerd voor Application Insights. De app is niet geïnstrumenteerd, of bewaking tijdens de uitvoering is uitgeschakeld met het hulpprogramma Status Monitor of met `Stop-ApplicationInsightsMonitoring`.
  * `SdkState==EnabledByCodeInstrumentation`: de app was geïnstrumenteerd door de SDK toe te voegen aan de broncode. De SDK kan niet worden bijgewerkt of gestopt.
  * `SdkVersion` toont de versie die voor het bewaken van deze app wordt gebruikt.
  * `LatestAvailableSdkVersion` toont de versie die momenteel beschikbaar is in de NuGet-galerie. Als u de app naar deze versie wilt bijwerken, gebruikt u `Update-ApplicationInsightsMonitoring`.

`Start-ApplicationInsightsMonitoring -Name appName -InstrumentationKey 00000000-000-000-000-0000000`

* `-Name` De naam van de app in IIS
* `-InstrumentationKey` De iKey van de Application Insights-resource waar u de resultaten wilt weergeven.
* Deze cmdlet geldt alleen voor apps die niet al zijn geïnstrumenteerd, dus SdkState==NotInstrumented.

    De cmdlet heeft geen invloed op een app die al is geïmplementeerd. Het maakt niet uit of de app is geïmplementeerd tijdens het bouwen (toen de SDK aan de code werd toegevoegd), of tijdens de uitvoering (met gebruik van deze cmdlet).

    De SDK-versie die voor het instrumenteren van de app is gebruikt, is de versie die het laatst is gedownload naar deze server.

    Voor het downloaden van de meest recente versie gebruikt u Update-ApplicationInsightsVersion.
* Retourneert `ApplicationInsightsApplication` wanneer het is gelukt. Als het mislukt, wordt er een tracering geregistreerd in stderr.

          Name                      : Default Web Site/WebApp1
          InstrumentationKey        : 00000000-0000-0000-0000-000000000000
          ProfilerState             : ApplicationInsights
          SdkState                  : EnabledAfterDeployment
          SdkVersion                : 1.2.1
          LatestAvailableSdkVersion : 1.2.3

`Stop-ApplicationInsightsMonitoring [-Name appName | -All]`

* `-Name` De naam van een app in IIS
* `-All` Stopt het bewaken van alle apps op deze IIS-server waarvoor `SdkState==EnabledAfterDeployment`
* Stopt het bewaken van de opgegeven apps en verwijdert instrumentatie. Deze functie werkt alleen voor apps die tijdens de uitvoering zijn geïnstrumenteerd met het hulpprogramma Status Monitor of Start-ApplicationInsightsApplication. (`SdkState==EnabledAfterDeployment`)
* Retourneert ApplicationInsightsApplication.

`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]

* `-Name` : de naam van een web-app in IIS.
* `-InstrumentationKey` (Optioneel.) Gebruik deze om de resource te wijzigen waarnaar de telemetrie van de app wordt verzonden.
* Deze cmdlet:
  * Upgradet de benoemde app naar de versie van de SDK die het laatst naar deze computer is gedownload. (Werkt alleen als `SdkState==EnabledAfterDeployment`)
  * Als u een instrumentatiesleutel opgeeft, wordt de vermelde app opnieuw geconfigureerd voor het verzenden van telemetrie naar de resource met die sleutel. (Werkt als `SdkState != Disabled`)

`Update-ApplicationInsightsVersion`

* Downloadt de nieuwste Application Insights-SDK naar de server.

## <a name="questions"></a>Vragen over Status Monitor

### <a name="what-is-status-monitor"></a>Wat is Status Monitor?

Een bureaubladtoepassing die u op uw IIS-webserver kunt installeren. Hiermee kunt u web-apps instrumenteren en configureren. 

### <a name="when-do-i-use-status-monitor"></a>Wanneer maak ik gebruik van Status Monitor?

* Wanneer u web-apps wilt instrumenteren die worden uitgevoerd op uw IIS-server, zelfs als deze al worden uitgevoerd.
* Om extra telemetrie mogelijk te maken voor web-apps die bij het compileren zijn [gebouwd met de Application Insights-SDK](app-insights-asp-net.md). 

### <a name="can-i-close-it-after-it-runs"></a>Kan ik de applicatie sluiten nadat deze is uitgevoerd?

Ja. Zodra de applicatie de gekozen websites heeft geïnstrumenteerd, kunt u deze sluiten.

Status Monitor verzamelt niet zelf telemetrie. Het configureert enkel de web-apps en stelt enkele machtigingen in.

### <a name="what-does-status-monitor-do"></a>Wat doet Status Monitor?

Wanneer u een web-app selecteert die u met Status Monitor wilt instrumenteren:

* Worden de Application Insights-assembly's en een .config-bestand gedownload en in de map met de binaire bestanden van de web-app geplaatst.
* Wordt `web.config` gewijzigd om de Application Insights HTTP-bewakingsmodule toe te voegen.
* Schakelt CLR-profilering in voor het verzamelen van afhankelijkheidsaanroepen.

### <a name="do-i-need-to-run-status-monitor-whenever-i-update-the-app"></a>Moet ik Status Monitor telkens uitvoeren wanneer ik de app heb bijgewerkt?

Niet als u deze stapsgewijs opnieuw implementeert. 

Als u de optie 'Bestaande bestanden verwijderen' selecteert in het publicatieproces, dient u Status Monitor opnieuw uit te voeren om Application Insights te configureren.

### <a name="what-telemetry-is-collected"></a>Welke telemetrie wordt verzameld?

Voor toepassingen die u met behulp van de Status Monitor bij het uitvoeren instrumenteert:

* HTTP-aanvragen
* Afhankelijkheidsaanroepen
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

* [Verken de metrische gegevens](app-insights-metrics-explorer.md) om de prestaties en het gebruik te bewaken
* [Doorzoek gebeurtenissen en logboeken][diagnostic] om problemen te analyseren
* [Gebruik analyses](app-insights-analytics.md) voor meer geavanceerde query's
* [Maak dashboards](app-insights-dashboards.md)

Meer telemetrie toevoegen:

* [Maak webtests][availability] om ervoor te zorgen dat uw site actief blijft.
* [Voeg telemetrie van de webclient toe][usage] om uitzonderingen op de webpaginacode weer te geven en traceringsaanroepen in te voegen.
* [Voeg de Application Insights-SDK toe aan uw code][greenbrown] zodat u tracerings- en logboekaanroepen kunt invoegen

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[availability]: app-insights-monitor-web-app-availability.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[roles]: app-insights-resources-roles-access-control.md
[usage]: app-insights-javascript.md
