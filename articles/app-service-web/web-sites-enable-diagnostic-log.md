---
title: aaaEnable Diagnostische logboekregistratie voor web-apps in Azure App Service
description: Meer informatie over hoe tooenable Diagnostische logboekregistratie en instrumentation tooyour-toepassing toevoegen, evenals hoe tooaccess Hallo informatie die wordt geregistreerd door Azure.
services: app-service
documentationcenter: .net
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: c9da27b2-47d4-4c33-a3cb-1819955ee43b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2016
ms.author: cephalin
ms.openlocfilehash: 4b2903ff31cc93180552cf51196c33505ffbaf07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-diagnostics-logging-for-web-apps-in-azure-app-service"></a>Logboekregistratie van diagnostische gegevens van web-apps in Azure App Service
## <a name="overview"></a>Overzicht
Azure biedt ingebouwde diagnostics tooassist met foutopsporing een [App Service-web-app](http://go.microsoft.com/fwlink/?LinkId=529714). In dit artikel leert u hoe diagnostische logboekregistratie tooenable en instrumentation tooyour-toepassing toevoegen, evenals hoe tooaccess Hallo informatie die wordt geregistreerd door Azure.

Dit artikel wordt Hallo [Azure Portal](https://portal.azure.com), Azure PowerShell en hello Azure-opdrachtregelinterface (Azure CLI) toowork met diagnostische logboeken. Zie voor meer informatie over het werken met Logboeken met diagnostische gegevens met Visual Studio [probleemoplossing voor Azure in Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="whatisdiag"></a>Web server diagnostics en application diagnostics
App Service-web-apps bieden diagnostische functionaliteit voor logboekinformatie van zowel Hallo-webserver en Hallo-webtoepassing. Deze logisch zijn verdeeld in **web server diagnostische** en **application diagnostics**.

### <a name="web-server-diagnostics"></a>Web server diagnostische gegevens
U kunt in- of uitschakelen van Hallo soorten logboeken te volgen:

* **Gedetailleerde fout logboekregistratie** -gedetailleerde informatie over de fout voor HTTP-statuscodes die wijzen op mislukte (statuscode 400 of hoger). Dit kan bevatten informatie om te bepalen waarom Hallo server Hallo foutcode geretourneerd.
* **Kan geen aanvraag voor het traceren** -gedetailleerde informatie over de mislukte aanvragen, met inbegrip van een tracering van Hallo IIS componenten gebruikt tooprocess Hallo aanvraag en Hallo-tijd benodigd in elk onderdeel. Dit is handig als u de siteprestaties tooincrease probeert of isoleren wat de oorzaak van een specifieke HTTP-fout toobe geretourneerd.
* **Web Server-logboekregistratie** -informatie over HTTP transacties met Hallo [uitgebreide W3C-logboekbestandsindeling](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx). Dit is handig bij het bepalen van de algemene site metrische gegevens zoals het aantal aanvragen dat is verwerkt Hallo of hoeveel aanvragen van een specifiek IP-adres.

### <a name="application-diagnostics"></a>Application diagnostics
Application diagnostics kunt u toocapture informatie die wordt geproduceerd door een webtoepassing. ASP.NET-toepassingen kunnen gebruikmaken van Hallo [System.Diagnostics.Trace](http://msdn.microsoft.com/library/36hhw2t6.aspx) klasse toolog informatie toohello application diagnostics melden. Bijvoorbeeld:

    System.Diagnostics.Trace.TraceError("If you're seeing this, something bad happened");

U kunt deze logboeken toohelp bij het oplossen van ophalen tijdens runtime. Zie voor meer informatie [probleemoplossing voor Azure-web-apps in Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md).

App Service WebApps zich ook aanmelden voor informatie over de implementatie, wanneer u inhoud tooa web-app publiceert. Dit gebeurt automatisch en er zijn geen configuratieinstellingen voor logboekregistratie in een implementatie. Logboekregistratie van de implementatie kunt u toodetermine waarom een implementatie is mislukt. Bijvoorbeeld, als u een aangepaste implementatiescript gebruikt, kunt u implementatie logboekregistratie toodetermine waarom Hallo-script is mislukt.

## <a name="enablediag"></a>Hoe diagnostische gegevens tooenable
tooenable diagnostische gegevens in Hallo [Azure Portal](https://portal.azure.com)Ga toohello blade voor uw web-app en klik **instellingen > diagnostische logboeken**.

<!-- todo:cleanup dogfood addresses in screenshot -->
![Logboeken-onderdeel](./media/web-sites-enable-diagnostic-log/logspart.png)

Wanneer u het inschakelen van **application diagnostics** u er ook voor kiezen Hallo **niveau**. Deze instelling kunt u toofilter Hallo informatie te vastgelegd**informatief**, **waarschuwing** of **fout** informatie. Te stellen**uitgebreide** wordt alle informatie die wordt geproduceerd door de toepassing hello aangemeld.

> [!NOTE]
> In tegenstelling tot het wijzigen van Hallo web.config maakt-bestand, Application diagnostics inschakelen of wijzigen van diagnostische logboekniveaus niet recyclen van toepassingsdomein Hallo die Hallo toepassing wordt uitgevoerd in.
>
>

In Hallo [klassieke portal](https://manage.windowsazure.com) Web-app **configureren** tabblad kunt u **opslag** of **bestandssysteem** voor **webserver logboekregistratie**. Selecteren **opslag** kunt u tooselect een opslagaccount en een blob-container Hallo Logboeken om te worden geschreven. Alle logboeken voor **diagnostics site** toohello bestandssysteem alleen worden geschreven.

Hallo [klassieke portal](https://manage.windowsazure.com) Web-app **configureren** tabblad heeft ook aanvullende instellingen voor application diagnostics:

* **Bestandssysteem** -stores Hallo application diagnostics informatie toohello web-app-bestandssysteem. Deze bestanden worden geopend door FTP of gedownload als een Zip-archief met behulp van hello Azure PowerShell of Azure-opdrachtregelinterface (Azure CLI).
* **Table storage** -stores Hallo toepassing diagnostische gegevens in het Hallo opgegeven Azure Storage-Account en tabel.
* **BLOB-opslag** -stores Hallo toepassing diagnostische gegevens in Hallo opgegeven Azure Storage-Account en de blob-container.
* **Bewaarperiode** -standaard logboeken worden niet automatisch verwijderd uit **blobopslag**. Selecteer **bewaarperiode instellen** en voer het aantal dagen tookeep logboeken desgewenst tooautomatically Logboeken verwijderen Hallo.

> [!NOTE]
> Als u [toegangssleutels voor uw opslagaccount opnieuw genereren](../storage/common/storage-create-storage-account.md), moet u Hallo respectieve logboekregistratie toouse Hallo bijgewerkt configuratiesleutels opnieuw instellen. toodo dit:
>
> 1. In Hallo **configureren** tabblad, stelt u de respectieve logboekfunctie hello te**uit**. Sla de instelling.
> 2. Logboekregistratie toohello storage-account blob of de tabel opnieuw inschakelen. Sla de instelling.
>
>

Een combinatie van het bestandssysteem, table storage of blob-opslag kan worden ingeschakeld op Hallo dezelfde tijdstip en afzonderlijk logboek-niveau configuraties hebben. Bijvoorbeeld, kunt u desgewenst toolog fouten en waarschuwingen tooblob opslag als lange termijn logboekregistratie oplossing tijdens het inschakelen van logboekregistratie in systeem met een uitgebreide machtigingsniveau.

Terwijl alle drie opslaglocaties Hallo bieden dezelfde algemene informatie voor de vastgelegde gebeurtenissen **tabel opslag** en **blobopslag** Meld u aanvullende informatie zoals Hallo exemplaar-ID, thread-ID en een meer gedetailleerde tijdstempel (maatstreepjes-indeling) dan de logboekregistratie te**bestandssysteem**.

> [!NOTE]
> Gegevens die zijn opgeslagen **tabel opslag** of **blobopslag** alleen toegankelijk is met een opslag-client of een toepassing die rechtstreeks met deze opslagsystemen kunt werken. Bijvoorbeeld, Visual Studio 2013 bevat een Opslagverkenner die gebruikt tooexplore tabel of blob storage worden kunnen en HDInsight toegang tot de gegevens die zijn opgeslagen in blob storage. U kunt ook een toepassing die toegang heeft tot Azure Storage met behulp van een Hallo schrijven [Azure SDK's](/downloads/#).
>
> [!NOTE]
> Diagnostische gegevens kunnen ook worden ingeschakeld vanuit Azure PowerShell Hallo met **Set AzureWebsite** cmdlet. Als u Azure PowerShell nog niet hebt geïnstalleerd of niet hebt geconfigureerd deze toouse uw Azure-abonnement, Zie [hoe tooUse Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/).
>
>

## <a name="download"></a>Hoe: Logboeken downloaden
Diagnostische gegevens opgeslagen toohello web-app-bestandssysteem zijn toegankelijk rechtstreeks met FTP. Het kan ook worden gedownload als een Zip-archief met Azure PowerShell of hello Azure-opdrachtregelinterface.

Hallo-mapstructuur die Hallo logboeken worden opgeslagen in is als volgt:

* **Toepassingslogboeken** -/LogFiles/toepassing /. Deze map bevat een of meer tekstbestanden met informatie die wordt geproduceerd door logboekregistratie van toepassingen.
* **Kan aanvraag traceringen** -logboekbestanden/W3SVC ### /. Deze map bevat een XSL-bestand en een of meer XML-bestanden. Zorg ervoor dat u in dezelfde map als XML bestand(en) omdat Hallo XSL-bestand functionaliteit biedt voor opmaak en filteren Hallo inhoud van XML Hallo Hallo bestand(en) ziet er in Internet Explorer Hallo Hallo XSL-bestand downloaden.
* **Gedetailleerde foutenlogboeken** -/LogFiles/DetailedErrors /. Deze map bevat een of meer htm-bestanden met uitgebreide informatie voor een HTTP-fouten dat is opgetreden.
* **Web Server-logboeken** -/LogFiles/http/RawLogs. Deze map bevat een of meer tekstbestanden die zijn geformatteerd met Hallo [uitgebreide W3C-logboekbestandsindeling](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).
* **Implementatielogboeken** -logboekbestanden/Git. Deze map bevat de logboeken die worden gegenereerd door Hallo interne implementatieprocessen die wordt gebruikt door de Azure-web-apps, evenals de logboeken voor Git-implementaties.

### <a name="ftp"></a>FTP
tooaccess diagnostische gegevens met behulp van FTP bezoek Hallo **Dashboard** van uw web-app in Hallo [klassieke portal](https://manage.windowsazure.com). In Hallo **snelle weergave** sectie, gebruikt u Hallo **FTP-logboeken met diagnostische gegevens** tooaccess Hallo-logboekbestanden met FTP koppelen. Hallo **implementatie/FTP-gebruiker** vermelding Hallo-gebruikersnaam die gebruikt tooaccess Hallo FTP-site worden moet bevat.

> [!NOTE]
> Als hello **implementatie/FTP-gebruiker** vermelding niet is ingesteld, of u Hallo wachtwoord voor deze gebruiker bent vergeten, kunt u een nieuwe gebruiker en een wachtwoord met behulp van Hallo **opnieuw instellen van referenties voor implementatie** koppeling in Hallo **snelle weergave** sectie Hallo **Dashboard**.
>
>

### <a name="download-with-azure-powershell"></a>Met Azure PowerShell downloaden
toodownload Hallo-logboekbestanden, start een nieuw exemplaar van Azure PowerShell en Hallo volgende opdracht gebruiken:

    Save-AzureWebSiteLog -Name webappname

Dit bespaart Hallo-logboeken voor Hallo web-app is opgegeven door Hallo **-naam** tooa parameterbestand met de naam **logs.zip** in de huidige map Hallo.

> [!NOTE]
> Als u Azure PowerShell nog niet hebt geïnstalleerd of niet hebt geconfigureerd deze toouse uw Azure-abonnement, Zie [hoe tooUse Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/).
>
>

### <a name="download-with-azure-command-line-interface"></a>Met Azure-opdrachtregelinterface downloaden
Hallo-logboekbestanden voor de toodownload met hello Azure-opdrachtregelinterface, opent u een nieuwe opdrachtprompt, PowerShell, Bash of terminalsessie en Voer Hallo volgende opdracht:

    azure site log download webappname

Dit bespaart Hallo-logboeken voor Hallo web-app met de naam 'webappname' tooa bestand met de naam **diagnostics.zip** in de huidige map Hallo.

> [!NOTE]
> Als u niet hebt geïnstalleerd hello Azure-opdrachtregelinterface (Azure CLI) of niet hebt geconfigureerd deze toouse uw Azure-abonnement, Zie [hoe tooUse Azure CLI](../cli-install-nodejs.md).
>
>

## <a name="how-to-view-logs-in-application-insights"></a>Hoe: weergave wordt geregistreerd in Application Insights
Visual Studio Application Insights biedt hulpprogramma's voor het filteren en zoeken naar Logboeken en voor het Hallo-logboeken correleren met aanvragen en andere gebeurtenissen.

1. Hallo Application Insights-SDK tooyour project toevoegen in Visual Studio.
   * Klik in Solution Explorer, klik met de rechtermuisknop op uw project en kies Application Insights toevoegen. U wordt nu door de stappen die bestaan uit het maken van een Application Insights-resource. [Meer informatie](../application-insights/app-insights-asp-net.md)
2. Hallo traceringslistener pakket tooyour project toevoegen.
   * Klik met de rechtermuisknop op uw project en kies NuGet-pakketten beheren. Selecteer `Microsoft.ApplicationInsights.TraceListener` [meer informatie](../application-insights/app-insights-asp-net-trace-logs.md)
3. Uploaden van uw project en voer dit toogenerate logboekgegevens.
4. In Hallo [Azure Portal](https://portal.azure.com/), tooyour nieuwe Application Insights-resource bladeren en open **Search**. Hier ziet u de logboekgegevens, samen met de aanvraag, het gebruik en andere telemetrie. Telemetrie duurt een paar minuten tooarrive: klik op vernieuwen. [Meer informatie](../application-insights/app-insights-diagnostic-search.md)

[Meer informatie over prestaties bijhouden met Application Insights](../application-insights/app-insights-azure-web-apps.md)

## <a name="streamlogs"></a>Hoe: Logboeken Stream
Tijdens het ontwikkelen van een toepassing, is het vaak nuttig toosee logboekinformatie in near-realtime. Dit kunt u doen door logboekregistratie informatie tooyour ontwikkelomgeving met behulp van Azure PowerShell of Azure-opdrachtregelinterface Hallo streaming.

> [!NOTE]
> Bepaalde typen logboekregistratie buffer schrijven toohello logboekbestand, wat tot volgorde gebeurtenissen in Hallo stroom leiden kan. Een logboekvermelding toepassing die deze gebeurtenis treedt op wanneer een gebruiker een pagina bezoekt kan bijvoorbeeld worden weergegeven in Hallo stroom voordat Hallo bijbehorende HTTP logboekvermelding voor Hallo-pagina-aanvraag.
>
> [!NOTE]
> Streaming-logboek wordt geschreven tooany tekstbestand opgeslagen in Hallo informatie ook stream **D:\\thuis\\logboekbestanden\\**  map.
>
>

### <a name="streaming-with-azure-powershell"></a>Streamen met Azure PowerShell
toostream logboekinformatie, start een nieuw exemplaar van Azure PowerShell en Hallo volgende opdracht gebruiken:

    Get-AzureWebSiteLog -Name webappname -Tail

Dit wordt toohello web-app is opgegeven door Hallo verbinden **-naam** parameter en wilt beginnen met streaming informatie toohello PowerShell-venster als logboekgebeurtenissen op Hallo web-app optreden. Alle gegevens die zijn geschreven toofiles eindigt op .txt, .log of .htm die zijn opgeslagen in Hallo /LogFiles directory (home-d:/logboekbestanden) wordt gestreamd toohello lokale console.

toofilter specifieke gebeurtenissen, zoals fouten, gebruik Hallo **-bericht** parameter. Bijvoorbeeld:

    Get-AzureWebSiteLog -Name webappname -Tail -Message Error

toofilter specifieke logboek typen, zoals HTTP, gebruik Hallo **-pad** parameter. Bijvoorbeeld:

    Get-AzureWebSiteLog -Name webappname -Tail -Path http

een lijst met beschikbare paden, gebruik Hallo - ListPath parameter toosee.

> [!NOTE]
> Als u Azure PowerShell nog niet hebt geïnstalleerd of niet hebt geconfigureerd deze toouse uw Azure-abonnement, Zie [hoe tooUse Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/).
>
>

### <a name="streaming-with-azure-command-line-interface"></a>Streamen met Azure-opdrachtregelinterface
toostream logboekinformatie, opent u een nieuwe opdrachtprompt, PowerShell, Bash of terminalsessie en voert u Hallo volgende opdracht:

    azure site log tail webappname

Dit wordt toohello web-app met de naam 'webappname' verbinden en streaming toohello informatievenster als logboekgebeurtenissen op Hallo web-app optreden begint. Alle gegevens die zijn geschreven toofiles eindigt op .txt, .log of .htm die zijn opgeslagen in Hallo /LogFiles directory (home-d:/logboekbestanden) wordt gestreamd toohello lokale console.

toofilter specifieke gebeurtenissen, zoals fouten, gebruik Hallo **--Filter** parameter. Bijvoorbeeld:

    azure site log tail webappname --filter Error

toofilter specifieke logboek typen, zoals HTTP, gebruik Hallo **--pad** parameter. Bijvoorbeeld:

    azure site log tail webappname --path http

> [!NOTE]
> Als u niet hebt geïnstalleerd hello Azure-opdrachtregelinterface of niet hebt geconfigureerd deze toouse uw Azure-abonnement, Zie [hoe Azure-opdrachtregelinterface tooUse](../cli-install-nodejs.md).
>
>

## <a name="understandlogs"></a>Hoe: inzicht in Logboeken met diagnostische gegevens
### <a name="application-diagnostics-logs"></a>Diagnostische logboeken
Application diagnostics wordt informatie opgeslagen in een specifieke indeling voor .NET-toepassingen, afhankelijk van of u Logboeken toohello bestandssysteem, tabelopslag, opslaan of blob-opslag. Hallo basisset van opgeslagen gegevens is dezelfde Hallo alle drie typen in de opslag - Hallo datum en tijd Hallo gebeurtenis heeft plaatsgevonden, Hallo proces-ID die geproduceerd Hallo gebeurtenis, gebeurtenistype hello (informatie, waarschuwing, fout) en gebeurtenis het Hallo-bericht.

**Bestandssysteem**

Elke regel geregistreerde toohello bestandssysteem of ontvangen met streaming niet in Hallo volgende indeling:

    {Date}  PID[{process id}] {event type/level} {message}

Een foutgebeurtenis zou bijvoorbeeld vergelijkbare toohello volgende weergegeven:

    2014-01-30T16:36:59  PID[3096] Error       Fatal error on hello page!

Logboekregistratie toohello bestandssysteem biedt Hallo meest elementaire informatie van Hallo drie beschikbare methoden bieden alleen Hallo tijd, proces-id, gebeurtenisniveau en bericht.

**Table Storage**

Tijdens de registratie van tootable opslag zijn aanvullende eigenschappen gebruikte toofacilitate Hallo-gegevens die zijn opgeslagen in de tabel hello, evenals meer gedetailleerde informatie over het Hallo-gebeurtenis zoeken. Hallo worden volgende eigenschappen (kolommen) gebruikt voor elke entiteit (rij) opgeslagen in de tabel Hallo.

| De naam van eigenschap | Waarde/indeling |
| --- | --- |
| PartitionKey |Datum/tijd van de gebeurtenis Hallo yyyyMMddHH-indeling |
| RowKey |Een GUID-waarde die is uniek voor deze entiteit |
| tijdstempel |Hallo-datum en tijd waarop Hallo gebeurtenis is opgetreden |
| EventTickCount |Hallo-datum en tijd waarop de gebeurtenis Hallo opgetreden, in de indeling van de maatstreepjes (nauwkeuriger) |
| ApplicationName |Hallo web-appnaam |
| Niveau |Gebeurtenisniveau (bijvoorbeeld fout, waarschuwing, informatie) |
| Gebeurtenis-id |Hallo-gebeurtenis-ID van deze gebeurtenis<p><p>Standaard too0 indien niet opgegeven |
| Exemplaar-id |Er is een exemplaar van Hallo web-app die zelfs Hallo opgetreden op |
| PID |Proces-ID |
| TID |Hallo thread-ID van Hallo thread die Hallo gebeurtenis geproduceerd |
| Bericht |Detail gebeurtenisbericht |

**Blob Storage**

Tijdens de registratie van tooblob opslag worden gegevens worden opgeslagen in de indeling met door komma's gescheiden waarden (CSV). Vergelijkbare tootable opslag, aanvullende velden zijn geregistreerde tooprovide gedetailleerdere informatie over het Hallo-gebeurtenis. Hallo worden volgende eigenschappen gebruikt voor elke rij in Hallo CSV:

| De naam van eigenschap | Waarde/indeling |
| --- | --- |
| Date |Hallo-datum en tijd waarop Hallo gebeurtenis is opgetreden |
| Niveau |Gebeurtenisniveau (bijvoorbeeld fout, waarschuwing, informatie) |
| ApplicationName |Hallo web-appnaam |
| Exemplaar-id |Er is een exemplaar van Hallo web-app die gebeurtenis Hallo opgetreden op |
| EventTickCount |Hallo-datum en tijd waarop de gebeurtenis Hallo opgetreden, in de indeling van de maatstreepjes (nauwkeuriger) |
| Gebeurtenis-id |Hallo-gebeurtenis-ID van deze gebeurtenis<p><p>Standaard too0 indien niet opgegeven |
| PID |Proces-ID |
| TID |Hallo thread-ID van Hallo thread die Hallo gebeurtenis geproduceerd |
| Bericht |Detail gebeurtenisbericht |

Hallo-gegevens die zijn opgeslagen in een blob eruit vergelijkbare toohello volgende:

    date,level,applicationName,instanceId,eventTickCount,eventId,pid,tid,message
    2014-01-30T16:36:52,Error,mywebapp,6ee38a,635266966128818593,0,3096,9,An error occurred

> [!NOTE]
> de eerste regel Hallo van Hallo logboek bevat kolomkoppen Hallo zoals wordt weergegeven in dit voorbeeld.
>
>

### <a name="failed-request-traces"></a>Aanvraag traceringen is mislukt
Traceringen van mislukte aanvragen zijn opgeslagen in XML-bestanden met de naam **fr ### .xml**. toomake deze eenvoudiger tooview Hallo geregistreerd informatie, een XSL-opmaakmodel met de naam **freb.xsl** wordt verstrekt in Hallo dezelfde map zoals Hallo XML-bestanden. Hallo XSL-opmaakmodel tooprovide weergegeven in een opgemaakt Hallo traceringsinformatie maakt gebruik van een Hallo XML-bestanden te openen in Internet Explorer. Deze wordt vergelijkbare toohello volgende weergegeven:

![mislukte aanvragen in de browser Hallo weergegeven](./media/web-sites-enable-diagnostic-log/tws-failedrequestinbrowser.png)

### <a name="detailed-error-logs"></a>Gedetailleerde foutenlogboeken
Gedetailleerde foutenlogboeken zijn HTML-documenten met meer gedetailleerde informatie over HTTP-fouten dat is opgetreden. Aangezien ze gewoon HTML-documenten, kunnen ze worden weergegeven met een webbrowser.

### <a name="web-server-logs"></a>Web server-Logboeken
Hallo webserverlogboeken zijn geformatteerd met Hallo [uitgebreide W3C-logboekbestandsindeling](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx). Deze informatie kan worden gelezen met een teksteditor of met behulp van de hulpprogramma's zoals geparseerd [Log Parser](http://go.microsoft.com/fwlink/?LinkId=246619).

> [!NOTE]
> Hallo logboeken die wordt geproduceerd door de Azure-web-apps bieden geen ondersteuning voor Hallo **s-computername**, **s-IP-**, of **cs-version** velden.
>
>

## <a name="nextsteps"></a> Volgende stappen
* [Hoe tooMonitor Web-Apps](http://docs.microsoft.com/en-us/azure/app-service-web/web-sites-monitor)
* [Het Azure-web-apps in Visual Studio oplossen](web-sites-dotnet-troubleshoot-visual-studio.md)
* [Analyseren web-Applogboeken in HDInsight](http://gallery.technet.microsoft.com/scriptcenter/Analyses-Windows-Azure-web-0b27d413)

> [!NOTE]
> Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen.
>
>

## <a name="whats-changed"></a>Wat is er gewijzigd
* Zie voor een handleiding toohello wijzigingen van de Websites tooApp Service: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)
* Zie voor een handleiding toohello wijziging van Hallo oude portal toohello nieuwe portal: [verwijzing voor het navigeren hello Azure-portal](http://go.microsoft.com/fwlink/?LinkId=529715)
