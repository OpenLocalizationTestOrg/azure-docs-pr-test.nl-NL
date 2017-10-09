---
title: 'Verbinding maken met frambozen Pi (knooppunt) tooAzure IoT - les 3: implementatie van de sjabloon | Microsoft Docs'
description: Hello Azure functie-app tooAzure IoT hub gebeurtenissen luistert, binnenkomende berichten worden verwerkt en schrijft deze tooAzure Table storage.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: opslaan van gegevens in de cloud hello, gegevens die zijn opgeslagen in de cloud, iot cloudservice
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 6c58de85-c5c4-4989-bb5e-08c45c549966
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b6c0a9530cb80e3f78c0e96037f6f3942b602aea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a>Een Azure-functie-app en Azure storage-account maken
[Azure Functions](../azure-functions/functions-overview.md) is een oplossing voor het eenvoudig uitvoeren *functies* (kleine stukjes code) in de cloud Hallo. Een Azure-functie-app fungeert als host Hallo uitvoering van uw functies in Azure.

## <a name="what-you-will-do"></a>Wat u doet
Een Azure-functie-app en een Azure storage-account, kunt u een toocreate Azure Resource Manager-sjabloon gebruiken. Hello Azure functie-app tooAzure IoT hub gebeurtenissen luistert, binnenkomende berichten worden verwerkt en schrijft deze tooAzure Table storage. Als u problemen hebt, zoeken naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>Wat u leert
In dit artikel leert u het:

* Hoe toouse [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) toodeploy Azure resources.
* Hoe toouse een Azure app tooprocess IoT hub berichten werken en schrijf deze tooa tabel op Azure Table storage.

## <a name="what-you-need"></a>Wat u nodig hebt
U moet hebben voltooid:
* [Aan de slag met frambozen Pi 3](iot-hub-raspberry-pi-kit-node-get-started.md)
* [Uw Azure-IoT-hub maken](iot-hub-raspberry-pi-kit-node-get-started.md)

## <a name="open-hello-sample-app"></a>Open Hallo voorbeeld-app
Hallo-voorbeeldproject openen in Visual Studio Code door het uitvoeren van de volgende opdrachten Hallo:

```bash
cd Lesson3
code .
```

![Structuur van de opslagplaats](media/iot-hub-raspberry-pi-lessons/lesson3/repo_structure.png)

* Hallo `app.js` bestand in Hallo `app` submap is Hallo sleutel bronbestand. Dit bronbestand bevat Hallo code toosend een bericht 20 keer tooyour IoT hub en knipperen Hallo LED voor elk bericht worden verzonden.
* Hallo `arm-template.json` bestand hello Azure Resource Manager-sjabloon met een Azure-functie-app en een Azure storage-account is.
* Hallo `arm-template-param.json` bestand is Hallo configuratiebestand door hello Azure Resource Manager-sjabloon gebruikt.
* Hallo `ReceiveDeviceMessages` submap Hallo Node.js-code voor hello Azure functie bevat.

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a>Configureren van Azure Resource Manager-sjablonen en resources in Azure maken
Update Hallo `arm-template-param.json` bestand in Visual Studio Code.

![Azure Resource Manager-Sjabloonparameters](media/iot-hub-raspberry-pi-lessons/lesson3/arm_para.png)

* Vervang **[naam van uw IoT-Hub]** met **{mijn hubnaam}** die u hebt opgegeven wanneer u [uw IoT-hub gemaakt en geregistreerd frambozen Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).
* Vervang **[voorvoegsel tekenreeks naar nieuwe bronnen]** met een voorvoegsel dat u wilt. Hallo voorvoegsel zorgt dat Hallo resourcenaam is globaal unieke tooavoid conflict. Gebruik geen een streepje of een cijfer initiële in Hallo voorvoegsel.

Na het bijwerken van Hallo `arm-template-param.json` bestand, Hallo resources tooAzure door het uitvoeren van de volgende opdracht Hallo implementeren:

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

Het duurt ongeveer vijf minuten toocreate deze resources. Tijdens het maken van de resource hello wordt uitgevoerd, kunt u op het volgende artikel toohello.

## <a name="summary"></a>Samenvatting
U uw Azure-functie app-tooprocess IoT hub berichten hebt gemaakt en een Azure-opslag rekening toostore deze berichten. U kunt nu implementeren en uitvoeren van hello voorbeeld toosend apparaat-naar-cloud-berichten met Pi.

## <a name="next-steps"></a>Volgende stappen
[Een voorbeeld toepassing toosend apparaat-naar-cloud-berichten worden uitgevoerd op frambozen Pi 3](iot-hub-raspberry-pi-kit-node-lesson3-run-azure-blink.md)

