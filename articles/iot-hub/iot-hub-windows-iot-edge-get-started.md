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
# <a name="explore-azure-iot-edge-architecture-on-windows"></a><span data-ttu-id="217e9-103">Verken rand van Azure IoT-architectuur in Windows</span><span class="sxs-lookup"><span data-stu-id="217e9-103">Explore Azure IoT Edge architecture on Windows</span></span>

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-windows](../../includes/iot-hub-iot-edge-install-build-windows.md)]

## <a name="how-toorun-hello-sample"></a><span data-ttu-id="217e9-104">Hoe toorun voorbeeld Hallo</span><span class="sxs-lookup"><span data-stu-id="217e9-104">How toorun hello sample</span></span>

<span data-ttu-id="217e9-105">Hallo **build.cmd** script genereert de uitvoer in Hallo **bouwen** map in het lokale exemplaar van Hallo **iot-edge** opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="217e9-105">hello **build.cmd** script generates its output in hello **build** folder in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="217e9-106">Deze uitvoer bevat Hallo twee IoT Edge-modules die in dit voorbeeld worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="217e9-106">This output includes hello two IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="217e9-107">Hallo build script plaatsen **logger.dll** in Hallo **bouwen\\modules\\berichtenlogboek\\Debug** map en **hello\_world.dll**  in Hallo **bouwen\\modules\\hello_world\\Debug** map.</span><span class="sxs-lookup"><span data-stu-id="217e9-107">hello build script places **logger.dll** in hello **build\\modules\\logger\\Debug** folder and **hello\_world.dll** in hello **build\\modules\\hello_world\\Debug** folder.</span></span> <span data-ttu-id="217e9-108">Gebruik deze paden voor Hallo **pad module** waarden zoals weergegeven in de volgende JSON-instellingenbestand Hallo.</span><span class="sxs-lookup"><span data-stu-id="217e9-108">Use these paths for hello **module path** values as shown in hello following JSON settings file.</span></span>

<span data-ttu-id="217e9-109">Hallo Hallo\_world\_Hallo pad tooa JSON-configuratiebestand als een opdrachtregelargument duurt dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="217e9-109">hello hello\_world\_sample process takes hello path tooa JSON configuration file as a command-line argument.</span></span> <span data-ttu-id="217e9-110">Hallo volgende voorbeeld van JSON-bestand vindt u in Hallo SDK opslagplaats op **voorbeelden\\hello\_world\\src\\hello\_world\_win.json**.</span><span class="sxs-lookup"><span data-stu-id="217e9-110">hello following example JSON file is provided in hello SDK repository at **samples\\hello\_world\\src\\hello\_world\_win.json**.</span></span> <span data-ttu-id="217e9-111">Deze configuratie bestand werkt zoals tenzij u Hallo wijzigen build script tooplace Hallo IoT rand modules of uitvoerbare bestanden in niet-standaardlocaties steekproef.</span><span class="sxs-lookup"><span data-stu-id="217e9-111">This configuration file works as is unless you modify hello build script tooplace hello IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="217e9-112">Hallo module paden zijn relatieve toohello directory waar Hallo Hallo\_world\_sample.exe zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="217e9-112">hello module paths are relative toohello directory where hello hello\_world\_sample.exe is located.</span></span> <span data-ttu-id="217e9-113">Hallo voorbeeld JSON configuratie bestand standaardwaarden toowriting 'log.txt' in de huidige werkmap.</span><span class="sxs-lookup"><span data-stu-id="217e9-113">hello sample JSON configuration file defaults toowriting 'log.txt' in your current working directory.</span></span>

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

1. <span data-ttu-id="217e9-114">Navigeer toohello **bouwen** map in de hoofdmap van uw lokale exemplaar van Hallo Hallo **iot-edge** opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="217e9-114">Navigate toohello **build** folder in hello root of your local copy of hello **iot-edge** repository.</span></span>

1. <span data-ttu-id="217e9-115">Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="217e9-115">Run hello following command:</span></span>

    ```cmd
    samples\hello_world\Debug\hello_world_sample.exe ..\samples\hello_world\src\hello_world_win.json
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]
