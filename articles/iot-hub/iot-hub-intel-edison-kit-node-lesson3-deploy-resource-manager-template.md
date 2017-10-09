---
title: 'Verbinding maken met Intel Edison (knooppunt) tooAzure IoT - les 3: functie-app maken | Microsoft Docs'
description: Hello Azure functie-app tooAzure IoT hub gebeurtenissen luistert, binnenkomende berichten worden verwerkt en schrijft deze tooAzure Table storage.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: opslaan van gegevens in de cloud hello, gegevens die zijn opgeslagen in de cloud, iot cloudservice
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 37ee5962-95ce-40e8-8162-17e735eaec21
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8ea0a4cdf978158d70e47eaed57e3de378b638d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a>Een Azure-functie-app en Azure storage-account maken
[Azure Functions](../../articles/azure-functions/functions-overview.md) is een oplossing voor het eenvoudig uitvoeren *functies* (kleine stukjes code) in de cloud Hallo. Een Azure-functie-app fungeert als host Hallo uitvoering van uw functies in Azure.

## <a name="what-will-you-do"></a>Wat doet u
Een Azure-functie-app en een Azure storage-account, kunt u een toocreate Azure Resource Manager-sjabloon gebruiken. Hello Azure functie-app tooAzure IoT hub gebeurtenissen luistert, binnenkomende berichten worden verwerkt en schrijft deze tooAzure Table storage. Hallo opslagaccount wordt gebruikt om te lezen Hallo persistent kopieën van berichten vanuit de Azure-tabel. Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina][troubleshooting].

## <a name="what-will-you-learn"></a>Wat leert u
In dit artikel leert u het:
* Hoe toouse [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) toodeploy Azure resources.
* Hoe toouse een Azure app tooprocess IoT hub berichten werken en schrijf deze tooa tabel op Azure Table storage.

## <a name="what-do-you-need"></a>Wat moet u
U moet hebben voltooid:
- [Aan de slag met uw Edison Intel][get-started-with-your-intel-edison]
- [Uw Azure-IoT-hub maken][create-your-azure-iot-hub]

## <a name="open-hello-sample-app"></a>Open Hallo voorbeeld-app
Hallo-voorbeeldproject openen in Visual Studio Code door het uitvoeren van de volgende opdrachten Hallo:

```bash
cd Lesson3
code .
```

![Structuur van de opslagplaats][repo-structure]

* Hallo-bestand in Hallo `app` submap is Hallo sleutel bronbestand. Dit bronbestand bevat Hallo code toosend een bericht 20 keer tooyour IoT hub en knipperen Hallo LED voor elk bericht worden verzonden.
* Hallo `arm-template.json` bestand hello Azure Resource Manager-sjabloon met een Azure-functie-app en een Azure storage-account is.
* Hallo `arm-template-param.json` bestand is Hallo configuratiebestand door hello Azure Resource Manager-sjabloon gebruikt.
* Hallo `ReceiveDeviceMessages` submap Hallo Node.js-code voor hello Azure functie bevat.

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a>Configureren van Azure Resource Manager-sjablonen en resources in Azure maken
Update Hallo `arm-template-param.json` bestand in Visual Studio Code.

![Azure Resource Manager-Sjabloonparameters][arm-template-parameters]

* Vervang **[naam van uw IoT-Hub]** met **{mijn hubnaam}** die u hebt opgegeven wanneer u [uw IoT-hub gemaakt en geregistreerd Intel Edison][created-your-iot-hub-and-registered-intel-edison].
* Vervang **[voorvoegsel tekenreeks naar nieuwe bronnen]** met een voorvoegsel dat u wilt. Hallo voorvoegsel zorgt dat Hallo resourcenaam is globaal unieke tooavoid conflict. Gebruik geen een streepje of een cijfer initiële in Hallo voorvoegsel.

Na het bijwerken van Hallo `arm-template-param.json` bestand, Hallo resources tooAzure door het uitvoeren van de volgende opdracht Hallo implementeren:

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

Het duurt ongeveer vijf minuten toocreate deze resources. Tijdens het maken van de resource hello wordt uitgevoerd, kunt u op het volgende artikel toohello.

## <a name="summary"></a>Samenvatting
U uw Azure-functie app-tooprocess IoT hub berichten hebt gemaakt en een Azure-opslag rekening toostore deze berichten. U kunt nu implementeren en uitvoeren van hello voorbeeld toosend apparaat-naar-cloud-berichten op Edison.

## <a name="next-steps"></a>Volgende stappen
[Een voorbeeld toepassing toosend apparaat-naar-cloud-berichten worden uitgevoerd op Intel Edison][send-device-to-cloud-messages].
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[get-started-with-your-intel-edison]: iot-hub-intel-edison-kit-node-get-started.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-node-get-started.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson3/repo_structure.png
[arm-template-parameters]: media/iot-hub-intel-edison-lessons/lesson3/arm_para.png
[created-your-iot-hub-and-registered-intel-edison]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[send-device-to-cloud-messages]: iot-hub-intel-edison-kit-node-lesson3-run-azure-blink.md