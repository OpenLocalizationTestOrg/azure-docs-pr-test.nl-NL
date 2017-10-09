---
title: aaaLearn toouse Hallo Salesforce-Connector in logic apps | Microsoft Docs
description: Logic apps maken met Azure App service. Hallo Salesforce-Connector biedt een API-toowork met Salesforce-objecten.
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 54fe5af8-7d2a-4da8-94e7-15d029e029bf
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/05/2016
ms.author: mandia; ladocs
ms.openlocfilehash: b14b41fa8a4648b4f0090472dc0f9575bf13a2ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-salesforce-connector"></a><span data-ttu-id="3cb73-104">Aan de slag met Hallo Salesforce-connector</span><span class="sxs-lookup"><span data-stu-id="3cb73-104">Get started with hello Salesforce connector</span></span>
<span data-ttu-id="3cb73-105">Hallo Salesforce-Connector biedt een API-toowork met Salesforce-objecten.</span><span class="sxs-lookup"><span data-stu-id="3cb73-105">hello Salesforce Connector provides an API toowork with Salesforce objects.</span></span>

<span data-ttu-id="3cb73-106">toouse [elke connector](apis-list.md), moet u eerst toocreate een logische app.</span><span class="sxs-lookup"><span data-stu-id="3cb73-106">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="3cb73-107">U kunt aan de slag door [maken van een logische app nu](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="3cb73-107">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toosalesforce-connector"></a><span data-ttu-id="3cb73-108">Verbinding maken met tooSalesforce-connector</span><span class="sxs-lookup"><span data-stu-id="3cb73-108">Connect tooSalesforce connector</span></span>
<span data-ttu-id="3cb73-109">Om uw logische app toegang alle services tot, moet u eerst toocreate een *verbinding* toohello service.</span><span class="sxs-lookup"><span data-stu-id="3cb73-109">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="3cb73-110">Een [verbinding](connectors-overview.md) biedt connectiviteit tussen een logische app en een andere service.</span><span class="sxs-lookup"><span data-stu-id="3cb73-110">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-toosalesforce-connector"></a><span data-ttu-id="3cb73-111">Een verbinding tooSalesforce-connector maken</span><span class="sxs-lookup"><span data-stu-id="3cb73-111">Create a connection tooSalesforce connector</span></span>
> [!INCLUDE [Steps toocreate a connection tooSalesforce Connector](../../includes/connectors-create-api-salesforce.md)]
> 
> 

## <a name="use-a-salesforce-connector-trigger"></a><span data-ttu-id="3cb73-112">Gebruik een trigger Salesforce-connector</span><span class="sxs-lookup"><span data-stu-id="3cb73-112">Use a Salesforce connector trigger</span></span>
<span data-ttu-id="3cb73-113">Een trigger is een gebeurtenis die gebruikt toostart Hallo werkstroom gedefinieerd in een logische app worden kan.</span><span class="sxs-lookup"><span data-stu-id="3cb73-113">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="3cb73-114">[Meer informatie over triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="3cb73-114">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

> [!INCLUDE [Steps toocreate a Salesforce trigger](../../includes/connectors-create-api-salesforce-trigger.md)]
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="3cb73-115">Een voorwaarde toevoegen</span><span class="sxs-lookup"><span data-stu-id="3cb73-115">Add a condition</span></span>
> [!INCLUDE [Steps toocreate a Salesforce condition](../../includes/connectors-create-api-salesforce-condition.md)]
> 
> 

## <a name="use-a-salesforce-connector-action"></a><span data-ttu-id="3cb73-116">Gebruik de actie van een Salesforce-connector</span><span class="sxs-lookup"><span data-stu-id="3cb73-116">Use a Salesforce connector action</span></span>
<span data-ttu-id="3cb73-117">Een actie is een bewerking uitgevoerd door Hallo werkstroom gedefinieerd in een logische app.</span><span class="sxs-lookup"><span data-stu-id="3cb73-117">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="3cb73-118">[Meer informatie over acties](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="3cb73-118">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

> [!INCLUDE [Steps toocreate a Salesforce action](../../includes/connectors-create-api-salesforce-action.md)]
> 
> 

## <a name="connector-specific-details"></a><span data-ttu-id="3cb73-119">Connector-specifieke details</span><span class="sxs-lookup"><span data-stu-id="3cb73-119">Connector-specific details</span></span>

<span data-ttu-id="3cb73-120">Alle triggers en acties die zijn gedefinieerd in swagger Hallo bekijken en ook bekijken in Hallo beperkingen [connector details](/connectors/salesforce/).</span><span class="sxs-lookup"><span data-stu-id="3cb73-120">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/salesforce/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3cb73-121">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3cb73-121">Next steps</span></span>
[<span data-ttu-id="3cb73-122">Een logische app maken</span><span class="sxs-lookup"><span data-stu-id="3cb73-122">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

