---
title: Informatie over het gebruik van de Azure Service Bus-connector in logic apps | Microsoft Docs
description: Logic apps maken met Azure App service. Verbinding maken met Azure Service Bus-berichten te verzenden en ontvangen. U kunt uitvoeren van acties zoals verzenden naar de wachtrij, verzenden naar het onderwerp van de wachtrij ontvangen en ontvangen van het abonnement.
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
ms.openlocfilehash: 1e2ce06f5993280dbdb67121849591e67f7979e9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-azure-service-bus-connector"></a><span data-ttu-id="b55cd-105">Aan de slag met de Azure Service Bus-connector</span><span class="sxs-lookup"><span data-stu-id="b55cd-105">Get started with the Azure Service Bus connector</span></span>
<span data-ttu-id="b55cd-106">Verbinding maken met Azure Service Bus-berichten te verzenden en ontvangen.</span><span class="sxs-lookup"><span data-stu-id="b55cd-106">Connect to Azure Service Bus to send and receive messages.</span></span> <span data-ttu-id="b55cd-107">U kunt uitvoeren van acties zoals verzenden naar de wachtrij, verzenden naar het onderwerp van de wachtrij ontvangen en ontvangen van het abonnement.</span><span class="sxs-lookup"><span data-stu-id="b55cd-107">You can perform actions such as send to queue, send to topic, receive from queue, and receive from subscription.</span></span>

<span data-ttu-id="b55cd-108">Gebruik [elke connector](apis-list.md), moet u eerst een logische app maken.</span><span class="sxs-lookup"><span data-stu-id="b55cd-108">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="b55cd-109">U kunt aan de slag door [maken van een logische app nu](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="b55cd-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-service-bus"></a><span data-ttu-id="b55cd-110">Verbinding maken met Servicebus</span><span class="sxs-lookup"><span data-stu-id="b55cd-110">Connect to Service Bus</span></span>
<span data-ttu-id="b55cd-111">Om uw logische app toegang alle services tot, moet u eerst een verbinding maken met de service.</span><span class="sxs-lookup"><span data-stu-id="b55cd-111">Before your logic app can access any service, you first need to create a connection to the service.</span></span> <span data-ttu-id="b55cd-112">Een [verbinding](connectors-overview.md) biedt connectiviteit tussen een logische app en een andere service.</span><span class="sxs-lookup"><span data-stu-id="b55cd-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

> [!INCLUDE [Steps to create a connection to Azure Service Bus](../../includes/connectors-create-api-servicebus.md)]
> 
> 

## <a name="use-a-service-bus-trigger"></a><span data-ttu-id="b55cd-113">Een Service Bus-trigger te gebruiken</span><span class="sxs-lookup"><span data-stu-id="b55cd-113">Use a Service Bus trigger</span></span>
<span data-ttu-id="b55cd-114">Een trigger is een gebeurtenis die kan worden gebruikt om de werkstroom die is gedefinieerd in een logische app te starten.</span><span class="sxs-lookup"><span data-stu-id="b55cd-114">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="b55cd-115">[Meer informatie over triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="b55cd-115">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps to create a Service Bus trigger](../../includes/connectors-create-api-servicebus-trigger.md)]
> 
> 

## <a name="use-a-service-bus-action"></a><span data-ttu-id="b55cd-116">Gebruik de actie van een Service Bus</span><span class="sxs-lookup"><span data-stu-id="b55cd-116">Use a Service Bus action</span></span>
<span data-ttu-id="b55cd-117">Een actie is een bewerking uitgevoerd door de werkstroom die is gedefinieerd in een logische app.</span><span class="sxs-lookup"><span data-stu-id="b55cd-117">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="b55cd-118">[Meer informatie over acties](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="b55cd-118">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

[!INCLUDE [Steps to create a Service Bus action](../../includes/connectors-create-api-servicebus-action.md)]

## <a name="connector-specific-details"></a><span data-ttu-id="b55cd-119">Connector-specifieke details</span><span class="sxs-lookup"><span data-stu-id="b55cd-119">Connector-specific details</span></span>

<span data-ttu-id="b55cd-120">Alle triggers en acties die zijn gedefinieerd in de swagger bekijken en ziet u ook de beperkingen in de [connector details](/connectors/servicebus/).</span><span class="sxs-lookup"><span data-stu-id="b55cd-120">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/servicebus/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b55cd-121">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b55cd-121">Next steps</span></span>
<span data-ttu-id="b55cd-122">[Een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="b55cd-122">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

