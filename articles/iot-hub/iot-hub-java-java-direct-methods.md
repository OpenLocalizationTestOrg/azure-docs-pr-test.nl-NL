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
# <a name="use-direct-methods-java"></a>Directe methoden (Java) gebruiken

[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

In deze zelfstudie maakt maken u twee console Java-apps:

* **Invoke-direct-method**, een Java-back-end-app die een methode wordt aangeroepen in de gesimuleerde apparaattoepassing Hallo en antwoord Hallo weergeeft.
* **simulated-device**, een Java-app die een apparaat verbinding te maken tooyour iothub met Hallo apparaat-id hebt u simuleert. Deze app reageert toohello direct worden aangeroepen vanuit de back-end Hallo.

> [!NOTE]
> Zie voor informatie over Hallo SDK's die u toobuild toepassingen toorun op apparaten en de back-end van uw oplossing gebruiken kunt [Azure IoT SDK's][lnk-hub-sdks].

toocomplete deze zelfstudie hebt u nodig:

* Java SE 8. <br/> [Uw ontwikkelingsomgeving voorbereiden] [ lnk-dev-setup] wordt beschreven hoe tooinstall Java voor deze zelfstudie op Windows of Linux.
* Maven 3.  <br/> [Uw ontwikkelingsomgeving voorbereiden] [ lnk-dev-setup] wordt beschreven hoe tooinstall [Maven] [ lnk-maven] voor deze zelfstudie op Windows of Linux.
* [Node.js-versie 0.10.0 of hoger](http://nodejs.org).

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>Een gesimuleerde apparaattoepassing maken

In deze sectie maakt u een Java-consoletoepassing die tooa methode aangeroepen door Hallo oplossing terug end reageert.

1. Maak een lege map genaamd iot-java-direct-methode.

1. Maak een Maven-project aangeroepen in Hallo iot-java-direct-method **simulated-device** met behulp van de volgende opdracht achter de opdrachtprompt Hallo. Hallo na de opdracht is een enkele, lange opdracht:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. Ga bij de opdrachtprompt de map simulated-device toohello.

1. Met een teksteditor Hallo pom.xml-bestand openen in de map simulated-device Hallo en toevoegen van Hallo afhankelijkheden toohello na **afhankelijkheden** knooppunt. Deze afhankelijkheid kunt u toouse Hallo iot-apparaat-client-pakket in uw app toocommunicate met uw IoT-hub:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > U kunt controleren op de meest recente versie van Hallo **iot-apparaat-client** met [Maven search][lnk-maven-device-search].

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

1. Opslaan en sluiten Hallo pom.xml-bestand.

1. Met een teksteditor Hallo simulated-device\src\main\java\com\mycompany\app\App.java bestand openen.

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
    private static String deviceId = "myDeviceId";
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    In dit voorbeeld-app gebruikt Hallo **protocol** variabele bij het instantiëren van een **DeviceClient** object. Op dit moment rechtstreeks toouse methoden u Hallo MQTT protocol moet gebruiken.

1. tooreturn een status code tooyour iothub, voeg Hallo volgende geneste klasse toohello **App** klasse:

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded toodevice method operation with status " + status.name());
      }
    }
    ```

1. toohandle hello directe methode aanroepen van Hallo back-end oplossing, voeg Hallo volgende geneste klasse toohello **App** klasse:

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

1. toocreate een **DeviceClient** en luisteren naar directe methode aanroepen, het toevoegen van een **belangrijkste** methode toohello **App** klasse:

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

1. Opslaan en sluiten van de bestand simulated-device\src\main\java\com\mycompany\app\App.java Hallo

1. Hallo bouwen **simulated-device** app en eventuele fouten te corrigeren. Ga bij de opdrachtprompt de map simulated-device toohello en Voer Hallo volgende opdracht:

    `mvn clean package -DskipTests`

## <a name="call-a-direct-method-on-a-device"></a>Een directe methode is aangeroepen voor een apparaat

In deze sectie maakt maken u een Java-consoletoepassing die een directe methode wordt aangeroepen en wordt vervolgens weergegeven antwoord Hallo. Deze consoletoepassing verbindt tooyour IoT Hub tooinvoke Hallo directe methode.

1. Maak een Maven-project aangeroepen in Hallo iot-java-direct-method **aanroepen directe methode** met behulp van de volgende opdracht achter de opdrachtprompt Hallo. Hallo na de opdracht is een enkele, lange opdracht:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=invoke-direct-method -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. Navigeer toohello aanroepen directe methode map bij de opdrachtprompt.

1. Met een teksteditor, open Hallo pom.xml-bestand in Hallo aanroepen directe methode map en Hallo afhankelijkheid toohello na toevoegen **afhankelijkheden** knooppunt. Deze afhankelijkheid kunt u toouse Hallo iot-service-client-pakket in uw app toocommunicate met uw IoT-hub:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > U kunt controleren op de meest recente versie van Hallo **iot-service-client** met [Maven search][lnk-maven-service-search].

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

1. Opslaan en sluiten Hallo pom.xml-bestand.

1. Met een teksteditor Hallo invoke-direct-method\src\main\java\com\mycompany\app\App.java bestand openen.

1. Voeg de volgende Hallo **importeren** instructies toohello bestand:

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceMethod;
    import com.microsoft.azure.sdk.iot.service.devicetwin.MethodResult;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.concurrent.TimeUnit;
    ```

1. Hallo klasseniveau variabelen toohello na toevoegen **App** klasse. Vervang `{youriothubconnectionstring}` met uw IoT hub-verbindingsreeks die u hebt genoteerd in Hallo *een IoT Hub maken* sectie:

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String methodName = "writeLine";
    public static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    public static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    public static final String payload = "a line toobe written";
    ```

1. tooinvoke Hallo methode op Hallo gesimuleerde apparaat toevoegen Hallo na code toohello **belangrijkste** methode:

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

1. Opslaan en sluiten Hallo invoke-direct-method\src\main\java\com\mycompany\app\App.java bestand

1. Hallo bouwen **aanroepen directe methode** app en eventuele fouten te corrigeren. Navigeer toohello aanroepen directe methode map en Voer Hallo volgende opdracht achter de opdrachtprompt:

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a>Hallo-apps uitvoeren

U bent nu klaar toorun Hallo console apps.

1. Voer bij een opdrachtprompt in de map simulated-device Hallo Hallo opdracht toobegin luisteren naar methodeaanroepen van uw IoT-hub te volgen:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![IoT Hub voor Java gesimuleerd apparaat app toolisten voor directe methodeaanroepen][8]

1. Bij een opdrachtprompt in Hallo aanroepen directe methode map Hallo opdracht toocall na een methode uitvoeren op uw gesimuleerde apparaat uit uw IoT-hub:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![IoT Hub voor Java service app toocall een directe methode][7]

1. Hallo gesimuleerd apparaat reageert toohello directe methode aanroepen:

    ![De gesimuleerde apparaattoepassing IoT-Hub voor Java reageert toohello directe methode-aanroep][9]

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie maakt u een nieuwe iothub geconfigureerd in hello Azure-portal en vervolgens een apparaat-id in de id-register Hallo iothub hebt gemaakt. U hebt deze apparaat-id tooenable Hallo gesimuleerd apparaat app tooreact toomethods aangeroepen door Hallo cloud gebruikt. Hebt u ook een app die wordt aangeroepen methoden op Hallo apparaat en geeft weer Hallo-antwoord van Hallo-apparaat hebt gemaakt.

tooexplore andere IoT-scenario's, Zie [plannen van taken op meerdere apparaten][lnk-devguide-jobs].

toolearn hoe tooextend uw IoT-oplossing en schema-methode aanroepen op meerdere apparaten, raadpleegt u Hallo [planning en broadcast taken] [ lnk-tutorial-jobs] zelfstudie.

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
