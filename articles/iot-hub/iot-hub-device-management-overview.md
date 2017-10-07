---
title: aaaDevice management met Azure IoT Hub | Microsoft Docs
description: 'Overzicht van apparaatbeheer in Azure IoT Hub: levenscyclus van bedrijfsapparaten en apparaatbeheerpatronen, zoals opnieuw opstarten, de fabrieksinstellingen herstellen, firmware bijwerken, configuratie, apparaatdubbels, query''s en taken.'
services: iot-hub
documentationcenter: 
author: bzurcher
manager: timlt
editor: 
ms.assetid: a367e715-55f6-4593-bd68-7863cbf0eb81
ms.service: iot-hub
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: briz
ms.openlocfilehash: 7e22fb6eb3c541a513b16a047c7c3ef557255532
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-device-management-with-iot-hub"></a>Overzicht van apparaatbeheer met IoT Hub
## <a name="introduction"></a>Inleiding
Azure IoT Hub biedt Hallo-onderdelen en een uitbreidbaarheidsmodel die het apparaat en oplossingen voor back-end-ontwikkelaars toobuild robuuste Apparaatbeheer. Het bereik van de apparaten van beperkte sensoren en één doeleinde microcontrollers, toopowerful gateways die communicatie voor groepen van apparaten te routeren.  Bovendien verschillen Hallo gebruiksvoorbeelden en vereisten voor de IoT-operators aanzienlijk tussen branches.  Apparaatbeheer met IoT Hub biedt ondanks deze afwijking Hallo mogelijkheden, patronen en bibliotheken toocater tooa diverse codeset van apparaten en eindgebruikers.

Een essentieel onderdeel van het maken van een geslaagde enterprise IoT-oplossing is tooprovide een strategie voor hoe operators Hallo voortdurend beheer van hun verzameling apparaten verwerken. IoT-operators vereisen eenvoudige en betrouwbare hulpprogramma's en toepassingen waarmee ze toofocus op Hallo meer strategische aspecten van hun werk. Dit artikel bevat:

* Een kort overzicht van Azure IoT Hub benadering toodevice management.
* Een beschrijving van de algemene principes van apparaatbeheer.
* Een beschrijving van de levenscyclus van Hallo-apparaten.
* Een overzicht van de algemene patronen van apparaatbeheer.

## <a name="device-management-principles"></a>Principes van apparaatbeheer
IoT brengt aan een unieke set van apparaat management uitdagingen en elke oplossing bedrijfsniveau moet houden Hallo principes van de volgende:

![Afbeelding Principes van apparaatbeheer][img-dm_principles]

* **Schaal en automatisering**: IoT-oplossingen vereisen toomanage miljoenen apparaten door medewerkers van eenvoudige hulpprogramma's die u kunnen routinematige taken automatiseren en een relatief klein operations inschakelen. Dagelijkse, operators verwachten toohandle apparaatbewerkingen op afstand in bulk en tooonly worden gewaarschuwd wanneer er problemen optreden die hun directe aandacht vereisen.
* **Compatibiliteit en toegankelijkheid**: Hallo apparaatecosysteem uitzonderlijk diverse is. Beheerhulpprogramma's moet op maat gemaakte tooaccommodate een groot aantal apparaatklassen, platforms en protocollen. Operators moeten kunnen veel soorten apparaten, uiteenlopend van Hallo meest beperkte toosupport ingesloten één proces chips, toopowerful en volledig functioneel computers.
* **Contextbewustzijn**: IoT-omgevingen zijn dynamisch en veranderen voortdurend. Betrouwbaarheid van de service is cruciaal. Apparaat beheerbewerkingen moeten rekening gehouden account Hallo factoren tooensure volgen dat onderhoud uitvaltijd niet invloed hebben op essentiële zakelijke activiteiten of gevaarlijke voorwaarden maken:
    * SLA-onderhoudsvensters
    * Netwerk- en voedingsstatussen
    * Voorwaarden wanneer in gebruik
    * Geolocatie van apparaat
* **Veel functies service**: ondersteuning voor Hallo unieke werkstromen en processen van IoT operations-functies is van cruciaal belang. Hallo beheerders moet eenheid in de omschrijving werken met Hallo gegeven beperkingen van interne IT-afdelingen.  Ze moeten ook duurzame manieren toosurface realtime apparaat operations informatie toosupervisors en andere zakelijke leidinggevende rollen vinden.

## <a name="device-lifecycle"></a>Levenscyclus van apparaat
Er is een reeks fasen in het algemeen apparaten die algemene tooall enterprise IoT-projecten zijn. Er zijn vijf fasen binnen de levenscyclus van apparaten Hallo in Azure IoT:

![Hallo vijf fasen van het apparaat de levenscyclus van Azure IoT: plannen, inrichten, configureren, bewaken en buiten gebruik stellen][img-device_lifecycle]

In elk van deze vijf fasen zijn er verschillende vereisten van het apparaat operator afgehandelde tooprovide een volledige-oplossing moeten zijn:

* **Plan**: operators toocreate een apparaat metagegevens schema waarmee ze tooeasily en nauwkeurige query voor inschakelen en een doelgroep van apparaten voor bulksgewijs beheerbewerkingen. U kunt deze Apparaatmetagegevens in Hallo vorm van labels en eigenschappen Hallo apparaat twin toostore.
  
    *Meer informatie*: [aan de slag met apparaat horende][lnk-twins-getstarted], [apparaat horende begrijpen][lnk-twins-devguide], [hoe Apparaateigenschappen voor twin toouse][lnk-twin-properties].
* **Inrichten**: veilig inrichten van nieuwe apparaten tooIoT Hub en schakel operators tooimmediately apparaatmogelijkheden detecteren.  Hallo Iothub identiteit register toocreate flexibele apparaat-id's en referenties gebruiken en deze bewerking niet uitvoeren in bulk met behulp van een taak. Maak apparaten tooreport hun mogelijkheden en voorwaarden via apparaateigenschappen in Hallo apparaat twin.
  
    *Meer informatie*: [apparaat identiteiten beheren][lnk-identity-registry], [bulksgewijs beheer van apparaat-id's][lnk-bulk-identity], [Hoe toouse apparaat eigenschappen twin][lnk-twin-properties].
* **Configureer**: bulksgewijs vergemakkelijken toodevices configuratiewijzigingen en firmware-updates en tegelijkertijd zowel de status en beveiliging. Voer deze apparaatbeheerbewerkingen bulksgewijs uit met behulp van de gewenste eigenschappen of met rechtstreekse methoden en broadcast-taken.
  
    *Meer informatie*: [direct methoden gebruiken][lnk-c2d-methods], [een directe methode aangeroepen voor een apparaat][lnk-methods-devguide], [hoe Apparaateigenschappen voor twin toouse][lnk-twin-properties], [planning en broadcast taken][lnk-jobs], [taken op meerdere apparatenplannen] [lnk-jobs-devguide].
* **Monitor**: bewaken van de verzameling van algemene Apparaatstatus, Hallo status van actieve bewerkingen en waarschuwing operators tooissues die mogelijk hun aandacht vereisen.  Hallo apparaat twin tooallow apparaten tooreport realtime omstandigheden en status van update-bewerkingen toepassen. Krachtige dashboardrapporten die surface Hallo direct problemen met apparaat twin query bouwen.
  
    *Meer informatie*: [hoe toouse apparaat eigenschappen twin][lnk-twin-properties], [querytaal IoT Hub voor apparaat horende, taken en berichtroutering] [ lnk-query-language].
* **Buiten gebruik stellen**: vervangen of buiten gebruik stellen van apparaten na een storing, cyclus, upgraden of achter Hallo Hallo service levensduur.  Hallo twin toomaintain apparaat apparaatgegevens gebruiken als de fysieke apparaat hello wordt vervangen, of als het buiten gebruik gesteld gearchiveerd. Hallo id-register IoT Hub gebruiken voor het veilig intrekken van apparaat-id's en referenties.
  
    *Meer informatie*: [hoe toouse apparaat eigenschappen twin][lnk-twin-properties], [apparaat identiteiten beheren][lnk-identity-registry].

## <a name="device-management-patterns"></a>Patronen voor apparaatbeheer
IoT-Hub kunt Hallo reeks apparaat management patronen te volgen.  Hallo [apparaat management zelfstudies] [ lnk-get-started] hoe u in meer detail tooextend deze patronen toofit uw exacte scenario en hoe nieuwe patronen toodesign op basis van deze sjablonen core.

* **Opnieuw opstarten** -back-endserver voor apps Hallo informeert Hallo apparaat via een directe methode dat wordt is opnieuw opgestart.  Hallo-apparaat gebruikt Hallo gerapporteerd eigenschappen tooupdate Hallo opnieuw opstarten status van Hallo-apparaat.
  
    ![Afbeelding van het opstartpatroon van apparaatbeheer][img-reboot_pattern]
* **Fabrieksinstellingen terugzetten** -back-endserver voor apps Hallo informeert Hallo apparaat via een directe methode dat deze fabrieksinstellingen is gestart.  Hallo-apparaat gebruikt Hallo gerapporteerd eigenschappen tooupdate Hallo de fabrieksinstellingen van status van Hallo-apparaat.
  
    ![Afbeelding van het patroon van herstel naar fabrieksinstellingen voor apparaatbeheer][img-facreset_pattern]
* **Configuratie** -Hallo back-endserver voor apps Hallo gewenst eigenschappen tooconfigure software die wordt uitgevoerd op Hallo-apparaat gebruikt.  Hallo-apparaat gebruikt Hallo gerapporteerd eigenschappen tooupdate configuratiestatus van Hallo-apparaat.
  
    ![Afbeelding van het configuratiepatroon van apparaatbeheer][img-config_pattern]
* **Firmware-Update** -back-endserver voor apps Hallo informeert Hallo apparaat via een directe methode dat deze een firmware-update is gestart.  Hallo apparaat start een proces toodownload Hallo firmware-installatiekopie, Hallo firmware-installatiekopie toe te passen en ten slotte verbinding toohello service IoT Hub.  In de gehele proces hello gerapporteerd Hallo apparaat gebruikt Hallo eigenschappen tooupdate Hallo voortgang en status van het Hallo-apparaat.
  
    ![Afbeelding van het firmware-updatepatroon van apparaatbeheer][img-fwupdate_pattern]
* **Rapportage van de voortgang en status** -Hallo back-end oplossing apparaat twin query's uitvoert in een reeks apparaten, tooreport op Hallo status en voortgang van de acties die worden uitgevoerd op Hallo-apparaten.
  
    ![Afbeelding van het proces- en statuspatroon van apparaatbeheerrapportage][img-report_progress_pattern]

## <a name="next-steps"></a>Volgende stappen
Hallo-mogelijkheden, patronen en codebibliotheken met IoT Hub voor Apparaatbeheer, kunnen u toocreate IoT-toepassingen die voldoen aan vereisten voor enterprise IoT-operator in elke fase van de levenscyclus van apparaat.

toocontinue leren over Hallo beheerfuncties voor apparaten in IoT-Hub, Zie Hallo [aan de slag met Apparaatbeheer] [ lnk-get-started] zelfstudie.

<!-- Images and links -->
[img-dm_principles]: media/iot-hub-device-management-overview/image4.png
[img-device_lifecycle]: media/iot-hub-device-management-overview/image5.png
[img-config_pattern]: media/iot-hub-device-management-overview/configuration-pattern.png
[img-facreset_pattern]: media/iot-hub-device-management-overview/facreset-pattern.png
[img-fwupdate_pattern]: media/iot-hub-device-management-overview/fwupdate-pattern.png
[img-reboot_pattern]: media/iot-hub-device-management-overview/reboot-pattern.png
[img-report_progress_pattern]: media/iot-hub-device-management-overview/report-progress-pattern.png

[lnk-twins-devguide]: iot-hub-devguide-device-twins.md
[lnk-get-started]: iot-hub-node-node-device-management-get-started.md
[lnk-twins-getstarted]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-properties]: iot-hub-node-node-twin-how-to-configure.md
[lnk-hub-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-identity-registry]: iot-hub-devguide-identity-registry.md
[lnk-bulk-identity]: iot-hub-bulk-identity-mgmt.md
[lnk-query-language]: iot-hub-devguide-query-language.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-methods-devguide]: iot-hub-devguide-direct-methods.md
[lnk-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-jobs-devguide]: iot-hub-devguide-jobs.md
