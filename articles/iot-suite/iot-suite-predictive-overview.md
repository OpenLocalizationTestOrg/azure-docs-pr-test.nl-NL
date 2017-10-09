---
title: aaaPredictive onderhoud vooraf geconfigureerde oplossing | Microsoft Docs
description: Een beschrijving van hello Azure IoT Suite voorspeld onderhoud vooraf geconfigureerde oplossing.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: b370b3d7-2ce5-4906-9818-3aeedd471ee3
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 2d09801467d33db6b7d6333fa071aea2bf573f20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="predictive-maintenance-preconfigured-solution-overview"></a>Overzicht van de vooraf geconfigureerde oplossing voor voorspeld onderhoud

Hallo *voorspeld onderhoud* [vooraf geconfigureerde oplossing] [ lnk_preconfigured_solutions] is een Hallo [Microsoft Azure IoT Suite] [ lnk_iot_suite] vooraf geconfigureerde oplossingen. Deze oplossing integreert het in realtime verzamelen van telemetriegegevens met een voorspellend model dat is gemaakt met behulp van [Azure Machine Learning][lnk-machine-learning].

Met Azure IoT Suite u snel en eenvoudig verbinding kunt tooand monitor activa, en analyseren van telemetrie in realtime in dashboards en visualisaties. In de oplossing voor voorspeld onderhoud hello bieden Hallo dashboards en visualisaties u nieuwe bedrijfsinformatie die kan efficiënter en meer inkomsten kunnen genereren.

## <a name="hello-scenario"></a>Hallo Scenario

Fabrikam is een regionale luchtvaartmaatschappij die zich toelegt op het leveren van een uitstekende klantervaring tegen concurrerende prijzen. Een oorzaak van vertragingen zijn onderhoudsproblemen, waarbij het onderhoud van vliegtuigmotoren een bijzondere uitdaging vormt. Fabrikam moet voorkomen motoren ontstaan tijdens de vlucht ten koste wat kost dus regelmatig de motoren inspecteert en gepland onderhoud op basis van tooa plan. Vliegtuig engines niet slijten Hallo echter hetzelfde. Soms wordt er onnodig onderhoud uitgevoerd op motoren. En wat belangrijker is, er doen zich soms problemen voor die ervoor zorgen dat een vliegtuig aan de grond moet blijven totdat het onderhoud is uitgevoerd. Als een vliegtuig zich op een locatie kunnen waar Hallo juiste technici of onderdelen zijn niet beschikbaar, deze problemen bijzonder kostbaar.

Hallo-engines van de vliegtuigen van Fabrikam zijn uitgerust met sensoren die motor tijdens de vlucht bewaken. Fabrikam gebruikt Hallo voorspeld onderhoud oplossing toocollect Hallo sensorgegevens die zijn verzameld tijdens de vlucht Hallo. Na jarenlang van operationele-engine en gegevens hebt verzameld van Fabrikam een manier toopredict Hallo resterende levensduur (resterende Levensduur) van een vliegtuigmotor gemodelleerd. Hallo-model maakt gebruik van een correlatie tussen gegevens van vier hello motorsensoren en de slijtage engine die tooeventual fout leidt. Terwijl Fabrikam tooperform regelmatige inspecties tooensure veiligheid doorgaat, kan nu gebruikmaken van Hallo modellen toocompute Hallo resterende Levensduur van elke motor na elke vlucht. Hallo model Hallo verzamelen van telemetriegegevens van Hallo-engines tijdens de vlucht Hallo gebruikt. Fabrikam is nu in staat om toekomstige probleempunten te voorspellen en om van tevoren onderhoud en reparatiewerkzaamheden te plannen.

> [!NOTE]
> Hallo oplossing model reële slijtagegegevens gebruikt.

Door het Hallo-punt voorspellen waarop onderhoud vereist, kan Fabrikam zijn bewerkingen tooreduce kosten optimaliseren.

Onderhoudscoördinatoren werken met planners:

- Plan onderhoud toocoincide een vliegtuig stoppen op een bepaalde locatie.
- Zorg ervoor dat voldoende tijd is beschikbaar voor Hallo vliegtuig toobe buiten de service zonder onderbreking van de planning.
- tooschedule technici tooensure vliegtuig efficiënt worden verwerkt zonder wachttijd.

Magazijnbeheerders ontvangen de onderhoudsplannen zodat zij hun bestelproces en hun voorraad met reserveonderdelen kunnen optimaliseren.

Deze activiteiten Fabrikam toominimize vliegtuig compleet tijd inschakelen en de operationele kosten verlagen terwijl de veiligheid van passagiers en bemanning Hallo.

toounderstand hoe [Azure IoT Suite] [ lnk_iot_suite] biedt Hallo mogelijkheden klanten nodig toorealize Hallo potentieel van voorspeld onderhoud controleert dit [infographic] [lnk_infographic].

## <a name="how-hello-predictive-maintenance-solution-is-built"></a>Hoe Hallo-oplossing voor voorspeld onderhoud is gebouwd

Hallo oplossing maakt gebruik van een bestaand Azure Machine Learning-model beschikbaar als een sjabloon tooshow deze mogelijkheden werken op basis van telemetriegegevens die zijn verzameld via IoT Suite-services. Microsoft heeft ontwikkeld een [regressiemodel] [ lnk_regression_model] van een vliegtuigmotor op basis van openbaar beschikbare gegevens<sup>\[1\]</sup>, en stapsgewijze hulp bij hoe toouse Hallo model.

Hallo-regressiemodel dat is gemaakt met deze sjabloon maakt gebruik van Hello Azure IoT-oplossing voor voorspeld onderhoud. Hallo-model is geïmplementeerd in uw Azure-abonnement en toegankelijk zijn via een automatisch gegenereerde API. Hallo-oplossing omvat een subset van Hallo testen van gegevens voor 4 (van in totaal 100) motoren en Hallo 4 (van in totaal 21) gegevensstromen. Deze gegevens zijn voldoende tooprovide een accuraat resultaat opleveren van Hallo getrainde model.

*\[1\] A. Saxena en K. Goebel (2008). 'Turbofan Engine Degradation Simulation Data Set', NASA Ames Prognostics Data Repository (http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/), NASA Ames Research Center, Moffett Field, CA*

## <a name="get-started-with-predictive-maintenance"></a>Aan de slag met voorspellend onderhoud

Deze zelfstudie leert u hoe tooprovision Hallo oplossing voor voorspeld onderhoud. Ook wordt u begeleid Hallo basisfuncties van Hallo-oplossing voor voorspeld onderhoud. Veel van deze functies kunt u openen via het dashboard van de oplossing Hallo die samen met de Hallo vooraf geconfigureerde oplossing implementeert.

toocomplete in deze zelfstudie, moet u een actief Azure-abonnement.

> [!NOTE]
> Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken. Zie [Gratis proefversie van Azure][lnk_free_trial] voor meer informatie.

1. Meld u aan te[azureiotsuite.com] [ lnk-azureiotsuite] met behulp van uw Azure accountreferenties en klikt u op  **+**  toocreate een oplossing.
1. Klik op **Selecteer** hello **voorspeld onderhoud** tegel.
1. Voer een **Naam van oplossing** in voor uw vooraf geconfigureerde oplossing voor voorspellend onderhoud.
1. Selecteer Hallo **regio** en **abonnement** toouse tooprovision Hallo oplossing.
1. Klik op **oplossing maken** toobegin Hallo inrichtingsproces. Dit proces duurt gewoonlijk enkele minuten toorun.

### <a name="wait-for-hello-provisioning-process-toocomplete"></a>Wachten op Hallo proces toocomplete inrichten

1. Klik op de tegel Hallo voor uw oplossing met **inrichten** status.
1. Kennisgeving Hallo **Inrichtingstatuswaarden** wanneer Azure-services worden geïmplementeerd in uw Azure-abonnement.
1. Nadat het inrichten is voltooid, Hallo u statuswijzigingen te**gereed**.
1. Klik op Hallo tegel toosee Hallo details van uw oplossing in het rechterdeelvenster Hallo. U kunt dit deelvenster Hallo oplossing dashboard en toegang Hallo Machine Learning-werkruimte starten.

> [!NOTE]
> Als u problemen Hallo vooraf geconfigureerde oplossing implementeren, controleren [machtigingen op Hallo azureiotsuite.com site] [ lnk-permissions] en Hallo [Veelgestelde vragen over] [ lnk-faq]. Als Hallo problemen zich blijven voordoen, maakt u een serviceticket op Hallo [portal][lnk-portal].

Zijn er details u mag verwachten toosee die voor uw oplossing niet vermeld? Geef ons suggesties voor functies op [User Voice](https://feedback.azure.com/forums/321918-azure-iot).

## <a name="view-hello-solution"></a>Hallo-oplossing weergeven

Deze sectie helpt u bij Hallo oplossing gebruikersinterface.

### <a name="predictive-maintenance-dashboard"></a>Dashboard voorspeld onderhoud

Deze pagina in Hallo-webtoepassing maakt gebruik van PowerBI JavaScript-besturingselementen (Zie Hallo [PowerBI-visuals repository][lnk-powerbi]) toovisualize:

* Hallo uitvoergegevens van Hallo Stream Analytics-taken in de blob-opslag.
* Hallo resterende Levensduur en aantal cycli per vliegtuigmotor.

### <a name="observing-hello-behavior-of-hello-cloud-solution"></a>Hallo-gedrag van Hallo cloudoplossing observeren

In Azure-portal hello, navigeert u toohello resourcegroep met de naam van de oplossing Hallo u hebt gekozen tooview uw ingerichte resources.

![][img-resource-group]

Wanneer u Hallo vooraf geconfigureerde oplossing inricht, krijgt u een e-mail met een koppeling toohello Machine Learning-werkruimte. U kunt ook toohello Machine Learning-werkruimte van Hallo navigeren [azureiotsuite.com] [ lnk-azureiotsuite] pagina voor de ingerichte oplossing. Een tegel is beschikbaar op deze pagina wanneer Hallo oplossing Hallo wordt **gereed** status.

![][img-machine-learning]

In de oplossingsportal hello ziet u dat Hallo-voorbeeld is ingericht met vier gesimuleerde apparaten toorepresent twee vliegtuig met twee motoren per vliegtuig, elk met vier sensoren. Wanneer u eerst toohello oplossingsportal navigeert, wordt Hallo simulatie gestopt.

![][img-simulation-stopped]

Klik op **simulatie starten** toobegin Hallo simulatie. Hallo sensor geschiedenis, resterende Levensduur, cycli en de resterende Levensduur geschiedenis vullen Hallo-dashboard.

![][img-simulation-running]

Wanneer de resterende Levensduur minder dan 160 is (een willekeurige drempel gekozen ter illustratie), wordt een waarschuwing symbool volgende toohello weergegeven resterende Levensduur in Hallo oplossingsportal weergegeven. Hallo oplossingsportal ook Hallo vliegtuigmotor geel gemarkeerd. U ziet hoe Hallo resterende Levensduur waarden hebben voor een algemene neerwaartse trend, maar vaak toobounce omhoog en omlaag. Dit probleem wordt veroorzaakt door verschillende lengten Hallo en Hallo model nauwkeurig.

![][img-simulation-warning]

de volledige simulatie Hallo duurt ongeveer 35 minuten toocomplete 148 cycli. Hallo 160 resterende Levensduur drempelwaarde wordt voldaan voor Hallo eerst na ongeveer 5 minuten en beide motoren Hallo drempelwaarde na ongeveer 8 minuten bereikt.

Hallo simulatie wordt uitgevoerd via Hallo volledige gegevensset voor 148 cycli en bepaalt dan het eindresultaat van laatste resterende Levensduur en waarden.

U kunt stoppen Hallo simulatie op elk punt, maar te klikken op **simulatie starten** replays Hallo simulatie van Hallo begin van Hallo gegevensset.

## <a name="next-steps"></a>Volgende stappen

meer informatie over hoe Azure IoT maakt voor voorspeld onderhoud-scenario's, lezen toolearn [vastleggen van de waarde van het Internet der dingen Hallo][lnk_capture_value].

Duren voordat een [scenario] [ lnk-predictive-walkthrough] van Hallo-oplossing voor voorspeld onderhoud.

U kunt ook verkennen van Hallo andere functies en mogelijkheden van Hallo vooraf geconfigureerde IoT Suite-oplossingen:

* [Veelgestelde vragen over IoT Suite][lnk-faq]
* [Beveiliging van de IoT van Hallo gemalen][lnk-security-groundup]

[img-resource-group]: media/iot-suite-predictive-overview/resource-group.png
[img-simulation-stopped]: media/iot-suite-predictive-overview/simulation-stopped.png
[img-simulation-running]: media/iot-suite-predictive-overview/simulation-running.png
[img-simulation-warning]: media/iot-suite-predictive-overview/simulation-warning.png
[img-machine-learning]: media/iot-suite-predictive-overview/machine-learning.png

[lnk-powerbi]: https://www.github.com/Microsoft/PowerBI-visuals
[lnk-predictive-walkthrough]: iot-suite-predictive-walkthrough.md
[lnk_preconfigured_solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk_iot_suite]: iot-suite-overview.md
[lnk_infographic]: https://www.microsoft.com/server-cloud/predictivemaintenance/Index.html
[lnk_regression_model]: http://gallery.cortanaanalytics.com/Collection/Predictive-Maintenance-Template-3

[lnk_capture_value]: http://download.microsoft.com/download/0/7/D/07D394CE-185D-4B96-AC3C-9B61179F7080/Capture_value_from_the_Internet%20of%20Things_with_Predictive_Maintenance.PDF
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-permissions]: iot-suite-permissions.md
[lnk-portal]: http://portal.azure.com/
[lnk-machine-learning]: https://azure.microsoft.com/services/machine-learning/