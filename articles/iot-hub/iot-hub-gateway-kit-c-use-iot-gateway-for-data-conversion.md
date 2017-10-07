---
title: conversie van aaaData bij IoT gateway met Azure IoT rand | Microsoft Docs
description: Gebruik IoT gateway tooconvert Hallo-indeling van sensorgegevens via een aangepaste module op basis van Azure IoT rand.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: conversie van IOT gateway, iot gateway gegevenstransformatie
ms.assetid: 75f2573d-500b-4405-bff7-61021c4c3500
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: ae94b1f96f36dfcb4f77fadc0ece3cff3d0bba91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-iot-gateway-for-sensor-data-transformation-with-azure-iot-edge"></a>Gebruik IoT gateway voor gegevenstransformatie sensor met Azure IoT rand

> [!NOTE]
> Voordat u deze zelfstudie begint, zorg er dan voor dat u bent voltooide Hallo uitkomsten in de juiste volgorde te volgen:
> * [Intel NUC instellen als IoT-gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
> * [Gebruik IoT gateway tooconnect dingen toohello cloud - SensorTag tooAzure IoT-Hub](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

Een doel van een Iot-gateway is tooprocess verzamelde gegevens voordat u deze toohello cloud verzendt. Azure IoT-rand introduceert modules die gemaakt en gemonteerd tooform Hallo gegevensverwerking werkstroom worden kunnen. Een module een bericht ontvangt, voert een bepaalde actie op deze en vervolgens voor andere modules tooprocess op verplaatsen.

## <a name="what-you-learn"></a>Wat u leert

U leert hoe een module tooconvert toocreate van berichten van Hallo SensorTag naar een andere indeling.

## <a name="what-you-do"></a>Wat u doet

* Maak een module tooconvert een ontvangen bericht naar Hallo .json-indeling.
* Hallo-module niet compileren.
* Hallo module toohello uitschakelen-voorbeeldtoepassing uit Azure IoT rand toevoegen.
* Hallo-voorbeeldtoepassing uitvoeren.

## <a name="what-you-need"></a>Wat u nodig hebt

* Hallo voltooid in de reeks zelfstudies te volgen:
  * [Intel NUC instellen als IoT-gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
  * [Gebruik IoT gateway tooconnect dingen toohello cloud - SensorTag tooAzure IoT-Hub](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)
* Een SSH-client die wordt uitgevoerd op de hostcomputer. PuTTY wordt aanbevolen voor Windows. Linux- en Mac OS al worden geleverd met een SSH-client.
* Hallo IP-adres en Hallo gebruikersnaam en wachtwoord tooaccess Hallo gateway vanuit Hallo SSH-client.
* Een internetverbinding.

## <a name="create-a-module"></a>Een module maken

1. Op de hostcomputer Hallo Hallo SSH-client wordt uitgevoerd en verbinding maken met toohello IoT gateway.
1. Hallo-bronbestanden van Hallo conversie module op basis van GitHub toohello-basismappen van Hallo IoT gateway door het uitvoeren van de volgende opdrachten Hallo klonen:

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-c-intel-nuc-gateway-customized-module.git
   ```

   Dit is een systeemeigen Azure rand module, geschreven in Hallo programmeertaal. Hallo-indeling van ontvangen berichten converteert Hallo module naar Hallo volgt:

   ```json
   {"deviceId": "Intel NUC Gateway", "messageId": 0, "temperature": 0.0}
   ```

## <a name="compile-hello-module"></a>Hallo-module niet compileren

toocompile Hallo-module, Hallo volgende opdrachten uitvoeren:

```bash
cd iot-hub-c-intel-nuc-gateway-customized-module/my_module
# change hello build script runnable
chmod 777 build.sh
# remove hello invalid windows character
sed -i -e "s/\r$//" build.sh
# run hello build shell script
./build.sh
```

U krijgt een `libmy_module.so` bestand nadat Hallo compileren is voltooid. Noteer Hallo absolute pad van dit bestand.

## <a name="add-hello-module-toohello-ble-sample-application"></a>Hallo module toohello uitschakelen voorbeeld van een toepassing toevoegen

1. Map met voorbeelden toohello gaan door het uitvoeren van de volgende opdracht Hallo:

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples
   ```

1. Hallo-configuratiebestand openen door het uitvoeren van de volgende opdracht Hallo:

   ```bash
   vi ble_gateway.json
   ```

1. Een module toevoegen door het invoegen van de volgende code toohello Hallo `modules` sectie.

   ```json
   {
       "name": "MyModule",
       "loader": {
           "name": "native",
           "entrypoint":{
               "module.path": "[Your libmy_module.so path]"
               }
            },
        "args": null
    },
    ```

1. Vervang `[Your libmy_module.so path]` in code met het absolute pad van Hallo libmy_module.so Hallo Hallo ' bestand.
1. Vervang de code Hallo in Hallo `links` sectie Hello volgt:

   ```json
   {
       "source": "SensorTag",
       "sink": "MyModule"
   },
   {
       "source": "MyModule",
       "sink": "mapping"
   }
   ```

1. Druk op `ESC`, en typ vervolgens `:wq` toosave Hallo-bestand.

## <a name="run-hello-sample-application"></a>Hallo-voorbeeldtoepassing uitvoeren

1. Hallo SensorTag inschakelen.
1. Hallo SSL_CERT_FILE omgevingsvariabele door het uitvoeren van de volgende opdracht Hallo instellen:

   ```bash
   export SSL_CERT_FILE=/etc/ssl/certs/ca-certificates.crt
   ```

1. Voer Hallo voorbeeldtoepassing met toegevoegde module Hallo door het uitvoeren van de volgende opdracht Hallo:

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a>Volgende stappen

U hebt gebruikt Hallo IoT gateway tooconvert Hallo-bericht van SensorTag naar Hallo .json-indeling.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
