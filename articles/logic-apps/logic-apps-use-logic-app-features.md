---
title: Voorwaarden toevoegen en starten van werkstromen - Azure Logic Apps | Microsoft Docs
description: Bepalen hoe werkstromen worden uitgevoerd in Azure Logic Apps door voorwaardelijke logica, triggers, acties en parameters toe te voegen.
author: stepsic-microsoft-com
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: e4e24de4-049a-4b3a-a14c-3bf3163287a8
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/28/2017
ms.author: LADocs; stepsic
ms.openlocfilehash: e632c48ed31e82536db55a9c54438bece0c38fd4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-logic-apps-features"></a><span data-ttu-id="17fd6-103">Functies van logische Apps gebruiken</span><span class="sxs-lookup"><span data-stu-id="17fd6-103">Use Logic Apps features</span></span>

<span data-ttu-id="17fd6-104">In een [vorige onderwerp](../logic-apps/logic-apps-create-a-logic-app.md), u hebt uw eerste logische app hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="17fd6-104">In a [previous topic](../logic-apps/logic-apps-create-a-logic-app.md), you created your first logic app.</span></span> <span data-ttu-id="17fd6-105">Als u uw logische app werkstroom wilt aanpassen, kunt u verschillende paden voor uw logische app om uit te voeren en het verwerken van gegevens in matrices, verzamelingen en batches.</span><span class="sxs-lookup"><span data-stu-id="17fd6-105">To control your logic app's workflow, you can specify different paths for your logic app to run and how to process data in arrays, collections, and batches.</span></span> <span data-ttu-id="17fd6-106">U kunt deze elementen opnemen in uw logische app werkstroom:</span><span class="sxs-lookup"><span data-stu-id="17fd6-106">You can include these elements in your logic app workflow:</span></span>

* <span data-ttu-id="17fd6-107">Voorwaarden en [overschakelen instructies](../logic-apps/logic-apps-switch-case.md) kunt u uw logische app uitgevoerd verschillende acties op basis van of bepaalde voorwaarden wordt voldaan.</span><span class="sxs-lookup"><span data-stu-id="17fd6-107">Conditions and [switch statements](../logic-apps/logic-apps-switch-case.md) let your logic app run different actions based on whether specific conditions are met.</span></span>

* <span data-ttu-id="17fd6-108">[Lussen](../logic-apps/logic-apps-loops-and-scopes.md) kunt u uw logische app herhaaldelijk stappen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="17fd6-108">[Loops](../logic-apps/logic-apps-loops-and-scopes.md) let your logic app run steps repeatedly.</span></span> <span data-ttu-id="17fd6-109">Bijvoorbeeld, u kunt acties herhalen via een matrix wanneer u een **For_each** lus.</span><span class="sxs-lookup"><span data-stu-id="17fd6-109">For example, you can repeat actions over an array when you use a **For_each** loop.</span></span> <span data-ttu-id="17fd6-110">Of u kunt acties herhalen totdat een voorwaarde wordt voldaan, wanneer u een **totdat** lus.</span><span class="sxs-lookup"><span data-stu-id="17fd6-110">Or you can repeat actions until a condition is met when you use an **Until** loop.</span></span>

* <span data-ttu-id="17fd6-111">[Scopes](../logic-apps/logic-apps-loops-and-scopes.md) laat u groeperen reeks acties, bijvoorbeeld voor het implementeren van afhandeling van uitzonderingen.</span><span class="sxs-lookup"><span data-stu-id="17fd6-111">[Scopes](../logic-apps/logic-apps-loops-and-scopes.md) let you group series of actions together, for example, to implement exception handling.</span></span>

* <span data-ttu-id="17fd6-112">[Debatching](../logic-apps/logic-apps-loops-and-scopes.md) kunt u uw logische app afzonderlijke werkstromen voor items in een matrix start wanneer u de **SplitOn** opdracht.</span><span class="sxs-lookup"><span data-stu-id="17fd6-112">[Debatching](../logic-apps/logic-apps-loops-and-scopes.md) lets your logic app start separate workflows for items in an array when you use the **SplitOn** command.</span></span>

<span data-ttu-id="17fd6-113">Dit onderwerp biedt informatie over andere concepten voor het bouwen van uw logische app:</span><span class="sxs-lookup"><span data-stu-id="17fd6-113">This topic introduces other concepts for building your logic app:</span></span>

* <span data-ttu-id="17fd6-114">Weergave van de code voor het bewerken van een bestaande logische app</span><span class="sxs-lookup"><span data-stu-id="17fd6-114">Code view to edit an existing logic app</span></span>
* <span data-ttu-id="17fd6-115">Opties voor het starten van een werkstroom</span><span class="sxs-lookup"><span data-stu-id="17fd6-115">Options for starting a workflow</span></span>

## <a name="conditions-run-steps-only-after-meeting-a-condition"></a><span data-ttu-id="17fd6-116">Voorwaarden: Stappen uitvoeren na het voldoen aan een voorwaarde</span><span class="sxs-lookup"><span data-stu-id="17fd6-116">Conditions: Run steps only after meeting a condition</span></span>

<span data-ttu-id="17fd6-117">Als u uw logische app stappen alleen uitgevoerd als gegevens aan bepaalde criteria voldoet, kunt u een voorwaarde waarmee wordt vergeleken gegevens in de werkstroom op basis van specifieke velden of waarden toevoegen.</span><span class="sxs-lookup"><span data-stu-id="17fd6-117">To have your logic app run steps only when data meets specific criteria, you can add a condition that compares data in the workflow against specific fields or values.</span></span>

<span data-ttu-id="17fd6-118">Stel dat u hebt een logische app die u op een website RSS-feed te veel e-mails voor berichten verzendt.</span><span class="sxs-lookup"><span data-stu-id="17fd6-118">For example, suppose you have a logic app that sends you too many emails for posts on a website's RSS feed.</span></span> <span data-ttu-id="17fd6-119">U kunt een voorwaarde toevoegen zodat uw logische app stuurt een e-mailbericht alleen als het nieuwe bericht tot een specifieke categorie behoort.</span><span class="sxs-lookup"><span data-stu-id="17fd6-119">You can add a condition so that your logic app sends email only when the new post belongs to a specific category.</span></span>

1. <span data-ttu-id="17fd6-120">In de [Azure-portal](https://portal.azure.com), zoeken en openen van uw logische app in Logic App-ontwerper.</span><span class="sxs-lookup"><span data-stu-id="17fd6-120">In the [Azure portal](https://portal.azure.com), find and open your logic app in Logic App Designer.</span></span>

2. <span data-ttu-id="17fd6-121">Een voorwaarde voor de locatie van de werkstroom die u wilt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="17fd6-121">Add a condition to the workflow location that you want.</span></span> 

   <span data-ttu-id="17fd6-122">Als u wilt de voorwaarde tussen bestaande stappen in de logic app-werkstroom toevoegen, de aanwijzer boven de pijl waar u de voorwaarde toevoegen.</span><span class="sxs-lookup"><span data-stu-id="17fd6-122">To add the condition between existing steps in the logic app workflow, move the pointer over the arrow where you want to add the condition.</span></span> 
   <span data-ttu-id="17fd6-123">Kies de **plusteken** (**+**), en kies vervolgens **een voorwaarde toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="17fd6-123">Choose the **plus sign** (**+**), then choose **Add a condition**.</span></span> <span data-ttu-id="17fd6-124">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="17fd6-124">For example:</span></span>

   ![Voorwaarde toevoegen aan logische app](./media/logic-apps-use-logic-app-features/add-condition.png)

   > [!NOTE]
   > <span data-ttu-id="17fd6-126">Als u een voorwaarde toevoegen aan het einde van uw huidige werkstroom wilt, Ga naar de onderkant van uw logische app en selecteer **+ een nieuwe stap**.</span><span class="sxs-lookup"><span data-stu-id="17fd6-126">If you want to add a condition at the end of your current workflow, go to the bottom of your logic app, and choose **+ New step**.</span></span>

3. <span data-ttu-id="17fd6-127">Nu de voorwaarde wordt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="17fd6-127">Now define the condition.</span></span> <span data-ttu-id="17fd6-128">Het veld voor de bron die u wilt evalueren, de bewerking uit te voeren en de doelwaarde of veld opgeven.</span><span class="sxs-lookup"><span data-stu-id="17fd6-128">Specify the source field that you want to evaluate, the operation to perform, and the target value or field.</span></span> <span data-ttu-id="17fd6-129">Om de bestaande velden toevoegen aan de voorwaarde, kiezen uit de **dynamische inhoud lijst toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="17fd6-129">To add existing fields to your condition, choose from the **Add dynamic content list**.</span></span>

   <span data-ttu-id="17fd6-130">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="17fd6-130">For example:</span></span>

   ![Voorwaarde in de standaardmodus bewerken](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode.png)

   <span data-ttu-id="17fd6-132">Dit is de volledige voorwaarde:</span><span class="sxs-lookup"><span data-stu-id="17fd6-132">Here's the complete condition:</span></span>

   ![Volledige voorwaarde](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode-2.png)

   > [!TIP]
   > <span data-ttu-id="17fd6-134">Als u wilt de voorwaarde wordt gedefinieerd in de code, kies **bewerken in de geavanceerde modus**.</span><span class="sxs-lookup"><span data-stu-id="17fd6-134">To define the condition in code, choose **Edit in advanced mode**.</span></span> <span data-ttu-id="17fd6-135">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="17fd6-135">For example:</span></span>
   > 
   > ![Voorwaarde in de code bewerken](./media/logic-apps-use-logic-app-features/edit-condition-advanced-mode.png)

4. <span data-ttu-id="17fd6-137">Onder **als Ja** en **als Nee**, voeg de stappen uit te voeren op basis van de vraag of de voorwaarde wordt voldaan.</span><span class="sxs-lookup"><span data-stu-id="17fd6-137">Under **IF YES** and **IF NO**, add the steps to perform based on whether the condition is met.</span></span>

   <span data-ttu-id="17fd6-138">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="17fd6-138">For example:</span></span>

   ![Voorwaarde van Ja en er worden geen paden](./media/logic-apps-use-logic-app-features/condition-yes-no-path.png)

   > [!TIP]
   > <span data-ttu-id="17fd6-140">Kunt u bestaande acties in de **als Ja** en **als Nee** paden.</span><span class="sxs-lookup"><span data-stu-id="17fd6-140">You can drag existing actions into the **IF YES** and **IF NO** paths.</span></span>

5. <span data-ttu-id="17fd6-141">Wanneer u bent klaar, slaat u uw logische app.</span><span class="sxs-lookup"><span data-stu-id="17fd6-141">When you're done, save your logic app.</span></span>

<span data-ttu-id="17fd6-142">U krijgt nu e-mailberichten alleen wanneer de berichten aan de voorwaarde voldoen.</span><span class="sxs-lookup"><span data-stu-id="17fd6-142">Now you get emails only when the posts meet your condition.</span></span>

## <a name="repeat-actions-over-a-list-with-foreach"></a><span data-ttu-id="17fd6-143">Acties over een lijst met forEach herhalen</span><span class="sxs-lookup"><span data-stu-id="17fd6-143">Repeat actions over a list with forEach</span></span>

<span data-ttu-id="17fd6-144">De lus forEach geeft een matrix als u wilt een via herhalen.</span><span class="sxs-lookup"><span data-stu-id="17fd6-144">The forEach loop specifies an array to repeat an action over.</span></span> <span data-ttu-id="17fd6-145">Als dit niet een matrix is, mislukt de stroom.</span><span class="sxs-lookup"><span data-stu-id="17fd6-145">If it is not an array, the flow fails.</span></span> <span data-ttu-id="17fd6-146">Als u action1 die een matrix van berichten hebt en u wilt dat elk bericht te verzenden, kunt u deze instructie forEach opnemen in de eigenschappen van de actie:`forEach : "@action('action1').outputs.messages"`</span><span class="sxs-lookup"><span data-stu-id="17fd6-146">For example, if you have action1 that outputs an array of messages, and you want to send each message, you can include this forEach statement in the properties of your action: `forEach : "@action('action1').outputs.messages"`</span></span>

## <a name="edit-the-code-definition-for-a-logic-app"></a><span data-ttu-id="17fd6-147">De definitie van de code voor een logische app bewerken</span><span class="sxs-lookup"><span data-stu-id="17fd6-147">Edit the code definition for a logic app</span></span>

<span data-ttu-id="17fd6-148">Hoewel u de ontwerpfunctie voor Logic App hebt, kunt u de code die een logische app bepaalt rechtstreeks bewerken.</span><span class="sxs-lookup"><span data-stu-id="17fd6-148">Although you have the Logic App Designer, you can directly edit the code that defines a logic app.</span></span>

1. <span data-ttu-id="17fd6-149">Kies op de opdrachtbalk **codeweergave**.</span><span class="sxs-lookup"><span data-stu-id="17fd6-149">On the command bar, choose **Code view**.</span></span>

    <span data-ttu-id="17fd6-150">Een volledige-editor wordt geopend en toont de definitie die u bewerkt.</span><span class="sxs-lookup"><span data-stu-id="17fd6-150">A full editor opens and shows the definition you edited.</span></span>

    ![Codeweergave](media/logic-apps-use-logic-app-features/codeview.png)

    <span data-ttu-id="17fd6-152">U kunt kopiëren en plakken van een willekeurig aantal acties binnen dezelfde logic app of tussen logische apps in de teksteditor.</span><span class="sxs-lookup"><span data-stu-id="17fd6-152">In the text editor, you can copy and paste any number of actions within the same logic app or between logic apps.</span></span> 
    <span data-ttu-id="17fd6-153">U kunt ook eenvoudig toevoegen of verwijderen van volledige secties van de definitie en u kunt ook definities met anderen delen.</span><span class="sxs-lookup"><span data-stu-id="17fd6-153">You can also easily add or remove entire sections from the definition, and you can also share definitions with others.</span></span>

2. <span data-ttu-id="17fd6-154">Om de wijzigingen opslaan, kies **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="17fd6-154">To save your edits, choose **Save**.</span></span>

## <a name="parameters"></a><span data-ttu-id="17fd6-155">Parameters</span><span class="sxs-lookup"><span data-stu-id="17fd6-155">Parameters</span></span>

<span data-ttu-id="17fd6-156">Enkele mogelijkheden van Logic Apps zijn alleen beschikbaar in de codeweergave, bijvoorbeeld parameters.</span><span class="sxs-lookup"><span data-stu-id="17fd6-156">Some Logic Apps capabilities are available only in code view, for example, parameters.</span></span> <span data-ttu-id="17fd6-157">Parameters kunnen u eenvoudig waarden in uw logische app opnieuw gebruiken.</span><span class="sxs-lookup"><span data-stu-id="17fd6-157">Parameters make it easy to reuse values throughout your logic app.</span></span> <span data-ttu-id="17fd6-158">Als u een e-mailadres die u gebruiken in verschillende acties wilt hebt, moet u dat e-mailadres definiëren als een parameter.</span><span class="sxs-lookup"><span data-stu-id="17fd6-158">For example, if you have an email address that you want use in several actions, you should define that email address as a parameter.</span></span>

<span data-ttu-id="17fd6-159">Parameters zijn goed voor het ophalen van waarden die u waarschijnlijk veel worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="17fd6-159">Parameters are good for pulling out values that you are likely to change a lot.</span></span> <span data-ttu-id="17fd6-160">Ze zijn vooral handig als u nodig hebt voor het onderdrukken van parameters in verschillende omgevingen.</span><span class="sxs-lookup"><span data-stu-id="17fd6-160">They are especially useful when you need to override parameters in different environments.</span></span> <span data-ttu-id="17fd6-161">Zie voor meer informatie over parameters die zijn gebaseerd op de omgeving overschrijven, [logic app-definities auteur](../logic-apps/logic-apps-author-definitions.md) en [REST API-documentatie](https://docs.microsoft.com/rest/api/logic).</span><span class="sxs-lookup"><span data-stu-id="17fd6-161">To learn how to override parameters based on environment, see [Author logic app definitions](../logic-apps/logic-apps-author-definitions.md) and [REST API documentation](https://docs.microsoft.com/rest/api/logic).</span></span>

<span data-ttu-id="17fd6-162">In dit voorbeeld laat zien hoe uw bestaande logische app bijwerken zodat u parameters voor de zoekterm gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="17fd6-162">This example shows how to update your existing logic app so that you can use parameters for the query term.</span></span>

1. <span data-ttu-id="17fd6-163">Zoeken in de codeweergave de `parameters : {}` object en voeg een `currentFeedUrl` object:</span><span class="sxs-lookup"><span data-stu-id="17fd6-163">In code view, find the `parameters : {}` object, and add a `currentFeedUrl` object:</span></span>

        "currentFeedUrl" : {
            "type" : "string",
            "defaultValue" : "http://rss.cnn.com/rss/cnn_topstories.rss"
        }

2. <span data-ttu-id="17fd6-164">Ga naar de `When_a_feed-item_is_published` actie, vinden de `queries` sectie en vervang de querywaarde met:`"feedUrl": "#@{parameters('currentFeedUrl')}"`</span><span class="sxs-lookup"><span data-stu-id="17fd6-164">Go to the `When_a_feed-item_is_published` action, find the `queries` section, and replace the query value with : `"feedUrl": "#@{parameters('currentFeedUrl')}"`</span></span> 

    <span data-ttu-id="17fd6-165">Als u wilt deelnemen aan twee of meer tekenreeksen, u kunt ook de `concat` functie.</span><span class="sxs-lookup"><span data-stu-id="17fd6-165">To join two or more strings, you can also use the `concat` function.</span></span> 
    <span data-ttu-id="17fd6-166">Bijvoorbeeld: `"@concat('#',parameters('currentFeedUrl'))"` werkt hetzelfde als de bovenstaande.</span><span class="sxs-lookup"><span data-stu-id="17fd6-166">For example, `"@concat('#',parameters('currentFeedUrl'))"` works the same as the above.</span></span>

3.  <span data-ttu-id="17fd6-167">Als u bent klaar, kiest u **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="17fd6-167">When you're done, choose **Save**.</span></span> 

    <span data-ttu-id="17fd6-168">Nu kunt u de website RSS-feed door een andere URL via de `currentFeedURL` object.</span><span class="sxs-lookup"><span data-stu-id="17fd6-168">Now you can change the website's RSS feed by passing a different URL through the `currentFeedURL` object.</span></span>

<span data-ttu-id="17fd6-169">Meer informatie over [hoe auteur logic app-definities](../logic-apps/logic-apps-author-definitions.md).</span><span class="sxs-lookup"><span data-stu-id="17fd6-169">Learn more about [how to author logic app definitions](../logic-apps/logic-apps-author-definitions.md).</span></span>

## <a name="start-logic-app-workflows"></a><span data-ttu-id="17fd6-170">Logic app-werkstromen starten</span><span class="sxs-lookup"><span data-stu-id="17fd6-170">Start logic app workflows</span></span>

<span data-ttu-id="17fd6-171">U hebt verschillende opties voor het starten van de werkstroom die is gedefinieerd in uw logische app.</span><span class="sxs-lookup"><span data-stu-id="17fd6-171">You have different options for starting the workflow defined in your logic app.</span></span> <span data-ttu-id="17fd6-172">U kunt altijd een werkstroom op verzoek starten in de [Azure-portal].</span><span class="sxs-lookup"><span data-stu-id="17fd6-172">You can always start a workflow on-demand in the [Azure portal].</span></span>

### <a name="recurrence-triggers"></a><span data-ttu-id="17fd6-173">Terugkeerpatroon triggers</span><span class="sxs-lookup"><span data-stu-id="17fd6-173">Recurrence triggers</span></span>

<span data-ttu-id="17fd6-174">Een terugkeerpatroon trigger wordt uitgevoerd met een interval dat u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="17fd6-174">A recurrence trigger runs at an interval that you specify.</span></span> <span data-ttu-id="17fd6-175">Wanneer de trigger voorwaardelijke logica heeft, bepaalt de trigger of de werkstroom moet worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="17fd6-175">When the trigger has conditional logic, the trigger determines whether the workflow needs to run.</span></span> <span data-ttu-id="17fd6-176">Een trigger geeft aan de werkstroom moet worden uitgevoerd door te retourneren een `200` statuscode.</span><span class="sxs-lookup"><span data-stu-id="17fd6-176">A trigger indicates the workflow should run by returning a `200` status code.</span></span> <span data-ttu-id="17fd6-177">Wanneer de werkstroom niet hoeft te worden uitgevoerd, de trigger retourneert een `202` statuscode.</span><span class="sxs-lookup"><span data-stu-id="17fd6-177">When the workflow doesn't need to run, the trigger returns a `202` status code.</span></span>

### <a name="callback-using-rest-apis"></a><span data-ttu-id="17fd6-178">Callback met REST API 's</span><span class="sxs-lookup"><span data-stu-id="17fd6-178">Callback using REST APIs</span></span>

<span data-ttu-id="17fd6-179">Voor het starten van een werkstroom kunnen services bellen en een logische app-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="17fd6-179">To start a workflow, services can call a logic app endpoint.</span></span> <span data-ttu-id="17fd6-180">Als u wilt dit soort logic app op de aanvraag, kies **nu uitvoeren** op de opdrachtbalk.</span><span class="sxs-lookup"><span data-stu-id="17fd6-180">To start this kind of logic app on-demand, choose **Run now** on the command bar.</span></span> <span data-ttu-id="17fd6-181">Zie [werkstromen starten door het aanroepen van logic app eindpunten als triggers](../logic-apps/logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="17fd6-181">See [Start workflows by calling logic app endpoints as triggers](../logic-apps/logic-apps-http-endpoint.md).</span></span> 

<!-- Shared links -->
<span data-ttu-id="17fd6-182">[Azure-portal]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="17fd6-182">[Azure portal]: https://portal.azure.com</span></span>

## <a name="next-steps"></a><span data-ttu-id="17fd6-183">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="17fd6-183">Next steps</span></span>

* [<span data-ttu-id="17fd6-184">Switch-instructies</span><span class="sxs-lookup"><span data-stu-id="17fd6-184">Switch statements</span></span>](../logic-apps/logic-apps-switch-case.md) 
* [<span data-ttu-id="17fd6-185">Lussen, bereiken en debatching</span><span class="sxs-lookup"><span data-stu-id="17fd6-185">Loops, scopes, and debatching</span></span>](../logic-apps/logic-apps-loops-and-scopes.md)
* [<span data-ttu-id="17fd6-186">Definities voor logische apps maken</span><span class="sxs-lookup"><span data-stu-id="17fd6-186">Author logic app definitions</span></span>](../logic-apps/logic-apps-author-definitions.md)