---
title: Azure IoT Hub apparaat-naar-cloud-berichten (Java) | Microsoft Docs
description: Klik hier voor meer informatie over het verwerken van IoT Hub apparaat-naar-cloud-berichten met behulp van regels voor het doorsturen en aangepaste eindpunten verzending van berichten naar andere back-end-services.
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
ms.openlocfilehash: d1aca8f39e305105d4ec9f63fbe7bee95487e294
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="process-iot-hub-device-to-cloud-messages-java"></a><span data-ttu-id="3b74f-103">Verwerken van Iothub apparaat-naar-cloud-berichten (Java)</span><span class="sxs-lookup"><span data-stu-id="3b74f-103">Process IoT Hub device-to-cloud messages (Java)</span></span>

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

<span data-ttu-id="3b74f-104">Azure IoT Hub is een volledig beheerde service waarmee betrouwbare en veilige tweerichtingscommunicatie tussen miljoenen apparaten en een oplossing voor back-end.</span><span class="sxs-lookup"><span data-stu-id="3b74f-104">Azure IoT Hub is a fully managed service that enables reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="3b74f-105">Andere zelfstudies ([aan de slag met IoT Hub] en [cloud naar apparaat verzenden met IoT Hub][lnk-c2d]) hoe u het basic apparaat-naar-cloud- en cloud-naar-apparaat gebruiken Messaging-functionaliteit van IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3b74f-105">Other tutorials ([Get started with IoT Hub] and [Send cloud-to-device messages with IoT Hub][lnk-c2d]) show you how to use the basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span>

<span data-ttu-id="3b74f-106">Deze zelfstudie bouwt voort op de code die wordt weergegeven de [aan de slag met IoT Hub] zelfstudie, en hoe u berichtroutering gebruiken voor het verwerken van apparaat-naar-cloud-berichten in een schaalbare manier.</span><span class="sxs-lookup"><span data-stu-id="3b74f-106">This tutorial builds on the code shown in the [Get started with IoT Hub] tutorial, and shows you how to use message routing to process device-to-cloud messages in a scalable way.</span></span> <span data-ttu-id="3b74f-107">De zelfstudie laat zien hoe berichten waarvoor onmiddellijke actie van de back-end oplossing te verwerken.</span><span class="sxs-lookup"><span data-stu-id="3b74f-107">The tutorial illustrates how to process messages that require immediate action from the solution back end.</span></span> <span data-ttu-id="3b74f-108">Een apparaat kan bijvoorbeeld een waarschuwing weergegeven dat activeert een ticket in een CRM-systeem invoegen verzenden.</span><span class="sxs-lookup"><span data-stu-id="3b74f-108">For example, a device might send an alarm message that triggers inserting a ticket into a CRM system.</span></span> <span data-ttu-id="3b74f-109">Gegevenspunt berichten feed daarentegen alleen in een analyse-engine.</span><span class="sxs-lookup"><span data-stu-id="3b74f-109">By contrast, data-point messages simply feed into an analytics engine.</span></span> <span data-ttu-id="3b74f-110">Telemetrie van de temperatuur van een apparaat dat moet worden opgeslagen voor latere analyse is bijvoorbeeld een gegevenspunt bericht.</span><span class="sxs-lookup"><span data-stu-id="3b74f-110">For example, temperature telemetry from a device that is to be stored for later analysis is a data-point message.</span></span>

<span data-ttu-id="3b74f-111">Aan het einde van deze zelfstudie, moet u drie Java-apps die console uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="3b74f-111">At the end of this tutorial, you run three Java console apps:</span></span>

* <span data-ttu-id="3b74f-112">**simulated-device**, een aangepaste versie van de app gemaakt in de [aan de slag met IoT Hub] zelfstudie verzendt gegevenspunt apparaat-naar-cloud-berichten per seconde en interactieve apparaat-naar-cloud met berichten voor elke 10 seconden .</span><span class="sxs-lookup"><span data-stu-id="3b74f-112">**simulated-device**, a modified version of the app created in the [Get started with IoT Hub] tutorial, sends data-point device-to-cloud messages every second, and interactive device-to-cloud messages every 10 seconds.</span></span> <span data-ttu-id="3b74f-113">Deze app gebruikt het AMQP-protocol om te communiceren met IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3b74f-113">This app uses the AMQP protocol to communicate with IoT Hub.</span></span>
* <span data-ttu-id="3b74f-114">**Read-d2c-messages** geeft de telemetrie die is verzonden door de app op uw apparaat weer.</span><span class="sxs-lookup"><span data-stu-id="3b74f-114">**read-d2c-messages** displays the telemetry sent by your device app.</span></span>
* <span data-ttu-id="3b74f-115">**alleen kritieke wachtrij** ongedaan de kritieke berichten uit de Service Bus-wachtrij gekoppeld aan de IoT-hub in de wachtrij geplaatst.</span><span class="sxs-lookup"><span data-stu-id="3b74f-115">**read-critical-queue** de-queues the critical messages from the Service Bus queue attached to the IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="3b74f-116">IoT Hub heeft ondersteuning voor veel apparaatplatforms en talen, waaronder C, Java en JavaScript SDK.</span><span class="sxs-lookup"><span data-stu-id="3b74f-116">IoT Hub has SDK support for many device platforms and languages, including C, Java, and JavaScript.</span></span> <span data-ttu-id="3b74f-117">Zie voor instructies over hoe het apparaat in deze zelfstudie vervangen door een fysiek apparaat en hoe apparaten verbinden met een IoT-Hub, de [Azure IoT Developer Center].</span><span class="sxs-lookup"><span data-stu-id="3b74f-117">For instructions on how to replace the device in this tutorial with a physical device, and how to connect devices to an IoT Hub, see the [Azure IoT Developer Center].</span></span>

<span data-ttu-id="3b74f-118">Voor het voltooien van deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="3b74f-118">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="3b74f-119">Een volledige werkende versie van de [aan de slag met IoT Hub] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="3b74f-119">A complete working version of the [Get started with IoT Hub] tutorial.</span></span>
* <span data-ttu-id="3b74f-120">De meest recente [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="3b74f-120">The latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="3b74f-121">Maven 3</span><span class="sxs-lookup"><span data-stu-id="3b74f-121">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="3b74f-122">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="3b74f-122">An active Azure account.</span></span> <span data-ttu-id="3b74f-123">(Als u geen account hebt, kunt u een [gratis account] [lnk-free-trial] binnen een paar minuten.)</span><span class="sxs-lookup"><span data-stu-id="3b74f-123">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="3b74f-124">Er is enige basiskennis van [Azure Storage] en [Azure Service Bus].</span><span class="sxs-lookup"><span data-stu-id="3b74f-124">You should have some basic knowledge of [Azure Storage] and [Azure Service Bus].</span></span>

## <a name="send-interactive-messages-from-a-device-app"></a><span data-ttu-id="3b74f-125">Interactieve berichten verzenden vanuit een apparaat-app</span><span class="sxs-lookup"><span data-stu-id="3b74f-125">Send interactive messages from a device app</span></span>
<span data-ttu-id="3b74f-126">In deze sectie die u wijzigt de apparaat-app die u hebt gemaakt in de [aan de slag met IoT Hub] zelfstudie af en toe om berichten te verzenden waarvoor onmiddellijke verwerking.</span><span class="sxs-lookup"><span data-stu-id="3b74f-126">In this section, you modify the device app you created in the [Get started with IoT Hub] tutorial to occasionally send messages that require immediate processing.</span></span>

1. <span data-ttu-id="3b74f-127">Gebruik een teksteditor te openen van het bestand simulated-device\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="3b74f-127">Use a text editor to open the simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span> <span data-ttu-id="3b74f-128">Dit bestand bevat de code voor de **simulated-device** app die u hebt gemaakt in de [aan de slag met IoT Hub] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="3b74f-128">This file contains the code for the **simulated-device** app you created in the [Get started with IoT Hub] tutorial.</span></span>

2. <span data-ttu-id="3b74f-129">Vervang de **MessageSender** klasse met de volgende code:</span><span class="sxs-lookup"><span data-stu-id="3b74f-129">Replace the **MessageSender** class with the following code:</span></span>

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
   
    <span data-ttu-id="3b74f-130">Deze methode wordt willekeurig toegevoegd voor de eigenschap `"level": "critical"` op berichten die door het apparaat verzonden, die een bericht dat directe actie is vereist door de toepassing van de back-end simuleert.</span><span class="sxs-lookup"><span data-stu-id="3b74f-130">This method randomly adds the property `"level": "critical"` to messages sent by the device, which simulates a message that requires immediate action by the application back-end.</span></span> <span data-ttu-id="3b74f-131">De toepassing geeft deze informatie in de berichteigenschappen in plaats van in de hoofdtekst van het bericht, zodat deze IoT Hub het bericht naar de juiste bestemming sturen kan.</span><span class="sxs-lookup"><span data-stu-id="3b74f-131">The application passes this information in the message properties, instead of in the message body, so that IoT Hub can route the message to the proper message destination.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="3b74f-132">U kunt de berichteigenschappen om berichten te routeren voor verschillende scenario's, inclusief de verwerking van koude pad, naast het hot pad voorbeeld dat hier wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3b74f-132">You can use message properties to route messages for various scenarios including cold-path processing, in addition to the hot path example shown here.</span></span>

2. <span data-ttu-id="3b74f-133">Sla en sluit het bestand simulated-device\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="3b74f-133">Save and close the simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3b74f-134">Omwille van de eenvoud in deze zelfstudie niet geïmplementeerd voor een beleid voor opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="3b74f-134">For the sake of simplicity, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="3b74f-135">In productiecode moet u een beleid voor opnieuw proberen zoals exponentieel uitstel, zoals voorgesteld in het MSDN-artikel implementeren [afhandeling van tijdelijke fout].</span><span class="sxs-lookup"><span data-stu-id="3b74f-135">In production code, you should implement a retry policy such as exponential backoff, as suggested in the MSDN article [Transient Fault Handling].</span></span>

3. <span data-ttu-id="3b74f-136">Als u de app **simulated-device** wilt maken met behulp van Maven, geeft u de volgende opdracht op in het opdrachtvenster in de map simulated-device:</span><span class="sxs-lookup"><span data-stu-id="3b74f-136">To build the **simulated-device** app using Maven, execute the following command at the command prompt in the simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="add-a-queue-to-your-iot-hub-and-route-messages-to-it"></a><span data-ttu-id="3b74f-137">Een wachtrij toevoegen aan uw IoT hub en route-berichten naar het</span><span class="sxs-lookup"><span data-stu-id="3b74f-137">Add a queue to your IoT hub and route messages to it</span></span>

<span data-ttu-id="3b74f-138">In deze sectie maakt een Service Bus-wachtrij, verbinden met uw IoT-hub en configureren van uw IoT-hub om berichten te verzenden naar de wachtrij op basis van de aanwezigheid van een eigenschap van het bericht.</span><span class="sxs-lookup"><span data-stu-id="3b74f-138">In this section, you create a Service Bus queue, connect it to your IoT hub, and configure your IoT hub to send messages to the queue based on the presence of a property on the message.</span></span> <span data-ttu-id="3b74f-139">Zie voor meer informatie over het verwerken van berichten van Service Bus-wachtrijen [aan de slag met wachtrijen][lnk-sb-queues-java].</span><span class="sxs-lookup"><span data-stu-id="3b74f-139">For more information about how to process messages from Service Bus queues, see [Get started with queues][lnk-sb-queues-java].</span></span>

1. <span data-ttu-id="3b74f-140">Een Service Bus-wachtrij maakt, zoals beschreven in [aan de slag met wachtrijen][lnk-sb-queues-java].</span><span class="sxs-lookup"><span data-stu-id="3b74f-140">Create a Service Bus queue as described in [Get started with queues][lnk-sb-queues-java].</span></span> <span data-ttu-id="3b74f-141">Noteer de naam van de naamruimte en de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="3b74f-141">Make a note of the namespace and queue name.</span></span>

2. <span data-ttu-id="3b74f-142">Open uw IoT-hub in de Azure-portal en klikt u op **eindpunten**.</span><span class="sxs-lookup"><span data-stu-id="3b74f-142">In the Azure portal, open your IoT hub and click **Endpoints**.</span></span>

    ![Eindpunten van IoT-hub][30]

3. <span data-ttu-id="3b74f-144">In de **eindpunten** blade, klikt u op **toevoegen** boven uw wachtrij toevoegen aan uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="3b74f-144">In the **Endpoints** blade, click **Add** at the top to add your queue to your IoT hub.</span></span> <span data-ttu-id="3b74f-145">Naam van het eindpunt **CriticalQueue** en selecteer met de vervolgkeuzelijsten **Service Bus-wachtrij**, de Service Bus-naamruimte waarin de wachtrij zich bevindt en de naam van de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="3b74f-145">Name the endpoint **CriticalQueue** and use the drop-downs to select **Service Bus queue**, the Service Bus namespace in which your queue resides, and the name of your queue.</span></span> <span data-ttu-id="3b74f-146">Wanneer u klaar bent, klikt u op **opslaan** onderaan.</span><span class="sxs-lookup"><span data-stu-id="3b74f-146">When you are done, click **Save** at the bottom.</span></span>

    ![Een eindpunt toevoegen][31]

4. <span data-ttu-id="3b74f-148">Klik nu op **Routes** in uw IoT-Hub.</span><span class="sxs-lookup"><span data-stu-id="3b74f-148">Now click **Routes** in your IoT Hub.</span></span> <span data-ttu-id="3b74f-149">Klik op **toevoegen** boven aan de blade voor het maken van een regel voor doorsturen waarmee berichten worden doorgestuurd naar de wachtrij die u zojuist hebt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="3b74f-149">Click **Add** at the top of the blade to create a routing rule that routes messages to the queue you just added.</span></span> <span data-ttu-id="3b74f-150">Selecteer **DeviceTelemetry** als de bron van gegevens.</span><span class="sxs-lookup"><span data-stu-id="3b74f-150">Select **DeviceTelemetry** as the source of data.</span></span> <span data-ttu-id="3b74f-151">Voer `level="critical"` als de voorwaarde, en kies de wachtrij die u zojuist hebt toegevoegd als een aangepaste eindpunt als de routering eindpunt van de regel.</span><span class="sxs-lookup"><span data-stu-id="3b74f-151">Enter `level="critical"` as the condition, and choose the queue you just added as a custom endpoint as the routing rule endpoint.</span></span> <span data-ttu-id="3b74f-152">Wanneer u klaar bent, klikt u op **opslaan** onderaan.</span><span class="sxs-lookup"><span data-stu-id="3b74f-152">When you are done, click **Save** at the bottom.</span></span>

    ![Toevoegen van een route][32]

    <span data-ttu-id="3b74f-154">Zorg ervoor dat de terugval route is ingesteld op **ON**.</span><span class="sxs-lookup"><span data-stu-id="3b74f-154">Make sure the fallback route is set to **ON**.</span></span> <span data-ttu-id="3b74f-155">Deze instelling is de standaardconfiguratie van een IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="3b74f-155">This setting is the default configuration of an IoT hub.</span></span>

    ![Route voor terugval][33]

## <a name="optional-read-from-the-queue-endpoint"></a><span data-ttu-id="3b74f-157">(Optioneel) Lezen van het eindpunt van de wachtrij</span><span class="sxs-lookup"><span data-stu-id="3b74f-157">(Optional) Read from the queue endpoint</span></span>

<span data-ttu-id="3b74f-158">U kunt eventueel de berichten van het eindpunt van de wachtrij lezen door de instructies in [aan de slag met wachtrijen][lnk-sb-queues-java].</span><span class="sxs-lookup"><span data-stu-id="3b74f-158">You can optionally read the messages from the queue endpoint by following the instructions in [Get started with queues][lnk-sb-queues-java].</span></span> <span data-ttu-id="3b74f-159">Naam van de app **lezen kritieke wachtrij**.</span><span class="sxs-lookup"><span data-stu-id="3b74f-159">Name the app **read-critical-queue**.</span></span>

## <a name="run-the-applications"></a><span data-ttu-id="3b74f-160">De toepassingen uitvoeren</span><span class="sxs-lookup"><span data-stu-id="3b74f-160">Run the applications</span></span>

<span data-ttu-id="3b74f-161">U bent nu klaar om uit te voeren van de drie toepassingen.</span><span class="sxs-lookup"><span data-stu-id="3b74f-161">Now you are ready to run the three applications.</span></span>

1. <span data-ttu-id="3b74f-162">Om uit te voeren de **read-d2c-messages** toepassing in een opdrachtprompt of een shell Navigeer naar de map read-d2c en voer de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="3b74f-162">To run the **read-d2c-messages** application, in a command prompt or shell navigate to the read-d2c folder and execute the following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```

   ![Read-d2c-messages uitvoeren][readd2c]

2. <span data-ttu-id="3b74f-164">Om uit te voeren de **lezen kritieke wachtrij** toepassing in een opdrachtprompt of een shell Navigeer naar de map lezen kritieke wachtrij en de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="3b74f-164">To run the **read-critical-queue** application, in a command prompt or shell navigate to the read-critical-queue folder and execute the following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Alleen kritieke berichten uitgevoerd][readqueue]

3. <span data-ttu-id="3b74f-166">Om uit te voeren de **simulated-device** app in een opdrachtprompt of een shell gaat u naar de map simulated-device en de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="3b74f-166">To run the **simulated-device** app, in a command prompt or shell navigate to the simulated-device folder and execute the following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Simulated-device uitvoeren][simulateddevice]

## <a name="next-steps"></a><span data-ttu-id="3b74f-168">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3b74f-168">Next steps</span></span>

<span data-ttu-id="3b74f-169">In deze zelfstudie hebt u geleerd hoe betrouwbaar apparaat-naar-cloud-berichten verzenden met behulp van de berichtroutering van IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3b74f-169">In this tutorial, you learned how to reliably dispatch device-to-cloud messages by using the message routing functionality of IoT Hub.</span></span>

<span data-ttu-id="3b74f-170">De [het verzenden van berichten van de cloud-naar-apparaat met IoT Hub] [ lnk-c2d] ziet u hoe u berichten verzenden naar uw apparaten vanuit de back-end van uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="3b74f-170">The [How to send cloud-to-device messages with IoT Hub][lnk-c2d] shows you how to send messages to your devices from your solution back end.</span></span>

<span data-ttu-id="3b74f-171">Zie voor voorbeelden van volledige end-to-end-oplossingen die gebruikmaken van IoT Hub [Azure IoT Suite][lnk-suite].</span><span class="sxs-lookup"><span data-stu-id="3b74f-171">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite][lnk-suite].</span></span>

<span data-ttu-id="3b74f-172">Zie voor meer informatie over het ontwikkelen van oplossingen met IoT Hub, de [Ontwikkelaarshandleiding voor IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="3b74f-172">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span></span>

<span data-ttu-id="3b74f-173">Zie voor meer informatie over het routeren van berichten van IoT-Hub, [berichten verzenden en ontvangen met IoT Hub][lnk-devguide-messaging].</span><span class="sxs-lookup"><span data-stu-id="3b74f-173">To learn more about message routing in IoT Hub, see [Send and receive messages with IoT Hub][lnk-devguide-messaging].</span></span>

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

<span data-ttu-id="3b74f-174">[Azure Storage]: https://azure.microsoft.com/documentation/services/storage/</span><span class="sxs-lookup"><span data-stu-id="3b74f-174">[Azure Storage]: https://azure.microsoft.com/documentation/services/storage/</span></span>
<span data-ttu-id="3b74f-175">[Azure Service Bus]: https://azure.microsoft.com/documentation/services/service-bus/</span><span class="sxs-lookup"><span data-stu-id="3b74f-175">[Azure Service Bus]: https://azure.microsoft.com/documentation/services/service-bus/</span></span>

<span data-ttu-id="3b74f-176">[Ontwikkelaarshandleiding voor IoT Hub]: iot-hub-devguide.md</span><span class="sxs-lookup"><span data-stu-id="3b74f-176">[IoT Hub developer guide]: iot-hub-devguide.md</span></span>
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
<span data-ttu-id="3b74f-177">[aan de slag met IoT Hub]: iot-hub-java-java-getstarted.md</span><span class="sxs-lookup"><span data-stu-id="3b74f-177">[Get started with IoT Hub]: iot-hub-java-java-getstarted.md</span></span>
<span data-ttu-id="3b74f-178">[Azure IoT Developer Center]: https://azure.microsoft.com/develop/iot</span><span class="sxs-lookup"><span data-stu-id="3b74f-178">[Azure IoT Developer Center]: https://azure.microsoft.com/develop/iot</span></span>
<span data-ttu-id="3b74f-179">[afhandeling van tijdelijke fout]: https://msdn.microsoft.com/library/hh675232.aspx</span><span class="sxs-lookup"><span data-stu-id="3b74f-179">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh675232.aspx</span></span>

<!-- Links -->
<span data-ttu-id="3b74f-180">[Afhandeling van tijdelijke fout]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span><span class="sxs-lookup"><span data-stu-id="3b74f-180">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span></span>

[lnk-c2d]: iot-hub-java-java-c2d.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
