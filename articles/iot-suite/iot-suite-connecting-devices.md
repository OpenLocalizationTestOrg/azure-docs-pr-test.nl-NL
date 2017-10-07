---
title: aaaConnect een apparaat met C op Windows | Microsoft Docs
description: Hierin wordt beschreven hoe tooconnect een apparaat toohello Azure IoT Suite vooraf geconfigureerde oplossing voor externe controle met behulp van een toepassing die is geschreven in C met Windows.
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 34e39a58-2434-482c-b3fa-29438a0c05e8
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 51041e0cec113a5cfa006ab2276096baf928eef5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-windows"></a><span data-ttu-id="664a2-103">Verbinding maken met uw apparaat toohello voor externe controle vooraf geconfigureerde oplossing (Windows)</span><span class="sxs-lookup"><span data-stu-id="664a2-103">Connect your device toohello remote monitoring preconfigured solution (Windows)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-c-sample-solution-on-windows"></a><span data-ttu-id="664a2-104">Een voorbeeld C oplossing maken in Windows</span><span class="sxs-lookup"><span data-stu-id="664a2-104">Create a C sample solution on Windows</span></span>
<span data-ttu-id="664a2-105">Hallo stappen ziet u hoe toocreate een clienttoepassing die met de Hallo externe controle communiceert vooraf geconfigureerde oplossing.</span><span class="sxs-lookup"><span data-stu-id="664a2-105">hello following steps show you how toocreate a client application that communicates with hello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="664a2-106">Deze toepassing is geschreven in C en gebouwd en op Windows worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="664a2-106">This application is written in C and built and run on Windows.</span></span>

<span data-ttu-id="664a2-107">Maak een starter-project in Visual Studio 2015 of Visual Studio 2017 en Hallo Iothub apparaat-client NuGet-pakketten toevoegen:</span><span class="sxs-lookup"><span data-stu-id="664a2-107">Create a starter project in Visual Studio 2015 or Visual Studio 2017 and add hello IoT Hub device client NuGet packages:</span></span>

1. <span data-ttu-id="664a2-108">Maak in Visual Studio een C-consoletoepassing met behulp van Visual C++ Hallo **Win32-consoletoepassing** sjabloon.</span><span class="sxs-lookup"><span data-stu-id="664a2-108">In Visual Studio, create a C console application using hello Visual C++ **Win32 Console Application** template.</span></span> <span data-ttu-id="664a2-109">Naam Hallo project **RMDevice**.</span><span class="sxs-lookup"><span data-stu-id="664a2-109">Name hello project **RMDevice**.</span></span>
2. <span data-ttu-id="664a2-110">Op Hallo **toepassingsinstellingen** pagina in Hallo **Wizard Win32-toepassing**, zorg ervoor dat **consoletoepassing** is geselecteerd en schakel het selectievakje **Precompiled koptekst** en **Security Development Lifecycle (SDL) controleert**.</span><span class="sxs-lookup"><span data-stu-id="664a2-110">On hello **Application Settings** page in hello **Win32 Application Wizard**, ensure that **Console application** is selected, and uncheck **Precompiled header** and **Security Development Lifecycle (SDL) checks**.</span></span>
3. <span data-ttu-id="664a2-111">In **Solution Explorer**, Hallo bestanden stdafx.h, targetver.h en stdafx.cpp worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="664a2-111">In **Solution Explorer**, delete hello files stdafx.h, targetver.h, and stdafx.cpp.</span></span>
4. <span data-ttu-id="664a2-112">In **Solution Explorer**, wijzig de naam van Hallo bestand RMDevice.cpp tooRMDevice.c.</span><span class="sxs-lookup"><span data-stu-id="664a2-112">In **Solution Explorer**, rename hello file RMDevice.cpp tooRMDevice.c.</span></span>
5. <span data-ttu-id="664a2-113">In **Solution Explorer**, met de rechtermuisknop op Hallo **RMDevice** project en klik vervolgens op **beheren NuGet-pakketten**.</span><span class="sxs-lookup"><span data-stu-id="664a2-113">In **Solution Explorer**, right-click on hello **RMDevice** project and then click **Manage NuGet packages**.</span></span> <span data-ttu-id="664a2-114">Klik op **Bladeren**, zoek vervolgens naar en installeren van Hallo NuGet-pakketten te volgen:</span><span class="sxs-lookup"><span data-stu-id="664a2-114">Click **Browse**, then search for and install hello following NuGet packages:</span></span>
   
   * <span data-ttu-id="664a2-115">Microsoft.Azure.IoTHub.Serializer</span><span class="sxs-lookup"><span data-stu-id="664a2-115">Microsoft.Azure.IoTHub.Serializer</span></span>
   * <span data-ttu-id="664a2-116">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="664a2-116">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
   * <span data-ttu-id="664a2-117">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="664a2-117">Microsoft.Azure.IoTHub.MqttTransport</span></span>
6. <span data-ttu-id="664a2-118">In **Solution Explorer**, met de rechtermuisknop op Hallo **RMDevice** project en klik vervolgens op **eigenschappen** tooopen Hallo project **eigenschappenvensters**in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="664a2-118">In **Solution Explorer**, right-click on hello **RMDevice** project and then click **Properties** tooopen hello project's **Property Pages** dialog box.</span></span> <span data-ttu-id="664a2-119">Zie voor meer informatie [instelling Visual C++-Projecteigenschappen][lnk-c-project-properties].</span><span class="sxs-lookup"><span data-stu-id="664a2-119">For details, see [Setting Visual C++ Project Properties][lnk-c-project-properties].</span></span> 
7. <span data-ttu-id="664a2-120">Klik op Hallo **Linker** map, klikt u vervolgens op Hallo **invoer** eigenschappenpagina.</span><span class="sxs-lookup"><span data-stu-id="664a2-120">Click hello **Linker** folder, then click hello **Input** property page.</span></span>
8. <span data-ttu-id="664a2-121">Voeg **crypt32.lib** toohello **extra afhankelijkheden** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="664a2-121">Add **crypt32.lib** toohello **Additional Dependencies** property.</span></span> <span data-ttu-id="664a2-122">Klik op **OK** en vervolgens **OK** opnieuw toosave Hallo project eigenschapswaarden.</span><span class="sxs-lookup"><span data-stu-id="664a2-122">Click **OK** and then **OK** again toosave hello project property values.</span></span>

<span data-ttu-id="664a2-123">Toevoegen van Hallo Parson JSON bibliotheek toohello **RMDevice** project en voeg Hallo vereist `#include` instructies:</span><span class="sxs-lookup"><span data-stu-id="664a2-123">Add hello Parson JSON library toohello **RMDevice** project and add hello required `#include` statements:</span></span>

1. <span data-ttu-id="664a2-124">Kloon Hallo Parson GitHub-opslagplaats met behulp van de volgende opdracht Hallo in een geschikte map op uw computer:</span><span class="sxs-lookup"><span data-stu-id="664a2-124">In a suitable folder on your computer, clone hello Parson GitHub repository using hello following command:</span></span>

    ```
    git clone https://github.com/kgabis/parson.git
    ```

1. <span data-ttu-id="664a2-125">Hallo parson.h en parson.c bestanden kopiëren van de lokale kopie Hallo van Hallo Parson opslagplaats tooyour **RMDevice** projectmap.</span><span class="sxs-lookup"><span data-stu-id="664a2-125">Copy hello parson.h and parson.c files from hello local copy of hello Parson repository tooyour **RMDevice** project folder.</span></span>

1. <span data-ttu-id="664a2-126">In Visual Studio met de rechtermuisknop op Hallo **RMDevice** project, klikt u op **toevoegen**, en klik vervolgens op **bestaand Item**.</span><span class="sxs-lookup"><span data-stu-id="664a2-126">In Visual Studio, right-click hello **RMDevice** project, click **Add**, and then click **Existing Item**.</span></span>

1. <span data-ttu-id="664a2-127">In Hallo **Add Existing Item** dialoogvenster, selecteer Hallo parson.h en parson.c bestanden in Hallo **RMDevice** projectmap.</span><span class="sxs-lookup"><span data-stu-id="664a2-127">In hello **Add Existing Item** dialog, select hello parson.h and parson.c files in hello **RMDevice** project folder.</span></span> <span data-ttu-id="664a2-128">Klik vervolgens op **toevoegen** tooadd deze twee bestanden tooyour-project.</span><span class="sxs-lookup"><span data-stu-id="664a2-128">Then click **Add** tooadd these two files tooyour project.</span></span>

1. <span data-ttu-id="664a2-129">In Visual Studio Hallo RMDevice.c bestand te openen.</span><span class="sxs-lookup"><span data-stu-id="664a2-129">In Visual Studio, open hello RMDevice.c file.</span></span> <span data-ttu-id="664a2-130">Hallo bestaande `#include` instructies met Hallo code te volgen:</span><span class="sxs-lookup"><span data-stu-id="664a2-130">Replace hello existing `#include` statements with hello following code:</span></span>
   
    ```c
    #include "iothubtransportmqtt.h"
    #include "schemalib.h"
    #include "iothub_client.h"
    #include "serializer_devicetwin.h"
    #include "schemaserializer.h"
    #include "azure_c_shared_utility/threadapi.h"
    #include "azure_c_shared_utility/platform.h"
    #include "parson.h"
    ```

    > [!NOTE]
    > <span data-ttu-id="664a2-131">Nu kunt u controleren of uw project de juiste afhankelijkheden Hallo is ingesteld heeft door het opstellen.</span><span class="sxs-lookup"><span data-stu-id="664a2-131">Now you can verify that your project has hello correct dependencies set up by building it.</span></span>

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-hello-sample"></a><span data-ttu-id="664a2-132">Bouwen en uitvoeren van Hallo-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="664a2-132">Build and run hello sample</span></span>

<span data-ttu-id="664a2-133">Toevoegen van code tooinvoke Hallo **externe\_bewaking\_uitvoeren** werken en vervolgens toepassing bouwen en uitvoeren Hallo apparaat.</span><span class="sxs-lookup"><span data-stu-id="664a2-133">Add code tooinvoke hello **remote\_monitoring\_run** function and then build and run hello device application.</span></span>

1. <span data-ttu-id="664a2-134">Vervang Hallo **belangrijkste** functie met de volgende code tooinvoke hello **externe\_bewaking\_uitvoeren** functie:</span><span class="sxs-lookup"><span data-stu-id="664a2-134">Replace hello **main** function with following code tooinvoke hello **remote\_monitoring\_run** function:</span></span>
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. <span data-ttu-id="664a2-135">Klik op **bouwen** en vervolgens **Build Solution** toobuild Hallo device-toepassing.</span><span class="sxs-lookup"><span data-stu-id="664a2-135">Click **Build** and then **Build Solution** toobuild hello device application.</span></span>

1. <span data-ttu-id="664a2-136">In **Solution Explorer**, klik met de rechtermuisknop Hallo **RMDevice** project, klikt u op **Debug**, en klik vervolgens op **nieuw exemplaar gestart** toorun Hallo voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="664a2-136">In **Solution Explorer**, right-click hello **RMDevice** project, click **Debug**, and then click **Start new instance** toorun hello sample.</span></span> <span data-ttu-id="664a2-137">Hallo-console geeft weer berichten hello toepassing verzendt voorbeeld telemetrie toohello vooraf geconfigureerde oplossing, ontvangt de gewenste eigenschapswaarden ingesteld in het dashboard van de oplossing Hallo en toomethods aangeroepen vanuit het dashboard van de oplossing Hallo reageert.</span><span class="sxs-lookup"><span data-stu-id="664a2-137">hello console displays messages as hello application sends sample telemetry toohello preconfigured solution, receives desired property values set in hello solution dashboard, and responds toomethods invoked from hello solution dashboard.</span></span>

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-c-project-properties]: https://msdn.microsoft.com/library/669zx6zc.aspx
