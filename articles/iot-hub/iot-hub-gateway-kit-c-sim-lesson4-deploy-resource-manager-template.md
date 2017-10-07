---
title: 'Gesimuleerde apparaat & Azure IoT Gateway - les 4: berichten opslaan | Microsoft Docs'
description: Berichten uit iothub van Intel NUC tooyour opslaan, tooAzure Table storage geschreven en ze vervolgens vanuit de cloud hello te lezen.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: opslaan van gegevens in de cloud hello, gegevens die zijn opgeslagen in de cloud, iot cloudservice
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
ms.openlocfilehash: 230f2708b62b89c6eed2e238efefc1c4da86e373
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-storage-account"></a>Een Azure-functie-app en opslagaccount maken

Azure Functions is een oplossing voor het eenvoudig uitvoeren _functies_ (kleine stukjes code) in de cloud Hallo. Een Azure-functie-app fungeert als host Hallo uitvoering van uw functies in Azure. 

## <a name="what-you-will-do"></a>Wat u doet

- Een Azure-functie-app en een Azure storage-account, kunt u een toocreate Azure Resource Manager-sjabloon gebruiken. Hello Azure functie-app tooAzure IoT hub gebeurtenissen luistert, binnenkomende berichten worden verwerkt en schrijft deze tooAzure Table storage.

Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-gateway-kit-c-sim-troubleshooting.md).


## <a name="what-you-will-learn"></a>Wat u leert

In deze les leert u het:

- Hoe toouse Azure Resource Manager toodeploy Azure-resources.
- Hoe toouse een Azure app tooprocess IoT Hub berichten werken en schrijf deze tooa tabel op Azure Table storage.

## <a name="what-you-need"></a>Wat u nodig hebt

U moet hebben voltooid Hallo vorige uitkomsten:

- [Les 1: Uw NUC Intel instellen als een IoT-gateway](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)
- [Les 2: Bereid u voor uw hostcomputer en Azure IoT hub](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
- [Les 3: Berichten ontvangen van het gesimuleerde apparaat Hallo en berichten lezen uit uw IoT-hub](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)

## <a name="open-a-sample-app"></a>Een voorbeeld-app openen

Ga tooyour `iot-hub-c-intel-nuc-gateway-getting-started` opslagplaats map, initialiseren Hallo-configuratiebestanden en open vervolgens Hallo-voorbeeldproject in Visual Studio Code door het uitvoeren van de volgende opdracht Hallo:

```bash
cd Lesson4
npm install
gulp init
code .
```

![Structuur van de opslagplaats](media/iot-hub-gateway-kit-lessons/lesson4/arm_template.png)

- Hallo `arm-template.json` bestand hello Azure Resource Manager-sjabloon met een Azure-functie-app en een Azure storage-account is.
- Hallo `arm-template-param.json` bestand is Hallo configuratiebestand door hello Azure Resource Manager-sjabloon gebruikt.
- Hallo `ReceiveDeviceMessages` submap Hallo Node.js-code voor hello Azure functie bevat.

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a>Configureren van Azure Resource Manager-sjablonen en resources in Azure maken

Update Hallo `arm-template-param.json` bestand in Visual Studio Code.

![arm-sjabloon json](media/iot-hub-gateway-kit-lessons/lesson4/arm_template_param.png)

- Vervang `[your IoT Hub name]` met `{my hub name}` die u hebt opgegeven in les 2.

Na het bijwerken van Hallo `arm-template-param.json` bestand, Hallo resources tooAzure door het uitvoeren van de volgende opdracht Hallo implementeren:

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-gateway
```

Gebruik `iot-gateway` als Hallo-waarde van `{resource group name}` als u Hallo-waarde in les 2 niet wijzigen.

## <a name="summary"></a>Samenvatting

U uw Azure-functie app-tooprocess IoT hub berichten hebt gemaakt en een Azure-opslag rekening toostore deze berichten. Nu kunt u lezen van berichten die door uw gateway tooyour iothub worden verzonden.

## <a name="next-steps"></a>Volgende stappen
[Alleen berichten permanent in Azure Storage](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).
