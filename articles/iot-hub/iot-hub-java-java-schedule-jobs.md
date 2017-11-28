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
# <a name="schedule-and-broadcast-jobs-java"></a><span data-ttu-id="c7f24-104">Planning en broadcast-taken (Java)</span><span class="sxs-lookup"><span data-stu-id="c7f24-104">Schedule and broadcast jobs (Java)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="c7f24-105">Gebruik Azure IoT Hub tooschedule en bijhouden taken die miljoenen apparaten worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="c7f24-105">Use Azure IoT Hub tooschedule and track jobs that update millions of devices.</span></span> <span data-ttu-id="c7f24-106">Taken die moeten worden gebruikt:</span><span class="sxs-lookup"><span data-stu-id="c7f24-106">Use jobs to:</span></span>

* <span data-ttu-id="c7f24-107">Gewenste eigenschappen bijwerken</span><span class="sxs-lookup"><span data-stu-id="c7f24-107">Update desired properties</span></span>
* <span data-ttu-id="c7f24-108">Labels bijwerken</span><span class="sxs-lookup"><span data-stu-id="c7f24-108">Update tags</span></span>
* <span data-ttu-id="c7f24-109">Directe methoden aanroepen</span><span class="sxs-lookup"><span data-stu-id="c7f24-109">Invoke direct methods</span></span>

<span data-ttu-id="c7f24-110">Een taak verpakt een van deze acties en houdt Hallo uitgevoerd op een reeks apparaten.</span><span class="sxs-lookup"><span data-stu-id="c7f24-110">A job wraps one of these actions and tracks hello execution against a set of devices.</span></span> <span data-ttu-id="c7f24-111">Een apparaat twin query definieert de set Hallo Hallo-taak uitgevoerd op basis van apparaten.</span><span class="sxs-lookup"><span data-stu-id="c7f24-111">A device twin query defines hello set of devices hello job executes against.</span></span> <span data-ttu-id="c7f24-112">Een back-endserver voor apps kunt bijvoorbeeld een taak tooinvoke een directe methode op 10.000 apparaten die opnieuw wordt opgestart Hallo-apparaten.</span><span class="sxs-lookup"><span data-stu-id="c7f24-112">For example, a back-end app can use a job tooinvoke a direct method on 10,000 devices that reboots hello devices.</span></span> <span data-ttu-id="c7f24-113">U geeft Hallo set apparaten met een apparaat twin query en Hallo taak toorun plannen op een later tijdstip.</span><span class="sxs-lookup"><span data-stu-id="c7f24-113">You specify hello set of devices with a device twin query and schedule hello job toorun at a future time.</span></span> <span data-ttu-id="c7f24-114">Hallo taak houdt voortgang als elk Hallo apparaten ontvangen en Hallo opnieuw opstarten directe methode uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="c7f24-114">hello job tracks progress as each of hello devices receive and execute hello reboot direct method.</span></span>

<span data-ttu-id="c7f24-115">toolearn meer informatie over elk van deze mogelijkheden, Zie:</span><span class="sxs-lookup"><span data-stu-id="c7f24-115">toolearn more about each of these capabilities, see:</span></span>

* <span data-ttu-id="c7f24-116">Apparaat-twin en eigenschappen: [aan de slag met horende apparaten](iot-hub-java-java-twin-getstarted.md)</span><span class="sxs-lookup"><span data-stu-id="c7f24-116">Device twin and properties: [Get started with device twins](iot-hub-java-java-twin-getstarted.md)</span></span>
* <span data-ttu-id="c7f24-117">Directe methoden: [IoT Hub developer guide - rechtstreekse methoden](iot-hub-devguide-direct-methods.md) en [zelfstudie: directe methoden gebruiken](iot-hub-java-java-direct-methods.md)</span><span class="sxs-lookup"><span data-stu-id="c7f24-117">Direct methods: [IoT Hub developer guide - direct methods](iot-hub-devguide-direct-methods.md) and [Tutorial: Use direct methods](iot-hub-java-java-direct-methods.md)</span></span>

<span data-ttu-id="c7f24-118">In deze handleiding ontdekt u hoe u:</span><span class="sxs-lookup"><span data-stu-id="c7f24-118">This tutorial shows you how to:</span></span>

* <span data-ttu-id="c7f24-119">Maakt een apparaat-app die u een directe methode aangeroepen implementeert **lockDoor**.</span><span class="sxs-lookup"><span data-stu-id="c7f24-119">Create a device app that implements a direct method called **lockDoor**.</span></span> <span data-ttu-id="c7f24-120">Hallo apparaattoepassing ontvangt ook de gewenste wijzigingen van Hallo back-endserver voor apps.</span><span class="sxs-lookup"><span data-stu-id="c7f24-120">hello device app also receives desired property changes from hello back-end app.</span></span>
* <span data-ttu-id="c7f24-121">Maakt een back-end-app die u een taak toocall hello maakt **lockDoor** directe methode op meerdere apparaten.</span><span class="sxs-lookup"><span data-stu-id="c7f24-121">Create a back-end app that creates a job toocall hello **lockDoor** direct method on multiple devices.</span></span> <span data-ttu-id="c7f24-122">Een andere taak verzendt gewenste eigenschap updates toomultiple apparaten.</span><span class="sxs-lookup"><span data-stu-id="c7f24-122">Another job sends desired property updates toomultiple devices.</span></span>

<span data-ttu-id="c7f24-123">Aan het einde van de Hallo van deze zelfstudie hebt u een java-consoletoepassing apparaat en het hulpprogramma voor het back-end van een java-consoletoepassing:</span><span class="sxs-lookup"><span data-stu-id="c7f24-123">At hello end of this tutorial, you have a java console device app and a java console back-end app:</span></span>

<span data-ttu-id="c7f24-124">**simulated-device** die verbinding tooyour IoT-hub maakt, implementeert Hallo **lockDoor** directe methode en ingangen gewenst eigenschapswijzigingen.</span><span class="sxs-lookup"><span data-stu-id="c7f24-124">**simulated-device** that connects tooyour IoT hub, implements hello **lockDoor** direct method, and handles desired property changes.</span></span>

<span data-ttu-id="c7f24-125">**taken plannen** die gebruikmaken van taken toocall hello **lockDoor** directe methode en update Hallo apparaat twin gewenst eigenschappen op meerdere apparaten.</span><span class="sxs-lookup"><span data-stu-id="c7f24-125">**schedule-jobs** that use jobs toocall hello **lockDoor** direct method and update hello device twin desired properties on multiple devices.</span></span>

> [!NOTE]
> <span data-ttu-id="c7f24-126">Hallo artikel [Azure IoT SDK's](iot-hub-devguide-sdks.md) bevat informatie over hello Azure IoT SDK's waarmee u toobuild kunt apparaat- en back-end-apps.</span><span class="sxs-lookup"><span data-stu-id="c7f24-126">hello article [Azure IoT SDKs](iot-hub-devguide-sdks.md) provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7f24-127">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c7f24-127">Prerequisites</span></span>

<span data-ttu-id="c7f24-128">toocomplete deze zelfstudie hebt u nodig:</span><span class="sxs-lookup"><span data-stu-id="c7f24-128">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="c7f24-129">meest recente Hallo [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="c7f24-129">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="c7f24-130">Maven 3</span><span class="sxs-lookup"><span data-stu-id="c7f24-130">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="c7f24-131">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="c7f24-131">An active Azure account.</span></span> <span data-ttu-id="c7f24-132">(Als u geen account hebt, kunt u een [gratis account](http://azure.microsoft.com/pricing/free-trial/) binnen een paar minuten.)</span><span class="sxs-lookup"><span data-stu-id="c7f24-132">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="c7f24-133">Desgewenst toocreate Hallo apparaat-id programmatisch lezen Hallo overeenkomstige sectie in Hallo [verbinding maken met uw apparaat tooyour iothub met Java](iot-hub-java-java-getstarted.md#create-a-device-identity) artikel.</span><span class="sxs-lookup"><span data-stu-id="c7f24-133">If you prefer toocreate hello device identity programmatically, read hello corresponding section in hello [Connect your device tooyour IoT hub using Java](iot-hub-java-java-getstarted.md#create-a-device-identity) article.</span></span> <span data-ttu-id="c7f24-134">U kunt ook Hallo [iothub explorer](https://github.com/Azure/iothub-explorer) hulpprogramma tooadd een apparaat tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="c7f24-134">You can also use hello [iothub-explorer](https://github.com/Azure/iothub-explorer) tool tooadd a device tooyour IoT hub.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="c7f24-135">Hallo-service-app maken</span><span class="sxs-lookup"><span data-stu-id="c7f24-135">Create hello service app</span></span>

<span data-ttu-id="c7f24-136">In deze sectie kunt u een Java-consoletoepassing die gebruikmaakt van taken te maken:</span><span class="sxs-lookup"><span data-stu-id="c7f24-136">In this section, you create a Java console app that uses jobs to:</span></span>

* <span data-ttu-id="c7f24-137">Hallo aanroepen **lockDoor** directe methode op meerdere apparaten.</span><span class="sxs-lookup"><span data-stu-id="c7f24-137">Call hello **lockDoor** direct method on multiple devices.</span></span>
* <span data-ttu-id="c7f24-138">Eigenschappen van de gewenste toomultiple apparaten verzenden.</span><span class="sxs-lookup"><span data-stu-id="c7f24-138">Send desired properties toomultiple devices.</span></span>

<span data-ttu-id="c7f24-139">toocreate hello app:</span><span class="sxs-lookup"><span data-stu-id="c7f24-139">toocreate hello app:</span></span>

1. <span data-ttu-id="c7f24-140">Maak een lege map genaamd op uw ontwikkelcomputer `iot-java-schedule-jobs`.</span><span class="sxs-lookup"><span data-stu-id="c7f24-140">On your development machine, create an empty folder called `iot-java-schedule-jobs`.</span></span>

1. <span data-ttu-id="c7f24-141">In Hallo `iot-java-schedule-jobs` map, maak een Maven-project aangeroepen **taken plannen** met behulp van de volgende opdracht achter de opdrachtprompt Hallo.</span><span class="sxs-lookup"><span data-stu-id="c7f24-141">In hello `iot-java-schedule-jobs` folder, create a Maven project called **schedule-jobs** using hello following command at your command prompt.</span></span> <span data-ttu-id="c7f24-142">Let op: dit is één enkele, lange opdracht:</span><span class="sxs-lookup"><span data-stu-id="c7f24-142">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=schedule-jobs -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="c7f24-143">Ga bij de opdrachtprompt toohello `schedule-jobs` map.</span><span class="sxs-lookup"><span data-stu-id="c7f24-143">At your command prompt, navigate toohello `schedule-jobs` folder.</span></span>

1. <span data-ttu-id="c7f24-144">Met een teksteditor openen Hallo `pom.xml` bestand in Hallo `schedule-jobs` map en Voeg na afhankelijkheid toohello hello **afhankelijkheden** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="c7f24-144">Using a text editor, open hello `pom.xml` file in hello `schedule-jobs` folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="c7f24-145">Deze afhankelijkheid kunt u toouse hello **iot-service-client** pakket in uw app toocommunicate met uw IoT-hub:</span><span class="sxs-lookup"><span data-stu-id="c7f24-145">This dependency enables you toouse hello **iot-service-client** package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="c7f24-146">U kunt controleren op de meest recente versie van Hallo **iot-service-client** met [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="c7f24-146">You can check for hello latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="c7f24-147">Voeg de volgende Hallo **bouwen** knooppunt na Hallo **afhankelijkheden** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="c7f24-147">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="c7f24-148">Deze configuratie wordt Java-Maven toouse 1.8 toobuild Hallo app:</span><span class="sxs-lookup"><span data-stu-id="c7f24-148">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="c7f24-149">Opslaan en sluiten Hallo `pom.xml` bestand.</span><span class="sxs-lookup"><span data-stu-id="c7f24-149">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="c7f24-150">Met een teksteditor openen Hallo `schedule-jobs\src\main\java\com\mycompany\app\App.java` bestand.</span><span class="sxs-lookup"><span data-stu-id="c7f24-150">Using a text editor, open hello `schedule-jobs\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="c7f24-151">Voeg de volgende Hallo **importeren** instructies toohello bestand:</span><span class="sxs-lookup"><span data-stu-id="c7f24-151">Add hello following **import** statements toohello file:</span></span>

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

1. <span data-ttu-id="c7f24-152">Hallo klasseniveau variabelen toohello na toevoegen **App** klasse.</span><span class="sxs-lookup"><span data-stu-id="c7f24-152">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="c7f24-153">Vervang `{youriothubconnectionstring}` met uw IoT hub-verbindingsreeks die u hebt genoteerd in Hallo *een IoT Hub maken* sectie:</span><span class="sxs-lookup"><span data-stu-id="c7f24-153">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in hello *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    // How long hello job is permitted toorun without
    // completing its work on hello set of devices
    private static final long maxExecutionTimeInSeconds = 30;
    ```

1. <span data-ttu-id="c7f24-154">Hallo na methode toohello toevoegen **App** klasse tooschedule een taak tooupdate hello **gebouw** en **Floor** gewenst eigenschappen in Hallo apparaat twin:</span><span class="sxs-lookup"><span data-stu-id="c7f24-154">Add hello following method toohello **App** class tooschedule a job tooupdate hello **Building** and **Floor** desired properties in hello device twin:</span></span>

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

1. <span data-ttu-id="c7f24-155">een taak toocall hello tooschedule **lockDoor** methode Hallo na methode toohello toevoegen **App** klasse:</span><span class="sxs-lookup"><span data-stu-id="c7f24-155">tooschedule a job toocall hello **lockDoor** method, add hello following method toohello **App** class:</span></span>

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

1. <span data-ttu-id="c7f24-156">toomonitor een taak toevoegen na methode toohello hello **App** klasse:</span><span class="sxs-lookup"><span data-stu-id="c7f24-156">toomonitor a job, add hello following method toohello **App** class:</span></span>

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

1. <span data-ttu-id="c7f24-157">tooquery voor meer informatie Hallo Hallo-taken die u hebt uitgevoerd, toevoegen Hallo methode te volgen:</span><span class="sxs-lookup"><span data-stu-id="c7f24-157">tooquery for hello details of hello jobs you ran, add hello following method:</span></span>

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

1. <span data-ttu-id="c7f24-158">Update Hallo **belangrijkste** methode handtekening tooinclude Hallo volgende `throws` component:</span><span class="sxs-lookup"><span data-stu-id="c7f24-158">Update hello **main** method signature tooinclude hello following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws Exception
    ```

1. <span data-ttu-id="c7f24-159">toorun en monitor twee taken opeenvolgend, toevoegen na de code toohello Hallo **belangrijkste** methode:</span><span class="sxs-lookup"><span data-stu-id="c7f24-159">toorun and monitor two jobs sequentially, add hello following code toohello **main** method:</span></span>

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

1. <span data-ttu-id="c7f24-160">Opslaan en sluiten Hallo `schedule-jobs\src\main\java\com\mycompany\app\App.java` bestand</span><span class="sxs-lookup"><span data-stu-id="c7f24-160">Save and close hello `schedule-jobs\src\main\java\com\mycompany\app\App.java` file</span></span>

1. <span data-ttu-id="c7f24-161">Hallo bouwen **taken plannen** app en eventuele fouten te corrigeren.</span><span class="sxs-lookup"><span data-stu-id="c7f24-161">Build hello **schedule-jobs** app and correct any errors.</span></span> <span data-ttu-id="c7f24-162">Ga bij de opdrachtprompt toohello `schedule-jobs` map en Voer Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="c7f24-162">At your command prompt, navigate toohello `schedule-jobs` folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a><span data-ttu-id="c7f24-163">Een apparaat-app maken</span><span class="sxs-lookup"><span data-stu-id="c7f24-163">Create a device app</span></span>

<span data-ttu-id="c7f24-164">In deze sectie maakt u een Java-consoletoepassing ingangen Hallo gewenste eigenschappen die worden verzonden vanuit Hallo directe methodeaanroep van IoT Hub en implementeert.</span><span class="sxs-lookup"><span data-stu-id="c7f24-164">In this section, you create a Java console app that handles hello desired properties sent from IoT Hub and implements hello direct method call.</span></span>

1. <span data-ttu-id="c7f24-165">In Hallo `iot-java-schedule-jobs` map, maak een Maven-project aangeroepen **simulated-device** met behulp van de volgende opdracht achter de opdrachtprompt Hallo.</span><span class="sxs-lookup"><span data-stu-id="c7f24-165">In hello `iot-java-schedule-jobs` folder, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="c7f24-166">Let op: dit is één enkele, lange opdracht:</span><span class="sxs-lookup"><span data-stu-id="c7f24-166">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="c7f24-167">Ga bij de opdrachtprompt toohello `simulated-device` map.</span><span class="sxs-lookup"><span data-stu-id="c7f24-167">At your command prompt, navigate toohello `simulated-device` folder.</span></span>

1. <span data-ttu-id="c7f24-168">Met een teksteditor openen Hallo `pom.xml` bestand in Hallo `simulated-device` map en Voeg na afhankelijkheden toohello hello **afhankelijkheden** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="c7f24-168">Using a text editor, open hello `pom.xml` file in hello `simulated-device` folder and add hello following dependencies toohello **dependencies** node.</span></span> <span data-ttu-id="c7f24-169">Deze afhankelijkheid kunt u toouse hello **iot-apparaat-client** pakket in uw app toocommunicate met uw IoT-hub:</span><span class="sxs-lookup"><span data-stu-id="c7f24-169">This dependency enables you toouse hello **iot-device-client** package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="c7f24-170">U kunt controleren op de meest recente versie van Hallo **iot-apparaat-client** met [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="c7f24-170">You can check for hello latest version of **iot-device-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="c7f24-171">Voeg de volgende Hallo **bouwen** knooppunt na Hallo **afhankelijkheden** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="c7f24-171">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="c7f24-172">Deze configuratie wordt Java-Maven toouse 1.8 toobuild Hallo app:</span><span class="sxs-lookup"><span data-stu-id="c7f24-172">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="c7f24-173">Opslaan en sluiten Hallo `pom.xml` bestand.</span><span class="sxs-lookup"><span data-stu-id="c7f24-173">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="c7f24-174">Met een teksteditor openen Hallo `simulated-device\src\main\java\com\mycompany\app\App.java` bestand.</span><span class="sxs-lookup"><span data-stu-id="c7f24-174">Using a text editor, open hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="c7f24-175">Voeg de volgende Hallo **importeren** instructies toohello bestand:</span><span class="sxs-lookup"><span data-stu-id="c7f24-175">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="c7f24-176">Hallo klasseniveau variabelen toohello na toevoegen **App** klasse.</span><span class="sxs-lookup"><span data-stu-id="c7f24-176">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="c7f24-177">Vervangen van `{youriothubname}` met de naam van uw IoT-hub en `{yourdevicekey}` met Hallo apparaat sleutelwaarde u hebt gegenereerd in Hallo *maken van een apparaat-id* sectie:</span><span class="sxs-lookup"><span data-stu-id="c7f24-177">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with hello device key value you generated in hello *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    <span data-ttu-id="c7f24-178">In dit voorbeeld-app gebruikt Hallo **protocol** variabele bij het instantiëren van een **DeviceClient** object.</span><span class="sxs-lookup"><span data-stu-id="c7f24-178">This sample app uses hello **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="c7f24-179">Op dit moment toouse twin apparaatfuncties u Hallo MQTT protocol moet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c7f24-179">Currently, toouse device twin features you must use hello MQTT protocol.</span></span>

1. <span data-ttu-id="c7f24-180">tooprint apparaat twin meldingen toohello console, voeg de volgende Hallo geneste klasse toohello **App** klasse:</span><span class="sxs-lookup"><span data-stu-id="c7f24-180">tooprint device twin notifications toohello console, add hello following nested class toohello **App** class:</span></span>

    ```java
    // Handler for device twin operation notifications from IoT Hub
    protected static class DeviceTwinStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toodevice twin operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="c7f24-181">tooprint directe methode meldingen toohello console, voeg de volgende Hallo geneste klasse toohello **App** klasse:</span><span class="sxs-lookup"><span data-stu-id="c7f24-181">tooprint direct method notifications toohello console, add hello following nested class toohello **App** class:</span></span>

    ```java
    // Handler for direct method notifications from IoT Hub
    protected static class DirectMethodStatusCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toodirect method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="c7f24-182">toohandle directe methodeaanroepen van IoT Hub, voeg Hallo volgende geneste klasse toohello **App** klasse:</span><span class="sxs-lookup"><span data-stu-id="c7f24-182">toohandle direct method calls from IoT Hub, add hello following nested class toohello **App** class:</span></span>

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

1. <span data-ttu-id="c7f24-183">Update Hallo **belangrijkste** methode handtekening tooinclude Hallo volgende `throws` component:</span><span class="sxs-lookup"><span data-stu-id="c7f24-183">Update hello **main** method signature tooinclude hello following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException
    ```

1. <span data-ttu-id="c7f24-184">Hallo na code toohello toevoegen **belangrijkste** methode:</span><span class="sxs-lookup"><span data-stu-id="c7f24-184">Add hello following code toohello **main** method to:</span></span>
    * <span data-ttu-id="c7f24-185">Maak een client apparaat toocommunicate met IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c7f24-185">Create a device client toocommunicate with IoT Hub.</span></span>
    * <span data-ttu-id="c7f24-186">Maak een **apparaat** toostore Hallo apparaateigenschappen twin object.</span><span class="sxs-lookup"><span data-stu-id="c7f24-186">Create a **Device** object toostore hello device twin properties.</span></span>

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

1. <span data-ttu-id="c7f24-187">toostart Hallo apparaat clientservices toevoegen na de code toohello Hallo **belangrijkste** methode:</span><span class="sxs-lookup"><span data-stu-id="c7f24-187">toostart hello device client services, add hello following code toohello **main** method:</span></span>

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

1. <span data-ttu-id="c7f24-188">toowait voor Hallo gebruiker toopress hello **Enter** sleutel voordat u afsluit, toevoegen van de volgende code toohello einde van Hallo Hallo **belangrijkste** methode:</span><span class="sxs-lookup"><span data-stu-id="c7f24-188">toowait for hello user toopress hello **Enter** key before shutting down, add hello following code toohello end of hello **main** method:</span></span>

    ```java
    // Close hello app
    System.out.println("Press any key tooexit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    dataCollector.clean();
    client.closeNow();
    scanner.close();
    ```

1. <span data-ttu-id="c7f24-189">Opslaan en sluiten Hallo `simulated-device\src\main\java\com\mycompany\app\App.java` bestand.</span><span class="sxs-lookup"><span data-stu-id="c7f24-189">Save and close hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="c7f24-190">Hallo bouwen **simulated-device** app en eventuele fouten te corrigeren.</span><span class="sxs-lookup"><span data-stu-id="c7f24-190">Build hello **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="c7f24-191">Ga bij de opdrachtprompt toohello `simulated-device` map en Voer Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="c7f24-191">At your command prompt, navigate toohello `simulated-device` folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a><span data-ttu-id="c7f24-192">Hallo-apps uitvoeren</span><span class="sxs-lookup"><span data-stu-id="c7f24-192">Run hello apps</span></span>

<span data-ttu-id="c7f24-193">U bent nu klaar toorun Hallo console apps.</span><span class="sxs-lookup"><span data-stu-id="c7f24-193">You are now ready toorun hello console apps.</span></span>

1. <span data-ttu-id="c7f24-194">Bij een opdrachtprompt in Hallo `simulated-device` map Hallo opdracht toostart Hallo apparaattoepassing luisteren naar de gewenste wijzigingen en directe methodeaanroepen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c7f24-194">At a command prompt in hello `simulated-device` folder, run hello following command toostart hello device app listening for desired property changes and direct method calls:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Hallo apparaat-client wordt gestart](media/iot-hub-java-java-schedule-jobs/device-app-1.png)

1. <span data-ttu-id="c7f24-196">Bij een opdrachtprompt in Hallo `schedule-jobs` map na de opdracht toorun Hallo Hallo **taken plannen** service app toorun twee taken.</span><span class="sxs-lookup"><span data-stu-id="c7f24-196">At a command prompt in hello `schedule-jobs` folder, run hello following command toorun hello **schedule-jobs** service app toorun two jobs.</span></span> <span data-ttu-id="c7f24-197">Hallo stelt eerst Hallo gewenst eigenschapswaarden, tweede aanroepen Hallo Hallo directe methode:</span><span class="sxs-lookup"><span data-stu-id="c7f24-197">hello first sets hello desired property values, hello second calls hello direct method:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Service-IoT-Hub voor Java-app maakt u twee taken](media/iot-hub-java-java-schedule-jobs/service-app-1.png)

1. <span data-ttu-id="c7f24-199">Hallo apparaattoepassing verwerkt Hallo gewenst eigenschap wijzigings- en Hallo directe methode aanroepen:</span><span class="sxs-lookup"><span data-stu-id="c7f24-199">hello device app handles hello desired property change and hello direct method call:</span></span>

    ![Hallo apparaatclient reageert toohello wijzigingen](media/iot-hub-java-java-schedule-jobs/device-app-2.png)

## <a name="next-steps"></a><span data-ttu-id="c7f24-201">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c7f24-201">Next steps</span></span>

<span data-ttu-id="c7f24-202">In deze zelfstudie maakt u een nieuwe iothub geconfigureerd in hello Azure-portal en vervolgens een apparaat-id in de id-register Hallo iothub hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c7f24-202">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="c7f24-203">U hebt gemaakt van een back-endserver voor apps toorun twee taken.</span><span class="sxs-lookup"><span data-stu-id="c7f24-203">You created a back-end app toorun two jobs.</span></span> <span data-ttu-id="c7f24-204">de eerste taak Hallo instellen gewenste eigenschapswaarden en Hallo tweede taak heeft een directe methode.</span><span class="sxs-lookup"><span data-stu-id="c7f24-204">hello first job set desired property values, and hello second job called a direct method.</span></span>

<span data-ttu-id="c7f24-205">Gebruik Hallo resources toolearn hoe volgende aan:</span><span class="sxs-lookup"><span data-stu-id="c7f24-205">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="c7f24-206">Verzenden van telemetrie vanaf apparaten Hello [aan de slag met IoT Hub](iot-hub-java-java-getstarted.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="c7f24-206">Send telemetry from devices with hello [Get started with IoT Hub](iot-hub-java-java-getstarted.md) tutorial.</span></span>
* <span data-ttu-id="c7f24-207">Beheren van apparaten interactief (zoals het inschakelen van een ventilator van een gebruiker beheerde app) met Hallo [direct methoden gebruiken](iot-hub-java-java-direct-methods.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="c7f24-207">Control devices interactively (such as turning on a fan from a user-controlled app) with hello [Use direct methods](iot-hub-java-java-direct-methods.md) tutorial.</span></span>
