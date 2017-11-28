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
# <a name="send-cloud-to-device-messages-with-iot-hub-java"></a><span data-ttu-id="257bb-104">Cloud-naar-apparaat-berichten verzenden met IoT Hub (Java)</span><span class="sxs-lookup"><span data-stu-id="257bb-104">Send cloud-to-device messages with IoT Hub (Java)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

<span data-ttu-id="257bb-105">Azure IoT Hub is een volledig beheerde service waarmee stabiele en veilige tweerichtingscommunicatie tussen miljoenen apparaten inschakelen en een back-end oplossing.</span><span class="sxs-lookup"><span data-stu-id="257bb-105">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="257bb-106">Hallo [aan de slag met IoT Hub] zelfstudie laat zien hoe toocreate een IoT-hub een apparaat-id in het inrichten en code van een gesimuleerde apparaattoepassing dat apparaat-naar-cloud-berichten verzendt.</span><span class="sxs-lookup"><span data-stu-id="257bb-106">hello [Get started with IoT Hub] tutorial shows how toocreate an IoT hub, provision a device identity in it, and code a simulated device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="257bb-107">Deze zelfstudie bouwt voort op [aan de slag met IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="257bb-107">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="257bb-108">Hier ziet u hoe aan:</span><span class="sxs-lookup"><span data-stu-id="257bb-108">It shows you how to:</span></span>

* <span data-ttu-id="257bb-109">Verzenden van uw back-end oplossing, cloud-naar-apparaatberichten tooa één apparaat via IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="257bb-109">From your solution back end, send cloud-to-device messages tooa single device through IoT Hub.</span></span>
* <span data-ttu-id="257bb-110">Cloud-naar-apparaat-berichten op een apparaat ontvangen.</span><span class="sxs-lookup"><span data-stu-id="257bb-110">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="257bb-111">Aanvragen van uw back-end oplossing, levering bevestiging (*feedback*) voor tooa apparaat van de berichten uit IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="257bb-111">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent tooa device from IoT Hub.</span></span>

<span data-ttu-id="257bb-112">U vindt meer informatie over cloud-naar-apparaat-berichten in Hallo [Ontwikkelaarshandleiding voor IoT Hub][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="257bb-112">You can find more information on cloud-to-device messages in hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="257bb-113">Aan het einde van de Hallo van deze zelfstudie, moet u twee Java-apps die console uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="257bb-113">At hello end of this tutorial, you run two Java console apps:</span></span>

* <span data-ttu-id="257bb-114">**simulated-device**, een aangepaste versie van het Hallo-app gemaakt in [aan de slag met IoT Hub], die verbinding maakt tooyour IoT-hub en cloud-naar-apparaat-berichten worden ontvangen.</span><span class="sxs-lookup"><span data-stu-id="257bb-114">**simulated-device**, a modified version of hello app created in [Get started with IoT Hub], which connects tooyour IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="257bb-115">**verzenden-c2d-berichten**, die een cloud-naar-apparaat bericht toohello gesimuleerde apparaattoepassing via IoT Hub verzendt en ontvangt u vervolgens de bevestiging levering.</span><span class="sxs-lookup"><span data-stu-id="257bb-115">**send-c2d-messages**, which sends a cloud-to-device message toohello simulated device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="257bb-116">IoT-Hub heeft SDK-ondersteuning voor veel apparaatplatforms en talen (inclusief C, Java en Javascript) via Azure IoT-apparaat-SDK's.</span><span class="sxs-lookup"><span data-stu-id="257bb-116">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="257bb-117">Voor stapsgewijze instructies voor hoe tooconnect uw apparaat toothis-zelfstudie code en over het algemeen tooAzure IoT Hub zien Hallo [Azure IoT Developer Center].</span><span class="sxs-lookup"><span data-stu-id="257bb-117">For step-by-step instructions on how tooconnect your device toothis tutorial's code, and generally tooAzure IoT Hub, see hello [Azure IoT Developer Center].</span></span>

<span data-ttu-id="257bb-118">toocomplete in deze zelfstudie, moet u hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="257bb-118">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="257bb-119">Een volledige werkende versie van Hallo [aan de slag met IoT Hub](iot-hub-java-java-getstarted.md) of [proces IoT Hub apparaat-naar-cloud-berichten](iot-hub-java-java-process-d2c.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="257bb-119">A complete working version of hello [Get started with IoT Hub](iot-hub-java-java-getstarted.md) or [Process IoT Hub device-to-cloud messages](iot-hub-java-java-process-d2c.md) tutorial.</span></span>
* <span data-ttu-id="257bb-120">meest recente Hallo [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="257bb-120">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="257bb-121">Maven 3</span><span class="sxs-lookup"><span data-stu-id="257bb-121">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="257bb-122">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="257bb-122">An active Azure account.</span></span> <span data-ttu-id="257bb-123">(Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)</span><span class="sxs-lookup"><span data-stu-id="257bb-123">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-hello-simulated-device-app"></a><span data-ttu-id="257bb-124">Berichten ontvangen in de gesimuleerde apparaattoepassing Hallo</span><span class="sxs-lookup"><span data-stu-id="257bb-124">Receive messages in hello simulated device app</span></span>

<span data-ttu-id="257bb-125">In deze sectie maakt u de gesimuleerde apparaattoepassing Hallo u hebt gemaakt in wijzigen [aan de slag met IoT Hub] tooreceive cloud-naar-apparaat-berichten uit Hallo iothub.</span><span class="sxs-lookup"><span data-stu-id="257bb-125">In this section, you modify hello simulated device app you created in [Get started with IoT Hub] tooreceive cloud-to-device messages from hello IoT hub.</span></span>

1. <span data-ttu-id="257bb-126">Met een teksteditor Hallo simulated-device\src\main\java\com\mycompany\app\App.java bestand openen.</span><span class="sxs-lookup"><span data-stu-id="257bb-126">Using a text editor, open hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

2. <span data-ttu-id="257bb-127">Voeg de volgende Hallo **MessageCallback** klasse als een geneste klasse binnen Hallo **App** klasse.</span><span class="sxs-lookup"><span data-stu-id="257bb-127">Add hello following **MessageCallback** class as a nested class inside hello **App** class.</span></span> <span data-ttu-id="257bb-128">Hallo **uitvoeren** methode wordt aangeroepen wanneer Hallo apparaat een bericht uit IoT Hub ontvangt.</span><span class="sxs-lookup"><span data-stu-id="257bb-128">hello **execute** method is invoked when hello device receives a message from IoT Hub.</span></span> <span data-ttu-id="257bb-129">In dit voorbeeld Hallo apparaat altijd een melding Hallo IoT-hub of het Hallo-bericht is voltooid:</span><span class="sxs-lookup"><span data-stu-id="257bb-129">In this example, hello device always notifies hello IoT hub that it has completed hello message:</span></span>

    ```java
    private static class AppMessageCallback implements MessageCallback {
      public IotHubMessageResult execute(Message msg, Object context) {
        System.out.println("Received message from hub: "
          + new String(msg.getBytes(), Message.DEFAULT_IOTHUB_MESSAGE_CHARSET));
    
        return IotHubMessageResult.COMPLETE;
      }
    }
    ```
3. <span data-ttu-id="257bb-130">Hallo wijzigen **belangrijkste** methode toocreate een **AppMessageCallback** exemplaar en aanroep Hallo **setMessageCallback** methode voordat het Hallo-client als volgt openen:</span><span class="sxs-lookup"><span data-stu-id="257bb-130">Modify hello **main** method toocreate an **AppMessageCallback** instance and call hello **setMessageCallback** method before it opens hello client as follows:</span></span>

    ```java
    client = new DeviceClient(connString, protocol);
   
    MessageCallback callback = new AppMessageCallback();
    client.setMessageCallback(callback, null);
    client.open();
    ```

    > [!NOTE]
    > <span data-ttu-id="257bb-131">Als u HTTP in plaats van MQTT of AMQP als Hallo transport gebruikt, Hallo **DeviceClient** exemplaar wordt gecontroleerd op berichten uit IoT Hub zelden (minder dan elke 25 minuten).</span><span class="sxs-lookup"><span data-stu-id="257bb-131">If you use HTTP instead of MQTT or AMQP as hello transport, hello **DeviceClient** instance checks for messages from IoT Hub infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="257bb-132">Zie voor meer informatie over Hallo verschillen tussen de protocollen MQTT, AMQP en HTTP-ondersteuning en Iothub beperking Hallo [Ontwikkelaarshandleiding voor IoT Hub][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="257bb-132">For more information about hello differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

4. <span data-ttu-id="257bb-133">Hallo toobuild **simulated-device** app met behulp van Maven, uitvoeren van de volgende opdracht achter de opdrachtprompt Hallo in de map simulated-device Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="257bb-133">toobuild hello **simulated-device** app using Maven, execute hello following command at hello command prompt in hello simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="257bb-134">Een cloud naar apparaat verzenden</span><span class="sxs-lookup"><span data-stu-id="257bb-134">Send a cloud-to-device message</span></span>

<span data-ttu-id="257bb-135">In deze sectie maakt maken u een Java-consoletoepassing die cloud-naar-apparaatberichten toohello gesimuleerde apparaattoepassing verzendt.</span><span class="sxs-lookup"><span data-stu-id="257bb-135">In this section, you create a Java console app that sends cloud-to-device messages toohello simulated device app.</span></span> <span data-ttu-id="257bb-136">U moet de apparaat-ID van het Hallo-apparaat die u hebt toegevoegd in Hallo Hallo [aan de slag met IoT Hub] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="257bb-136">You need hello device ID of hello device you added in hello [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="257bb-137">U moet de verbindingsreeks IoT Hub ook Hallo voor uw hub die u in Hallo vinden kunt [Azure-portal].</span><span class="sxs-lookup"><span data-stu-id="257bb-137">You also need hello IoT Hub connection string for your hub that you can find in hello [Azure portal].</span></span>

1. <span data-ttu-id="257bb-138">Maak een Maven-project aangeroepen **verzenden-c2d-berichten** met behulp van de volgende opdracht achter de opdrachtprompt Hallo.</span><span class="sxs-lookup"><span data-stu-id="257bb-138">Create a Maven project called **send-c2d-messages** using hello following command at your command prompt.</span></span> <span data-ttu-id="257bb-139">Houd rekening met dat deze opdracht is een enkele, lange opdracht:</span><span class="sxs-lookup"><span data-stu-id="257bb-139">Note this command is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=send-c2d-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="257bb-140">Navigeer toohello nieuwe verzenden-c2d-berichten map bij de opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="257bb-140">At your command prompt, navigate toohello new send-c2d-messages folder.</span></span>

3. <span data-ttu-id="257bb-141">Met een teksteditor, open Hallo pom.xml-bestand in Hallo verzenden-c2d-berichten map en Hallo afhankelijkheid toohello na toevoegen **afhankelijkheden** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="257bb-141">Using a text editor, open hello pom.xml file in hello send-c2d-messages folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="257bb-142">Hallo-afhankelijkheid toevoegen kunt u toouse hello **iothub-java-service-client** pakket in uw toepassing toocommunicate met de service van uw IoT-hub:</span><span class="sxs-lookup"><span data-stu-id="257bb-142">Adding hello dependency enables you toouse hello **iothub-java-service-client** package in your application toocommunicate with your IoT hub service:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="257bb-143">U kunt controleren op de meest recente versie van Hallo **iot-service-client** met [Maven search][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="257bb-143">You can check for hello latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

4. <span data-ttu-id="257bb-144">Opslaan en sluiten Hallo pom.xml-bestand.</span><span class="sxs-lookup"><span data-stu-id="257bb-144">Save and close hello pom.xml file.</span></span>

5. <span data-ttu-id="257bb-145">Met een teksteditor Hallo send-c2d-messages\src\main\java\com\mycompany\app\App.java bestand openen.</span><span class="sxs-lookup"><span data-stu-id="257bb-145">Using a text editor, open hello send-c2d-messages\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="257bb-146">Voeg de volgende Hallo **importeren** instructies toohello bestand:</span><span class="sxs-lookup"><span data-stu-id="257bb-146">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. <span data-ttu-id="257bb-147">Hallo klasseniveau variabelen toohello na toevoegen **App** klasse, Vervang **{yourhubconnectionstring}** en **{yourdeviceid}** Hello waarden uw aangegeven eerder:</span><span class="sxs-lookup"><span data-stu-id="257bb-147">Add hello following class-level variables toohello **App** class, replacing **{yourhubconnectionstring}** and **{yourdeviceid}** with hello values your noted earlier:</span></span>

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "{yourdeviceid}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    ```

8. <span data-ttu-id="257bb-148">Vervang Hallo **belangrijkste** methode Hello code te volgen.</span><span class="sxs-lookup"><span data-stu-id="257bb-148">Replace hello **main** method with hello following code.</span></span> <span data-ttu-id="257bb-149">Deze code tooyour IoT-hub verbindt, verzendt een bericht tooyour apparaat en wordt er gewacht totdat een bevestiging dat Hallo-bericht ontvangen en verwerken Hallo van apparaat:</span><span class="sxs-lookup"><span data-stu-id="257bb-149">This code connects tooyour IoT hub, sends a message tooyour device, and then waits for an acknowledgment that hello device received and processed hello message:</span></span>
   
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
    > <span data-ttu-id="257bb-150">Deze zelfstudie implementeert voor de eenvoud mogelijk te houden, niet een beleid voor opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="257bb-150">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="257bb-151">In productiecode moet u beleid voor opnieuw proberen (zoals exponentieel uitstel), zoals voorgesteld in de MSDN-artikel Hallo implementeren [afhandeling van tijdelijke fout].</span><span class="sxs-lookup"><span data-stu-id="257bb-151">In production code, you should implement retry policies (such as exponential backoff), as suggested in hello MSDN article [Transient Fault Handling].</span></span>


9. <span data-ttu-id="257bb-152">Hallo toobuild **simulated-device** app met behulp van Maven, uitvoeren van de volgende opdracht achter de opdrachtprompt Hallo in de map simulated-device Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="257bb-152">toobuild hello **simulated-device** app using Maven, execute hello following command at hello command prompt in hello simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-hello-applications"></a><span data-ttu-id="257bb-153">Hallo-toepassingen uitvoeren</span><span class="sxs-lookup"><span data-stu-id="257bb-153">Run hello applications</span></span>

<span data-ttu-id="257bb-154">U bent nu klaar toorun Hallo toepassingen.</span><span class="sxs-lookup"><span data-stu-id="257bb-154">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="257bb-155">Uitvoeren bij een opdrachtprompt in de map simulated-device Hallo Hallo opdracht toobegin verzenden van telemetrie tooyour iothub en toolisten voor cloud-naar-apparaat-berichten van uw hub te volgen:</span><span class="sxs-lookup"><span data-stu-id="257bb-155">At a command prompt in hello simulated-device folder, run hello following command toobegin sending telemetry tooyour IoT hub and toolisten for cloud-to-device messages sent from your hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![De gesimuleerde apparaattoepassing Hallo uitvoeren][img-simulated-device]

2. <span data-ttu-id="257bb-157">Voer bij een opdrachtprompt in Hallo verzenden-c2d-berichten map Hallo opdracht toosend na een cloud-naar-apparaat-bericht en de wachttijd voor een bevestiging feedback:</span><span class="sxs-lookup"><span data-stu-id="257bb-157">At a command prompt in hello send-c2d-messages folder, run hello following command toosend a cloud-to-device message and wait for a feedback acknowledgment:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![Hallo opdracht toosend Hallo-bericht van cloud-naar-apparaat worden uitgevoerd][img-send-command]

## <a name="next-steps"></a><span data-ttu-id="257bb-159">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="257bb-159">Next steps</span></span>

<span data-ttu-id="257bb-160">In deze zelfstudie hebt u geleerd hoe toosend en cloud-naar-apparaat-berichten ontvangen.</span><span class="sxs-lookup"><span data-stu-id="257bb-160">In this tutorial, you learned how toosend and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="257bb-161">Voorbeelden van volledige end-to-end-oplossingen die gebruikmaken van IoT Hub toosee Zie [Azure IoT Suite].</span><span class="sxs-lookup"><span data-stu-id="257bb-161">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="257bb-162">toolearn meer informatie over het ontwikkelen van oplossingen met IoT Hub, Zie Hallo [Ontwikkelaarshandleiding voor IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="257bb-162">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

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