---
title: Maken van uw eerste Azure IoT Gateway module | Microsoft Docs
description: Maak een module en toe te voegen aan een voorbeeld-app voor het aanpassen van de module gedrag.
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
ms.openlocfilehash: 5e28422158684c3aaf0ac3fdf5b19c80fbccfb02
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-5-create-your-first-azure-iot-gateway-module"></a><span data-ttu-id="5abf4-103">Les 5: Uw eerste Azure IoT Gateway-module maken</span><span class="sxs-lookup"><span data-stu-id="5abf4-103">Lesson 5: Create your first Azure IoT Gateway module</span></span>
<span data-ttu-id="5abf4-104">Azure IoT rand kunt u modules die zijn geschreven in Java, .NET of Node.js bouwen, deze zelfstudie leert u de stappen voor het bouwen van een module in C.</span><span class="sxs-lookup"><span data-stu-id="5abf4-104">While Azure IoT Edge allows you to build modules written in Java, .NET, or Node.js, this tutorial walks you through the steps for building a module in C.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="5abf4-105">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="5abf4-105">What you will do</span></span>

- <span data-ttu-id="5abf4-106">Compileer en voer de hello_world voorbeeld-app op Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="5abf4-106">Compile and run the hello_world sample app on Intel NUC.</span></span>
- <span data-ttu-id="5abf4-107">Maak een module en op Intel NUC worden gecompileerd.</span><span class="sxs-lookup"><span data-stu-id="5abf4-107">Create a module and compile it on Intel NUC.</span></span>
- <span data-ttu-id="5abf4-108">De nieuwe module toevoegen aan de hello_world voorbeeld-app en voer vervolgens het voorbeeld op Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="5abf4-108">Add the new module to the hello_world sample app and then run the sample on Intel NUC.</span></span> <span data-ttu-id="5abf4-109">De nieuwe module 'hello_world'-berichten met een tijdstempel wordt afgedrukt.</span><span class="sxs-lookup"><span data-stu-id="5abf4-109">The new module prints out "hello_world" messages with a timestamp.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5abf4-110">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="5abf4-110">What you will learn</span></span>

- <span data-ttu-id="5abf4-111">Het compileren en een voorbeeld-app op Intel NUC uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="5abf4-111">How to compile and run a sample app on Intel NUC.</span></span>
- <span data-ttu-id="5abf4-112">Het maken van een module.</span><span class="sxs-lookup"><span data-stu-id="5abf4-112">How to create a module.</span></span>
- <span data-ttu-id="5abf4-113">Het module toevoegen aan een voorbeeld-app.</span><span class="sxs-lookup"><span data-stu-id="5abf4-113">How to add module to a sample app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5abf4-114">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="5abf4-114">What you need</span></span>

<span data-ttu-id="5abf4-115">Azure IoT-rand die is geïnstalleerd op de hostcomputer.</span><span class="sxs-lookup"><span data-stu-id="5abf4-115">Azure IoT Edge that has been installed on your host computer.</span></span>

## <a name="folder-structure"></a><span data-ttu-id="5abf4-116">Mapstructuur</span><span class="sxs-lookup"><span data-stu-id="5abf4-116">Folder structure</span></span>

<span data-ttu-id="5abf4-117">In de submap les 5 van de voorbeeldcode die u in les 1 gekloond, er is een `module` map en een `sample` map.</span><span class="sxs-lookup"><span data-stu-id="5abf4-117">In the Lesson 5 subfolder of the sample code which you cloned in lesson 1, there is a `module` folder and a `sample` folder.</span></span>

![my_module](media/iot-hub-gateway-kit-lessons/lesson5/my_module.png)

- <span data-ttu-id="5abf4-119">De `module/my_module` map bevat de broncode en het script voor het bouwen van de module.</span><span class="sxs-lookup"><span data-stu-id="5abf4-119">The `module/my_module` folder contains the source code and script to build the module.</span></span>
- <span data-ttu-id="5abf4-120">De `sample` map bevat de broncode en het script voor het bouwen van de voorbeeld-app.</span><span class="sxs-lookup"><span data-stu-id="5abf4-120">The `sample` folder contains the source code and script to build the sample app.</span></span>

## <a name="compile-and-run-the-helloworld-sample-app-on-intel-nuc"></a><span data-ttu-id="5abf4-121">Compileer en voer de hello_world voorbeeld-app op Intel NUC</span><span class="sxs-lookup"><span data-stu-id="5abf4-121">Compile and run the hello_world sample app on Intel NUC</span></span>

<span data-ttu-id="5abf4-122">De `hello_world` voorbeeld maakt u een gateway op basis van de `hello_world.json` bestand waarin de twee vooraf gedefinieerde modules die zijn gekoppeld aan de app.</span><span class="sxs-lookup"><span data-stu-id="5abf4-122">The `hello_world` sample creates a gateway based on the `hello_world.json` file which specifies the two predefined modules associated with the app.</span></span> <span data-ttu-id="5abf4-123">De gateway-logboeken een 'Hallo wereld'-bericht naar een bestand om de vijf seconden.</span><span class="sxs-lookup"><span data-stu-id="5abf4-123">The gateway logs a "hello world" message to a file every 5 seconds.</span></span> <span data-ttu-id="5abf4-124">In deze sectie maakt u Compileer en voer de `hello_world` app met de standaardmodule.</span><span class="sxs-lookup"><span data-stu-id="5abf4-124">In this section, you compile and run the `hello_world` app with its default module.</span></span>

<span data-ttu-id="5abf4-125">Het compileren en uitvoeren van de `hello_world` app, als volgt te werk op de hostcomputer:</span><span class="sxs-lookup"><span data-stu-id="5abf4-125">To compile and run the `hello_world` app, follow these steps on your host computer:</span></span>

1. <span data-ttu-id="5abf4-126">De configuratiebestanden initialiseren met de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="5abf4-126">Initialize the configuration files by running the following commands:</span></span>

   ```bash
   cd iot-hub-c-intel-nuc-gateway-getting-started
   cd Lesson5
   npm install
   gulp init
   ```

1. <span data-ttu-id="5abf4-127">Het configuratiebestand van de gateway met het MAC-adres van Intel NUC bijwerken.</span><span class="sxs-lookup"><span data-stu-id="5abf4-127">Update the gateway configuration file with the MAC address of Intel NUC.</span></span> <span data-ttu-id="5abf4-128">Deze stap overslaan als u de les hebt doorlopen [configureren en uitvoeren van een voorbeeldtoepassing uitschakelen][config_ble].</span><span class="sxs-lookup"><span data-stu-id="5abf4-128">Skip this step if you have gone through the lesson to [configure and run a BLE sample application][config_ble].</span></span>

   1. <span data-ttu-id="5abf4-129">Open het configuratiebestand van de gateway met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="5abf4-129">Open the gateway configuration file by running the following command:</span></span>

      ```bash
      # For Windows command prompt
      code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json

      # For MacOS or Ubuntu
      code ~/.iot-hub-getting-started/config-gateway.json
      ```

   1. <span data-ttu-id="5abf4-130">Update van de gateway MAC-adres wanneer u [Intel NUC als IoT gateway instellen][setup_nuc], en sla het bestand.</span><span class="sxs-lookup"><span data-stu-id="5abf4-130">Update the gateway's MAC address when you [set up Intel NUC as a IoT gateway][setup_nuc], and then save the file.</span></span>

1. <span data-ttu-id="5abf4-131">De voorbeeldcode van de bron worden gecompileerd met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="5abf4-131">Compile the sample source code by running the following command:</span></span>

   ```bash
   gulp compile
   ```

   <span data-ttu-id="5abf4-132">De opdracht worden de voorbeeldcode van de gegevensbron overgebracht naar Intel NUC en wordt uitgevoerd `build.sh` voor het compileren van het.</span><span class="sxs-lookup"><span data-stu-id="5abf4-132">The command transfers the sample source code to Intel NUC and runs `build.sh` to compile it.</span></span>

1. <span data-ttu-id="5abf4-133">Voer de `hello_world` app op Intel NUC met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="5abf4-133">Run the `hello_world` app on Intel NUC by running the following command:</span></span>

   ```bash
   gulp run
   ```

   <span data-ttu-id="5abf4-134">De opdracht wordt uitgevoerd `../Tools/run-hello-world.js` die is opgegeven in `config.json` starten van de voorbeeld-app op Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="5abf4-134">The command runs `../Tools/run-hello-world.js` that is specified in `config.json` to start the sample app on Intel NUC.</span></span>

   ![run_sample](media/iot-hub-gateway-kit-lessons/lesson5/run_sample.png)

## <a name="create-a-new-module-and-compile-it-on-intel-nuc"></a><span data-ttu-id="5abf4-136">Maak een nieuwe module gecompileerd en op Intel NUC</span><span class="sxs-lookup"><span data-stu-id="5abf4-136">Create a new module and compile it on Intel NUC</span></span>

<span data-ttu-id="5abf4-137">De onderstaande stappen helpt u bij het maken van een nieuwe module en op Intel NUC worden gecompileerd.</span><span class="sxs-lookup"><span data-stu-id="5abf4-137">The steps below walk you through creating a new module and compile it on Intel NUC.</span></span> <span data-ttu-id="5abf4-138">De module wordt afgedrukt berichten met een tijdstempel nadat deze is ontvangen.</span><span class="sxs-lookup"><span data-stu-id="5abf4-138">The module prints out messages with a timestamp upon receiving them.</span></span> <span data-ttu-id="5abf4-139">In deze sectie maakt u uw eerste aangepaste gateway-module.</span><span class="sxs-lookup"><span data-stu-id="5abf4-139">You will create your first customized gateway module in this section.</span></span>

<span data-ttu-id="5abf4-140">Iedere module Azure IoT Edge moet de volgende interfaces implementeren:</span><span class="sxs-lookup"><span data-stu-id="5abf4-140">Any Azure IoT Edge module must implement the following interfaces:</span></span>

   ```C
   pfModule_ParseConfigurationFromJson Module_ParseConfigurationFromJson
   pfModule_FreeConfiguration Module_FreeConfiguration
   pfModule_Create Module_Create
   pfModule_Destroy Module_Destroy
   pfModule_Receive Module_Receive
   ```

<span data-ttu-id="5abf4-141">U kunt desgewenst de volgende interface implementeren:</span><span class="sxs-lookup"><span data-stu-id="5abf4-141">You can optionally implement the following interface:</span></span>

   ```C
   pfModule_Start Module_Start
   ```

<span data-ttu-id="5abf4-142">Het volgende diagram toont de status van belangrijke paden van een module.</span><span class="sxs-lookup"><span data-stu-id="5abf4-142">The following diagram shows the important state paths of a module.</span></span> <span data-ttu-id="5abf4-143">De vierkante rechthoeken vertegenwoordigen methoden die u voor bewerkingen uitvoeren wanneer de module worden verplaatst tussen de statussen implementeren.</span><span class="sxs-lookup"><span data-stu-id="5abf4-143">The square rectangles represent methods you implement to perform operations when the module moves between states.</span></span> <span data-ttu-id="5abf4-144">De ovalen worden belangrijke weergegeven in de module worden.</span><span class="sxs-lookup"><span data-stu-id="5abf4-144">The ovals are major states the module can be in.</span></span>

![state_path](media/iot-hub-gateway-kit-lessons/lesson5/state_path.png)

<span data-ttu-id="5abf4-146">Nu gaan we een module op basis van de sjabloon te maken:</span><span class="sxs-lookup"><span data-stu-id="5abf4-146">Now let’s create a module based on the template:</span></span>

1. <span data-ttu-id="5abf4-147">Open de sjabloonmap met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="5abf4-147">Open the template folder by running the following command:</span></span>

   ```bash
   code module/my_module
   ```

   ![code_module](media/iot-hub-gateway-kit-lessons/lesson5/code_module.png)

   - <span data-ttu-id="5abf4-149">`src/my_module.c`fungeert als een sjabloon voor het maken van een module.</span><span class="sxs-lookup"><span data-stu-id="5abf4-149">`src/my_module.c` serves as a template that facilitates the creation of a module.</span></span> <span data-ttu-id="5abf4-150">De sjabloon verklaart de interfaces.</span><span class="sxs-lookup"><span data-stu-id="5abf4-150">The template declares the interfaces.</span></span> <span data-ttu-id="5abf4-151">U hoeft te doen is het toevoegen van logica voor de `MyModule_Receive` functie.</span><span class="sxs-lookup"><span data-stu-id="5abf4-151">All you need to do is to add logic to the `MyModule_Receive` function.</span></span>
   - <span data-ttu-id="5abf4-152">`build.sh`het build-script voor het compileren van de module voor op Intel NUC is.</span><span class="sxs-lookup"><span data-stu-id="5abf4-152">`build.sh` is the build script to compile the module on Intel NUC.</span></span>
1. <span data-ttu-id="5abf4-153">Open de `src/my_module.c` -bestand en bevatten twee header-bestanden:</span><span class="sxs-lookup"><span data-stu-id="5abf4-153">Open the `src/my_module.c` file and include two header files:</span></span>

   ```C
   #include <stdio.h>
   #include "azure_c_shared_utility/xlogging.h"
   ```

1. <span data-ttu-id="5abf4-154">Voeg de volgende code naar de `MyModule_Receive` functie:</span><span class="sxs-lookup"><span data-stu-id="5abf4-154">Add the following code to the `MyModule_Receive` function:</span></span>

   ```C
   if (message == NULL)
   {
      LogError("invalid arg message");
   }
   else
   {
      // get the message content
      const CONSTBUFFER * content = Message_GetContent(message);
      // get the local time and format it
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
                  LogError("unable to strftime");
              }
              else
              {
                  printf("[%s] %.*s\r\n", timetemp, (int)content->size, content->buffer);
              }
          }
      }
   }
   ```

1. <span data-ttu-id="5abf4-155">Update de `config.json` te geven de `workspace` map op de hostcomputer en het pad van de implementatie op Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="5abf4-155">Update the `config.json` file to specify the `workspace` folder on your host computer and the deployment path on Intel NUC.</span></span> <span data-ttu-id="5abf4-156">Tijdens het compileren van de bestanden in de `workspace` map wordt overgedragen naar het pad van de implementatie.</span><span class="sxs-lookup"><span data-stu-id="5abf4-156">During compiling, the files in the `workspace` folder will be transferred to the deployment path.</span></span>

   1. <span data-ttu-id="5abf4-157">Open de `config.json` bestand met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="5abf4-157">Open the `config.json` file by running the following command:</span></span>

      ```bash
      code config.json
      ```

   1. <span data-ttu-id="5abf4-158">Update `config.json` met de volgende configuratie:</span><span class="sxs-lookup"><span data-stu-id="5abf4-158">Update `config.json` with the following configuration:</span></span>

      ```json
      "workspace": "./module/my_module",
      "deploy_path": "module/my_module"
      ```

      ![config_json](media/iot-hub-gateway-kit-lessons/lesson5/config_json.png)

1. <span data-ttu-id="5abf4-160">Compileren van de module met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="5abf4-160">Compile the module by running the following command:</span></span>

   ```bash
   gulp compile
   ```

   <span data-ttu-id="5abf4-161">De opdracht worden de broncode overgebracht naar Intel NUC en wordt uitgevoerd `build.sh` voor het compileren van de module.</span><span class="sxs-lookup"><span data-stu-id="5abf4-161">The command transfers the source code to Intel NUC and runs `build.sh` to compile the module.</span></span>

## <a name="add-the-module-to-the-helloworld-sample-app-and-run-the-app-on-intel-nuc"></a><span data-ttu-id="5abf4-162">De module toevoegen aan de hello_world voorbeeld-app en voer de app op Intel NUC</span><span class="sxs-lookup"><span data-stu-id="5abf4-162">Add the module to the hello_world sample app and run the app on Intel NUC</span></span>

<span data-ttu-id="5abf4-163">Volg deze stappen voor het uitvoeren van deze taak:</span><span class="sxs-lookup"><span data-stu-id="5abf4-163">To perform this task, follow these steps:</span></span>

1. <span data-ttu-id="5abf4-164">Lijst alle de beschikbare module binaire bestanden (.so-bestanden) op Intel NUC met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="5abf4-164">List all the available module binaries (.so files) on Intel NUC by running the following command:</span></span>

   ```bash
   gulp modules --list
   ```

   <span data-ttu-id="5abf4-165">Het binaire pad van `my_module` gecompileerde zou moeten worden vermeld als hieronder:</span><span class="sxs-lookup"><span data-stu-id="5abf4-165">The binary path of `my_module` that you compiled should be listed as below:</span></span>

   ```path
   /root/gateway_sample/module/my_module/build/libmy_module.so
   ```

   <span data-ttu-id="5abf4-166">Als u wijzigt de standaardgebruikersnaam aanmelding in `config-gateway.json`, binair pad wordt gestart met `home/<your username>` in plaats van `root`.</span><span class="sxs-lookup"><span data-stu-id="5abf4-166">If you change the default login username in `config-gateway.json`, the binary path will start with `home/<your username>` instead of `root`.</span></span>

1. <span data-ttu-id="5abf4-167">Voeg `my_module` naar de `hello_world` voorbeeld-app:</span><span class="sxs-lookup"><span data-stu-id="5abf4-167">Add `my_module` to the `hello_world` sample app:</span></span>

   1. <span data-ttu-id="5abf4-168">Open de `hello_world.json` bestand met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="5abf4-168">Open the `hello_world.json` file by running the following command:</span></span>

      ```bash
      code sample/hello_world/src/hello_world.json
      ```

   1. <span data-ttu-id="5abf4-169">Voeg de volgende code naar de `modules` sectie:</span><span class="sxs-lookup"><span data-stu-id="5abf4-169">Add the following code to the `modules` section:</span></span>

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

      <span data-ttu-id="5abf4-170">De waarde van `module.path` moet `/root/gateway_sample/module/my_module/build/libmy_module.so`.</span><span class="sxs-lookup"><span data-stu-id="5abf4-170">The value of `module.path` should be `/root/gateway_sample/module/my_module/build/libmy_module.so`.</span></span> <span data-ttu-id="5abf4-171">De code declareert `my_module` moet worden gekoppeld met de gateway, evenals de locatie van de binaire opgegeven module in `module.path`.</span><span class="sxs-lookup"><span data-stu-id="5abf4-171">The code declares `my_module` to be associated with the gateway as well as the location of the module binary specified in `module.path`.</span></span>
   1. <span data-ttu-id="5abf4-172">Voeg de volgende code naar de `links` sectie:</span><span class="sxs-lookup"><span data-stu-id="5abf4-172">Add the following code to the `links` section:</span></span>

      ```json
      {
        "source": "hello_world",
        "sink": "my_module"
      }
      ```

      <span data-ttu-id="5abf4-173">Deze code geeft aan dat berichten worden verzonden vanaf de `hello_world` module `my_module`.</span><span class="sxs-lookup"><span data-stu-id="5abf4-173">This code specifies that messages are transferred from the `hello_world` module to `my_module`.</span></span>

      ![hello_world_json](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_json.png)

1. <span data-ttu-id="5abf4-175">Voer de `hello_world` voorbeeld-app met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="5abf4-175">Run the `hello_world` sample app by running the following command:</span></span>

   ```bash
   gulp run --config sample/hello_world/src/hello_world.json
   ```

   <span data-ttu-id="5abf4-176">De `--config` parameter dwingt de `run-hello-world.js` script uit te voeren met behulp van de `hello_world.json` bestand.</span><span class="sxs-lookup"><span data-stu-id="5abf4-176">The `--config` parameter forces the `run-hello-world.js` script to run by using the `hello_world.json` file.</span></span>

   ![hello_world_new](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_new.png)

<span data-ttu-id="5abf4-178">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="5abf4-178">Congratulations.</span></span> <span data-ttu-id="5abf4-179">Nu ziet u het gedrag van deze nieuwe module, gewoon worden afgedrukt 'Hallo wereld'-berichten met een tijdstempel, een ander resultaat van de oorspronkelijke 'hello_world'-module.</span><span class="sxs-lookup"><span data-stu-id="5abf4-179">You can now see the behavior of this new module, it simply prints out "hello world" messages with a timestamp, a different result from the original "hello_world" module.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5abf4-180">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5abf4-180">Next Steps</span></span>

<span data-ttu-id="5abf4-181">U hebt een nieuwe module gemaakt, worden deze toegevoegd aan de hello_world voorbeeld en download de voorbeeldapp uit te voeren met de nieuwe module op de gateway.</span><span class="sxs-lookup"><span data-stu-id="5abf4-181">You’ve created a new module, added it to the hello_world sample, and get the sample app to run with the new module on your gateway.</span></span> <span data-ttu-id="5abf4-182">Als u weten over Azure IoT gateway modules wilt, vindt u hier meer module-voorbeelden: [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules).</span><span class="sxs-lookup"><span data-stu-id="5abf4-182">If you want to learn more about Azure IoT gateway modules, you can find more module samples here: [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules).</span></span>

<!-- Images and links -->

[config_ble]: iot-hub-gateway-kit-c-lesson3-configure-ble-app.md
[setup_nuc]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
