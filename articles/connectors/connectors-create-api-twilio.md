---
title: aaaAdd hello Twilio-Connector in uw Azure Logic apps | Microsoft Docs
description: Overzicht van Hallo Twilio-Connector met de parameters van de REST-API
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 43116187-4a2f-42e5-9852-a0d62f08c5fc
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 09/19/2016
ms.author: mandia; ladocs
ms.openlocfilehash: b2b487f34bc76bee24b4237a71ee767d0d22ff7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-twilio-connector"></a>Aan de slag met Hallo Twilio-connector
Verbind tooTwilio toosend en globale SMS, MMS en IP-berichten ontvangen. Met Twilio, kunt u het volgende doen:

* Bouw uw zakelijke flow op basis van Hallo gegevens die u via Twilio krijgen. 
* Acties als er een bericht en lijst berichten gebruiken. Deze acties reageert en breng Hallo uitvoer beschikbaar voor andere acties. Bijvoorbeeld, wanneer u een nieuwe Twilio-bericht ontvangt, kunt u nemen dit bericht en een Service Bus-werkstroom. 

Aan de slag door het maken van een logische app; Zie [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="create-a-connection-tootwilio"></a>Een tooTwilio verbinding maken
Wanneer u deze Connector tooyour logische apps toevoegt, Voer Hallo Twilio waarden te volgen:

| Eigenschap | Vereist | Beschrijving |
| --- | --- | --- |
| Account-ID |Ja |Voer uw Twilio-account-ID |
| Toegangstoken |Ja |Voer uw Twilio-toegangstoken |

> [!INCLUDE [Steps toocreate a connection tooTwilio](../../includes/connectors-create-api-twilio.md)]
> 
> 

Als u een toegangstoken Twilio hebt, raadpleegt u [gebruikersidentiteit & toegangstokens](https://www.twilio.com/docs/api/chat/guides/identity).

## <a name="connector-specific-details"></a>Connector-specifieke details

Alle triggers en acties die zijn gedefinieerd in swagger Hallo bekijken en ook bekijken in Hallo beperkingen [connector details](/connectors/twilio/).

## <a name="more-connectors"></a>Meer connectors
Ga terug toohello [API's lijst](apis-list.md).
