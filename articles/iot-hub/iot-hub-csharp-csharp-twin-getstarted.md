---
title: aaaGet de slag met Azure IoT Hub apparaat horende (.NET/.NET) | Microsoft Docs
description: Hoe toouse Azure IoT Hub apparaat horende tooadd tags en gebruik vervolgens een IoT Hub-query. U hello Azure IoT-device SDK voor .NET tooimplement Hallo gesimuleerde apparaattoepassing en hello Azure IoT service SDK voor .NET tooimplement een service-app die Hallo-labels toegevoegd en Hallo IoT Hub-query wordt uitgevoerd.
services: iot-hub
documentationcenter: node
author: dsk-2015
manager: timlt
editor: 
ms.assetid: f7e23b6e-bfde-4fba-a6ec-dbb0f0e005f4
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: dkshir
ms.openlocfilehash: 7fa73ac896c44e79c6522d252cd1515bd6e7bb2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-netnet"></a>Aan de slag met apparaat horende (.NET/.NET)
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

Aan het einde van de Hallo van deze zelfstudie hebt u deze apps van .NET-console:

* **CreateDeviceIdentity**, een .NET-app die u maakt een apparaat-id en de bijbehorende sleutel tooconnect app op uw gesimuleerde apparaat.
* **AddTagsAndQuery**, een .NET-back-end-app die labels toegevoegd en wordt opgevraagd horende apparaten.
* **ReportConnectivity**, een .NET-apparaattoepassing dat een apparaat simuleert dat tooyour IoT-hub is verbonden met de apparaat-id Hallo eerder hebt gemaakt, en rapporteert de voorwaarde van de verbinding.

> [!NOTE]
> Hallo artikel [Azure IoT SDK's] [ lnk-hub-sdks] bevat informatie over hello Azure IoT SDK's waarmee u toobuild kunt apparaat- en back-end-apps.
> 
> 

toocomplete in deze zelfstudie hebt u Hallo volgende nodig:

* Visual Studio 2015 of Visual Studio 2017.
* Een actief Azure-account. (Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

Als u toocreate Hallo apparaat-id via een programma in plaats daarvan wilt, lezen Hallo overeenkomstige sectie in Hallo [verbinding maken met uw gesimuleerde apparaat tooyour iothub met .NET] [ lnk-device-identity-csharp] artikel.

## <a name="create-hello-service-app"></a>Hallo-service-app maken
In deze sectie maakt u een .NET-consoletoepassing maken (met C#) die wordt toegevoegd locatie metagegevens toohello apparaat twin die zijn gekoppeld aan **myDeviceId**. Vervolgens query's Hallo apparaat horende opgeslagen ons in IoT-hub Hallo Hallo apparaten zich in Hallo selecteren en vervolgens Hallo die een mobiele verbinding gerapporteerd.

1. Voeg in Visual Studio een Visual C# Classic Windows Desktop-project toohello huidige oplossing met behulp van Hallo **consoletoepassing** projectsjabloon. Naam Hallo project **AddTagsAndQuery**.
   
    ![Nieuw Windows Classic Desktop-project in Visual C#][img-createapp]
1. Klik in Solution Explorer met de rechtermuisknop op Hallo **AddTagsAndQuery** project en klik vervolgens op **NuGet-pakketten beheren...** .
1. In Hallo **NuGet Package Manager** Selecteer **Bladeren** en zoek naar **microsoft.azure.devices**. Selecteer **installeren** tooinstall hello **Microsoft.Azure.Devices** Inpakken en accepteer de gebruiksvoorwaarden Hallo. Deze procedure downloadt, installeert en voegt u een verwijzing toohello [Azure IoT service SDK] [ lnk-nuget-service-sdk] NuGet-pakket en de bijbehorende afhankelijkheden.
   
    ![Sluit het venster Nuget Package Manager.][img-servicenuget]
1. Voeg de volgende Hallo `using` instructies boven Hallo Hallo **Program.cs** bestand:
   
        using Microsoft.Azure.Devices;
1. Hallo na toohello velden toevoegen **programma** klasse. Vervang Hallo tijdelijke aanduidingswaarde met IoT Hub-verbindingsreeks voor Hallo-hub die u hebt gemaakt in de vorige sectie Hallo Hallo.
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. Hallo na methode toohello toevoegen **programma** klasse:
   
        public static async Task AddTagsAndQuery()
        {
            var twin = await registryManager.GetTwinAsync("myDeviceId");
            var patch =
                @"{
                    tags: {
                        location: {
                            region: 'US',
                            plant: 'Redmond43'
                        }
                    }
                }";
            await registryManager.UpdateTwinAsync(twin.DeviceId, patch, twin.ETag);
   
            var query = registryManager.CreateQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            var twinsInRedmond43 = await query.GetNextAsTwinAsync();
            Console.WriteLine("Devices in Redmond43: {0}", string.Join(", ", twinsInRedmond43.Select(t => t.DeviceId)));
   
            query = registryManager.CreateQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            var twinsInRedmond43UsingCellular = await query.GetNextAsTwinAsync();
            Console.WriteLine("Devices in Redmond43 using cellular network: {0}", string.Join(", ", twinsInRedmond43UsingCellular.Select(t => t.DeviceId)));
        }
   
    Hallo **RegistryManager** klasse beschrijft alle Hallo methoden vereist toointeract met apparaat horende van Hallo-service. Hallo vorige code initialiseert eerst Hallo **registryManager** object, en vervolgens haalt Hallo apparaat twin voor **myDeviceId**, en ten slotte de labels bijgewerkt met informatie over de locatie van de gewenste Hallo.
   
    Na het bijwerken, deze twee query's uitvoert: Hallo selecteert eerst alleen Hallo apparaat horende apparaten zich in Hallo **Redmond43** installaties en Hallo tweede verfijning Hallo query tooselect alleen Hallo apparaten die ook zijn verbonden via mobiel netwerk.
   
    Houd er rekening mee dat vorige code Hallo bij het maken van Hallo **query** object, geeft u een maximum aantal geretourneerde documenten. Hallo **query** object bevat een **HasMoreResults** Boole-eigenschap waarmee u tooinvoke hello kunt **GetNextAsTwinAsync** methoden meerdere keren tooretrieve alle resultaten. Een methode aangeroepen **GetNextAsJson** is beschikbaar voor de resultaten die bijvoorbeeld niet apparaat horende zijn resultaten van query's voor aggregatie.
1. Voeg regels toohello na Hallo **Main** methode:
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. Open in Solution Explorer hello, Hallo **opstartprojecten instellen...**  en zorg ervoor dat Hallo **actie** voor **AddTagsAndQuery** project **Start**. Hallo-oplossing bouwen.
1. Deze toepassing uitvoeren door met de rechtermuisknop op Hallo **AddTagsAndQuery** project en selecteer **Debug**, gevolgd door **nieuw exemplaar gestart**. U ziet één apparaat in Hallo resultaten voor Hallo query vragen voor alle apparaten vinden in **Redmond43** en geen voor de Hallo-query die Hallo beperkt resultaten toodevices die gebruikmaken van een mobiel netwerk.
   
    ![De resultaten van de query-venster][img-addtagapp]

In de volgende sectie Hallo, maakt u een apparaat-app die Hallo connectiviteit informatie rapporteert en wijzigingen resultaat van query in de vorige sectie Hallo HALLO hallo.

## <a name="create-hello-device-app"></a>Hallo apparaattoepassing maken
In deze sectie maakt u een .NET-consoletoepassing die verbinding tooyour hub als maakt **myDeviceId**, en werkt vervolgens de gerapporteerde toocontain Hallo eigenschapsgegevens dat is verbonden met een mobiel netwerk.

1. Voeg in Visual Studio een Visual C# Classic Windows Desktop-project toohello huidige oplossing met behulp van Hallo **consoletoepassing** projectsjabloon. Naam Hallo project **ReportConnectivity**.
   
    ![Nieuwe Visual C# klassieke Windows-apparaat-app][img-createdeviceapp]
    
1. Klik in Solution Explorer met de rechtermuisknop op Hallo **ReportConnectivity** project en klik vervolgens op **NuGet-pakketten beheren...** .
1. In Hallo **NuGet Package Manager** Selecteer **Bladeren** en zoek naar **microsoft.azure.devices.client**. Selecteer **installeren** tooinstall hello **Microsoft.Azure.Devices.Client** Inpakken en accepteer de gebruiksvoorwaarden Hallo. Deze procedure downloadt, installeert en voegt u een verwijzing toohello [Azure IoT-device SDK] [ lnk-nuget-client-sdk] NuGet-pakket en de bijbehorende afhankelijkheden.
   
    ![NuGet-Pakketbeheer venster Client-app][img-clientnuget]
1. Voeg de volgende Hallo `using` instructies boven Hallo Hallo **Program.cs** bestand:
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. Hallo na toohello velden toevoegen **programma** klasse. Vervang Hallo tijdelijke aanduidingswaarde met de verbindingsreeks van het Hallo-apparaat die u hebt genoteerd in de vorige sectie Hallo.
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. Hallo na methode toohello toevoegen **programma** klasse:

       public static async void InitClient()
        {
            try
            {
                Console.WriteLine("Connecting toohub");
                Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);
                Console.WriteLine("Retrieving twin");
                await Client.GetTwinAsync();
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

    Hallo **Client** object bevat alle Hallo-methoden die u nodig hebt toointeract met apparaat horende van Hallo-apparaat. Hallo hierboven weergegeven code initialiseert Hallo **Client** object, en vervolgens haalt Hallo apparaat twin voor **myDeviceId**.

1. Hallo na methode toohello toevoegen **programma** klasse:
   
        public static async void ReportConnectivity()
        {
            try
            {
                Console.WriteLine("Sending connectivity data as reported property");
                
                TwinCollection reportedProperties, connectivity;
                reportedProperties = new TwinCollection();
                connectivity = new TwinCollection();
                connectivity["type"] = "cellular";
                reportedProperties["connectivity"] = connectivity;
                await Client.UpdateReportedPropertiesAsync(reportedProperties);
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

   Hallo bovenstaande updates code **myDeviceId**de eigenschap met de informatie over de connectiviteit van Hallo gerapporteerd.

1. Voeg regels toohello na Hallo **Main** methode:
   
       try
       {
            InitClient();
            ReportConnectivity();
       }
       catch (Exception ex)
       {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
       }
       Console.WriteLine("Press Enter tooexit.");
       Console.ReadLine();

1. Open in Solution Explorer hello, Hallo **opstartprojecten instellen...**  en zorg ervoor dat Hallo **actie** voor **ReportConnectivity** project **Start**. Hallo-oplossing bouwen.
1. Deze toepassing uitvoeren door met de rechtermuisknop op Hallo **ReportConnectivity** project en selecteer **Debug**, gevolgd door **nieuw exemplaar gestart**. U ziet het Hallo twin informatie verkrijgen en vervolgens verzenden connectiviteit heeft als een *gerapporteerd eigenschap*.
   
    ![Connectiviteit van apparaten app tooreport uitvoeren][img-rundeviceapp]
    
    
1. Nu dat hello apparaat de connectiviteit informatie gerapporteerd, moet deze worden weergegeven in beide query's. Voer Hallo .NET **AddTagsAndQuery** app toorun Hallo query opnieuw. Deze tijd **myDeviceId** moet worden weergegeven in beide queryresultaten.
   
    ![Connectiviteit van apparaten is gerapporteerd][img-tagappsuccess]

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie maakt u een nieuwe iothub geconfigureerd in hello Azure-portal en vervolgens een apparaat-id in de id-register Hallo iothub hebt gemaakt. U metagegevens van apparaten als labels toegevoegd vanuit een back-end-app en een gesimuleerd apparaat app tooreport-apparaatgegevens connectiviteit in Hallo apparaat twin geschreven. U hebt ook geleerd hoe tooquery deze informatie Hallo IoT-Hub SQL-achtige query language gebruiken.

Gebruik Hallo resources toolearn hoe volgende aan:

* verzenden van telemetrie vanaf apparaten Hello [aan de slag met IoT Hub] [ lnk-iothub-getstarted] zelfstudie
* apparaten configureren met de gewenste eigenschappen van apparaat twin Hello [gebruik gewenst eigenschappen tooconfigure apparaten] [ lnk-twin-how-to-configure] zelfstudie
* beheren van apparaten interactief (zoals het inschakelen van een ventilator van een gebruiker beheerde app) met Hallo [direct methoden gebruiken] [ lnk-methods-tutorial] zelfstudie.

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-csharp-twin-getstarted/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-csharp-twin-getstarted/createnetapp.png
[img-addtagapp]: media/iot-hub-csharp-csharp-twin-getstarted/addtagapp.png
[img-createdeviceapp]: media/iot-hub-csharp-csharp-twin-getstarted/createdeviceapp.png
[img-clientnuget]: media/iot-hub-csharp-csharp-twin-getstarted/clientsdknuget.png
[img-rundeviceapp]: media/iot-hub-csharp-csharp-twin-getstarted/rundeviceapp.png
[img-tagappsuccess]: media/iot-hub-csharp-csharp-twin-getstarted/tagappsuccess.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/

[lnk-device-identity-csharp]: iot-hub-csharp-csharp-getstarted.md#DeviceIdentity_csharp
[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-twin-how-to-configure]: iot-hub-csharp-node-twin-how-to-configure.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

