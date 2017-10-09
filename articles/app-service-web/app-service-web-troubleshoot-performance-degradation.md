---
title: prestaties van aaaSlow web-app in App Service | Microsoft Docs
description: In dit artikel helpt u problemen met trage web app prestaties in Azure App Service.
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: top-support-issue
keywords: Web-appprestaties, trage app de app is langzaam
ms.assetid: b8783c10-3a4a-4dd6-af8c-856baafbdde5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2016
ms.author: cephalin
ms.openlocfilehash: 3e56b99b48db0e7baae1fac797a7fcb9eff74c9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-slow-web-app-performance-issues-in-azure-app-service"></a>Oplossen van prestatieproblemen van trage web-app in Azure App Service
Dit artikel helpt u problemen met trage web app prestaties in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).

Als u meer hulp op elk gewenst moment in dit artikel nodig hebt, kunt u raadplegen hello Azure deskundigen op [hello Azure MSDN en forums Stack Overflow Hallo](https://azure.microsoft.com/support/forums/). U kunt ook kunt u ook een incident voor ondersteuning van Azure bestand. Ga toohello [ondersteuning van Azure site](https://azure.microsoft.com/support/options/) en klik op **Get Support**.

## <a name="symptom"></a>Symptoom
Als u Hallo web-app bladert, Hallo laden van pagina's traag en soms time-out.

## <a name="cause"></a>Oorzaak
Dit probleem wordt vaak veroorzaakt door problemen met toepassingen niveau, zoals:

* netwerkaanvragen duurt lang
* toepassing code of database-query's wordt inefficiënt
* toepassing met hoge geheugen/CPU
* toepassing is gecrasht vanwege uitzondering tooan

## <a name="troubleshooting-steps"></a>Stappen voor probleemoplossing
Het oplossen van problemen kan worden onderverdeeld in drie verschillende taken in opeenvolgende volgorde:

1. [Bekijken en controleren van gedrag van toepassingen](#observe)
2. [Gegevens verzamelen](#collect)
3. [Hallo probleem verhelpen](#mitigate)

[App Service Web Apps](/services/app-service/web/) biedt verschillende opties bij elke stap.

<a name="observe" />

### <a name="1-observe-and-monitor-application-behavior"></a>1. Bekijken en controleren van gedrag van toepassingen
#### <a name="track-service-health"></a>Servicestatus bijhouden
Microsoft Azure publicizes telkens wanneer er een service wordt onderbroken of de prestaties nadelig beïnvloeden is. U kunt Hallo status van Hallo service bijhouden op Hallo [Azure-portal](https://portal.azure.com/). Zie voor meer informatie [bijhouden servicestatus](../monitoring-and-diagnostics/insights-service-health.md).

#### <a name="monitor-your-web-app"></a>Uw web-app bewaken
Deze optie kunt u toofind uit als uw toepassing problemen ondervindt. Klik in de blade van uw web-app op Hallo **aanvragen en fouten** tegel. Hallo **metriek** blade ziet u alle Hallo metrische gegevens u kunt toevoegen.

Aantal Hallo metrische gegevens die u toomonitor voor uw web-app wilt mogelijk

* Gemiddelde geheugen werkset
* Gemiddelde reactietijd
* CPU-tijd
* Geheugen-werkset
* Aanvragen

![web-app-prestaties bewaken](./media/app-service-web-troubleshoot-performance-degradation/1-monitor-metrics.png)

Zie voor meer informatie:

* [Web-Apps bewaken in Azure App Service](web-sites-monitor.md)
* [Waarschuwingen ontvangen](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

#### <a name="monitor-web-endpoint-status"></a>Web-Eindpuntstatus controleren
Als u uw web-app in Hallo uitvoert **standaard** Web-Apps prijscategorie, kunt u twee eindpunten van drie verschillende geografische locaties bewaken.

Eindpuntcontrole configureert webtests van geografisch verspreide locaties met reactietijden en uptime van web-URL's testen. Hallo test voert een HTTP GET-bewerking op Hallo web-URL toodetermine Hallo reactietijd en bedrijfstijd vanaf elke locatie. Elke geconfigureerde locatie wordt een test om de vijf minuten uitgevoerd.

Actieve tijdsduur wordt bewaakt met HTTP-antwoordcodes en reactietijd wordt gemeten in milliseconden. Een bewakingstest mislukt als Hallo HTTP-antwoordcode is groter dan of gelijk too400 of als antwoord Hallo langer dan 30 seconden duurt. Een eindpunt wordt aangemerkt als beschikbaar als de bewakingstests uit alle slagen Hallo opgegeven locaties.

tooset deze, Zie [in Azure App Service-apps bewaken](web-sites-monitor.md).

Zie ook [Azure-websites te houden van plus Eindpuntcontrole - met Stefan Schackow](https://channel9.msdn.com/Shows/Azure-Friday/Keeping-Azure-Web-Sites-up-plus-Endpoint-Monitoring-with-Stefan-Schackow) voor een video over eindpuntcontrole.

#### <a name="application-performance-monitoring-using-extensions"></a>APM-extensies gebruiken
U kunt ook de toepassingsprestaties van uw bewaken met behulp van *site-uitbreidingen*.

Elke App Service-web-app biedt een uitbreidbare management-eindpunt waarmee u toouse een krachtige reeks hulpprogramma's die zijn geïmplementeerd als site-uitbreidingen. Extensies zijn onder andere: 

- Bron code-editors, zoals [Visual Studio Team Services](https://www.visualstudio.com/products/what-is-visual-studio-online-vs.aspx). 
- Beheerhulpprogramma's voor verbonden resources, zoals een MySQL-database verbonden tooa web-app.

[Azure Application Insights](/services/application-insights/) en [New Relic](/marketplace/partners/newrelic/newrelic/) zijn twee Hallo-site-uitbreidingen die beschikbaar zijn voor prestatiebewaking. New Relic toouse, u installeert een agent tijdens runtime. Azure Application Insights toouse, dat u uw code bij een SDK bouwen en u kunt ook een uitbreiding die voorzien van toegang tot tooadditional gegevens installeren. Hallo SDK kunt u code toomonitor Hallo gebruik en prestaties van uw app in meer detail schrijven.

Zie toouse Application Insights [prestaties van webtoepassingen bewaken](../application-insights/app-insights-web-monitor-performance.md).

Zie toouse New Relic [nieuwe Relic prestaties Toepassingsbeheer op Azure](../store-new-relic-cloud-services-dotnet-application-performance-management.md).

<a name="collect" />

### <a name="2-collect-data"></a>2. Gegevens verzamelen
Hallo-Web-Apps-omgeving biedt diagnostische functionaliteit voor logboekinformatie van zowel Hallo-webserver en Hallo-webtoepassing. Hallo-informatie is onderverdeeld in web server diagnostics en application diagnostics.

#### <a name="enable-web-server-diagnostics"></a>Web server diagnostische gegevens inschakelen
U kunt in- of uitschakelen van Hallo soorten logboeken te volgen:

* **Gedetailleerde fout logboekregistratie** -gedetailleerde informatie over de fout voor HTTP-statuscodes die wijzen op mislukte (statuscode 400 of hoger). Dit kan bevatten informatie om te bepalen waarom Hallo server Hallo foutcode geretourneerd.
* **Kan geen aanvraag voor het traceren** -gedetailleerde informatie over de mislukte aanvragen, met inbegrip van een tracering van Hallo IIS componenten gebruikt tooprocess Hallo aanvraag en Hallo-tijd benodigd in elk onderdeel. Dit is handig als u de webprestaties app tooimprove probeert of komen wat een specifieke HTTP-fout wordt veroorzaakt.
* **Web Server-logboekregistratie** -informatie over HTTP transacties met uitgebreide Hallo W3C-logboekindeling. Dit is handig bij het bepalen van de algemene web app metrische gegevens, zoals het aantal aanvragen dat is verwerkt Hallo of hoeveel aanvragen van een specifiek IP-adres zijn.

#### <a name="enable-application-diagnostics"></a>Toepassing diagnostische gegevens inschakelen
Er zijn verschillende opties toocollect prestatiegegevens van toepassingen vanuit Web Apps, profiel van uw toepassing live vanuit Visual Studio of te wijzigen van uw toepassing code toolog meer informatie en traceringen. Hallo-opties op basis kunt u op hoeveel toegang hebt u toohello toepassing en u waargenomen van Hallo controlehulpprogramma's.

##### <a name="use-application-insights-profiler"></a>Gebruik Application Insights Profiler
U kunt Hallo Application Insights Profiler toostart gedetailleerde prestaties traceringen vastleggen inschakelen. Toegang tot traceringen up toofive dagen geleden wanneer u nodig tooinvestigate problemen hebt is opgetreden in de afgelopen Hallo vastgelegd. U kunt deze optie als u Application Insights-resource toegang toohello van web-app in Azure portal hebt.

Application Insights Profiler voorziet in statistieken op de reactietijd voor elke aanroep van de web- en traceringen die aangeeft welke coderegel veroorzaakt Hallo trage reacties. Soms hello App Service-app is langzaam omdat bepaalde code niet in een zodat geschreven wordt manier. Voorbeelden zijn opeenvolgende code die in de database voor parallelle en ongewenste vergrendeling contentions kan worden uitgevoerd. Deze knelpunten in Hallo code verwijdert, wordt het Hallo-app sneller, maar ze zijn harde toodetect zonder uitgebreide traceringen en logboeken te stellen. Hallo traceringen verzameld door Application Insights Profiler helpt Hallo regels code waarmee de toepassing hello vertraagd te identificeren en deze uitdaging voor App Service-apps te ondervangen.

 Zie voor meer informatie [Profiling live Azure-web-apps met Application Insights](../application-insights/app-insights-profiler.md).

##### <a name="use-remote-profiling"></a>Profileren van externe gebruiken
In Azure App Service Web Apps, API-Apps en WebJobs kunnen op afstand profiling wordt gestart. Selecteer deze optie als u resource toegang toohello web-app hebt en u weet hoe tooreproduce probleem Hallo of als u Hallo exacte weet tijd interval Hallo prestatieprobleem gebeurt.

Externe Profiling is handig als Hallo CPU-gebruik van Hallo-proces hoog is en uw proces trager dan verwacht wordt uitgevoerd of Hallo latentie van HTTP-aanvragen zijn hoger dan normaal, u kunt op afstand uw proces bekijken en Hallo CPU steekproeven aanroep stacks tooanalyze ophalen Hallo procesactiviteit en code hot paden.

Zie voor meer informatie [afstand profileren ondersteuning in Azure App Service](https://azure.microsoft.com/blog/remote-profiling-support-in-azure-app-service).

##### <a name="set-up-diagnostic-traces-manually"></a>Diagnostische traceringen handmatig instellen
Als u toegang toohello web application-broncode hebt, kunt u Application diagnostics toocapture informatie die wordt geproduceerd door een webtoepassing. ASP.NET-toepassingen kunnen gebruikmaken van Hallo `System.Diagnostics.Trace` klasse toolog informatie toohello application diagnostics melden. U moet echter toochange Hallo code en uw toepassing opnieuw distribueren. Deze methode wordt aanbevolen als uw app wordt uitgevoerd op een testomgeving.

Voor gedetailleerde instructies voor het tooconfigure uw toepassing voor logboekregistratie, Zie [logboekregistratie van diagnostische gegevens van web-apps in Azure App Service](web-sites-enable-diagnostic-log.md).

#### <a name="use-hello-azure-app-service-support-portal"></a>Hello Azure App Service-ondersteuning portal gebruiken
Web Apps biedt Hallo mogelijkheid tootroubleshoot problemen gerelateerde tooyour web-app door te kijken HTTP Logboeken, gebeurtenislogboeken proces dumpbestanden en meer. U toegang hebt tot deze informatie met onze portal ondersteuning op **http://&lt;uw app-naam >.scm.azurewebsites.net/Support**

Hello Azure App Service-ondersteuning portal biedt drie afzonderlijke tabbladen toosupport Hallo drie stappen van een algemeen scenario voor het oplossen van problemen:

1. Huidige gedrag observeren
2. Door het verzamelen van diagnostische gegevens en Hallo ingebouwde analyzers analyseren
3. Beperken

Als het probleem Hallo nu zich voordoet, klikt u op **analyseren** > **Diagnostics** > **onderzoeken nu** toocreate een diagnostische sessie voor u HTTP-Logboeken, logboeken geheugendumps, PHP-foutenlogboek en PHP-proces rapport verzamelt.

Zodra het Hallo-gegevens worden verzameld, wordt een analyse uitgevoerd op gegevens Hallo Hallo ondersteuning portal op en biedt u een HTML-rapport.

Als u wilt dat toodownload Hallo gegevens, standaard, zou dit worden opgeslagen in Hallo D:\home\data\DaaS map.

Zie voor meer informatie over hello Azure App Service-ondersteuning portal [nieuwe Updates tooSupport Site-uitbreiding voor Azure Websites](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).

#### <a name="use-hello-kudu-debug-console"></a>Hallo Kudu-Console voor foutopsporing gebruiken
Web-Apps wordt geleverd met een Foutopsporingsconsole die u gebruiken kunt voor foutopsporing, verkennen, het uploaden van bestanden, evenals de JSON-eindpunten voor het ophalen van informatie over uw omgeving. Deze console wordt aangeroepen Hallo *Kudu-Console* of Hallo *SCM Dashboard* voor uw web-app.

U kunt toegang krijgen tot dit dashboard toohello koppeling gaat **https://&lt;uw app-naam >.scm.azurewebsites.net/**.

Enkele van de Kudu verschaft Hallo zaken zijn:

* omgevingsinstellingen voor uw toepassing
* logboekstream
* diagnostische dump
* fouten opsporen console waarin u Powershell-cmdlets en basic DOS-opdrachten kunt uitvoeren.

Een andere handige functie van Kudu is dat, als uw toepassing die eerste kans uitzonderingen, kunt u Kudu en Hallo SysInternals-hulpprogramma Procdump toocreate geheugendumps. Deze geheugendumps momentopnamen van het Hallo-proces en vaak kunt u meer gecompliceerde problemen oplossen met uw web-app.

Zie voor meer informatie over functies die beschikbaar zijn in Kudu [Azure Websites Team Services-hulpprogramma's die u moet weten over](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).

<a name="mitigate" />

### <a name="3-mitigate-hello-issue"></a>3. Hallo probleem verhelpen
#### <a name="scale-hello-web-app"></a>Schaal Hallo web-app
In Azure App Service kunt voor betere prestaties en doorvoer, u aanpassen Hallo schaal waarmee u uw toepassing uitvoert. Schalen van een web-app omvat twee gerelateerde acties: uw App Service plan tooa hogere prijscategorie en bepaalde instellingen configureren nadat u hebt gekozen toohello hoger prijscategorie te wijzigen.

Zie voor meer informatie over het schalen [schalen van een web-app in Azure App Service](web-sites-scale.md).

U kunt bovendien kiezen toorun uw toepassing op meer dan één exemplaar. Uitschalen niet alleen biedt u meer verwerkingscapaciteit maar kunt u ook bepaalde hoeveelheid fouttolerantie. Als Hallo-proces uitgeschakeld op één exemplaar wordt, blijven hello andere exemplaren tooserve aanvragen.

U kunt Hallo toobe handmatig of automatisch schalen instellen.

#### <a name="use-autoheal"></a>Gebruik AutoHeal
AutoHeal wordt gerecycled werkproces Hallo voor uw app op basis van de instellingen die u kiest (zoals wijzigingen in de configuratie, aanvragen, op basis van geheugen limieten of Hallo tijd nodig tooexecute een aanvraag). Meestal Hallo is recyclen Hallo proces Hallo snelste manier toorecover van een probleem. Hoewel u altijd opnieuw Hallo web-app uit rechtstreeks in hello Azure-portal opstarten kunt, doet AutoHeal dit automatisch voor u. Toodo hoeft u sommige triggers in Hallo root web.config voor uw web-app toevoegen. Deze instellingen zijn werk gaat in Hallo dezelfde manier zelfs als uw toepassing niet een .net-app is.

Zie voor meer informatie [Azure websites automatisch herstel](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).

#### <a name="restart-hello-web-app"></a>Hallo-web-app starten
Opnieuw starten is vaak het eenvoudigste manier toorecover Hallo eenmalige problemen. Op Hallo [Azure-portal](https://portal.azure.com/), op de blade van uw web-app en u hebt Hallo opties toostop of opnieuw opstarten van uw app.

 ![opnieuw opstarten toosolve prestatieproblemen met de web-app](./media/app-service-web-troubleshoot-performance-degradation/2-restart.png)

U kunt ook uw web-app met Azure Powershell beheren. Zie [Azure PowerShell gebruiken met Azure Resource Manager](../powershell-azure-resource-manager.md) voor meer informatie.
