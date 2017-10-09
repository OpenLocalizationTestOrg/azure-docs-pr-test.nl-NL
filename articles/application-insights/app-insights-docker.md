---
title: aaaMonitor Docker-toepassingen in Azure Application Insights | Microsoft Docs
description: Docker-prestatiemeteritems, gebeurtenissen en uitzonderingen kunnen worden weergegeven op de Application Insights, samen met de Hallo telemetrie van Hallo beperkte apps.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 27a3083d-d67f-4a07-8f3c-4edb65a0a685
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 9aaf1076bae25485a396db1bb3dcd13bccd87c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-docker-applications-in-application-insights"></a>Docker-toepassingen bewaken in Application Insights
Prestatiemeteritems van de levenscyclus van gebeurtenissen en de prestaties van [Docker](https://www.docker.com/) containers kunnen diagram op Application Insights. Hallo installeren [Application Insights](app-insights-overview.md) installatiekopie in een container in de host en prestatiemeteritems voor het Hallo-host, worden weergegeven als Hallo als voor andere installatiekopieën.

Met Docker, moet u uw apps in lightweight containers met alle afhankelijkheden voltooid distribueren. Ze kunnen worden uitgevoerd op elke host waarop een Docker-Engine wordt uitgevoerd.

Bij het uitvoeren van Hallo [Application Insights installatiekopie](https://hub.docker.com/r/microsoft/applicationinsights/) op uw host Docker dat u deze voordelen:

* De levenscyclus van telemetrie over alle Hallo containers die worden uitgevoerd op host Hallo - starten, stoppen, enzovoort.
* Prestatiemeteritems voor alle Hallo containers. CPU, geheugen, netwerkgebruik en meer.
* Als u [Application Insights-SDK voor Java geïnstalleerd](app-insights-java-live.md) Hallo apps die worden uitgevoerd in Hallo-containers, alle Hallo telemetrie van deze apps aanvullende eigenschappen identificeren Hallo-container en hostmachine zullen hebben. Als u exemplaren van een app in meer dan één host worden uitgevoerd, kunt u dus bijvoorbeeld eenvoudig uw app telemetrie door host filteren.

![Voorbeeld](./media/app-insights-docker/00.png)

## <a name="set-up-your-application-insights-resource"></a>Instellen van uw Application Insights-resource
1. Meld u aan bij [Microsoft Azure-portal](https://azure.com) en open Hallo Application Insights-resource voor uw app of [Maak een nieuwe](app-insights-create-new-resource.md). 
   
    *Welke resource moet ik gebruiken?* Als Hallo-apps die u op de host uitvoert zijn ontwikkeld door iemand anders, moet u te[Maak een nieuwe Application Insights-resource](app-insights-create-new-resource.md). Dit is waar u weergeven en analyseren van Hallo telemetrie. (Selecteer algemene voor Hallo app-type.)
   
    Maar als u Hallo ontwikkelaar van Hallo apps bent, klikt u vervolgens we hopen dat u [Application Insights-SDK toegevoegd](app-insights-java-live.md) tooeach hiervan. Als ze alle echt onderdelen van een enkele business-toepassing u ze allemaal toosend telemetrie tooone bron mogelijk configureert en gebruikt u dezelfde resource toodisplay hello Docker en prestaties van de levenscyclus van gegevens. 
   
    Een derde scenario is dat u de meeste Hallo apps ontwikkeld, maar u van afzonderlijke resources toodisplay hun telemetrie gebruikmaakt. In dat geval u waarschijnlijk ook wilt toocreate een afzonderlijke resource voor Hallo Docker-gegevens. 
2. Add Hallo Docker tegel: kies **toevoegen tegel**Hallo Docker tegel slepen vanuit galerie Hallo en klik vervolgens op **gedaan**. 
   
    ![Voorbeeld](./media/app-insights-docker/03.png)
3. Klik op Hallo **Essentials** vervolgkeuzelijst en Hallo Instrumentatiesleutel kopiëren. U gebruikt deze tootell Hallo SDK waar toosend de telemetrie.

    ![Voorbeeld](./media/app-insights-docker/02-props.png)

Houd dat browservenster handig als u dan terug tooit snel krijgt toolook op uw telemetrie.

## <a name="run-hello-application-insights-monitor-on-your-host"></a>Hallo Application Insights monitor op uw host worden uitgevoerd
Nu dat u ergens toodisplay Hallo telemetrie hebt, kunt u beperkte Hallo-app die wordt verzameld en verzonden instellen.

1. Verbinding maken met tooyour Docker-host. 
2. De instrumentatiesleutel in deze opdracht bewerken en vervolgens uit te voeren:
   
   ```
   
   docker run -v /var/run/docker.sock:/docker.sock -d microsoft/applicationinsights ikey=000000-1111-2222-3333-444444444
   ```

U hoeft slechts één installatiekopie van de Application Insights per Docker-host. Als uw toepassing wordt geïmplementeerd op meerdere Docker-hosts, herhaalt u de opdracht Hallo op elke host.

## <a name="update-your-app"></a>Uw app bijwerken
Als uw toepassing is uitgerust met Hallo [Application Insights-SDK voor Java](app-insights-java-get-started.md), toevoegen van de volgende regel in Hallo ApplicationInsights.xml-bestand in uw project, onder Hallo Hallo `<TelemetryInitializers>` element:

```xml

    <Add type="com.microsoft.applicationinsights.extensibility.initializer.docker.DockerContextInitializer"/> 
```

Docker informatie zoals de container en host-id tooevery telemetrie-item dat verzonden vanuit uw app wordt toegevoegd.

## <a name="view-your-telemetry"></a>Uw telemetrie weergeven
Ga terug tooyour Application Insights-resource in hello Azure-portal.

Klik in het Hallo Docker-tegel.

U ziet kort gegevens die binnenkomen in Hallo Docker-app, met name als u andere containers uitgevoerd op uw Docker-engine.

Hier zijn enkele Hallo weergaven die u kunt ophalen.

### <a name="perf-counters-by-host-activity-by-image"></a>Prestatiemeteritems door host activiteit door de installatiekopie
![Voorbeeld](./media/app-insights-docker/10.png)

![Voorbeeld](./media/app-insights-docker/11.png)

Klik op een host- of image-naam voor meer informatie.

toocustomize hello weergave, klikt u op een grafiek, Hallo raster kop, of gebruik grafiek toevoegen. 

[Meer informatie over metrics explorer](app-insights-metrics-explorer.md).

### <a name="docker-container-events"></a>Gebeurtenissen van docker-container
![Voorbeeld](./media/app-insights-docker/13.png)

tooinvestigate afzonderlijke gebeurtenissen, klikt u op [Search](app-insights-diagnostic-search.md). Zoeken en toofind Hallo gebeurtenissen die u wilt filteren. Klik op een gebeurtenis tooget meer details.

### <a name="exceptions-by-container-name"></a>Uitzonderingen op de naam van de container
![Voorbeeld](./media/app-insights-docker/14.png)

### <a name="docker-context-added-tooapp-telemetry"></a>Docker-context tooapp telemetrie toegevoegd
Telemetrie verzonden vanuit Hallo toepassing uitgerust met AI-SDK, verrijkt met Docker-context aanvragen:

![Voorbeeld](./media/app-insights-docker/16.png)

Tijd van processor en geheugen prestatiemeteritems, uitgebreid en gegroepeerd op de naam van de Docker-container:

![Voorbeeld](./media/app-insights-docker/15.png)

## <a name="q--a"></a>Vragen en antwoorden
*Wat Application Insights opleveren die ik bij Docker ophalen kan?*

* Detail van prestatiemeteritems door container en de installatiekopie.
* Integreer container en app-gegevens in één dashboard.
* [Exporteren van telemetrie](app-insights-export-telemetry.md) voor verdere analyse tooa database, Power BI of andere dashboard.

*Hoe krijg ik telemetrie van Hallo app zelf?*

* Hallo Application Insights-SDK installeren in Hallo-app. Meer informatie over hoe voor: [Java-web-apps](app-insights-java-get-started.md), [Windows web-apps](app-insights-asp-net.md).

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Volgende stappen

* [Application Insights voor Java](app-insights-java-get-started.md)
* [Application Insights voor Node.js](app-insights-nodejs.md)
* [Application Insights voor ASP.NET](app-insights-asp-net.md)
