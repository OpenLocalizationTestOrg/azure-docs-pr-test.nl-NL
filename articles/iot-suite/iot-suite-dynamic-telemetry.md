---
title: dynamische telemetrie aaaUse | Microsoft Docs
description: Volg deze zelfstudie toolearn hoe dynamische telemetrie toouse met hello Azure IoT Suite remote monitoring vooraf geconfigureerde oplossing.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 562799dc-06ea-4cdd-b822-80d1f70d2f09
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 06cb2a370b67b4950efdfa4c7d906ac92106f4a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-dynamic-telemetry-with-hello-remote-monitoring-preconfigured-solution"></a>Gebruik dynamische telemetrie Hello vooraf geconfigureerde oplossing voor externe controle

Dynamische telemetrie kunt u toovisualize alle telemetrie verzonden toohello vooraf geconfigureerde oplossing voor externe controle. Hallo gesimuleerde apparaten die met Hallo vooraf geconfigureerde oplossing implementeren verzenden temperatuur en vochtigheid telemetrie die u op Hallo dashboard visualiseren kunt. Als u bestaande gesimuleerde apparaten wilt aanpassen, nieuwe gesimuleerde apparaten maken of fysieke apparaten toohello vooraf geconfigureerde oplossing kunt u andere waarden telemetrie zoals externe temperatuur hello, RPM of windsnelheid verzenden verbinden. U kunt vervolgens visualiseren van deze extra telemetrie op Hallo-dashboard.

Deze zelfstudie wordt een eenvoudige Node.js gesimuleerd apparaat kunt u eenvoudig tooexperiment met dynamische telemetrie wijzigen.

toocomplete in deze zelfstudie hebt u nodig:

* Een actief Azure-abonnement. Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken. Zie [Gratis proefversie van Azure][lnk_free_trial] voor meer informatie.
* [Node.js] [ lnk-node] versie 0.12.x of hoger.

U kunt voltooien van deze zelfstudie op elk besturingssysteem, zoals Windows of Linux, waar u Node.js kunt installeren.

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

## <a name="add-a-telemetry-type"></a>Een type telemetrie toevoegen

de volgende stap Hallo is tooreplace Hallo telemetrie die worden gegenereerd door Hallo Node.js gesimuleerd apparaat met een nieuwe set met waarden:

1. Stop Hallo Node.js gesimuleerd apparaat door te typen **Ctrl + C** in uw opdrachtprompt of de shell.
2. Hallo remote_monitoring.js bestand ziet u Hallo basisgegevens waarden voor Hallo bestaande temperatuur en vochtigheid externe temperatuur telemetrie. Voeg een waarde basisgegevens voor **rpm** als volgt:

    ```nodejs
    // Sensors data
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    var rpm = 200;
    ```

3. Hallo Node.js gesimuleerd apparaat maakt gebruik van Hallo **generateRandomIncrement** werken in Hallo remote_monitoring.js bestand tooadd een willekeurige verhoging toohello basisgegevens waarden. Hallo willekeurige **rpm** waarde door een regel code na Hallo bestaande randomizations toe te voegen als volgt:

    ```nodejs
    temperature += generateRandomIncrement();
    externalTemperature += generateRandomIncrement();
    humidity += generateRandomIncrement();
    rpm += generateRandomIncrement();
    ```

4. Hallo nieuwe rpm waarde toohello JSON-nettolading Hallo apparaat verzendt tooIoT Hub toevoegen:

    ```nodejs
    var data = JSON.stringify({
      'DeviceID': deviceId,
      'Temperature': temperature,
      'Humidity': humidity,
      'ExternalTemperature': externalTemperature,
      'RPM': rpm
    });
    ```

5. Hallo Node.js gesimuleerd apparaat met behulp van de volgende opdracht Hallo uitvoeren:

    `node remote_monitoring.js`

6. Houd rekening met Hallo nieuw RPM telemetrie type dat wordt weergegeven in de grafiek Hallo in Hallo dashboard:

![RPM toohello dashboard toevoegen][image3]

> [!NOTE]
> U kunt toodisable moet en schakel vervolgens Hallo Node.js-apparaat op Hallo **apparaten** pagina in Hallo dashboard toosee Hallo wijziging onmiddellijk.

## <a name="customize-hello-dashboard-display"></a>Hallo-dashboard aanpassen

Hallo **apparaatgegevens** bericht metagegevens kunt opnemen over Hallo telemetrie Hallo apparaat tooIoT Hub kunt verzenden. Deze metagegevens kunt Hallo telemetrie typen Hallo apparaat verzendt opgeven. Hallo wijzigen **deviceMetaData** waarde in Hallo remote_monitoring.js bestand tooinclude een **telemetrie** definitie Hallo na **opdrachten** definitie. Hallo volgende codefragment toont Hallo **opdrachten** definition (ervoor tooadd worden een `,` na Hallo **opdrachten** definitie):

```nodejs
'Commands': [{
  'Name': 'SetTemperature',
  'Parameters': [{
    'Name': 'Temperature',
    'Type': 'double'
  }]
},
{
  'Name': 'SetHumidity',
  'Parameters': [{
    'Name': 'Humidity',
    'Type': 'double'
  }]
}],
'Telemetry': [{
  'Name': 'Temperature',
  'Type': 'double'
},
{
  'Name': 'Humidity',
  'Type': 'double'
},
{
  'Name': 'ExternalTemperature',
  'Type': 'double'
}]
```

> [!NOTE]
> Hallo-oplossing voor externe controle maakt gebruik van de definitie van een niet-hoofdlettergevoelige overeenkomst toocompare Hallo metagegevens met gegevens in de telemetriestroom Hallo.


Toevoegen van een **telemetrie** definitie zoals weergegeven in de voorgaande Hallo codefragment verandert niet Hallo gedrag van Hallo-dashboard. Hallo metagegevens kan echter ook bevatten een **DisplayName** kenmerk toocustomize Hallo weergave in Hallo-dashboard. Update Hallo **telemetrie** definitie van metagegevens zoals weergegeven in het volgende codefragment Hallo:

```nodejs
'Telemetry': [
{
  'Name': 'Temperature',
  'Type': 'double',
  'DisplayName': 'Temperature (C*)'
},
{
  'Name': 'Humidity',
  'Type': 'double',
  'DisplayName': 'Humidity (relative)'
},
{
  'Name': 'ExternalTemperature',
  'Type': 'double',
  'DisplayName': 'Outdoor Temperature (C*)'
}
]
```

Hallo volgende schermafbeelding ziet u hoe de grafieklegenda Hallo op Hallo dashboard Hiermee wijzigt u deze wijziging:

![De grafieklegenda Hallo aanpassen][image4]

> [!NOTE]
> U kunt toodisable moet en schakel vervolgens Hallo Node.js-apparaat op Hallo **apparaten** pagina in Hallo dashboard toosee Hallo wijziging onmiddellijk.

## <a name="filter-hello-telemetry-types"></a>Hallo telemetrie typen worden gefilterd

Hallo-grafiek op Hallo dashboard wordt standaard elke gegevensreeks in Hallo telemetriestroom. U kunt Hallo **apparaatgegevens** metagegevens toosuppress Hallo weergave van specifieke telemetrie typen op Hallo-grafiek. 

toomake hello grafiek weergeven alleen temperatuur en vochtigheid telemetrie, weglaten **ExternalTemperature** van Hallo **apparaatgegevens** **telemetrie** metagegevens als volgt:

```nodejs
'Telemetry': [
{
  'Name': 'Temperature',
  'Type': 'double',
  'DisplayName': 'Temperature (C*)'
},
{
  'Name': 'Humidity',
  'Type': 'double',
  'DisplayName': 'Humidity (relative)'
},
//{
//  'Name': 'ExternalTemperature',
//  'Type': 'double',
//  'DisplayName': 'Outdoor Temperature (C*)'
//}
]
```

Hallo **buiten temperatuur** niet meer weergegeven op het Hallo-grafiek:

![Filter Hallo telemetrie op Hallo-dashboard][image5]

Deze wijziging is alleen van invloed op Hallo grafiekweergave. Hallo **ExternalTemperature** gegevenswaarden nog steeds worden opgeslagen en beschikbaar gesteld voor de verwerking van de back-end.

> [!NOTE]
> U kunt toodisable moet en schakel vervolgens Hallo Node.js-apparaat op Hallo **apparaten** pagina in Hallo dashboard toosee Hallo wijziging onmiddellijk.

## <a name="handle-errors"></a>Afhandelen van fouten

Voor een toodisplay van de gegevensstroom in de grafiek hello, de **Type** in Hallo **apparaatgegevens** metagegevens moet overeenkomen met de Hallo-gegevenstype van Hallo telemetrie waarden. Bijvoorbeeld, als hello metagegevens geeft aan dat Hallo **Type** van vochtigheid gegevens is **int** en een **dubbele** is gevonden in de telemetriestroom Hallo vervolgens Hallo vochtigheid telemetrie biedt niet weergegeven op het Hallo-grafiek. Hallo echter **vochtigheid** waarden zijn nog steeds opgeslagen en beschikbaar gesteld voor de verwerking van de back-end.

## <a name="next-steps"></a>Volgende stappen

Nu dat u hebt gezien hoe dynamische telemetrie toouse, voor meer informatie over hoe Hallo vooraf oplossingen geconfigureerde gebruiken apparaatgegevens: [apparaat informatie metagegevens in Hallo externe controle vooraf geconfigureerde oplossing] [ lnk-devinfo].

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[image3]: media/iot-suite-dynamic-telemetry/image3.png
[image4]: media/iot-suite-dynamic-telemetry/image4.png
[image5]: media/iot-suite-dynamic-telemetry/image5.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
