---
title: Logic Apps B2B edifact decoderen oplossen UNH2.5 - Azure Logic Apps | Microsoft Docs
description: Azure Logic Apps B2B edifact decoderen oplossen UNH2.5
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 62ad8183cc6e9f56255b2729a04ee7710d00a21a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-handle-edifact-documents-having-unh25-segment"></a><span data-ttu-id="8e405-103">Hoe moet worden verwerkt EDIFACT documenten UNH2.5 segment</span><span class="sxs-lookup"><span data-stu-id="8e405-103">How to handle EDIFACT documents having UNH2.5 segment</span></span>
<span data-ttu-id="8e405-104">Wanneer UNH2.5 aanwezig in het document EDIFACT is, wordt deze gebruikt voor het opzoeken van het schema.</span><span class="sxs-lookup"><span data-stu-id="8e405-104">When UNH2.5 is present in the EDIFACT document, it is being used for schema lookup.</span></span> 

<span data-ttu-id="8e405-105">Voorbeeld: Het veld UNH is **EAN008** in het bericht EDIFACT</span><span class="sxs-lookup"><span data-stu-id="8e405-105">Example: The UNH field is **EAN008** in the EDIFACT message</span></span>  
<span data-ttu-id="8e405-106">UNH + SSDD1 + ORDERS: D: 03B: ONGEDAAN MAKEN:**EAN008**'</span><span class="sxs-lookup"><span data-stu-id="8e405-106">UNH+SSDD1+ORDERS:D:03B:UN:**EAN008**'</span></span>  

<span data-ttu-id="8e405-107">Stappen voor het afhandelen van het bericht</span><span class="sxs-lookup"><span data-stu-id="8e405-107">Steps to follow to handle the message</span></span> 
1. <span data-ttu-id="8e405-108">Het schema bijwerken</span><span class="sxs-lookup"><span data-stu-id="8e405-108">Update the schema</span></span>
2. <span data-ttu-id="8e405-109">Controleer de instellingen van de overeenkomst</span><span class="sxs-lookup"><span data-stu-id="8e405-109">Check the agreement settings</span></span>  

## <a name="update-the-schema"></a><span data-ttu-id="8e405-110">Het schema bijwerken</span><span class="sxs-lookup"><span data-stu-id="8e405-110">Update the schema</span></span>
<span data-ttu-id="8e405-111">Voor het verwerken van het bericht, moet u een schema met de naam UNH2.5 hoofdknooppunt implementeren.</span><span class="sxs-lookup"><span data-stu-id="8e405-111">To process the message, you need to deploy a schema with the UNH2.5 root node name.</span></span>  <span data-ttu-id="8e405-112">Voor een voorbeeld gegeven, zijn de naam van het schema-hoofdmap **EFACT_D03B_ORDERS_EAN008**</span><span class="sxs-lookup"><span data-stu-id="8e405-112">For given an example, the schema root name would be **EFACT_D03B_ORDERS_EAN008**</span></span>  

<span data-ttu-id="8e405-113">Voor elke D03B_ORDERS met een andere UNH2.5 segment, zou u moet een afzonderlijk schema implementeren.</span><span class="sxs-lookup"><span data-stu-id="8e405-113">For each D03B_ORDERS with a different UNH2.5 segment, you would have to deploy an individual schema.</span></span>  

## <a name="add-schema-to-the-edifact-agreement"></a><span data-ttu-id="8e405-114">Schema niet toevoegen aan de overeenkomst EDIFACT</span><span class="sxs-lookup"><span data-stu-id="8e405-114">Add schema to the EDIFACT agreement</span></span>
### <a name="edifact-decode"></a><span data-ttu-id="8e405-115">EDIFACT decoderen</span><span class="sxs-lookup"><span data-stu-id="8e405-115">EDIFACT Decode</span></span>
<span data-ttu-id="8e405-116">Het schema configureren voor het decoderen van het binnenkomende bericht in de EDIFACT ontvangen overeenkomst instellingen</span><span class="sxs-lookup"><span data-stu-id="8e405-116">To Decode the incoming message, configure the schema in the EDIFACT agreement receive settings</span></span>
1. <span data-ttu-id="8e405-117">Het schema niet toevoegen aan de integratie-account</span><span class="sxs-lookup"><span data-stu-id="8e405-117">Add the schema to the integration account</span></span>    
2. <span data-ttu-id="8e405-118">Het schema te configureren in de EDIFACT ontvangen overeenkomst instellingen.</span><span class="sxs-lookup"><span data-stu-id="8e405-118">Configure the schema in the EDIFACT agreement receive settings.</span></span> 
3. <span data-ttu-id="8e405-119">Selecteer EDIFACT overeenkomst en klik op **bewerken als JSON**.</span><span class="sxs-lookup"><span data-stu-id="8e405-119">Select EDIFACT agreement and click **Edit as JSON**.</span></span>  <span data-ttu-id="8e405-120">UNH2.5 waarde toevoegen in de overeenkomst ontvangen **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png)</span><span class="sxs-lookup"><span data-stu-id="8e405-120">Add UNH2.5 value in the Receive Agreement **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png)</span></span>

### <a name="edifact-encode"></a><span data-ttu-id="8e405-121">EDIFACT coderen</span><span class="sxs-lookup"><span data-stu-id="8e405-121">EDIFACT Encode</span></span>
<span data-ttu-id="8e405-122">Het schema voor het coderen van het binnenkomende bericht configureren in de instellingen voor EDIFACT overeenkomst verzenden</span><span class="sxs-lookup"><span data-stu-id="8e405-122">To Encode the incoming message, configure the schema in the EDIFACT agreement send settings</span></span>
1. <span data-ttu-id="8e405-123">Het schema niet toevoegen aan de integratie-account</span><span class="sxs-lookup"><span data-stu-id="8e405-123">Add the schema to the integration account</span></span>    
2. <span data-ttu-id="8e405-124">Configureer het schema in de instellingen voor EDIFACT overeenkomst verzenden.</span><span class="sxs-lookup"><span data-stu-id="8e405-124">Configure the schema in the EDIFACT agreement send settings.</span></span> 
3. <span data-ttu-id="8e405-125">Selecteer EDIFACT overeenkomst en klik op **bewerken als JSON**.</span><span class="sxs-lookup"><span data-stu-id="8e405-125">Select EDIFACT agreement and click **Edit as JSON**.</span></span>  <span data-ttu-id="8e405-126">UNH2.5 waarde toevoegen in de overeenkomst verzenden **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)</span><span class="sxs-lookup"><span data-stu-id="8e405-126">Add UNH2.5 value in the Send Agreement **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e405-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8e405-127">Next Steps</span></span>
* [<span data-ttu-id="8e405-128">Meer informatie over de integratie account overeenkomsten</span><span class="sxs-lookup"><span data-stu-id="8e405-128">Learn more about integration account agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "meer informatie over enterprise integration-overeenkomsten")  