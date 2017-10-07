---
title: aaaTroubleshooting geen gegevens - Application Insights voor .NET
description: Gegevens in Azure Application Insights niet zien? Probeer hier.
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: e231569f-1b38-48f8-a744-6329f41d91d3
ms.service: application-insights
ms.workload: mobile
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 261c25c89884c46e41bbc305474ac854360221ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-no-data---application-insights-for-net"></a>Problemen met ontbrekende gegevens oplossen - Application Insights voor .NET
## <a name="some-of-my-telemetry-is-missing"></a>Sommige van mijn telemetrie ontbreekt
*In Application Insights Zie ik slechts een deel van het Hallo-gebeurtenissen die worden gegenereerd door de app.*

* Als u consistent ziet Hallo dezelfde fractie, de waarschijnlijk vanwege tooadaptive [steekproeven](app-insights-sampling.md). tooconfirm, zoeken openen (van de blade overzicht Hallo) en zoek naar een exemplaar van een aanvraag of een andere gebeurtenis. Klik op '...' tooget volledige eigenschapdetails Hallo onderaan Hallo sectie met eigenschappen in. Als aanvragen Count > 1 en vervolgens steekproeven wordt uitgevoerd. 
* Anders is het mogelijk dat u bent kunt u door een [limiet](app-insights-pricing.md#limits-summary) voor uw prijscategorie. Deze beperkingen worden per minuut toegepast.

## <a name="no-data-from-my-server"></a>Er zijn geen gegevens van mijn server
*Ik mijn app hebt geïnstalleerd op de webserver en nu alle telemetrie van het niet wordt weergegeven. Deze OK op mijn computer Developer gewerkt.*

* Waarschijnlijk een firewallprobleem met. [Instellen van firewalluitzonderingen voor gegevens van Application Insights toosend](app-insights-ip-addresses.md).

*Ik [geïnstalleerd Status Monitor](app-insights-monitor-performance-live-website-now.md) op mijn web server toomonitor bestaande apps. Geen resultaten wordt niet weergegeven.*

* Zie [probleemoplossing statuscontrole](app-insights-monitor-performance-live-website-now.md#troubleshooting-runtime-configuration-of-application-insights). 

## <a name="q01"></a>Geen optie 'Application Insights toevoegen' in Visual Studio
*Wanneer ik een bestaand project in Solution Explorer met de rechtermuisknop, wordt geen Application Insights-opties niet weergegeven.*

* Niet alle soorten .NET project worden ondersteund door het Hallo-hulpprogramma's. Web- en WCF-projecten worden ondersteund. U kunt ook voor andere projecttypen zoals toepassingen voor desktop- of [handmatig toevoegen van een Application Insights-SDK-project tooyour](app-insights-windows-desktop.md).
* Zorg ervoor dat u hebt [Visual Studio 2013 Update 3 of hoger](http://go.microsoft.com/fwlink/?LinkId=397827). Het is voorgeïnstalleerd met ontwikkelaars hulpprogramma's voor webanalyse, waarmee Hallo Application Insights-SDK.
* Selecteer **extra**, **uitbreidingen en Updates** en controleert u of **Analytics hulpprogramma's voor ontwikkelaars** is geïnstalleerd en ingeschakeld. Als dit het geval is, klikt u op **Updates** toosee als er een update beschikbaar.
* Open het dialoogvenster Nieuw Project Hallo en kies van ASP.NET-webtoepassing. Als u ziet er Application Insights-optie Hallo vervolgens Hallo-hulpprogramma's zijn geïnstalleerd. Als dat niet het geval is, probeer te verwijderen en vervolgens opnieuw Hallo Application Insights Tools te installeren.

## <a name="q02"></a>Application Insights toevoegen is mislukt
*Wanneer ik probeer tooadd Application Insights tooan bestaand project, er een foutbericht weergegeven.*

Mogelijke oorzaken:

* Communicatie met de Hallo Application Insights-portal is mislukt; of
* Er is een probleem met uw Azure-account;
* U hoeft alleen [leestoegang toohello abonnement of de groep waar u toocreate Hallo nieuwe resource probeerde](app-insights-resources-roles-access-control.md).

FIX:

* Controleer of u aanmeldingsreferenties voor Hallo rechts Azure-account opgegeven. 
* In de browser, Controleer of u hebt toegang tot toohello [Azure-portal](https://portal.azure.com). Open instellingen en zien of er beperking.
* [Add Application Insights tooyour bestaand project](app-insights-asp-net.md): In Solution Explorer, klik met de rechtermuisknop op uw project en kies 'Application Insights toevoegen'.
* Als deze nog steeds niet werkt, voert u de Hallo [handmatige procedure](app-insights-windows-services.md) tooadd een resource in het Hallo-portal en voeg vervolgens Hallo SDK tooyour-project. 

## <a name="emptykey"></a>Een fout ophalen 'instrumentatiesleutel mag niet leeg zijn'
Lijkt erop dat is iets verkeerd gegaan tijdens de installatie Application Insights of mogelijk een adapter logboekregistratie.

Klik in Solution Explorer met de rechtermuisknop op uw project en kies **Application Insights > Application Insights configureren**. U krijgt een dialoogvenster met een uitnodiging toosign in tooAzure en maak een Application Insights-resource opnieuw of gebruik een bestaande.

## <a name="NuGetBuild"></a>"NuGet-pakketten ontbreken' op mijn buildserver
*Alles bouwt OK wanneer ik ben foutopsporing op de ontwikkelcomputer, maar er een NuGet-fout op Hallo build-server verschijnt.*

Zie [NuGet-pakket herstellen](http://docs.nuget.org/Consume/Package-Restore) en [automatische pakket herstellen](http://docs.nuget.org/Consume/package-restore/migrating-to-automatic-package-restore).

## <a name="missing-menu-command-tooopen-application-insights-from-visual-studio"></a>Ontbrekende menu opdracht tooopen Application Insights vanuit Visual Studio
*Wanneer ik mijn project Solution Explorer met de rechtermuisknop, zie ik geen Application Insights-opdrachten of een Open Application Insights-opdracht niet weergegeven.*

Mogelijke oorzaken:

* Als u handmatig Hallo Application Insights-resource gemaakt of als Hallo project van een type dat niet wordt ondersteund door Hallo Application Insights-hulpprogramma's.
* Hallo-hulpprogramma's voor ontwikkelaars Analytics zijn uitgeschakeld in uw Visual Studio. 
* Uw Visual Studio is ouder dan 2013 Update 3.

FIX:

* Zorg ervoor dat uw versie van Visual Studio 2013 update 3 of hoger.
* Selecteer **extra**, **uitbreidingen en Updates** en controleert u of **hulpprogramma's voor ontwikkelaars webanalyse** is geïnstalleerd en ingeschakeld. Als dit het geval is, klikt u op **Updates** toosee als er een update beschikbaar.
* Met de rechtermuisknop op het project in Solution Explorer. Als u de opdracht Hallo ziet **Application Insights > Application Insights configureren**, tooconnect gebruiken uw toohello projectresource in Hallo Application Insights-service.

Anders dat het projecttype van uw direct wordt niet ondersteund door Hallo Application Insights-hulpprogramma's. toosee uw telemetrie, aanmelden toohello [Azure-portal](https://portal.azure.com), Application Insights kiezen op de linkernavigatiebalk Hallo en selecteert u uw toepassing.

## <a name="access-denied-on-opening-application-insights-from-visual-studio"></a>'Toegang geweigerd' Application Insights wordt geopend vanuit Visual Studio
*de menuopdracht 'Open Application Insights' Hello, ga ik toohello Azure-portal, maar ophalen van een 'toegang geweigerd'-fout.*

![](./media/app-insights-asp-net-troubleshoot-no-data/access-denied.png)

Hallo Microsoft aanmelden die het laatst op de standaardbrowser gebruikte heeft geen toegang te[resource die is gemaakt bij de Application Insights is toegevoegd toothis app Hallo](app-insights-asp-net.md). Er zijn twee waarschijnlijke oorzaken: 

* Hebt u meer dan een Microsoft-account - mogelijk een werk- en een persoonlijk Microsoft-account? Hallo aanmelding die het laatst op de standaardbrowser gebruikte is voor een ander account dan Hallo die toegang te heeft[Application Insights toohello project toevoegen](app-insights-asp-net.md). 
  
  * FIX: Klik op de naam van uw op bovenste rechts van het browservenster Hallo en meld u af. Meld u aan met van Hallo-account dat toegang heeft. Klik vervolgens op Hallo linkernavigatiebalk op Application Insights en selecteer uw app.
* Iemand anders Application Insights toohello project toegevoegd en ze toogive vergeten u [toegang toohello resourcegroep](app-insights-resources-roles-access-control.md) waarin deze is gemaakt. 
  
  * FIX: Als ze een organisatie-account gebruikt, kunnen ze toevoegen u toohello team; of kunnen ze u afzonderlijke toohello resourcegroep toegang verlenen.

## <a name="asset-not-found-on-opening-application-insights-from-visual-studio"></a>'Asset niet gevonden' Application Insights wordt geopend vanuit Visual Studio
*de menuopdracht 'Open Application Insights' Hello, ga ik toohello Azure-portal, maar verschijnt het foutbericht 'asset niet gevonden'.*

Mogelijke oorzaken:

* Hallo Application Insights-resource voor de toepassing is verwijderd; of
* Hallo-instrumentatiesleutel is ingesteld of gewijzigd in ApplicationInsights.config door direct bewerken zonder bij te werken Hallo projectbestand. 

Hallo instrumentatiesleutel in ApplicationInsights.config besturingselementen waarbij Hallo telemetrie wordt verzonden. Een regel in het projectbestand Hallo bepaalt welke resource wordt geopend wanneer u Hallo-opdracht in Visual Studio gebruiken. 

FIX:

* Klik in Solution Explorer met de rechtermuisknop op het Hallo-project en kies Application Insights, Application Insights configureren. In het dialoogvenster hello, klikt u toosend telemetrie tooan bestaande bron kiezen of een nieuwe maken. Of:
* Resource-Hallo rechtstreeks openen. Aanmelden te[hello Azure-portal](https://portal.azure.com)Application Insights op de linkernavigatiebalk Hallo op en selecteer vervolgens uw app.

## <a name="where-do-i-find-my-telemetry"></a>Waar vind ik mijn telemetrie?
*Ik heb ondertekend in toohello [Microsoft Azure-portal](https://portal.azure.com), en ik ben hello Azure Startdashboard kijken. Dus waar vind ik mijn gegevens Application Insights?*

* Klik op Hallo linkernavigatiebalk Application Insights, klikt u vervolgens de naam van uw app. Als u geen projecten er hebt, moet u deze te[toevoegen of configureren van Application Insights in uw webproject](app-insights-asp-net.md).
  
    U ziet er sommige samenvatting grafieken. U kunt doorklikken ze toosee meer informatie.
* In Visual Studio, terwijl u fouten uw app opspoort, klikt u op de knop Application Insights Hallo.

## <a name="q03"></a>Er is geen server-gegevens (of geen gegevens op alle)
*Ik heb mijn app wordt uitgevoerd en vervolgens geopend Hallo Application Insights-service in Microsoft Azure, maar alle grafieken weergeven Hallo ' leren hoe toocollect...' of 'Niet geconfigureerd'.* Of, *alleen paginaweergave-en gebruikersgegevens, maar er zijn geen servergegevens.*

* Voer uw toepassing in de foutopsporingsmodus in Visual Studio (F5). Gebruik de toepassing hello dus als toogenerate telemetrie. Controleer of u gebeurtenissen vastgelegd in het venster voor Hallo Visual Studio kunt zien. 
  
    ![](./media/app-insights-asp-net-troubleshoot-no-data/output-window.png)
* Open in de Application Insights-portal Hallo [diagnostische gegevens doorzoeken](app-insights-diagnostic-search.md). Gegevens weergegeven meestal hier eerst.
* Klik op de knop Vernieuwen Hallo. Hallo-blade automatisch wordt vernieuwd periodiek, maar u kunt ook dit handmatig doen. Hallo-interval voor vernieuwen is verlengd voor grotere tijdsbereik.
* Controleer Hallo instrumentatiesleutels overeenkomen. Op de hoofdblade Hallo voor uw app in Hallo Application Insights-portal in Hallo **Essentials** vervolgkeuzelijst, kijkt u naar **instrumentatiesleutel**. In het project in Visual Studio, open vervolgens ApplicationInsights.config en Hallo zoeken `<instrumentationkey>`. Controleer of er twee sleutels Hallo gelijk zijn. Als dat niet het:
  
  * In Hallo-portal op Application Insights en zoek Hallo app resource met de juiste sleutel Hallo; of
  * In Visual Studio Solution Explorer met de rechtermuisknop op het Hallo-project en kies Application Insights configureren. Opnieuw instellen Hallo app toosend telemetrie toohello juiste resource.
  * Als u Hallo die overeenkomt met de sleutels niet kunt vinden, Controleer of u dezelfde Hallo aanmeldingsreferenties in Visual Studio als toohello portal in.
    
    ![](./media/app-insights-asp-net-troubleshoot-no-data/ikey-check.png)
* In Hallo [Microsoft Azure-Startdashboard](https://portal.azure.com), bekijkt hello servicestatus kaart. Als er een waarschuwing aanwijzingen zijn, wacht u totdat ze zijn tooOK geretourneerd en vervolgens sluiten en opnieuw de blade van het Application Insights-toepassing openen.
* Controleer ook [ons blog status](http://blogs.msdn.com/b/applicationinsights-status/).
* Hebt u een code te schrijven voor Hallo [serverzijde SDK](app-insights-api-custom-events-metrics.md) die kan worden gewijzigd Hallo instrumentatiesleutel in `TelemetryClient` exemplaren of in `TelemetryContext`? Of hebt u schrijft een [filter of steekproeven configuratie](app-insights-api-filtering-sampling.md) die het filter worden mogelijk te veel?
* Als u ApplicationInsights.config hebt bewerkt, Controleer zorgvuldig Hallo configuratie van [TelemetryInitializers en TelemetryProcessors](app-insights-api-filtering-sampling.md). Een verkeerde naam type of de parameter kan leiden tot Hallo SDK toosend geen gegevens.

## <a name="q04"></a>Er zijn geen gegevens over het gebruik van de Browsers, paginaweergaven
*Gegevens in serverreactietijd en serveraanvragen grafieken, maar er zijn geen gegevens in de laadtijd van pagina weergeven of weergegeven in de Browser Hallo of gebruik blades.*

Hallo gegevens afkomstig van scripts in Hallo webpagina's. 

* Als u Application Insights tooan-webproject bestaande toegevoegd [u tooadd Hallo scripts handmatig hebt](app-insights-javascript.md).
* Controleer of dat Internet Explorer uw site wordt niet weergegeven in de compatibiliteitsmodus.
* Gebruik van de browser Hallo foutopsporing functie (F12 op sommige browsers, kies netwerk) tooverify die gegevens te worden verzonden`dc.services.visualstudio.com`.

## <a name="no-dependency-or-exception-data"></a>Er zijn geen gegevens afhankelijkheid of uitzondering
Zie [afhankelijkheidstelemetrie](app-insights-asp-net-dependencies.md) en [uitzonderingstelemetrie](app-insights-asp-net-exceptions.md).

## <a name="no-performance-data"></a>Er is geen prestatiegegevens
Prestatiegegevens (CPU, i/o-snelheid, enzovoort) beschikbaar is voor [Java-web-services](app-insights-java-collectd.md), [Windows desktop-apps](app-insights-windows-desktop.md), [IIS web-apps en services als u de statusmonitor installeren](app-insights-monitor-performance-live-website-now.md), en [Azure-Cloudservices](app-insights-azure.md). u vindt deze onder instellingen voor Servers.

Het is niet beschikbaar voor Azure websites.

## <a name="no-server-data-since-i-published-hello-app-toomy-server"></a>Er zijn geen gegevens (server) sinds de publicatie van de appserver toomy Hallo
* Controleer of u daadwerkelijk alle Hallo Microsoft gekopieerd. DLL's ApplicationInsights toohello server samen met Microsoft.Diagnostics.Instrumentation.Extensions.Intercept.dll
* In de firewall, moet u wellicht te[enkele TCP-poorten](app-insights-ip-addresses.md#data-access-api).
* Als u een proxy-toosend toouse buiten uw bedrijfsnetwerk hebt, stelt u [defaultProxy](https://msdn.microsoft.com/library/aa903360.aspx) in Web.config
* WindowsServer 2008: Zorg ervoor dat u Hallo na updates hebt geïnstalleerd: [KB2468871](https://support.microsoft.com/kb/2468871), [KB2533523](https://support.microsoft.com/kb/2533523), [KB2600217](https://support.microsoft.com/kb/2600217).

## <a name="i-used-toosee-data-but-it-has-stopped"></a>Ik toosee gegevens gebruikt, maar deze is gestopt
* Controleer de Hallo [status blog](http://blogs.msdn.com/b/applicationinsights-status/).
* Hebt u uw maandelijkse quotum van gegevenspunten bereikt? Open Hallo-instellingen/quotum en prijzen toofind uit. Als dit het geval is, kunt u uw abonnement upgraden of betalen voor extra capaciteit. Zie Hallo [prijzen schema](https://azure.microsoft.com/pricing/details/application-insights/).

## <a name="i-dont-see-all-hello-data-im-expecting"></a>Alle Hallo gegevens die ik ben verwacht wordt niet weergegeven
Als uw toepassing grote hoeveelheden gegevens verzendt en u hello Application Insights-SDK voor ASP.NET-versie 2.0.0-beta3 of later Hallo [adaptieve steekproeven](app-insights-sampling.md) functie kan werken en slechts een percentage van uw telemetrie verzenden. 

U kunt deze uitschakelen, maar dit wordt niet aanbevolen. Steekproeven is zodanig ontworpen dat gerelateerde telemetrie correct wordt verzonden, voor diagnostische doeleinden. 

## <a name="wrong-geographical-data-in-user-telemetry"></a>Onjuiste geografische gegevens in de telemetrie van de gebruiker
Hallo stad, regio en land-dimensies zijn afgeleid van IP-adressen en niet altijd nauwkeurig.

## <a name="exception-method-not-found-on-running-in-azure-cloud-services"></a>Uitzondering Methode niet gevonden bij het uitvoeren van uw app in Azure Cloud Services
Hebt u uw app ontwikkeld voor .NET 4.6? 4.6 wordt niet automatisch ondersteund in Azure Cloud Services-rollen. [Installeer 4.6 voor elke rol](../cloud-services/cloud-services-dotnet-install-dotnet.md) voordat u uw app uitvoert.

## <a name="still-not-working"></a>Nog steeds werkt niet...
* [Application Insights-forum](https://social.msdn.microsoft.com/Forums/vstudio/en-US/home?forum=ApplicationInsights)

