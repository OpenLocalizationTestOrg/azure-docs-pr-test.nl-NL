---
title: aaaGet de slag met Azure IoT Hub Apparaatbeheer (Java) | Microsoft Docs
description: Hoe toouse Azure IoT Hub apparaat management tooinitiate een extern apparaat opnieuw worden opgestart. U gebruikt hello Azure IoT-device SDK voor Java tooimplement een gesimuleerde apparaattoepassing met een directe methode en hello Azure IoT service SDK voor Java tooimplement een service-app die Hallo directe methode aanroept.
services: iot-hub
documentationcenter: .java
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 7aaeda9d4ff7002e5c66adfd61e2dfd5bcea964f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-management-java"></a>Aan de slag met Apparaatbeheer (Java)

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

In deze handleiding ontdekt u hoe u:

* Gebruik Hallo toocreate met Azure portal een IoT-Hub en een apparaat-id maakt in uw IoT-hub.
* Maak een gesimuleerde apparaattoepassing die een directe methode tooreboot Hallo apparaat implementeert. Rechtstreekse methoden worden aangeroepen vanuit Hallo cloud.
* Maak een app die wordt aangeroepen Hallo opnieuw opstarten directe methode in Hallo gesimuleerde apparaattoepassing via uw IoT-hub. Deze app vervolgens monitors gemelde eigenschappen van Hallo apparaat toosee Hallo wanneer Hallo opnieuw opstarten voltooid is.

Aan het einde van de Hallo van deze zelfstudie hebt u twee Java-apps die console:

**simulated-device**. Deze app:

* Tooyour IoT-hub is verbonden met de apparaat-id Hallo eerder hebt gemaakt.
* Een aanroep van de directe methode opnieuw opstarten ontvangt.
* Simuleert fysieke computer opnieuw is opgestart.
* Rapporten Hallo tijdstip Hallo laatste keer opnieuw opstarten via een gerapporteerde eigenschap.

**trigger-reboot**. Deze app:

* Een directe methode wordt aangeroepen in de gesimuleerde apparaattoepassing Hallo.
* Hallo antwoord toohello directe aanroep van methode verzonden door het gesimuleerde apparaat hello wordt weergegeven
* Geeft Hallo bijgewerkt gerapporteerd eigenschappen.

> [!NOTE]
> Zie voor informatie over Hallo SDK's die u toobuild toepassingen toorun op apparaten en de back-end van uw oplossing gebruiken kunt [Azure IoT SDK's][lnk-hub-sdks].

toocomplete deze zelfstudie hebt u nodig:

* Java SE 8. <br/> [Uw ontwikkelingsomgeving voorbereiden] [ lnk-dev-setup] wordt beschreven hoe tooinstall Java voor deze zelfstudie op Windows of Linux.
* Maven 3.  <br/> [Uw ontwikkelingsomgeving voorbereiden] [ lnk-dev-setup] wordt beschreven hoe tooinstall [Maven] [ lnk-maven] voor deze zelfstudie op Windows of Linux.
* [Node.js-versie 0.10.0 of hoger](http://nodejs.org).

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a>Activeren van een extern opnieuw opstarten op Hallo-apparaat met een directe methode

In deze sectie maakt u een Java-consoletoepassing maken die:

1. Roept Hallo directe methode in de gesimuleerde apparaattoepassing Hallo van opnieuw opstarten.
1. Geeft antwoord Hallo weer.
1. Polls Hallo gerapporteerd eigenschappen is verzonden vanaf Hallo apparaat toodetermine wanneer Hallo opnieuw opstarten voltooid is.

Deze consoletoepassing verbindt tooyour IoT Hub gerapporteerde tooinvoke Hallo directe methode en lezen Hallo eigenschappen.

1. Maak een lege map dm-get-started.

1. Maak in map dm-get-started Hallo een Maven-project aangeroepen **trigger-reboot** met behulp van de volgende opdracht achter de opdrachtprompt Hallo. Hallo hieronder vindt u een enkele, lange opdracht:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=trigger-reboot -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. Navigeer toohello trigger-reboot map bij de opdrachtprompt.

1. Met een teksteditor, open Hallo pom.xml-bestand in Hallo trigger-reboot map en Hallo afhankelijkheid toohello na toevoegen **afhankelijkheden** knooppunt. Deze afhankelijkheid kunt u toouse Hallo iot-service-client-pakket in uw app toocommunicate met uw IoT-hub:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > U kunt controleren op de meest recente versie van Hallo **iot-service-client** met [Maven search][lnk-maven-service-search].

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

1. Opslaan en sluiten Hallo pom.xml-bestand.

1. Open met een teksteditor Hallo trigger-reboot\src\main\java\com\mycompany\app\App.java bronbestand.

1. Voeg de volgende Hallo **importeren** instructies toohello bestand:

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceMethod;
    import com.microsoft.azure.sdk.iot.service.devicetwin.MethodResult;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceTwin;
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceTwinDevice;

    import java.io.IOException;
    import java.util.concurrent.TimeUnit;
    import java.util.concurrent.Executors;
    import java.util.concurrent.ExecutorService;
    ```

1. Hallo klasseniveau variabelen toohello na toevoegen **App** klasse. Vervang `{youriothubconnectionstring}` met uw IoT hub-verbindingsreeks die u hebt genoteerd in Hallo *een IoT Hub maken* sectie:

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    private static final String methodName = "reboot";
    private static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    private static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    ```

1. een thread die Hallo leest tooimplement gerapporteerd eigenschappen van Hallo apparaat twin Voeg elke 10 seconden Hallo volgende geneste klasse toohello **App** klasse:

    ```java
    private static class ShowReportedProperties implements Runnable {
      public void run() {
        try {
          DeviceTwin deviceTwins = DeviceTwin.createFromConnectionString(iotHubConnectionString);
          DeviceTwinDevice twinDevice = new DeviceTwinDevice(deviceId);
          while (true) {
            System.out.println("Get reported properties from device twin");
            deviceTwins.getTwin(twinDevice);
            System.out.println(twinDevice.reportedPropertiesToString());
            Thread.sleep(10000);
          }
        } catch (Exception ex) {
          System.out.println("Exception reading reported properties: " + ex.getMessage());
        }
      }
    }
    ```

1. tooinvoke Hallo opnieuw opstarten directe methode op Hallo gesimuleerd apparaat toevoegen Hallo code toohello na **belangrijkste** methode:

    ```java
    System.out.println("Starting sample...");
    DeviceMethod methodClient = DeviceMethod.createFromConnectionString(iotHubConnectionString);

    try
    {
      System.out.println("Invoke reboot direct method");
      MethodResult result = methodClient.invoke(deviceId, methodName, responseTimeout, connectTimeout, null);

      if(result == null)
      {
        throw new IOException("Invoke direct method reboot returns null");
      }
      System.out.println("Invoked reboot on device");
      System.out.println("Status for device:   " + result.getStatus());
      System.out.println("Message from device: " + result.getPayload());
    }
    catch (IotHubException e)
    {
        System.out.println(e.getMessage());
    }
    ```

1. toostart Hallo thread toopoll Hallo gemelde eigenschappen van het gesimuleerde apparaat hello, toevoegen na de code toohello Hallo **belangrijkste** methode:

    ```java
    ShowReportedProperties showReportedProperties = new ShowReportedProperties();
    ExecutorService executor = Executors.newFixedThreadPool(1);
    executor.execute(showReportedProperties);
    ```

1. tooenable u toostop Hallo-app toevoegen na de code toohello Hallo **belangrijkste** methode:

    ```java
    System.out.println("Press ENTER tooexit.");
    System.in.read();
    executor.shutdownNow();
    System.out.println("Shutting down sample...");
    ```

1. Opslaan en sluiten Hallo trigger-reboot\src\main\java\com\mycompany\app\App.java bestand.

1. Hallo bouwen **trigger-reboot** back-endserver voor Apps en eventuele fouten te corrigeren. Navigeer toohello trigger-reboot map en Voer Hallo volgende opdracht achter de opdrachtprompt:

    `mvn clean package -DskipTests`

## <a name="create-a-simulated-device-app"></a>Een gesimuleerde apparaattoepassing maken

In deze sectie maakt u een Java-consoletoepassing die een apparaat simuleert. Hallo app luistert naar Hallo opnieuw opstarten directe methode-aanroep van uw IoT-hub en onmiddellijk reageert toothat aanroep. Hallo-app en vervolgens de inactieve modus inschakelt voor een tijdje toosimulate Hallo opnieuw opstarten proces voordat gebruikmaakt van een gerapporteerde eigenschap toonotify hello **trigger-reboot** back-end-app die Hallo opnieuw opstarten is voltooid.

1. Maak in map dm-get-started Hallo een Maven-project aangeroepen **simulated-device** met behulp van de volgende opdracht achter de opdrachtprompt Hallo. Hallo hieronder vindt u een enkele, lange opdracht:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. Ga bij de opdrachtprompt de map simulated-device toohello.

1. Met een teksteditor Hallo pom.xml-bestand openen in de map simulated-device Hallo en toevoegen van Hallo afhankelijkheid toohello na **afhankelijkheden** knooppunt. Deze afhankelijkheid kunt u toouse Hallo iot-service-client-pakket in uw app toocommunicate met uw IoT-hub:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > U kunt controleren op de meest recente versie van Hallo **iot-apparaat-client** met [Maven search][lnk-maven-device-search].

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

1. Opslaan en sluiten Hallo pom.xml-bestand.

1. Open met een teksteditor Hallo simulated-device\src\main\java\com\mycompany\app\App.java bronbestand.

1. Voeg de volgende Hallo **importeren** instructies toohello bestand:

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.time.LocalDateTime;
    import java.util.Scanner;
    import java.util.Set;
    import java.util.HashSet;
    ```

1. Hallo klasseniveau variabelen toohello na toevoegen **App** klasse. Vervang `{yourdeviceconnectionstring}` met Hallo apparaat-verbindingsreeks hebt genoteerd in Hallo *maken van een apparaat-id* sectie:

    ```java
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;

    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String connString = "{yourdeviceconnectionstring}";
    private static DeviceClient client;
    ```

1. tooimplement een retouraanroep-handler voor directe methode statusgebeurtenissen, voeg Hallo volgende geneste klasse toohello **App** klasse:

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded toodevice method operation with status " + status.name());
      }
    }
    ```

1. tooimplement een retouraanroep-handler voor apparaat twin statusgebeurtenissen, voeg Hallo volgende geneste klasse toohello **App** klasse:

    ```java
    protected static class DeviceTwinStatusCallback implements IotHubEventCallback
    {
        public void execute(IotHubStatusCode status, Object context)
        {
            System.out.println("IoT Hub responded toodevice twin operation with status " + status.name());
        }
    }
    ```

1. tooimplement een retouraanroep-handler voor gebeurtenissen van de eigenschap, voeg Hallo volgende geneste klasse toohello **App** klasse:

    ```java
    protected static class PropertyCallback implements PropertyCallBack<String, String>
    {
      public void PropertyCall(String propertyKey, String propertyValue, Object context)
      {
        System.out.println("PropertyKey:     " + propertyKey);
        System.out.println("PropertyKvalue:  " + propertyKey);
      }
    }
    ```

1. tooimplement thread toosimulate Hallo apparaat opnieuw worden opgestart, voeg Hallo volgende geneste klasse toohello **App** klasse. Hallo thread modus ingeschakeld gedurende vijf seconden en vervolgens stelt Hallo **lastReboot** eigenschap gerapporteerd:

    ```java
    protected static class RebootDeviceThread implements Runnable {
      public void run() {
        try {
          System.out.println("Rebooting...");
          Thread.sleep(5000);
          Property property = new Property("lastReboot", LocalDateTime.now());
          Set<Property> properties = new HashSet<Property>();
          properties.add(property);
          client.sendReportedProperties(properties);
          System.out.println("Rebooted");
        }
        catch (Exception ex) {
          System.out.println("Exception in reboot thread: " + ex.getMessage());
        }
      }
    }
    ```

1. tooimplement hello directe methode op Hallo-apparaat, voeg Hallo volgende geneste klasse toohello **App** klasse. Wanneer Hallo gesimuleerde app ontvangt voor een aanroep van toohello **opnieuw opstarten** directe methode wordt een bevestiging toohello beller en start vervolgens begint een thread tooprocess Hallo opnieuw:

    ```java
    protected static class DirectMethodCallback implements com.microsoft.azure.sdk.iot.device.DeviceTwin.DeviceMethodCallback
    {
      @Override
      public DeviceMethodData call(String methodName, Object methodData, Object context)
      {
        DeviceMethodData deviceMethodData;
        switch (methodName)
        {
          case "reboot" :
          {
            int status = METHOD_SUCCESS;
            System.out.println("Received reboot request");
            deviceMethodData = new DeviceMethodData(status, "Started reboot");
            RebootDeviceThread rebootThread = new RebootDeviceThread();
            Thread t = new Thread(rebootThread);
            t.start();
            break;
          }
          default:
          {
            int status = METHOD_NOT_DEFINED;
            deviceMethodData = new DeviceMethodData(status, "Not defined direct method " + methodName);
          }
        }
        return deviceMethodData;
      }
    }
    ```

1. Wijzig de handtekening Hallo Hallo **belangrijkste** methode toothrow Hallo volgende uitzonderingen:

    ```java
    public static void main(String[] args) throws IOException, URISyntaxException
    ```

1. tooinstantiate een **DeviceClient**, toevoegen na de code toohello Hallo **belangrijkste** methode:

    ```java
    System.out.println("Starting device client sample...");
    client = new DeviceClient(connString, protocol);
    ```

1. toostart luisteren voor directe methode-aanroepen toevoegen na de code toohello Hallo **belangrijkste** methode:

    ```java
    try
    {
      client.open();
      client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
      client.startDeviceTwin(new DeviceTwinStatusCallback(), null, new PropertyCallback(), null);
      System.out.println("Subscribed toodirect methods and polling for reported properties. Waiting...");
    }
    catch (Exception e)
    {
      System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" +  e.getMessage());
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. tooshut omlaag apparaatsimulator hello, toevoegen na de code toohello Hallo **belangrijkste** methode:

    ```java
    System.out.println("Press any key tooexit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    scanner.close();
    client.close();
    System.out.println("Shutting down...");
    ```

1. Opslaan en sluiten van de bestand simulated-device\src\main\java\com\mycompany\app\App.java Hallo.

1. Hallo bouwen **simulated-device** back-endserver voor Apps en eventuele fouten te corrigeren. Ga bij de opdrachtprompt de map simulated-device toohello en Voer Hallo volgende opdracht:

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a>Hallo-apps uitvoeren

U bent nu klaar toorun Hallo apps.

1. Voer bij een opdrachtprompt in de map simulated-device Hallo Hallo opdracht toobegin luisteren naar de methodeaanroepen opnieuw opstarten van uw IoT-hub te volgen:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![IoT Hub voor Java gesimuleerd apparaat app toolisten voor opnieuw opstarten directe methodeaanroepen][1]

1. Voer bij een opdrachtprompt in Hallo trigger-reboot map Hallo volgende opdracht toocall Hallo opnieuw opstarten methode op uw gesimuleerde apparaat uit uw IoT-hub:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![IoT Hub voor Java service app toocall Hallo directe methode opnieuw opstarten][2]

1. Hallo gesimuleerd apparaat reageert toohello opnieuw opstarten directe methode aanroepen:

    ![De gesimuleerde apparaattoepassing IoT-Hub voor Java reageert toohello directe methode-aanroep][3]

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[1]: ./media/iot-hub-java-java-device-management-getstarted/launchsimulator.png
[2]: ./media/iot-hub-java-java-device-management-getstarted/triggerreboot.png
[3]: ./media/iot-hub-java-java-device-management-getstarted/respondtoreboot.png
<!-- Links -->

[lnk-maven]: https://maven.apache.org/what-is-maven.html

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java/blob/master/doc/java-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md

[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-device-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22