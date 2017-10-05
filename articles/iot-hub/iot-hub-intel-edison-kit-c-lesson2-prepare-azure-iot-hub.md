---
title: 'Connect Intel Edison (C) naar Azure IoT - les 2: apparaat registreren | Microsoft Docs'
description: Een resourcegroep maken, een Azure IoT hub maken en Edison registreren in de Azure IoT hub met behulp van de Azure CLI.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: 
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 80bfc3cd-a1fc-4775-8994-d8033381dd3d
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 52e3e4734dfd2b89f79b0c66683163e69b8e5f25
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-iot-hub-and-register-intel-edison"></a>Het maken van uw IoT-hub en Intel Edison registreren
## <a name="what-you-will-do"></a>Wat u doet
* Maak een resourcegroep.
* Uw Azure-IoT-hub in de resourcegroep maken.
* Intel Edison toevoegen aan de Azure IoT hub met behulp van de Azure-opdrachtregelinterface (Azure CLI).

Wanneer u de Azure CLI Edison toevoegen aan uw IoT-hub, genereert de service een sleutel voor Edison voor verificatie met de service. Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina][troubleshooting].

## <a name="what-you-will-learn"></a>Wat u leert
In dit artikel leert u het:
* Het gebruik van de Azure CLI voor het maken van een IoT-hub.
* Het maken van een apparaat-id voor Edison in uw IoT-hub.

## <a name="what-you-need"></a>Wat u nodig hebt
* Een Azure-account. Als u geen Azure-account hebt, maakt u een [gratis proefaccount voor Azure](http://azure.microsoft.com/pricing/free-trial/) over een paar minuten.
* U moet de Azure CLI geïnstalleerd hebben.

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
> De naam van uw IoT-hub moet wereldwijd uniek zijn.
> U kunt slechts één F1-editie van Azure IoT Hub maken onder uw Azure-abonnement.


## <a name="register-edison-in-your-iot-hub"></a>Edison registreren in uw IoT-hub
Elk apparaat dat berichten naar uw IoT-hub verzendt en ontvangt berichten van uw IoT-hub moet zijn geregistreerd met een unieke ID.

Registreren Edison in uw IoT-hub door het uitvoeren van de volgende opdracht:

```bash
az iot device create --device-id myinteledison --hub-name {my hub name}
```

## <a name="summary"></a>Samenvatting
U hebt een IoT-hub gemaakt en geregistreerd Edison met een apparaat-id in uw IoT-hub. U kunt meer informatie over het verzenden van berichten vanaf Edison naar uw IoT-hub.

## <a name="next-steps"></a>Volgende stappen
[Maak een Azure-functie-app en een Azure Storage-account om te verwerken en opslaan van IoT hub berichten][process-and-store-iot-hub-messages].


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-c-lesson3-deploy-resource-manager-template.md