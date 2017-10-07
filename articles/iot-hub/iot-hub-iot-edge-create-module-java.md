---
title: een Azure IoT Edge-Module met behulp van Java aaaCreate | Microsoft Docs
description: Deze zelfstudie wordt gepresenteerd hoe toowrite een Aanmeldingsprompt gegevens converter module met de meest recente Azure IoT rand Maven pakketten Hallo.
services: iot-hub
author: junyi
manager: timlt
ms.service: iot-hub
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 06/28/2017
ms.author: junyi
ms.openlocfilehash: abb560933d13d133ae9a1da08b503d5735b230e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-iot-edge-module-with-java"></a>Een Azure IoT-Edge-Module maken met behulp van Java

Deze zelfstudie wordt gepresenteerd hoe een een-module voor Azure IoT rand in Java mogelijk maken.

In deze zelfstudie we helpt bij het instellen van de omgeving en hoe toowrite een [uitschakelen](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) gegevens converter module met behulp van de meest recente Azure IoT rand Maven-pakketten Hallo.

## <a name="prerequisites"></a>Vereisten

In deze sectie wordt u uw omgeving voor het ontwikkelen van de module IoT rand instellen. Toepassing tooboth *64-bits Windows* en *64-bits Linux (8 Ubuntu/Debian)* besturingssystemen.

Hallo volgende software is vereist:

* [GIT Client](https://git-scm.com/downloads).
* [**x64** JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
* [Maven](https://maven.apache.org/install.html).

Open een opdrachtregel terminal-venster en kloon Hallo opslagplaats te volgen:

1. `git clone https://github.com/Azure-Samples/iot-edge-samples.git`.
2. `cd iot-edge-samples/java/simulated_ble`

## <a name="overall-architecture"></a>Algehele architectuur

Hello Azure IoT rand platform aanneemt sterk Hallo [Von Neumann architectuur](https://en.wikipedia.org/wiki/Von_Neumann_architecture). Wat betekent dat Hallo volledige rand van Azure IoT-architectuur is een systeem dat invoer verwerkt en produceert uitvoer; en elke afzonderlijke module is ook een klein input-output-subsysteem. In deze zelfstudie stellen we Hallo na twee modules:

1. Een module die u een gesimuleerde ontvangt [uitschakelen](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) signaal en converteert naar een geformatteerde [JSON](https://en.wikipedia.org/wiki/JSON) bericht.
2. Een module die worden afgedrukt Hallo ontvangen [JSON](https://en.wikipedia.org/wiki/JSON) bericht.

Hallo bevat volgende afbeelding Hallo typische end-to-end-gegevensstroom voor dit project:

![Gegevensstroom tussen drie modules](media/iot-hub-iot-edge-create-module/dataflow.png "invoer: gesimuleerde uitschakelen Module. Processor: Converter Module. Uitvoer: Printer Module")

## <a name="understanding-hello-code"></a>Understanding Hallo code

### <a name="maven-project-structure"></a>De structuur van de maven-project

Omdat Azure IoT rand pakketten zijn gebaseerd op Maven, moeten we toocreate een typische Maven projectstructuur, waarin een `pom.xml` bestand.

Hallo POM neemt over van Hallo `com.microsoft.azure.gateway.gateway-module-base` pakket dat alle Hallo afhankelijkheden die nodig is voor een module-project met Hallo runtime binaire bestanden, pad configuratiebestand Hallo gateway en Hallo uitvoeringsgedrag declareert. Dit hoeven we veel tijd en Hallo nodig toowrite elimineren en herschrijven honderden coderegels dan opnieuw.

Moet het bestand pom.xml tooupdate Hallo vereist afhankelijkheden/plugins en Hallo-naam van Hallo configuration file toobe gebruikt door de module, zoals wordt weergegeven in het volgende codefragment Hallo declareert.

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <!-- Inherit from parent -->
  <parent>
    <groupId>com.microsoft.azure.gateway</groupId>
    <artifactId>gateway-module-base</artifactId>
    <version>1.0.1</version>
  </parent>
  
  <groupId>com.microsoft.azure.gateway</groupId>
  <artifactId>ble-converter</artifactId>
  <version>1.0</version>
  <packaging>jar</packaging>

  <!-- Set hello filename of hello Azure IoT Edge configuration located
       under ./src/main/resources/gateway/ which is used in parent -->
  <properties>
    <gw.config.fileName>gw-config.json</gw.config.fileName>
  </properties>

  <!-- Re-declare dependencies used in parent -->
  <dependencies>
    <dependency>
      <groupId>com.microsoft.azure.gateway</groupId>
      <artifactId>gateway-java-binding</artifactId>
    </dependency>
    <dependency>
      <groupId>${dependency.runtime.group}</groupId>
      <artifactId>${dependency.runtime.name}</artifactId>
    </dependency>
  </dependencies>

  <!-- Re-declare plugins used in parent -->
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-dependency-plugin</artifactId>
      </plugin>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-resources-plugin</artifactId>
      </plugin>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-shade-plugin</artifactId>
      </plugin>
      <plugin>
        <groupId>org.codehaus.mojo</groupId>
        <artifactId>exec-maven-plugin</artifactId>
      </plugin>
    </plugins>
  </build>
</project>
```

### <a name="basic-understanding-of-an-azure-iot-edge-module"></a>Basiskennis van een Azure-IoT-Edge-module

U kunt een module voor Azure IoT rand behandelen als een processor van de gegevens waarvan de taak is: invoer ontvangen, verwerken en uitvoer te produceren.

Hallo invoer mogelijk gegevens van hardware (zoals een detectie beweging), een bericht van andere modules of iets anders (zoals een willekeurig getal die regelmatig worden gegenereerd door een timer).

Hallo-uitvoer is vergelijkbaar toohello invoer gebruikt, kan het gedrag van hardware (zoals Hallo knipperende LED), een bericht tooother modules of iets anders (zoals afdrukken toohello console) activeren.

Modules communiceren met elkaar met behulp van `com.microsoft.azure.gateway.messaging.Message` klasse. Hallo **inhoud** van een `Message` is een bytematrix die geschikt is voor elk soort gegevens die u wilt dat vertegenwoordigt. **Eigenschappen** zijn ook beschikbaar in Hallo `Message` en gewoon de toewijzing van een tekenreeks-naar-tekenreeks zijn. U kunt zien **eigenschappen** als Hallo veldnamen in een HTTP-aanvraag of Hallo metagegevens van een bestand.

In de volgorde toodevelop een Edge van Azure IoT-module in Java, moet u een nieuwe moduleklasse die eigenschappen van overneemt toocreate `com.microsoft.azure.gateway.core.GatewayModule` en implementeren van de abstracte methoden Hallo vereist `receive()` en `destroy()`. Op dit moment, u kunt ook tooimplement Hallo optionele `start()` of `create()` ook methoden. Hallo volgende codefragment ziet u hoe het ontwerpen van een module voor Azure IoT-Edge van tooget wordt gestart.

```java
import com.microsoft.azure.gateway.core.Broker;
import com.microsoft.azure.gateway.core.GatewayModule;
import com.microsoft.azure.gateway.messaging.Message;

public class MyEdgeModule extends GatewayModule {
  public MyEdgeModule(long address, Broker broker, String configuration) {
    /* Let hello GatewayModule do hello dirty work of initialization. It's also
       a good time tooparse your own configuration defined in Azure IoT Edge
       configuration file (typically ./src/main/resources/gateway/gw-config.json) */
    super(address, broker, configuration);
  }

  @Override
  public void start() {
    /* Acquire hello resources you need. If you don't
       need any resources, you may omit this method. */
  }

  @Override
  public void destroy() {
    /* It's time toorelease all resources. This method is required. */
  }

  @Override
  public void receive(Message message) {
    /* Logic tooprocess hello input message. This method is required. */
    // ...
    /* Use publish() method toodo hello output. You are
       allowed toopublish your new Message instance. */
    this.publish(message);
  }
}
```

### <a name="converter-module"></a>Converter module

| Invoer                    | Processor                              | Uitvoer                 | Bronbestand            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| Bericht temperatuur-gegevens | Parseren en het maken van een nieuwe JSON-bericht | Structuur JSON-bericht | `ConverterModule.java` |

Dit is een typische Azure IoT Edge-module. De cmdlet accepteert temperatuur berichten van andere modules (een hardware-module of in dit geval onze gesimuleerde uitschakelen module); en vervolgens normaliseert temperatuur het Hallo-bericht in tooa gestructureerd JSON bericht (inclusief voegen Hallo bericht-ID, Hallo-eigenschap van het of we tootrigger Hallo temperatuur waarschuwing moeten enzovoort).

```java
@Override
public void receive(Message message) {
  try {
    JSONObject messageFromBle = new JSONObject(new String(message.getContent()));
    double temperature = messageFromBle.getDouble("temperature");
    Map<String, String> inputProperties = message.getProperties();

    HashMap<String, String> properties = new HashMap<>();
    properties.put("source", inputProperties.get("source"));
    properties.put("macAddress", inputProperties.get("macAddress"));
    properties.put("temperatureAlert", temperature > 30 ? "true" : "false");

    String content = String.format(
        "{ \"deviceId\": \"Intel NUC Gateway\", \"messageId\": %d, \"temperature\": %f }",
        ++this.messageCount, temperature);

    this.publish(new Message(content.getBytes(), properties));
  } catch (Exception ex) {
    ex.printStackTrace();
  }
}
```

### <a name="printer-module"></a>Module printer

| Invoer                          | Processor | Uitvoer                     | Bronbestand          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| Een bericht ontvangen van andere modules | N.v.t.       | Meld u Hallo-bericht tooconsole | `PrinterModule.java` |

Dit is een eenvoudige, zelfverklarend, module dit Hallo ontvangen berichten toohello terminalvenster levert.

```java
@Override
public void receive(Message message) {
  System.out.println(message.toString());
}
```

### <a name="azure-iot-edge-configuration"></a>Azure IoT Edge-configuratie

laatste stap voordat u de modules Hallo Hallo is tooconfigure hello Azure IoT rand en tooestablish Hallo verbindingen tussen modules.

Eerst moet u toodeclare onze Java-laadprogramma (sinds het Azure IoT rand ondersteunt laadprogramma's van verschillende talen) die kan worden verwezen door de `name` in daarna Hallo-secties.

```json
"loaders": [{
  "type": "java",
  "name": "java",
  "configuration": {
    "jvm.options": {
      "library.path": "./"
    }
  }
}]
```

Wanneer we onze laadprogramma's hebt gedeclareerd, moet er ook toodeclare ook onze modules. Te laadprogramma's vergelijkbaar toodeclaring hello, kan ook worden verwezen door hun `name` kenmerk. Als u een module definieert, moeten we toospecify Hallo loader het moet gebruiken (dit moet Hallo een we gedefinieerd vóór zijn) en het Hallo ingangspunt (moet Hallo genormaliseerde klassenaam van onze module zijn) voor elke module. Hallo `simulated_device` is een systeemeigen module die is opgenomen in hello Azure IoT rand core runtime-pakket. U moet altijd opnemen `args` in JSON-bestand zelfs indien deze Hallo `null`.

```json
"modules": [
  {
    "name": "simulated_device",
    "loader": {
      "name": "native",
      "entrypoint": {
        "module.path": "simulated_device"
      }
    },
    "args": {
      "macAddress": "01:02:03:03:02:01",
      "messagePeriod": 500
    }
  },
  {
    "name": "converter",
    "loader": {
      "name": "java",
      "entrypoint": {
        "class.name": "com/microsoft/azure/gateway/ConverterModule",
        "class.path": "./ble-converter-1.0-with-deps.jar"
      }
    },
    "args": null
  },
  {
    "name": "print",
    "loader": {
      "name": "java",
      "entrypoint": {
        "class.name": "com/microsoft/azure/gateway/PrinterModule",
        "class.path": "./ble-converter-1.0-with-deps.jar"
      }
    },
    "args": null
  }
]
```

Aan het einde van de Hallo van Hallo configuratie maken we Hallo verbindingen. Elke verbinding wordt uitgedrukt door `source` en `sink`. Ze moeten beide verwijzen naar een vooraf gedefinieerde module. Hallo-bericht van uitvoer van `source` module doorgestuurd toohello invoer van `sink` module.

```json
"links": [
  {
    "source": "simulated_device",
    "sink": "converter"
  },
  {
    "source": "converter",
    "sink": "print"
  }
]
```

## <a name="running-hello-modules"></a>Hallo-modules uitgevoerd

Gebruik `mvn package` toobuild alles in Hallo `target/` map. `mvn clean package`ook wordt aanbevolen voor een nieuwe build.

Gebruik `mvn exec:exec` toorun hello Azure IoT rand en u rekening moet houden dat Hallo temperatuur gegevens en alle Hallo-eigenschappen afgedrukte toohello-console op een vast tarief zijn.

Als u tooterminate Hallo toepassing wilt, drukt u op `<Enter>` sleutel.

> [!IMPORTANT]
> Het wordt niet aangeraden toouse Ctrl + C tooterminate Hallo rand IoT gateway-toepassing. Als dit Hallo proces tooterminate abnormaal veroorzaken kan.

