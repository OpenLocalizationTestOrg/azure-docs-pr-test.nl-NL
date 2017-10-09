---
title: aaaCloud-naar-apparaat-berichten met Azure IoT Hub (.NET) | Microsoft Docs
description: Hoe berichten toosend cloud-naar-apparaat tooa apparaat van een Azure IoT hub met hello Azure IoT SDK's voor .NET. U een apparaat app tooreceive cloud-naar-apparaat-berichten wijzigen en wijzigen van een back-endserver voor apps toosend hello cloud-naar-apparaat-berichten.
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: a31c05ed-6ec0-40f3-99ab-8fdd28b1a89a
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.openlocfilehash: f6a7618b164d95c8ddaf28943f244aeeb568217f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="send-messages-from-hello-cloud-tooyour-device-with-iot-hub-net"></a>Berichten verzenden van Hallo cloud tooyour apparaat met IoT Hub (.NET)
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a>Inleiding
Azure IoT Hub is een volledig beheerde service waarmee stabiele en veilige tweerichtingscommunicatie tussen miljoenen apparaten inschakelen en een back-end oplossing. Hallo [aan de slag met IoT Hub] zelfstudie laat zien hoe toocreate een IoT-hub een apparaat-id in het inrichten en code van de app voor een apparaat dat apparaat-naar-cloud-berichten verzendt.

Deze zelfstudie bouwt voort op [aan de slag met IoT Hub]. Hier ziet u hoe aan:

* Verzenden van uw back-end oplossing, cloud-naar-apparaatberichten tooa één apparaat via IoT Hub.
* Cloud-naar-apparaat-berichten op een apparaat ontvangen.
* Aanvragen van uw back-end oplossing, levering bevestiging (*feedback*) voor tooa apparaat van de berichten uit IoT Hub.

U vindt meer informatie over cloud-naar-apparaat-berichten in Hallo [Ontwikkelaarshandleiding voor IoT Hub][IoT Hub developer guide - C2D].

Aan het einde van de Hallo van deze zelfstudie, moet u twee apps voor .NET-console uitvoeren:

* **SimulatedDevice**, een aangepaste versie van het Hallo-app gemaakt in [aan de slag met IoT Hub], die verbinding maakt tooyour IoT-hub en cloud-naar-apparaat-berichten worden ontvangen.
* **SendCloudToDevice**, die een cloud-naar-apparaat bericht toohello apparaattoepassing via IoT Hub verzendt en ontvangt u vervolgens de bevestiging levering.

> [!NOTE]
> IoT-Hub SDK-ondersteuning voor veel apparaatplatforms en talen (inclusief C, Java en Javascript) via heeft [apparaat Azure IoT SDK's]. Voor stapsgewijze instructies voor hoe tooconnect uw apparaat toothis-zelfstudie code en over het algemeen tooAzure IoT Hub zien Hallo [Ontwikkelaarshandleiding voor IoT Hub].
> 
> 

toocomplete in deze zelfstudie, moet u hello te volgen:

* Visual Studio 2015 of Visual Studio 2017
* Een actief Azure-account. (Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)

## <a name="receive-messages-in-hello-device-app"></a>Berichten ontvangen in Hallo apparaattoepassing
In deze sectie bewerkt u Hallo apparaattoepassing u hebt gemaakt in [aan de slag met IoT Hub] tooreceive cloud-naar-apparaat-berichten uit Hallo iothub.

1. In Visual Studio in Hallo **SimulatedDevice** project, het toevoegen van Hallo na methode toohello **programma** klasse.
   
        private static async void ReceiveC2dAsync()
        {
            Console.WriteLine("\nReceiving cloud toodevice messages from service");
            while (true)
            {
                Message receivedMessage = await deviceClient.ReceiveAsync();
                if (receivedMessage == null) continue;
   
                Console.ForegroundColor = ConsoleColor.Yellow;
                Console.WriteLine("Received message: {0}", Encoding.ASCII.GetString(receivedMessage.GetBytes()));
                Console.ResetColor();
   
                await deviceClient.CompleteAsync(receivedMessage);
            }
        }
   
    Hallo `ReceiveAsync` methode retourneert asynchroon ontvangen welkomstbericht op Hallo moment dat deze is ontvangen door het Hallo-apparaat. Deze retourneert *null* na een specifiable time-outperiode (in dit geval de standaard Hallo van één minuut wordt gebruikt). Wanneer Hallo app ontvangt een *null*, toowait op nieuwe berichten moet worden voortgezet. Deze vereiste is Hallo reden voor Hallo `if (receivedMessage == null) continue` regel.
   
    Hallo aanroep te`CompleteAsync()` IoT Hub een melding dat het Hallo-bericht is verwerkt. Hallo-bericht kan veilig worden verwijderd uit Hallo apparaatwachtrij. Als er iets opgetreden die Hallo apparaat-app voltooid Hallo verwerking van het Hallo-bericht, bezorgd IoT-Hub opnieuw. Vervolgens is het belangrijk dat logica in apparaattoepassing Hallo-berichten wordt *idempotent*, zodat de ontvangst van hetzelfde bericht meerdere keren produceert Hallo Hallo hetzelfde resultaat. Een toepassing kan een bericht, hetgeen resulteert in IoT-hub behoud het Hallo-bericht in de wachtrij Hallo voor toekomstige consumptie ook tijdelijk afbreken. Of Hallo toepassing kan een bericht dat het Hallo-bericht permanent verwijderd uit de wachtrij Hallo weigeren. Zie voor meer informatie over de levenscyclus van de cloud-naar-apparaat bericht Hallo Hallo [Ontwikkelaarshandleiding voor IoT Hub][IoT Hub developer guide - C2D].
   
   > [!NOTE]
   > Wanneer u HTTP gebruikt in plaats van MQTT of AMQP als transport, Hallo `ReceiveAsync` methode retourneert onmiddellijk. Hallo ondersteund patroon voor cloud-naar-apparaat-berichten met HTTP is tijdelijk verbonden apparaten controleren voor berichten zelden (minder dan elke 25 minuten). Uitgifte van meer HTTP ontvangt resultaten in IoT Hub bandbreedteregeling Hallo aanvragen. Zie voor meer informatie over Hallo verschillen tussen de protocollen MQTT, AMQP en HTTP-ondersteuning en Iothub beperking Hallo [Ontwikkelaarshandleiding voor IoT Hub][IoT Hub developer guide - C2D].
   > 
   > 
2. Toevoegen van de volgende methode in Hallo Hallo **Main** methode aan vóór Hallo `Console.ReadLine()` regel:
   
        ReceiveC2dAsync();

> [!NOTE]
> Deze zelfstudie implementeert voor de eenvoud mogelijk te houden, niet een beleid voor opnieuw proberen. In productiecode moet u beleid voor opnieuw proberen (zoals exponentieel uitstel), zoals voorgesteld in de MSDN-artikel Hallo implementeren [afhandeling van tijdelijke fout].
> 
> 

## <a name="send-a-cloud-to-device-message"></a>Een cloud naar apparaat verzenden
In deze sectie schrijft u een .NET-consoletoepassing die cloud-naar-apparaatberichten toohello apparaat app verzendt.

1. Maak in Hallo huidige Visual Studio-oplossing een Visual C# bureaublad-App-project met behulp van Hallo **consoletoepassing** projectsjabloon. Naam Hallo project **SendCloudToDevice**.
   
    ![Nieuw project in Visual Studio][20]
2. Klik in Solution Explorer met de rechtermuisknop op het Hallo-oplossing en klik vervolgens op **NuGet-pakketten beheren voor oplossing...** . 
   
    Hiermee Hallo **NuGet-pakketten beheren** venster.
3. Zoeken naar **Microsoft.Azure.Devices**, klikt u op **installeren**, en accepteer de gebruiksvoorwaarden Hallo. 
   
    Dit downloadt, installeert en voegt u een verwijzing toohello [Azure IoT service SDK NuGet-pakket].

4. Voeg de volgende Hallo `using` instructie bovenaan Hallo Hallo **Program.cs** bestand:
   
        using Microsoft.Azure.Devices;
5. Hallo na toohello velden toevoegen **programma** klasse. Vervang de aanduidingswaarde Hallo door Hallo IoT hub-verbindingsreeks uit [aan de slag met IoT Hub]:
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. Hallo na methode toohello toevoegen **programma** klasse:
   
        private async static Task SendCloudToDeviceMessageAsync()
        {
            var commandMessage = new Message(Encoding.ASCII.GetBytes("Cloud toodevice message."));
            await serviceClient.SendAsync("myFirstDevice", commandMessage);
        }
   
    Deze methode verzendt een nieuw bericht cloud-naar-apparaat toohello apparaat met Hallo-ID, `myFirstDevice`. Deze parameter alleen wijzigen als u deze hebt gewijzigd van Hallo die wordt gebruikt bij [aan de slag met IoT Hub].
7. Voeg regels toohello na Hallo **Main** methode:
   
        Console.WriteLine("Send Cloud-to-Device message\n");
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
   
        Console.WriteLine("Press any key toosend a C2D message.");
        Console.ReadLine();
        SendCloudToDeviceMessageAsync().Wait();
        Console.ReadLine();
8. Vanuit Visual Studio met de rechtermuisknop op uw oplossing en selecteer **opstartprojecten instellen...** . Selecteer **meerdere opstartprojecten**, selecteer daarna Hallo **Start** actie voor **ReadDeviceToCloudMessages**, **SimulatedDevice**, en **SendCloudToDevice**.
9. Druk op **F5**. Alle drie de toepassingen moeten worden gestart. Selecteer Hallo **SendCloudToDevice** windows en druk op **Enter**. U ziet het Hallo-bericht ontvangen door Hallo apparaattoepassing.
   
   ![App-ontvangende bericht][21]

## <a name="receive-delivery-feedback"></a>Leveringsfeedback ontvangen
Het is mogelijk toorequest levering (of verlopen) bevestigingen van IoT Hub voor elk bericht cloud-naar-apparaat. Deze optie schakelt Hallo oplossing voor back-end tooeasily kennis opnieuw of compensatie logica. Zie voor meer informatie over de cloud-naar-apparaat feedback Hallo [Ontwikkelaarshandleiding voor IoT Hub][IoT Hub developer guide - C2D].

In deze sectie maakt u Hallo wijzigen **SendCloudToDevice** app toorequest feedback, en deze uit IoT Hub worden ontvangen.

1. In Visual Studio in Hallo **SendCloudToDevice** project, het toevoegen van Hallo na methode toohello **programma** klasse.
   
        private async static void ReceiveFeedbackAsync()
        {
            var feedbackReceiver = serviceClient.GetFeedbackReceiver();
   
            Console.WriteLine("\nReceiving c2d feedback from service");
            while (true)
            {
                var feedbackBatch = await feedbackReceiver.ReceiveAsync();
                if (feedbackBatch == null) continue;
   
                Console.ForegroundColor = ConsoleColor.Yellow;
                Console.WriteLine("Received feedback: {0}", string.Join(", ", feedbackBatch.Records.Select(f => f.StatusCode)));
                Console.ResetColor();
   
                await feedbackReceiver.CompleteAsync(feedbackBatch);
            }
        }
   
    Opmerking: dit patroon ontvangen is dezelfde één gebruikte tooreceive cloud-naar-apparaat berichten van apparaattoepassing Hallo Hallo.
2. Toevoegen van de volgende methode in Hallo Hallo **Main** methode, meteen na Hallo `serviceClient = ServiceClient.CreateFromConnectionString(connectionString)` regel:
   
        ReceiveFeedbackAsync();
3. toorequest feedback voor het leveren van Hallo van uw bericht cloud-naar-apparaat, hebt u toospecify een eigenschap in Hallo **SendCloudToDeviceMessageAsync** methode. Hallo volgt regel, direct na Hallo toevoegen `var commandMessage = new Message(...);` regel:
   
        commandMessage.Ack = DeliveryAcknowledgement.Full;
4. Hallo-apps uitvoeren door te drukken **F5**. Hier ziet u alle drie de toepassingen starten. Selecteer Hallo **SendCloudToDevice** windows en druk op **Enter**. U ziet Hallo-bericht wordt ontvangen door Hallo apparaattoepassing en na enkele seconden, Hallo Feedbackbericht wordt ontvangen door uw **SendCloudToDevice** toepassing.
   
   ![App-ontvangende bericht][22]

> [!NOTE]
> Deze zelfstudie implementeert voor de eenvoud mogelijk te houden, niet een beleid voor opnieuw proberen. In productiecode moet u beleid voor opnieuw proberen (zoals exponentieel uitstel), zoals voorgesteld in de MSDN-artikel Hallo implementeren [afhandeling van tijdelijke fout].
> 
> 

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie hebt u geleerd hoe toosend en cloud-naar-apparaat-berichten ontvangen. 

Voorbeelden van volledige end-to-end-oplossingen die gebruikmaken van IoT Hub toosee Zie [Azure IoT Suite].

toolearn meer informatie over het ontwikkelen van oplossingen met IoT Hub, Zie Hallo [Ontwikkelaarshandleiding voor IoT Hub].

<!-- Images -->
[20]: ./media/iot-hub-csharp-csharp-c2d/create-identity-csharp1.png
[21]: ./media/iot-hub-csharp-csharp-c2d/sendc2d1.png
[22]: ./media/iot-hub-csharp-csharp-c2d/sendc2d2.png

<!-- Links -->

[Azure IoT service SDK NuGet-pakket]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[afhandeling van tijdelijke fout]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md

[Ontwikkelaarshandleiding voor IoT Hub]: iot-hub-devguide.md
[aan de slag met IoT Hub]: iot-hub-csharp-csharp-getstarted.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure IoT Suite]: https://docs.microsoft.com/en-us/azure/iot-suite/
[apparaat Azure IoT SDK's]: iot-hub-devguide-sdks.md