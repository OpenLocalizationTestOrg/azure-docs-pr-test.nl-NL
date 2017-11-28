---
title: bijhouden van schema's voor B2B aaaCustom monitoring - Azure Logic Apps | Microsoft Docs
description: Bijhouden van aangepaste schema's toomonitor B2B-berichten van transacties in uw Azure-integratie-Account maken.
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 433ae852-a833-44d3-a3c3-14cca33403a2
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8cf26a43d89f0414a2a8c5ef59d804235afeb5d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-tracking-toomonitor-your-complete-workflow-end-to-end"></a><span data-ttu-id="67699-103">Uw volledige werkstroom, end-to-end voor bijhouden toomonitor inschakelen</span><span class="sxs-lookup"><span data-stu-id="67699-103">Enable tracking toomonitor your complete workflow, end-to-end</span></span>
<span data-ttu-id="67699-104">Er is ingebouwde bijhouden dat u voor de verschillende onderdelen van uw business-to-business-werkstroom, zoals bijhouden AS2 of X12 berichten inschakelen kunt.</span><span class="sxs-lookup"><span data-stu-id="67699-104">There is built-in tracking that you can enable for different parts of your business-to-business workflow, such as tracking AS2 or X12 messages.</span></span> <span data-ttu-id="67699-105">Wanneer u werkstromen met een logische app, BizTalk Server, SQL Server of een andere laag maakt, kunt u aangepaste bijhouden die legt gebeurtenissen van Hallo begin toohello einde van uw werkstroom vast.</span><span class="sxs-lookup"><span data-stu-id="67699-105">When you create workflows that includes a logic app, BizTalk Server, SQL Server, or any other layer, then you can enable custom tracking that logs events from hello beginning toohello end of your workflow.</span></span> 

<span data-ttu-id="67699-106">Dit onderwerp bevat aangepaste code die u in Hallo lagen buiten uw logische app gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="67699-106">This topic provides custom code that you can use in hello layers outside of your logic app.</span></span> 

## <a name="custom-tracking-schema"></a><span data-ttu-id="67699-107">Bijhouden van aangepaste schema</span><span class="sxs-lookup"><span data-stu-id="67699-107">Custom tracking schema</span></span>
````java

        {
            "sourceType": "",
            "source": {

            "workflow": {
                "systemId": ""
            },
            "runInstance": {
                "runId": ""
            },
            "operation": {
                "operationName": "",
                "repeatItemScopeName": "",
                "repeatItemIndex": "",
                "trackingId": "",
                "correlationId": "",
                "clientRequestId": ""
                }
            },
            "events": [
            {
                "eventLevel": "",
                "eventTime": "",
                "recordType": "",
                "record": {                
                }
            }
         ]
      }

````

| <span data-ttu-id="67699-108">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="67699-108">Property</span></span> | <span data-ttu-id="67699-109">Type</span><span class="sxs-lookup"><span data-stu-id="67699-109">Type</span></span> | <span data-ttu-id="67699-110">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="67699-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="67699-111">SourceType</span><span class="sxs-lookup"><span data-stu-id="67699-111">sourceType</span></span> |   | <span data-ttu-id="67699-112">Type bron Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="67699-112">Type of hello run source.</span></span> <span data-ttu-id="67699-113">Toegestane waarden zijn **Microsoft.Logic/workflows** en **aangepaste**.</span><span class="sxs-lookup"><span data-stu-id="67699-113">Allowed values are **Microsoft.Logic/workflows** and **custom**.</span></span> <span data-ttu-id="67699-114">(Verplicht)</span><span class="sxs-lookup"><span data-stu-id="67699-114">(Mandatory)</span></span> |
| <span data-ttu-id="67699-115">Bron</span><span class="sxs-lookup"><span data-stu-id="67699-115">Source</span></span> |   | <span data-ttu-id="67699-116">Als het brontype Hallo **Microsoft.Logic/workflows**, Hallo broninformatie moet toofollow dit schema.</span><span class="sxs-lookup"><span data-stu-id="67699-116">If hello source type is **Microsoft.Logic/workflows**, hello source information needs toofollow this schema.</span></span> <span data-ttu-id="67699-117">Als het brontype Hallo **aangepaste**, Hallo-schema is een JToken.</span><span class="sxs-lookup"><span data-stu-id="67699-117">If hello source type is **custom**, hello schema is a JToken.</span></span> <span data-ttu-id="67699-118">(Verplicht)</span><span class="sxs-lookup"><span data-stu-id="67699-118">(Mandatory)</span></span> |
| <span data-ttu-id="67699-119">systeem-id</span><span class="sxs-lookup"><span data-stu-id="67699-119">systemId</span></span> | <span data-ttu-id="67699-120">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="67699-120">String</span></span> | <span data-ttu-id="67699-121">Logic app systeem-ID.</span><span class="sxs-lookup"><span data-stu-id="67699-121">Logic app system ID.</span></span> <span data-ttu-id="67699-122">(Verplicht)</span><span class="sxs-lookup"><span data-stu-id="67699-122">(Mandatory)</span></span> |
| <span data-ttu-id="67699-123">runId</span><span class="sxs-lookup"><span data-stu-id="67699-123">runId</span></span> | <span data-ttu-id="67699-124">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="67699-124">String</span></span> | <span data-ttu-id="67699-125">Logische app uitgevoerd ID.</span><span class="sxs-lookup"><span data-stu-id="67699-125">Logic app run ID.</span></span> <span data-ttu-id="67699-126">(Verplicht)</span><span class="sxs-lookup"><span data-stu-id="67699-126">(Mandatory)</span></span> |
| <span data-ttu-id="67699-127">operationName</span><span class="sxs-lookup"><span data-stu-id="67699-127">operationName</span></span> | <span data-ttu-id="67699-128">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="67699-128">String</span></span> | <span data-ttu-id="67699-129">Naam van bewerking hello (bijvoorbeeld actie of trigger).</span><span class="sxs-lookup"><span data-stu-id="67699-129">Name of hello operation (for example, action or trigger).</span></span> <span data-ttu-id="67699-130">(Verplicht)</span><span class="sxs-lookup"><span data-stu-id="67699-130">(Mandatory)</span></span> |
| <span data-ttu-id="67699-131">repeatItemScopeName</span><span class="sxs-lookup"><span data-stu-id="67699-131">repeatItemScopeName</span></span> | <span data-ttu-id="67699-132">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="67699-132">String</span></span> | <span data-ttu-id="67699-133">Herhaal itemnaam als Hallo actie binnen een `foreach` / `until` lus.</span><span class="sxs-lookup"><span data-stu-id="67699-133">Repeat item name if hello action is inside a `foreach`/`until` loop.</span></span> <span data-ttu-id="67699-134">(Verplicht)</span><span class="sxs-lookup"><span data-stu-id="67699-134">(Mandatory)</span></span> |
| <span data-ttu-id="67699-135">repeatItemIndex</span><span class="sxs-lookup"><span data-stu-id="67699-135">repeatItemIndex</span></span> | <span data-ttu-id="67699-136">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="67699-136">Integer</span></span> | <span data-ttu-id="67699-137">Of Hallo actie is binnen een `foreach` / `until` lus.</span><span class="sxs-lookup"><span data-stu-id="67699-137">Whether hello action is inside a `foreach`/`until` loop.</span></span> <span data-ttu-id="67699-138">Hiermee wordt aangegeven Hallo herhaalde itemindex.</span><span class="sxs-lookup"><span data-stu-id="67699-138">Indicates hello repeated item index.</span></span> <span data-ttu-id="67699-139">(Verplicht)</span><span class="sxs-lookup"><span data-stu-id="67699-139">(Mandatory)</span></span> |
| <span data-ttu-id="67699-140">trackingId</span><span class="sxs-lookup"><span data-stu-id="67699-140">trackingId</span></span> | <span data-ttu-id="67699-141">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="67699-141">String</span></span> | <span data-ttu-id="67699-142">Tracerings-ID, toocorrelate Hallo-berichten.</span><span class="sxs-lookup"><span data-stu-id="67699-142">Tracking ID, toocorrelate hello messages.</span></span> <span data-ttu-id="67699-143">(Optioneel)</span><span class="sxs-lookup"><span data-stu-id="67699-143">(Optional)</span></span> |
| <span data-ttu-id="67699-144">correlationId</span><span class="sxs-lookup"><span data-stu-id="67699-144">correlationId</span></span> | <span data-ttu-id="67699-145">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="67699-145">String</span></span> | <span data-ttu-id="67699-146">Correlatie-ID, toocorrelate Hallo-berichten.</span><span class="sxs-lookup"><span data-stu-id="67699-146">Correlation ID, toocorrelate hello messages.</span></span> <span data-ttu-id="67699-147">(Optioneel)</span><span class="sxs-lookup"><span data-stu-id="67699-147">(Optional)</span></span> |
| <span data-ttu-id="67699-148">clientRequestId</span><span class="sxs-lookup"><span data-stu-id="67699-148">clientRequestId</span></span> | <span data-ttu-id="67699-149">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="67699-149">String</span></span> | <span data-ttu-id="67699-150">Client kan het vullen toocorrelate berichten.</span><span class="sxs-lookup"><span data-stu-id="67699-150">Client can populate it toocorrelate messages.</span></span> <span data-ttu-id="67699-151">(Optioneel)</span><span class="sxs-lookup"><span data-stu-id="67699-151">(Optional)</span></span> |
| <span data-ttu-id="67699-152">eventLevel</span><span class="sxs-lookup"><span data-stu-id="67699-152">eventLevel</span></span> |   | <span data-ttu-id="67699-153">Niveau van het Hallo-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="67699-153">Level of hello event.</span></span> <span data-ttu-id="67699-154">(Verplicht)</span><span class="sxs-lookup"><span data-stu-id="67699-154">(Mandatory)</span></span> |
| <span data-ttu-id="67699-155">eventTime</span><span class="sxs-lookup"><span data-stu-id="67699-155">eventTime</span></span> |   | <span data-ttu-id="67699-156">Tijd van de Hallo gebeurtenis, in UTC-notatie jjjj-MM-DDTHH:MM:SS.00000Z.</span><span class="sxs-lookup"><span data-stu-id="67699-156">Time of hello event, in UTC format YYYY-MM-DDTHH:MM:SS.00000Z.</span></span> <span data-ttu-id="67699-157">(Verplicht)</span><span class="sxs-lookup"><span data-stu-id="67699-157">(Mandatory)</span></span> |
| <span data-ttu-id="67699-158">recordType</span><span class="sxs-lookup"><span data-stu-id="67699-158">recordType</span></span> |   | <span data-ttu-id="67699-159">Type Hallo bijhouden record.</span><span class="sxs-lookup"><span data-stu-id="67699-159">Type of hello track record.</span></span> <span data-ttu-id="67699-160">De waarde is toegestaan **aangepaste**.</span><span class="sxs-lookup"><span data-stu-id="67699-160">Allowed value is **custom**.</span></span> <span data-ttu-id="67699-161">(Verplicht)</span><span class="sxs-lookup"><span data-stu-id="67699-161">(Mandatory)</span></span> |
| <span data-ttu-id="67699-162">Record</span><span class="sxs-lookup"><span data-stu-id="67699-162">record</span></span> |   | <span data-ttu-id="67699-163">Aangepaste recordtype.</span><span class="sxs-lookup"><span data-stu-id="67699-163">Custom record type.</span></span> <span data-ttu-id="67699-164">Toegestane indeling is JToken.</span><span class="sxs-lookup"><span data-stu-id="67699-164">Allowed format is JToken.</span></span> <span data-ttu-id="67699-165">(Verplicht)</span><span class="sxs-lookup"><span data-stu-id="67699-165">(Mandatory)</span></span> |

## <a name="b2b-protocol-tracking-schemas"></a><span data-ttu-id="67699-166">Schema's voor bijhouden van B2B-protocol</span><span class="sxs-lookup"><span data-stu-id="67699-166">B2B protocol tracking schemas</span></span>
<span data-ttu-id="67699-167">Zie voor informatie over B2B-protocol voor het bijhouden van schema's:</span><span class="sxs-lookup"><span data-stu-id="67699-167">For information about B2B protocol tracking schemas, see:</span></span>
* [<span data-ttu-id="67699-168">Volgschema’s voor AS2</span><span class="sxs-lookup"><span data-stu-id="67699-168">AS2 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)   
* [<span data-ttu-id="67699-169">Volgschema’s voor X12</span><span class="sxs-lookup"><span data-stu-id="67699-169">X12 tracking schemas</span></span>](logic-apps-track-integration-account-x12-tracking-schema.md)

## <a name="next-steps"></a><span data-ttu-id="67699-170">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="67699-170">Next steps</span></span>
* <span data-ttu-id="67699-171">Meer informatie over [B2B-berichten controleren](logic-apps-monitor-b2b-message.md).</span><span class="sxs-lookup"><span data-stu-id="67699-171">Learn more about [monitoring B2B messages](logic-apps-monitor-b2b-message.md).</span></span>   
* <span data-ttu-id="67699-172">Meer informatie over [B2B-berichten in de Operations Management Suite-portal Hallo traceren](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="67699-172">Learn about [tracking B2B messages in hello Operations Management Suite portal](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>
* <span data-ttu-id="67699-173">Meer informatie over Hallo [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="67699-173">Learn more about hello [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span></span>
