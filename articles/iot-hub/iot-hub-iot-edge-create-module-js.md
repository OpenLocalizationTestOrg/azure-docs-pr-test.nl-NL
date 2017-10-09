---
title: aaaCreate een Azure IoT Edge-Module met behulp van Node.js | Microsoft Docs
description: Deze zelfstudie gepresenteerd hoe een Aanmeldingsprompt gegevens converter module met toowrite Hallo meest recente Azure IoT rand NPM pakketten en Yeoman generator.
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
ms.openlocfilehash: d3e696b5a310377ffb8e99998ff0714bf7c0bb41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-iot-edge-module-with-nodejs"></a><span data-ttu-id="8434e-103">Een Azure IoT-Edge-Module maken met behulp van Node.js</span><span class="sxs-lookup"><span data-stu-id="8434e-103">Create an Azure IoT Edge Module with Node.js</span></span>

<span data-ttu-id="8434e-104">Deze zelfstudie gepresenteerd hoe toocreate een module voor Azure IoT rand in de JS.</span><span class="sxs-lookup"><span data-stu-id="8434e-104">This tutorial showcases how toocreate a module for Azure IoT Edge in JS.</span></span>

<span data-ttu-id="8434e-105">In deze zelfstudie bekijken we omgeving in te stellen en hoe toowrite een [uitschakelen](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) gegevens converter module met behulp van de meest recente Azure IoT rand NPM pakketten Hallo.</span><span class="sxs-lookup"><span data-stu-id="8434e-105">In this tutorial, we walk through environment setup and how toowrite a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using hello latest Azure IoT Edge NPM packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8434e-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8434e-106">Prerequisites</span></span>

<span data-ttu-id="8434e-107">In deze sectie, moet u uw omgeving voor het ontwikkelen van de module IoT rand instellen.</span><span class="sxs-lookup"><span data-stu-id="8434e-107">In this section, you set up your environment for IoT Edge module development.</span></span> <span data-ttu-id="8434e-108">Toepassing tooboth *64-bits Windows* en *64-bits Linux (Ubuntu) 14 +* besturingssystemen.</span><span class="sxs-lookup"><span data-stu-id="8434e-108">It applies tooboth *64-bit Windows* and *64-bit Linux (Ubuntu 14+)* operating systems.</span></span>

<span data-ttu-id="8434e-109">Hallo volgende software is vereist:</span><span class="sxs-lookup"><span data-stu-id="8434e-109">hello following software is required:</span></span>
* <span data-ttu-id="8434e-110">[GIT Client](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="8434e-110">[Git Client](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="8434e-111">[Knooppunt TNS](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="8434e-111">[Node LTS](https://nodejs.org).</span></span>
* <span data-ttu-id="8434e-112">`npm install -g yo`.</span><span class="sxs-lookup"><span data-stu-id="8434e-112">`npm install -g yo`.</span></span>
* `npm install -g generator-az-iot-gw-module`

## <a name="architecture"></a><span data-ttu-id="8434e-113">Architectuur</span><span class="sxs-lookup"><span data-stu-id="8434e-113">Architecture</span></span>

<span data-ttu-id="8434e-114">Hello Azure IoT rand platform aanneemt sterk Hallo [Von Neumann architectuur](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span><span class="sxs-lookup"><span data-stu-id="8434e-114">hello Azure IoT Edge platform heavily adopts hello [Von Neumann architecture](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span></span> <span data-ttu-id="8434e-115">Wat betekent dat Hallo volledige rand van Azure IoT-architectuur is een systeem dat invoer verwerkt en produceert uitvoer; en elke afzonderlijke module is ook een klein input-output-subsysteem.</span><span class="sxs-lookup"><span data-stu-id="8434e-115">Which means that hello entire Azure IoT Edge architecture is a system that processes input and produces output; and that each individual module is also a tiny input-output subsystem.</span></span> <span data-ttu-id="8434e-116">In deze zelfstudie stellen we Hallo na twee modules:</span><span class="sxs-lookup"><span data-stu-id="8434e-116">In this tutorial, we introduce hello following two modules:</span></span>

1. <span data-ttu-id="8434e-117">Een module die u een gesimuleerde ontvangt [uitschakelen](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) signaal en converteert naar een geformatteerde [JSON](https://en.wikipedia.org/wiki/JSON) bericht.</span><span class="sxs-lookup"><span data-stu-id="8434e-117">A module that receives a simulated [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) signal and converts it into a formatted [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>
2. <span data-ttu-id="8434e-118">Een module die worden afgedrukt Hallo ontvangen [JSON](https://en.wikipedia.org/wiki/JSON) bericht.</span><span class="sxs-lookup"><span data-stu-id="8434e-118">A module that prints hello received [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>

<span data-ttu-id="8434e-119">Hallo bevat volgende afbeelding Hallo typische end tooend gegevensstroom voor dit project:</span><span class="sxs-lookup"><span data-stu-id="8434e-119">hello following image displays hello typical end tooend dataflow for this project:</span></span>

<span data-ttu-id="8434e-120">![Gegevensstroom tussen drie modules](media/iot-hub-iot-edge-create-module/dataflow.png "invoer: gesimuleerde uitschakelen Module. Processor: Converter Module. Uitvoer: Printer Module")</span><span class="sxs-lookup"><span data-stu-id="8434e-120">![Dataflow between three modules](media/iot-hub-iot-edge-create-module/dataflow.png "Input: Simulated BLE Module; Processor: Converter Module; Output: Printer Module")</span></span>

## <a name="set-up-hello-environment"></a><span data-ttu-id="8434e-121">Hallo-omgeving instellen</span><span class="sxs-lookup"><span data-stu-id="8434e-121">Set up hello environment</span></span>
<span data-ttu-id="8434e-122">Hieronder zien we u hoe tooquickly ingesteld omgeving toostart toowrite uw eerste uitschakelen converter module met JS.</span><span class="sxs-lookup"><span data-stu-id="8434e-122">Below we show you how tooquickly set up environment toostart toowrite your first BLE converter module with JS.</span></span>

### <a name="create-module-project"></a><span data-ttu-id="8434e-123">Module-project maken</span><span class="sxs-lookup"><span data-stu-id="8434e-123">Create module project</span></span>
1. <span data-ttu-id="8434e-124">Open een opdrachtregelvenster, voert u `yo az-iot-gw-module`.</span><span class="sxs-lookup"><span data-stu-id="8434e-124">Open a command-line window, run `yo az-iot-gw-module`.</span></span>
2. <span data-ttu-id="8434e-125">Volg de stappen Hallo op Hallo scherm toofinish Hallo initialisatie van de module-project.</span><span class="sxs-lookup"><span data-stu-id="8434e-125">Follow hello steps on hello screen toofinish hello initialization of your module project.</span></span>

### <a name="project-structure"></a><span data-ttu-id="8434e-126">Projectstructuur</span><span class="sxs-lookup"><span data-stu-id="8434e-126">Project structure</span></span>
<span data-ttu-id="8434e-127">Een module JS project bestaat uit Hallo volgende onderdelen:</span><span class="sxs-lookup"><span data-stu-id="8434e-127">A JS module project consists of hello following components:</span></span>

<span data-ttu-id="8434e-128">`modules`-Hallo aangepast JS module bronbestanden.</span><span class="sxs-lookup"><span data-stu-id="8434e-128">`modules` - hello customized JS module source files.</span></span> <span data-ttu-id="8434e-129">Hallo standaard vervangen `sensor.js` en `printer.js` met uw eigen module-bestanden.</span><span class="sxs-lookup"><span data-stu-id="8434e-129">Replace hello default `sensor.js` and `printer.js` with your own module files.</span></span>

<span data-ttu-id="8434e-130">`app.js`-Hallo vermelding bestand toostart Hallo rand exemplaar.</span><span class="sxs-lookup"><span data-stu-id="8434e-130">`app.js` - hello entry file toostart hello Edge instance.</span></span>

<span data-ttu-id="8434e-131">`gw.config.json`-Hallo configuration file toocustomize Hallo modules toobe geladen door een rand.</span><span class="sxs-lookup"><span data-stu-id="8434e-131">`gw.config.json` - hello configuration file toocustomize hello modules toobe loaded by Edge.</span></span>

<span data-ttu-id="8434e-132">`package.json`-Hallo-metagegevens voor de module project.</span><span class="sxs-lookup"><span data-stu-id="8434e-132">`package.json` - hello metadata information for module project.</span></span>

<span data-ttu-id="8434e-133">`README.md`-Hallo basisdocumentatie voor module project.</span><span class="sxs-lookup"><span data-stu-id="8434e-133">`README.md` - hello basic documentation for module project.</span></span>


### <a name="package-file"></a><span data-ttu-id="8434e-134">Het pakketbestand</span><span class="sxs-lookup"><span data-stu-id="8434e-134">Package file</span></span>

<span data-ttu-id="8434e-135">Dit `package.json` alle Hallo metagegevens die nodig is voor een module-project met de naam, versie, post, scripts, runtime en ontwikkeling afhankelijkheden Hallo declareert.</span><span class="sxs-lookup"><span data-stu-id="8434e-135">This `package.json` declares all hello metadata information needed by a module project that includes hello name, version, entry, scripts, runtime, and development dependencies.</span></span>

<span data-ttu-id="8434e-136">Na de code codefragment bevat steekproef tooconfigure uitschakelen conversieprogramma voor hoe project.</span><span class="sxs-lookup"><span data-stu-id="8434e-136">Following code snippet shows how tooconfigure for BLE converter sample project.</span></span>
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


### <a name="entry-file"></a><span data-ttu-id="8434e-137">Post-bestand</span><span class="sxs-lookup"><span data-stu-id="8434e-137">Entry file</span></span>
<span data-ttu-id="8434e-138">Hallo `app.js` Hallo manier tooinitialize Hallo rand exemplaar definieert.</span><span class="sxs-lookup"><span data-stu-id="8434e-138">hello `app.js` defines hello way tooinitialize hello edge instance.</span></span> <span data-ttu-id="8434e-139">Hier moeten niet we toomake elke wijziging.</span><span class="sxs-lookup"><span data-stu-id="8434e-139">Here we don't need toomake any change.</span></span>

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

### <a name="interface-of-module"></a><span data-ttu-id="8434e-140">Interface van de module</span><span class="sxs-lookup"><span data-stu-id="8434e-140">Interface of module</span></span>
<span data-ttu-id="8434e-141">U kunt een module voor Azure IoT rand behandelen als een processor van de gegevens waarvan de taak is: invoer ontvangen, verwerken en uitvoer te produceren.</span><span class="sxs-lookup"><span data-stu-id="8434e-141">You can treat an Azure IoT Edge module as a data processor whose job is to: receive input, process it, and produce output.</span></span>

<span data-ttu-id="8434e-142">Hallo invoer mogelijk gegevens van hardware (zoals een detectie beweging), een bericht van andere modules of iets anders (zoals een willekeurig getal die regelmatig worden gegenereerd door een timer).</span><span class="sxs-lookup"><span data-stu-id="8434e-142">hello input might be data from hardware (like a motion detector), a message from other modules, or anything else (like a random number generated periodically by a timer).</span></span>

<span data-ttu-id="8434e-143">Hallo-uitvoer is vergelijkbaar toohello invoer gebruikt, kan het gedrag van hardware (zoals Hallo knipperende LED), een bericht tooother modules of iets anders (zoals afdrukken toohello console) activeren.</span><span class="sxs-lookup"><span data-stu-id="8434e-143">hello output is similar toohello input, it could trigger hardware behavior (like hello blinking LED), a message tooother modules, or anything else (like printing toohello console).</span></span>

<span data-ttu-id="8434e-144">Modules communiceren met elkaar met behulp van `message` object.</span><span class="sxs-lookup"><span data-stu-id="8434e-144">Modules communicate with each other using `message` object.</span></span> <span data-ttu-id="8434e-145">Hallo **inhoud** van een `message` is een bytematrix die geschikt is voor elk soort gegevens die u wilt dat vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="8434e-145">hello **content** of a `message` is a byte array that is capable of representing any kind of data you like.</span></span> <span data-ttu-id="8434e-146">**Eigenschappen** zijn ook beschikbaar in Hallo `message` en gewoon de toewijzing van een tekenreeks-naar-tekenreeks zijn.</span><span class="sxs-lookup"><span data-stu-id="8434e-146">**Properties** are also available in hello `message` and are simply a string-to-string mapping.</span></span> <span data-ttu-id="8434e-147">U kunt zien **eigenschappen** als Hallo veldnamen in een HTTP-aanvraag of Hallo metagegevens van een bestand.</span><span class="sxs-lookup"><span data-stu-id="8434e-147">You may think of **properties** as hello headers in an HTTP request, or hello metadata of a file.</span></span>

<span data-ttu-id="8434e-148">In de volgorde toodevelop een Azure-IoT-Edge van de module JS, moet u een nieuwe moduleobject dat Hallo vereist methoden implementeert toocreate `receive()`.</span><span class="sxs-lookup"><span data-stu-id="8434e-148">In order toodevelop an Azure IoT Edge module in JS, you need toocreate a new module object that implements hello required methods `receive()`.</span></span> <span data-ttu-id="8434e-149">Op dit moment, u kunt ook tooimplement Hallo optionele `create()` of `start()`, of `destroy()` ook methoden.</span><span class="sxs-lookup"><span data-stu-id="8434e-149">At this point, you may also choose tooimplement hello optional `create()` or `start()`, or `destroy()` methods as well.</span></span> <span data-ttu-id="8434e-150">Hallo volgende codefragment toont dat u Hallo scaffolding van JS module-object.</span><span class="sxs-lookup"><span data-stu-id="8434e-150">hello following code snippet shows you hello scaffolding of JS module object.</span></span>

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

### <a name="converter-module"></a><span data-ttu-id="8434e-151">Converter module</span><span class="sxs-lookup"><span data-stu-id="8434e-151">Converter module</span></span>
| <span data-ttu-id="8434e-152">Invoer</span><span class="sxs-lookup"><span data-stu-id="8434e-152">Input</span></span>                    | <span data-ttu-id="8434e-153">Processor</span><span class="sxs-lookup"><span data-stu-id="8434e-153">Processor</span></span>                              | <span data-ttu-id="8434e-154">Uitvoer</span><span class="sxs-lookup"><span data-stu-id="8434e-154">Output</span></span>                 | <span data-ttu-id="8434e-155">Bronbestand</span><span class="sxs-lookup"><span data-stu-id="8434e-155">Source File</span></span>            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| <span data-ttu-id="8434e-156">Bericht temperatuur-gegevens</span><span class="sxs-lookup"><span data-stu-id="8434e-156">Temperature data message</span></span> | <span data-ttu-id="8434e-157">Parseren en het maken van een nieuwe JSON-bericht</span><span class="sxs-lookup"><span data-stu-id="8434e-157">Parse and construct a new JSON message</span></span> | <span data-ttu-id="8434e-158">Structuur JSON-bericht</span><span class="sxs-lookup"><span data-stu-id="8434e-158">Structure JSON message</span></span> | `converter.js` |

<span data-ttu-id="8434e-159">Dit is een typische Azure IoT Edge-module.</span><span class="sxs-lookup"><span data-stu-id="8434e-159">This module is a typical Azure IoT Edge module.</span></span> <span data-ttu-id="8434e-160">De cmdlet accepteert temperatuur berichten van andere modules (een hardware-module of in dit geval onze gesimuleerde uitschakelen module); en vervolgens normaliseert temperatuur het Hallo-bericht in tooa gestructureerd JSON bericht (inclusief voegen Hallo bericht-ID, Hallo-eigenschap van het of we tootrigger Hallo temperatuur waarschuwing moeten enzovoort).</span><span class="sxs-lookup"><span data-stu-id="8434e-160">It accepts temperature messages from other modules (a hardware module, or in this case our simulated BLE module); and then normalizes hello temperature message in tooa structured JSON message (including appending hello message ID, setting hello property of whether we need tootrigger hello temperature alert, and so on).</span></span>

```javascript
receive: function (message) {
  // Initialize hello messageCount in global object at first time.
  if (!global.messageCount) {
    global.messageCount = 0;
  }

  // Read hello content and properties objects from message.
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

  // Publish hello new message toobroker.
  this.broker.publish(
    {
      properties: newProperties,
      content: new Uint8Array(Buffer.from(JSON.stringify(newContent), 'utf8'))
    }
  );
},
```

### <a name="printer-module"></a><span data-ttu-id="8434e-161">Module printer</span><span class="sxs-lookup"><span data-stu-id="8434e-161">Printer module</span></span>
| <span data-ttu-id="8434e-162">Invoer</span><span class="sxs-lookup"><span data-stu-id="8434e-162">Input</span></span>                          | <span data-ttu-id="8434e-163">Processor</span><span class="sxs-lookup"><span data-stu-id="8434e-163">Processor</span></span> | <span data-ttu-id="8434e-164">Uitvoer</span><span class="sxs-lookup"><span data-stu-id="8434e-164">Output</span></span>                     | <span data-ttu-id="8434e-165">Bronbestand</span><span class="sxs-lookup"><span data-stu-id="8434e-165">Source File</span></span>          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| <span data-ttu-id="8434e-166">Een bericht ontvangen van andere modules</span><span class="sxs-lookup"><span data-stu-id="8434e-166">Any message from other modules</span></span> | <span data-ttu-id="8434e-167">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="8434e-167">N/A</span></span>       | <span data-ttu-id="8434e-168">Meld u Hallo-bericht tooconsole</span><span class="sxs-lookup"><span data-stu-id="8434e-168">Log hello message tooconsole</span></span> | `printer.js` |

<span data-ttu-id="8434e-169">Deze module is eenvoudig, zelfverklarend, die Hallo ontvangen berichten (eigenschap, inhoud) toohello terminalvenster levert.</span><span class="sxs-lookup"><span data-stu-id="8434e-169">This module is simple, self-explanatory, which outputs hello received messages(property, content) toohello terminal window.</span></span>

```javascript
receive: function (message) {
  let properties = JSON.stringify(message.properties);
  let content = Buffer.from(message.content).toString('utf8');

  console.log(`printer.receive.properties - ${properties}`);
  console.log(`printer.receive.content - ${content}\n`);
}
```

### <a name="configuration"></a><span data-ttu-id="8434e-170">Configuratie</span><span class="sxs-lookup"><span data-stu-id="8434e-170">Configuration</span></span>
<span data-ttu-id="8434e-171">laatste stap voordat u de modules Hallo Hallo is tooconfigure hello Azure IoT rand en tooestablish Hallo verbindingen tussen modules.</span><span class="sxs-lookup"><span data-stu-id="8434e-171">hello final step before running hello modules is tooconfigure hello Azure IoT Edge and tooestablish hello connections between modules.</span></span>

<span data-ttu-id="8434e-172">Eerst moet u toodeclare onze `node` loader (sinds het Azure IoT rand ondersteunt laadprogramma's van verschillende talen) die kan worden verwezen door de `name` in daarna Hallo-secties.</span><span class="sxs-lookup"><span data-stu-id="8434e-172">First we need toodeclare our `node` loader (since Azure IoT Edge supports loaders of different languages) which could be referenced by its `name` in hello sections afterward.</span></span>

```json
"loaders": [
  {
    "type": "node",
    "name": "node"
  }
]
```

<span data-ttu-id="8434e-173">Wanneer we onze laadprogramma's hebt gedeclareerd, ook moet toodeclare ook onze modules.</span><span class="sxs-lookup"><span data-stu-id="8434e-173">Once we have declared our loaders, we also need toodeclare our modules as well.</span></span> <span data-ttu-id="8434e-174">Te laadprogramma's vergelijkbaar toodeclaring hello, kan ook worden verwezen door hun `name` kenmerk.</span><span class="sxs-lookup"><span data-stu-id="8434e-174">Similar toodeclaring hello loaders, they can also be referenced by their `name` attribute.</span></span> <span data-ttu-id="8434e-175">Als u een module definieert, moeten we toospecify Hallo loader het moet gebruiken (dit moet Hallo een we gedefinieerd vóór zijn) en het Hallo ingangspunt (moet Hallo genormaliseerde klassenaam van onze module zijn) voor elke module.</span><span class="sxs-lookup"><span data-stu-id="8434e-175">When declaring a module, we need toospecify hello loader it should use (which should be hello one we defined before) and hello entry-point (should be hello normalized class name of our module) for each module.</span></span> <span data-ttu-id="8434e-176">Hallo `simulated_device` is een systeemeigen module die is opgenomen in hello Azure IoT rand core runtime-pakket.</span><span class="sxs-lookup"><span data-stu-id="8434e-176">hello `simulated_device` module is a native module that is included in hello Azure IoT Edge core runtime package.</span></span> <span data-ttu-id="8434e-177">Omvatten `args` in JSON-bestand zelfs indien deze Hallo `null`.</span><span class="sxs-lookup"><span data-stu-id="8434e-177">Include `args` in hello JSON file even if it is `null`.</span></span>

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

<span data-ttu-id="8434e-178">Aan het einde van de Hallo van Hallo configuratie maken we Hallo verbindingen.</span><span class="sxs-lookup"><span data-stu-id="8434e-178">At hello end of hello configuration, we establish hello connections.</span></span> <span data-ttu-id="8434e-179">Elke verbinding wordt uitgedrukt door `source` en `sink`.</span><span class="sxs-lookup"><span data-stu-id="8434e-179">Each connection is expressed by `source` and `sink`.</span></span> <span data-ttu-id="8434e-180">Ze moeten beide verwijzen naar een vooraf gedefinieerde module.</span><span class="sxs-lookup"><span data-stu-id="8434e-180">They should both reference a pre-defined module.</span></span> <span data-ttu-id="8434e-181">Hallo-bericht van uitvoer van `source` module doorgestuurd toohello invoer van `sink` module.</span><span class="sxs-lookup"><span data-stu-id="8434e-181">hello output message of `source` module is forwarded toohello input of `sink` module.</span></span>

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

## <a name="running-hello-modules"></a><span data-ttu-id="8434e-182">Hallo-modules uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="8434e-182">Running hello modules</span></span>
1. `npm install`
2. `npm start`

<span data-ttu-id="8434e-183">Als u tooterminate Hallo toepassing wilt, drukt u op `<Enter>` sleutel.</span><span class="sxs-lookup"><span data-stu-id="8434e-183">If you want tooterminate hello application, press `<Enter>` key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8434e-184">Het wordt niet aangeraden toouse Ctrl + C tooterminate Hallo IoT rand toepassing.</span><span class="sxs-lookup"><span data-stu-id="8434e-184">It is not recommended toouse Ctrl + C tooterminate hello IoT Edge application.</span></span> <span data-ttu-id="8434e-185">Als op deze manier Hallo proces tooterminate abnormaal veroorzaken kan.</span><span class="sxs-lookup"><span data-stu-id="8434e-185">As this way may cause hello process tooterminate abnormally.</span></span>
