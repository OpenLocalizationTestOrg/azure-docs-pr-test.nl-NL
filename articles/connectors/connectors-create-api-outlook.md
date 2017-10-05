---
title: Outlook.com-connector in Azure Logic Apps | Microsoft Docs
description: Logic apps maken met Azure App service. Outlook.com-connector kunt u uw e-mail, agenda en contactpersonen beheren. U kunt uitvoeren van verschillende acties zoals e-mail verzenden, vergaderingen plannen, Voeg contactpersonen, enzovoort.
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 87113c85-d158-4dd5-9ed5-5748130003d6
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: bde1629504c97cf6706b42219570ffa6243073dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-outlookcom-connector"></a><span data-ttu-id="c64e9-105">Aan de slag met de Outlook.com-connector</span><span class="sxs-lookup"><span data-stu-id="c64e9-105">Get started with the Outlook.com connector</span></span>
<span data-ttu-id="c64e9-106">Outlook.com-connector kunt u uw e-mail, agenda en contactpersonen beheren.</span><span class="sxs-lookup"><span data-stu-id="c64e9-106">Outlook.com connector allows you to manage your mail, calendars, and contacts.</span></span> <span data-ttu-id="c64e9-107">U kunt uitvoeren van verschillende acties zoals e-mail verzenden, vergaderingen plannen, Voeg contactpersonen, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="c64e9-107">You can perform various actions such as send mail, schedule meetings, add contacts, etc.</span></span>

<span data-ttu-id="c64e9-108">U kunt aan de slag door het maken van een logische app nu, Zie [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="c64e9-108">You can get started by creating a Logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-outlookcom"></a><span data-ttu-id="c64e9-109">Maak een verbinding met Outlook.com</span><span class="sxs-lookup"><span data-stu-id="c64e9-109">Create a connection to Outlook.com</span></span>
<span data-ttu-id="c64e9-110">Logic apps maken met Outlook.com, moet u eerst maken een **verbinding** Geef vervolgens de details voor de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="c64e9-110">To create Logic apps with Outlook.com, you must first create a **connection** then provide the details for the following properties:</span></span>

| <span data-ttu-id="c64e9-111">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="c64e9-111">Property</span></span> | <span data-ttu-id="c64e9-112">Vereist</span><span class="sxs-lookup"><span data-stu-id="c64e9-112">Required</span></span> | <span data-ttu-id="c64e9-113">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c64e9-113">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c64e9-114">Token</span><span class="sxs-lookup"><span data-stu-id="c64e9-114">Token</span></span> |<span data-ttu-id="c64e9-115">Ja</span><span class="sxs-lookup"><span data-stu-id="c64e9-115">Yes</span></span> |<span data-ttu-id="c64e9-116">Geef referenties op Outlook.com</span><span class="sxs-lookup"><span data-stu-id="c64e9-116">Provide Outlook.com Credentials</span></span> |

<span data-ttu-id="c64e9-117">Nadat u de verbinding hebt gemaakt, kunt u het uitvoeren van de acties te luisteren voor de triggers die in dit artikel wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="c64e9-117">After you create the connection, you can use it to execute the actions and listen for the triggers described in this article.</span></span>

> [!INCLUDE [Steps to create a connection to Outlook.com](../../includes/connectors-create-api-outlook.md)]
>

## <a name="connector-specific-details"></a><span data-ttu-id="c64e9-118">Connector-specifieke details</span><span class="sxs-lookup"><span data-stu-id="c64e9-118">Connector-specific details</span></span>

<span data-ttu-id="c64e9-119">Alle triggers en acties die zijn gedefinieerd in de swagger bekijken en ziet u ook de beperkingen in de [connector details](/connectors/outlook/).</span><span class="sxs-lookup"><span data-stu-id="c64e9-119">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/outlook/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="c64e9-120">Meer connectors</span><span class="sxs-lookup"><span data-stu-id="c64e9-120">More connectors</span></span>
<span data-ttu-id="c64e9-121">Ga terug naar de [API's lijst](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="c64e9-121">Go back to the [APIs list](apis-list.md).</span></span>