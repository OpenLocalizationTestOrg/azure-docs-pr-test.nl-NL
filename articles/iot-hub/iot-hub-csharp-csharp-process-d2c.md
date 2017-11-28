---
title: Azure IoT Hub apparaat-naar-cloud-berichten met behulp van routes (.Net) | Microsoft Docs
description: Klik hier voor meer informatie over het verwerken van IoT Hub apparaat-naar-cloud-berichten met behulp van regels voor het doorsturen en aangepaste eindpunten verzending van berichten naar andere back-end-services.
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
ms.openlocfilehash: 1d2b52ea005ab520bf294efa603512c00a92ee63
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="process-iot-hub-device-to-cloud-messages-using-routes-net"></a><span data-ttu-id="43131-103">Verwerken van Iothub apparaat-naar-cloud-berichten met behulp van routes (.NET)</span><span class="sxs-lookup"><span data-stu-id="43131-103">Process IoT Hub device-to-cloud messages using routes (.NET)</span></span>

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

<span data-ttu-id="43131-104">Deze zelfstudie bouwt voort op de [aan de slag met IoT Hub] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="43131-104">This tutorial builds on the [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="43131-105">De zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="43131-105">The tutorial:</span></span>

* <span data-ttu-id="43131-106">Laat zien hoe u regels voor doorsturen verzending van apparaat-naar-cloud-berichten in een eenvoudig en gebaseerd op configuratie-hulpprogramma te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="43131-106">Shows you how to use routing rules to dispatch device-to-cloud messages in an easy, configuration-based way.</span></span>
* <span data-ttu-id="43131-107">Laat zien hoe isoleren interactieve berichten die directe actie van de back-end oplossing voor verdere verwerking is vereist.</span><span class="sxs-lookup"><span data-stu-id="43131-107">Illustrates how to isolate interactive messages that require immediate action from the solution back end for further processing.</span></span> <span data-ttu-id="43131-108">Een apparaat kan bijvoorbeeld een waarschuwing weergegeven dat activeert een ticket in een CRM-systeem invoegen verzenden.</span><span class="sxs-lookup"><span data-stu-id="43131-108">For example, a device might send an alarm message that triggers inserting a ticket into a CRM system.</span></span> <span data-ttu-id="43131-109">Daarentegen feed gegevenspunt berichten, zoals temperatuur telemetrie, in een analyse-engine.</span><span class="sxs-lookup"><span data-stu-id="43131-109">In contrast, data-point messages, such as temperature telemetry, feed into an analytics engine.</span></span>

<span data-ttu-id="43131-110">Aan het einde van deze zelfstudie, moet u drie console .NET-toepassingen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="43131-110">At the end of this tutorial, you run three .NET console apps:</span></span>

* <span data-ttu-id="43131-111">**SimulatedDevice**, een aangepaste versie van de app gemaakt in de [aan de slag met IoT Hub] zelfstudie verzendt gegevenspunt apparaat-naar-cloud-berichten per seconde en interactieve apparaat-naar-cloud met berichten voor elke 10 seconden.</span><span class="sxs-lookup"><span data-stu-id="43131-111">**SimulatedDevice**, a modified version of the app created in the [Get started with IoT Hub] tutorial sends data-point device-to-cloud messages every second, and interactive device-to-cloud messages every 10 seconds.</span></span>
* <span data-ttu-id="43131-112">**ReadDeviceToCloudMessages** waarmee de niet-kritieke telemetrie verzonden door de app op uw apparaat worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="43131-112">**ReadDeviceToCloudMessages** that displays the non-critical telemetry sent by your device app.</span></span>
* <span data-ttu-id="43131-113">**ReadCriticalQueue** ongedaan wachtrijen de kritieke berichten is verzonden door uw app voor het apparaat van een Service Bus-wachtrij.</span><span class="sxs-lookup"><span data-stu-id="43131-113">**ReadCriticalQueue** de-queues the critical messages sent by your device app from a Service Bus queue.</span></span> <span data-ttu-id="43131-114">Deze wachtrij is gekoppeld aan de IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="43131-114">This queue is attached to the IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="43131-115">IoT Hub heeft ondersteuning voor veel apparaatplatforms en talen, waaronder C, Java en JavaScript SDK.</span><span class="sxs-lookup"><span data-stu-id="43131-115">IoT Hub has SDK support for many device platforms and languages, including C, Java, and JavaScript.</span></span> <span data-ttu-id="43131-116">Zie voor meer informatie over het gesimuleerde apparaat in deze zelfstudie vervangen door een fysiek apparaat, de [Azure IoT Developer Center].</span><span class="sxs-lookup"><span data-stu-id="43131-116">To learn how to replace the simulated device in this tutorial with a physical device, see the [Azure IoT Developer Center].</span></span>

<span data-ttu-id="43131-117">Voor het voltooien van deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="43131-117">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="43131-118">Visual Studio 2015 of Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="43131-118">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="43131-119">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="43131-119">An active Azure account.</span></span> <br/><span data-ttu-id="43131-120">Als u geen account hebt, kunt u een [gratis account](https://azure.microsoft.com/free/) binnen een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="43131-120">If you don't have an account, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

<span data-ttu-id="43131-121">Er is enige basiskennis van [Azure Storage] en [Azure Service Bus].</span><span class="sxs-lookup"><span data-stu-id="43131-121">You should have some basic knowledge of [Azure Storage] and [Azure Service Bus].</span></span>

## <a name="send-interactive-messages"></a><span data-ttu-id="43131-122">Interactieve berichten verzenden</span><span class="sxs-lookup"><span data-stu-id="43131-122">Send interactive messages</span></span>

<span data-ttu-id="43131-123">Wijzigen van de apparaat-app die u hebt gemaakt in de [aan de slag met IoT Hub] zelfstudie af en interactieve om berichten te verzenden.</span><span class="sxs-lookup"><span data-stu-id="43131-123">Modify the device app you created in the [Get started with IoT Hub] tutorial to occasionally send interactive messages.</span></span>

<span data-ttu-id="43131-124">In Visual Studio in de **SimulatedDevice** project, vervangen door de `SendDeviceToCloudMessagesAsync` methode met de volgende code:</span><span class="sxs-lookup"><span data-stu-id="43131-124">In Visual Studio, in the **SimulatedDevice** project, replace the `SendDeviceToCloudMessagesAsync` method with the following code:</span></span>

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

<span data-ttu-id="43131-125">Deze methode wordt willekeurig toegevoegd voor de eigenschap `"level": "critical"` op berichten die door het apparaat verzonden, die een bericht dat directe actie is vereist door de oplossing voor back-end simuleert.</span><span class="sxs-lookup"><span data-stu-id="43131-125">This method randomly adds the property `"level": "critical"` to messages sent by the device, which simulates a message that requires immediate action by the solution back-end.</span></span> <span data-ttu-id="43131-126">De apparaattoepassing geeft deze informatie in de berichteigenschappen in plaats van in de hoofdtekst van het bericht, zodat deze IoT Hub het bericht naar de juiste bestemming sturen kan.</span><span class="sxs-lookup"><span data-stu-id="43131-126">The device app passes this information in the message properties, instead of in the message body, so that IoT Hub can route the message to the proper message destination.</span></span>

> [!NOTE]
> <span data-ttu-id="43131-127">U kunt de berichteigenschappen om berichten te routeren voor verschillende scenario's, inclusief de verwerking van koude pad, naast het hot pad voorbeeld dat hier wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="43131-127">You can use message properties to route messages for various scenarios including cold-path processing, in addition to the hot-path example shown here.</span></span>

> [!NOTE]
> <span data-ttu-id="43131-128">Omwille van de eenvoud in deze zelfstudie niet geïmplementeerd voor een beleid voor opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="43131-128">For the sake of simplicity, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="43131-129">In productiecode moet u een beleid voor opnieuw proberen zoals exponentieel uitstel, zoals voorgesteld in het MSDN-artikel implementeren [afhandeling van tijdelijke fout].</span><span class="sxs-lookup"><span data-stu-id="43131-129">In production code, you should implement a retry policy such as exponential backoff, as suggested in the MSDN article [Transient Fault Handling].</span></span>

## <a name="route-messages-to-a-queue-in-your-iot-hub"></a><span data-ttu-id="43131-130">Routeren van berichten aan een wachtrij in uw IoT-hub</span><span class="sxs-lookup"><span data-stu-id="43131-130">Route messages to a queue in your IoT hub</span></span>

<span data-ttu-id="43131-131">In deze sectie doet u het volgende:</span><span class="sxs-lookup"><span data-stu-id="43131-131">In this section, you:</span></span>

* <span data-ttu-id="43131-132">Een Service Bus-wachtrij maken.</span><span class="sxs-lookup"><span data-stu-id="43131-132">Create a Service Bus queue.</span></span>
* <span data-ttu-id="43131-133">Verbindt dit met uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="43131-133">Connect it to your IoT hub.</span></span>
* <span data-ttu-id="43131-134">Configureer uw IoT-hub om berichten te verzenden naar de wachtrij op basis van de aanwezigheid van een eigenschap van het bericht.</span><span class="sxs-lookup"><span data-stu-id="43131-134">Configure your IoT hub to send messages to the queue based on the presence of a property on the message.</span></span>

<span data-ttu-id="43131-135">Zie voor meer informatie over het verwerken van berichten van Service Bus-wachtrijen [aan de slag met wachtrijen][Service Bus queue].</span><span class="sxs-lookup"><span data-stu-id="43131-135">For more information about how to process messages from Service Bus queues, see [Get started with queues][Service Bus queue].</span></span>

1. <span data-ttu-id="43131-136">Een Service Bus-wachtrij maakt, zoals beschreven in [aan de slag met wachtrijen][Service Bus queue].</span><span class="sxs-lookup"><span data-stu-id="43131-136">Create a Service Bus queue as described in [Get started with queues][Service Bus queue].</span></span> <span data-ttu-id="43131-137">De wachtrij moet zich in hetzelfde abonnement en dezelfde regio als uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="43131-137">The queue must be in the same subscription and region as your IoT hub.</span></span> <span data-ttu-id="43131-138">Noteer de naam van de naamruimte en de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="43131-138">Make a note of the namespace and queue name.</span></span>

    > [!NOTE]
    > <span data-ttu-id="43131-139">Service Bus-wachtrijen en onderwerpen die worden gebruikt als IoT-hubeindpunten mag geen **sessies** of **detectie van dubbele** ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="43131-139">Service Bus queues and topics used as IoT Hub endpoints must not have **Sessions** or **Duplicate Detection** enabled.</span></span> <span data-ttu-id="43131-140">Als een van deze opties zijn ingeschakeld, het eindpunt wordt weergegeven als **onbereikbaar** in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="43131-140">If either of those options are enabled, the endpoint appears as **Unreachable** in the Azure portal.</span></span>

2. <span data-ttu-id="43131-141">Open uw IoT-hub in de Azure-portal en klikt u op **eindpunten**.</span><span class="sxs-lookup"><span data-stu-id="43131-141">In the Azure portal, open your IoT hub and click **Endpoints**.</span></span>
    
    ![Eindpunten van IoT-hub][30]

3. <span data-ttu-id="43131-143">In de **eindpunten** blade, klikt u op **toevoegen** boven uw wachtrij toevoegen aan uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="43131-143">In the **Endpoints** blade, click **Add** at the top to add your queue to your IoT hub.</span></span> <span data-ttu-id="43131-144">Naam van het eindpunt **CriticalQueue** en selecteer met de vervolgkeuzelijsten **Service Bus-wachtrij**, de Service Bus-naamruimte waarin de wachtrij zich bevindt en de naam van de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="43131-144">Name the endpoint **CriticalQueue** and use the drop-downs to select **Service Bus queue**, the Service Bus namespace in which your queue resides, and the name of your queue.</span></span> <span data-ttu-id="43131-145">Wanneer u klaar bent, klikt u op **opslaan** onderaan.</span><span class="sxs-lookup"><span data-stu-id="43131-145">When you are done, click **Save** at the bottom.</span></span>
    
    ![Een eindpunt toevoegen][31]
    
4. <span data-ttu-id="43131-147">Klik nu op **Routes** in uw IoT-Hub.</span><span class="sxs-lookup"><span data-stu-id="43131-147">Now click **Routes** in your IoT Hub.</span></span> <span data-ttu-id="43131-148">Klik op **toevoegen** boven aan de blade voor het maken van een regel voor doorsturen waarmee berichten worden doorgestuurd naar de wachtrij die u zojuist hebt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="43131-148">Click **Add** at the top of the blade to create a routing rule that routes messages to the queue you just added.</span></span> <span data-ttu-id="43131-149">Selecteer **DeviceTelemetry** als de bron van gegevens.</span><span class="sxs-lookup"><span data-stu-id="43131-149">Select **DeviceTelemetry** as the source of data.</span></span> <span data-ttu-id="43131-150">Voer `level="critical"` als de voorwaarde, en kies de wachtrij die u zojuist hebt toegevoegd als een aangepaste eindpunt als de routering eindpunt van de regel.</span><span class="sxs-lookup"><span data-stu-id="43131-150">Enter `level="critical"` as the condition, and choose the queue you just added as a custom endpoint as the routing rule endpoint.</span></span> <span data-ttu-id="43131-151">Wanneer u klaar bent, klikt u op **opslaan** onderaan.</span><span class="sxs-lookup"><span data-stu-id="43131-151">When you are done, click **Save** at the bottom.</span></span>
    
    ![Toevoegen van een route][32]
    
    <span data-ttu-id="43131-153">Zorg ervoor dat de terugval route is ingesteld op **ON**.</span><span class="sxs-lookup"><span data-stu-id="43131-153">Make sure the fallback route is set to **ON**.</span></span> <span data-ttu-id="43131-154">Deze waarde is de standaardconfiguratie voor een IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="43131-154">This value is the default configuration for an IoT hub.</span></span>
    
    ![Route voor terugval][33]

## <a name="read-from-the-queue-endpoint"></a><span data-ttu-id="43131-156">Lezen van het eindpunt van de wachtrij</span><span class="sxs-lookup"><span data-stu-id="43131-156">Read from the queue endpoint</span></span>

<span data-ttu-id="43131-157">In deze sectie kunt u de berichten van het eindpunt van de wachtrij lezen.</span><span class="sxs-lookup"><span data-stu-id="43131-157">In this section, you read the messages from the queue endpoint.</span></span>

1. <span data-ttu-id="43131-158">Voeg in Visual Studio een Visual C# Classic Windows Desktop-project toe aan de huidige oplossing met behulp van de projectsjabloon **Console App (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="43131-158">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution, by using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="43131-159">Noem het project **ReadCriticalQueue**.</span><span class="sxs-lookup"><span data-stu-id="43131-159">Name the project **ReadCriticalQueue**.</span></span>

2. <span data-ttu-id="43131-160">Klik in Solution Explorer met de rechtermuisknop op de **ReadCriticalQueue** project en klik vervolgens op **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="43131-160">In Solution Explorer, right-click the **ReadCriticalQueue** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="43131-161">Met deze bewerking wordt de **NuGet Package Manager** venster.</span><span class="sxs-lookup"><span data-stu-id="43131-161">This operation displays the **NuGet Package Manager** window.</span></span>

3. <span data-ttu-id="43131-162">Zoeken naar **WindowsAzure.ServiceBus**, klikt u op **installeren**, en accepteer de gebruiksvoorwaarden.</span><span class="sxs-lookup"><span data-stu-id="43131-162">Search for **WindowsAzure.ServiceBus**, click **Install**, and accept the terms of use.</span></span> <span data-ttu-id="43131-163">Deze bewerking downloadt, installeert en voegt een verwijzing naar de Azure Service Bus, inclusief alle afhankelijkheden ervan.</span><span class="sxs-lookup"><span data-stu-id="43131-163">This operation downloads, installs, and adds a reference to the Azure Service Bus, with all its dependencies.</span></span>

4. <span data-ttu-id="43131-164">Voeg de volgende **met** instructies aan het begin van de **Program.cs** bestand:</span><span class="sxs-lookup"><span data-stu-id="43131-164">Add the following **using** statements at the top of the **Program.cs** file:</span></span>
   
    ```csharp
    using System.IO;
    using Microsoft.ServiceBus.Messaging;
    ```

5. <span data-ttu-id="43131-165">Voeg de volgende regels voor de **Main** methode.</span><span class="sxs-lookup"><span data-stu-id="43131-165">Finally, add the following lines to the **Main** method.</span></span> <span data-ttu-id="43131-166">Vervang de verbindingsreeks met **luisteren** machtigingen voor de wachtrij:</span><span class="sxs-lookup"><span data-stu-id="43131-166">Substitute the connection string with **Listen** permissions for the queue:</span></span>
   
    ```csharp
    Console.WriteLine("Receive critical messages. Ctrl-C to exit.\n");
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

## <a name="run-the-applications"></a><span data-ttu-id="43131-167">De toepassingen uitvoeren</span><span class="sxs-lookup"><span data-stu-id="43131-167">Run the applications</span></span>
<span data-ttu-id="43131-168">U kunt nu de toepassingen gaan uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="43131-168">Now you are ready to run the applications.</span></span>

1. <span data-ttu-id="43131-169">In Visual Studio in Solution Explorer met de rechtermuisknop op uw oplossing en selecteer **Opstartprojecten instellen**.</span><span class="sxs-lookup"><span data-stu-id="43131-169">In Visual Studio, in Solution Explorer, right-click your solution and select **Set StartUp Projects**.</span></span> <span data-ttu-id="43131-170">Selecteer **meerdere opstartprojecten**, selecteer daarna **Start** als de actie voor de **ReadDeviceToCloudMessages**, **SimulatedDevice**, en **ReadCriticalQueue** projecten.</span><span class="sxs-lookup"><span data-stu-id="43131-170">Select **Multiple startup projects**, then select **Start** as the action for the **ReadDeviceToCloudMessages**, **SimulatedDevice**, and **ReadCriticalQueue** projects.</span></span>
2. <span data-ttu-id="43131-171">Druk op **F5** starten die de drie console apps.</span><span class="sxs-lookup"><span data-stu-id="43131-171">Press **F5** to start the three console apps.</span></span> <span data-ttu-id="43131-172">De **ReadDeviceToCloudMessages** app heeft alleen niet-kritieke berichten van de **SimulatedDevice** toepassing, en de **ReadCriticalQueue** app heeft alleen kritieke berichten.</span><span class="sxs-lookup"><span data-stu-id="43131-172">The **ReadDeviceToCloudMessages** app has only non-critical messages sent from the **SimulatedDevice** application, and the **ReadCriticalQueue** app has only critical messages.</span></span>
   
   ![Drie console-apps][50]

## <a name="next-steps"></a><span data-ttu-id="43131-174">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="43131-174">Next steps</span></span>
<span data-ttu-id="43131-175">In deze zelfstudie hebt u geleerd hoe betrouwbaar apparaat-naar-cloud-berichten verzenden met behulp van de berichtroutering van IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="43131-175">In this tutorial, you learned how to reliably dispatch device-to-cloud messages by using the message routing functionality of IoT Hub.</span></span>

<span data-ttu-id="43131-176">De [het verzenden van berichten van de cloud-naar-apparaat met IoT Hub] [ lnk-c2d] ziet u hoe u berichten verzenden naar uw apparaten vanuit de back-end van uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="43131-176">The [How to send cloud-to-device messages with IoT Hub][lnk-c2d] shows you how to send messages to your devices from your solution back end.</span></span>

<span data-ttu-id="43131-177">Zie voor voorbeelden van volledige end-to-end-oplossingen die gebruikmaken van IoT Hub [Azure IoT Suite][lnk-suite].</span><span class="sxs-lookup"><span data-stu-id="43131-177">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite][lnk-suite].</span></span>

<span data-ttu-id="43131-178">Zie voor meer informatie over het ontwikkelen van oplossingen met IoT Hub, de [Ontwikkelaarshandleiding voor IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="43131-178">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span></span>

<span data-ttu-id="43131-179">Zie voor meer informatie over het routeren van berichten van IoT-Hub, [berichten verzenden en ontvangen met IoT Hub][lnk-devguide-messaging].</span><span class="sxs-lookup"><span data-stu-id="43131-179">To learn more about message routing in IoT Hub, see [Send and receive messages with IoT Hub][lnk-devguide-messaging].</span></span>

<!-- Images. -->
[50]: ./media/iot-hub-csharp-csharp-process-d2c/run1.png
[30]: ./media/iot-hub-csharp-csharp-process-d2c/click-endpoints.png
[31]: ./media/iot-hub-csharp-csharp-process-d2c/endpoint-creation.png
[32]: ./media/iot-hub-csharp-csharp-process-d2c/route-creation.png
[33]: ./media/iot-hub-csharp-csharp-process-d2c/fallback-route.png

<!-- Links -->
[Service Bus queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
<span data-ttu-id="43131-180">[Azure Storage]: https://azure.microsoft.com/documentation/services/storage/</span><span class="sxs-lookup"><span data-stu-id="43131-180">[Azure Storage]: https://azure.microsoft.com/documentation/services/storage/</span></span>
<span data-ttu-id="43131-181">[Azure Service Bus]: https://azure.microsoft.com/documentation/services/service-bus/</span><span class="sxs-lookup"><span data-stu-id="43131-181">[Azure Service Bus]: https://azure.microsoft.com/documentation/services/service-bus/</span></span>
<span data-ttu-id="43131-182">[Ontwikkelaarshandleiding voor IoT Hub]: iot-hub-devguide.md</span><span class="sxs-lookup"><span data-stu-id="43131-182">[IoT Hub developer guide]: iot-hub-devguide.md</span></span>
<span data-ttu-id="43131-183">[aan de slag met IoT Hub]: iot-hub-csharp-csharp-getstarted.md</span><span class="sxs-lookup"><span data-stu-id="43131-183">[Get started with IoT Hub]: iot-hub-csharp-csharp-getstarted.md</span></span>
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
<span data-ttu-id="43131-184">[Azure IoT Developer Center]: https://azure.microsoft.com/develop/iot</span><span class="sxs-lookup"><span data-stu-id="43131-184">[Azure IoT Developer Center]: https://azure.microsoft.com/develop/iot</span></span>
<span data-ttu-id="43131-185">[afhandeling van tijdelijke fout]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span><span class="sxs-lookup"><span data-stu-id="43131-185">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span></span>
[lnk-c2d]: iot-hub-csharp-csharp-process-d2c.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
