---
title: 'Gesimuleerde apparaat & Azure IoT Gateway - les 4: berichten opslaan | Microsoft Docs'
description: Intel NUC berichten opslaan op uw IoT-hub, geschreven naar Azure Table storage en ze vervolgens vanuit de cloud te lezen.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: opslaan van gegevens in de cloud, de gegevens die zijn opgeslagen in de cloud, iot cloudservice
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: ffed0c2e-b092-40e1-9113-8196ec057d67
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c7fc47b07acede28ffe790debca7e38521726011
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-app-and-storage-account"></a>Een Azure-functie-app en opslagaccount maken

Azure Functions is een oplossing voor het eenvoudig uitvoeren _functies_ (kleine stukjes code) in de cloud. Een Azure-functie-app als host fungeert voor de uitvoering van uw functies in Azure. 

## <a name="what-you-will-do"></a>Wat u doet

- Een Azure Resource Manager-sjabloon gebruiken om een Azure-functie-app en een Azure storage-account te maken. De app Azure functie luistert naar gebeurtenissen van Azure IoT hub, binnenkomende berichten worden verwerkt en schrijft deze naar Azure Table storage.

Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina](iot-hub-gateway-kit-c-sim-troubleshooting.md).


## <a name="what-you-will-learn"></a>Wat u leert

In deze les leert u het:

- Het gebruik van Azure Resource Manager voor het implementeren van Azure-resources.
- Het gebruik van een Azure-functie-app worden IoT Hub berichten verwerken en geschreven naar een tabel in Azure Table storage.

## <a name="what-you-need"></a>Wat u nodig hebt

U moet hebt voltooid de vorige uitkomsten:

- [Les 1: Uw NUC Intel instellen als een IoT-gateway](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)
- [Les 2: Bereid u voor uw hostcomputer en Azure IoT hub](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
- [Les 3: Berichten ontvangen van het gesimuleerde apparaat en de berichten lezen uit uw IoT-hub](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)

## <a name="open-a-sample-app"></a>Een voorbeeld-app openen

Ga naar uw `iot-hub-c-intel-nuc-gateway-getting-started` opslagplaats map initialiseren van de configuratiebestanden en open vervolgens het voorbeeldproject in Visual Studio Code met de volgende opdracht:

```bash
cd Lesson4
npm install
gulp init
code .
```

![Structuur van de opslagplaats](media/iot-hub-gateway-kit-lessons/lesson4/arm_template.png)

- De `arm-template.json` bestand is de Azure Resource Manager-sjabloon met een Azure-functie-app en een Azure storage-account.
- De `arm-template-param.json` bestand is het configuratiebestand gebruikt door de Azure Resource Manager-sjabloon.
- De `ReceiveDeviceMessages` submap bevat de Node.js-code voor de Azure-functie.

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a>Configureren van Azure Resource Manager-sjablonen en resources in Azure maken

Update de `arm-template-param.json` bestand in Visual Studio Code.

![arm-sjabloon json](media/iot-hub-gateway-kit-lessons/lesson4/arm_template_param.png)

- Vervang `[your IoT Hub name]` met `{my hub name}` die u hebt opgegeven in les 2.

Na het bijwerken van de `arm-template-param.json` bestand, het implementeren van de resources in Azure met de volgende opdracht:

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-gateway
```

Gebruik `iot-gateway` als de waarde van `{resource group name}` als u de waarde in les 2 is niet gewijzigd.

## <a name="summary"></a>Samenvatting

U kunt uw Azure-functie-app voor het verwerken van IoT hub berichten en een Azure storage-account voor het opslaan van deze berichten hebt gemaakt. Nu kunt u lezen van berichten die door uw gateway uit naar uw IoT-hub worden verzonden.

## <a name="next-steps"></a>Volgende stappen
[Alleen berichten permanent in Azure Storage](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).
