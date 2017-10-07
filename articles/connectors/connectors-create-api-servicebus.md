---
title: aaaLearn toouse hello Azure Service Bus-connector in uw logische apps | Microsoft Docs
description: Logic apps maken met Azure App service. Verbinding maken met Service Bus-toosend tooAzure en ontvangen van berichten. U kunt uitvoeren van acties zoals verzenden tooqueue, tootopic verzenden van de wachtrij ontvangen en ontvangen van het abonnement.
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d6d14f5f-2126-4e33-808e-41de08e6721f
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/02/2016
ms.author: mandia; ladocs
ms.openlocfilehash: c815ac167c3106ade470ce139d119085558a9497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-azure-service-bus-connector"></a>Aan de slag met hello Azure Service Bus-connector
Verbinding maken met Service Bus-toosend tooAzure en ontvangen van berichten. U kunt uitvoeren van acties zoals verzenden tooqueue, tootopic verzenden van de wachtrij ontvangen en ontvangen van het abonnement.

toouse [elke connector](apis-list.md), moet u eerst toocreate een logische app. U kunt aan de slag door [maken van een logische app nu](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-tooservice-bus"></a>Verbinding maken met tooService Bus
Om uw logische app toegang alle services tot, moet u eerst een verbinding toohello service toocreate. Een [verbinding](connectors-overview.md) biedt connectiviteit tussen een logische app en een andere service.  

> [!INCLUDE [Steps toocreate a connection tooAzure Service Bus](../../includes/connectors-create-api-servicebus.md)]
> 
> 

## <a name="use-a-service-bus-trigger"></a>Een Service Bus-trigger te gebruiken
Een trigger is een gebeurtenis die gebruikt toostart Hallo werkstroom gedefinieerd in een logische app worden kan. [Meer informatie over triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

> [!INCLUDE [Steps toocreate a Service Bus trigger](../../includes/connectors-create-api-servicebus-trigger.md)]
> 
> 

## <a name="use-a-service-bus-action"></a>Gebruik de actie van een Service Bus
Een actie is een bewerking uitgevoerd door Hallo werkstroom gedefinieerd in een logische app. [Meer informatie over acties](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

[!INCLUDE [Steps toocreate a Service Bus action](../../includes/connectors-create-api-servicebus-action.md)]

## <a name="connector-specific-details"></a>Connector-specifieke details

Alle triggers en acties die zijn gedefinieerd in swagger Hallo bekijken en ook bekijken in Hallo beperkingen [connector details](/connectors/servicebus/). 

## <a name="next-steps"></a>Volgende stappen
[Een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).

