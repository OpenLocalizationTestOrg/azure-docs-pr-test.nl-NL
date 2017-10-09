---
title: Azure IoT Hub aaaUse directe methoden (Java) | Microsoft Docs
description: Hoe Azure IoT Hub toouse directe methoden. U gebruikt hello Azure IoT-device SDK voor Java tooimplement een gesimuleerde apparaattoepassing met een directe methode en hello Azure IoT service SDK voor Java tooimplement een service-app die Hallo directe methode aanroept.
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: b6f2f4a64535ab649a3965cd9c5a19bebaf88eef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-java"></a><span data-ttu-id="1a137-104">Directe methoden (Java) gebruiken</span><span class="sxs-lookup"><span data-stu-id="1a137-104">Use direct methods (Java)</span></span>

[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="1a137-105">In deze zelfstudie maakt maken u twee console Java-apps:</span><span class="sxs-lookup"><span data-stu-id="1a137-105">In this tutorial, you create two Java console apps:</span></span>

* <span data-ttu-id="1a137-106">**Invoke-direct-method**, een Java-back-end-app die een methode wordt aangeroepen in de gesimuleerde apparaattoepassing Hallo en antwoord Hallo weergeeft.</span><span class="sxs-lookup"><span data-stu-id="1a137-106">**invoke-direct-method**, a Java back-end app that calls a method in hello simulated device app and displays hello response.</span></span>
* <span data-ttu-id="1a137-107">**simulated-device**, een Java-app die een apparaat verbinding te maken tooyour iothub met Hallo apparaat-id hebt u simuleert.</span><span class="sxs-lookup"><span data-stu-id="1a137-107">**simulated-device**, a Java app that simulates a device connecting tooyour IoT hub with hello device identity you create.</span></span> <span data-ttu-id="1a137-108">Deze app reageert toohello direct worden aangeroepen vanuit de back-end Hallo.</span><span class="sxs-lookup"><span data-stu-id="1a137-108">This app responds toohello direct invoked from hello back end.</span></span>

> [!NOTE]
> <span data-ttu-id="1a137-109">Zie voor informatie over Hallo SDK's die u toobuild toepassingen toorun op apparaten en de back-end van uw oplossing gebruiken kunt [Azure IoT SDK's][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="1a137-109">For information about hello SDKs that you can use toobuild applications toorun on devices and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="1a137-110">toocomplete deze zelfstudie hebt u nodig:</span><span class="sxs-lookup"><span data-stu-id="1a137-110">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="1a137-111">Java SE 8.</span><span class="sxs-lookup"><span data-stu-id="1a137-111">Java SE 8.</span></span> <br/> <span data-ttu-id="1a137-112">[Uw ontwikkelingsomgeving voorbereiden] [ lnk-dev-setup] wordt beschreven hoe tooinstall Java voor deze zelfstudie op Windows of Linux.</span><span class="sxs-lookup"><span data-stu-id="1a137-112">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Java for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="1a137-113">Maven 3.</span><span class="sxs-lookup"><span data-stu-id="1a137-113">Maven 3.</span></span>  <br/> <span data-ttu-id="1a137-114">[Uw ontwikkelingsomgeving voorbereiden] [ lnk-dev-setup] wordt beschreven hoe tooinstall [Maven] [ lnk-maven] voor deze zelfstudie op Windows of Linux.</span><span class="sxs-lookup"><span data-stu-id="1a137-114">[Prepare your development environment][lnk-dev-setup] describes how tooinstall [Maven][lnk-maven] for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="1a137-115">[Node.js-versie 0.10.0 of hoger](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="1a137-115">[Node.js version 0.10.0 or later](http://nodejs.org).</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="1a137-116">Een gesimuleerde apparaattoepassing maken</span><span class="sxs-lookup"><span data-stu-id="1a137-116">Create a simulated device app</span></span>

<span data-ttu-id="1a137-117">In deze sectie maakt u een Java-consoletoepassing die tooa methode aangeroepen door Hallo oplossing terug end reageert.</span><span class="sxs-lookup"><span data-stu-id="1a137-117">In this section, you create a Java console app that responds tooa method called by hello solution back end.</span></span>

1. <span data-ttu-id="1a137-118">Maak een lege map genaamd iot-java-direct-methode.</span><span class="sxs-lookup"><span data-stu-id="1a137-118">Create an empty folder called iot-java-direct-method.</span></span>

1. <span data-ttu-id="1a137-119">Maak een Maven-project aangeroepen in Hallo iot-java-direct-method **simulated-device** met behulp van de volgende opdracht achter de opdrachtprompt Hallo.</span><span class="sxs-lookup"><span data-stu-id="1a137-119">In hello iot-java-direct-method folder, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="1a137-120">Hallo na de opdracht is een enkele, lange opdracht:</span><span class="sxs-lookup"><span data-stu-id="1a137-120">hello following command is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="1a137-121">Ga bij de opdrachtprompt de map simulated-device toohello.</span><span class="sxs-lookup"><span data-stu-id="1a137-121">At your command prompt, navigate toohello simulated-device folder.</span></span>

1. <span data-ttu-id="1a137-122">Met een teksteditor Hallo pom.xml-bestand openen in de map simulated-device Hallo en toevoegen van Hallo afhankelijkheden toohello na **afhankelijkheden** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="1a137-122">Using a text editor, open hello pom.xml file in hello simulated-device folder and add hello following dependencies toohello **dependencies** node.</span></span> <span data-ttu-id="1a137-123">Deze afhankelijkheid kunt u toouse Hallo iot-apparaat-client-pakket in uw app toocommunicate met uw IoT-hub:</span><span class="sxs-lookup"><span data-stu-id="1a137-123">This dependency enables you toouse hello iot-device-client package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="1a137-124">U kunt controleren op de meest recente versie van Hallo **iot-apparaat-client** met [Maven search][lnk-maven-device-search].</span><span class="sxs-lookup"><span data-stu-id="1a137-124">You can check for hello latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

1. <span data-ttu-id="1a137-125">Voeg de volgende Hallo **bouwen** knooppunt na Hallo **afhankelijkheden** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="1a137-125">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="1a137-126">Deze configuratie wordt Java-Maven toouse 1.8 toobuild Hallo app:</span><span class="sxs-lookup"><span data-stu-id="1a137-126">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="1a137-127">Opslaan en sluiten Hallo pom.xml-bestand.</span><span class="sxs-lookup"><span data-stu-id="1a137-127">Save and close hello pom.xml file.</span></span>

1. <span data-ttu-id="1a137-128">Met een teksteditor Hallo simulated-device\src\main\java\com\mycompany\app\App.java bestand openen.</span><span class="sxs-lookup"><span data-stu-id="1a137-128">Using a text editor, open hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="1a137-129">Voeg de volgende Hallo **importeren** instructies toohello bestand:</span><span class="sxs-lookup"><span data-stu-id="1a137-129">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="1a137-130">Hallo klasseniveau variabelen toohello na toevoegen **App** klasse.</span><span class="sxs-lookup"><span data-stu-id="1a137-130">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="1a137-131">Vervangen van `{youriothubname}` met de naam van uw IoT-hub en `{yourdevicekey}` met Hallo apparaat sleutelwaarde u hebt gegenereerd in Hallo *maken van een apparaat-id* sectie:</span><span class="sxs-lookup"><span data-stu-id="1a137-131">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with hello device key value you generated in hello *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myDeviceId";
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    <span data-ttu-id="1a137-132">In dit voorbeeld-app gebruikt Hallo **protocol** variabele bij het instantiëren van een **DeviceClient** object.</span><span class="sxs-lookup"><span data-stu-id="1a137-132">This sample app uses hello **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="1a137-133">Op dit moment rechtstreeks toouse methoden u Hallo MQTT protocol moet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1a137-133">Currently, toouse direct methods you must use hello MQTT protocol.</span></span>

1. <span data-ttu-id="1a137-134">tooreturn een status code tooyour iothub, voeg Hallo volgende geneste klasse toohello **App** klasse:</span><span class="sxs-lookup"><span data-stu-id="1a137-134">tooreturn a status code tooyour IoT hub, add hello following nested class toohello **App** class:</span></span>

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded toodevice method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="1a137-135">toohandle hello directe methode aanroepen van Hallo back-end oplossing, voeg Hallo volgende geneste klasse toohello **App** klasse:</span><span class="sxs-lookup"><span data-stu-id="1a137-135">toohandle hello direct method invocations from hello solution back end, add hello following nested class toohello **App** class:</span></span>

    ```java
    protected static class DirectMethodCallback implements com.microsoft.azure.sdk.iot.device.DeviceTwin.DeviceMethodCallback
    {
      @Override
      public DeviceMethodData call(String methodName, Object methodData, Object context)
      {
        DeviceMethodData deviceMethodData;
        switch (methodName)
        {
          case "writeLine" :
          {
            int status = METHOD_SUCCESS;
            System.out.println(new String((byte[])methodData));
            deviceMethodData = new DeviceMethodData(status, "Executed direct method " + methodName);
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

1. <span data-ttu-id="1a137-136">toocreate een **DeviceClient** en luisteren naar directe methode aanroepen, het toevoegen van een **belangrijkste** methode toohello **App** klasse:</span><span class="sxs-lookup"><span data-stu-id="1a137-136">toocreate a **DeviceClient** and listen for direct method invocations, add a **main** method toohello **App** class:</span></span>

    ```java
    public static void main(String[] args)
      throws IOException, URISyntaxException
    {
      System.out.println("Starting device sample...");

      DeviceClient client = new DeviceClient(connString, protocol);

      try
      {
        client.open();
        client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
        System.out.println("Subscribed toodirect methods. Waiting...");
      }
      catch (Exception e)
      {
        System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" +  e.getMessage());
        client.close();
        System.out.println("Shutting down...");
      }

      System.out.println("Press any key tooexit...");
      Scanner scanner = new Scanner(System.in);
      scanner.nextLine();
      scanner.close();
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. <span data-ttu-id="1a137-137">Opslaan en sluiten van de bestand simulated-device\src\main\java\com\mycompany\app\App.java Hallo</span><span class="sxs-lookup"><span data-stu-id="1a137-137">Save and close hello simulated-device\src\main\java\com\mycompany\app\App.java file</span></span>

1. <span data-ttu-id="1a137-138">Hallo bouwen **simulated-device** app en eventuele fouten te corrigeren.</span><span class="sxs-lookup"><span data-stu-id="1a137-138">Build hello **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="1a137-139">Ga bij de opdrachtprompt de map simulated-device toohello en Voer Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="1a137-139">At your command prompt, navigate toohello simulated-device folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="1a137-140">Een directe methode is aangeroepen voor een apparaat</span><span class="sxs-lookup"><span data-stu-id="1a137-140">Call a direct method on a device</span></span>

<span data-ttu-id="1a137-141">In deze sectie maakt maken u een Java-consoletoepassing die een directe methode wordt aangeroepen en wordt vervolgens weergegeven antwoord Hallo.</span><span class="sxs-lookup"><span data-stu-id="1a137-141">In this section, you create a Java console app that invokes a direct method and then displays hello response.</span></span> <span data-ttu-id="1a137-142">Deze consoletoepassing verbindt tooyour IoT Hub tooinvoke Hallo directe methode.</span><span class="sxs-lookup"><span data-stu-id="1a137-142">This console app connects tooyour IoT Hub tooinvoke hello direct method.</span></span>

1. <span data-ttu-id="1a137-143">Maak een Maven-project aangeroepen in Hallo iot-java-direct-method **aanroepen directe methode** met behulp van de volgende opdracht achter de opdrachtprompt Hallo.</span><span class="sxs-lookup"><span data-stu-id="1a137-143">In hello iot-java-direct-method folder, create a Maven project called **invoke-direct-method** using hello following command at your command prompt.</span></span> <span data-ttu-id="1a137-144">Hallo na de opdracht is een enkele, lange opdracht:</span><span class="sxs-lookup"><span data-stu-id="1a137-144">hello following command is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=invoke-direct-method -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="1a137-145">Navigeer toohello aanroepen directe methode map bij de opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="1a137-145">At your command prompt, navigate toohello invoke-direct-method folder.</span></span>

1. <span data-ttu-id="1a137-146">Met een teksteditor, open Hallo pom.xml-bestand in Hallo aanroepen directe methode map en Hallo afhankelijkheid toohello na toevoegen **afhankelijkheden** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="1a137-146">Using a text editor, open hello pom.xml file in hello invoke-direct-method folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="1a137-147">Deze afhankelijkheid kunt u toouse Hallo iot-service-client-pakket in uw app toocommunicate met uw IoT-hub:</span><span class="sxs-lookup"><span data-stu-id="1a137-147">This dependency enables you toouse hello iot-service-client package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="1a137-148">U kunt controleren op de meest recente versie van Hallo **iot-service-client** met [Maven search][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="1a137-148">You can check for hello latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

1. <span data-ttu-id="1a137-149">Voeg de volgende Hallo **bouwen** knooppunt na Hallo **afhankelijkheden** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="1a137-149">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="1a137-150">Deze configuratie wordt Java-Maven toouse 1.8 toobuild Hallo app:</span><span class="sxs-lookup"><span data-stu-id="1a137-150">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="1a137-151">Opslaan en sluiten Hallo pom.xml-bestand.</span><span class="sxs-lookup"><span data-stu-id="1a137-151">Save and close hello pom.xml file.</span></span>

1. <span data-ttu-id="1a137-152">Met een teksteditor Hallo invoke-direct-method\src\main\java\com\mycompany\app\App.java bestand openen.</span><span class="sxs-lookup"><span data-stu-id="1a137-152">Using a text editor, open hello invoke-direct-method\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="1a137-153">Voeg de volgende Hallo **importeren** instructies toohello bestand:</span><span class="sxs-lookup"><span data-stu-id="1a137-153">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceMethod;
    import com.microsoft.azure.sdk.iot.service.devicetwin.MethodResult;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.concurrent.TimeUnit;
    ```

1. <span data-ttu-id="1a137-154">Hallo klasseniveau variabelen toohello na toevoegen **App** klasse.</span><span class="sxs-lookup"><span data-stu-id="1a137-154">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="1a137-155">Vervang `{youriothubconnectionstring}` met uw IoT hub-verbindingsreeks die u hebt genoteerd in Hallo *een IoT Hub maken* sectie:</span><span class="sxs-lookup"><span data-stu-id="1a137-155">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in hello *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String methodName = "writeLine";
    public static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    public static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    public static final String payload = "a line toobe written";
    ```

1. <span data-ttu-id="1a137-156">tooinvoke Hallo methode op Hallo gesimuleerde apparaat toevoegen Hallo na code toohello **belangrijkste** methode:</span><span class="sxs-lookup"><span data-stu-id="1a137-156">tooinvoke hello method on hello simulated device, add hello following code toohello **main** method:</span></span>

    ```java
    System.out.println("Starting sample...");
    DeviceMethod methodClient = DeviceMethod.createFromConnectionString(iotHubConnectionString);

    try
    {
        System.out.println("Invoke direct method");
        MethodResult result = methodClient.invoke(deviceId, methodName, responseTimeout, connectTimeout, payload);

        if(result == null)
        {
            throw new IOException("Direct method invoke returns null");
        }
        System.out.println("Status=" + result.getStatus());
        System.out.println("Payload=" + result.getPayload());
    }
    catch (IotHubException e)
    {
        System.out.println(e.getMessage());
    }

    System.out.println("Shutting down sample...");
    ```

1. <span data-ttu-id="1a137-157">Opslaan en sluiten Hallo invoke-direct-method\src\main\java\com\mycompany\app\App.java bestand</span><span class="sxs-lookup"><span data-stu-id="1a137-157">Save and close hello invoke-direct-method\src\main\java\com\mycompany\app\App.java file</span></span>

1. <span data-ttu-id="1a137-158">Hallo bouwen **aanroepen directe methode** app en eventuele fouten te corrigeren.</span><span class="sxs-lookup"><span data-stu-id="1a137-158">Build hello **invoke-direct-method** app and correct any errors.</span></span> <span data-ttu-id="1a137-159">Navigeer toohello aanroepen directe methode map en Voer Hallo volgende opdracht achter de opdrachtprompt:</span><span class="sxs-lookup"><span data-stu-id="1a137-159">At your command prompt, navigate toohello invoke-direct-method folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a><span data-ttu-id="1a137-160">Hallo-apps uitvoeren</span><span class="sxs-lookup"><span data-stu-id="1a137-160">Run hello apps</span></span>

<span data-ttu-id="1a137-161">U bent nu klaar toorun Hallo console apps.</span><span class="sxs-lookup"><span data-stu-id="1a137-161">You are now ready toorun hello console apps.</span></span>

1. <span data-ttu-id="1a137-162">Voer bij een opdrachtprompt in de map simulated-device Hallo Hallo opdracht toobegin luisteren naar methodeaanroepen van uw IoT-hub te volgen:</span><span class="sxs-lookup"><span data-stu-id="1a137-162">At a command prompt in hello simulated-device folder, run hello following command toobegin listening for method calls from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![IoT Hub voor Java gesimuleerd apparaat app toolisten voor directe methodeaanroepen][8]

1. <span data-ttu-id="1a137-164">Bij een opdrachtprompt in Hallo aanroepen directe methode map Hallo opdracht toocall na een methode uitvoeren op uw gesimuleerde apparaat uit uw IoT-hub:</span><span class="sxs-lookup"><span data-stu-id="1a137-164">At a command prompt in hello invoke-direct-method folder, run hello following command toocall a method on your simulated device from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![IoT Hub voor Java service app toocall een directe methode][7]

1. <span data-ttu-id="1a137-166">Hallo gesimuleerd apparaat reageert toohello directe methode aanroepen:</span><span class="sxs-lookup"><span data-stu-id="1a137-166">hello simulated device responds toohello direct method call:</span></span>

    ![De gesimuleerde apparaattoepassing IoT-Hub voor Java reageert toohello directe methode-aanroep][9]

## <a name="next-steps"></a><span data-ttu-id="1a137-168">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1a137-168">Next steps</span></span>

<span data-ttu-id="1a137-169">In deze zelfstudie maakt u een nieuwe iothub geconfigureerd in hello Azure-portal en vervolgens een apparaat-id in de id-register Hallo iothub hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1a137-169">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="1a137-170">U hebt deze apparaat-id tooenable Hallo gesimuleerd apparaat app tooreact toomethods aangeroepen door Hallo cloud gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1a137-170">You used this device identity tooenable hello simulated device app tooreact toomethods invoked by hello cloud.</span></span> <span data-ttu-id="1a137-171">Hebt u ook een app die wordt aangeroepen methoden op Hallo apparaat en geeft weer Hallo-antwoord van Hallo-apparaat hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1a137-171">You also created an app that invokes methods on hello device and displays hello response from hello device.</span></span>

<span data-ttu-id="1a137-172">tooexplore andere IoT-scenario's, Zie [plannen van taken op meerdere apparaten][lnk-devguide-jobs].</span><span class="sxs-lookup"><span data-stu-id="1a137-172">tooexplore other IoT scenarios, see [Schedule jobs on multiple devices][lnk-devguide-jobs].</span></span>

<span data-ttu-id="1a137-173">toolearn hoe tooextend uw IoT-oplossing en schema-methode aanroepen op meerdere apparaten, raadpleegt u Hallo [planning en broadcast taken] [ lnk-tutorial-jobs] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="1a137-173">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

<!-- Images. -->
[7]: ./media/iot-hub-java-java-direct-methods/invoke-method.png
[8]: ./media/iot-hub-java-java-direct-methods/device-listen.png
[9]: ./media/iot-hub-java-java-direct-methods/device-respond.png

<!-- Links -->
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java/blob/master/doc/java-devbox-setup.md
[lnk-maven]: https://maven.apache.org/what-is-maven.html
[lnk-hub-sdks]: iot-hub-devguide-sdks.md

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-device-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
