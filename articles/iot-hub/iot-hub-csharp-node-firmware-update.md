---
title: aaaDevice firmware-update met Azure IoT Hub (.NET/knooppunt) | Microsoft Docs
description: Hoe worden Apparaatbeheer toouse op Azure IoT Hub tooinitiate een apparaatfirmware bijwerken. U gebruikt hello Azure IoT-apparaat SDK voor Node.js tooimplement een gesimuleerde apparaattoepassing en hello Azure IoT service SDK voor .NET tooimplement een service-app waarmee de Hallo firmware-update wordt geactiveerd.
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 70b84258-bc9f-43b1-b7cf-de1bb715f2cf
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/17/2017
ms.author: juanpere
ms.openlocfilehash: d48899651bcd5d67e577c971be0f9453c8f21592
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-device-management-tooinitiate-a-device-firmware-update-netnode"></a><span data-ttu-id="03f2b-104">Device management tooinitiate een apparaat firmware-update (.NET/knooppunt) gebruiken</span><span class="sxs-lookup"><span data-stu-id="03f2b-104">Use device management tooinitiate a device firmware update (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a><span data-ttu-id="03f2b-105">Inleiding</span><span class="sxs-lookup"><span data-stu-id="03f2b-105">Introduction</span></span>
<span data-ttu-id="03f2b-106">In Hallo [aan de slag met Apparaatbeheer] [ lnk-dm-getstarted] zelfstudie hebt u gezien hoe toouse hello [apparaat twin] [ lnk-devtwin] en [direct methoden] [ lnk-c2dmethod] primitieven tooremotely opnieuw opstarten van een apparaat.</span><span class="sxs-lookup"><span data-stu-id="03f2b-106">In hello [Get started with device management][lnk-dm-getstarted] tutorial, you saw how toouse hello [device twin][lnk-devtwin] and [direct methods][lnk-c2dmethod] primitives tooremotely reboot a device.</span></span> <span data-ttu-id="03f2b-107">Deze zelfstudie maakt gebruik van dezelfde Iothub primitieven Hallo en ziet u hoe een end-to-end toodo gesimuleerde firmware-update.</span><span class="sxs-lookup"><span data-stu-id="03f2b-107">This tutorial uses hello same IoT Hub primitives and shows you how toodo an end-to-end simulated firmware update.</span></span>  <span data-ttu-id="03f2b-108">Dit patroon wordt gebruikt in Hallo firmware-update-implementatie voor Hallo [frambozen Pi apparaat implementatie voorbeeld][lnk-rpi-implementation].</span><span class="sxs-lookup"><span data-stu-id="03f2b-108">This pattern is used in hello firmware update implementation for hello [Raspberry Pi device implementation sample][lnk-rpi-implementation].</span></span>

<span data-ttu-id="03f2b-109">In deze handleiding ontdekt u hoe u:</span><span class="sxs-lookup"><span data-stu-id="03f2b-109">This tutorial shows you how to:</span></span>

* <span data-ttu-id="03f2b-110">Een .NET-consoletoepassing die Hallo firmwareUpdate directe methode in Hallo gesimuleerde apparaattoepassing via uw IoT-hub aanroept maken.</span><span class="sxs-lookup"><span data-stu-id="03f2b-110">Create a .NET console app that calls hello firmwareUpdate direct method in hello simulated device app through your IoT hub.</span></span>
* <span data-ttu-id="03f2b-111">Maakt een gesimuleerd apparaat-app die u implementeert een **firmwareUpdate** directe methode.</span><span class="sxs-lookup"><span data-stu-id="03f2b-111">Create a simulated device app that implements a **firmwareUpdate** direct method.</span></span> <span data-ttu-id="03f2b-112">Deze methode initieert een fasen proces dat wordt gewacht toodownload Hallo firmware-image, Hallo firmware afbeelding gedownload en ten slotte is van toepassing hello firmware-image.</span><span class="sxs-lookup"><span data-stu-id="03f2b-112">This method initiates a multi-stage process that waits toodownload hello firmware image, downloads hello firmware image, and finally applies hello firmware image.</span></span> <span data-ttu-id="03f2b-113">Tijdens elke fase van de update Hallo gerapporteerd Hallo apparaat gebruikt Hallo eigenschappen tooreport op uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="03f2b-113">During each stage of hello update, hello device uses hello reported properties tooreport on progress.</span></span>

<span data-ttu-id="03f2b-114">Aan het einde van de Hallo van deze zelfstudie hebt u een Node.js-consoletoepassing apparaat en een app in de back-end voor .NET (C#)-console:</span><span class="sxs-lookup"><span data-stu-id="03f2b-114">At hello end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="03f2b-115">**dmpatterns_fwupdate_service.js**, die een directe methode wordt aangeroepen in de gesimuleerde apparaattoepassing hello, geeft antwoord Hallo en wordt regelmatig (elke 500ms) geeft Hallo bijgewerkt gerapporteerd eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="03f2b-115">**dmpatterns_fwupdate_service.js**, which calls a direct method in hello simulated device app, displays hello response, and periodically (every 500ms) displays hello updated reported properties.</span></span>

<span data-ttu-id="03f2b-116">**TriggerFWUpdate**, die tooyour IoT-hub is verbonden met de apparaat-id Hallo eerder hebt gemaakt, ontvangen een directe methode firmwareUpdate, wordt uitgevoerd via een toosimulate meerdere proces een firmware-update inclusief: wachten op Hallo installatiekopie downloaden downloaden van de nieuwe installatiekopie Hallo en ten slotte toepassen Hallo image.</span><span class="sxs-lookup"><span data-stu-id="03f2b-116">**TriggerFWUpdate**, which connects tooyour IoT hub with hello device identity created earlier, receives a firmwareUpdate direct method, runs through a multi-state process toosimulate a firmware update including: waiting for hello image download, downloading hello new image, and finally applying hello image.</span></span>

<span data-ttu-id="03f2b-117">toocomplete in deze zelfstudie, moet u hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="03f2b-117">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="03f2b-118">Visual Studio 2015 of Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="03f2b-118">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="03f2b-119">Node.js-versie 0.12.x of hoger</span><span class="sxs-lookup"><span data-stu-id="03f2b-119">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="03f2b-120">[Uw ontwikkelingsomgeving voorbereiden] [ lnk-dev-setup] wordt beschreven hoe tooinstall Node.js voor deze zelfstudie op Windows of Linux.</span><span class="sxs-lookup"><span data-stu-id="03f2b-120">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="03f2b-121">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="03f2b-121">An active Azure account.</span></span> <span data-ttu-id="03f2b-122">(Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)</span><span class="sxs-lookup"><span data-stu-id="03f2b-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="03f2b-123">Ga als volgt Hallo [aan de slag met Apparaatbeheer](iot-hub-csharp-node-device-management-get-started.md) artikel toocreate uw IoT-hub en uw IoT Hub-verbindingsreeks ophalen.</span><span class="sxs-lookup"><span data-stu-id="03f2b-123">Follow hello [Get started with device management](iot-hub-csharp-node-device-management-get-started.md) article toocreate your IoT hub and get your IoT Hub connection string.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-hello-device-using-a-direct-method"></a><span data-ttu-id="03f2b-124">Activeren van een externe firmware-update op Hallo-apparaat met een directe methode</span><span class="sxs-lookup"><span data-stu-id="03f2b-124">Trigger a remote firmware update on hello device using a direct method</span></span>
<span data-ttu-id="03f2b-125">In deze sectie maakt u een .NET-consoletoepassing (met C#) die een externe firmware-update op een apparaat start.</span><span class="sxs-lookup"><span data-stu-id="03f2b-125">In this section, you create a .NET console app (using C#) that initiates a remote firmware update on a device.</span></span> <span data-ttu-id="03f2b-126">Hallo app gebruikmaakt van een directe methode tooinitiate Hallo-update en maakt gebruik van apparaat twin query's tooperiodically Hallo status Hallo active firmware-update ophalen.</span><span class="sxs-lookup"><span data-stu-id="03f2b-126">hello app uses a direct method tooinitiate hello update and uses device twin queries tooperiodically get hello status of hello active firmware update.</span></span>

1. <span data-ttu-id="03f2b-127">Voeg in Visual Studio een Visual C# Classic Windows Desktop-project toohello huidige oplossing met behulp van Hallo **consoletoepassing** projectsjabloon.</span><span class="sxs-lookup"><span data-stu-id="03f2b-127">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="03f2b-128">Naam Hallo project **TriggerFWUpdate**.</span><span class="sxs-lookup"><span data-stu-id="03f2b-128">Name hello project **TriggerFWUpdate**.</span></span>

    ![Nieuw Windows Classic Desktop-project in Visual C#][img-createapp]

1. <span data-ttu-id="03f2b-130">Klik in Solution Explorer met de rechtermuisknop op Hallo **TriggerFWUpdate** project en klik vervolgens op **NuGet-pakketten beheren...** .</span><span class="sxs-lookup"><span data-stu-id="03f2b-130">In Solution Explorer, right-click hello **TriggerFWUpdate** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="03f2b-131">In Hallo **NuGet Package Manager** Selecteer **Bladeren**, zoeken naar **microsoft.azure.devices**, selecteer **installeren** tooinstall Hallo **Microsoft.Azure.Devices** Inpakken en accepteer de gebruiksvoorwaarden Hallo.</span><span class="sxs-lookup"><span data-stu-id="03f2b-131">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="03f2b-132">Deze procedure downloadt, installeert en voegt u een verwijzing toohello [Azure IoT service SDK] [ lnk-nuget-service-sdk] NuGet-pakket en de bijbehorende afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="03f2b-132">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![Sluit het venster Nuget Package Manager.][img-servicenuget]
1. <span data-ttu-id="03f2b-134">Voeg de volgende Hallo `using` instructies boven Hallo Hallo **Program.cs** bestand:</span><span class="sxs-lookup"><span data-stu-id="03f2b-134">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
1. <span data-ttu-id="03f2b-135">Hallo na toohello velden toevoegen **programma** klasse.</span><span class="sxs-lookup"><span data-stu-id="03f2b-135">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="03f2b-136">Vervang Hallo meerdere tijdelijke aanduiding voor waarden met IoT Hub-verbindingsreeks voor Hallo-hub die u hebt gemaakt in de vorige sectie Hallo Hallo en Hallo-Id van uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="03f2b-136">Replace hello multiple placeholder values with hello IoT Hub connection string for hello hub that you created in hello previous section and hello Id of your device.</span></span>
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
1. <span data-ttu-id="03f2b-137">Hallo na methode toohello toevoegen **programma** klasse:</span><span class="sxs-lookup"><span data-stu-id="03f2b-137">Add hello following method toohello **Program** class:</span></span>
   
        public static async Task QueryTwinFWUpdateReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
1. <span data-ttu-id="03f2b-138">Hallo na methode toohello toevoegen **programma** klasse:</span><span class="sxs-lookup"><span data-stu-id="03f2b-138">Add hello following method toohello **Program** class:</span></span>

        public static async Task StartFirmwareUpdate()
        {
            client = ServiceClient.CreateFromConnectionString(connString);
            CloudToDeviceMethod method = new CloudToDeviceMethod("firmwareUpdate");
            method.ResponseTimeout = TimeSpan.FromSeconds(30);
            method.SetPayloadJson(
                @"{
                    fwPackageUri : 'https://someurl'
                }");

            CloudToDeviceMethodResult result = await client.InvokeDeviceMethodAsync(targetDevice, method);

            Console.WriteLine("Invoked firmware update on device.");
        }

1. <span data-ttu-id="03f2b-139">Voeg regels toohello na Hallo **Main** methode:</span><span class="sxs-lookup"><span data-stu-id="03f2b-139">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartFirmwareUpdate().Wait();
        QueryTwinFWUpdateReported().Wait();
        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
        
1. <span data-ttu-id="03f2b-140">Open in Solution Explorer hello, Hallo **opstartprojecten instellen...**  en zorg ervoor dat Hallo **actie** voor **TriggerFWUpdate** project **Start**.</span><span class="sxs-lookup"><span data-stu-id="03f2b-140">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **TriggerFWUpdate** project is **Start**.</span></span>

1. <span data-ttu-id="03f2b-141">Hallo-oplossing bouwen.</span><span class="sxs-lookup"><span data-stu-id="03f2b-141">Build hello solution.</span></span>

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-hello-apps"></a><span data-ttu-id="03f2b-142">Hallo-apps uitvoeren</span><span class="sxs-lookup"><span data-stu-id="03f2b-142">Run hello apps</span></span>
<span data-ttu-id="03f2b-143">U bent nu klaar toorun Hallo apps.</span><span class="sxs-lookup"><span data-stu-id="03f2b-143">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="03f2b-144">Bij de opdrachtprompt Hallo in Hallo **manageddevice** map Hallo opdracht toobegin luisteren naar Hallo opnieuw opstarten directe methode te volgen.</span><span class="sxs-lookup"><span data-stu-id="03f2b-144">At hello command prompt in hello **manageddevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. <span data-ttu-id="03f2b-145">In Visual Studio met de rechtermuisknop op Hallo **TriggerFWUpdate** projectRun toohello C#-consoletoepassing, selecteer **Debug** en **nieuw exemplaar gestart**.</span><span class="sxs-lookup"><span data-stu-id="03f2b-145">In Visual Studio, right-click on hello **TriggerFWUpdate** projectRun toohello C# console app, select **Debug** and **Start new instance**.</span></span>

3. <span data-ttu-id="03f2b-146">U ziet Hallo apparaat antwoord toohello directe methode in Hallo-console.</span><span class="sxs-lookup"><span data-stu-id="03f2b-146">You see hello device response toohello direct method in hello console.</span></span>

    ![Firmware is bijgewerkt][img-fwupdate]

## <a name="next-steps"></a><span data-ttu-id="03f2b-148">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="03f2b-148">Next steps</span></span>
<span data-ttu-id="03f2b-149">In deze zelfstudie gebruikt u een directe methode tootrigger een externe firmware-update op een apparaat en de gebruikte Hallo eigenschappen toofollow Hallo voortgang van de firmware-update Hallo gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="03f2b-149">In this tutorial, you used a direct method tootrigger a remote firmware update on a device and used hello reported properties toofollow hello progress of hello firmware update.</span></span>

<span data-ttu-id="03f2b-150">toolearn hoe tooextend uw IoT-oplossing en schema-methode aanroepen op meerdere apparaten, raadpleegt u Hallo [planning en broadcast taken] [ lnk-tutorial-jobs] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="03f2b-150">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-firmware-update/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-firmware-update/createnetapp.png
[img-fwupdate]: media/iot-hub-csharp-node-firmware-update/fwupdated.png

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-rpi-implementation]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_client/samples/iothub_client_sample_mqtt_dm/pi_device
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/