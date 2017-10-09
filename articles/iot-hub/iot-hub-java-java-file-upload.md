---
title: aaaUpload bestanden van apparaten tooAzure IoT Hub met Java | Microsoft Docs
description: "Hoe tooupload bestanden van een apparaat toohello cloud met Azure IoT-device SDK voor Java. Geüploade bestanden worden opgeslagen in een Azure storage-blob-container."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4759d229-f856-4526-abda-414f8b00a56d
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: dobett
ms.openlocfilehash: e305fe61bf7ca0aeb2c092bc2c7efebdc78d4f68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-from-your-device-toohello-cloud-with-iot-hub"></a><span data-ttu-id="c203a-104">Uploaden van bestanden van uw apparaat toohello cloud met IoT Hub</span><span class="sxs-lookup"><span data-stu-id="c203a-104">Upload files from your device toohello cloud with IoT Hub</span></span>

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

<span data-ttu-id="c203a-105">Deze zelfstudie bouwt voort op Hallo-code in Hallo [Cloud naar apparaat verzenden met IoT Hub](iot-hub-java-java-c2d.md) zelfstudie tooshow u hoe toouse hello [bestand uploaden mogelijkheden van IoT Hub](iot-hub-devguide-file-upload.md) tooupload een bestand te[ Azure-blobopslag](../storage/index.md).</span><span class="sxs-lookup"><span data-stu-id="c203a-105">This tutorial builds on hello code in hello [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) tutorial tooshow you how toouse hello [file upload capabilities of IoT Hub](iot-hub-devguide-file-upload.md) tooupload a file too[Azure blob storage](../storage/index.md).</span></span> <span data-ttu-id="c203a-106">Hallo-zelfstudie ziet u hoe aan:</span><span class="sxs-lookup"><span data-stu-id="c203a-106">hello tutorial shows you how to:</span></span>

- <span data-ttu-id="c203a-107">Veilig een apparaat voorzien van een Azure blob-URI voor het uploaden van een bestand.</span><span class="sxs-lookup"><span data-stu-id="c203a-107">Securely provide a device with an Azure blob URI for uploading a file.</span></span>
- <span data-ttu-id="c203a-108">Hallo IoT Hub-bestand uploaden meldingen tootrigger verwerken Hallo-bestand in de back-end van uw app gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c203a-108">Use hello IoT Hub file upload notifications tootrigger processing hello file in your app back end.</span></span>

<span data-ttu-id="c203a-109">Hallo [aan de slag met IoT Hub](iot-hub-java-java-getstarted.md) en [Cloud naar apparaat verzenden met IoT Hub](iot-hub-java-java-c2d.md) zelfstudies ziet Hallo apparaat-naar-cloud- en cloud-naar-apparaat messaging basisfunctionaliteit van IoT-Hub.</span><span class="sxs-lookup"><span data-stu-id="c203a-109">hello [Get started with IoT Hub](iot-hub-java-java-getstarted.md) and [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) tutorials show hello basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span> <span data-ttu-id="c203a-110">Hallo [proces apparaat-naar-cloudberichten](iot-hub-java-java-process-d2c.md) zelfstudie beschrijft een manier tooreliably store apparaat-naar-cloud-berichten in Azure blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="c203a-110">hello [Process Device-to-Cloud messages](iot-hub-java-java-process-d2c.md) tutorial describes a way tooreliably store device-to-cloud messages in Azure blob storage.</span></span> <span data-ttu-id="c203a-111">In sommige scenario's kan niet u echter gemakkelijk toewijzen hello gegevens verzenden van uw apparaten in hello relatief klein apparaat-naar-cloud-berichten die IoT Hub accepteert.</span><span class="sxs-lookup"><span data-stu-id="c203a-111">However, in some scenarios you cannot easily map hello data your devices send into hello relatively small device-to-cloud messages that IoT Hub accepts.</span></span> <span data-ttu-id="c203a-112">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="c203a-112">For example:</span></span>

* <span data-ttu-id="c203a-113">Grote bestanden met afbeeldingen</span><span class="sxs-lookup"><span data-stu-id="c203a-113">Large files that contain images</span></span>
* <span data-ttu-id="c203a-114">Video's</span><span class="sxs-lookup"><span data-stu-id="c203a-114">Videos</span></span>
* <span data-ttu-id="c203a-115">Trillingen gegevens dat met hoge frequentie</span><span class="sxs-lookup"><span data-stu-id="c203a-115">Vibration data sampled at high frequency</span></span>
* <span data-ttu-id="c203a-116">Een vorm van voorverwerkte gegevens.</span><span class="sxs-lookup"><span data-stu-id="c203a-116">Some form of preprocessed data.</span></span>

<span data-ttu-id="c203a-117">Deze bestanden zijn meestal batch verwerkt in Hallo cloud met hulpprogramma's zoals [Azure Data Factory](../data-factory/index.md) of Hallo [Hadoop](../hdinsight/index.md) stack.</span><span class="sxs-lookup"><span data-stu-id="c203a-117">These files are typically batch processed in hello cloud using tools such as [Azure Data Factory](../data-factory/index.md) or hello [Hadoop](../hdinsight/index.md) stack.</span></span> <span data-ttu-id="c203a-118">Wanneer u tooupland bestanden van een apparaat nodig hebt, kunt u nog steeds Hallo beveiliging en betrouwbaarheid van IoT Hub gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c203a-118">When you need tooupland files from a device, you can still use hello security and reliability of IoT Hub.</span></span>

<span data-ttu-id="c203a-119">Aan Hallo einde van deze zelfstudie kunt u twee Java-apps die console uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="c203a-119">At hello end of this tutorial you run two Java console apps:</span></span>

* <span data-ttu-id="c203a-120">**simulated-device**, een aangepaste versie van het Hallo-app in de zelfstudie Hallo [berichten verzenden Cloud-naar-apparaat met IoT Hub] gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c203a-120">**simulated-device**, a modified version of hello app created in hello [Send Cloud-to-Device messages with IoT Hub] tutorial.</span></span> <span data-ttu-id="c203a-121">Deze app uploadt een bestand toostorage met behulp van een SAS-URI geleverd door uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="c203a-121">This app uploads a file toostorage using a SAS URI provided by your IoT hub.</span></span>
* <span data-ttu-id="c203a-122">**Lees-bestand-upload-melding**, dat bestand uploaden meldingen ontvangt van uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="c203a-122">**read-file-upload-notification**, which receives file upload notifications from your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="c203a-123">IoT Hub biedt ondersteuning voor veel apparaatplatforms en talen (inclusief C, .NET en Javascript) via Azure IoT-apparaat SDK's.</span><span class="sxs-lookup"><span data-stu-id="c203a-123">IoT Hub supports many device platforms and languages (including C, .NET, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="c203a-124">Raadpleeg toohello [Azure IoT Developer Center] voor stapsgewijze instructies voor het tooconnect uw apparaat tooAzure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c203a-124">Refer toohello [Azure IoT Developer Center] for step-by-step instructions on how tooconnect your device tooAzure IoT Hub.</span></span>

<span data-ttu-id="c203a-125">toocomplete in deze zelfstudie, moet u hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="c203a-125">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="c203a-126">meest recente Hallo [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="c203a-126">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="c203a-127">Maven 3</span><span class="sxs-lookup"><span data-stu-id="c203a-127">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="c203a-128">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="c203a-128">An active Azure account.</span></span> <span data-ttu-id="c203a-129">(Als u geen account hebt, kunt u een [gratis account](http://azure.microsoft.com/pricing/free-trial/) binnen een paar minuten.)</span><span class="sxs-lookup"><span data-stu-id="c203a-129">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a><span data-ttu-id="c203a-130">Een bestand vanaf een apparaat-app uploaden</span><span class="sxs-lookup"><span data-stu-id="c203a-130">Upload a file from a device app</span></span>

<span data-ttu-id="c203a-131">In deze sectie maakt u Hallo apparaattoepassing u hebt gemaakt in wijzigen [Cloud naar apparaat verzenden met IoT Hub](iot-hub-java-java-c2d.md) tooupload een bestand tooIoT hub.</span><span class="sxs-lookup"><span data-stu-id="c203a-131">In this section, you modify hello device app you created in [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) tooupload a file tooIoT hub.</span></span>

1. <span data-ttu-id="c203a-132">Kopiëren van een installatiekopie van bestand toohello `simulated-device` map en wijzig de naam `myimage.png`.</span><span class="sxs-lookup"><span data-stu-id="c203a-132">Copy an image file toohello `simulated-device` folder and rename it `myimage.png`.</span></span>

1. <span data-ttu-id="c203a-133">Met een teksteditor openen Hallo `simulated-device\src\main\java\com\mycompany\app\App.java` bestand.</span><span class="sxs-lookup"><span data-stu-id="c203a-133">Using a text editor, open hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="c203a-134">Toevoegen van Hallo variabelendeclaratie toohello **App** klasse:</span><span class="sxs-lookup"><span data-stu-id="c203a-134">Add hello variable declaration toohello **App** class:</span></span>

    ```java
    private static String fileName = "myimage.png";
    ```

1. <span data-ttu-id="c203a-135">tooprocess bestand uploaden callback statusberichten, voeg de volgende Hallo geneste klasse toohello **App** klasse:</span><span class="sxs-lookup"><span data-stu-id="c203a-135">tooprocess file upload status callback messages, add hello following nested class toohello **App** class:</span></span>

    ```java
    // Define a callback method tooprint status codes from IoT Hub.
    protected static class FileUploadStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toofile upload for " + fileName
            + " operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="c203a-136">tooupload afbeeldingen tooIoT Hub toevoegen na methode toohello hello **App** klasse tooupload afbeeldingen tooIoT Hub:</span><span class="sxs-lookup"><span data-stu-id="c203a-136">tooupload images tooIoT Hub, add hello following method toohello **App** class tooupload images tooIoT Hub:</span></span>

    ```java
    // Use IoT Hub tooupload a file asynchronously tooAzure blob storage.
    private static void uploadFile(String fullFileName) throws FileNotFoundException, IOException
    {
      File file = new File(fullFileName);
      InputStream inputStream = new FileInputStream(file);
      long streamLength = file.length();

      client.uploadToBlobAsync(fileName, inputStream, streamLength, new FileUploadStatusCallBack(), null);
    }
    ```

1. <span data-ttu-id="c203a-137">Hallo wijzigen **belangrijkste** methode toocall hello **uploadFile** methode, zoals wordt weergegeven in het volgende codefragment Hallo:</span><span class="sxs-lookup"><span data-stu-id="c203a-137">Modify hello **main** method toocall hello **uploadFile** method as shown in hello following snippet:</span></span>

    ```java
    client.open();

    try
    {
      // Get hello filename and start hello upload.
      String fullFileName = System.getProperty("user.dir") + File.separator + fileName;
      uploadFile(fullFileName);
      System.out.println("File upload started with success");
    }
    catch (Exception e)
    {
      System.out.println("Exception uploading file: " + e.getCause() + " \nERROR: " + e.getMessage());
    }

    MessageSender sender = new MessageSender();
    ```

1. <span data-ttu-id="c203a-138">Gebruik Hallo volgende opdracht toobuild hello **simulated-device** app en controleren op fouten:</span><span class="sxs-lookup"><span data-stu-id="c203a-138">Use hello following command toobuild hello **simulated-device** app and check for errors:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="receive-a-file-upload-notification"></a><span data-ttu-id="c203a-139">Ontvangt een melding van bestand uploaden</span><span class="sxs-lookup"><span data-stu-id="c203a-139">Receive a file upload notification</span></span>

<span data-ttu-id="c203a-140">In deze sectie maakt u een Java-consoletoepassing die bestand uploaden meldingsberichten uit IoT Hub ontvangt.</span><span class="sxs-lookup"><span data-stu-id="c203a-140">In this section, you create a Java console app that receives file upload notification messages from IoT Hub.</span></span>

<span data-ttu-id="c203a-141">U moet Hallo **iothubowner** connection string voor uw IoT-Hub toocomplete in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="c203a-141">You need hello **iothubowner** connection string for your IoT Hub toocomplete this section.</span></span> <span data-ttu-id="c203a-142">U vindt Hallo-verbindingsreeks in Hallo [Azure-portal](https://portal.azure.com/) op Hallo **beleid voor gedeelde toegang** blade.</span><span class="sxs-lookup"><span data-stu-id="c203a-142">You can find hello connection string in hello [Azure portal](https://portal.azure.com/) on hello **Shared access policy** blade.</span></span>

1. <span data-ttu-id="c203a-143">Maak een Maven-project aangeroepen **lezen-bestand-upload-melding** met behulp van de volgende opdracht achter de opdrachtprompt Hallo.</span><span class="sxs-lookup"><span data-stu-id="c203a-143">Create a Maven project called **read-file-upload-notification** using hello following command at your command prompt.</span></span> <span data-ttu-id="c203a-144">Houd rekening met dat deze opdracht is een enkele, lange opdracht:</span><span class="sxs-lookup"><span data-stu-id="c203a-144">Note this command is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-file-upload-notification -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

1. <span data-ttu-id="c203a-145">Ga bij de opdrachtprompt toohello nieuwe `read-file-upload-notification` map.</span><span class="sxs-lookup"><span data-stu-id="c203a-145">At your command prompt, navigate toohello new `read-file-upload-notification` folder.</span></span>

1. <span data-ttu-id="c203a-146">Met een teksteditor openen Hallo `pom.xml` bestand in Hallo `read-file-upload-notification` map en Voeg na afhankelijkheid toohello hello **afhankelijkheden** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="c203a-146">Using a text editor, open hello `pom.xml` file in hello `read-file-upload-notification` folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="c203a-147">Hallo-afhankelijkheid toevoegen kunt u toouse hello **iothub-java-service-client** pakket in uw toepassing toocommunicate met de service van uw IoT-hub:</span><span class="sxs-lookup"><span data-stu-id="c203a-147">Adding hello dependency enables you toouse hello **iothub-java-service-client** package in your application toocommunicate with your IoT hub service:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="c203a-148">U kunt controleren op de meest recente versie van Hallo **iot-service-client** met [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="c203a-148">You can check for hello latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="c203a-149">Opslaan en sluiten Hallo `pom.xml` bestand.</span><span class="sxs-lookup"><span data-stu-id="c203a-149">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="c203a-150">Met een teksteditor openen Hallo `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` bestand.</span><span class="sxs-lookup"><span data-stu-id="c203a-150">Using a text editor, open hello `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="c203a-151">Voeg de volgende Hallo **importeren** instructies toohello bestand:</span><span class="sxs-lookup"><span data-stu-id="c203a-151">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.concurrent.ExecutorService;
    import java.util.concurrent.Executors;
    ```

1. <span data-ttu-id="c203a-152">Hallo klasseniveau variabelen toohello na toevoegen **App** klasse:</span><span class="sxs-lookup"><span data-stu-id="c203a-152">Add hello following class-level variables toohello **App** class:</span></span>

    ```java
    private static final String connectionString = "{Your IoT Hub connection string}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    private static FileUploadNotificationReceiver fileUploadNotificationReceiver = null;
    ```

1. <span data-ttu-id="c203a-153">informatie over Hallo-bestand uploaden toohello console tooprint Voeg Hallo volgende geneste klasse toohello **App** klasse:</span><span class="sxs-lookup"><span data-stu-id="c203a-153">tooprint information about hello file upload toohello console, add hello following nested class toohello **App** class:</span></span>

    ```java
    // Create a thread tooreceive file upload notifications.
    private static class ShowFileUploadNotifications implements Runnable {
      public void run() {
        try {
          while (true) {
            System.out.println("Recieve file upload notifications...");
            FileUploadNotification fileUploadNotification = fileUploadNotificationReceiver.receive();
            if (fileUploadNotification != null) {
              System.out.println("File Upload notification received");
              System.out.println("Device Id : " + fileUploadNotification.getDeviceId());
              System.out.println("Blob Uri: " + fileUploadNotification.getBlobUri());
              System.out.println("Blob Name: " + fileUploadNotification.getBlobName());
              System.out.println("Last Updated : " + fileUploadNotification.getLastUpdatedTimeDate());
              System.out.println("Blob Size (Bytes): " + fileUploadNotification.getBlobSizeInBytes());
              System.out.println("Enqueued Time: " + fileUploadNotification.getEnqueuedTimeUtcDate());
            }
          }
        } catch (Exception ex) {
          System.out.println("Exception reading reported properties: " + ex.getMessage());
        }
      }
    }
    ```

1. <span data-ttu-id="c203a-154">toostart hello thread die luistert naar bestand uploaden meldingen toevoegen na de code toohello Hallo **belangrijkste** methode:</span><span class="sxs-lookup"><span data-stu-id="c203a-154">toostart hello thread that listens for file upload notifications, add hello following code toohello **main** method:</span></span>

    ```java
    public static void main(String[] args) throws IOException, URISyntaxException, Exception {
      ServiceClient serviceClient = ServiceClient.createFromConnectionString(connectionString, protocol);

      if (serviceClient != null) {
        serviceClient.open();

        // Get a file upload notification receiver from hello ServiceClient.
        fileUploadNotificationReceiver = serviceClient.getFileUploadNotificationReceiver();
        fileUploadNotificationReceiver.open();

        // Start hello thread tooreceive file upload notifications.
        ShowFileUploadNotifications showFileUploadNotifications = new ShowFileUploadNotifications();
        ExecutorService executor = Executors.newFixedThreadPool(1);
        executor.execute(showFileUploadNotifications);

        System.out.println("Press ENTER tooexit.");
        System.in.read();
        executor.shutdownNow();
        System.out.println("Shutting down sample...");
        fileUploadNotificationReceiver.close();
        serviceClient.close();
      }
    }
    ```

1. <span data-ttu-id="c203a-155">Opslaan en sluiten Hallo `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` bestand.</span><span class="sxs-lookup"><span data-stu-id="c203a-155">Save and close hello `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="c203a-156">Gebruik Hallo volgende opdracht toobuild hello **lezen-bestand-upload-melding** app en controleren op fouten:</span><span class="sxs-lookup"><span data-stu-id="c203a-156">Use hello following command toobuild hello **read-file-upload-notification** app and check for errors:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-hello-applications"></a><span data-ttu-id="c203a-157">Hallo-toepassingen uitvoeren</span><span class="sxs-lookup"><span data-stu-id="c203a-157">Run hello applications</span></span>

<span data-ttu-id="c203a-158">U bent nu klaar toorun Hallo toepassingen.</span><span class="sxs-lookup"><span data-stu-id="c203a-158">Now you are ready toorun hello applications.</span></span>

<span data-ttu-id="c203a-159">Bij een opdrachtprompt in Hallo `read-file-upload-notification` map Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="c203a-159">At a command prompt in hello `read-file-upload-notification` folder, run hello following command:</span></span>

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

<span data-ttu-id="c203a-160">Bij een opdrachtprompt in Hallo `simulated-device` map Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="c203a-160">At a command prompt in hello `simulated-device` folder, run hello following command:</span></span>

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

<span data-ttu-id="c203a-161">Hallo volgende schermafbeelding ziet u uitvoer van Hallo Hallo **simulated-device** app:</span><span class="sxs-lookup"><span data-stu-id="c203a-161">hello following screenshot shows hello output from hello **simulated-device** app:</span></span>

![De uitvoer van de gesimuleerde apparaattoepassing](media/iot-hub-java-java-upload/simulated-device.png)

<span data-ttu-id="c203a-163">Hallo volgende schermafbeelding ziet u uitvoer van Hallo Hallo **lezen-bestand-upload-melding** app:</span><span class="sxs-lookup"><span data-stu-id="c203a-163">hello following screenshot shows hello output from hello **read-file-upload-notification** app:</span></span>

![De uitvoer van de lezen-bestand-upload-melding app](media/iot-hub-java-java-upload/read-file-upload-notification.png)

<span data-ttu-id="c203a-165">Hallo portal tooview Hallo geüpload bestand in Hallo-opslagcontainer die u hebt geconfigureerd, kunt u gebruiken:</span><span class="sxs-lookup"><span data-stu-id="c203a-165">You can use hello portal tooview hello uploaded file in hello storage container you configured:</span></span>

![Geüploade bestand](media/iot-hub-java-java-upload/uploaded-file.png)

## <a name="next-steps"></a><span data-ttu-id="c203a-167">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c203a-167">Next steps</span></span>

<span data-ttu-id="c203a-168">In deze zelfstudie hebt u geleerd hoe toouse Hallo bestand mogelijkheden van IoT-Hub toosimplify bestand van apparaten uploadt uploaden.</span><span class="sxs-lookup"><span data-stu-id="c203a-168">In this tutorial, you learned how toouse hello file upload capabilities of IoT Hub toosimplify file uploads from devices.</span></span> <span data-ttu-id="c203a-169">Scenario's en tooexplore IoT hub-functies kunt u doorgaan met de Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c203a-169">You can continue tooexplore IoT hub features and scenarios with hello following articles:</span></span>

* <span data-ttu-id="c203a-170">[Een iothub via een programma maken][lnk-create-hub]</span><span class="sxs-lookup"><span data-stu-id="c203a-170">[Create an IoT hub programmatically][lnk-create-hub]</span></span>
* <span data-ttu-id="c203a-171">[Inleiding tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="c203a-171">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="c203a-172">[Azure IoT SDK 's][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="c203a-172">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="c203a-173">toofurther verkennen Hallo-mogelijkheden van IoT Hub, Zie:</span><span class="sxs-lookup"><span data-stu-id="c203a-173">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="c203a-174">[Een apparaat simuleren met IoT rand][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="c203a-174">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

<!-- Images. -->

[50]: ./media/iot-hub-csharp-csharp-file-upload/run-apps1.png
[1]: ./media/iot-hub-csharp-csharp-file-upload/image-properties.png
[2]: ./media/iot-hub-csharp-csharp-file-upload/file-upload-project-csharp1.png
[3]: ./media/iot-hub-csharp-csharp-file-upload/enable-file-notifications.png

<!-- Links -->



[Azure IoT Developer Center]: http://www.azure.com/develop/iot

[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[Azure Storage]:../storage/common/storage-create-storage-account.md#create-a-storage-account
[lnk-configure-upload]: iot-hub-configure-file-upload.md
[Azure IoT service SDK NuGet package]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-windows-iot-edge-simulated-device.md


