---
title: Informatie over het gebruik van de Salesforce-Connector in logic apps | Microsoft Docs
description: Logic apps maken met Azure App service. De Salesforce-connector biedt een API voor het werken met Salesforce-objecten.
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
ms.openlocfilehash: c2e2efd356382df9404f5c4ed54f24758b2cd22b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-salesforce-connector"></a><span data-ttu-id="aadd9-104">Aan de slag met de Salesforce-connector</span><span class="sxs-lookup"><span data-stu-id="aadd9-104">Get started with the Salesforce connector</span></span>
<span data-ttu-id="aadd9-105">De Salesforce-connector biedt een API voor het werken met Salesforce-objecten.</span><span class="sxs-lookup"><span data-stu-id="aadd9-105">The Salesforce Connector provides an API to work with Salesforce objects.</span></span>

<span data-ttu-id="aadd9-106">Gebruik [elke connector](apis-list.md), moet u eerst een logische app maken.</span><span class="sxs-lookup"><span data-stu-id="aadd9-106">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="aadd9-107">U kunt aan de slag door [maken van een logische app nu](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="aadd9-107">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-salesforce-connector"></a><span data-ttu-id="aadd9-108">Verbinding maken met de Salesforce-connector</span><span class="sxs-lookup"><span data-stu-id="aadd9-108">Connect to Salesforce connector</span></span>
<span data-ttu-id="aadd9-109">Om uw logische app toegang alle services tot, moet u eerst maken een *verbinding* naar de service.</span><span class="sxs-lookup"><span data-stu-id="aadd9-109">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="aadd9-110">Een [verbinding](connectors-overview.md) biedt connectiviteit tussen een logische app en een andere service.</span><span class="sxs-lookup"><span data-stu-id="aadd9-110">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-salesforce-connector"></a><span data-ttu-id="aadd9-111">Maak een verbinding met de Salesforce-connector</span><span class="sxs-lookup"><span data-stu-id="aadd9-111">Create a connection to Salesforce connector</span></span>
> [!INCLUDE [Steps to create a connection to Salesforce Connector](../../includes/connectors-create-api-salesforce.md)]
> 
> 

## <a name="use-a-salesforce-connector-trigger"></a><span data-ttu-id="aadd9-112">Gebruik een trigger Salesforce-connector</span><span class="sxs-lookup"><span data-stu-id="aadd9-112">Use a Salesforce connector trigger</span></span>
<span data-ttu-id="aadd9-113">Een trigger is een gebeurtenis die kan worden gebruikt om de werkstroom die is gedefinieerd in een logische app te starten.</span><span class="sxs-lookup"><span data-stu-id="aadd9-113">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="aadd9-114">[Meer informatie over triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="aadd9-114">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

> [!INCLUDE [Steps to create a Salesforce trigger](../../includes/connectors-create-api-salesforce-trigger.md)]
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="aadd9-115">Een voorwaarde toevoegen</span><span class="sxs-lookup"><span data-stu-id="aadd9-115">Add a condition</span></span>
> [!INCLUDE [Steps to create a Salesforce condition](../../includes/connectors-create-api-salesforce-condition.md)]
> 
> 

## <a name="use-a-salesforce-connector-action"></a><span data-ttu-id="aadd9-116">Gebruik de actie van een Salesforce-connector</span><span class="sxs-lookup"><span data-stu-id="aadd9-116">Use a Salesforce connector action</span></span>
<span data-ttu-id="aadd9-117">Een actie is een bewerking uitgevoerd door de werkstroom die is gedefinieerd in een logische app.</span><span class="sxs-lookup"><span data-stu-id="aadd9-117">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="aadd9-118">[Meer informatie over acties](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="aadd9-118">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

> [!INCLUDE [Steps to create a Salesforce action](../../includes/connectors-create-api-salesforce-action.md)]
> 
> 

## <a name="connector-specific-details"></a><span data-ttu-id="aadd9-119">Connector-specifieke details</span><span class="sxs-lookup"><span data-stu-id="aadd9-119">Connector-specific details</span></span>

<span data-ttu-id="aadd9-120">Alle triggers en acties die zijn gedefinieerd in de swagger bekijken en ziet u ook de beperkingen in de [connector details](/connectors/salesforce/).</span><span class="sxs-lookup"><span data-stu-id="aadd9-120">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/salesforce/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="aadd9-121">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="aadd9-121">Next steps</span></span>
[<span data-ttu-id="aadd9-122">Een logische app maken</span><span class="sxs-lookup"><span data-stu-id="aadd9-122">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

