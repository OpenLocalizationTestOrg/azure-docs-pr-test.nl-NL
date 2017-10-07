---
title: Azure IoT Hub aaaUse directe methoden (.NET/.NET) | Microsoft Docs
description: Hoe Azure IoT Hub toouse directe methoden. U gebruikt hello Azure IoT-device SDK voor .NET tooimplement een gesimuleerde apparaattoepassing met een directe methode en hello Azure IoT service SDK voor .NET tooimplement een service-app die Hallo directe methode aanroept.
services: iot-hub
documentationcenter: 
author: dsk-2015
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: dkshir
ms.openlocfilehash: d4fa093a99558ec6faf294c2583a14a722b9ac03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-netnet"></a>Directe methoden (.NET/.NET) gebruiken
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

In deze zelfstudie zijn we continu toodevelop twee .NET-console apps:

* **CallMethodOnDevice**, een back-end-app, die een methode wordt aangeroepen in de gesimuleerde apparaattoepassing Hallo en antwoord Hallo weergegeven.
* **SimulateDeviceMethods**, een consoletoepassing die overeenkomt met een apparaat tooyour IoT-hub te koppelen aan de apparaat-id Hallo eerder hebt gemaakt en toohello methode aangeroepen door Hallo cloud reageert.

> [!NOTE]
> Hallo artikel [Azure IoT SDK's] [ lnk-hub-sdks] bevat informatie over hello Azure IoT SDK's waarmee u toobuild beide toorun toepassingen op apparaten en de back-end van uw oplossing kunt.
> 
> 

toocomplete deze zelfstudie hebt u nodig:

* Visual Studio 2015 of Visual Studio 2017.
* Een actief Azure-account. (Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

Als u toocreate Hallo apparaat-id via een programma in plaats daarvan wilt, lezen Hallo overeenkomstige sectie in Hallo [verbinding maken met uw gesimuleerde apparaat tooyour iothub met .NET] [ lnk-device-identity-csharp] artikel.


## <a name="create-a-simulated-device-app"></a>Een gesimuleerde apparaattoepassing maken
In deze sectie maakt u een .NET-consoletoepassing die tooa methode met de naam door Hallo oplossing back-end reageert.

1. Voeg in Visual Studio een Visual C# Classic Windows Desktop-project toohello huidige oplossing met behulp van Hallo **consoletoepassing** projectsjabloon. Naam Hallo project **SimulateDeviceMethods**.
   
    ![Nieuwe Visual C# klassieke Windows-apparaat-app][img-createdeviceapp]
    
1. Klik in Solution Explorer met de rechtermuisknop op Hallo **SimulateDeviceMethods** project en klik vervolgens op **NuGet-pakketten beheren...** .
1. In Hallo **NuGet Package Manager** Selecteer **Bladeren** en zoek naar **microsoft.azure.devices.client**. Selecteer **installeren** tooinstall hello **Microsoft.Azure.Devices.Client** Inpakken en accepteer de gebruiksvoorwaarden Hallo. Deze procedure downloadt, installeert en voegt u een verwijzing toohello [Azure IoT-device SDK] [ lnk-nuget-client-sdk] NuGet-pakket en de bijbehorende afhankelijkheden.
   
    ![NuGet-Pakketbeheer venster Client-app][img-clientnuget]
1. Voeg de volgende Hallo `using` instructies boven Hallo Hallo **Program.cs** bestand:
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;

1. Hallo na toohello velden toevoegen **programma** klasse. Vervang Hallo tijdelijke aanduidingswaarde met de verbindingsreeks van het Hallo-apparaat die u hebt genoteerd in de vorige sectie Hallo.
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. Hallo tooimplement Hallo directe methode volgen op Hallo apparaat toevoegen:

        static Task<MethodResponse> WriteLineToConsole(MethodRequest methodRequest, object userContext)
        {
            Console.WriteLine();
            Console.WriteLine("\t{0}", methodRequest.DataAsJson);
            Console.WriteLine("\nReturning response for method {0}", methodRequest.Name);

            string result = "'Input was written toolog.'";
            return Task.FromResult(new MethodResponse(Encoding.UTF8.GetBytes(result), 200));
        }

1. Voeg code toohello na Hallo **Main** methode tooopen Hallo verbinding tooyour IoT hub en geïnitialiseerd Hallo methode listener:
   
        try
        {
            Console.WriteLine("Connecting toohub");
            Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);

            // setup callback for "writeLine" method
            Client.SetMethodHandlerAsync("writeLine", WriteLineToConsole, null).Wait();
            Console.WriteLine("Waiting for direct method call\n Press enter tooexit.");
            Console.ReadLine();

            Console.WriteLine("Exiting...");

            // as a good practice, remove hello "writeLine" handler
            Client.SetMethodHandlerAsync("writeLine", null, null).Wait();
            Client.CloseAsync().Wait();
        }
        catch (Exception ex)
        {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
        }
        
1. In Visual Studio Solution Explorer hello, met de rechtermuisknop op uw oplossing en klik op **Opstartprojecten instellen...** . Selecteer **één opstartproject**, en selecteer vervolgens Hallo **SimulateDeviceMethods** -project in het vervolgkeuzemenu Hallo.        

> [!NOTE]
> tookeep dingen eenvoudige, deze zelfstudie wordt niet geïmplementeerd voor een beleid voor opnieuw proberen. In productiecode moet u beleid voor opnieuw proberen (zoals verbinding opnieuw), zoals voorgesteld in de MSDN-artikel Hallo implementeren [afhandeling van tijdelijke fout][lnk-transient-faults].
> 
> 

## <a name="call-a-direct-method-on-a-device"></a>Een directe methode is aangeroepen voor een apparaat
In deze sectie maakt maken u een .NET-consoletoepassing die een methode wordt aangeroepen in de gesimuleerde apparaattoepassing Hallo en wordt vervolgens weergegeven antwoord Hallo.

1. Voeg in Visual Studio een Visual C# Classic Windows Desktop-project toohello huidige oplossing met behulp van Hallo **consoletoepassing** projectsjabloon. Zorg ervoor dat .NET Framework-versie Hallo 4.5.1 of later. Naam Hallo project **CallMethodOnDevice**.
   
    ![Nieuw Windows Classic Desktop-project in Visual C#][img-createserviceapp]
2. Klik in Solution Explorer met de rechtermuisknop op Hallo **CallMethodOnDevice** project en klik vervolgens op **NuGet-pakketten beheren...** .
3. In Hallo **NuGet Package Manager** Selecteer **Bladeren**, zoeken naar **microsoft.azure.devices**, selecteer **installeren** tooinstall Hallo **Microsoft.Azure.Devices** Inpakken en accepteer de gebruiksvoorwaarden Hallo. Deze procedure downloadt, installeert en voegt u een verwijzing toohello [Azure IoT service SDK] [ lnk-nuget-service-sdk] NuGet-pakket en de bijbehorende afhankelijkheden.
   
    ![Sluit het venster Nuget Package Manager.][img-servicenuget]

4. Voeg de volgende Hallo `using` instructies boven Hallo Hallo **Program.cs** bestand:
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. Hallo na toohello velden toevoegen **programma** klasse. Vervang Hallo tijdelijke aanduidingswaarde met IoT Hub-verbindingsreeks voor Hallo-hub die u hebt gemaakt in de vorige sectie Hallo Hallo.
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. Hallo na methode toohello toevoegen **programma** klasse:
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line toobe written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    Deze methode wordt aangeroepen voor een directe methode met de naam `writeLine` op Hallo `myDeviceId` apparaat. Vervolgens worden Hallo respons van Hallo-apparaat op Hallo console geschreven. Houd er rekening mee hoe het is mogelijk toospecify een time-outwaarde voor Hallo apparaat toorespond.
7. Voeg regels toohello na Hallo **Main** methode:
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. In Visual Studio Solution Explorer hello, met de rechtermuisknop op uw oplossing en klik op **Opstartprojecten instellen...** . Selecteer **één opstartproject**, en selecteer vervolgens Hallo **CallMethodOnDevice** -project in het vervolgkeuzemenu Hallo.

## <a name="run-hello-applications"></a>Hallo-toepassingen uitvoeren
U bent nu klaar toorun Hallo toepassingen.

1. Uitvoeren van .NET-apparaattoepassing Hallo **SimulateDeviceMethods**. Deze zou moeten starten luisteren naar methodeaanroepen van uw IoT-Hub: 

    ![Apparaat-app uitvoeren][img-deviceapprun]
1. Nu dat het Hallo-apparaat is verbonden en Hallo .NET wacht methode aanroepen, voer **CallMethodOnDevice** app tooinvoke Hallo methode in de gesimuleerde apparaattoepassing Hallo. U ziet Hallo apparaat antwoord is geschreven in Hallo-console.
   
    ![Service-app uitvoeren][img-serviceapprun]
1. Hallo apparaat reageert vervolgens toohello methode door dit bericht afdrukken:
   
    ![Directe methode aangeroepen op Hallo-apparaat][img-directmethodinvoked]

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie maakt u een nieuwe iothub geconfigureerd in hello Azure-portal en vervolgens een apparaat-id in de id-register Hallo iothub hebt gemaakt. U hebt deze apparaat-id tooenable Hallo gesimuleerd apparaat app tooreact toomethods aangeroepen door Hallo cloud gebruikt. Hebt u ook een app die wordt aangeroepen methoden op Hallo apparaat en geeft weer Hallo-antwoord van Hallo-apparaat hebt gemaakt. 

toocontinue aan de slag met IoT Hub en tooexplore raadpleegt u andere IoT-scenario's:

* [Aan de slag met IoT Hub]
* [Taken plannen op meerdere apparaten][lnk-devguide-jobs]

toolearn hoe tooextend uw IoT-oplossing en schema-methode aanroepen op meerdere apparaten, raadpleegt u Hallo [planning en broadcast taken] [ lnk-tutorial-jobs] zelfstudie.

<!-- Images. -->
[img-createdeviceapp]: ./media/iot-hub-csharp-csharp-direct-methods/create-device-app.png
[img-clientnuget]: ./media/iot-hub-csharp-csharp-direct-methods/device-app-nuget.png
[img-createserviceapp]: ./media/iot-hub-csharp-csharp-direct-methods/create-service-app.png
[img-servicenuget]: ./media/iot-hub-csharp-csharp-direct-methods/service-app-nuget.png
[img-deviceapprun]: ./media/iot-hub-csharp-csharp-direct-methods/run-device-app.png
[img-serviceapprun]: ./media/iot-hub-csharp-csharp-direct-methods/run-service-app.png
[img-directmethodinvoked]: ./media/iot-hub-csharp-csharp-direct-methods/direct-method-invoked.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-device-identity-csharp]: iot-hub-csharp-csharp-getstarted.md#DeviceIdentity_csharp

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[Aan de slag met IoT Hub]: iot-hub-node-node-getstarted.md
