---
title: aaaGet de slag met Azure IoT Hub apparaat horende (Java) | Microsoft Docs
description: Hoe toouse Azure IoT Hub apparaat horende tooadd tags en gebruik vervolgens een IoT Hub-query. U hello Azure IoT-device SDK voor Java tooimplement Hallo apparaattoepassing en hello Azure IoT service SDK voor Java tooimplement een service-app die Hallo-labels toegevoegd en Hallo IoT Hub-query wordt uitgevoerd.
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/04/2017
ms.author: dobett
ms.openlocfilehash: 25f6fc81471d59c62bcdc3766bb5c33f5733c930
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-java"></a>Aan de slag met apparaat horende (Java)

[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

In deze zelfstudie maakt maken u twee console Java-apps:

* **toevoegen-tags-query**, een Java-back-end-app die labels toegevoegd en wordt opgevraagd horende apparaten.
* **simulated-device**, een Java-apparaat-app of die een verbinding maakt tooyour iothub en rapporten zijn connectiviteit toestand met een eigenschap gemeld.

> [!NOTE]
> Hallo artikel [Azure IoT SDK's](iot-hub-devguide-sdks.md) bevat informatie over hello Azure IoT SDK's waarmee u toobuild kunt apparaat- en back-end-apps.

toocomplete deze zelfstudie hebt u nodig:

* meest recente Hallo [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* Een actief Azure-account. (Als u geen account hebt, kunt u een [gratis account](http://azure.microsoft.com/pricing/free-trial/) binnen een paar minuten.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

Desgewenst toocreate Hallo apparaat-id programmatisch lezen Hallo overeenkomstige sectie in Hallo [verbinding maken met uw apparaat tooyour iothub met Java](iot-hub-java-java-getstarted.md#create-a-device-identity) artikel.

## <a name="create-hello-service-app"></a>Hallo-service-app maken

In deze sectie maakt u een Java-app die locatie metagegevens toegevoegd, zoals een tag toohello apparaat twin in IoT-Hub die zijn gekoppeld aan **myDeviceId**. Hallo app eerst een query uit iothub voor apparaten die zich bevinden in VS Hallo en voor apparaten die rapporteren van de verbinding van een mobiel netwerk.

1. Maak een lege map genaamd op uw ontwikkelcomputer `iot-java-twin-getstarted`.

1. In Hallo `iot-java-twin-getstarted` map, maak een Maven-project aangeroepen **toevoegen-tags-query** met behulp van de volgende opdracht achter de opdrachtprompt Hallo. Let op: dit is één enkele, lange opdracht:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=add-tags-query -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. Ga bij de opdrachtprompt toohello `add-tags-query` map.

1. Met een teksteditor openen Hallo `pom.xml` bestand in Hallo `add-tags-query` map en Voeg na afhankelijkheid toohello hello **afhankelijkheden** knooppunt. Deze afhankelijkheid kunt u toouse hello **iot-service-client** pakket in uw app toocommunicate met uw IoT-hub:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > U kunt controleren op de meest recente versie van Hallo **iot-service-client** met [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).

1. Voeg de volgende Hallo **bouwen** knooppunt na Hallo **afhankelijkheden** knooppunt. Deze configuratie wordt Java-Maven toouse 1.8 toobuild Hallo app:

    ```xml
    <build>
      <plugins>
        <plugin>
          <groupId>org.apache.maven.plugins</groupId>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.3</version>
          <configuration>
            <source>1.8</source>
            <target>1.8</target>
          </configuration>
        </plugin>
      </plugins>
    </build>
    ```

1. Opslaan en sluiten Hallo `pom.xml` bestand.

1. Met een teksteditor openen Hallo `add-tags-query\src\main\java\com\mycompany\app\App.java` bestand.

1. Voeg de volgende Hallo **importeren** instructies toohello bestand:

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.*;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.HashSet;
    import java.util.Set;
    ```

1. Hallo klasseniveau variabelen toohello na toevoegen **App** klasse. Vervang `{youriothubconnectionstring}` met uw IoT hub-verbindingsreeks die u hebt genoteerd in Hallo *een IoT Hub maken* sectie:

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String region = "US";
    public static final String plant = "Redmond43";
    ```

1. Update Hallo **belangrijkste** methode handtekening tooinclude Hallo volgende `throws` component:

    ```java
    public static void main( String[] args ) throws IOException
    ```

1. Hallo na code toohello toevoegen **belangrijkste** methode toocreate hello **DeviceTwin** en **DeviceTwinDevice** objecten. Hallo **DeviceTwin** object verwerkt Hallo communicatie met uw IoT-hub. Hallo **DeviceTwinDevice** object vertegenwoordigt Hallo apparaat twin met eigenschappen en tags:

    ```java
    // Get hello DeviceTwin and DeviceTwinDevice objects
    DeviceTwin twinClient = DeviceTwin.createFromConnectionString(iotHubConnectionString);
    DeviceTwinDevice device = new DeviceTwinDevice(deviceId);
    ```

1. Voeg de volgende Hallo `try/catch` blokkeren toohello **belangrijkste** methode:

    ```java
    try {
      // Code goes here
    } catch (IotHubException e) {
      System.out.println(e.getMessage());
    } catch (IOException e) {
      System.out.println(e.getMessage());
    }
    ```

1. Hallo tooupdate **regio** en **plant** apparaat twin labels in uw twin apparaat toevoegen na de code in Hallo Hallo `try` blokkeren:

    ```java
    // Get hello device twin from IoT Hub
    System.out.println("Device twin before update:");
    twinClient.getTwin(device);
    System.out.println(device);

    // Update device twin tags if they are different
    // from hello existing values
    String currentTags = device.tagsToString();
    if ((!currentTags.contains("region=" + region) && !currentTags.contains("plant=" + plant))) {
      // Create hello tags and attach them toohello DeviceTwinDevice object
      Set<Pair> tags = new HashSet<Pair>();
      tags.add(new Pair("region", region));
      tags.add(new Pair("plant", plant));
      device.setTags(tags);

      // Update hello device twin in IoT Hub
      System.out.println("Updating device twin");
      twinClient.updateTwin(device);
    }

    // Retrieve hello device twin with hello tag values from IoT Hub
    System.out.println("Device twin after update:");
    twinClient.getTwin(device);
    System.out.println(device);
    ```

1. tooquery hello apparaat horende in IoT-hub toevoegen na de code toohello Hallo `try` blok na het Hallo-code die u in de vorige stap Hallo hebt toegevoegd. Hallo-code wordt uitgevoerd twee query's. Elke query retourneert maximaal 100 apparaten:

    ```java
    // Query hello device twins in IoT Hub
    System.out.println("Devices in Redmond:");

    // Construct hello query
    SqlQuery sqlQuery = SqlQuery.createSqlQuery("*", SqlQuery.FromType.DEVICES, "tags.plant='Redmond43'", null);

    // Run hello query, returning a maximum of 100 devices
    Query twinQuery = twinClient.queryTwin(sqlQuery.getQuery(), 100);
    while (twinClient.hasNextDeviceTwin(twinQuery)) {
      DeviceTwinDevice d = twinClient.getNextDeviceTwin(twinQuery);
      System.out.println(d.getDeviceId());
    }

    System.out.println("Devices in Redmond using a cellular network:");

    // Construct hello query
    sqlQuery = SqlQuery.createSqlQuery("*", SqlQuery.FromType.DEVICES, "tags.plant='Redmond43' AND properties.reported.connectivityType = 'cellular'", null);

    // Run hello query, returning a maximum of 100 devices
    twinQuery = twinClient.queryTwin(sqlQuery.getQuery(), 3);
    while (twinClient.hasNextDeviceTwin(twinQuery)) {
      DeviceTwinDevice d = twinClient.getNextDeviceTwin(twinQuery);
      System.out.println(d.getDeviceId());
    }
    ```

1. Opslaan en sluiten Hallo `add-tags-query\src\main\java\com\mycompany\app\App.java` bestand

1. Hallo bouwen **toevoegen-tags-query** app en eventuele fouten te corrigeren. Ga bij de opdrachtprompt toohello `add-tags-query` map en Voer Hallo volgende opdracht:

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a>Een apparaat-app maken

In deze sectie maakt u een Java-consoletoepassing die stelt u een eigenschapswaarde gemeld dat tooIoT Hub wordt verzonden.

1. In Hallo `iot-java-twin-getstarted` map, maak een Maven-project aangeroepen **simulated-device** met behulp van de volgende opdracht achter de opdrachtprompt Hallo. Let op: dit is één enkele, lange opdracht:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. Ga bij de opdrachtprompt toohello `simulated-device` map.

1. Met een teksteditor openen Hallo `pom.xml` bestand in Hallo `simulated-device` map en Voeg na afhankelijkheden toohello hello **afhankelijkheden** knooppunt. Deze afhankelijkheid kunt u toouse hello **iot-apparaat-client** pakket in uw app toocommunicate met uw IoT-hub:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > U kunt controleren op de meest recente versie van Hallo **iot-apparaat-client** met [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).

1. Voeg de volgende Hallo **bouwen** knooppunt na Hallo **afhankelijkheden** knooppunt. Deze configuratie wordt Java-Maven toouse 1.8 toobuild Hallo app:

    ```xml
    <build>
      <plugins>
        <plugin>
          <groupId>org.apache.maven.plugins</groupId>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.3</version>
          <configuration>
            <source>1.8</source>
            <target>1.8</target>
          </configuration>
        </plugin>
      </plugins>
    </build>
    ```

1. Opslaan en sluiten Hallo `pom.xml` bestand.

1. Met een teksteditor openen Hallo `simulated-device\src\main\java\com\mycompany\app\App.java` bestand.

1. Voeg de volgende Hallo **importeren** instructies toohello bestand:

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. Hallo klasseniveau variabelen toohello na toevoegen **App** klasse. Vervangen van `{youriothubname}` met de naam van uw IoT-hub en `{yourdevicekey}` met Hallo apparaat sleutelwaarde u hebt gegenereerd in Hallo *maken van een apparaat-id* sectie:

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myDeviceId";
    ```

    In dit voorbeeld-app gebruikt Hallo **protocol** variabele bij het instantiëren van een **DeviceClient** object. Op dit moment toouse twin apparaatfuncties u Hallo MQTT protocol moet gebruiken.

1. Hallo na code toohello toevoegen **belangrijkste** methode:
    * Maak een client apparaat toocommunicate met IoT Hub.
    * Maak een **apparaat** toostore Hallo apparaateigenschappen twin object.

    ```java
    DeviceClient client = new DeviceClient(connString, protocol);

    // Create a Device object toostore hello device twin properties
    Device dataCollector = new Device() {
      // Print details when a property value changes
      @Override
      public void PropertyCall(String propertyKey, Object propertyValue, Object context) {
        System.out.println(propertyKey + " changed too" + propertyValue);
      }
    };
    ```

1. Hallo na code toohello toevoegen **belangrijkste** methode toocreate een **connectivityType** eigenschap gerapporteerd en dit tooIoT Hub te verzenden:

    ```java
    try {
      // Open hello DeviceClient and start hello device twin services.
      client.open();
      client.startDeviceTwin(new DeviceTwinStatusCallBack(), null, dataCollector, null);

      // Create a reported property and send it tooyour IoT hub.
      dataCollector.setReportedProp(new Property("connectivityType", "cellular"));
      client.sendReportedProperties(dataCollector.getReportedProp());
    }
    catch (Exception e) {
      System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" + e.getMessage());
      dataCollector.clean();
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. Toevoegen van de volgende code toohello einde van Hallo Hallo **belangrijkste** methode. Wachten op Hallo **Enter** sleutel kan tijd voor IoT Hub tooreport Hallo status van Hallo apparaat twin bewerkingen:

    ```java
    System.out.println("Press any key tooexit...");

    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();

    dataCollector.clean();
    client.close();
    ```

1. Opslaan en sluiten Hallo `simulated-device\src\main\java\com\mycompany\app\App.java` bestand.

1. Hallo bouwen **simulated-device** app en eventuele fouten te corrigeren. Ga bij de opdrachtprompt toohello `simulated-device` map en Voer Hallo volgende opdracht:

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a>Hallo-apps uitvoeren

U bent nu klaar toorun Hallo console apps.

1. Bij een opdrachtprompt in Hallo `add-tags-query` map na de opdracht toorun Hallo Hallo **toevoegen-tags-query** service-app:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![IoT Hub voor Java service app tooupdate waarden code en elk apparaat query's uitvoeren](media/iot-hub-java-java-twin-getstarted/service-app-1.png)

    U kunt zien Hallo **plant** en **regio** labels toohello apparaat twin toegevoegd. Hallo eerste query retourneert het apparaat, maar Hallo tweede niet.

1. Bij een opdrachtprompt in Hallo `simulated-device` map na de opdracht tooadd Hallo Hallo **connectivityType** eigenschap toohello apparaat twin gerapporteerd:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Hallo-apparaatclient voegt Hallo ** connectivityType ** eigenschap gerapporteerd](media/iot-hub-java-java-twin-getstarted/device-app-1.png)

1. Bij een opdrachtprompt in Hallo `add-tags-query` map na de opdracht toorun Hallo Hallo **toevoegen-tags-query** service-app een tweede keer:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![IoT Hub voor Java service app tooupdate waarden code en elk apparaat query's uitvoeren](media/iot-hub-java-java-twin-getstarted/service-app-2.png)

    Nu u uw apparaat heeft verzonden hello **connectivityType** eigenschap tooIoT Hub, Hallo tweede query retourneert het apparaat.

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie maakt u een nieuwe iothub geconfigureerd in hello Azure-portal en vervolgens een apparaat-id in de id-register Hallo iothub hebt gemaakt. U metagegevens van apparaten als labels toegevoegd vanuit een back-end-app en een app tooreport apparaat connectiviteit apparaatgegevens in Hallo apparaat twin geschreven. U hebt ook geleerd hoe tooquery Hallo twin apparaatgegevens Hallo IoT-Hub SQL-achtige query language gebruiken.

Gebruik Hallo resources toolearn hoe volgende aan:

* Verzenden van telemetrie vanaf apparaten Hello [aan de slag met IoT Hub](iot-hub-java-java-getstarted.md) zelfstudie.
* Beheren van apparaten interactief (zoals het inschakelen van een ventilator van een gebruiker beheerde app) met Hallo [direct methoden gebruiken](iot-hub-java-java-direct-methods.md) zelfstudie.

<!-- Images. -->
[7]: ./media/iot-hub-java-java-twin-getstarted/invoke-method.png
[8]: ./media/iot-hub-java-java-twin-getstarted/device-listen.png
[9]: ./media/iot-hub-java-java-twin-getstarted/device-respond.png

<!-- Links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
