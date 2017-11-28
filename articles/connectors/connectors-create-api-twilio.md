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
# <a name="get-started-with-hello-twilio-connector"></a><span data-ttu-id="563f4-103">Aan de slag met Hallo Twilio-connector</span><span class="sxs-lookup"><span data-stu-id="563f4-103">Get started with hello Twilio connector</span></span>
<span data-ttu-id="563f4-104">Verbind tooTwilio toosend en globale SMS, MMS en IP-berichten ontvangen.</span><span class="sxs-lookup"><span data-stu-id="563f4-104">Connect tooTwilio toosend and receive global SMS, MMS, and IP messages.</span></span> <span data-ttu-id="563f4-105">Met Twilio, kunt u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="563f4-105">With Twilio, you can:</span></span>

* <span data-ttu-id="563f4-106">Bouw uw zakelijke flow op basis van Hallo gegevens die u via Twilio krijgen.</span><span class="sxs-lookup"><span data-stu-id="563f4-106">Build your business flow based on hello data you get from Twilio.</span></span> 
* <span data-ttu-id="563f4-107">Acties als er een bericht en lijst berichten gebruiken.</span><span class="sxs-lookup"><span data-stu-id="563f4-107">Use actions that get a message, list messages, and more.</span></span> <span data-ttu-id="563f4-108">Deze acties reageert en breng Hallo uitvoer beschikbaar voor andere acties.</span><span class="sxs-lookup"><span data-stu-id="563f4-108">These actions get a response, and then make hello output available for other actions.</span></span> <span data-ttu-id="563f4-109">Bijvoorbeeld, wanneer u een nieuwe Twilio-bericht ontvangt, kunt u nemen dit bericht en een Service Bus-werkstroom.</span><span class="sxs-lookup"><span data-stu-id="563f4-109">For example, when  you get a new Twilio message, you can take this message and use it a Service Bus workflow.</span></span> 

<span data-ttu-id="563f4-110">Aan de slag door het maken van een logische app; Zie [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="563f4-110">Get started by creating a logic app; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-tootwilio"></a><span data-ttu-id="563f4-111">Een tooTwilio verbinding maken</span><span class="sxs-lookup"><span data-stu-id="563f4-111">Create a connection tooTwilio</span></span>
<span data-ttu-id="563f4-112">Wanneer u deze Connector tooyour logische apps toevoegt, Voer Hallo Twilio waarden te volgen:</span><span class="sxs-lookup"><span data-stu-id="563f4-112">When you add this Connector tooyour logic apps, enter hello following Twilio values:</span></span>

| <span data-ttu-id="563f4-113">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="563f4-113">Property</span></span> | <span data-ttu-id="563f4-114">Vereist</span><span class="sxs-lookup"><span data-stu-id="563f4-114">Required</span></span> | <span data-ttu-id="563f4-115">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="563f4-115">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="563f4-116">Account-ID</span><span class="sxs-lookup"><span data-stu-id="563f4-116">Account ID</span></span> |<span data-ttu-id="563f4-117">Ja</span><span class="sxs-lookup"><span data-stu-id="563f4-117">Yes</span></span> |<span data-ttu-id="563f4-118">Voer uw Twilio-account-ID</span><span class="sxs-lookup"><span data-stu-id="563f4-118">Enter your Twilio account ID</span></span> |
| <span data-ttu-id="563f4-119">Toegangstoken</span><span class="sxs-lookup"><span data-stu-id="563f4-119">Access Token</span></span> |<span data-ttu-id="563f4-120">Ja</span><span class="sxs-lookup"><span data-stu-id="563f4-120">Yes</span></span> |<span data-ttu-id="563f4-121">Voer uw Twilio-toegangstoken</span><span class="sxs-lookup"><span data-stu-id="563f4-121">Enter your Twilio access token</span></span> |

> [!INCLUDE [Steps toocreate a connection tooTwilio](../../includes/connectors-create-api-twilio.md)]
> 
> 

<span data-ttu-id="563f4-122">Als u een toegangstoken Twilio hebt, raadpleegt u [gebruikersidentiteit & toegangstokens](https://www.twilio.com/docs/api/chat/guides/identity).</span><span class="sxs-lookup"><span data-stu-id="563f4-122">If you don't have a Twilio access token, see [User Identity & Access Tokens](https://www.twilio.com/docs/api/chat/guides/identity).</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="563f4-123">Connector-specifieke details</span><span class="sxs-lookup"><span data-stu-id="563f4-123">Connector-specific details</span></span>

<span data-ttu-id="563f4-124">Alle triggers en acties die zijn gedefinieerd in swagger Hallo bekijken en ook bekijken in Hallo beperkingen [connector details](/connectors/twilio/).</span><span class="sxs-lookup"><span data-stu-id="563f4-124">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/twilio/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="563f4-125">Meer connectors</span><span class="sxs-lookup"><span data-stu-id="563f4-125">More connectors</span></span>
<span data-ttu-id="563f4-126">Ga terug toohello [API's lijst](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="563f4-126">Go back toohello [APIs list](apis-list.md).</span></span>
