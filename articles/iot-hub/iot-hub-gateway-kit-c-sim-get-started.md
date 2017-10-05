---
title: Gesimuleerde apparaat & Azure IoT Gateway - aan de slag | Microsoft Docs
description: Aan de slag met IoT Gateway Starter Kit, maakt u uw Azure-IoT-hub en verbinding maken met de Gateway met de iothub
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Azure iothub, iot-gateway aan de slag met het internet der dingen, iot toolkit
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 0c110b8b-bee4-4aec-a18a-dfc292aa17a3
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 916fa40d9ac857dfa72197b40c232834593d3891
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-simulated-device"></a>Aan de slag met IoT Gateway Starter Kit met een gesimuleerd apparaat

> [!div class="op_single_selector"]
> * [SensorTag](iot-hub-gateway-kit-c-get-started.md)
> * [Gesimuleerde apparaat](iot-hub-gateway-kit-c-sim-get-started.md)

In deze zelfstudie maakt u eerst leren over het werken met [IoT Gateway Starter Kit](https://aka.ms/gateway-kit). U werkt met Intel NUC die o de Linux wordt uitgevoerd. U leert hoe seamleesly verbinding maken uw apparaten naar de cloud met behulp van Azure IoT Hub.

***
**Een kit nog geen hebt?:** klikt u op [hier](https://aka.ms/gateway-kit).
***

## <a name="lesson-1-configure-your-nuc"></a>Les 1: Uw NUC configureren
![Lesson1 end-to-end-diagram](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson1.png)

In deze les Intel NUC (volgende eenheid van computers) in de set als een Azure IoT gateway instellen, de rand van Azure IoT-pakket op NUC installeren en uitvoeren van een voorbeeld-app om te controleren of de functionaliteit van de gateway.

*Geschatte duur: 15 minuten*

Ga naar [Intel NUC als een IoT-gateway instellen](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)

## <a name="lesson-2-create-your-iot-hub"></a>Les 2: Uw IoT-hub maken
![Lesson2 end-to-end-diagram](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson2.png)

In deze les installeert u de hulpprogramma's en software op de hostcomputer. Vervolgens maken uw gratis Azure-account, het inrichten van uw Azure-IoT-hub en maken van uw eerste apparaat in de IoT-hub.

Les 1 voltooien voordat u deze les.

### <a name="get-the-tools"></a>Hulpprogramma's ophalen
De hulpprogramma's en -software installeren op de hostcomputer.

*Geschatte duur: 20 minuten*

Ga naar [Download de hulpprogramma's](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)

### <a name="create-an-iot-hub-and-register-your-device"></a>Een iothub maken en uw apparaat registreren
Uw eerste apparaat toevoegen aan de iothub met de Azure CLI uw resourcegroep maken en inrichten van uw eerste Azure-IoT-hub.

*Geschatte duur: 10 minuten*

Ga naar [een iothub maken en uw apparaat registreren](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)

## <a name="lesson-3-receive-messages-from-the-simulated-device-and-read-messages-from-your-iot-hub"></a>Les 3: Berichten ontvangen van het gesimuleerde apparaat en de berichten lezen uit uw IoT-hub
In deze les wordt u scripts gebruiken voor het automatiseren van de configuratie en uitvoering van een gesimuleerde apparaattoepassing in uw gateway. De gesimuleerde apparaattoepassing temperatuur voorbeeldgegevens genereert en verzendt het naar een IoT hub-module. De module IoT-hub pakketten van de ontvangen gegevens en verzendt het naar uw IoT-hub via het gateway-framework dat is opgegeven in de Azure IoT rand.

![Les 3 end-to-end-diagram](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson3.png)

### <a name="configure-and-run-a-simulated-device"></a>Configureren en uitvoeren van een gesimuleerd apparaat
Bereid de voorbeeld-codes. Vervolgens configureren en uitvoeren van de voorbeeldtoepassing gesimuleerde apparaat.

*Geschatte duur: 15 minuten*

Ga naar [en voer een gesimuleerd apparaat configureren](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)

### <a name="read-messages-from-your-iot-hub"></a>Lezen van berichten uit uw IoT-hub
Een voorbeeld van code uitvoeren op de hostcomputer de berichten lezen uit uw IoT-hub.

*Geschatte duur: 15 minuten*

Ga naar [berichten lezen uit uw IoT-hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)

## <a name="lesson-4-save-messages-to-azure-table-storage"></a>Les 4: Berichten opslaan in Azure Table Storage
Maak een Azure-functie-app die berichten ontvangt van uw IoT-hub en schrijft deze naar Azure Table storage.

![Les 4 end-to-end-diagram](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a>Een Azure-functie-app en Azure Storage-account maken
Een Azure Resource Manager-sjabloon gebruiken om een Azure-functie-app en een Azure Storage-account te maken.

*Geschatte duur: 10 minuten*

Ga naar [een Azure-functie-app en Azure Storage-account maken](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)

### <a name="read-messages-persisted-in-azure-table-storage"></a>Alleen berichten permanent in Azure Table storage
De gateway-naar-cloud-berichten bewaken zoals ze zijn geschreven naar Azure Table storage.

*Geschatte duur: 5 minuten*

Ga naar [gelezen berichten permanent in Azure Table storage](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).

## <a name="troubleshooting"></a>Problemen oplossen
Als u problemen tijdens de uitkomsten hebt, zoekt u naar oplossingen in de [probleemoplossing](iot-hub-gateway-kit-c-sim-troubleshooting.md) artikel.

## <a name="explore-more"></a>Meer verkennen
Ga naar de [Intel IoT Gateway Kit developer zone](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit) voor meer informatie.