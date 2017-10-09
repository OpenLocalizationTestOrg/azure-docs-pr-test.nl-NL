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
# <a name="lesson-5-create-your-first-azure-iot-gateway-module"></a>Les 5: Uw eerste Azure IoT Gateway-module maken
Azure IoT rand kunt toobuild modules die zijn geschreven in Java, .NET of Node.js, leert deze zelfstudie u Hallo voor het bouwen van een module in C.

## <a name="what-you-will-do"></a>Wat u doet

- Compileren en Hallo hello_world voorbeeld-app op Intel NUC uitgevoerd.
- Maak een module en op Intel NUC worden gecompileerd.
- Hallo nieuwe module toohello hello_world voorbeeld-app toevoegen en voer vervolgens Hallo voorbeeld op Intel NUC. de nieuwe module Hallo 'hello_world'-berichten met een tijdstempel wordt afgedrukt.

## <a name="what-you-will-learn"></a>Wat u leert

- Hoe toocompile en een voorbeeld-app op Intel NUC uitgevoerd.
- Hoe toocreate een module.
- Hoe tooadd module tooa voorbeeld-app.

## <a name="what-you-need"></a>Wat u nodig hebt

Azure IoT-rand die is geïnstalleerd op de hostcomputer.

## <a name="folder-structure"></a>Mapstructuur

In de submap Hallo les 5 van Hallo voorbeeldcode die u in les 1 gekloond, er is een `module` map en een `sample` map.

![my_module](media/iot-hub-gateway-kit-lessons/lesson5/my_module.png)

- Hallo `module/my_module` map Hallo source code en scripts toobuild Hallo-module bevat.
- Hallo `sample` map Hallo source code en scripts toobuild Hallo voorbeeld-app bevat.

## <a name="compile-and-run-hello-helloworld-sample-app-on-intel-nuc"></a>Compileren en Hallo hello_world voorbeeld-app uitvoeren op Intel NUC

Hallo `hello_world` voorbeeld maakt u een gateway op basis van Hallo `hello_world.json` bestand waarin Hallo twee vooraf gedefinieerde modules die zijn gekoppeld aan het Hallo-app. Hallo-gateway-een "Hallo wereld" tooa berichtbestand Logboeken om de vijf seconden. In deze sectie maakt u compileren en uitvoeren van Hallo `hello_world` app met de standaardmodule.

toocompile en Voer Hallo `hello_world` app, als volgt te werk op de hostcomputer:

1. Hallo-configuratiebestanden door het uitvoeren van de volgende opdrachten Hallo initialiseren:

   ```bash
   cd iot-hub-c-intel-nuc-gateway-getting-started
   cd Lesson5
   npm install
   gulp init
   ```

1. Hallo gateway-configuratiebestand Hello MAC-adres van Intel NUC bijwerken. Deze stap overslaan als u Hallo les te hebben doorlopen[configureren en uitvoeren van een voorbeeldtoepassing uitschakelen][config_ble].

   1. Hallo gateway-configuratiebestand openen door het uitvoeren van de volgende opdracht Hallo:

      ```bash
      # For Windows command prompt
      code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json

      # For MacOS or Ubuntu
      code ~/.iot-hub-getting-started/config-gateway.json
      ```

   1. Update Hallo gateway MAC-adres wanneer u [Intel NUC als IoT gateway instellen][setup_nuc], en sla Hallo-bestand.

1. Hallo voorbeeldcode gecompileerd door het uitvoeren van de volgende opdracht Hallo:

   ```bash
   gulp compile
   ```

   Hallo opdracht Hallo voorbeeld source code tooIntel NUC overgedragen en wordt uitgevoerd `build.sh` toocompile deze.

1. Voer Hallo `hello_world` app op Intel NUC door het uitvoeren van de volgende opdracht Hallo:

   ```bash
   gulp run
   ```

   opdracht is uitgevoerd Hallo `../Tools/run-hello-world.js` die is opgegeven in `config.json` toostart Hallo voorbeeld-app op Intel NUC.

   ![run_sample](media/iot-hub-gateway-kit-lessons/lesson5/run_sample.png)

## <a name="create-a-new-module-and-compile-it-on-intel-nuc"></a>Maak een nieuwe module gecompileerd en op Intel NUC

Hallo stappen hieronder helpt u bij het maken van een nieuwe module en op Intel NUC worden gecompileerd. berichten met een tijdstempel bij ontvangst van deze module Hello wordt afgedrukt. In deze sectie maakt u uw eerste aangepaste gateway-module.

Iedere module Azure IoT Edge moet Hallo volgende interfaces implementeren:

   ```C
   pfModule_ParseConfigurationFromJson Module_ParseConfigurationFromJson
   pfModule_FreeConfiguration Module_FreeConfiguration
   pfModule_Create Module_Create
   pfModule_Destroy Module_Destroy
   pfModule_Receive Module_Receive
   ```

U kunt eventueel Hallo interface volgende implementeren:

   ```C
   pfModule_Start Module_Start
   ```

Hallo toont volgende diagram Hallo belangrijk status paden van een module. Hallo vierkante rechthoeken vertegenwoordigen methoden u tooperform operations implementeren wanneer Hallo-module worden verplaatst tussen statussen. Hallo ovalen worden belangrijke Hallo module deel kan uitmaken.

![state_path](media/iot-hub-gateway-kit-lessons/lesson5/state_path.png)

Nu gaan we een module op basis van sjabloon Hallo maken:

1. Open de sjabloonmap Hallo door het uitvoeren van de volgende opdracht Hallo:

   ```bash
   code module/my_module
   ```

   ![code_module](media/iot-hub-gateway-kit-lessons/lesson5/code_module.png)

   - `src/my_module.c`fungeert als een sjabloon voor Hallo maken van een module. Hallo sjabloon declareert Hallo-interfaces. Toodo hoeft u tooadd logica toohello `MyModule_Receive` functie.
   - `build.sh`Hallo build script toocompile Hallo-module op Intel NUC is.
1. Open Hallo `src/my_module.c` bestands- en twee header-bestanden bevatten:

   ```C
   #include <stdio.h>
   #include "azure_c_shared_utility/xlogging.h"
   ```

1. Hallo na code toohello toevoegen `MyModule_Receive` functie:

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

1. Update Hallo `config.json` bestand toospecify hello `workspace` map op uw host computer en Hallo distributiepad op Intel NUC. Tijdens het compileren, Hallo bestanden in Hallo `workspace` map worden overgedragen toohello implementatie pad.

   1. Open Hallo `config.json` bestand door het uitvoeren van de volgende opdracht Hallo:

      ```bash
      code config.json
      ```

   1. Update `config.json` Hello volgende configuratie:

      ```json
      "workspace": "./module/my_module",
      "deploy_path": "module/my_module"
      ```

      ![config_json](media/iot-hub-gateway-kit-lessons/lesson5/config_json.png)

1. Hallo-module worden gecompileerd door het uitvoeren van de volgende opdracht Hallo:

   ```bash
   gulp compile
   ```

   Hallo opdracht Hallo source code tooIntel NUC overgedragen en wordt uitgevoerd `build.sh` toocompile Hallo-module.

## <a name="add-hello-module-toohello-helloworld-sample-app-and-run-hello-app-on-intel-nuc"></a>Hallo module toohello hello_world voorbeeld-app toevoegen en Hallo-app op Intel NUC uitvoeren

tooperform dit taak als volgt te werk:

1. Lijst alle Hallo beschikbaar module binaire bestanden (.so-bestanden) op Intel NUC door het uitvoeren van de volgende opdracht Hallo:

   ```bash
   gulp modules --list
   ```

   binair pad Hallo van `my_module` gecompileerde zou moeten worden vermeld als hieronder:

   ```path
   /root/gateway_sample/module/my_module/build/libmy_module.so
   ```

   Als u Hallo standaardgebruikersnaam aanmelding in wijzigt `config-gateway.json`, Hallo binair pad wordt gestart met `home/<your username>` in plaats van `root`.

1. Voeg `my_module` toohello `hello_world` voorbeeld-app:

   1. Open Hallo `hello_world.json` bestand door het uitvoeren van de volgende opdracht Hallo:

      ```bash
      code sample/hello_world/src/hello_world.json
      ```

   1. Hallo na code toohello toevoegen `modules` sectie:

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

      waarde van Hallo `module.path` moet `/root/gateway_sample/module/my_module/build/libmy_module.so`. Hallo code declareert `my_module` toobe die zijn gekoppeld aan het Hallo-gateway, evenals Hallo-locatie van Hallo module binair is opgegeven in `module.path`.
   1. Hallo na code toohello toevoegen `links` sectie:

      ```json
      {
        "source": "hello_world",
        "sink": "my_module"
      }
      ```

      Deze code geeft aan dat berichten worden overgebracht van Hallo `hello_world` module te`my_module`.

      ![hello_world_json](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_json.png)

1. Voer Hallo `hello_world` voorbeeld-app door het uitvoeren van de volgende opdracht Hallo:

   ```bash
   gulp run --config sample/hello_world/src/hello_world.json
   ```

   Hallo `--config` parameter zorgt ervoor dat Hallo `run-hello-world.js` toorun script met behulp van Hallo `hello_world.json` bestand.

   ![hello_world_new](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_new.png)

Gefeliciteerd. U kunt nu zien Hallo gedrag van deze nieuwe module, gewoon worden afgedrukt 'Hallo wereld'-berichten met een tijdstempel, een ander resultaat uit de oorspronkelijke 'hello_world' module Hallo.

## <a name="next-steps"></a>Volgende stappen

U hebt gemaakt van een nieuwe module, dit hebt toegevoegd en get Hallo voorbeeld-app toorun met de nieuwe module Hallo toohello hello_world voorbeelden op uw gateway. Als u meer informatie over Azure IoT gateway modules toolearn wilt, kunt u hier meer module-voorbeelden zoeken: [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules).

<!-- Images and links -->

[config_ble]: iot-hub-gateway-kit-c-lesson3-configure-ble-app.md
[setup_nuc]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
