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
# <a name="send-messages-from-hello-cloud-tooyour-device-with-iot-hub-net"></a><span data-ttu-id="1635a-104">Berichten verzenden van Hallo cloud tooyour apparaat met IoT Hub (.NET)</span><span class="sxs-lookup"><span data-stu-id="1635a-104">Send messages from hello cloud tooyour device with IoT Hub (.NET)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a><span data-ttu-id="1635a-105">Inleiding</span><span class="sxs-lookup"><span data-stu-id="1635a-105">Introduction</span></span>
<span data-ttu-id="1635a-106">Azure IoT Hub is een volledig beheerde service waarmee stabiele en veilige tweerichtingscommunicatie tussen miljoenen apparaten inschakelen en een back-end oplossing.</span><span class="sxs-lookup"><span data-stu-id="1635a-106">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="1635a-107">Hallo [aan de slag met IoT Hub] zelfstudie laat zien hoe toocreate een IoT-hub een apparaat-id in het inrichten en code van de app voor een apparaat dat apparaat-naar-cloud-berichten verzendt.</span><span class="sxs-lookup"><span data-stu-id="1635a-107">hello [Get started with IoT Hub] tutorial shows how toocreate an IoT hub, provision a device identity in it, and code a device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="1635a-108">Deze zelfstudie bouwt voort op [aan de slag met IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="1635a-108">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="1635a-109">Hier ziet u hoe aan:</span><span class="sxs-lookup"><span data-stu-id="1635a-109">It shows you how to:</span></span>

* <span data-ttu-id="1635a-110">Verzenden van uw back-end oplossing, cloud-naar-apparaatberichten tooa één apparaat via IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1635a-110">From your solution back end, send cloud-to-device messages tooa single device through IoT Hub.</span></span>
* <span data-ttu-id="1635a-111">Cloud-naar-apparaat-berichten op een apparaat ontvangen.</span><span class="sxs-lookup"><span data-stu-id="1635a-111">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="1635a-112">Aanvragen van uw back-end oplossing, levering bevestiging (*feedback*) voor tooa apparaat van de berichten uit IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1635a-112">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent tooa device from IoT Hub.</span></span>

<span data-ttu-id="1635a-113">U vindt meer informatie over cloud-naar-apparaat-berichten in Hallo [Ontwikkelaarshandleiding voor IoT Hub][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="1635a-113">You can find more information on cloud-to-device messages in hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="1635a-114">Aan het einde van de Hallo van deze zelfstudie, moet u twee apps voor .NET-console uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="1635a-114">At hello end of this tutorial, you run two .NET console apps:</span></span>

* <span data-ttu-id="1635a-115">**SimulatedDevice**, een aangepaste versie van het Hallo-app gemaakt in [aan de slag met IoT Hub], die verbinding maakt tooyour IoT-hub en cloud-naar-apparaat-berichten worden ontvangen.</span><span class="sxs-lookup"><span data-stu-id="1635a-115">**SimulatedDevice**, a modified version of hello app created in [Get started with IoT Hub], which connects tooyour IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="1635a-116">**SendCloudToDevice**, die een cloud-naar-apparaat bericht toohello apparaattoepassing via IoT Hub verzendt en ontvangt u vervolgens de bevestiging levering.</span><span class="sxs-lookup"><span data-stu-id="1635a-116">**SendCloudToDevice**, which sends a cloud-to-device message toohello device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="1635a-117">IoT-Hub SDK-ondersteuning voor veel apparaatplatforms en talen (inclusief C, Java en Javascript) via heeft [apparaat Azure IoT SDK's].</span><span class="sxs-lookup"><span data-stu-id="1635a-117">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through [Azure IoT device SDKs].</span></span> <span data-ttu-id="1635a-118">Voor stapsgewijze instructies voor hoe tooconnect uw apparaat toothis-zelfstudie code en over het algemeen tooAzure IoT Hub zien Hallo [Ontwikkelaarshandleiding voor IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="1635a-118">For step-by-step instructions on how tooconnect your device toothis tutorial's code, and generally tooAzure IoT Hub, see hello [IoT Hub developer guide].</span></span>
> 
> 

<span data-ttu-id="1635a-119">toocomplete in deze zelfstudie, moet u hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="1635a-119">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="1635a-120">Visual Studio 2015 of Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="1635a-120">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="1635a-121">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="1635a-121">An active Azure account.</span></span> <span data-ttu-id="1635a-122">(Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)</span><span class="sxs-lookup"><span data-stu-id="1635a-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-hello-device-app"></a><span data-ttu-id="1635a-123">Berichten ontvangen in Hallo apparaattoepassing</span><span class="sxs-lookup"><span data-stu-id="1635a-123">Receive messages in hello device app</span></span>
<span data-ttu-id="1635a-124">In deze sectie bewerkt u Hallo apparaattoepassing u hebt gemaakt in [aan de slag met IoT Hub] tooreceive cloud-naar-apparaat-berichten uit Hallo iothub.</span><span class="sxs-lookup"><span data-stu-id="1635a-124">In this section, you'll modify hello device app you created in [Get started with IoT Hub] tooreceive cloud-to-device messages from hello IoT hub.</span></span>

1. <span data-ttu-id="1635a-125">In Visual Studio in Hallo **SimulatedDevice** project, het toevoegen van Hallo na methode toohello **programma** klasse.</span><span class="sxs-lookup"><span data-stu-id="1635a-125">In Visual Studio, in hello **SimulatedDevice** project, add hello following method toohello **Program** class.</span></span>
   
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
   
    <span data-ttu-id="1635a-126">Hallo `ReceiveAsync` methode retourneert asynchroon ontvangen welkomstbericht op Hallo moment dat deze is ontvangen door het Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="1635a-126">hello `ReceiveAsync` method asynchronously returns hello received message at hello time that it is received by hello device.</span></span> <span data-ttu-id="1635a-127">Deze retourneert *null* na een specifiable time-outperiode (in dit geval de standaard Hallo van één minuut wordt gebruikt).</span><span class="sxs-lookup"><span data-stu-id="1635a-127">It returns *null* after a specifiable timeout period (in this case, hello default of one minute is used).</span></span> <span data-ttu-id="1635a-128">Wanneer Hallo app ontvangt een *null*, toowait op nieuwe berichten moet worden voortgezet.</span><span class="sxs-lookup"><span data-stu-id="1635a-128">When hello app receives a *null*, it should continue toowait for new messages.</span></span> <span data-ttu-id="1635a-129">Deze vereiste is Hallo reden voor Hallo `if (receivedMessage == null) continue` regel.</span><span class="sxs-lookup"><span data-stu-id="1635a-129">This requirement is hello reason for hello `if (receivedMessage == null) continue` line.</span></span>
   
    <span data-ttu-id="1635a-130">Hallo aanroep te`CompleteAsync()` IoT Hub een melding dat het Hallo-bericht is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="1635a-130">hello call too`CompleteAsync()` notifies IoT Hub that hello message has been successfully processed.</span></span> <span data-ttu-id="1635a-131">Hallo-bericht kan veilig worden verwijderd uit Hallo apparaatwachtrij.</span><span class="sxs-lookup"><span data-stu-id="1635a-131">hello message can be safely removed from hello device queue.</span></span> <span data-ttu-id="1635a-132">Als er iets opgetreden die Hallo apparaat-app voltooid Hallo verwerking van het Hallo-bericht, bezorgd IoT-Hub opnieuw.</span><span class="sxs-lookup"><span data-stu-id="1635a-132">If something happened that prevented hello device app from completing hello processing of hello message, IoT Hub delivers it again.</span></span> <span data-ttu-id="1635a-133">Vervolgens is het belangrijk dat logica in apparaattoepassing Hallo-berichten wordt *idempotent*, zodat de ontvangst van hetzelfde bericht meerdere keren produceert Hallo Hallo hetzelfde resultaat.</span><span class="sxs-lookup"><span data-stu-id="1635a-133">It is then important that message processing logic in hello device app is *idempotent*, so that receiving hello same message multiple times produces hello same result.</span></span> <span data-ttu-id="1635a-134">Een toepassing kan een bericht, hetgeen resulteert in IoT-hub behoud het Hallo-bericht in de wachtrij Hallo voor toekomstige consumptie ook tijdelijk afbreken.</span><span class="sxs-lookup"><span data-stu-id="1635a-134">An application can also temporarily abandon a message, which results in IoT hub retaining hello message in hello queue for future consumption.</span></span> <span data-ttu-id="1635a-135">Of Hallo toepassing kan een bericht dat het Hallo-bericht permanent verwijderd uit de wachtrij Hallo weigeren.</span><span class="sxs-lookup"><span data-stu-id="1635a-135">Or, hello application can reject a message, which permanently removes hello message from hello queue.</span></span> <span data-ttu-id="1635a-136">Zie voor meer informatie over de levenscyclus van de cloud-naar-apparaat bericht Hallo Hallo [Ontwikkelaarshandleiding voor IoT Hub][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="1635a-136">For more information about hello cloud-to-device message lifecycle, see hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="1635a-137">Wanneer u HTTP gebruikt in plaats van MQTT of AMQP als transport, Hallo `ReceiveAsync` methode retourneert onmiddellijk.</span><span class="sxs-lookup"><span data-stu-id="1635a-137">When using HTTP instead of MQTT or AMQP as a transport, hello `ReceiveAsync` method returns immediately.</span></span> <span data-ttu-id="1635a-138">Hallo ondersteund patroon voor cloud-naar-apparaat-berichten met HTTP is tijdelijk verbonden apparaten controleren voor berichten zelden (minder dan elke 25 minuten).</span><span class="sxs-lookup"><span data-stu-id="1635a-138">hello supported pattern for cloud-to-device messages with HTTP is intermittently connected devices that check for messages infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="1635a-139">Uitgifte van meer HTTP ontvangt resultaten in IoT Hub bandbreedteregeling Hallo aanvragen.</span><span class="sxs-lookup"><span data-stu-id="1635a-139">Issuing more HTTP receives results in IoT Hub throttling hello requests.</span></span> <span data-ttu-id="1635a-140">Zie voor meer informatie over Hallo verschillen tussen de protocollen MQTT, AMQP en HTTP-ondersteuning en Iothub beperking Hallo [Ontwikkelaarshandleiding voor IoT Hub][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="1635a-140">For more information about hello differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   > 
   > 
2. <span data-ttu-id="1635a-141">Toevoegen van de volgende methode in Hallo Hallo **Main** methode aan vóór Hallo `Console.ReadLine()` regel:</span><span class="sxs-lookup"><span data-stu-id="1635a-141">Add hello following method in hello **Main** method, right before hello `Console.ReadLine()` line:</span></span>
   
        ReceiveC2dAsync();

> [!NOTE]
> <span data-ttu-id="1635a-142">Deze zelfstudie implementeert voor de eenvoud mogelijk te houden, niet een beleid voor opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="1635a-142">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="1635a-143">In productiecode moet u beleid voor opnieuw proberen (zoals exponentieel uitstel), zoals voorgesteld in de MSDN-artikel Hallo implementeren [afhandeling van tijdelijke fout].</span><span class="sxs-lookup"><span data-stu-id="1635a-143">In production code, you should implement retry policies (such as exponential backoff), as suggested in hello MSDN article [Transient Fault Handling].</span></span>
> 
> 

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="1635a-144">Een cloud naar apparaat verzenden</span><span class="sxs-lookup"><span data-stu-id="1635a-144">Send a cloud-to-device message</span></span>
<span data-ttu-id="1635a-145">In deze sectie schrijft u een .NET-consoletoepassing die cloud-naar-apparaatberichten toohello apparaat app verzendt.</span><span class="sxs-lookup"><span data-stu-id="1635a-145">In this section, you write a .NET console app that sends cloud-to-device messages toohello device app.</span></span>

1. <span data-ttu-id="1635a-146">Maak in Hallo huidige Visual Studio-oplossing een Visual C# bureaublad-App-project met behulp van Hallo **consoletoepassing** projectsjabloon.</span><span class="sxs-lookup"><span data-stu-id="1635a-146">In hello current Visual Studio solution, create a Visual C# Desktop App project by using hello **Console Application** project template.</span></span> <span data-ttu-id="1635a-147">Naam Hallo project **SendCloudToDevice**.</span><span class="sxs-lookup"><span data-stu-id="1635a-147">Name hello project **SendCloudToDevice**.</span></span>
   
    ![Nieuw project in Visual Studio][20]
2. <span data-ttu-id="1635a-149">Klik in Solution Explorer met de rechtermuisknop op het Hallo-oplossing en klik vervolgens op **NuGet-pakketten beheren voor oplossing...** .</span><span class="sxs-lookup"><span data-stu-id="1635a-149">In Solution Explorer, right-click hello solution, and then click **Manage NuGet Packages for Solution...**.</span></span> 
   
    <span data-ttu-id="1635a-150">Hiermee Hallo **NuGet-pakketten beheren** venster.</span><span class="sxs-lookup"><span data-stu-id="1635a-150">This action opens hello **Manage NuGet Packages** window.</span></span>
3. <span data-ttu-id="1635a-151">Zoeken naar **Microsoft.Azure.Devices**, klikt u op **installeren**, en accepteer de gebruiksvoorwaarden Hallo.</span><span class="sxs-lookup"><span data-stu-id="1635a-151">Search for **Microsoft.Azure.Devices**, click **Install**, and accept hello terms of use.</span></span> 
   
    <span data-ttu-id="1635a-152">Dit downloadt, installeert en voegt u een verwijzing toohello [Azure IoT service SDK NuGet-pakket].</span><span class="sxs-lookup"><span data-stu-id="1635a-152">This downloads, installs, and adds a reference toohello [Azure IoT service SDK NuGet package].</span></span>

4. <span data-ttu-id="1635a-153">Voeg de volgende Hallo `using` instructie bovenaan Hallo Hallo **Program.cs** bestand:</span><span class="sxs-lookup"><span data-stu-id="1635a-153">Add hello following `using` statement at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="1635a-154">Hallo na toohello velden toevoegen **programma** klasse.</span><span class="sxs-lookup"><span data-stu-id="1635a-154">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="1635a-155">Vervang de aanduidingswaarde Hallo door Hallo IoT hub-verbindingsreeks uit [aan de slag met IoT Hub]:</span><span class="sxs-lookup"><span data-stu-id="1635a-155">Substitute hello placeholder value with hello IoT hub connection string from [Get started with IoT Hub]:</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="1635a-156">Hallo na methode toohello toevoegen **programma** klasse:</span><span class="sxs-lookup"><span data-stu-id="1635a-156">Add hello following method toohello **Program** class:</span></span>
   
        private async static Task SendCloudToDeviceMessageAsync()
        {
            var commandMessage = new Message(Encoding.ASCII.GetBytes("Cloud toodevice message."));
            await serviceClient.SendAsync("myFirstDevice", commandMessage);
        }
   
    <span data-ttu-id="1635a-157">Deze methode verzendt een nieuw bericht cloud-naar-apparaat toohello apparaat met Hallo-ID, `myFirstDevice`.</span><span class="sxs-lookup"><span data-stu-id="1635a-157">This method sends a new cloud-to-device message toohello device with hello ID, `myFirstDevice`.</span></span> <span data-ttu-id="1635a-158">Deze parameter alleen wijzigen als u deze hebt gewijzigd van Hallo die wordt gebruikt bij [aan de slag met IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="1635a-158">Change this parameter only if you modified it from hello one used in [Get started with IoT Hub].</span></span>
7. <span data-ttu-id="1635a-159">Voeg regels toohello na Hallo **Main** methode:</span><span class="sxs-lookup"><span data-stu-id="1635a-159">Finally, add hello following lines toohello **Main** method:</span></span>
   
        Console.WriteLine("Send Cloud-to-Device message\n");
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
   
        Console.WriteLine("Press any key toosend a C2D message.");
        Console.ReadLine();
        SendCloudToDeviceMessageAsync().Wait();
        Console.ReadLine();
8. <span data-ttu-id="1635a-160">Vanuit Visual Studio met de rechtermuisknop op uw oplossing en selecteer **opstartprojecten instellen...** . Selecteer **meerdere opstartprojecten**, selecteer daarna Hallo **Start** actie voor **ReadDeviceToCloudMessages**, **SimulatedDevice**, en **SendCloudToDevice**.</span><span class="sxs-lookup"><span data-stu-id="1635a-160">From within Visual Studio, right-click your solution, and select **Set StartUp projects...**. Select **Multiple startup projects**, then select hello **Start** action for **ReadDeviceToCloudMessages**, **SimulatedDevice**, and **SendCloudToDevice**.</span></span>
9. <span data-ttu-id="1635a-161">Druk op **F5**.</span><span class="sxs-lookup"><span data-stu-id="1635a-161">Press **F5**.</span></span> <span data-ttu-id="1635a-162">Alle drie de toepassingen moeten worden gestart.</span><span class="sxs-lookup"><span data-stu-id="1635a-162">All three applications should start.</span></span> <span data-ttu-id="1635a-163">Selecteer Hallo **SendCloudToDevice** windows en druk op **Enter**.</span><span class="sxs-lookup"><span data-stu-id="1635a-163">Select hello **SendCloudToDevice** windows, and press **Enter**.</span></span> <span data-ttu-id="1635a-164">U ziet het Hallo-bericht ontvangen door Hallo apparaattoepassing.</span><span class="sxs-lookup"><span data-stu-id="1635a-164">You should see hello message being received by hello device app.</span></span>
   
   ![App-ontvangende bericht][21]

## <a name="receive-delivery-feedback"></a><span data-ttu-id="1635a-166">Leveringsfeedback ontvangen</span><span class="sxs-lookup"><span data-stu-id="1635a-166">Receive delivery feedback</span></span>
<span data-ttu-id="1635a-167">Het is mogelijk toorequest levering (of verlopen) bevestigingen van IoT Hub voor elk bericht cloud-naar-apparaat.</span><span class="sxs-lookup"><span data-stu-id="1635a-167">It is possible toorequest delivery (or expiration) acknowledgements from IoT Hub for each cloud-to-device message.</span></span> <span data-ttu-id="1635a-168">Deze optie schakelt Hallo oplossing voor back-end tooeasily kennis opnieuw of compensatie logica.</span><span class="sxs-lookup"><span data-stu-id="1635a-168">This option enables hello solution back end tooeasily inform retry or compensation logic.</span></span> <span data-ttu-id="1635a-169">Zie voor meer informatie over de cloud-naar-apparaat feedback Hallo [Ontwikkelaarshandleiding voor IoT Hub][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="1635a-169">For more information about cloud-to-device feedback, see hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="1635a-170">In deze sectie maakt u Hallo wijzigen **SendCloudToDevice** app toorequest feedback, en deze uit IoT Hub worden ontvangen.</span><span class="sxs-lookup"><span data-stu-id="1635a-170">In this section, you modify hello **SendCloudToDevice** app toorequest feedback, and receive it from IoT Hub.</span></span>

1. <span data-ttu-id="1635a-171">In Visual Studio in Hallo **SendCloudToDevice** project, het toevoegen van Hallo na methode toohello **programma** klasse.</span><span class="sxs-lookup"><span data-stu-id="1635a-171">In Visual Studio, in hello **SendCloudToDevice** project, add hello following method toohello **Program** class.</span></span>
   
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
   
    <span data-ttu-id="1635a-172">Opmerking: dit patroon ontvangen is dezelfde één gebruikte tooreceive cloud-naar-apparaat berichten van apparaattoepassing Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="1635a-172">Note this receive pattern is hello same one used tooreceive cloud-to-device messages from hello device app.</span></span>
2. <span data-ttu-id="1635a-173">Toevoegen van de volgende methode in Hallo Hallo **Main** methode, meteen na Hallo `serviceClient = ServiceClient.CreateFromConnectionString(connectionString)` regel:</span><span class="sxs-lookup"><span data-stu-id="1635a-173">Add hello following method in hello **Main** method, right after hello `serviceClient = ServiceClient.CreateFromConnectionString(connectionString)` line:</span></span>
   
        ReceiveFeedbackAsync();
3. <span data-ttu-id="1635a-174">toorequest feedback voor het leveren van Hallo van uw bericht cloud-naar-apparaat, hebt u toospecify een eigenschap in Hallo **SendCloudToDeviceMessageAsync** methode.</span><span class="sxs-lookup"><span data-stu-id="1635a-174">toorequest feedback for hello delivery of your cloud-to-device message, you have toospecify a property in hello **SendCloudToDeviceMessageAsync** method.</span></span> <span data-ttu-id="1635a-175">Hallo volgt regel, direct na Hallo toevoegen `var commandMessage = new Message(...);` regel:</span><span class="sxs-lookup"><span data-stu-id="1635a-175">Add hello following line, right after hello `var commandMessage = new Message(...);` line:</span></span>
   
        commandMessage.Ack = DeliveryAcknowledgement.Full;
4. <span data-ttu-id="1635a-176">Hallo-apps uitvoeren door te drukken **F5**.</span><span class="sxs-lookup"><span data-stu-id="1635a-176">Run hello apps by pressing **F5**.</span></span> <span data-ttu-id="1635a-177">Hier ziet u alle drie de toepassingen starten.</span><span class="sxs-lookup"><span data-stu-id="1635a-177">You should see all three applications start.</span></span> <span data-ttu-id="1635a-178">Selecteer Hallo **SendCloudToDevice** windows en druk op **Enter**.</span><span class="sxs-lookup"><span data-stu-id="1635a-178">Select hello **SendCloudToDevice** windows, and press **Enter**.</span></span> <span data-ttu-id="1635a-179">U ziet Hallo-bericht wordt ontvangen door Hallo apparaattoepassing en na enkele seconden, Hallo Feedbackbericht wordt ontvangen door uw **SendCloudToDevice** toepassing.</span><span class="sxs-lookup"><span data-stu-id="1635a-179">You should see hello message being received by hello device app, and after a few seconds, hello feedback message being received by your **SendCloudToDevice** application.</span></span>
   
   ![App-ontvangende bericht][22]

> [!NOTE]
> <span data-ttu-id="1635a-181">Deze zelfstudie implementeert voor de eenvoud mogelijk te houden, niet een beleid voor opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="1635a-181">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="1635a-182">In productiecode moet u beleid voor opnieuw proberen (zoals exponentieel uitstel), zoals voorgesteld in de MSDN-artikel Hallo implementeren [afhandeling van tijdelijke fout].</span><span class="sxs-lookup"><span data-stu-id="1635a-182">In production code, you should implement retry policies (such as exponential backoff), as suggested in hello MSDN article [Transient Fault Handling].</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="1635a-183">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1635a-183">Next steps</span></span>
<span data-ttu-id="1635a-184">In deze zelfstudie hebt u geleerd hoe toosend en cloud-naar-apparaat-berichten ontvangen.</span><span class="sxs-lookup"><span data-stu-id="1635a-184">In this tutorial, you learned how toosend and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="1635a-185">Voorbeelden van volledige end-to-end-oplossingen die gebruikmaken van IoT Hub toosee Zie [Azure IoT Suite].</span><span class="sxs-lookup"><span data-stu-id="1635a-185">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="1635a-186">toolearn meer informatie over het ontwikkelen van oplossingen met IoT Hub, Zie Hallo [Ontwikkelaarshandleiding voor IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="1635a-186">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

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