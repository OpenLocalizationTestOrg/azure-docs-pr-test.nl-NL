---
title: aaaSchedule taken met Azure IoT Hub (Java) | Microsoft Docs
description: Hoe een Azure-IoT-Hub tooschedule taak tooinvoke een directe methode en een gewenste eigenschap instellen op meerdere apparaten. U gebruikt hello Azure IoT-device SDK voor Java tooimplement Hallo gesimuleerd apparaat-apps en hello Azure IoT service SDK voor Java tooimplement een service-app toorun Hallo taak.
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
ms.date: 07/10/2017
ms.author: dobett
ms.openlocfilehash: b1b05fa56c3ce96af0b33d4cca0dd54da0f4e927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-java"></a>Planning en broadcast-taken (Java)

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

Gebruik Azure IoT Hub tooschedule en bijhouden taken die miljoenen apparaten worden bijgewerkt. Taken die moeten worden gebruikt:

* Gewenste eigenschappen bijwerken
* Labels bijwerken
* Directe methoden aanroepen

Een taak verpakt een van deze acties en houdt Hallo uitgevoerd op een reeks apparaten. Een apparaat twin query definieert de set Hallo Hallo-taak uitgevoerd op basis van apparaten. Een back-endserver voor apps kunt bijvoorbeeld een taak tooinvoke een directe methode op 10.000 apparaten die opnieuw wordt opgestart Hallo-apparaten. U geeft Hallo set apparaten met een apparaat twin query en Hallo taak toorun plannen op een later tijdstip. Hallo taak houdt voortgang als elk Hallo apparaten ontvangen en Hallo opnieuw opstarten directe methode uitvoeren.

toolearn meer informatie over elk van deze mogelijkheden, Zie:

* Apparaat-twin en eigenschappen: [aan de slag met horende apparaten](iot-hub-java-java-twin-getstarted.md)
* Directe methoden: [IoT Hub developer guide - rechtstreekse methoden](iot-hub-devguide-direct-methods.md) en [zelfstudie: directe methoden gebruiken](iot-hub-java-java-direct-methods.md)

In deze handleiding ontdekt u hoe u:

* Maakt een apparaat-app die u een directe methode aangeroepen implementeert **lockDoor**. Hallo apparaattoepassing ontvangt ook de gewenste wijzigingen van Hallo back-endserver voor apps.
* Maakt een back-end-app die u een taak toocall hello maakt **lockDoor** directe methode op meerdere apparaten. Een andere taak verzendt gewenste eigenschap updates toomultiple apparaten.

Aan het einde van de Hallo van deze zelfstudie hebt u een java-consoletoepassing apparaat en het hulpprogramma voor het back-end van een java-consoletoepassing:

**simulated-device** die verbinding tooyour IoT-hub maakt, implementeert Hallo **lockDoor** directe methode en ingangen gewenst eigenschapswijzigingen.

**taken plannen** die gebruikmaken van taken toocall hello **lockDoor** directe methode en update Hallo apparaat twin gewenst eigenschappen op meerdere apparaten.

> [!NOTE]
> Hallo artikel [Azure IoT SDK's](iot-hub-devguide-sdks.md) bevat informatie over hello Azure IoT SDK's waarmee u toobuild kunt apparaat- en back-end-apps.

## <a name="prerequisites"></a>Vereisten

toocomplete deze zelfstudie hebt u nodig:

* meest recente Hallo [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* Een actief Azure-account. (Als u geen account hebt, kunt u een [gratis account](http://azure.microsoft.com/pricing/free-trial/) binnen een paar minuten.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

Desgewenst toocreate Hallo apparaat-id programmatisch lezen Hallo overeenkomstige sectie in Hallo [verbinding maken met uw apparaat tooyour iothub met Java](iot-hub-java-java-getstarted.md#create-a-device-identity) artikel. U kunt ook Hallo [iothub explorer](https://github.com/Azure/iothub-explorer) hulpprogramma tooadd een apparaat tooyour IoT-hub.

## <a name="create-hello-service-app"></a>Hallo-service-app maken

In deze sectie kunt u een Java-consoletoepassing die gebruikmaakt van taken te maken:

* Hallo aanroepen **lockDoor** directe methode op meerdere apparaten.
* Eigenschappen van de gewenste toomultiple apparaten verzenden.

toocreate hello app:

1. Maak een lege map genaamd op uw ontwikkelcomputer `iot-java-schedule-jobs`.

1. In Hallo `iot-java-schedule-jobs` map, maak een Maven-project aangeroepen **taken plannen** met behulp van de volgende opdracht achter de opdrachtprompt Hallo. Let op: dit is één enkele, lange opdracht:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=schedule-jobs -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. Ga bij de opdrachtprompt toohello `schedule-jobs` map.

1. Met een teksteditor openen Hallo `pom.xml` bestand in Hallo `schedule-jobs` map en Voeg na afhankelijkheid toohello hello **afhankelijkheden** knooppunt. Deze afhankelijkheid kunt u toouse hello **iot-service-client** pakket in uw app toocommunicate met uw IoT-hub:

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

1. Met een teksteditor openen Hallo `schedule-jobs\src\main\java\com\mycompany\app\App.java` bestand.

1. Voeg de volgende Hallo **importeren** instructies toohello bestand:

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceTwinDevice;
    import com.microsoft.azure.sdk.iot.service.devicetwin.Pair;
    import com.microsoft.azure.sdk.iot.service.devicetwin.Query;
    import com.microsoft.azure.sdk.iot.service.devicetwin.SqlQuery;
    import com.microsoft.azure.sdk.iot.service.jobs.JobClient;
    import com.microsoft.azure.sdk.iot.service.jobs.JobResult;
    import com.microsoft.azure.sdk.iot.service.jobs.JobStatus;

    import java.util.Date;
    import java.time.Instant;
    import java.util.HashSet;
    import java.util.Set;
    import java.util.UUID;
    ```

1. Hallo klasseniveau variabelen toohello na toevoegen **App** klasse. Vervang `{youriothubconnectionstring}` met uw IoT hub-verbindingsreeks die u hebt genoteerd in Hallo *een IoT Hub maken* sectie:

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    // How long hello job is permitted toorun without
    // completing its work on hello set of devices
    private static final long maxExecutionTimeInSeconds = 30;
    ```

1. Hallo na methode toohello toevoegen **App** klasse tooschedule een taak tooupdate hello **gebouw** en **Floor** gewenst eigenschappen in Hallo apparaat twin:

    ```java
    private static JobResult scheduleJobSetDesiredProperties(JobClient jobClient, String jobId) {
      DeviceTwinDevice twin = new DeviceTwinDevice(deviceId);
      Set<Pair> desiredProperties = new HashSet<Pair>();
      desiredProperties.add(new Pair("Building", 43));
      desiredProperties.add(new Pair("Floor", 3));
      twin.setDesiredProperties(desiredProperties);
      // Optimistic concurrency control
      twin.setETag("*");

      // Schedule hello update twin job toorun now
      // against a single device
      System.out.println("Schedule job " + jobId + " for device " + deviceId);
      try {
        JobResult jobResult = jobClient.scheduleUpdateTwin(jobId, 
          "deviceId='" + deviceId + "'",
          twin,
          new Date(),
          maxExecutionTimeInSeconds);
        return jobResult;
      } catch (Exception e) {
        System.out.println("Exception scheduling desired properties job: " + jobId);
        System.out.println(e.getMessage());
        return null;
      }
    }
    ```

1. een taak toocall hello tooschedule **lockDoor** methode Hallo na methode toohello toevoegen **App** klasse:

    ```java
    private static JobResult scheduleJobCallDirectMethod(JobClient jobClient, String jobId) {
      // Schedule a job now toocall hello lockDoor direct method
      // against a single device. Response and connection
      // timeouts are set too5 seconds.
      System.out.println("Schedule job " + jobId + " for device " + deviceId);
      try {
        JobResult jobResult = jobClient.scheduleDeviceMethod(jobId,
          "deviceId='" + deviceId + "'",
          "lockDoor",
          5L, 5L, null,
          new Date(),
          maxExecutionTimeInSeconds);
        return jobResult;
      } catch (Exception e) {
        System.out.println("Exception scheduling direct method job: " + jobId);
        System.out.println(e.getMessage());
        return null;
      }
    };
    ```

1. toomonitor een taak toevoegen na methode toohello hello **App** klasse:

    ```java
    private static void monitorJob(JobClient jobClient, String jobId) {
      try {
        JobResult jobResult = jobClient.getJob(jobId);
        if(jobResult == null)
        {
          System.out.println("No JobResult for: " + jobId);
          return;
        }
        // Check hello job result until it's completed
        while(jobResult.getJobStatus() != JobStatus.completed)
        {
          Thread.sleep(100);
          jobResult = jobClient.getJob(jobId);
          System.out.println("Status " + jobResult.getJobStatus() + " for job " + jobId);
        }
        System.out.println("Final status " + jobResult.getJobStatus() + " for job " + jobId);
      } catch (Exception e) {
        System.out.println("Exception monitoring job: " + jobId);
        System.out.println(e.getMessage());
        return;
      }
    }
    ```

1. tooquery voor meer informatie Hallo Hallo-taken die u hebt uitgevoerd, toevoegen Hallo methode te volgen:

    ```java
    private static void queryDeviceJobs(JobClient jobClient, String start) throws Exception {
      System.out.println("\nQuery device jobs since " + start);

      // Create a jobs query using hello time hello jobs started
      Query deviceJobQuery = jobClient
          .queryDeviceJob(SqlQuery.createSqlQuery("*", SqlQuery.FromType.JOBS, "devices.jobs.startTimeUtc > '" + start + "'", null).getQuery());

      // Iterate over hello list of jobs and print hello details
      while (jobClient.hasNextJob(deviceJobQuery)) {
        System.out.println(jobClient.getNextJob(deviceJobQuery));
      }
    }
    ```

1. Update Hallo **belangrijkste** methode handtekening tooinclude Hallo volgende `throws` component:

    ```java
    public static void main( String[] args ) throws Exception
    ```

1. toorun en monitor twee taken opeenvolgend, toevoegen na de code toohello Hallo **belangrijkste** methode:

    ```java
    // Record hello start time
    String start = Instant.now().toString();

    // Create JobClient
    JobClient jobClient = JobClient.createFromConnectionString(iotHubConnectionString);
    System.out.println("JobClient created with success");

    // Schedule twin job desired properties
    // Maximum concurrent jobs is 1 for Free and S1 tiers
    String desiredPropertiesJobId = "DPCMD" + UUID.randomUUID();
    scheduleJobSetDesiredProperties(jobClient, desiredPropertiesJobId);
    monitorJob(jobClient, desiredPropertiesJobId);

    // Schedule twin job direct method
    String directMethodJobId = "DMCMD" + UUID.randomUUID();
    scheduleJobCallDirectMethod(jobClient, directMethodJobId);
    monitorJob(jobClient, directMethodJobId);

    // Run a query tooshow hello job detail
    queryDeviceJobs(jobClient, start);

    System.out.println("Shutting down schedule-jobs app");
    ```

1. Opslaan en sluiten Hallo `schedule-jobs\src\main\java\com\mycompany\app\App.java` bestand

1. Hallo bouwen **taken plannen** app en eventuele fouten te corrigeren. Ga bij de opdrachtprompt toohello `schedule-jobs` map en Voer Hallo volgende opdracht:

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a>Een apparaat-app maken

In deze sectie maakt u een Java-consoletoepassing ingangen Hallo gewenste eigenschappen die worden verzonden vanuit Hallo directe methodeaanroep van IoT Hub en implementeert.

1. In Hallo `iot-java-schedule-jobs` map, maak een Maven-project aangeroepen **simulated-device** met behulp van de volgende opdracht achter de opdrachtprompt Hallo. Let op: dit is één enkele, lange opdracht:

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
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    In dit voorbeeld-app gebruikt Hallo **protocol** variabele bij het instantiëren van een **DeviceClient** object. Op dit moment toouse twin apparaatfuncties u Hallo MQTT protocol moet gebruiken.

1. tooprint apparaat twin meldingen toohello console, voeg de volgende Hallo geneste klasse toohello **App** klasse:

    ```java
    // Handler for device twin operation notifications from IoT Hub
    protected static class DeviceTwinStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toodevice twin operation with status " + status.name());
      }
    }
    ```

1. tooprint directe methode meldingen toohello console, voeg de volgende Hallo geneste klasse toohello **App** klasse:

    ```java
    // Handler for direct method notifications from IoT Hub
    protected static class DirectMethodStatusCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toodirect method operation with status " + status.name());
      }
    }
    ```

1. toohandle directe methodeaanroepen van IoT Hub, voeg Hallo volgende geneste klasse toohello **App** klasse:

    ```java
    // Handler for direct method calls from IoT Hub
    protected static class DirectMethodCallback
        implements DeviceMethodCallback {
      @Override
      public DeviceMethodData call(String methodName, Object methodData, Object context) {
        DeviceMethodData deviceMethodData;
        switch (methodName) {
          case "lockDoor": {
            System.out.println("Executing direct method: " + methodName);
            deviceMethodData = new DeviceMethodData(METHOD_SUCCESS, "Executed direct method " + methodName);
            break;
          }
          default: {
            deviceMethodData = new DeviceMethodData(METHOD_NOT_DEFINED, "Not defined direct method " + methodName);
          }
        }
        // Notify IoT Hub of result
        return deviceMethodData;
      }
    }
    ```

1. Update Hallo **belangrijkste** methode handtekening tooinclude Hallo volgende `throws` component:

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException
    ```

1. Hallo na code toohello toevoegen **belangrijkste** methode:
    * Maak een client apparaat toocommunicate met IoT Hub.
    * Maak een **apparaat** toostore Hallo apparaateigenschappen twin object.

    ```java
    // Create a device client
    DeviceClient client = new DeviceClient(connString, protocol);

    // An object toomanage device twin desired and reported properties
    Device dataCollector = new Device() {
      @Override
      public void PropertyCall(String propertyKey, Object propertyValue, Object context)
      {
        System.out.println("Received desired property change: " + propertyKey + " " + propertyValue);
      }
    };
    ```

1. toostart Hallo apparaat clientservices toevoegen na de code toohello Hallo **belangrijkste** methode:

    ```java
    try {
      // Open hello DeviceClient
      // Start hello device twin services
      // Subscribe toodirect method calls
      client.open();
      client.startDeviceTwin(new DeviceTwinStatusCallBack(), null, dataCollector, null);
      client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
    } catch (Exception e) {
      System.out.println("Exception, shutting down \n" + " Cause: " + e.getCause() + " \n" + e.getMessage());
      dataCollector.clean();
      client.closeNow();
      System.out.println("Shutting down...");
    }
    ```

1. toowait voor Hallo gebruiker toopress hello **Enter** sleutel voordat u afsluit, toevoegen van de volgende code toohello einde van Hallo Hallo **belangrijkste** methode:

    ```java
    // Close hello app
    System.out.println("Press any key tooexit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    dataCollector.clean();
    client.closeNow();
    scanner.close();
    ```

1. Opslaan en sluiten Hallo `simulated-device\src\main\java\com\mycompany\app\App.java` bestand.

1. Hallo bouwen **simulated-device** app en eventuele fouten te corrigeren. Ga bij de opdrachtprompt toohello `simulated-device` map en Voer Hallo volgende opdracht:

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a>Hallo-apps uitvoeren

U bent nu klaar toorun Hallo console apps.

1. Bij een opdrachtprompt in Hallo `simulated-device` map Hallo opdracht toostart Hallo apparaattoepassing luisteren naar de gewenste wijzigingen en directe methodeaanroepen te volgen:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Hallo apparaat-client wordt gestart](media/iot-hub-java-java-schedule-jobs/device-app-1.png)

1. Bij een opdrachtprompt in Hallo `schedule-jobs` map na de opdracht toorun Hallo Hallo **taken plannen** service app toorun twee taken. Hallo stelt eerst Hallo gewenst eigenschapswaarden, tweede aanroepen Hallo Hallo directe methode:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Service-IoT-Hub voor Java-app maakt u twee taken](media/iot-hub-java-java-schedule-jobs/service-app-1.png)

1. Hallo apparaattoepassing verwerkt Hallo gewenst eigenschap wijzigings- en Hallo directe methode aanroepen:

    ![Hallo apparaatclient reageert toohello wijzigingen](media/iot-hub-java-java-schedule-jobs/device-app-2.png)

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie maakt u een nieuwe iothub geconfigureerd in hello Azure-portal en vervolgens een apparaat-id in de id-register Hallo iothub hebt gemaakt. U hebt gemaakt van een back-endserver voor apps toorun twee taken. de eerste taak Hallo instellen gewenste eigenschapswaarden en Hallo tweede taak heeft een directe methode.

Gebruik Hallo resources toolearn hoe volgende aan:

* Verzenden van telemetrie vanaf apparaten Hello [aan de slag met IoT Hub](iot-hub-java-java-getstarted.md) zelfstudie.
* Beheren van apparaten interactief (zoals het inschakelen van een ventilator van een gebruiker beheerde app) met Hallo [direct methoden gebruiken](iot-hub-java-java-direct-methods.md) zelfstudie.
