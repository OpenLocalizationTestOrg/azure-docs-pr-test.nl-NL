---
title: aaaDecode X12 berichten - Azure Logic Apps | Microsoft Docs
description: EDI valideren en genereren van bevestigingen met Hallo X12 bericht decoder in Enterprise Integration Pack Hallo voor Azure Logic Apps
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 4fd48d2d-2008-4080-b6a1-8ae183b48131
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 1ffececca1ff835b319b64c85f86c421395833c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="decode-x12-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="765b3-103">Decoderen X12 berichten voor Azure Logic Apps Hello Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="765b3-103">Decode X12 messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="765b3-104">Met Hallo decoderen X12 bericht-connector, kunt u valideren Hallo envelop tegen een handelspartnerovereenkomst, valideren EDI- en partner-specifieke eigenschappen uitgewisseld in transacties sets splitsen of volledige uitgewisseld behouden en genereren ontvangstbevestigingen voor transacties verwerkt.</span><span class="sxs-lookup"><span data-stu-id="765b3-104">With hello Decode X12 message connector, you can validate hello envelope against a trading partner agreement, validate EDI and partner-specific properties, split interchanges into transactions sets or preserve entire interchanges, and generate acknowledgments for processed transactions.</span></span> <span data-ttu-id="765b3-105">toouse deze connector, moet u Hallo connector tooan bestaande trigger in uw logische app toevoegen.</span><span class="sxs-lookup"><span data-stu-id="765b3-105">toouse this connector, you must add hello connector tooan existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="765b3-106">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="765b3-106">Before you start</span></span>

<span data-ttu-id="765b3-107">Hier volgt Hallo items die u nodig:</span><span class="sxs-lookup"><span data-stu-id="765b3-107">Here's hello items you need:</span></span>

* <span data-ttu-id="765b3-108">Een Azure-account; kunt u een [gratis account](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="765b3-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="765b3-109">Een [integratie account](logic-apps-enterprise-integration-create-integration-account.md) die al is gedefinieerd en die zijn gekoppeld aan uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="765b3-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="765b3-110">U moet een connector integratie account toouse Hallo decoderen X12 bericht hebben.</span><span class="sxs-lookup"><span data-stu-id="765b3-110">You must have an integration account toouse hello Decode X12 message connector.</span></span>
* <span data-ttu-id="765b3-111">Ten minste twee [partners](logic-apps-enterprise-integration-partners.md) die al zijn gedefinieerd in uw account integratie</span><span class="sxs-lookup"><span data-stu-id="765b3-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="765b3-112">Een [X12 overeenkomst](logic-apps-enterprise-integration-x12.md) die al is gedefinieerd in uw account integratie</span><span class="sxs-lookup"><span data-stu-id="765b3-112">An [X12 agreement](logic-apps-enterprise-integration-x12.md) that's already defined in your integration account</span></span>

## <a name="decode-x12-messages"></a><span data-ttu-id="765b3-113">Decoderen X12 berichten</span><span class="sxs-lookup"><span data-stu-id="765b3-113">Decode X12 messages</span></span>

1. <span data-ttu-id="765b3-114">[Een logische app maken](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="765b3-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="765b3-115">Hallo decoderen X12 bericht connector geen triggers, dus moet u een trigger voor het starten van uw logische app, zoals een aanvraag-trigger toevoegen.</span><span class="sxs-lookup"><span data-stu-id="765b3-115">hello Decode X12 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="765b3-116">In Hallo Logic App-ontwerper, een trigger toevoegen en voeg vervolgens een actie tooyour logische app.</span><span class="sxs-lookup"><span data-stu-id="765b3-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="765b3-117">Voer in het zoekvak hello, 'x12' voor uw filter.</span><span class="sxs-lookup"><span data-stu-id="765b3-117">In hello search box, enter "x12" for your filter.</span></span> <span data-ttu-id="765b3-118">Selecteer **X12-decoderen X12 bericht**.</span><span class="sxs-lookup"><span data-stu-id="765b3-118">Select **X12 - Decode X12 message**.</span></span>
   
    ![Zoek naar 'x12'](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage1.png)  

3. <span data-ttu-id="765b3-120">Als u niet alle verbindingen eerder tooyour integratie account maakt, wordt u gevraagd toocreate nu dat connection.</span><span class="sxs-lookup"><span data-stu-id="765b3-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="765b3-121">Naam van uw verbinding en Hallo integratie-account dat u wilt dat tooconnect selecteren.</span><span class="sxs-lookup"><span data-stu-id="765b3-121">Name your connection, and select hello integration account that you want tooconnect.</span></span> 

    ![Bieden integratie Verbindingsdetails voor account](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage4.png)

    <span data-ttu-id="765b3-123">Eigenschappen met een sterretje zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="765b3-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="765b3-124">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="765b3-124">Property</span></span> | <span data-ttu-id="765b3-125">Details</span><span class="sxs-lookup"><span data-stu-id="765b3-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="765b3-126">Verbindingsnaam *</span><span class="sxs-lookup"><span data-stu-id="765b3-126">Connection Name *</span></span> |<span data-ttu-id="765b3-127">Voer een naam voor de verbinding.</span><span class="sxs-lookup"><span data-stu-id="765b3-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="765b3-128">Integratie Account *</span><span class="sxs-lookup"><span data-stu-id="765b3-128">Integration Account *</span></span> |<span data-ttu-id="765b3-129">Voer een naam voor uw account integratie.</span><span class="sxs-lookup"><span data-stu-id="765b3-129">Enter a name for your integration account.</span></span> <span data-ttu-id="765b3-130">Zorg ervoor dat uw account en logica app voor integratie in Hallo dezelfde Azure-locatie.</span><span class="sxs-lookup"><span data-stu-id="765b3-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="765b3-131">Wanneer u bent klaar, ziet uw Verbindingsdetails vergelijkbaar toothis voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="765b3-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="765b3-132">maken van uw verbinding toofinish kiezen **maken**.</span><span class="sxs-lookup"><span data-stu-id="765b3-132">toofinish creating your connection, choose **Create**.</span></span>
   
    ![de accountdetails verbinding integratie](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage5.png) 

6. <span data-ttu-id="765b3-134">Nadat de verbinding is gemaakt, zoals in dit voorbeeld, selecteer Hallo X12 plat bestand-bericht toodecode.</span><span class="sxs-lookup"><span data-stu-id="765b3-134">After your connection is created, as shown in this example, select hello X12 flat file message toodecode.</span></span>

    ![integratie-account verbinding is gemaakt](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage6.png) 

    <span data-ttu-id="765b3-136">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="765b3-136">For example:</span></span>

    ![Selecteer X12 platte bericht voor het decoderen van bestand](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage7.png) 

## <a name="x12-decode-details"></a><span data-ttu-id="765b3-138">X12 decoderen details</span><span class="sxs-lookup"><span data-stu-id="765b3-138">X12 Decode details</span></span>

<span data-ttu-id="765b3-139">Hallo X12 decoderen connector voert deze taken uit:</span><span class="sxs-lookup"><span data-stu-id="765b3-139">hello X12 Decode connector performs these tasks:</span></span>

* <span data-ttu-id="765b3-140">Valideert Hallo envelop tegen trading partner agreement</span><span class="sxs-lookup"><span data-stu-id="765b3-140">Validates hello envelope against trading partner agreement</span></span>
* <span data-ttu-id="765b3-141">Valideert EDI en partner-specifieke eigenschappen</span><span class="sxs-lookup"><span data-stu-id="765b3-141">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="765b3-142">Structurele EDI-validatie en uitgebreide schemavalidatie</span><span class="sxs-lookup"><span data-stu-id="765b3-142">EDI structural validation, and extended schema validation</span></span>
  * <span data-ttu-id="765b3-143">Validatie van de structuur van Hallo interchange envelop Hallo.</span><span class="sxs-lookup"><span data-stu-id="765b3-143">Validation of hello structure of hello interchange envelope.</span></span>
  * <span data-ttu-id="765b3-144">Schemavalidatie van Hallo envelop volgens het schema voor Hallo-besturingselement.</span><span class="sxs-lookup"><span data-stu-id="765b3-144">Schema validation of hello envelope against hello control schema.</span></span>
  * <span data-ttu-id="765b3-145">Schemavalidatie van Hallo transactie-set gegevenselementen volgens het schema voor Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="765b3-145">Schema validation of hello transaction-set data elements against hello message schema.</span></span>
  * <span data-ttu-id="765b3-146">EDI-validatie wordt uitgevoerd op transactie-set gegevenselementen</span><span class="sxs-lookup"><span data-stu-id="765b3-146">EDI validation performed on transaction-set data elements</span></span> 
* <span data-ttu-id="765b3-147">Controleert of Hallo interchange, groep en transactie set besturingselement getallen zijn niet identiek</span><span class="sxs-lookup"><span data-stu-id="765b3-147">Verifies that hello interchange, group, and transaction set control numbers are not duplicates</span></span>
  * <span data-ttu-id="765b3-148">Hallo interchange controle-aantal tegen eerder ontvangen uitgewisseld controleert.</span><span class="sxs-lookup"><span data-stu-id="765b3-148">Checks hello interchange control number against previously received interchanges.</span></span>
  * <span data-ttu-id="765b3-149">Hallo groepsnummer beheer op basis van andere getallen groep besturingselement in Hallo interchange controleert.</span><span class="sxs-lookup"><span data-stu-id="765b3-149">Checks hello group control number against other group control numbers in hello interchange.</span></span>
  * <span data-ttu-id="765b3-150">Controleert Hallo transactie controle-aantal ingesteld op basis van andere cijfers voor het instellen van transactie in die groep.</span><span class="sxs-lookup"><span data-stu-id="765b3-150">Checks hello transaction set control number against other transaction set control numbers in that group.</span></span>
* <span data-ttu-id="765b3-151">Hallo interchange in transactie sets splitst of behoudt de gehele uitwisseling Hallo:</span><span class="sxs-lookup"><span data-stu-id="765b3-151">Splits hello interchange into transaction sets, or preserves hello entire interchange:</span></span>
  * <span data-ttu-id="765b3-152">Gesplitste Interchange als transaction sets - transactie sets onderbreken bij fout: splitsingen interchange in transactie wordt ingesteld en wordt elke transactie set geparseerd.</span><span class="sxs-lookup"><span data-stu-id="765b3-152">Split Interchange as transaction sets - suspend transaction sets on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="765b3-153">Hallo X12 decoderen actie levert die transactie-sets die validatie niet doorstaan te`badMessages`, en levert Hallo resterende transacties te worden ingesteld als`goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="765b3-153">hello X12 Decode action outputs only those transaction sets that fail validation too`badMessages`, and outputs hello remaining transactions sets too`goodMessages`.</span></span>
  * <span data-ttu-id="765b3-154">Gesplitste Interchange als transaction sets - uitwisseling onderbreken bij fout: splitsingen interchange in transactie wordt ingesteld en wordt elke transactie set geparseerd.</span><span class="sxs-lookup"><span data-stu-id="765b3-154">Split Interchange as transaction sets - suspend interchange on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="765b3-155">Als een of meer transactie wordt ingesteld in Hallo interchange mislukken validatie, Hallo X12 decoderen actie levert alle Hallo transactie stelt in dat interchange te`badMessages`.</span><span class="sxs-lookup"><span data-stu-id="765b3-155">If one or more transaction sets in hello interchange fail validation, hello X12 Decode action outputs all hello transaction sets in that interchange too`badMessages`.</span></span>
  * <span data-ttu-id="765b3-156">Behouden DIF - transactie sets onderbreken bij fout: Preserve Hallo interchange en proces Hallo hele batch interchange.</span><span class="sxs-lookup"><span data-stu-id="765b3-156">Preserve Interchange - suspend transaction sets on error: Preserve hello interchange and process hello entire batched interchange.</span></span> 
  <span data-ttu-id="765b3-157">Hallo X12 decoderen actie levert die transactie-sets die validatie niet doorstaan te`badMessages`, en levert Hallo resterende transacties te worden ingesteld als`goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="765b3-157">hello X12 Decode action outputs only those transaction sets that fail validation too`badMessages`, and outputs hello remaining transactions sets too`goodMessages`.</span></span>
  * <span data-ttu-id="765b3-158">Behouden DIF - uitwisseling onderbreken bij fout: Preserve Hallo interchange en proces Hallo hele batch interchange.</span><span class="sxs-lookup"><span data-stu-id="765b3-158">Preserve Interchange - suspend interchange on error: Preserve hello interchange and process hello entire batched interchange.</span></span> 
  <span data-ttu-id="765b3-159">Als een of meer transactie wordt ingesteld in Hallo interchange mislukken validatie, Hallo X12 decoderen actie levert alle Hallo transactie stelt in dat interchange te`badMessages`.</span><span class="sxs-lookup"><span data-stu-id="765b3-159">If one or more transaction sets in hello interchange fail validation, hello X12 Decode action outputs all hello transaction sets in that interchange too`badMessages`.</span></span> 
* <span data-ttu-id="765b3-160">Genereert een bevestiging technische en/of functionele (indien geconfigureerd).</span><span class="sxs-lookup"><span data-stu-id="765b3-160">Generates a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="765b3-161">Een technische bevestiging genereert als gevolg van header-validatie.</span><span class="sxs-lookup"><span data-stu-id="765b3-161">A Technical Acknowledgment generates as a result of header validation.</span></span> <span data-ttu-id="765b3-162">Hallo technische bevestiging gerapporteerd Hallo van Hallo verwerking van een DIF-header en trailer door Hallo adres ontvanger.</span><span class="sxs-lookup"><span data-stu-id="765b3-162">hello technical acknowledgment reports hello status of hello processing of an interchange header and trailer by hello address receiver.</span></span>
  * <span data-ttu-id="765b3-163">Een functionele bevestiging genereert als gevolg van validatie van de hoofdtekst.</span><span class="sxs-lookup"><span data-stu-id="765b3-163">A Functional Acknowledgment generates as a result of body validation.</span></span> <span data-ttu-id="765b3-164">Hallo rapporten functionele bevestiging elke fout is opgetreden bij het verwerken Hallo document ontvangen</span><span class="sxs-lookup"><span data-stu-id="765b3-164">hello functional acknowledgment reports each error encountered while processing hello received document</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="765b3-165">Weergave Hallo swagger</span><span class="sxs-lookup"><span data-stu-id="765b3-165">View hello swagger</span></span>
<span data-ttu-id="765b3-166">Zie Hallo [swagger details](/connectors/x12/).</span><span class="sxs-lookup"><span data-stu-id="765b3-166">See hello [swagger details](/connectors/x12/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="765b3-167">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="765b3-167">Next steps</span></span>
[<span data-ttu-id="765b3-168">Meer informatie over Enterprise Integration Pack Hallo</span><span class="sxs-lookup"><span data-stu-id="765b3-168">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "meer informatie over Enterprise Integration Pack") 

