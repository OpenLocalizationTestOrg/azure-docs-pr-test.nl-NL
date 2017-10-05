---
title: Switch-instructie voor verschillende acties in Azure Logic Apps | Microsoft Docs
description: Kies verschillende acties uitvoeren in logic apps op basis van Expressiewaarden met behulp van een switch-instructie
services: logic-apps
keywords: Switch-instructie
author: derek1ee
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: LADocs; deli
ms.openlocfilehash: 338b6a5b549d7bf81186550295608438ac4aee32
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="perform-different-actions-in-logic-apps-with-a-switch-statement"></a><span data-ttu-id="695be-104">Verschillende acties worden uitgevoerd in logic apps met een switch-instructie</span><span class="sxs-lookup"><span data-stu-id="695be-104">Perform different actions in logic apps with a switch statement</span></span>

<span data-ttu-id="695be-105">Bij het ontwerpen van een werkstroom, moet u vaak andere acties onderneemt op basis van de waarde van een object of een expressie.</span><span class="sxs-lookup"><span data-stu-id="695be-105">When authoring a workflow, you often have to take different actions based on the value of an object or expression.</span></span> <span data-ttu-id="695be-106">Bijvoorbeeld, kunt u uw logische app zich gedragen anders op basis van de statuscode van een HTTP-aanvraag, of een optie in een e-mailbericht hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="695be-106">For example, you might want your logic app to behave differently based on the status code of an HTTP request, or an option selected in an email.</span></span>

<span data-ttu-id="695be-107">U kunt een switch-instructie voor het implementeren van deze scenario's.</span><span class="sxs-lookup"><span data-stu-id="695be-107">You can use a switch statement to implement these scenarios.</span></span> <span data-ttu-id="695be-108">Uw logische app kunt evalueren van een token of een expressie en kies het geval is bij dezelfde waarde binnen de opgegeven acties uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="695be-108">Your logic app can evaluate a token or expression, and choose the case with the same value to execute the specified actions.</span></span> <span data-ttu-id="695be-109">Slechts één case moet overeenkomen met de switch-instructie.</span><span class="sxs-lookup"><span data-stu-id="695be-109">Only one case should match the switch statement.</span></span>

> [!TIP]
> <span data-ttu-id="695be-110">Net als alle programmeertalen ondersteuning switch instructies alleen gelijkheid operators.</span><span class="sxs-lookup"><span data-stu-id="695be-110">Like all programming languages, switch statements support only equality operators.</span></span> <span data-ttu-id="695be-111">Als u andere relationele operators, zoals 'groter dan', gebruikt u een voorwaardeninstructie.</span><span class="sxs-lookup"><span data-stu-id="695be-111">If you need other relational operators, such as "greater than", use a condition statement.</span></span>
> <span data-ttu-id="695be-112">Om ervoor te zorgen deterministische uitvoeringsgedrag, moeten gevallen een uniek en statische waarde in plaats van de dynamische-tokens of expressie bevatten.</span><span class="sxs-lookup"><span data-stu-id="695be-112">To ensure deterministic execution behavior, cases must contain a unique and static value instead of dynamic tokens or expression.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="695be-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="695be-113">Prerequisites</span></span>

- <span data-ttu-id="695be-114">Een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="695be-114">An active Azure subscription.</span></span> <span data-ttu-id="695be-115">Als u een actief Azure-abonnement geen [een gratis account maken](https://azure.microsoft.com/free/), of probeer [Logic Apps voor gratis](https://tryappservice.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="695be-115">If you don't have an active Azure subscription, [create a free account](https://azure.microsoft.com/free/), or try [Logic Apps for free](https://tryappservice.azure.com/).</span></span>
- [<span data-ttu-id="695be-116">Elementaire kennis over logic apps</span><span class="sxs-lookup"><span data-stu-id="695be-116">Basic knowledge about logic apps</span></span>](logic-apps-what-are-logic-apps.md)

## <a name="add-a-switch-statement-to-your-workflow"></a><span data-ttu-id="695be-117">Een switchinstructie toevoegen aan uw werkstroom</span><span class="sxs-lookup"><span data-stu-id="695be-117">Add a switch statement to your workflow</span></span>

<span data-ttu-id="695be-118">Als u wilt weergeven op de werking van een switch-instructie, wordt in dit voorbeeld een logische app dat bestanden geüpload naar Dropbox bewaakt.</span><span class="sxs-lookup"><span data-stu-id="695be-118">To show how a switch statement works, this example creates a logic app that monitors files uploaded to Dropbox.</span></span> <span data-ttu-id="695be-119">Wanneer de nieuwe bestanden zijn geüpload, verzendt de logische app e-mail naar een goedkeurder die u kiest of moet worden overgedragen van die bestanden naar SharePoint.</span><span class="sxs-lookup"><span data-stu-id="695be-119">When the new files are uploaded, the logic app sends email to an approver who chooses whether to transfer those files to SharePoint.</span></span> <span data-ttu-id="695be-120">De app gebruikmaakt van een switch-instructie waarmee u verschillende acties die zijn gebaseerd op de waarde die de goedkeurder selecteert.</span><span class="sxs-lookup"><span data-stu-id="695be-120">The app uses a switch statement that performs different actions based on the value that the approver selects.</span></span>

1. <span data-ttu-id="695be-121">Een logische app maken en selecteer deze trigger: **Dropbox - wanneer een bestand wordt gemaakt**.</span><span class="sxs-lookup"><span data-stu-id="695be-121">Create a logic app, and select this trigger: **Dropbox - When a file is created**.</span></span>

   ![Dropbox - gebruiken wanneer een bestand trigger wordt gemaakt](./media/logic-apps-switch-case/dropbox-trigger.jpg)

2. <span data-ttu-id="695be-123">Deze actie toevoegen onder de trigger: **Outlook.com - e-mailbericht verzenden-goedkeuring**</span><span class="sxs-lookup"><span data-stu-id="695be-123">Under the trigger, add this action: **Outlook.com - Send approval email**</span></span>

   > [!TIP]
   > <span data-ttu-id="695be-124">Logische apps ondersteunen ook verzenden goedkeuring e-scenario's uit een Outlook van Office 365-account.</span><span class="sxs-lookup"><span data-stu-id="695be-124">Logic apps also support sending approval email scenarios from an Office 365 Outlook account.</span></span>

   - <span data-ttu-id="695be-125">Als u een bestaande verbinding geen hebt, wordt u gevraagd een maken.</span><span class="sxs-lookup"><span data-stu-id="695be-125">If you don't have an existing connection, you're prompted to create one.</span></span>
   - <span data-ttu-id="695be-126">Vul de vereiste velden in.</span><span class="sxs-lookup"><span data-stu-id="695be-126">Fill in the required fields.</span></span> <span data-ttu-id="695be-127">Bijvoorbeeld onder **naar**, geef het e-mailadres voor het verzenden van het e-mailbericht goedkeurder.</span><span class="sxs-lookup"><span data-stu-id="695be-127">For example, under **To**, specify the email address for sending the approver email.</span></span>
   - <span data-ttu-id="695be-128">Onder **gebruikersopties**, voer `Approve, Reject`.</span><span class="sxs-lookup"><span data-stu-id="695be-128">Under **User Options**, enter `Approve, Reject`.</span></span>

   ![Configureer de verbinding](./media/logic-apps-switch-case/send-approval-email-action.jpg)

3. <span data-ttu-id="695be-130">Toevoegen van een switchinstructie.</span><span class="sxs-lookup"><span data-stu-id="695be-130">Add a switch statement.</span></span>

   - <span data-ttu-id="695be-131">Selecteer **+ een nieuwe stap** > **... Meer** > **toevoegen van een case**.</span><span class="sxs-lookup"><span data-stu-id="695be-131">Select **+ New step** > **... More** > **Add a switch case**.</span></span> 
   - <span data-ttu-id="695be-132">Nu we willen selecteert u de actie om uit te voeren op basis van de `SelectedOptions` de uitvoer van de *goedkeuring per E-mail* in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="695be-132">Now we want to select the action to perform based on the `SelectedOptions` output from the *Send approval email* action.</span></span> 
   <span data-ttu-id="695be-133">U vindt dit veld in de **dynamische inhoud toevoegen** selector.</span><span class="sxs-lookup"><span data-stu-id="695be-133">You can find this field in the **Add dynamic content** selector.</span></span>
   - <span data-ttu-id="695be-134">Gebruik *geval 1* om af te handelen wanneer de goedkeurder selecteert `Approve`.</span><span class="sxs-lookup"><span data-stu-id="695be-134">Use *Case 1* to handle when the approver selects `Approve`.</span></span>
     - <span data-ttu-id="695be-135">Als goedgekeurd, kopieert u het oorspronkelijke bestand tot SharePoint Online met de [ **SharePoint Online - bestand maken** actie](../connectors/connectors-create-api-sharepointonline.md).</span><span class="sxs-lookup"><span data-stu-id="695be-135">If approved, copy the original file to SharePoint Online with the [**SharePoint Online - Create file** action](../connectors/connectors-create-api-sharepointonline.md).</span></span>
     - <span data-ttu-id="695be-136">Voeg een andere actie binnen de aanvraag om gebruikers te waarschuwen dat een nieuw bestand beschikbaar in SharePoint is.</span><span class="sxs-lookup"><span data-stu-id="695be-136">Add another action within the case to notify users that a new file is available on SharePoint.</span></span>
   - <span data-ttu-id="695be-137">Een andere aanvraag om af te handelen wanneer gebruiker selecteert toevoegen `Reject`.</span><span class="sxs-lookup"><span data-stu-id="695be-137">Add another case to handle when user selects `Reject`.</span></span>
     - <span data-ttu-id="695be-138">Als afgewezen, verzendt u een e-mailmelding andere goedkeurders wordt geïnformeerd dat het bestand wordt geweigerd en geen verdere actie vereist is.</span><span class="sxs-lookup"><span data-stu-id="695be-138">If rejected, send a notification email informing other approvers that the file is rejected and no further action is required.</span></span>
   - <span data-ttu-id="695be-139">`SelectedOptions`biedt slechts twee opties, zodat we kunt laten de **standaard** geval leeg.</span><span class="sxs-lookup"><span data-stu-id="695be-139">`SelectedOptions` provides only two options, so we can leave the **Default** case empty.</span></span>

   ![Switch-instructie](./media/logic-apps-switch-case/switch.jpg)

   > [!NOTE]
   > <span data-ttu-id="695be-141">Switch-instructie moet ten minste één case naast de standaard-case.</span><span class="sxs-lookup"><span data-stu-id="695be-141">A switch statement needs at least one case in addition to the default case.</span></span>

4. <span data-ttu-id="695be-142">Het oorspronkelijke bestand geüpload naar Dropbox door deze actie toe te voegen na de instructie switch worden verwijderd: **Dropbox - bestand verwijderen**</span><span class="sxs-lookup"><span data-stu-id="695be-142">After the switch statement, delete the original file uploaded to Dropbox by adding this action: **Dropbox - Delete file**</span></span>

5. <span data-ttu-id="695be-143">Sla uw logische app.</span><span class="sxs-lookup"><span data-stu-id="695be-143">Save your logic app.</span></span> <span data-ttu-id="695be-144">Uw app testen door een bestand uploadt naar Dropbox.</span><span class="sxs-lookup"><span data-stu-id="695be-144">Test your app by uploading a file to Dropbox.</span></span> <span data-ttu-id="695be-145">U ontvangt binnenkort een e-mailbericht goedkeuring.</span><span class="sxs-lookup"><span data-stu-id="695be-145">You should receive an approval email shortly.</span></span> <span data-ttu-id="695be-146">Selecteer een optie en het gedrag observeren.</span><span class="sxs-lookup"><span data-stu-id="695be-146">Select an option, and observe the behavior.</span></span>

   > [!TIP]
   > <span data-ttu-id="695be-147">Bekijk hoe [uw logische apps bewaken](logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="695be-147">Check out how to [monitor your logic apps](logic-apps-monitor-your-logic-apps.md).</span></span>

## <a name="understand-the-code-behind-switch-statements"></a><span data-ttu-id="695be-148">Inzicht in de code achter de switch-instructies</span><span class="sxs-lookup"><span data-stu-id="695be-148">Understand the code behind switch statements</span></span>

<span data-ttu-id="695be-149">Nu dat u een logische app met een switchinstructie is gemaakt, bekijken we de definitie van de code achter de switch-instructie.</span><span class="sxs-lookup"><span data-stu-id="695be-149">Now that you successfully created a logic app using a switch statement, let's look at the code definition behind the switch statement.</span></span>

```json
"Switch": {
    "type": "Switch",
    "expression": "@body('Send_approval_email')?['SelectedOption']",
    "cases": {
        "Case 1" : {
            "case" : "Approved",
            "actions" : {}
        },
        "Case 2" : {
            "case" : "Rejected",
            "actions" : {}
        }
    },
    "default": {
        "actions": {}
    },
    "runAfter": {
        "Send_approval_email": [
            "Succeeded"
        ]
    }
}
```

* <span data-ttu-id="695be-150">`"Switch"`is de naam van de switch-instructie, waarmee u kunt de naam voor de leesbaarheid.</span><span class="sxs-lookup"><span data-stu-id="695be-150">`"Switch"` is the name of the switch statement, which you can rename for readability.</span></span> 
* <span data-ttu-id="695be-151">`"type": "Switch"`Hiermee wordt aangegeven dat de actie een switch-instructie is.</span><span class="sxs-lookup"><span data-stu-id="695be-151">`"type": "Switch"` indicates that the action is a switch statement.</span></span> 
* <span data-ttu-id="695be-152">`"expression"`de goedkeurder geselecteerde optie in dit voorbeeld is en wordt geëvalueerd op basis van elk geval later in de definitie is gedeclareerd.</span><span class="sxs-lookup"><span data-stu-id="695be-152">`"expression"` is the approver's selected option in this example and is evaluated against each case declared later in the definition.</span></span> 
* <span data-ttu-id="695be-153">`"cases"`kan een onbeperkt aantal gevallen bevatten.</span><span class="sxs-lookup"><span data-stu-id="695be-153">`"cases"` can contain any number of cases.</span></span> <span data-ttu-id="695be-154">Voor elk geval `"Case *"` is de standaardnaam van de aanvraag die u kunt de naam voor de leesbaarheid.</span><span class="sxs-lookup"><span data-stu-id="695be-154">For each case, `"Case *"` is the default name of the case, which you can rename for readability.</span></span> 
<span data-ttu-id="695be-155">`"case"`Hiermee geeft u de case-label, waarbij de switch-expressie wordt gebruikt voor vergelijking, en moet een constante en unieke waarde.</span><span class="sxs-lookup"><span data-stu-id="695be-155">`"case"` specifies the case label, which the switch expression uses for comparison, and must be a constant and unique value.</span></span> <span data-ttu-id="695be-156">Als geen van de gevallen overeenkomt met de schakeloptie-expressie, acties onder `"default"` worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="695be-156">If none of the cases match the switch expression, actions under `"default"` are executed.</span></span>

## <a name="get-help"></a><span data-ttu-id="695be-157">Help opvragen</span><span class="sxs-lookup"><span data-stu-id="695be-157">Get help</span></span>

<span data-ttu-id="695be-158">Ga naar het [forum voor Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) om vragen te stellen, vragen te beantwoorden en te zien wat andere gebruikers van Azure Logic Apps aan het doen zijn.</span><span class="sxs-lookup"><span data-stu-id="695be-158">To ask questions, answer questions, and see what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="695be-159">Ter verbetering van Azure Logic Apps en connectors kunt u stemmen op ideeën of ideeën indien op de [site voor gebruikersfeedback van Azure Logic Apps](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="695be-159">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="695be-160">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="695be-160">Next steps</span></span>

- <span data-ttu-id="695be-161">Meer informatie over hoe [voorwaarden toevoegen](logic-apps-use-logic-app-features.md)</span><span class="sxs-lookup"><span data-stu-id="695be-161">Learn how to [add conditions](logic-apps-use-logic-app-features.md)</span></span>
- <span data-ttu-id="695be-162">Meer informatie over [fout en uitzonderingsverwerking](logic-apps-exception-handling.md)</span><span class="sxs-lookup"><span data-stu-id="695be-162">Learn about [error and exception handling](logic-apps-exception-handling.md)</span></span>
- <span data-ttu-id="695be-163">Ontdek meer [werkstroom taal mogelijkheden](logic-apps-author-definitions.md)</span><span class="sxs-lookup"><span data-stu-id="695be-163">Explore more [workflow language capabilities](logic-apps-author-definitions.md)</span></span>