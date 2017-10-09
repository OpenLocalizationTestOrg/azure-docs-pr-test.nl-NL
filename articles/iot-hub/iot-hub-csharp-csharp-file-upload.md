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
# <a name="upload-files-from-your-device-toohello-cloud-with-iot-hub-using-net"></a><span data-ttu-id="f01e8-104">Uploaden van bestanden van uw apparaat toohello cloud met IoT Hub met .NET</span><span class="sxs-lookup"><span data-stu-id="f01e8-104">Upload files from your device toohello cloud with IoT Hub using .NET</span></span>

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

<span data-ttu-id="f01e8-105">Deze zelfstudie bouwt voort op Hallo-code in Hallo [Cloud naar apparaat verzenden met IoT Hub](iot-hub-csharp-csharp-c2d.md) zelfstudie tooshow u hoe toouse Hallo functies voor het uploaden van bestanden van IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="f01e8-105">This tutorial builds on hello code in hello [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorial tooshow you how toouse hello file upload capabilities of IoT Hub.</span></span> <span data-ttu-id="f01e8-106">Hier ziet u hoe aan:</span><span class="sxs-lookup"><span data-stu-id="f01e8-106">It shows you how to:</span></span>

- <span data-ttu-id="f01e8-107">Veilig een apparaat voorzien van een Azure blob-URI voor het uploaden van een bestand.</span><span class="sxs-lookup"><span data-stu-id="f01e8-107">Securely provide a device with an Azure blob URI for uploading a file.</span></span>
- <span data-ttu-id="f01e8-108">Hallo IoT Hub-bestand uploaden meldingen tootrigger verwerken Hallo-bestand in de back-end van uw app gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f01e8-108">Use hello IoT Hub file upload notifications tootrigger processing hello file in your app back end.</span></span>

<span data-ttu-id="f01e8-109">Hallo [aan de slag met IoT Hub](iot-hub-csharp-csharp-getstarted.md) en [Cloud naar apparaat verzenden met IoT Hub](iot-hub-csharp-csharp-c2d.md) zelfstudies ziet Hallo apparaat-naar-cloud- en cloud-naar-apparaat messaging basisfunctionaliteit van IoT-Hub.</span><span class="sxs-lookup"><span data-stu-id="f01e8-109">hello [Get started with IoT Hub](iot-hub-csharp-csharp-getstarted.md) and [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorials show hello basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span> <span data-ttu-id="f01e8-110">Hallo [proces apparaat-naar-cloudberichten](iot-hub-csharp-csharp-process-d2c.md) zelfstudie beschrijft een manier tooreliably store apparaat-naar-cloud-berichten in Azure blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="f01e8-110">hello [Process Device-to-Cloud messages](iot-hub-csharp-csharp-process-d2c.md) tutorial describes a way tooreliably store device-to-cloud messages in Azure blob storage.</span></span> <span data-ttu-id="f01e8-111">In sommige scenario's kan niet u echter gemakkelijk toewijzen hello gegevens verzenden van uw apparaten in hello relatief klein apparaat-naar-cloud-berichten die IoT Hub accepteert.</span><span class="sxs-lookup"><span data-stu-id="f01e8-111">However, in some scenarios you cannot easily map hello data your devices send into hello relatively small device-to-cloud messages that IoT Hub accepts.</span></span> <span data-ttu-id="f01e8-112">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f01e8-112">For example:</span></span>

* <span data-ttu-id="f01e8-113">Grote bestanden met afbeeldingen</span><span class="sxs-lookup"><span data-stu-id="f01e8-113">Large files that contain images</span></span>
* <span data-ttu-id="f01e8-114">Video's</span><span class="sxs-lookup"><span data-stu-id="f01e8-114">Videos</span></span>
* <span data-ttu-id="f01e8-115">Trillingen gegevens dat met hoge frequentie</span><span class="sxs-lookup"><span data-stu-id="f01e8-115">Vibration data sampled at high frequency</span></span>
* <span data-ttu-id="f01e8-116">Een vorm van voorverwerkte gegevens</span><span class="sxs-lookup"><span data-stu-id="f01e8-116">Some form of preprocessed data</span></span>

<span data-ttu-id="f01e8-117">Deze bestanden zijn meestal batch verwerkt in Hallo cloud met hulpprogramma's zoals [Azure Data Factory](../data-factory/index.md) of Hallo [Hadoop](../hdinsight/index.md) stack.</span><span class="sxs-lookup"><span data-stu-id="f01e8-117">These files are typically batch processed in hello cloud using tools such as [Azure Data Factory](../data-factory/index.md) or hello [Hadoop](../hdinsight/index.md) stack.</span></span> <span data-ttu-id="f01e8-118">Wanneer u tooupload bestanden van een apparaat nodig hebt, kunt u nog steeds Hallo beveiliging en betrouwbaarheid van IoT Hub gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f01e8-118">When you need tooupload files from a device, you can still use hello security and reliability of IoT Hub.</span></span>

<span data-ttu-id="f01e8-119">Aan Hallo einde van deze zelfstudie kunt u twee apps voor .NET-console uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f01e8-119">At hello end of this tutorial you run two .NET console apps:</span></span>

* <span data-ttu-id="f01e8-120">**SimulatedDevice**, een aangepaste versie van het Hallo-app gemaakt in Hallo [Cloud naar apparaat verzenden met IoT Hub](iot-hub-csharp-csharp-c2d.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="f01e8-120">**SimulatedDevice**, a modified version of hello app created in hello [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorial.</span></span> <span data-ttu-id="f01e8-121">Deze app uploadt een bestand toostorage met behulp van een SAS-URI geleverd door uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="f01e8-121">This app uploads a file toostorage using a SAS URI provided by your IoT hub.</span></span>
* <span data-ttu-id="f01e8-122">**ReadFileUploadNotification**, dat bestand uploaden meldingen ontvangt van uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="f01e8-122">**ReadFileUploadNotification**, which receives file upload notifications from your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="f01e8-123">IoT Hub biedt ondersteuning voor veel apparaatplatforms en talen (inclusief C, Java en Javascript) via Azure IoT-apparaat SDK's.</span><span class="sxs-lookup"><span data-stu-id="f01e8-123">IoT Hub supports many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="f01e8-124">Raadpleeg toohello [Azure IoT Developer Center] voor stapsgewijze instructies voor het tooconnect uw apparaat tooAzure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="f01e8-124">Refer toohello [Azure IoT Developer Center] for step-by-step instructions on how tooconnect your device tooAzure IoT Hub.</span></span>

<span data-ttu-id="f01e8-125">toocomplete in deze zelfstudie, moet u hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="f01e8-125">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="f01e8-126">Visual Studio 2015 of Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="f01e8-126">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="f01e8-127">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="f01e8-127">An active Azure account.</span></span> <span data-ttu-id="f01e8-128">(Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)</span><span class="sxs-lookup"><span data-stu-id="f01e8-128">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a><span data-ttu-id="f01e8-129">Een bestand vanaf een apparaat-app uploaden</span><span class="sxs-lookup"><span data-stu-id="f01e8-129">Upload a file from a device app</span></span>

<span data-ttu-id="f01e8-130">In deze sectie maakt u Hallo apparaattoepassing u hebt gemaakt in wijzigen [Cloud naar apparaat verzenden met IoT Hub](iot-hub-csharp-csharp-c2d.md) tooreceive cloud-naar-apparaat-berichten uit Hallo iothub.</span><span class="sxs-lookup"><span data-stu-id="f01e8-130">In this section, you modify hello device app you created in [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tooreceive cloud-to-device messages from hello IoT hub.</span></span>

1. <span data-ttu-id="f01e8-131">In Visual Studio met de rechtermuisknop op Hallo **SimulatedDevice** project, klikt u op **toevoegen**, en klik vervolgens op **bestaand Item**.</span><span class="sxs-lookup"><span data-stu-id="f01e8-131">In Visual Studio, right-click hello **SimulatedDevice** project, click **Add**, and then click **Existing Item**.</span></span> <span data-ttu-id="f01e8-132">Navigeer tooan afbeeldingsbestand en deze opnemen in uw project.</span><span class="sxs-lookup"><span data-stu-id="f01e8-132">Navigate tooan image file and include it in your project.</span></span> <span data-ttu-id="f01e8-133">Deze zelfstudie wordt ervan uitgegaan dat Hallo installatiekopie heet `image.jpg`.</span><span class="sxs-lookup"><span data-stu-id="f01e8-133">This tutorial assumes hello image is named `image.jpg`.</span></span>

1. <span data-ttu-id="f01e8-134">Met de rechtermuisknop op de installatiekopie van het Hallo en klik vervolgens op **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="f01e8-134">Right-click on hello image, and then click **Properties**.</span></span> <span data-ttu-id="f01e8-135">Zorg ervoor dat **tooOutput Directory kopiëren** te is ingesteld,**altijd kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="f01e8-135">Make sure that **Copy tooOutput Directory** is set too**Copy always**.</span></span>

    ![][1]

1. <span data-ttu-id="f01e8-136">In Hallo **Program.cs** bestand, het toevoegen van Hallo instructies Hallo boven aan het Hallo-bestand te volgen:</span><span class="sxs-lookup"><span data-stu-id="f01e8-136">In hello **Program.cs** file, add hello following statements at hello top of hello file:</span></span>

    ```csharp
    using System.IO;
    ```

1. <span data-ttu-id="f01e8-137">Hallo na methode toohello toevoegen **programma** klasse:</span><span class="sxs-lookup"><span data-stu-id="f01e8-137">Add hello following method toohello **Program** class:</span></span>

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

    <span data-ttu-id="f01e8-138">Hallo `UploadToBlobAsync` methode neemt in Hallo bestandsnaam en bron van de stroom van Hallo bestand toobe geüpload en Hallo uploaden toostorage verwerkt.</span><span class="sxs-lookup"><span data-stu-id="f01e8-138">hello `UploadToBlobAsync` method takes in hello file name and stream source of hello file toobe uploaded and handles hello upload toostorage.</span></span> <span data-ttu-id="f01e8-139">Hallo-consoletoepassing weergeven Hallo duurt tooupload Hallo-bestand</span><span class="sxs-lookup"><span data-stu-id="f01e8-139">hello console app displays hello time it takes tooupload hello file.</span></span>

1. <span data-ttu-id="f01e8-140">Toevoegen van de volgende methode in Hallo Hallo **Main** methode aan vóór Hallo `Console.ReadLine()` regel:</span><span class="sxs-lookup"><span data-stu-id="f01e8-140">Add hello following method in hello **Main** method, right before hello `Console.ReadLine()` line:</span></span>

    ```csharp
    SendToBlobAsync();
    ```

> [!NOTE]
> <span data-ttu-id="f01e8-141">Deze zelfstudie implementeert voor de eenvoud mogelijk te houden, niet een beleid voor opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="f01e8-141">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="f01e8-142">In productiecode moet u beleid voor opnieuw proberen (zoals exponentieel uitstel), zoals voorgesteld in de MSDN-artikel Hallo implementeren [afhandeling van tijdelijke fout].</span><span class="sxs-lookup"><span data-stu-id="f01e8-142">In production code, you should implement retry policies (such as exponential backoff), as suggested in hello MSDN article [Transient Fault Handling].</span></span>

## <a name="receive-a-file-upload-notification"></a><span data-ttu-id="f01e8-143">Ontvangt een melding van bestand uploaden</span><span class="sxs-lookup"><span data-stu-id="f01e8-143">Receive a file upload notification</span></span>

<span data-ttu-id="f01e8-144">In deze sectie schrijft u een .NET-consoletoepassing die bestand uploaden meldingsberichten uit IoT Hub ontvangt.</span><span class="sxs-lookup"><span data-stu-id="f01e8-144">In this section, you write a .NET console app that receives file upload notification messages from IoT Hub.</span></span>

1. <span data-ttu-id="f01e8-145">Maak in Hallo huidige Visual Studio-oplossing een Visual C# Windows-project met behulp van Hallo **consoletoepassing** projectsjabloon.</span><span class="sxs-lookup"><span data-stu-id="f01e8-145">In hello current Visual Studio solution, create a Visual C# Windows project by using hello **Console Application** project template.</span></span> <span data-ttu-id="f01e8-146">Naam Hallo project **ReadFileUploadNotification**.</span><span class="sxs-lookup"><span data-stu-id="f01e8-146">Name hello project **ReadFileUploadNotification**.</span></span>

    ![Nieuw project in Visual Studio][2]

1. <span data-ttu-id="f01e8-148">Klik in Solution Explorer met de rechtermuisknop op Hallo **ReadFileUploadNotification** project en klik vervolgens op **NuGet-pakketten beheren...** .</span><span class="sxs-lookup"><span data-stu-id="f01e8-148">In Solution Explorer, right-click hello **ReadFileUploadNotification** project, and then click **Manage NuGet Packages...**.</span></span>

1. <span data-ttu-id="f01e8-149">In Hallo **NuGet Package Manager** venster, zoekt u **Microsoft.Azure.Devices**, klikt u op **installeren**, en accepteer de gebruiksvoorwaarden Hallo.</span><span class="sxs-lookup"><span data-stu-id="f01e8-149">In hello **NuGet Package Manager** window, search for **Microsoft.Azure.Devices**, click **Install**, and accept hello terms of use.</span></span>

    <span data-ttu-id="f01e8-150">Deze actie downloadt, installeert en voegt u een verwijzing toohello [Azure IoT service SDK NuGet-pakket] in Hallo **ReadFileUploadNotification** project.</span><span class="sxs-lookup"><span data-stu-id="f01e8-150">This action downloads, installs, and adds a reference toohello [Azure IoT service SDK NuGet package] in hello **ReadFileUploadNotification** project.</span></span>

1. <span data-ttu-id="f01e8-151">In Hallo **Program.cs** bestand, het toevoegen van Hallo instructies Hallo boven aan het Hallo-bestand te volgen:</span><span class="sxs-lookup"><span data-stu-id="f01e8-151">In hello **Program.cs** file, add hello following statements at hello top of hello file:</span></span>

    ```csharp
    using Microsoft.Azure.Devices;
    ```

1. <span data-ttu-id="f01e8-152">Hallo na toohello velden toevoegen **programma** klasse.</span><span class="sxs-lookup"><span data-stu-id="f01e8-152">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="f01e8-153">Vervang de aanduidingswaarde Hallo door Hallo IoT hub-verbindingsreeks uit [aan de slag met IoT Hub]:</span><span class="sxs-lookup"><span data-stu-id="f01e8-153">Substitute hello placeholder value with hello IoT hub connection string from [Get started with IoT Hub]:</span></span>

    ```csharp
    static ServiceClient serviceClient;
    static string connectionString = "{iot hub connection string}";
    ```

1. <span data-ttu-id="f01e8-154">Hallo na methode toohello toevoegen **programma** klasse:</span><span class="sxs-lookup"><span data-stu-id="f01e8-154">Add hello following method toohello **Program** class:</span></span>

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

    <span data-ttu-id="f01e8-155">Opmerking: dit patroon ontvangen is dezelfde één gebruikte tooreceive cloud-naar-apparaat berichten van apparaattoepassing Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="f01e8-155">Note this receive pattern is hello same one used tooreceive cloud-to-device messages from hello device app.</span></span>

1. <span data-ttu-id="f01e8-156">Voeg regels toohello na Hallo **Main** methode:</span><span class="sxs-lookup"><span data-stu-id="f01e8-156">Finally, add hello following lines toohello **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Receive file upload notifications\n");
    serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
    ReceiveFileUploadNotificationAsync();
    Console.WriteLine("Press Enter tooexit\n");
    Console.ReadLine();
    ```

## <a name="run-hello-applications"></a><span data-ttu-id="f01e8-157">Hallo-toepassingen uitvoeren</span><span class="sxs-lookup"><span data-stu-id="f01e8-157">Run hello applications</span></span>

<span data-ttu-id="f01e8-158">U bent nu klaar toorun Hallo toepassingen.</span><span class="sxs-lookup"><span data-stu-id="f01e8-158">Now you are ready toorun hello applications.</span></span>

1. <span data-ttu-id="f01e8-159">Met de rechtermuisknop op uw oplossing in Visual Studio, en selecteer **Set StartUp projects**.</span><span class="sxs-lookup"><span data-stu-id="f01e8-159">In Visual Studio, right-click your solution, and select **Set StartUp projects**.</span></span> <span data-ttu-id="f01e8-160">Selecteer **meerdere opstartprojecten**, selecteer daarna Hallo **Start** actie voor **ReadFileUploadNotification** en **SimulatedDevice**.</span><span class="sxs-lookup"><span data-stu-id="f01e8-160">Select **Multiple startup projects**, then select hello **Start** action for **ReadFileUploadNotification** and **SimulatedDevice**.</span></span>

1. <span data-ttu-id="f01e8-161">Druk op **F5**.</span><span class="sxs-lookup"><span data-stu-id="f01e8-161">Press **F5**.</span></span> <span data-ttu-id="f01e8-162">Beide toepassingen moeten worden gestart.</span><span class="sxs-lookup"><span data-stu-id="f01e8-162">Both applications should start.</span></span> <span data-ttu-id="f01e8-163">U ziet Hallo uploaden is voltooid in één console-app en Hallo upload-melding is ontvangen door Hallo andere console-app.</span><span class="sxs-lookup"><span data-stu-id="f01e8-163">You should see hello upload completed in one console app and hello upload notification message received by hello other console app.</span></span> <span data-ttu-id="f01e8-164">U kunt Hallo [Azure-portal] of Visual Studio Server Explorer toocheck op Hallo aanwezigheid van Hallo geüpload bestand in uw Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="f01e8-164">You can use hello [Azure portal] or Visual Studio Server Explorer toocheck for hello presence of hello uploaded file in your Azure Storage account.</span></span>

    ![][50]

## <a name="next-steps"></a><span data-ttu-id="f01e8-165">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f01e8-165">Next steps</span></span>

<span data-ttu-id="f01e8-166">In deze zelfstudie hebt u geleerd hoe toouse Hallo bestand mogelijkheden van IoT-Hub toosimplify bestand van apparaten uploadt uploaden.</span><span class="sxs-lookup"><span data-stu-id="f01e8-166">In this tutorial, you learned how toouse hello file upload capabilities of IoT Hub toosimplify file uploads from devices.</span></span> <span data-ttu-id="f01e8-167">Scenario's en tooexplore IoT hub-functies kunt u doorgaan met de Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f01e8-167">You can continue tooexplore IoT hub features and scenarios with hello following articles:</span></span>

* <span data-ttu-id="f01e8-168">[Een iothub via een programma maken][lnk-create-hub]</span><span class="sxs-lookup"><span data-stu-id="f01e8-168">[Create an IoT hub programmatically][lnk-create-hub]</span></span>
* <span data-ttu-id="f01e8-169">[Inleiding tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="f01e8-169">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="f01e8-170">[Azure IoT SDK 's][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="f01e8-170">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="f01e8-171">toofurther verkennen Hallo-mogelijkheden van IoT Hub, Zie:</span><span class="sxs-lookup"><span data-stu-id="f01e8-171">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="f01e8-172">[Een apparaat simuleren met IoT rand][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="f01e8-172">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

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
