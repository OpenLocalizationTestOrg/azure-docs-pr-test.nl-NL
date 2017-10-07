---
title: aaaCloud-naar-apparaat-berichten met Azure IoT Hub (Java) | Microsoft Docs
description: Hoe berichten toosend cloud-naar-apparaat tooa apparaat van een Azure IoT hub met hello Azure IoT SDK's voor Java. U wijzigt de berichten van een gesimuleerd apparaat app tooreceive cloud-naar-apparaat en wijzigen van een back-endserver voor apps toosend hello cloud-naar-apparaat-berichten.
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 7f785ea8-e7c2-40c5-87ef-96525e9b9e1e
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: dobett
ms.openlocfilehash: 8721f18428c849ed9a04aa2e45c65605c3e38101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-to-device-messages-with-iot-hub-java"></a>Cloud-naar-apparaat-berichten verzenden met IoT Hub (Java)
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

Azure IoT Hub is een volledig beheerde service waarmee stabiele en veilige tweerichtingscommunicatie tussen miljoenen apparaten inschakelen en een back-end oplossing. Hallo [aan de slag met IoT Hub] zelfstudie laat zien hoe toocreate een IoT-hub een apparaat-id in het inrichten en code van een gesimuleerde apparaattoepassing dat apparaat-naar-cloud-berichten verzendt.

Deze zelfstudie bouwt voort op [aan de slag met IoT Hub]. Hier ziet u hoe aan:

* Verzenden van uw back-end oplossing, cloud-naar-apparaatberichten tooa één apparaat via IoT Hub.
* Cloud-naar-apparaat-berichten op een apparaat ontvangen.
* Aanvragen van uw back-end oplossing, levering bevestiging (*feedback*) voor tooa apparaat van de berichten uit IoT Hub.

U vindt meer informatie over cloud-naar-apparaat-berichten in Hallo [Ontwikkelaarshandleiding voor IoT Hub][IoT Hub developer guide - C2D].

Aan het einde van de Hallo van deze zelfstudie, moet u twee Java-apps die console uitvoeren:

* **simulated-device**, een aangepaste versie van het Hallo-app gemaakt in [aan de slag met IoT Hub], die verbinding maakt tooyour IoT-hub en cloud-naar-apparaat-berichten worden ontvangen.
* **verzenden-c2d-berichten**, die een cloud-naar-apparaat bericht toohello gesimuleerde apparaattoepassing via IoT Hub verzendt en ontvangt u vervolgens de bevestiging levering.

> [!NOTE]
> IoT-Hub heeft SDK-ondersteuning voor veel apparaatplatforms en talen (inclusief C, Java en Javascript) via Azure IoT-apparaat-SDK's. Voor stapsgewijze instructies voor hoe tooconnect uw apparaat toothis-zelfstudie code en over het algemeen tooAzure IoT Hub zien Hallo [Azure IoT Developer Center].

toocomplete in deze zelfstudie, moet u hello te volgen:

* Een volledige werkende versie van Hallo [aan de slag met IoT Hub](iot-hub-java-java-getstarted.md) of [proces IoT Hub apparaat-naar-cloud-berichten](iot-hub-java-java-process-d2c.md) zelfstudie.
* meest recente Hallo [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* Een actief Azure-account. (Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)

## <a name="receive-messages-in-hello-simulated-device-app"></a>Berichten ontvangen in de gesimuleerde apparaattoepassing Hallo

In deze sectie maakt u de gesimuleerde apparaattoepassing Hallo u hebt gemaakt in wijzigen [aan de slag met IoT Hub] tooreceive cloud-naar-apparaat-berichten uit Hallo iothub.

1. Met een teksteditor Hallo simulated-device\src\main\java\com\mycompany\app\App.java bestand openen.

2. Voeg de volgende Hallo **MessageCallback** klasse als een geneste klasse binnen Hallo **App** klasse. Hallo **uitvoeren** methode wordt aangeroepen wanneer Hallo apparaat een bericht uit IoT Hub ontvangt. In dit voorbeeld Hallo apparaat altijd een melding Hallo IoT-hub of het Hallo-bericht is voltooid:

    ```java
    private static class AppMessageCallback implements MessageCallback {
      public IotHubMessageResult execute(Message msg, Object context) {
        System.out.println("Received message from hub: "
          + new String(msg.getBytes(), Message.DEFAULT_IOTHUB_MESSAGE_CHARSET));
    
        return IotHubMessageResult.COMPLETE;
      }
    }
    ```
3. Hallo wijzigen **belangrijkste** methode toocreate een **AppMessageCallback** exemplaar en aanroep Hallo **setMessageCallback** methode voordat het Hallo-client als volgt openen:

    ```java
    client = new DeviceClient(connString, protocol);
   
    MessageCallback callback = new AppMessageCallback();
    client.setMessageCallback(callback, null);
    client.open();
    ```

    > [!NOTE]
    > Als u HTTP in plaats van MQTT of AMQP als Hallo transport gebruikt, Hallo **DeviceClient** exemplaar wordt gecontroleerd op berichten uit IoT Hub zelden (minder dan elke 25 minuten). Zie voor meer informatie over Hallo verschillen tussen de protocollen MQTT, AMQP en HTTP-ondersteuning en Iothub beperking Hallo [Ontwikkelaarshandleiding voor IoT Hub][IoT Hub developer guide - C2D].

4. Hallo toobuild **simulated-device** app met behulp van Maven, uitvoeren van de volgende opdracht achter de opdrachtprompt Hallo in de map simulated-device Hallo Hallo:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="send-a-cloud-to-device-message"></a>Een cloud naar apparaat verzenden

In deze sectie maakt maken u een Java-consoletoepassing die cloud-naar-apparaatberichten toohello gesimuleerde apparaattoepassing verzendt. U moet de apparaat-ID van het Hallo-apparaat die u hebt toegevoegd in Hallo Hallo [aan de slag met IoT Hub] zelfstudie. U moet de verbindingsreeks IoT Hub ook Hallo voor uw hub die u in Hallo vinden kunt [Azure-portal].

1. Maak een Maven-project aangeroepen **verzenden-c2d-berichten** met behulp van de volgende opdracht achter de opdrachtprompt Hallo. Houd rekening met dat deze opdracht is een enkele, lange opdracht:

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=send-c2d-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. Navigeer toohello nieuwe verzenden-c2d-berichten map bij de opdrachtprompt.

3. Met een teksteditor, open Hallo pom.xml-bestand in Hallo verzenden-c2d-berichten map en Hallo afhankelijkheid toohello na toevoegen **afhankelijkheden** knooppunt. Hallo-afhankelijkheid toevoegen kunt u toouse hello **iothub-java-service-client** pakket in uw toepassing toocommunicate met de service van uw IoT-hub:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > U kunt controleren op de meest recente versie van Hallo **iot-service-client** met [Maven search][lnk-maven-service-search].

4. Opslaan en sluiten Hallo pom.xml-bestand.

5. Met een teksteditor Hallo send-c2d-messages\src\main\java\com\mycompany\app\App.java bestand openen.

6. Voeg de volgende Hallo **importeren** instructies toohello bestand:

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. Hallo klasseniveau variabelen toohello na toevoegen **App** klasse, Vervang **{yourhubconnectionstring}** en **{yourdeviceid}** Hello waarden uw aangegeven eerder:

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "{yourdeviceid}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    ```

8. Vervang Hallo **belangrijkste** methode Hello code te volgen. Deze code tooyour IoT-hub verbindt, verzendt een bericht tooyour apparaat en wordt er gewacht totdat een bevestiging dat Hallo-bericht ontvangen en verwerken Hallo van apparaat:
   
    ```java
    public static void main(String[] args) throws IOException,
        URISyntaxException, Exception {
      ServiceClient serviceClient = ServiceClient.createFromConnectionString(
        connectionString, protocol);
   
      if (serviceClient != null) {
        serviceClient.open();
        FeedbackReceiver feedbackReceiver = serviceClient
          .getFeedbackReceiver();
        if (feedbackReceiver != null) feedbackReceiver.open();
   
        Message messageToSend = new Message("Cloud toodevice message.");
        messageToSend.setDeliveryAcknowledgement(DeliveryAcknowledgement.Full);
   
        serviceClient.send(deviceId, messageToSend);
        System.out.println("Message sent toodevice");
   
        FeedbackBatch feedbackBatch = feedbackReceiver.receive(10000);
        if (feedbackBatch != null) {
          System.out.println("Message feedback received, feedback time: "
            + feedbackBatch.getEnqueuedTimeUtc().toString());
        }
   
        if (feedbackReceiver != null) feedbackReceiver.close();
        serviceClient.close();
      }
    }
    ```

    > [!NOTE]
    > Deze zelfstudie implementeert voor de eenvoud mogelijk te houden, niet een beleid voor opnieuw proberen. In productiecode moet u beleid voor opnieuw proberen (zoals exponentieel uitstel), zoals voorgesteld in de MSDN-artikel Hallo implementeren [afhandeling van tijdelijke fout].


9. Hallo toobuild **simulated-device** app met behulp van Maven, uitvoeren van de volgende opdracht achter de opdrachtprompt Hallo in de map simulated-device Hallo Hallo:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-hello-applications"></a>Hallo-toepassingen uitvoeren

U bent nu klaar toorun Hallo toepassingen.

1. Uitvoeren bij een opdrachtprompt in de map simulated-device Hallo Hallo opdracht toobegin verzenden van telemetrie tooyour iothub en toolisten voor cloud-naar-apparaat-berichten van uw hub te volgen:

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![De gesimuleerde apparaattoepassing Hallo uitvoeren][img-simulated-device]

2. Voer bij een opdrachtprompt in Hallo verzenden-c2d-berichten map Hallo opdracht toosend na een cloud-naar-apparaat-bericht en de wachttijd voor een bevestiging feedback:

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![Hallo opdracht toosend Hallo-bericht van cloud-naar-apparaat worden uitgevoerd][img-send-command]

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie hebt u geleerd hoe toosend en cloud-naar-apparaat-berichten ontvangen. 

Voorbeelden van volledige end-to-end-oplossingen die gebruikmaken van IoT Hub toosee Zie [Azure IoT Suite].

toolearn meer informatie over het ontwikkelen van oplossingen met IoT Hub, Zie Hallo [Ontwikkelaarshandleiding voor IoT Hub].

<!-- Images -->
[img-simulated-device]: media/iot-hub-java-java-c2d/receivec2d.png
[img-send-command]:  media/iot-hub-java-java-c2d/sendc2d.png
<!-- Links -->

[aan de slag met IoT Hub]: iot-hub-java-java-getstarted.md
[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md
[Ontwikkelaarshandleiding voor IoT Hub]: iot-hub-devguide.md
[Azure IoT Developer Center]: http://www.azure.com/develop/iot
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java
[afhandeling van tijdelijke fout]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[Azure-portal]: https://portal.azure.com
[Azure IoT Suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22