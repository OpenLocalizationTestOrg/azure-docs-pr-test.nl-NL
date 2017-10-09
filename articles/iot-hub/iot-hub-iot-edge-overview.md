---
title: aaaOverview van Azure IoT rand | Microsoft Docs
description: Hallo architectuur worden de basisconcepten beschreven in de Azure IoT rand zoals gateways, modules en beleggingsmakelaars.
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: dobett
ms.openlocfilehash: 32debc0d4f40cfd7f2cce7cf8c76b12ec18ee2dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-edge-architectural-concepts"></a>Azure IoT rand architectuur concepten

Voordat u een voorbeeld van code bekijken of uw eigen IoT rand met veldgateway maken, moet u weten Hallo belangrijkste concepten die onderbouwing Hallo-architectuur van IoT rand.

## <a name="iot-edge-modules"></a>Rand van de IoT-modules

U een gateway bouwen met Azure IoT rand door te maken en montage *IoT rand modules*. Modules gebruiken *berichten* tooexchange gegevens met elkaar. Een module een bericht ontvangt, voert een bepaalde actie op deze desgewenst getransformeerd tot een nieuw bericht en publiceert deze voor andere tooprocess modules. Sommige modules kunnen alleen nieuwe berichten produceren en verwerken nooit binnenkomende berichten. Een keten van modules maakt een pijplijn gegevensverwerking met elke module voor het uitvoeren van een transformatie op Hallo van gegevens op één punt in deze pijplijn.

![Een keten van modules in de gateway gebouwd met de Azure IoT Edge][1]

IoT-rand bevat Hallo volgende onderdelen:

* Vooraf geschreven modules die algemene functies van de gateway uitvoeren.
* Hallo-interfaces een ontwikkelaar kan toowrite aangepaste modules kunnen gebruiken.
* Hallo infrastructuur nodig toodeploy en een set van modules uitvoeren.

Hallo SDK biedt een abstractielaag waarmee u toobuild gateways toorun op verschillende besturingssystemen en platforms.

![Azure IoT Edge-abstractielaag][2]

## <a name="messages"></a>Berichten

Hoewel u nadenkt over modules doorgeven van berichten tooeach andere is een handige manier tooconceptualize hoe de functies van een gateway, komt deze niet nauwkeurig overeen met wat er gebeurt. Een broker toocommunicate IoT Edge-modules gebruiken met elkaar. Modules publiceren van berichten toohello broker (messaging patronen, zoals bus of publiceren/abonneren met) en vervolgens laat u Hallo broker route Hallo-bericht toohello modules verbonden tooit.

Hallo maakt gebruik van een module **Broker_Publish** toopublish bericht toohello broker werken. Hallo broker biedt berichten tooa module door een callback-functie wordt aangeroepen. Een bericht bestaat uit een reeks sleutel/waarde-eigenschappen en inhoud die als een blok geheugen worden doorgegeven.

![Hallo-rol van Hallo Broker in de Azure IoT rand][3]

## <a name="message-routing-and-filtering"></a>Berichtroutering en filteren

Er zijn twee manieren toodirect berichten toohello juiste IoT rand modules:

* U kunt een set koppelingen doorgeven kunnen worden doorgegeven, is de toohello broker zodat Hallo broker Hallo bron- en sink voor elke module.
* Een module kunt filteren op Hallo eigenschappen van het Hallo-bericht.

Een module moet alleen reageren op een bericht als het Hallo-bericht is bedoeld voor het. Koppelingen en effectief filteren bericht maakt een pijplijn bericht.

## <a name="next-steps"></a>Volgende stappen

toosee deze concepten die worden toegepast in een voorbeeld van een u kunt uitvoeren, Zie [verkennen Azure IoT rand architectuur][lnk-hello-world].

<!-- Images -->
[1]: media/iot-hub-iot-edge-overview/modules.png
[2]: media/iot-hub-iot-edge-overview/modules_2.png
[3]: media/iot-hub-iot-edge-overview/messages_1.png

<!-- Links -->
[lnk-hello-world]: ./iot-hub-linux-iot-edge-get-started.md