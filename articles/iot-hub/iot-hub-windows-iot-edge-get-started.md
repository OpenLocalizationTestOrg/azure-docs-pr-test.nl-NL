---
title: Aan de slag met Azure IoT rand (Windows) | Microsoft Docs
description: Het maken van een Azure-IoT-Edge-gateway op een Windows-machine en meer informatie over belangrijke concepten in Azure IoT rand zoals modules en JSON-configuratiebestanden.
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
ms.openlocfilehash: 5db39bab8e31a8e7026b34e72b4614b0f6f57772
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="explore-azure-iot-edge-architecture-on-windows"></a>Verken rand van Azure IoT-architectuur in Windows

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-windows](../../includes/iot-hub-iot-edge-install-build-windows.md)]

## <a name="how-to-run-the-sample"></a>Het voorbeeld uitvoeren

De **build.cmd** script genereert de uitvoer ervan weergegeven in de **bouwen** map in de lokale kopie van de **iot-edge** opslagplaats. Deze uitvoer bevat de twee IoT Edge-modules die in dit voorbeeld worden gebruikt.

De build script plaatsen **logger.dll** in de **bouwen\\modules\\berichtenlogboek\\Debug** map en **hello\_world.dll** in de **bouwen\\modules\\hello_world\\Debug** map. Deze paden voor de **pad module** waarden zoals weergegeven in het volgende JSON-bestand met instellingen.

De Hallo\_world\_voorbeeld wordt het pad naar een JSON-configuratiebestand als een opdrachtregelargument. Het volgende voorbeeld JSON-bestand is opgegeven in de SDK-opslagplaats op **voorbeelden\\hello\_world\\src\\hello\_world\_win.json**. Dit configuratiebestand werkt zoals tenzij u het build script wijzigen voor de rand van de IoT-modules of voorbeeld uitvoerbare bestanden in niet-standaardlocaties plaatsen.

> [!NOTE]
> De module-paden zijn ten opzichte van de map waar de Hallo\_world\_sample.exe zich bevindt. Het voorbeeld-JSON-configuratiebestand schrijft standaard 'log.txt' in uw huidige werkmap.

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

1. Navigeer naar de **bouwen** map in de hoofdmap van uw lokale exemplaar van de **iot-edge** opslagplaats.

1. Voer de volgende opdracht uit:

    ```cmd
    samples\hello_world\Debug\hello_world_sample.exe ..\samples\hello_world\src\hello_world_win.json
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]
