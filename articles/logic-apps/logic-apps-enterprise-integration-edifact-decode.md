---
title: aaaDecode EDIFACT berichten - Azure Logic Apps | Microsoft Docs
description: EDI valideren en genereren van bevestigingen met Hallo EDIFACT bericht decoder in Enterprise Integration Pack Hallo voor Azure Logic Apps
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 0e61501d-21a2-4419-8c6c-88724d346e81
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 94faebdec4e4ffc8ad76ad1609495ddf9f002250
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="decode-edifact-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="19c33-103">EDIFACT-berichten voor Azure Logic Apps decoderen Hello Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="19c33-103">Decode EDIFACT messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="19c33-104">Met Hallo decoderen EDIFACT bericht connector kunt u valideren EDI- en partner-specifieke eigenschappen, uitgewisseld in transacties sets splitsen of behouden van de hele uitgewisseld en genereren van bevestigingen voor verwerkte transacties.</span><span class="sxs-lookup"><span data-stu-id="19c33-104">With hello Decode EDIFACT message connector, you can validate EDI and partner-specific properties, split interchanges into transactions sets or preserve entire interchanges, and generate acknowledgments for processed transactions.</span></span> <span data-ttu-id="19c33-105">toouse deze connector, moet u Hallo connector tooan bestaande trigger in uw logische app toevoegen.</span><span class="sxs-lookup"><span data-stu-id="19c33-105">toouse this connector, you must add hello connector tooan existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="19c33-106">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="19c33-106">Before you start</span></span>

<span data-ttu-id="19c33-107">Hier volgt Hallo items die u nodig:</span><span class="sxs-lookup"><span data-stu-id="19c33-107">Here's hello items you need:</span></span>

* <span data-ttu-id="19c33-108">Een Azure-account; kunt u een [gratis account](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="19c33-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="19c33-109">Een [integratie account](logic-apps-enterprise-integration-create-integration-account.md) die al is gedefinieerd en die zijn gekoppeld aan uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="19c33-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="19c33-110">U moet een connector integratie account toouse Hallo decoderen EDIFACT bericht hebben.</span><span class="sxs-lookup"><span data-stu-id="19c33-110">You must have an integration account toouse hello Decode EDIFACT message connector.</span></span> 
* <span data-ttu-id="19c33-111">Ten minste twee [partners](logic-apps-enterprise-integration-partners.md) die al zijn gedefinieerd in uw account integratie</span><span class="sxs-lookup"><span data-stu-id="19c33-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="19c33-112">Een [EDIFACT overeenkomst](logic-apps-enterprise-integration-edifact.md) die al is gedefinieerd in uw account integratie</span><span class="sxs-lookup"><span data-stu-id="19c33-112">An [EDIFACT agreement](logic-apps-enterprise-integration-edifact.md) that's already defined in your integration account</span></span>

## <a name="decode-edifact-messages"></a><span data-ttu-id="19c33-113">EDIFACT-berichten worden gedecodeerd</span><span class="sxs-lookup"><span data-stu-id="19c33-113">Decode EDIFACT messages</span></span>

1. <span data-ttu-id="19c33-114">[Een logische app maken](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="19c33-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="19c33-115">Hallo decoderen EDIFACT bericht connector geen triggers, dus moet u een trigger voor het starten van uw logische app, zoals een aanvraag-trigger toevoegen.</span><span class="sxs-lookup"><span data-stu-id="19c33-115">hello Decode EDIFACT message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="19c33-116">In Hallo Logic App-ontwerper, een trigger toevoegen en voeg vervolgens een actie tooyour logische app.</span><span class="sxs-lookup"><span data-stu-id="19c33-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3. <span data-ttu-id="19c33-117">Voer in het zoekvak hello, 'EDIFACT' als filter.</span><span class="sxs-lookup"><span data-stu-id="19c33-117">In hello search box, enter "EDIFACT" as your filter.</span></span> <span data-ttu-id="19c33-118">Selecteer **decoderen EDIFACT bericht**.</span><span class="sxs-lookup"><span data-stu-id="19c33-118">Select **Decode EDIFACT Message**.</span></span>
   
    ![EDIFACT zoeken](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage1.png)

3. <span data-ttu-id="19c33-120">Als u niet alle verbindingen eerder tooyour integratie account maakt, wordt u gevraagd toocreate nu dat connection.</span><span class="sxs-lookup"><span data-stu-id="19c33-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="19c33-121">Naam van uw verbinding en Hallo integratie-account dat u wilt dat tooconnect selecteren.</span><span class="sxs-lookup"><span data-stu-id="19c33-121">Name your connection, and select hello integration account that you want tooconnect.</span></span>
   
    ![integratie-account maken](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage2.png)

    <span data-ttu-id="19c33-123">Eigenschappen met een sterretje zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="19c33-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="19c33-124">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="19c33-124">Property</span></span> | <span data-ttu-id="19c33-125">Details</span><span class="sxs-lookup"><span data-stu-id="19c33-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="19c33-126">Verbindingsnaam *</span><span class="sxs-lookup"><span data-stu-id="19c33-126">Connection Name *</span></span> |<span data-ttu-id="19c33-127">Voer een naam voor de verbinding.</span><span class="sxs-lookup"><span data-stu-id="19c33-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="19c33-128">Integratie Account *</span><span class="sxs-lookup"><span data-stu-id="19c33-128">Integration Account *</span></span> |<span data-ttu-id="19c33-129">Voer een naam voor uw account integratie.</span><span class="sxs-lookup"><span data-stu-id="19c33-129">Enter a name for your integration account.</span></span> <span data-ttu-id="19c33-130">Zorg ervoor dat uw account en logica app voor integratie in Hallo dezelfde Azure-locatie.</span><span class="sxs-lookup"><span data-stu-id="19c33-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

4. <span data-ttu-id="19c33-131">Wanneer u klaar bent met het maken van uw verbinding toofinish kiezen **maken**.</span><span class="sxs-lookup"><span data-stu-id="19c33-131">When you're done toofinish creating your connection, choose **Create**.</span></span> <span data-ttu-id="19c33-132">De verbindingsdetails ziet vergelijkbaar toothis voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="19c33-132">Your connection details should look similar toothis example:</span></span>

    ![de accountdetails integratie](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage3.png)  

5. <span data-ttu-id="19c33-134">Nadat de verbinding is gemaakt, zoals in dit voorbeeld, selecteer toodecode Hallo EDIFACT plat bestand-bericht.</span><span class="sxs-lookup"><span data-stu-id="19c33-134">After your connection is created, as shown in this example, select hello EDIFACT flat file message toodecode.</span></span>

    ![integratie-account verbinding is gemaakt](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage4.png)  

    <span data-ttu-id="19c33-136">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="19c33-136">For example:</span></span>

    ![Selecteer EDIFACT plat bestand-bericht voor het decoderen van](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage5.png)  

## <a name="edifact-decoder-details"></a><span data-ttu-id="19c33-138">EDIFACT decoder details</span><span class="sxs-lookup"><span data-stu-id="19c33-138">EDIFACT decoder details</span></span>

<span data-ttu-id="19c33-139">Hallo decoderen EDIFACT connector voert deze taken uit:</span><span class="sxs-lookup"><span data-stu-id="19c33-139">hello Decode EDIFACT connector performs these tasks:</span></span> 

* <span data-ttu-id="19c33-140">Hallo envelop tegen trading partner agreement valideert.</span><span class="sxs-lookup"><span data-stu-id="19c33-140">Validates hello envelope against trading partner agreement.</span></span>
* <span data-ttu-id="19c33-141">Oplossing Hallo overeenkomst door overeenkomende Hallo afzender kwalificatie & -id en ontvanger kwalificatie & -id.</span><span class="sxs-lookup"><span data-stu-id="19c33-141">Resolves hello agreement by matching hello sender qualifier & identifier and receiver qualifier & identifier.</span></span>
* <span data-ttu-id="19c33-142">Een knooppunt in meerdere transacties splitst wanneer Hallo interchange heeft meer dan één transactie op basis van het Hallo-overeenkomst instellingen configuratie ontvangen.</span><span class="sxs-lookup"><span data-stu-id="19c33-142">Splits an interchange into multiple transactions when hello interchange has more than one transaction based on hello agreement's receive settings configuration.</span></span>
* <span data-ttu-id="19c33-143">Hallo interchange ontleed.</span><span class="sxs-lookup"><span data-stu-id="19c33-143">Disassembles hello interchange.</span></span>
* <span data-ttu-id="19c33-144">Valideert EDI en partner-specifieke eigenschappen, waaronder:</span><span class="sxs-lookup"><span data-stu-id="19c33-144">Validates EDI and partner-specific properties including:</span></span>
  * <span data-ttu-id="19c33-145">Validatie van Hallo interchange envelop structuur</span><span class="sxs-lookup"><span data-stu-id="19c33-145">Validation of hello interchange envelope structure</span></span>
  * <span data-ttu-id="19c33-146">Schemavalidatie van Hallo envelop volgens het schema voor Hallo-besturingselement</span><span class="sxs-lookup"><span data-stu-id="19c33-146">Schema validation of hello envelope against hello control schema</span></span>
  * <span data-ttu-id="19c33-147">Schemavalidatie van Hallo transactie-set gegevenselementen volgens het schema voor Hallo-bericht</span><span class="sxs-lookup"><span data-stu-id="19c33-147">Schema validation of hello transaction-set data elements against hello message schema</span></span>
  * <span data-ttu-id="19c33-148">EDI-validatie wordt uitgevoerd op transactie-set gegevenselementen</span><span class="sxs-lookup"><span data-stu-id="19c33-148">EDI validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="19c33-149">Verifieert dat Hallo interchange, groep en transactie set besturingselement getallen niet identiek zijn (indien geconfigureerd)</span><span class="sxs-lookup"><span data-stu-id="19c33-149">Verifies that hello interchange, group, and transaction set control numbers are not duplicates (if configured)</span></span> 
  * <span data-ttu-id="19c33-150">Hallo interchange controle-aantal tegen eerder ontvangen uitgewisseld controleert.</span><span class="sxs-lookup"><span data-stu-id="19c33-150">Checks hello interchange control number against previously received interchanges.</span></span> 
  * <span data-ttu-id="19c33-151">Hallo groepsnummer beheer op basis van andere getallen groep besturingselement in Hallo interchange controleert.</span><span class="sxs-lookup"><span data-stu-id="19c33-151">Checks hello group control number against other group control numbers in hello interchange.</span></span> 
  * <span data-ttu-id="19c33-152">Controleert Hallo transactie controle-aantal ingesteld op basis van andere cijfers voor het instellen van transactie in die groep.</span><span class="sxs-lookup"><span data-stu-id="19c33-152">Checks hello transaction set control number against other transaction set control numbers in that group.</span></span>
* <span data-ttu-id="19c33-153">Hallo interchange in transactie sets splitst of behoudt de gehele uitwisseling Hallo:</span><span class="sxs-lookup"><span data-stu-id="19c33-153">Splits hello interchange into transaction sets, or preserves hello entire interchange:</span></span>
  * <span data-ttu-id="19c33-154">Gesplitste Interchange als transaction sets - transactie sets onderbreken bij fout: splitsingen interchange in transactie wordt ingesteld en wordt elke transactie set geparseerd.</span><span class="sxs-lookup"><span data-stu-id="19c33-154">Split Interchange as transaction sets - suspend transaction sets on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="19c33-155">Hallo X12 decoderen actie levert die transactie-sets die validatie niet doorstaan te`badMessages`, en levert Hallo resterende transacties te worden ingesteld als`goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="19c33-155">hello X12 Decode action outputs only those transaction sets that fail validation too`badMessages`, and outputs hello remaining transactions sets too`goodMessages`.</span></span>
  * <span data-ttu-id="19c33-156">Gesplitste Interchange als transaction sets - uitwisseling onderbreken bij fout: splitsingen interchange in transactie wordt ingesteld en wordt elke transactie set geparseerd.</span><span class="sxs-lookup"><span data-stu-id="19c33-156">Split Interchange as transaction sets - suspend interchange on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="19c33-157">Als een of meer transactie wordt ingesteld in Hallo interchange mislukken validatie, Hallo X12 decoderen actie levert alle Hallo transactie stelt in dat interchange te`badMessages`.</span><span class="sxs-lookup"><span data-stu-id="19c33-157">If one or more transaction sets in hello interchange fail validation, hello X12 Decode action outputs all hello transaction sets in that interchange too`badMessages`.</span></span>
  * <span data-ttu-id="19c33-158">Behouden DIF - transactie sets onderbreken bij fout: Preserve Hallo interchange en proces Hallo hele batch interchange.</span><span class="sxs-lookup"><span data-stu-id="19c33-158">Preserve Interchange - suspend transaction sets on error: Preserve hello interchange and process hello entire batched interchange.</span></span> 
  <span data-ttu-id="19c33-159">Hallo X12 decoderen actie levert die transactie-sets die validatie niet doorstaan te`badMessages`, en levert Hallo resterende transacties te worden ingesteld als`goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="19c33-159">hello X12 Decode action outputs only those transaction sets that fail validation too`badMessages`, and outputs hello remaining transactions sets too`goodMessages`.</span></span>
  * <span data-ttu-id="19c33-160">Behouden DIF - uitwisseling onderbreken bij fout: Preserve Hallo interchange en proces Hallo hele batch interchange.</span><span class="sxs-lookup"><span data-stu-id="19c33-160">Preserve Interchange - suspend interchange on error: Preserve hello interchange and process hello entire batched interchange.</span></span> 
  <span data-ttu-id="19c33-161">Als een of meer transactie wordt ingesteld in Hallo interchange mislukken validatie, Hallo X12 decoderen actie levert alle Hallo transactie stelt in dat interchange te`badMessages`.</span><span class="sxs-lookup"><span data-stu-id="19c33-161">If one or more transaction sets in hello interchange fail validation, hello X12 Decode action outputs all hello transaction sets in that interchange too`badMessages`.</span></span>
* <span data-ttu-id="19c33-162">Genereert een technische (beheer) en/of functionele bevestiging (indien geconfigureerd).</span><span class="sxs-lookup"><span data-stu-id="19c33-162">Generates a Technical (control) and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="19c33-163">Een technische bevestigings- of Hallo CONTRL ACK rapporten Hallo resultaten van een syntactische controle van de uitwisseling Hallo voltooid ontvangen.</span><span class="sxs-lookup"><span data-stu-id="19c33-163">A Technical Acknowledgment or hello CONTRL ACK reports hello results of a syntactical check of hello complete received interchange.</span></span>
  * <span data-ttu-id="19c33-164">Een functionele bevestiging erkent accepteren of weigeren van een ontvangen interchange of een groep</span><span class="sxs-lookup"><span data-stu-id="19c33-164">A functional acknowledgment acknowledges accept or reject a received interchange or a group</span></span>

## <a name="view-swagger-file"></a><span data-ttu-id="19c33-165">Swagger-bestand weergeven</span><span class="sxs-lookup"><span data-stu-id="19c33-165">View Swagger file</span></span>
<span data-ttu-id="19c33-166">tooview hello Swagger voor Hallo EDIFACT connector, Zie [EDIFACT](/connectors/edifact/).</span><span class="sxs-lookup"><span data-stu-id="19c33-166">tooview hello Swagger details for hello EDIFACT connector, see [EDIFACT](/connectors/edifact/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="19c33-167">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="19c33-167">Next steps</span></span>
[<span data-ttu-id="19c33-168">Meer informatie over Enterprise Integration Pack Hallo</span><span class="sxs-lookup"><span data-stu-id="19c33-168">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "meer informatie over Enterprise Integration Pack") 

