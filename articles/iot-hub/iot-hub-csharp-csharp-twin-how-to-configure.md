---
title: aaaUse Azure IoT Hub twin apparaateigenschappen (.NET/.NET) | Microsoft Docs
description: Hoe toouse Azure IoT Hub apparaat horende tooconfigure apparaten. U gebruikt hello Azure IoT-apparaat SDK voor .NET tooimplement een gesimuleerde apparaattoepassing en hello Azure IoT service SDK voor .NET tooimplement een service-app die de apparaatconfiguratie van een met behulp van een apparaat-twin wijzigt.
services: iot-hub
documentationcenter: .net
author: dsk-2015
manager: timlt
editor: 
ms.assetid: 3c627476-f982-43c9-bd17-e0698c5d236d
ms.service: iot-hub
ms.devlang: csharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/10/2017
ms.author: dkshir
ms.openlocfilehash: 486436d29abfd5158c253adc5abf5935e0e1fdba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices"></a>Eigenschappen van de gewenste tooconfigure apparaten gebruiken
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

Aan het einde van de Hallo van deze zelfstudie hebt u twee apps voor .NET-console:

* **SimulateDeviceConfiguration**, een gesimuleerde apparaattoepassing die wordt gewacht op een gewenste configuratie-update en rapporten Hallo status van een gesimuleerde configuratieproces voor de update.
* **SetDesiredConfigurationAndQuery**, een back-end-app, die ingesteld Hallo gewenste configuratie op een apparaat en query's Hallo update configuratieproces.

> [!NOTE]
> Hallo artikel [Azure IoT SDK's] [ lnk-hub-sdks] bevat informatie over hello Azure IoT SDK's waarmee u toobuild kunt apparaat- en back-end-apps.
> 
> 

toocomplete in deze zelfstudie hebt u Hallo volgende nodig:

* Visual Studio 2015 of Visual Studio 2017.
* Een actief Azure-account. Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.

Als u Hallo gevolgd [aan de slag met apparaat horende] [ lnk-twin-tutorial] zelfstudie, u hebt al een IoT-hub en een apparaat-id genoemd **myDeviceId**. In dat geval kunt u overslaan toohello [maken Hallo gesimuleerde apparaattoepassing] [ lnk-how-to-configure-createapp] sectie.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<a id="#create-the-simulated-device-app"></a>
## <a name="create-hello-simulated-device-app"></a>Hallo gesimuleerde apparaattoepassing maken
In deze sectie maakt u een .NET-consoletoepassing die verbinding tooyour hub als maakt **myDeviceId**, wordt gewacht op een gewenste configuratie-update en vervolgens rapporten updates op Hallo gesimuleerde update configuratieproces.

1. Maak in Visual Studio een nieuw Visual C# Classic Windows Desktop-project met behulp van Hallo **consoletoepassing** projectsjabloon. Naam Hallo project **SimulateDeviceConfiguration**.
   
    ![Nieuwe Visual C# klassieke Windows-apparaat-app][img-createdeviceapp]

1. Klik in Solution Explorer met de rechtermuisknop op Hallo **SimulateDeviceConfiguration** project en klik vervolgens op **NuGet-pakketten beheren...** .
1. In Hallo **NuGet Package Manager** Selecteer **Bladeren** en zoek naar **microsoft.azure.devices.client**. Selecteer **installeren** tooinstall hello **Microsoft.Azure.Devices.Client** Inpakken en accepteer de gebruiksvoorwaarden Hallo. Deze procedure downloadt, installeert en voegt u een verwijzing toohello [Azure IoT-device SDK] [ lnk-nuget-client-sdk] NuGet-pakket en de bijbehorende afhankelijkheden.
   
    ![NuGet-Pakketbeheer venster Client-app][img-clientnuget]
1. Voeg de volgende Hallo `using` instructies boven Hallo Hallo **Program.cs** bestand:
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. Hallo na toohello velden toevoegen **programma** klasse. Vervang Hallo tijdelijke aanduidingswaarde met de verbindingsreeks van het Hallo-apparaat die u hebt genoteerd in de vorige sectie Hallo.
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;
        static TwinCollection reportedProperties = new TwinCollection();

1. Hallo na methode toohello toevoegen **programma** klasse:
 
        public static void InitClient()
        {
            try
            {
                Console.WriteLine("Connecting toohub");
                Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }
    Hallo **Client** object bevat alle Hallo-methoden die u nodig hebt toointeract met apparaat horende van Hallo-apparaat. Hallo hierboven weergegeven code initialiseert Hallo **Client** object, en vervolgens haalt Hallo apparaat twin voor **myDeviceId**.

1. Hallo na methode toohello toevoegen **programma** klasse. Deze methode stelt Hallo Beginwaarden telemetrie op Hallo lokale apparaat en klikt u vervolgens updates apparaat twin Hallo.

        public static async void InitTelemetry()
        {
            try
            {
                Console.WriteLine("Report initial telemetry config:");
                TwinCollection telemetryConfig = new TwinCollection();
                
                telemetryConfig["configId"] = "0";
                telemetryConfig["sendFrequency"] = "24h";
                reportedProperties["telemetryConfig"] = telemetryConfig;
                Console.WriteLine(JsonConvert.SerializeObject(reportedProperties));

                await Client.UpdateReportedPropertiesAsync(reportedProperties);
            }
            catch (AggregateException ex)
            {
                foreach (Exception exception in ex.InnerExceptions)
                {
                    Console.WriteLine();
                    Console.WriteLine("Error in sample: {0}", exception);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

1. Hallo na methode toohello toevoegen **programma** klasse. Dit is een terugbelactie die een wijziging in detecteert *gewenst eigenschappen* in Hallo apparaat twin.

        private static async Task OnDesiredPropertyChanged(TwinCollection desiredProperties, object userContext)
        {
            try
            {
                Console.WriteLine("Desired property change:");
                Console.WriteLine(JsonConvert.SerializeObject(desiredProperties));

                var currentTelemetryConfig = reportedProperties["telemetryConfig"];
                var desiredTelemetryConfig = desiredProperties["telemetryConfig"];

                if ((desiredTelemetryConfig != null) && (desiredTelemetryConfig["configId"] != currentTelemetryConfig["configId"]))
                {
                    Console.WriteLine("\nInitiating config change");
                    currentTelemetryConfig["status"] = "Pending";
                    currentTelemetryConfig["pendingConfig"] = desiredTelemetryConfig;

                    await Client.UpdateReportedPropertiesAsync(reportedProperties);

                    CompleteConfigChange();
                }
            }
            catch (AggregateException ex)
            {
                foreach (Exception exception in ex.InnerExceptions)
                {
                    Console.WriteLine();
                    Console.WriteLine("Error in sample: {0}", exception);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

    Deze methode updates Hallo gerapporteerd eigenschappen op Hallo lokale twin apparaatobject met Hallo configuratie updatestatus aanvraag en sets hello te**in behandeling**, en vervolgens de updates Hallo apparaat twin op Hallo-service. Nadat het Hallo apparaat twin is bijgewerkt, Hallo configuratiewijziging is voltooid door het Hallo-methode aanroepen `CompleteConfigChange` in het volgende punt Hallo beschreven.

1. Hallo na methode toohello toevoegen **programma** klasse. Deze methode wordt gesimuleerd apparaat opnieuw instellen en vervolgens updates Hallo eigenschappen van de lokale gerapporteerde status hello te stellen**geslaagd** en verwijdert Hallo **pendingConfig** element. Hallo apparaat twin op Hallo-service wordt vervolgens bijgewerkt. 

        public static async void CompleteConfigChange()
        {
            try
            {
                var currentTelemetryConfig = reportedProperties["telemetryConfig"];

                Console.WriteLine("\nSimulating device reset");
                await Task.Delay(30000); 

                Console.WriteLine("\nCompleting config change");
                currentTelemetryConfig["configId"] = currentTelemetryConfig["pendingConfig"]["configId"];
                currentTelemetryConfig["sendFrequency"] = currentTelemetryConfig["pendingConfig"]["sendFrequency"];
                currentTelemetryConfig["status"] = "Success";
                currentTelemetryConfig["pendingConfig"] = null;

                await Client.UpdateReportedPropertiesAsync(reportedProperties);
                Console.WriteLine("Config change complete \nPress any key tooexit.");
            }
            catch (AggregateException ex)
            {
                foreach (Exception exception in ex.InnerExceptions)
                {
                    Console.WriteLine();
                    Console.WriteLine("Error in sample: {0}", exception);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

1. Ten slotte toevoegen Hallo volgende regels toohello **Main** methode:

        try
        {
            InitClient();
            InitTelemetry();

            Console.WriteLine("Wait for desired telemetry...");
            Client.SetDesiredPropertyUpdateCallback(OnDesiredPropertyChanged, null).Wait();
            Console.ReadKey();
        }
        catch (AggregateException ex)
        {
            foreach (Exception exception in ex.InnerExceptions)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", exception);
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
        }

   > [!NOTE]
   > Deze zelfstudie wordt een gedrag voor updates voor gelijktijdige configuratie niet simuleren. Bepaalde configuratie-update-processen mogelijk wijzigingen van de doelconfiguratie kunnen tooaccommodate terwijl Hallo update wordt uitgevoerd, enkele mogelijk tooqueue ze en sommige kan weigeren met een fout opgetreden. Zorg ervoor dat tooconsider Hallo gewenste gedrag voor uw specifieke configuratieproces en Hallo juiste logica toevoegen voordat u begint Hallo configuratiewijziging.
   > 
   > 
1. Hallo-oplossing opzetten en Voer Hallo apparaattoepassing vanuit Visual Studio door te klikken op **F5**. U ziet op Hallo uitvoer console Hallo-berichten die aangeeft dat uw gesimuleerde apparaat is Hallo apparaat twin ophalen, Hallo telemetrie instellen en wijzigen van de gewenste eigenschap wachten. Houd Hallo-app die wordt uitgevoerd.

## <a name="create-hello-service-app"></a>Hallo-service-app maken
In deze sectie maakt u een .NET-consoletoepassing die updates Hallo *gewenst eigenschappen* op Hallo apparaat twin gekoppeld **myDeviceId** met een nieuwe telemetrie configuration-object. Vervolgens vraagt Hallo apparaat horende opgeslagen in Hallo IoT-hub en toont Hallo verschil tussen Hallo gewenst en configuraties van Hallo apparaat gerapporteerd.

1. Voeg in Visual Studio een Visual C# Classic Windows Desktop-project toohello huidige oplossing met behulp van Hallo **consoletoepassing** projectsjabloon. Naam Hallo project **SetDesiredConfigurationAndQuery**.
   
    ![Nieuw Windows Classic Desktop-project in Visual C#][img-createapp]
1. Klik in Solution Explorer met de rechtermuisknop op Hallo **SetDesiredConfigurationAndQuery** project en klik vervolgens op **NuGet-pakketten beheren...** .
1. In Hallo **NuGet Package Manager** Selecteer **Bladeren**, zoeken naar **microsoft.azure.devices**, selecteer **installeren** tooinstall Hallo **Microsoft.Azure.Devices** Inpakken en accepteer de gebruiksvoorwaarden Hallo. Deze procedure downloadt, installeert en voegt u een verwijzing toohello [Azure IoT service SDK] [ lnk-nuget-service-sdk] NuGet-pakket en de bijbehorende afhankelijkheden.
   
    ![Sluit het venster Nuget Package Manager.][img-servicenuget]
1. Voeg de volgende Hallo `using` instructies boven Hallo Hallo **Program.cs** bestand:
   
        using Microsoft.Azure.Devices;
        using System.Threading;
        using Newtonsoft.Json;
1. Hallo na toohello velden toevoegen **programma** klasse. Vervang Hallo tijdelijke aanduidingswaarde met IoT Hub-verbindingsreeks voor Hallo-hub die u hebt gemaakt in de vorige sectie Hallo Hallo.
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. Hallo na methode toohello toevoegen **programma** klasse:
   
        static private async Task SetDesiredConfigurationAndQuery()
        {
            var twin = await registryManager.GetTwinAsync("myDeviceId");
            var patch = new {
                    properties = new {
                        desired = new {
                            telemetryConfig = new {
                                configId = Guid.NewGuid().ToString(),
                                sendFrequency = "5m"
                            }
                        }
                    }
                };
   
            await registryManager.UpdateTwinAsync(twin.DeviceId, JsonConvert.SerializeObject(patch), twin.ETag);
            Console.WriteLine("Updated desired configuration");
   
            while (true)
            {
                var query = registryManager.CreateQuery("SELECT * FROM devices WHERE deviceId = 'myDeviceId'");
                var results = await query.GetNextAsTwinAsync();
                foreach (var result in results)
                {
                    Console.WriteLine("Config report for: {0}", result.DeviceId);
                    Console.WriteLine("Desired telemetryConfig: {0}", JsonConvert.SerializeObject(result.Properties.Desired["telemetryConfig"], Formatting.Indented));
                    Console.WriteLine("Reported telemetryConfig: {0}", JsonConvert.SerializeObject(result.Properties.Reported["telemetryConfig"], Formatting.Indented));
                    Console.WriteLine();
                }
                Thread.Sleep(10000);
            }
        }
   
    Hallo **register** object beschrijft alle Hallo methoden vereist toointeract met apparaat horende van Hallo-service. Deze code initialiseert Hallo **register** -object is opgehaald Hallo apparaat twin voor **myDeviceId**, en werkt vervolgens de gewenste eigenschappen met een nieuwe telemetrie configuration-object.
    Daarna wordt opgevraagd Hallo apparaat horende opgeslagen in de IoT-hub Hallo elke 10 seconden en afdrukken bestellen Hallo gewenst en telemetrie configuraties gerapporteerd. Raadpleeg toohello [IoT Hub-querytaal] [ lnk-query] toolearn hoe toogenerate rich op alle apparaten in uw rapporten.
   
   > [!IMPORTANT]
   > Deze toepassing een IoT Hub query elke 10 seconden ter illustratie. Gebruik een query toogenerate gebruikersgerichte rapporten over veel apparaten, en niet toodetect wijzigingen. Als uw oplossing realtime meldingen over apparaatgebeurtenissen vereist, gebruikt u [twin meldingen][lnk-twin-notifications].
   > 
   > 
1. Voeg regels toohello na Hallo **Main** methode:
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        SetDesiredConfigurationAndQuery();
        Console.WriteLine("Press any key tooquit.");
        Console.ReadLine();
1. Open in Solution Explorer hello, Hallo **opstartprojecten instellen...**  en zorg ervoor dat Hallo **actie** voor **SetDesiredConfigurationAndQuery** project **Start**. Hallo-oplossing bouwen.
1. Met **SimulateDeviceConfiguration** apparaat app wordt uitgevoerd, service-app uitvoeren Hallo vanuit Visual Studio met **F5**. Er is gemeld Hallo-configuratie wijzigen vanuit **in behandeling** te**geslaagd** verzenden met de nieuwe actief Hallo frequentie van vijf minuten in plaats van 24 uur.

 ![Apparaten die zijn geconfigureerd][img-deviceconfigured]
   
   > [!IMPORTANT]
   > Er is een vertraging van up tooa minuut tussen Hallo apparaat rapport opnieuw en Hallo queryresultaat. Dit is tooenable Hallo query infrastructuur toowork op zeer grote schaal. tooretrieve consistente weergaven van een enkel apparaat twin gebruiken Hallo **getDeviceTwin** methode in Hallo **register** klasse.
   > 
   > 

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie stelt u een gewenste configuratie als *gewenst eigenschappen* van Hallo oplossing back-end en een apparaat app toodetect die wijzigen en een updateproces van meerdere stappen rapportage van de status ervan via Hallo gerapporteerd simuleren geschreven Eigenschappen.

Gebruik Hallo resources toolearn hoe volgende aan:

* verzenden van telemetrie vanaf apparaten Hello [aan de slag met IoT Hub] [ lnk-iothub-getstarted] zelfstudie
* plannen of uitvoeren van bewerkingen op grote sets van apparaten Zie Hallo [planning en broadcast taken] [ lnk-schedule-jobs] zelfstudie.
* beheren van apparaten interactief (zoals het inschakelen van een ventilator van een gebruiker beheerde app), met Hallo [direct methoden gebruiken] [ lnk-methods-tutorial] zelfstudie.

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-csharp-twin-how-to-configure/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-csharp-twin-how-to-configure/createnetapp.png
[img-deviceconfigured]: media/iot-hub-csharp-csharp-twin-how-to-configure/deviceconfigured.png
[img-createdeviceapp]: media/iot-hub-csharp-csharp-twin-how-to-configure/createdeviceapp.png
[img-clientnuget]: media/iot-hub-csharp-csharp-twin-how-to-configure/devicesdknuget.png
[img-deviceconfigured]: media/iot-hub-csharp-csharp-twin-how-to-configure/deviceconfigured.png


<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/1.1.0/

[lnk-query]: iot-hub-devguide-query-language.md
[lnk-twin-notifications]: iot-hub-devguide-device-twins.md#back-end-operations
[lnk-twin-tutorial]: iot-hub-csharp-csharp-twin-getstarted.md
[lnk-schedule-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-iothub-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-how-to-configure-createapp]: iot-hub-csharp-csharp-twin-how-to-configure.md#create-the-simulated-device-app
