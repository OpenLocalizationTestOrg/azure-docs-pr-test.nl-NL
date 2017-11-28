---
title: aaaProcess Azure IoT Hub apparaat-naar-cloud-berichten (Java) | Microsoft Docs
description: Hoe berichten tooprocess IoT Hub apparaat-naar-cloud-berichten met behulp van regels voor het doorsturen en aangepaste eindpunten toodispatch tooother back-end-services.
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: bd9af5f9-a740-4780-a2a6-8c0e2752cf48
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: dobett
ms.openlocfilehash: 084e84e721ca4297c4d7d6cb06a43b0bed9bce85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="process-iot-hub-device-to-cloud-messages-java"></a><span data-ttu-id="a76d6-103">Verwerken van Iothub apparaat-naar-cloud-berichten (Java)</span><span class="sxs-lookup"><span data-stu-id="a76d6-103">Process IoT Hub device-to-cloud messages (Java)</span></span>

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

<span data-ttu-id="a76d6-104">Azure IoT Hub is een volledig beheerde service waarmee betrouwbare en veilige tweerichtingscommunicatie tussen miljoenen apparaten en een oplossing voor back-end.</span><span class="sxs-lookup"><span data-stu-id="a76d6-104">Azure IoT Hub is a fully managed service that enables reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="a76d6-105">Andere zelfstudies ([aan de slag met IoT Hub] en [cloud naar apparaat verzenden met IoT Hub][lnk-c2d]) ziet u hoe toouse Hallo basic apparaat-naar-cloud- en cloud-naar-apparaat Messaging-functionaliteit van IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a76d6-105">Other tutorials ([Get started with IoT Hub] and [Send cloud-to-device messages with IoT Hub][lnk-c2d]) show you how toouse hello basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span>

<span data-ttu-id="a76d6-106">Deze zelfstudie bouwt voort op Hallo-code die wordt weergegeven in Hallo [aan de slag met IoT Hub] zelfstudie en toont u hoe toouse routering tooprocess apparaat-naar-cloud-berichten in een schaalbare manier bericht.</span><span class="sxs-lookup"><span data-stu-id="a76d6-106">This tutorial builds on hello code shown in hello [Get started with IoT Hub] tutorial, and shows you how toouse message routing tooprocess device-to-cloud messages in a scalable way.</span></span> <span data-ttu-id="a76d6-107">Hallo-zelfstudie ziet u hoe tooprocess berichten waarvoor onmiddellijke actie van de oplossing Hallo back-end.</span><span class="sxs-lookup"><span data-stu-id="a76d6-107">hello tutorial illustrates how tooprocess messages that require immediate action from hello solution back end.</span></span> <span data-ttu-id="a76d6-108">Een apparaat kan bijvoorbeeld een waarschuwing weergegeven dat activeert een ticket in een CRM-systeem invoegen verzenden.</span><span class="sxs-lookup"><span data-stu-id="a76d6-108">For example, a device might send an alarm message that triggers inserting a ticket into a CRM system.</span></span> <span data-ttu-id="a76d6-109">Gegevenspunt berichten feed daarentegen alleen in een analyse-engine.</span><span class="sxs-lookup"><span data-stu-id="a76d6-109">By contrast, data-point messages simply feed into an analytics engine.</span></span> <span data-ttu-id="a76d6-110">Telemetrie van de temperatuur van een apparaat dat is opgeslagen voor latere analyse toobe is bijvoorbeeld een gegevenspunt bericht.</span><span class="sxs-lookup"><span data-stu-id="a76d6-110">For example, temperature telemetry from a device that is toobe stored for later analysis is a data-point message.</span></span>

<span data-ttu-id="a76d6-111">Aan het einde van de Hallo van deze zelfstudie, moet u drie Java-apps die console uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="a76d6-111">At hello end of this tutorial, you run three Java console apps:</span></span>

* <span data-ttu-id="a76d6-112">**simulated-device**, een aangepaste versie van het Hallo-app gemaakt in Hallo [aan de slag met IoT Hub] zelfstudie verzendt gegevenspunt apparaat-naar-cloud-berichten per seconde en interactieve apparaat-naar-cloud met berichten voor elke 10 seconden.</span><span class="sxs-lookup"><span data-stu-id="a76d6-112">**simulated-device**, a modified version of hello app created in hello [Get started with IoT Hub] tutorial, sends data-point device-to-cloud messages every second, and interactive device-to-cloud messages every 10 seconds.</span></span> <span data-ttu-id="a76d6-113">Deze app gebruikt Hallo AMQP-protocol toocommunicate met IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a76d6-113">This app uses hello AMQP protocol toocommunicate with IoT Hub.</span></span>
* <span data-ttu-id="a76d6-114">**Read-d2c-messages** Hallo telemetrie verzonden door de app op uw apparaat weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a76d6-114">**read-d2c-messages** displays hello telemetry sent by your device app.</span></span>
* <span data-ttu-id="a76d6-115">**alleen kritieke wachtrij** ongedaan kritieke Hallo-berichten van Hallo Service Bus-wachtrij gekoppeld toohello IoT-hub in de wachtrij geplaatst.</span><span class="sxs-lookup"><span data-stu-id="a76d6-115">**read-critical-queue** de-queues hello critical messages from hello Service Bus queue attached toohello IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="a76d6-116">IoT Hub heeft ondersteuning voor veel apparaatplatforms en talen, waaronder C, Java en JavaScript SDK.</span><span class="sxs-lookup"><span data-stu-id="a76d6-116">IoT Hub has SDK support for many device platforms and languages, including C, Java, and JavaScript.</span></span> <span data-ttu-id="a76d6-117">Voor instructies over hoe tooreplace apparaat Hallo in deze zelfstudie met een fysiek apparaat en hoe tooconnect apparaten tooan IoT Hub Hallo zien [Azure IoT Developer Center].</span><span class="sxs-lookup"><span data-stu-id="a76d6-117">For instructions on how tooreplace hello device in this tutorial with a physical device, and how tooconnect devices tooan IoT Hub, see hello [Azure IoT Developer Center].</span></span>

<span data-ttu-id="a76d6-118">toocomplete in deze zelfstudie, moet u hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="a76d6-118">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="a76d6-119">Een volledige werkende versie van Hallo [aan de slag met IoT Hub] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="a76d6-119">A complete working version of hello [Get started with IoT Hub] tutorial.</span></span>
* <span data-ttu-id="a76d6-120">meest recente Hallo [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="a76d6-120">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="a76d6-121">Maven 3</span><span class="sxs-lookup"><span data-stu-id="a76d6-121">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="a76d6-122">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="a76d6-122">An active Azure account.</span></span> <span data-ttu-id="a76d6-123">(Als u geen account hebt, kunt u een [gratis account] [lnk-free-trial] binnen een paar minuten.)</span><span class="sxs-lookup"><span data-stu-id="a76d6-123">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="a76d6-124">Er is enige basiskennis van [Azure Storage] en [Azure Service Bus].</span><span class="sxs-lookup"><span data-stu-id="a76d6-124">You should have some basic knowledge of [Azure Storage] and [Azure Service Bus].</span></span>

## <a name="send-interactive-messages-from-a-device-app"></a><span data-ttu-id="a76d6-125">Interactieve berichten verzenden vanuit een apparaat-app</span><span class="sxs-lookup"><span data-stu-id="a76d6-125">Send interactive messages from a device app</span></span>
<span data-ttu-id="a76d6-126">In deze sectie maakt u Hallo apparaattoepassing u hebt gemaakt in Hallo wijzigen [aan de slag met IoT Hub] zelfstudie toooccasionally berichten verzenden die direct verwerking vereist.</span><span class="sxs-lookup"><span data-stu-id="a76d6-126">In this section, you modify hello device app you created in hello [Get started with IoT Hub] tutorial toooccasionally send messages that require immediate processing.</span></span>

1. <span data-ttu-id="a76d6-127">Gebruik een editor tooopen hello simulated-device\src\main\java\com\mycompany\app\App.java tekstbestand.</span><span class="sxs-lookup"><span data-stu-id="a76d6-127">Use a text editor tooopen hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span> <span data-ttu-id="a76d6-128">Dit bestand bevat de code voor Hallo Hallo **simulated-device** app die u hebt gemaakt in Hallo [aan de slag met IoT Hub] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="a76d6-128">This file contains hello code for hello **simulated-device** app you created in hello [Get started with IoT Hub] tutorial.</span></span>

2. <span data-ttu-id="a76d6-129">Vervang Hallo **MessageSender** klasse Hello code te volgen:</span><span class="sxs-lookup"><span data-stu-id="a76d6-129">Replace hello **MessageSender** class with hello following code:</span></span>

    ```java
    private static class MessageSender implements Runnable {

        public void run()  {
            try {
                double minTemperature = 20;
                double minHumidity = 60;
                Random rand = new Random();

                while (true) {
                    String msgStr;
                    Message msg;
                    if (new Random().nextDouble() > 0.7) {
                        msgStr = "This is a critical message.";
                        msg = new Message(msgStr);
                        msg.setProperty("level", "critical");
                    } else {
                        double currentTemperature = minTemperature + rand.nextDouble() * 15;
                        double currentHumidity = minHumidity + rand.nextDouble() * 20; 
                        TelemetryDataPoint telemetryDataPoint = new TelemetryDataPoint();
                        telemetryDataPoint.deviceId = deviceId;
                        telemetryDataPoint.temperature = currentTemperature;
                        telemetryDataPoint.humidity = currentHumidity;

                        msgStr = telemetryDataPoint.serialize();
                        msg = new Message(msgStr);
                    }
                    
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
   
    <span data-ttu-id="a76d6-130">Met deze methode wordt willekeurig Hallo eigenschap `"level": "critical"` toomessages verzonden door het Hallo apparaat simuleert een bericht dat directe actie is vereist door Hallo toepassing back-end.</span><span class="sxs-lookup"><span data-stu-id="a76d6-130">This method randomly adds hello property `"level": "critical"` toomessages sent by hello device, which simulates a message that requires immediate action by hello application back-end.</span></span> <span data-ttu-id="a76d6-131">Hallo-toepassing geeft deze informatie in de eigenschappen van Hallo-bericht, in plaats van in de hoofdtekst van Hallo-bericht, zodat deze IoT-Hub Hallo-bericht toohello juiste berichtenbestemming versturen kunt.</span><span class="sxs-lookup"><span data-stu-id="a76d6-131">hello application passes this information in hello message properties, instead of in hello message body, so that IoT Hub can route hello message toohello proper message destination.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a76d6-132">U kunt bericht eigenschappen tooroute berichten gebruiken voor verschillende scenario's, met inbegrip van koude pad verwerken bovendien toohello hot pad voorbeeld hier weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a76d6-132">You can use message properties tooroute messages for various scenarios including cold-path processing, in addition toohello hot path example shown here.</span></span>

2. <span data-ttu-id="a76d6-133">Opslaan en sluiten van de bestand simulated-device\src\main\java\com\mycompany\app\App.java Hallo.</span><span class="sxs-lookup"><span data-stu-id="a76d6-133">Save and close hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a76d6-134">Deze zelfstudie implementeert voor Hallo mogelijk te houden van eenvoud, niet een beleid voor opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="a76d6-134">For hello sake of simplicity, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="a76d6-135">In productiecode moet u een beleid voor opnieuw proberen zoals exponentieel uitstel, zoals voorgesteld in de MSDN-artikel Hallo implementeren [afhandeling van tijdelijke fout].</span><span class="sxs-lookup"><span data-stu-id="a76d6-135">In production code, you should implement a retry policy such as exponential backoff, as suggested in hello MSDN article [Transient Fault Handling].</span></span>

3. <span data-ttu-id="a76d6-136">Hallo toobuild **simulated-device** app met behulp van Maven, uitvoeren van de volgende opdracht achter de opdrachtprompt Hallo in de map simulated-device Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="a76d6-136">toobuild hello **simulated-device** app using Maven, execute hello following command at hello command prompt in hello simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="add-a-queue-tooyour-iot-hub-and-route-messages-tooit"></a><span data-ttu-id="a76d6-137">IoT een tooyour wachtrij hub en route u het tooit berichten toevoegen</span><span class="sxs-lookup"><span data-stu-id="a76d6-137">Add a queue tooyour IoT hub and route messages tooit</span></span>

<span data-ttu-id="a76d6-138">In deze sectie maakt een Service Bus-wachtrij, verbindt u deze tooyour IoT-hub en configureren van uw IoT hub toosend berichten toohello wachtrij op basis van Hallo aanwezigheid van een eigenschap van het Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="a76d6-138">In this section, you create a Service Bus queue, connect it tooyour IoT hub, and configure your IoT hub toosend messages toohello queue based on hello presence of a property on hello message.</span></span> <span data-ttu-id="a76d6-139">Zie voor meer informatie over hoe tooprocess van van Service Bus-wachtrijen berichten [aan de slag met wachtrijen][lnk-sb-queues-java].</span><span class="sxs-lookup"><span data-stu-id="a76d6-139">For more information about how tooprocess messages from Service Bus queues, see [Get started with queues][lnk-sb-queues-java].</span></span>

1. <span data-ttu-id="a76d6-140">Een Service Bus-wachtrij maakt, zoals beschreven in [aan de slag met wachtrijen][lnk-sb-queues-java].</span><span class="sxs-lookup"><span data-stu-id="a76d6-140">Create a Service Bus queue as described in [Get started with queues][lnk-sb-queues-java].</span></span> <span data-ttu-id="a76d6-141">Maak een notitie van Hallo naamruimte en de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="a76d6-141">Make a note of hello namespace and queue name.</span></span>

2. <span data-ttu-id="a76d6-142">In Azure-portal hello, opent u uw IoT-hub en klik op **eindpunten**.</span><span class="sxs-lookup"><span data-stu-id="a76d6-142">In hello Azure portal, open your IoT hub and click **Endpoints**.</span></span>

    ![Eindpunten van IoT-hub][30]

3. <span data-ttu-id="a76d6-144">In Hallo **eindpunten** blade, klikt u op **toevoegen** op Hallo bovenste tooadd uw wachtrij tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="a76d6-144">In hello **Endpoints** blade, click **Add** at hello top tooadd your queue tooyour IoT hub.</span></span> <span data-ttu-id="a76d6-145">Naam Hallo eindpunt **CriticalQueue** en gebruik Hallo-keuzelijsten tooselect **Service Bus-wachtrij**Hallo Service Bus-naamruimte waarin de wachtrij zich bevindt en de naam van uw wachtrij Hallo.</span><span class="sxs-lookup"><span data-stu-id="a76d6-145">Name hello endpoint **CriticalQueue** and use hello drop-downs tooselect **Service Bus queue**, hello Service Bus namespace in which your queue resides, and hello name of your queue.</span></span> <span data-ttu-id="a76d6-146">Wanneer u klaar bent, klikt u op **opslaan** Hallo onderaan.</span><span class="sxs-lookup"><span data-stu-id="a76d6-146">When you are done, click **Save** at hello bottom.</span></span>

    ![Een eindpunt toevoegen][31]

4. <span data-ttu-id="a76d6-148">Klik nu op **Routes** in uw IoT-Hub.</span><span class="sxs-lookup"><span data-stu-id="a76d6-148">Now click **Routes** in your IoT Hub.</span></span> <span data-ttu-id="a76d6-149">Klik op **toevoegen** bovenaan Hallo Hallo blade toocreate een regel voor doorsturen die routeert berichten toohello wachtrij u zojuist hebt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="a76d6-149">Click **Add** at hello top of hello blade toocreate a routing rule that routes messages toohello queue you just added.</span></span> <span data-ttu-id="a76d6-150">Selecteer **DeviceTelemetry** als Hallo gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="a76d6-150">Select **DeviceTelemetry** as hello source of data.</span></span> <span data-ttu-id="a76d6-151">Voer `level="critical"` als Hallo voorwaarde, en kies Hallo wachtrij die u zojuist hebt toegevoegd als een aangepaste eindpunt als Hallo regel eindpunt routering.</span><span class="sxs-lookup"><span data-stu-id="a76d6-151">Enter `level="critical"` as hello condition, and choose hello queue you just added as a custom endpoint as hello routing rule endpoint.</span></span> <span data-ttu-id="a76d6-152">Wanneer u klaar bent, klikt u op **opslaan** Hallo onderaan.</span><span class="sxs-lookup"><span data-stu-id="a76d6-152">When you are done, click **Save** at hello bottom.</span></span>

    ![Toevoegen van een route][32]

    <span data-ttu-id="a76d6-154">Zorg ervoor dat Hallo terugval route is ingesteld, te**ON**.</span><span class="sxs-lookup"><span data-stu-id="a76d6-154">Make sure hello fallback route is set too**ON**.</span></span> <span data-ttu-id="a76d6-155">Deze instelling is de standaardconfiguratie Hallo van een IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="a76d6-155">This setting is hello default configuration of an IoT hub.</span></span>

    ![Route voor terugval][33]

## <a name="optional-read-from-hello-queue-endpoint"></a><span data-ttu-id="a76d6-157">(Optioneel) Lezen van Hallo wachtrij eindpunt</span><span class="sxs-lookup"><span data-stu-id="a76d6-157">(Optional) Read from hello queue endpoint</span></span>

<span data-ttu-id="a76d6-158">U kunt eventueel Hallo-berichten lezen van Hallo wachtrij eindpunt door het Hallo-instructies in [aan de slag met wachtrijen][lnk-sb-queues-java].</span><span class="sxs-lookup"><span data-stu-id="a76d6-158">You can optionally read hello messages from hello queue endpoint by following hello instructions in [Get started with queues][lnk-sb-queues-java].</span></span> <span data-ttu-id="a76d6-159">Naam Hallo app **lezen kritieke wachtrij**.</span><span class="sxs-lookup"><span data-stu-id="a76d6-159">Name hello app **read-critical-queue**.</span></span>

## <a name="run-hello-applications"></a><span data-ttu-id="a76d6-160">Hallo-toepassingen uitvoeren</span><span class="sxs-lookup"><span data-stu-id="a76d6-160">Run hello applications</span></span>

<span data-ttu-id="a76d6-161">U bent nu klaar toorun Hallo drie toepassingen.</span><span class="sxs-lookup"><span data-stu-id="a76d6-161">Now you are ready toorun hello three applications.</span></span>

1. <span data-ttu-id="a76d6-162">Hallo toorun **read-d2c-messages** toepassing in een opdrachtprompt of een shell toohello read-d2c-map te navigeren en Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="a76d6-162">toorun hello **read-d2c-messages** application, in a command prompt or shell navigate toohello read-d2c folder and execute hello following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```

   ![Read-d2c-messages uitvoeren][readd2c]

2. <span data-ttu-id="a76d6-164">Hallo toorun **lezen kritieke wachtrij** toepassing in een opdrachtprompt of een shell toohello lezen kritieke wachtrij map te navigeren en Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="a76d6-164">toorun hello **read-critical-queue** application, in a command prompt or shell navigate toohello read-critical-queue folder and execute hello following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Alleen kritieke berichten uitgevoerd][readqueue]

3. <span data-ttu-id="a76d6-166">Hallo toorun **simulated-device** app in een opdrachtprompt of een shell gaat u de map simulated-device toohello en Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="a76d6-166">toorun hello **simulated-device** app, in a command prompt or shell navigate toohello simulated-device folder and execute hello following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Simulated-device uitvoeren][simulateddevice]

## <a name="next-steps"></a><span data-ttu-id="a76d6-168">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a76d6-168">Next steps</span></span>

<span data-ttu-id="a76d6-169">In deze zelfstudie hebt u geleerd hoe tooreliably apparaat-naar-cloud-berichten verzenden met behulp van Hallo-bericht routeringsfunctionaliteit van IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a76d6-169">In this tutorial, you learned how tooreliably dispatch device-to-cloud messages by using hello message routing functionality of IoT Hub.</span></span>

<span data-ttu-id="a76d6-170">Hallo [hoe toosend cloud-naar-apparaat met IoT Hub berichten] [ lnk-c2d] ziet u hoe toosend tooyour apparaten uit de back-end van uw oplossing berichten.</span><span class="sxs-lookup"><span data-stu-id="a76d6-170">hello [How toosend cloud-to-device messages with IoT Hub][lnk-c2d] shows you how toosend messages tooyour devices from your solution back end.</span></span>

<span data-ttu-id="a76d6-171">Voorbeelden van volledige end-to-end-oplossingen die gebruikmaken van IoT Hub toosee Zie [Azure IoT Suite][lnk-suite].</span><span class="sxs-lookup"><span data-stu-id="a76d6-171">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite][lnk-suite].</span></span>

<span data-ttu-id="a76d6-172">toolearn meer informatie over het ontwikkelen van oplossingen met IoT Hub, Zie Hallo [Ontwikkelaarshandleiding voor IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="a76d6-172">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

<span data-ttu-id="a76d6-173">Zie toolearn meer informatie over het routeren van berichten van IoT-Hub [berichten verzenden en ontvangen met IoT Hub][lnk-devguide-messaging].</span><span class="sxs-lookup"><span data-stu-id="a76d6-173">toolearn more about message routing in IoT Hub, see [Send and receive messages with IoT Hub][lnk-devguide-messaging].</span></span>

<!-- Images. -->
<!-- TODO: UPDATE PICTURES -->
[simulateddevice]: ./media/iot-hub-java-java-process-d2c/runsimulateddevice.png
[readd2c]: ./media/iot-hub-java-java-process-d2c/runprocessinteractive.png
[readqueue]: ./media/iot-hub-java-java-process-d2c/runprocessd2c.png

[30]: ./media/iot-hub-java-java-process-d2c/click-endpoints.png
[31]: ./media/iot-hub-java-java-process-d2c/endpoint-creation.png
[32]: ./media/iot-hub-java-java-process-d2c/route-creation.png
[33]: ./media/iot-hub-java-java-process-d2c/fallback-route.png

<!-- Links -->

[lnk-sb-queues-java]: ../service-bus-messaging/service-bus-java-how-to-use-queues.md

[Azure Storage]: https://azure.microsoft.com/documentation/services/storage/
[Azure Service Bus]: https://azure.microsoft.com/documentation/services/service-bus/

[Ontwikkelaarshandleiding voor IoT Hub]: iot-hub-devguide.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
[aan de slag met IoT Hub]: iot-hub-java-java-getstarted.md
[Azure IoT Developer Center]: https://azure.microsoft.com/develop/iot
[afhandeling van tijdelijke fout]: https://msdn.microsoft.com/library/hh675232.aspx

<!-- Links -->
[Afhandeling van tijdelijke fout]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-c2d]: iot-hub-java-java-c2d.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
