---
title: aaaAdd voorwaarden en werkstromen - Azure Logic Apps starten | Microsoft Docs
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
ms.openlocfilehash: 76d5e44590ffa14cf70d7a93b99a241d286d555b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-logic-apps-features"></a><span data-ttu-id="84480-103">Functies van logische Apps gebruiken</span><span class="sxs-lookup"><span data-stu-id="84480-103">Use Logic Apps features</span></span>

<span data-ttu-id="84480-104">In een [vorige onderwerp](../logic-apps/logic-apps-create-a-logic-app.md), u hebt uw eerste logische app hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="84480-104">In a [previous topic](../logic-apps/logic-apps-create-a-logic-app.md), you created your first logic app.</span></span> <span data-ttu-id="84480-105">toocontrol uw logische app werkstroom, kunt u verschillende paden voor uw logische app toorun opgeven en hoe te verwerken gegevens in matrices, verzamelingen en batches.</span><span class="sxs-lookup"><span data-stu-id="84480-105">toocontrol your logic app's workflow, you can specify different paths for your logic app toorun and how too process data in arrays, collections, and batches.</span></span> <span data-ttu-id="84480-106">U kunt deze elementen opnemen in uw logische app werkstroom:</span><span class="sxs-lookup"><span data-stu-id="84480-106">You can include these elements in your logic app workflow:</span></span>

* <span data-ttu-id="84480-107">Voorwaarden en [overschakelen instructies](../logic-apps/logic-apps-switch-case.md) kunt u uw logische app uitgevoerd verschillende acties op basis van of bepaalde voorwaarden wordt voldaan.</span><span class="sxs-lookup"><span data-stu-id="84480-107">Conditions and [switch statements](../logic-apps/logic-apps-switch-case.md) let your logic app run different actions based on whether specific conditions are met.</span></span>

* <span data-ttu-id="84480-108">[Lussen](../logic-apps/logic-apps-loops-and-scopes.md) kunt u uw logische app herhaaldelijk stappen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="84480-108">[Loops](../logic-apps/logic-apps-loops-and-scopes.md) let your logic app run steps repeatedly.</span></span> <span data-ttu-id="84480-109">Bijvoorbeeld, u kunt acties herhalen via een matrix wanneer u een **For_each** lus.</span><span class="sxs-lookup"><span data-stu-id="84480-109">For example, you can repeat actions over an array when you use a **For_each** loop.</span></span> <span data-ttu-id="84480-110">Of u kunt acties herhalen totdat een voorwaarde wordt voldaan, wanneer u een **totdat** lus.</span><span class="sxs-lookup"><span data-stu-id="84480-110">Or you can repeat actions until a condition is met when you use an **Until** loop.</span></span>

* <span data-ttu-id="84480-111">[Scopes](../logic-apps/logic-apps-loops-and-scopes.md) laat u groeperen reeks acties, bijvoorbeeld tooimplement uitzonderingsverwerking.</span><span class="sxs-lookup"><span data-stu-id="84480-111">[Scopes](../logic-apps/logic-apps-loops-and-scopes.md) let you group series of actions together, for example, tooimplement exception handling.</span></span>

* <span data-ttu-id="84480-112">[Debatching](../logic-apps/logic-apps-loops-and-scopes.md) kunt u uw logische app afzonderlijke werkstromen voor items in een matrix met gestart Hallo **SplitOn** opdracht.</span><span class="sxs-lookup"><span data-stu-id="84480-112">[Debatching](../logic-apps/logic-apps-loops-and-scopes.md) lets your logic app start separate workflows for items in an array when you use hello **SplitOn** command.</span></span>

<span data-ttu-id="84480-113">Dit onderwerp biedt informatie over andere concepten voor het bouwen van uw logische app:</span><span class="sxs-lookup"><span data-stu-id="84480-113">This topic introduces other concepts for building your logic app:</span></span>

* <span data-ttu-id="84480-114">Weergave tooedit een bestaande logische app-code</span><span class="sxs-lookup"><span data-stu-id="84480-114">Code view tooedit an existing logic app</span></span>
* <span data-ttu-id="84480-115">Opties voor het starten van een werkstroom</span><span class="sxs-lookup"><span data-stu-id="84480-115">Options for starting a workflow</span></span>

## <a name="conditions-run-steps-only-after-meeting-a-condition"></a><span data-ttu-id="84480-116">Voorwaarden: Stappen uitvoeren na het voldoen aan een voorwaarde</span><span class="sxs-lookup"><span data-stu-id="84480-116">Conditions: Run steps only after meeting a condition</span></span>

<span data-ttu-id="84480-117">toohave uw logische app stappen alleen uitgevoerd als gegevens aan bepaalde criteria voldoet, kunt u een voorwaarde waarmee gegevens in de werkstroom op basis van specifieke velden of waarden Hallo vergeleken toevoegen.</span><span class="sxs-lookup"><span data-stu-id="84480-117">toohave your logic app run steps only when data meets specific criteria, you can add a condition that compares data in hello workflow against specific fields or values.</span></span>

<span data-ttu-id="84480-118">Stel dat u hebt een logische app die u op een website RSS-feed te veel e-mails voor berichten verzendt.</span><span class="sxs-lookup"><span data-stu-id="84480-118">For example, suppose you have a logic app that sends you too many emails for posts on a website's RSS feed.</span></span> <span data-ttu-id="84480-119">U kunt toevoegen om dat een voorwaarde zodat uw logische app stuurt een e-mailbericht alleen wanneer nieuwe Hallo boekt behoort tooa specifieke categorie.</span><span class="sxs-lookup"><span data-stu-id="84480-119">You can add a condition so that your logic app sends email only when hello new post belongs tooa specific category.</span></span>

1. <span data-ttu-id="84480-120">In Hallo [Azure-portal](https://portal.azure.com), zoeken en openen van uw logische app in Logic App-ontwerper.</span><span class="sxs-lookup"><span data-stu-id="84480-120">In hello [Azure portal](https://portal.azure.com), find and open your logic app in Logic App Designer.</span></span>

2. <span data-ttu-id="84480-121">Een voorwaarde toohello werkstroom locatie die u wilt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="84480-121">Add a condition toohello workflow location that you want.</span></span> 

   <span data-ttu-id="84480-122">tooadd hello voorwaarde tussen bestaande stappen in Hallo logic app werkstroom aanwijzer Hallo boven Hallo pijl waar u tooadd Hallo voorwaarde.</span><span class="sxs-lookup"><span data-stu-id="84480-122">tooadd hello condition between existing steps in hello logic app workflow, move hello pointer over hello arrow where you want tooadd hello condition.</span></span> 
   <span data-ttu-id="84480-123">Kies Hallo **plusteken** (**+**), en kies vervolgens **een voorwaarde toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="84480-123">Choose hello **plus sign** (**+**), then choose **Add a condition**.</span></span> <span data-ttu-id="84480-124">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="84480-124">For example:</span></span>

   ![Voorwaarde toologic app toevoegen](./media/logic-apps-use-logic-app-features/add-condition.png)

   > [!NOTE]
   > <span data-ttu-id="84480-126">Als u een voorwaarde tooadd aan Hallo einde van uw huidige werkstroom wilt, gaat u toohello onder aan uw logische app en kies **+ een nieuwe stap**.</span><span class="sxs-lookup"><span data-stu-id="84480-126">If you want tooadd a condition at hello end of your current workflow, go toohello bottom of your logic app, and choose **+ New step**.</span></span>

3. <span data-ttu-id="84480-127">Nu Hallo voorwaarde definiëren.</span><span class="sxs-lookup"><span data-stu-id="84480-127">Now define hello condition.</span></span> <span data-ttu-id="84480-128">Hallo bronveld dat u tooevaluate, Hallo bewerking tooperform, en de doelwaarde Hallo of veld wilt opgeven.</span><span class="sxs-lookup"><span data-stu-id="84480-128">Specify hello source field that you want tooevaluate, hello operation tooperform, and hello target value or field.</span></span> <span data-ttu-id="84480-129">tooyour voorwaarde tooadd bestaande velden kiezen uit Hallo **dynamische inhoud lijst toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="84480-129">tooadd existing fields tooyour condition, choose from hello **Add dynamic content list**.</span></span>

   <span data-ttu-id="84480-130">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="84480-130">For example:</span></span>

   ![Voorwaarde in de standaardmodus bewerken](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode.png)

   <span data-ttu-id="84480-132">Dit is de volledige voorwaarde Hallo:</span><span class="sxs-lookup"><span data-stu-id="84480-132">Here's hello complete condition:</span></span>

   ![Volledige voorwaarde](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode-2.png)

   > [!TIP]
   > <span data-ttu-id="84480-134">Kies toodefine Hallo voorwaarde in code **bewerken in de geavanceerde modus**.</span><span class="sxs-lookup"><span data-stu-id="84480-134">toodefine hello condition in code, choose **Edit in advanced mode**.</span></span> <span data-ttu-id="84480-135">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="84480-135">For example:</span></span>
   > 
   > ![Voorwaarde in de code bewerken](./media/logic-apps-use-logic-app-features/edit-condition-advanced-mode.png)

4. <span data-ttu-id="84480-137">Onder **als Ja** en **als Nee**, voeg Hallo stappen tooperform op basis van of Hallo voorwaarde wordt voldaan.</span><span class="sxs-lookup"><span data-stu-id="84480-137">Under **IF YES** and **IF NO**, add hello steps tooperform based on whether hello condition is met.</span></span>

   <span data-ttu-id="84480-138">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="84480-138">For example:</span></span>

   ![Voorwaarde van Ja en er worden geen paden](./media/logic-apps-use-logic-app-features/condition-yes-no-path.png)

   > [!TIP]
   > <span data-ttu-id="84480-140">U kunt bestaande acties naar Hallo slepen **als Ja** en **als Nee** paden.</span><span class="sxs-lookup"><span data-stu-id="84480-140">You can drag existing actions into hello **IF YES** and **IF NO** paths.</span></span>

5. <span data-ttu-id="84480-141">Wanneer u bent klaar, slaat u uw logische app.</span><span class="sxs-lookup"><span data-stu-id="84480-141">When you're done, save your logic app.</span></span>

<span data-ttu-id="84480-142">U krijgt nu e-mailberichten alleen wanneer het Hallo-berichten aan de voorwaarde voldoen.</span><span class="sxs-lookup"><span data-stu-id="84480-142">Now you get emails only when hello posts meet your condition.</span></span>

## <a name="repeat-actions-over-a-list-with-foreach"></a><span data-ttu-id="84480-143">Acties over een lijst met forEach herhalen</span><span class="sxs-lookup"><span data-stu-id="84480-143">Repeat actions over a list with forEach</span></span>

<span data-ttu-id="84480-144">Hallo forEach lus bevat een matrix toorepeat een actie via.</span><span class="sxs-lookup"><span data-stu-id="84480-144">hello forEach loop specifies an array toorepeat an action over.</span></span> <span data-ttu-id="84480-145">Als het is niet een matrix, mislukt de Hallo-stroom.</span><span class="sxs-lookup"><span data-stu-id="84480-145">If it is not an array, hello flow fails.</span></span> <span data-ttu-id="84480-146">Als er action1 die een matrix van berichten en toosend elk bericht gewenste, kunt u deze instructie forEach opnemen in de eigenschappen van uw actie Hallo:`forEach : "@action('action1').outputs.messages"`</span><span class="sxs-lookup"><span data-stu-id="84480-146">For example, if you have action1 that outputs an array of messages, and you want toosend each message, you can include this forEach statement in hello properties of your action: `forEach : "@action('action1').outputs.messages"`</span></span>

## <a name="edit-hello-code-definition-for-a-logic-app"></a><span data-ttu-id="84480-147">Hallo codedefinitie voor een logische app bewerken</span><span class="sxs-lookup"><span data-stu-id="84480-147">Edit hello code definition for a logic app</span></span>

<span data-ttu-id="84480-148">Hoewel u Hallo Logic App-ontwerper hebt, kunt u direct Hallo-code die een logische app definieert bewerken.</span><span class="sxs-lookup"><span data-stu-id="84480-148">Although you have hello Logic App Designer, you can directly edit hello code that defines a logic app.</span></span>

1. <span data-ttu-id="84480-149">Kies op de opdrachtbalk Hallo **codeweergave**.</span><span class="sxs-lookup"><span data-stu-id="84480-149">On hello command bar, choose **Code view**.</span></span>

    <span data-ttu-id="84480-150">Een volledige-editor wordt geopend en toont Hallo-definitie die u bewerkt.</span><span class="sxs-lookup"><span data-stu-id="84480-150">A full editor opens and shows hello definition you edited.</span></span>

    ![Codeweergave](media/logic-apps-use-logic-app-features/codeview.png)

    <span data-ttu-id="84480-152">In de teksteditor hello, kunt u kopiëren en plakken van een willekeurig aantal acties in Hallo dezelfde logische app of tussen logische apps.</span><span class="sxs-lookup"><span data-stu-id="84480-152">In hello text editor, you can copy and paste any number of actions within hello same logic app or between logic apps.</span></span> 
    <span data-ttu-id="84480-153">U kunt ook eenvoudig toevoegen of verwijderen van volledige secties van Hallo definitie en u kunt ook definities met anderen delen.</span><span class="sxs-lookup"><span data-stu-id="84480-153">You can also easily add or remove entire sections from hello definition, and you can also share definitions with others.</span></span>

2. <span data-ttu-id="84480-154">toosave uw bewerkingen kiezen **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="84480-154">toosave your edits, choose **Save**.</span></span>

## <a name="parameters"></a><span data-ttu-id="84480-155">Parameters</span><span class="sxs-lookup"><span data-stu-id="84480-155">Parameters</span></span>

<span data-ttu-id="84480-156">Enkele mogelijkheden van Logic Apps zijn alleen beschikbaar in de codeweergave, bijvoorbeeld parameters.</span><span class="sxs-lookup"><span data-stu-id="84480-156">Some Logic Apps capabilities are available only in code view, for example, parameters.</span></span> <span data-ttu-id="84480-157">Parameters kunnen u eenvoudig tooreuse waarden in uw logische app.</span><span class="sxs-lookup"><span data-stu-id="84480-157">Parameters make it easy tooreuse values throughout your logic app.</span></span> <span data-ttu-id="84480-158">Als u een e-mailadres die u gebruiken in verschillende acties wilt hebt, moet u dat e-mailadres definiëren als een parameter.</span><span class="sxs-lookup"><span data-stu-id="84480-158">For example, if you have an email address that you want use in several actions, you should define that email address as a parameter.</span></span>

<span data-ttu-id="84480-159">Parameters zijn goed voor het ophalen van waarden waarschijnlijk toochange veel te zijn.</span><span class="sxs-lookup"><span data-stu-id="84480-159">Parameters are good for pulling out values that you are likely toochange a lot.</span></span> <span data-ttu-id="84480-160">Ze zijn vooral nuttig wanneer u parameters in verschillende omgevingen toooverride nodig.</span><span class="sxs-lookup"><span data-stu-id="84480-160">They are especially useful when you need toooverride parameters in different environments.</span></span> <span data-ttu-id="84480-161">hoe toooverride parameters op basis van de omgeving, Zie toolearn [logic app-definities auteur](../logic-apps/logic-apps-author-definitions.md) en [REST API-documentatie](https://docs.microsoft.com/rest/api/logic).</span><span class="sxs-lookup"><span data-stu-id="84480-161">toolearn how toooverride parameters based on environment, see [Author logic app definitions](../logic-apps/logic-apps-author-definitions.md) and [REST API documentation](https://docs.microsoft.com/rest/api/logic).</span></span>

<span data-ttu-id="84480-162">Dit voorbeeld ziet u hoe tooupdate uw bestaande logische app zodat u kunt de parameters voor de zoekterm hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="84480-162">This example shows how tooupdate your existing logic app so that you can use parameters for hello query term.</span></span>

1. <span data-ttu-id="84480-163">Hallo zoeken in de codeweergave `parameters : {}` object en voeg een `currentFeedUrl` object:</span><span class="sxs-lookup"><span data-stu-id="84480-163">In code view, find hello `parameters : {}` object, and add a `currentFeedUrl` object:</span></span>

        "currentFeedUrl" : {
            "type" : "string",
            "defaultValue" : "http://rss.cnn.com/rss/cnn_topstories.rss"
        }

2. <span data-ttu-id="84480-164">Ga toohello `When_a_feed-item_is_published` actie, zoeken Hallo `queries` sectie en vervang de waarde van de query Hallo met:`"feedUrl": "#@{parameters('currentFeedUrl')}"`</span><span class="sxs-lookup"><span data-stu-id="84480-164">Go toohello `When_a_feed-item_is_published` action, find hello `queries` section, and replace hello query value with : `"feedUrl": "#@{parameters('currentFeedUrl')}"`</span></span> 

    <span data-ttu-id="84480-165">toojoin twee of meer tekenreeksen, u kunt ook Hallo `concat` functie.</span><span class="sxs-lookup"><span data-stu-id="84480-165">toojoin two or more strings, you can also use hello `concat` function.</span></span> 
    <span data-ttu-id="84480-166">Bijvoorbeeld: `"@concat('#',parameters('currentFeedUrl'))"` werkt hetzelfde als bovenstaande Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="84480-166">For example, `"@concat('#',parameters('currentFeedUrl'))"` works hello same as hello above.</span></span>

3.  <span data-ttu-id="84480-167">Als u bent klaar, kiest u **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="84480-167">When you're done, choose **Save**.</span></span> 

    <span data-ttu-id="84480-168">Nu kunt u Hallo-website RSS-feed door een andere URL via Hallo `currentFeedURL` object.</span><span class="sxs-lookup"><span data-stu-id="84480-168">Now you can change hello website's RSS feed by passing a different URL through hello `currentFeedURL` object.</span></span>

<span data-ttu-id="84480-169">Meer informatie over [hoe tooauthor logic app-definities](../logic-apps/logic-apps-author-definitions.md).</span><span class="sxs-lookup"><span data-stu-id="84480-169">Learn more about [how tooauthor logic app definitions](../logic-apps/logic-apps-author-definitions.md).</span></span>

## <a name="start-logic-app-workflows"></a><span data-ttu-id="84480-170">Logic app-werkstromen starten</span><span class="sxs-lookup"><span data-stu-id="84480-170">Start logic app workflows</span></span>

<span data-ttu-id="84480-171">U hebt verschillende opties voor het starten van Hallo werkstroom gedefinieerd in uw logische app.</span><span class="sxs-lookup"><span data-stu-id="84480-171">You have different options for starting hello workflow defined in your logic app.</span></span> <span data-ttu-id="84480-172">U kunt altijd een werkstroom op verzoek starten in Hallo [Azure-portal].</span><span class="sxs-lookup"><span data-stu-id="84480-172">You can always start a workflow on-demand in hello [Azure portal].</span></span>

### <a name="recurrence-triggers"></a><span data-ttu-id="84480-173">Terugkeerpatroon triggers</span><span class="sxs-lookup"><span data-stu-id="84480-173">Recurrence triggers</span></span>

<span data-ttu-id="84480-174">Een terugkeerpatroon trigger wordt uitgevoerd met een interval dat u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="84480-174">A recurrence trigger runs at an interval that you specify.</span></span> <span data-ttu-id="84480-175">Wanneer Hallo-trigger voorwaardelijke logica heeft, bepaalt Hallo trigger of Hallo werkstroom toorun nodig.</span><span class="sxs-lookup"><span data-stu-id="84480-175">When hello trigger has conditional logic, hello trigger determines whether hello workflow needs toorun.</span></span> <span data-ttu-id="84480-176">Een trigger geeft Hallo werkstroom moet worden uitgevoerd door te retourneren een `200` statuscode.</span><span class="sxs-lookup"><span data-stu-id="84480-176">A trigger indicates hello workflow should run by returning a `200` status code.</span></span> <span data-ttu-id="84480-177">Wanneer Hallo werkstroom niet toorun hoeft, Hallo trigger retourneert een `202` statuscode.</span><span class="sxs-lookup"><span data-stu-id="84480-177">When hello workflow doesn't need toorun, hello trigger returns a `202` status code.</span></span>

### <a name="callback-using-rest-apis"></a><span data-ttu-id="84480-178">Callback met REST API 's</span><span class="sxs-lookup"><span data-stu-id="84480-178">Callback using REST APIs</span></span>

<span data-ttu-id="84480-179">een werkstroom toostart, services kunnen een logic app-eindpunt aanroepen.</span><span class="sxs-lookup"><span data-stu-id="84480-179">toostart a workflow, services can call a logic app endpoint.</span></span> <span data-ttu-id="84480-180">Dit soort logic app op aanvraag, kiest u toostart **nu uitvoeren** op Hallo opdrachtbalk klikken.</span><span class="sxs-lookup"><span data-stu-id="84480-180">toostart this kind of logic app on-demand, choose **Run now** on hello command bar.</span></span> <span data-ttu-id="84480-181">Zie [werkstromen starten door het aanroepen van logic app eindpunten als triggers](../logic-apps/logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="84480-181">See [Start workflows by calling logic app endpoints as triggers](../logic-apps/logic-apps-http-endpoint.md).</span></span> 

<!-- Shared links -->
[Azure-portal]: https://portal.azure.com

## <a name="next-steps"></a><span data-ttu-id="84480-183">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="84480-183">Next steps</span></span>

* [<span data-ttu-id="84480-184">Switch-instructies</span><span class="sxs-lookup"><span data-stu-id="84480-184">Switch statements</span></span>](../logic-apps/logic-apps-switch-case.md) 
* [<span data-ttu-id="84480-185">Lussen, bereiken en debatching</span><span class="sxs-lookup"><span data-stu-id="84480-185">Loops, scopes, and debatching</span></span>](../logic-apps/logic-apps-loops-and-scopes.md)
* [<span data-ttu-id="84480-186">Definities voor logische apps maken</span><span class="sxs-lookup"><span data-stu-id="84480-186">Author logic app definitions</span></span>](../logic-apps/logic-apps-author-definitions.md)