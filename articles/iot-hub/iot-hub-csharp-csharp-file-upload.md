---
title: aaaUpload bestanden van apparaten tooAzure IoT Hub met .NET | Microsoft Docs
description: "Hoe tooupload bestanden van een apparaat toohello cloud met Azure IoT-device SDK voor .NET. Geüploade bestanden worden opgeslagen in een Azure storage-blob-container."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 4759d229-f856-4526-abda-414f8b00a56d
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/04/2017
ms.author: elioda
ms.openlocfilehash: 07d555f6ba8b067bbd3233bc8eebaa220ad2388b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-from-your-device-toohello-cloud-with-iot-hub-using-net"></a>Uploaden van bestanden van uw apparaat toohello cloud met IoT Hub met .NET

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

Deze zelfstudie bouwt voort op Hallo-code in Hallo [Cloud naar apparaat verzenden met IoT Hub](iot-hub-csharp-csharp-c2d.md) zelfstudie tooshow u hoe toouse Hallo functies voor het uploaden van bestanden van IoT Hub. Hier ziet u hoe aan:

- Veilig een apparaat voorzien van een Azure blob-URI voor het uploaden van een bestand.
- Hallo IoT Hub-bestand uploaden meldingen tootrigger verwerken Hallo-bestand in de back-end van uw app gebruiken.

Hallo [aan de slag met IoT Hub](iot-hub-csharp-csharp-getstarted.md) en [Cloud naar apparaat verzenden met IoT Hub](iot-hub-csharp-csharp-c2d.md) zelfstudies ziet Hallo apparaat-naar-cloud- en cloud-naar-apparaat messaging basisfunctionaliteit van IoT-Hub. Hallo [proces apparaat-naar-cloudberichten](iot-hub-csharp-csharp-process-d2c.md) zelfstudie beschrijft een manier tooreliably store apparaat-naar-cloud-berichten in Azure blob-opslag. In sommige scenario's kan niet u echter gemakkelijk toewijzen hello gegevens verzenden van uw apparaten in hello relatief klein apparaat-naar-cloud-berichten die IoT Hub accepteert. Bijvoorbeeld:

* Grote bestanden met afbeeldingen
* Video's
* Trillingen gegevens dat met hoge frequentie
* Een vorm van voorverwerkte gegevens

Deze bestanden zijn meestal batch verwerkt in Hallo cloud met hulpprogramma's zoals [Azure Data Factory](../data-factory/index.md) of Hallo [Hadoop](../hdinsight/index.md) stack. Wanneer u tooupload bestanden van een apparaat nodig hebt, kunt u nog steeds Hallo beveiliging en betrouwbaarheid van IoT Hub gebruiken.

Aan Hallo einde van deze zelfstudie kunt u twee apps voor .NET-console uitvoeren:

* **SimulatedDevice**, een aangepaste versie van het Hallo-app gemaakt in Hallo [Cloud naar apparaat verzenden met IoT Hub](iot-hub-csharp-csharp-c2d.md) zelfstudie. Deze app uploadt een bestand toostorage met behulp van een SAS-URI geleverd door uw IoT-hub.
* **ReadFileUploadNotification**, dat bestand uploaden meldingen ontvangt van uw IoT-hub.

> [!NOTE]
> IoT Hub biedt ondersteuning voor veel apparaatplatforms en talen (inclusief C, Java en Javascript) via Azure IoT-apparaat SDK's. Raadpleeg toohello [Azure IoT Developer Center] voor stapsgewijze instructies voor het tooconnect uw apparaat tooAzure IoT Hub.

toocomplete in deze zelfstudie, moet u hello te volgen:

* Visual Studio 2015 of Visual Studio 2017
* Een actief Azure-account. (Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a>Een bestand vanaf een apparaat-app uploaden

In deze sectie maakt u Hallo apparaattoepassing u hebt gemaakt in wijzigen [Cloud naar apparaat verzenden met IoT Hub](iot-hub-csharp-csharp-c2d.md) tooreceive cloud-naar-apparaat-berichten uit Hallo iothub.

1. In Visual Studio met de rechtermuisknop op Hallo **SimulatedDevice** project, klikt u op **toevoegen**, en klik vervolgens op **bestaand Item**. Navigeer tooan afbeeldingsbestand en deze opnemen in uw project. Deze zelfstudie wordt ervan uitgegaan dat Hallo installatiekopie heet `image.jpg`.

1. Met de rechtermuisknop op de installatiekopie van het Hallo en klik vervolgens op **eigenschappen**. Zorg ervoor dat **tooOutput Directory kopiëren** te is ingesteld,**altijd kopiëren**.

    ![][1]

1. In Hallo **Program.cs** bestand, het toevoegen van Hallo instructies Hallo boven aan het Hallo-bestand te volgen:

    ```csharp
    using System.IO;
    ```

1. Hallo na methode toohello toevoegen **programma** klasse:

    ```csharp
    private static async void SendToBlobAsync()
    {
        string fileName = "image.jpg";
        Console.WriteLine("Uploading file: {0}", fileName);
        var watch = System.Diagnostics.Stopwatch.StartNew();

        using (var sourceData = new FileStream(@"image.jpg", FileMode.Open))
        {
            await deviceClient.UploadToBlobAsync(fileName, sourceData);
        }

        watch.Stop();
        Console.WriteLine("Time tooupload file: {0}ms\n", watch.ElapsedMilliseconds);
    }
    ```

    Hallo `UploadToBlobAsync` methode neemt in Hallo bestandsnaam en bron van de stroom van Hallo bestand toobe geüpload en Hallo uploaden toostorage verwerkt. Hallo-consoletoepassing weergeven Hallo duurt tooupload Hallo-bestand

1. Toevoegen van de volgende methode in Hallo Hallo **Main** methode aan vóór Hallo `Console.ReadLine()` regel:

    ```csharp
    SendToBlobAsync();
    ```

> [!NOTE]
> Deze zelfstudie implementeert voor de eenvoud mogelijk te houden, niet een beleid voor opnieuw proberen. In productiecode moet u beleid voor opnieuw proberen (zoals exponentieel uitstel), zoals voorgesteld in de MSDN-artikel Hallo implementeren [afhandeling van tijdelijke fout].

## <a name="receive-a-file-upload-notification"></a>Ontvangt een melding van bestand uploaden

In deze sectie schrijft u een .NET-consoletoepassing die bestand uploaden meldingsberichten uit IoT Hub ontvangt.

1. Maak in Hallo huidige Visual Studio-oplossing een Visual C# Windows-project met behulp van Hallo **consoletoepassing** projectsjabloon. Naam Hallo project **ReadFileUploadNotification**.

    ![Nieuw project in Visual Studio][2]

1. Klik in Solution Explorer met de rechtermuisknop op Hallo **ReadFileUploadNotification** project en klik vervolgens op **NuGet-pakketten beheren...** .

1. In Hallo **NuGet Package Manager** venster, zoekt u **Microsoft.Azure.Devices**, klikt u op **installeren**, en accepteer de gebruiksvoorwaarden Hallo.

    Deze actie downloadt, installeert en voegt u een verwijzing toohello [Azure IoT service SDK NuGet-pakket] in Hallo **ReadFileUploadNotification** project.

1. In Hallo **Program.cs** bestand, het toevoegen van Hallo instructies Hallo boven aan het Hallo-bestand te volgen:

    ```csharp
    using Microsoft.Azure.Devices;
    ```

1. Hallo na toohello velden toevoegen **programma** klasse. Vervang de aanduidingswaarde Hallo door Hallo IoT hub-verbindingsreeks uit [aan de slag met IoT Hub]:

    ```csharp
    static ServiceClient serviceClient;
    static string connectionString = "{iot hub connection string}";
    ```

1. Hallo na methode toohello toevoegen **programma** klasse:

    ```csharp
    private async static void ReceiveFileUploadNotificationAsync()
    {
        var notificationReceiver = serviceClient.GetFileNotificationReceiver();

        Console.WriteLine("\nReceiving file upload notification from service");
        while (true)
        {
            var fileUploadNotification = await notificationReceiver.ReceiveAsync();
            if (fileUploadNotification == null) continue;

            Console.ForegroundColor = ConsoleColor.Yellow;
            Console.WriteLine("Received file upload noticiation: {0}", string.Join(", ", fileUploadNotification.BlobName));
            Console.ResetColor();

            await notificationReceiver.CompleteAsync(fileUploadNotification);
        }
    }
    ```

    Opmerking: dit patroon ontvangen is dezelfde één gebruikte tooreceive cloud-naar-apparaat berichten van apparaattoepassing Hallo Hallo.

1. Voeg regels toohello na Hallo **Main** methode:

    ```csharp
    Console.WriteLine("Receive file upload notifications\n");
    serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
    ReceiveFileUploadNotificationAsync();
    Console.WriteLine("Press Enter tooexit\n");
    Console.ReadLine();
    ```

## <a name="run-hello-applications"></a>Hallo-toepassingen uitvoeren

U bent nu klaar toorun Hallo toepassingen.

1. Met de rechtermuisknop op uw oplossing in Visual Studio, en selecteer **Set StartUp projects**. Selecteer **meerdere opstartprojecten**, selecteer daarna Hallo **Start** actie voor **ReadFileUploadNotification** en **SimulatedDevice**.

1. Druk op **F5**. Beide toepassingen moeten worden gestart. U ziet Hallo uploaden is voltooid in één console-app en Hallo upload-melding is ontvangen door Hallo andere console-app. U kunt Hallo [Azure-portal] of Visual Studio Server Explorer toocheck op Hallo aanwezigheid van Hallo geüpload bestand in uw Azure Storage-account.

    ![][50]

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie hebt u geleerd hoe toouse Hallo bestand mogelijkheden van IoT-Hub toosimplify bestand van apparaten uploadt uploaden. Scenario's en tooexplore IoT hub-functies kunt u doorgaan met de Hallo artikelen te volgen:

* [Een iothub via een programma maken][lnk-create-hub]
* [Inleiding tooC SDK][lnk-c-sdk]
* [Azure IoT SDK 's][lnk-sdks]

toofurther verkennen Hallo-mogelijkheden van IoT Hub, Zie:

* [Een apparaat simuleren met IoT rand][lnk-iotedge]

<!-- Images. -->

[50]: ./media/iot-hub-csharp-csharp-file-upload/run-apps1.png
[1]: ./media/iot-hub-csharp-csharp-file-upload/image-properties.png
[2]: ./media/iot-hub-csharp-csharp-file-upload/file-upload-project-csharp1.png

<!-- Links -->

[Azure-portal]: https://portal.azure.com/

[Azure IoT Developer Center]: http://www.azure.com/develop/iot

[afhandeling van tijdelijke fout]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[Azure IoT service SDK NuGet-pakket]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-windows-iot-edge-simulated-device.md
