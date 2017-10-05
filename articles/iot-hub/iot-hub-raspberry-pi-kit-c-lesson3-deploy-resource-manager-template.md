---
title: 'Connect Raspberry PI (C) naar Azure IoT - les 3: implementatie van de sjabloon | Microsoft Docs'
description: De app Azure functie luistert naar gebeurtenissen van Azure IoT hub, binnenkomende berichten worden verwerkt en schrijft deze naar Azure Table storage.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: opslaan van gegevens in de cloud, de gegevens die zijn opgeslagen in de cloud, iot cloudservice
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 4bcfb071-b3ae-48cc-8ea5-7e7434732287
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b8bab31489f2e912b51212cb58cb598a9db9b59d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a>Een Azure-functie-app en Azure storage-account maken
[Azure Functions](../../articles/azure-functions/functions-overview.md) is een oplossing voor het eenvoudig uitvoeren *functies* (kleine stukjes code) in de cloud. Een Azure-functie-app als host fungeert voor de uitvoering van uw functies in Azure.

## <a name="what-will-you-do"></a>Wat doet u
Een Azure Resource Manager-sjabloon gebruiken om een Azure-functie-app en een Azure storage-account te maken. De app Azure functie luistert naar gebeurtenissen van Azure IoT hub, binnenkomende berichten worden verwerkt en schrijft deze naar Azure Table storage. Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-will-you-learn"></a>Wat leert u
In dit artikel leert u het:
* Het gebruik van [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) voor het implementeren van Azure-resources.
* Het gebruik van een Azure-functie-app voor het verwerken van IoT hub berichten en geschreven naar een tabel in Azure Table storage.

## <a name="what-do-you-need"></a>Wat moet u
* U moet hebben voltooid:
- [Aan de slag met uw frambozen Pi 3](iot-hub-raspberry-pi-kit-c-get-started.md)
- [Uw Azure-IoT-hub maken](iot-hub-raspberry-pi-kit-c-get-started.md)

## <a name="open-the-sample-app"></a>Open de voorbeeld-app
Het voorbeeldproject openen in Visual Studio Code met de volgende opdrachten:

```bash
cd Lesson3
code .
```

![Structuur van de opslagplaats](media/iot-hub-raspberry-pi-lessons/lesson3/repo_structure_c.png)

* De `main.c` bestand de `app` submap is het belangrijkste bronbestand. Dit bestand bevat de code voor een bericht 20 keer verzendt naar uw IoT-hub en knipperen de LED voor elk bericht die worden verzonden.
* De `arm-template.json` bestand is de Azure Resource Manager-sjabloon met een Azure-functie-app en een Azure storage-account.
* De `arm-template-param.json` bestand is het configuratiebestand gebruikt door de Azure Resource Manager-sjabloon.
* De `ReceiveDeviceMessages` submap bevat de Node.js-code voor de Azure-functie.

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a>Configureren van Azure Resource Manager-sjablonen en resources in Azure maken
Update de `arm-template-param.json` bestand in Visual Studio Code.

![Azure Resource Manager-Sjabloonparameters](media/iot-hub-raspberry-pi-lessons/lesson3/arm_para_c.png)

* Vervang **[naam van uw IoT-Hub]** met **{mijn hubnaam}** die u hebt opgegeven wanneer u [uw IoT-hub gemaakt en geregistreerd frambozen Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md).
* Vervang **[voorvoegsel tekenreeks naar nieuwe bronnen]** met een voorvoegsel dat u wilt. Het voorvoegsel zorgt ervoor dat de resourcenaam globaal unieke om conflicten te voorkomen. Gebruik geen een streepje of een cijfer eerste in het voorvoegsel.

Na het bijwerken van de `arm-template-param.json` bestand, het implementeren van de resources in Azure met de volgende opdracht:

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

Het duurt ongeveer vijf minuten voor het maken van deze resources. Tijdens het maken van de resource uitgevoerd wordt, kunt u op het volgende artikel.

## <a name="summary"></a>Samenvatting
U kunt uw Azure-functie-app voor het verwerken van IoT hub berichten en een Azure storage-account voor het opslaan van deze berichten hebt gemaakt. U kunt nu implementeren en uitvoeren van het voorbeeld voor het verzenden van apparaat-naar-cloud-berichten met Pi.

## <a name="next-steps"></a>Volgende stappen
[Voer een voorbeeldtoepassing om apparaat-naar-cloud-berichten te verzenden](iot-hub-raspberry-pi-kit-c-lesson3-run-azure-blink.md)

