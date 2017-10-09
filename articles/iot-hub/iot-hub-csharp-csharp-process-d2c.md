---
title: aaaProcess Azure IoT Hub apparaat-naar-cloud-berichten met behulp van routes (.Net) | Microsoft Docs
description: Hoe berichten tooprocess IoT Hub apparaat-naar-cloud-berichten met behulp van regels voor het doorsturen en aangepaste eindpunten toodispatch tooother back-end-services.
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 5177bac9-722f-47ef-8a14-b201142ba4bc
ms.service: iot-hub
ms.devlang: csharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: c1dd5be04ca30c65af2be466ba6c8c1858333154
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="process-iot-hub-device-to-cloud-messages-using-routes-net"></a>Verwerken van Iothub apparaat-naar-cloud-berichten met behulp van routes (.NET)

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

Deze zelfstudie bouwt voort op Hallo [aan de slag met IoT Hub] zelfstudie. Hallo-zelfstudie:

* Ziet u hoe de apparaat-naar-cloud-berichten toodispatch toouse routering regels in een eenvoudig en gebaseerd op configuratie-hulpprogramma.
* Ziet u hoe tooisolate interactieve berichten waarvoor onmiddellijke actie van de oplossing Hallo back-end voor verdere verwerking. Een apparaat kan bijvoorbeeld een waarschuwing weergegeven dat activeert een ticket in een CRM-systeem invoegen verzenden. Daarentegen feed gegevenspunt berichten, zoals temperatuur telemetrie, in een analyse-engine.

Aan het einde van de Hallo van deze zelfstudie, moet u drie console .NET-toepassingen uitvoeren:

* **SimulatedDevice**, een aangepaste versie van het Hallo-app gemaakt in Hallo [aan de slag met IoT Hub] zelfstudie verzendt gegevenspunt apparaat-naar-cloud-berichten per seconde en interactieve apparaat-naar-cloud met berichten voor elke 10 seconden.
* **ReadDeviceToCloudMessages** dat geeft niet-kritieke telemetrie verzonden door de app op uw apparaat Hallo.
* **ReadCriticalQueue** ongedaan wachtrijen kritieke Hallo-berichten verzonden door de app op uw apparaat van een Service Bus-wachtrij. Deze wachtrij is aangesloten toohello IoT-hub.

> [!NOTE]
> IoT Hub heeft ondersteuning voor veel apparaatplatforms en talen, waaronder C, Java en JavaScript SDK. toolearn hoe tooreplace Hallo gesimuleerd apparaat in deze zelfstudie met een fysiek apparaat, raadpleegt u Hallo [Azure IoT Developer Center].

toocomplete in deze zelfstudie, moet u hello te volgen:

* Visual Studio 2015 of Visual Studio 2017.
* Een actief Azure-account. <br/>Als u geen account hebt, kunt u een [gratis account](https://azure.microsoft.com/free/) binnen een paar minuten.

Er is enige basiskennis van [Azure Storage] en [Azure Service Bus].

## <a name="send-interactive-messages"></a>Interactieve berichten verzenden

Hallo apparaat app die u hebt gemaakt in Hallo wijzigen [aan de slag met IoT Hub] zelfstudie toooccasionally interactieve berichten verzenden.

In Visual Studio in Hallo **SimulatedDevice** project, vervang Hallo `SendDeviceToCloudMessagesAsync` methode Hello code te volgen:

```csharp
private static async void SendDeviceToCloudMessagesAsync()
{
    double minTemperature = 20;
    double minHumidity = 60;
    Random rand = new Random();

    while (true)
    {
        double currentTemperature = minTemperature + rand.NextDouble() * 15;
        double currentHumidity = minHumidity + rand.NextDouble() * 20;

        var telemetryDataPoint = new
        {
            deviceId = "myFirstDevice",
            temperature = currentTemperature,
            humidity = currentHumidity
        };
        var messageString = JsonConvert.SerializeObject(telemetryDataPoint);
        string levelValue;

        if (rand.NextDouble() > 0.7)
        {
            messageString = "This is a critical message";
            levelValue = "critical";
        }
        else
        {
            levelValue = "normal";
        }
        
        var message = new Message(Encoding.ASCII.GetBytes(messageString));
        message.Properties.Add("level", levelValue);
        
        await deviceClient.SendEventAsync(message);
        Console.WriteLine("{0} > Sent message: {1}", DateTime.Now, messageString);

        await Task.Delay(1000);
    }
}
```

Met deze methode wordt willekeurig Hallo eigenschap `"level": "critical"` toomessages verzonden door het Hallo apparaat simuleert een bericht dat directe actie is vereist door Hallo oplossing voor back-end. Hallo apparaattoepassing geeft deze informatie in de eigenschappen van Hallo-bericht, in plaats van in de hoofdtekst van Hallo-bericht, zodat deze IoT-Hub Hallo-bericht toohello juiste berichtenbestemming versturen kunt.

> [!NOTE]
> U kunt bericht eigenschappen tooroute berichten gebruiken voor verschillende scenario's, met inbegrip van koude pad verwerken bovendien toohello hot pad voorbeeld hier weergegeven.

> [!NOTE]
> Deze zelfstudie implementeert voor Hallo mogelijk te houden van eenvoud, niet een beleid voor opnieuw proberen. In productiecode moet u een beleid voor opnieuw proberen zoals exponentieel uitstel, zoals voorgesteld in de MSDN-artikel Hallo implementeren [afhandeling van tijdelijke fout].

## <a name="route-messages-tooa-queue-in-your-iot-hub"></a>Route berichten tooa wachtrij in uw IoT-hub

In deze sectie doet u het volgende:

* Een Service Bus-wachtrij maken.
* Hiermee sluit u het tooyour IoT-hub.
* Configureer uw IoT hub toosend berichten toohello wachtrij op basis van Hallo aanwezigheid van een eigenschap van het Hallo-bericht.

Zie voor meer informatie over hoe tooprocess van van Service Bus-wachtrijen berichten [aan de slag met wachtrijen][Service Bus queue].

1. Een Service Bus-wachtrij maakt, zoals beschreven in [aan de slag met wachtrijen][Service Bus queue]. Hallo wachtrij moet Hallo hetzelfde abonnement en dezelfde regio bevinden als uw IoT-hub. Maak een notitie van Hallo naamruimte en de wachtrij.

    > [!NOTE]
    > Service Bus-wachtrijen en onderwerpen die worden gebruikt als IoT-hubeindpunten mag geen **sessies** of **detectie van dubbele** ingeschakeld. Als een van deze opties zijn ingeschakeld, Hallo-eindpunt wordt weergegeven als **onbereikbaar** in hello Azure-portal.

2. In Azure-portal hello, opent u uw IoT-hub en klik op **eindpunten**.
    
    ![Eindpunten van IoT-hub][30]

3. In Hallo **eindpunten** blade, klikt u op **toevoegen** op Hallo bovenste tooadd uw wachtrij tooyour IoT-hub. Naam Hallo eindpunt **CriticalQueue** en gebruik Hallo-keuzelijsten tooselect **Service Bus-wachtrij**Hallo Service Bus-naamruimte waarin de wachtrij zich bevindt en de naam van uw wachtrij Hallo. Wanneer u klaar bent, klikt u op **opslaan** Hallo onderaan.
    
    ![Een eindpunt toevoegen][31]
    
4. Klik nu op **Routes** in uw IoT-Hub. Klik op **toevoegen** bovenaan Hallo Hallo blade toocreate een regel voor doorsturen die routeert berichten toohello wachtrij u zojuist hebt toegevoegd. Selecteer **DeviceTelemetry** als Hallo gegevensbron. Voer `level="critical"` als Hallo voorwaarde, en kies Hallo wachtrij die u zojuist hebt toegevoegd als een aangepaste eindpunt als Hallo regel eindpunt routering. Wanneer u klaar bent, klikt u op **opslaan** Hallo onderaan.
    
    ![Toevoegen van een route][32]
    
    Zorg ervoor dat Hallo terugval route is ingesteld, te**ON**. Deze waarde is de standaardconfiguratie Hallo voor een IoT-hub.
    
    ![Route voor terugval][33]

## <a name="read-from-hello-queue-endpoint"></a>Lezen van Hallo wachtrij eindpunt

In deze sectie kunt u Hallo-berichten lezen van Hallo wachtrij eindpunt.

1. Voeg in Visual Studio een Visual C# Classic Windows Desktop-project toohello huidige oplossing met behulp van Hallo **Console-App (.NET Framework)** projectsjabloon. Naam Hallo project **ReadCriticalQueue**.

2. Klik in Solution Explorer met de rechtermuisknop op Hallo **ReadCriticalQueue** project en klik vervolgens op **NuGet-pakketten beheren**. Met deze bewerking wordt Hallo **NuGet Package Manager** venster.

3. Zoeken naar **WindowsAzure.ServiceBus**, klikt u op **installeren**, en accepteer de gebruiksvoorwaarden Hallo. Deze bewerking downloadt, installeert en voegt een verwijzing toohello Azure Service Bus, inclusief alle afhankelijkheden ervan.

4. Voeg de volgende Hallo **met** instructies boven Hallo Hallo **Program.cs** bestand:
   
    ```csharp
    using System.IO;
    using Microsoft.ServiceBus.Messaging;
    ```

5. Voeg regels toohello na Hallo **Main** methode. Vervang de verbindingsreeks Hallo met **luisteren** machtigingen voor Hallo wachtrij:
   
    ```csharp
    Console.WriteLine("Receive critical messages. Ctrl-C tooexit.\n");
    var connectionString = "{service bus listen string}";
    var queueName = "{queue name}";
    
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);

    client.OnMessage(message =>
        {
            Stream stream = message.GetBody<Stream>();
            StreamReader reader = new StreamReader(stream, Encoding.ASCII);
            string s = reader.ReadToEnd();
            Console.WriteLine(String.Format("Message body: {0}", s));
        });
        
    Console.ReadLine();
    ```

## <a name="run-hello-applications"></a>Hallo-toepassingen uitvoeren
U bent nu klaar toorun Hallo toepassingen.

1. In Visual Studio in Solution Explorer met de rechtermuisknop op uw oplossing en selecteer **Opstartprojecten instellen**. Selecteer **meerdere opstartprojecten**, selecteer daarna **Start** als actie voor Hallo Hallo **ReadDeviceToCloudMessages**, **SimulatedDevice**, en **ReadCriticalQueue** projecten.
2. Druk op **F5** toostart Hallo drie console-apps. Hallo **ReadDeviceToCloudMessages** app heeft alleen niet-kritieke berichten van Hallo **SimulatedDevice** toepassings- en Hallo **ReadCriticalQueue** app heeft alleen kritieke berichten.
   
   ![Drie console-apps][50]

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie hebt u geleerd hoe tooreliably apparaat-naar-cloud-berichten verzenden met behulp van Hallo-bericht routeringsfunctionaliteit van IoT Hub.

Hallo [hoe toosend cloud-naar-apparaat met IoT Hub berichten] [ lnk-c2d] ziet u hoe toosend tooyour apparaten uit de back-end van uw oplossing berichten.

Voorbeelden van volledige end-to-end-oplossingen die gebruikmaken van IoT Hub toosee Zie [Azure IoT Suite][lnk-suite].

toolearn meer informatie over het ontwikkelen van oplossingen met IoT Hub, Zie Hallo [Ontwikkelaarshandleiding voor IoT Hub].

Zie toolearn meer informatie over het routeren van berichten van IoT-Hub [berichten verzenden en ontvangen met IoT Hub][lnk-devguide-messaging].

<!-- Images. -->
[50]: ./media/iot-hub-csharp-csharp-process-d2c/run1.png
[30]: ./media/iot-hub-csharp-csharp-process-d2c/click-endpoints.png
[31]: ./media/iot-hub-csharp-csharp-process-d2c/endpoint-creation.png
[32]: ./media/iot-hub-csharp-csharp-process-d2c/route-creation.png
[33]: ./media/iot-hub-csharp-csharp-process-d2c/fallback-route.png

<!-- Links -->
[Service Bus queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[Azure Storage]: https://azure.microsoft.com/documentation/services/storage/
[Azure Service Bus]: https://azure.microsoft.com/documentation/services/service-bus/
[Ontwikkelaarshandleiding voor IoT Hub]: iot-hub-devguide.md
[aan de slag met IoT Hub]: iot-hub-csharp-csharp-getstarted.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
[Azure IoT Developer Center]: https://azure.microsoft.com/develop/iot
[afhandeling van tijdelijke fout]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-c2d]: iot-hub-csharp-csharp-process-d2c.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
