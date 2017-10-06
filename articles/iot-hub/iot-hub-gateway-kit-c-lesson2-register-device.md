---
title: 'SensorTag apparaat & Azure IoT Gateway - les 2: apparaat registreren | Microsoft Docs'
description: 
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Azure iothub, internet van dingen cloud azure iothub maken apparaat, ti sensortag, ti uitschakelen
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 2c18f5ae-e39a-48ae-a9fe-04bb595740a0
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5d2322268aa18f52f60c2833778323773ac4eec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-azure-iot-hub-and-register-your-device"></a>Maken van uw Azure-IoT-hub en Registreer uw apparaat

## <a name="what-you-will-do"></a>Wat u doet

- Een resourcegroep maken
- Uw eerste IoT-hub maken
- Registreer uw apparaat in uw iothub met behulp van hello Azure CLI. 

Wanneer u uw apparaat in uw IoT-hub registreren, genereert Hallo service Azure IoT Hub een sleutel voor uw apparaat toouse tooauthenticate met Hallo-service. 

Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Wat u leert

In deze les leert u het:

- Hoe toouse hello Azure CLI toocreate een IoT-hub.
- Hoe tooregister een apparaat in een IoT-hub.

## <a name="what-you-need"></a>Wat u nodig hebt

- Een actief Azure-abonnement. Als u geen Azure-account hebt, kunt u een [gratis proefaccount voor Azure](http://azure.microsoft.com/pricing/free-trial/) over een paar minuten.
- U hebt hello die Azure CLI is geïnstalleerd.

## <a name="create-an-iot-hub"></a>Een IoT Hub maken

een IoT-hub toocreate als volgt te werk:

1. Meld u aan tooyour Azure-account door het uitvoeren van de volgende opdracht Hallo:

   ```bash
   az login
   ```

   Alle beschikbare abonnementen worden weergegeven na een geslaagde aanmelden.

2. Hallo standaard Azure-abonnement dat u door het uitvoeren van de volgende opdracht Hallo toouse wilt instellen:

   ```bash
   az account set --subscription {subscription id or name}
   ```

   `subscription ID or name`kunt u vinden in de uitvoer van Hallo Hallo `az login` of Hallo `az account list` opdracht.

3. Hallo-provider door het uitvoeren van de volgende opdracht Hallo registreren. Resourceproviders zijn services die bronnen voor uw toepassing bieden. Voordat u Azure-resource die provider aanbiedingen Hallo Hallo kunt implementeren, moet u Hallo provider registreren.

   ```bash
   az provider register -n "Microsoft.Devices"
   ```

4. Maak een resourcegroep met de naam `iot-gateway` in de regio VS-West Hallo door het uitvoeren van de volgende opdracht Hallo:

   ```bash
   az group create --name iot-gateway --location westus
   ```
   
   `westus`Hallo locatie maken van de resourcegroep is. Als u wilt dat toouse een andere locatie, kunt u uitvoeren `az account list-locations -o table` toosee alle Hallo locaties Azure ondersteunt.

5. Maken van een IoT-hub in Hallo `iot-gateway` resourcegroep door het uitvoeren van de volgende opdracht Hallo:

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-gateway
   ```

Hallo hulpprogramma maakt standaard een IoT-Hub in de gratis prijscategorie Hallo. Zie voor meer informatie [prijzen van Azure IoT Hub](https://azure.microsoft.com/pricing/details/iot-hub/).

> [!NOTE]
> Hallo-naam van uw IoT-hub moet wereldwijd uniek zijn. U kunt slechts één F1-editie van Azure Iot Hub maken onder uw Azure-abonnement.

## <a name="register-your-device-in-your-iot-hub"></a>Registreer uw apparaat bij uw IoT-hub

Elk apparaat dat berichten tooyour iothub verzendt en ontvangt berichten van uw IoT-hub moet zijn geregistreerd met een unieke ID.
Registreer uw apparaat in uw IoT-hub door met volgende opdracht:

```bash
az iot device create --device-id mydevice --hub-name {my hub name} --resource-group iot-gateway
```

## <a name="summary"></a>Samenvatting

U hebt een IoT-hub gemaakt en het logische apparaat geregistreerd bij een apparaat-id in uw IoT-hub. U bent klaar toolearn hoe tooconfigure en voer een gateway toepassing toosend voorbeeldgegevens van uw fysieke apparaat tooyour IoT-hub in Hallo cloud.

## <a name="next-steps"></a>Volgende stappen
[Configureren en uitvoeren van een voorbeeldapp uitschakelen](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)