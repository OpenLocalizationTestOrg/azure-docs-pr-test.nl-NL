---
title: GitHub-connector in Azure Logic Apps | Microsoft Docs
description: Logic apps maken met Azure App service. GitHub is een webgebaseerde Git-opslagplaats die service host. Biedt alle gedistribueerde revisie besturingselement en gegevensbron code management (SCM) functionaliteit Git, evenals van zijn eigen functies toe te voegen.
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 8f873e6c-f4c0-4c2e-a5bd-2e953efe5e2b
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: d4614b0ceff0ec0d36dbb1a136551f985f2fc1a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-github-connector"></a><span data-ttu-id="0c6c5-105">Aan de slag met de GitHub-connector</span><span class="sxs-lookup"><span data-stu-id="0c6c5-105">Get started with the GitHub connector</span></span>
<span data-ttu-id="0c6c5-106">GitHub is een webgebaseerde Git-opslagplaats die service host.</span><span class="sxs-lookup"><span data-stu-id="0c6c5-106">GitHub is a web-based Git repository hosting service.</span></span> <span data-ttu-id="0c6c5-107">Biedt alle gedistribueerde revisie besturingselement en gegevensbron code management (SCM) functionaliteit Git, evenals van zijn eigen functies toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="0c6c5-107">It offers all of the distributed revision control and source code management (SCM) functionality of Git as well as adding its own features.</span></span>

<span data-ttu-id="0c6c5-108">U kunt aan de slag door het maken van een logische app nu, Zie [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="0c6c5-108">You can get started by creating a Logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-github"></a><span data-ttu-id="0c6c5-109">Maak een verbinding met GitHub</span><span class="sxs-lookup"><span data-stu-id="0c6c5-109">Create a connection to GitHub</span></span>
<span data-ttu-id="0c6c5-110">Logische apps maakt met GitHub, moet u eerst maken een **verbinding** Geef vervolgens de details voor de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="0c6c5-110">To create Logic apps with GitHub, you must first create a **connection** then provide the details for the following properties:</span></span> 

| <span data-ttu-id="0c6c5-111">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="0c6c5-111">Property</span></span> | <span data-ttu-id="0c6c5-112">Vereist</span><span class="sxs-lookup"><span data-stu-id="0c6c5-112">Required</span></span> | <span data-ttu-id="0c6c5-113">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0c6c5-113">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0c6c5-114">Token</span><span class="sxs-lookup"><span data-stu-id="0c6c5-114">Token</span></span> |<span data-ttu-id="0c6c5-115">Ja</span><span class="sxs-lookup"><span data-stu-id="0c6c5-115">Yes</span></span> |<span data-ttu-id="0c6c5-116">Geef referenties op GitHub</span><span class="sxs-lookup"><span data-stu-id="0c6c5-116">Provide GitHub Credentials</span></span> |

<span data-ttu-id="0c6c5-117">Nadat u de verbinding hebt gemaakt, kunt u het uitvoeren van de acties te luisteren voor de triggers die in dit artikel wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="0c6c5-117">After you create the connection, you can use it to execute the actions and listen for the triggers described in this article.</span></span> 

> [!INCLUDE [Steps to create a connection to GitHub](../../includes/connectors-create-api-github.md)]
> 

## <a name="connector-specific-details"></a><span data-ttu-id="0c6c5-118">Connector-specifieke details</span><span class="sxs-lookup"><span data-stu-id="0c6c5-118">Connector-specific details</span></span>

<span data-ttu-id="0c6c5-119">Alle triggers en acties die zijn gedefinieerd in de swagger bekijken en ziet u ook de beperkingen in de [connector details](/connectors/github/).</span><span class="sxs-lookup"><span data-stu-id="0c6c5-119">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/github/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="0c6c5-120">Meer connectors</span><span class="sxs-lookup"><span data-stu-id="0c6c5-120">More connectors</span></span>
<span data-ttu-id="0c6c5-121">Ga terug naar de [API's lijst](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="0c6c5-121">Go back to the [APIs list](apis-list.md).</span></span>