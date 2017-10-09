---
title: aaaEncode EDIFACT berichten - Azure Logic Apps | Microsoft Docs
description: EDI valideren en genereren van XML met EDIFACT berichtencoder in Enterprise Integration Pack Hallo voor Azure Logic Apps
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
ms.openlocfilehash: b3799dbd2492adef597022d017cf28f5ceb1085c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="encode-edifact-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="c7997-103">EDIFACT-berichten voor Azure Logic Apps Hello Enterprise Integration Pack coderen</span><span class="sxs-lookup"><span data-stu-id="c7997-103">Encode EDIFACT messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="c7997-104">Met Hallo coderen EDIFACT bericht connector, kunt u valideren EDI- en partner-specifieke eigenschappen, een XML-document voor elke set transactie genereren en aanvragen van een bevestiging van technische, functionele bevestiging of beide.</span><span class="sxs-lookup"><span data-stu-id="c7997-104">With hello Encode EDIFACT message connector, you can validate EDI and partner-specific properties, generate an XML document for each transaction set, and request a Technical Acknowledgement, Functional Acknowledgment, or both.</span></span>
<span data-ttu-id="c7997-105">toouse deze connector, moet u Hallo connector tooan bestaande trigger in uw logische app toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c7997-105">toouse this connector, you must add hello connector tooan existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="c7997-106">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="c7997-106">Before you start</span></span>

<span data-ttu-id="c7997-107">Hier volgt Hallo items die u nodig:</span><span class="sxs-lookup"><span data-stu-id="c7997-107">Here's hello items you need:</span></span>

* <span data-ttu-id="c7997-108">Een Azure-account; kunt u een [gratis account](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="c7997-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="c7997-109">Een [integratie account](logic-apps-enterprise-integration-create-integration-account.md) die al is gedefinieerd en die zijn gekoppeld aan uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="c7997-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="c7997-110">U moet een connector integratie account toouse Hallo coderen EDIFACT bericht hebben.</span><span class="sxs-lookup"><span data-stu-id="c7997-110">You must have an integration account toouse hello Encode EDIFACT message connector.</span></span> 
* <span data-ttu-id="c7997-111">Ten minste twee [partners](logic-apps-enterprise-integration-partners.md) die al zijn gedefinieerd in uw account integratie</span><span class="sxs-lookup"><span data-stu-id="c7997-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="c7997-112">Een [EDIFACT overeenkomst](logic-apps-enterprise-integration-edifact.md) die al is gedefinieerd in uw account integratie</span><span class="sxs-lookup"><span data-stu-id="c7997-112">An [EDIFACT agreement](logic-apps-enterprise-integration-edifact.md) that's already defined in your integration account</span></span>

## <a name="encode-edifact-messages"></a><span data-ttu-id="c7997-113">EDIFACT-berichten te coderen</span><span class="sxs-lookup"><span data-stu-id="c7997-113">Encode EDIFACT messages</span></span>

1. <span data-ttu-id="c7997-114">[Een logische app maken](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="c7997-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="c7997-115">Hallo coderen EDIFACT bericht connector geen triggers, dus moet u een trigger voor het starten van uw logische app, zoals een aanvraag-trigger toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c7997-115">hello Encode EDIFACT message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="c7997-116">In Hallo Logic App-ontwerper, een trigger toevoegen en voeg vervolgens een actie tooyour logische app.</span><span class="sxs-lookup"><span data-stu-id="c7997-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="c7997-117">Voer in het zoekvak hello, 'EDIFACT' als filter.</span><span class="sxs-lookup"><span data-stu-id="c7997-117">In hello search box, enter "EDIFACT" as your filter.</span></span> <span data-ttu-id="c7997-118">Selecteer een **coderen EDIFACT bericht met de Overeenkomstnaam** of **coderen tooEDIFACT bericht door identiteiten**.</span><span class="sxs-lookup"><span data-stu-id="c7997-118">Select either **Encode EDIFACT Message by agreement name** or **Encode tooEDIFACT message by identities**.</span></span>
   
    ![EDIFACT zoeken](media/logic-apps-enterprise-integration-edifact-encode/edifactdecodeimage1.png)  

3. <span data-ttu-id="c7997-120">Als u niet alle verbindingen eerder tooyour integratie account maakt, wordt u gevraagd toocreate nu dat connection.</span><span class="sxs-lookup"><span data-stu-id="c7997-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="c7997-121">Naam van uw verbinding en Hallo integratie-account dat u wilt dat tooconnect selecteren.</span><span class="sxs-lookup"><span data-stu-id="c7997-121">Name your connection, and select hello integration account that you want tooconnect.</span></span>

    ![integratie-account verbinding maken](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage1.png)  

    <span data-ttu-id="c7997-123">Eigenschappen met een sterretje zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="c7997-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="c7997-124">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="c7997-124">Property</span></span> | <span data-ttu-id="c7997-125">Details</span><span class="sxs-lookup"><span data-stu-id="c7997-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="c7997-126">Verbindingsnaam *</span><span class="sxs-lookup"><span data-stu-id="c7997-126">Connection Name *</span></span> |<span data-ttu-id="c7997-127">Voer een naam voor de verbinding.</span><span class="sxs-lookup"><span data-stu-id="c7997-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="c7997-128">Integratie Account *</span><span class="sxs-lookup"><span data-stu-id="c7997-128">Integration Account *</span></span> |<span data-ttu-id="c7997-129">Voer een naam voor uw account integratie.</span><span class="sxs-lookup"><span data-stu-id="c7997-129">Enter a name for your integration account.</span></span> <span data-ttu-id="c7997-130">Zorg ervoor dat uw account en logica app voor integratie in Hallo dezelfde Azure-locatie.</span><span class="sxs-lookup"><span data-stu-id="c7997-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="c7997-131">Wanneer u bent klaar, ziet uw Verbindingsdetails vergelijkbaar toothis voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="c7997-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="c7997-132">maken van uw verbinding toofinish kiezen **maken**.</span><span class="sxs-lookup"><span data-stu-id="c7997-132">toofinish creating your connection, choose **Create**.</span></span>

    ![de accountdetails verbinding integratie](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage2.png)

    <span data-ttu-id="c7997-134">De verbinding wordt nu gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c7997-134">Your connection is now created.</span></span>

    ![integratie-account verbinding is gemaakt](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage4.png)

#### <a name="encode-edifact-message-by-agreement-name"></a><span data-ttu-id="c7997-136">EDIFACT-bericht met de Overeenkomstnaam coderen</span><span class="sxs-lookup"><span data-stu-id="c7997-136">Encode EDIFACT Message by agreement name</span></span>

<span data-ttu-id="c7997-137">Als u hebt gekozen tooencode EDIFACT berichten door de naam van de overeenkomst, open Hallo **overeenkomst met de naam van EDIFACT** lijst, typ of Selecteer de naam van de overeenkomst EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="c7997-137">If you chose tooencode EDIFACT messages by agreement name, open hello **Name of EDIFACT agreement** list, enter or select your EDIFACT agreement name.</span></span> <span data-ttu-id="c7997-138">Voer Hallo XML-bericht tooencode.</span><span class="sxs-lookup"><span data-stu-id="c7997-138">Enter hello XML message tooencode.</span></span>

![Voer de naam van de overeenkomst EDIFACT en XML-bericht tooencode](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage6.png)

#### <a name="encode-edifact-message-by-identities"></a><span data-ttu-id="c7997-140">EDIFACT-bericht met identiteiten coderen</span><span class="sxs-lookup"><span data-stu-id="c7997-140">Encode EDIFACT Message by identities</span></span>

<span data-ttu-id="c7997-141">Als u tooencode EDIFACT berichten door identiteiten kiest, Voer Hallo afzender-id, kwalificatie afzender, ontvanger-id en ontvanger kwalificatie zoals geconfigureerd in uw EDIFACT-overeenkomst.</span><span class="sxs-lookup"><span data-stu-id="c7997-141">If you choose tooencode EDIFACT messages by identities, enter hello sender identifier, sender qualifier, receiver identifier, and receiver qualifier as configured in your EDIFACT agreement.</span></span> <span data-ttu-id="c7997-142">Selecteer Hallo XML-bericht tooencode.</span><span class="sxs-lookup"><span data-stu-id="c7997-142">Select hello XML message tooencode.</span></span>

![Geef identiteiten voor een afzender en ontvanger, selecteer van XML-bericht tooencode](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage7.png)

## <a name="edifact-encode-details"></a><span data-ttu-id="c7997-144">Details EDIFACT coderen</span><span class="sxs-lookup"><span data-stu-id="c7997-144">EDIFACT Encode details</span></span>

<span data-ttu-id="c7997-145">Hallo coderen EDIFACT connector voert deze taken uit:</span><span class="sxs-lookup"><span data-stu-id="c7997-145">hello Encode EDIFACT connector performs these tasks:</span></span> 

* <span data-ttu-id="c7997-146">Hallo overeenkomst oplossen door het overeenkomende Hallo afzender kwalificatie & -id en ontvanger kwalificatie en id</span><span class="sxs-lookup"><span data-stu-id="c7997-146">Resolve hello agreement by matching hello sender qualifier & identifier and receiver qualifier and identifier</span></span>
* <span data-ttu-id="c7997-147">Hallo EDI uitwisseling van berichten XML-indeling converteren naar EDI transactie sets in een Hallo interchange serialiseert.</span><span class="sxs-lookup"><span data-stu-id="c7997-147">Serializes hello EDI interchange, converting XML-encoded messages into EDI transaction sets in hello interchange.</span></span>
* <span data-ttu-id="c7997-148">Transactie set-header en trailer segmenten van toepassing is</span><span class="sxs-lookup"><span data-stu-id="c7997-148">Applies transaction set header and trailer segments</span></span>
* <span data-ttu-id="c7997-149">Genereren van een besturingselement interchange getal, een besturingselement groepsnummer en een getal voor het instellen van transactie voor elke uitgaande uitwisseling</span><span class="sxs-lookup"><span data-stu-id="c7997-149">Generates an interchange control number, a group control number, and a transaction set control number for each outgoing interchange</span></span>
* <span data-ttu-id="c7997-150">Vervangt scheidingstekens in Hallo-nettolading</span><span class="sxs-lookup"><span data-stu-id="c7997-150">Replaces separators in hello payload data</span></span>
* <span data-ttu-id="c7997-151">Valideert EDI en partner-specifieke eigenschappen</span><span class="sxs-lookup"><span data-stu-id="c7997-151">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="c7997-152">Schemavalidatie van Hallo transactie-set gegevenselementen volgens het schema voor Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="c7997-152">Schema validation of hello transaction-set data elements against hello message schema.</span></span>
  * <span data-ttu-id="c7997-153">EDI gevalideerd gegevenselementen transactie-set.</span><span class="sxs-lookup"><span data-stu-id="c7997-153">EDI validation performed on transaction-set data elements.</span></span>
  * <span data-ttu-id="c7997-154">Uitgebreide validatie uitgevoerd op van de transactie-set-gegevenselementen</span><span class="sxs-lookup"><span data-stu-id="c7997-154">Extended validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="c7997-155">Genereert een XML-document voor elke set transactie.</span><span class="sxs-lookup"><span data-stu-id="c7997-155">Generates an XML document for each transaction set.</span></span>
* <span data-ttu-id="c7997-156">Vraagt om bevestiging van de technische en/of functionele (indien geconfigureerd).</span><span class="sxs-lookup"><span data-stu-id="c7997-156">Requests a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="c7997-157">Een technische bevestiging duidt CONTRL het Hallo-bericht ontvangst van een knooppunt.</span><span class="sxs-lookup"><span data-stu-id="c7997-157">As a technical acknowledgment, hello CONTRL message indicates receipt of an interchange.</span></span>
  * <span data-ttu-id="c7997-158">Als een functionele bevestiging CONTRL het Hallo-bericht geeft aan acceptatie- of afwijzing van Hallo ontvangen interchange, groep of -bericht, een lijst met fouten of niet-ondersteunde functies</span><span class="sxs-lookup"><span data-stu-id="c7997-158">As a functional acknowledgment, hello CONTRL message indicates acceptance or rejection of hello received interchange, group, or message, with a list of errors or unsupported functionality</span></span>

## <a name="view-swagger-file"></a><span data-ttu-id="c7997-159">Swagger-bestand weergeven</span><span class="sxs-lookup"><span data-stu-id="c7997-159">View Swagger file</span></span>
<span data-ttu-id="c7997-160">tooview hello Swagger voor Hallo EDIFACT connector, Zie [EDIFACT](/connectors/edifact/).</span><span class="sxs-lookup"><span data-stu-id="c7997-160">tooview hello Swagger details for hello EDIFACT connector, see [EDIFACT](/connectors/edifact/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7997-161">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c7997-161">Next steps</span></span>
[<span data-ttu-id="c7997-162">Meer informatie over Enterprise Integration Pack Hallo</span><span class="sxs-lookup"><span data-stu-id="c7997-162">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "meer informatie over Enterprise Integration Pack") 

