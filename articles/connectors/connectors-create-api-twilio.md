---
title: De Twilio-Connector in Azure Logic apps toevoegen | Microsoft Docs
description: Overzicht van de Twilio Connector met parameters van de REST-API
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
ms.openlocfilehash: a790ac51b0fea7e3fa379d20e0e094e7ce0d7696
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-twilio-connector"></a><span data-ttu-id="70dfe-103">Aan de slag met de Twilio-connector</span><span class="sxs-lookup"><span data-stu-id="70dfe-103">Get started with the Twilio connector</span></span>
<span data-ttu-id="70dfe-104">Verbinding maken met Twilio globale SMS, MMS en IP-berichten te verzenden en ontvangen.</span><span class="sxs-lookup"><span data-stu-id="70dfe-104">Connect to Twilio to send and receive global SMS, MMS, and IP messages.</span></span> <span data-ttu-id="70dfe-105">Met Twilio, kunt u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="70dfe-105">With Twilio, you can:</span></span>

* <span data-ttu-id="70dfe-106">Bouw uw zakelijke flow op basis van de gegevens die u van Twilio krijgt.</span><span class="sxs-lookup"><span data-stu-id="70dfe-106">Build your business flow based on the data you get from Twilio.</span></span> 
* <span data-ttu-id="70dfe-107">Acties als er een bericht en lijst berichten gebruiken.</span><span class="sxs-lookup"><span data-stu-id="70dfe-107">Use actions that get a message, list messages, and more.</span></span> <span data-ttu-id="70dfe-108">Deze acties reageert en vervolgens de uitvoer beschikbaar maken voor andere acties.</span><span class="sxs-lookup"><span data-stu-id="70dfe-108">These actions get a response, and then make the output available for other actions.</span></span> <span data-ttu-id="70dfe-109">Bijvoorbeeld, wanneer u een nieuwe Twilio-bericht ontvangt, kunt u nemen dit bericht en een Service Bus-werkstroom.</span><span class="sxs-lookup"><span data-stu-id="70dfe-109">For example, when  you get a new Twilio message, you can take this message and use it a Service Bus workflow.</span></span> 

<span data-ttu-id="70dfe-110">Aan de slag door het maken van een logische app; Zie [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="70dfe-110">Get started by creating a logic app; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-twilio"></a><span data-ttu-id="70dfe-111">Maak een verbinding met Twilio</span><span class="sxs-lookup"><span data-stu-id="70dfe-111">Create a connection to Twilio</span></span>
<span data-ttu-id="70dfe-112">Wanneer u deze Connector aan uw logische apps toevoegen, typt u de volgende Twilio-waarden:</span><span class="sxs-lookup"><span data-stu-id="70dfe-112">When you add this Connector to your logic apps, enter the following Twilio values:</span></span>

| <span data-ttu-id="70dfe-113">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="70dfe-113">Property</span></span> | <span data-ttu-id="70dfe-114">Vereist</span><span class="sxs-lookup"><span data-stu-id="70dfe-114">Required</span></span> | <span data-ttu-id="70dfe-115">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="70dfe-115">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="70dfe-116">Account-ID</span><span class="sxs-lookup"><span data-stu-id="70dfe-116">Account ID</span></span> |<span data-ttu-id="70dfe-117">Ja</span><span class="sxs-lookup"><span data-stu-id="70dfe-117">Yes</span></span> |<span data-ttu-id="70dfe-118">Voer uw Twilio-account-ID</span><span class="sxs-lookup"><span data-stu-id="70dfe-118">Enter your Twilio account ID</span></span> |
| <span data-ttu-id="70dfe-119">Toegangstoken</span><span class="sxs-lookup"><span data-stu-id="70dfe-119">Access Token</span></span> |<span data-ttu-id="70dfe-120">Ja</span><span class="sxs-lookup"><span data-stu-id="70dfe-120">Yes</span></span> |<span data-ttu-id="70dfe-121">Voer uw Twilio-toegangstoken</span><span class="sxs-lookup"><span data-stu-id="70dfe-121">Enter your Twilio access token</span></span> |

> [!INCLUDE [Steps to create a connection to Twilio](../../includes/connectors-create-api-twilio.md)]
> 
> 

<span data-ttu-id="70dfe-122">Als u een toegangstoken Twilio hebt, raadpleegt u [gebruikersidentiteit & toegangstokens](https://www.twilio.com/docs/api/chat/guides/identity).</span><span class="sxs-lookup"><span data-stu-id="70dfe-122">If you don't have a Twilio access token, see [User Identity & Access Tokens](https://www.twilio.com/docs/api/chat/guides/identity).</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="70dfe-123">Connector-specifieke details</span><span class="sxs-lookup"><span data-stu-id="70dfe-123">Connector-specific details</span></span>

<span data-ttu-id="70dfe-124">Alle triggers en acties die zijn gedefinieerd in de swagger bekijken en ziet u ook de beperkingen in de [connector details](/connectors/twilio/).</span><span class="sxs-lookup"><span data-stu-id="70dfe-124">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/twilio/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="70dfe-125">Meer connectors</span><span class="sxs-lookup"><span data-stu-id="70dfe-125">More connectors</span></span>
<span data-ttu-id="70dfe-126">Ga terug naar de [API's lijst](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="70dfe-126">Go back to the [APIs list](apis-list.md).</span></span>