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
# <a name="connect-your-device-tooyour-iot-hub-using-java"></a><span data-ttu-id="92cd5-104">Verbinding maken met uw apparaat tooyour iothub met Java</span><span class="sxs-lookup"><span data-stu-id="92cd5-104">Connect your device tooyour IoT hub using Java</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="92cd5-105">Aan het einde van de Hallo van deze zelfstudie hebt u drie Java-apps die console:</span><span class="sxs-lookup"><span data-stu-id="92cd5-105">At hello end of this tutorial, you have three Java console apps:</span></span>

* <span data-ttu-id="92cd5-106">**Create-device-identity**, die een apparaat-id maakt en gekoppelde beveiliging sleutel tooconnect app op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="92cd5-106">**create-device-identity**, which creates a device identity and associated security key tooconnect your device app.</span></span>
* <span data-ttu-id="92cd5-107">**Read-d2c-messages**, weergeven met Hallo telemetrie verzonden door de app op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="92cd5-107">**read-d2c-messages**, which displays hello telemetry sent by your device app.</span></span>
* <span data-ttu-id="92cd5-108">**simulated-device**, die tooyour IoT-hub aan Hallo apparaat-id eerder hebt gemaakt, en verzendt een elke tweede met behulp van protocollen MQTT protocol Hallo telemetrie-bericht.</span><span class="sxs-lookup"><span data-stu-id="92cd5-108">**simulated-device**, which connects tooyour IoT hub with hello device identity created earlier, and sends a telemetry message every second using hello MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="92cd5-109">Hallo artikel [Azure IoT SDK's] [ lnk-hub-sdks] bevat informatie over hello Azure IoT SDK's waarmee u toobuild beide toorun apps op apparaten en de back-end van uw oplossing kunt.</span><span class="sxs-lookup"><span data-stu-id="92cd5-109">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both apps toorun on devices and your solution back end.</span></span>

<span data-ttu-id="92cd5-110">toocomplete in deze zelfstudie, moet u hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="92cd5-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="92cd5-111">meest recente Hallo [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="92cd5-111">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span> 
* [<span data-ttu-id="92cd5-112">Maven 3</span><span class="sxs-lookup"><span data-stu-id="92cd5-112">Maven 3</span></span>](https://maven.apache.org/install.html) 
* <span data-ttu-id="92cd5-113">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="92cd5-113">An active Azure account.</span></span> <span data-ttu-id="92cd5-114">(Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)</span><span class="sxs-lookup"><span data-stu-id="92cd5-114">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="92cd5-115">Als een laatste stap Noteer Hallo **primaire sleutel** waarde.</span><span class="sxs-lookup"><span data-stu-id="92cd5-115">As a final step, make a note of hello **Primary key** value.</span></span> <span data-ttu-id="92cd5-116">Klik vervolgens op **eindpunten** en Hallo **gebeurtenissen** ingebouwd eindpunt.</span><span class="sxs-lookup"><span data-stu-id="92cd5-116">Then click **Endpoints** and hello **Events** built-in endpoint.</span></span> <span data-ttu-id="92cd5-117">Op Hallo **eigenschappen** blade, maakt u een notitie van Hallo **Event Hub-compatibele naam** en Hallo **Event Hub-compatibele eindpunt** adres.</span><span class="sxs-lookup"><span data-stu-id="92cd5-117">On hello **Properties** blade, make a note of hello **Event Hub-compatible name** and hello **Event Hub-compatible endpoint** address.</span></span> <span data-ttu-id="92cd5-118">U hebt deze drie waarden nodig wanneer u uw **read-d2c-messages**-app maakt.</span><span class="sxs-lookup"><span data-stu-id="92cd5-118">You need these three values when you create your **read-d2c-messages** app.</span></span>

![Blade IoT Hub-berichten in Azure Portal][6]

<span data-ttu-id="92cd5-120">U hebt nu uw IoT-hub gemaakt.</span><span class="sxs-lookup"><span data-stu-id="92cd5-120">You have now created your IoT hub.</span></span> <span data-ttu-id="92cd5-121">U hebt Hallo IoT Hub-hostnaam, verbindingsreeks IoT Hub, primaire sleutel van IoT Hub, Event Hub-compatibele naam en Event Hub-compatibele eindpunt u toocomplete in deze zelfstudie nodig.</span><span class="sxs-lookup"><span data-stu-id="92cd5-121">You have hello IoT Hub host name, IoT Hub connection string, IoT Hub Primary Key, Event Hub-compatible name, and Event Hub-compatible endpoint you need toocomplete this tutorial.</span></span>

## <a name="create-a-device-identity"></a><span data-ttu-id="92cd5-122">Een apparaat-id maken</span><span class="sxs-lookup"><span data-stu-id="92cd5-122">Create a device identity</span></span>
<span data-ttu-id="92cd5-123">In deze sectie maakt maken u een Java-consoletoepassing die een apparaat-id in Hallo identiteitenregister van uw IoT-hub maakt.</span><span class="sxs-lookup"><span data-stu-id="92cd5-123">In this section, you create a Java console app that creates a device identity in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="92cd5-124">Een apparaat kan geen verbinding tooIoT hub maken, tenzij er een vermelding in het identiteitenregister Hallo.</span><span class="sxs-lookup"><span data-stu-id="92cd5-124">A device cannot connect tooIoT hub unless it has an entry in hello identity registry.</span></span> <span data-ttu-id="92cd5-125">Zie voor meer informatie, Hallo **Identiteitsregister** sectie Hallo [Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="92cd5-125">For more information, see hello **Identity Registry** section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="92cd5-126">Wanneer u deze consoletoepassing uitvoert, wordt een unieke apparaat-ID gegenereerd en sleutel waarmee het apparaat tooidentify zelf kunt wanneer het apparaat-naar-cloud verzendt berichten tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="92cd5-126">When you run this console app, it generates a unique device ID and key that your device can use tooidentify itself when it sends device-to-cloud messages tooIoT Hub.</span></span>

1. <span data-ttu-id="92cd5-127">Maak een lege map genaamd iot-java-get-started.</span><span class="sxs-lookup"><span data-stu-id="92cd5-127">Create an empty folder called iot-java-get-started.</span></span> <span data-ttu-id="92cd5-128">Maak een Maven-project aangeroepen in Hallo iot-java-get-started map **create-device-identity** met behulp van de volgende opdracht achter de opdrachtprompt Hallo.</span><span class="sxs-lookup"><span data-stu-id="92cd5-128">In hello iot-java-get-started folder, create a Maven project called **create-device-identity** using hello following command at your command prompt.</span></span> <span data-ttu-id="92cd5-129">Let op: dit is één enkele, lange opdracht:</span><span class="sxs-lookup"><span data-stu-id="92cd5-129">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=create-device-identity -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="92cd5-130">Navigeer toohello create-device-identity-map bij de opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="92cd5-130">At your command prompt, navigate toohello create-device-identity folder.</span></span>

3. <span data-ttu-id="92cd5-131">Met een teksteditor, open Hallo pom.xml-bestand in Hallo create-device-identity-map en Hallo afhankelijkheid toohello na toevoegen **afhankelijkheden** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="92cd5-131">Using a text editor, open hello pom.xml file in hello create-device-identity folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="92cd5-132">Deze afhankelijkheid kunt u toouse Hallo iot-service-client-pakket in uw app:</span><span class="sxs-lookup"><span data-stu-id="92cd5-132">This dependency enables you toouse hello iot-service-client package in your app:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="92cd5-133">U kunt controleren op de meest recente versie van Hallo **iot-service-client** met [Maven search][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="92cd5-133">You can check for hello latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

4. <span data-ttu-id="92cd5-134">Opslaan en sluiten Hallo pom.xml-bestand.</span><span class="sxs-lookup"><span data-stu-id="92cd5-134">Save and close hello pom.xml file.</span></span>

5. <span data-ttu-id="92cd5-135">Met een teksteditor Hallo create-device-identity\src\main\java\com\mycompany\app\App.java bestand openen.</span><span class="sxs-lookup"><span data-stu-id="92cd5-135">Using a text editor, open hello create-device-identity\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="92cd5-136">Voeg de volgende Hallo **importeren** instructies toohello bestand:</span><span class="sxs-lookup"><span data-stu-id="92cd5-136">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;
    import com.microsoft.azure.sdk.iot.service.Device;
    import com.microsoft.azure.sdk.iot.service.RegistryManager;
   
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. <span data-ttu-id="92cd5-137">Hallo klasseniveau variabelen toohello na toevoegen **App** klasse, Vervang **{yourhubconnectionstring}** Hello waarde uw aangegeven eerder:</span><span class="sxs-lookup"><span data-stu-id="92cd5-137">Add hello following class-level variables toohello **App** class, replacing **{yourhubconnectionstring}** with hello value your noted earlier:</span></span>

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "myFirstJavaDevice";
    ```
[!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

8. <span data-ttu-id="92cd5-138">Wijzig de handtekening Hallo Hallo **belangrijkste** methode tooinclude Hallo uitzonderingen als volgt:</span><span class="sxs-lookup"><span data-stu-id="92cd5-138">Modify hello signature of hello **main** method tooinclude hello exceptions as follows:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException, Exception
    ```

9. <span data-ttu-id="92cd5-139">Toevoegen na de code als de berichttekst Hallo HALLO hallo **belangrijkste** methode.</span><span class="sxs-lookup"><span data-stu-id="92cd5-139">Add hello following code as hello body of hello **main** method.</span></span> <span data-ttu-id="92cd5-140">Deze code maakt een apparaat in het identiteitsregister van de IoT Hub dat *javadevice* heet als dit nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="92cd5-140">This code creates a device called *javadevice* in your IoT Hub identity registry if doesn't already exist.</span></span> <span data-ttu-id="92cd5-141">Vervolgens wordt weergegeven Hallo apparaat-ID en sleutel die u later nodig:</span><span class="sxs-lookup"><span data-stu-id="92cd5-141">It then displays hello device ID and key that you need later:</span></span>

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

10. <span data-ttu-id="92cd5-142">Opslaan en sluiten Hallo App.java bestand.</span><span class="sxs-lookup"><span data-stu-id="92cd5-142">Save and close hello App.java file.</span></span>

11. <span data-ttu-id="92cd5-143">Hallo toobuild **create-device-identity** app met behulp van Maven, uitvoeren van de volgende opdracht achter de opdrachtprompt Hallo in Hallo create-device-identity map Hallo:</span><span class="sxs-lookup"><span data-stu-id="92cd5-143">toobuild hello **create-device-identity** app using Maven, execute hello following command at hello command prompt in hello create-device-identity folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

12. <span data-ttu-id="92cd5-144">Hallo toorun **create-device-identity** app met behulp van Maven, uitvoeren van de volgende opdracht achter de opdrachtprompt Hallo in Hallo create-device-identity map Hallo:</span><span class="sxs-lookup"><span data-stu-id="92cd5-144">toorun hello **create-device-identity** app using Maven, execute hello following command at hello command prompt in hello create-device-identity folder:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

13. <span data-ttu-id="92cd5-145">Maak een notitie van Hallo **apparaat-ID** en **apparaatsleutel**.</span><span class="sxs-lookup"><span data-stu-id="92cd5-145">Make a note of hello **Device ID** and **Device key**.</span></span> <span data-ttu-id="92cd5-146">U moet deze waarden later bij het maken van een app die tooIoT Hub als apparaat verbinding maakt.</span><span class="sxs-lookup"><span data-stu-id="92cd5-146">You need these values later when you create an app that connects tooIoT Hub as a device.</span></span>

> [!NOTE]
> <span data-ttu-id="92cd5-147">Hallo id-register IoT Hub bewaart alleen apparaat-id's tooenable veilige toegang toohello IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="92cd5-147">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="92cd5-148">Apparaat-id's en sleutels toouse worden opgeslagen als beveiligingsreferenties en waarmee u toodisable toegang tot een afzonderlijk apparaat kunt vlag voor ingeschakeld/uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="92cd5-148">It stores device IDs and keys toouse as security credentials and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="92cd5-149">Als uw app toostore andere apparaatspecifieke metagegevens moet, moet deze een app-specifiek store gebruiken.</span><span class="sxs-lookup"><span data-stu-id="92cd5-149">If your app needs toostore other device-specific metadata, it should use an app-specific store.</span></span> <span data-ttu-id="92cd5-150">Zie voor meer informatie, Hallo [Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="92cd5-150">For more information, see hello [IoT Hub developer guide][lnk-devguide-identity].</span></span>

## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="92cd5-151">Apparaat-naar-cloud-berichten ontvangen</span><span class="sxs-lookup"><span data-stu-id="92cd5-151">Receive device-to-cloud messages</span></span>

<span data-ttu-id="92cd5-152">In dit gedeelte maakt u een Java-consoletoepassing die apparaat-naar-cloud-berichten uit IoT Hub kan lezen.</span><span class="sxs-lookup"><span data-stu-id="92cd5-152">In this section, you create a Java console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="92cd5-153">Een iothub toont een [Event Hub][lnk-event-hubs-overview]-compatibel eindpunt tooenable u tooread apparaat-naar-cloud-berichten.</span><span class="sxs-lookup"><span data-stu-id="92cd5-153">An IoT hub exposes an [Event Hub][lnk-event-hubs-overview]-compatible endpoint tooenable you tooread device-to-cloud messages.</span></span> <span data-ttu-id="92cd5-154">tookeep dingen eenvoudige, deze zelfstudie maakt u een basislezer die niet geschikt voor een implementatie met hoge doorvoer.</span><span class="sxs-lookup"><span data-stu-id="92cd5-154">tookeep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="92cd5-155">Hallo [apparaat-naar-cloud-berichten verwerken] [ lnk-process-d2c-tutorial] zelfstudie laat zien hoe tooprocess apparaat-naar-cloud-berichten op grote schaal.</span><span class="sxs-lookup"><span data-stu-id="92cd5-155">hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial shows you how tooprocess device-to-cloud messages at scale.</span></span> <span data-ttu-id="92cd5-156">Hallo [aan de slag met Event Hubs] [ lnk-eventhubs-tutorial] zelfstudie bevat meer informatie over hoe tooprocess van berichten van Event Hubs en toepasselijke toohello IoT Hub Event Hub-compatibele eindpunten is.</span><span class="sxs-lookup"><span data-stu-id="92cd5-156">hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial provides further information on how tooprocess messages from Event Hubs and is applicable toohello IoT Hub Event Hub-compatible endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="92cd5-157">Hallo Event Hub-compatibele eindpunt voor het lezen van apparaat-naar-cloudberichten altijd gebruikt Hallo AMQP-protocol.</span><span class="sxs-lookup"><span data-stu-id="92cd5-157">hello Event Hub-compatible endpoint for reading device-to-cloud messages always uses hello AMQP protocol.</span></span>

1. <span data-ttu-id="92cd5-158">In Hallo map iot-java-get-started die u hebt gemaakt in Hallo *maken van een apparaat-id* sectie, maakt u een Maven-project aangeroepen **read-d2c-messages** met behulp van de volgende opdracht achter de opdrachtprompt Hallo.</span><span class="sxs-lookup"><span data-stu-id="92cd5-158">In hello iot-java-get-started folder you created in hello *Create a device identity* section, create a Maven project called **read-d2c-messages** using hello following command at your command prompt.</span></span> <span data-ttu-id="92cd5-159">Let op: dit is één enkele, lange opdracht:</span><span class="sxs-lookup"><span data-stu-id="92cd5-159">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-d2c-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="92cd5-160">Navigeer toohello read-d2c-messages map bij de opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="92cd5-160">At your command prompt, navigate toohello read-d2c-messages folder.</span></span>

3. <span data-ttu-id="92cd5-161">Met een teksteditor, open Hallo pom.xml-bestand in Hallo read-d2c-messages map en Hallo afhankelijkheid toohello na toevoegen **afhankelijkheden** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="92cd5-161">Using a text editor, open hello pom.xml file in hello read-d2c-messages folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="92cd5-162">Deze afhankelijkheid kunt u toouse hello eventhubs-client-pakket in uw app tooread van Hallo Event Hub-compatibele eindpunt:</span><span class="sxs-lookup"><span data-stu-id="92cd5-162">This dependency enables you toouse hello eventhubs-client package in your app tooread from hello Event Hub-compatible endpoint:</span></span>

    ```xml
    <dependency> 
        <groupId>com.microsoft.azure</groupId> 
        <artifactId>azure-eventhubs</artifactId> 
        <version>0.13.0</version> 
    </dependency>
    ```

4. <span data-ttu-id="92cd5-163">Opslaan en sluiten Hallo pom.xml-bestand.</span><span class="sxs-lookup"><span data-stu-id="92cd5-163">Save and close hello pom.xml file.</span></span>

5. <span data-ttu-id="92cd5-164">Met een teksteditor Hallo read-d2c-messages\src\main\java\com\mycompany\app\App.java bestand openen.</span><span class="sxs-lookup"><span data-stu-id="92cd5-164">Using a text editor, open hello read-d2c-messages\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="92cd5-165">Voeg de volgende Hallo **importeren** instructies toohello bestand:</span><span class="sxs-lookup"><span data-stu-id="92cd5-165">Add hello following **import** statements toohello file:</span></span>

    ```java
    import java.io.IOException;
    import com.microsoft.azure.eventhubs.*;
    import com.microsoft.azure.servicebus.*;

    import java.nio.charset.Charset;
    import java.time.*;
    import java.util.function.*;
    ```

7. <span data-ttu-id="92cd5-166">Hallo klasseniveau variabele toohello na toevoegen **App** klasse.</span><span class="sxs-lookup"><span data-stu-id="92cd5-166">Add hello following class-level variable toohello **App** class.</span></span> <span data-ttu-id="92cd5-167">Vervang **{youriothubkey}**, **{youreventhubcompatibleendpoint}**, en **{youreventhubcompatiblename}** met Hallo-waarden die u eerder hebt genoteerd:</span><span class="sxs-lookup"><span data-stu-id="92cd5-167">Replace **{youriothubkey}**, **{youreventhubcompatibleendpoint}**, and **{youreventhubcompatiblename}** with hello values you noted previously:</span></span>

    ```java
    private static String connStr = "Endpoint={youreventhubcompatibleendpoint};EntityPath={youreventhubcompatiblename};SharedAccessKeyName=iothubowner;SharedAccessKey={youriothubkey}";
    ```

8. <span data-ttu-id="92cd5-168">Voeg de volgende Hallo **receiveMessages** methode toohello **App** klasse.</span><span class="sxs-lookup"><span data-stu-id="92cd5-168">Add hello following **receiveMessages** method toohello **App** class.</span></span> <span data-ttu-id="92cd5-169">Deze methode maakt u een **EventHubClient** tooconnect toohello Event Hub-compatibele eindpunt-instantie en vervolgens maakt u asynchroon een **PartitionReceiver** tooread exemplaar van een Event Hub partitie.</span><span class="sxs-lookup"><span data-stu-id="92cd5-169">This method creates an **EventHubClient** instance tooconnect toohello Event Hub-compatible endpoint and then asynchronously creates a **PartitionReceiver** instance tooread from an Event Hub partition.</span></span> <span data-ttu-id="92cd5-170">Dit wordt continu uitgevoerd en Hallo berichtgegevens worden afgedrukt totdat het Hallo-app wordt beëindigd.</span><span class="sxs-lookup"><span data-stu-id="92cd5-170">It loops continuously and prints hello message details until hello app terminates.</span></span>

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
   > <span data-ttu-id="92cd5-171">Deze methode gebruikt een filter bij het maken van Hallo ontvanger zodat hello ontvanger alleen berichten tooIoT Hub leest nadat Hallo ontvanger is geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="92cd5-171">This method uses a filter when it creates hello receiver so that hello receiver only reads messages sent tooIoT Hub after hello receiver starts running.</span></span> <span data-ttu-id="92cd5-172">Dit is handig in een testomgeving zodat u Hallo huidige reeks berichten kunt zien.</span><span class="sxs-lookup"><span data-stu-id="92cd5-172">This technique is useful in a test environment so you can see hello current set of messages.</span></span> <span data-ttu-id="92cd5-173">In een productieomgeving moet uw code Zorg ervoor dat alle berichten Hallo - voor meer informatie worden verwerkt, Zie Hallo [hoe tooprocess IoT Hub apparaat-naar-cloud-berichten] [ lnk-process-d2c-tutorial] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="92cd5-173">In a production environment, your code should make sure that it processes all hello messages - for more information, see hello [How tooprocess IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>

9. <span data-ttu-id="92cd5-174">Wijzig de handtekening Hallo Hallo **belangrijkste** methode tooinclude Hallo uitzondering als volgt:</span><span class="sxs-lookup"><span data-stu-id="92cd5-174">Modify hello signature of hello **main** method tooinclude hello exception as follows:</span></span>

    ```java
    public static void main( String[] args ) throws IOException
    ```

10. <span data-ttu-id="92cd5-175">Hallo na code toohello toevoegen **belangrijkste** methode in Hallo **App** klasse.</span><span class="sxs-lookup"><span data-stu-id="92cd5-175">Add hello following code toohello **main** method in hello **App** class.</span></span> <span data-ttu-id="92cd5-176">Deze code maakt twee Hallo **EventHubClient** en **PartitionReceiver** exemplaren en kunt u tooclose Hallo app wanneer u klaar bent met het verwerken van berichten:</span><span class="sxs-lookup"><span data-stu-id="92cd5-176">This code creates hello two **EventHubClient** and **PartitionReceiver** instances and enables you tooclose hello app when you have finished processing messages:</span></span>

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
    > <span data-ttu-id="92cd5-177">Deze code wordt ervan uitgegaan dat u uw IoT-hub in (gratis) F1-laag Hallo gemaakt.</span><span class="sxs-lookup"><span data-stu-id="92cd5-177">This code assumes you created your IoT hub in hello F1 (free) tier.</span></span> <span data-ttu-id="92cd5-178">Een gratis IoT-hub heeft twee partities, genaamd "0" en "1".</span><span class="sxs-lookup"><span data-stu-id="92cd5-178">A free IoT hub has two partitions named "0" and "1".</span></span>

11. <span data-ttu-id="92cd5-179">Opslaan en sluiten Hallo App.java bestand.</span><span class="sxs-lookup"><span data-stu-id="92cd5-179">Save and close hello App.java file.</span></span>

12. <span data-ttu-id="92cd5-180">Hallo toobuild **read-d2c-messages** app met behulp van Maven, uitvoeren van de volgende opdracht achter de opdrachtprompt Hallo in Hallo read-d2c-messages map Hallo:</span><span class="sxs-lookup"><span data-stu-id="92cd5-180">toobuild hello **read-d2c-messages** app using Maven, execute hello following command at hello command prompt in hello read-d2c-messages folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="create-a-device-app"></a><span data-ttu-id="92cd5-181">Een apparaat-app maken</span><span class="sxs-lookup"><span data-stu-id="92cd5-181">Create a device app</span></span>
<span data-ttu-id="92cd5-182">In deze sectie maakt u een Java-consoletoepassing die een apparaat simuleert dat apparaat-naar-cloudberichten tooan iothub verzendt.</span><span class="sxs-lookup"><span data-stu-id="92cd5-182">In this section, you create a Java console app that simulates a device that sends device-to-cloud messages tooan IoT hub.</span></span>

1. <span data-ttu-id="92cd5-183">In Hallo map iot-java-get-started die u hebt gemaakt in Hallo *maken van een apparaat-id* sectie, maakt u een Maven-project aangeroepen **simulated-device** met behulp van de volgende opdracht achter de opdrachtprompt Hallo.</span><span class="sxs-lookup"><span data-stu-id="92cd5-183">In hello iot-java-get-started folder you created in hello *Create a device identity* section, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="92cd5-184">Let op: dit is één enkele, lange opdracht:</span><span class="sxs-lookup"><span data-stu-id="92cd5-184">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="92cd5-185">Ga bij de opdrachtprompt de map simulated-device toohello.</span><span class="sxs-lookup"><span data-stu-id="92cd5-185">At your command prompt, navigate toohello simulated-device folder.</span></span>

3. <span data-ttu-id="92cd5-186">Met een teksteditor Hallo pom.xml-bestand openen in de map simulated-device Hallo en toevoegen van Hallo afhankelijkheden toohello na **afhankelijkheden** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="92cd5-186">Using a text editor, open hello pom.xml file in hello simulated-device folder and add hello following dependencies toohello **dependencies** node.</span></span> <span data-ttu-id="92cd5-187">Deze afhankelijkheid kunt u toouse hello iothub-java-client-pakket in uw app toocommunicate met uw IoT-hub en Java-objecten tooJSON tooserialize:</span><span class="sxs-lookup"><span data-stu-id="92cd5-187">This dependency enables you toouse hello iothub-java-client package in your app toocommunicate with your IoT hub and tooserialize Java objects tooJSON:</span></span>

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
    > <span data-ttu-id="92cd5-188">U kunt controleren op de meest recente versie van Hallo **iot-apparaat-client** met [Maven search][lnk-maven-device-search].</span><span class="sxs-lookup"><span data-stu-id="92cd5-188">You can check for hello latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

4. <span data-ttu-id="92cd5-189">Opslaan en sluiten Hallo pom.xml-bestand.</span><span class="sxs-lookup"><span data-stu-id="92cd5-189">Save and close hello pom.xml file.</span></span>

5. <span data-ttu-id="92cd5-190">Met een teksteditor Hallo simulated-device\src\main\java\com\mycompany\app\App.java bestand openen.</span><span class="sxs-lookup"><span data-stu-id="92cd5-190">Using a text editor, open hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="92cd5-191">Voeg de volgende Hallo **importeren** instructies toohello bestand:</span><span class="sxs-lookup"><span data-stu-id="92cd5-191">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.google.gson.Gson;

    import java.io.*;
    import java.net.URISyntaxException;
    import java.util.Random;
    import java.util.concurrent.Executors;
    import java.util.concurrent.ExecutorService;
    ```

7. <span data-ttu-id="92cd5-192">Hallo klasseniveau variabelen toohello na toevoegen **App** klasse.</span><span class="sxs-lookup"><span data-stu-id="92cd5-192">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="92cd5-193">Vervangen van **{youriothubname}** met de naam van uw IoT-hub en **{yourdevicekey}** met Hallo apparaat sleutelwaarde u hebt gegenereerd in Hallo *maken van een apparaat-id* sectie:</span><span class="sxs-lookup"><span data-stu-id="92cd5-193">Replacing **{youriothubname}** with your IoT hub name, and **{yourdevicekey}** with hello device key value you generated in hello *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myFirstJavaDevice;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myFirstJavaDevice";
    private static DeviceClient client;
    ```
   
    <span data-ttu-id="92cd5-194">In dit voorbeeld-app gebruikt Hallo **protocol** variabele bij het instantiëren van een **DeviceClient** object.</span><span class="sxs-lookup"><span data-stu-id="92cd5-194">This sample app uses hello **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="92cd5-195">U kunt beide toocommunicate hello MQTT, AMQP of HTTP-protocol gebruiken met IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="92cd5-195">You can use either hello MQTT, AMQP, or HTTP protocol toocommunicate with IoT Hub.</span></span>

8. <span data-ttu-id="92cd5-196">Voeg Hallo volgende geneste **TelemetryDataPoint** klasse binnen Hallo **App** klasse toospecify Hallo telemetrische gegevens uw apparaat verzendt tooyour IoT-hub:</span><span class="sxs-lookup"><span data-stu-id="92cd5-196">Add hello following nested **TelemetryDataPoint** class inside hello **App** class toospecify hello telemetry data your device sends tooyour IoT hub:</span></span>

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
9. <span data-ttu-id="92cd5-197">Voeg Hallo volgende geneste **EventCallback** klasse binnen Hallo **App** klasse toodisplay Hallo bevestiging status of IoT-hub Hallo bij de verwerking van een bericht van Hallo apparaattoepassing retourneert.</span><span class="sxs-lookup"><span data-stu-id="92cd5-197">Add hello following nested **EventCallback** class inside hello **App** class toodisplay hello acknowledgement status that hello IoT hub returns when it processes a message from hello device app.</span></span> <span data-ttu-id="92cd5-198">Deze methode ook Hallo hoofdthread in Hallo-app een melding wanneer het Hallo-bericht is verwerkt:</span><span class="sxs-lookup"><span data-stu-id="92cd5-198">This method also notifies hello main thread in hello app when hello message has been processed:</span></span>
   
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

10. <span data-ttu-id="92cd5-199">Voeg Hallo volgende geneste **MessageSender** klasse binnen Hallo **App** klasse.</span><span class="sxs-lookup"><span data-stu-id="92cd5-199">Add hello following nested **MessageSender** class inside hello **App** class.</span></span> <span data-ttu-id="92cd5-200">Hallo **uitvoeren** methode in deze klasse genereert voorbeeld telemetrie gegevens toosend tooyour IoT-hub en wordt gewacht op een bevestiging voordat het volgende Hallo-bericht verzonden:</span><span class="sxs-lookup"><span data-stu-id="92cd5-200">hello **run** method in this class generates sample telemetry data toosend tooyour IoT hub and waits for an acknowledgement before sending hello next message:</span></span>

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

    <span data-ttu-id="92cd5-201">Deze methode verzendt één seconde nadat Hallo IoT-hub Hallo vorige bericht erkent een nieuw apparaat-naar-cloud bericht uit.</span><span class="sxs-lookup"><span data-stu-id="92cd5-201">This method sends a new device-to-cloud message one second after hello IoT hub acknowledges hello previous message.</span></span> <span data-ttu-id="92cd5-202">Hallo-bericht bevat een JSON-geserialiseerd object met Hallo deviceId en willekeurige cijfers toosimulate een temperatuursensor en een sensor vochtigheid.</span><span class="sxs-lookup"><span data-stu-id="92cd5-202">hello message contains a JSON-serialized object with hello deviceId and randomly generated numbers toosimulate a temperature sensor, and a humidity sensor.</span></span>

11. <span data-ttu-id="92cd5-203">Vervang Hallo **belangrijkste** methode Hello code die wordt gemaakt van een thread toosend apparaat-naar-cloudberichten tooyour IoT-hub te volgen:</span><span class="sxs-lookup"><span data-stu-id="92cd5-203">Replace hello **main** method with hello following code that creates a thread toosend device-to-cloud messages tooyour IoT hub:</span></span>

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

12. <span data-ttu-id="92cd5-204">Opslaan en sluiten Hallo App.java bestand.</span><span class="sxs-lookup"><span data-stu-id="92cd5-204">Save and close hello App.java file.</span></span>

13. <span data-ttu-id="92cd5-205">Hallo toobuild **simulated-device** app met behulp van Maven, uitvoeren van de volgende opdracht achter de opdrachtprompt Hallo in de map simulated-device Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="92cd5-205">toobuild hello **simulated-device** app using Maven, execute hello following command at hello command prompt in hello simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

> [!NOTE]
> <span data-ttu-id="92cd5-206">tookeep dingen eenvoudige, deze zelfstudie wordt niet geïmplementeerd voor een beleid voor opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="92cd5-206">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="92cd5-207">In productiecode moet u beleid voor opnieuw proberen (zoals exponentieel uitstel), zoals voorgesteld in de MSDN-artikel Hallo implementeren [afhandeling van tijdelijke fout][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="92cd5-207">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="92cd5-208">Hallo-apps uitvoeren</span><span class="sxs-lookup"><span data-stu-id="92cd5-208">Run hello apps</span></span>

<span data-ttu-id="92cd5-209">U bent nu klaar toorun Hallo apps.</span><span class="sxs-lookup"><span data-stu-id="92cd5-209">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="92cd5-210">Voer bij een opdrachtprompt in Hallo read-d2c-map Hallo opdracht toobegin bewaking van de eerste partitie Hallo in uw IoT-hub te volgen:</span><span class="sxs-lookup"><span data-stu-id="92cd5-210">At a command prompt in hello read-d2c folder, run hello following command toobegin monitoring hello first partition in your IoT hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![Java IoT Hub service app toomonitor apparaat-naar-cloud-berichten][7]

2. <span data-ttu-id="92cd5-212">Voer bij een opdrachtprompt in de map simulated-device Hallo Hallo opdracht toobegin verzenden van telemetrie gegevens tooyour IoT-hub te volgen:</span><span class="sxs-lookup"><span data-stu-id="92cd5-212">At a command prompt in hello simulated-device folder, run hello following command toobegin sending telemetry data tooyour IoT hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![Java IoT Hub apparaat-app toosend apparaat-naar-cloud-berichten][8]

3. <span data-ttu-id="92cd5-214">Hallo **gebruik** -tegel in Hallo [Azure-portal] [ lnk-portal] toont Hallo aantal verzonden berichten toohello IoT-hub:</span><span class="sxs-lookup"><span data-stu-id="92cd5-214">hello **Usage** tile in hello [Azure portal][lnk-portal] shows hello number of messages sent toohello IoT hub:</span></span>

    ![Azure portal gebruik tegel met aantal verzonden berichten tooIoT Hub][43]

## <a name="next-steps"></a><span data-ttu-id="92cd5-216">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="92cd5-216">Next steps</span></span>
<span data-ttu-id="92cd5-217">In deze zelfstudie maakt u een nieuwe iothub geconfigureerd in hello Azure-portal en vervolgens een apparaat-id in de id-register Hallo iothub hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="92cd5-217">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="92cd5-218">U hebt deze apparaat-id tooenable Hallo apparaat app toosend apparaat-naar-cloudberichten toohello iothub gebruikt.</span><span class="sxs-lookup"><span data-stu-id="92cd5-218">You used this device identity tooenable hello device app toosend device-to-cloud messages toohello IoT hub.</span></span> <span data-ttu-id="92cd5-219">Hebt u ook een app die wordt weergegeven Hallo-berichten dat is ontvangen door de Hallo iothub hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="92cd5-219">You also created an app that displays hello messages received by hello IoT hub.</span></span>

<span data-ttu-id="92cd5-220">toocontinue aan de slag met IoT Hub en tooexplore raadpleegt u andere IoT-scenario's:</span><span class="sxs-lookup"><span data-stu-id="92cd5-220">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="92cd5-221">[Verbinding maken met uw apparaat][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="92cd5-221">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="92cd5-222">[Aan de slag met apparaatbeheer][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="92cd5-222">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="92cd5-223">[Aan de slag met Azure IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="92cd5-223">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="92cd5-224">toolearn hoe tooextend uw IoT-oplossing en proces apparaat-naar-cloud-berichten op grote schaal, zien Hallo [apparaat-naar-cloud-berichten verwerken] [ lnk-process-d2c-tutorial] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="92cd5-224">toolearn how tooextend your IoT solution and process device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
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
