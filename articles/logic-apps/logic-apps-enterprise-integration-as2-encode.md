---
title: Coderen van berichten in AS2 - Azure Logic Apps | Microsoft Docs
description: Het gebruik van het coderingsprogramma AS2 in de Enterprise-integratiepakket voor Azure Logic Apps
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 332fb9e3-576c-4683-bd10-d177a0ebe9a3
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 7889bf9e4e02143b6bb4c797531afa54f8647ce5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="encode-as2-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="fdcee-103">AS2-berichten te coderen voor Azure Logic Apps met de Enterprise-integratiepakket</span><span class="sxs-lookup"><span data-stu-id="fdcee-103">Encode AS2 messages for Azure Logic Apps with the Enterprise Integration Pack</span></span>

<span data-ttu-id="fdcee-104">Om vast te stellen op beveiliging en betrouwbaarheid bij het verzenden van berichten, de coderen AS2-bericht-connector te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fdcee-104">To establish security and reliability while transmitting messages, use the Encode AS2 message connector.</span></span> <span data-ttu-id="fdcee-105">Deze connector biedt digitale ondertekening, versleuteling en bevestigingen via bericht Disposition meldingen (MDN), zodat de ook ondersteuning voor niet-afwijzing.</span><span class="sxs-lookup"><span data-stu-id="fdcee-105">This connector provides digital signing, encryption, and acknowledgements through Message Disposition Notifications (MDN), which also leads to support for Non-Repudiation.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="fdcee-106">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="fdcee-106">Before you start</span></span>

<span data-ttu-id="fdcee-107">Hier volgt de items die u nodig:</span><span class="sxs-lookup"><span data-stu-id="fdcee-107">Here's the items you need:</span></span>

* <span data-ttu-id="fdcee-108">Een Azure-account; kunt u een [gratis account](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="fdcee-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="fdcee-109">Een [integratie account](logic-apps-enterprise-integration-create-integration-account.md) die al is gedefinieerd en die zijn gekoppeld aan uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="fdcee-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="fdcee-110">U moet een integratie-account aan het gebruik van de connector coderen AS2-bericht hebben.</span><span class="sxs-lookup"><span data-stu-id="fdcee-110">You must have an integration account to use the Encode AS2 message connector.</span></span>
* <span data-ttu-id="fdcee-111">Ten minste twee [partners](logic-apps-enterprise-integration-partners.md) die al zijn gedefinieerd in uw account integratie</span><span class="sxs-lookup"><span data-stu-id="fdcee-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="fdcee-112">Een [AS2-overeenkomst](logic-apps-enterprise-integration-as2.md) die al is gedefinieerd in uw account integratie</span><span class="sxs-lookup"><span data-stu-id="fdcee-112">An [AS2 agreement](logic-apps-enterprise-integration-as2.md) that's already defined in your integration account</span></span>

## <a name="encode-as2-messages"></a><span data-ttu-id="fdcee-113">AS2-berichten te coderen</span><span class="sxs-lookup"><span data-stu-id="fdcee-113">Encode AS2 messages</span></span>

1. <span data-ttu-id="fdcee-114">[Een logische app maken](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="fdcee-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="fdcee-115">De connector coderen AS2-bericht geen triggers, dus moet u een trigger voor het starten van uw logische app, zoals een aanvraag-trigger toevoegen.</span><span class="sxs-lookup"><span data-stu-id="fdcee-115">The Encode AS2 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="fdcee-116">In de ontwerpfunctie voor Logic App een trigger toevoegen en vervolgens een actie toevoegen aan uw logische app.</span><span class="sxs-lookup"><span data-stu-id="fdcee-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3.  <span data-ttu-id="fdcee-117">Voer in het zoekvak 'AS2' voor uw filter.</span><span class="sxs-lookup"><span data-stu-id="fdcee-117">In the search box, enter "AS2" for your filter.</span></span> <span data-ttu-id="fdcee-118">Selecteer **AS2 - coderen AS2-bericht**.</span><span class="sxs-lookup"><span data-stu-id="fdcee-118">Select **AS2 - Encode AS2 message**.</span></span>
   
    ![Zoek naar 'AS2'](./media/logic-apps-enterprise-integration-as2-encode/as2decodeimage1.png)

4. <span data-ttu-id="fdcee-120">Als u geen verbindingen tot je account integratie eerder hebt gemaakt, wordt u gevraagd nu die verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="fdcee-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="fdcee-121">Naam van uw verbinding en selecteer de integratie-account waarmee u verbinding wilt maken.</span><span class="sxs-lookup"><span data-stu-id="fdcee-121">Name your connection, and select the integration account that you want to connect.</span></span> 
   
    ![Maak verbinding met de integratie-account](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage1.png)  

    <span data-ttu-id="fdcee-123">Eigenschappen met een sterretje zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="fdcee-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="fdcee-124">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="fdcee-124">Property</span></span> | <span data-ttu-id="fdcee-125">Details</span><span class="sxs-lookup"><span data-stu-id="fdcee-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="fdcee-126">Verbindingsnaam *</span><span class="sxs-lookup"><span data-stu-id="fdcee-126">Connection Name *</span></span> |<span data-ttu-id="fdcee-127">Voer een naam voor de verbinding.</span><span class="sxs-lookup"><span data-stu-id="fdcee-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="fdcee-128">Integratie Account *</span><span class="sxs-lookup"><span data-stu-id="fdcee-128">Integration Account *</span></span> |<span data-ttu-id="fdcee-129">Voer een naam voor uw account integratie.</span><span class="sxs-lookup"><span data-stu-id="fdcee-129">Enter a name for your integration account.</span></span> <span data-ttu-id="fdcee-130">Zorg ervoor dat uw account en logica app voor integratie in dezelfde Azure-locatie.</span><span class="sxs-lookup"><span data-stu-id="fdcee-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

5.  <span data-ttu-id="fdcee-131">Wanneer u bent klaar, de verbindingsdetails van uw moeten er ongeveer uitzien in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="fdcee-131">When you're done, your connection details should look similar to this example.</span></span> <span data-ttu-id="fdcee-132">Voor het voltooien van de verbinding te maken, kies **maken**.</span><span class="sxs-lookup"><span data-stu-id="fdcee-132">To finish creating your connection, choose **Create**.</span></span>
   
    ![de verbindingsdetails integratie](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage2.png)

6. <span data-ttu-id="fdcee-134">Nadat de verbinding is gemaakt, zoals in dit voorbeeld, vindt u informatie voor **AS2-van**, **AS2-aan-id's** zoals geconfigureerd in de overeenkomst en **hoofdtekst**, die is de nettolading van het bericht.</span><span class="sxs-lookup"><span data-stu-id="fdcee-134">After your connection is created, as shown in this example, provide details for **AS2-From**, **AS2-To identifiers** as configured in your agreement, and **Body**, which is the message payload.</span></span>
   
    ![verplichte velden bieden](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage3.png)

## <a name="as2-encoder-details"></a><span data-ttu-id="fdcee-136">AS2-encoder details</span><span class="sxs-lookup"><span data-stu-id="fdcee-136">AS2 encoder details</span></span>

<span data-ttu-id="fdcee-137">Het coderen AS2-connector voert deze taken uit:</span><span class="sxs-lookup"><span data-stu-id="fdcee-137">The Encode AS2 connector performs these tasks:</span></span> 

* <span data-ttu-id="fdcee-138">AS2/HTTP-headers van toepassing is</span><span class="sxs-lookup"><span data-stu-id="fdcee-138">Applies AS2/HTTP headers</span></span>
* <span data-ttu-id="fdcee-139">Tekenen uitgaande berichten (indien geconfigureerd)</span><span class="sxs-lookup"><span data-stu-id="fdcee-139">Signs outgoing messages (if configured)</span></span>
* <span data-ttu-id="fdcee-140">Versleutelt uitgaande berichten (indien geconfigureerd)</span><span class="sxs-lookup"><span data-stu-id="fdcee-140">Encrypts outgoing messages (if configured)</span></span>
* <span data-ttu-id="fdcee-141">Comprimeren van het bericht (indien geconfigureerd)</span><span class="sxs-lookup"><span data-stu-id="fdcee-141">Compresses the message (if configured)</span></span>

## <a name="try-this-sample"></a><span data-ttu-id="fdcee-142">Probeer dit voorbeeld</span><span class="sxs-lookup"><span data-stu-id="fdcee-142">Try this sample</span></span>

<span data-ttu-id="fdcee-143">Als u wilt proberen een volledig operationeel logic app en voorbeeld AS2-scenario implementeren, Zie de [AS2 logic app-sjabloon en het scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span><span class="sxs-lookup"><span data-stu-id="fdcee-143">To try deploying a fully operational logic app and sample AS2 scenario, see the [AS2 logic app template and scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span></span>

## <a name="view-the-swagger"></a><span data-ttu-id="fdcee-144">De swagger weergeven</span><span class="sxs-lookup"><span data-stu-id="fdcee-144">View the swagger</span></span>
<span data-ttu-id="fdcee-145">Zie de [swagger details](/connectors/as2/).</span><span class="sxs-lookup"><span data-stu-id="fdcee-145">See the [swagger details](/connectors/as2/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="fdcee-146">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fdcee-146">Next steps</span></span>
[<span data-ttu-id="fdcee-147">Meer informatie over het Enterprise-integratiepakket</span><span class="sxs-lookup"><span data-stu-id="fdcee-147">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "meer informatie over Enterprise Integration Pack") 

