---
title: aaaData en opslag in Azure Application Insights | Microsoft Docs
description: Beleidsverklaring bewaren en privacy
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: a6268811-c8df-42b5-8b1b-1d5a7e94cbca
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: bwren
ms.openlocfilehash: 7823431d03a57db5268d2724a0604e40666009f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="data-collection-retention-and-storage-in-application-insights"></a>Verzameling, retentie en opslag van gegevens in Application Insights


Wanneer u installeert [Azure Application Insights] [ start] SDK in uw app verzendt telemetrie over uw app toohello Cloud. Natuurlijk kunnen verantwoordelijk ontwikkelaars tooknow precies welke gegevens worden verzonden, wat er gebeurt toohello gegevens, en hoe ze nu de controle kunnen houden. In het bijzonder kan gevoelige gegevens worden verzonden, waarbij is opgeslagen, en hoe veilig is het? 

Eerst Hallo korte antwoord:

* Hallo standaard telemetrie modules die worden uitgevoerd 'out of box Hallo' zijn onwaarschijnlijk toosend gevoelige gegevens toohello service. Hallo telemetrie heeft betrekking op de belasting, prestaties en gebruik metrische gegevens, uitzonderingenrapporten en andere diagnostische gegevens. Hallo belangrijkste gebruikersgegevens in Hallo diagnostische rapporten zichtbaar zijn URL's; maar uw app in ieder geval gevoelige gegevens in tekst zonder opmaak in een URL mag niet plaatsen.
* U kunt code schrijven waarmee toohelp aanvullende aangepaste telemetrie verzendt u met diagnostische gegevens en gebruiksgegevens voor bewaking. (Deze uitbreidbaarheid is een uitstekende functie van Application Insights.) Het is mogelijk fout, toowrite dit met alle persoonlijke code en andere gevoelige gegevens. Als uw toepassing met dergelijke gegevens werkt, moet u een grondig processen tooall Hallo code die u schrijft toepassen.
* Tijdens het ontwikkelen en testen van uw app, is het eenvoudig tooinspect wat wordt verzonden door Hallo SDK. Hallo gegevens weergegeven in Hallo uitvoer windows hello IDE en browser foutopsporing. 
* Hallo-gegevens worden bewaard [Microsoft Azure](http://azure.com) servers in Hallo Verenigde Staten of Europa. (Maar overal kan worden uitgevoerd door uw app.) Azure heeft [sterke beveiliging verwerkt en voldoet aan een breed scala aan nalevingsstandaards](https://azure.microsoft.com/support/trust-center/). Alleen u en uw aangewezen team hebben toegang tot tooyour gegevens. Medewerkers van Microsoft kan toegang tooit beperkt tot specifieke beperkte omstandigheden met uw kennis hebt beperkt. Het versleuteld in doorvoer, maar niet in Hallo-servers.

Hallo rest van dit artikel meer volledig wordt ingegaan op wordt deze antwoorden. Het is ingesloten, toobe zo ontworpen dat u toocolleagues die geen deel uitmaken van uw team kunt weergeven.

## <a name="what-is-application-insights"></a>Wat is Application Insights?
[Azure Application Insights] [ start] is een service van Microsoft die u helpt verbeteren Hallo prestaties en bruikbaarheid van uw live-toepassing. Het bewaakt uw toepassing alle Hallo tijd uitgevoerd, zowel tijdens het testen en nadat u hebt gepubliceerd of geïmplementeerd. Application Insights grafieken en tabellen die u maakt, bijvoorbeeld welke tijdstippen ophalen van de meeste gebruikers hoe responsief Hallo-app is en hoe deze in behandeling is genomen door een externe bron services waar deze afhankelijk is van. Als er crashes, fouten of prestatieproblemen, kunt u zoeken via Hallo telemetrische gegevens in detail toodiagnose Hallo oorzaak. En het Hallo-service verzendt u e-mailberichten als er wijzigingen in Hallo beschikbaarheid en prestaties van uw app.

In volgorde tooget deze functionaliteit, installeert u een Application Insights-SDK in uw toepassing, dat deel van de code uitmaakt. Als uw app wordt uitgevoerd, controleert de werking ervan hello SDK- en verzendt telemetrie toohello Application Insights-service. Dit is een cloudservice wordt gehost door [Microsoft Azure](http://azure.com). (Maar Application Insights werkt voor alle toepassingen, niet alleen met toepassingen die worden gehost in Azure.)

![Hallo SDK in uw app verzendt telemetrie toohello Application Insights-service.](./media/app-insights-data-retention-privacy/01-scheme.png)

Hallo Application Insights-service worden opgeslagen en Hallo telemetriegegevens te analyseren. toosee hello analysis of zoeken via Hallo opgeslagen telemetrie, u zich aanmeldt tooyour Azure-account en open Hallo Application Insights-resource voor uw toepassing. U kunt ook toegang toohello-gegevens delen met andere leden van uw team of met de opgegeven Azure-abonnees.

U kunt de gegevens die zijn geëxporteerd uit Hallo Application Insights-service hebben bijvoorbeeld tooa database of tooexternal hulpprogramma's. U kunt elk hulpprogramma opgeven met een speciale sleutel die u Hallo-service aanschaft. Hallo-sleutel kan worden ingetrokken, indien nodig. 

Application Insights-SDK's zijn beschikbaar voor een bereik van toepassingstypen: webservices die worden gehost in uw eigen servers J2EE of ASP.NET of in Azure. webserver en webclients - dat wil zeggen, Hallo code die wordt uitgevoerd in een webpagina. Desktop-apps en services; apparaat-apps, zoals Windows Phone, iOS en Android. Ze alle telemetrie toohello verzenden dezelfde service.

## <a name="what-data-does-it-collect"></a>Welke gegevens verzamelt deze?
### <a name="how-is-hello-data-is-collected"></a>Wat is het Hallo-gegevens worden verzameld?
Er zijn drie gegevensbronnen:

* Hallo SDK, die u integreert met uw app ofwel [in ontwikkeling](app-insights-asp-net.md) of [tijdens runtime](app-insights-monitor-performance-live-website-now.md). Er zijn verschillende SDK's voor verschillende toepassingstypen. Er is ook een [SDK voor webpagina's](app-insights-javascript.md), die in de browser Hallo eindgebruiker samen met de Hallo pagina wordt geladen.
  
  * Elke SDK heeft een aantal [modules](app-insights-configuration-with-applicationinsights-config.md), welke andere technieken toocollect verschillende typen telemetrie gebruiken.
  * Als u Hallo SDK in de ontwikkeling installeren, kunt u de API-toosend uw eigen telemetrie in toevoeging toohello standaard modules. Deze aangepaste telemetrie kunt gewenste toosend gegevens bevatten.
* In sommige webservers zijn er ook agents die naast Hallo app worden uitgevoerd en het verzenden van telemetrie over CPU, geheugen en het netwerk bezetting. Bijvoorbeeld, virtuele Azure-machines, Docker-hosts en [J2EE-servers](app-insights-java-agent.md) dergelijke agents kan hebben.
* [Beschikbaarheidstests](app-insights-monitor-web-app-availability.md) processen worden uitgevoerd door Microsoft die aanvragen tooyour web-app verzenden met regelmatige tussenpozen. Hallo resultaten worden toohello Application Insights-service verzonden.

### <a name="what-kinds-of-data-are-collected"></a>Welke typen gegevens worden verzameld?
Hallo hoofdcategorieën zijn:

* [Web servertelemetrie](app-insights-asp-net.md) -HTTP-aanvragen.  URI, tijd benodigd tooprocess Hallo aanvraag, antwoordcode, client-IP-adres. Sessie-id.
* [Webpagina's](app-insights-javascript.md) -pagina-, gebruikers- en sessiegegevens aantallen. Laadtijden voor pagina's. Uitzonderingen. AJAX-aanroepen.
* Prestaties tellers - geheugen, CPU, i/o, netwerk-bezetting.
* Client en server context - OS, landinstellingen, apparaattype, browser, schermresolutie.
* [Uitzonderingen](app-insights-asp-net-exceptions.md) en crashes - **dumpbestanden stack**, CPU-type-id te bouwen. 
* [Afhankelijkheden](app-insights-asp-net-dependencies.md) -tooexternal services zoals REST, SQL, AJAX-aanroepen. URI of verbindingstekenreeks, duur, geslaagd, opdracht.
* [Beschikbaarheidstests](app-insights-monitor-web-app-availability.md) -duur van de test en stappen, antwoorden.
* [Traceerlogboeken](app-insights-asp-net-trace-logs.md) en [aangepaste telemetrie](app-insights-api-custom-events-metrics.md) - **alles wat u de code in de logboeken of de telemetrie**.

[Meer details](#data-sent-by-application-insights).

## <a name="how-can-i-verify-whats-being-collected"></a>Hoe kan ik controleren wat worden verzameld?
Als u ontwikkelt Hallo-app met Visual Studio, Hallo app uitvoeren in de foutopsporingsmodus (F5). Hallo telemetrie wordt weergegeven in het uitvoervenster Hallo. U kunt van daaruit kopiëren en formatteert u het als JSON voor eenvoudig inspectie. 

![](./media/app-insights-data-retention-privacy/06-vs.png)

Er is ook een beter leesbare weergave in Hallo Diagnostics-venster.

Open uw browservenster foutopsporing voor webpagina's.

![Druk op F12 en open tabblad Hallo-netwerk.](./media/app-insights-data-retention-privacy/08-browser.png)

### <a name="can-i-write-code-toofilter-hello-telemetry-before-it-is-sent"></a>Kan ik code toofilter Hallo telemetrie schrijven voordat deze wordt verzonden?
Door te schrijven mogelijk zou dit een [telemetrie processor invoegtoepassing](app-insights-api-filtering-sampling.md).

## <a name="how-long-is-hello-data-kept"></a>Hoe lang is Hallo gegevens behouden?
Onbewerkte gegevenspunten (items die u kunt een query in Analytics en controleren in de zoekopdracht) worden too90 dagen bewaard. Als u tookeep gegevens langer duurt dan nodig hebt, kunt u [continue export](app-insights-export-telemetry.md) toocopy het tooa storage-account.

Cumulatieve gegevens (dat wil zeggen, aantallen, gemiddelden en andere statistische gegevens die u in de metriek Explorer ziet) worden op een interval van 1 minuut gedurende 90 dagen bewaard.

## <a name="who-can-access-hello-data"></a>Wie toegang heeft tot Hallo gegevens?
Hallo-gegevens zijn zichtbaar tooyou en hebt u een organisatieaccount, leden van uw team. 

Het door u en uw teamleden kan worden geëxporteerd en kan worden gekopieerd tooother locaties en doorgegeven tooother mensen.

#### <a name="what-does-microsoft-do-with-hello-information-my-app-sends-tooapplication-insights"></a>Wat is Microsoft doen met Hallo informatie mijn app verzendt tooApplication Insights?
Microsoft gebruikt Hallo gegevens alleen in volgorde tooprovide Hallo service tooyou.

## <a name="where-is-hello-data-held"></a>Waar wordt Hallo gegevens gehouden?
* In de Verenigde Staten Hallo of Europa. Wanneer u een nieuwe Application Insights-resource maakt, kunt u Hallo locatie selecteren. 


#### <a name="does-that-mean-my-app-has-toobe-hosted-in-hello-usa-or-europe"></a>Betekent dat is gehost in Hallo Verenigde Staten of Europa toobe mijn app?
* Nee. Uw toepassing overal kan worden uitgevoerd, in uw eigen lokale hosts of in Hallo Cloud.

## <a name="how-secure-is-my-data"></a>Hoe veilig is mijn gegevens?
Application Insights is een Azure-Service. Beveiligingsbeleid worden beschreven in Hallo [whitepaper Azure-beveiliging, Privacy en naleving](http://go.microsoft.com/fwlink/?linkid=392408).

Hallo-gegevens worden opgeslagen in Microsoft Azure-servers. Voor accounts in Azure Portal Hallo accountbeperkingen worden beschreven in Hallo [Azure-beveiliging, Privacy en naleving document](http://go.microsoft.com/fwlink/?linkid=392408).

Toegang tot tooyour gegevens door medewerkers van Microsoft is beperkt. We toegang tot uw gegevens alleen met uw toestemming en als het benodigde toosupport uw gebruik van Application Insights. 

Gegevens in een statistische functie in alle onze klanten toepassingen (zoals gegevenssnelheden en de gemiddelde grootte van het traceren van) is gebruikt tooimprove Application Insights.

#### <a name="could-someone-elses-telemetry-interfere-with-my-application-insights-data"></a>Kan de telemetrie van iemand anders verstoren mijn gegevens Application Insights?
Ze kunnen extra telemetrie tooyour account verzenden met behulp van de instrumentatiesleutel hello, die kan worden gevonden in Hallo-code van uw webpagina's. Met voldoende extra gegevens zou metrische gegevens over uw niet exact overeen met de prestaties en het gebruik van uw app.

Als u code met andere projecten deelt, moet u tooremove uw instrumentatiesleutel.

## <a name="is-hello-data-encrypted"></a>Hallo gegevens versleuteld?
Niet in het Hallo-servers op dit moment.

Alle gegevens worden versleuteld doorloopt datacenters.

#### <a name="is-hello-data-encrypted-in-transit-from-my-application-tooapplication-insights-servers"></a>Worden Hallo gegevens versleuteld tijdens de overdracht van mijn toepassing tooApplication Insights servers?
Ja, gebruiken we https toosend toohello gegevensportal van bijna alle SDK's, inclusief webservers, apparaten en HTTPS-webpagina's. Hallo enige uitzondering hierop zijn gegevens verzonden van gewone HTTP-webpagina's. 

## <a name="personally-identifiable-information"></a>Persoonlijke gegevens
#### <a name="could-personally-identifiable-information-pii-be-sent-tooapplication-insights"></a>Kan worden persoonsgegevens (PII) tooApplication Insights verzonden?
Ja, is het mogelijk. 

Algemene richtlijnen:

* Meest standaard telemetrie (dat wil zeggen, telemetrie verzonden zonder dat u code schrijven) bevat geen expliciete PII. Het kan echter mogelijk tooidentify personen met Deductie uit een verzameling van gebeurtenissen zijn.
* Uitzondering en tracering berichten kunnen PII bevatten
* Aangepaste telemetrie - aanroepen zoals TrackEvent die u schrijft in code met behulp van de API- of logboekbestand traceringen Hallo - kunt u gegevens bevatten.

Hallo tabel aan Hallo einde van dit document bevat meer gedetailleerde beschrijvingen van Hallo gegevens die zijn verzameld.

#### <a name="am-i-responsible-for-complying-with-laws-and-regulations-in-regard-toopii"></a>Kan ik verantwoordelijk is voor die voldoet aan de wet- en regelgeving in inachtneming tooPII?
Ja. Het is uw verantwoordelijkheid tooensure die Hallo verzamelen en gebruiken van gegevens Hallo voldoet met wet- en regelgeving en met Hallo Microsoft Online servicevoorwaarden.

U moet uw klanten op de juiste wijze informeren over Hallo gegevens door die uw toepassing worden verzameld en hoe hello worden gebruikt.

#### <a name="can-my-users-turn-off-application-insights"></a>Kunnen mijn gebruikers uitschakelen Application Insights?
Niet rechtstreeks. We een switch niet bieden dat uw gebruikers tooturn uit Application Insights kunnen werken.

U kunt deze functie echter implementeren in uw toepassing. Alle Hallo SDK's bevatten een API-instelling wordt uitgeschakeld telemetrie-verzameling. 

#### <a name="my-application-is-unintentionally-collecting-sensitive-information-can-application-insights-scrub-this-data-so-it-isnt-retained"></a>Mijn toepassing verzamelen per ongeluk gevoelige informatie. Kan Application Insights deze gegevens wissen zodat deze wordt niet behouden
Application Insights niet filteren of verwijderen van uw gegevens. U moet Hallo gegevens op de juiste wijze beheren en te voorkomen dat dergelijke gegevens tooApplication Insights verzenden.

## <a name="data-sent-by-application-insights"></a>Gegevens die worden verzonden door de Application Insights
Hallo-SDK's variëren tussen platforms en er zijn verschillende onderdelen die u kunt installeren. (Raadpleeg te[Application Insights - overzicht][start].) Elk onderdeel verzendt verschillende gegevens.

#### <a name="classes-of-data-sent-in-different-scenarios"></a>Klassen van gegevens die worden verzonden in verschillende scenario 's
| De actie | Gegevensklassen verzameld (Zie de volgende tabel) |
| --- | --- |
| [Application Insights-SDK tooa .NET webproject toevoegen][greenbrown] |ServerContext<br/>Afgeleid<br/>-Prestatiemeteritems<br/>Aanvragen<br/>**Uitzonderingen**<br/>Sessie<br/>gebruikers |
| [Statusmonitor installeren op IIS][redfield] |Afhankelijkheden<br/>ServerContext<br/>Afgeleid<br/>-Prestatiemeteritems |
| [Application Insights-SDK tooa Java-web-app toevoegen][java] |ServerContext<br/>Afgeleid<br/>Aanvraag<br/>Sessie<br/>gebruikers |
| [JavaScript SDK tooweb pagina toevoegen][client] |ClientContext <br/>Afgeleid<br/>Pagina<br/>ClientPerf<br/>AJAX |
| [Standaard-eigenschappen definiëren][apiproperties] |**Eigenschappen** op alle standaard- en aangepaste gebeurtenissen |
| [Aanroep TrackMetric][api] |Numerieke waarden<br/>**Eigenschappen** |
| [Aanroep bijhouden *][api] |De naam van gebeurtenis<br/>**Eigenschappen** |
| [Aanroep TrackException][api] |**Uitzonderingen**<br/>Stackdump<br/>**Eigenschappen** |
| SDK kan geen gegevens verzamelen. Bijvoorbeeld: <br/> -heeft geen toegang tot prestatiemeteritems<br/> -uitzondering in telemetrie initialisatiefunctie |SDK diagnostische gegevens |

Voor [SDK's voor andere platforms][platforms], Zie hun documenten.

#### <a name="hello-classes-of-collected-data"></a>Hallo klassen van de verzamelde gegevens
| Klasse van de verzamelde gegevens | (Geen uitputtende lijst) bevat |
| --- | --- |
| **Eigenschappen** |**Een gegevens - bepaald door uw code** |
| DeviceContext |ID, IP-, landinstellingen, Apparaatmodel, netwerk, netwerktype, OEM-naam, schermresolutie Rolinstantie, Role-naam, Type apparaat |
| ClientContext |OS landinstellingen, taal, netwerk, venster resolutie |
| Sessie |Sessie-id |
| ServerContext |Naam van de computer, landinstellingen, besturingssysteem, apparaat, gebruikerssessie, gebruikerscontext, bewerking |
| Afgeleid |geografische locatie van IP-adres, timestamp, besturingssysteem, browser |
| Metrische gegevens |Metrische naam en waarde |
| Gebeurtenissen |Gebeurtenisnaam en waarde |
| PageViews |URL- en de naam of scherm |
| Client perf |Naam van de URL/pagina, laadtijd van de browser |
| AJAX |HTTP-verzoeken van webpagina tooserver |
| Aanvragen |De URL, duur, antwoordcode |
| Afhankelijkheden |Type (SQL, HTTP,...), de verbindingsreeks of de URI, sync/async, duur, geslaagd, SQL-instructie (met Status Monitor) |
| **Uitzonderingen** |Type **bericht**, stacks aanroepen, bron- en regelnummer number, thread-id |
| Crashes |Proces-id, proces-id van bovenliggende, crashes thread-id; toepassingspatch, -id, build;  uitzonderingstype, adres, reden; verborgen symbolen en registers binaire begin- en -adressen, binaire naam en pad, cpu-type |
| Tracering |**Bericht** en ernst |
| -Prestatiemeteritems |Processortijd, beschikbaar geheugen, frequentie van aanvragen, uitzondering snelheid, proces eigen bytes, i/o-snelheid, duur van de aanvraag, lengte van aanvraagwachtrij |
| Beschikbaarheid |Web-test antwoord-code, de duur van elke stap, naam van test, timestamp, geslaagd, reactietijden, testlocatie |
| SDK diagnostische gegevens |Trace-bericht of uitzondering |

U kunt [Hallo gegevens door te bewerken ApplicationInsights.config uitschakelen][config]

## <a name="credits"></a>Tegoed
Dit product bevat GeoLite2 gegevens die zijn gemaakt door MaxMind beschikbaar is via [http://www.maxmind.com](http://www.maxmind.com).



<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiproperties]: app-insights-api-custom-events-metrics.md#properties
[client]: app-insights-javascript.md
[config]: app-insights-configuration-with-applicationinsights-config.md
[greenbrown]: app-insights-asp-net.md
[java]: app-insights-java-get-started.md
[platforms]: app-insights-platforms.md
[pricing]: http://azure.microsoft.com/pricing/details/application-insights/
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md

