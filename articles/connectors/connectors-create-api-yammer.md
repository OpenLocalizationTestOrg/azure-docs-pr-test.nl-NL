---
title: De Connector Yammer in Azure Logic Apps toevoegen | Microsoft Docs
description: Overzicht van de Connector Yammer met parameters van de REST-API
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b5ae0827-fbb3-45ec-8f45-ad1cc2e7eccc
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: c7a213343b4fb2b5a89a5052a459061b404a431c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-yammer-connector"></a><span data-ttu-id="2c1bf-103">Aan de slag met de Yammer-connector</span><span class="sxs-lookup"><span data-stu-id="2c1bf-103">Get started with the Yammer connector</span></span>
<span data-ttu-id="2c1bf-104">Verbinding maken met Yammer aan gesprekken toegang in uw bedrijfsnetwerk.</span><span class="sxs-lookup"><span data-stu-id="2c1bf-104">Connect to Yammer to access conversations in your enterprise network.</span></span> <span data-ttu-id="2c1bf-105">Met Yammer, kunt u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="2c1bf-105">With Yammer, you can:</span></span>

* <span data-ttu-id="2c1bf-106">Bouw uw zakelijke flow op basis van de gegevens die u met Yammer.</span><span class="sxs-lookup"><span data-stu-id="2c1bf-106">Build your business flow based on the data you get from Yammer.</span></span> 
* <span data-ttu-id="2c1bf-107">Gebruik voor wordt geactiveerd wanneer er een nieuw bericht in een groep of een feed uw volgende.</span><span class="sxs-lookup"><span data-stu-id="2c1bf-107">Use triggers for when there is a new message in a group, or a feed your following.</span></span>
* <span data-ttu-id="2c1bf-108">Acties gebruiken om een bericht plaatsen, alle berichten en meer te vinden.</span><span class="sxs-lookup"><span data-stu-id="2c1bf-108">Use actions to post a message, get all messages, and more.</span></span> <span data-ttu-id="2c1bf-109">Deze acties reageert en vervolgens de uitvoer beschikbaar maken voor andere acties.</span><span class="sxs-lookup"><span data-stu-id="2c1bf-109">These actions get a response, and then make the output available for other actions.</span></span> <span data-ttu-id="2c1bf-110">Wanneer een nieuw bericht wordt weergegeven, kunt u bijvoorbeeld een e-mailbericht met Office 365 verzenden.</span><span class="sxs-lookup"><span data-stu-id="2c1bf-110">For example, when a new message appears, you can send an email using Office 365.</span></span>

<span data-ttu-id="2c1bf-111">Aan de slag door het maken van een logische app nu; Zie [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="2c1bf-111">Get started by creating a logic app now; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-yammer"></a><span data-ttu-id="2c1bf-112">Maak een verbinding met Yammer</span><span class="sxs-lookup"><span data-stu-id="2c1bf-112">Create a connection to Yammer</span></span>
<span data-ttu-id="2c1bf-113">Voor het gebruik van de Yammer-connector maakt u eerst een **verbinding** Geef vervolgens de details voor deze eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="2c1bf-113">To use the Yammer connector, you first create a **connection** then provide the details for these properties:</span></span> 

| <span data-ttu-id="2c1bf-114">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="2c1bf-114">Property</span></span> | <span data-ttu-id="2c1bf-115">Vereist</span><span class="sxs-lookup"><span data-stu-id="2c1bf-115">Required</span></span> | <span data-ttu-id="2c1bf-116">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="2c1bf-116">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2c1bf-117">Token</span><span class="sxs-lookup"><span data-stu-id="2c1bf-117">Token</span></span> |<span data-ttu-id="2c1bf-118">Ja</span><span class="sxs-lookup"><span data-stu-id="2c1bf-118">Yes</span></span> |<span data-ttu-id="2c1bf-119">Geef referenties op Yammer</span><span class="sxs-lookup"><span data-stu-id="2c1bf-119">Provide Yammer Credentials</span></span> |

> [!INCLUDE [Steps to create a connection to Yammer](../../includes/connectors-create-api-yammer.md)]
> 

## <a name="connector-specific-details"></a><span data-ttu-id="2c1bf-120">Connector-specifieke details</span><span class="sxs-lookup"><span data-stu-id="2c1bf-120">Connector-specific details</span></span>

<span data-ttu-id="2c1bf-121">Alle triggers en acties die zijn gedefinieerd in de swagger bekijken en ziet u ook de beperkingen in de [connector details](/connectors/yammer/).</span><span class="sxs-lookup"><span data-stu-id="2c1bf-121">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/yammer/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="2c1bf-122">Meer connectors</span><span class="sxs-lookup"><span data-stu-id="2c1bf-122">More connectors</span></span>
<span data-ttu-id="2c1bf-123">Ga terug naar de [API's lijst](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="2c1bf-123">Go back to the [APIs list](apis-list.md).</span></span>