---
featureFlags: usabilla
title: 'Verbinding maken met frambozen Pi (knooppunt) tooAzure IoT - les 2: apparaat registreren | Microsoft Docs'
description: Een resourcegroep maken, een Azure IoT hub maken en registreren Pi in Hallo id-register IoT Hub met Azure CLI.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: verbinding maken Raspberry pi cloud, pi-cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 736215b6-e7e4-46f9-af30-0ded9ffa5204
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 97533298d52d1187c49a4c35ddda922d6e45c87d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-raspberry-pi-3"></a>Het maken van uw IoT-hub en frambozen Pi 3 registreren
## <a name="what-you-will-do"></a>Wat u doet
* Maak een resourcegroep.
* Uw Azure-IoT-hub in de resourcegroep Hallo maken.
* Frambozen Pi 3 toohello Azure IoT hub toevoegen met behulp van hello Azure-opdrachtregelinterface (Azure CLI).

Wanneer u Azure CLI tooadd Pi tooyour iothub, genereert Hallo-service een sleutel voor Pi tooauthenticate met Hallo-service. Als u problemen hebt, zoeken naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>Wat u leert
In dit artikel leert u het:
* Hoe toouse Azure CLI toocreate een IoT-hub
* Hoe toocreate een apparaat-id voor Pi in uw IoT-hub

## <a name="what-you-need"></a>Wat u nodig hebt
* Een Azure-account
* Een Mac- of een computer met Windows Hello Azure CLI is geïnstalleerd

## <a name="create-your-iot-hub"></a>Maken van uw IoT-hub
Azure IoT-Hub kunt u verbinding maken, bewaken en beheren van miljoenen IoT activa. toocreate uw IoT-hub als volgt te werk:

1. Meld u aan tooyour Azure-account door het uitvoeren van de volgende opdracht Hallo:

   ```bash
   az login
   ```

   Alle beschikbare abonnementen worden weergegeven na een geslaagde aanmelden.

2. Hallo standaardabonnement die u door het uitvoeren van de volgende opdracht Hallo toouse wilt instellen:

   ```bash
   az account set --subscription {subscription id or name}
   ```

   `subscription ID or name`kunt u vinden in de uitvoer van Hallo Hallo `az login` of Hallo `az account list` opdracht.

3. Hallo-provider door het uitvoeren van de volgende opdracht Hallo registreren. Resourceproviders zijn services die bronnen voor uw toepassing bieden. Voordat u Azure-resource die provider aanbiedingen Hallo Hallo kunt implementeren, moet u Hallo provider registreren.

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. Maak een resourcegroep met de naam iot-sample in de regio VS-West Hallo door het uitvoeren van de volgende opdracht Hallo:

   ```bash
   az group create --name iot-sample --location westus
   ```

   `westus`Hallo locatie maken van de resourcegroep is. Als u wilt dat toouse een andere locatie, kunt u uitvoeren `az account list-locations -o table` toosee alle Hallo locaties Azure ondersteunt.
 
5. Een iothub in Hallo iot-sample resourcegroep maken door het uitvoeren van de volgende opdracht Hallo:

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

   Hallo hulpprogramma maakt standaard een IoT-Hub in de gratis prijscategorie Hallo. Zie voor meer informatie [prijzen van Azure IoT Hub](https://azure.microsoft.com/pricing/details/iot-hub/).

> [!NOTE] 
> Hallo-naam van uw IoT-hub moet wereldwijd uniek zijn. U kunt slechts één F1-editie van Azure IoT Hub maken onder uw Azure-abonnement.

## <a name="register-pi-in-your-iot-hub"></a>Pi registreren in uw IoT-hub
Elk apparaat dat berichten tooyour iothub verzendt en ontvangt berichten van uw IoT-hub moet zijn geregistreerd met een unieke ID. U uw Pi tooregister Azure CLI gebruiken en maken van een zelfondertekend X.509-certificaat voor verificatie van apparaten.

Hallo volgende opdracht uitvoeren:

```bash
# For Windows command prompt
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir %USERPROFILE%\.iot-hub-getting-started
 
# For macOS or Ubuntu
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir ~/.iot-hub-getting-started
```

## <a name="summary"></a>Samenvatting
U hebt een IoT-hub gemaakt en geregistreerd Pi met een apparaat-id in uw IoT-hub. U bent klaar toolearn hoe toosend uit Pi tooyour iothub berichten.

## <a name="next-steps"></a>Volgende stappen
[Maak een Azure-functie-app en een Azure storage-account tooprocess en IoT hub berichten worden opgeslagen](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md)

