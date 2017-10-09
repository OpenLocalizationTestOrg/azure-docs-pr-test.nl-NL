---
title: aaaCreate uw eerste Azure IoT Gateway module | Microsoft Docs
description: Maak een module en voeg deze tooa voorbeeld-app toocustomize module gedrag.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: 
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: cd7660f4-7b8b-4091-8d71-bb8723165b0b
ms.service: iot-hub
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 48996fc026c8b708e328b5629801465810e5b6a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="lesson-5-create-your-first-azure-iot-gateway-module"></a><span data-ttu-id="5f383-103">Les 5: Uw eerste Azure IoT Gateway-module maken</span><span class="sxs-lookup"><span data-stu-id="5f383-103">Lesson 5: Create your first Azure IoT Gateway module</span></span>
<span data-ttu-id="5f383-104">Azure IoT rand kunt toobuild modules die zijn geschreven in Java, .NET of Node.js, leert deze zelfstudie u Hallo voor het bouwen van een module in C.</span><span class="sxs-lookup"><span data-stu-id="5f383-104">While Azure IoT Edge allows you toobuild modules written in Java, .NET, or Node.js, this tutorial walks you through hello steps for building a module in C.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="5f383-105">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="5f383-105">What you will do</span></span>

- <span data-ttu-id="5f383-106">Compileren en Hallo hello_world voorbeeld-app op Intel NUC uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5f383-106">Compile and run hello hello_world sample app on Intel NUC.</span></span>
- <span data-ttu-id="5f383-107">Maak een module en op Intel NUC worden gecompileerd.</span><span class="sxs-lookup"><span data-stu-id="5f383-107">Create a module and compile it on Intel NUC.</span></span>
- <span data-ttu-id="5f383-108">Hallo nieuwe module toohello hello_world voorbeeld-app toevoegen en voer vervolgens Hallo voorbeeld op Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="5f383-108">Add hello new module toohello hello_world sample app and then run hello sample on Intel NUC.</span></span> <span data-ttu-id="5f383-109">de nieuwe module Hallo 'hello_world'-berichten met een tijdstempel wordt afgedrukt.</span><span class="sxs-lookup"><span data-stu-id="5f383-109">hello new module prints out "hello_world" messages with a timestamp.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5f383-110">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="5f383-110">What you will learn</span></span>

- <span data-ttu-id="5f383-111">Hoe toocompile en een voorbeeld-app op Intel NUC uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5f383-111">How toocompile and run a sample app on Intel NUC.</span></span>
- <span data-ttu-id="5f383-112">Hoe toocreate een module.</span><span class="sxs-lookup"><span data-stu-id="5f383-112">How toocreate a module.</span></span>
- <span data-ttu-id="5f383-113">Hoe tooadd module tooa voorbeeld-app.</span><span class="sxs-lookup"><span data-stu-id="5f383-113">How tooadd module tooa sample app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5f383-114">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="5f383-114">What you need</span></span>

<span data-ttu-id="5f383-115">Azure IoT-rand die is geïnstalleerd op de hostcomputer.</span><span class="sxs-lookup"><span data-stu-id="5f383-115">Azure IoT Edge that has been installed on your host computer.</span></span>

## <a name="folder-structure"></a><span data-ttu-id="5f383-116">Mapstructuur</span><span class="sxs-lookup"><span data-stu-id="5f383-116">Folder structure</span></span>

<span data-ttu-id="5f383-117">In de submap Hallo les 5 van Hallo voorbeeldcode die u in les 1 gekloond, er is een `module` map en een `sample` map.</span><span class="sxs-lookup"><span data-stu-id="5f383-117">In hello Lesson 5 subfolder of hello sample code which you cloned in lesson 1, there is a `module` folder and a `sample` folder.</span></span>

![my_module](media/iot-hub-gateway-kit-lessons/lesson5/my_module.png)

- <span data-ttu-id="5f383-119">Hallo `module/my_module` map Hallo source code en scripts toobuild Hallo-module bevat.</span><span class="sxs-lookup"><span data-stu-id="5f383-119">hello `module/my_module` folder contains hello source code and script toobuild hello module.</span></span>
- <span data-ttu-id="5f383-120">Hallo `sample` map Hallo source code en scripts toobuild Hallo voorbeeld-app bevat.</span><span class="sxs-lookup"><span data-stu-id="5f383-120">hello `sample` folder contains hello source code and script toobuild hello sample app.</span></span>

## <a name="compile-and-run-hello-helloworld-sample-app-on-intel-nuc"></a><span data-ttu-id="5f383-121">Compileren en Hallo hello_world voorbeeld-app uitvoeren op Intel NUC</span><span class="sxs-lookup"><span data-stu-id="5f383-121">Compile and run hello hello_world sample app on Intel NUC</span></span>

<span data-ttu-id="5f383-122">Hallo `hello_world` voorbeeld maakt u een gateway op basis van Hallo `hello_world.json` bestand waarin Hallo twee vooraf gedefinieerde modules die zijn gekoppeld aan het Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="5f383-122">hello `hello_world` sample creates a gateway based on hello `hello_world.json` file which specifies hello two predefined modules associated with hello app.</span></span> <span data-ttu-id="5f383-123">Hallo-gateway-een "Hallo wereld" tooa berichtbestand Logboeken om de vijf seconden.</span><span class="sxs-lookup"><span data-stu-id="5f383-123">hello gateway logs a "hello world" message tooa file every 5 seconds.</span></span> <span data-ttu-id="5f383-124">In deze sectie maakt u compileren en uitvoeren van Hallo `hello_world` app met de standaardmodule.</span><span class="sxs-lookup"><span data-stu-id="5f383-124">In this section, you compile and run hello `hello_world` app with its default module.</span></span>

<span data-ttu-id="5f383-125">toocompile en Voer Hallo `hello_world` app, als volgt te werk op de hostcomputer:</span><span class="sxs-lookup"><span data-stu-id="5f383-125">toocompile and run hello `hello_world` app, follow these steps on your host computer:</span></span>

1. <span data-ttu-id="5f383-126">Hallo-configuratiebestanden door het uitvoeren van de volgende opdrachten Hallo initialiseren:</span><span class="sxs-lookup"><span data-stu-id="5f383-126">Initialize hello configuration files by running hello following commands:</span></span>

   ```bash
   cd iot-hub-c-intel-nuc-gateway-getting-started
   cd Lesson5
   npm install
   gulp init
   ```

1. <span data-ttu-id="5f383-127">Hallo gateway-configuratiebestand Hello MAC-adres van Intel NUC bijwerken.</span><span class="sxs-lookup"><span data-stu-id="5f383-127">Update hello gateway configuration file with hello MAC address of Intel NUC.</span></span> <span data-ttu-id="5f383-128">Deze stap overslaan als u Hallo les te hebben doorlopen[configureren en uitvoeren van een voorbeeldtoepassing uitschakelen][config_ble].</span><span class="sxs-lookup"><span data-stu-id="5f383-128">Skip this step if you have gone through hello lesson too[configure and run a BLE sample application][config_ble].</span></span>

   1. <span data-ttu-id="5f383-129">Hallo gateway-configuratiebestand openen door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="5f383-129">Open hello gateway configuration file by running hello following command:</span></span>

      ```bash
      # For Windows command prompt
      code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json

      # For MacOS or Ubuntu
      code ~/.iot-hub-getting-started/config-gateway.json
      ```

   1. <span data-ttu-id="5f383-130">Update Hallo gateway MAC-adres wanneer u [Intel NUC als IoT gateway instellen][setup_nuc], en sla Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="5f383-130">Update hello gateway's MAC address when you [set up Intel NUC as a IoT gateway][setup_nuc], and then save hello file.</span></span>

1. <span data-ttu-id="5f383-131">Hallo voorbeeldcode gecompileerd door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="5f383-131">Compile hello sample source code by running hello following command:</span></span>

   ```bash
   gulp compile
   ```

   <span data-ttu-id="5f383-132">Hallo opdracht Hallo voorbeeld source code tooIntel NUC overgedragen en wordt uitgevoerd `build.sh` toocompile deze.</span><span class="sxs-lookup"><span data-stu-id="5f383-132">hello command transfers hello sample source code tooIntel NUC and runs `build.sh` toocompile it.</span></span>

1. <span data-ttu-id="5f383-133">Voer Hallo `hello_world` app op Intel NUC door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="5f383-133">Run hello `hello_world` app on Intel NUC by running hello following command:</span></span>

   ```bash
   gulp run
   ```

   <span data-ttu-id="5f383-134">opdracht is uitgevoerd Hallo `../Tools/run-hello-world.js` die is opgegeven in `config.json` toostart Hallo voorbeeld-app op Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="5f383-134">hello command runs `../Tools/run-hello-world.js` that is specified in `config.json` toostart hello sample app on Intel NUC.</span></span>

   ![run_sample](media/iot-hub-gateway-kit-lessons/lesson5/run_sample.png)

## <a name="create-a-new-module-and-compile-it-on-intel-nuc"></a><span data-ttu-id="5f383-136">Maak een nieuwe module gecompileerd en op Intel NUC</span><span class="sxs-lookup"><span data-stu-id="5f383-136">Create a new module and compile it on Intel NUC</span></span>

<span data-ttu-id="5f383-137">Hallo stappen hieronder helpt u bij het maken van een nieuwe module en op Intel NUC worden gecompileerd.</span><span class="sxs-lookup"><span data-stu-id="5f383-137">hello steps below walk you through creating a new module and compile it on Intel NUC.</span></span> <span data-ttu-id="5f383-138">berichten met een tijdstempel bij ontvangst van deze module Hello wordt afgedrukt.</span><span class="sxs-lookup"><span data-stu-id="5f383-138">hello module prints out messages with a timestamp upon receiving them.</span></span> <span data-ttu-id="5f383-139">In deze sectie maakt u uw eerste aangepaste gateway-module.</span><span class="sxs-lookup"><span data-stu-id="5f383-139">You will create your first customized gateway module in this section.</span></span>

<span data-ttu-id="5f383-140">Iedere module Azure IoT Edge moet Hallo volgende interfaces implementeren:</span><span class="sxs-lookup"><span data-stu-id="5f383-140">Any Azure IoT Edge module must implement hello following interfaces:</span></span>

   ```C
   pfModule_ParseConfigurationFromJson Module_ParseConfigurationFromJson
   pfModule_FreeConfiguration Module_FreeConfiguration
   pfModule_Create Module_Create
   pfModule_Destroy Module_Destroy
   pfModule_Receive Module_Receive
   ```

<span data-ttu-id="5f383-141">U kunt eventueel Hallo interface volgende implementeren:</span><span class="sxs-lookup"><span data-stu-id="5f383-141">You can optionally implement hello following interface:</span></span>

   ```C
   pfModule_Start Module_Start
   ```

<span data-ttu-id="5f383-142">Hallo toont volgende diagram Hallo belangrijk status paden van een module.</span><span class="sxs-lookup"><span data-stu-id="5f383-142">hello following diagram shows hello important state paths of a module.</span></span> <span data-ttu-id="5f383-143">Hallo vierkante rechthoeken vertegenwoordigen methoden u tooperform operations implementeren wanneer Hallo-module worden verplaatst tussen statussen.</span><span class="sxs-lookup"><span data-stu-id="5f383-143">hello square rectangles represent methods you implement tooperform operations when hello module moves between states.</span></span> <span data-ttu-id="5f383-144">Hallo ovalen worden belangrijke Hallo module deel kan uitmaken.</span><span class="sxs-lookup"><span data-stu-id="5f383-144">hello ovals are major states hello module can be in.</span></span>

![state_path](media/iot-hub-gateway-kit-lessons/lesson5/state_path.png)

<span data-ttu-id="5f383-146">Nu gaan we een module op basis van sjabloon Hallo maken:</span><span class="sxs-lookup"><span data-stu-id="5f383-146">Now let’s create a module based on hello template:</span></span>

1. <span data-ttu-id="5f383-147">Open de sjabloonmap Hallo door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="5f383-147">Open hello template folder by running hello following command:</span></span>

   ```bash
   code module/my_module
   ```

   ![code_module](media/iot-hub-gateway-kit-lessons/lesson5/code_module.png)

   - <span data-ttu-id="5f383-149">`src/my_module.c`fungeert als een sjabloon voor Hallo maken van een module.</span><span class="sxs-lookup"><span data-stu-id="5f383-149">`src/my_module.c` serves as a template that facilitates hello creation of a module.</span></span> <span data-ttu-id="5f383-150">Hallo sjabloon declareert Hallo-interfaces.</span><span class="sxs-lookup"><span data-stu-id="5f383-150">hello template declares hello interfaces.</span></span> <span data-ttu-id="5f383-151">Toodo hoeft u tooadd logica toohello `MyModule_Receive` functie.</span><span class="sxs-lookup"><span data-stu-id="5f383-151">All you need toodo is tooadd logic toohello `MyModule_Receive` function.</span></span>
   - <span data-ttu-id="5f383-152">`build.sh`Hallo build script toocompile Hallo-module op Intel NUC is.</span><span class="sxs-lookup"><span data-stu-id="5f383-152">`build.sh` is hello build script toocompile hello module on Intel NUC.</span></span>
1. <span data-ttu-id="5f383-153">Open Hallo `src/my_module.c` bestands- en twee header-bestanden bevatten:</span><span class="sxs-lookup"><span data-stu-id="5f383-153">Open hello `src/my_module.c` file and include two header files:</span></span>

   ```C
   #include <stdio.h>
   #include "azure_c_shared_utility/xlogging.h"
   ```

1. <span data-ttu-id="5f383-154">Hallo na code toohello toevoegen `MyModule_Receive` functie:</span><span class="sxs-lookup"><span data-stu-id="5f383-154">Add hello following code toohello `MyModule_Receive` function:</span></span>

   ```C
   if (message == NULL)
   {
      LogError("invalid arg message");
   }
   else
   {
      // get hello message content
      const CONSTBUFFER * content = Message_GetContent(message);
      // get hello local time and format it
      time_t temp = time(NULL);
      if (temp == (time_t)-1)
      {
          LogError("time function failed");
      }
      else
      {
          struct tm* t = localtime(&temp);
          if (t == NULL)
          {
              LogError("localtime failed");
          }
          else
          {
              char timetemp[80] = { 0 };
              if (strftime(timetemp, sizeof(timetemp) / sizeof(timetemp[0]), "%c", t) == 0)
              {
                  LogError("unable toostrftime");
              }
              else
              {
                  printf("[%s] %.*s\r\n", timetemp, (int)content->size, content->buffer);
              }
          }
      }
   }
   ```

1. <span data-ttu-id="5f383-155">Update Hallo `config.json` bestand toospecify hello `workspace` map op uw host computer en Hallo distributiepad op Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="5f383-155">Update hello `config.json` file toospecify hello `workspace` folder on your host computer and hello deployment path on Intel NUC.</span></span> <span data-ttu-id="5f383-156">Tijdens het compileren, Hallo bestanden in Hallo `workspace` map worden overgedragen toohello implementatie pad.</span><span class="sxs-lookup"><span data-stu-id="5f383-156">During compiling, hello files in hello `workspace` folder will be transferred toohello deployment path.</span></span>

   1. <span data-ttu-id="5f383-157">Open Hallo `config.json` bestand door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="5f383-157">Open hello `config.json` file by running hello following command:</span></span>

      ```bash
      code config.json
      ```

   1. <span data-ttu-id="5f383-158">Update `config.json` Hello volgende configuratie:</span><span class="sxs-lookup"><span data-stu-id="5f383-158">Update `config.json` with hello following configuration:</span></span>

      ```json
      "workspace": "./module/my_module",
      "deploy_path": "module/my_module"
      ```

      ![config_json](media/iot-hub-gateway-kit-lessons/lesson5/config_json.png)

1. <span data-ttu-id="5f383-160">Hallo-module worden gecompileerd door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="5f383-160">Compile hello module by running hello following command:</span></span>

   ```bash
   gulp compile
   ```

   <span data-ttu-id="5f383-161">Hallo opdracht Hallo source code tooIntel NUC overgedragen en wordt uitgevoerd `build.sh` toocompile Hallo-module.</span><span class="sxs-lookup"><span data-stu-id="5f383-161">hello command transfers hello source code tooIntel NUC and runs `build.sh` toocompile hello module.</span></span>

## <a name="add-hello-module-toohello-helloworld-sample-app-and-run-hello-app-on-intel-nuc"></a><span data-ttu-id="5f383-162">Hallo module toohello hello_world voorbeeld-app toevoegen en Hallo-app op Intel NUC uitvoeren</span><span class="sxs-lookup"><span data-stu-id="5f383-162">Add hello module toohello hello_world sample app and run hello app on Intel NUC</span></span>

<span data-ttu-id="5f383-163">tooperform dit taak als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="5f383-163">tooperform this task, follow these steps:</span></span>

1. <span data-ttu-id="5f383-164">Lijst alle Hallo beschikbaar module binaire bestanden (.so-bestanden) op Intel NUC door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="5f383-164">List all hello available module binaries (.so files) on Intel NUC by running hello following command:</span></span>

   ```bash
   gulp modules --list
   ```

   <span data-ttu-id="5f383-165">binair pad Hallo van `my_module` gecompileerde zou moeten worden vermeld als hieronder:</span><span class="sxs-lookup"><span data-stu-id="5f383-165">hello binary path of `my_module` that you compiled should be listed as below:</span></span>

   ```path
   /root/gateway_sample/module/my_module/build/libmy_module.so
   ```

   <span data-ttu-id="5f383-166">Als u Hallo standaardgebruikersnaam aanmelding in wijzigt `config-gateway.json`, Hallo binair pad wordt gestart met `home/<your username>` in plaats van `root`.</span><span class="sxs-lookup"><span data-stu-id="5f383-166">If you change hello default login username in `config-gateway.json`, hello binary path will start with `home/<your username>` instead of `root`.</span></span>

1. <span data-ttu-id="5f383-167">Voeg `my_module` toohello `hello_world` voorbeeld-app:</span><span class="sxs-lookup"><span data-stu-id="5f383-167">Add `my_module` toohello `hello_world` sample app:</span></span>

   1. <span data-ttu-id="5f383-168">Open Hallo `hello_world.json` bestand door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="5f383-168">Open hello `hello_world.json` file by running hello following command:</span></span>

      ```bash
      code sample/hello_world/src/hello_world.json
      ```

   1. <span data-ttu-id="5f383-169">Hallo na code toohello toevoegen `modules` sectie:</span><span class="sxs-lookup"><span data-stu-id="5f383-169">Add hello following code toohello `modules` section:</span></span>

      ```json
      {
       "name": "my_module",
       "loader": {
       "name": "native",
       "entrypoint": {
       "module.path": "/root/gateway_sample/module/my_module/build/libmy_module.so"
         }
        },
       "args": null
      }
      ```

      <span data-ttu-id="5f383-170">waarde van Hallo `module.path` moet `/root/gateway_sample/module/my_module/build/libmy_module.so`.</span><span class="sxs-lookup"><span data-stu-id="5f383-170">hello value of `module.path` should be `/root/gateway_sample/module/my_module/build/libmy_module.so`.</span></span> <span data-ttu-id="5f383-171">Hallo code declareert `my_module` toobe die zijn gekoppeld aan het Hallo-gateway, evenals Hallo-locatie van Hallo module binair is opgegeven in `module.path`.</span><span class="sxs-lookup"><span data-stu-id="5f383-171">hello code declares `my_module` toobe associated with hello gateway as well as hello location of hello module binary specified in `module.path`.</span></span>
   1. <span data-ttu-id="5f383-172">Hallo na code toohello toevoegen `links` sectie:</span><span class="sxs-lookup"><span data-stu-id="5f383-172">Add hello following code toohello `links` section:</span></span>

      ```json
      {
        "source": "hello_world",
        "sink": "my_module"
      }
      ```

      <span data-ttu-id="5f383-173">Deze code geeft aan dat berichten worden overgebracht van Hallo `hello_world` module te`my_module`.</span><span class="sxs-lookup"><span data-stu-id="5f383-173">This code specifies that messages are transferred from hello `hello_world` module too`my_module`.</span></span>

      ![hello_world_json](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_json.png)

1. <span data-ttu-id="5f383-175">Voer Hallo `hello_world` voorbeeld-app door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="5f383-175">Run hello `hello_world` sample app by running hello following command:</span></span>

   ```bash
   gulp run --config sample/hello_world/src/hello_world.json
   ```

   <span data-ttu-id="5f383-176">Hallo `--config` parameter zorgt ervoor dat Hallo `run-hello-world.js` toorun script met behulp van Hallo `hello_world.json` bestand.</span><span class="sxs-lookup"><span data-stu-id="5f383-176">hello `--config` parameter forces hello `run-hello-world.js` script toorun by using hello `hello_world.json` file.</span></span>

   ![hello_world_new](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_new.png)

<span data-ttu-id="5f383-178">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="5f383-178">Congratulations.</span></span> <span data-ttu-id="5f383-179">U kunt nu zien Hallo gedrag van deze nieuwe module, gewoon worden afgedrukt 'Hallo wereld'-berichten met een tijdstempel, een ander resultaat uit de oorspronkelijke 'hello_world' module Hallo.</span><span class="sxs-lookup"><span data-stu-id="5f383-179">You can now see hello behavior of this new module, it simply prints out "hello world" messages with a timestamp, a different result from hello original "hello_world" module.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5f383-180">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5f383-180">Next Steps</span></span>

<span data-ttu-id="5f383-181">U hebt gemaakt van een nieuwe module, dit hebt toegevoegd en get Hallo voorbeeld-app toorun met de nieuwe module Hallo toohello hello_world voorbeelden op uw gateway.</span><span class="sxs-lookup"><span data-stu-id="5f383-181">You’ve created a new module, added it toohello hello_world sample, and get hello sample app toorun with hello new module on your gateway.</span></span> <span data-ttu-id="5f383-182">Als u meer informatie over Azure IoT gateway modules toolearn wilt, kunt u hier meer module-voorbeelden zoeken: [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules).</span><span class="sxs-lookup"><span data-stu-id="5f383-182">If you want toolearn more about Azure IoT gateway modules, you can find more module samples here: [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules).</span></span>

<!-- Images and links -->

[config_ble]: iot-hub-gateway-kit-c-lesson3-configure-ble-app.md
[setup_nuc]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
