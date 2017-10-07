---
title: aaaGet de slag met Azure Relay hybride verbindingen in knooppunt | Microsoft Docs
description: Een knooppuntconsoletoepassing schrijven voor hybride Relay-verbindingen van Azure.
services: service-bus-relay
documentationcenter: node
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e44e4867-3cf3-46be-8f8a-7671e2013bc4
ms.service: service-bus-relay
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: node
ms.workload: na
ms.date: 07/07/2017
ms.author: sethm
ms.openlocfilehash: 235548399570074f7fd160fec28de8d3633625c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-relay-hybrid-connections"></a>Aan de slag met hybride Relay-verbindingen

[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

Deze zelfstudie bevat een inleiding te[Azure Relay hybride verbindingen](relay-what-is-it.md#hybrid-connections), en wordt aangegeven hoe toouse Node.js toocreate een clienttoepassing die verzendt berichten tooa bijbehorende listener-toepassing. 

## <a name="what-will-be-accomplished"></a>Wat wordt bereikt

Omdat voor hybride verbindingen zowel een client- als een serveronderdeel is vereist, maken we in deze zelfstudie twee consoletoepassingen. Hier volgen Hallo stappen:

1. Maak een Relay-naamruimte met behulp van hello Azure-portal.
2. Een hybride verbinding maken, met hello Azure-portal.
3. Een server console toepassing tooreceive berichten schrijven.
4. Een client console toepassing toosend berichten schrijven.

## <a name="prerequisites"></a>Vereisten

1. [Node.js](https://nodejs.org/en/).
2. Een Azure-abonnement.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a>1. Maken van een naamruimte met behulp van hello Azure-portal

Als u al een Relay-naamruimte gemaakt, gaan toohello [een hybride verbinding maken met Azure-portal Hallo](#2-create-a-hybrid-connection-using-the-azure-portal) sectie.

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-hello-azure-portal"></a>2. Een hybride verbinding maken met hello Azure-portal

Als u al een hybride verbinding gemaakt, gaan toohello [maken van een servertoepassing](#3-create-a-server-application-listener) sectie.

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a>3. Een servertoepassing (listener) maken

toolisten en ontvangen van Hallo Relay, wordt er een Node.js-consoletoepassing schrijven.

[!INCLUDE [relay-hybrid-connections-node-get-started-server](../../includes/relay-hybrid-connections-node-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a>4. Een clienttoepassing maken (afzender)

toosend berichten toohello Relay, wordt er een Node.js-consoletoepassing schrijven.

[!INCLUDE [relay-hybrid-connections-node-get-started-client](../../includes/relay-hybrid-connections-node-get-started-client.md)]

## <a name="5-run-hello-applications"></a>5. Hallo-toepassingen uitvoeren

1. Uitvoeren van de servertoepassing Hallo: vanaf een opdrachtprompt te typen Node.js `node listener.js`.
2. Hallo-clienttoepassing uitvoert: vanaf een opdrachtprompt te typen Node.js `node sender.js`, en voer tekst in.
3. Zorg ervoor dat die server Hallo toepassing console uitvoer Hallo tekst die is ingevoerd in de clienttoepassing Hallo.

![actieve-toepassingen](./media/relay-hybrid-connections-node-get-started/running-applications.png)

Gefeliciteerd, u hebt een end-to-endtoepassing met hybride verbindingen gemaakt met behulp van Node.js!

## <a name="next-steps"></a>Volgende stappen:

* [Veelgestelde vragen over Relay](relay-faq.md)
* [Een naamruimte maken](relay-create-namespace-portal.md)
* [Aan de slag met .NET](relay-hybrid-connections-dotnet-get-started.md)
* [Aan de slag met knooppunten](relay-hybrid-connections-node-get-started.md)

