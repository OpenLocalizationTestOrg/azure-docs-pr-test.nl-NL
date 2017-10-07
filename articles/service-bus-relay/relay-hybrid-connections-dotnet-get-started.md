---
title: aaaGet de slag met Azure Relay hybride verbindingen in .NET | Microsoft Docs
description: Een consoletoepassing in C# schrijven voor hybride Relay-verbindingen van Azure.
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: d1386900-b942-4abf-acfc-38d2ef826253
ms.service: service-bus-relay
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 07/07/2017
ms.author: sethm
ms.openlocfilehash: 1e4af28e7cd4393c8ca965a149a0b83ebcc44f22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-relay-hybrid-connections"></a>Aan de slag met hybride Relay-verbindingen
[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

Deze zelfstudie bevat een inleiding te[Azure Relay hybride verbindingen](relay-what-is-it.md#hybrid-connections), en wordt aangegeven hoe toouse .NET toocreate een clienttoepassing die verzendt berichten tooa bijbehorende listener-toepassing. 

## <a name="what-will-be-accomplished"></a>Wat wordt bereikt
Omdat voor hybride verbindingen vereist zowel een client en een serveronderdeel, maakt Hallo zelfstudie twee consoletoepassingen. Hier volgen Hallo stappen:

1. Maak een Relay-naamruimte met behulp van hello Azure-portal.
2. Een hybride verbinding maken in waarmee de naamruimte, met behulp van hello Azure-portal.
3. Een (listener) serverconsole tooreceive toepassingsberichten schrijven.
4. Schrijven van een console-client (afzender) toosend toepassingsberichten.

## <a name="prerequisites"></a>Vereisten

toocomplete in deze zelfstudie, moet u Hallo volgende vereisten:

1. [Visual Studio 2015 of hoger](http://www.visualstudio.com). Hallo-voorbeelden in deze zelfstudie gebruikt Visual Studio 2017.
2. Een Azure-abonnement.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a>1. Maken van een naamruimte met behulp van hello Azure-portal
Als u al een Relay-naamruimte hebt gemaakt, gaan toohello [een hybride verbinding maken met Azure-portal Hallo](#2-create-a-hybrid-connection-using-the-azure-portal) sectie.

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-hello-azure-portal"></a>2. Een hybride verbinding maken met hello Azure-portal
Als u al een hybride verbinding hebt gemaakt, gaan toohello [maken van een servertoepassing](#3-create-a-server-application-listener) sectie.

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a>3. Een servertoepassing (listener) maken
toolisten en ontvangen van berichten van Hallo Relay, we een C#-consoletoepassing met Visual Studio worden geschreven.

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-server](../../includes/relay-hybrid-connections-dotnet-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a>4. Een clienttoepassing maken (afzender)
toosend berichten toohello sturen we een C#-consoletoepassing met Visual Studio worden geschreven.

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-client](../../includes/relay-hybrid-connections-dotnet-get-started-client.md)]

## <a name="5-run-hello-applications"></a>5. Hallo-toepassingen uitvoeren
1. Hallo-servertoepassing wordt uitgevoerd.
2. Voer Hallo-clienttoepassing en tekst opgeven.
3. Zorg ervoor dat die server Hallo toepassing console uitvoer Hallo tekst die is ingevoerd in de clienttoepassing Hallo.

![actieve-toepassingen](./media/relay-hybrid-connections-dotnet-get-started/running-applications.png)

Gefeliciteerd, u hebt een end-to-end toepassing met hybride verbindingen gemaakt.

## <a name="next-steps"></a>Volgende stappen:
* [Veelgestelde vragen over Relay](relay-faq.md)
* [Een naamruimte maken](relay-create-namespace-portal.md)
* [Aan de slag met knooppunten](relay-hybrid-connections-node-get-started.md)

