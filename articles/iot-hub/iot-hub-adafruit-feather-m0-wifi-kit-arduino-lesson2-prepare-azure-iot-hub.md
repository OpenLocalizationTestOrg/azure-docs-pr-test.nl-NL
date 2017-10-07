---
title: 'Verbinding maken met Arduino tooAzure IoT - les 2: apparaat registreren | Microsoft Docs'
description: Een resourcegroep maken, een Azure IoT hub maken en registreren Adafruit Doezelaar M0 Wi-Fi in hello Azure IoT hub met behulp van hello Azure CLI.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: verbinding maken met arduino toocloud, azure iothub, internet der dingen cloud, azure iothub apparaat, arduino cloud maken
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 5edc690b-7a1d-4ebc-b011-ff27bfffe6e8
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ca362f9c143dd3a98bf47a66b63a9725a0ffc2d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-your-adafruit-feather-m0-wifi-arduino-board"></a>Het maken van uw IoT-hub en het mededelingenbord Adafruit Doezelaar M0 Wi-Fi Arduino registreren

## <a name="what-you-will-do"></a>Wat u doet
* Maak een resourcegroep.
* Uw Azure-IoT-hub in de resourcegroep Hallo maken.
* Uw Arduino mededelingenbord toohello Azure IoT hub toevoegen met behulp van hello Azure-opdrachtregelinterface (Azure CLI).

Wanneer u uw Arduino mededelingenbord tooyour IoT-hub hello Azure CLI tooadd opgeeft, genereert Hallo-service een sleutel voor uw Arduino mededelingenbord tooauthenticate met Hallo-service. Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina][troubleshoot].

## <a name="what-you-will-learn"></a>Wat u leert
In dit artikel leert u het:
* Hoe toouse hello Azure CLI toocreate een IoT-hub.
* Hoe een apparaat-id voor uw Arduino toocreate board in uw IoT-hub.

## <a name="what-you-need"></a>Wat u nodig hebt
* Een Azure-account
* De installatie van een computer met hello Azure CLI

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
> Hallo-naam van uw IoT-hub moet wereldwijd uniek zijn.
> U kunt slechts één F1-editie van Azure IoT Hub maken onder uw Azure-abonnement.

## <a name="register-your-arduino-board-in-your-iot-hub"></a>Het mededelingenbord Arduino registreren in uw IoT-hub
Elk apparaat dat berichten tooyour iothub verzendt en ontvangt berichten van uw IoT-hub moet zijn geregistreerd met een unieke ID.

Het mededelingenbord Arduino in uw IoT-hub registreren door de volgende opdracht uitvoeren:

```bash
az iot device create --device-id mym0wifi --hub-name {my hub name}
```

## <a name="summary"></a>Samenvatting
U hebt een IoT-hub gemaakt en het mededelingenbord Arduino geregistreerd met een apparaat-id in uw IoT-hub. U bent klaar toolearn hoe toosend berichten uit uw Arduino mededelingenbord tooyour iothub.

## <a name="next-steps"></a>Volgende stappen
[Maak een Azure-functie-app en een Azure Storage-account tooprocess en store IoT-hub berichten][process-and-store-iot-hub-messages].


<!-- Images and links -->

[troubleshoot]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md