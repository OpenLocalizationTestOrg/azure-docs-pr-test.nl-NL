---
title: aaaGet de slag met Azure IoT rand (Windows) | Microsoft Docs
description: Hoe toobuild een Edge van Azure IoT gateway op een Windows-machine en meer informatie over belangrijke concepten in Azure IoT rand zoals modules en JSON-configuratiebestanden.
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 9aff3724-5e4e-40ec-b95a-d00df4f590c5
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: andbuc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5dd13cbfc02eeb55d9f2dbffca5021f2624acf14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="explore-azure-iot-edge-architecture-on-windows"></a>Verken rand van Azure IoT-architectuur in Windows

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-windows](../../includes/iot-hub-iot-edge-install-build-windows.md)]

## <a name="how-toorun-hello-sample"></a>Hoe toorun voorbeeld Hallo

Hallo **build.cmd** script genereert de uitvoer in Hallo **bouwen** map in het lokale exemplaar van Hallo **iot-edge** opslagplaats. Deze uitvoer bevat Hallo twee IoT Edge-modules die in dit voorbeeld worden gebruikt.

Hallo build script plaatsen **logger.dll** in Hallo **bouwen\\modules\\berichtenlogboek\\Debug** map en **hello\_world.dll**  in Hallo **bouwen\\modules\\hello_world\\Debug** map. Gebruik deze paden voor Hallo **pad module** waarden zoals weergegeven in de volgende JSON-instellingenbestand Hallo.

Hallo Hallo\_world\_Hallo pad tooa JSON-configuratiebestand als een opdrachtregelargument duurt dit voorbeeld. Hallo volgende voorbeeld van JSON-bestand vindt u in Hallo SDK opslagplaats op **voorbeelden\\hello\_world\\src\\hello\_world\_win.json**. Deze configuratie bestand werkt zoals tenzij u Hallo wijzigen build script tooplace Hallo IoT rand modules of uitvoerbare bestanden in niet-standaardlocaties steekproef.

> [!NOTE]
> Hallo module paden zijn relatieve toohello directory waar Hallo Hallo\_world\_sample.exe zich bevindt. Hallo voorbeeld JSON configuratie bestand standaardwaarden toowriting 'log.txt' in de huidige werkmap.

```json
{
  "modules": [
    {
      "name": "logger",
      "loader": {
        "name": "native",
        "entrypoint": {
          "module.path": "..\\..\\..\\modules\\logger\\Debug\\logger.dll"
        }
      },
      "args": { "filename": "log.txt" }
    },
    {
      "name": "hello_world",
      "loader": {
        "name": "native",
        "entrypoint": {
          "module.path": "..\\..\\..\\modules\\hello_world\\Debug\\hello_world.dll"
        }
      },
      "args": null
      }
  ],
  "links": [
    {
      "source": "hello_world",
      "sink": "logger"
    }
  ]
}
```

1. Navigeer toohello **bouwen** map in de hoofdmap van uw lokale exemplaar van Hallo Hallo **iot-edge** opslagplaats.

1. Hallo volgende opdracht uitvoeren:

    ```cmd
    samples\hello_world\Debug\hello_world_sample.exe ..\samples\hello_world\src\hello_world_win.json
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]
