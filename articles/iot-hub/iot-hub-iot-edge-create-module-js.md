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
# <a name="create-an-azure-iot-edge-module-with-nodejs"></a>Een Azure IoT-Edge-Module maken met behulp van Node.js

Deze zelfstudie gepresenteerd hoe toocreate een module voor Azure IoT rand in de JS.

In deze zelfstudie bekijken we omgeving in te stellen en hoe toowrite een [uitschakelen](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) gegevens converter module met behulp van de meest recente Azure IoT rand NPM pakketten Hallo.

## <a name="prerequisites"></a>Vereisten

In deze sectie, moet u uw omgeving voor het ontwikkelen van de module IoT rand instellen. Toepassing tooboth *64-bits Windows* en *64-bits Linux (Ubuntu) 14 +* besturingssystemen.

Hallo volgende software is vereist:
* [GIT Client](https://git-scm.com/downloads).
* [Knooppunt TNS](https://nodejs.org).
* `npm install -g yo`.
* `npm install -g generator-az-iot-gw-module`

## <a name="architecture"></a>Architectuur

Hello Azure IoT rand platform aanneemt sterk Hallo [Von Neumann architectuur](https://en.wikipedia.org/wiki/Von_Neumann_architecture). Wat betekent dat Hallo volledige rand van Azure IoT-architectuur is een systeem dat invoer verwerkt en produceert uitvoer; en elke afzonderlijke module is ook een klein input-output-subsysteem. In deze zelfstudie stellen we Hallo na twee modules:

1. Een module die u een gesimuleerde ontvangt [uitschakelen](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) signaal en converteert naar een geformatteerde [JSON](https://en.wikipedia.org/wiki/JSON) bericht.
2. Een module die worden afgedrukt Hallo ontvangen [JSON](https://en.wikipedia.org/wiki/JSON) bericht.

Hallo bevat volgende afbeelding Hallo typische end tooend gegevensstroom voor dit project:

![Gegevensstroom tussen drie modules](media/iot-hub-iot-edge-create-module/dataflow.png "invoer: gesimuleerde uitschakelen Module. Processor: Converter Module. Uitvoer: Printer Module")

## <a name="set-up-hello-environment"></a>Hallo-omgeving instellen
Hieronder zien we u hoe tooquickly ingesteld omgeving toostart toowrite uw eerste uitschakelen converter module met JS.

### <a name="create-module-project"></a>Module-project maken
1. Open een opdrachtregelvenster, voert u `yo az-iot-gw-module`.
2. Volg de stappen Hallo op Hallo scherm toofinish Hallo initialisatie van de module-project.

### <a name="project-structure"></a>Projectstructuur
Een module JS project bestaat uit Hallo volgende onderdelen:

`modules`-Hallo aangepast JS module bronbestanden. Hallo standaard vervangen `sensor.js` en `printer.js` met uw eigen module-bestanden.

`app.js`-Hallo vermelding bestand toostart Hallo rand exemplaar.

`gw.config.json`-Hallo configuration file toocustomize Hallo modules toobe geladen door een rand.

`package.json`-Hallo-metagegevens voor de module project.

`README.md`-Hallo basisdocumentatie voor module project.


### <a name="package-file"></a>Het pakketbestand

Dit `package.json` alle Hallo metagegevens die nodig is voor een module-project met de naam, versie, post, scripts, runtime en ontwikkeling afhankelijkheden Hallo declareert.

Na de code codefragment bevat steekproef tooconfigure uitschakelen conversieprogramma voor hoe project.
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


### <a name="entry-file"></a>Post-bestand
Hallo `app.js` Hallo manier tooinitialize Hallo rand exemplaar definieert. Hier moeten niet we toomake elke wijziging.

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

### <a name="interface-of-module"></a>Interface van de module
U kunt een module voor Azure IoT rand behandelen als een processor van de gegevens waarvan de taak is: invoer ontvangen, verwerken en uitvoer te produceren.

Hallo invoer mogelijk gegevens van hardware (zoals een detectie beweging), een bericht van andere modules of iets anders (zoals een willekeurig getal die regelmatig worden gegenereerd door een timer).

Hallo-uitvoer is vergelijkbaar toohello invoer gebruikt, kan het gedrag van hardware (zoals Hallo knipperende LED), een bericht tooother modules of iets anders (zoals afdrukken toohello console) activeren.

Modules communiceren met elkaar met behulp van `message` object. Hallo **inhoud** van een `message` is een bytematrix die geschikt is voor elk soort gegevens die u wilt dat vertegenwoordigt. **Eigenschappen** zijn ook beschikbaar in Hallo `message` en gewoon de toewijzing van een tekenreeks-naar-tekenreeks zijn. U kunt zien **eigenschappen** als Hallo veldnamen in een HTTP-aanvraag of Hallo metagegevens van een bestand.

In de volgorde toodevelop een Azure-IoT-Edge van de module JS, moet u een nieuwe moduleobject dat Hallo vereist methoden implementeert toocreate `receive()`. Op dit moment, u kunt ook tooimplement Hallo optionele `create()` of `start()`, of `destroy()` ook methoden. Hallo volgende codefragment toont dat u Hallo scaffolding van JS module-object.

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

### <a name="converter-module"></a>Converter module
| Invoer                    | Processor                              | Uitvoer                 | Bronbestand            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| Bericht temperatuur-gegevens | Parseren en het maken van een nieuwe JSON-bericht | Structuur JSON-bericht | `converter.js` |

Dit is een typische Azure IoT Edge-module. De cmdlet accepteert temperatuur berichten van andere modules (een hardware-module of in dit geval onze gesimuleerde uitschakelen module); en vervolgens normaliseert temperatuur het Hallo-bericht in tooa gestructureerd JSON bericht (inclusief voegen Hallo bericht-ID, Hallo-eigenschap van het of we tootrigger Hallo temperatuur waarschuwing moeten enzovoort).

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

### <a name="printer-module"></a>Module printer
| Invoer                          | Processor | Uitvoer                     | Bronbestand          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| Een bericht ontvangen van andere modules | N.v.t.       | Meld u Hallo-bericht tooconsole | `printer.js` |

Deze module is eenvoudig, zelfverklarend, die Hallo ontvangen berichten (eigenschap, inhoud) toohello terminalvenster levert.

```javascript
receive: function (message) {
  let properties = JSON.stringify(message.properties);
  let content = Buffer.from(message.content).toString('utf8');

  console.log(`printer.receive.properties - ${properties}`);
  console.log(`printer.receive.content - ${content}\n`);
}
```

### <a name="configuration"></a>Configuratie
laatste stap voordat u de modules Hallo Hallo is tooconfigure hello Azure IoT rand en tooestablish Hallo verbindingen tussen modules.

Eerst moet u toodeclare onze `node` loader (sinds het Azure IoT rand ondersteunt laadprogramma's van verschillende talen) die kan worden verwezen door de `name` in daarna Hallo-secties.

```json
"loaders": [
  {
    "type": "node",
    "name": "node"
  }
]
```

Wanneer we onze laadprogramma's hebt gedeclareerd, ook moet toodeclare ook onze modules. Te laadprogramma's vergelijkbaar toodeclaring hello, kan ook worden verwezen door hun `name` kenmerk. Als u een module definieert, moeten we toospecify Hallo loader het moet gebruiken (dit moet Hallo een we gedefinieerd vóór zijn) en het Hallo ingangspunt (moet Hallo genormaliseerde klassenaam van onze module zijn) voor elke module. Hallo `simulated_device` is een systeemeigen module die is opgenomen in hello Azure IoT rand core runtime-pakket. Omvatten `args` in JSON-bestand zelfs indien deze Hallo `null`.

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

Aan het einde van de Hallo van Hallo configuratie maken we Hallo verbindingen. Elke verbinding wordt uitgedrukt door `source` en `sink`. Ze moeten beide verwijzen naar een vooraf gedefinieerde module. Hallo-bericht van uitvoer van `source` module doorgestuurd toohello invoer van `sink` module.

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

## <a name="running-hello-modules"></a>Hallo-modules uitgevoerd
1. `npm install`
2. `npm start`

Als u tooterminate Hallo toepassing wilt, drukt u op `<Enter>` sleutel.

> [!IMPORTANT]
> Het wordt niet aangeraden toouse Ctrl + C tooterminate Hallo IoT rand toepassing. Als op deze manier Hallo proces tooterminate abnormaal veroorzaken kan.
