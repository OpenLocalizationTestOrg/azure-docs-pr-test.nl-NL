---
title: aaaLogic Apps B2B edifact decoderen oplossen UNH2.5 - Azure Logic Apps | Microsoft Docs
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
ms.openlocfilehash: 6d85242d0f828fa52cdc9689938f3ba1e51b1183
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toohandle-edifact-documents-having-unh25-segment"></a><span data-ttu-id="dabf8-103">Hoe toohandle EDIFACT documenten met UNH2.5 segment</span><span class="sxs-lookup"><span data-stu-id="dabf8-103">How toohandle EDIFACT documents having UNH2.5 segment</span></span>
<span data-ttu-id="dabf8-104">Wanneer UNH2.5 op Hallo EDIFACT document aanwezig is, wordt deze gebruikt voor het opzoeken van het schema.</span><span class="sxs-lookup"><span data-stu-id="dabf8-104">When UNH2.5 is present in hello EDIFACT document, it is being used for schema lookup.</span></span> 

<span data-ttu-id="dabf8-105">Voorbeeld: Hallo UNH veld is **EAN008** in EDIFACT het Hallo-bericht</span><span class="sxs-lookup"><span data-stu-id="dabf8-105">Example: hello UNH field is **EAN008** in hello EDIFACT message</span></span>  
<span data-ttu-id="dabf8-106">UNH + SSDD1 + ORDERS: D: 03B: ONGEDAAN MAKEN:**EAN008**'</span><span class="sxs-lookup"><span data-stu-id="dabf8-106">UNH+SSDD1+ORDERS:D:03B:UN:**EAN008**'</span></span>  

<span data-ttu-id="dabf8-107">Stappen toofollow toohandle Hallo-bericht</span><span class="sxs-lookup"><span data-stu-id="dabf8-107">Steps toofollow toohandle hello message</span></span> 
1. <span data-ttu-id="dabf8-108">Hallo-schema bijwerken</span><span class="sxs-lookup"><span data-stu-id="dabf8-108">Update hello schema</span></span>
2. <span data-ttu-id="dabf8-109">Controleer de instellingen van de overeenkomst Hallo</span><span class="sxs-lookup"><span data-stu-id="dabf8-109">Check hello agreement settings</span></span>  

## <a name="update-hello-schema"></a><span data-ttu-id="dabf8-110">Hallo-schema bijwerken</span><span class="sxs-lookup"><span data-stu-id="dabf8-110">Update hello schema</span></span>
<span data-ttu-id="dabf8-111">tooprocess het Hallo-bericht, moet u een schema met de naam hoofdknooppunt Hallo UNH2.5 toodeploy.</span><span class="sxs-lookup"><span data-stu-id="dabf8-111">tooprocess hello message, you need toodeploy a schema with hello UNH2.5 root node name.</span></span>  <span data-ttu-id="dabf8-112">Voor een voorbeeld gegeven, hoofdnaam Hallo-schema zou worden **EFACT_D03B_ORDERS_EAN008**</span><span class="sxs-lookup"><span data-stu-id="dabf8-112">For given an example, hello schema root name would be **EFACT_D03B_ORDERS_EAN008**</span></span>  

<span data-ttu-id="dabf8-113">Voor elke D03B_ORDERS met een andere UNH2.5 segment hebt u toodeploy een afzonderlijk schema.</span><span class="sxs-lookup"><span data-stu-id="dabf8-113">For each D03B_ORDERS with a different UNH2.5 segment, you would have toodeploy an individual schema.</span></span>  

## <a name="add-schema-toohello-edifact-agreement"></a><span data-ttu-id="dabf8-114">Schema toohello EDIFACT overeenkomst toevoegen</span><span class="sxs-lookup"><span data-stu-id="dabf8-114">Add schema toohello EDIFACT agreement</span></span>
### <a name="edifact-decode"></a><span data-ttu-id="dabf8-115">EDIFACT decoderen</span><span class="sxs-lookup"><span data-stu-id="dabf8-115">EDIFACT Decode</span></span>
<span data-ttu-id="dabf8-116">tooDecode Hallo binnenkomend bericht, Hallo schema configureren in Hallo EDIFACT ontvangen overeenkomst instellingen</span><span class="sxs-lookup"><span data-stu-id="dabf8-116">tooDecode hello incoming message, configure hello schema in hello EDIFACT agreement receive settings</span></span>
1. <span data-ttu-id="dabf8-117">Hallo schema toohello integratie account toevoegen</span><span class="sxs-lookup"><span data-stu-id="dabf8-117">Add hello schema toohello integration account</span></span>    
2. <span data-ttu-id="dabf8-118">Hallo-schema configureren in Hallo EDIFACT ontvangen overeenkomst instellingen.</span><span class="sxs-lookup"><span data-stu-id="dabf8-118">Configure hello schema in hello EDIFACT agreement receive settings.</span></span> 
3. <span data-ttu-id="dabf8-119">Selecteer EDIFACT overeenkomst en klik op **bewerken als JSON**.</span><span class="sxs-lookup"><span data-stu-id="dabf8-119">Select EDIFACT agreement and click **Edit as JSON**.</span></span>  <span data-ttu-id="dabf8-120">UNH2.5 waarde toevoegen in Hallo ontvangen overeenkomst **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png)</span><span class="sxs-lookup"><span data-stu-id="dabf8-120">Add UNH2.5 value in hello Receive Agreement **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png)</span></span>

### <a name="edifact-encode"></a><span data-ttu-id="dabf8-121">EDIFACT coderen</span><span class="sxs-lookup"><span data-stu-id="dabf8-121">EDIFACT Encode</span></span>
<span data-ttu-id="dabf8-122">tooEncode Hallo binnenkomend bericht, Hallo schema in Hallo EDIFACT overeenkomst verzendinstellingen configureren</span><span class="sxs-lookup"><span data-stu-id="dabf8-122">tooEncode hello incoming message, configure hello schema in hello EDIFACT agreement send settings</span></span>
1. <span data-ttu-id="dabf8-123">Hallo schema toohello integratie account toevoegen</span><span class="sxs-lookup"><span data-stu-id="dabf8-123">Add hello schema toohello integration account</span></span>    
2. <span data-ttu-id="dabf8-124">Hallo-schema in Hallo EDIFACT overeenkomst verzendinstellingen configureren.</span><span class="sxs-lookup"><span data-stu-id="dabf8-124">Configure hello schema in hello EDIFACT agreement send settings.</span></span> 
3. <span data-ttu-id="dabf8-125">Selecteer EDIFACT overeenkomst en klik op **bewerken als JSON**.</span><span class="sxs-lookup"><span data-stu-id="dabf8-125">Select EDIFACT agreement and click **Edit as JSON**.</span></span>  <span data-ttu-id="dabf8-126">UNH2.5 waarde toevoegen in Hallo overeenkomst verzenden **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)</span><span class="sxs-lookup"><span data-stu-id="dabf8-126">Add UNH2.5 value in hello Send Agreement **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="dabf8-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="dabf8-127">Next Steps</span></span>
* [<span data-ttu-id="dabf8-128">Meer informatie over de integratie account overeenkomsten</span><span class="sxs-lookup"><span data-stu-id="dabf8-128">Learn more about integration account agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "meer informatie over enterprise integration-overeenkomsten")  