---
title: Aan de slag met Azure IoT Hub apparaat horende (.NET/.NET) | Microsoft Docs
description: Het gebruik van Azure IoT Hub apparaat horende labels toevoegen en vervolgens met de query voor een IoT Hub. U het apparaat met Azure IoT SDK voor .NET gebruiken voor het implementeren van de gesimuleerde apparaattoepassing en de Azure IoT service SDK voor .NET voor het implementeren van een service-app die de labels worden toegevoegd en de IoT Hub-query wordt uitgevoerd.
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
ms.openlocfilehash: 6073d594117e69676b753a1e3af25fffa3583a2b
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/11/2017
---
# <a name="get-started-with-device-twins-netnet"></a>Aan de slag met apparaat horende (.NET/.NET)
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

Aan het einde van deze zelfstudie hebt u deze apps van .NET-console:

* **CreateDeviceIdentity**, een .NET-app die u maakt een apparaat-id en de bijbehorende beveiligingssleutel waarmee uw gesimuleerde apparaat app verbinden.
* **AddTagsAndQuery**, een .NET-back-end-app die labels toegevoegd en wordt opgevraagd horende apparaten.
* **ReportConnectivity**, een .NET-apparaattoepassing dat een apparaat simuleert dat verbinding met uw IoT-hub aan de apparaat-id eerder hebt gemaakt maakt, en rapporteert de voorwaarde van de verbinding.

> [!NOTE]
> Het artikel [Azure IoT SDK's] [ lnk-hub-sdks] bevat informatie over de Azure IoT SDK's dat u gebruiken kunt om zowel apparaatgegevens als back-end-apps te bouwen.
> 
> 

Voor deze zelfstudie hebt u het volgende nodig:

* Visual Studio 2015 of Visual Studio 2017.
* Een actief Azure-account. (Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

Als u de apparaat-id in plaats daarvan programmatisch maken wilt, leest u de bijbehorende sectie in het [uw gesimuleerde apparaat verbonden met uw iothub met .NET] [ lnk-device-identity-csharp] artikel.

## <a name="create-the-service-app"></a>De service-app maken
In deze sectie maakt u een .NET-consoletoepassing maken (met C#) waarmee de metagegevens van de locatie wordt toegevoegd aan de apparaat-twin gekoppeld **myDeviceId**. Deze vervolgens het apparaat horende opgeslagen in de IoT-hub te selecteren van de apparaten die zich in de Verenigde Staten en de waarden die gerapporteerd van een mobiele verbinding een query.

1. Voeg in Visual Studio een Visual C# Classic Windows Desktop-project toe aan de huidige oplossing met behulp van de projectsjabloon **Console Application**. Noem het project **AddTagsAndQuery**.
   
    ![Nieuw Windows Classic Desktop-project in Visual C#][img-createapp]
1. Klik in Solution Explorer met de rechtermuisknop op de **AddTagsAndQuery** project en klik vervolgens op **NuGet-pakketten beheren...** .
1. In de **NuGet Package Manager** Selecteer **Bladeren** en zoek naar **microsoft.azure.devices**. Selecteer **installeren** voor het installeren van de **Microsoft.Azure.Devices** Inpakken en accepteer de gebruiksvoorwaarden. Met deze procedure worden de [Azure IoT-service-SDK][lnk-nuget-service-sdk], het NuGet-pakket en de bijbehorende afhankelijkheden gedownload en geïnstalleerd. Ook worden verwijzingen hiernaar toegevoegd.
   
    ![Sluit het venster Nuget Package Manager.][img-servicenuget]
1. Voeg aan het begin van het bestand **Program.cs** de volgende `using` instructies toe:
   
        using Microsoft.Azure.Devices;
1. Voeg de volgende velden toe aan de klasse **Program**: Vervang de tijdelijke aanduidingswaarde met de IoT Hub-verbindingsreeks voor de hub die u hebt gemaakt in de vorige sectie.
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. Voeg de volgende methode toe aan de klasse **Program**:
   
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
   
    De **RegistryManager** klasse bevat alle methoden die zijn vereist voor interactie met horende apparaten van de service. De vorige code eerst initialiseert de **registryManager** object en vervolgens haalt de apparaat-twin voor **myDeviceId**, en ten slotte de labels bijgewerkt met informatie over de gewenste locatie.
   
    Na het bijwerken, deze twee query's uitvoert: de eerste selecteert alleen de apparaat-horende apparaten zich in de **Redmond43** plant en de tweede verfijning de query voor het selecteren van alleen de apparaten die ook via het mobiele netwerk zijn verbonden.
   
    Houd er rekening mee dat de vorige code bij het maken van de **query** object, geeft u een maximum aantal geretourneerde documenten. De **query** object bevat een **HasMoreResults** Boole-eigenschap die u gebruiken kunt om aan te roepen de **GetNextAsTwinAsync** methoden meerdere keren voor het ophalen van alle resultaten. Een methode aangeroepen **GetNextAsJson** is beschikbaar voor de resultaten die bijvoorbeeld niet apparaat horende zijn resultaten van query's voor aggregatie.
1. Voeg tot slot de volgende regels toe aan de methode **Main**:
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter to exit.");
        Console.ReadLine();

1. Open in Solution Explorer de **opstartprojecten instellen...**  en zorg ervoor dat de **actie** voor **AddTagsAndQuery** project **Start**. De oplossing bouwen.
1. Deze toepassing uitvoeren door met de rechtermuisknop op de **AddTagsAndQuery** project en selecteer **Debug**, gevolgd door **nieuw exemplaar gestart**. U ziet één apparaat in de resultaten van de query wordt gevraagd voor alle apparaten vinden in **Redmond43** en er is geen voor de query die de resultaten beperkt tot apparaten die gebruikmaken van een mobiel netwerk.
   
    ![De resultaten van de query-venster][img-addtagapp]

In de volgende sectie maakt u een apparaat-app die rapporten de informatie over de connectiviteit en het resultaat van de query in de vorige sectie wordt gewijzigd.

## <a name="create-the-device-app"></a>De apparaat-app maken
In deze sectie maakt u een .NET-consoletoepassing die is verbonden met uw hub als **myDeviceId**, en werkt vervolgens de gerapporteerde eigenschappen bevatten informatie die is verbonden met een mobiel netwerk.

1. Voeg in Visual Studio een Visual C# Classic Windows Desktop-project toe aan de huidige oplossing met behulp van de projectsjabloon **Console Application**. Noem het project **ReportConnectivity**.
   
    ![Nieuwe Visual C# klassieke Windows-apparaat-app][img-createdeviceapp]
    
1. Klik in Solution Explorer met de rechtermuisknop op de **ReportConnectivity** project en klik vervolgens op **NuGet-pakketten beheren...** .
1. In de **NuGet Package Manager** Selecteer **Bladeren** en zoek naar **microsoft.azure.devices.client**. Selecteer **installeren** voor het installeren van de **Microsoft.Azure.Devices.Client** Inpakken en accepteer de gebruiksvoorwaarden. Deze procedure downloadt, installeert en voegt u een verwijzing naar de [Azure IoT-device SDK] [ lnk-nuget-client-sdk] NuGet-pakket en de bijbehorende afhankelijkheden.
   
    ![NuGet-Pakketbeheer venster Client-app][img-clientnuget]
1. Voeg aan het begin van het bestand **Program.cs** de volgende `using` instructies toe:
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. Voeg de volgende velden toe aan de klasse **Program**: Vervang de tijdelijke aanduidingswaarde met de verbindingsreeks voor apparaten die u in de vorige sectie hebt genoteerd.
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. Voeg de volgende methode toe aan de klasse **Program**:

       public static async void InitClient()
        {
            try
            {
                Console.WriteLine("Connecting to hub");
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

    De **Client** object bevat de methoden die u nodig hebt om te communiceren met horende apparaten van het apparaat. De hierboven weergegeven code initialiseert de **Client** object, en vervolgens haalt de apparaat-twin voor **myDeviceId**.

1. Voeg de volgende methode toe aan de klasse **Program**:
   
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

   De bovenstaande updates code **myDeviceId**de eigenschap met de connectiviteit-informatie gerapporteerd.

1. Voeg tot slot de volgende regels toe aan de methode **Main**:
   
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
       Console.WriteLine("Press Enter to exit.");
       Console.ReadLine();

1. Open in Solution Explorer de **opstartprojecten instellen...**  en zorg ervoor dat de **actie** voor **ReportConnectivity** project **Start**. De oplossing bouwen.
1. Deze toepassing uitvoeren door met de rechtermuisknop op de **ReportConnectivity** project en selecteer **Debug**, gevolgd door **nieuw exemplaar gestart**. U ziet het ophalen van de informatie twin, en vervolgens verzenden connectiviteit heeft als een *gerapporteerd eigenschap*.
   
    ![Apparaat-app verbinding rapport uitvoeren][img-rundeviceapp]
    
    
1. Nu dat het apparaat heeft gemeld dat de gegevens over de connectiviteit, moet deze worden weergegeven in beide query's. Uitvoeren van de .NET **AddTagsAndQuery** app opnieuw uit te voeren de query's. Deze tijd **myDeviceId** moet worden weergegeven in beide queryresultaten.
   
    ![Connectiviteit van apparaten is gerapporteerd][img-tagappsuccess]

## <a name="next-steps"></a>Volgende stappen
In deze handleiding hebt u een nieuwe IoT-hub geconfigureerd in Azure Portal en vervolgens een apparaat-id gemaakt in het id-register van de IoT-hub. U metagegevens van apparaten als labels toegevoegd vanuit een back-end-app en een gesimuleerde apparaattoepassing geschreven naar apparaten connectiviteit rapportgegevens in de apparaat-twin. Ook hebt u geleerd hoe deze gegevens met behulp van de SQL-achtige IoT Hub-querytaal opvragen.

Gebruik de volgende bronnen voor meer informatie over hoe:

* verzenden van telemetrie vanaf apparaten met de [aan de slag met IoT Hub] [ lnk-iothub-getstarted] zelfstudie
* apparaten configureren met de gewenste eigenschappen van apparaat twin met de [gebruik gewenst eigenschappen voor het configureren van apparaten] [ lnk-twin-how-to-configure] zelfstudie
* beheren van apparaten interactief (zoals het inschakelen van een ventilator van een gebruiker beheerde app) met de [direct methoden gebruiken] [ lnk-methods-tutorial] zelfstudie.

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

