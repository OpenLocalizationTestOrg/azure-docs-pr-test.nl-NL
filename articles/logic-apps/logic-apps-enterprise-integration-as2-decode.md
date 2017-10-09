---
title: berichten aaaDecode AS2 - Azure Logic Apps | Microsoft Docs
description: Hoe toouse AS2 decoder in Hallo Enterprise Integration Pack Hallo voor Azure Logic Apps
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
ms.date: 01/27/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 2406e5ec68e0906700fad97d60cb83ef0d106cd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="decode-as2-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="a5594-103">AS2-berichten voor Azure Logic Apps decoderen Hello Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="a5594-103">Decode AS2 messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span> 

<span data-ttu-id="a5594-104">tooestablish beveiliging en betrouwbaarheid tijdens de verzending van berichten, moet u Hallo decoderen AS2 bericht connector gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a5594-104">tooestablish security and reliability while transmitting messages, use hello Decode AS2 message connector.</span></span> <span data-ttu-id="a5594-105">Deze connector biedt digitale ondertekening, ontsleuteling en bevestigingen via bericht Disposition meldingen (MDN).</span><span class="sxs-lookup"><span data-stu-id="a5594-105">This connector provides digital signing, decryption, and acknowledgements through Message Disposition Notifications (MDN).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="a5594-106">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="a5594-106">Before you start</span></span>

<span data-ttu-id="a5594-107">Hier volgt Hallo items die u nodig:</span><span class="sxs-lookup"><span data-stu-id="a5594-107">Here's hello items you need:</span></span>

* <span data-ttu-id="a5594-108">Een Azure-account; kunt u een [gratis account](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="a5594-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="a5594-109">Een [integratie account](logic-apps-enterprise-integration-create-integration-account.md) die al is gedefinieerd en die zijn gekoppeld aan uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="a5594-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="a5594-110">U moet een connector integratie account toouse Hallo decoderen AS2 bericht hebben.</span><span class="sxs-lookup"><span data-stu-id="a5594-110">You must have an integration account toouse hello Decode AS2 message connector.</span></span>
* <span data-ttu-id="a5594-111">Ten minste twee [partners](logic-apps-enterprise-integration-partners.md) die al zijn gedefinieerd in uw account integratie</span><span class="sxs-lookup"><span data-stu-id="a5594-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="a5594-112">Een [AS2-overeenkomst](logic-apps-enterprise-integration-as2.md) die al is gedefinieerd in uw account integratie</span><span class="sxs-lookup"><span data-stu-id="a5594-112">An [AS2 agreement](logic-apps-enterprise-integration-as2.md) that's already defined in your integration account</span></span>

## <a name="decode-as2-messages"></a><span data-ttu-id="a5594-113">AS2-berichten worden gedecodeerd</span><span class="sxs-lookup"><span data-stu-id="a5594-113">Decode AS2 messages</span></span>

1. <span data-ttu-id="a5594-114">[Een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="a5594-114">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="a5594-115">Hallo decoderen AS2-bericht connector geen triggers, dus moet u een trigger voor het starten van uw logische app, zoals een aanvraag-trigger toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a5594-115">hello Decode AS2 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="a5594-116">In Hallo Logic App-ontwerper, een trigger toevoegen en voeg vervolgens een actie tooyour logische app.</span><span class="sxs-lookup"><span data-stu-id="a5594-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="a5594-117">Voer in het zoekvak hello, 'AS2' voor uw filter.</span><span class="sxs-lookup"><span data-stu-id="a5594-117">In hello search box, enter "AS2" for your filter.</span></span> <span data-ttu-id="a5594-118">Selecteer **AS2 - decoderen AS2-bericht**.</span><span class="sxs-lookup"><span data-stu-id="a5594-118">Select **AS2 - Decode AS2 message**.</span></span>
   
    ![Zoek naar 'AS2'](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage1.png)

4. <span data-ttu-id="a5594-120">Als u niet alle verbindingen eerder tooyour integratie account maakt, wordt u gevraagd toocreate nu dat connection.</span><span class="sxs-lookup"><span data-stu-id="a5594-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="a5594-121">Naam van uw verbinding en Hallo integratie-account dat u wilt dat tooconnect selecteren.</span><span class="sxs-lookup"><span data-stu-id="a5594-121">Name your connection, and select hello integration account that you want tooconnect.</span></span>
   
    ![Integratie verbinding maken](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage2.png)

    <span data-ttu-id="a5594-123">Eigenschappen met een sterretje zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="a5594-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="a5594-124">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="a5594-124">Property</span></span> | <span data-ttu-id="a5594-125">Details</span><span class="sxs-lookup"><span data-stu-id="a5594-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="a5594-126">Verbindingsnaam *</span><span class="sxs-lookup"><span data-stu-id="a5594-126">Connection Name *</span></span> |<span data-ttu-id="a5594-127">Voer een naam voor de verbinding.</span><span class="sxs-lookup"><span data-stu-id="a5594-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="a5594-128">Integratie Account *</span><span class="sxs-lookup"><span data-stu-id="a5594-128">Integration Account *</span></span> |<span data-ttu-id="a5594-129">Voer een naam voor uw account integratie.</span><span class="sxs-lookup"><span data-stu-id="a5594-129">Enter a name for your integration account.</span></span> <span data-ttu-id="a5594-130">Zorg ervoor dat uw account en logica app voor integratie in Hallo dezelfde Azure-locatie.</span><span class="sxs-lookup"><span data-stu-id="a5594-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="a5594-131">Wanneer u bent klaar, ziet uw Verbindingsdetails vergelijkbaar toothis voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="a5594-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="a5594-132">maken van uw verbinding toofinish kiezen **maken**.</span><span class="sxs-lookup"><span data-stu-id="a5594-132">toofinish creating your connection, choose **Create**.</span></span>

    ![de verbindingsdetails integratie](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage3.png)

6. <span data-ttu-id="a5594-134">Nadat de verbinding is gemaakt, zoals in dit voorbeeld, selecteer **hoofdtekst** en **Headers** aanvragen van Hallo uitvoer.</span><span class="sxs-lookup"><span data-stu-id="a5594-134">After your connection is created, as shown in this example, select **Body** and **Headers** from hello Request outputs.</span></span>
   
    ![integratie van verbinding is gemaakt](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage4.png) 

    <span data-ttu-id="a5594-136">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="a5594-136">For example:</span></span>

    ![Selecteer hoofdtekst en Headers van de uitvoer van de aanvraag](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage5.png) 

## <a name="as2-decoder-details"></a><span data-ttu-id="a5594-138">AS2-decoder details</span><span class="sxs-lookup"><span data-stu-id="a5594-138">AS2 decoder details</span></span>

<span data-ttu-id="a5594-139">Hallo decoderen AS2-connector voert deze taken uit:</span><span class="sxs-lookup"><span data-stu-id="a5594-139">hello Decode AS2 connector performs these tasks:</span></span> 

* <span data-ttu-id="a5594-140">AS2/HTTP-headers worden verwerkt</span><span class="sxs-lookup"><span data-stu-id="a5594-140">Processes AS2/HTTP headers</span></span>
* <span data-ttu-id="a5594-141">Controleert of Hallo handtekening (indien geconfigureerd)</span><span class="sxs-lookup"><span data-stu-id="a5594-141">Verifies hello signature (if configured)</span></span>
* <span data-ttu-id="a5594-142">Hallo-berichten ontsleutelt (indien geconfigureerd)</span><span class="sxs-lookup"><span data-stu-id="a5594-142">Decrypts hello messages (if configured)</span></span>
* <span data-ttu-id="a5594-143">Decomprimeert Hallo-bericht (indien geconfigureerd)</span><span class="sxs-lookup"><span data-stu-id="a5594-143">Decompresses hello message (if configured)</span></span>
* <span data-ttu-id="a5594-144">Voor overeenstemming zorgt met een ontvangen MDN met het oorspronkelijke uitgaand bericht Hallo</span><span class="sxs-lookup"><span data-stu-id="a5594-144">Reconciles a received MDN with hello original outbound message</span></span>
* <span data-ttu-id="a5594-145">Updates en correleert records in Hallo onweerlegbaarheid-database</span><span class="sxs-lookup"><span data-stu-id="a5594-145">Updates and correlates records in hello non-repudiation database</span></span>
* <span data-ttu-id="a5594-146">Records voor statusrapportage AS2 schrijft</span><span class="sxs-lookup"><span data-stu-id="a5594-146">Writes records for AS2 status reporting</span></span>
* <span data-ttu-id="a5594-147">Hallo uitvoer van de nettolading van inhoud zijn base64-gecodeerd</span><span class="sxs-lookup"><span data-stu-id="a5594-147">hello output payload contents are base64 encoded</span></span>
* <span data-ttu-id="a5594-148">Bepaalt of een MDN vereist is, en of Hallo MDN synchrone moet of asynchrone op basis van configuratie in AS2-overeenkomst</span><span class="sxs-lookup"><span data-stu-id="a5594-148">Determines whether an MDN is required, and whether hello MDN should be synchronous or asynchronous based on configuration in AS2 agreement</span></span>
* <span data-ttu-id="a5594-149">Genereert een synchrone of asynchrone MDN (op basis van overeenkomst configuraties)</span><span class="sxs-lookup"><span data-stu-id="a5594-149">Generates a synchronous or asynchronous MDN (based on agreement configurations)</span></span>
* <span data-ttu-id="a5594-150">Eigenschappen en Hallo correlatietokens ingesteld op Hallo MDN</span><span class="sxs-lookup"><span data-stu-id="a5594-150">Sets hello correlation tokens and properties on hello MDN</span></span>

## <a name="try-this-sample"></a><span data-ttu-id="a5594-151">Probeer dit voorbeeld</span><span class="sxs-lookup"><span data-stu-id="a5594-151">Try this sample</span></span>

<span data-ttu-id="a5594-152">een volledig operationeel logic app en voorbeeld AS2-scenario implementeren tootry Zie Hallo [AS2 logic app-sjabloon en het scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span><span class="sxs-lookup"><span data-stu-id="a5594-152">tootry deploying a fully operational logic app and sample AS2 scenario, see hello [AS2 logic app template and scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="a5594-153">Weergave Hallo swagger</span><span class="sxs-lookup"><span data-stu-id="a5594-153">View hello swagger</span></span>
<span data-ttu-id="a5594-154">Zie Hallo [swagger details](/connectors/as2/).</span><span class="sxs-lookup"><span data-stu-id="a5594-154">See hello [swagger details](/connectors/as2/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a5594-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a5594-155">Next steps</span></span>
[<span data-ttu-id="a5594-156">Meer informatie over Enterprise Integration Pack Hallo</span><span class="sxs-lookup"><span data-stu-id="a5594-156">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md) 

