---
title: aaaGet de slag met Azure IoT Hub (Java) | Microsoft Docs
description: Meer informatie over hoe toosend apparaat-naar-cloud tooAzure IoT Hub met IoT SDK's voor Java berichten. Gesimuleerde apparaat en service-apps tooregister uw apparaat maken en berichten uit iothub berichten verzenden.
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 70dae4a8-0e98-4c53-b5a5-9d6963abb245
ms.service: iot-hub
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac954f0522b46ed2a5b4a819bc611c13be0b9a9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-tooyour-iot-hub-using-java"></a>Verbinding maken met uw apparaat tooyour iothub met Java
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

Aan het einde van de Hallo van deze zelfstudie hebt u drie Java-apps die console:

* **Create-device-identity**, die een apparaat-id maakt en gekoppelde beveiliging sleutel tooconnect app op uw apparaat.
* **Read-d2c-messages**, weergeven met Hallo telemetrie verzonden door de app op uw apparaat.
* **simulated-device**, die tooyour IoT-hub aan Hallo apparaat-id eerder hebt gemaakt, en verzendt een elke tweede met behulp van protocollen MQTT protocol Hallo telemetrie-bericht.

> [!NOTE]
> Hallo artikel [Azure IoT SDK's] [ lnk-hub-sdks] bevat informatie over hello Azure IoT SDK's waarmee u toobuild beide toorun apps op apparaten en de back-end van uw oplossing kunt.

toocomplete in deze zelfstudie, moet u hello te volgen:

* meest recente Hallo [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) 
* [Maven 3](https://maven.apache.org/install.html) 
* Een actief Azure-account. (Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

Als een laatste stap Noteer Hallo **primaire sleutel** waarde. Klik vervolgens op **eindpunten** en Hallo **gebeurtenissen** ingebouwd eindpunt. Op Hallo **eigenschappen** blade, maakt u een notitie van Hallo **Event Hub-compatibele naam** en Hallo **Event Hub-compatibele eindpunt** adres. U hebt deze drie waarden nodig wanneer u uw **read-d2c-messages**-app maakt.

![Blade IoT Hub-berichten in Azure Portal][6]

U hebt nu uw IoT-hub gemaakt. U hebt Hallo IoT Hub-hostnaam, verbindingsreeks IoT Hub, primaire sleutel van IoT Hub, Event Hub-compatibele naam en Event Hub-compatibele eindpunt u toocomplete in deze zelfstudie nodig.

## <a name="create-a-device-identity"></a>Een apparaat-id maken
In deze sectie maakt maken u een Java-consoletoepassing die een apparaat-id in Hallo identiteitenregister van uw IoT-hub maakt. Een apparaat kan geen verbinding tooIoT hub maken, tenzij er een vermelding in het identiteitenregister Hallo. Zie voor meer informatie, Hallo **Identiteitsregister** sectie Hallo [Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide-identity]. Wanneer u deze consoletoepassing uitvoert, wordt een unieke apparaat-ID gegenereerd en sleutel waarmee het apparaat tooidentify zelf kunt wanneer het apparaat-naar-cloud verzendt berichten tooIoT Hub.

1. Maak een lege map genaamd iot-java-get-started. Maak een Maven-project aangeroepen in Hallo iot-java-get-started map **create-device-identity** met behulp van de volgende opdracht achter de opdrachtprompt Hallo. Let op: dit is één enkele, lange opdracht:

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=create-device-identity -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. Navigeer toohello create-device-identity-map bij de opdrachtprompt.

3. Met een teksteditor, open Hallo pom.xml-bestand in Hallo create-device-identity-map en Hallo afhankelijkheid toohello na toevoegen **afhankelijkheden** knooppunt. Deze afhankelijkheid kunt u toouse Hallo iot-service-client-pakket in uw app:

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

5. Met een teksteditor Hallo create-device-identity\src\main\java\com\mycompany\app\App.java bestand openen.

6. Voeg de volgende Hallo **importeren** instructies toohello bestand:

    ```java
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;
    import com.microsoft.azure.sdk.iot.service.Device;
    import com.microsoft.azure.sdk.iot.service.RegistryManager;
   
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. Hallo klasseniveau variabelen toohello na toevoegen **App** klasse, Vervang **{yourhubconnectionstring}** Hello waarde uw aangegeven eerder:

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "myFirstJavaDevice";
    ```
[!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

8. Wijzig de handtekening Hallo Hallo **belangrijkste** methode tooinclude Hallo uitzonderingen als volgt:

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException, Exception
    ```

9. Toevoegen na de code als de berichttekst Hallo HALLO hallo **belangrijkste** methode. Deze code maakt een apparaat in het identiteitsregister van de IoT Hub dat *javadevice* heet als dit nog niet bestaat. Vervolgens wordt weergegeven Hallo apparaat-ID en sleutel die u later nodig:

    ```java
    RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);
RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);

    // Create a device that's enabled by default, 
    // with an autogenerated key.
    Device device = Device.createFromId(deviceId, null, null);
    try {
      device = registryManager.addDevice(device);
    } catch (IotHubException iote) {
      // If hello device already exists.
      try {
        device = registryManager.getDevice(deviceId);
      } catch (IotHubException iotf) {
        iotf.printStackTrace();
      }
    }

    // Display information about the
    // device you created.
    System.out.println("Device Id: " + device.getDeviceId());
    System.out.println("Device key: " + device.getPrimaryKey());
    // Create a device that's enabled by default, 
    // with an autogenerated key.
    Device device = Device.createFromId(deviceId, null, null);
    try {
      device = registryManager.addDevice(device);
    } catch (IotHubException iote) {
      // If hello device already exists.
      try {
        device = registryManager.getDevice(deviceId);
      } catch (IotHubException iotf) {
        iotf.printStackTrace();
      }
    }

    // Display information about the
    // device you created.
    System.out.println("Device Id: " + device.getDeviceId());
    System.out.println("Device key: " + device.getPrimaryKey());
    ```

10. Opslaan en sluiten Hallo App.java bestand.

11. Hallo toobuild **create-device-identity** app met behulp van Maven, uitvoeren van de volgende opdracht achter de opdrachtprompt Hallo in Hallo create-device-identity map Hallo:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

12. Hallo toorun **create-device-identity** app met behulp van Maven, uitvoeren van de volgende opdracht achter de opdrachtprompt Hallo in Hallo create-device-identity map Hallo:

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

13. Maak een notitie van Hallo **apparaat-ID** en **apparaatsleutel**. U moet deze waarden later bij het maken van een app die tooIoT Hub als apparaat verbinding maakt.

> [!NOTE]
> Hallo id-register IoT Hub bewaart alleen apparaat-id's tooenable veilige toegang toohello IoT-hub. Apparaat-id's en sleutels toouse worden opgeslagen als beveiligingsreferenties en waarmee u toodisable toegang tot een afzonderlijk apparaat kunt vlag voor ingeschakeld/uitgeschakeld. Als uw app toostore andere apparaatspecifieke metagegevens moet, moet deze een app-specifiek store gebruiken. Zie voor meer informatie, Hallo [Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide-identity].

## <a name="receive-device-to-cloud-messages"></a>Apparaat-naar-cloud-berichten ontvangen

In dit gedeelte maakt u een Java-consoletoepassing die apparaat-naar-cloud-berichten uit IoT Hub kan lezen. Een iothub toont een [Event Hub][lnk-event-hubs-overview]-compatibel eindpunt tooenable u tooread apparaat-naar-cloud-berichten. tookeep dingen eenvoudige, deze zelfstudie maakt u een basislezer die niet geschikt voor een implementatie met hoge doorvoer. Hallo [apparaat-naar-cloud-berichten verwerken] [ lnk-process-d2c-tutorial] zelfstudie laat zien hoe tooprocess apparaat-naar-cloud-berichten op grote schaal. Hallo [aan de slag met Event Hubs] [ lnk-eventhubs-tutorial] zelfstudie bevat meer informatie over hoe tooprocess van berichten van Event Hubs en toepasselijke toohello IoT Hub Event Hub-compatibele eindpunten is.

> [!NOTE]
> Hallo Event Hub-compatibele eindpunt voor het lezen van apparaat-naar-cloudberichten altijd gebruikt Hallo AMQP-protocol.

1. In Hallo map iot-java-get-started die u hebt gemaakt in Hallo *maken van een apparaat-id* sectie, maakt u een Maven-project aangeroepen **read-d2c-messages** met behulp van de volgende opdracht achter de opdrachtprompt Hallo. Let op: dit is één enkele, lange opdracht:

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-d2c-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. Navigeer toohello read-d2c-messages map bij de opdrachtprompt.

3. Met een teksteditor, open Hallo pom.xml-bestand in Hallo read-d2c-messages map en Hallo afhankelijkheid toohello na toevoegen **afhankelijkheden** knooppunt. Deze afhankelijkheid kunt u toouse hello eventhubs-client-pakket in uw app tooread van Hallo Event Hub-compatibele eindpunt:

    ```xml
    <dependency> 
        <groupId>com.microsoft.azure</groupId> 
        <artifactId>azure-eventhubs</artifactId> 
        <version>0.13.0</version> 
    </dependency>
    ```

4. Opslaan en sluiten Hallo pom.xml-bestand.

5. Met een teksteditor Hallo read-d2c-messages\src\main\java\com\mycompany\app\App.java bestand openen.

6. Voeg de volgende Hallo **importeren** instructies toohello bestand:

    ```java
    import java.io.IOException;
    import com.microsoft.azure.eventhubs.*;
    import com.microsoft.azure.servicebus.*;

    import java.nio.charset.Charset;
    import java.time.*;
    import java.util.function.*;
    ```

7. Hallo klasseniveau variabele toohello na toevoegen **App** klasse. Vervang **{youriothubkey}**, **{youreventhubcompatibleendpoint}**, en **{youreventhubcompatiblename}** met Hallo-waarden die u eerder hebt genoteerd:

    ```java
    private static String connStr = "Endpoint={youreventhubcompatibleendpoint};EntityPath={youreventhubcompatiblename};SharedAccessKeyName=iothubowner;SharedAccessKey={youriothubkey}";
    ```

8. Voeg de volgende Hallo **receiveMessages** methode toohello **App** klasse. Deze methode maakt u een **EventHubClient** tooconnect toohello Event Hub-compatibele eindpunt-instantie en vervolgens maakt u asynchroon een **PartitionReceiver** tooread exemplaar van een Event Hub partitie. Dit wordt continu uitgevoerd en Hallo berichtgegevens worden afgedrukt totdat het Hallo-app wordt beëindigd.

    ```java
    // Create a receiver on a partition.
    private static EventHubClient receiveMessages(final String partitionId) {
      EventHubClient client = null;
      try {
        client = EventHubClient.createFromConnectionStringSync(connStr);
      } catch (Exception e) {
        System.out.println("Failed toocreate client: " + e.getMessage());
        System.exit(1);
      }
      try {
        // Create a receiver using the
        // default Event Hubs consumer group
        // that listens for messages from now on.
        client.createReceiver(EventHubClient.DEFAULT_CONSUMER_GROUP_NAME, partitionId, Instant.now())
          .thenAccept(new Consumer<PartitionReceiver>() {
            public void accept(PartitionReceiver receiver) {
              System.out.println("** Created receiver on partition " + partitionId);
              try {
                while (true) {
                  Iterable<EventData> receivedEvents = receiver.receive(100).get();
                  int batchSize = 0;
                  if (receivedEvents != null) {
                    System.out.println("Got some evenst");
                    for (EventData receivedEvent : receivedEvents) {
                      System.out.println(String.format("Offset: %s, SeqNo: %s, EnqueueTime: %s",
                        receivedEvent.getSystemProperties().getOffset(),
                        receivedEvent.getSystemProperties().getSequenceNumber(),
                        receivedEvent.getSystemProperties().getEnqueuedTime()));
                      System.out.println(String.format("| Device ID: %s",
                        receivedEvent.getSystemProperties().get("iothub-connection-device-id")));
                      System.out.println(String.format("| Message Payload: %s",
                        new String(receivedEvent.getBytes(), Charset.defaultCharset())));
                      batchSize++;
                    }
                  }
                  System.out.println(String.format("Partition: %s, ReceivedBatch Size: %s", partitionId, batchSize));
                }
              } catch (Exception e) {
                System.out.println("Failed tooreceive messages: " + e.getMessage());
              }
            }
          });
        } catch (Exception e) {
          System.out.println("Failed toocreate receiver: " + e.getMessage());
      }
      return client;
    }
    ```

   > [!NOTE]
   > Deze methode gebruikt een filter bij het maken van Hallo ontvanger zodat hello ontvanger alleen berichten tooIoT Hub leest nadat Hallo ontvanger is geactiveerd. Dit is handig in een testomgeving zodat u Hallo huidige reeks berichten kunt zien. In een productieomgeving moet uw code Zorg ervoor dat alle berichten Hallo - voor meer informatie worden verwerkt, Zie Hallo [hoe tooprocess IoT Hub apparaat-naar-cloud-berichten] [ lnk-process-d2c-tutorial] zelfstudie.

9. Wijzig de handtekening Hallo Hallo **belangrijkste** methode tooinclude Hallo uitzondering als volgt:

    ```java
    public static void main( String[] args ) throws IOException
    ```

10. Hallo na code toohello toevoegen **belangrijkste** methode in Hallo **App** klasse. Deze code maakt twee Hallo **EventHubClient** en **PartitionReceiver** exemplaren en kunt u tooclose Hallo app wanneer u klaar bent met het verwerken van berichten:

    ```java
    // Create receivers for partitions 0 and 1.
    EventHubClient client0 = receiveMessages("0");
    EventHubClient client1 = receiveMessages("1");
    System.out.println("Press ENTER tooexit.");
    System.in.read();
    try {
      client0.closeSync();
      client1.closeSync();
      System.exit(0);
    } catch (ServiceBusException sbe) {
      System.exit(1);
    }
    ```

    > [!NOTE]
    > Deze code wordt ervan uitgegaan dat u uw IoT-hub in (gratis) F1-laag Hallo gemaakt. Een gratis IoT-hub heeft twee partities, genaamd "0" en "1".

11. Opslaan en sluiten Hallo App.java bestand.

12. Hallo toobuild **read-d2c-messages** app met behulp van Maven, uitvoeren van de volgende opdracht achter de opdrachtprompt Hallo in Hallo read-d2c-messages map Hallo:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="create-a-device-app"></a>Een apparaat-app maken
In deze sectie maakt u een Java-consoletoepassing die een apparaat simuleert dat apparaat-naar-cloudberichten tooan iothub verzendt.

1. In Hallo map iot-java-get-started die u hebt gemaakt in Hallo *maken van een apparaat-id* sectie, maakt u een Maven-project aangeroepen **simulated-device** met behulp van de volgende opdracht achter de opdrachtprompt Hallo. Let op: dit is één enkele, lange opdracht:

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. Ga bij de opdrachtprompt de map simulated-device toohello.

3. Met een teksteditor Hallo pom.xml-bestand openen in de map simulated-device Hallo en toevoegen van Hallo afhankelijkheden toohello na **afhankelijkheden** knooppunt. Deze afhankelijkheid kunt u toouse hello iothub-java-client-pakket in uw app toocommunicate met uw IoT-hub en Java-objecten tooJSON tooserialize:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    <dependency>
      <groupId>com.google.code.gson</groupId>
      <artifactId>gson</artifactId>
      <version>2.3.1</version>
    </dependency>
    ```

    > [!NOTE]
    > U kunt controleren op de meest recente versie van Hallo **iot-apparaat-client** met [Maven search][lnk-maven-device-search].

4. Opslaan en sluiten Hallo pom.xml-bestand.

5. Met een teksteditor Hallo simulated-device\src\main\java\com\mycompany\app\App.java bestand openen.

6. Voeg de volgende Hallo **importeren** instructies toohello bestand:

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.google.gson.Gson;

    import java.io.*;
    import java.net.URISyntaxException;
    import java.util.Random;
    import java.util.concurrent.Executors;
    import java.util.concurrent.ExecutorService;
    ```

7. Hallo klasseniveau variabelen toohello na toevoegen **App** klasse. Vervangen van **{youriothubname}** met de naam van uw IoT-hub en **{yourdevicekey}** met Hallo apparaat sleutelwaarde u hebt gegenereerd in Hallo *maken van een apparaat-id* sectie:

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myFirstJavaDevice;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myFirstJavaDevice";
    private static DeviceClient client;
    ```
   
    In dit voorbeeld-app gebruikt Hallo **protocol** variabele bij het instantiëren van een **DeviceClient** object. U kunt beide toocommunicate hello MQTT, AMQP of HTTP-protocol gebruiken met IoT Hub.

8. Voeg Hallo volgende geneste **TelemetryDataPoint** klasse binnen Hallo **App** klasse toospecify Hallo telemetrische gegevens uw apparaat verzendt tooyour IoT-hub:

    ```java
    private static class TelemetryDataPoint {
      public String deviceId;
      public double temperature;
      public double humidity;
   
      public String serialize() {
        Gson gson = new Gson();
        return gson.toJson(this);
      }
    }
    ```
9. Voeg Hallo volgende geneste **EventCallback** klasse binnen Hallo **App** klasse toodisplay Hallo bevestiging status of IoT-hub Hallo bij de verwerking van een bericht van Hallo apparaattoepassing retourneert. Deze methode ook Hallo hoofdthread in Hallo-app een melding wanneer het Hallo-bericht is verwerkt:
   
    ```java
    private static class EventCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toomessage with status: " + status.name());
   
        if (context != null) {
          synchronized (context) {
            context.notify();
          }
        }
      }
    }
    ```

10. Voeg Hallo volgende geneste **MessageSender** klasse binnen Hallo **App** klasse. Hallo **uitvoeren** methode in deze klasse genereert voorbeeld telemetrie gegevens toosend tooyour IoT-hub en wordt gewacht op een bevestiging voordat het volgende Hallo-bericht verzonden:

    ```java
    private static class MessageSender implements Runnable {
      public void run()  {
        try {
          double minTemperature = 20;
          double minHumidity = 60;
          Random rand = new Random();
    
          while (true) {
            double currentTemperature = minTemperature + rand.nextDouble() * 15;
            double currentHumidity = minHumidity + rand.nextDouble() * 20;
            TelemetryDataPoint telemetryDataPoint = new TelemetryDataPoint();
            telemetryDataPoint.deviceId = deviceId;
            telemetryDataPoint.temperature = currentTemperature;
            telemetryDataPoint.humidity = currentHumidity;
    
            String msgStr = telemetryDataPoint.serialize();
            Message msg = new Message(msgStr);
            msg.setProperty("temperatureAlert", (currentTemperature > 30) ? "true" : "false");
            msg.setMessageId(java.util.UUID.randomUUID().toString()); 
            System.out.println("Sending: " + msgStr);
    
            Object lockobj = new Object();
            EventCallback callback = new EventCallback();
            client.sendEventAsync(msg, callback, lockobj);
    
            synchronized (lockobj) {
              lockobj.wait();
            }
            Thread.sleep(1000);
          }
        } catch (InterruptedException e) {
          System.out.println("Finished.");
        }
      }
    }
    ```

    Deze methode verzendt één seconde nadat Hallo IoT-hub Hallo vorige bericht erkent een nieuw apparaat-naar-cloud bericht uit. Hallo-bericht bevat een JSON-geserialiseerd object met Hallo deviceId en willekeurige cijfers toosimulate een temperatuursensor en een sensor vochtigheid.

11. Vervang Hallo **belangrijkste** methode Hello code die wordt gemaakt van een thread toosend apparaat-naar-cloudberichten tooyour IoT-hub te volgen:

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException {
      client = new DeviceClient(connString, protocol);
      client.open();
    
      MessageSender sender = new MessageSender();
    
      ExecutorService executor = Executors.newFixedThreadPool(1);
      executor.execute(sender);
    
      System.out.println("Press ENTER tooexit.");
      System.in.read();
      executor.shutdownNow();
      client.closeNow();
    }
    ```

12. Opslaan en sluiten Hallo App.java bestand.

13. Hallo toobuild **simulated-device** app met behulp van Maven, uitvoeren van de volgende opdracht achter de opdrachtprompt Hallo in de map simulated-device Hallo Hallo:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

> [!NOTE]
> tookeep dingen eenvoudige, deze zelfstudie wordt niet geïmplementeerd voor een beleid voor opnieuw proberen. In productiecode moet u beleid voor opnieuw proberen (zoals exponentieel uitstel), zoals voorgesteld in de MSDN-artikel Hallo implementeren [afhandeling van tijdelijke fout][lnk-transient-faults].

## <a name="run-hello-apps"></a>Hallo-apps uitvoeren

U bent nu klaar toorun Hallo apps.

1. Voer bij een opdrachtprompt in Hallo read-d2c-map Hallo opdracht toobegin bewaking van de eerste partitie Hallo in uw IoT-hub te volgen:

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![Java IoT Hub service app toomonitor apparaat-naar-cloud-berichten][7]

2. Voer bij een opdrachtprompt in de map simulated-device Hallo Hallo opdracht toobegin verzenden van telemetrie gegevens tooyour IoT-hub te volgen:

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![Java IoT Hub apparaat-app toosend apparaat-naar-cloud-berichten][8]

3. Hallo **gebruik** -tegel in Hallo [Azure-portal] [ lnk-portal] toont Hallo aantal verzonden berichten toohello IoT-hub:

    ![Azure portal gebruik tegel met aantal verzonden berichten tooIoT Hub][43]

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie maakt u een nieuwe iothub geconfigureerd in hello Azure-portal en vervolgens een apparaat-id in de id-register Hallo iothub hebt gemaakt. U hebt deze apparaat-id tooenable Hallo apparaat app toosend apparaat-naar-cloudberichten toohello iothub gebruikt. Hebt u ook een app die wordt weergegeven Hallo-berichten dat is ontvangen door de Hallo iothub hebt gemaakt.

toocontinue aan de slag met IoT Hub en tooexplore raadpleegt u andere IoT-scenario's:

* [Verbinding maken met uw apparaat][lnk-connect-device]
* [Aan de slag met apparaatbeheer][lnk-device-management]
* [Aan de slag met Azure IoT Edge][lnk-iot-edge]

toolearn hoe tooextend uw IoT-oplossing en proces apparaat-naar-cloud-berichten op grote schaal, zien Hallo [apparaat-naar-cloud-berichten verwerken] [ lnk-process-d2c-tutorial] zelfstudie.
[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

<!-- Images. -->
[6]: ./media/iot-hub-java-java-getstarted/create-iot-hub6.png
[7]: ./media/iot-hub-java-java-getstarted/runapp1.png
[8]: ./media/iot-hub-java-java-getstarted/runapp2.png
[43]: ./media/iot-hub-java-java-getstarted/usage.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-device-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-eventhubs-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22
