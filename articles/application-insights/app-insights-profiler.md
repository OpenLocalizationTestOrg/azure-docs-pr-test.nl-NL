---
title: Profileren van live web-apps in Azure met Application Insights | Microsoft Docs
description: Identificeer de hot pad in uw web server-code met een lage footprint profiler.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: bwren
ms.openlocfilehash: ff39f9a84b86c14859aaee50ee368643fb2848ea
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="profiling-live-azure-web-apps-with-application-insights"></a>Profileren van live Azure-web-apps met Application Insights

*Deze functie van Application Insights is NH voor App-Services en in preview voor Compute.*

Na hoeveel tijd is besteed aan elke methode in uw live-webtoepassing met het hulpprogramma profilering van weten [Azure Application Insights](app-insights-overview.md). Deze leest u gedetailleerde profielen van live-aanvragen die door uw app zijn behandeld en markeert de 'hot pad' die met behulp van de meeste tijd. Deze voorbeelden die u verschillende responstijden hebt automatisch geselecteerd. De profiler maakt gebruik van verschillende technieken overhead te minimaliseren.

De profiler werkt momenteel voor ASP.NET-web-apps uitgevoerd op Azure App Services in ten minste het Basic prijscategorie. 

<a id="installation"></a>
## <a name="enable-the-profiler"></a>De profiler inschakelen

[Installeer Application Insights-](app-insights-asp-net.md) in uw code. Als deze al geïnstalleerd, zorg er dan voor dat u de meest recente versie hebt. (U doet dit door met de rechtermuisknop op het project in Solution Explorer en kies beheren NuGet-pakketten. Selecteer Updates en alle updatepakketten.) Uw app opnieuw implementeren.

*Met behulp van ASP.NET Core? [Schakel dit selectievakje](#aspnetcore).*

In [https://portal.azure.com](https://portal.azure.com), opent u de Application Insights-resource voor uw web-app. Open **prestaties** en klik op **Profiler voor Application Insights inschakelen...** .

![Klik op de banner van de profiler inschakelen][enable-profiler-banner]

U kunt ook u kunt altijd op **configureren** als status wilt weergeven, inschakelen of uitschakelen van de Profiler.

![Klik op configureren in de blade Performance][performance-blade]

Web-apps die zijn geconfigureerd met Application Insights worden vermeld op de blade configureren. Volg de instructies voor het installeren van de agent Profiler indien nodig. Als er geen web-app is geconfigureerd met Application Insights nog, klikt u op *gekoppelde Apps toevoegen*.

Gebruik de *Profiler inschakelen* of *Profiler uitschakelen* knoppen in de blade configureren om te bepalen van de Profiler op alle gekoppelde Webapps.



![Blade configureren][linked app services]

Als u wilt stoppen of opnieuw starten van de profiler voor een afzonderlijke App Service-exemplaar, kijkt u **in de bron-App Service**in **webtaken**. Zoek wilt verwijderen, onder **extensies**.

![Profiler voor een webtaken uitschakelen][disable-profiler-webjob]

We raden u aan de Profiler die is ingeschakeld op alle web-apps voor het detecteren van eventuele prestatieproblemen zo snel mogelijk.

Als u Web Deploy te implementeren wijzigingen aan uw webtoepassing hebt gebruikt, zorg ervoor dat u deze uitsluiten van de **App_Data** map worden verwijderd tijdens de implementatie. Anders wordt worden de profiler extensiebestanden verwijderd wanneer u naast de webtoepassing naar Azure implementeert.

### <a name="using-profiler-with-azure-vms-and-compute-resources-preview"></a>Profiler gebruiken met Azure VM's en rekenresources (preview)

Wanneer u [Application Insights inschakelen voor Azure app services tijdens runtime](app-insights-azure-web-apps.md#run-time-instrumentation-with-application-insights), Profiler is automatisch beschikbaar. (Als u al Application Insights voor de resource hebt ingeschakeld, moet u mogelijk om bij te werken naar de laatste versie door de **configureren** wizard.)

Er is een [preview-versie van de Profiler voor Azure Compute-bronnen](https://go.microsoft.com/fwlink/?linkid=848155).


## <a name="limits"></a>Limieten

De bewaartermijn van de gegevens standaard is 5 dagen. Maximaal 10 GB per dag wordt ingenomen.

Er zijn geen kosten voor de profiler-service. Uw web-app moet worden gehost in ten minste de basisstaffel van App-Services.

## <a name="viewing-profiler-data"></a>Profiler gegevens bekijken

Open de blade Performance en blader naar de Bewerkingslijst.




![Application Insights-prestaties blade voorbeelden kolom][performance-blade-examples]

De kolommen in de tabel zijn:

* **Aantal** -het aantal van deze aanvragen in het tijdsbereik van de blade.
* **Mediaan** - typische duurt voordat uw app om te reageren op een aanvraag. De helft van alle antwoorden zijn sneller dan dit.
* **95e percentiel** 95% van de antwoorden sneller dan dit zijn. Als deze afbeelding heel verschillend van de mediaan is, is er mogelijk een onregelmatig probleem met uw app. (Of het kan worden verklaard door een ontwerpfunctie zoals opslaan in cache).
* **Voorbeelden** -een pictogram geeft aan dat de profiler stack-traces voor deze bewerking is vastgelegd.

Klik op het pictogram voorbeelden om de tracering explorer te openen. De explorer enkele voorbeelden ziet u dat de profiler is vastgelegd, geclassificeerd door reactietijd.

Selecteer een voorbeeld om weer te geven van een code-niveau verdeling van tijd besteed aan de aanvraag wordt uitgevoerd.

![Application Insights Trace Explorer][trace-explorer]

**Hot pad weergeven** wordt geopend de grootste blad knooppunt of ten minste iets sluit. In de meeste gevallen wordt dit knooppunt worden naast het prestatieknelpunt.



* **Label**: de naam van de functie of de gebeurtenis. De structuur bevat een mengeling van code en gebeurtenissen die hebben plaatsgevonden (zoals SQL- en HTTP-gebeurtenissen). De eerste gebeurtenis vertegenwoordigt de totale duur van de aanvraag.
* **Verstreken**: het tijdsinterval tussen het begin van de bewerking en het einde.
* **Wanneer**: bevat waarop de functie/gebeurtenis werd uitgevoerd in de relatie aan andere functies.

## <a name="how-to-read-performance-data"></a>Het lezen van prestatiegegevens

Profiler voor Microsoft-service gebruikt een combinatie van methode en instrumentatie voor het analyseren van de prestaties van uw toepassing.
Wanneer uitgebreide verzameling uitgevoerd wordt, voorbeelden serviceprofiler de instructie aanwijzer van elk van de machine CPU in elke milliseconde.
Elk voorbeeld wordt de volledige aanroepstack van de thread die momenteel wordt uitgevoerd, waarin gedetailleerde en nuttige informatie over wat u dat thread werd uitgevoerd op beide hoge en lage niveaus van abstractie vastgelegd. Profiler service verzamelt ook andere gebeurtenissen zoals context switch gebeurtenissen, TPL gebeurtenissen en threadgroep correlatie van activiteit en oorzakelijk verband bijhouden.

De aanroepstack wordt weergegeven in de tijdlijnweergave is het resultaat van de bovenstaande steekproeven en instrumentation. Omdat elk voorbeeld de volledige aanroepstack van de thread bevat, bevat de code van .NET framework, evenals andere frameworks die u verwijst.

### <a id="jitnewobj"></a>Object-toewijzing (`clr!JIT\_New or clr!JIT\_Newarr1`)
`clr!JIT\_New and clr!JIT\_Newarr1`Help-functies in .NET framework die wijst geheugen toe vanuit beheerde heap zijn. `clr!JIT\_New`wordt aangeroepen wanneer een object is toegewezen. `clr!JIT\_Newarr1`wordt aangeroepen wanneer een objectmatrix is toegewezen. Deze twee functies zijn meestal zeer snel en relatief klein hoeveelheid tijd moeten uitvoeren. Als u ziet `clr!JIT\_New` of `clr!JIT\_Newarr1` een aanzienlijke hoeveelheid tijd kosten in de tijdlijn, is het een indicatie dat de code kan worden veel objecten toewijzen en aanzienlijke hoeveelheid geheugen.

### <a id="theprestub"></a>Bij het laden van Code (`clr!ThePreStub`)
`clr!ThePreStub`is een Help-functie in .NET framework die de code uit te voeren voor de eerste keer wordt voorbereid. Dit doorgaans omvat, maar niet beperkt tot, (alleen In Time) JIT-compilatie. Voor elke methode C# `clr!ThePreStub` mag maximaal één keer tijdens de levensduur van een proces worden aangeroepen.

Als u ziet `clr!ThePreStub` neemt veel tijd voor een aanvraag, dit geeft aan dat aanvraag is de eerste die wordt uitgevoerd die methode en de tijd voor .NET framework runtime laden van deze methode aanzienlijk is. U kunt overwegen een opgewarmd-proces dat wordt uitgevoerd dat deel van de code voordat uw gebruikers toegang dit tot of overweeg NGen uitgevoerd op uw assembly's.

### <a id="lockcontention"></a>Aantal conflicten vergrendelen (`clr!JITutil\_MonContention` of `clr!JITutil\_MonEnterWorker`)
`clr!JITutil\_MonContention`of `clr!JITutil\_MonEnterWorker` geven aan de huidige thread wacht op een vergrendeling worden vrijgegeven. Dit doorgaans weergegeven bij het uitvoeren van een C# lock-instructie Monitor.Enter methode wordt aangeroepen of een methode met het kenmerk MethodImplOptions.Synchronized wordt aangeroepen. Vergrendelingsconflicten gebeurt meestal wanneer de thread A verkrijgt een vergrendeling en thread B probeert de vergrendeling te verkrijgen dezelfde voordat een thread is vrijgegeven.

### <a id="ngencold"></a>Bij het laden van code (`[COLD]`)
Als de naam van de methode bevat `[COLD]`, zoals `mscorlib.ni![COLD]System.Reflection.CustomAttribute.IsDefined`, betekent dit dat de .NET framework runtime is worden gebruikt voor het uitvoeren van code dat niet is geoptimaliseerd door <a href="https://msdn.microsoft.com/library/e7k32f4k.aspx">optimalisatie profiel begeleide</a> voor de eerste keer. Voor elke methode moet worden weergegeven van maximaal één keer tijdens de levensduur van het proces.

Als bij het laden van code aanzienlijke hoeveelheid tijd voor een aanvraag duurt, geeft u aan deze aanvraag is de eerste uit te voeren van het niet geoptimaliseerde gedeelte van de methode. U kunt een warme up proces dat wordt uitgevoerd dat deel van de code voordat uw gebruikers toegang krijgen het tot overwegen.

### <a id="httpclientsend"></a>HTTP-aanvraag verzenden
Methoden zoals `HttpClient.Send` geven de code wacht op een HTTP-verzoek om te voltooien.

### <a id="sqlcommand"></a>Databasebewerking
Methode zoals SqlCommand.Execute geeft dat de code wacht tot een databasebewerking te voltooien.

### <a id="await"></a>Wachten op (`AWAIT\_TIME`)
`AWAIT\_TIME`Hiermee geeft u dat de code wordt gewacht op een andere taak is voltooid. Dit gebeurt gewoonlijk met C# 'await' instructie. Wanneer de code een C# 'await', de thread wordt afgewikkeld en wordt de besturing aan de threadgroep en er is geen thread die wachten op de 'await' om te voltooien is geblokkeerd. Logisch wordt de thread die de wizard de await heeft echter 'geblokkeerd' wachten totdat de bewerking te voltooien. De `AWAIT\_TIME` geeft de tijd die het geblokkeerde wachten op de taak is voltooid.

### <a id="block"></a>Geblokkeerde tijd
`BLOCKED_TIME`Hiermee geeft u dat de code wordt gewacht op een andere bron beschikbaar, zoals het wachten op een synchronisatieobject wachten op een thread beschikbaar of wachten op een aanvraag te voltooien.

### <a id="cpu"></a>CPU-tijd
De CPU is bezig met uitvoeren van de instructies.

### <a id="disk"></a>Schijftijd
De toepassing uitvoert schijfbewerkingen.

### <a id="network"></a>Network Time
De toepassing met het uitvoeren van bewerkingen in het netwerk.

### <a id="when"></a>Wanneer kolom
Dit is een visualisatie van hoe de inclusief voorbeelden die worden verzameld voor een knooppunt gedurende een bepaalde periode variëren. Het totale bereik van de aanvraag is onderverdeeld in 32 tijd buckets en inclusief voorbeelden voor dat knooppunt in deze buckets 32 wordt geteld. Elke bucket wordt vervolgens weergegeven als een balk waarvan u de hoogte een uitgebreid waarde vertegenwoordigt. Voor knooppunten gemarkeerd `CPU_TIME` of `BLOCKED_TIME`, of wanneer er een duidelijke relatie van de consumptie van een resource (cpu, schijf, een thread), de balk staat voor een van deze resources voor de periode van die bucket verbruikt. Voor deze metrische gegevens krijgt u meer dan 100% door meerdere resources verbruikt. Bijvoorbeeld, als Gemiddeld u twee CPU's tijdens een interval van gebruiken krijgt vervolgens u 200%.


## <a id="troubleshooting"></a>Problemen oplossen

### <a name="how-can-i-know-whether-application-insights-profiler-is-running"></a>Hoe weet ik of Application Insights profiler wordt uitgevoerd?

De profiler wordt uitgevoerd als een taak continu web in Web-App. U kunt de Web-App-resource openen in https://portal.azure.com en controleer de status 'ApplicationInsightsProfiler' in de blade WebJobs. Als deze niet wordt uitgevoerd, opent u **logboeken** voor meer informatie.

### <a name="why-cant-i-find-any-stack-examples-even-though-the-profiler-is-running"></a>Waarom kan ik geen voorbeelden stack vinden ook al de profiler wordt uitgevoerd?

Hier volgen enkele dingen die u kunt controleren.

1. Zorg ervoor dat uw Web-App Service-Plan basisstaffel en hoger.
2. Zorg ervoor dat uw Web-App heeft Application Insights SDK 2.2 Beta en hierboven ingeschakeld.
3. Zorg ervoor dat uw Web-App is ingesteld op APPINSIGHTS_INSTRUMENTATIONKEY met dezelfde instrumentatiesleutel die wordt gebruikt door de Application Insights-SDK.
4. Zorg ervoor dat uw Web-App wordt uitgevoerd op .net Framework 4.6.
5. Als het een toepassing ASP.NET Core, Controleer ook of [de vereiste afhankelijkheden](#aspnetcore).

Nadat de profiler is gestart, is er een korte opgewarmd periode wanneer de profiler actief traceringen worden verzameld verschillende prestaties. Hierna is de profiler traceringen worden verzameld prestaties twee minuten in elk uur.  

### <a name="i-was-using-azure-service-profiler-what-happened-to-it"></a>Ik werd Azure Service Profiler gebruikt. Wat is er gebeurd met het?  

Wanneer u Application Insights Profiler inschakelt, is Azure Service Profiler agent uitgeschakeld.

### <a id="double-counting"></a>Dubbele parallelle threads tellen

In sommige gevallen is de totale tijd metrische gegevens in de stack-viewer hoger dan de werkelijke duur van de aanvraag.

Dit kan gebeuren wanneer er twee of meer threads die zijn gekoppeld aan een aanvraag, parallel uitgevoerd. De tijd van de totale thread is meer dan de verstreken tijd. In veel gevallen kan één thread worden wacht op de andere te voltooien. De viewer wil dit detecteren en laat de niet-interessante wachten, maar errs aan de kant van te veel in plaats van als weggelaten welke essentiële informatie kunnen worden weergegeven.  

Wanneer u parallelle threads in uw traceringen zien, moet u bepalen welke threads wachten zodat u het kritieke pad voor de aanvraag kunt zien. In de meeste gevallen is gewoon de thread die probeert het snel de status van een wait wacht op de andere threads. Richten op de andere en de tijd in de wachtende threads wordt genegeerd.

### <a id="issue-loading-trace-in-viewer"></a>Er is geen profileringsgegevens

1. Als de gegevens die u probeert weer te geven ouder dan een paar weken is, kunt u uw tijdfilter beperken en probeer het opnieuw.

2. Controleer dat proxy of firewall hebben geen toegang tot geblokkeerd https://gateway.azureserviceprofiler.net.

3. Controleer of de Application Insights-instrumentatiesleutel die u in uw app werkt hetzelfde als de Application Insights-resource die u hebt ingeschakeld met profilering. De sleutel bevindt zich doorgaans in ApplicationInsights.config, maar u kunt ook vinden in web.config of app.config.

### <a name="error-report-in-the-profiling-viewer"></a>Foutrapport in de viewer voor profielservices gegeven

Het bestand is een ondersteuningsticket vanuit de portal. Neem de correlatie-ID van het foutbericht.

## <a name="manual-installation"></a>Handmatige installatie

Wanneer u de profiler configureert, worden de volgende updates zijn aangebracht aan de Web-App-instellingen. U kunt ze zelf doen handmatig als uw omgeving, bijvoorbeeld, vereist als uw toepassing wordt uitgevoerd in Azure App Service omgeving (as-omgeving):

1. Open de instellingen in de blade web-app-beheer.
2. Stel '.Net Framework-versie ' naar 4.6.
3. Ingesteld 'Altijd aan' op.
4. App-instelling toevoegen '__APPINSIGHTS_INSTRUMENTATIONKEY__' en de waarde ingesteld op de dezelfde instrumentatiesleutel die wordt gebruikt door de SDK.
5. Open geavanceerde hulpprogramma's.
6. Klik op "Ga' naar de Kudu-website openen.
7. Selecteer in de website Kudu 'Site-uitbreidingen'.
8. Installeer '__Application Insights__' uit de galerie.
9. Start opnieuw op de web-app.

## <a id="aspnetcore"></a>ASP.NET Core-ondersteuning

ASP.NET Core toepassing moet installeren Microsoft.ApplicationInsights.AspNetCore Nuget-pakket 2.1.0-beta6 of hoger werken met de Profiler. We bieden geen ondersteuning voor de lagere versies na 27-6/2017.

## <a name="next-steps"></a>Volgende stappen

* [Met Application Insights werken in Visual Studio](https://docs.microsoft.com/azure/application-insights/app-insights-visual-studio)

[performance-blade]: ./media/app-insights-profiler/performance-blade.png
[performance-blade-examples]: ./media/app-insights-profiler/performance-blade-examples.png
[trace-explorer]: ./media/app-insights-profiler/trace-explorer.png
[trace-explorer-toolbar]: ./media/app-insights-profiler/trace-explorer-toolbar.png
[trace-explorer-hint-tip]: ./media/app-insights-profiler/trace-explorer-hint-tip.png
[trace-explorer-hot-path]: ./media/app-insights-profiler/trace-explorer-hot-path.png
[enable-profiler-banner]: ./media/app-insights-profiler/enable-profiler-banner.png
[disable-profiler-webjob]: ./media/app-insights-profiler/disable-profiler-webjob.png
[linked app services]: ./media/app-insights-profiler/linked-app-services.png
