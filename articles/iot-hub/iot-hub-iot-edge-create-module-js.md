---
title: Een Azure IoT-Edge-Module maken met behulp van Node.js | Microsoft Docs
description: Deze zelfstudie gepresenteerd het schrijven van een Aanmeldingsprompt gegevens converter module met behulp van de meest recente Azure IoT rand NPM pakketten en Yeoman generator.
services: iot-hub
author: sushi
manager: timlt
ms.service: iot-hub
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: js
ms.topic: article
ms.date: 06/28/2017
ms.author: sushi
ms.openlocfilehash: ba466f47e157d805600c41fa3d84ed5a0363969c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-azure-iot-edge-module-with-nodejs"></a><span data-ttu-id="f92a0-103">Een Azure IoT-Edge-Module maken met behulp van Node.js</span><span class="sxs-lookup"><span data-stu-id="f92a0-103">Create an Azure IoT Edge Module with Node.js</span></span>

<span data-ttu-id="f92a0-104">Deze zelfstudie maken van een module voor Azure IoT rand in de JS gepresenteerd.</span><span class="sxs-lookup"><span data-stu-id="f92a0-104">This tutorial showcases how to create a module for Azure IoT Edge in JS.</span></span>

<span data-ttu-id="f92a0-105">In deze zelfstudie we doorlopen omgeving in te stellen en het schrijven van een [uitschakelen](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) gegevens converter module met behulp van de meest recente Azure IoT rand NPM-pakketten.</span><span class="sxs-lookup"><span data-stu-id="f92a0-105">In this tutorial, we walk through environment setup and how to write a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using the latest Azure IoT Edge NPM packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f92a0-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f92a0-106">Prerequisites</span></span>

<span data-ttu-id="f92a0-107">In deze sectie, moet u uw omgeving voor het ontwikkelen van de module IoT rand instellen.</span><span class="sxs-lookup"><span data-stu-id="f92a0-107">In this section, you set up your environment for IoT Edge module development.</span></span> <span data-ttu-id="f92a0-108">Van toepassing op beide *64-bits Windows* en *64-bits Linux (Ubuntu) 14 +* besturingssystemen.</span><span class="sxs-lookup"><span data-stu-id="f92a0-108">It applies to both *64-bit Windows* and *64-bit Linux (Ubuntu 14+)* operating systems.</span></span>

<span data-ttu-id="f92a0-109">De volgende software is vereist:</span><span class="sxs-lookup"><span data-stu-id="f92a0-109">The following software is required:</span></span>
* <span data-ttu-id="f92a0-110">[GIT Client](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="f92a0-110">[Git Client](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="f92a0-111">[Knooppunt TNS](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="f92a0-111">[Node LTS](https://nodejs.org).</span></span>
* <span data-ttu-id="f92a0-112">`npm install -g yo`.</span><span class="sxs-lookup"><span data-stu-id="f92a0-112">`npm install -g yo`.</span></span>
* `npm install -g generator-az-iot-gw-module`

## <a name="architecture"></a><span data-ttu-id="f92a0-113">Architectuur</span><span class="sxs-lookup"><span data-stu-id="f92a0-113">Architecture</span></span>

<span data-ttu-id="f92a0-114">Het platform Azure IoT rand sterk neemt de [Von Neumann architectuur](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span><span class="sxs-lookup"><span data-stu-id="f92a0-114">The Azure IoT Edge platform heavily adopts the [Von Neumann architecture](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span></span> <span data-ttu-id="f92a0-115">Wat betekent dat de volledige rand van Azure IoT-architectuur is een systeem dat invoer verwerkt en produceert uitvoer; en elke afzonderlijke module is ook een klein input-output-subsysteem.</span><span class="sxs-lookup"><span data-stu-id="f92a0-115">Which means that the entire Azure IoT Edge architecture is a system that processes input and produces output; and that each individual module is also a tiny input-output subsystem.</span></span> <span data-ttu-id="f92a0-116">In deze zelfstudie stellen we de volgende twee modules:</span><span class="sxs-lookup"><span data-stu-id="f92a0-116">In this tutorial, we introduce the following two modules:</span></span>

1. <span data-ttu-id="f92a0-117">Een module die u een gesimuleerde ontvangt [uitschakelen](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) signaal en converteert naar een geformatteerde [JSON](https://en.wikipedia.org/wiki/JSON) bericht.</span><span class="sxs-lookup"><span data-stu-id="f92a0-117">A module that receives a simulated [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) signal and converts it into a formatted [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>
2. <span data-ttu-id="f92a0-118">Een module die worden afgedrukt de ontvangen [JSON](https://en.wikipedia.org/wiki/JSON) bericht.</span><span class="sxs-lookup"><span data-stu-id="f92a0-118">A module that prints the received [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>

<span data-ttu-id="f92a0-119">De volgende afbeelding geeft de typische end-to-end-gegevensstroom voor dit project weer:</span><span class="sxs-lookup"><span data-stu-id="f92a0-119">The following image displays the typical end to end dataflow for this project:</span></span>

<span data-ttu-id="f92a0-120">![Gegevensstroom tussen drie modules](media/iot-hub-iot-edge-create-module/dataflow.png "invoer: gesimuleerde uitschakelen Module. Processor: Converter Module. Uitvoer: Printer Module")</span><span class="sxs-lookup"><span data-stu-id="f92a0-120">![Dataflow between three modules](media/iot-hub-iot-edge-create-module/dataflow.png "Input: Simulated BLE Module; Processor: Converter Module; Output: Printer Module")</span></span>

## <a name="set-up-the-environment"></a><span data-ttu-id="f92a0-121">De omgeving instellen</span><span class="sxs-lookup"><span data-stu-id="f92a0-121">Set up the environment</span></span>
<span data-ttu-id="f92a0-122">Hieronder wordt beschreven hoe u snel omgeving instellen om te beginnen met het schrijven van uw eerste uitschakelen converter module met JS.</span><span class="sxs-lookup"><span data-stu-id="f92a0-122">Below we show you how to quickly set up environment to start to write your first BLE converter module with JS.</span></span>

### <a name="create-module-project"></a><span data-ttu-id="f92a0-123">Module-project maken</span><span class="sxs-lookup"><span data-stu-id="f92a0-123">Create module project</span></span>
1. <span data-ttu-id="f92a0-124">Open een opdrachtregelvenster, voert u `yo az-iot-gw-module`.</span><span class="sxs-lookup"><span data-stu-id="f92a0-124">Open a command-line window, run `yo az-iot-gw-module`.</span></span>
2. <span data-ttu-id="f92a0-125">Volg de stappen op het scherm voor het voltooien van de initialisatie van de module-project.</span><span class="sxs-lookup"><span data-stu-id="f92a0-125">Follow the steps on the screen to finish the initialization of your module project.</span></span>

### <a name="project-structure"></a><span data-ttu-id="f92a0-126">Projectstructuur</span><span class="sxs-lookup"><span data-stu-id="f92a0-126">Project structure</span></span>
<span data-ttu-id="f92a0-127">Een module JS project bestaat uit de volgende onderdelen:</span><span class="sxs-lookup"><span data-stu-id="f92a0-127">A JS module project consists of the following components:</span></span>

<span data-ttu-id="f92a0-128">`modules`-De aangepaste JS module bronbestanden.</span><span class="sxs-lookup"><span data-stu-id="f92a0-128">`modules` - The customized JS module source files.</span></span> <span data-ttu-id="f92a0-129">De standaard vervangen `sensor.js` en `printer.js` met uw eigen module-bestanden.</span><span class="sxs-lookup"><span data-stu-id="f92a0-129">Replace the default `sensor.js` and `printer.js` with your own module files.</span></span>

<span data-ttu-id="f92a0-130">`app.js`-De post-bestand om het exemplaar van de rand te starten.</span><span class="sxs-lookup"><span data-stu-id="f92a0-130">`app.js` - The entry file to start the Edge instance.</span></span>

<span data-ttu-id="f92a0-131">`gw.config.json`-Het configuratiebestand voor het aanpassen van de modules moeten worden geladen door een rand.</span><span class="sxs-lookup"><span data-stu-id="f92a0-131">`gw.config.json` - The configuration file to customize the modules to be loaded by Edge.</span></span>

<span data-ttu-id="f92a0-132">`package.json`-Informatie over de metagegevens voor module project.</span><span class="sxs-lookup"><span data-stu-id="f92a0-132">`package.json` - The metadata information for module project.</span></span>

<span data-ttu-id="f92a0-133">`README.md`-De basisdocumentatie voor module project.</span><span class="sxs-lookup"><span data-stu-id="f92a0-133">`README.md` - The basic documentation for module project.</span></span>


### <a name="package-file"></a><span data-ttu-id="f92a0-134">Het pakketbestand</span><span class="sxs-lookup"><span data-stu-id="f92a0-134">Package file</span></span>

<span data-ttu-id="f92a0-135">Dit `package.json` declareert alle informatie over de metagegevens die nodig is voor een module-project met de naam, versie, post, scripts, runtime en ontwikkeling afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="f92a0-135">This `package.json` declares all the metadata information needed by a module project that includes the name, version, entry, scripts, runtime, and development dependencies.</span></span>

<span data-ttu-id="f92a0-136">Volgende codefragment toont hoe u configureert voor converter-voorbeeldproject uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="f92a0-136">Following code snippet shows how to configure for BLE converter sample project.</span></span>
```json
{
  "name": "converter",
  "version": "1.0.0",
  "description": "BLE data converter sample for Azure IoT Edge.",
  "repository": {
    "type": "git",
    "url": "https://github.com/Azure-Samples/iot-edge-samples"
  },
  "main": "app.js",
  "scripts": {
    "start": "node app.js"
  },
  "author": "Microsoft Corporation",
  "license": "MIT",
  "dependencies": {
  },
  "devDependencies": {
    "azure-iot-gateway": "~1.1.3"
  }
}
```


### <a name="entry-file"></a><span data-ttu-id="f92a0-137">Post-bestand</span><span class="sxs-lookup"><span data-stu-id="f92a0-137">Entry file</span></span>
<span data-ttu-id="f92a0-138">De `app.js` definieert de manier waarop het exemplaar van de rand initialiseren.</span><span class="sxs-lookup"><span data-stu-id="f92a0-138">The `app.js` defines the way to initialize the edge instance.</span></span> <span data-ttu-id="f92a0-139">Er hoeft niet hier een wijziging aanbrengt.</span><span class="sxs-lookup"><span data-stu-id="f92a0-139">Here we don't need to make any change.</span></span>

```javascript
(function() {
  'use strict';

  const Gateway = require('azure-iot-gateway');
  let config_path = './gw.config.json';

  // node app.js
  if (process.argv.length < 2) {
    throw 'Calling pattern should be node app.js.';
  }

  const gw = new Gateway(config_path);
  gw.run();
})();
```

### <a name="interface-of-module"></a><span data-ttu-id="f92a0-140">Interface van de module</span><span class="sxs-lookup"><span data-stu-id="f92a0-140">Interface of module</span></span>
<span data-ttu-id="f92a0-141">U kunt een module voor Azure IoT rand behandelen als een processor van de gegevens waarvan de taak is: invoer ontvangen, verwerken en uitvoer te produceren.</span><span class="sxs-lookup"><span data-stu-id="f92a0-141">You can treat an Azure IoT Edge module as a data processor whose job is to: receive input, process it, and produce output.</span></span>

<span data-ttu-id="f92a0-142">De invoer mogelijk gegevens van hardware (zoals een detectie beweging), een bericht van andere modules of iets anders (zoals een willekeurig getal die regelmatig worden gegenereerd door een timer).</span><span class="sxs-lookup"><span data-stu-id="f92a0-142">The input might be data from hardware (like a motion detector), a message from other modules, or anything else (like a random number generated periodically by a timer).</span></span>

<span data-ttu-id="f92a0-143">De uitvoer is vergelijkbaar met de invoer gebruikt, kan het gedrag van hardware (zoals de knipperende LED), een bericht naar de andere modules of iets anders (zoals afdrukken naar de console) activeren.</span><span class="sxs-lookup"><span data-stu-id="f92a0-143">The output is similar to the input, it could trigger hardware behavior (like the blinking LED), a message to other modules, or anything else (like printing to the console).</span></span>

<span data-ttu-id="f92a0-144">Modules communiceren met elkaar met behulp van `message` object.</span><span class="sxs-lookup"><span data-stu-id="f92a0-144">Modules communicate with each other using `message` object.</span></span> <span data-ttu-id="f92a0-145">De **inhoud** van een `message` is een bytematrix die geschikt is voor elk soort gegevens die u wilt dat vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="f92a0-145">The **content** of a `message` is a byte array that is capable of representing any kind of data you like.</span></span> <span data-ttu-id="f92a0-146">**Eigenschappen** zijn ook beschikbaar in de `message` en gewoon de toewijzing van een tekenreeks-naar-tekenreeks zijn.</span><span class="sxs-lookup"><span data-stu-id="f92a0-146">**Properties** are also available in the `message` and are simply a string-to-string mapping.</span></span> <span data-ttu-id="f92a0-147">U kunt zien **eigenschappen** als de kopteksten in een HTTP-aanvraag of de metagegevens van een bestand.</span><span class="sxs-lookup"><span data-stu-id="f92a0-147">You may think of **properties** as the headers in an HTTP request, or the metadata of a file.</span></span>

<span data-ttu-id="f92a0-148">Om een Azure-IoT-Edge van de module JS ontwikkelt, moet u een nieuwe module-object dat de vereiste methoden implementeert maken `receive()`.</span><span class="sxs-lookup"><span data-stu-id="f92a0-148">In order to develop an Azure IoT Edge module in JS, you need to create a new module object that implements the required methods `receive()`.</span></span> <span data-ttu-id="f92a0-149">Op dit punt wordt u mogelijk ook voor kiezen voor het implementeren van de optionele `create()` of `start()`, of `destroy()` ook methoden.</span><span class="sxs-lookup"><span data-stu-id="f92a0-149">At this point, you may also choose to implement the optional `create()` or `start()`, or `destroy()` methods as well.</span></span> <span data-ttu-id="f92a0-150">Het volgende codefragment bevat de steiger van JS module-object.</span><span class="sxs-lookup"><span data-stu-id="f92a0-150">The following code snippet shows you the scaffolding of JS module object.</span></span>

```javascript
'use strict';

module.exports = {
  broker: null,
  configuration: null,

  create: function (broker, configuration) {
    // Default implementation.
    this.broker = broker;
    this.configuration = configuration;

    return true;
  },

  start: function () {
    // Produce
  },

  receive: function (message) {
    // Consume
  },

  destroy: function () {
  }
};
```

### <a name="converter-module"></a><span data-ttu-id="f92a0-151">Converter module</span><span class="sxs-lookup"><span data-stu-id="f92a0-151">Converter module</span></span>
| <span data-ttu-id="f92a0-152">Invoer</span><span class="sxs-lookup"><span data-stu-id="f92a0-152">Input</span></span>                    | <span data-ttu-id="f92a0-153">Processor</span><span class="sxs-lookup"><span data-stu-id="f92a0-153">Processor</span></span>                              | <span data-ttu-id="f92a0-154">Uitvoer</span><span class="sxs-lookup"><span data-stu-id="f92a0-154">Output</span></span>                 | <span data-ttu-id="f92a0-155">Bronbestand</span><span class="sxs-lookup"><span data-stu-id="f92a0-155">Source File</span></span>            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| <span data-ttu-id="f92a0-156">Bericht temperatuur-gegevens</span><span class="sxs-lookup"><span data-stu-id="f92a0-156">Temperature data message</span></span> | <span data-ttu-id="f92a0-157">Parseren en het maken van een nieuwe JSON-bericht</span><span class="sxs-lookup"><span data-stu-id="f92a0-157">Parse and construct a new JSON message</span></span> | <span data-ttu-id="f92a0-158">Structuur JSON-bericht</span><span class="sxs-lookup"><span data-stu-id="f92a0-158">Structure JSON message</span></span> | `converter.js` |

<span data-ttu-id="f92a0-159">Dit is een typische Azure IoT Edge-module.</span><span class="sxs-lookup"><span data-stu-id="f92a0-159">This module is a typical Azure IoT Edge module.</span></span> <span data-ttu-id="f92a0-160">De cmdlet accepteert temperatuur berichten van andere modules (een hardware-module of in dit geval onze gesimuleerde uitschakelen module); en vervolgens Normaliseert het temperatuur-bericht in een gestructureerde JSON-bericht (inclusief het toevoegen van de bericht-ID, de eigenschap van het of we moeten de temperatuur waarschuwing activeren, enzovoort).</span><span class="sxs-lookup"><span data-stu-id="f92a0-160">It accepts temperature messages from other modules (a hardware module, or in this case our simulated BLE module); and then normalizes the temperature message in to a structured JSON message (including appending the message ID, setting the property of whether we need to trigger the temperature alert, and so on).</span></span>

```javascript
receive: function (message) {
  // Initialize the messageCount in global object at first time.
  if (!global.messageCount) {
    global.messageCount = 0;
  }

  // Read the content and properties objects from message.
  let rawContent = JSON.parse(Buffer.from(message.content).toString('utf8'));
  let rawProperties = message.properties;

  // Generate new properties object.
  let newProperties = {
    source: rawProperties.source,
    macAddress: rawProperties.macAddress,
    temperatureAlert: rawContent.temperature > 30 ? 'true' : 'false'
  };

  // Generate new content object.
  let newContent = {
    deviceId: 'Intel NUC Gateway',
    messageId: ++global.messageCount,
    temperature: rawContent.temperature
  };

  // Publish the new message to broker.
  this.broker.publish(
    {
      properties: newProperties,
      content: new Uint8Array(Buffer.from(JSON.stringify(newContent), 'utf8'))
    }
  );
},
```

### <a name="printer-module"></a><span data-ttu-id="f92a0-161">Module printer</span><span class="sxs-lookup"><span data-stu-id="f92a0-161">Printer module</span></span>
| <span data-ttu-id="f92a0-162">Invoer</span><span class="sxs-lookup"><span data-stu-id="f92a0-162">Input</span></span>                          | <span data-ttu-id="f92a0-163">Processor</span><span class="sxs-lookup"><span data-stu-id="f92a0-163">Processor</span></span> | <span data-ttu-id="f92a0-164">Uitvoer</span><span class="sxs-lookup"><span data-stu-id="f92a0-164">Output</span></span>                     | <span data-ttu-id="f92a0-165">Bronbestand</span><span class="sxs-lookup"><span data-stu-id="f92a0-165">Source File</span></span>          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| <span data-ttu-id="f92a0-166">Een bericht ontvangen van andere modules</span><span class="sxs-lookup"><span data-stu-id="f92a0-166">Any message from other modules</span></span> | <span data-ttu-id="f92a0-167">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="f92a0-167">N/A</span></span>       | <span data-ttu-id="f92a0-168">Meld u het bericht aan console</span><span class="sxs-lookup"><span data-stu-id="f92a0-168">Log the message to console</span></span> | `printer.js` |

<span data-ttu-id="f92a0-169">Deze module is eenvoudig, zelfverklarend, die het terminalvenster uitgang van de ontvangen berichten (eigenschap, inhoud).</span><span class="sxs-lookup"><span data-stu-id="f92a0-169">This module is simple, self-explanatory, which outputs the received messages(property, content) to the terminal window.</span></span>

```javascript
receive: function (message) {
  let properties = JSON.stringify(message.properties);
  let content = Buffer.from(message.content).toString('utf8');

  console.log(`printer.receive.properties - ${properties}`);
  console.log(`printer.receive.content - ${content}\n`);
}
```

### <a name="configuration"></a><span data-ttu-id="f92a0-170">Configuratie</span><span class="sxs-lookup"><span data-stu-id="f92a0-170">Configuration</span></span>
<span data-ttu-id="f92a0-171">De laatste stap voordat u de modules is voor het configureren van de rand van de IoT Azure en de verbindingen tussen modules.</span><span class="sxs-lookup"><span data-stu-id="f92a0-171">The final step before running the modules is to configure the Azure IoT Edge and to establish the connections between modules.</span></span>

<span data-ttu-id="f92a0-172">Eerst moet u declareren onze `node` loader (sinds het Azure IoT rand ondersteunt laadprogramma's van verschillende talen) die kan worden verwezen door de `name` in de secties later.</span><span class="sxs-lookup"><span data-stu-id="f92a0-172">First we need to declare our `node` loader (since Azure IoT Edge supports loaders of different languages) which could be referenced by its `name` in the sections afterward.</span></span>

```json
"loaders": [
  {
    "type": "node",
    "name": "node"
  }
]
```

<span data-ttu-id="f92a0-173">Wanneer we onze laadprogramma's hebt gedeclareerd, moeten we ook onze modules ook declareren.</span><span class="sxs-lookup"><span data-stu-id="f92a0-173">Once we have declared our loaders, we also need to declare our modules as well.</span></span> <span data-ttu-id="f92a0-174">Net als bij het declareren van het laadprogramma's, kan ook worden verwezen door hun `name` kenmerk.</span><span class="sxs-lookup"><span data-stu-id="f92a0-174">Similar to declaring the loaders, they can also be referenced by their `name` attribute.</span></span> <span data-ttu-id="f92a0-175">Als u een module definieert, moeten we de lader van de het moet gebruiken (dit moet zijn voordat is gedefinieerd) opgeven en het-ingangspunt (moet de genormaliseerde klassenaam van onze module zijn) voor elke module.</span><span class="sxs-lookup"><span data-stu-id="f92a0-175">When declaring a module, we need to specify the loader it should use (which should be the one we defined before) and the entry-point (should be the normalized class name of our module) for each module.</span></span> <span data-ttu-id="f92a0-176">De `simulated_device` is een systeemeigen module die is opgenomen in de Azure IoT rand core runtime-pakket.</span><span class="sxs-lookup"><span data-stu-id="f92a0-176">The `simulated_device` module is a native module that is included in the Azure IoT Edge core runtime package.</span></span> <span data-ttu-id="f92a0-177">Omvatten `args` in de JSON-bestand, zelfs indien deze `null`.</span><span class="sxs-lookup"><span data-stu-id="f92a0-177">Include `args` in the JSON file even if it is `null`.</span></span>

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
      "name": "node",
      "entrypoint": {
        "main.path": "modules/converter.js"
      }
    },
    "args": null
  },
  {
    "name": "printer",
    "loader": {
      "name": "node",
      "entrypoint": {
        "main.path": "modules/printer.js"
      }
    },
    "args": null
  }
]
```

<span data-ttu-id="f92a0-178">Aan het einde van de configuratie maken we de verbindingen.</span><span class="sxs-lookup"><span data-stu-id="f92a0-178">At the end of the configuration, we establish the connections.</span></span> <span data-ttu-id="f92a0-179">Elke verbinding wordt uitgedrukt door `source` en `sink`.</span><span class="sxs-lookup"><span data-stu-id="f92a0-179">Each connection is expressed by `source` and `sink`.</span></span> <span data-ttu-id="f92a0-180">Ze moeten beide verwijzen naar een vooraf gedefinieerde module.</span><span class="sxs-lookup"><span data-stu-id="f92a0-180">They should both reference a pre-defined module.</span></span> <span data-ttu-id="f92a0-181">Het uitvoerbericht van `source` module wordt doorgestuurd naar de invoer van `sink` module.</span><span class="sxs-lookup"><span data-stu-id="f92a0-181">The output message of `source` module is forwarded to the input of `sink` module.</span></span>

```json
"links": [
  {
    "source": "simulated_device",
    "sink": "converter"
  },
  {
    "source": "converter",
    "sink": "printer"
  }
]
```

## <a name="running-the-modules"></a><span data-ttu-id="f92a0-182">De modules uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="f92a0-182">Running the modules</span></span>
1. `npm install`
2. `npm start`

<span data-ttu-id="f92a0-183">Als u wilt dat de toepassing beëindigt, drukt u op `<Enter>` sleutel.</span><span class="sxs-lookup"><span data-stu-id="f92a0-183">If you want to terminate the application, press `<Enter>` key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f92a0-184">Het is niet raadzaam gebruik Ctrl + c drukken om de rand van de IoT-toepassing te beëindigen.</span><span class="sxs-lookup"><span data-stu-id="f92a0-184">It is not recommended to use Ctrl + C to terminate the IoT Edge application.</span></span> <span data-ttu-id="f92a0-185">Als op deze manier ertoe leiden het proces is abnormaal beëindigd dat kan.</span><span class="sxs-lookup"><span data-stu-id="f92a0-185">As this way may cause the process to terminate abnormally.</span></span>
