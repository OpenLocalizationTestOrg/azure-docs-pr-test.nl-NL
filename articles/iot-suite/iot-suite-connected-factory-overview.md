---
title: aaaAzure IoT Suite verbonden factory overzicht | Microsoft Docs
description: Een beschrijving van hello Azure IoT Suite verbonden factory vooraf geconfigureerde oplossing.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: dobett
ms.openlocfilehash: 929b5ed41ef7d82c9b4480d02aa3f0db38931919
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-connected-factory-preconfigured-solution"></a>Aan de slag met Hallo verbonden factory vooraf geconfigureerde oplossing

Azure IoT Suite [vooraf geconfigureerde oplossingen] [ lnk-preconfigured-solutions] combineren meerdere Azure IoT services toodeliver end-to-end-oplossingen die algemene IoT-bedrijfsscenario's implementeren. Hallo *verbonden factory* tooand monitors uw industriële apparaten vooraf geconfigureerde oplossing verbonden. U kunt Hallo oplossing tooanalyze Hallo stroom van gegevens van uw apparaten en toodrive operationele productiviteit en winstgevendheid.

Deze zelfstudie laat zien hoe tooprovision Hallo factory verbonden vooraf geconfigureerde oplossing. Ook wordt u begeleid Hallo basisfuncties van Hallo vooraf geconfigureerde oplossing. U veel van deze functies kunt openen vanaf Hallo oplossing *dashboard* die als onderdeel van Hallo vooraf geconfigureerde oplossing implementeert:

![dashboard van de vooraf geconfigureerde oplossing voor verbonden factory's][img-cf-home]

toocomplete in deze zelfstudie, moet u een actief Azure-abonnement.

> [!NOTE]
> Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken. Zie [Gratis proefversie van Azure][lnk_free_trial] voor meer informatie.
> 
> 

## <a name="provision-hello-solution"></a>Hallo-oplossing inrichten

1. Meld u aan tooazureiotsuite.com met behulp van de referenties van uw Azure-account en klik op '**+**' toocreate een oplossing.
2. Klik op **Selecteer** op Hallo **verbonden factory** tegel.
3. Voer een **oplossingsnaam** in voor uw verbonden vooraf geconfigureerde oplossing.
4. Selecteer Hallo **abonnement** en **regio** toouse tooprovision Hallo oplossing.
5. Klik op **oplossing maken** toobegin Hallo inrichtingsproces. Dit proces duurt gewoonlijk enkele minuten toorun.

### <a name="while-you-wait-for-hello-provisioning-process-toocomplete"></a>Terwijl u wacht op Hallo proces toocomplete inrichten

1. Klik op de tegel Hallo voor uw oplossing met **inrichten** status.
2. Kennisgeving Hallo **Inrichtingstatuswaarden** wanneer Azure-services worden geïmplementeerd in uw Azure-abonnement.
3. Nadat het inrichten is voltooid, Hallo u statuswijzigingen te**gereed**.
4. Klik op Hallo tegel toosee Hallo details van uw oplossing in het rechterdeelvenster Hallo.

> [!NOTE]
> Als u problemen Hallo vooraf geconfigureerde oplossing implementeren, controleren [machtigingen op Hallo azureiotsuite.com site] [ lnk-permissions] en Hallo [verbonden factory Veelgestelde vragen over](iot-suite-faq-cf.md). Als Hallo problemen zich blijven voordoen, maakt u een serviceticket op Hallo [portal][lnk-portal].

Zijn er details u mag verwachten toosee die voor uw oplossing niet vermeld? Geef ons suggesties voor functies op [User Voice](https://feedback.azure.com/forums/321918-azure-iot).

## <a name="scenario-overview"></a>Overzicht van scenario's

Bij het implementeren van Hallo verbonden factory vooraf geconfigureerde oplossing, het is vooraf ingevuld met de resources die u in staat toostep via een gemeenschappelijke industriële scenario stellen. In dit scenario verschillende fabrieken toohello oplossing rapport Hallo gegevenswaarden vereist toocompute verbonden algehele apparatuur efficiëntie (OEE) en prestatie-indicatoren (KPI's). Hallo volgende secties ziet u hoe aan:

* de factory, de productielijnen, de OEE van stations en de KPI-waarden controleert;
* Hallo telemetrische gegevens gegenereerd op basis van deze apparaten met behulp van Azure Time Series Insights analyseren
* Reageren op waarschuwingen toofix problemen

Een belangrijke functie van dit scenario is dat u al deze acties extern vanuit Hallo oplossing dashboard uitvoeren kunt. U hoeft geen fysieke toegang toohello apparaten.

## <a name="view-hello-solution-dashboard"></a>Dashboard van oplossing Hallo weergeven

Hallo oplossing dashboard kunt u toomanage Hallo geïmplementeerd oplossing. Het is een hiërarchische weergave van een overkoepelende factoryconfiguratie. U kunt bijvoorbeeld de OEE en KPI's weergeven, nieuwe knooppunten voor telemetrie publiceren en waarschuwingen uitvoeren.

1. Wanneer Hallo inrichten is voltooid en Hallo tegel voor uw vooraf geconfigureerde oplossing geeft **gereed**, kies **starten** tooopen uw oplossingsportal verbonden factory in een nieuw tabblad.

    ![Hallo vooraf geconfigureerde oplossing starten][img-launch-solution]

1. Standaard ziet u de oplossingsportal Hallo Hallo *dashboard*. toonavigate tooother gebieden van Hallo portal gebruik Hallo menu aan de linkerkant Hallo van Hallo pagina.

    ![Dashboard van de vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-menu]

Hallo dashboard toont de Hallo volgende informatie:

* Een **Factory lijst** Configuratiescherm waarin Hallo status, de locatie en de huidige productconfiguratie in Hallo-oplossing. Wanneer u Hallo oplossing voor het eerst uitvoert, moet u er een aantal gesimuleerde apparaten zijn. Hallo productie regel simulatie bestaat uit drie echte OPC UA servers per regel productie die gesimuleerde taken uitvoeren en gegevens delen. Zie voor meer informatie over OPC UA Hallo [verbonden factory Veelgestelde vragen over](iot-suite-faq-cf.md).
* Een **kaart** dat Hiermee Hallo locatie van elk apparaat toohello oplossing verbonden. Hallo-oplossing kunt Hallo Bing kaarten-API tooplot informatie gebruiken op Hallo-kaart. Als de Bing Kaarten Enterprise-API is ingeschakeld voor uw abonnement, wordt deze functie automatisch gebruikt. Als dit niet het geval is, Zie Hallo [Veelgestelde vragen over] [ lnk-faq] toolearn hoe toomake kaart dynamische Hallo.
* Een paneel **Waarschuwingen** dat waarschuwingen weergeeft die worden gegenereerd wanneer een telemetrie- of OEE-/KPI-waarde een bepaalde drempelwaarde overschrijdt.
* Een **algehele apparatuur efficiëntie** Configuratiescherm die toont Hallo OEE waarden voor de hele onderneming Hallo of Hallo productie-factory regel/station u bekijkt. Deze waarde wordt geaggregeerd van Hallo station weergave toohello enterprise niveau. Hallo OEE afbeelding en de bijbehorende samenstellende elementen kunnen verder worden geanalyseerd.
* **Key Performance Indicators** bekijkt hello aantal geproduceerde eenheden en energie gebruikt door de hele onderneming Hallo of Hallo productie-factory regel/station u paneel. Deze waarden worden van een station weergave toohello enterprise-niveau samengevoegd.

## <a name="view-factories"></a>Factory's weergeven

Hallo *fabrieken* toont Hallo van geografische locatie van alle Hallo fabrieken in Hallo-oplossing, hun status en de huidige productconfiguratie van het deelvenster. Uit Hallo locaties lijst, kunt u toohello andere niveaus in Hallo oplossing hiërarchie navigeren. Hallo rijen in de lijst Hallo zijn hyperlinks die een koppeling details van Hallo productie regels op die locatie. Is deze mogelijk toodrill in productie-regeldetails Hallo en omlaag weergave toohello station niveau. U kunt ook een filterlijst toohello toepassen.

![Factory's van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-factories] 

1. Hallo **Factory Configuratiescherm** toont Hallo lijst van de fabriek voor deze oplossing.

2. Hallo factory lijst geeft in eerste instantie zes factory's die zijn gemaakt door Hallo inrichtingsproces. U kunt extra gesimuleerde en fysieke apparaten toohello oplossing toevoegen.

3. tooview hello details van een fabriek, klikt u op Hallo rij in Hallo factory lijst.

4. tooview hello details van een regel voor productie, klikt u op Hallo rij in de lijst Hallo.

5. tooview hello OPC UA-knooppunten van een station op Hallo productie regel gepubliceerd, klikt u op Hallo rij in de lijst Hallo.

6. tooview op een specifiek knooppunt in het Hallo-station, klikt u op Hallo rij in de lijst Hallo. Deze actie wordt gestart Hallo context Configuratiescherm met Time Series Insights visualisaties. Klik op deze grafieken toodo verdere analyse in Hallo Time Series Insights explorer-omgeving.

## <a name="view-map"></a>Kaart weergeven

Als uw abonnement toegang toohello Bing kaarten-API heeft, Hallo *fabrieken* kaart toont u Hallo geografische locatie en status van alle Hallo fabrieken in Hallo-oplossing. toodrill op Hallo locatiegegevens, klikt u op Hallo locaties op Hallo kaart weergegeven.

![Kaart van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-map]

## <a name="view-alerts"></a>Waarschuwingen weergeven

Hallo **waarschuwing** deelvenster ziet u de waarschuwingen die worden gegenereerd vanwege tooa gerapporteerd waarde of een berekende OEE/KPI-waarde van meer dan de geconfigureerde drempelwaarde. Dit deelvenster geeft waarschuwingen weer op elk niveau van de hiërarchie hello, van Hallo station weergave niveau toohello globale weergave. Hallo-berichten bevatten een beschrijving van waarschuwing hello, datum, tijd, locatie en het aantal exemplaren. Kan krijgt u inzicht in toohello gegevens die met behulp van Hallo Time Series-inzichtgegevens Hallo-waarschuwing heeft veroorzaakt. Hallo Time Series Insights gegevens worden weergegeven in Hallo waarschuwingen, indien van toepassing. Als u een beheerder bent, kunt u de standaardacties uitvoeren op Hallo van waarschuwingen, zoals:

* Waarschuwing sluiten Hallo.
* Begrijp Hallo waarschuwing.

Eventueel kunt u complexere acties uitvoeren. Voor Hallo druk OPC UA knooppunt Hallo Assembly kan u bijvoorbeeld:

* Ondersteunende informatie weergeven op een webpagina in een nieuw browservenster.
* Hallo oorzaak van de waarschuwing Hallo beperken door het aanroepen van een methode OPC UA op Hallo-apparaat.
* Hallo-beschikbaarheid van Hallo standaardacties onderdrukken.

    ![Waarschuwingen van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-alerts]

> [!NOTE]
> Deze waarschuwingen worden gegenereerd door regels die zijn opgegeven in een configuratiebestand in Hallo vooraf geconfigureerde oplossing. Deze regels kunnen waarschuwingen genereren wanneer Hallo OEE of KPI cijfers of OPC UA knooppunt waarden de geconfigureerde drempelwaarde overschrijdt.

1. Hallo **waarschuwingen Configuratiescherm** toont Hallo waarschuwingen gegenereerd in deze oplossing.

2. tooview hello details van een waarschuwing, klik op Hallo-waarschuwing in Hallo waarschuwingen Configuratiescherm.

3. toofurther hello waarschuwingsgegevens analyseren, klikt u op Hallo grafiek in Hallo waarschuwing Configuratiescherm tooopen Hallo Time Series Insights explorer-omgeving.

4. tooaddress Hallo waarschuwing, verschillende acties zijn beschikbaar in de waarschuwing deelvenster Hallo. Kies de gewenste optie Hallo voor u en klikt u op Hallo opdrachtknop actie uitvoeren.

## <a name="view-overall-equipment-efficiency"></a>Algemene apparatuurefficiëntie weergeven

OEE tarieven Hallo efficiëntie Hallo fabricageproces met behulp van een sleutel operationele gerelateerd aan de productie-parameters. OEE is een industrie standaardeenheid berekend door vermenigvuldiging tarief hello, frequentie van de prestaties en kwaliteit snelheid: OEE = beschikbaarheid x prestaties x kwaliteit.

![OEE van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-oee]

1. tooview OEE voor elk niveau in de hiërarchie hello, navigeer toohello specifieke weergave die u nodig hebt. Hallo OEE voor deze weergave wordt weergegeven in Configuratiescherm samen met elk van de Hallo elementen waaruit percentage OEE Hallo Hallo.

2. toofurther hello OEE voor elk niveau in Hallo hiërarchiegegevens analyseren, klikt u op Hallo OEE, beschikbaarheid, prestaties of kwaliteit percentage. Een context paneel wordt weergegeven met Time Series Insights voeding visualisaties waarin gegevens uit Hallo laatste uur, de afgelopen 24 uur en de afgelopen 7 dagen.

    ![TSI-visualisatie van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-tsi-visualization]

3. toofurther hello waarschuwingsgegevens analyseren, klikt u op Hallo grafiek in Hallo waarschuwing Configuratiescherm. Deze actie wordt geopend Hallo Time Series Insights explorer-omgeving.

    ![TSI-verkenner van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-tsi-explorer]

## <a name="view-key-performance-indicators"></a>Key performance indicators weergeven

Hallo-oplossing biedt twee prestatie-indicatoren *eenheden per uur* en *energieverbruik in kWh*.

![KPI van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-kpi]

1. tooview eenheden per uur of energie gebruikt voor elk niveau in de hiërarchie hello, navigeer toohello specifieke weergave die u nodig hebt. Hallo-eenheden per uur en energie weergeven in Hallo Configuratiescherm gebruikt.

2. tooanalyze eenheden per uur of energie gebruikt voor elk niveau in Hallo hiërarchie verdere, klikt u op Hallo meter in Hallo **Key Performance Indicators** Configuratiescherm. Een paneel context weergegeven met Time Series Insights ingeschakeld visualisaties zodat u tooview gegevens van Hallo afgelopen uur Hallo afgelopen 24 uur en de afgelopen 7 dagen.

## <a name="scenario-review"></a>Samenvatting van scenario

In dit scenario moet u uw fabrieken OEE en KPI's waarden, Hallo dashboard bewaakt. U vervolgens gebruikt Time Series Insights tooprovide meer informatie toohelp lager niveau verder Hallo telemetriegegevens voor OEE en KPI's toohelp met afwijkingen detecteren. U gebruikt ook Hallo waarschuwing Configuratiescherm tooview problemen met uw fabrieken en u Hallo acties beschikbaar tooyou tooresolve Hallo waarschuwing gebruikt.

## <a name="other-features"></a>Andere functies

Hallo volgende secties worden enkele aanvullende functies van Hallo verbonden factory-oplossing die niet zijn beschreven in het voorgaande scenario Hallo beschreven.

## <a name="apply-filters"></a>Filters toepassen

1. Klik op Hallo **punthaak** toodisplay een lijst met beschikbare filters in ofwel Hallo factory locaties deelvenster of Hallo waarschuwingen.

2. Hallo filters deelvenster wordt weergegeven voor u. 

    ![Filters van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-alert-filter]

3. Kies Hallo filter die u nodig hebt. Het is ook mogelijk tootype vrije tekst in Hallo filtervelden.

4. Hallo-filter wordt vervolgens toegepast voor u. Hallo-filterstatus wordt ook weergegeven in het dashboard Hallo via een trechter die wordt weergegeven in Hallo fabrieken en waarschuwt tabellen.

    ![Filters van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-alert-filter-funnel]

    > [!NOTE]
    > Een actieve filter heeft geen invloed op de waarden van Hallo weergegeven OEE en KPI's, het Hallo lijstinhoud alleen wordt gefilterd.

5. een filter tooclear Hallo trechter en klik op filter in het deelvenster Hallo filter-context. tekst Hello **alle** wordt weergegeven in Hallo fabrieken en waarschuwingen tabellen.

## <a name="browse-an-opc-ua-server"></a>Door een OPC UA-server bladeren

Wanneer u Hallo vooraf geconfigureerde oplossing implementeert, worden automatisch gesimuleerde OPC UA-servers die u via Hallo oplossing browser bladeren kunt inrichten. Deze servers zijn *gesimuleerde OPC UA-servers*. Gesimuleerde servers maakt het eenvoudig voor u tooexperiment met Hallo vooraf geconfigureerde oplossing zonder Hallo nodig toodeploy echte servers. Als u dat een echte OPC UA toohello serveroplossing tooconnect wilt, raadpleegt u Hallo [uw OPC UA apparaat toohello verbonden factory vooraf geconfigureerde oplossing verbinden] [ lnk-connect-cf] zelfstudie.

1. Klik op Hallo **factory pictogram** in de navigatiebalk Hallo-dashboard.

    ![Serverbrowser van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-server-browser]

2. Kies een van de servers Hallo uit Hallo vooraf geconfigureerde lijst. Deze lijst bevat Hallo-servers die in Hallo vooraf geconfigureerde oplossing voor u zijn geïmplementeerd.

    ![Serverselectie van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-server-choice]

3. Klik op **Verbinden**. Er wordt een beveiligingsdialoogvenster weergegeven. Voor de simulatie hello, is het veilig tooclick **doorgaan**

4. tooexpand hello knooppunten in de serverstructuur hello, klikt u op. Naast knooppunten die telemetrie publiceren, staat een vinkje.

    ![Serverstructuur van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-server-tree]

5. Met de rechtermuisknop op een item tooread, schrijven, publiceren of aanroepen van dat knooppunt. Hallo acties beschikbaar tooyou, is afhankelijk van uw machtigingen en kenmerken van knooppunt Hallo Hallo. Hallo lezen optie toodisplays een context paneel Hallo-waarde van een specifiek knooppunt Hallo weergeeft. Hallo schrijven optie geeft een context paneel waarin u een nieuwe waarde kunt invoeren. Hallo aanroep optie bevat een knooppunt waarin u Hallo parameters voor Hallo-aanroep invoeren kunt.

## <a name="publish-a-node"></a>Een knooppunt publiceren

Wanneer u bladert een *gesimuleerde OPC UA-server*, u kunt ook toopublish nieuwe knooppunten. U kunt analyseren Hallo telemetrie van deze knooppunten in het Hallo-oplossing. Deze *OPC UA-servers in de simulatie* eenvoudig tooexperiment met Hallo vooraf geconfigureerde oplossing maken zonder het echte apparaten implementeren.

1. Blader tooa knooppunt in Hallo OPC UA browser serverstructuur gewenste toopublish.

2. Met de rechtermuisknop op Hallo-knooppunt.

3. Kies **Publiceren**.

    ![Verbonden factory publiceert knooppunt][cf-img-publish-node]

4. Een paneel context wordt weergegeven dat aangeeft dat Hallo publiceren is voltooid. Hallo-knooppunt wordt weergegeven in Hallo station weergave van niveau met een vinkje.

    ![Succesvolle publicatie van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-publish-success]

## <a name="command-and-control"></a>Opdracht en controle

Hallo verbonden factory kunt u de opdracht en beheren van uw apparaten bedrijfstak rechtstreeks vanuit de cloud Hallo. U kunt deze functie toorespond tooalerts gegenereerd door Hallo-apparaat gebruiken. U kan bijvoorbeeld een opdracht toohello apparaat verzenden vanuit Hallo cloud. U vindt Hallo beschikbare opdrachten in Hallo **StationCommands** knooppunt in Hallo OPC UA servers browser structuur. In dit scenario moet u een zware belasting release klep op Hallo assembly station van een regel productie in München openen. toouse hello opdracht en controle functionaliteit, moet u in Hallo **beheerder** rol voor Hallo vooraf geconfigureerde oplossing voor implementatie.

1. Blader toohello **StationCommands** knooppunt in Hallo OPC UA-server browser-structuur.

2. Hallo kiest dat u gebruiken wilt.

3. Met de rechtermuisknop op Hallo-knooppunt.

4. Kies **Aanroepen**.

    ![Aanroepopdracht van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-call-command]

5. Een context paneel wordt weergegeven waarin wordt gemeld welke methode u gaat toocall en eventuele details van de parameter is van toepassing.

6. Kies **Aanroepen**.

    ![Aanroepcontext van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-call-context]

7. Hallo context deelvenster is bijgewerkte tooinform dat Hallo methodeaanroep is voltooid. U kunt controleren of Hallo-aanroep is voltooid door te lezen Hallo-waarde van Hallo zware belasting op het knooppunt dat als gevolg van het Hallo-aanroep bijgewerkt.

    ![Aanroepen voltooid van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-call-success]


## <a name="behind-hello-scenes"></a>Achter de schermen Hallo

Wanneer u een vooraf geconfigureerde oplossing implementeert, maakt Hallo implementatieproces meerdere resources in hello Azure-abonnement u hebt geselecteerd. U kunt deze resources weergeven in hello Azure [portal][lnk-portal]. Hallo-implementatieproces maakt een **resourcegroep** met een naam op basis van Hallo-naam die u voor uw vooraf geconfigureerde oplossing kiest:

![Vooraf geconfigureerde oplossing in hello Azure-portal][img-cf-portal]

U kunt instellingen Hallo van elke resource weergeven door deze te selecteren in lijst van resources in de resourcegroep Hallo Hallo.

U kunt ook de broncode Hallo voor Hallo vooraf geconfigureerde oplossing weergeven. Hallo verbonden factory vooraf geconfigureerde oplossing broncode is in Hallo [azure-iot-verbonden-factory] [ lnk-cfgithub] GitHub-opslagplaats:

Wanneer u klaar bent, kunt u Hallo vooraf geconfigureerde oplossing verwijderen uit uw Azure-abonnement op Hallo [azureiotsuite.com] [ lnk-azureiotsuite] site. Deze site kunt u alle resources die zijn ingericht toen u Hallo vooraf geconfigureerde oplossing maakte Hallo tooeasily-verwijderen.

> [!NOTE]
> tooensure u Alles verwijderen gerelateerde toohello vooraf geconfigureerde oplossing, te verwijderen op Hallo [azureiotsuite.com] [ lnk-azureiotsuite] site. Hallo-resourcegroep in Hallo portal niet verwijderen.

## <a name="next-steps"></a>Volgende stappen

Nu dat u een werkende vooraf geconfigureerde oplossing hebt geïmplementeerd, kunt u blijven aan de slag met IoT Suite door te lezen Hallo artikelen te volgen:

* [Overzicht van de vooraf geconfigureerde oplossing voor verbonden factory's][lnk-rm-walkthrough]
* [Uw apparaat toohello verbonden factory vooraf geconfigureerde oplossing verbinden][lnk-connect-cf]
* [Machtigingen op Hallo azureiotsuite.com site][lnk-permissions]

[img-cf-home]:media/iot-suite-connected-factory-overview/cf-dashboard.png
[img-launch-solution]: media/iot-suite-connected-factory-overview/launch-cf.png
[cf-img-menu]: media/iot-suite-connected-factory-overview/cf-dashboard-menu.png
[cf-img-factories]:media/iot-suite-connected-factory-overview/cf-dashboard-factory.png
[cf-img-map]:media/iot-suite-connected-factory-overview/cf-dashboard-map.png
[cf-img-alerts]:media/iot-suite-connected-factory-overview/cf-dashboard-alerts.png
[cf-img-oee]:media/iot-suite-connected-factory-overview/cf-dashboard-oee.png
[cf-img-kpi]:media/iot-suite-connected-factory-overview/cf-dashboard-kpi.png
[cf-img-tsi-visualization]:media/iot-suite-connected-factory-overview/cf-dashboard-tsi.png
[cf-img-tsi-explorer]:media/iot-suite-connected-factory-overview/tsi-explorer.png
[cf-img-server-browser]: media/iot-suite-connected-factory-overview/cf-dashboard-browser.png
[cf-img-server-choice]: media/iot-suite-connected-factory-overview/cf-select-server.png
[cf-img-server-tree]:media/iot-suite-connected-factory-overview/cf-server-tree.png
[cf-img-publish-node]:media/iot-suite-connected-factory-overview/cf-publish-node1.png
[cf-img-publish-success]:media/iot-suite-connected-factory-overview/cf-publish-success.png
[cf-img-call-command]:media/iot-suite-connected-factory-overview/cf-command-and-control-call.png
[cf-img-call-context]:media/iot-suite-connected-factory-overview/cf-command-and-control-call-button.png
[cf-img-call-success]:media/iot-suite-connected-factory-overview/cf-command-and-control-succeed.png
[img-cf-portal]:media/iot-suite-connected-factory-overview/cf-resource-group.png
[cf-img-alert-filter]:media/iot-suite-connected-factory-overview/cf-filter.png
[cf-img-alert-filter-funnel]:media/iot-suite-connected-factory-overview/cf-filter-funnel.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-portal]: http://portal.azure.com/
[lnk-cfgithub]: https://github.com/Azure/azure-iot-connected-factory
[lnk-rm-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[lnk-connect-cf]: iot-suite-connected-factory-gateway-deployment.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-faq]: iot-suite-faq.md