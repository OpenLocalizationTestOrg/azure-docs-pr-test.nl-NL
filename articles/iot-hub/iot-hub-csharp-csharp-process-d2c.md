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
# <a name="process-iot-hub-device-to-cloud-messages-using-routes-net"></a><span data-ttu-id="c7a5e-103">Verwerken van Iothub apparaat-naar-cloud-berichten met behulp van routes (.NET)</span><span class="sxs-lookup"><span data-stu-id="c7a5e-103">Process IoT Hub device-to-cloud messages using routes (.NET)</span></span>

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

<span data-ttu-id="c7a5e-104">Deze zelfstudie bouwt voort op Hallo [aan de slag met IoT Hub] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-104">This tutorial builds on hello [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="c7a5e-105">Hallo-zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="c7a5e-105">hello tutorial:</span></span>

* <span data-ttu-id="c7a5e-106">Ziet u hoe de apparaat-naar-cloud-berichten toodispatch toouse routering regels in een eenvoudig en gebaseerd op configuratie-hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-106">Shows you how toouse routing rules toodispatch device-to-cloud messages in an easy, configuration-based way.</span></span>
* <span data-ttu-id="c7a5e-107">Ziet u hoe tooisolate interactieve berichten waarvoor onmiddellijke actie van de oplossing Hallo back-end voor verdere verwerking.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-107">Illustrates how tooisolate interactive messages that require immediate action from hello solution back end for further processing.</span></span> <span data-ttu-id="c7a5e-108">Een apparaat kan bijvoorbeeld een waarschuwing weergegeven dat activeert een ticket in een CRM-systeem invoegen verzenden.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-108">For example, a device might send an alarm message that triggers inserting a ticket into a CRM system.</span></span> <span data-ttu-id="c7a5e-109">Daarentegen feed gegevenspunt berichten, zoals temperatuur telemetrie, in een analyse-engine.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-109">In contrast, data-point messages, such as temperature telemetry, feed into an analytics engine.</span></span>

<span data-ttu-id="c7a5e-110">Aan het einde van de Hallo van deze zelfstudie, moet u drie console .NET-toepassingen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="c7a5e-110">At hello end of this tutorial, you run three .NET console apps:</span></span>

* <span data-ttu-id="c7a5e-111">**SimulatedDevice**, een aangepaste versie van het Hallo-app gemaakt in Hallo [aan de slag met IoT Hub] zelfstudie verzendt gegevenspunt apparaat-naar-cloud-berichten per seconde en interactieve apparaat-naar-cloud met berichten voor elke 10 seconden.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-111">**SimulatedDevice**, a modified version of hello app created in hello [Get started with IoT Hub] tutorial sends data-point device-to-cloud messages every second, and interactive device-to-cloud messages every 10 seconds.</span></span>
* <span data-ttu-id="c7a5e-112">**ReadDeviceToCloudMessages** dat geeft niet-kritieke telemetrie verzonden door de app op uw apparaat Hallo.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-112">**ReadDeviceToCloudMessages** that displays hello non-critical telemetry sent by your device app.</span></span>
* <span data-ttu-id="c7a5e-113">**ReadCriticalQueue** ongedaan wachtrijen kritieke Hallo-berichten verzonden door de app op uw apparaat van een Service Bus-wachtrij.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-113">**ReadCriticalQueue** de-queues hello critical messages sent by your device app from a Service Bus queue.</span></span> <span data-ttu-id="c7a5e-114">Deze wachtrij is aangesloten toohello IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-114">This queue is attached toohello IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="c7a5e-115">IoT Hub heeft ondersteuning voor veel apparaatplatforms en talen, waaronder C, Java en JavaScript SDK.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-115">IoT Hub has SDK support for many device platforms and languages, including C, Java, and JavaScript.</span></span> <span data-ttu-id="c7a5e-116">toolearn hoe tooreplace Hallo gesimuleerd apparaat in deze zelfstudie met een fysiek apparaat, raadpleegt u Hallo [Azure IoT Developer Center].</span><span class="sxs-lookup"><span data-stu-id="c7a5e-116">toolearn how tooreplace hello simulated device in this tutorial with a physical device, see hello [Azure IoT Developer Center].</span></span>

<span data-ttu-id="c7a5e-117">toocomplete in deze zelfstudie, moet u hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="c7a5e-117">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="c7a5e-118">Visual Studio 2015 of Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-118">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="c7a5e-119">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-119">An active Azure account.</span></span> <br/><span data-ttu-id="c7a5e-120">Als u geen account hebt, kunt u een [gratis account](https://azure.microsoft.com/free/) binnen een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-120">If you don't have an account, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

<span data-ttu-id="c7a5e-121">Er is enige basiskennis van [Azure Storage] en [Azure Service Bus].</span><span class="sxs-lookup"><span data-stu-id="c7a5e-121">You should have some basic knowledge of [Azure Storage] and [Azure Service Bus].</span></span>

## <a name="send-interactive-messages"></a><span data-ttu-id="c7a5e-122">Interactieve berichten verzenden</span><span class="sxs-lookup"><span data-stu-id="c7a5e-122">Send interactive messages</span></span>

<span data-ttu-id="c7a5e-123">Hallo apparaat app die u hebt gemaakt in Hallo wijzigen [aan de slag met IoT Hub] zelfstudie toooccasionally interactieve berichten verzenden.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-123">Modify hello device app you created in hello [Get started with IoT Hub] tutorial toooccasionally send interactive messages.</span></span>

<span data-ttu-id="c7a5e-124">In Visual Studio in Hallo **SimulatedDevice** project, vervang Hallo `SendDeviceToCloudMessagesAsync` methode Hello code te volgen:</span><span class="sxs-lookup"><span data-stu-id="c7a5e-124">In Visual Studio, in hello **SimulatedDevice** project, replace hello `SendDeviceToCloudMessagesAsync` method with hello following code:</span></span>

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

<span data-ttu-id="c7a5e-125">Met deze methode wordt willekeurig Hallo eigenschap `"level": "critical"` toomessages verzonden door het Hallo apparaat simuleert een bericht dat directe actie is vereist door Hallo oplossing voor back-end.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-125">This method randomly adds hello property `"level": "critical"` toomessages sent by hello device, which simulates a message that requires immediate action by hello solution back-end.</span></span> <span data-ttu-id="c7a5e-126">Hallo apparaattoepassing geeft deze informatie in de eigenschappen van Hallo-bericht, in plaats van in de hoofdtekst van Hallo-bericht, zodat deze IoT-Hub Hallo-bericht toohello juiste berichtenbestemming versturen kunt.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-126">hello device app passes this information in hello message properties, instead of in hello message body, so that IoT Hub can route hello message toohello proper message destination.</span></span>

> [!NOTE]
> <span data-ttu-id="c7a5e-127">U kunt bericht eigenschappen tooroute berichten gebruiken voor verschillende scenario's, met inbegrip van koude pad verwerken bovendien toohello hot pad voorbeeld hier weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-127">You can use message properties tooroute messages for various scenarios including cold-path processing, in addition toohello hot-path example shown here.</span></span>

> [!NOTE]
> <span data-ttu-id="c7a5e-128">Deze zelfstudie implementeert voor Hallo mogelijk te houden van eenvoud, niet een beleid voor opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-128">For hello sake of simplicity, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="c7a5e-129">In productiecode moet u een beleid voor opnieuw proberen zoals exponentieel uitstel, zoals voorgesteld in de MSDN-artikel Hallo implementeren [afhandeling van tijdelijke fout].</span><span class="sxs-lookup"><span data-stu-id="c7a5e-129">In production code, you should implement a retry policy such as exponential backoff, as suggested in hello MSDN article [Transient Fault Handling].</span></span>

## <a name="route-messages-tooa-queue-in-your-iot-hub"></a><span data-ttu-id="c7a5e-130">Route berichten tooa wachtrij in uw IoT-hub</span><span class="sxs-lookup"><span data-stu-id="c7a5e-130">Route messages tooa queue in your IoT hub</span></span>

<span data-ttu-id="c7a5e-131">In deze sectie doet u het volgende:</span><span class="sxs-lookup"><span data-stu-id="c7a5e-131">In this section, you:</span></span>

* <span data-ttu-id="c7a5e-132">Een Service Bus-wachtrij maken.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-132">Create a Service Bus queue.</span></span>
* <span data-ttu-id="c7a5e-133">Hiermee sluit u het tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-133">Connect it tooyour IoT hub.</span></span>
* <span data-ttu-id="c7a5e-134">Configureer uw IoT hub toosend berichten toohello wachtrij op basis van Hallo aanwezigheid van een eigenschap van het Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-134">Configure your IoT hub toosend messages toohello queue based on hello presence of a property on hello message.</span></span>

<span data-ttu-id="c7a5e-135">Zie voor meer informatie over hoe tooprocess van van Service Bus-wachtrijen berichten [aan de slag met wachtrijen][Service Bus queue].</span><span class="sxs-lookup"><span data-stu-id="c7a5e-135">For more information about how tooprocess messages from Service Bus queues, see [Get started with queues][Service Bus queue].</span></span>

1. <span data-ttu-id="c7a5e-136">Een Service Bus-wachtrij maakt, zoals beschreven in [aan de slag met wachtrijen][Service Bus queue].</span><span class="sxs-lookup"><span data-stu-id="c7a5e-136">Create a Service Bus queue as described in [Get started with queues][Service Bus queue].</span></span> <span data-ttu-id="c7a5e-137">Hallo wachtrij moet Hallo hetzelfde abonnement en dezelfde regio bevinden als uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-137">hello queue must be in hello same subscription and region as your IoT hub.</span></span> <span data-ttu-id="c7a5e-138">Maak een notitie van Hallo naamruimte en de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-138">Make a note of hello namespace and queue name.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c7a5e-139">Service Bus-wachtrijen en onderwerpen die worden gebruikt als IoT-hubeindpunten mag geen **sessies** of **detectie van dubbele** ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-139">Service Bus queues and topics used as IoT Hub endpoints must not have **Sessions** or **Duplicate Detection** enabled.</span></span> <span data-ttu-id="c7a5e-140">Als een van deze opties zijn ingeschakeld, Hallo-eindpunt wordt weergegeven als **onbereikbaar** in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-140">If either of those options are enabled, hello endpoint appears as **Unreachable** in hello Azure portal.</span></span>

2. <span data-ttu-id="c7a5e-141">In Azure-portal hello, opent u uw IoT-hub en klik op **eindpunten**.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-141">In hello Azure portal, open your IoT hub and click **Endpoints**.</span></span>
    
    ![Eindpunten van IoT-hub][30]

3. <span data-ttu-id="c7a5e-143">In Hallo **eindpunten** blade, klikt u op **toevoegen** op Hallo bovenste tooadd uw wachtrij tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-143">In hello **Endpoints** blade, click **Add** at hello top tooadd your queue tooyour IoT hub.</span></span> <span data-ttu-id="c7a5e-144">Naam Hallo eindpunt **CriticalQueue** en gebruik Hallo-keuzelijsten tooselect **Service Bus-wachtrij**Hallo Service Bus-naamruimte waarin de wachtrij zich bevindt en de naam van uw wachtrij Hallo.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-144">Name hello endpoint **CriticalQueue** and use hello drop-downs tooselect **Service Bus queue**, hello Service Bus namespace in which your queue resides, and hello name of your queue.</span></span> <span data-ttu-id="c7a5e-145">Wanneer u klaar bent, klikt u op **opslaan** Hallo onderaan.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-145">When you are done, click **Save** at hello bottom.</span></span>
    
    ![Een eindpunt toevoegen][31]
    
4. <span data-ttu-id="c7a5e-147">Klik nu op **Routes** in uw IoT-Hub.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-147">Now click **Routes** in your IoT Hub.</span></span> <span data-ttu-id="c7a5e-148">Klik op **toevoegen** bovenaan Hallo Hallo blade toocreate een regel voor doorsturen die routeert berichten toohello wachtrij u zojuist hebt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-148">Click **Add** at hello top of hello blade toocreate a routing rule that routes messages toohello queue you just added.</span></span> <span data-ttu-id="c7a5e-149">Selecteer **DeviceTelemetry** als Hallo gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-149">Select **DeviceTelemetry** as hello source of data.</span></span> <span data-ttu-id="c7a5e-150">Voer `level="critical"` als Hallo voorwaarde, en kies Hallo wachtrij die u zojuist hebt toegevoegd als een aangepaste eindpunt als Hallo regel eindpunt routering.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-150">Enter `level="critical"` as hello condition, and choose hello queue you just added as a custom endpoint as hello routing rule endpoint.</span></span> <span data-ttu-id="c7a5e-151">Wanneer u klaar bent, klikt u op **opslaan** Hallo onderaan.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-151">When you are done, click **Save** at hello bottom.</span></span>
    
    ![Toevoegen van een route][32]
    
    <span data-ttu-id="c7a5e-153">Zorg ervoor dat Hallo terugval route is ingesteld, te**ON**.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-153">Make sure hello fallback route is set too**ON**.</span></span> <span data-ttu-id="c7a5e-154">Deze waarde is de standaardconfiguratie Hallo voor een IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-154">This value is hello default configuration for an IoT hub.</span></span>
    
    ![Route voor terugval][33]

## <a name="read-from-hello-queue-endpoint"></a><span data-ttu-id="c7a5e-156">Lezen van Hallo wachtrij eindpunt</span><span class="sxs-lookup"><span data-stu-id="c7a5e-156">Read from hello queue endpoint</span></span>

<span data-ttu-id="c7a5e-157">In deze sectie kunt u Hallo-berichten lezen van Hallo wachtrij eindpunt.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-157">In this section, you read hello messages from hello queue endpoint.</span></span>

1. <span data-ttu-id="c7a5e-158">Voeg in Visual Studio een Visual C# Classic Windows Desktop-project toohello huidige oplossing met behulp van Hallo **Console-App (.NET Framework)** projectsjabloon.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-158">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution, by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="c7a5e-159">Naam Hallo project **ReadCriticalQueue**.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-159">Name hello project **ReadCriticalQueue**.</span></span>

2. <span data-ttu-id="c7a5e-160">Klik in Solution Explorer met de rechtermuisknop op Hallo **ReadCriticalQueue** project en klik vervolgens op **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-160">In Solution Explorer, right-click hello **ReadCriticalQueue** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="c7a5e-161">Met deze bewerking wordt Hallo **NuGet Package Manager** venster.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-161">This operation displays hello **NuGet Package Manager** window.</span></span>

3. <span data-ttu-id="c7a5e-162">Zoeken naar **WindowsAzure.ServiceBus**, klikt u op **installeren**, en accepteer de gebruiksvoorwaarden Hallo.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-162">Search for **WindowsAzure.ServiceBus**, click **Install**, and accept hello terms of use.</span></span> <span data-ttu-id="c7a5e-163">Deze bewerking downloadt, installeert en voegt een verwijzing toohello Azure Service Bus, inclusief alle afhankelijkheden ervan.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-163">This operation downloads, installs, and adds a reference toohello Azure Service Bus, with all its dependencies.</span></span>

4. <span data-ttu-id="c7a5e-164">Voeg de volgende Hallo **met** instructies boven Hallo Hallo **Program.cs** bestand:</span><span class="sxs-lookup"><span data-stu-id="c7a5e-164">Add hello following **using** statements at hello top of hello **Program.cs** file:</span></span>
   
    ```csharp
    using System.IO;
    using Microsoft.ServiceBus.Messaging;
    ```

5. <span data-ttu-id="c7a5e-165">Voeg regels toohello na Hallo **Main** methode.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-165">Finally, add hello following lines toohello **Main** method.</span></span> <span data-ttu-id="c7a5e-166">Vervang de verbindingsreeks Hallo met **luisteren** machtigingen voor Hallo wachtrij:</span><span class="sxs-lookup"><span data-stu-id="c7a5e-166">Substitute hello connection string with **Listen** permissions for hello queue:</span></span>
   
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

## <a name="run-hello-applications"></a><span data-ttu-id="c7a5e-167">Hallo-toepassingen uitvoeren</span><span class="sxs-lookup"><span data-stu-id="c7a5e-167">Run hello applications</span></span>
<span data-ttu-id="c7a5e-168">U bent nu klaar toorun Hallo toepassingen.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-168">Now you are ready toorun hello applications.</span></span>

1. <span data-ttu-id="c7a5e-169">In Visual Studio in Solution Explorer met de rechtermuisknop op uw oplossing en selecteer **Opstartprojecten instellen**.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-169">In Visual Studio, in Solution Explorer, right-click your solution and select **Set StartUp Projects**.</span></span> <span data-ttu-id="c7a5e-170">Selecteer **meerdere opstartprojecten**, selecteer daarna **Start** als actie voor Hallo Hallo **ReadDeviceToCloudMessages**, **SimulatedDevice**, en **ReadCriticalQueue** projecten.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-170">Select **Multiple startup projects**, then select **Start** as hello action for hello **ReadDeviceToCloudMessages**, **SimulatedDevice**, and **ReadCriticalQueue** projects.</span></span>
2. <span data-ttu-id="c7a5e-171">Druk op **F5** toostart Hallo drie console-apps.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-171">Press **F5** toostart hello three console apps.</span></span> <span data-ttu-id="c7a5e-172">Hallo **ReadDeviceToCloudMessages** app heeft alleen niet-kritieke berichten van Hallo **SimulatedDevice** toepassings- en Hallo **ReadCriticalQueue** app heeft alleen kritieke berichten.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-172">hello **ReadDeviceToCloudMessages** app has only non-critical messages sent from hello **SimulatedDevice** application, and hello **ReadCriticalQueue** app has only critical messages.</span></span>
   
   ![Drie console-apps][50]

## <a name="next-steps"></a><span data-ttu-id="c7a5e-174">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c7a5e-174">Next steps</span></span>
<span data-ttu-id="c7a5e-175">In deze zelfstudie hebt u geleerd hoe tooreliably apparaat-naar-cloud-berichten verzenden met behulp van Hallo-bericht routeringsfunctionaliteit van IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-175">In this tutorial, you learned how tooreliably dispatch device-to-cloud messages by using hello message routing functionality of IoT Hub.</span></span>

<span data-ttu-id="c7a5e-176">Hallo [hoe toosend cloud-naar-apparaat met IoT Hub berichten] [ lnk-c2d] ziet u hoe toosend tooyour apparaten uit de back-end van uw oplossing berichten.</span><span class="sxs-lookup"><span data-stu-id="c7a5e-176">hello [How toosend cloud-to-device messages with IoT Hub][lnk-c2d] shows you how toosend messages tooyour devices from your solution back end.</span></span>

<span data-ttu-id="c7a5e-177">Voorbeelden van volledige end-to-end-oplossingen die gebruikmaken van IoT Hub toosee Zie [Azure IoT Suite][lnk-suite].</span><span class="sxs-lookup"><span data-stu-id="c7a5e-177">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite][lnk-suite].</span></span>

<span data-ttu-id="c7a5e-178">toolearn meer informatie over het ontwikkelen van oplossingen met IoT Hub, Zie Hallo [Ontwikkelaarshandleiding voor IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="c7a5e-178">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

<span data-ttu-id="c7a5e-179">Zie toolearn meer informatie over het routeren van berichten van IoT-Hub [berichten verzenden en ontvangen met IoT Hub][lnk-devguide-messaging].</span><span class="sxs-lookup"><span data-stu-id="c7a5e-179">toolearn more about message routing in IoT Hub, see [Send and receive messages with IoT Hub][lnk-devguide-messaging].</span></span>

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
