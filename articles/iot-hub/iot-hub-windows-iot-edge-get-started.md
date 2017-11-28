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
# <a name="explore-azure-iot-edge-architecture-on-windows"></a><span data-ttu-id="a312d-103">Verken rand van Azure IoT-architectuur in Windows</span><span class="sxs-lookup"><span data-stu-id="a312d-103">Explore Azure IoT Edge architecture on Windows</span></span>

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-windows](../../includes/iot-hub-iot-edge-install-build-windows.md)]

## <a name="how-to-run-the-sample"></a><span data-ttu-id="a312d-104">Het voorbeeld uitvoeren</span><span class="sxs-lookup"><span data-stu-id="a312d-104">How to run the sample</span></span>

<span data-ttu-id="a312d-105">De **build.cmd** script genereert de uitvoer ervan weergegeven in de **bouwen** map in de lokale kopie van de **iot-edge** opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="a312d-105">The **build.cmd** script generates its output in the **build** folder in your local copy of the **iot-edge** repository.</span></span> <span data-ttu-id="a312d-106">Deze uitvoer bevat de twee IoT Edge-modules die in dit voorbeeld worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a312d-106">This output includes the two IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="a312d-107">De build script plaatsen **logger.dll** in de **bouwen\\modules\\berichtenlogboek\\Debug** map en **hello\_world.dll** in de **bouwen\\modules\\hello_world\\Debug** map.</span><span class="sxs-lookup"><span data-stu-id="a312d-107">The build script places **logger.dll** in the **build\\modules\\logger\\Debug** folder and **hello\_world.dll** in the **build\\modules\\hello_world\\Debug** folder.</span></span> <span data-ttu-id="a312d-108">Deze paden voor de **pad module** waarden zoals weergegeven in het volgende JSON-bestand met instellingen.</span><span class="sxs-lookup"><span data-stu-id="a312d-108">Use these paths for the **module path** values as shown in the following JSON settings file.</span></span>

<span data-ttu-id="a312d-109">De Hallo\_world\_voorbeeld wordt het pad naar een JSON-configuratiebestand als een opdrachtregelargument.</span><span class="sxs-lookup"><span data-stu-id="a312d-109">The hello\_world\_sample process takes the path to a JSON configuration file as a command-line argument.</span></span> <span data-ttu-id="a312d-110">Het volgende voorbeeld JSON-bestand is opgegeven in de SDK-opslagplaats op **voorbeelden\\hello\_world\\src\\hello\_world\_win.json**.</span><span class="sxs-lookup"><span data-stu-id="a312d-110">The following example JSON file is provided in the SDK repository at **samples\\hello\_world\\src\\hello\_world\_win.json**.</span></span> <span data-ttu-id="a312d-111">Dit configuratiebestand werkt zoals tenzij u het build script wijzigen voor de rand van de IoT-modules of voorbeeld uitvoerbare bestanden in niet-standaardlocaties plaatsen.</span><span class="sxs-lookup"><span data-stu-id="a312d-111">This configuration file works as is unless you modify the build script to place the IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="a312d-112">De module-paden zijn ten opzichte van de map waar de Hallo\_world\_sample.exe zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="a312d-112">The module paths are relative to the directory where the hello\_world\_sample.exe is located.</span></span> <span data-ttu-id="a312d-113">Het voorbeeld-JSON-configuratiebestand schrijft standaard 'log.txt' in uw huidige werkmap.</span><span class="sxs-lookup"><span data-stu-id="a312d-113">The sample JSON configuration file defaults to writing 'log.txt' in your current working directory.</span></span>

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

1. <span data-ttu-id="a312d-114">Navigeer naar de **bouwen** map in de hoofdmap van uw lokale exemplaar van de **iot-edge** opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="a312d-114">Navigate to the **build** folder in the root of your local copy of the **iot-edge** repository.</span></span>

1. <span data-ttu-id="a312d-115">Voer de volgende opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="a312d-115">Run the following command:</span></span>

    ```cmd
    samples\hello_world\Debug\hello_world_sample.exe ..\samples\hello_world\src\hello_world_win.json
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]
