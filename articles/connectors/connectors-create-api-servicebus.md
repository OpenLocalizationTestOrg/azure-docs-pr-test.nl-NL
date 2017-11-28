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
# <a name="get-started-with-hello-azure-service-bus-connector"></a><span data-ttu-id="46a6e-105">Aan de slag met hello Azure Service Bus-connector</span><span class="sxs-lookup"><span data-stu-id="46a6e-105">Get started with hello Azure Service Bus connector</span></span>
<span data-ttu-id="46a6e-106">Verbinding maken met Service Bus-toosend tooAzure en ontvangen van berichten.</span><span class="sxs-lookup"><span data-stu-id="46a6e-106">Connect tooAzure Service Bus toosend and receive messages.</span></span> <span data-ttu-id="46a6e-107">U kunt uitvoeren van acties zoals verzenden tooqueue, tootopic verzenden van de wachtrij ontvangen en ontvangen van het abonnement.</span><span class="sxs-lookup"><span data-stu-id="46a6e-107">You can perform actions such as send tooqueue, send tootopic, receive from queue, and receive from subscription.</span></span>

<span data-ttu-id="46a6e-108">toouse [elke connector](apis-list.md), moet u eerst toocreate een logische app.</span><span class="sxs-lookup"><span data-stu-id="46a6e-108">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="46a6e-109">U kunt aan de slag door [maken van een logische app nu](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="46a6e-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooservice-bus"></a><span data-ttu-id="46a6e-110">Verbinding maken met tooService Bus</span><span class="sxs-lookup"><span data-stu-id="46a6e-110">Connect tooService Bus</span></span>
<span data-ttu-id="46a6e-111">Om uw logische app toegang alle services tot, moet u eerst een verbinding toohello service toocreate.</span><span class="sxs-lookup"><span data-stu-id="46a6e-111">Before your logic app can access any service, you first need toocreate a connection toohello service.</span></span> <span data-ttu-id="46a6e-112">Een [verbinding](connectors-overview.md) biedt connectiviteit tussen een logische app en een andere service.</span><span class="sxs-lookup"><span data-stu-id="46a6e-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

> [!INCLUDE [Steps toocreate a connection tooAzure Service Bus](../../includes/connectors-create-api-servicebus.md)]
> 
> 

## <a name="use-a-service-bus-trigger"></a><span data-ttu-id="46a6e-113">Een Service Bus-trigger te gebruiken</span><span class="sxs-lookup"><span data-stu-id="46a6e-113">Use a Service Bus trigger</span></span>
<span data-ttu-id="46a6e-114">Een trigger is een gebeurtenis die gebruikt toostart Hallo werkstroom gedefinieerd in een logische app worden kan.</span><span class="sxs-lookup"><span data-stu-id="46a6e-114">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="46a6e-115">[Meer informatie over triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="46a6e-115">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps toocreate a Service Bus trigger](../../includes/connectors-create-api-servicebus-trigger.md)]
> 
> 

## <a name="use-a-service-bus-action"></a><span data-ttu-id="46a6e-116">Gebruik de actie van een Service Bus</span><span class="sxs-lookup"><span data-stu-id="46a6e-116">Use a Service Bus action</span></span>
<span data-ttu-id="46a6e-117">Een actie is een bewerking uitgevoerd door Hallo werkstroom gedefinieerd in een logische app.</span><span class="sxs-lookup"><span data-stu-id="46a6e-117">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="46a6e-118">[Meer informatie over acties](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="46a6e-118">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

[!INCLUDE [Steps toocreate a Service Bus action](../../includes/connectors-create-api-servicebus-action.md)]

## <a name="connector-specific-details"></a><span data-ttu-id="46a6e-119">Connector-specifieke details</span><span class="sxs-lookup"><span data-stu-id="46a6e-119">Connector-specific details</span></span>

<span data-ttu-id="46a6e-120">Alle triggers en acties die zijn gedefinieerd in swagger Hallo bekijken en ook bekijken in Hallo beperkingen [connector details](/connectors/servicebus/).</span><span class="sxs-lookup"><span data-stu-id="46a6e-120">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/servicebus/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="46a6e-121">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="46a6e-121">Next steps</span></span>
<span data-ttu-id="46a6e-122">[Een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="46a6e-122">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

