---
title: aaaEncode X12 berichten - Azure Logic Apps | Microsoft Docs
description: EDI valideren en converteren XML-codering berichten met X12 bericht encoder in Enterprise Integration Pack Hallo voor Azure Logic Apps
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: a01e9ca9-816b-479e-ab11-4a984f10f62d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 785dbd2c7c82463154732921e07e3586d2307840
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="encode-x12-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="5940a-103">Codeer X12 berichten voor Azure Logic Apps Hello Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="5940a-103">Encode X12 messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="5940a-104">Met Hallo coderen X12 bericht connector kunt u valideren EDI- en partner-specifieke eigenschappen, XML-codering berichten converteren naar EDI transactie sets in een Hallo interchange en aanvragen van een bevestiging van technische, functionele bevestiging of beide.</span><span class="sxs-lookup"><span data-stu-id="5940a-104">With hello Encode X12 message connector, you can validate EDI and partner-specific properties, convert XML-encoded messages into EDI transaction sets in hello interchange, and request a Technical Acknowledgement, Functional Acknowledgment, or both.</span></span>
<span data-ttu-id="5940a-105">toouse deze connector, moet u Hallo connector tooan bestaande trigger in uw logische app toevoegen.</span><span class="sxs-lookup"><span data-stu-id="5940a-105">toouse this connector, you must add hello connector tooan existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="5940a-106">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="5940a-106">Before you start</span></span>

<span data-ttu-id="5940a-107">Hier volgt Hallo items die u nodig:</span><span class="sxs-lookup"><span data-stu-id="5940a-107">Here's hello items you need:</span></span>

* <span data-ttu-id="5940a-108">Een Azure-account; kunt u een [gratis account](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="5940a-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="5940a-109">Een [integratie account](logic-apps-enterprise-integration-create-integration-account.md) die al is gedefinieerd en die zijn gekoppeld aan uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="5940a-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="5940a-110">U moet een connector integratie account toouse Hallo coderen X12 bericht hebben.</span><span class="sxs-lookup"><span data-stu-id="5940a-110">You must have an integration account toouse hello Encode X12 message connector.</span></span>
* <span data-ttu-id="5940a-111">Ten minste twee [partners](logic-apps-enterprise-integration-partners.md) die al zijn gedefinieerd in uw account integratie</span><span class="sxs-lookup"><span data-stu-id="5940a-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="5940a-112">Een [X12 overeenkomst](logic-apps-enterprise-integration-x12.md) die al is gedefinieerd in uw account integratie</span><span class="sxs-lookup"><span data-stu-id="5940a-112">An [X12 agreement](logic-apps-enterprise-integration-x12.md) that's already defined in your integration account</span></span>

## <a name="encode-x12-messages"></a><span data-ttu-id="5940a-113">Codeer X12 berichten</span><span class="sxs-lookup"><span data-stu-id="5940a-113">Encode X12 messages</span></span>

1. <span data-ttu-id="5940a-114">[Een logische app maken](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="5940a-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="5940a-115">Hallo coderen X12 bericht connector geen triggers, dus moet u een trigger voor het starten van uw logische app, zoals een aanvraag-trigger toevoegen.</span><span class="sxs-lookup"><span data-stu-id="5940a-115">hello Encode X12 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="5940a-116">In Hallo Logic App-ontwerper, een trigger toevoegen en voeg vervolgens een actie tooyour logische app.</span><span class="sxs-lookup"><span data-stu-id="5940a-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="5940a-117">Voer in het zoekvak hello, 'x12' voor uw filter.</span><span class="sxs-lookup"><span data-stu-id="5940a-117">In hello search box, enter "x12" for your filter.</span></span> <span data-ttu-id="5940a-118">Selecteer een **X12-tooX12 bericht coderen door de naam van de overeenkomst** of **X12-tooX12 bericht coderen met identiteiten**.</span><span class="sxs-lookup"><span data-stu-id="5940a-118">Select either **X12 - Encode tooX12 message by agreement name** or **X12 - Encode tooX12 message by identities**.</span></span>
   
    ![Zoek naar 'x12'](./media/logic-apps-enterprise-integration-x12-encode/x12decodeimage1.png) 

3. <span data-ttu-id="5940a-120">Als u niet alle verbindingen eerder tooyour integratie account maakt, wordt u gevraagd toocreate nu dat connection.</span><span class="sxs-lookup"><span data-stu-id="5940a-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="5940a-121">Naam van uw verbinding en Hallo integratie-account dat u wilt dat tooconnect selecteren.</span><span class="sxs-lookup"><span data-stu-id="5940a-121">Name your connection, and select hello integration account that you want tooconnect.</span></span> 
   
    ![integratie-account verbinding](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage1.png)

    <span data-ttu-id="5940a-123">Eigenschappen met een sterretje zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="5940a-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="5940a-124">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="5940a-124">Property</span></span> | <span data-ttu-id="5940a-125">Details</span><span class="sxs-lookup"><span data-stu-id="5940a-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="5940a-126">Verbindingsnaam *</span><span class="sxs-lookup"><span data-stu-id="5940a-126">Connection Name *</span></span> |<span data-ttu-id="5940a-127">Voer een naam voor de verbinding.</span><span class="sxs-lookup"><span data-stu-id="5940a-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="5940a-128">Integratie Account *</span><span class="sxs-lookup"><span data-stu-id="5940a-128">Integration Account *</span></span> |<span data-ttu-id="5940a-129">Voer een naam voor uw account integratie.</span><span class="sxs-lookup"><span data-stu-id="5940a-129">Enter a name for your integration account.</span></span> <span data-ttu-id="5940a-130">Zorg ervoor dat uw account en logica app voor integratie in Hallo dezelfde Azure-locatie.</span><span class="sxs-lookup"><span data-stu-id="5940a-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="5940a-131">Wanneer u bent klaar, ziet uw Verbindingsdetails vergelijkbaar toothis voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="5940a-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="5940a-132">maken van uw verbinding toofinish kiezen **maken**.</span><span class="sxs-lookup"><span data-stu-id="5940a-132">toofinish creating your connection, choose **Create**.</span></span>

    ![integratie-account verbinding is gemaakt](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage2.png)

    <span data-ttu-id="5940a-134">De verbinding wordt nu gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5940a-134">Your connection is now created.</span></span>

    ![de accountdetails verbinding integratie](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage3.png) 

#### <a name="encode-x12-messages-by-agreement-name"></a><span data-ttu-id="5940a-136">Codeer X12 berichten door de naam van de overeenkomst</span><span class="sxs-lookup"><span data-stu-id="5940a-136">Encode X12 messages by agreement name</span></span>

<span data-ttu-id="5940a-137">Als u hebt gekozen tooencode X12 berichten door de naam van de overeenkomst, open Hallo **naam van X12 overeenkomst** lijst Typ of Selecteer uw bestaande X12 overeenkomst.</span><span class="sxs-lookup"><span data-stu-id="5940a-137">If you chose tooencode X12 messages by agreement name, open hello **Name of X12 agreement** list, enter or select your existing X12 agreement.</span></span> <span data-ttu-id="5940a-138">Voer Hallo XML-bericht tooencode.</span><span class="sxs-lookup"><span data-stu-id="5940a-138">Enter hello XML message tooencode.</span></span>

![Voer X12 overeenkomst naam en het XML-bericht tooencode](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage4.png)

#### <a name="encode-x12-messages-by-identities"></a><span data-ttu-id="5940a-140">Codeer X12 berichten door identiteiten</span><span class="sxs-lookup"><span data-stu-id="5940a-140">Encode X12 messages by identities</span></span>

<span data-ttu-id="5940a-141">Als u tooencode X12 berichten door identiteiten kiest, Hallo afzender-id, kwalificatie afzender, ontvanger-id en ontvanger kwalificatie invoeren zoals geconfigureerd in uw x12-overeenkomst(en) overeenkomst.</span><span class="sxs-lookup"><span data-stu-id="5940a-141">If you choose tooencode X12 messages by identities, enter hello sender identifier, sender qualifier, receiver identifier, and receiver qualifier as configured in your X12 agreement.</span></span> <span data-ttu-id="5940a-142">Selecteer Hallo XML-bericht tooencode.</span><span class="sxs-lookup"><span data-stu-id="5940a-142">Select hello XML message tooencode.</span></span>
   
![Geef identiteiten voor een afzender en ontvanger, selecteer van XML-bericht tooencode](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage5.png) 

## <a name="x12-encode-details"></a><span data-ttu-id="5940a-144">X12 details coderen</span><span class="sxs-lookup"><span data-stu-id="5940a-144">X12 Encode details</span></span>

<span data-ttu-id="5940a-145">Hallo X12 coderen connector voert deze taken uit:</span><span class="sxs-lookup"><span data-stu-id="5940a-145">hello X12 Encode connector performs these tasks:</span></span>

* <span data-ttu-id="5940a-146">De resolutie van de overeenkomst door overeenkomende zender en ontvanger context-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="5940a-146">Agreement resolution by matching sender and receiver context properties.</span></span>
* <span data-ttu-id="5940a-147">Hallo EDI uitwisseling van berichten XML-indeling converteren naar EDI transactie sets in een Hallo interchange serialiseert.</span><span class="sxs-lookup"><span data-stu-id="5940a-147">Serializes hello EDI interchange, converting XML-encoded messages into EDI transaction sets in hello interchange.</span></span>
* <span data-ttu-id="5940a-148">Transactie set-header en trailer segmenten van toepassing is</span><span class="sxs-lookup"><span data-stu-id="5940a-148">Applies transaction set header and trailer segments</span></span>
* <span data-ttu-id="5940a-149">Genereren van een besturingselement interchange getal, een besturingselement groepsnummer en een getal voor het instellen van transactie voor elke uitgaande uitwisseling</span><span class="sxs-lookup"><span data-stu-id="5940a-149">Generates an interchange control number, a group control number, and a transaction set control number for each outgoing interchange</span></span>
* <span data-ttu-id="5940a-150">Vervangt scheidingstekens in Hallo-nettolading</span><span class="sxs-lookup"><span data-stu-id="5940a-150">Replaces separators in hello payload data</span></span>
* <span data-ttu-id="5940a-151">Valideert EDI en partner-specifieke eigenschappen</span><span class="sxs-lookup"><span data-stu-id="5940a-151">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="5940a-152">Schemavalidatie van Hallo transactie-set gegevenselementen tegen Schema het Hallo-bericht</span><span class="sxs-lookup"><span data-stu-id="5940a-152">Schema validation of hello transaction-set data elements against hello message Schema</span></span>
  * <span data-ttu-id="5940a-153">EDI gevalideerd gegevenselementen transactie-set.</span><span class="sxs-lookup"><span data-stu-id="5940a-153">EDI validation performed on transaction-set data elements.</span></span>
  * <span data-ttu-id="5940a-154">Uitgebreide validatie uitgevoerd op van de transactie-set-gegevenselementen</span><span class="sxs-lookup"><span data-stu-id="5940a-154">Extended validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="5940a-155">Vraagt om bevestiging van de technische en/of functionele (indien geconfigureerd).</span><span class="sxs-lookup"><span data-stu-id="5940a-155">Requests a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="5940a-156">Een technische bevestiging genereert als gevolg van header-validatie.</span><span class="sxs-lookup"><span data-stu-id="5940a-156">A Technical Acknowledgment generates as a result of header validation.</span></span> <span data-ttu-id="5940a-157">Hallo technische bevestiging rapporten Hallo status van Hallo verwerking van een DIF-header en trailer door Hallo adres ontvanger</span><span class="sxs-lookup"><span data-stu-id="5940a-157">hello technical acknowledgment reports hello status of hello processing of an interchange header and trailer by hello address receiver</span></span>
  * <span data-ttu-id="5940a-158">Een functionele bevestiging genereert als gevolg van validatie van de hoofdtekst.</span><span class="sxs-lookup"><span data-stu-id="5940a-158">A Functional Acknowledgment generates as a result of body validation.</span></span> <span data-ttu-id="5940a-159">Hallo rapporten functionele bevestiging elke fout is opgetreden bij het verwerken Hallo document ontvangen</span><span class="sxs-lookup"><span data-stu-id="5940a-159">hello functional acknowledgment reports each error encountered while processing hello received document</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="5940a-160">Weergave Hallo swagger</span><span class="sxs-lookup"><span data-stu-id="5940a-160">View hello swagger</span></span>
<span data-ttu-id="5940a-161">Zie Hallo [swagger details](/connectors/x12/).</span><span class="sxs-lookup"><span data-stu-id="5940a-161">See hello [swagger details](/connectors/x12/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5940a-162">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5940a-162">Next steps</span></span>
[<span data-ttu-id="5940a-163">Meer informatie over Enterprise Integration Pack Hallo</span><span class="sxs-lookup"><span data-stu-id="5940a-163">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "meer informatie over Enterprise Integration Pack") 

