---
title: Gesimuleerde apparaat & Azure IoT Gateway - aan de slag | Microsoft Docs
description: Aan de slag met IoT Gateway Starter Kit, maakt u uw Azure-IoT-hub en sluit Gateway toohello iothub
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Azure iothub, iot-gateway aan de slag met Hallo internet der dingen, iot toolkit
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
ms.openlocfilehash: 1a54a5e5f1c1d9b2e657c9e4448274256e2533f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-simulated-device"></a>Aan de slag met IoT Gateway Starter Kit met een gesimuleerd apparaat

> [!div class="op_single_selector"]
> * [SensorTag](iot-hub-gateway-kit-c-get-started.md)
> * [Gesimuleerde apparaat](iot-hub-gateway-kit-c-sim-get-started.md)

In deze zelfstudie maakt u eerst learning Hallo basisbeginselen van het werken met [IoT Gateway Starter Kit](https://aka.ms/gateway-kit). U werkt met Intel NUC die o de Linux wordt uitgevoerd. U leert hoe tooseamleesly uw apparaten toohello cloud verbinding met behulp van Azure IoT Hub.

***
**Een kit nog geen hebt?:** klikt u op [hier](https://aka.ms/gateway-kit).
***

## <a name="lesson-1-configure-your-nuc"></a>Les 1: Uw NUC configureren
![Lesson1 end-to-end-diagram](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson1.png)

In deze les Intel NUC (volgende eenheid van computers) instellen in Hallo Kit als een Azure-IoT-gateway, hello Azure IoT rand pakket op NUC installeren en uitvoeren van een voorbeeld-app tooverify Hallo functionaliteit van de gateway.

*Geschatte tijd toocomplete: 15 minuten*

Ga te[Intel NUC als een IoT-gateway instellen](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)

## <a name="lesson-2-create-your-iot-hub"></a>Les 2: Uw IoT-hub maken
![Lesson2 end-to-end-diagram](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson2.png)

In deze les installeert u Hallo-hulpprogramma's en software op de hostcomputer. Vervolgens maken uw gratis Azure-account, het inrichten van uw Azure-IoT-hub en uw eerste apparaat maakt in Hallo IoT-hub.

Les 1 voltooien voordat u deze les.

### <a name="get-hello-tools"></a>Hallo-hulpprogramma's ophalen
Hallo-hulpprogramma's en -software installeren op de hostcomputer.

*Geschatte tijd toocomplete: 20 minuten*

Ga te[Hallo-hulpprogramma's ophalen](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)

### <a name="create-an-iot-hub-and-register-your-device"></a>Een iothub maken en uw apparaat registreren
Toevoegen van uw eerste apparaat toohello IoT-hub hello Azure CLI met uw resourcegroep maken en inrichten van uw eerste Azure-IoT-hub.

*Geschatte tijd toocomplete: 10 minuten*

Ga te[een iothub maken en uw apparaat registreren](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)

## <a name="lesson-3-receive-messages-from-hello-simulated-device-and-read-messages-from-your-iot-hub"></a>Les 3: Berichten ontvangen van het gesimuleerde apparaat Hallo en berichten lezen uit uw IoT-hub
In deze les gebruikt u scripts tooautomate Hallo configuratie en uitvoering van een gesimuleerde apparaattoepassing in uw gateway. de gesimuleerde apparaattoepassing Hallo temperatuur voorbeeldgegevens genereert en verzendt het tooan IoT hub-module. Hallo IoT hub module pakketten Hallo gegevens ontvangen en verzendt deze tooyour IoT-hub door Hallo gateway raamwerk geleverd in Azure IoT rand.

![Les 3 end-to-end-diagram](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson3.png)

### <a name="configure-and-run-a-simulated-device"></a>Configureren en uitvoeren van een gesimuleerd apparaat
Bereid Hallo voorbeeld codes. Vervolgens configureren en uitvoeren van de voorbeeldtoepassing voor Hallo gesimuleerde apparaat.

*Geschatte tijd toocomplete: 15 minuten*

Ga te[en voer een gesimuleerd apparaat configureren](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)

### <a name="read-messages-from-your-iot-hub"></a>Lezen van berichten uit uw IoT-hub
Een voorbeeld van code uitvoeren op uw host computer tooread Hallo-berichten uit uw IoT-hub.

*Geschatte tijd toocomplete: 15 minuten*

Ga te[berichten lezen uit uw IoT-hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)

## <a name="lesson-4-save-messages-tooazure-table-storage"></a>Les 4: Berichten tooAzure Table storage opslaan
Maak een Azure-functie-app die binnenkomende berichten ontvangt van uw IoT-hub en schrijft deze tooAzure Table storage.

![Les 4 end-to-end-diagram](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a>Een Azure-functie-app en Azure Storage-account maken
Een Azure-functie-app en een Azure Storage-account, kunt u een toocreate Azure Resource Manager-sjabloon gebruiken.

*Geschatte tijd toocomplete: 10 minuten*

Ga te[een Azure-functie-app en Azure Storage-account maken](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)

### <a name="read-messages-persisted-in-azure-table-storage"></a>Alleen berichten permanent in Azure Table storage
Hallo gateway-naar-cloud-berichten bewaken tijdens deze tooAzure Table storage worden geschreven.

*Geschatte tijd toocomplete: 5 minuten*

Ga te[gelezen berichten permanent in Azure Table storage](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).

## <a name="troubleshooting"></a>Problemen oplossen
Als u problemen tijdens Hallo uitkomsten hebt, zoekt u naar oplossingen in Hallo [probleemoplossing](iot-hub-gateway-kit-c-sim-troubleshooting.md) artikel.

## <a name="explore-more"></a>Meer verkennen
Ga naar Hallo [Intel IoT Gateway Kit developer zone](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit) toolearn meer.
