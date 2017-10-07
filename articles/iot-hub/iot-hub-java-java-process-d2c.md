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
# <a name="process-iot-hub-device-to-cloud-messages-java"></a>Verwerken van Iothub apparaat-naar-cloud-berichten (Java)

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

Azure IoT Hub is een volledig beheerde service waarmee betrouwbare en veilige tweerichtingscommunicatie tussen miljoenen apparaten en een oplossing voor back-end. Andere zelfstudies ([aan de slag met IoT Hub] en [cloud naar apparaat verzenden met IoT Hub][lnk-c2d]) ziet u hoe toouse Hallo basic apparaat-naar-cloud- en cloud-naar-apparaat Messaging-functionaliteit van IoT Hub.

Deze zelfstudie bouwt voort op Hallo-code die wordt weergegeven in Hallo [aan de slag met IoT Hub] zelfstudie en toont u hoe toouse routering tooprocess apparaat-naar-cloud-berichten in een schaalbare manier bericht. Hallo-zelfstudie ziet u hoe tooprocess berichten waarvoor onmiddellijke actie van de oplossing Hallo back-end. Een apparaat kan bijvoorbeeld een waarschuwing weergegeven dat activeert een ticket in een CRM-systeem invoegen verzenden. Gegevenspunt berichten feed daarentegen alleen in een analyse-engine. Telemetrie van de temperatuur van een apparaat dat is opgeslagen voor latere analyse toobe is bijvoorbeeld een gegevenspunt bericht.

Aan het einde van de Hallo van deze zelfstudie, moet u drie Java-apps die console uitvoeren:

* **simulated-device**, een aangepaste versie van het Hallo-app gemaakt in Hallo [aan de slag met IoT Hub] zelfstudie verzendt gegevenspunt apparaat-naar-cloud-berichten per seconde en interactieve apparaat-naar-cloud met berichten voor elke 10 seconden. Deze app gebruikt Hallo AMQP-protocol toocommunicate met IoT Hub.
* **Read-d2c-messages** Hallo telemetrie verzonden door de app op uw apparaat weergegeven.
* **alleen kritieke wachtrij** ongedaan kritieke Hallo-berichten van Hallo Service Bus-wachtrij gekoppeld toohello IoT-hub in de wachtrij geplaatst.

> [!NOTE]
> IoT Hub heeft ondersteuning voor veel apparaatplatforms en talen, waaronder C, Java en JavaScript SDK. Voor instructies over hoe tooreplace apparaat Hallo in deze zelfstudie met een fysiek apparaat en hoe tooconnect apparaten tooan IoT Hub Hallo zien [Azure IoT Developer Center].

toocomplete in deze zelfstudie, moet u hello te volgen:

* Een volledige werkende versie van Hallo [aan de slag met IoT Hub] zelfstudie.
* meest recente Hallo [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* Een actief Azure-account. (Als u geen account hebt, kunt u een [gratis account] [lnk-free-trial] binnen een paar minuten.)

Er is enige basiskennis van [Azure Storage] en [Azure Service Bus].

## <a name="send-interactive-messages-from-a-device-app"></a>Interactieve berichten verzenden vanuit een apparaat-app
In deze sectie maakt u Hallo apparaattoepassing u hebt gemaakt in Hallo wijzigen [aan de slag met IoT Hub] zelfstudie toooccasionally berichten verzenden die direct verwerking vereist.

1. Gebruik een editor tooopen hello simulated-device\src\main\java\com\mycompany\app\App.java tekstbestand. Dit bestand bevat de code voor Hallo Hallo **simulated-device** app die u hebt gemaakt in Hallo [aan de slag met IoT Hub] zelfstudie.

2. Vervang Hallo **MessageSender** klasse Hello code te volgen:

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
   
    Met deze methode wordt willekeurig Hallo eigenschap `"level": "critical"` toomessages verzonden door het Hallo apparaat simuleert een bericht dat directe actie is vereist door Hallo toepassing back-end. Hallo-toepassing geeft deze informatie in de eigenschappen van Hallo-bericht, in plaats van in de hoofdtekst van Hallo-bericht, zodat deze IoT-Hub Hallo-bericht toohello juiste berichtenbestemming versturen kunt.
   
   > [!NOTE]
   > U kunt bericht eigenschappen tooroute berichten gebruiken voor verschillende scenario's, met inbegrip van koude pad verwerken bovendien toohello hot pad voorbeeld hier weergegeven.

2. Opslaan en sluiten van de bestand simulated-device\src\main\java\com\mycompany\app\App.java Hallo.

    > [!NOTE]
    > Deze zelfstudie implementeert voor Hallo mogelijk te houden van eenvoud, niet een beleid voor opnieuw proberen. In productiecode moet u een beleid voor opnieuw proberen zoals exponentieel uitstel, zoals voorgesteld in de MSDN-artikel Hallo implementeren [afhandeling van tijdelijke fout].

3. Hallo toobuild **simulated-device** app met behulp van Maven, uitvoeren van de volgende opdracht achter de opdrachtprompt Hallo in de map simulated-device Hallo Hallo:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="add-a-queue-tooyour-iot-hub-and-route-messages-tooit"></a>IoT een tooyour wachtrij hub en route u het tooit berichten toevoegen

In deze sectie maakt een Service Bus-wachtrij, verbindt u deze tooyour IoT-hub en configureren van uw IoT hub toosend berichten toohello wachtrij op basis van Hallo aanwezigheid van een eigenschap van het Hallo-bericht. Zie voor meer informatie over hoe tooprocess van van Service Bus-wachtrijen berichten [aan de slag met wachtrijen][lnk-sb-queues-java].

1. Een Service Bus-wachtrij maakt, zoals beschreven in [aan de slag met wachtrijen][lnk-sb-queues-java]. Maak een notitie van Hallo naamruimte en de wachtrij.

2. In Azure-portal hello, opent u uw IoT-hub en klik op **eindpunten**.

    ![Eindpunten van IoT-hub][30]

3. In Hallo **eindpunten** blade, klikt u op **toevoegen** op Hallo bovenste tooadd uw wachtrij tooyour IoT-hub. Naam Hallo eindpunt **CriticalQueue** en gebruik Hallo-keuzelijsten tooselect **Service Bus-wachtrij**Hallo Service Bus-naamruimte waarin de wachtrij zich bevindt en de naam van uw wachtrij Hallo. Wanneer u klaar bent, klikt u op **opslaan** Hallo onderaan.

    ![Een eindpunt toevoegen][31]

4. Klik nu op **Routes** in uw IoT-Hub. Klik op **toevoegen** bovenaan Hallo Hallo blade toocreate een regel voor doorsturen die routeert berichten toohello wachtrij u zojuist hebt toegevoegd. Selecteer **DeviceTelemetry** als Hallo gegevensbron. Voer `level="critical"` als Hallo voorwaarde, en kies Hallo wachtrij die u zojuist hebt toegevoegd als een aangepaste eindpunt als Hallo regel eindpunt routering. Wanneer u klaar bent, klikt u op **opslaan** Hallo onderaan.

    ![Toevoegen van een route][32]

    Zorg ervoor dat Hallo terugval route is ingesteld, te**ON**. Deze instelling is de standaardconfiguratie Hallo van een IoT-hub.

    ![Route voor terugval][33]

## <a name="optional-read-from-hello-queue-endpoint"></a>(Optioneel) Lezen van Hallo wachtrij eindpunt

U kunt eventueel Hallo-berichten lezen van Hallo wachtrij eindpunt door het Hallo-instructies in [aan de slag met wachtrijen][lnk-sb-queues-java]. Naam Hallo app **lezen kritieke wachtrij**.

## <a name="run-hello-applications"></a>Hallo-toepassingen uitvoeren

U bent nu klaar toorun Hallo drie toepassingen.

1. Hallo toorun **read-d2c-messages** toepassing in een opdrachtprompt of een shell toohello read-d2c-map te navigeren en Hallo volgende opdracht uitvoeren:

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```

   ![Read-d2c-messages uitvoeren][readd2c]

2. Hallo toorun **lezen kritieke wachtrij** toepassing in een opdrachtprompt of een shell toohello lezen kritieke wachtrij map te navigeren en Hallo volgende opdracht uitvoeren:

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Alleen kritieke berichten uitgevoerd][readqueue]

3. Hallo toorun **simulated-device** app in een opdrachtprompt of een shell gaat u de map simulated-device toohello en Hallo volgende opdracht uitvoeren:

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Simulated-device uitvoeren][simulateddevice]

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie hebt u geleerd hoe tooreliably apparaat-naar-cloud-berichten verzenden met behulp van Hallo-bericht routeringsfunctionaliteit van IoT Hub.

Hallo [hoe toosend cloud-naar-apparaat met IoT Hub berichten] [ lnk-c2d] ziet u hoe toosend tooyour apparaten uit de back-end van uw oplossing berichten.

Voorbeelden van volledige end-to-end-oplossingen die gebruikmaken van IoT Hub toosee Zie [Azure IoT Suite][lnk-suite].

toolearn meer informatie over het ontwikkelen van oplossingen met IoT Hub, Zie Hallo [Ontwikkelaarshandleiding voor IoT Hub].

Zie toolearn meer informatie over het routeren van berichten van IoT-Hub [berichten verzenden en ontvangen met IoT Hub][lnk-devguide-messaging].

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
