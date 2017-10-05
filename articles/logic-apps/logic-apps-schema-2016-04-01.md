---
title: Schema-updates 1 juni 2016 - Azure Logic Apps | Microsoft Docs
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
ms.openlocfilehash: 43df04d6478e44c82c88b17d916cfc9fe4afc03e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="schema-updates-for-azure-logic-apps---june-1-2016"></a><span data-ttu-id="16659-103">Schema-updates voor Azure Logic Apps - 1 juni 2016</span><span class="sxs-lookup"><span data-stu-id="16659-103">Schema updates for Azure Logic Apps - June 1, 2016</span></span>

<span data-ttu-id="16659-104">Deze nieuwe schema en de API-versie voor Azure Logic Apps bevat belangrijke verbeteringen die logische apps betrouwbaarder en eenvoudiger te gebruiken:</span><span class="sxs-lookup"><span data-stu-id="16659-104">This new schema and API version for Azure Logic Apps includes key improvements that make logic apps more reliable and easier to use:</span></span>

* <span data-ttu-id="16659-105">[Scopes](#scopes) kunt u een groep of acties nesten als een verzameling van acties.</span><span class="sxs-lookup"><span data-stu-id="16659-105">[Scopes](#scopes) let you group or nest actions as a collection of actions.</span></span>
* <span data-ttu-id="16659-106">[Voorwaarden en lussen](#conditions-loops) zijn nu klas acties.</span><span class="sxs-lookup"><span data-stu-id="16659-106">[Conditions and loops](#conditions-loops) are now first-class actions.</span></span>
* <span data-ttu-id="16659-107">Nauwkeurigere ordening voor het uitvoeren van acties met de `runAfter` eigenschap vervangen`dependsOn`</span><span class="sxs-lookup"><span data-stu-id="16659-107">More precise ordering for running actions with the `runAfter` property, replacing `dependsOn`</span></span>

<span data-ttu-id="16659-108">Upgrade van uw logische apps van het schema van de preview 1 augustus 2015 aan het schema 1 juni 2016 [Raadpleeg de sectie upgrade](##upgrade-your-schema).</span><span class="sxs-lookup"><span data-stu-id="16659-108">To upgrade your logic apps from the August 1, 2015 preview schema to the June 1, 2016 schema, [check out the upgrade section](##upgrade-your-schema).</span></span>

<a name="scopes"></a>
## <a name="scopes"></a><span data-ttu-id="16659-109">Scopes</span><span class="sxs-lookup"><span data-stu-id="16659-109">Scopes</span></span>

<span data-ttu-id="16659-110">Dit schema bevat bereiken, waarmee u groep samen of nest acties in de andere.</span><span class="sxs-lookup"><span data-stu-id="16659-110">This schema includes scopes, which let you group actions together, or nest actions inside each other.</span></span> <span data-ttu-id="16659-111">Een voorwaarde kan bijvoorbeeld een voorwaarde bevatten.</span><span class="sxs-lookup"><span data-stu-id="16659-111">For example, a condition can contain another condition.</span></span> <span data-ttu-id="16659-112">Meer informatie over [bereik syntaxis](../logic-apps/logic-apps-loops-and-scopes.md), of in dit voorbeeld basic bereik bekijken:</span><span class="sxs-lookup"><span data-stu-id="16659-112">Learn more about [scope syntax](../logic-apps/logic-apps-loops-and-scopes.md), or review this basic scope example:</span></span>

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
## <a name="conditions-and-loops-changes"></a><span data-ttu-id="16659-113">Voorwaarden en lussen wijzigingen</span><span class="sxs-lookup"><span data-stu-id="16659-113">Conditions and loops changes</span></span>

<span data-ttu-id="16659-114">Zijn parameters die zijn gekoppeld aan één actie in het schema van vorige versies, de voorwaarden en lussen.</span><span class="sxs-lookup"><span data-stu-id="16659-114">In previous schema versions, conditions and loops were parameters associated with a single action.</span></span> <span data-ttu-id="16659-115">Dit schema liftonderhoud deze beperking, zodat de voorwaarden en lussen nu worden weergegeven als actietypen.</span><span class="sxs-lookup"><span data-stu-id="16659-115">This schema lifts this limitation, so conditions and loops now appear as action types.</span></span> <span data-ttu-id="16659-116">Meer informatie over [lussen en -scopes](../logic-apps/logic-apps-loops-and-scopes.md), of dit eenvoudige voorbeeld voor een actie voorwaarde bekijken:</span><span class="sxs-lookup"><span data-stu-id="16659-116">Learn more about [loops and scopes](../logic-apps/logic-apps-loops-and-scopes.md), or review this basic example for a condition action:</span></span>

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
## <a name="runafter-property"></a><span data-ttu-id="16659-117">de eigenschap 'runAfter'</span><span class="sxs-lookup"><span data-stu-id="16659-117">'runAfter' property</span></span>

<span data-ttu-id="16659-118">De `runAfter` eigenschap vervangt `dependsOn`, mits nauwkeuriger wanneer u de volgorde voor acties opgeven op basis van de status van de vorige acties.</span><span class="sxs-lookup"><span data-stu-id="16659-118">The `runAfter` property replaces `dependsOn`, providing more precision when you specify the run order for actions based on the status of previous actions.</span></span>

<span data-ttu-id="16659-119">De `dependsOn` eigenschap is gelijk aan 'de actie is uitgevoerd en is geslaagd', niet van belang hoe vaak u wilt uitvoeren van een actie, op basis van of de vorige bewerking geslaagd is, mislukt of overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="16659-119">The `dependsOn` property was synonymous with "the action ran and was successful", no matter how many times you wanted to execute an action, based on whether the previous action was successful, failed, or skipped.</span></span> <span data-ttu-id="16659-120">De `runAfter` eigenschap die flexibel als een object dat Hiermee geeft u alle actienamen waarna het object wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="16659-120">The `runAfter` property provides that flexibility as an object that specifies all the action names after which the object runs.</span></span> <span data-ttu-id="16659-121">Deze eigenschap bepaalt ook een matrix van statussen die geaccepteerd als triggers worden.</span><span class="sxs-lookup"><span data-stu-id="16659-121">This property also defines an array of statuses that are acceptable as triggers.</span></span> <span data-ttu-id="16659-122">Bijvoorbeeld, als u uitvoeren wilt nadat de stap voor stap een kan worden uitgevoerd en ook na stap B is gelukt of mislukt, u samenstellen dit `runAfter` eigenschap:</span><span class="sxs-lookup"><span data-stu-id="16659-122">For example, if you wanted to run after step A succeeds and also after step B succeeds or fails, you construct this `runAfter` property:</span></span>

```
{
    "...",
    "runAfter": {
        "A": ["Succeeded"],
        "B": ["Succeeded", "Failed"]
    }
}
```

## <a name="upgrade-your-schema"></a><span data-ttu-id="16659-123">Uw schema bijwerken</span><span class="sxs-lookup"><span data-stu-id="16659-123">Upgrade your schema</span></span>

<span data-ttu-id="16659-124">Een upgrade naar het nieuwe schema duurt slechts een paar stappen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="16659-124">Upgrading to the new schema only takes a few steps.</span></span> <span data-ttu-id="16659-125">Het upgradeproces bevat het upgrade-script uitgevoerd op te slaan als een nieuwe logische app, en als u wilt, mogelijk wordt de vorige logische app overschreven.</span><span class="sxs-lookup"><span data-stu-id="16659-125">The upgrade process includes running the upgrade script, saving as a new logic app, and if you want, possibly overwriting the previous logic app.</span></span>

1. <span data-ttu-id="16659-126">Open uw logische app in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="16659-126">In the Azure portal, open your logic app.</span></span>

2. <span data-ttu-id="16659-127">Ga naar **overzicht**.</span><span class="sxs-lookup"><span data-stu-id="16659-127">Go to **Overview**.</span></span> <span data-ttu-id="16659-128">Kies op de werkbalk van de app logica **Schema bijwerken**.</span><span class="sxs-lookup"><span data-stu-id="16659-128">On the logic app toolbar, choose **Update Schema**.</span></span>
   
    ![Kies Schema bijwerken][1]
   
    <span data-ttu-id="16659-130">De bijgewerkte definitie wordt geretourneerd, die u kunt kopiëren en plakken in de resourcedefinitie van een, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="16659-130">The upgraded definition is returned, which you can copy and paste into a resource definition if necessary.</span></span> 
    <span data-ttu-id="16659-131">Maar we **aangeraden** u **OpslaanAls** om ervoor te zorgen dat alle verbinding verwijzingen geldig in de bijgewerkte logische app zijn.</span><span class="sxs-lookup"><span data-stu-id="16659-131">However, we **strongly recommend** you choose **Save As** to make sure that all connection references are valid in the upgraded logic app.</span></span>

3. <span data-ttu-id="16659-132">Kies in de werkbalk upgrade blade **OpslaanAls**.</span><span class="sxs-lookup"><span data-stu-id="16659-132">In the upgrade blade toolbar, choose **Save As**.</span></span>

4. <span data-ttu-id="16659-133">Voer de naam van de logica en status.</span><span class="sxs-lookup"><span data-stu-id="16659-133">Enter the logic name and status.</span></span> <span data-ttu-id="16659-134">Als u wilt uw bijgewerkte logische app implementeren, kies **maken**.</span><span class="sxs-lookup"><span data-stu-id="16659-134">To deploy your upgraded logic app, choose **Create**.</span></span>

5. <span data-ttu-id="16659-135">Controleer of uw bijgewerkte logische app werkt zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="16659-135">Confirm that your upgraded logic app works as expected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="16659-136">Als u van een trigger handmatig of aanvraag gebruikmaakt, wordt de callback-URL gewijzigd in de nieuwe logische app.</span><span class="sxs-lookup"><span data-stu-id="16659-136">If you are using a manual or request trigger, the callback URL changes in your new logic app.</span></span> <span data-ttu-id="16659-137">Test de nieuwe URL om te controleren of de end-to-end-ervaring werkt.</span><span class="sxs-lookup"><span data-stu-id="16659-137">Test the new URL to make sure the end-to-end experience works.</span></span> <span data-ttu-id="16659-138">Als u wilt behouden vorige URL's, kunt u via uw bestaande logische app klonen.</span><span class="sxs-lookup"><span data-stu-id="16659-138">To preserve previous URLs, you can clone over your existing logic app.</span></span>

6. <span data-ttu-id="16659-139">*Optionele* kiezen als u wilt uw vorige logische app overschrijven met de nieuwe schemaversie op de werkbalk **kloon**naast **Schema bijwerken**.</span><span class="sxs-lookup"><span data-stu-id="16659-139">*Optional* To overwrite your previous logic app with the new schema version, on the toolbar, choose **Clone**, next to **Update Schema**.</span></span> <span data-ttu-id="16659-140">Deze stap is alleen nodig als u wilt behouden dezelfde resource-ID of de aanvraag-URL van uw logische app trigger.</span><span class="sxs-lookup"><span data-stu-id="16659-140">This step is necessary only if you want to keep the same resource ID or request trigger URL of your logic app.</span></span>

### <a name="upgrade-tool-notes"></a><span data-ttu-id="16659-141">Opmerkingen bij de upgrade hulpprogramma</span><span class="sxs-lookup"><span data-stu-id="16659-141">Upgrade tool notes</span></span>

#### <a name="mapping-conditions"></a><span data-ttu-id="16659-142">Toewijzing van voorwaarden</span><span class="sxs-lookup"><span data-stu-id="16659-142">Mapping conditions</span></span>

<span data-ttu-id="16659-143">In de bijgewerkte definitie maakt het hulpprogramma een zo goed mogelijke poging op true en false vertakking acties groeperen als bereik.</span><span class="sxs-lookup"><span data-stu-id="16659-143">In the upgraded definition, the tool makes a best effort at grouping true and false branch actions together as a scope.</span></span> <span data-ttu-id="16659-144">In het bijzonder de ontwerpfunctie patroon van `@equals(actions('a').status, 'Skipped')` moet worden weergegeven als een `else` in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="16659-144">Specifically, the designer pattern of `@equals(actions('a').status, 'Skipped')` should appear as an `else` action.</span></span> <span data-ttu-id="16659-145">Als het hulpprogramma onherkenbare patronen detecteert, kan het hulpprogramma echter afzonderlijke voorwaarden voor zowel de true als de vertakking ONWAAR maken.</span><span class="sxs-lookup"><span data-stu-id="16659-145">However, if the tool detects unrecognizable patterns, the tool might create separate conditions for both the true and the false branch.</span></span> <span data-ttu-id="16659-146">U kunt acties opnieuw toewijzen na de upgrade, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="16659-146">You can remap actions after upgrading, if necessary.</span></span>

#### <a name="foreach-loop-with-condition"></a><span data-ttu-id="16659-147">'foreach' lus met voorwaarde</span><span class="sxs-lookup"><span data-stu-id="16659-147">'foreach' loop with condition</span></span>

<span data-ttu-id="16659-148">In het nieuwe schema, kunt u de filteractie voor replicatie van het patroon van een `foreach` lus met een voorwaarde per object, maar deze wijziging automatisch moet gebeuren wanneer u een upgrade uitvoert.</span><span class="sxs-lookup"><span data-stu-id="16659-148">In the new schema, you can use the filter action to replicate the pattern of a `foreach` loop with a condition per item, but this change should automatically happen when you upgrade.</span></span> <span data-ttu-id="16659-149">De voorwaarde wordt een filteractie voordat de foreach-lus voor het retourneren van een reeks items die overeenkomen met de voorwaarde en deze reeks wordt doorgegeven in de foreach-actie.</span><span class="sxs-lookup"><span data-stu-id="16659-149">The condition becomes a filter action before the foreach loop for returning only an array of items that match the condition, and that array is passed into the foreach action.</span></span> <span data-ttu-id="16659-150">Zie voor een voorbeeld [lussen en -scopes](../logic-apps/logic-apps-loops-and-scopes.md).</span><span class="sxs-lookup"><span data-stu-id="16659-150">For an example, see [Loops and scopes](../logic-apps/logic-apps-loops-and-scopes.md).</span></span>

#### <a name="resource-tags"></a><span data-ttu-id="16659-151">Resourcetags</span><span class="sxs-lookup"><span data-stu-id="16659-151">Resource tags</span></span>

<span data-ttu-id="16659-152">Na de upgrade, worden resourcetags verwijderd, zodat u ze voor de bijgewerkte workflow moet opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="16659-152">After you upgrade, resource tags are removed, so you must reset them for the upgraded workflow.</span></span>

## <a name="other-changes"></a><span data-ttu-id="16659-153">Andere wijzigingen</span><span class="sxs-lookup"><span data-stu-id="16659-153">Other changes</span></span>

### <a name="renamed-manual-trigger-to-request-trigger"></a><span data-ttu-id="16659-154">Nieuwe naam 'manual' trigger 'aanvraag' activeren</span><span class="sxs-lookup"><span data-stu-id="16659-154">Renamed 'manual' trigger to 'request' trigger</span></span>

<span data-ttu-id="16659-155">De `manual` triggertype is afgeschaft en gewijzigd in `request` met type `http`.</span><span class="sxs-lookup"><span data-stu-id="16659-155">The `manual` trigger type was deprecated and renamed to `request` with type `http`.</span></span> <span data-ttu-id="16659-156">Deze wijziging meer van de consistentie van het soort patroon maakt die de trigger wordt gebruikt om samen te stellen.</span><span class="sxs-lookup"><span data-stu-id="16659-156">This change creates more consistency for the kind of pattern that the trigger is used to build.</span></span>

### <a name="new-filter-action"></a><span data-ttu-id="16659-157">Nieuwe 'filter' actie</span><span class="sxs-lookup"><span data-stu-id="16659-157">New 'filter' action</span></span>

<span data-ttu-id="16659-158">Voor het filteren van een grote matrix naar beneden op een kleiner aantal items, de nieuwe `filter` type accepteert een matrix en een voorwaarde, de voorwaarde voor elk item wordt geëvalueerd en resulteert in een matrix met items die voldoen aan de voorwaarde.</span><span class="sxs-lookup"><span data-stu-id="16659-158">To filter a large array down to a smaller set of items, the new `filter` type accepts an array and a condition, evaluates the condition for each item, and returns an array with items meeting the condition.</span></span>

### <a name="restrictions-for-foreach-and-until-actions"></a><span data-ttu-id="16659-159">Beperkingen voor 'foreach' en 'tot' acties</span><span class="sxs-lookup"><span data-stu-id="16659-159">Restrictions for 'foreach' and 'until' actions</span></span>

<span data-ttu-id="16659-160">De `foreach` en `until` lus zijn beperkt tot één actie.</span><span class="sxs-lookup"><span data-stu-id="16659-160">The `foreach` and `until` loop are restricted to a single action.</span></span>

### <a name="new-trackedproperties-for-actions"></a><span data-ttu-id="16659-161">Nieuwe 'trackedProperties' voor acties</span><span class="sxs-lookup"><span data-stu-id="16659-161">New 'trackedProperties' for actions</span></span>

<span data-ttu-id="16659-162">Acties hebt nu een extra eigenschap met de naam `trackedProperties`, namelijk op hetzelfde niveau naar de `runAfter` en `type` eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="16659-162">Actions can now have an additional property called `trackedProperties`, which is sibling to the `runAfter` and `type` properties.</span></span> <span data-ttu-id="16659-163">Dit object geeft een bepaalde actie in- of uitgangen die u opnemen in de Azure diagnostische telemetrie wilt, verzonden als onderdeel van een werkstroom.</span><span class="sxs-lookup"><span data-stu-id="16659-163">This object specifies certain action inputs or outputs that you want to include in the Azure Diagnostic telemetry, emitted as part of a workflow.</span></span> <span data-ttu-id="16659-164">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="16659-164">For example:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="16659-165">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="16659-165">Next Steps</span></span>
* [<span data-ttu-id="16659-166">Werkstroomdefinities voor logic apps maken</span><span class="sxs-lookup"><span data-stu-id="16659-166">Create workflow definitions for logic apps</span></span>](../logic-apps/logic-apps-author-definitions.md)
* [<span data-ttu-id="16659-167">Van implementatiesjablonen maken voor logische apps</span><span class="sxs-lookup"><span data-stu-id="16659-167">Create deployment templates for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)

<!-- Image references -->
[1]: ./media/logic-apps-schema-2016-04-01/upgradeButton.png
