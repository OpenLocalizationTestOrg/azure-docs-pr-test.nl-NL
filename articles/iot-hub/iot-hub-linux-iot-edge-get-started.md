---
title: Aan de slag met Azure IoT rand (Linux) | Microsoft Docs
description: Kom meer te weten over het bouwen van een gateway op een Linux-computer en over belangrijke concepten in de Azure IoT Edge, zoals modules en JSON-configuratiebestanden.
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
ms.openlocfilehash: b02d79fcd9cd2a2ef0041aac4e85528263c8d58a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="explore-azure-iot-edge-architecture-on-linux"></a><span data-ttu-id="5ef89-103">Azure IoT Edge-architectuur in Linux verkennen</span><span class="sxs-lookup"><span data-stu-id="5ef89-103">Explore Azure IoT Edge architecture on Linux</span></span>

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-linux](../../includes/iot-hub-iot-edge-install-build-linux.md)]

## <a name="how-to-run-the-sample"></a><span data-ttu-id="5ef89-104">Het voorbeeld uitvoeren</span><span class="sxs-lookup"><span data-stu-id="5ef89-104">How to run the sample</span></span>

<span data-ttu-id="5ef89-105">De uitvoer van het script **build.sh** wordt gegenereerd in de map **build** in de lokale kopie van de **iot-edge**-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="5ef89-105">The **build.sh** script generates its output in the **build** folder in your local copy of the **iot-edge** repository.</span></span> <span data-ttu-id="5ef89-106">Deze uitvoer bevat de twee IoT Edge-modules die in dit voorbeeld worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="5ef89-106">This output includes the two IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="5ef89-107">Het bouwscript plaatst **liblogger.so** in de map **build/modules/logger/** en **libhello\_world.so** in de map **build/modules/hello_world/**.</span><span class="sxs-lookup"><span data-stu-id="5ef89-107">The build script places **liblogger.so** in the **build/modules/logger/** folder and **libhello\_world.so** in the **build/modules/hello_world/** folder.</span></span> <span data-ttu-id="5ef89-108">Deze paden voor de **pad module** waarden zoals weergegeven in het volgende voorbeeld JSON-instellingenbestand.</span><span class="sxs-lookup"><span data-stu-id="5ef89-108">Use these paths for the **module path** values as shown in the following example JSON settings file.</span></span>

<span data-ttu-id="5ef89-109">In het voorbeeldproces hello\_world\_ wordt het pad naar een JSON-configuratiebestand gebruikt als een argument op de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="5ef89-109">The hello\_world\_sample process takes the path to a JSON configuration file a command-line argument.</span></span> <span data-ttu-id="5ef89-110">Het volgende voorbeeld van een JSON-bestand maakt deel uit van de SDK-opslagplaats op **samples/hello\_world/src/hello\_world\_lin.json**.</span><span class="sxs-lookup"><span data-stu-id="5ef89-110">The following example JSON file is provided in the SDK repository at **samples/hello\_world/src/hello\_world\_lin.json**.</span></span> <span data-ttu-id="5ef89-111">Dit configuratiebestand werkt zoals tenzij u het build script wijzigen voor de rand van de IoT-modules of voorbeeld uitvoerbare bestanden in niet-standaardlocaties plaatsen.</span><span class="sxs-lookup"><span data-stu-id="5ef89-111">This configuration file works as is unless you modify the build script to place the IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="5ef89-112">De modulepaden zijn relatief aan de huidige werkmap vanwaaruit het uitvoerbare bestand hello\_world\_sample wordt gestart, niet aan de map waarin het uitvoerbare bestand zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="5ef89-112">The module paths are relative to the current working directory from where the hello\_world\_sample executable is launched, not the directory where the executable is located.</span></span> <span data-ttu-id="5ef89-113">Het voorbeeld-JSON-configuratiebestand schrijft standaard 'log.txt' in uw huidige werkmap.</span><span class="sxs-lookup"><span data-stu-id="5ef89-113">The sample JSON configuration file defaults to writing 'log.txt' in your current working directory.</span></span>

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

1. <span data-ttu-id="5ef89-114">Navigeer naar de **bouwen** map in de hoofdmap van uw lokale exemplaar van de **iot-edge** opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="5ef89-114">Navigate to the **build** folder in the root of your local copy of the **iot-edge** repository.</span></span>

1. <span data-ttu-id="5ef89-115">Voer de volgende opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="5ef89-115">Run the following command:</span></span>

    ```sh
    ./samples/hello_world/hello_world_sample ../samples/hello_world/src/hello_world_lin.json`
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]

