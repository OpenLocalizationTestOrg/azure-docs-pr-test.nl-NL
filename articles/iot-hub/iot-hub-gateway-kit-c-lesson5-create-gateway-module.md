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
# <a name="lesson-5-create-your-first-azure-iot-gateway-module"></a>Les 5: Uw eerste Azure IoT Gateway-module maken
Azure IoT rand kunt u modules die zijn geschreven in Java, .NET of Node.js bouwen, deze zelfstudie leert u de stappen voor het bouwen van een module in C.

## <a name="what-you-will-do"></a>Wat u doet

- Compileer en voer de hello_world voorbeeld-app op Intel NUC.
- Maak een module en op Intel NUC worden gecompileerd.
- De nieuwe module toevoegen aan de hello_world voorbeeld-app en voer vervolgens het voorbeeld op Intel NUC. De nieuwe module 'hello_world'-berichten met een tijdstempel wordt afgedrukt.

## <a name="what-you-will-learn"></a>Wat u leert

- Het compileren en een voorbeeld-app op Intel NUC uitvoeren.
- Het maken van een module.
- Het module toevoegen aan een voorbeeld-app.

## <a name="what-you-need"></a>Wat u nodig hebt

Azure IoT-rand die is geïnstalleerd op de hostcomputer.

## <a name="folder-structure"></a>Mapstructuur

In de submap les 5 van de voorbeeldcode die u in les 1 gekloond, er is een `module` map en een `sample` map.

![my_module](media/iot-hub-gateway-kit-lessons/lesson5/my_module.png)

- De `module/my_module` map bevat de broncode en het script voor het bouwen van de module.
- De `sample` map bevat de broncode en het script voor het bouwen van de voorbeeld-app.

## <a name="compile-and-run-the-helloworld-sample-app-on-intel-nuc"></a>Compileer en voer de hello_world voorbeeld-app op Intel NUC

De `hello_world` voorbeeld maakt u een gateway op basis van de `hello_world.json` bestand waarin de twee vooraf gedefinieerde modules die zijn gekoppeld aan de app. De gateway-logboeken een 'Hallo wereld'-bericht naar een bestand om de vijf seconden. In deze sectie maakt u Compileer en voer de `hello_world` app met de standaardmodule.

Het compileren en uitvoeren van de `hello_world` app, als volgt te werk op de hostcomputer:

1. De configuratiebestanden initialiseren met de volgende opdrachten:

   ```bash
   cd iot-hub-c-intel-nuc-gateway-getting-started
   cd Lesson5
   npm install
   gulp init
   ```

1. Het configuratiebestand van de gateway met het MAC-adres van Intel NUC bijwerken. Deze stap overslaan als u de les hebt doorlopen [configureren en uitvoeren van een voorbeeldtoepassing uitschakelen][config_ble].

   1. Open het configuratiebestand van de gateway met de volgende opdracht:

      ```bash
      # For Windows command prompt
      code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json

      # For MacOS or Ubuntu
      code ~/.iot-hub-getting-started/config-gateway.json
      ```

   1. Update van de gateway MAC-adres wanneer u [Intel NUC als IoT gateway instellen][setup_nuc], en sla het bestand.

1. De voorbeeldcode van de bron worden gecompileerd met de volgende opdracht:

   ```bash
   gulp compile
   ```

   De opdracht worden de voorbeeldcode van de gegevensbron overgebracht naar Intel NUC en wordt uitgevoerd `build.sh` voor het compileren van het.

1. Voer de `hello_world` app op Intel NUC met de volgende opdracht:

   ```bash
   gulp run
   ```

   De opdracht wordt uitgevoerd `../Tools/run-hello-world.js` die is opgegeven in `config.json` starten van de voorbeeld-app op Intel NUC.

   ![run_sample](media/iot-hub-gateway-kit-lessons/lesson5/run_sample.png)

## <a name="create-a-new-module-and-compile-it-on-intel-nuc"></a>Maak een nieuwe module gecompileerd en op Intel NUC

De onderstaande stappen helpt u bij het maken van een nieuwe module en op Intel NUC worden gecompileerd. De module wordt afgedrukt berichten met een tijdstempel nadat deze is ontvangen. In deze sectie maakt u uw eerste aangepaste gateway-module.

Iedere module Azure IoT Edge moet de volgende interfaces implementeren:

   ```C
   pfModule_ParseConfigurationFromJson Module_ParseConfigurationFromJson
   pfModule_FreeConfiguration Module_FreeConfiguration
   pfModule_Create Module_Create
   pfModule_Destroy Module_Destroy
   pfModule_Receive Module_Receive
   ```

U kunt desgewenst de volgende interface implementeren:

   ```C
   pfModule_Start Module_Start
   ```

Het volgende diagram toont de status van belangrijke paden van een module. De vierkante rechthoeken vertegenwoordigen methoden die u voor bewerkingen uitvoeren wanneer de module worden verplaatst tussen de statussen implementeren. De ovalen worden belangrijke weergegeven in de module worden.

![state_path](media/iot-hub-gateway-kit-lessons/lesson5/state_path.png)

Nu gaan we een module op basis van de sjabloon te maken:

1. Open de sjabloonmap met de volgende opdracht:

   ```bash
   code module/my_module
   ```

   ![code_module](media/iot-hub-gateway-kit-lessons/lesson5/code_module.png)

   - `src/my_module.c`fungeert als een sjabloon voor het maken van een module. De sjabloon verklaart de interfaces. U hoeft te doen is het toevoegen van logica voor de `MyModule_Receive` functie.
   - `build.sh`het build-script voor het compileren van de module voor op Intel NUC is.
1. Open de `src/my_module.c` -bestand en bevatten twee header-bestanden:

   ```C
   #include <stdio.h>
   #include "azure_c_shared_utility/xlogging.h"
   ```

1. Voeg de volgende code naar de `MyModule_Receive` functie:

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

1. Update de `config.json` te geven de `workspace` map op de hostcomputer en het pad van de implementatie op Intel NUC. Tijdens het compileren van de bestanden in de `workspace` map wordt overgedragen naar het pad van de implementatie.

   1. Open de `config.json` bestand met de volgende opdracht:

      ```bash
      code config.json
      ```

   1. Update `config.json` met de volgende configuratie:

      ```json
      "workspace": "./module/my_module",
      "deploy_path": "module/my_module"
      ```

      ![config_json](media/iot-hub-gateway-kit-lessons/lesson5/config_json.png)

1. Compileren van de module met de volgende opdracht:

   ```bash
   gulp compile
   ```

   De opdracht worden de broncode overgebracht naar Intel NUC en wordt uitgevoerd `build.sh` voor het compileren van de module.

## <a name="add-the-module-to-the-helloworld-sample-app-and-run-the-app-on-intel-nuc"></a>De module toevoegen aan de hello_world voorbeeld-app en voer de app op Intel NUC

Volg deze stappen voor het uitvoeren van deze taak:

1. Lijst alle de beschikbare module binaire bestanden (.so-bestanden) op Intel NUC met de volgende opdracht:

   ```bash
   gulp modules --list
   ```

   Het binaire pad van `my_module` gecompileerde zou moeten worden vermeld als hieronder:

   ```path
   /root/gateway_sample/module/my_module/build/libmy_module.so
   ```

   Als u wijzigt de standaardgebruikersnaam aanmelding in `config-gateway.json`, binair pad wordt gestart met `home/<your username>` in plaats van `root`.

1. Voeg `my_module` naar de `hello_world` voorbeeld-app:

   1. Open de `hello_world.json` bestand met de volgende opdracht:

      ```bash
      code sample/hello_world/src/hello_world.json
      ```

   1. Voeg de volgende code naar de `modules` sectie:

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

      De waarde van `module.path` moet `/root/gateway_sample/module/my_module/build/libmy_module.so`. De code declareert `my_module` moet worden gekoppeld met de gateway, evenals de locatie van de binaire opgegeven module in `module.path`.
   1. Voeg de volgende code naar de `links` sectie:

      ```json
      {
        "source": "hello_world",
        "sink": "my_module"
      }
      ```

      Deze code geeft aan dat berichten worden verzonden vanaf de `hello_world` module `my_module`.

      ![hello_world_json](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_json.png)

1. Voer de `hello_world` voorbeeld-app met de volgende opdracht:

   ```bash
   gulp run --config sample/hello_world/src/hello_world.json
   ```

   De `--config` parameter dwingt de `run-hello-world.js` script uit te voeren met behulp van de `hello_world.json` bestand.

   ![hello_world_new](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_new.png)

Gefeliciteerd. Nu ziet u het gedrag van deze nieuwe module, gewoon worden afgedrukt 'Hallo wereld'-berichten met een tijdstempel, een ander resultaat van de oorspronkelijke 'hello_world'-module.

## <a name="next-steps"></a>Volgende stappen

U hebt een nieuwe module gemaakt, worden deze toegevoegd aan de hello_world voorbeeld en download de voorbeeldapp uit te voeren met de nieuwe module op de gateway. Als u weten over Azure IoT gateway modules wilt, vindt u hier meer module-voorbeelden: [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules).

<!-- Images and links -->

[config_ble]: iot-hub-gateway-kit-c-lesson3-configure-ble-app.md
[setup_nuc]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
