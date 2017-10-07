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
# <a name="create-an-azure-iot-edge-module-with-java"></a><span data-ttu-id="ac35e-103">Een Azure IoT-Edge-Module maken met behulp van Java</span><span class="sxs-lookup"><span data-stu-id="ac35e-103">Create an Azure IoT Edge Module with Java</span></span>

<span data-ttu-id="ac35e-104">Deze zelfstudie wordt gepresenteerd hoe een een-module voor Azure IoT rand in Java mogelijk maken.</span><span class="sxs-lookup"><span data-stu-id="ac35e-104">This tutorial showcases how one might build a module for Azure IoT Edge in Java.</span></span>

<span data-ttu-id="ac35e-105">In deze zelfstudie we helpt bij het instellen van de omgeving en hoe toowrite een [uitschakelen](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) gegevens converter module met behulp van de meest recente Azure IoT rand Maven-pakketten Hallo.</span><span class="sxs-lookup"><span data-stu-id="ac35e-105">In this tutorial, we will walk through environment setup and how toowrite a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using hello latest Azure IoT Edge Maven packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ac35e-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ac35e-106">Prerequisites</span></span>

<span data-ttu-id="ac35e-107">In deze sectie wordt u uw omgeving voor het ontwikkelen van de module IoT rand instellen.</span><span class="sxs-lookup"><span data-stu-id="ac35e-107">In this section, you will set up your environment for IoT Edge module development.</span></span> <span data-ttu-id="ac35e-108">Toepassing tooboth *64-bits Windows* en *64-bits Linux (8 Ubuntu/Debian)* besturingssystemen.</span><span class="sxs-lookup"><span data-stu-id="ac35e-108">It applies tooboth *64-bit Windows* and *64-bit Linux (Ubuntu/Debian 8)* operating systems.</span></span>

<span data-ttu-id="ac35e-109">Hallo volgende software is vereist:</span><span class="sxs-lookup"><span data-stu-id="ac35e-109">hello following software is required:</span></span>

* <span data-ttu-id="ac35e-110">[GIT Client](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="ac35e-110">[Git Client](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="ac35e-111">[**x64** JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="ac35e-111">[**x64** JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="ac35e-112">[Maven](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="ac35e-112">[Maven](https://maven.apache.org/install.html).</span></span>

<span data-ttu-id="ac35e-113">Open een opdrachtregel terminal-venster en kloon Hallo opslagplaats te volgen:</span><span class="sxs-lookup"><span data-stu-id="ac35e-113">Open a command-line terminal window and clone hello following repository:</span></span>

1. <span data-ttu-id="ac35e-114">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span><span class="sxs-lookup"><span data-stu-id="ac35e-114">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span></span>
2. `cd iot-edge-samples/java/simulated_ble`

## <a name="overall-architecture"></a><span data-ttu-id="ac35e-115">Algehele architectuur</span><span class="sxs-lookup"><span data-stu-id="ac35e-115">Overall architecture</span></span>

<span data-ttu-id="ac35e-116">Hello Azure IoT rand platform aanneemt sterk Hallo [Von Neumann architectuur](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span><span class="sxs-lookup"><span data-stu-id="ac35e-116">hello Azure IoT Edge platform heavily adopts hello [Von Neumann architecture](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span></span> <span data-ttu-id="ac35e-117">Wat betekent dat Hallo volledige rand van Azure IoT-architectuur is een systeem dat invoer verwerkt en produceert uitvoer; en elke afzonderlijke module is ook een klein input-output-subsysteem.</span><span class="sxs-lookup"><span data-stu-id="ac35e-117">Which means that hello entire Azure IoT Edge architecture is a system which processes input and produces output; and that each individual module is also a tiny input-output subsystem.</span></span> <span data-ttu-id="ac35e-118">In deze zelfstudie stellen we Hallo na twee modules:</span><span class="sxs-lookup"><span data-stu-id="ac35e-118">In this tutorial, we will introduce hello following two modules:</span></span>

1. <span data-ttu-id="ac35e-119">Een module die u een gesimuleerde ontvangt [uitschakelen](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) signaal en converteert naar een geformatteerde [JSON](https://en.wikipedia.org/wiki/JSON) bericht.</span><span class="sxs-lookup"><span data-stu-id="ac35e-119">A module which receives a simulated [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) signal and converts it into a formatted [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>
2. <span data-ttu-id="ac35e-120">Een module die worden afgedrukt Hallo ontvangen [JSON](https://en.wikipedia.org/wiki/JSON) bericht.</span><span class="sxs-lookup"><span data-stu-id="ac35e-120">A module which prints hello received [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>

<span data-ttu-id="ac35e-121">Hallo bevat volgende afbeelding Hallo typische end-to-end-gegevensstroom voor dit project:</span><span class="sxs-lookup"><span data-stu-id="ac35e-121">hello following image displays hello typical end-to-end dataflow for this project:</span></span>

<span data-ttu-id="ac35e-122">![Gegevensstroom tussen drie modules](media/iot-hub-iot-edge-create-module/dataflow.png "invoer: gesimuleerde uitschakelen Module. Processor: Converter Module. Uitvoer: Printer Module")</span><span class="sxs-lookup"><span data-stu-id="ac35e-122">![Dataflow between three modules](media/iot-hub-iot-edge-create-module/dataflow.png "Input: Simulated BLE Module; Processor: Converter Module; Output: Printer Module")</span></span>

## <a name="understanding-hello-code"></a><span data-ttu-id="ac35e-123">Understanding Hallo code</span><span class="sxs-lookup"><span data-stu-id="ac35e-123">Understanding hello code</span></span>

### <a name="maven-project-structure"></a><span data-ttu-id="ac35e-124">De structuur van de maven-project</span><span class="sxs-lookup"><span data-stu-id="ac35e-124">Maven project structure</span></span>

<span data-ttu-id="ac35e-125">Omdat Azure IoT rand pakketten zijn gebaseerd op Maven, moeten we toocreate een typische Maven projectstructuur, waarin een `pom.xml` bestand.</span><span class="sxs-lookup"><span data-stu-id="ac35e-125">Since Azure IoT Edge packages are based on Maven, we need toocreate a typical Maven project structure, which contains a `pom.xml` file.</span></span>

<span data-ttu-id="ac35e-126">Hallo POM neemt over van Hallo `com.microsoft.azure.gateway.gateway-module-base` pakket dat alle Hallo afhankelijkheden die nodig is voor een module-project met Hallo runtime binaire bestanden, pad configuratiebestand Hallo gateway en Hallo uitvoeringsgedrag declareert.</span><span class="sxs-lookup"><span data-stu-id="ac35e-126">hello POM inherits from hello `com.microsoft.azure.gateway.gateway-module-base` package, which declares all of hello dependencies needed by a module project which includes hello runtime binaries, hello gateway configuration file path, and hello execution behavior.</span></span> <span data-ttu-id="ac35e-127">Dit hoeven we veel tijd en Hallo nodig toowrite elimineren en herschrijven honderden coderegels dan opnieuw.</span><span class="sxs-lookup"><span data-stu-id="ac35e-127">This saves us lots of time and eliminate hello need toowrite and rewrite hundreds of lines of code over and over again.</span></span>

<span data-ttu-id="ac35e-128">Moet het bestand pom.xml tooupdate Hallo vereist afhankelijkheden/plugins en Hallo-naam van Hallo configuration file toobe gebruikt door de module, zoals wordt weergegeven in het volgende codefragment Hallo declareert.</span><span class="sxs-lookup"><span data-stu-id="ac35e-128">We need tooupdate the pom.xml file by declaring hello required dependencies/plugins and hello name of hello configuration file toobe used by our module as shown in hello following code snippet.</span></span>

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

### <a name="basic-understanding-of-an-azure-iot-edge-module"></a><span data-ttu-id="ac35e-129">Basiskennis van een Azure-IoT-Edge-module</span><span class="sxs-lookup"><span data-stu-id="ac35e-129">Basic understanding of an Azure IoT Edge module</span></span>

<span data-ttu-id="ac35e-130">U kunt een module voor Azure IoT rand behandelen als een processor van de gegevens waarvan de taak is: invoer ontvangen, verwerken en uitvoer te produceren.</span><span class="sxs-lookup"><span data-stu-id="ac35e-130">You can treat an Azure IoT Edge module as a data processor whose job is to: receive input, process it, and produce output.</span></span>

<span data-ttu-id="ac35e-131">Hallo invoer mogelijk gegevens van hardware (zoals een detectie beweging), een bericht van andere modules of iets anders (zoals een willekeurig getal die regelmatig worden gegenereerd door een timer).</span><span class="sxs-lookup"><span data-stu-id="ac35e-131">hello input might be data from hardware (like a motion detector), a message from other modules, or anything else (like a random number generated periodically by a timer).</span></span>

<span data-ttu-id="ac35e-132">Hallo-uitvoer is vergelijkbaar toohello invoer gebruikt, kan het gedrag van hardware (zoals Hallo knipperende LED), een bericht tooother modules of iets anders (zoals afdrukken toohello console) activeren.</span><span class="sxs-lookup"><span data-stu-id="ac35e-132">hello output is similar toohello input, it could trigger hardware behavior (like hello blinking LED), a message tooother modules, or anything else (like printing toohello console).</span></span>

<span data-ttu-id="ac35e-133">Modules communiceren met elkaar met behulp van `com.microsoft.azure.gateway.messaging.Message` klasse.</span><span class="sxs-lookup"><span data-stu-id="ac35e-133">Modules communicate with each other using `com.microsoft.azure.gateway.messaging.Message` class.</span></span> <span data-ttu-id="ac35e-134">Hallo **inhoud** van een `Message` is een bytematrix die geschikt is voor elk soort gegevens die u wilt dat vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="ac35e-134">hello **Content** of a `Message` is a byte array which is capable of representing any kind of data you like.</span></span> <span data-ttu-id="ac35e-135">**Eigenschappen** zijn ook beschikbaar in Hallo `Message` en gewoon de toewijzing van een tekenreeks-naar-tekenreeks zijn.</span><span class="sxs-lookup"><span data-stu-id="ac35e-135">**Properties** are also available in hello `Message` and are simply a string-to-string mapping.</span></span> <span data-ttu-id="ac35e-136">U kunt zien **eigenschappen** als Hallo veldnamen in een HTTP-aanvraag of Hallo metagegevens van een bestand.</span><span class="sxs-lookup"><span data-stu-id="ac35e-136">You may think of **Properties** as hello headers in an HTTP request, or hello metadata of a file.</span></span>

<span data-ttu-id="ac35e-137">In de volgorde toodevelop een Edge van Azure IoT-module in Java, moet u een nieuwe moduleklasse die eigenschappen van overneemt toocreate `com.microsoft.azure.gateway.core.GatewayModule` en implementeren van de abstracte methoden Hallo vereist `receive()` en `destroy()`.</span><span class="sxs-lookup"><span data-stu-id="ac35e-137">In order toodevelop an Azure IoT Edge module in Java, you need toocreate a new module class which inherits from `com.microsoft.azure.gateway.core.GatewayModule` and implement hello required abstract methods `receive()` and `destroy()`.</span></span> <span data-ttu-id="ac35e-138">Op dit moment, u kunt ook tooimplement Hallo optionele `start()` of `create()` ook methoden.</span><span class="sxs-lookup"><span data-stu-id="ac35e-138">At this point, you may also choose tooimplement hello optional `start()` or `create()` methods as well.</span></span> <span data-ttu-id="ac35e-139">Hallo volgende codefragment ziet u hoe het ontwerpen van een module voor Azure IoT-Edge van tooget wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="ac35e-139">hello following code snippet shows you how tooget started authoring an Azure IoT Edge module.</span></span>

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

### <a name="converter-module"></a><span data-ttu-id="ac35e-140">Converter module</span><span class="sxs-lookup"><span data-stu-id="ac35e-140">Converter module</span></span>

| <span data-ttu-id="ac35e-141">Invoer</span><span class="sxs-lookup"><span data-stu-id="ac35e-141">Input</span></span>                    | <span data-ttu-id="ac35e-142">Processor</span><span class="sxs-lookup"><span data-stu-id="ac35e-142">Processor</span></span>                              | <span data-ttu-id="ac35e-143">Uitvoer</span><span class="sxs-lookup"><span data-stu-id="ac35e-143">Output</span></span>                 | <span data-ttu-id="ac35e-144">Bronbestand</span><span class="sxs-lookup"><span data-stu-id="ac35e-144">Source File</span></span>            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| <span data-ttu-id="ac35e-145">Bericht temperatuur-gegevens</span><span class="sxs-lookup"><span data-stu-id="ac35e-145">Temperature data message</span></span> | <span data-ttu-id="ac35e-146">Parseren en het maken van een nieuwe JSON-bericht</span><span class="sxs-lookup"><span data-stu-id="ac35e-146">Parse and construct a new JSON message</span></span> | <span data-ttu-id="ac35e-147">Structuur JSON-bericht</span><span class="sxs-lookup"><span data-stu-id="ac35e-147">Structure JSON message</span></span> | `ConverterModule.java` |

<span data-ttu-id="ac35e-148">Dit is een typische Azure IoT Edge-module.</span><span class="sxs-lookup"><span data-stu-id="ac35e-148">This module is a typical Azure IoT Edge module.</span></span> <span data-ttu-id="ac35e-149">De cmdlet accepteert temperatuur berichten van andere modules (een hardware-module of in dit geval onze gesimuleerde uitschakelen module); en vervolgens normaliseert temperatuur het Hallo-bericht in tooa gestructureerd JSON bericht (inclusief voegen Hallo bericht-ID, Hallo-eigenschap van het of we tootrigger Hallo temperatuur waarschuwing moeten enzovoort).</span><span class="sxs-lookup"><span data-stu-id="ac35e-149">It accepts temperature messages from other modules (a hardware module, or in this case our simulated BLE module); and then normalizes hello temperature message in tooa structured JSON message (including appending hello message ID, setting hello property of whether we need tootrigger hello temperature alert, and so on).</span></span>

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

### <a name="printer-module"></a><span data-ttu-id="ac35e-150">Module printer</span><span class="sxs-lookup"><span data-stu-id="ac35e-150">Printer module</span></span>

| <span data-ttu-id="ac35e-151">Invoer</span><span class="sxs-lookup"><span data-stu-id="ac35e-151">Input</span></span>                          | <span data-ttu-id="ac35e-152">Processor</span><span class="sxs-lookup"><span data-stu-id="ac35e-152">Processor</span></span> | <span data-ttu-id="ac35e-153">Uitvoer</span><span class="sxs-lookup"><span data-stu-id="ac35e-153">Output</span></span>                     | <span data-ttu-id="ac35e-154">Bronbestand</span><span class="sxs-lookup"><span data-stu-id="ac35e-154">Source File</span></span>          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| <span data-ttu-id="ac35e-155">Een bericht ontvangen van andere modules</span><span class="sxs-lookup"><span data-stu-id="ac35e-155">Any message from other modules</span></span> | <span data-ttu-id="ac35e-156">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="ac35e-156">N/A</span></span>       | <span data-ttu-id="ac35e-157">Meld u Hallo-bericht tooconsole</span><span class="sxs-lookup"><span data-stu-id="ac35e-157">Log hello message tooconsole</span></span> | `PrinterModule.java` |

<span data-ttu-id="ac35e-158">Dit is een eenvoudige, zelfverklarend, module dit Hallo ontvangen berichten toohello terminalvenster levert.</span><span class="sxs-lookup"><span data-stu-id="ac35e-158">This is a simple, self-explanatory, module which outputs hello received messages toohello terminal window.</span></span>

```java
@Override
public void receive(Message message) {
  System.out.println(message.toString());
}
```

### <a name="azure-iot-edge-configuration"></a><span data-ttu-id="ac35e-159">Azure IoT Edge-configuratie</span><span class="sxs-lookup"><span data-stu-id="ac35e-159">Azure IoT Edge configuration</span></span>

<span data-ttu-id="ac35e-160">laatste stap voordat u de modules Hallo Hallo is tooconfigure hello Azure IoT rand en tooestablish Hallo verbindingen tussen modules.</span><span class="sxs-lookup"><span data-stu-id="ac35e-160">hello final step before running hello modules is tooconfigure hello Azure IoT Edge and tooestablish hello connections between modules.</span></span>

<span data-ttu-id="ac35e-161">Eerst moet u toodeclare onze Java-laadprogramma (sinds het Azure IoT rand ondersteunt laadprogramma's van verschillende talen) die kan worden verwezen door de `name` in daarna Hallo-secties.</span><span class="sxs-lookup"><span data-stu-id="ac35e-161">First we need toodeclare our Java loader (since Azure IoT Edge supports loaders of different languages) which could be referenced by its `name` in hello sections afterward.</span></span>

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

<span data-ttu-id="ac35e-162">Wanneer we onze laadprogramma's hebt gedeclareerd, moet er ook toodeclare ook onze modules.</span><span class="sxs-lookup"><span data-stu-id="ac35e-162">Once we have declared our loaders, we will also need toodeclare our modules as well.</span></span> <span data-ttu-id="ac35e-163">Te laadprogramma's vergelijkbaar toodeclaring hello, kan ook worden verwezen door hun `name` kenmerk.</span><span class="sxs-lookup"><span data-stu-id="ac35e-163">Similar toodeclaring hello loaders, they can also be referenced by their `name` attribute.</span></span> <span data-ttu-id="ac35e-164">Als u een module definieert, moeten we toospecify Hallo loader het moet gebruiken (dit moet Hallo een we gedefinieerd vóór zijn) en het Hallo ingangspunt (moet Hallo genormaliseerde klassenaam van onze module zijn) voor elke module.</span><span class="sxs-lookup"><span data-stu-id="ac35e-164">When declaring a module, we need toospecify hello loader it should use (which should be hello one we defined before) and hello entry-point (should be hello normalized class name of our module) for each module.</span></span> <span data-ttu-id="ac35e-165">Hallo `simulated_device` is een systeemeigen module die is opgenomen in hello Azure IoT rand core runtime-pakket.</span><span class="sxs-lookup"><span data-stu-id="ac35e-165">hello `simulated_device` module is a native module which is included in hello Azure IoT Edge core runtime package.</span></span> <span data-ttu-id="ac35e-166">U moet altijd opnemen `args` in JSON-bestand zelfs indien deze Hallo `null`.</span><span class="sxs-lookup"><span data-stu-id="ac35e-166">You should always include `args` in hello JSON file even if it is `null`.</span></span>

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

<span data-ttu-id="ac35e-167">Aan het einde van de Hallo van Hallo configuratie maken we Hallo verbindingen.</span><span class="sxs-lookup"><span data-stu-id="ac35e-167">At hello end of hello configuration, we establish hello connections.</span></span> <span data-ttu-id="ac35e-168">Elke verbinding wordt uitgedrukt door `source` en `sink`.</span><span class="sxs-lookup"><span data-stu-id="ac35e-168">Each connection is expressed by `source` and `sink`.</span></span> <span data-ttu-id="ac35e-169">Ze moeten beide verwijzen naar een vooraf gedefinieerde module.</span><span class="sxs-lookup"><span data-stu-id="ac35e-169">They should both reference a pre-defined module.</span></span> <span data-ttu-id="ac35e-170">Hallo-bericht van uitvoer van `source` module doorgestuurd toohello invoer van `sink` module.</span><span class="sxs-lookup"><span data-stu-id="ac35e-170">hello output message of `source` module will be forwarded toohello input of `sink` module.</span></span>

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

## <a name="running-hello-modules"></a><span data-ttu-id="ac35e-171">Hallo-modules uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="ac35e-171">Running hello modules</span></span>

<span data-ttu-id="ac35e-172">Gebruik `mvn package` toobuild alles in Hallo `target/` map.</span><span class="sxs-lookup"><span data-stu-id="ac35e-172">Use `mvn package` toobuild everything into hello `target/` folder.</span></span> <span data-ttu-id="ac35e-173">`mvn clean package`ook wordt aanbevolen voor een nieuwe build.</span><span class="sxs-lookup"><span data-stu-id="ac35e-173">`mvn clean package` is also recommended for a clean build.</span></span>

<span data-ttu-id="ac35e-174">Gebruik `mvn exec:exec` toorun hello Azure IoT rand en u rekening moet houden dat Hallo temperatuur gegevens en alle Hallo-eigenschappen afgedrukte toohello-console op een vast tarief zijn.</span><span class="sxs-lookup"><span data-stu-id="ac35e-174">Use `mvn exec:exec` toorun hello Azure IoT Edge and you should observe that hello temperature data and all hello properties are printed toohello console at a fixed rate.</span></span>

<span data-ttu-id="ac35e-175">Als u tooterminate Hallo toepassing wilt, drukt u op `<Enter>` sleutel.</span><span class="sxs-lookup"><span data-stu-id="ac35e-175">If you want tooterminate hello application, press `<Enter>` key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ac35e-176">Het wordt niet aangeraden toouse Ctrl + C tooterminate Hallo rand IoT gateway-toepassing.</span><span class="sxs-lookup"><span data-stu-id="ac35e-176">It is not recommended toouse Ctrl + C tooterminate hello IoT Edge gateway application.</span></span> <span data-ttu-id="ac35e-177">Als dit Hallo proces tooterminate abnormaal veroorzaken kan.</span><span class="sxs-lookup"><span data-stu-id="ac35e-177">As this may cause hello process tooterminate abnormally.</span></span>

