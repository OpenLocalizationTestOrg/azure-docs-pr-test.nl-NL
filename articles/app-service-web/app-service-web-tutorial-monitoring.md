---
title: Een Web-App bewaken | Microsoft Docs
description: Meer informatie over het instellen van de controle op uw Web-App
services: App-Service
keywords: 
author: btardif
ms.author: byvinyal
ms.date: 04/04/2017
ms.topic: article
ms.service: app-service-web
ms.openlocfilehash: 29df824062d00e01b786533033097948c008588f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-app-service"></a>App Service bewaken
Deze zelfstudie wordt u via uw app voor bewaking en oplossen van problemen wanneer ze zich voordoen met behulp van de ingebouwde platformhulpprogramma's.

Elke sectie van dit document gaat over een specifieke functie. Samen met behulp van de functies, kunt u:
- Identificeren van een probleem in uw app.
- Bepalen wanneer het probleem wordt veroorzaakt door uw code of het platform.
- Verfijn de bron van het probleem in uw code.
- Foutopsporing en verhelpen van het probleem.

## <a name="before-you-begin"></a>Voordat u begint
- U moet een Web-App om te controleren en volg de stappen beschreven.
    - Kunt u een toepassing die de stappen in de [een ASP.NET-app maken in Azure met SQL Database](app-service-web-tutorial-dotnet-sqldatabase.md) zelfstudie.

- Als u wilt uitproberen **foutopsporing op afstand** van uw toepassing, moet u Visual Studio.
    - Als u Visual Studio 2017 geïnstalleerd nog geen hebt, kunt u downloaden en gebruiken de gratis [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).
    - Zorg ervoor dat u **Azure-ontwikkeling** inschakelt tijdens de installatie van Visual Studio.

## <a name="metrics"></a>Stap 1 - metrische gegevens weergeven
**Metrische gegevens** zijn handig om te begrijpen:
- Toepassingsstatus
- Appprestaties
- Resourceverbruik

Bij het onderzoeken van een toepassingsprobleem is metrische gegevens controleren een goede plaats om te starten. Azure-portal is een snelle manier om visueel controleren en de metrische gegevens van uw app met **Azure Monitor**.

Metrische gegevens bestaan uit een historisch overzicht over diverse belangrijke aggregaties voor uw app. Voor elke app die wordt gehost in app service, moet u zowel de Web-App en de App Service-abonnement controleren.

> [!NOTE]
> Een App Service-plan bestaat uit een verzameling van fysieke resources die worden gebruikt voor het hosten van uw apps. Alle toepassingen die zijn toegewezen aan een App Service-plan, delen de gedefinieerde resources, zodat u kosten kunt besparen als u meerdere apps host.
>
> In App Service-plannen wordt het volgende gedefinieerd:
> * Regio: Noord-Europa, VS-Oost, Zuidoost-Azië, enzovoort.
> * Exemplaargrootte: Klein, normaal, groot, enzovoort.
> * Aantal van de schaal: een, twee of drie exemplaren, enzovoort.
> * SKU: Vrij gedeeld, Basic, Standard, Premium, enzovoort.

Als u wilt controleren metrische gegevens voor uw Web-App, gaat u naar de **overzicht** blade van de app die u wilt bewaken. Hier vindt u een grafiek voor metrische gegevens van uw app als een **bewaking tegel**. Klik op de tegel om te bewerken en configureren welke metrische gegevens weergeven en het tijdsbereik om weer te geven.

De resourceblade biedt standaard een weergave voor de toepassingsaanvragen en fouten voor het afgelopen uur.
![App controleren](media/app-service-web-tutorial-monitoring/app-service-monitor.png)

Zoals u in het voorbeeld zien kunt, hebben we een toepassing die veel genereert **HTTP-Server-fouten**. Het grote aantal fouten is de eerste vermelding moet voor het onderzoeken van deze toepassing.

> [!TIP]
> Meer informatie over Azure-Monitor met de volgende koppelingen:
> - [Aan de slag met Azure-Monitor](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [Azure metrische gegevens](..\monitoring-and-diagnostics\monitoring-overview-metrics.md)
> - [Ondersteunde metrische gegevens met Azure-Monitor](..\monitoring-and-diagnostics\monitoring-supported-metrics.md)
> - [Azure Dashboards](..\azure-portal\azure-portal-dashboards.md)

## <a name="alerts"></a>Stap 2: waarschuwingen configureren
**Waarschuwingen** kunnen worden geconfigureerd als reactie op bepaalde voorwaarden voor uw app.

In [stap 1 - metrische gegevens weergeven](#metrics), hebt gezien dat de toepassing een groot aantal fouten heeft.

U kunt configureren een waarschuwing automatisch Blijf op de hoogte wanneer er fouten optreden. In dit geval willen we de waarschuwing te verzenden en e-telkens wanneer het aantal HTTP-50 X fouten over een bepaalde drempelwaarde komt gaat.

Voor het maken van een waarschuwing, gaat u naar **bewaking** > **waarschuwingen** en klik op **[+] Waarschuwing toevoegen**.

![Waarschuwingen](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts.png)

Geef waarden op voor de configuratie van de waarschuwing:
- **Bron:** de site om te bewaken die de waarschuwing.
- **Naam:** een naam voor de waarschuwing, in dit geval: *hoge HTTP 50 X*.
- **Beschrijving:** tekst zonder opmaak uitleg van wat deze waarschuwing kijken is.
- **Waarschuwen bij:** waarschuwingen kunnen raadplegen metrische gegevens of gebeurtenissen, in dit voorbeeld wordt de metrische gegevens kijken.
- **Metrische gegevens:** welke metriek te bewaken, in dit geval: *HTTP-Server-fouten*.
- **Voorwaarde:** wanneer op waarschuwing, in dit geval selecteert de *groter is dan* optie.
- **Drempelwaarde:** wat is de waarde te zoeken, in dit geval: *400*.
- **Periode:** waarschuwingen bepalen het verloop van de gemiddelde waarde van een metriek. Kleinere perioden yield gevoeliger waarschuwingen. in dit geval we kijkt *5 minuten*.
- **E-eigenaars en bijdragers:** in dit geval: *ingeschakeld*.

Nu dat de waarschuwing is gemaakt wordt een e-mail verzonden telkens wanneer de app via de geconfigureerde drempelwaarde wordt. Actieve waarschuwingen kunnen ook worden gecontroleerd in de Azure portal.

![Geactiveerde waarschuwingen](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts-triggered.png)


> [!TIP]
> Meer informatie over Azure-waarschuwingen met de volgende koppelingen:
> - [Wat zijn de waarschuwingen in Microsoft Azure](..\monitoring-and-diagnostics\monitoring-overview-alerts.md)
> - [Metrische gegevens van actie ondernemen](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [Metrische waarschuwingen maken](..\monitoring-and-diagnostics\insights-alerts-portal.md)

## <a name="companion"></a>Stap 3 - Companion-App Service
**App Service companion** biedt een handige manier om het bewaken van uw app met een systeemeigen ervaring in uw mobiele apparaat (iOS of Android).

App Service-Companion te gebruiken:
- Toepassing metrische gegevens controleren
- Bekijken en reageren op waarschuwingen toepassingsfouten en aanbevelingen
- Oplossen (bladeren, starten, stoppen, start de app opnieuw)
- Pushmeldingen voor kritieke gebeurtenissen worden opgehaald.

![Companion-App Service](media/app-service-web-tutorial-monitoring/app-service-companion.png)

[![App Service Companion App Store](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![Companion Google Play-App Service](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)

U kunt aanvullende van App Service installeren de [App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) of [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)

## <a name="diagnose"></a>Stap 4: diagnosticeren en oplossen van problemen
**Diagnosticeren en oplossen van problemen met** helpt u problemen met toepassingen verschillende vormen problemen met het platform. Het kan ook mogelijke oplossingen voor uw Web-App op in orde voorstellen.

![Diagnosticeren en oplossen van problemen](media/app-service-web-tutorial-monitoring/app-service-monitor-diagnosis.png)

U doorgaat met de vorige stappen van voorbeeld formulier, ziet u dat de toepassing heeft zijn er wanneer problemen. Daarentegen is dat de Platformbeschikbaarheid niet heeft verplaatst van 100%.

Bij de app is een probleem en de blijft platform up, is een duidelijke aanwijzing dat we zijn een toepassingsprobleem betreft.

## <a name="logging"></a>Stap 5 - logboekregistratie
Nu dat we hebben de fouten voor een toepassingsprobleem domeinpartitie, kunnen we de toepassing en de server-logboeken voor meer informatie bekijken.

Logboekregistratie kunt u beide verzamelen **Application Diagnostics** en **Web Server Diagnostische** logboeken voor uw Web-App.

### <a name="application-diagnostics"></a>Application Diagnostics
Application diagnostics kunt u vastleggen van traces geproduceerd door de toepassing tijdens runtime.

Toe te voegen aanzienlijk tracering voor uw toepassing verbetert de mogelijkheid opsporen en speldenpunt problemen.

In ASP.NET, kunt u zich aanmelden met behulp van toepassingstraceringen [System.Diagnostics.Trace klasse](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) voor het genereren van gebeurtenissen die door de infrastructuur van het logboek worden vastgelegd. U kunt ook de ernst van de tracering voor het filteren van eenvoudiger opgeven.

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
Schakel toepassingslogboeken in Ga naar de **bewaking** > **diagnostische logboeken** en toepassing logboekregistratie inschakelen met behulp van de in-of uitschakelen.

![App controleren](media/app-service-web-tutorial-monitoring/app-service-monitor-applogs.png)

Toepassingslogboeken worden opgeslagen in uw Web-App-bestandssysteem of naar de blob storage wordt gepusht. Het is raadzaam voor productiescenario's blob storage gebruiken.

> [!IMPORTANT]
> Logboekregistratie inschakelen, heeft een invloed op de prestatie- en gebruik van uw toepassing. Foutenlogboeken worden aanbevolen voor productiescenario's. Alleen meer uitgebreide logboekregistratie inschakelen bij het onderzoeken van problemen.

 ### <a name="web-server-diagnostics"></a>Web Server Diagnostische gegevens
Webserverlogboeken zijn gegenereerd, zelfs als uw app is niet geïnstrumenteerd. App Service kunt drie soorten server-logboeken verzamelen:

- **Web Server-logboekregistratie**
    - Informatie over HTTP transacties met behulp van de [uitgebreide W3C-logboekbestandsindeling](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).
    - Dit is handig bij het bepalen van de algemene site metrische gegevens zoals het aantal aanvragen dat is verwerkt of hoeveel aanvragen van een specifiek IP-adres.
- **Gedetailleerde fouten vastleggen**
    - Gedetailleerde informatie over de fout voor HTTP-statuscodes die wijzen op mislukte (statuscode 400 of hoger).
    - [Meer informatie over logboekregistratie van gedetailleerde fout](https://www.iis.net/learn/troubleshoot/diagnosing-http-errors/how-to-use-http-detailed-errors-in-iis)
- **Tracering van mislukte aanvragen**
    - Gedetailleerde informatie over mislukte verzoeken, met inbegrip van een tracering van de IIS-onderdelen gebruikt voor het verwerken van de aanvraag en de tijd die in elk onderdeel.
    - Mislukte aanvragen logboeken handig zijn wanneer u probeert te isoleren wat wordt veroorzaakt door een specifieke HTTP-fout.
    - [Meer informatie over de tracering van mislukte aanvragen](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis)

Server-logboekregistratie inschakelen:
- Ga naar **bewaking** > **diagnostische logboeken**.
- Schakel de verschillende soorten Web Server Diagnostische gegevens met behulp van de in-of uitschakelen.

![App controleren](media/app-service-web-tutorial-monitoring/app-service-monitor-serverlogs.png)

> [!IMPORTANT]
> Logboekregistratie inschakelen, heeft een invloed op de prestatie- en gebruik van uw toepassing. Voor productiescenario's worden foutenlogboeken aanbevolen, wordt alleen inschakelen uitgebreide logboekregistratie bij het onderzoeken van problemen.

### <a name="accessing-logs"></a>Toegang tot logboeken
Logboeken die zijn opgeslagen in blob storage worden geopend met behulp van Azure Storage Explorer. Logboeken die zijn opgeslagen in de Web-App bestandssysteem toegankelijk zijn via FTP onder de volgende paden:

- **Toepassingslogboeken** - `%HOME%/LogFiles/Application/`.
    - Deze map bevat een of meer tekstbestanden met informatie die wordt geproduceerd door logboekregistratie van toepassingen.
- **Kan aanvraag traceringen** - `%HOME%/LogFiles/W3SVC#########/`.
    - Deze map bevat een XSL-bestand en een of meer XML-bestanden.
- **Gedetailleerde foutenlogboeken** - `%HOME%/LogFiles/DetailedErrors/`.
    - Deze map bevat een of meer htm-bestanden met uitgebreide informatie over HTTP-fouten die zijn gegenereerd door uw app.
- **Web Server-logboeken** - `%HOME%/LogFiles/http/RawLogs`.
    - Deze map bevat een of meer tekstbestanden die zijn geformatteerd met de indeling van het W3C-uitgebreide logboekbestand.

## <a name="streaming"></a>Stap 6 - Streaming-logboek
Streaminglogboeken zijn handig als u fouten opspoort van een toepassing omdat bespaart u tijd vergeleken met [toegang tot de logboeken](#Accessing-Logs) via FTP.

App Service kan worden gestreamd **toepassingslogboeken** en **Webserverlogboeken** nadat ze zijn gegenereerd.

> [!TIP]
> Voordat u probeert te streamen van Logboeken, controleert u of u het verzamelen van Logboeken hebt ingeschakeld zoals beschreven in de [logboekregistratie](#logging) sectie.

Om te streamen van Logboeken, gaat u naar **bewaking**> **Logboekstream**. Selecteer **toepassingslogboeken** of **Web server-logboeken** afhankelijk van welke informatie u zoekt. Hier kunt u ook onderbreken, opnieuw opstarten en wissen van de buffer.

![Streaminglogboeken](media/app-service-web-tutorial-monitoring/app-service-monitor-logstream.png)

> [!TIP]
> Logboeken worden alleen gemaakt wanneer er verkeer op de app, kunt u ook de uitgebreidheid van Logboeken meer gebeurtenissen of gegevens ophalen verhogen.

## <a name="remote"></a>Stap 7 - foutopsporing op afstand
Zodra u pincode-in het vervolgmenu van de bron van de problemen met toepassingen, gebruikt u **foutopsporing op afstand** stapsgewijs door de code.

Externe foutopsporing kunt u een foutopsporingsprogramma koppelen aan uw Web-App uitgevoerd in de cloud. U kunt onderbrekingspunten instellen, geheugen rechtstreeks te manipuleren, analyseer code en zelfs de codepad wijzigen, net zoals u zou doen voor een app die lokaal wordt uitgevoerd.

Het foutopsporingsprogramma koppelen aan uw app uitgevoerd in de cloud:

- Visual Studio 2017, opent u de oplossing voor de app die u wilt opsporen
- Enkele punten bedient net zoals u zou voor lokale ontwikkeling doen ingesteld.
- Open **cloud explorer** (ctr + /, ctrl + x).
- Aanmelden met uw azure-referenties indien nodig.
- De app die u wilt voor foutopsporing te zoeken
- Selecteer **foutopsporingsprogramma koppelen** formulier de **acties** deelvenster.

![Foutopsporing op afstand](media/app-service-web-tutorial-monitoring/app-service-monitor-vsdebug.png)

Visual Studio, configureert u uw toepassing voor foutopsporing op afstand en opent een browservenster dat naar uw app navigeren. Blader door uw app voor het activeren van onderbreking en doorloop de code.

> [!WARNING]
> Uitgevoerd in de foutopsporingsmodus in productie wordt niet aanbevolen. Als uw productie-app niet naar meerdere exemplaren van server is uitgebreid, foutopsporing te voorkomen dat de webserver reageert op andere aanvragen. Voor de productieproblemen wilt oplossen, is het de beste bron te [logboekregistratie configureren](#logging) en [Application Insights](#insights).



## <a name="explorer"></a>Stap 8 - Procesverkenner
Wanneer uw toepassing wordt uitgebreid naar meer dan één exemplaar **procesverkenner** kunt u exemplaar specifieke problemen te identificeren.

Gebruik **Explorer verwerken** naar:

- Alle processen opsommen over verschillende exemplaren van uw App Service-abonnement.
- Inzoomen en weergeven van de ingangen en de modules die zijn gekoppeld aan elk proces.
- CPU, werkset, weergeven en threads op het procesniveau van het om te identificeren voor overmatig processen
- Geopende bestandsingangen vinden en zelfs voor afsluiten van een specifiek proces-exemplaar.

Proces Explorer kunt u vinden onder **bewaking** > **Procesverkenner**.

![Procesverkenner](media/app-service-web-tutorial-monitoring/app-service-monitor-processexplorer.png)


## <a name="insights"></a>Stap 9 - Application Insights
**Application Insights** toepassingen en geavanceerde mogelijkheden voor bewaking biedt voor uw app.

Application Insights gebruiken om te detecteren en onderzoeken van uitzonderingen en prestatieproblemen in uw Web-App.

U kunt Application Insights inschakelen voor uw Web-App onder **bewaking** > **Application Insights**

> [!NOTE]
> Application Insights vragen u voor het installeren van de extensie Application Insights site om te beginnen met het verzamelen van gegevens. Installeren van de site-extensie zorgt ervoor dat een toepassing opnieuw starten.

![Application Insights](media/app-service-web-tutorial-monitoring/app-service-monitor-appinsights.png)

Application Insights is een geavanceerde functie instellen, volgt u de opgenomen in koppelingen voor meer informatie de [Vervolgstappen](#next) sectie.

## <a name="next"></a> Volgende stappen

 - [Wat is Application Insights](..\application-insights\app-insights-overview.md)
 - [Bewaking van prestaties van de Azure-web-app met Application Insights](..\application-insights\app-insights-azure-web-apps.md)
 - [Beschikbaarheid en reactiesnelheid van een website met Application Insights bewaken](..\application-insights\app-insights-monitor-web-app-availability.md)
