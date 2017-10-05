---
featureFlags: usabilla
title: 'Frambozen Pi (knooppunt) verbinden met Azure IoT - les 2: apparaat registreren | Microsoft Docs'
description: Een resourcegroep maken, een Azure IoT hub maken en Pi registreren in het identiteitenregister van IoT Hub met behulp van Azure CLI.
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
ms.openlocfilehash: 774f9356d7a11b2c61905ada75bed92d44e5fc0c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-iot-hub-and-register-raspberry-pi-3"></a>Het maken van uw IoT-hub en frambozen Pi 3 registreren
## <a name="what-you-will-do"></a>Wat u doet
* Maak een resourcegroep.
* Uw Azure-IoT-hub in de resourcegroep maken.
* Frambozen Pi 3 toevoegen aan de Azure IoT hub met behulp van de Azure-opdrachtregelinterface (Azure CLI).

Wanneer u Azure CLI Pi toevoegen aan uw IoT-hub, genereert de service een sleutel voor Pi voor verificatie met de service. Als u problemen hebt, oplossingen zoeken op de [probleemoplossing pagina](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>Wat u leert
In dit artikel leert u het:
* Het gebruik van Azure CLI voor een iothub maken
* Het maken van een apparaat-id voor Pi in uw IoT-hub

## <a name="what-you-need"></a>Wat u nodig hebt
* Een Azure-account
* Een Mac- of een Windows-computer met de Azure CLI geïnstalleerd

## <a name="create-your-iot-hub"></a>Maken van uw IoT-hub
Azure IoT-Hub kunt u verbinding maken, bewaken en beheren van miljoenen IoT activa. Volg deze stappen voor het maken van uw IoT-hub:

1. Meld u aan bij uw Azure-account met de volgende opdracht:

   ```bash
   az login
   ```

   Alle beschikbare abonnementen worden weergegeven na een geslaagde aanmelden.

2. Stel de standaardabonnement dat u gebruiken wilt met de volgende opdracht:

   ```bash
   az account set --subscription {subscription id or name}
   ```

   `subscription ID or name`kunt u vinden in de uitvoer van de `az login` of de `az account list` opdracht.

3. Registreer de provider door de volgende opdracht uit te voeren. Resourceproviders zijn services die bronnen voor uw toepassing bieden. Voordat u de Azure-resource die de provider biedt kunt implementeren, moet u de provider registreren.

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. Maak een resourcegroep met de iot-voorbeeld in de regio VS-West naam door de volgende opdracht uit te voeren:

   ```bash
   az group create --name iot-sample --location westus
   ```

   `westus`is de locatie die u maakt de resourcegroep. Als u gebruiken van een andere locatie wilt, kunt u uitvoeren `az account list-locations -o table` voor een overzicht van alle locaties Azure ondersteunt.
 
5. Een iothub in de iot-sample resourcegroep maken met de volgende opdracht:

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

   Het hulpprogramma maakt standaard een IoT-Hub in de prijscategorie gratis. Zie voor meer informatie [prijzen van Azure IoT Hub](https://azure.microsoft.com/pricing/details/iot-hub/).

> [!NOTE] 
> De naam van uw IoT-hub moet wereldwijd uniek zijn. U kunt slechts één F1-editie van Azure IoT Hub maken onder uw Azure-abonnement.

## <a name="register-pi-in-your-iot-hub"></a>Pi registreren in uw IoT-hub
Elk apparaat dat berichten naar uw IoT-hub verzendt en ontvangt berichten van uw IoT-hub moet zijn geregistreerd met een unieke ID. U kunt Azure CLI uw Pi registreren en maak een zelfondertekend X.509-certificaat voor verificatie van apparaten.

Voer de volgende opdracht uit:

```bash
# For Windows command prompt
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir %USERPROFILE%\.iot-hub-getting-started
 
# For macOS or Ubuntu
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir ~/.iot-hub-getting-started
```

## <a name="summary"></a>Samenvatting
U hebt een IoT-hub gemaakt en geregistreerd Pi met een apparaat-id in uw IoT-hub. U kunt meer informatie over het verzenden van berichten vanaf Pi naar uw IoT-hub.

## <a name="next-steps"></a>Volgende stappen
[Maak een Azure-functie-app en een Azure storage-account om te verwerken en IoT hub berichten opslaan](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md)

