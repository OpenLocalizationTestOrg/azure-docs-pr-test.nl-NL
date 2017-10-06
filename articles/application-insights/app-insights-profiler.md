---
title: aaaProfiling live web-apps in Azure met Application Insights | Microsoft Docs
description: Hallo hot pad in uw servercode web identificeren met een lage footprint profiler.
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
ms.openlocfilehash: 3c7f21076f19335e0f006327932e13623ec9526b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="profiling-live-azure-web-apps-with-application-insights"></a>Profileren van live Azure-web-apps met Application Insights

*Deze functie van Application Insights is NH voor App-Services en in preview voor Compute.*

Na hoeveel tijd is besteed aan elke methode in uw live-webtoepassing met behulp van hulpprogramma profilering Hallo weten [Azure Application Insights](app-insights-overview.md). U gedetailleerde profielen van live-aanvragen die zijn geleverd door uw app worden weergegeven, en licht Hallo 'hot pad' Hallo meeste tijd is gebruikt. Deze voorbeelden die u verschillende responstijden hebt automatisch geselecteerd. Hallo profiler maakt gebruik van verschillende technieken toominimize overhead.

Hallo profiler momenteel werkt voor ASP.NET-web-apps die worden uitgevoerd op Azure App Services in ten minste Hallo Basic prijscategorie. 

<a id="installation"></a>
## <a name="enable-hello-profiler"></a>Hallo profiler inschakelen

[Installeer Application Insights-](app-insights-asp-net.md) in uw code. Als deze al geïnstalleerd, zorg er dan voor dat u beschikt over de nieuwste versie Hallo. (toodo dit door met de rechtermuisknop op het project in Solution Explorer en kies beheren NuGet-pakketten. Selecteer Updates en alle updatepakketten.) Uw app opnieuw implementeren.

*Met behulp van ASP.NET Core? [Schakel dit selectievakje](#aspnetcore).*

In [https://portal.azure.com](https://portal.azure.com), Hallo Application Insights-resource voor uw web-app openen. Open **prestaties** en klik op **Profiler voor Application Insights inschakelen...** .

![Klik op Hallo profiler banner inschakelen][enable-profiler-banner]

U kunt ook u kunt altijd op **configureren** tooview status, inschakelen of uitschakelen van Hallo Profiler.

![In de blade Performance hello, klikt u op configureren][performance-blade]

Web-apps die zijn geconfigureerd met Application Insights worden vermeld op de blade configureren. Volg de instructies tooinstall Hallo Profiler agent indien nodig. Als er geen web-app is geconfigureerd met Application Insights nog, klikt u op *gekoppelde Apps toevoegen*.

Gebruik Hallo *Profiler inschakelen* of *Profiler uitschakelen* knoppen in Hallo configureren blade toocontrol Hallo Profiler op alle gekoppelde Webapps.



![Blade configureren][linked app services]

toostop of opnieuw opstarten Hallo profiler voor een afzonderlijke App Service-exemplaar, kijkt u **in App Service-resource Hallo**in **webtaken**. toodelete ervan, kijk onder **extensies**.

![Profiler voor een webtaken uitschakelen][disable-profiler-webjob]

We raden u aan Hallo Profiler ingeschakeld op alle uw web-apps toodiscover eventuele prestatieproblemen met zo snel mogelijk.

Als u Web Deploy toodeploy wijzigingen tooyour-webtoepassing hebt gebruikt, zorg ervoor dat u deze uitsluiten van Hallo **App_Data** map worden verwijderd tijdens de implementatie. Anders worden hello profiler extensiebestanden verwijderd wanneer u naast Hallo web application tooAzure implementeert.

### <a name="using-profiler-with-azure-vms-and-compute-resources-preview"></a>Profiler gebruiken met Azure VM's en rekenresources (preview)

Wanneer u [Application Insights inschakelen voor Azure app services tijdens runtime](app-insights-azure-web-apps.md#run-time-instrumentation-with-application-insights), Profiler is automatisch beschikbaar. (Als u al Application Insights voor Hallo resource hebt ingeschakeld, moet u mogelijk tooupdate toohello laatste versie via Hallo **configureren** wizard.)

Er is een [preview-versie van Hallo Profiler voor Azure Compute-bronnen](https://go.microsoft.com/fwlink/?linkid=848155).


## <a name="limits"></a>Limieten

bewaren van gegevens van Hallo standaard is 5 dagen. Maximaal 10 GB per dag wordt ingenomen.

Er zijn geen kosten voor Hallo profiler service. Uw web-app moet worden gehost in ten minste Hallo basisstaffel van App-Services.

## <a name="viewing-profiler-data"></a>Profiler gegevens bekijken

Open de blade Performance Hallo en schuif omlaag in de Bewerkingslijst toohello.




![Application Insights-prestaties blade voorbeelden kolom][performance-blade-examples]

Hallo-kolommen in tabel Hallo zijn:

* **Aantal** -nummer van deze aanvragen in het tijdsbereik Hallo van Hallo blade Hallo.
* **Mediaan** -Hallo typische duurt voordat uw app toorespond tooa aanvraag. De helft van alle antwoorden zijn sneller dan dit.
* **95e percentiel** 95% van de antwoorden sneller dan dit zijn. Als deze afbeelding heel verschillend van Hallo mediaan is, is er mogelijk een onregelmatig probleem met uw app. (Of het kan worden verklaard door een ontwerpfunctie zoals opslaan in cache).
* **Voorbeelden** -een pictogram geeft aan dat profiler Hallo stack-traces voor deze bewerking is vastgelegd.

Klik op Hallo voorbeelden pictogram tooopen Hallo trace explorer. Hallo explorer geeft enkele voorbeelden die Hallo profiler is vastgelegd, geclassificeerd door reactietijd.

Selecteer een voorbeeld tooshow een code-niveau verdeling van tijd besteed aan het uitvoerende Hallo-aanvraag.

![Application Insights Trace Explorer][trace-explorer]

**Hot pad weergeven** wordt geopend Hallo grootste leaf-knooppunt of ten minste iets sluit. In de meeste gevallen is dit knooppunt aangrenzende tooa prestatieknelpunt.



* **Label**: Hallo-naam van de functie Hallo of gebeurtenis. Hallo-structuur bevat een mengeling van code en gebeurtenissen die hebben plaatsgevonden (zoals SQL- en HTTP-gebeurtenissen). Hallo bovenste gebeurtenis geeft Hallo totale duur van aanvraag.
* **Verstreken**: Hallo tijdsinterval tussen Hallo Hallo-bewerking is gestart en Hallo-end.
* **Wanneer**: ziet u wanneer Hallo functie/gebeurtenis werd uitgevoerd in de relatie tooother functies.

## <a name="how-tooread-performance-data"></a>Hoe tooread prestatiegegevens

Profiler voor Microsoft-service gebruikt een combinatie van de steekproef nemen methode en instrumentation tooanalyze Hallo-prestaties van uw toepassing.
Wanneer uitgebreide verzameling uitgevoerd wordt, Hallo service profiler voorbeelden instructie aanwijzer van elk van de machine Hallo CPU in elke milliseconde.
Elke steekproef vastgelegd Hallo volledige aanroepstack van Hallo thread momenteel wordt uitgevoerd, waarin gedetailleerde en nuttige informatie over wat u dat thread werd uitgevoerd op beide hoge en lage niveaus van abstractie. Profiler service verzamelt ook andere gebeurtenissen zoals context switch gebeurtenissen, TPL gebeurtenissen, en threadgroep gebeurtenissen tootrack activiteit correlatie en oorzakelijk verband.

Hallo aanroepstack wordt weergegeven in de tijdlijnweergave Hallo is Hallo resultaat Hallo boven steekproeven en instrumentation. Omdat elk voorbeeld vastgelegd Hallo volledige aanroepstack van Hallo thread, bevat de code van Hallo .NET framework, evenals andere frameworks die u verwijst.

### <a id="jitnewobj"></a>Object-toewijzing (`clr!JIT\_New or clr!JIT\_Newarr1`)
`clr!JIT\_New and clr!JIT\_Newarr1`Help-functies in .NET framework die wijst geheugen toe vanuit beheerde heap zijn. `clr!JIT\_New`wordt aangeroepen wanneer een object is toegewezen. `clr!JIT\_Newarr1`wordt aangeroepen wanneer een objectmatrix is toegewezen. Deze twee functies zijn meestal zeer snel en relatief klein hoeveelheid tijd moeten uitvoeren. Als u ziet `clr!JIT\_New` of `clr!JIT\_Newarr1` een aanzienlijke hoeveelheid tijd kosten in de tijdlijn, is het een indicatie dat Hallo code kan worden veel objecten toewijzen en aanzienlijke hoeveelheid geheugen.

### <a id="theprestub"></a>Bij het laden van Code (`clr!ThePreStub`)
`clr!ThePreStub`is een Help-functie in .NET framework die wordt voorbereid Hallo code tooexecute voor Hallo eerst. Dit doorgaans omvat, maar niet beperkt tot, (alleen In Time) JIT-compilatie. Voor elke methode C# `clr!ThePreStub` mag maximaal één keer tijdens de levensduur van een proces Hallo worden aangeroepen.

Als u ziet `clr!ThePreStub` neemt veel tijd voor een aanvraag, betekent dit dat die aanvraag Hallo eerste één die wordt uitgevoerd die methode en het Hallo-tijd voor .NET framework runtime tooload methode is belangrijk. U kunt overwegen een opgewarmd-proces dat wordt uitgevoerd dat deel van het Hallo-code voordat uw gebruikers toegang dit tot of overweeg NGen uitgevoerd op uw assembly's.

### <a id="lockcontention"></a>Aantal conflicten vergrendelen (`clr!JITutil\_MonContention` of `clr!JITutil\_MonEnterWorker`)
`clr!JITutil\_MonContention`of `clr!JITutil\_MonEnterWorker` geven aan de huidige thread Hallo wacht op een vergrendeling toobe uitgebracht. Dit doorgaans weergegeven bij het uitvoeren van een C# lock-instructie Monitor.Enter methode wordt aangeroepen of een methode met het kenmerk MethodImplOptions.Synchronized wordt aangeroepen. Vergrendelingsconflicten gebeurt meestal wanneer de thread A verkrijgt een vergrendeling en thread B probeert tooacquire Hallo dezelfde vergrendelen voordat een thread is vrijgegeven.

### <a id="ngencold"></a>Bij het laden van code (`[COLD]`)
Als de naam van de methode Hallo bevat `[COLD]`, zoals `mscorlib.ni![COLD]System.Reflection.CustomAttribute.IsDefined`, betekent dit dat Hallo .NET framework runtime is uitvoeren van code dat niet is geoptimaliseerd door <a href="https://msdn.microsoft.com/library/e7k32f4k.aspx">optimalisatie profiel begeleide</a> voor Hallo eerst. Voor elke methode moet worden weergegeven van maximaal één keer tijdens de levensduur Hallo van Hallo-proces.

Als bij het laden van code aanzienlijke hoeveelheid tijd voor een aanvraag duurt, geeft aan dat verzoek is Hallo eerste één tooexecute Hallo niet geoptimaliseerde gedeelte van Hallo-methode. U kunt een warme up proces dat wordt uitgevoerd dat deel van het Hallo-code voordat uw gebruikers toegang krijgen het tot overwegen.

### <a id="httpclientsend"></a>HTTP-aanvraag verzenden
Methoden zoals `HttpClient.Send` Hallo code wordt gewacht op een HTTP-aanvraag toocomplete aangeven.

### <a id="sqlcommand"></a>Databasebewerking
Methode zoals SqlCommand.Execute geeft Hallo code wordt gewacht op een toocomplete database-bewerking.

### <a id="await"></a>Wachten op (`AWAIT\_TIME`)
`AWAIT\_TIME`Hiermee wordt aangegeven op Hallo code wordt gewacht op een andere taak toocomplete. Dit gebeurt gewoonlijk met C# 'await' instructie. Als Hallo-code heeft een C# 'await', hello thread afgewikkeld besturingselement toohello threadgroep retourneert en er is geen thread die wachten op Hallo 'await' toofinish is geblokkeerd. Logisch Hallo echter dat is Hallo await 'geblokkeerd' Hallo bewerking toocomplete wachten op thread. De `AWAIT\_TIME` geeft Hallo geblokkeerd tijd Hallo taak toocomplete wachten.

### <a id="block"></a>Geblokkeerde tijd
`BLOCKED_TIME`Hiermee wordt aangegeven op Hallo code wordt gewacht op een andere resource toobe beschikbaar, zoals het wachten op een synchronisatieobject, een thread-toobe beschikbaar of wacht op een aanvraag toofinish wachten.

### <a id="cpu"></a>CPU-tijd
Hallo CPU is bezig met uitvoeren Hallo-instructies.

### <a id="disk"></a>Schijftijd
de toepassing Hello uitvoert schijfbewerkingen.

### <a id="network"></a>Network Time
Hallo-toepassing met het uitvoeren van bewerkingen in het netwerk.

### <a id="when"></a>Wanneer kolom
Dit is een visualisatie van hoe Hallo inclusief voorbeelden die worden verzameld voor een knooppunt gedurende een bepaalde periode variëren. totale bereik van de aanvraag Hallo Hallo is onderverdeeld in 32 tijd buckets en Hallo inclusief voorbeelden voor dat knooppunt in deze buckets 32 wordt geteld. Elke bucket wordt vervolgens weergegeven als een balk waarvan u de hoogte een uitgebreid waarde vertegenwoordigt. Voor knooppunten gemarkeerd `CPU_TIME` of `BLOCKED_TIME`, of wanneer er een duidelijke relatie van de consumptie van een resource (cpu, schijf, een thread), Hallo balk vertegenwoordigt een van deze resources voor Hallo tijdsperiode die bucket verbruikt. Voor deze metrische gegevens krijgt u meer dan 100% door meerdere resources verbruikt. Bijvoorbeeld, als Gemiddeld u twee CPU's tijdens een interval van gebruiken krijgt vervolgens u 200%.


## <a id="troubleshooting"></a>Problemen oplossen

### <a name="how-can-i-know-whether-application-insights-profiler-is-running"></a>Hoe weet ik of Application Insights profiler wordt uitgevoerd?

Hallo profiler wordt uitgevoerd als een taak continu web in Web-App. U kunt Hallo Web-App-resource openen in https://portal.azure.com en controleer de status 'ApplicationInsightsProfiler' hello WebJobs-blade. Als deze niet wordt uitgevoerd, opent u **logboeken** toofind meer informatie.

### <a name="why-cant-i-find-any-stack-examples-even-though-hello-profiler-is-running"></a>Waarom kan ik geen voorbeelden stack vinden ook al Hallo profiler wordt uitgevoerd?

Hier volgen enkele dingen die u kunt controleren.

1. Zorg ervoor dat uw Web-App Service-Plan basisstaffel en hoger.
2. Zorg ervoor dat uw Web-App heeft Application Insights SDK 2.2 Beta en hierboven ingeschakeld.
3. Zorg ervoor dat uw Web-App Hallo APPINSIGHTS_INSTRUMENTATIONKEY instelling Hello dezelfde instrumentatiesleutel wordt gebruikt door de Application Insights-SDK.
4. Zorg ervoor dat uw Web-App wordt uitgevoerd op .net Framework 4.6.
5. Als het een toepassing ASP.NET Core, Controleer ook of [Hallo afhankelijkheden vereist](#aspnetcore).

Nadat de profiler Hallo is gestart, is er een korte opgewarmd periode wanneer Hallo profiler actief traceringen worden verzameld verschillende prestaties. Daarna Hallo profiler traceringen worden verzameld prestaties twee minuten in elk uur.  

### <a name="i-was-using-azure-service-profiler-what-happened-tooit"></a>Ik werd Azure Service Profiler gebruikt. Welke happened tooit?  

Wanneer u Application Insights Profiler inschakelt, is Azure Service Profiler agent uitgeschakeld.

### <a id="double-counting"></a>Dubbele parallelle threads tellen

In sommige gevallen Hallo is metric van de totale tijd in Hallo stack-viewer hoger dan de werkelijke duur van aanvraag Hallo Hallo.

Dit kan gebeuren wanneer er twee of meer threads die zijn gekoppeld aan een aanvraag, parallel uitgevoerd. tijd van de totale thread Hallo is meer dan Hallo verstreken tijd. Hallo in veel gevallen één thread wachten op een kan andere toocomplete. Hallo viewer pogingen toodetect dit en niet-interessante wacht Hallo weglaten, maar errs Hallo-zijde van te veel in plaats van als weggelaten welke essentiële informatie kunnen worden weergegeven.  

Wanneer u parallelle threads in uw traceringen zien, moet u toodetermine die threads wachten zodat u Hallo kritieke pad voor Hallo aanvraag kunt zien. In de meeste gevallen Hallo Hallo thread die in de modus wachttijd is snel gewoon wachten op een andere threads. Concentreren op Hallo van anderen en Hallo tijd in Hallo wachtende threads te negeren.

### <a id="issue-loading-trace-in-viewer"></a>Er is geen profileringsgegevens

1. Als Hallo gegevens die u probeert tooview ouder is dan een paar weken, kunt u uw tijdfilter beperken en probeer het opnieuw.

2. Controleer dat proxy of firewall toegang toohttps://gateway.azureserviceprofiler.net niet geblokkeerd.

3. Controleer dat Application Insights-instrumentatiesleutel die u in uw app gebruikt is dezelfde als Hallo Application Insights-resource die u hebt ingeschakeld met profilering Hallo Hallo. Hallo sleutel bevindt zich doorgaans in ApplicationInsights.config, maar u kunt ook vinden in web.config of app.config.

### <a name="error-report-in-hello-profiling-viewer"></a>Foutenrapport in Hallo viewer profileren

Een ondersteuningsticket vanuit de portal Hallo-bestand. Neem Hallo correlatie-ID van de fout het Hallo-bericht.

## <a name="manual-installation"></a>Handmatige installatie

Bij het configureren van Hallo profiler zijn hello volgende updates aangebracht toohello van Web-App-instellingen. U kunt ze zelf doen handmatig als uw omgeving, bijvoorbeeld, vereist als uw toepassing wordt uitgevoerd in Azure App Service omgeving (as-omgeving):

1. Open de instellingen in Hallo blade web-app besturingselement.
2. Stel '.Net Framework-versie ' toov4.6.
3. 'Altijd aan' tooOn ingesteld.
4. App-instelling toevoegen '__APPINSIGHTS_INSTRUMENTATIONKEY__' en set Hallo waarde toohello dezelfde instrumentatiesleutel door Hallo SDK gebruikt.
5. Open geavanceerde hulpprogramma's.
6. Klik op 'Ga' tooopen hello Kudu website.
7. Selecteer 'Site-uitbreidingen' hello Kudu website.
8. Installeer '__Application Insights__' uit de galerie.
9. Opnieuw opstarten Hallo web-app.

## <a id="aspnetcore"></a>ASP.NET Core-ondersteuning

ASP.NET Core toepassing moet tooinstall Microsoft.ApplicationInsights.AspNetCore Nuget-pakket 2.1.0-beta6 of hoger toowork Hello Profiler. We bieden geen ondersteuning voor lagere versies Hallo na 27-6/2017.

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
