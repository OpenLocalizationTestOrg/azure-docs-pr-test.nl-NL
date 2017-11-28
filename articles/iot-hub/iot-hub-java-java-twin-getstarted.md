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
# <a name="get-started-with-device-twins-java"></a><span data-ttu-id="7381f-104">Aan de slag met apparaat horende (Java)</span><span class="sxs-lookup"><span data-stu-id="7381f-104">Get started with device twins (Java)</span></span>

[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="7381f-105">In deze zelfstudie maakt maken u twee console Java-apps:</span><span class="sxs-lookup"><span data-stu-id="7381f-105">In this tutorial, you create two Java console apps:</span></span>

* <span data-ttu-id="7381f-106">**toevoegen-tags-query**, een Java-back-end-app die labels toegevoegd en wordt opgevraagd horende apparaten.</span><span class="sxs-lookup"><span data-stu-id="7381f-106">**add-tags-query**, a Java back-end app that adds tags and queries device twins.</span></span>
* <span data-ttu-id="7381f-107">**simulated-device**, een Java-apparaat-app of die een verbinding maakt tooyour iothub en rapporten zijn connectiviteit toestand met een eigenschap gemeld.</span><span class="sxs-lookup"><span data-stu-id="7381f-107">**simulated-device**, a Java device app that that connects tooyour IoT hub and reports its connectivity condition using a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="7381f-108">Hallo artikel [Azure IoT SDK's](iot-hub-devguide-sdks.md) bevat informatie over hello Azure IoT SDK's waarmee u toobuild kunt apparaat- en back-end-apps.</span><span class="sxs-lookup"><span data-stu-id="7381f-108">hello article [Azure IoT SDKs](iot-hub-devguide-sdks.md) provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>

<span data-ttu-id="7381f-109">toocomplete deze zelfstudie hebt u nodig:</span><span class="sxs-lookup"><span data-stu-id="7381f-109">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="7381f-110">meest recente Hallo [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="7381f-110">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="7381f-111">Maven 3</span><span class="sxs-lookup"><span data-stu-id="7381f-111">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="7381f-112">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="7381f-112">An active Azure account.</span></span> <span data-ttu-id="7381f-113">(Als u geen account hebt, kunt u een [gratis account](http://azure.microsoft.com/pricing/free-trial/) binnen een paar minuten.)</span><span class="sxs-lookup"><span data-stu-id="7381f-113">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="7381f-114">Desgewenst toocreate Hallo apparaat-id programmatisch lezen Hallo overeenkomstige sectie in Hallo [verbinding maken met uw apparaat tooyour iothub met Java](iot-hub-java-java-getstarted.md#create-a-device-identity) artikel.</span><span class="sxs-lookup"><span data-stu-id="7381f-114">If you prefer toocreate hello device identity programmatically, read hello corresponding section in hello [Connect your device tooyour IoT hub using Java](iot-hub-java-java-getstarted.md#create-a-device-identity) article.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="7381f-115">Hallo-service-app maken</span><span class="sxs-lookup"><span data-stu-id="7381f-115">Create hello service app</span></span>

<span data-ttu-id="7381f-116">In deze sectie maakt u een Java-app die locatie metagegevens toegevoegd, zoals een tag toohello apparaat twin in IoT-Hub die zijn gekoppeld aan **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="7381f-116">In this section, you create a Java app that adds location metadata as a tag toohello device twin in IoT Hub associated with **myDeviceId**.</span></span> <span data-ttu-id="7381f-117">Hallo app eerst een query uit iothub voor apparaten die zich bevinden in VS Hallo en voor apparaten die rapporteren van de verbinding van een mobiel netwerk.</span><span class="sxs-lookup"><span data-stu-id="7381f-117">hello app first queries IoT hub for devices located in hello US, and then for devices that report a cellular network connection.</span></span>

1. <span data-ttu-id="7381f-118">Maak een lege map genaamd op uw ontwikkelcomputer `iot-java-twin-getstarted`.</span><span class="sxs-lookup"><span data-stu-id="7381f-118">On your development machine, create an empty folder called `iot-java-twin-getstarted`.</span></span>

1. <span data-ttu-id="7381f-119">In Hallo `iot-java-twin-getstarted` map, maak een Maven-project aangeroepen **toevoegen-tags-query** met behulp van de volgende opdracht achter de opdrachtprompt Hallo.</span><span class="sxs-lookup"><span data-stu-id="7381f-119">In hello `iot-java-twin-getstarted` folder, create a Maven project called **add-tags-query** using hello following command at your command prompt.</span></span> <span data-ttu-id="7381f-120">Let op: dit is één enkele, lange opdracht:</span><span class="sxs-lookup"><span data-stu-id="7381f-120">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=add-tags-query -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="7381f-121">Ga bij de opdrachtprompt toohello `add-tags-query` map.</span><span class="sxs-lookup"><span data-stu-id="7381f-121">At your command prompt, navigate toohello `add-tags-query` folder.</span></span>

1. <span data-ttu-id="7381f-122">Met een teksteditor openen Hallo `pom.xml` bestand in Hallo `add-tags-query` map en Voeg na afhankelijkheid toohello hello **afhankelijkheden** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="7381f-122">Using a text editor, open hello `pom.xml` file in hello `add-tags-query` folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="7381f-123">Deze afhankelijkheid kunt u toouse hello **iot-service-client** pakket in uw app toocommunicate met uw IoT-hub:</span><span class="sxs-lookup"><span data-stu-id="7381f-123">This dependency enables you toouse hello **iot-service-client** package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="7381f-124">U kunt controleren op de meest recente versie van Hallo **iot-service-client** met [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="7381f-124">You can check for hello latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="7381f-125">Voeg de volgende Hallo **bouwen** knooppunt na Hallo **afhankelijkheden** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="7381f-125">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="7381f-126">Deze configuratie wordt Java-Maven toouse 1.8 toobuild Hallo app:</span><span class="sxs-lookup"><span data-stu-id="7381f-126">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="7381f-127">Opslaan en sluiten Hallo `pom.xml` bestand.</span><span class="sxs-lookup"><span data-stu-id="7381f-127">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="7381f-128">Met een teksteditor openen Hallo `add-tags-query\src\main\java\com\mycompany\app\App.java` bestand.</span><span class="sxs-lookup"><span data-stu-id="7381f-128">Using a text editor, open hello `add-tags-query\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="7381f-129">Voeg de volgende Hallo **importeren** instructies toohello bestand:</span><span class="sxs-lookup"><span data-stu-id="7381f-129">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.*;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.HashSet;
    import java.util.Set;
    ```

1. <span data-ttu-id="7381f-130">Hallo klasseniveau variabelen toohello na toevoegen **App** klasse.</span><span class="sxs-lookup"><span data-stu-id="7381f-130">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="7381f-131">Vervang `{youriothubconnectionstring}` met uw IoT hub-verbindingsreeks die u hebt genoteerd in Hallo *een IoT Hub maken* sectie:</span><span class="sxs-lookup"><span data-stu-id="7381f-131">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in hello *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String region = "US";
    public static final String plant = "Redmond43";
    ```

1. <span data-ttu-id="7381f-132">Update Hallo **belangrijkste** methode handtekening tooinclude Hallo volgende `throws` component:</span><span class="sxs-lookup"><span data-stu-id="7381f-132">Update hello **main** method signature tooinclude hello following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws IOException
    ```

1. <span data-ttu-id="7381f-133">Hallo na code toohello toevoegen **belangrijkste** methode toocreate hello **DeviceTwin** en **DeviceTwinDevice** objecten.</span><span class="sxs-lookup"><span data-stu-id="7381f-133">Add hello following code toohello **main** method toocreate hello **DeviceTwin** and **DeviceTwinDevice** objects.</span></span> <span data-ttu-id="7381f-134">Hallo **DeviceTwin** object verwerkt Hallo communicatie met uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="7381f-134">hello **DeviceTwin** object handles hello communication with your IoT hub.</span></span> <span data-ttu-id="7381f-135">Hallo **DeviceTwinDevice** object vertegenwoordigt Hallo apparaat twin met eigenschappen en tags:</span><span class="sxs-lookup"><span data-stu-id="7381f-135">hello **DeviceTwinDevice** object represents hello device twin with its properties and tags:</span></span>

    ```java
    // Get hello DeviceTwin and DeviceTwinDevice objects
    DeviceTwin twinClient = DeviceTwin.createFromConnectionString(iotHubConnectionString);
    DeviceTwinDevice device = new DeviceTwinDevice(deviceId);
    ```

1. <span data-ttu-id="7381f-136">Voeg de volgende Hallo `try/catch` blokkeren toohello **belangrijkste** methode:</span><span class="sxs-lookup"><span data-stu-id="7381f-136">Add hello following `try/catch` block toohello **main** method:</span></span>

    ```java
    try {
      // Code goes here
    } catch (IotHubException e) {
      System.out.println(e.getMessage());
    } catch (IOException e) {
      System.out.println(e.getMessage());
    }
    ```

1. <span data-ttu-id="7381f-137">Hallo tooupdate **regio** en **plant** apparaat twin labels in uw twin apparaat toevoegen na de code in Hallo Hallo `try` blokkeren:</span><span class="sxs-lookup"><span data-stu-id="7381f-137">tooupdate hello **region** and **plant** device twin tags in your device twin, add hello following code in hello `try` block:</span></span>

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

1. <span data-ttu-id="7381f-138">tooquery hello apparaat horende in IoT-hub toevoegen na de code toohello Hallo `try` blok na het Hallo-code die u in de vorige stap Hallo hebt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="7381f-138">tooquery hello device twins in IoT hub, add hello following code toohello `try` block after hello code you added in hello previous step.</span></span> <span data-ttu-id="7381f-139">Hallo-code wordt uitgevoerd twee query's.</span><span class="sxs-lookup"><span data-stu-id="7381f-139">hello code runs two queries.</span></span> <span data-ttu-id="7381f-140">Elke query retourneert maximaal 100 apparaten:</span><span class="sxs-lookup"><span data-stu-id="7381f-140">Each query returns a maximum of 100 devices:</span></span>

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

1. <span data-ttu-id="7381f-141">Opslaan en sluiten Hallo `add-tags-query\src\main\java\com\mycompany\app\App.java` bestand</span><span class="sxs-lookup"><span data-stu-id="7381f-141">Save and close hello `add-tags-query\src\main\java\com\mycompany\app\App.java` file</span></span>

1. <span data-ttu-id="7381f-142">Hallo bouwen **toevoegen-tags-query** app en eventuele fouten te corrigeren.</span><span class="sxs-lookup"><span data-stu-id="7381f-142">Build hello **add-tags-query** app and correct any errors.</span></span> <span data-ttu-id="7381f-143">Ga bij de opdrachtprompt toohello `add-tags-query` map en Voer Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="7381f-143">At your command prompt, navigate toohello `add-tags-query` folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a><span data-ttu-id="7381f-144">Een apparaat-app maken</span><span class="sxs-lookup"><span data-stu-id="7381f-144">Create a device app</span></span>

<span data-ttu-id="7381f-145">In deze sectie maakt u een Java-consoletoepassing die stelt u een eigenschapswaarde gemeld dat tooIoT Hub wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="7381f-145">In this section, you create a Java console app that sets a reported property value that is sent tooIoT Hub.</span></span>

1. <span data-ttu-id="7381f-146">In Hallo `iot-java-twin-getstarted` map, maak een Maven-project aangeroepen **simulated-device** met behulp van de volgende opdracht achter de opdrachtprompt Hallo.</span><span class="sxs-lookup"><span data-stu-id="7381f-146">In hello `iot-java-twin-getstarted` folder, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="7381f-147">Let op: dit is één enkele, lange opdracht:</span><span class="sxs-lookup"><span data-stu-id="7381f-147">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="7381f-148">Ga bij de opdrachtprompt toohello `simulated-device` map.</span><span class="sxs-lookup"><span data-stu-id="7381f-148">At your command prompt, navigate toohello `simulated-device` folder.</span></span>

1. <span data-ttu-id="7381f-149">Met een teksteditor openen Hallo `pom.xml` bestand in Hallo `simulated-device` map en Voeg na afhankelijkheden toohello hello **afhankelijkheden** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="7381f-149">Using a text editor, open hello `pom.xml` file in hello `simulated-device` folder and add hello following dependencies toohello **dependencies** node.</span></span> <span data-ttu-id="7381f-150">Deze afhankelijkheid kunt u toouse hello **iot-apparaat-client** pakket in uw app toocommunicate met uw IoT-hub:</span><span class="sxs-lookup"><span data-stu-id="7381f-150">This dependency enables you toouse hello **iot-device-client** package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="7381f-151">U kunt controleren op de meest recente versie van Hallo **iot-apparaat-client** met [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="7381f-151">You can check for hello latest version of **iot-device-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="7381f-152">Voeg de volgende Hallo **bouwen** knooppunt na Hallo **afhankelijkheden** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="7381f-152">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="7381f-153">Deze configuratie wordt Java-Maven toouse 1.8 toobuild Hallo app:</span><span class="sxs-lookup"><span data-stu-id="7381f-153">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="7381f-154">Opslaan en sluiten Hallo `pom.xml` bestand.</span><span class="sxs-lookup"><span data-stu-id="7381f-154">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="7381f-155">Met een teksteditor openen Hallo `simulated-device\src\main\java\com\mycompany\app\App.java` bestand.</span><span class="sxs-lookup"><span data-stu-id="7381f-155">Using a text editor, open hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="7381f-156">Voeg de volgende Hallo **importeren** instructies toohello bestand:</span><span class="sxs-lookup"><span data-stu-id="7381f-156">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="7381f-157">Hallo klasseniveau variabelen toohello na toevoegen **App** klasse.</span><span class="sxs-lookup"><span data-stu-id="7381f-157">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="7381f-158">Vervangen van `{youriothubname}` met de naam van uw IoT-hub en `{yourdevicekey}` met Hallo apparaat sleutelwaarde u hebt gegenereerd in Hallo *maken van een apparaat-id* sectie:</span><span class="sxs-lookup"><span data-stu-id="7381f-158">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with hello device key value you generated in hello *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myDeviceId";
    ```

    <span data-ttu-id="7381f-159">In dit voorbeeld-app gebruikt Hallo **protocol** variabele bij het instantiëren van een **DeviceClient** object.</span><span class="sxs-lookup"><span data-stu-id="7381f-159">This sample app uses hello **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="7381f-160">Op dit moment toouse twin apparaatfuncties u Hallo MQTT protocol moet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7381f-160">Currently, toouse device twin features you must use hello MQTT protocol.</span></span>

1. <span data-ttu-id="7381f-161">Hallo na code toohello toevoegen **belangrijkste** methode:</span><span class="sxs-lookup"><span data-stu-id="7381f-161">Add hello following code toohello **main** method to:</span></span>
    * <span data-ttu-id="7381f-162">Maak een client apparaat toocommunicate met IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="7381f-162">Create a device client toocommunicate with IoT Hub.</span></span>
    * <span data-ttu-id="7381f-163">Maak een **apparaat** toostore Hallo apparaateigenschappen twin object.</span><span class="sxs-lookup"><span data-stu-id="7381f-163">Create a **Device** object toostore hello device twin properties.</span></span>

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

1. <span data-ttu-id="7381f-164">Hallo na code toohello toevoegen **belangrijkste** methode toocreate een **connectivityType** eigenschap gerapporteerd en dit tooIoT Hub te verzenden:</span><span class="sxs-lookup"><span data-stu-id="7381f-164">Add hello following code toohello **main** method toocreate a **connectivityType** reported property and send it tooIoT Hub:</span></span>

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

1. <span data-ttu-id="7381f-165">Toevoegen van de volgende code toohello einde van Hallo Hallo **belangrijkste** methode.</span><span class="sxs-lookup"><span data-stu-id="7381f-165">Add hello following code toohello end of hello **main** method.</span></span> <span data-ttu-id="7381f-166">Wachten op Hallo **Enter** sleutel kan tijd voor IoT Hub tooreport Hallo status van Hallo apparaat twin bewerkingen:</span><span class="sxs-lookup"><span data-stu-id="7381f-166">Waiting for hello **Enter** key allows time for IoT Hub tooreport hello status of hello device twin operations:</span></span>

    ```java
    System.out.println("Press any key tooexit...");

    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();

    dataCollector.clean();
    client.close();
    ```

1. <span data-ttu-id="7381f-167">Opslaan en sluiten Hallo `simulated-device\src\main\java\com\mycompany\app\App.java` bestand.</span><span class="sxs-lookup"><span data-stu-id="7381f-167">Save and close hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="7381f-168">Hallo bouwen **simulated-device** app en eventuele fouten te corrigeren.</span><span class="sxs-lookup"><span data-stu-id="7381f-168">Build hello **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="7381f-169">Ga bij de opdrachtprompt toohello `simulated-device` map en Voer Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="7381f-169">At your command prompt, navigate toohello `simulated-device` folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a><span data-ttu-id="7381f-170">Hallo-apps uitvoeren</span><span class="sxs-lookup"><span data-stu-id="7381f-170">Run hello apps</span></span>

<span data-ttu-id="7381f-171">U bent nu klaar toorun Hallo console apps.</span><span class="sxs-lookup"><span data-stu-id="7381f-171">You are now ready toorun hello console apps.</span></span>

1. <span data-ttu-id="7381f-172">Bij een opdrachtprompt in Hallo `add-tags-query` map na de opdracht toorun Hallo Hallo **toevoegen-tags-query** service-app:</span><span class="sxs-lookup"><span data-stu-id="7381f-172">At a command prompt in hello `add-tags-query` folder, run hello following command toorun hello **add-tags-query** service app:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![IoT Hub voor Java service app tooupdate waarden code en elk apparaat query's uitvoeren](media/iot-hub-java-java-twin-getstarted/service-app-1.png)

    <span data-ttu-id="7381f-174">U kunt zien Hallo **plant** en **regio** labels toohello apparaat twin toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="7381f-174">You can see hello **plant** and **region** tags added toohello device twin.</span></span> <span data-ttu-id="7381f-175">Hallo eerste query retourneert het apparaat, maar Hallo tweede niet.</span><span class="sxs-lookup"><span data-stu-id="7381f-175">hello first query returns your device, but hello second does not.</span></span>

1. <span data-ttu-id="7381f-176">Bij een opdrachtprompt in Hallo `simulated-device` map na de opdracht tooadd Hallo Hallo **connectivityType** eigenschap toohello apparaat twin gerapporteerd:</span><span class="sxs-lookup"><span data-stu-id="7381f-176">At a command prompt in hello `simulated-device` folder, run hello following command tooadd hello **connectivityType** reported property toohello device twin:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Hallo-apparaatclient voegt Hallo ** connectivityType ** eigenschap gerapporteerd](media/iot-hub-java-java-twin-getstarted/device-app-1.png)

1. <span data-ttu-id="7381f-178">Bij een opdrachtprompt in Hallo `add-tags-query` map na de opdracht toorun Hallo Hallo **toevoegen-tags-query** service-app een tweede keer:</span><span class="sxs-lookup"><span data-stu-id="7381f-178">At a command prompt in hello `add-tags-query` folder, run hello following command toorun hello **add-tags-query** service app a second time:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![IoT Hub voor Java service app tooupdate waarden code en elk apparaat query's uitvoeren](media/iot-hub-java-java-twin-getstarted/service-app-2.png)

    <span data-ttu-id="7381f-180">Nu u uw apparaat heeft verzonden hello **connectivityType** eigenschap tooIoT Hub, Hallo tweede query retourneert het apparaat.</span><span class="sxs-lookup"><span data-stu-id="7381f-180">Now your device has sent hello **connectivityType** property tooIoT Hub, hello second query returns your device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7381f-181">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7381f-181">Next steps</span></span>

<span data-ttu-id="7381f-182">In deze zelfstudie maakt u een nieuwe iothub geconfigureerd in hello Azure-portal en vervolgens een apparaat-id in de id-register Hallo iothub hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7381f-182">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="7381f-183">U metagegevens van apparaten als labels toegevoegd vanuit een back-end-app en een app tooreport apparaat connectiviteit apparaatgegevens in Hallo apparaat twin geschreven.</span><span class="sxs-lookup"><span data-stu-id="7381f-183">You added device metadata as tags from a back-end app, and wrote a device app tooreport device connectivity information in hello device twin.</span></span> <span data-ttu-id="7381f-184">U hebt ook geleerd hoe tooquery Hallo twin apparaatgegevens Hallo IoT-Hub SQL-achtige query language gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7381f-184">You also learned how tooquery hello device twin information using hello SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="7381f-185">Gebruik Hallo resources toolearn hoe volgende aan:</span><span class="sxs-lookup"><span data-stu-id="7381f-185">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="7381f-186">Verzenden van telemetrie vanaf apparaten Hello [aan de slag met IoT Hub](iot-hub-java-java-getstarted.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="7381f-186">Send telemetry from devices with hello [Get started with IoT Hub](iot-hub-java-java-getstarted.md) tutorial.</span></span>
* <span data-ttu-id="7381f-187">Beheren van apparaten interactief (zoals het inschakelen van een ventilator van een gebruiker beheerde app) met Hallo [direct methoden gebruiken](iot-hub-java-java-direct-methods.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="7381f-187">Control devices interactively (such as turning on a fan from a user-controlled app) with hello [Use direct methods](iot-hub-java-java-direct-methods.md) tutorial.</span></span>

<!-- Images. -->
[7]: ./media/iot-hub-java-java-twin-getstarted/invoke-method.png
[8]: ./media/iot-hub-java-java-twin-getstarted/device-listen.png
[9]: ./media/iot-hub-java-java-twin-getstarted/device-respond.png

<!-- Links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
