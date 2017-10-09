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
# <a name="explore-azure-iot-edge-architecture-on-linux"></a><span data-ttu-id="ed5fb-103">Azure IoT Edge-architectuur in Linux verkennen</span><span class="sxs-lookup"><span data-stu-id="ed5fb-103">Explore Azure IoT Edge architecture on Linux</span></span>

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-linux](../../includes/iot-hub-iot-edge-install-build-linux.md)]

## <a name="how-toorun-hello-sample"></a><span data-ttu-id="ed5fb-104">Hoe toorun voorbeeld Hallo</span><span class="sxs-lookup"><span data-stu-id="ed5fb-104">How toorun hello sample</span></span>

<span data-ttu-id="ed5fb-105">Hallo **build.sh** script genereert de uitvoer in Hallo **bouwen** map in het lokale exemplaar van Hallo **iot-edge** opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="ed5fb-105">hello **build.sh** script generates its output in hello **build** folder in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="ed5fb-106">Deze uitvoer bevat Hallo twee IoT Edge-modules die in dit voorbeeld worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ed5fb-106">This output includes hello two IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="ed5fb-107">Hallo build script plaatsen **liblogger.so** in Hallo **modules-build-logboekregistratie/** map en **libhello\_world.so** in Hallo **bouwen / modules/hello_world/** map.</span><span class="sxs-lookup"><span data-stu-id="ed5fb-107">hello build script places **liblogger.so** in hello **build/modules/logger/** folder and **libhello\_world.so** in hello **build/modules/hello_world/** folder.</span></span> <span data-ttu-id="ed5fb-108">Gebruik deze paden voor Hallo **pad module** waarden zoals weergegeven in Hallo voorbeeld JSON-bestand met instellingen te volgen.</span><span class="sxs-lookup"><span data-stu-id="ed5fb-108">Use these paths for hello **module path** values as shown in hello following example JSON settings file.</span></span>

<span data-ttu-id="ed5fb-109">Hallo Hallo\_world\_voorbeeld duurt Hallo pad tooa JSON-configuratiebestand opdrachtregelargumenten.</span><span class="sxs-lookup"><span data-stu-id="ed5fb-109">hello hello\_world\_sample process takes hello path tooa JSON configuration file a command-line argument.</span></span> <span data-ttu-id="ed5fb-110">Hallo volgende voorbeeld van JSON-bestand vindt u in Hallo SDK opslagplaats op **samples/Hallo\_world/src/Hallo\_world\_lin.json**.</span><span class="sxs-lookup"><span data-stu-id="ed5fb-110">hello following example JSON file is provided in hello SDK repository at **samples/hello\_world/src/hello\_world\_lin.json**.</span></span> <span data-ttu-id="ed5fb-111">Deze configuratie bestand werkt zoals tenzij u Hallo wijzigen build script tooplace Hallo IoT rand modules of uitvoerbare bestanden in niet-standaardlocaties steekproef.</span><span class="sxs-lookup"><span data-stu-id="ed5fb-111">This configuration file works as is unless you modify hello build script tooplace hello IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="ed5fb-112">Hallo module paden zijn huidige werkmap relatieve toohello waar Hallo Hallo\_world\_voorbeeld uitvoerbaar bestand wordt gestart, wordt niet Hallo map waar Hallo uitvoerbare bevindt.</span><span class="sxs-lookup"><span data-stu-id="ed5fb-112">hello module paths are relative toohello current working directory from where hello hello\_world\_sample executable is launched, not hello directory where hello executable is located.</span></span> <span data-ttu-id="ed5fb-113">Hallo voorbeeld JSON configuratie bestand standaardwaarden toowriting 'log.txt' in de huidige werkmap.</span><span class="sxs-lookup"><span data-stu-id="ed5fb-113">hello sample JSON configuration file defaults toowriting 'log.txt' in your current working directory.</span></span>

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

1. <span data-ttu-id="ed5fb-114">Navigeer toohello **bouwen** map in de hoofdmap van uw lokale exemplaar van Hallo Hallo **iot-edge** opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="ed5fb-114">Navigate toohello **build** folder in hello root of your local copy of hello **iot-edge** repository.</span></span>

1. <span data-ttu-id="ed5fb-115">Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="ed5fb-115">Run hello following command:</span></span>

    ```sh
    ./samples/hello_world/hello_world_sample ../samples/hello_world/src/hello_world_lin.json`
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]

