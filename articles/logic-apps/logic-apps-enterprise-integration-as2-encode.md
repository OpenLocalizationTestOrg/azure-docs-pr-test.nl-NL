---
title: berichten aaaEncode AS2 - Azure Logic Apps | Microsoft Docs
description: Hoe toouse AS2-codering in Hallo Enterprise Integration Pack Hallo voor Azure Logic Apps
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
ms.openlocfilehash: 2b372c416512ffa9ea5dc50ce0f767bfd8aefbc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="encode-as2-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="86148-103">AS2-berichten voor Azure Logic Apps Hello Enterprise Integration Pack coderen</span><span class="sxs-lookup"><span data-stu-id="86148-103">Encode AS2 messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="86148-104">tooestablish beveiliging en betrouwbaarheid tijdens de verzending van berichten, moet u Hallo coderen AS2 bericht connector gebruiken.</span><span class="sxs-lookup"><span data-stu-id="86148-104">tooestablish security and reliability while transmitting messages, use hello Encode AS2 message connector.</span></span> <span data-ttu-id="86148-105">Deze connector biedt digitale ondertekening, versleuteling en bevestigingen via bericht Disposition meldingen (MDN), wat ook toosupport voor niet-afwijzing leidt.</span><span class="sxs-lookup"><span data-stu-id="86148-105">This connector provides digital signing, encryption, and acknowledgements through Message Disposition Notifications (MDN), which also leads toosupport for Non-Repudiation.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="86148-106">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="86148-106">Before you start</span></span>

<span data-ttu-id="86148-107">Hier volgt Hallo items die u nodig:</span><span class="sxs-lookup"><span data-stu-id="86148-107">Here's hello items you need:</span></span>

* <span data-ttu-id="86148-108">Een Azure-account; kunt u een [gratis account](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="86148-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="86148-109">Een [integratie account](logic-apps-enterprise-integration-create-integration-account.md) die al is gedefinieerd en die zijn gekoppeld aan uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="86148-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="86148-110">U moet een connector integratie account toouse Hallo coderen AS2 bericht hebben.</span><span class="sxs-lookup"><span data-stu-id="86148-110">You must have an integration account toouse hello Encode AS2 message connector.</span></span>
* <span data-ttu-id="86148-111">Ten minste twee [partners](logic-apps-enterprise-integration-partners.md) die al zijn gedefinieerd in uw account integratie</span><span class="sxs-lookup"><span data-stu-id="86148-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="86148-112">Een [AS2-overeenkomst](logic-apps-enterprise-integration-as2.md) die al is gedefinieerd in uw account integratie</span><span class="sxs-lookup"><span data-stu-id="86148-112">An [AS2 agreement](logic-apps-enterprise-integration-as2.md) that's already defined in your integration account</span></span>

## <a name="encode-as2-messages"></a><span data-ttu-id="86148-113">AS2-berichten te coderen</span><span class="sxs-lookup"><span data-stu-id="86148-113">Encode AS2 messages</span></span>

1. <span data-ttu-id="86148-114">[Een logische app maken](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="86148-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="86148-115">Hallo coderen AS2-bericht connector geen triggers, dus moet u een trigger voor het starten van uw logische app, zoals een aanvraag-trigger toevoegen.</span><span class="sxs-lookup"><span data-stu-id="86148-115">hello Encode AS2 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="86148-116">In Hallo Logic App-ontwerper, een trigger toevoegen en voeg vervolgens een actie tooyour logische app.</span><span class="sxs-lookup"><span data-stu-id="86148-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="86148-117">Voer in het zoekvak hello, 'AS2' voor uw filter.</span><span class="sxs-lookup"><span data-stu-id="86148-117">In hello search box, enter "AS2" for your filter.</span></span> <span data-ttu-id="86148-118">Selecteer **AS2 - coderen AS2-bericht**.</span><span class="sxs-lookup"><span data-stu-id="86148-118">Select **AS2 - Encode AS2 message**.</span></span>
   
    ![Zoek naar 'AS2'](./media/logic-apps-enterprise-integration-as2-encode/as2decodeimage1.png)

4. <span data-ttu-id="86148-120">Als u niet alle verbindingen eerder tooyour integratie account maakt, wordt u gevraagd toocreate nu dat connection.</span><span class="sxs-lookup"><span data-stu-id="86148-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="86148-121">Naam van uw verbinding en Hallo integratie-account dat u wilt dat tooconnect selecteren.</span><span class="sxs-lookup"><span data-stu-id="86148-121">Name your connection, and select hello integration account that you want tooconnect.</span></span> 
   
    ![verbinding toointegration-account maken](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage1.png)  

    <span data-ttu-id="86148-123">Eigenschappen met een sterretje zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="86148-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="86148-124">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="86148-124">Property</span></span> | <span data-ttu-id="86148-125">Details</span><span class="sxs-lookup"><span data-stu-id="86148-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="86148-126">Verbindingsnaam *</span><span class="sxs-lookup"><span data-stu-id="86148-126">Connection Name *</span></span> |<span data-ttu-id="86148-127">Voer een naam voor de verbinding.</span><span class="sxs-lookup"><span data-stu-id="86148-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="86148-128">Integratie Account *</span><span class="sxs-lookup"><span data-stu-id="86148-128">Integration Account *</span></span> |<span data-ttu-id="86148-129">Voer een naam voor uw account integratie.</span><span class="sxs-lookup"><span data-stu-id="86148-129">Enter a name for your integration account.</span></span> <span data-ttu-id="86148-130">Zorg ervoor dat uw account en logica app voor integratie in Hallo dezelfde Azure-locatie.</span><span class="sxs-lookup"><span data-stu-id="86148-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="86148-131">Wanneer u bent klaar, ziet uw Verbindingsdetails vergelijkbaar toothis voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="86148-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="86148-132">maken van uw verbinding toofinish kiezen **maken**.</span><span class="sxs-lookup"><span data-stu-id="86148-132">toofinish creating your connection, choose **Create**.</span></span>
   
    ![de verbindingsdetails integratie](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage2.png)

6. <span data-ttu-id="86148-134">Nadat de verbinding is gemaakt, zoals in dit voorbeeld, vindt u informatie voor **AS2-van**, **AS2-tooidentifiers** zoals geconfigureerd in de overeenkomst en **hoofdtekst**, die is Hallo-bericht nettolading.</span><span class="sxs-lookup"><span data-stu-id="86148-134">After your connection is created, as shown in this example, provide details for **AS2-From**, **AS2-tooidentifiers** as configured in your agreement, and **Body**, which is hello message payload.</span></span>
   
    ![verplichte velden bieden](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage3.png)

## <a name="as2-encoder-details"></a><span data-ttu-id="86148-136">AS2-encoder details</span><span class="sxs-lookup"><span data-stu-id="86148-136">AS2 encoder details</span></span>

<span data-ttu-id="86148-137">Hallo coderen AS2-connector voert deze taken uit:</span><span class="sxs-lookup"><span data-stu-id="86148-137">hello Encode AS2 connector performs these tasks:</span></span> 

* <span data-ttu-id="86148-138">AS2/HTTP-headers van toepassing is</span><span class="sxs-lookup"><span data-stu-id="86148-138">Applies AS2/HTTP headers</span></span>
* <span data-ttu-id="86148-139">Tekenen uitgaande berichten (indien geconfigureerd)</span><span class="sxs-lookup"><span data-stu-id="86148-139">Signs outgoing messages (if configured)</span></span>
* <span data-ttu-id="86148-140">Versleutelt uitgaande berichten (indien geconfigureerd)</span><span class="sxs-lookup"><span data-stu-id="86148-140">Encrypts outgoing messages (if configured)</span></span>
* <span data-ttu-id="86148-141">Comprimeren van het Hallo-bericht (indien geconfigureerd)</span><span class="sxs-lookup"><span data-stu-id="86148-141">Compresses hello message (if configured)</span></span>

## <a name="try-this-sample"></a><span data-ttu-id="86148-142">Probeer dit voorbeeld</span><span class="sxs-lookup"><span data-stu-id="86148-142">Try this sample</span></span>

<span data-ttu-id="86148-143">een volledig operationeel logic app en voorbeeld AS2-scenario implementeren tootry Zie Hallo [AS2 logic app-sjabloon en het scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span><span class="sxs-lookup"><span data-stu-id="86148-143">tootry deploying a fully operational logic app and sample AS2 scenario, see hello [AS2 logic app template and scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="86148-144">Weergave Hallo swagger</span><span class="sxs-lookup"><span data-stu-id="86148-144">View hello swagger</span></span>
<span data-ttu-id="86148-145">Zie Hallo [swagger details](/connectors/as2/).</span><span class="sxs-lookup"><span data-stu-id="86148-145">See hello [swagger details](/connectors/as2/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="86148-146">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="86148-146">Next steps</span></span>
[<span data-ttu-id="86148-147">Meer informatie over Enterprise Integration Pack Hallo</span><span class="sxs-lookup"><span data-stu-id="86148-147">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "meer informatie over Enterprise Integration Pack") 

