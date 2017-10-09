---
title: aaaSet van web-app-analyse voor ASP.NET met Azure Application Insights | Microsoft Docs
description: Configureer prestaties, beschikbaarheid en gebruiksanalyse voor uw ASP.NET-website die on-premises of in Azure wordt gehost.
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d0eee3c0-b328-448f-8123-f478052751db
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: 61a3cdce68da48bfb9450b1d296acc1535f50a38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-application-insights-for-your-aspnet-website"></a>Application Insights instellen voor uw ASP.NET-website

Deze procedure configureert u uw ASP.NET web app toosend telemetrie toohello [Azure Application Insights](app-insights-overview.md) service. De Tool werkt voor ASP.NET-apps die worden gehost in een eigen IIS-server of in Hallo Cloud. Ophalen van grafieken en een krachtige querytaal die u helpen begrijpen Hallo prestaties van uw app en hoe mensen gebruikt, plus automatische waarschuwingen op fouten of prestatieproblemen. Veel ontwikkelaars vinden deze functies geweldige zoals ze zijn, maar u kunt ook uitbreiden en aanpassen Hallo telemetrie als u wilt.

Voor de Setup zijn maar een paar klikken nodig in Visual Studio. U hebt Hallo optie tooavoid kosten door te beperken Hallo volume telemetrie. Hiermee kunt u tooexperiment en foutopsporing of toomonitor een site met niet veel gebruikers. Als u besluit dat u wilt toogo vooruit en controleren van uw productiesite, is het eenvoudig tooraise Hallo limiet later.

## <a name="before-you-start"></a>Voordat u begint
U hebt de volgende zaken nodig:

* Visual Studio 2013 update 3 of later. Later is beter.
* Een abonnement te[Microsoft Azure](http://azure.com). Als uw team of organisatie een Azure-abonnement heeft, Hallo kan eigenaar u toevoegen tooit, met behulp van uw [Microsoft-account](http://live.com).

Er zijn andere onderwerpen toolook op als u geïnteresseerd bent in:

* [Een web-app instrumenteren tijdens runtime](app-insights-monitor-performance-live-website-now.md)
* [Azure Cloud Services](app-insights-cloudservices.md)

## <a name="ide"></a>Stap 1: Hallo Application Insights-SDK toevoegen

Klik in Solution Explorer met de rechtermuisknop op het web-app-project. Kies **Toevoegen** > **Application Insights Telemetry...** of **Application Insights configureren**.

![Schermopname van Solution Explorer waarin Application Insights Telemetry toevoegen is gemarkeerd](./media/app-insights-asp-net/appinsights-03-addExisting.png)

(In Visual Studio 2015, er is ook een optie tooadd Application Insights in het dialoogvenster Nieuw Project Hallo.)

Pagina toohello Application Insights-configuratie worden voortgezet:

![Schermopname van de pagina Uw app registreren bij Application Insights](./media/app-insights-asp-net/visual-studio-register-dialog.png)

**a.** Hallo-account en dat u tooaccess Azure-abonnement selecteren.

**b.** Selecteer Hallo resource in Azure waar u toosee Hallo gegevens van uw app. Meestal:

* Gebruik [één resource voor verschillende onderdelen](app-insights-monitor-multi-role-apps.md) van één toepassing. 
* Maak afzonderlijke resources voor niet-gerelateerde toepassingen.
 
Als u wilt dat tooset Hallo groep of Hallo Resourcelocatie waar uw gegevens worden opgeslagen, klikt u op **configureren**. Resourcegroepen zijn gebruikte toocontrol toegang toodata. Bijvoorbeeld, als u verschillende web-apps die deel uitmaken van hebt Hallo dezelfde systeem, kunt u hun Application Insights-gegevens plaatsen dezelfde resourcegroep Hallo.

**c.** Stel een limiet op Hallo-limiet voor het volume van beschikbare gegevens, tooavoid kosten. Application Insights verkeert momenteel vrijmaken tooa bepaald volume van telemetrie. Nadat Hallo resource is gemaakt, kunt u uw selectie in de portal Hallo wijzigen door het openen van **functies en prijzen** > **volume gegevensbeheer** > **per dag volume cap**.

**d.** Klik op **registreren** toogo vooruit en Application Insights configureren voor uw web-app. Telemetrie verzonden toohello [Azure-portal](https://portal.azure.com), zowel tijdens de foutopsporing en nadat u uw app hebt gepubliceerd.

**e.** Als u niet dat toosend telemetrie toohello portal wilt terwijl u fouten opspoort, Hallo Application Insights-SDK tooyour app toevoegen maar een resource in Hallo portal niet configureren. U zult kunnen toosee telemetrie in Visual Studio terwijl u fouten opspoort. Later kunt u de configuratiepagina toothis retourneren, of u kan wachten totdat nadat u uw app hebt geïmplementeerd en [telemetrie inschakelen tijdens de uitvoering](app-insights-monitor-performance-live-website-now.md).


## <a name="run"></a> Stap 2: uw app uitvoeren
Voer uw app uit met F5. Open verschillende pagina's toogenerate telemetrie.

In Visual Studio ziet u een aantal Hallo-gebeurtenissen die zijn geregistreerd.

![Schermopname van Visual Studio. de knop Application Insights Hallo weergegeven tijdens het opsporen van fouten.](./media/app-insights-asp-net/54.png)

## <a name="step-3-see-your-telemetry"></a>Stap 3: uw telemetrie weergeven
U ziet uw telemetrie in Visual Studio of in Hallo Application Insights-webportal. Telemetrie zoeken in Visual Studio toohelp u uw app fouten opsporen. Bewaak prestaties en gebruik in de webportal Hallo wanneer uw systeem live is. 

### <a name="see-your-telemetry-in-visual-studio"></a>De telemetrie bekijken in Visual Studio

Open in Visual Studio Hallo Application Insights-venster. Hallo klikt u op **Application Insights** knop of met de rechtermuisknop op het project in Solution Explorer, selecteer **Application Insights**, en klik vervolgens op **zoeken Live telemetrie**.

Zie in Hallo Visual Studio Application Insights zoeken venster Hallo **gegevens van foutopsporingssessie** weergave voor de telemetrie die is gegenereerd in Hallo servergedeelte van uw app. Experimenteren met Hallo filters en klikt u op een gebeurtenis toosee meer details.

![Schermopname van Hallo gegevens van foutopsporingssessie weergeven in Application Insights-venster Hallo.](./media/app-insights-asp-net/55.png)

> [!NOTE]
> Als u niet alle gegevens ziet, zorg Hallo tijdsbereik juist is en klik op het zoekpictogram Hallo.

[Meer informatie over Application Insights-hulpprogramma's in Visual Studio](app-insights-visual-studio.md).

<a name="monitor"></a>
### <a name="see-telemetry-in-web-portal"></a>Telemetrie bekijken in de webportal

U ziet ook telemetrie in Application Insights-webportal hello (tenzij u kiest voor tooinstall alleen Hallo SDK). Hallo-portal biedt meer grafieken, hulpprogramma's voor analyse en weergaven voor cross-onderdeel dan Visual Studio. Hallo-portal biedt ook waarschuwingen.

Open uw Application Insights-resource. Een toohello aanmelden [Azure-portal](https://portal.azure.com/) en vinden er of met de rechtermuisknop op Hallo project in Visual Studio en laat deze te gaan.

![Schermopname van Visual Studio die laat zien hoe tooopen Hallo Application Insights-portal](./media/app-insights-asp-net/appinsights-04-openPortal.png)

> [!NOTE]
> Als u een access-fout krijgt: hebt u meer dan één set referenties van Microsoft en u bent aangemeld met de verkeerde set Hallo? In de portal Hallo afmelden en opnieuw aanmelden.

Hallo wordt geopend in een weergave van Hallo telemetrie van uw app.

![Schermopname van Application Insights-overzichtspagina](./media/app-insights-asp-net/66.png)

Klik in Hallo portal op een tegel of grafiek toosee meer details.

[Meer informatie over het gebruik van Application Insights in hello Azure-portal](app-insights-dashboards.md).

## <a name="step-4-publish-your-app"></a>Stap 4: uw app publiceren
Uw app tooyour IIS-server of tooAzure publiceren. Bekijk [livestream metrische gegevens](app-insights-metrics-explorer.md#live-metrics-stream) toomake ervoor dat alles goed wordt uitgevoerd.

Uw telemetrie wordt opgebouwd in Hallo Application Insights-portal, waar u kunt metrische gegevens controleren, doorzoeken uw Telemetrie en instellen van [dashboards](app-insights-dashboards.md). U kunt ook Hallo krachtige [querytaal van logboekanalyse](https://docs.loganalytics.io/) tooanalyze gebruik en prestaties of toofind specifieke gebeurtenissen.

U kunt tooanalyze ook blijven uw telemetrie in [Visual Studio](app-insights-visual-studio.md), met hulpprogramma's zoals diagnostische gegevens doorzoeken en [trends](app-insights-visual-studio-trends.md).

> [!NOTE]
> Als uw app voldoende telemetrie tooapproach hello verzendt [beperking limieten](app-insights-pricing.md#limits-summary), automatische [steekproeven](app-insights-sampling.md) switches op. Steekproeven vermindert Hallo hoeveelheid telemetrie van uw app verzonden behoud gecorreleerde gegevens voor diagnostische doeleinden.
>
>

## <a name="land"></a> U bent nu klaar

Gefeliciteerd. U Hallo Application Insights-pakket geïnstalleerd in uw app en het toosend telemetrie toohello Application Insights-service hebt geconfigureerd in Azure.

![Diagram van verplaatsing van telemetrie](./media/app-insights-asp-net/01-scheme.png)

Hello Azure-resource die telemetrie van uw app ontvangt wordt geïdentificeerd door een *instrumentatiesleutel*. U vindt deze sleutel in Hallo ApplicationInsights.config-bestand.


## <a name="upgrade-toofuture-sdk-versions"></a>De SDK-versies toofuture bijwerken
tooupgrade tooa [nieuwe release van Hallo SDK](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases)Open Hallo **NuGet-Pakketbeheer** opnieuw, en filteren op geïnstalleerde pakketten. Selecteer **Microsoft.ApplicationInsights.Web** en kies **Upgraden**.

Als u alle aanpassingen tooApplicationInsights.config genomen, een kopie van deze opslaan voordat u een upgrade. Vervolgens uw wijzigingen samen in de nieuwe versie Hallo.

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Volgende stappen

### <a name="more-telemetry"></a>Meer telemetrie

* **[Laadgegevens voor browser en pagina](app-insights-javascript.md)**: voeg een codefragment in uw webpagina's in.
* **[Gedetailleerde bewaking van afhankelijkheid en uitzonderingen](app-insights-monitor-performance-live-website-now.md)**: installeer Status Monitor op uw server.
* **[Aangepaste gebeurtenissen code](app-insights-api-custom-events-metrics.md)**  toocount, tijd en acties van de gebruiker te meten.
* **[Haal logboekgegevens op](app-insights-asp-net-trace-logs.md)**: koppel logboekgegevens aan uw telemetrie.

### <a name="analysis"></a>Analyse

* **[Met Application Insights werken in Visual Studio](app-insights-visual-studio.md)**<br/>Bevat informatie over foutopsporing met telemetrie, diagnostische gegevens doorzoeken en detailanalyse toocode.
* **[Werken met Hallo Application Insights-portal](app-insights-dashboards.md)**<br/> Bevat informatie over dashboards, krachtige hulpprogramma's voor diagnose en analyse, waarschuwingen, een live afhankelijkheidskaart van uw toepassing en exportmogelijkheden voor telemetrie.
* **[Analytics](app-insights-analytics-tour.md)**  -Hallo krachtige querytaal.

### <a name="alerts"></a>Waarschuwingen

* [Beschikbaarheidstests](app-insights-monitor-web-app-availability.md): tests maken toomake ervoor dat uw site op Hallo web zichtbaar is.
* [Diagnostische gegevens van smartcard](app-insights-proactive-diagnostics.md): deze tests uitgevoerd automatisch, dus u geen toodo alles tooset hebt deze. Deze geeft aan of een app een ongebruikelijk aantal mislukte aanvragen heeft.
* [Metrische waarschuwingen](app-insights-alerts.md): Stel deze toowarn u als een waarde een drempelwaarde overschrijdt. U kunt deze instellen op aangepaste metrische gegevens die u in uw app codeert.

### <a name="automation"></a>Automation

* [Het maken van een Application Insights-resource automatiseren](app-insights-powershell.md)
