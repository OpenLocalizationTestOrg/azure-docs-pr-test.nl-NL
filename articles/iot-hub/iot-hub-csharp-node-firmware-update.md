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
# <a name="use-device-management-tooinitiate-a-device-firmware-update-netnode"></a>Device management tooinitiate een apparaat firmware-update (.NET/knooppunt) gebruiken
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a>Inleiding
In Hallo [aan de slag met Apparaatbeheer] [ lnk-dm-getstarted] zelfstudie hebt u gezien hoe toouse hello [apparaat twin] [ lnk-devtwin] en [direct methoden] [ lnk-c2dmethod] primitieven tooremotely opnieuw opstarten van een apparaat. Deze zelfstudie maakt gebruik van dezelfde Iothub primitieven Hallo en ziet u hoe een end-to-end toodo gesimuleerde firmware-update.  Dit patroon wordt gebruikt in Hallo firmware-update-implementatie voor Hallo [frambozen Pi apparaat implementatie voorbeeld][lnk-rpi-implementation].

In deze handleiding ontdekt u hoe u:

* Een .NET-consoletoepassing die Hallo firmwareUpdate directe methode in Hallo gesimuleerde apparaattoepassing via uw IoT-hub aanroept maken.
* Maakt een gesimuleerd apparaat-app die u implementeert een **firmwareUpdate** directe methode. Deze methode initieert een fasen proces dat wordt gewacht toodownload Hallo firmware-image, Hallo firmware afbeelding gedownload en ten slotte is van toepassing hello firmware-image. Tijdens elke fase van de update Hallo gerapporteerd Hallo apparaat gebruikt Hallo eigenschappen tooreport op uitgevoerd.

Aan het einde van de Hallo van deze zelfstudie hebt u een Node.js-consoletoepassing apparaat en een app in de back-end voor .NET (C#)-console:

**dmpatterns_fwupdate_service.js**, die een directe methode wordt aangeroepen in de gesimuleerde apparaattoepassing hello, geeft antwoord Hallo en wordt regelmatig (elke 500ms) geeft Hallo bijgewerkt gerapporteerd eigenschappen.

**TriggerFWUpdate**, die tooyour IoT-hub is verbonden met de apparaat-id Hallo eerder hebt gemaakt, ontvangen een directe methode firmwareUpdate, wordt uitgevoerd via een toosimulate meerdere proces een firmware-update inclusief: wachten op Hallo installatiekopie downloaden downloaden van de nieuwe installatiekopie Hallo en ten slotte toepassen Hallo image.

toocomplete in deze zelfstudie, moet u hello te volgen:

* Visual Studio 2015 of Visual Studio 2017.
* Node.js-versie 0.12.x of hoger <br/>  [Uw ontwikkelingsomgeving voorbereiden] [ lnk-dev-setup] wordt beschreven hoe tooinstall Node.js voor deze zelfstudie op Windows of Linux.
* Een actief Azure-account. (Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)

Ga als volgt Hallo [aan de slag met Apparaatbeheer](iot-hub-csharp-node-device-management-get-started.md) artikel toocreate uw IoT-hub en uw IoT Hub-verbindingsreeks ophalen.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-hello-device-using-a-direct-method"></a>Activeren van een externe firmware-update op Hallo-apparaat met een directe methode
In deze sectie maakt u een .NET-consoletoepassing (met C#) die een externe firmware-update op een apparaat start. Hallo app gebruikmaakt van een directe methode tooinitiate Hallo-update en maakt gebruik van apparaat twin query's tooperiodically Hallo status Hallo active firmware-update ophalen.

1. Voeg in Visual Studio een Visual C# Classic Windows Desktop-project toohello huidige oplossing met behulp van Hallo **consoletoepassing** projectsjabloon. Naam Hallo project **TriggerFWUpdate**.

    ![Nieuw Windows Classic Desktop-project in Visual C#][img-createapp]

1. Klik in Solution Explorer met de rechtermuisknop op Hallo **TriggerFWUpdate** project en klik vervolgens op **NuGet-pakketten beheren...** .
1. In Hallo **NuGet Package Manager** Selecteer **Bladeren**, zoeken naar **microsoft.azure.devices**, selecteer **installeren** tooinstall Hallo **Microsoft.Azure.Devices** Inpakken en accepteer de gebruiksvoorwaarden Hallo. Deze procedure downloadt, installeert en voegt u een verwijzing toohello [Azure IoT service SDK] [ lnk-nuget-service-sdk] NuGet-pakket en de bijbehorende afhankelijkheden.

    ![Sluit het venster Nuget Package Manager.][img-servicenuget]
1. Voeg de volgende Hallo `using` instructies boven Hallo Hallo **Program.cs** bestand:
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
1. Hallo na toohello velden toevoegen **programma** klasse. Vervang Hallo meerdere tijdelijke aanduiding voor waarden met IoT Hub-verbindingsreeks voor Hallo-hub die u hebt gemaakt in de vorige sectie Hallo Hallo en Hallo-Id van uw apparaat.
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
1. Hallo na methode toohello toevoegen **programma** klasse:
   
        public static async Task QueryTwinFWUpdateReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
1. Hallo na methode toohello toevoegen **programma** klasse:

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

1. Voeg regels toohello na Hallo **Main** methode:
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartFirmwareUpdate().Wait();
        QueryTwinFWUpdateReported().Wait();
        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
        
1. Open in Solution Explorer hello, Hallo **opstartprojecten instellen...**  en zorg ervoor dat Hallo **actie** voor **TriggerFWUpdate** project **Start**.

1. Hallo-oplossing bouwen.

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-hello-apps"></a>Hallo-apps uitvoeren
U bent nu klaar toorun Hallo apps.

1. Bij de opdrachtprompt Hallo in Hallo **manageddevice** map Hallo opdracht toobegin luisteren naar Hallo opnieuw opstarten directe methode te volgen.
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. In Visual Studio met de rechtermuisknop op Hallo **TriggerFWUpdate** projectRun toohello C#-consoletoepassing, selecteer **Debug** en **nieuw exemplaar gestart**.

3. U ziet Hallo apparaat antwoord toohello directe methode in Hallo-console.

    ![Firmware is bijgewerkt][img-fwupdate]

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie gebruikt u een directe methode tootrigger een externe firmware-update op een apparaat en de gebruikte Hallo eigenschappen toofollow Hallo voortgang van de firmware-update Hallo gerapporteerd.

toolearn hoe tooextend uw IoT-oplossing en schema-methode aanroepen op meerdere apparaten, raadpleegt u Hallo [planning en broadcast taken] [ lnk-tutorial-jobs] zelfstudie.

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