---
title: aaaConnect een apparaat met C op Linux | Microsoft Docs
description: Hierin wordt beschreven hoe tooconnect een apparaat toohello Azure IoT Suite vooraf geconfigureerde oplossing voor externe controle met behulp van een toepassing die is geschreven in C op Linux wordt uitgevoerd.
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 0c7c8039-0bbf-4bb5-9e79-ed8cff433629
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 57393817d40d3555177956a01fa71058bc256988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-linux"></a>Verbinding maken met uw apparaat toohello voor externe controle vooraf geconfigureerde oplossing (Linux)
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="build-and-run-a-sample-c-client-linux"></a>Bouwen en uitvoeren van een voorbeeld van C client Linux
Hallo stappen ziet u hoe toocreate een clienttoepassing die met de Hallo externe controle communiceert vooraf geconfigureerde oplossing. Deze toepassing is geschreven in C en gebaseerd en op Ubuntu Linux wordt uitgevoerd.

toocomplete deze stappen, moet u een apparaat met Ubuntu versie 15.04 of 15.10. Voordat u doorgaat, vereiste hello-pakketten te installeren op uw Ubuntu-apparaat met behulp van de volgende opdracht Hallo:

```
sudo apt-get install cmake gcc g++
```

## <a name="install-hello-client-libraries-on-your-device"></a>Hallo-clientbibliotheken op uw apparaat installeert
Hallo clientbibliotheken van Azure IoT Hub zijn beschikbaar als een pakket dat u kunt installeren op uw Ubuntu apparaat Hallo **apt get-** opdracht. Volgende stappen tooinstall Hallo pakket met de Hallo clientbibliotheek van IoT Hub en header-bestanden op uw computer Ubuntu Hallo voltooien:

1. Voeg in een shell Hallo AzureIoT opslagplaats tooyour computer:
   
    ```
    sudo add-apt-repository ppa:aziotsdklinux/ppa-azureiot
    sudo apt-get update
    ```
2. Hello azure-iot-sdk-c-dev-pakket installeren
   
    ```
    sudo apt-get install -y azure-iot-sdk-c-dev
    ```

## <a name="install-hello-parson-json-parser"></a>Hallo Parson JSON-parser installeren
Hallo IoT Hub client bibliotheken gebruiken Hallo Parson JSON-parser tooparse bericht nettoladingen. Kloon Hallo Parson GitHub-opslagplaats met behulp van de volgende opdracht Hallo in een geschikte map op uw computer:

```
git clone https://github.com/kgabis/parson.git
```

## <a name="prepare-your-project"></a>Voorbereiden van uw project
Maak een map op uw machine Ubuntu **externe\_bewaking**. In Hallo **externe\_bewaking** map:

- Hallo vier bestanden maken **main.c**, **externe\_monitoring.c**, **externe\_monitoring.h**, en **CMakeLists.txt**.
- Maken van de map met de naam **parson**.

Hallo-bestanden kopiëren **parson.c** en **parson.h** uit het lokale exemplaar van Hallo Parson opslagplaats in Hallo **externe\_bewaking/parson** map.

Open in een teksteditor Hallo **externe\_monitoring.c** bestand. Voeg de volgende Hallo `#include` instructies:
   
```
#include "iothubtransportmqtt.h"
#include "schemalib.h"
#include "iothub_client.h"
#include "serializer_devicetwin.h"
#include "schemaserializer.h"
#include "azure_c_shared_utility/threadapi.h"
#include "azure_c_shared_utility/platform.h"
#include "parson.h"
```

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="call-hello-remotemonitoringrun-function"></a>Hallo externe aanroep\_bewaking\_functie uitvoeren
Open in een teksteditor Hallo **remote_monitoring.h** bestand. Hallo na code toevoegen:

```
void remote_monitoring_run(void);
```

Open in een teksteditor Hallo **main.c** bestand. Hallo na code toevoegen:

```
#include "remote_monitoring.h"

int main(void)
{
    remote_monitoring_run();

    return 0;
}
```

## <a name="build-and-run-hello-application"></a>Hallo-toepassing bouwen en uitvoeren
Hallo volgende stappen wordt beschreven hoe toouse *CMake* toobuild uw clienttoepassing.

1. Open in een teksteditor Hallo **CMakeLists.txt** bestand in Hallo **remote_monitoring** map.

1. Hallo toodefine instructies hoe na toevoegen toobuild uw clienttoepassing:
   
    ```
    macro(compileAsC99)
      if (CMAKE_VERSION VERSION_LESS "3.1")
        if (CMAKE_C_COMPILER_ID STREQUAL "GNU")
          set (CMAKE_C_FLAGS "--std=c99 ${CMAKE_C_FLAGS}")
          set (CMAKE_CXX_FLAGS "--std=c++11 ${CMAKE_CXX_FLAGS}")
        endif()
      else()
        set (CMAKE_C_STANDARD 99)
        set (CMAKE_CXX_STANDARD 11)
      endif()
    endmacro(compileAsC99)

    cmake_minimum_required(VERSION 2.8.11)
    compileAsC99()

    set(AZUREIOT_INC_FOLDER "${CMAKE_SOURCE_DIR}" "${CMAKE_SOURCE_DIR}/parson" "/usr/include/azureiot" "/usr/include/azureiot/inc")

    include_directories(${AZUREIOT_INC_FOLDER})

    set(sample_application_c_files
        ./parson/parson.c
        ./remote_monitoring.c
        ./main.c
    )

    set(sample_application_h_files
        ./parson/parson.h
        ./remote_monitoring.h
    )

    add_executable(sample_app ${sample_application_c_files} ${sample_application_h_files})

    target_link_libraries(sample_app
        serializer
        iothub_client
        iothub_client_mqtt_transport
        aziotsharedutil
        umqtt
        pthread
        curl
        ssl
        crypto
        m
    )
    ```
1. In Hallo **remote_monitoring** map maken van een map toostore hello *zorg* bestanden die CMake genereert en voer vervolgens Hallo **cmake** en **maken** opdrachten als volgt:
   
    ```
    mkdir cmake
    cd cmake
    cmake ../
    make
    ```

1. Voer Hallo-clienttoepassing en verzenden van telemetrie tooIoT Hub:
   
    ```
    ./sample_app
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

