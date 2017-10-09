---
title: aaaGet de slag met Azure IoT rand (Linux) | Microsoft Docs
description: Hoe een gateway op een Linux toobuild machine en meer informatie over belangrijke concepten in Azure IoT rand zoals modules en JSON-configuratiebestanden.
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: cf537bdd-2352-4bb1-96cd-a283fcd3d6cf
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: andbuc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 40aa9c8ddca6a974c361cbb0b453c7d0ddc71b8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="explore-azure-iot-edge-architecture-on-linux"></a>Azure IoT Edge-architectuur in Linux verkennen

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-linux](../../includes/iot-hub-iot-edge-install-build-linux.md)]

## <a name="how-toorun-hello-sample"></a>Hoe toorun voorbeeld Hallo

Hallo **build.sh** script genereert de uitvoer in Hallo **bouwen** map in het lokale exemplaar van Hallo **iot-edge** opslagplaats. Deze uitvoer bevat Hallo twee IoT Edge-modules die in dit voorbeeld worden gebruikt.

Hallo build script plaatsen **liblogger.so** in Hallo **modules-build-logboekregistratie/** map en **libhello\_world.so** in Hallo **bouwen / modules/hello_world/** map. Gebruik deze paden voor Hallo **pad module** waarden zoals weergegeven in Hallo voorbeeld JSON-bestand met instellingen te volgen.

Hallo Hallo\_world\_voorbeeld duurt Hallo pad tooa JSON-configuratiebestand opdrachtregelargumenten. Hallo volgende voorbeeld van JSON-bestand vindt u in Hallo SDK opslagplaats op **samples/Hallo\_world/src/Hallo\_world\_lin.json**. Deze configuratie bestand werkt zoals tenzij u Hallo wijzigen build script tooplace Hallo IoT rand modules of uitvoerbare bestanden in niet-standaardlocaties steekproef.

> [!NOTE]
> Hallo module paden zijn huidige werkmap relatieve toohello waar Hallo Hallo\_world\_voorbeeld uitvoerbaar bestand wordt gestart, wordt niet Hallo map waar Hallo uitvoerbare bevindt. Hallo voorbeeld JSON configuratie bestand standaardwaarden toowriting 'log.txt' in de huidige werkmap.

```json
{
    "modules" :
    [
        {
            "name" : "logger",
            "loader": {
            "name": "native",
            "entrypoint": {
                "module.path": "./modules/logger/liblogger.so"
            }
            },
            "args" : {"filename":"log.txt"}
        },
        {
            "name" : "hello_world",
            "loader": {
            "name": "native",
            "entrypoint": {
                "module.path": "./modules/hello_world/libhello_world.so"
            }
            },
            "args" : null
        }
    ],
    "links":
    [
        {
            "source": "hello_world",
            "sink": "logger"
        }
    ]
}
```

1. Navigeer toohello **bouwen** map in de hoofdmap van uw lokale exemplaar van Hallo Hallo **iot-edge** opslagplaats.

1. Hallo volgende opdracht uitvoeren:

    ```sh
    ./samples/hello_world/hello_world_sample ../samples/hello_world/src/hello_world_lin.json`
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]

