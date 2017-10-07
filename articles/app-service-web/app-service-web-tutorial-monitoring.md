---
title: een Web-App aaaMonitor | Microsoft Docs
description: Meer informatie over hoe tooset van controle op uw Web-App
services: App-Service
keywords: 
author: btardif
ms.author: byvinyal
ms.date: 04/04/2017
ms.topic: article
ms.service: app-service-web
ms.openlocfilehash: c2f5e9842c732a804f1caee5d67e53dad24e190a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-app-service"></a>App Service bewaken
Deze zelfstudie wordt u via uw app voor bewaking en het gebruik van Hallo ingebouwde platform extra toosolve problemen wanneer deze optreden.

Elke sectie van dit document gaat over een specifieke functie. Hallo functies samen gebruikt, kunt u:
- Identificeren van een probleem in uw app.
- Bepalen wanneer Hallo probleem wordt veroorzaakt door uw code of het Hallo-platform.
- Verfijn Hallo bron van Hallo probleem in uw code.
- Foutopsporing en het verhelpen Hallo probleem.

## <a name="before-you-begin"></a>Voordat u begint
- U moet een toomonitor Web-App en Hallo volgen die worden beschreven stappen.
    - U kunt een toepassing hello stappen in Hallo maken [een ASP.NET-app maken in Azure met SQL Database](app-service-web-tutorial-dotnet-sqldatabase.md) zelfstudie.

- Als u wilt dat tootry uit **foutopsporing op afstand** van uw toepassing, moet u Visual Studio.
    - Als u Visual Studio 2017 geïnstalleerd nog geen hebt, kunt u downloaden en gebruiken van Hallo gratis [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).
    - Zorg ervoor dat u inschakelt **ontwikkelen van Azure** tijdens de installatie van Visual Studio Hallo.

## <a name="metrics"></a>Stap 1 - metrische gegevens weergeven
**Metrische gegevens** zijn nuttig toounderstand:
- Toepassingsstatus
- Appprestaties
- Resourceverbruik

Bij het onderzoeken van een toepassingsprobleem is metrische gegevens controleren een goede plaats toostart. Azure-portal is een snelle manier toovisually inspecteren Hallo metrische gegevens van uw app met **Azure Monitor**.

Metrische gegevens bestaan uit een historisch overzicht over diverse belangrijke aggregaties voor uw app. Voor elke app die wordt gehost in app service, moet u zowel Hallo Web-App en Hallo App Service-abonnement controleren.

> [!NOTE]
> Een App Service-plan vertegenwoordigt de verzameling Hallo van fysieke resources gebruikt toohost uw apps. Alle toepassingen toegewezen tooan App Service plan Hallo resources delen door deze zodat u toosave kosten bij het hosten van meerdere apps gedefinieerd.
>
> In App Service-plannen wordt het volgende gedefinieerd:
> * Regio: Noord-Europa, VS-Oost, Zuidoost-Azië, enzovoort.
> * Exemplaargrootte: Klein, normaal, groot, enzovoort.
> * Aantal van de schaal: een, twee of drie exemplaren, enzovoort.
> * SKU: Vrij gedeeld, Basic, Standard, Premium, enzovoort.

tooreview metrische gegevens voor uw Web-App, Ga toohello **overzicht** blade Hallo app dat u wilt dat toomonitor. Hier vindt u een grafiek voor metrische gegevens van uw app als een **bewaking tegel**. Klik op Hallo tegel tooedit configureren welke tooview metrische gegevens en Hallo tijd bereik toodisplay.

Standaard Hallo resourceblade biedt een weergave voor Hallo aanvragen en fouten voor Hallo afgelopen uur.
![App controleren](media/app-service-web-tutorial-monitoring/app-service-monitor.png)

Zoals u in voorbeeld hello ziet, we hebben een toepassing die veel genereert **HTTP-Server-fouten**. Hallo groot aantal fouten is de eerste vermelding Hallo tooinvestigate deze toepassing moet.

> [!TIP]
> Meer informatie over Azure-Monitor met Hallo koppelingen te volgen:
> - [Aan de slag met Azure-Monitor](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [Azure metrische gegevens](..\monitoring-and-diagnostics\monitoring-overview-metrics.md)
> - [Ondersteunde metrische gegevens met Azure-Monitor](..\monitoring-and-diagnostics\monitoring-supported-metrics.md)
> - [Azure Dashboards](..\azure-portal\azure-portal-dashboards.md)

## <a name="alerts"></a>Stap 2: waarschuwingen configureren
**Waarschuwingen** geconfigureerde tootrigger op bepaalde voorwaarden voor uw app kunt worden.

In [stap 1 - metrische gegevens weergeven](#metrics), hebt gezien dat Hallo-toepassing een groot aantal fouten heeft.

Een waarschuwing configureren kunt tooautomatically Blijf op de hoogte wanneer er fouten optreden. In dit geval we wilt Hallo waarschuwing toosend en e-telkens wanneer het aantal HTTP-50 X fouten Hallo over een bepaalde drempelwaarde komt gaat.

toocreate een waarschuwing, te navigeren**bewaking** > **waarschuwingen** en klik op **[+] Waarschuwing toevoegen**.

![Waarschuwingen](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts.png)

Geef waarden op voor de configuratie van de waarschuwing Hallo:
- **Bron:** Hallo site toomonitor met Hallo waarschuwing.
- **Naam:** een naam voor de waarschuwing, in dit geval: *hoge HTTP 50 X*.
- **Beschrijving:** tekst zonder opmaak uitleg van wat deze waarschuwing kijken is.
- **Waarschuwen bij:** waarschuwingen kunnen raadplegen metrische gegevens of gebeurtenissen, in dit voorbeeld wordt de metrische gegevens kijken.
- **Metrische gegevens:** welke metrische toomonitor, in dit geval: *HTTP-Server-fouten*.
- **Voorwaarde:** wanneer tooalert, in dit geval selecteert Hallo *groter is dan* optie.
- **Drempelwaarde:** wat toolook waarde, in dit geval is: *400*.
- **Periode:** waarschuwingen bepalen het verloop Hallo gemiddelde waarde van een metriek. Kleinere perioden yield gevoeliger waarschuwingen. in dit geval we kijkt *5 minuten*.
- **E-eigenaars en bijdragers:** in dit geval: *ingeschakeld*.

Nu dat hello waarschuwing wordt gemaakt een e-mailbericht wordt verzonden zodra hello app boven de drempelwaarde Hallo geconfigureerd gaat. Actieve waarschuwingen kunnen ook worden gecontroleerd in hello Azure-portal.

![Geactiveerde waarschuwingen](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts-triggered.png)


> [!TIP]
> Meer informatie over Azure-waarschuwingen Hello koppelingen te volgen:
> - [Wat zijn de waarschuwingen in Microsoft Azure](..\monitoring-and-diagnostics\monitoring-overview-alerts.md)
> - [Metrische gegevens van actie ondernemen](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [Metrische waarschuwingen maken](..\monitoring-and-diagnostics\insights-alerts-portal.md)

## <a name="companion"></a>Stap 3 - Companion-App Service
**App Service companion** biedt een handige manier toomonitor uw app met een systeemeigen ervaring in uw mobiele apparaat (iOS of Android).

App Service-Companion te gebruiken:
- Toepassing metrische gegevens controleren
- Bekijken en reageren op waarschuwingen toepassingsfouten en aanbevelingen
- Oplossen (bladeren, starten, stoppen, opnieuw opstarten Hallo app)
- Pushmeldingen voor kritieke gebeurtenissen worden opgehaald.

![Companion-App Service](media/app-service-web-tutorial-monitoring/app-service-companion.png)

[![App Service Companion App Store](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![Companion Google Play-App Service](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)

U kunt aanvullende App Service installeren vanaf Hallo [App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) of [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)

## <a name="diagnose"></a>Stap 4: diagnosticeren en oplossen van problemen
**Diagnosticeren en oplossen van problemen met** helpt u problemen met toepassingen verschillende vormen problemen met het platform. Deze kunt mogelijke oplossingen tooget ook uw Web-App back toohealthy voorstellen.

![Diagnosticeren en oplossen van problemen](media/app-service-web-tutorial-monitoring/app-service-monitor-diagnosis.png)

Hallo voorbeeld formulier vorige stappen voortzet, ziet u dat de toepassing hello heeft zijn er wanneer problemen. Hallo Platformbeschikbaarheid is daarentegen geen verplaatst van 100%.

Wanneer Hallo app heeft met het probleem en hello platform blijft up, is een duidelijke aanwijzing dat we zijn een toepassingsprobleem betreft.

## <a name="logging"></a>Stap 5 - logboekregistratie
Nu dat we hebben Hallo fouten tooan toepassingsprobleem domeinpartitie, kunnen we kijken Hallo toepassings- en logboeken tooget meer informatie.

Logboekregistratie kunt u beide toocollect **Application Diagnostics** en **Web Server Diagnostische** logboeken voor uw Web-App.

### <a name="application-diagnostics"></a>Application Diagnostics
Application diagnostics kunt u toocapture traceringen geproduceerd door de toepassing hello tijdens runtime.

Toe te voegen tracering tooyour verbetert toepassing aanzienlijk de mogelijkheid toodebug en speldenpunt problemen.

In ASP.NET, kunt u zich aanmelden met behulp van toepassingstraceringen [System.Diagnostics.Trace klasse](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) toogenerate gebeurtenissen die worden vastgelegd door Hallo logboek-infrastructuur. U kunt ook Hallo ernst van Hallo tracering voor het filteren van eenvoudiger opgeven.

```csharp
public ActionResult Delete(Guid? id)
{
    System.Diagnostics.Trace.TraceInformation("GET /Todos/Delete/" + id);
    if (id == null)
    {
        System.Diagnostics.Trace.TraceError("/Todos/Delete/ failed, ID is null");
        return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
    }
    Todo todo = db.Todoes.Find(id);
    if (todo == null)
    {
        System.Diagnostics.Trace.TraceWarning("/Todos/Delete/ failed, ID: " + id + " could not be found");
        return HttpNotFound();
    }
    System.Diagnostics.Trace.TraceInformation("GET /Todos/Delete/" + id + "completed successfully");
    return View(todo);
}
```
toepassingslogboeken tooenable te gaan**bewaking** > **diagnostische logboeken** en toepassing logboekregistratie inschakelen met behulp van Hallo Schakelknoppen.

![App controleren](media/app-service-web-tutorial-monitoring/app-service-monitor-applogs.png)

Toepassingslogboeken kunnen bestandssysteem opgeslagen tooyour van Web-App of tooblob opslag gepusht. Voor productiescenario's is het aanbevolen toouse blob-opslag.

> [!IMPORTANT]
> Logboekregistratie inschakelen, heeft een invloed op de prestatie- en gebruik van uw toepassing. Foutenlogboeken worden aanbevolen voor productiescenario's. Alleen meer uitgebreide logboekregistratie inschakelen bij het onderzoeken van problemen.

 ### <a name="web-server-diagnostics"></a>Web Server Diagnostische gegevens
Webserverlogboeken zijn gegenereerd, zelfs als uw app is niet geïnstrumenteerd. App Service kunt drie soorten server-logboeken verzamelen:

- **Web Server-logboekregistratie**
    - Informatie over HTTP transacties met Hallo [uitgebreide W3C-logboekbestandsindeling](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).
    - Dit is handig bij het bepalen van de algemene site metrische gegevens zoals het aantal aanvragen dat is verwerkt Hallo of hoeveel aanvragen van een specifiek IP-adres zijn.
- **Gedetailleerde fouten vastleggen**
    - Gedetailleerde informatie over de fout voor HTTP-statuscodes die wijzen op mislukte (statuscode 400 of hoger).
    - [Meer informatie over logboekregistratie van gedetailleerde fout](https://www.iis.net/learn/troubleshoot/diagnosing-http-errors/how-to-use-http-detailed-errors-in-iis)
- **Tracering van mislukte aanvragen**
    - Gedetailleerde informatie over mislukte verzoeken, met inbegrip van een tracering van Hallo IIS componenten gebruikt tooprocess Hallo-aanvraag en Hallo tijd benodigd in elk onderdeel.
    - Logboeken voor mislukte aanvragen zijn nuttig wanneer u probeert tooisolate wat de oorzaak van een specifieke HTTP-fout.
    - [Meer informatie over de tracering van mislukte aanvragen](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis)

logboekregistratie van tooenable-Server:
- Ga te**bewaking** > **diagnostische logboeken**.
- Verschillende soorten Web Server van diagnostische gegevens met Hallo Schakelknoppen Hallo inschakelen.

![App controleren](media/app-service-web-tutorial-monitoring/app-service-monitor-serverlogs.png)

> [!IMPORTANT]
> Logboekregistratie inschakelen, heeft een invloed op de prestatie- en gebruik van uw toepassing. Voor productiescenario's worden foutenlogboeken aanbevolen, wordt alleen inschakelen uitgebreide logboekregistratie bij het onderzoeken van problemen.

### <a name="accessing-logs"></a>Toegang tot logboeken
Logboeken die zijn opgeslagen in blob storage worden geopend met behulp van Azure Storage Explorer. Logboeken die zijn opgeslagen in het bestandssysteem Hallo van Web-App toegankelijk zijn via FTP onder Hallo paden te volgen:

- **Toepassingslogboeken** - `%HOME%/LogFiles/Application/`.
    - Deze map bevat een of meer tekstbestanden met informatie die wordt geproduceerd door logboekregistratie van toepassingen.
- **Kan aanvraag traceringen** - `%HOME%/LogFiles/W3SVC#########/`.
    - Deze map bevat een XSL-bestand en een of meer XML-bestanden.
- **Gedetailleerde foutenlogboeken** - `%HOME%/LogFiles/DetailedErrors/`.
    - Deze map bevat een of meer htm-bestanden met uitgebreide informatie over HTTP-fouten die zijn gegenereerd door uw app.
- **Web Server-logboeken** - `%HOME%/LogFiles/http/RawLogs`.
    - Deze map bevat een of meer tekstbestanden die zijn geformatteerd met uitgebreide Hallo W3C-logboekindeling.

## <a name="streaming"></a>Stap 6 - Streaming-logboek
Streaminglogboeken zijn handig als u fouten opspoort van een toepassing omdat bespaart u tijd te vergeleken[Hallo Logboeken openen](#Accessing-Logs) via FTP.

App Service kan worden gestreamd **toepassingslogboeken** en **Webserverlogboeken** nadat ze zijn gegenereerd.

> [!TIP]
> Voordat u zich aanmeldt toostream, zorg ervoor dat u kunt het verzamelen van Logboeken hebt ingeschakeld, zoals beschreven in Hallo [logboekregistratie](#logging) sectie.

toostream-logboeken te gaan**bewaking**> **Logboekstream**. Selecteer **toepassingslogboeken** of **Web server-logboeken** afhankelijk van welke informatie u zoekt. Hier kunt u ook onderbreken, opnieuw opstarten en Hallo buffer wissen.

![Streaminglogboeken](media/app-service-web-tutorial-monitoring/app-service-monitor-logstream.png)

> [!TIP]
> Logboeken worden alleen gemaakt wanneer er verkeer op Hallo app, u kunt ook Hallo uitgebreidheid van Logboeken tooget vergroten meer gebeurtenissen of informatie.

## <a name="remote"></a>Stap 7 - foutopsporing op afstand
Zodra u de pincode-waarnaar wordt verwezen Hallo bron van Hallo toepassingen problemen hebt, gebruikt **foutopsporing op afstand** toowalk via Hallo-code.

Externe foutopsporing kunt u koppelt een foutopsporingsprogramma tooyour Web-App uitgevoerd in de cloud Hallo. U kunt onderbrekingspunten instellen, geheugen rechtstreeks te manipuleren, analyseer code en zelfs wijzigen Hallo codepad net zoals u zou doen voor een app die lokaal wordt uitgevoerd.

tooattach hello foutopsporingsprogramma tooyour app uitgevoerd in de cloud Hallo:

- Met behulp van Visual Studio 2017 open Hallo-oplossing voor het Hallo-app wilt toodebug
- Enkele punten bedient net zoals u zou voor lokale ontwikkeling doen ingesteld.
- Open **cloud explorer** (ctr + /, ctrl + x).
- Aanmelden met uw azure-referenties indien nodig.
- Zoeken naar Hallo app gewenste toodebug
- Selecteer **foutopsporingsprogramma koppelen** formulier Hallo **acties** deelvenster.

![Foutopsporing op afstand](media/app-service-web-tutorial-monitoring/app-service-monitor-vsdebug.png)

Visual Studio, configureert u uw toepassing voor foutopsporing op afstand en opent een browservenster dat tooyour app navigeert. Blader door de onderbreking van uw app-tootrigger en analyseer Hallo-code.

> [!WARNING]
> Uitgevoerd in de foutopsporingsmodus in productie wordt niet aanbevolen. Als uw productie-app is toomultiple server-exemplaren niet worden uitgebreid, foutopsporing Hallo-webserver niet reageert tooother aanvragen voorkomen. Voor het oplossen van problemen, is de beste bron te[logboekregistratie configureren](#logging) en [Application Insights](#insights).



## <a name="explorer"></a>Stap 8 - Procesverkenner
Wanneer uw toepassing uit toomore dan één exemplaar wordt geschaald **procesverkenner** kunt u exemplaar specifieke problemen te identificeren.

Gebruik **Explorer verwerken** naar:

- Het inventariseren van alle Hallo-processen tussen verschillende exemplaren van uw App Service-abonnement.
- Inzoomen en Hallo-ingangen en modules die zijn gekoppeld aan elk proces weergeven.
- Weergave CPU, werkset en Thread aantal bij Hallo verwerken niveau toohelp u buitensporige processen identificeren
- Geopende bestandsingangen vinden en zelfs voor afsluiten van een specifiek proces-exemplaar.

Proces Explorer kunt u vinden onder **bewaking** > **Procesverkenner**.

![Procesverkenner](media/app-service-web-tutorial-monitoring/app-service-monitor-processexplorer.png)


## <a name="insights"></a>Stap 9 - Application Insights
**Application Insights** toepassingen en geavanceerde mogelijkheden voor bewaking biedt voor uw app.

Gebruik Application Insights toodetect en onderzoeken van uitzonderingen en prestatieproblemen in uw Web-App.

U kunt Application Insights inschakelen voor uw Web-App onder **bewaking** > **Application Insights**

> [!NOTE]
> Application Insights mogelijk wordt u gevraagd tooinstall Hallo Application Insights-site-uitbreiding toostart verzamelen van gegevens. Installeren van site-extensie Hallo zorgt ervoor dat een toepassing opnieuw starten.

![Application Insights](media/app-service-web-tutorial-monitoring/app-service-monitor-appinsights.png)

Application Insights is een geavanceerde functie stelt toolearn meer Hallo koppelingen volgen opgenomen in Hallo [Vervolgstappen](#next) sectie.

## <a name="next"></a> Volgende stappen

 - [Wat is Application Insights](..\application-insights\app-insights-overview.md)
 - [Bewaking van prestaties van de Azure-web-app met Application Insights](..\application-insights\app-insights-azure-web-apps.md)
 - [Beschikbaarheid en reactiesnelheid van een website met Application Insights bewaken](..\application-insights\app-insights-monitor-web-app-availability.md)
