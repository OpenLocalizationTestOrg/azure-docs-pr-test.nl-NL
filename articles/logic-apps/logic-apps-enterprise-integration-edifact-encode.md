---
title: Codeer EDIFACT berichten - Azure Logic Apps | Microsoft Docs
description: EDI valideren en genereren van XML met EDIFACT berichtencoder in de Enterprise-integratiepakket voor Azure Logic Apps
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 974ac339-d97a-4715-bc92-62d02281e900
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: b8d577326d23ec45cb4a9ec0e450ebf7afd945f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="encode-edifact-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="5b9c1-103">EDIFACT-berichten te coderen voor Azure Logic Apps met de Enterprise-integratiepakket</span><span class="sxs-lookup"><span data-stu-id="5b9c1-103">Encode EDIFACT messages for Azure Logic Apps with the Enterprise Integration Pack</span></span>

<span data-ttu-id="5b9c1-104">Met de connector van het bericht EDIFACT coderen, kunt u valideren EDI- en partner-specifieke eigenschappen, een XML-document voor elke set transactie genereren en aanvragen van een bevestiging van technische, functionele bevestiging of beide.</span><span class="sxs-lookup"><span data-stu-id="5b9c1-104">With the Encode EDIFACT message connector, you can validate EDI and partner-specific properties, generate an XML document for each transaction set, and request a Technical Acknowledgement, Functional Acknowledgment, or both.</span></span>
<span data-ttu-id="5b9c1-105">Voor het gebruik van deze connector, moet u de connector toevoegen aan een bestaande trigger in uw logische app.</span><span class="sxs-lookup"><span data-stu-id="5b9c1-105">To use this connector, you must add the connector to an existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="5b9c1-106">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="5b9c1-106">Before you start</span></span>

<span data-ttu-id="5b9c1-107">Hier volgt de items die u nodig:</span><span class="sxs-lookup"><span data-stu-id="5b9c1-107">Here's the items you need:</span></span>

* <span data-ttu-id="5b9c1-108">Een Azure-account; kunt u een [gratis account](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="5b9c1-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="5b9c1-109">Een [integratie account](logic-apps-enterprise-integration-create-integration-account.md) die al is gedefinieerd en die zijn gekoppeld aan uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="5b9c1-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="5b9c1-110">U moet een integratie-account aan het gebruik van de connector coderen EDIFACT-bericht hebben.</span><span class="sxs-lookup"><span data-stu-id="5b9c1-110">You must have an integration account to use the Encode EDIFACT message connector.</span></span> 
* <span data-ttu-id="5b9c1-111">Ten minste twee [partners](logic-apps-enterprise-integration-partners.md) die al zijn gedefinieerd in uw account integratie</span><span class="sxs-lookup"><span data-stu-id="5b9c1-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="5b9c1-112">Een [EDIFACT overeenkomst](logic-apps-enterprise-integration-edifact.md) die al is gedefinieerd in uw account integratie</span><span class="sxs-lookup"><span data-stu-id="5b9c1-112">An [EDIFACT agreement](logic-apps-enterprise-integration-edifact.md) that's already defined in your integration account</span></span>

## <a name="encode-edifact-messages"></a><span data-ttu-id="5b9c1-113">EDIFACT-berichten te coderen</span><span class="sxs-lookup"><span data-stu-id="5b9c1-113">Encode EDIFACT messages</span></span>

1. <span data-ttu-id="5b9c1-114">[Een logische app maken](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="5b9c1-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="5b9c1-115">Het bericht coderen EDIFACT connector geen triggers, dus moet u een trigger voor het starten van uw logische app, zoals een aanvraag-trigger toevoegen.</span><span class="sxs-lookup"><span data-stu-id="5b9c1-115">The Encode EDIFACT message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="5b9c1-116">In de ontwerpfunctie voor Logic App een trigger toevoegen en vervolgens een actie toevoegen aan uw logische app.</span><span class="sxs-lookup"><span data-stu-id="5b9c1-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3.  <span data-ttu-id="5b9c1-117">Voer in het zoekvak 'EDIFACT' als filter.</span><span class="sxs-lookup"><span data-stu-id="5b9c1-117">In the search box, enter "EDIFACT" as your filter.</span></span> <span data-ttu-id="5b9c1-118">Selecteer een **coderen EDIFACT bericht met de Overeenkomstnaam** of **coderen EDIFACT-bericht met identiteiten**.</span><span class="sxs-lookup"><span data-stu-id="5b9c1-118">Select either **Encode EDIFACT Message by agreement name** or **Encode to EDIFACT message by identities**.</span></span>
   
    ![EDIFACT zoeken](media/logic-apps-enterprise-integration-edifact-encode/edifactdecodeimage1.png)  

3. <span data-ttu-id="5b9c1-120">Als u geen verbindingen tot je account integratie eerder hebt gemaakt, wordt u gevraagd nu die verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="5b9c1-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="5b9c1-121">Naam van uw verbinding en selecteer de integratie-account waarmee u verbinding wilt maken.</span><span class="sxs-lookup"><span data-stu-id="5b9c1-121">Name your connection, and select the integration account that you want to connect.</span></span>

    ![integratie-account verbinding maken](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage1.png)  

    <span data-ttu-id="5b9c1-123">Eigenschappen met een sterretje zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="5b9c1-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="5b9c1-124">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="5b9c1-124">Property</span></span> | <span data-ttu-id="5b9c1-125">Details</span><span class="sxs-lookup"><span data-stu-id="5b9c1-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="5b9c1-126">Verbindingsnaam *</span><span class="sxs-lookup"><span data-stu-id="5b9c1-126">Connection Name *</span></span> |<span data-ttu-id="5b9c1-127">Voer een naam voor de verbinding.</span><span class="sxs-lookup"><span data-stu-id="5b9c1-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="5b9c1-128">Integratie Account *</span><span class="sxs-lookup"><span data-stu-id="5b9c1-128">Integration Account *</span></span> |<span data-ttu-id="5b9c1-129">Voer een naam voor uw account integratie.</span><span class="sxs-lookup"><span data-stu-id="5b9c1-129">Enter a name for your integration account.</span></span> <span data-ttu-id="5b9c1-130">Zorg ervoor dat uw account en logica app voor integratie in dezelfde Azure-locatie.</span><span class="sxs-lookup"><span data-stu-id="5b9c1-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

5.  <span data-ttu-id="5b9c1-131">Wanneer u bent klaar, de verbindingsdetails van uw moeten er ongeveer uitzien in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="5b9c1-131">When you're done, your connection details should look similar to this example.</span></span> <span data-ttu-id="5b9c1-132">Voor het voltooien van de verbinding te maken, kies **maken**.</span><span class="sxs-lookup"><span data-stu-id="5b9c1-132">To finish creating your connection, choose **Create**.</span></span>

    ![de accountdetails verbinding integratie](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage2.png)

    <span data-ttu-id="5b9c1-134">De verbinding wordt nu gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5b9c1-134">Your connection is now created.</span></span>

    ![integratie-account verbinding is gemaakt](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage4.png)

#### <a name="encode-edifact-message-by-agreement-name"></a><span data-ttu-id="5b9c1-136">EDIFACT-bericht met de Overeenkomstnaam coderen</span><span class="sxs-lookup"><span data-stu-id="5b9c1-136">Encode EDIFACT Message by agreement name</span></span>

<span data-ttu-id="5b9c1-137">Als u hebt gekozen voor het coderen van EDIFACT berichten door de naam van de overeenkomst, opent u de **overeenkomst met de naam van EDIFACT** lijst, typ of Selecteer de naam van de overeenkomst EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="5b9c1-137">If you chose to encode EDIFACT messages by agreement name, open the **Name of EDIFACT agreement** list, enter or select your EDIFACT agreement name.</span></span> <span data-ttu-id="5b9c1-138">Voer in het XML-bericht voor het coderen.</span><span class="sxs-lookup"><span data-stu-id="5b9c1-138">Enter the XML message to encode.</span></span>

![Voer de naam van de overeenkomst EDIFACT en XML-bericht voor het coderen van](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage6.png)

#### <a name="encode-edifact-message-by-identities"></a><span data-ttu-id="5b9c1-140">EDIFACT-bericht met identiteiten coderen</span><span class="sxs-lookup"><span data-stu-id="5b9c1-140">Encode EDIFACT Message by identities</span></span>

<span data-ttu-id="5b9c1-141">Als u kiest voor het coderen van EDIFACT berichten door identiteiten, voert u de afzender-id, kwalificatie afzender, ontvanger-id en ontvanger kwalificatie zoals geconfigureerd in uw EDIFACT-overeenkomst.</span><span class="sxs-lookup"><span data-stu-id="5b9c1-141">If you choose to encode EDIFACT messages by identities, enter the sender identifier, sender qualifier, receiver identifier, and receiver qualifier as configured in your EDIFACT agreement.</span></span> <span data-ttu-id="5b9c1-142">Selecteer het XML-bericht voor het coderen.</span><span class="sxs-lookup"><span data-stu-id="5b9c1-142">Select the XML message to encode.</span></span>

![Geef identiteiten voor een afzender en ontvanger, selecteer van XML-bericht voor het coderen van](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage7.png)

## <a name="edifact-encode-details"></a><span data-ttu-id="5b9c1-144">Details EDIFACT coderen</span><span class="sxs-lookup"><span data-stu-id="5b9c1-144">EDIFACT Encode details</span></span>

<span data-ttu-id="5b9c1-145">De connector coderen EDIFACT voert deze taken uit:</span><span class="sxs-lookup"><span data-stu-id="5b9c1-145">The Encode EDIFACT connector performs these tasks:</span></span> 

* <span data-ttu-id="5b9c1-146">De overeenkomst oplossen door de afzender kwalificatie & -id en ontvanger kwalificatie en id overeenkomende</span><span class="sxs-lookup"><span data-stu-id="5b9c1-146">Resolve the agreement by matching the sender qualifier & identifier and receiver qualifier and identifier</span></span>
* <span data-ttu-id="5b9c1-147">De EDI-uitwisseling, conversie van XML-codering berichten naar EDI transactie sets in de uitwisseling serialiseert.</span><span class="sxs-lookup"><span data-stu-id="5b9c1-147">Serializes the EDI interchange, converting XML-encoded messages into EDI transaction sets in the interchange.</span></span>
* <span data-ttu-id="5b9c1-148">Transactie set-header en trailer segmenten van toepassing is</span><span class="sxs-lookup"><span data-stu-id="5b9c1-148">Applies transaction set header and trailer segments</span></span>
* <span data-ttu-id="5b9c1-149">Genereren van een besturingselement interchange getal, een besturingselement groepsnummer en een getal voor het instellen van transactie voor elke uitgaande uitwisseling</span><span class="sxs-lookup"><span data-stu-id="5b9c1-149">Generates an interchange control number, a group control number, and a transaction set control number for each outgoing interchange</span></span>
* <span data-ttu-id="5b9c1-150">Vervangt scheidingstekens in de nettolading</span><span class="sxs-lookup"><span data-stu-id="5b9c1-150">Replaces separators in the payload data</span></span>
* <span data-ttu-id="5b9c1-151">Valideert EDI en partner-specifieke eigenschappen</span><span class="sxs-lookup"><span data-stu-id="5b9c1-151">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="5b9c1-152">Schemavalidatie van de gegevenselementen van de transactie-set tegen het berichtschema.</span><span class="sxs-lookup"><span data-stu-id="5b9c1-152">Schema validation of the transaction-set data elements against the message schema.</span></span>
  * <span data-ttu-id="5b9c1-153">EDI gevalideerd gegevenselementen transactie-set.</span><span class="sxs-lookup"><span data-stu-id="5b9c1-153">EDI validation performed on transaction-set data elements.</span></span>
  * <span data-ttu-id="5b9c1-154">Uitgebreide validatie uitgevoerd op van de transactie-set-gegevenselementen</span><span class="sxs-lookup"><span data-stu-id="5b9c1-154">Extended validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="5b9c1-155">Genereert een XML-document voor elke set transactie.</span><span class="sxs-lookup"><span data-stu-id="5b9c1-155">Generates an XML document for each transaction set.</span></span>
* <span data-ttu-id="5b9c1-156">Vraagt om bevestiging van de technische en/of functionele (indien geconfigureerd).</span><span class="sxs-lookup"><span data-stu-id="5b9c1-156">Requests a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="5b9c1-157">Als een technische bevestiging geeft het bericht CONTRL ontvangst van een knooppunt aan.</span><span class="sxs-lookup"><span data-stu-id="5b9c1-157">As a technical acknowledgment, the CONTRL message indicates receipt of an interchange.</span></span>
  * <span data-ttu-id="5b9c1-158">Als een functionele bevestiging geeft het bericht CONTRL aan acceptatie- of afwijzing van de ontvangen interchange, groep of een bericht met een lijst met fouten of niet-ondersteunde functies</span><span class="sxs-lookup"><span data-stu-id="5b9c1-158">As a functional acknowledgment, the CONTRL message indicates acceptance or rejection of the received interchange, group, or message, with a list of errors or unsupported functionality</span></span>

## <a name="view-swagger-file"></a><span data-ttu-id="5b9c1-159">Swagger-bestand weergeven</span><span class="sxs-lookup"><span data-stu-id="5b9c1-159">View Swagger file</span></span>
<span data-ttu-id="5b9c1-160">De Swagger-details voor de connector EDIFACT Zie [EDIFACT](/connectors/edifact/).</span><span class="sxs-lookup"><span data-stu-id="5b9c1-160">To view the Swagger details for the EDIFACT connector, see [EDIFACT](/connectors/edifact/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b9c1-161">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5b9c1-161">Next steps</span></span>
[<span data-ttu-id="5b9c1-162">Meer informatie over het Enterprise-integratiepakket</span><span class="sxs-lookup"><span data-stu-id="5b9c1-162">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "meer informatie over Enterprise Integration Pack") 

