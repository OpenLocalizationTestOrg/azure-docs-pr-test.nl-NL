---
title: aaaTroubleshoot Application Insights in een Java-webproject
description: Problemen oplossen met - bewaking live Java-apps met Application Insights.
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: ef602767-18f2-44d2-b7ef-42b404edd0e9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: bwren
ms.openlocfilehash: c274c01b1992971fae194c3e510512ca06ab76b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-and-q-and-a-for-application-insights-for-java"></a>Probleemoplossing voor en antwoorden op vragen over Application Insights voor Java
Vragen of problemen met [Azure Application Insights in Java][java]? Hier volgen enkele tips.

## <a name="build-errors"></a>Fouten bouwen
**In Eclipse wanneer toe te voegen Hallo Application Insights-SDK via Maven of Gradle, wordt er validatiefouten in build of controlesom.**

* Als afhankelijkheid Hallo <version> element gebruikt een patroon met jokertekens (bijvoorbeeld (Maven) `<version>[1.0,)</version>` of (Gradle) `version:'1.0.+'`), kunt u een specifieke versie te gebruiken in plaats daarvan opgeven zoals `1.0.2`. Zie Hallo [release-opmerkingen](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) voor Hallo meest recente versie.

## <a name="no-data"></a>Er zijn geen gegevens
**Ik heb Application Insights is toegevoegd en Mijn app uitgevoerd, maar ik gegevens in de portal Hallo nooit hebt gezien.**

* Wacht even en klik op vernieuwen. Hallo grafieken worden regelmatig vernieuwd, maar u kunt ook handmatig vernieuwen. Hallo-interval voor vernieuwen is afhankelijk van tijdsbereik Hallo van Hallo-grafiek.
* Controleer of u een instrumentatiesleutel die is gedefinieerd in Hallo ApplicationInsights.xml-bestand (in Hallo map van de bronnen in uw project hebt)
* Controleer of er geen `<DisableTelemetry>true</DisableTelemetry>` knooppunt in Hallo XML-bestand.
* In de firewall wellicht tooopen TCP-poorten 80 en 443 voor het uitgaande verkeer toodc.services.visualstudio.com. Zie Hallo [volledige lijst met uitzonderingen voor firewall](app-insights-ip-addresses.md)
* In Microsoft Azure Hallo start board, bekijkt hello status Serviceoverzicht. Als er een waarschuwing aanwijzingen zijn, wacht u totdat ze zijn tooOK geretourneerd en vervolgens sluiten en opnieuw de blade van het Application Insights-toepassing openen.
* Schakelt logboekregistratie toohello IDE-consolevenster, door toe te voegen in een `<SDKLogger />` element onder het hoofdknooppunt Hallo in Hallo ApplicationInsights.xml-bestand (in Hallo map van de bronnen in uw project) en Controleer op vermeldingen die vooraf worden gegaan door [fout].
* Zorg ervoor dat Hallo juiste ApplicationInsights.xml-bestand is geladen door Hallo Java SDK, door te kijken Hallo-console-Uitvoerberichten voor een 'configuratiebestand is gevonden'-instructie.
* Als het Hallo-configuratiebestand is niet gevonden, Controleer Hallo uitvoer berichten toosee waar Hallo-configuratiebestand wordt gezocht en zorg ervoor dat Hallo die applicationinsights.xml bevindt zich in een van deze zoeklocaties. Als vuistregel, kunt u Hallo configuratiebestand plaatsen in de buurt Hallo Application Insights SDK JARs. Bijvoorbeeld: in Tomcat, dit zou betekenen Hallo WEB-INF/lib map.

#### <a name="i-used-toosee-data-but-it-has-stopped"></a>Ik toosee gegevens gebruikt, maar deze is gestopt
* Controleer de Hallo [status blog](http://blogs.msdn.com/b/applicationinsights-status/).
* Hebt u uw maandelijkse quotum van gegevenspunten bereikt? Open instellingen/quotum en prijzen toofind uit. Als dit het geval is, kunt u uw abonnement upgraden of betalen voor extra capaciteit. Zie Hallo [prijzen schema](https://azure.microsoft.com/pricing/details/application-insights/).

#### <a name="i-dont-see-all-hello-data-im-expecting"></a>Alle Hallo gegevens die ik ben verwacht wordt niet weergegeven
* Open Hallo quota's en prijzen blade en controleer of [steekproeven](app-insights-sampling.md) wordt uitgevoerd. (de verzending van 100% betekent dat steekproeven in bewerking niet.) Hallo Application Insights-service kan worden ingesteld tooaccept slechts een fractie van Hallo telemetrie van uw app binnenkomt. Hiermee houdt u binnen uw maandelijkse quotum telemetrie. 

## <a name="no-usage-data"></a>Geen gebruiksgegevens
**Gegevens over aanvragen en reactietijden, maar er is geen paginaweergave, browser of gebruikersgegevens weergegeven.**

U ingesteld uw app toosend telemetrie van Hallo-server. Nu de volgende stap te is[instellen van uw webpagina's toosend telemetrie vanuit de webbrowser Hallo][usage].

U kunt ook als de client is een app in een [telefoon of ander apparaat][platforms], voor het verzenden van telemetrie vanaf daar. 

Gebruik dezelfde Hallo instrumentation sleutel tooset up telemetrie van uw client en de server. Hallo gegevens weergegeven dezelfde Application Insights-resource Hallo en u zult kunnen toocorrelate gebeurtenissen van de client en server.


## <a name="disabling-telemetry"></a>Telemetrie uitschakelen
**Hoe kan ik telemetrie verzameling uitschakelen?**

In de code:

```Java

    TelemetryConfiguration config = TelemetryConfiguration.getActive();
    config.setTrackingIsDisabled(true);
```

**Of** 

Werk ApplicationInsights.xml (in Hallo map van de bronnen in uw project). Voeg de volgende Hallo onder Hallo hoofdknooppunt:

```XML

    <DisableTelemetry>true</DisableTelemetry>
```

Hallo XML-methode gebruikt, hebt u toorestart Hallo toepassing wanneer u Hallo waarde wijzigen.

## <a name="changing-hello-target"></a>Hallo doel wijzigen
**Hoe kan ik welke Azure-resource mijn project gegevens worden verzonden wijzigen?**

* [Hallo-instrumentatiesleutel van de nieuwe resource Hallo ophalen.][java]
* Als u Application Insights tooyour project met hello Azure Toolkit voor Eclipse hebt toegevoegd, klik met de rechtermuisknop op uw webproject, selecteer **Azure**, **Configure Application Insights**, en wijzig Hallo-sleutel.
* Anders werken Hallo-sleutel in ApplicationInsights.xml in de map van de Hallo bronnen in uw project.

## <a name="debug-data-from-hello-sdk"></a>Gegevens van Hallo SDK Debug

**Hoe vind ik welke Hallo SDK doet?**

tooget meer informatie over wat er gebeurt in Hallo-API toevoegen `<SDKLogger/>` onder het hoofdknooppunt Hallo van Hallo ApplicationInsights.xml-configuratiebestand.

U kunt ook de opdracht geven Hallo berichtenlogboek toooutput tooa bestand:

```XML

    <SDKLogger type="FILE">
      <enabled>True</enabled>
      <UniquePrefix>JavaSDKLog</UniquePrefix>
    </SDKLogger>
```

Hallo-bestanden kunnen worden gevonden in het `%temp%\javasdklogs` of `java.io.tmpdir` in geval van Tomcat-server.


## <a name="hello-azure-start-screen"></a>Hello Azure startscherm
**Ik ben kijken [hello Azure-portal](https://portal.azure.com). Hallo-kaart zegt iets over mijn app?**

Nee, het Hallo-status van de Azure-servers bevat Hallo wereld.

*Van hello Azure start board (startscherm), hoe vind ik gegevens over mijn app?*

Ervan uitgaande dat u [stelt u de app voor Application Insights][java], klik op Bladeren, selecteer Application Insights en selecteer Hallo app bron die u voor uw app hebt gemaakt. tooget er sneller in de toekomst, u kunt vastmaken uw app toohello start board.

## <a name="intranet-servers"></a>Servers van intranet
**Kan ik een server bewaken op mijn intranet**

Ja, mits uw server kunt verzenden telemetrie toohello Application Insights-portal via openbaar internet Hallo. 

In de firewall wellicht tooopen TCP-poorten 80 en 443 voor het uitgaande verkeer toodc.services.visualstudio.com en f5.services.visualstudio.com.

## <a name="data-retention"></a>Bewaartijd van gegevens
**Hoe lang gegevens bewaard in de portal Hallo? Is het veilig?**

Zie [bewaren van gegevens en privacy][data].

## <a name="next-steps"></a>Volgende stappen
**Ik instellen Application Insights voor de app my server Java. Wat kan ik doen?**

* [Beschikbaarheid van uw webpagina's bewaken][availability]
* [Webpagina-gebruik controleren][usage]
* [Gebruik bijhouden en onderzoeken van problemen in uw apps op apparaten][platforms]
* [Schrijven van code tootrack informatie over het gebruik van uw app][track]
* [Logboeken met diagnostische gegevens vastleggen][javalogs]

## <a name="get-help"></a>Help opvragen
* [Stack Overflow](http://stackoverflow.com/questions/tagged/ms-application-insights)

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[data]: app-insights-data-retention-privacy.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[platforms]: app-insights-platforms.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md

