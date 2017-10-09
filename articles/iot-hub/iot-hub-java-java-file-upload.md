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
# <a name="upload-files-from-your-device-toohello-cloud-with-iot-hub"></a>Uploaden van bestanden van uw apparaat toohello cloud met IoT Hub

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

Deze zelfstudie bouwt voort op Hallo-code in Hallo [Cloud naar apparaat verzenden met IoT Hub](iot-hub-java-java-c2d.md) zelfstudie tooshow u hoe toouse hello [bestand uploaden mogelijkheden van IoT Hub](iot-hub-devguide-file-upload.md) tooupload een bestand te[ Azure-blobopslag](../storage/index.md). Hallo-zelfstudie ziet u hoe aan:

- Veilig een apparaat voorzien van een Azure blob-URI voor het uploaden van een bestand.
- Hallo IoT Hub-bestand uploaden meldingen tootrigger verwerken Hallo-bestand in de back-end van uw app gebruiken.

Hallo [aan de slag met IoT Hub](iot-hub-java-java-getstarted.md) en [Cloud naar apparaat verzenden met IoT Hub](iot-hub-java-java-c2d.md) zelfstudies ziet Hallo apparaat-naar-cloud- en cloud-naar-apparaat messaging basisfunctionaliteit van IoT-Hub. Hallo [proces apparaat-naar-cloudberichten](iot-hub-java-java-process-d2c.md) zelfstudie beschrijft een manier tooreliably store apparaat-naar-cloud-berichten in Azure blob-opslag. In sommige scenario's kan niet u echter gemakkelijk toewijzen hello gegevens verzenden van uw apparaten in hello relatief klein apparaat-naar-cloud-berichten die IoT Hub accepteert. Bijvoorbeeld:

* Grote bestanden met afbeeldingen
* Video's
* Trillingen gegevens dat met hoge frequentie
* Een vorm van voorverwerkte gegevens.

Deze bestanden zijn meestal batch verwerkt in Hallo cloud met hulpprogramma's zoals [Azure Data Factory](../data-factory/index.md) of Hallo [Hadoop](../hdinsight/index.md) stack. Wanneer u tooupland bestanden van een apparaat nodig hebt, kunt u nog steeds Hallo beveiliging en betrouwbaarheid van IoT Hub gebruiken.

Aan Hallo einde van deze zelfstudie kunt u twee Java-apps die console uitvoeren:

* **simulated-device**, een aangepaste versie van het Hallo-app in de zelfstudie Hallo [berichten verzenden Cloud-naar-apparaat met IoT Hub] gemaakt. Deze app uploadt een bestand toostorage met behulp van een SAS-URI geleverd door uw IoT-hub.
* **Lees-bestand-upload-melding**, dat bestand uploaden meldingen ontvangt van uw IoT-hub.

> [!NOTE]
> IoT Hub biedt ondersteuning voor veel apparaatplatforms en talen (inclusief C, .NET en Javascript) via Azure IoT-apparaat SDK's. Raadpleeg toohello [Azure IoT Developer Center] voor stapsgewijze instructies voor het tooconnect uw apparaat tooAzure IoT Hub.

toocomplete in deze zelfstudie, moet u hello te volgen:

* meest recente Hallo [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* Een actief Azure-account. (Als u geen account hebt, kunt u een [gratis account](http://azure.microsoft.com/pricing/free-trial/) binnen een paar minuten.)

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a>Een bestand vanaf een apparaat-app uploaden

In deze sectie maakt u Hallo apparaattoepassing u hebt gemaakt in wijzigen [Cloud naar apparaat verzenden met IoT Hub](iot-hub-java-java-c2d.md) tooupload een bestand tooIoT hub.

1. Kopiëren van een installatiekopie van bestand toohello `simulated-device` map en wijzig de naam `myimage.png`.

1. Met een teksteditor openen Hallo `simulated-device\src\main\java\com\mycompany\app\App.java` bestand.

1. Toevoegen van Hallo variabelendeclaratie toohello **App** klasse:

    ```java
    private static String fileName = "myimage.png";
    ```

1. tooprocess bestand uploaden callback statusberichten, voeg de volgende Hallo geneste klasse toohello **App** klasse:

    ```java
    // Define a callback method tooprint status codes from IoT Hub.
    protected static class FileUploadStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toofile upload for " + fileName
            + " operation with status " + status.name());
      }
    }
    ```

1. tooupload afbeeldingen tooIoT Hub toevoegen na methode toohello hello **App** klasse tooupload afbeeldingen tooIoT Hub:

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

1. Hallo wijzigen **belangrijkste** methode toocall hello **uploadFile** methode, zoals wordt weergegeven in het volgende codefragment Hallo:

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

1. Gebruik Hallo volgende opdracht toobuild hello **simulated-device** app en controleren op fouten:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="receive-a-file-upload-notification"></a>Ontvangt een melding van bestand uploaden

In deze sectie maakt u een Java-consoletoepassing die bestand uploaden meldingsberichten uit IoT Hub ontvangt.

U moet Hallo **iothubowner** connection string voor uw IoT-Hub toocomplete in deze sectie. U vindt Hallo-verbindingsreeks in Hallo [Azure-portal](https://portal.azure.com/) op Hallo **beleid voor gedeelde toegang** blade.

1. Maak een Maven-project aangeroepen **lezen-bestand-upload-melding** met behulp van de volgende opdracht achter de opdrachtprompt Hallo. Houd rekening met dat deze opdracht is een enkele, lange opdracht:

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-file-upload-notification -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

1. Ga bij de opdrachtprompt toohello nieuwe `read-file-upload-notification` map.

1. Met een teksteditor openen Hallo `pom.xml` bestand in Hallo `read-file-upload-notification` map en Voeg na afhankelijkheid toohello hello **afhankelijkheden** knooppunt. Hallo-afhankelijkheid toevoegen kunt u toouse hello **iothub-java-service-client** pakket in uw toepassing toocommunicate met de service van uw IoT-hub:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > U kunt controleren op de meest recente versie van Hallo **iot-service-client** met [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).

1. Opslaan en sluiten Hallo `pom.xml` bestand.

1. Met een teksteditor openen Hallo `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` bestand.

1. Voeg de volgende Hallo **importeren** instructies toohello bestand:

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.concurrent.ExecutorService;
    import java.util.concurrent.Executors;
    ```

1. Hallo klasseniveau variabelen toohello na toevoegen **App** klasse:

    ```java
    private static final String connectionString = "{Your IoT Hub connection string}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    private static FileUploadNotificationReceiver fileUploadNotificationReceiver = null;
    ```

1. informatie over Hallo-bestand uploaden toohello console tooprint Voeg Hallo volgende geneste klasse toohello **App** klasse:

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

1. toostart hello thread die luistert naar bestand uploaden meldingen toevoegen na de code toohello Hallo **belangrijkste** methode:

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

1. Opslaan en sluiten Hallo `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` bestand.

1. Gebruik Hallo volgende opdracht toobuild hello **lezen-bestand-upload-melding** app en controleren op fouten:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-hello-applications"></a>Hallo-toepassingen uitvoeren

U bent nu klaar toorun Hallo toepassingen.

Bij een opdrachtprompt in Hallo `read-file-upload-notification` map Hallo volgende opdracht:

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

Bij een opdrachtprompt in Hallo `simulated-device` map Hallo volgende opdracht:

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

Hallo volgende schermafbeelding ziet u uitvoer van Hallo Hallo **simulated-device** app:

![De uitvoer van de gesimuleerde apparaattoepassing](media/iot-hub-java-java-upload/simulated-device.png)

Hallo volgende schermafbeelding ziet u uitvoer van Hallo Hallo **lezen-bestand-upload-melding** app:

![De uitvoer van de lezen-bestand-upload-melding app](media/iot-hub-java-java-upload/read-file-upload-notification.png)

Hallo portal tooview Hallo geüpload bestand in Hallo-opslagcontainer die u hebt geconfigureerd, kunt u gebruiken:

![Geüploade bestand](media/iot-hub-java-java-upload/uploaded-file.png)

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


