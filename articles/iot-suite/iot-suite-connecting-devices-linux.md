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
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-linux"></a><span data-ttu-id="5fd4b-103">Verbinding maken met uw apparaat toohello voor externe controle vooraf geconfigureerde oplossing (Linux)</span><span class="sxs-lookup"><span data-stu-id="5fd4b-103">Connect your device toohello remote monitoring preconfigured solution (Linux)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="build-and-run-a-sample-c-client-linux"></a><span data-ttu-id="5fd4b-104">Bouwen en uitvoeren van een voorbeeld van C client Linux</span><span class="sxs-lookup"><span data-stu-id="5fd4b-104">Build and run a sample C client Linux</span></span>
<span data-ttu-id="5fd4b-105">Hallo stappen ziet u hoe toocreate een clienttoepassing die met de Hallo externe controle communiceert vooraf geconfigureerde oplossing.</span><span class="sxs-lookup"><span data-stu-id="5fd4b-105">hello following steps show you how toocreate a client application that communicates with hello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="5fd4b-106">Deze toepassing is geschreven in C en gebaseerd en op Ubuntu Linux wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5fd4b-106">This application is written in C and built and run on Ubuntu Linux.</span></span>

<span data-ttu-id="5fd4b-107">toocomplete deze stappen, moet u een apparaat met Ubuntu versie 15.04 of 15.10.</span><span class="sxs-lookup"><span data-stu-id="5fd4b-107">toocomplete these steps, you need a device running Ubuntu version 15.04 or 15.10.</span></span> <span data-ttu-id="5fd4b-108">Voordat u doorgaat, vereiste hello-pakketten te installeren op uw Ubuntu-apparaat met behulp van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="5fd4b-108">Before proceeding, install hello prerequisite packages on your Ubuntu device using hello following command:</span></span>

```
sudo apt-get install cmake gcc g++
```

## <a name="install-hello-client-libraries-on-your-device"></a><span data-ttu-id="5fd4b-109">Hallo-clientbibliotheken op uw apparaat installeert</span><span class="sxs-lookup"><span data-stu-id="5fd4b-109">Install hello client libraries on your device</span></span>
<span data-ttu-id="5fd4b-110">Hallo clientbibliotheken van Azure IoT Hub zijn beschikbaar als een pakket dat u kunt installeren op uw Ubuntu apparaat Hallo **apt get-** opdracht.</span><span class="sxs-lookup"><span data-stu-id="5fd4b-110">hello Azure IoT Hub client libraries are available as a package you can install on your Ubuntu device using hello **apt-get** command.</span></span> <span data-ttu-id="5fd4b-111">Volgende stappen tooinstall Hallo pakket met de Hallo clientbibliotheek van IoT Hub en header-bestanden op uw computer Ubuntu Hallo voltooien:</span><span class="sxs-lookup"><span data-stu-id="5fd4b-111">Complete hello following steps tooinstall hello package that contains hello IoT Hub client library and header files on your Ubuntu computer:</span></span>

1. <span data-ttu-id="5fd4b-112">Voeg in een shell Hallo AzureIoT opslagplaats tooyour computer:</span><span class="sxs-lookup"><span data-stu-id="5fd4b-112">In a shell, add hello AzureIoT repository tooyour computer:</span></span>
   
    ```
    sudo add-apt-repository ppa:aziotsdklinux/ppa-azureiot
    sudo apt-get update
    ```
2. <span data-ttu-id="5fd4b-113">Hello azure-iot-sdk-c-dev-pakket installeren</span><span class="sxs-lookup"><span data-stu-id="5fd4b-113">Install hello azure-iot-sdk-c-dev package</span></span>
   
    ```
    sudo apt-get install -y azure-iot-sdk-c-dev
    ```

## <a name="install-hello-parson-json-parser"></a><span data-ttu-id="5fd4b-114">Hallo Parson JSON-parser installeren</span><span class="sxs-lookup"><span data-stu-id="5fd4b-114">Install hello Parson JSON parser</span></span>
<span data-ttu-id="5fd4b-115">Hallo IoT Hub client bibliotheken gebruiken Hallo Parson JSON-parser tooparse bericht nettoladingen.</span><span class="sxs-lookup"><span data-stu-id="5fd4b-115">hello IoT Hub client libraries use hello Parson JSON parser tooparse message payloads.</span></span> <span data-ttu-id="5fd4b-116">Kloon Hallo Parson GitHub-opslagplaats met behulp van de volgende opdracht Hallo in een geschikte map op uw computer:</span><span class="sxs-lookup"><span data-stu-id="5fd4b-116">In a suitable folder on your computer, clone hello Parson GitHub repository using hello following command:</span></span>

```
git clone https://github.com/kgabis/parson.git
```

## <a name="prepare-your-project"></a><span data-ttu-id="5fd4b-117">Voorbereiden van uw project</span><span class="sxs-lookup"><span data-stu-id="5fd4b-117">Prepare your project</span></span>
<span data-ttu-id="5fd4b-118">Maak een map op uw machine Ubuntu **externe\_bewaking**.</span><span class="sxs-lookup"><span data-stu-id="5fd4b-118">On your Ubuntu machine, create a folder called **remote\_monitoring**.</span></span> <span data-ttu-id="5fd4b-119">In Hallo **externe\_bewaking** map:</span><span class="sxs-lookup"><span data-stu-id="5fd4b-119">In hello **remote\_monitoring** folder:</span></span>

- <span data-ttu-id="5fd4b-120">Hallo vier bestanden maken **main.c**, **externe\_monitoring.c**, **externe\_monitoring.h**, en **CMakeLists.txt**.</span><span class="sxs-lookup"><span data-stu-id="5fd4b-120">Create hello four files **main.c**, **remote\_monitoring.c**, **remote\_monitoring.h**, and **CMakeLists.txt**.</span></span>
- <span data-ttu-id="5fd4b-121">Maken van de map met de naam **parson**.</span><span class="sxs-lookup"><span data-stu-id="5fd4b-121">Create folder called **parson**.</span></span>

<span data-ttu-id="5fd4b-122">Hallo-bestanden kopiëren **parson.c** en **parson.h** uit het lokale exemplaar van Hallo Parson opslagplaats in Hallo **externe\_bewaking/parson** map.</span><span class="sxs-lookup"><span data-stu-id="5fd4b-122">Copy hello files **parson.c** and **parson.h** from your local copy of hello Parson repository into hello **remote\_monitoring/parson** folder.</span></span>

<span data-ttu-id="5fd4b-123">Open in een teksteditor Hallo **externe\_monitoring.c** bestand.</span><span class="sxs-lookup"><span data-stu-id="5fd4b-123">In a text editor, open hello **remote\_monitoring.c** file.</span></span> <span data-ttu-id="5fd4b-124">Voeg de volgende Hallo `#include` instructies:</span><span class="sxs-lookup"><span data-stu-id="5fd4b-124">Add hello following `#include` statements:</span></span>
   
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

## <a name="call-hello-remotemonitoringrun-function"></a><span data-ttu-id="5fd4b-125">Hallo externe aanroep\_bewaking\_functie uitvoeren</span><span class="sxs-lookup"><span data-stu-id="5fd4b-125">Call hello remote\_monitoring\_run function</span></span>
<span data-ttu-id="5fd4b-126">Open in een teksteditor Hallo **remote_monitoring.h** bestand.</span><span class="sxs-lookup"><span data-stu-id="5fd4b-126">In a text editor, open hello **remote_monitoring.h** file.</span></span> <span data-ttu-id="5fd4b-127">Hallo na code toevoegen:</span><span class="sxs-lookup"><span data-stu-id="5fd4b-127">Add hello following code:</span></span>

```
void remote_monitoring_run(void);
```

<span data-ttu-id="5fd4b-128">Open in een teksteditor Hallo **main.c** bestand.</span><span class="sxs-lookup"><span data-stu-id="5fd4b-128">In a text editor, open hello **main.c** file.</span></span> <span data-ttu-id="5fd4b-129">Hallo na code toevoegen:</span><span class="sxs-lookup"><span data-stu-id="5fd4b-129">Add hello following code:</span></span>

```
#include "remote_monitoring.h"

int main(void)
{
    remote_monitoring_run();

    return 0;
}
```

## <a name="build-and-run-hello-application"></a><span data-ttu-id="5fd4b-130">Hallo-toepassing bouwen en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="5fd4b-130">Build and run hello application</span></span>
<span data-ttu-id="5fd4b-131">Hallo volgende stappen wordt beschreven hoe toouse *CMake* toobuild uw clienttoepassing.</span><span class="sxs-lookup"><span data-stu-id="5fd4b-131">hello following steps describe how toouse *CMake* toobuild your client application.</span></span>

1. <span data-ttu-id="5fd4b-132">Open in een teksteditor Hallo **CMakeLists.txt** bestand in Hallo **remote_monitoring** map.</span><span class="sxs-lookup"><span data-stu-id="5fd4b-132">In a text editor, open hello **CMakeLists.txt** file in hello **remote_monitoring** folder.</span></span>

1. <span data-ttu-id="5fd4b-133">Hallo toodefine instructies hoe na toevoegen toobuild uw clienttoepassing:</span><span class="sxs-lookup"><span data-stu-id="5fd4b-133">Add hello following instructions toodefine how toobuild your client application:</span></span>
   
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
1. <span data-ttu-id="5fd4b-134">In Hallo **remote_monitoring** map maken van een map toostore hello *zorg* bestanden die CMake genereert en voer vervolgens Hallo **cmake** en **maken** opdrachten als volgt:</span><span class="sxs-lookup"><span data-stu-id="5fd4b-134">In hello **remote_monitoring** folder, create a folder toostore hello *make* files that CMake generates and then run hello **cmake** and **make** commands as follows:</span></span>
   
    ```
    mkdir cmake
    cd cmake
    cmake ../
    make
    ```

1. <span data-ttu-id="5fd4b-135">Voer Hallo-clienttoepassing en verzenden van telemetrie tooIoT Hub:</span><span class="sxs-lookup"><span data-stu-id="5fd4b-135">Run hello client application and send telemetry tooIoT Hub:</span></span>
   
    ```
    ./sample_app
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

