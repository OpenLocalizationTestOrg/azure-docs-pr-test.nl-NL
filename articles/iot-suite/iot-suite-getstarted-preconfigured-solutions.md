---
title: aaaGet de slag met vooraf geconfigureerde oplossingen | Microsoft Docs
description: Volg deze zelfstudie toolearn hoe toodeploy een Azure IoT Suite vooraf geconfigureerde oplossing.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 6ab38d1a-b564-469e-8a87-e597aa51d0f7
ms.service: iot-suite
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: a7f46023d26b08de2e8ed48c34c5066a43e3fa38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-preconfigured-solutions"></a>Aan de slag met Hallo vooraf geconfigureerde oplossingen

Azure IoT Suite [vooraf geconfigureerde oplossingen] [ lnk-preconfigured-solutions] combineren meerdere Azure IoT services toodeliver end-to-end-oplossingen die algemene IoT-bedrijfsscenario's implementeren. Hallo *externe controle* vooraf geconfigureerde oplossing voor uw apparaten tooand monitors verbonden. Hallo oplossing tooanalyze Hallo stroom van gegevens van uw apparaten en tooimprove bedrijfsresultaten kunt u door het maken van processen automatisch toothat gegevensstroom reageren.

Deze zelfstudie leert u hoe tooprovision Hallo externe controle vooraf geconfigureerde oplossing. Ook wordt u begeleid Hallo basisfuncties van Hallo vooraf geconfigureerde oplossing. U veel van deze functies kunt openen vanaf Hallo oplossing *dashboard* die als onderdeel van Hallo vooraf geconfigureerde oplossing implementeert:

![Vooraf geconfigureerd oplossingsdashboard voor externe controle][img-dashboard]

toocomplete in deze zelfstudie, moet u een actief Azure-abonnement.

> [!NOTE]
> Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken. Zie [Gratis proefversie van Azure][lnk_free_trial] voor meer informatie.

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

## <a name="scenario-overview"></a>Overzicht van scenario's

Wanneer u Hallo vooraf geconfigureerde oplossing voor externe controle implementeert, is deze vooraf ingevuld met resources waarmee u toostep via een algemeen scenario voor externe controle. In dit scenario zijn verschillende apparaten verbonden toohello oplossing onverwachte temperatuur waarden rapportage. Hallo volgende secties ziet u hoe aan:

* Onverwachte temperatuur waarden verzenden Hallo-apparaten kan identificeren.
* Configureren van deze apparaten toosend meer gedetailleerde telemetrie.
* Hallo probleem oplossen door het bijwerken van de firmware Hallo op deze apparaten.
* Controleer of dat uw actie Hallo probleem is opgelost.

Een belangrijke functie van dit scenario is dat u al deze acties extern vanuit Hallo oplossing dashboard uitvoeren kunt. U hoeft geen fysieke toegang toohello apparaten.

## <a name="view-hello-solution-dashboard"></a>Dashboard van oplossing Hallo weergeven

Hallo oplossing dashboard kunt u toomanage Hallo geïmplementeerd oplossing. U kunt er bijvoorbeeld telemetrie weergeven, apparaten toevoegen en regels configureren.

1. Wanneer Hallo inrichten is voltooid en Hallo tegel voor uw vooraf geconfigureerde oplossing geeft **gereed**, kies **starten** tooopen uw externe controle portal van de oplossing in een nieuw tabblad.

    ![Hallo vooraf geconfigureerde oplossing starten][img-launch-solution]

1. Standaard ziet u de oplossingsportal Hallo Hallo *dashboard*. U kunt tooother gebieden van de portal van de oplossing Hallo Hallo menu aan de linkerkant Hallo van Hallo pagina met navigeren.

    ![Vooraf geconfigureerd oplossingsdashboard voor externe controle][img-menu]

Hallo dashboard toont de Hallo volgende informatie:

* Een kaart die wordt weergegeven Hallo-locatie van elk apparaat verbonden toohello oplossing. Wanneer u Hallo oplossing voor het eerst uitvoert, moet u er 25 gesimuleerde apparaten zijn. Hallo gesimuleerde apparaten worden geïmplementeerd als Azure WebJobs en Hallo oplossing gebruikt Hallo Bing kaarten-API tooplot informatie op Hallo-kaart. Zie Hallo [Veelgestelde vragen over] [ lnk-faq] toolearn hoe toomake kaart dynamische Hallo.
* Een deelvenster **Telemetriegeschiedenis** dat de vochtigheids- en temperatuurtelemetrie van een geselecteerd apparaat in bijna realtime tekent en statistische gegevens weergeeft, zoals de maximale, minimale en gemiddelde vochtigheid.
* Een deelvenster **Geschiedenis van waarschuwingen** dat recente waarschuwingsgebeurtenissen toont wanneer voor een telemetriewaarde een drempelwaarde wordt overschreden. U kunt uw eigen alarmen definiëren in toevoeging toohello voorbeelden is gemaakt door Hallo vooraf geconfigureerde oplossing.
* Een deelvenster **Taken** dat informatie weergeeft over geplande taken. U kunt uw eigen taken plannen op de pagina **Beheertaken**.

## <a name="view-alarms"></a>Waarschuwingen weergeven

Hallo alarm geschiedenis deelvenster ziet u dat de melden van vijf apparaten hoger dan de verwachte telemetrie waarden.

![Geschiedenis van TODO-waarschuwingen op Hallo oplossing dashboard][img-alarms]

> [!NOTE]
> Deze waarschuwingen worden gegenereerd door een regel die is opgenomen in Hallo vooraf geconfigureerde oplossing. Deze regel genereert een waarschuwing wanneer Hallo temperatuur waarde die is verzonden door een apparaat hoger is dan 60. U kunt uw eigen regels en acties definiëren door te kiezen [regels](#add-a-rule) en [acties](#add-an-action) in het menu links van Hallo.

## <a name="view-devices"></a>Apparaten weergeven

Hallo *apparaten* lijst bevat alle Hallo geregistreerde apparaten in Hallo-oplossing. Vanaf Hallo lijst met apparaten kunt u bekijken en bewerken van metagegevens van apparaten, toevoegen of verwijderen van apparaten en methoden niet aanroepen voor apparaten. U kunt filteren en sorteren Hallo lijst met apparaten in de lijst met Hallo-apparaten. U kunt ook weergegeven in de lijst met apparaten Hallo Hallo-kolommen aanpassen.

1. Kies **apparaten** tooshow Hallo lijst met apparaten voor deze oplossing.

   ![Lijst met apparaten van weergave-Hallo in de oplossingsportal Hallo][img-devicelist]

1. lijst met apparaten Hallo toont in eerste instantie 25 gesimuleerde apparaten die zijn gemaakt door Hallo inrichtingsproces. U kunt extra gesimuleerde en fysieke apparaten toohello oplossing toevoegen.

1. tooview hello details van een apparaat, kies een apparaat in de lijst met Hallo-apparaten.

   ![Hallo Apparaatdetails in de oplossingsportal Hallo weergeven][img-devicedetails]

Hallo **Apparaatdetails** deelvenster bevat zes secties:

* Een verzameling van koppelingen die u toocustomize Hallo pictogram van het apparaat inschakelen, Hallo apparaat uitschakelt, een regel kunt toevoegen, een methode aangeroepen of een opdracht verzenden. Zie [Cloud-to-device communications guidance][lnk-c2d-guidance] (Richtlijnen voor communicatie tussen cloud en apparaat) voor een vergelijking van opdrachten (berichten van apparaat naar cloud) en methoden (directe methoden).
* Hallo **apparaat Twin - Tags** sectie kunt u tooedit labelwaarden voor Hallo-apparaat. U kunt tagwaarden worden weergegeven in de lijst met apparaten Hallo en tag waarden toofilter Hallo apparatenlijst gebruiken.
* Hallo **apparaat Twin - eigenschappen gewenst** sectie kunt u tooset eigenschap waarden toobe verzonden toohello apparaat.
* Hallo **apparaat Twin - eigenschappen gerapporteerd** sectie toont de waarden van Hallo apparaat verzonden.
* Hallo **apparaateigenschappen** sectie wordt informatie weergegeven uit Hallo identiteitsregister zoals Hallo apparaat-id- en verificatiesleutels.
* Hallo **recente taken** sectie bevat informatie over alle taken die dit apparaat onlangs zijn gericht.

## <a name="filter-hello-device-list"></a>Lijst met apparaten Hallo filteren

Alleen de apparaten die onverwachte temperatuur waarden verzendt, kunt u een filter toodisplay gebruiken. Hallo vooraf geconfigureerde oplossing voor externe controle omvat Hallo **slecht apparaten** tooshow apparaten met een gemiddelde temperatuur-waarde die groter zijn dan 60 filteren. U kunt ook [uw eigen filters maken](#add-a-filter).

1. Kies **opgeslagen filter openen** toodisplay een lijst met beschikbare filters. Kies vervolgens **slecht apparaten** tooapply Hallo filter:

    ![Hallo-lijst met filters weergeven][img-unhealthy-filter]

1. lijst met apparaten Hallo wordt nu alleen apparaten met een gemiddelde temperatuur-waarde groter dan 60.

    ![Weergave Hallo gefilterde lijst met apparaten niet in orde apparaten weergegeven][img-filtered-unhealthy-list]

## <a name="update-desired-properties"></a>Gewenste eigenschappen bijwerken

U hebt nu een set apparaten geïdentificeerd die mogelijk moeten worden hersteld. Echter, u besluit Hallo gegevensfrequentie van 15 seconden is niet voldoende voor een duidelijke diagnose van Hallo probleem. Het wijzigen van Hallo telemetrie frequentie toofive seconden tooprovide diagnosticeren u met meer gegevenspunten toobetter Hallo probleem. U kunt deze configuratie wijzigen tooyour externe apparaten uit de oplossingsportal Hallo push. U kunt slechts één keer evalueren Hallo impact, en vervolgens reageren op resultaten Hallo Hallo wijzigen.

Volg deze stappen toorun een taak die wijzigingen Hallo **TelemetryInterval** gewenst eigenschap voor Hallo van invloed op apparaten. Wanneer apparaten Hallo Hallo nieuwe ontvangt **TelemetryInterval** eigenschapswaarde, dat ze hun configuratie toosend telemetrie om de vijf seconden in plaats van elke 15 seconden wijzigen:

1. Terwijl u Hallo lijst met apparaten die niet in orde worden weergegeven in de lijst met apparaten hello, kies **Taakplanner**, klikt u vervolgens **bewerken apparaat Twin**.

1. Hallo taak aanroepen **interval voor wijzigen van telemetrie**.

1. Wijzig de waarde Hallo Hallo **gewenste eigenschap** naam **gewenste. Config.TelemetryInterval** toofive seconden.

1. Kies **Planning**.

    ![Hallo TelemetryInterval eigenschap toofive seconden wijzigen][img-change-interval]

1. U kunt Hallo voortgang van de taak Hallo op Hallo **Management taken** pagina in Hallo-portal.

> [!NOTE]
> Als u toochange een gewenste eigenschapwaarde voor een afzonderlijk apparaat wilt, gebruikt u Hallo **gewenste eigenschappen** sectie in Hallo **Apparaatdetails** deelvenster in plaats van een taak wordt uitgevoerd.

Deze taak wordt Hallo-waarde van Hallo **TelemetryInterval** eigenschap in Hallo apparaat twin gewenst voor alle apparaten die zijn geselecteerd door Hallo filter Hallo. Hallo apparaten deze waarde wordt opgehaald uit Hallo apparaat twin en hun gedrag bij te werken. Als u een apparaat worden opgehaald en verwerkt een gewenste eigenschap van een apparaat-twin, wordt Hallo overeenkomende gemelde waarde eigenschap.

## <a name="invoke-methods"></a>Aanroepmethodes

Tijdens het Hallo-taak wordt uitgevoerd, ziet u in de lijst Hallo met slechte apparaten dat al deze apparaten oude (minder dan versie 1.6) firmware hebben versies.

![Weergave Hallo firmwareversie voor Hallo slecht apparaten gerapporteerd][img-old-firmware]

Deze firmwareversie is mogelijk de hoofdoorzaak Hallo Hallo onverwachte temperatuur waarden omdat u weet dat andere apparaten in orde onlangs bijgewerkt tooversion 2.0 zijn. U kunt ingebouwde Hallo **oude firmware apparaten** filteren tooidentify alle apparaten met oude firmware-versies. Vanuit de portal Hallo kunt u alle Hallo apparaten nog steeds met oude firmwareversies vervolgens extern bijwerken:

1. Kies **opgeslagen filter openen** toodisplay een lijst met beschikbare filters. Kies vervolgens **oude firmware apparaten** tooapply Hallo filter:

    ![Hallo-lijst met filters weergeven][img-old-filter]

1. lijst met apparaten Hello wordt nu alleen apparaten met oude firmware-versies. Deze lijst bevat Hallo vijf apparaten die worden geïdentificeerd door Hallo **slecht apparaten** filteren en drie extra apparaten:

    ![Weergave Hallo gefilterde lijst met apparaten oude apparaten weergegeven][img-filtered-old-list]

1. Kies **Job Scheduler** en vervolgens **Aanroepmethode**.

1. Stel **taaknaam** te**Firmware-update tooversion 2.0**.

1. Kies **InitiateFirmwareUpdate** als Hallo **methode**.

1. Set Hallo **FwPackageUri** parameter te**https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin**.

1. Kies **Planning**. Hallo standaard is nu voor Hallo taak toorun.

    ![Taak tooupdate Hallo firmware van apparaten Hallo geselecteerd maken][img-method-update]

> [!NOTE]
> Als u tooinvoke een methode op een bepaald apparaat wilt, kies **methoden** in Hallo **Apparaatdetails** deelvenster in plaats van een taak wordt uitgevoerd.

Deze taak wordt aangeroepen Hallo **InitiateFirmwareUpdate** directe methode op alle Hallo apparaten ingeschakeld door het Hallo-filter. Apparaten onmiddellijk tooIoT Hub reageren en start vervolgens asynchroon Hallo firmware updateproces. Hallo-apparaten bieden statusinformatie over Hallo firmware updateproces via gemelde eigenschapswaarden, zoals wordt weergegeven in de volgende schermafbeeldingen Hallo. Kies Hallo **vernieuwen** pictogram tooupdate Hallo informatie in de apparaat- en lijsten Hallo:

![Takenlijst Hallo lijst firmware-update wordt uitgevoerd met][img-update-1]
![lijst met apparaten weer met de status van de firmware-update][img-update-2]
![taak lijst met Hallo firmware-update een lijst voltooid][img-update-3]

> [!NOTE]
> U kunt taken toorun plannen tijdens een onderhoudsvenster aangewezen in een productieomgeving.

## <a name="scenario-review"></a>Samenvatting van scenario

In dit scenario kunt u een mogelijk probleem met enkele van uw externe apparaten met behulp van de geschiedenis van waarschuwingen Hallo op Hallo dashboard en een filter geïdentificeerd. U vervolgens gebruikte Hallo-filter en een taak tooremotely configureren Hallo apparaten tooprovide toohelp voor meer informatie Hallo probleem opsporen. Ten slotte, gebruikt u een filter en een taak tooschedule onderhoud op Hallo van invloed op apparaten. Als u toohello dashboard terugkeert, kunt u controleren dat er niet langer zijn alle alarmen afkomstig zijn van apparaten in uw oplossing. U kunt een filter tooverify die Hallo firmware op alle Hallo-apparaten in uw oplossing up-to-date is en of er niet meer slecht apparaten:

![Filter dat laat zien dat alle apparaten bijgewerkte firmware hebben][img-updated]

![Filter dat laat zien dat alle apparaten in orde zijn][img-healthy]

## <a name="other-features"></a>Andere functies

Hallo volgende secties worden enkele aanvullende functies van Hallo vooraf geconfigureerde oplossing voor externe controle die niet als onderdeel van het vorige scenario Hallo zijn beschreven.

### <a name="customize-columns"></a>Kolommen aanpassen

U kunt aanpassen Hallo informatie wordt weergegeven in de lijst met apparaten Hallo door te kiezen **kolom editor**. U kunt kolommen die gerapporteerde eigenschaps- en tagwaarden weergeven, toevoegen en verwijderen. U kunt ook de volgorde en namen van de kolommen wijzigen:

   ![Lijst met kolommen editor bewaartermijn Hallo apparaat][img-columneditor]

### <a name="customize-hello-device-icon"></a>Pictogram Hallo aanpassen

U kunt aanpassen Hallo apparaat pictogram weergegeven in de lijst met apparaten op Hallo van Hallo **Apparaatdetails** paneel als volgt:

1. Kies Hallo pen pictogram tooopen hello **bewerken installatiekopie** Configuratiescherm voor een apparaat:

   ![De afbeeldingseditor van het apparaat openen][img-startimageedit]

1. Een nieuwe installatiekopie uploaden of gebruik een van de bestaande installatiekopieën Hallo en kies vervolgens **opslaan**:

   ![De afbeelding van het apparaat bewerken in de afbeeldingseditor][img-imageedit]

1. Hallo nu geselecteerde afbeelding wordt weergegeven in Hallo **pictogram** kolom voor Hallo-apparaat.

> [!NOTE]
> Hallo-installatiekopie is opgeslagen in blob storage. Een tag op in Hallo apparaat twin bevat een koppeling toohello installatiekopie in de blob-opslag.

### <a name="add-a-device"></a>Een apparaat toevoegen

Wanneer u Hallo vooraf geconfigureerde oplossing implementeert, worden automatisch 25 voorbeeld-apparaten die u in de lijst met Hallo apparaten zien kunt inrichten. Deze apparaten zijn *gesimuleerde apparaten* uitgevoerd in een Azure WebJob. Gesimuleerde apparaten eenvoudiger voor u tooexperiment met Hallo vooraf geconfigureerde oplossing zonder Hallo nodig toodeploy echte apparaten. Als u dat een echte toohello oplossing tooconnect wilt, raadpleegt u Hallo [verbinding maken met uw vooraf geconfigureerde oplossing voor externe controle apparaat toohello] [ lnk-connect-rm] zelfstudie.

Hallo volgende stappen ziet u hoe tooadd een gesimuleerd apparaat toohello-oplossing:

1. Navigeer terug toohello lijst met apparaten.

1. tooadd een apparaat, kies **+ een apparaat toevoegen** in Hallo linkerbenedenhoek.

   ![Een apparaat toohello vooraf geconfigureerde oplossing toevoegen][img-adddevice]

1. Kies **nieuwe toevoegen** op Hallo **gesimuleerd apparaat** tegel.

   ![Nieuwe apparaatgegevens in het dashboard instellen][img-addnew]

   In aanvulling toocreating een nieuw gesimuleerd apparaat, kunt u ook toevoegen een fysiek apparaat als u ervoor toocreate kiest een **aangepast apparaat**. toolearn meer informatie over het verbinden van fysieke apparaten toohello-oplossing, Zie [verbinding maken met uw apparaat toohello IoT Suite vooraf geconfigureerde oplossing voor externe controle][lnk-connect-rm].

1. Selecteer **Laat mij mijn eigen apparaat-id definiëren** en voer de unieke id van een apparaatnaam in, zoals **mijnapparaat_01**.

1. Kies **Maken**.

   ![Een nieuw apparaat opslaan][img-definedevice]

1. In stap 3 van **een gesimuleerd apparaat toevoegen**, kies **gedaan** tooreturn toohello lijst met apparaten.

1. U kunt uw apparaat weergeven **uitgevoerd** in de lijst met Hallo-apparaten.

    ![Nieuw apparaat weergeven in de apparatenlijst][img-runningnew]

1. U kunt ook weergeven Hallo gesimuleerde telemetrie van het nieuwe apparaat op Hallo dashboard:

    ![Telemetrie voor nieuw apparaat weergeven][img-runningnew-2]

### <a name="disable-and-delete-a-device"></a>Een apparaat uitschakelen en verwijderen

U kunt een apparaat uitschakelen en nadat het is uitgeschakeld kunt u het verwijderen:

![Een apparaat uitschakelen en verwijderen][img-disable]

### <a name="add-a-rule"></a>Een regel toevoegen

Er zijn geen regels voor het nieuwe apparaat Hallo die u zojuist hebt toegevoegd. In deze sectie voegt u een regel die een waarschuwing activeert wanneer de temperatuur Hallo gemeld door Hallo nieuwe apparaat 47 graden overschrijdt. Voordat u begint, zoals u ziet dat Hallo telemetriegeschiedenis voor nieuwe apparaat Hallo op Hallo dashboard toont Hallo apparaat temperatuur nooit meer dan 45 graden.

1. Navigeer terug toohello lijst met apparaten.

1. tooadd een regel voor Hallo-apparaat, selecteert u het nieuwe apparaat in Hallo **lijst met apparaten**, en kies vervolgens **regel toevoegen**.

1. Een regel maken die gebruikmaakt van **temperatuur** als Hallo gegevensveld gebruikt en **AlarmTemp** zoals Hallo uitvoer wanneer Hallo temperatuur 47 graden overschrijdt:

    ![Een apparaatregel toevoegen][img-adddevicerule]

1. kiest u uw wijzigingen toosave **regels opslaan en weergeven**.

1. Kies **opdrachten** in Hallo deelvenster Apparaatdetails voor het nieuwe apparaat Hallo.

    ![Een apparaatregel toevoegen][img-adddevicerule2]

1. Selecteer **ChangeSetPointTemp** van Hallo Opdrachtlijst en stel **SetPointTemp** too45. Kies vervolgens **Opdracht verzenden**:

    ![Een apparaatregel toevoegen][img-adddevicerule3]

1. Navigeer terug toohello dashboard. Na korte tijd, ziet u een nieuwe vermelding in Hallo **geschiedenis van waarschuwingen** deelvenster wanneer Hallo temperatuur gemeld door het nieuwe apparaat Hallo-47 graden overschrijdt:

    ![Een apparaatregel toevoegen][img-adddevicerule4]

1. U kunt bekijken en bewerken van alle regels op Hallo **regels** pagina van Hallo dashboard:

    ![Lijst met apparaatregels][img-rules]

1. U kunt bekijken en bewerken van alle Hallo-acties die kunnen worden uitgevoerd in reactie tooa regel op Hallo **acties** pagina van Hallo dashboard:

    ![Lijst met apparaatacties][img-actions]

> [!NOTE]
> Het is mogelijk toodefine acties die een e-mailbericht kunnen verzenden of SMS in antwoord tooa regel of integreren met een line-of-business-systeem via een [logische App][lnk-logic-apps]. Zie voor meer informatie, Hallo [tooyour van logische App verbinding maken met Azure IoT Suite Remote Monitoring vooraf geconfigureerde oplossing][lnk-logicapptutorial].

### <a name="manage-filters"></a>Filters beheren

In de lijst met apparaten van hello, kunt u maken, opslaan en laden van filters toodisplay een aangepaste lijst met apparaten verbonden tooyour hub. een filter toocreate:

1. Kies Hallo bewerken filterpictogram boven Hallo-lijst van apparaten:

    ![Open Hallo filter-editor][img-editfiltericon]

1. In Hallo **Filter editor**, Hallo velden, operators en waarden toofilter Hallo apparatenlijst toevoegen. U kunt meerdere componenten toorefine uw filter toevoegen. Kies **Filter** tooapply Hallo filter:

    ![Een filter maken][img-filtereditor]

1. In dit voorbeeld wordt Hallo lijst gefilterd op fabrikant en het modelnummer:

    ![Gefilterde lijst][img-filterelist]

1. toosave uw filter met de naam van een aangepaste kiezen Hallo **opslaan als** pictogram:

    ![Een filter opslaan][img-savefilter]

1. tooreapply een filter dat u eerder hebt opgeslagen, kies Hallo **opgeslagen filter openen** pictogram:

    ![Een filter openen][img-openfilter]

U kunt filters maken op basis van apparaat-id, apparaatstatus gewenste eigenschappen, gerapporteerde eigenschappen en tags. U uw eigen aangepaste labels tooa apparaat toevoegen in Hallo **labels** sectie Hallo **Apparaatdetails** deelvenster of een taak tooupdate labels worden uitgevoerd op meerdere apparaten.

> [!NOTE]
> In Hallo **Filter editor**, kunt u Hallo **weergave Geavanceerd** tooedit Hallo querytekst rechtstreeks.

### <a name="commands"></a>Opdrachten

Van Hallo **Apparaatdetails** Configuratiescherm kunt u opdrachten toohello apparaat verzenden. Wanneer een apparaat eerst wordt gestart, stuurt informatie over het Hallo-opdrachten dat het toohello-oplossing ondersteunt. Zie voor een beschrijving van Hallo verschillen tussen opdrachten en -methoden [Azure IoT Hub cloud-naar-apparaat opties][lnk-c2d-guidance].

1. Kies **opdrachten** in Hallo **Apparaatdetails** Configuratiescherm voor het geselecteerde apparaat Hallo:

   ![Apparaatopdrachten in het dashboard][img-devicecommands]

1. Selecteer **PingDevice** uit Hallo Opdrachtlijst.

1. Kies **Opdracht verzenden**.

1. U kunt de status van de Hallo Hallo-opdracht in de opdrachtgeschiedenis Hallo kunt zien.

   ![Opdrachtstatus in het dashboard][img-pingcommand]

Hallo oplossing houdt Hallo status van elke opdracht die worden verzonden. In eerste instantie Hallo resultaat is **in behandeling**. Wanneer Hallo apparaat meldt dat het Hallo-opdracht heeft uitgevoerd, Hallo resultaat te ingesteld**geslaagd**.

## <a name="behind-hello-scenes"></a>Achter de schermen Hallo

Wanneer u een vooraf geconfigureerde oplossing implementeert, maakt Hallo implementatieproces meerdere resources in hello Azure-abonnement u hebt geselecteerd. U kunt deze resources weergeven in hello Azure [portal][lnk-portal]. Hallo-implementatieproces maakt een **resourcegroep** met een naam op basis van Hallo-naam die u voor uw vooraf geconfigureerde oplossing kiest:

![Vooraf geconfigureerde oplossing in hello Azure-portal][img-portal]

U kunt instellingen Hallo van elke resource weergeven door deze te selecteren in lijst van resources in de resourcegroep Hallo Hallo.

U kunt ook de broncode Hallo voor Hallo vooraf geconfigureerde oplossing weergeven. Hallo voor externe controle van de broncode van de vooraf geconfigureerde oplossing is in Hallo [azure-iot-remote-monitoring] [ lnk-rmgithub] GitHub-opslagplaats:

* Hallo **DeviceAdministration** map bevat de broncode Hallo voor Hallo-dashboard.
* Hallo **Simulator** map bevat de broncode Hallo voor Hallo gesimuleerde apparaat.
* Hallo **EventProcessor** map bevat de broncode Hallo voor Hallo back-endproces dat Hallo binnenkomende telemetrie verwerkt.

Wanneer u klaar bent, kunt u Hallo vooraf geconfigureerde oplossing verwijderen uit uw Azure-abonnement op Hallo [azureiotsuite.com] [ lnk-azureiotsuite] site. Deze site kunt u alle resources die zijn ingericht toen u Hallo vooraf geconfigureerde oplossing maakte Hallo tooeasily-verwijderen.

> [!NOTE]
> tooensure u Alles verwijderen gerelateerde toohello vooraf geconfigureerde oplossing, te verwijderen op Hallo [azureiotsuite.com] [ lnk-azureiotsuite] site en het Hallo-resourcegroep in Hallo portal niet verwijderen.

## <a name="next-steps"></a>Volgende stappen

Nu dat u een werkende vooraf geconfigureerde oplossing hebt geïmplementeerd, kunt u blijven aan de slag met IoT Suite door te lezen Hallo artikelen te volgen:

* [Walkthrough over de vooraf geconfigureerde oplossing voor externe bewaking][lnk-rm-walkthrough]
* [Verbinding maken met uw apparaat toohello vooraf geconfigureerde oplossing voor externe controle][lnk-connect-rm]
* [Machtigingen op Hallo azureiotsuite.com site][lnk-permissions]

[img-launch-solution]: media/iot-suite-getstarted-preconfigured-solutions/launch.png
[img-dashboard]: media/iot-suite-getstarted-preconfigured-solutions/dashboard.png
[img-menu]: media/iot-suite-getstarted-preconfigured-solutions/menu.png
[img-devicelist]: media/iot-suite-getstarted-preconfigured-solutions/devicelist.png
[img-alarms]: media/iot-suite-getstarted-preconfigured-solutions/alarms.png
[img-devicedetails]: media/iot-suite-getstarted-preconfigured-solutions/devicedetails.png
[img-devicecommands]: media/iot-suite-getstarted-preconfigured-solutions/devicecommands.png
[img-pingcommand]: media/iot-suite-getstarted-preconfigured-solutions/pingcommand.png
[img-adddevice]: media/iot-suite-getstarted-preconfigured-solutions/adddevice.png
[img-addnew]: media/iot-suite-getstarted-preconfigured-solutions/addnew.png
[img-definedevice]: media/iot-suite-getstarted-preconfigured-solutions/definedevice.png
[img-runningnew]: media/iot-suite-getstarted-preconfigured-solutions/runningnew.png
[img-runningnew-2]: media/iot-suite-getstarted-preconfigured-solutions/runningnew2.png
[img-rules]: media/iot-suite-getstarted-preconfigured-solutions/rules.png
[img-adddevicerule]: media/iot-suite-getstarted-preconfigured-solutions/addrule.png
[img-adddevicerule2]: media/iot-suite-getstarted-preconfigured-solutions/addrule2.png
[img-adddevicerule3]: media/iot-suite-getstarted-preconfigured-solutions/addrule3.png
[img-adddevicerule4]: media/iot-suite-getstarted-preconfigured-solutions/addrule4.png
[img-actions]: media/iot-suite-getstarted-preconfigured-solutions/actions.png
[img-portal]: media/iot-suite-getstarted-preconfigured-solutions/portal.png
[img-disable]: media/iot-suite-getstarted-preconfigured-solutions/solutionportal_08.png
[img-columneditor]: media/iot-suite-getstarted-preconfigured-solutions/columneditor.png
[img-startimageedit]: media/iot-suite-getstarted-preconfigured-solutions/imagedit1.png
[img-imageedit]: media/iot-suite-getstarted-preconfigured-solutions/imagedit2.png
[img-editfiltericon]: media/iot-suite-getstarted-preconfigured-solutions/editfiltericon.png
[img-filtereditor]: media/iot-suite-getstarted-preconfigured-solutions/filtereditor.png
[img-filterelist]: media/iot-suite-getstarted-preconfigured-solutions/filteredlist.png
[img-savefilter]: media/iot-suite-getstarted-preconfigured-solutions/savefilter.png
[img-openfilter]:  media/iot-suite-getstarted-preconfigured-solutions/openfilter.png
[img-unhealthy-filter]: media/iot-suite-getstarted-preconfigured-solutions/unhealthyfilter.png
[img-filtered-unhealthy-list]: media/iot-suite-getstarted-preconfigured-solutions/unhealthylist.png
[img-change-interval]: media/iot-suite-getstarted-preconfigured-solutions/changeinterval.png
[img-old-firmware]: media/iot-suite-getstarted-preconfigured-solutions/noticeold.png
[img-old-filter]: media/iot-suite-getstarted-preconfigured-solutions/oldfilter.png
[img-filtered-old-list]: media/iot-suite-getstarted-preconfigured-solutions/oldlist.png
[img-method-update]: media/iot-suite-getstarted-preconfigured-solutions/methodupdate.png
[img-update-1]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate1.png
[img-update-2]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate2.png
[img-update-3]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate3.png
[img-updated]: media/iot-suite-getstarted-preconfigured-solutions/updated.png
[img-healthy]: media/iot-suite-getstarted-preconfigured-solutions/healthy.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-logic-apps]: https://azure.microsoft.com/documentation/services/app-service/logic/
[lnk-portal]: http://portal.azure.com/
[lnk-rmgithub]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-logicapptutorial]: iot-suite-logic-apps-tutorial.md
[lnk-rm-walkthrough]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-connect-rm]: iot-suite-connecting-devices.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-faq]: iot-suite-faq.md