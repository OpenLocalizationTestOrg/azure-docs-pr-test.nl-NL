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
# <a name="get-started-with-device-management-java"></a><span data-ttu-id="ef3b7-104">Aan de slag met Apparaatbeheer (Java)</span><span class="sxs-lookup"><span data-stu-id="ef3b7-104">Get started with device management (Java)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="ef3b7-105">In deze handleiding ontdekt u hoe u:</span><span class="sxs-lookup"><span data-stu-id="ef3b7-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="ef3b7-106">Gebruik Hallo toocreate met Azure portal een IoT-Hub en een apparaat-id maakt in uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="ef3b7-106">Use hello Azure portal toocreate an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="ef3b7-107">Maak een gesimuleerde apparaattoepassing die een directe methode tooreboot Hallo apparaat implementeert.</span><span class="sxs-lookup"><span data-stu-id="ef3b7-107">Create a simulated device app that implements a direct method tooreboot hello device.</span></span> <span data-ttu-id="ef3b7-108">Rechtstreekse methoden worden aangeroepen vanuit Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="ef3b7-108">Direct methods are invoked from hello cloud.</span></span>
* <span data-ttu-id="ef3b7-109">Maak een app die wordt aangeroepen Hallo opnieuw opstarten directe methode in Hallo gesimuleerde apparaattoepassing via uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="ef3b7-109">Create an app that invokes hello reboot direct method in hello simulated device app through your IoT hub.</span></span> <span data-ttu-id="ef3b7-110">Deze app vervolgens monitors gemelde eigenschappen van Hallo apparaat toosee Hallo wanneer Hallo opnieuw opstarten voltooid is.</span><span class="sxs-lookup"><span data-stu-id="ef3b7-110">This app then monitors hello reported properties from hello device toosee when hello reboot operation is complete.</span></span>

<span data-ttu-id="ef3b7-111">Aan het einde van de Hallo van deze zelfstudie hebt u twee Java-apps die console:</span><span class="sxs-lookup"><span data-stu-id="ef3b7-111">At hello end of this tutorial, you have two Java console apps:</span></span>

<span data-ttu-id="ef3b7-112">**simulated-device**.</span><span class="sxs-lookup"><span data-stu-id="ef3b7-112">**simulated-device**.</span></span> <span data-ttu-id="ef3b7-113">Deze app:</span><span class="sxs-lookup"><span data-stu-id="ef3b7-113">This app:</span></span>

* <span data-ttu-id="ef3b7-114">Tooyour IoT-hub is verbonden met de apparaat-id Hallo eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ef3b7-114">Connects tooyour IoT hub with hello device identity created earlier.</span></span>
* <span data-ttu-id="ef3b7-115">Een aanroep van de directe methode opnieuw opstarten ontvangt.</span><span class="sxs-lookup"><span data-stu-id="ef3b7-115">Receives a reboot direct method call.</span></span>
* <span data-ttu-id="ef3b7-116">Simuleert fysieke computer opnieuw is opgestart.</span><span class="sxs-lookup"><span data-stu-id="ef3b7-116">Simulates a physical reboot.</span></span>
* <span data-ttu-id="ef3b7-117">Rapporten Hallo tijdstip Hallo laatste keer opnieuw opstarten via een gerapporteerde eigenschap.</span><span class="sxs-lookup"><span data-stu-id="ef3b7-117">Reports hello time of hello last reboot through a reported property.</span></span>

<span data-ttu-id="ef3b7-118">**trigger-reboot**.</span><span class="sxs-lookup"><span data-stu-id="ef3b7-118">**trigger-reboot**.</span></span> <span data-ttu-id="ef3b7-119">Deze app:</span><span class="sxs-lookup"><span data-stu-id="ef3b7-119">This app:</span></span>

* <span data-ttu-id="ef3b7-120">Een directe methode wordt aangeroepen in de gesimuleerde apparaattoepassing Hallo.</span><span class="sxs-lookup"><span data-stu-id="ef3b7-120">Calls a direct method in hello simulated device app.</span></span>
* <span data-ttu-id="ef3b7-121">Hallo antwoord toohello directe aanroep van methode verzonden door het gesimuleerde apparaat hello wordt weergegeven</span><span class="sxs-lookup"><span data-stu-id="ef3b7-121">Displays hello response toohello direct method call sent by hello simulated device</span></span>
* <span data-ttu-id="ef3b7-122">Geeft Hallo bijgewerkt gerapporteerd eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="ef3b7-122">Displays hello updated reported properties.</span></span>

> [!NOTE]
> <span data-ttu-id="ef3b7-123">Zie voor informatie over Hallo SDK's die u toobuild toepassingen toorun op apparaten en de back-end van uw oplossing gebruiken kunt [Azure IoT SDK's][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="ef3b7-123">For information about hello SDKs that you can use toobuild applications toorun on devices and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="ef3b7-124">toocomplete deze zelfstudie hebt u nodig:</span><span class="sxs-lookup"><span data-stu-id="ef3b7-124">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="ef3b7-125">Java SE 8.</span><span class="sxs-lookup"><span data-stu-id="ef3b7-125">Java SE 8.</span></span> <br/> <span data-ttu-id="ef3b7-126">[Uw ontwikkelingsomgeving voorbereiden] [ lnk-dev-setup] wordt beschreven hoe tooinstall Java voor deze zelfstudie op Windows of Linux.</span><span class="sxs-lookup"><span data-stu-id="ef3b7-126">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Java for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="ef3b7-127">Maven 3.</span><span class="sxs-lookup"><span data-stu-id="ef3b7-127">Maven 3.</span></span>  <br/> <span data-ttu-id="ef3b7-128">[Uw ontwikkelingsomgeving voorbereiden] [ lnk-dev-setup] wordt beschreven hoe tooinstall [Maven] [ lnk-maven] voor deze zelfstudie op Windows of Linux.</span><span class="sxs-lookup"><span data-stu-id="ef3b7-128">[Prepare your development environment][lnk-dev-setup] describes how tooinstall [Maven][lnk-maven] for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="ef3b7-129">[Node.js-versie 0.10.0 of hoger](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="ef3b7-129">[Node.js version 0.10.0 or later](http://nodejs.org).</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a><span data-ttu-id="ef3b7-130">Activeren van een extern opnieuw opstarten op Hallo-apparaat met een directe methode</span><span class="sxs-lookup"><span data-stu-id="ef3b7-130">Trigger a remote reboot on hello device using a direct method</span></span>

<span data-ttu-id="ef3b7-131">In deze sectie maakt u een Java-consoletoepassing maken die:</span><span class="sxs-lookup"><span data-stu-id="ef3b7-131">In this section, you create a Java console app that:</span></span>

1. <span data-ttu-id="ef3b7-132">Roept Hallo directe methode in de gesimuleerde apparaattoepassing Hallo van opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="ef3b7-132">Invokes hello reboot direct method in hello simulated device app.</span></span>
1. <span data-ttu-id="ef3b7-133">Geeft antwoord Hallo weer.</span><span class="sxs-lookup"><span data-stu-id="ef3b7-133">Displays hello response.</span></span>
1. <span data-ttu-id="ef3b7-134">Polls Hallo gerapporteerd eigenschappen is verzonden vanaf Hallo apparaat toodetermine wanneer Hallo opnieuw opstarten voltooid is.</span><span class="sxs-lookup"><span data-stu-id="ef3b7-134">Polls hello reported properties sent from hello device toodetermine when hello reboot is complete.</span></span>

<span data-ttu-id="ef3b7-135">Deze consoletoepassing verbindt tooyour IoT Hub gerapporteerde tooinvoke Hallo directe methode en lezen Hallo eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="ef3b7-135">This console app connects tooyour IoT Hub tooinvoke hello direct method and read hello reported properties.</span></span>

1. <span data-ttu-id="ef3b7-136">Maak een lege map dm-get-started.</span><span class="sxs-lookup"><span data-stu-id="ef3b7-136">Create an empty folder called dm-get-started.</span></span>

1. <span data-ttu-id="ef3b7-137">Maak in map dm-get-started Hallo een Maven-project aangeroepen **trigger-reboot** met behulp van de volgende opdracht achter de opdrachtprompt Hallo.</span><span class="sxs-lookup"><span data-stu-id="ef3b7-137">In hello dm-get-started folder, create a Maven project called **trigger-reboot** using hello following command at your command prompt.</span></span> <span data-ttu-id="ef3b7-138">Hallo hieronder vindt u een enkele, lange opdracht:</span><span class="sxs-lookup"><span data-stu-id="ef3b7-138">hello following shows a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=trigger-reboot -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="ef3b7-139">Navigeer toohello trigger-reboot map bij de opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="ef3b7-139">At your command prompt, navigate toohello trigger-reboot folder.</span></span>

1. <span data-ttu-id="ef3b7-140">Met een teksteditor, open Hallo pom.xml-bestand in Hallo trigger-reboot map en Hallo afhankelijkheid toohello na toevoegen **afhankelijkheden** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="ef3b7-140">Using a text editor, open hello pom.xml file in hello trigger-reboot folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="ef3b7-141">Deze afhankelijkheid kunt u toouse Hallo iot-service-client-pakket in uw app toocommunicate met uw IoT-hub:</span><span class="sxs-lookup"><span data-stu-id="ef3b7-141">This dependency enables you toouse hello iot-service-client package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="ef3b7-142">U kunt controleren op de meest recente versie van Hallo **iot-service-client** met [Maven search][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="ef3b7-142">You can check for hello latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

1. <span data-ttu-id="ef3b7-143">Voeg de volgende Hallo **bouwen** knooppunt na Hallo **afhankelijkheden** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="ef3b7-143">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="ef3b7-144">Deze configuratie wordt Java-Maven toouse 1.8 toobuild Hallo app:</span><span class="sxs-lookup"><span data-stu-id="ef3b7-144">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="ef3b7-145">Opslaan en sluiten Hallo pom.xml-bestand.</span><span class="sxs-lookup"><span data-stu-id="ef3b7-145">Save and close hello pom.xml file.</span></span>

1. <span data-ttu-id="ef3b7-146">Open met een teksteditor Hallo trigger-reboot\src\main\java\com\mycompany\app\App.java bronbestand.</span><span class="sxs-lookup"><span data-stu-id="ef3b7-146">Using a text editor, open hello trigger-reboot\src\main\java\com\mycompany\app\App.java source file.</span></span>

1. <span data-ttu-id="ef3b7-147">Voeg de volgende Hallo **importeren** instructies toohello bestand:</span><span class="sxs-lookup"><span data-stu-id="ef3b7-147">Add hello following **import** statements toohello file:</span></span>

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

1. <span data-ttu-id="ef3b7-148">Hallo klasseniveau variabelen toohello na toevoegen **App** klasse.</span><span class="sxs-lookup"><span data-stu-id="ef3b7-148">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="ef3b7-149">Vervang `{youriothubconnectionstring}` met uw IoT hub-verbindingsreeks die u hebt genoteerd in Hallo *een IoT Hub maken* sectie:</span><span class="sxs-lookup"><span data-stu-id="ef3b7-149">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in hello *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    private static final String methodName = "reboot";
    private static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    private static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    ```

1. <span data-ttu-id="ef3b7-150">een thread die Hallo leest tooimplement gerapporteerd eigenschappen van Hallo apparaat twin Voeg elke 10 seconden Hallo volgende geneste klasse toohello **App** klasse:</span><span class="sxs-lookup"><span data-stu-id="ef3b7-150">tooimplement a thread that reads hello reported properties from hello device twin every 10 seconds, add hello following nested class toohello **App** class:</span></span>

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

1. <span data-ttu-id="ef3b7-151">tooinvoke Hallo opnieuw opstarten directe methode op Hallo gesimuleerd apparaat toevoegen Hallo code toohello na **belangrijkste** methode:</span><span class="sxs-lookup"><span data-stu-id="ef3b7-151">tooinvoke hello reboot direct method on hello simulated device, add hello following code toohello **main** method:</span></span>

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

1. <span data-ttu-id="ef3b7-152">toostart Hallo thread toopoll Hallo gemelde eigenschappen van het gesimuleerde apparaat hello, toevoegen na de code toohello Hallo **belangrijkste** methode:</span><span class="sxs-lookup"><span data-stu-id="ef3b7-152">toostart hello thread toopoll hello reported properties from hello simulated device, add hello following code toohello **main** method:</span></span>

    ```java
    ShowReportedProperties showReportedProperties = new ShowReportedProperties();
    ExecutorService executor = Executors.newFixedThreadPool(1);
    executor.execute(showReportedProperties);
    ```

1. <span data-ttu-id="ef3b7-153">tooenable u toostop Hallo-app toevoegen na de code toohello Hallo **belangrijkste** methode:</span><span class="sxs-lookup"><span data-stu-id="ef3b7-153">tooenable you toostop hello app, add hello following code toohello **main** method:</span></span>

    ```java
    System.out.println("Press ENTER tooexit.");
    System.in.read();
    executor.shutdownNow();
    System.out.println("Shutting down sample...");
    ```

1. <span data-ttu-id="ef3b7-154">Opslaan en sluiten Hallo trigger-reboot\src\main\java\com\mycompany\app\App.java bestand.</span><span class="sxs-lookup"><span data-stu-id="ef3b7-154">Save and close hello trigger-reboot\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="ef3b7-155">Hallo bouwen **trigger-reboot** back-endserver voor Apps en eventuele fouten te corrigeren.</span><span class="sxs-lookup"><span data-stu-id="ef3b7-155">Build hello **trigger-reboot** back-end app and correct any errors.</span></span> <span data-ttu-id="ef3b7-156">Navigeer toohello trigger-reboot map en Voer Hallo volgende opdracht achter de opdrachtprompt:</span><span class="sxs-lookup"><span data-stu-id="ef3b7-156">At your command prompt, navigate toohello trigger-reboot folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="ef3b7-157">Een gesimuleerde apparaattoepassing maken</span><span class="sxs-lookup"><span data-stu-id="ef3b7-157">Create a simulated device app</span></span>

<span data-ttu-id="ef3b7-158">In deze sectie maakt u een Java-consoletoepassing die een apparaat simuleert.</span><span class="sxs-lookup"><span data-stu-id="ef3b7-158">In this section, you create a Java console app that simulates a device.</span></span> <span data-ttu-id="ef3b7-159">Hallo app luistert naar Hallo opnieuw opstarten directe methode-aanroep van uw IoT-hub en onmiddellijk reageert toothat aanroep.</span><span class="sxs-lookup"><span data-stu-id="ef3b7-159">hello app listens for hello reboot direct method call from your IoT hub and immediately responds toothat call.</span></span> <span data-ttu-id="ef3b7-160">Hallo-app en vervolgens de inactieve modus inschakelt voor een tijdje toosimulate Hallo opnieuw opstarten proces voordat gebruikmaakt van een gerapporteerde eigenschap toonotify hello **trigger-reboot** back-end-app die Hallo opnieuw opstarten is voltooid.</span><span class="sxs-lookup"><span data-stu-id="ef3b7-160">hello app then sleeps for a while toosimulate hello reboot process before it uses a reported property toonotify hello **trigger-reboot** back-end app that hello reboot is complete.</span></span>

1. <span data-ttu-id="ef3b7-161">Maak in map dm-get-started Hallo een Maven-project aangeroepen **simulated-device** met behulp van de volgende opdracht achter de opdrachtprompt Hallo.</span><span class="sxs-lookup"><span data-stu-id="ef3b7-161">In hello dm-get-started folder, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="ef3b7-162">Hallo hieronder vindt u een enkele, lange opdracht:</span><span class="sxs-lookup"><span data-stu-id="ef3b7-162">hello following is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="ef3b7-163">Ga bij de opdrachtprompt de map simulated-device toohello.</span><span class="sxs-lookup"><span data-stu-id="ef3b7-163">At your command prompt, navigate toohello simulated-device folder.</span></span>

1. <span data-ttu-id="ef3b7-164">Met een teksteditor Hallo pom.xml-bestand openen in de map simulated-device Hallo en toevoegen van Hallo afhankelijkheid toohello na **afhankelijkheden** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="ef3b7-164">Using a text editor, open hello pom.xml file in hello simulated-device folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="ef3b7-165">Deze afhankelijkheid kunt u toouse Hallo iot-service-client-pakket in uw app toocommunicate met uw IoT-hub:</span><span class="sxs-lookup"><span data-stu-id="ef3b7-165">This dependency enables you toouse hello iot-service-client package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="ef3b7-166">U kunt controleren op de meest recente versie van Hallo **iot-apparaat-client** met [Maven search][lnk-maven-device-search].</span><span class="sxs-lookup"><span data-stu-id="ef3b7-166">You can check for hello latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

1. <span data-ttu-id="ef3b7-167">Voeg de volgende Hallo **bouwen** knooppunt na Hallo **afhankelijkheden** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="ef3b7-167">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="ef3b7-168">Deze configuratie wordt Java-Maven toouse 1.8 toobuild Hallo app:</span><span class="sxs-lookup"><span data-stu-id="ef3b7-168">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="ef3b7-169">Opslaan en sluiten Hallo pom.xml-bestand.</span><span class="sxs-lookup"><span data-stu-id="ef3b7-169">Save and close hello pom.xml file.</span></span>

1. <span data-ttu-id="ef3b7-170">Open met een teksteditor Hallo simulated-device\src\main\java\com\mycompany\app\App.java bronbestand.</span><span class="sxs-lookup"><span data-stu-id="ef3b7-170">Using a text editor, open hello simulated-device\src\main\java\com\mycompany\app\App.java source file.</span></span>

1. <span data-ttu-id="ef3b7-171">Voeg de volgende Hallo **importeren** instructies toohello bestand:</span><span class="sxs-lookup"><span data-stu-id="ef3b7-171">Add hello following **import** statements toohello file:</span></span>

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

1. <span data-ttu-id="ef3b7-172">Hallo klasseniveau variabelen toohello na toevoegen **App** klasse.</span><span class="sxs-lookup"><span data-stu-id="ef3b7-172">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="ef3b7-173">Vervang `{yourdeviceconnectionstring}` met Hallo apparaat-verbindingsreeks hebt genoteerd in Hallo *maken van een apparaat-id* sectie:</span><span class="sxs-lookup"><span data-stu-id="ef3b7-173">Replace `{yourdeviceconnectionstring}` with hello device connection string you noted in hello *Create a device identity* section:</span></span>

    ```java
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;

    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String connString = "{yourdeviceconnectionstring}";
    private static DeviceClient client;
    ```

1. <span data-ttu-id="ef3b7-174">tooimplement een retouraanroep-handler voor directe methode statusgebeurtenissen, voeg Hallo volgende geneste klasse toohello **App** klasse:</span><span class="sxs-lookup"><span data-stu-id="ef3b7-174">tooimplement a callback handler for direct method status events, add hello following nested class toohello **App** class:</span></span>

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded toodevice method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="ef3b7-175">tooimplement een retouraanroep-handler voor apparaat twin statusgebeurtenissen, voeg Hallo volgende geneste klasse toohello **App** klasse:</span><span class="sxs-lookup"><span data-stu-id="ef3b7-175">tooimplement a callback handler for device twin status events, add hello following nested class toohello **App** class:</span></span>

    ```java
    protected static class DeviceTwinStatusCallback implements IotHubEventCallback
    {
        public void execute(IotHubStatusCode status, Object context)
        {
            System.out.println("IoT Hub responded toodevice twin operation with status " + status.name());
        }
    }
    ```

1. <span data-ttu-id="ef3b7-176">tooimplement een retouraanroep-handler voor gebeurtenissen van de eigenschap, voeg Hallo volgende geneste klasse toohello **App** klasse:</span><span class="sxs-lookup"><span data-stu-id="ef3b7-176">tooimplement a callback handler for property events, add hello following nested class toohello **App** class:</span></span>

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

1. <span data-ttu-id="ef3b7-177">tooimplement thread toosimulate Hallo apparaat opnieuw worden opgestart, voeg Hallo volgende geneste klasse toohello **App** klasse.</span><span class="sxs-lookup"><span data-stu-id="ef3b7-177">tooimplement a thread toosimulate hello device reboot, add hello following nested class toohello **App** class.</span></span> <span data-ttu-id="ef3b7-178">Hallo thread modus ingeschakeld gedurende vijf seconden en vervolgens stelt Hallo **lastReboot** eigenschap gerapporteerd:</span><span class="sxs-lookup"><span data-stu-id="ef3b7-178">hello thread sleeps for five seconds and then sets hello **lastReboot** reported property:</span></span>

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

1. <span data-ttu-id="ef3b7-179">tooimplement hello directe methode op Hallo-apparaat, voeg Hallo volgende geneste klasse toohello **App** klasse.</span><span class="sxs-lookup"><span data-stu-id="ef3b7-179">tooimplement hello direct method on hello device, add hello following nested class toohello **App** class.</span></span> <span data-ttu-id="ef3b7-180">Wanneer Hallo gesimuleerde app ontvangt voor een aanroep van toohello **opnieuw opstarten** directe methode wordt een bevestiging toohello beller en start vervolgens begint een thread tooprocess Hallo opnieuw:</span><span class="sxs-lookup"><span data-stu-id="ef3b7-180">When hello simulated app receives a call toohello **reboot** direct method, it returns an acknowledgement toohello caller and then starts a thread tooprocess hello reboot:</span></span>

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

1. <span data-ttu-id="ef3b7-181">Wijzig de handtekening Hallo Hallo **belangrijkste** methode toothrow Hallo volgende uitzonderingen:</span><span class="sxs-lookup"><span data-stu-id="ef3b7-181">Modify hello signature of hello **main** method toothrow hello following exceptions:</span></span>

    ```java
    public static void main(String[] args) throws IOException, URISyntaxException
    ```

1. <span data-ttu-id="ef3b7-182">tooinstantiate een **DeviceClient**, toevoegen na de code toohello Hallo **belangrijkste** methode:</span><span class="sxs-lookup"><span data-stu-id="ef3b7-182">tooinstantiate a **DeviceClient**, add hello following code toohello **main** method:</span></span>

    ```java
    System.out.println("Starting device client sample...");
    client = new DeviceClient(connString, protocol);
    ```

1. <span data-ttu-id="ef3b7-183">toostart luisteren voor directe methode-aanroepen toevoegen na de code toohello Hallo **belangrijkste** methode:</span><span class="sxs-lookup"><span data-stu-id="ef3b7-183">toostart listening for direct method calls, add hello following code toohello **main** method:</span></span>

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

1. <span data-ttu-id="ef3b7-184">tooshut omlaag apparaatsimulator hello, toevoegen na de code toohello Hallo **belangrijkste** methode:</span><span class="sxs-lookup"><span data-stu-id="ef3b7-184">tooshut down hello device simulator, add hello following code toohello **main** method:</span></span>

    ```java
    System.out.println("Press any key tooexit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    scanner.close();
    client.close();
    System.out.println("Shutting down...");
    ```

1. <span data-ttu-id="ef3b7-185">Opslaan en sluiten van de bestand simulated-device\src\main\java\com\mycompany\app\App.java Hallo.</span><span class="sxs-lookup"><span data-stu-id="ef3b7-185">Save and close hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="ef3b7-186">Hallo bouwen **simulated-device** back-endserver voor Apps en eventuele fouten te corrigeren.</span><span class="sxs-lookup"><span data-stu-id="ef3b7-186">Build hello **simulated-device** back-end app and correct any errors.</span></span> <span data-ttu-id="ef3b7-187">Ga bij de opdrachtprompt de map simulated-device toohello en Voer Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="ef3b7-187">At your command prompt, navigate toohello simulated-device folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a><span data-ttu-id="ef3b7-188">Hallo-apps uitvoeren</span><span class="sxs-lookup"><span data-stu-id="ef3b7-188">Run hello apps</span></span>

<span data-ttu-id="ef3b7-189">U bent nu klaar toorun Hallo apps.</span><span class="sxs-lookup"><span data-stu-id="ef3b7-189">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="ef3b7-190">Voer bij een opdrachtprompt in de map simulated-device Hallo Hallo opdracht toobegin luisteren naar de methodeaanroepen opnieuw opstarten van uw IoT-hub te volgen:</span><span class="sxs-lookup"><span data-stu-id="ef3b7-190">At a command prompt in hello simulated-device folder, run hello following command toobegin listening for reboot method calls from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![IoT Hub voor Java gesimuleerd apparaat app toolisten voor opnieuw opstarten directe methodeaanroepen][1]

1. <span data-ttu-id="ef3b7-192">Voer bij een opdrachtprompt in Hallo trigger-reboot map Hallo volgende opdracht toocall Hallo opnieuw opstarten methode op uw gesimuleerde apparaat uit uw IoT-hub:</span><span class="sxs-lookup"><span data-stu-id="ef3b7-192">At a command prompt in hello trigger-reboot folder, run hello following command toocall hello reboot method on your simulated device from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![IoT Hub voor Java service app toocall Hallo directe methode opnieuw opstarten][2]

1. <span data-ttu-id="ef3b7-194">Hallo gesimuleerd apparaat reageert toohello opnieuw opstarten directe methode aanroepen:</span><span class="sxs-lookup"><span data-stu-id="ef3b7-194">hello simulated device responds toohello reboot direct method call:</span></span>

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