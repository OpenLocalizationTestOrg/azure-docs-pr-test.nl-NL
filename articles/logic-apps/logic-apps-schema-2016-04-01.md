---
title: aaaSchema updates 1 juni 2016 - Azure Logic Apps | Microsoft Docs
description: JSON-definities voor Azure Logic Apps maken met schemaversie 2016-06-01
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 349d57e8-f62b-4ec6-a92f-a6e0242d6c0e
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/25/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: b0347fbbd692a93b63a2f8b741402a225450b35a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="schema-updates-for-azure-logic-apps---june-1-2016"></a><span data-ttu-id="59c6e-103">Schema-updates voor Azure Logic Apps - 1 juni 2016</span><span class="sxs-lookup"><span data-stu-id="59c6e-103">Schema updates for Azure Logic Apps - June 1, 2016</span></span>

<span data-ttu-id="59c6e-104">Deze nieuwe schema en de API-versie voor Azure Logic Apps bevat belangrijke verbeteringen die het maken van logische apps meer betrouwbare en gemakkelijker toouse:</span><span class="sxs-lookup"><span data-stu-id="59c6e-104">This new schema and API version for Azure Logic Apps includes key improvements that make logic apps more reliable and easier toouse:</span></span>

* <span data-ttu-id="59c6e-105">[Scopes](#scopes) kunt u een groep of acties nesten als een verzameling van acties.</span><span class="sxs-lookup"><span data-stu-id="59c6e-105">[Scopes](#scopes) let you group or nest actions as a collection of actions.</span></span>
* <span data-ttu-id="59c6e-106">[Voorwaarden en lussen](#conditions-loops) zijn nu klas acties.</span><span class="sxs-lookup"><span data-stu-id="59c6e-106">[Conditions and loops](#conditions-loops) are now first-class actions.</span></span>
* <span data-ttu-id="59c6e-107">Nauwkeurigere ordening voor het uitvoeren van acties met Hallo `runAfter` eigenschap vervangen`dependsOn`</span><span class="sxs-lookup"><span data-stu-id="59c6e-107">More precise ordering for running actions with hello `runAfter` property, replacing `dependsOn`</span></span>

<span data-ttu-id="59c6e-108">uw logische apps van 1 augustus 2015 Hallo tooupgrade preview-schema toohello 1 juni 2016 schema [uitchecken sectie Hallo-upgrade](##upgrade-your-schema).</span><span class="sxs-lookup"><span data-stu-id="59c6e-108">tooupgrade your logic apps from hello August 1, 2015 preview schema toohello June 1, 2016 schema, [check out hello upgrade section](##upgrade-your-schema).</span></span>

<a name="scopes"></a>
## <a name="scopes"></a><span data-ttu-id="59c6e-109">Scopes</span><span class="sxs-lookup"><span data-stu-id="59c6e-109">Scopes</span></span>

<span data-ttu-id="59c6e-110">Dit schema bevat bereiken, waarmee u groep samen of nest acties in de andere.</span><span class="sxs-lookup"><span data-stu-id="59c6e-110">This schema includes scopes, which let you group actions together, or nest actions inside each other.</span></span> <span data-ttu-id="59c6e-111">Een voorwaarde kan bijvoorbeeld een voorwaarde bevatten.</span><span class="sxs-lookup"><span data-stu-id="59c6e-111">For example, a condition can contain another condition.</span></span> <span data-ttu-id="59c6e-112">Meer informatie over [bereik syntaxis](../logic-apps/logic-apps-loops-and-scopes.md), of in dit voorbeeld basic bereik bekijken:</span><span class="sxs-lookup"><span data-stu-id="59c6e-112">Learn more about [scope syntax](../logic-apps/logic-apps-loops-and-scopes.md), or review this basic scope example:</span></span>

```
{
    "actions": {
        "My_Scope": {
            "type": "scope",
            "actions": {                
                "Http": {
                    "inputs": {
                        "method": "GET",
                        "uri": "http://www.bing.com"
                    },
                    "runAfter": {},
                    "type": "Http"
                }
            }
        }
    }
}
```

<a name="conditions-loops"></a>
## <a name="conditions-and-loops-changes"></a><span data-ttu-id="59c6e-113">Voorwaarden en lussen wijzigingen</span><span class="sxs-lookup"><span data-stu-id="59c6e-113">Conditions and loops changes</span></span>

<span data-ttu-id="59c6e-114">Zijn parameters die zijn gekoppeld aan één actie in het schema van vorige versies, de voorwaarden en lussen.</span><span class="sxs-lookup"><span data-stu-id="59c6e-114">In previous schema versions, conditions and loops were parameters associated with a single action.</span></span> <span data-ttu-id="59c6e-115">Dit schema liftonderhoud deze beperking, zodat de voorwaarden en lussen nu worden weergegeven als actietypen.</span><span class="sxs-lookup"><span data-stu-id="59c6e-115">This schema lifts this limitation, so conditions and loops now appear as action types.</span></span> <span data-ttu-id="59c6e-116">Meer informatie over [lussen en -scopes](../logic-apps/logic-apps-loops-and-scopes.md), of dit eenvoudige voorbeeld voor een actie voorwaarde bekijken:</span><span class="sxs-lookup"><span data-stu-id="59c6e-116">Learn more about [loops and scopes](../logic-apps/logic-apps-loops-and-scopes.md), or review this basic example for a condition action:</span></span>

```
{
    "If_trigger_is_some-trigger": {
        "type": "If",
        "expression": "@equals(triggerBody(), 'some-trigger')",
        "runAfter": { },
        "actions": {
            "Http_2": {
                "inputs": {
                    "method": "GET",
                    "uri": "http://www.bing.com"
                },
                "runAfter": {},
                "type": "Http"
            }
        },
        "else": 
        {
            "if_trigger_is_another-trigger": "..."
        }      
    }
}
```

<a name="run-after"></a>
## <a name="runafter-property"></a><span data-ttu-id="59c6e-117">de eigenschap 'runAfter'</span><span class="sxs-lookup"><span data-stu-id="59c6e-117">'runAfter' property</span></span>

<span data-ttu-id="59c6e-118">Hallo `runAfter` eigenschap vervangt `dependsOn`, mits nauwkeuriger wanneer u Hallo uitvoeren om acties opgeeft die is gebaseerd op Hallo status van vorige acties.</span><span class="sxs-lookup"><span data-stu-id="59c6e-118">hello `runAfter` property replaces `dependsOn`, providing more precision when you specify hello run order for actions based on hello status of previous actions.</span></span>

<span data-ttu-id="59c6e-119">Hallo `dependsOn` eigenschap is gelijk aan 'hello actie is uitgevoerd en is geslaagd', ongeacht hoe vaak de gewenste tooexecute een actie op basis van of de vorige actie Hallo geslaagd is, mislukt of overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="59c6e-119">hello `dependsOn` property was synonymous with "hello action ran and was successful", no matter how many times you wanted tooexecute an action, based on whether hello previous action was successful, failed, or skipped.</span></span> <span data-ttu-id="59c6e-120">Hallo `runAfter` eigenschap die flexibel als een object dat Hiermee geeft u alle Hallo actienamen waarna Hallo-object wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="59c6e-120">hello `runAfter` property provides that flexibility as an object that specifies all hello action names after which hello object runs.</span></span> <span data-ttu-id="59c6e-121">Deze eigenschap bepaalt ook een matrix van statussen die geaccepteerd als triggers worden.</span><span class="sxs-lookup"><span data-stu-id="59c6e-121">This property also defines an array of statuses that are acceptable as triggers.</span></span> <span data-ttu-id="59c6e-122">Bijvoorbeeld, als u toorun wilde nadat lukt de stap A en ook na stap B is gelukt of mislukt, u samenstellen dit `runAfter` eigenschap:</span><span class="sxs-lookup"><span data-stu-id="59c6e-122">For example, if you wanted toorun after step A succeeds and also after step B succeeds or fails, you construct this `runAfter` property:</span></span>

```
{
    "...",
    "runAfter": {
        "A": ["Succeeded"],
        "B": ["Succeeded", "Failed"]
    }
}
```

## <a name="upgrade-your-schema"></a><span data-ttu-id="59c6e-123">Uw schema bijwerken</span><span class="sxs-lookup"><span data-stu-id="59c6e-123">Upgrade your schema</span></span>

<span data-ttu-id="59c6e-124">Toohello upgraden duurt nieuwe schema slechts een paar stappen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="59c6e-124">Upgrading toohello new schema only takes a few steps.</span></span> <span data-ttu-id="59c6e-125">Hallo upgradeproces bevat uitgevoerd Hallo upgrade-script, op te slaan als een nieuwe logische app, en als u wilt, mogelijk Hallo vorige logische app overschrijven.</span><span class="sxs-lookup"><span data-stu-id="59c6e-125">hello upgrade process includes running hello upgrade script, saving as a new logic app, and if you want, possibly overwriting hello previous logic app.</span></span>

1. <span data-ttu-id="59c6e-126">Open uw logische app in Azure-portal hello.</span><span class="sxs-lookup"><span data-stu-id="59c6e-126">In hello Azure portal, open your logic app.</span></span>

2. <span data-ttu-id="59c6e-127">Ga te**overzicht**.</span><span class="sxs-lookup"><span data-stu-id="59c6e-127">Go too**Overview**.</span></span> <span data-ttu-id="59c6e-128">Kies op Hallo logic app werkbalk **Schema bijwerken**.</span><span class="sxs-lookup"><span data-stu-id="59c6e-128">On hello logic app toolbar, choose **Update Schema**.</span></span>
   
    ![Kies Schema bijwerken][1]
   
    <span data-ttu-id="59c6e-130">Hallo wordt bijgewerkte definitie geretourneerd, die u kunt kopiëren en plakken in de resourcedefinitie van een, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="59c6e-130">hello upgraded definition is returned, which you can copy and paste into a resource definition if necessary.</span></span> 
    <span data-ttu-id="59c6e-131">Echter, we **aangeraden** u **OpslaanAls** toomake ervoor dat alle verbinding verwijzingen geldig in Hallo zijn bijgewerkt logische app.</span><span class="sxs-lookup"><span data-stu-id="59c6e-131">However, we **strongly recommend** you choose **Save As** toomake sure that all connection references are valid in hello upgraded logic app.</span></span>

3. <span data-ttu-id="59c6e-132">Kies in de werkbalk van Hallo upgrade blade **OpslaanAls**.</span><span class="sxs-lookup"><span data-stu-id="59c6e-132">In hello upgrade blade toolbar, choose **Save As**.</span></span>

4. <span data-ttu-id="59c6e-133">Voer Hallo logica naam en status.</span><span class="sxs-lookup"><span data-stu-id="59c6e-133">Enter hello logic name and status.</span></span> <span data-ttu-id="59c6e-134">toodeploy uw bijgewerkte logische app, kies **maken**.</span><span class="sxs-lookup"><span data-stu-id="59c6e-134">toodeploy your upgraded logic app, choose **Create**.</span></span>

5. <span data-ttu-id="59c6e-135">Controleer of uw bijgewerkte logische app werkt zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="59c6e-135">Confirm that your upgraded logic app works as expected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="59c6e-136">Als u van een trigger handmatig of aanvraag gebruikmaakt, Hallo callback URL wordt gewijzigd in de nieuwe logische app.</span><span class="sxs-lookup"><span data-stu-id="59c6e-136">If you are using a manual or request trigger, hello callback URL changes in your new logic app.</span></span> <span data-ttu-id="59c6e-137">Test Hallo nieuwe URL toomake ervoor Hallo end-to-end ervaren werkt.</span><span class="sxs-lookup"><span data-stu-id="59c6e-137">Test hello new URL toomake sure hello end-to-end experience works.</span></span> <span data-ttu-id="59c6e-138">toopreserve vorige URL's die u via uw bestaande logische app kunt klonen.</span><span class="sxs-lookup"><span data-stu-id="59c6e-138">toopreserve previous URLs, you can clone over your existing logic app.</span></span>

6. <span data-ttu-id="59c6e-139">*Optionele* toooverwrite uw vorige logische app met Hallo nieuwe schemaversie, op de werkbalk hello, kies **kloon**, het volgende te**Schema bijwerken**.</span><span class="sxs-lookup"><span data-stu-id="59c6e-139">*Optional* toooverwrite your previous logic app with hello new schema version, on hello toolbar, choose **Clone**, next too**Update Schema**.</span></span> <span data-ttu-id="59c6e-140">Deze stap is nodig alleen als u tookeep Hallo dezelfde bron-ID of aanvraag trigger-URL van uw logische app.</span><span class="sxs-lookup"><span data-stu-id="59c6e-140">This step is necessary only if you want tookeep hello same resource ID or request trigger URL of your logic app.</span></span>

### <a name="upgrade-tool-notes"></a><span data-ttu-id="59c6e-141">Opmerkingen bij de upgrade hulpprogramma</span><span class="sxs-lookup"><span data-stu-id="59c6e-141">Upgrade tool notes</span></span>

#### <a name="mapping-conditions"></a><span data-ttu-id="59c6e-142">Toewijzing van voorwaarden</span><span class="sxs-lookup"><span data-stu-id="59c6e-142">Mapping conditions</span></span>

<span data-ttu-id="59c6e-143">In de definitie Hallo bijgewerkt kunt Hallo hulpprogramma u een zo goed mogelijke poging op true en false vertakking acties groeperen als bereik.</span><span class="sxs-lookup"><span data-stu-id="59c6e-143">In hello upgraded definition, hello tool makes a best effort at grouping true and false branch actions together as a scope.</span></span> <span data-ttu-id="59c6e-144">Designer patroon in het bijzonder Hallo van `@equals(actions('a').status, 'Skipped')` moet worden weergegeven als een `else` in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="59c6e-144">Specifically, hello designer pattern of `@equals(actions('a').status, 'Skipped')` should appear as an `else` action.</span></span> <span data-ttu-id="59c6e-145">Als Hallo hulpprogramma onherkenbare patronen detecteert, mogelijk Hallo hulpprogramma echter afzonderlijke voorwaarden voor zowel Hallo waar en ONWAAR vertakking Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="59c6e-145">However, if hello tool detects unrecognizable patterns, hello tool might create separate conditions for both hello true and hello false branch.</span></span> <span data-ttu-id="59c6e-146">U kunt acties opnieuw toewijzen na de upgrade, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="59c6e-146">You can remap actions after upgrading, if necessary.</span></span>

#### <a name="foreach-loop-with-condition"></a><span data-ttu-id="59c6e-147">'foreach' lus met voorwaarde</span><span class="sxs-lookup"><span data-stu-id="59c6e-147">'foreach' loop with condition</span></span>

<span data-ttu-id="59c6e-148">In het nieuwe schema hello, kunt u Hallo actie tooreplicate Hallo filterpatroon van een `foreach` lus met een voorwaarde per object, maar deze wijziging automatisch moet gebeuren wanneer u een upgrade uitvoert.</span><span class="sxs-lookup"><span data-stu-id="59c6e-148">In hello new schema, you can use hello filter action tooreplicate hello pattern of a `foreach` loop with a condition per item, but this change should automatically happen when you upgrade.</span></span> <span data-ttu-id="59c6e-149">Hallo voorwaarde wordt een filteractie voordat Hallo foreach-lus voor het retourneren van een reeks items die overeenkomen met de voorwaarde Hallo en deze reeks wordt doorgegeven aan Hallo foreach-actie.</span><span class="sxs-lookup"><span data-stu-id="59c6e-149">hello condition becomes a filter action before hello foreach loop for returning only an array of items that match hello condition, and that array is passed into hello foreach action.</span></span> <span data-ttu-id="59c6e-150">Zie voor een voorbeeld [lussen en -scopes](../logic-apps/logic-apps-loops-and-scopes.md).</span><span class="sxs-lookup"><span data-stu-id="59c6e-150">For an example, see [Loops and scopes](../logic-apps/logic-apps-loops-and-scopes.md).</span></span>

#### <a name="resource-tags"></a><span data-ttu-id="59c6e-151">Resourcetags</span><span class="sxs-lookup"><span data-stu-id="59c6e-151">Resource tags</span></span>

<span data-ttu-id="59c6e-152">Na de upgrade, worden resourcetags verwijderd, zodat u ze voor Hallo bijgewerkt werkstroom moet opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="59c6e-152">After you upgrade, resource tags are removed, so you must reset them for hello upgraded workflow.</span></span>

## <a name="other-changes"></a><span data-ttu-id="59c6e-153">Andere wijzigingen</span><span class="sxs-lookup"><span data-stu-id="59c6e-153">Other changes</span></span>

### <a name="renamed-manual-trigger-toorequest-trigger"></a><span data-ttu-id="59c6e-154">'Manual' trigger too'request hernoemd ' trigger</span><span class="sxs-lookup"><span data-stu-id="59c6e-154">Renamed 'manual' trigger too'request' trigger</span></span>

<span data-ttu-id="59c6e-155">Hallo `manual` triggertype is afgeschaft en hernoemd te`request` met type `http`.</span><span class="sxs-lookup"><span data-stu-id="59c6e-155">hello `manual` trigger type was deprecated and renamed too`request` with type `http`.</span></span> <span data-ttu-id="59c6e-156">Deze wijziging maakt meer consistentie voor Hallo soort patroon dat Hallo trigger gebruikte toobuild is.</span><span class="sxs-lookup"><span data-stu-id="59c6e-156">This change creates more consistency for hello kind of pattern that hello trigger is used toobuild.</span></span>

### <a name="new-filter-action"></a><span data-ttu-id="59c6e-157">Nieuwe 'filter' actie</span><span class="sxs-lookup"><span data-stu-id="59c6e-157">New 'filter' action</span></span>

<span data-ttu-id="59c6e-158">een grote matrix omlaag kleiner aantal items, nieuwe Hallo tooa toofilter `filter` type accepteert een matrix en een voorwaarde, Hallo voorwaarde voor elk item wordt geëvalueerd en resulteert in een matrix met items die voldoen aan de voorwaarde Hallo.</span><span class="sxs-lookup"><span data-stu-id="59c6e-158">toofilter a large array down tooa smaller set of items, hello new `filter` type accepts an array and a condition, evaluates hello condition for each item, and returns an array with items meeting hello condition.</span></span>

### <a name="restrictions-for-foreach-and-until-actions"></a><span data-ttu-id="59c6e-159">Beperkingen voor 'foreach' en 'tot' acties</span><span class="sxs-lookup"><span data-stu-id="59c6e-159">Restrictions for 'foreach' and 'until' actions</span></span>

<span data-ttu-id="59c6e-160">Hallo `foreach` en `until` lus beperkte tooa één actie zijn.</span><span class="sxs-lookup"><span data-stu-id="59c6e-160">hello `foreach` and `until` loop are restricted tooa single action.</span></span>

### <a name="new-trackedproperties-for-actions"></a><span data-ttu-id="59c6e-161">Nieuwe 'trackedProperties' voor acties</span><span class="sxs-lookup"><span data-stu-id="59c6e-161">New 'trackedProperties' for actions</span></span>

<span data-ttu-id="59c6e-162">Acties hebt nu een extra eigenschap met de naam `trackedProperties`, namelijk op hetzelfde niveau toohello `runAfter` en `type` eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="59c6e-162">Actions can now have an additional property called `trackedProperties`, which is sibling toohello `runAfter` and `type` properties.</span></span> <span data-ttu-id="59c6e-163">Dit object geeft bepaalde actie invoer of uitvoer die u wilt dat tooinclude in hello Azure diagnostische telemetrie, verzonden als onderdeel van een werkstroom.</span><span class="sxs-lookup"><span data-stu-id="59c6e-163">This object specifies certain action inputs or outputs that you want tooinclude in hello Azure Diagnostic telemetry, emitted as part of a workflow.</span></span> <span data-ttu-id="59c6e-164">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="59c6e-164">For example:</span></span>

```
{                
    "Http": {
        "inputs": {
            "method": "GET",
            "uri": "http://www.bing.com"
        },
        "runAfter": {},
        "type": "Http",
        "trackedProperties": {
            "responseCode": "@action().outputs.statusCode",
            "uri": "@action().inputs.uri"
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="59c6e-165">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="59c6e-165">Next Steps</span></span>
* [<span data-ttu-id="59c6e-166">Werkstroomdefinities voor logic apps maken</span><span class="sxs-lookup"><span data-stu-id="59c6e-166">Create workflow definitions for logic apps</span></span>](../logic-apps/logic-apps-author-definitions.md)
* [<span data-ttu-id="59c6e-167">Van implementatiesjablonen maken voor logische apps</span><span class="sxs-lookup"><span data-stu-id="59c6e-167">Create deployment templates for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)

<!-- Image references -->
[1]: ./media/logic-apps-schema-2016-04-01/upgradeButton.png
