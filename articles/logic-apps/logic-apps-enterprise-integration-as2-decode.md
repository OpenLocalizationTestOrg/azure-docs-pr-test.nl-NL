---
title: Decoderen van berichten in AS2 - Azure Logic Apps | Microsoft Docs
description: Het gebruik van de decoder AS2 in de Enterprise-integratiepakket voor Azure Logic Apps
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
ms.openlocfilehash: a7920b2509fe368c6f7d55e17fe0bf0020c4562c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="decode-as2-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="e26da-103">AS2-berichten worden gedecodeerd voor Azure Logic Apps met de Enterprise-integratiepakket</span><span class="sxs-lookup"><span data-stu-id="e26da-103">Decode AS2 messages for Azure Logic Apps with the Enterprise Integration Pack</span></span> 

<span data-ttu-id="e26da-104">Om vast te stellen op beveiliging en betrouwbaarheid bij het verzenden van berichten, de decoderen AS2-bericht-connector te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e26da-104">To establish security and reliability while transmitting messages, use the Decode AS2 message connector.</span></span> <span data-ttu-id="e26da-105">Deze connector biedt digitale ondertekening, ontsleuteling en bevestigingen via bericht Disposition meldingen (MDN).</span><span class="sxs-lookup"><span data-stu-id="e26da-105">This connector provides digital signing, decryption, and acknowledgements through Message Disposition Notifications (MDN).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="e26da-106">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="e26da-106">Before you start</span></span>

<span data-ttu-id="e26da-107">Hier volgt de items die u nodig:</span><span class="sxs-lookup"><span data-stu-id="e26da-107">Here's the items you need:</span></span>

* <span data-ttu-id="e26da-108">Een Azure-account; kunt u een [gratis account](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="e26da-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="e26da-109">Een [integratie account](logic-apps-enterprise-integration-create-integration-account.md) die al is gedefinieerd en die zijn gekoppeld aan uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="e26da-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="e26da-110">U moet een integratie-account aan het gebruik van de connector decoderen AS2-bericht hebben.</span><span class="sxs-lookup"><span data-stu-id="e26da-110">You must have an integration account to use the Decode AS2 message connector.</span></span>
* <span data-ttu-id="e26da-111">Ten minste twee [partners](logic-apps-enterprise-integration-partners.md) die al zijn gedefinieerd in uw account integratie</span><span class="sxs-lookup"><span data-stu-id="e26da-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="e26da-112">Een [AS2-overeenkomst](logic-apps-enterprise-integration-as2.md) die al is gedefinieerd in uw account integratie</span><span class="sxs-lookup"><span data-stu-id="e26da-112">An [AS2 agreement](logic-apps-enterprise-integration-as2.md) that's already defined in your integration account</span></span>

## <a name="decode-as2-messages"></a><span data-ttu-id="e26da-113">AS2-berichten worden gedecodeerd</span><span class="sxs-lookup"><span data-stu-id="e26da-113">Decode AS2 messages</span></span>

1. <span data-ttu-id="e26da-114">[Een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="e26da-114">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="e26da-115">De connector decoderen AS2-bericht geen triggers, dus moet u een trigger voor het starten van uw logische app, zoals een aanvraag-trigger toevoegen.</span><span class="sxs-lookup"><span data-stu-id="e26da-115">The Decode AS2 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="e26da-116">In de ontwerpfunctie voor Logic App een trigger toevoegen en vervolgens een actie toevoegen aan uw logische app.</span><span class="sxs-lookup"><span data-stu-id="e26da-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3.  <span data-ttu-id="e26da-117">Voer in het zoekvak 'AS2' voor uw filter.</span><span class="sxs-lookup"><span data-stu-id="e26da-117">In the search box, enter "AS2" for your filter.</span></span> <span data-ttu-id="e26da-118">Selecteer **AS2 - decoderen AS2-bericht**.</span><span class="sxs-lookup"><span data-stu-id="e26da-118">Select **AS2 - Decode AS2 message**.</span></span>
   
    ![Zoek naar 'AS2'](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage1.png)

4. <span data-ttu-id="e26da-120">Als u geen verbindingen tot je account integratie eerder hebt gemaakt, wordt u gevraagd nu die verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="e26da-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="e26da-121">Naam van uw verbinding en selecteer de integratie-account waarmee u verbinding wilt maken.</span><span class="sxs-lookup"><span data-stu-id="e26da-121">Name your connection, and select the integration account that you want to connect.</span></span>
   
    ![Integratie verbinding maken](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage2.png)

    <span data-ttu-id="e26da-123">Eigenschappen met een sterretje zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="e26da-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="e26da-124">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="e26da-124">Property</span></span> | <span data-ttu-id="e26da-125">Details</span><span class="sxs-lookup"><span data-stu-id="e26da-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="e26da-126">Verbindingsnaam *</span><span class="sxs-lookup"><span data-stu-id="e26da-126">Connection Name *</span></span> |<span data-ttu-id="e26da-127">Voer een naam voor de verbinding.</span><span class="sxs-lookup"><span data-stu-id="e26da-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="e26da-128">Integratie Account *</span><span class="sxs-lookup"><span data-stu-id="e26da-128">Integration Account *</span></span> |<span data-ttu-id="e26da-129">Voer een naam voor uw account integratie.</span><span class="sxs-lookup"><span data-stu-id="e26da-129">Enter a name for your integration account.</span></span> <span data-ttu-id="e26da-130">Zorg ervoor dat uw account en logica app voor integratie in dezelfde Azure-locatie.</span><span class="sxs-lookup"><span data-stu-id="e26da-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

5.  <span data-ttu-id="e26da-131">Wanneer u bent klaar, de verbindingsdetails van uw moeten er ongeveer uitzien in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="e26da-131">When you're done, your connection details should look similar to this example.</span></span> <span data-ttu-id="e26da-132">Voor het voltooien van de verbinding te maken, kies **maken**.</span><span class="sxs-lookup"><span data-stu-id="e26da-132">To finish creating your connection, choose **Create**.</span></span>

    ![de verbindingsdetails integratie](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage3.png)

6. <span data-ttu-id="e26da-134">Nadat de verbinding is gemaakt, zoals in dit voorbeeld, selecteer **hoofdtekst** en **Headers** van de uitvoer van de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="e26da-134">After your connection is created, as shown in this example, select **Body** and **Headers** from the Request outputs.</span></span>
   
    ![integratie van verbinding is gemaakt](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage4.png) 

    <span data-ttu-id="e26da-136">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e26da-136">For example:</span></span>

    ![Selecteer hoofdtekst en Headers van de uitvoer van de aanvraag](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage5.png) 

## <a name="as2-decoder-details"></a><span data-ttu-id="e26da-138">AS2-decoder details</span><span class="sxs-lookup"><span data-stu-id="e26da-138">AS2 decoder details</span></span>

<span data-ttu-id="e26da-139">Het decoderen AS2-connector voert deze taken uit:</span><span class="sxs-lookup"><span data-stu-id="e26da-139">The Decode AS2 connector performs these tasks:</span></span> 

* <span data-ttu-id="e26da-140">AS2/HTTP-headers worden verwerkt</span><span class="sxs-lookup"><span data-stu-id="e26da-140">Processes AS2/HTTP headers</span></span>
* <span data-ttu-id="e26da-141">Verifieert de handtekening (indien geconfigureerd)</span><span class="sxs-lookup"><span data-stu-id="e26da-141">Verifies the signature (if configured)</span></span>
* <span data-ttu-id="e26da-142">De berichten ontsleutelt (indien geconfigureerd)</span><span class="sxs-lookup"><span data-stu-id="e26da-142">Decrypts the messages (if configured)</span></span>
* <span data-ttu-id="e26da-143">Het bericht decomprimeert (indien geconfigureerd)</span><span class="sxs-lookup"><span data-stu-id="e26da-143">Decompresses the message (if configured)</span></span>
* <span data-ttu-id="e26da-144">Voor overeenstemming zorgt met een ontvangen MDN met het oorspronkelijke uitgaand bericht</span><span class="sxs-lookup"><span data-stu-id="e26da-144">Reconciles a received MDN with the original outbound message</span></span>
* <span data-ttu-id="e26da-145">Updates en records in de database onweerlegbaarheid correleert</span><span class="sxs-lookup"><span data-stu-id="e26da-145">Updates and correlates records in the non-repudiation database</span></span>
* <span data-ttu-id="e26da-146">Records voor statusrapportage AS2 schrijft</span><span class="sxs-lookup"><span data-stu-id="e26da-146">Writes records for AS2 status reporting</span></span>
* <span data-ttu-id="e26da-147">De inhoud van het uitvoer-nettolading is base64-codering</span><span class="sxs-lookup"><span data-stu-id="e26da-147">The output payload contents are base64 encoded</span></span>
* <span data-ttu-id="e26da-148">Bepaalt of een MDN vereist is, en of de MDN synchrone moet of asynchrone op basis van configuratie in AS2-overeenkomst</span><span class="sxs-lookup"><span data-stu-id="e26da-148">Determines whether an MDN is required, and whether the MDN should be synchronous or asynchronous based on configuration in AS2 agreement</span></span>
* <span data-ttu-id="e26da-149">Genereert een synchrone of asynchrone MDN (op basis van overeenkomst configuraties)</span><span class="sxs-lookup"><span data-stu-id="e26da-149">Generates a synchronous or asynchronous MDN (based on agreement configurations)</span></span>
* <span data-ttu-id="e26da-150">De eigenschappen en correlatietokens ingesteld op de MDN</span><span class="sxs-lookup"><span data-stu-id="e26da-150">Sets the correlation tokens and properties on the MDN</span></span>

## <a name="try-this-sample"></a><span data-ttu-id="e26da-151">Probeer dit voorbeeld</span><span class="sxs-lookup"><span data-stu-id="e26da-151">Try this sample</span></span>

<span data-ttu-id="e26da-152">Als u wilt proberen een volledig operationeel logic app en voorbeeld AS2-scenario implementeren, Zie de [AS2 logic app-sjabloon en het scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span><span class="sxs-lookup"><span data-stu-id="e26da-152">To try deploying a fully operational logic app and sample AS2 scenario, see the [AS2 logic app template and scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span></span>

## <a name="view-the-swagger"></a><span data-ttu-id="e26da-153">De swagger weergeven</span><span class="sxs-lookup"><span data-stu-id="e26da-153">View the swagger</span></span>
<span data-ttu-id="e26da-154">Zie de [swagger details](/connectors/as2/).</span><span class="sxs-lookup"><span data-stu-id="e26da-154">See the [swagger details](/connectors/as2/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e26da-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e26da-155">Next steps</span></span>
[<span data-ttu-id="e26da-156">Meer informatie over het Enterprise-integratiepakket</span><span class="sxs-lookup"><span data-stu-id="e26da-156">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md) 

