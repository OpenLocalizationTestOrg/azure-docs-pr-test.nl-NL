---
title: aaaApplication prestaties Veelgestelde vragen voor Azure-web-apps | Microsoft Docs
description: Toofrequently van antwoorden op veelgestelde vragen over de beschikbaarheid, prestaties en problemen met toepassingen in de functie voor Hallo-Web-Apps van Azure App Service worden opgehaald.
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 7f2383743079e4c630fd548b0efd9993029afe11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="application-performance-faqs-for-web-apps-in-azure"></a>Toepassingsprestaties Veelgestelde vragen voor Web-Apps in Azure

In dit artikel bevat antwoorden toofrequently Veelgestelde vragen (FAQ's) over toepassing prestatieproblemen voor Hallo [functie van Azure App Service Web Apps](https://azure.microsoft.com/services/app-service/web/).

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-is-my-app-slow"></a>Waarom wordt mijn trage app?

Meerdere factoren zou tooslow appprestaties. Zie voor gedetailleerde stappen voor probleemoplossing, [problemen met trage web appprestaties](app-service-web-troubleshoot-performance-degradation.md).

## <a name="how-do-i-troubleshoot-a-high-cpu-consumption-scenario"></a>Hoe kan ik een hoog CPU-verbruik scenario oplossen?

Uw app kunnen in sommige gevallen hoog CPU-verbruik echt vereist meer bronnen. Overweeg in dat geval tooa hogere servicelaag schalen zodat Hallo toepassing krijgt alle Hallo-resources die nodig is. Andere keren kan hoog CPU-verbruik worden veroorzaakt door een onjuiste lus of door de code uit veiligheidsoverwegingen. Om inzicht te krijgen in wat meer CPU-verbruik wordt activering is een tweedelige-proces. Eerst een Procesdump maken en vervolgens analyseren Hallo-dump verwerken. Zie voor meer informatie [vastleggen en analyseren van een dumpbestand voor hoog CPU-verbruik voor Web-Apps](https://blogs.msdn.microsoft.com/asiatech/2016/01/20/how-to-capture-dump-when-intermittent-high-cpu-happens-on-azure-web-app/).

## <a name="how-do-i-troubleshoot-a-high-memory-consumption-scenario"></a>Hoe kan ik een scenario hoog geheugengebruik oplossen?

Uw app kunnen in sommige gevallen hoog geheugengebruik echt vereist meer bronnen. Overweeg in dat geval tooa hogere servicelaag schalen zodat Hallo toepassing krijgt alle Hallo-resources die nodig is. Andere tijden kan een bug in Hallo code een geheugenlek veroorzaken. Code uit veiligheidsoverwegingen mogelijk ook geheugenverbruik verhogen. Om inzicht te krijgen in wat wordt activering van veel geheugen verbruik bestaat uit twee fasen. Eerst een Procesdump maken en vervolgens analyseren Hallo-dump verwerken. Crash Diagnoser van Hallo galerie van Azure Site-uitbreiding kunt efficiënt beide deze stappen uitvoeren. Zie voor meer informatie [vastleggen en analyseren van een dumpbestand voor onregelmatige veel geheugen voor Web-Apps](https://blogs.msdn.microsoft.com/asiatech/2016/02/02/how-to-capture-and-analyze-dump-for-intermittent-high-memory-on-azure-web-app/).

## <a name="how-do-i-automate-app-service-web-apps-by-using-powershell"></a>Hoe ik App Service-web-apps met behulp van PowerShell automatiseren?

U kunt de PowerShell-cmdlets toomanage gebruiken en onderhouden van App Service-web-apps. In onze blogbericht [web-apps die worden gehost in Azure App Service met behulp van PowerShell automatiseren](https://blogs.msdn.microsoft.com/puneetgupta/2016/03/21/automating-webapps-hosted-in-azure-app-service-through-powershell-arm-way/), we beschrijven hoe toouse op basis van Azure Resource Manager PowerShell-cmdlets tooautomate algemene taken. Hallo blogbericht heeft ook een voorbeeld van code voor verschillende beheertaken voor web-apps. Zie voor beschrijvingen en de syntaxis voor alle cmdlets van App Service web apps [AzureRM.Websites](https://docs.microsoft.com/powershell/module/azurerm.websites/?view=azurermps-4.0.0).

## <a name="how-do-i-view-my-web-apps-event-logs"></a>Hoe kan ik mijn web-app-gebeurtenislogboeken bekijken?

tooview uw web-app gebeurtenislogboeken:

1. Meld u aan tooyour [Kudu website](https://*yourwebsitename*.scm.azurewebsites.net).
2. Selecteer in het menu Hallo **Console voor foutopsporing** > **CMD**.
3. Selecteer Hallo **logboekbestanden** map.
4. gebeurtenislogboeken tooview, selecteer Hallo potloodpictogram naast te**eventlog.xml**.
5. toodownload hello Logboeken, voer de PowerShell-cmdlet Hallo `Save-AzureWebSiteLog -Name webappname`.

## <a name="how-do-i-capture-a-user-mode-memory-dump-of-my-web-app"></a>Hoe ik een geheugendump gebruikersmodus van mijn web-app vastleggen?

een geheugendump gebruikersmodus van uw web-app toocapture:

1. Meld u aan tooyour [Kudu website](https://*yourwebsitename*.scm.azurewebsites.net).
2. Selecteer Hallo **Procesverkenner** menu.
3. Klik met de rechtermuisknop Hallo **w3wp.exe** proces of de webtaak wordt uitgevoerd.
4. Selecteer **geheugendump downloaden** > **Dump volledige**.

## <a name="how-do-i-view-process-level-info-for-my-web-app"></a>Hoe kan ik voor mijn web-app procesniveau info bekijken?

U hebt twee opties voor het weergeven van procesniveau informatie voor uw web-app:

*   In hello Azure-portal:
    1. Open Hallo **Procesverkenner** voor Hallo web-app.
    2. toosee hello details, selecteer Hallo **w3wp.exe** proces.
*   In Hallo Kudu-console:
    1. Meld u aan tooyour [Kudu website](https://*yourwebsitename*.scm.azurewebsites.net).
    2. Selecteer Hallo **Procesverkenner** menu.
    3. Voor Hallo **w3wp.exe** proces, selecteer **eigenschappen**.

## <a name="when-i-browse-toomy-app-i-see-error-403---this-web-app-is-stopped-how-do-i-resolve-this"></a>Als ik toomy app bladert, zie ik "Fout 403 - deze web-app is gestopt." Hoe kan ik dit oplossen?

Drie voorwaarden kunnen leiden tot deze fout:

* Hallo-web-app een facturering limiet heeft bereikt en uw site is uitgeschakeld.
* Hallo-web-app is in de portal Hallo gestopt.
* Hallo-web-app heeft een resource quotumlimiet die mogelijk van toepassing tooa Free of Shared scale service-abonnement bereikt.

toosee veroorzaakt Hallo fout en tooresolve Hallo probleem, volg Hallo stappen in [Web-Apps: 'Fout 403 – deze web-app is gestopt'](https://blogs.msdn.microsoft.com/waws/2016/01/05/azure-web-apps-error-403-this-web-app-is-stopped/).

## <a name="where-can-i-learn-more-about-quotas-and-limits-for-various-app-service-plans"></a>Waar vind ik meer informatie over quota en limieten voor verschillende App Service-abonnementen?

Zie voor meer informatie over quota en limieten [App Service-beperkingen](../azure-subscription-service-limits.md#app-service-limits). 

## <a name="how-do-i-decrease-hello-response-time-for-hello-first-request-after-idle-time"></a>Hoe ik Hallo reactietijd voor de eerste aanvraag Hallo na niet-actieve tijd verkleinen?

Standaard worden web-apps uit het geheugen verwijderd als ze inactief gedurende een bepaalde tijd zijn. Op deze manier Hallo-systeem kunt besparen. Hallo nadeel is hello antwoord toohello eerste aanvraag nadat Hallo web-app verwijderd wordt, is langer, tooallow Hallo tooload voor web-app en start afhandeling van reacties. In de service-abonnementen, Basic en Standard, kunt u schakelen op Hallo **altijd op** instelling tookeep Hallo app altijd geladen. Hierdoor langer laadtijden nadat Hallo app actief is. Hallo toochange **altijd op** instelling:

1. Ga in de Azure-portal hello, tooyour web-app.
2. Selecteer **toepassingsinstellingen**.
3. Voor **altijd op**, selecteer **op**.

## <a name="how-do-i-turned-on-failed-request-tracing"></a>Hoe ik tracering van mislukte aanvragen ingeschakeld?

tooturn op de tracering van mislukte aanvragen:

1. Ga in de Azure-portal hello, tooyour web-app.
3. Selecteer **alle instellingen** > **diagnostische logboeken**.
4. Voor **tracering van mislukte aanvragen**, selecteer **op**.
5. Selecteer **Opslaan**.
6. Selecteer op Hallo blade web-app **extra**.
7. Selecteer **Visual Studio Online**.
8. Als de instelling Hallo niet **op**, selecteer **op**.
9. Selecteer **gaat**.
10. Selecteer **Web.config**.
11. In system.webServer, voegt u deze configuratie (toocapture een specifieke URL):

    ```
    <system.webServer>
    <tracing> <traceFailedRequests>
    <remove path="*api*" />
    <add path="*api*">
    <traceAreas>
    <add provider="ASP" verbosity="Verbose" />
    <add provider="ASPNET" areas="Infrastructure,Module,Page,AppServices" verbosity="Verbose" />
    <add provider="ISAPI Extension" verbosity="Verbose" />
    <add provider="WWW Server" areas="Authentication,Security,Filter,StaticFile,CGI,Compression, Cache,RequestNotifications,Module,FastCGI" verbosity="Verbose" />
    </traceAreas>
    <failureDefinitions statusCodes="200-999" />
    </add> </traceFailedRequests>
    </tracing>
    ```
12. Deze configuratie toevoegen tootroubleshoot trage prestaties problemen (als Hallo vastleggen van de aanvraag duurt langer dan 30 seconden):
    ```
    <system.webServer>
    <tracing> <traceFailedRequests>
    <remove path="*" />
    <add path="*">
    <traceAreas> <add provider="ASP" verbosity="Verbose" />
    <add provider="ASPNET" areas="Infrastructure,Module,Page,AppServices" verbosity="Verbose" />
    <add provider="ISAPI Extension" verbosity="Verbose" />
    <add provider="WWW Server" areas="Authentication,Security,Filter,StaticFile,CGI,Compression, Cache,RequestNotifications,Module,FastCGI" verbosity="Verbose" />
    </traceAreas>
    <failureDefinitions timeTaken="00:00:30" statusCodes="200-999" />
    </add> </traceFailedRequests>
    </tracing>
    ```
13. Hallo toodownload is mislukt voor aanvraag traceringen, in Hallo [portal](https://portal.azure.com), gaat u tooyour website.
15. Selecteer **extra** > **Kudu** > **gaat**.
18. Selecteer in het menu Hallo **Console voor foutopsporing** > **CMD**.
19. Selecteer Hallo **logboekbestanden** map en selecteer vervolgens Hallo-map met een naam die met begint **W3SVC**.
20. toosee hello XML-bestand, selecteer Hallo potloodpictogram.

## <a name="i-see-hello-message-worker-process-requested-recycle-due-toopercent-memory-limit-how-do-i-address-this-issue"></a>Zie ik het Hallo-bericht ' werkproces recyclebewerking aangevraagd vanwege too'Percent geheugen ' limiet. " Hoe ik dit probleem op te lossen?

Hallo maximaal beschikbare hoeveelheid geheugen voor een 32-bits proces (zelfs op een 64-bits besturingssysteem) is 2 GB. Standaard is het werkproces Hallo too32-bits in App Service (voor compatibiliteit met oudere webtoepassingen) ingesteld.

Overweeg het gebruik too64-bits processen zodat u van extra geheugen Hallo beschikbaar in uw Web-werkrol profiteren kunt. Dit activeert een web-app opnieuw starten, dus plannen dienovereenkomstig.

Let ook op een 64-bits-omgeving hebt u een Basic- of Standard service-abonnement nodig. Gratis en plannen van gedeelde altijd uitgevoerd in een 32-bits-omgeving.

Zie voor meer informatie [configureren van web-apps in App Service](https://docs.microsoft.com/azure/app-service-web/web-sites-configure).

## <a name="why-does-my-request-time-out-after-240-seconds"></a>Waarom wordt mijn time-out aanvraag na 240 seconden?

Azure Load Balancer heeft een time-out voor inactiviteit standaardinstelling van vier minuten. Doorgaans is dit een redelijke antwoord tijdslimiet voor een webaanvraag. Als uw web-app achtergrondverwerking vereist, wordt u aangeraden Azure WebJobs. Hello Azure-web-app kunt aanroepen WebJobs en een melding krijgen wanneer achtergrondverwerking is voltooid. U kunt kiezen uit meerdere methoden voor het gebruik van WebJobs, met inbegrip van wachtrijen en triggers.

WebJobs is ontworpen voor de achtergrond wordt verwerkt. U kunt doen zoveel achtergrond verwerkt als u in een webtaak wilt. Zie voor meer informatie over WebJobs [achtergrondtaken uitvoeren met WebJobs](https://docs.microsoft.com/azure/app-service-web/web-sites-create-web-jobs).

## <a name="aspnet-core-applications-that-are-hosted-in-app-service-sometimes-stop-responding-how-do-i-fix-this-issue"></a>ASP.NET Core toepassingen die worden gehost in App Service soms reageert. Hoe kan ik dit probleem oplossen?

Een bekend probleem met een eerdere [Kestrel versie](https://github.com/aspnet/KestrelHttpServer/issues/1182) kan ertoe leiden dat een ASP.NET Core 1.0-app die wordt gehost in App Service toointermittently reageert. Ook ziet u dit bericht: "hello opgegeven CGI-toepassing heeft een fout en Hallo beëindigd Hallo serverproces aangetroffen."

Dit probleem is opgelost in Kestrel versie 1.0.2. Deze versie is opgenomen in Hallo ASP.NET Core 1.0.3 update. tooresolve dit probleem, zorg ervoor dat u uw app-afhankelijkheden toouse Kestrel 1.0.2 bijwerken. U kunt ook kunt u een van twee oplossingen die worden beschreven in het blogbericht Hallo [trage prestaties van ASP.NET Core 1.0 problemen in App Service WebApps](https://blogs.msdn.microsoft.com/waws/2016/12/11/asp-net-core-slow-perf-issues-on-azure-websites).


## <a name="i-cant-find-my-log-files-in-hello-file-structure-of-my-web-app-how-can-i-find-them"></a>Ik kan mijn logboekbestanden in de bestandsstructuur Hallo van mijn web-app niet vinden. Hoe kan ik ze vinden?

Als u Hallo lokale cachefunctie van App Service gebruikt, zijn de mapstructuur Hallo Hallo logboekbestanden en gegevensmappen voor uw App Service-exemplaar worden beïnvloed. Wanneer lokale Cache wordt gebruikt, worden de submappen gemaakt in Hallo opslag, logboekbestanden en mappen. Hallo submappen gebruik Hallo naming patroon 'unieke id' + tijdstempel. Elke submap komt overeen tooa VM-instantie in welke Hallo web-app wordt uitgevoerd of is uitgevoerd.

ongeacht of u lokale Cache, Controleer uw App Service toodetermine **toepassingsinstellingen** tabblad. Als de lokale Cache wordt gebruikt, app-instelling Hallo `WEBSITE_LOCAL_CACHE_OPTION` te is ingesteld`Always`. Zie voor meer informatie over de lokale Cache Hallo [lokale App Service-Cache-overzicht](https://docs.microsoft.com/azure/app-service/app-service-local-cache).

Als u geen van lokale Cache gebruikmaakt en dit probleem zich voordoet, indienen ondersteuning aan te vragen.

## <a name="i-see-hello-message-an-attempt-was-made-tooaccess-a-socket-in-a-way-forbidden-by-its-access-permissions-how-do-i-resolve-this"></a>Zie ik het Hallo-bericht ' is een poging gedaan tooaccess een socket op een manier is niet toegestaan volgens de toegangsmachtigingen. " Hoe kan ik dit oplossen?

Deze fout treedt meestal op als uitgaande TCP-verbindingen op de VM-instantie Hallo Hallo zijn uitgeput. In App Service gelden limieten voor Hallo kunt u het maximum aantal uitgaande verbindingen die kunnen worden gemaakt voor elke VM-instantie. Zie voor meer informatie [Cross-VM numerieke limieten](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox#cross-vm-numerical-limits).

Deze fout kan ook optreden als u een lokaal adres tooaccess van uw toepassing probeert. Zie voor meer informatie [aanvragen van lokaal adres](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox#local-address-requests).

Zie voor meer informatie over uitgaande verbindingen in uw web-app Hallo blogbericht over [uitgaande verbindingen tooAzure websites](http://www.freekpaans.nl/2015/08/starving-outgoing-connections-on-windows-azure-web-sites/).

## <a name="how-do-i-use-visual-studio-tooremote-debug-my-app-service-web-app"></a>Hoe gebruik ik foutopsporing van Visual Studio tooremote mijn App Service-web-app?

Voor een gedetailleerd overzicht waarin wordt getoond hoe toodebug uw web-app met behulp van Visual Studio, Zie [afstand fouten opsporen in uw App Service-web-app](https://blogs.msdn.microsoft.com/benjaminperkins/2016/09/22/remote-debug-your-azure-app-service-web-app/).
