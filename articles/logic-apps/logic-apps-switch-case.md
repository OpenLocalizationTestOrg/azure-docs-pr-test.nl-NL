---
title: de instructie aaaSwitch voor verschillende acties in Azure Logic Apps | Microsoft Docs
description: Kies verschillende acties tooperform in logic apps op basis van Expressiewaarden met behulp van een switch-instructie
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
ms.openlocfilehash: 09ed7e4a752003aba157e9156bf4dc89ef86f5ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="perform-different-actions-in-logic-apps-with-a-switch-statement"></a><span data-ttu-id="aaffa-104">Verschillende acties worden uitgevoerd in logic apps met een switch-instructie</span><span class="sxs-lookup"><span data-stu-id="aaffa-104">Perform different actions in logic apps with a switch statement</span></span>

<span data-ttu-id="aaffa-105">Wanneer het ontwerpen van een werkstroom, hebt u vaak tootake verschillende acties die zijn gebaseerd op Hallo-waarde van een object of een expressie.</span><span class="sxs-lookup"><span data-stu-id="aaffa-105">When authoring a workflow, you often have tootake different actions based on hello value of an object or expression.</span></span> <span data-ttu-id="aaffa-106">Bijvoorbeeld, wilt u mogelijk uw logische app toobehave anders op basis van de statuscode Hallo van een HTTP-aanvraag, of een optie in een e-mailbericht hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="aaffa-106">For example, you might want your logic app toobehave differently based on hello status code of an HTTP request, or an option selected in an email.</span></span>

<span data-ttu-id="aaffa-107">U kunt een instructie switch tooimplement deze scenario's gebruiken.</span><span class="sxs-lookup"><span data-stu-id="aaffa-107">You can use a switch statement tooimplement these scenarios.</span></span> <span data-ttu-id="aaffa-108">Uw logische app kunt beoordelen een token of een expressie, en kies Hallo geval Hello dezelfde waarde tooexecute Hallo opgegeven acties.</span><span class="sxs-lookup"><span data-stu-id="aaffa-108">Your logic app can evaluate a token or expression, and choose hello case with hello same value tooexecute hello specified actions.</span></span> <span data-ttu-id="aaffa-109">Slechts één case moet overeenkomen met de Hallo switch-instructie.</span><span class="sxs-lookup"><span data-stu-id="aaffa-109">Only one case should match hello switch statement.</span></span>

> [!TIP]
> <span data-ttu-id="aaffa-110">Net als alle programmeertalen ondersteuning switch instructies alleen gelijkheid operators.</span><span class="sxs-lookup"><span data-stu-id="aaffa-110">Like all programming languages, switch statements support only equality operators.</span></span> <span data-ttu-id="aaffa-111">Als u andere relationele operators, zoals 'groter dan', gebruikt u een voorwaardeninstructie.</span><span class="sxs-lookup"><span data-stu-id="aaffa-111">If you need other relational operators, such as "greater than", use a condition statement.</span></span>
> <span data-ttu-id="aaffa-112">tooensure deterministische uitvoeringsgedrag, gevallen moeten een uniek en statische waarde in plaats van de dynamische-tokens of expressie bevatten.</span><span class="sxs-lookup"><span data-stu-id="aaffa-112">tooensure deterministic execution behavior, cases must contain a unique and static value instead of dynamic tokens or expression.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aaffa-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="aaffa-113">Prerequisites</span></span>

- <span data-ttu-id="aaffa-114">Een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="aaffa-114">An active Azure subscription.</span></span> <span data-ttu-id="aaffa-115">Als u een actief Azure-abonnement geen [een gratis account maken](https://azure.microsoft.com/free/), of probeer [Logic Apps voor gratis](https://tryappservice.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="aaffa-115">If you don't have an active Azure subscription, [create a free account](https://azure.microsoft.com/free/), or try [Logic Apps for free](https://tryappservice.azure.com/).</span></span>
- [<span data-ttu-id="aaffa-116">Elementaire kennis over logic apps</span><span class="sxs-lookup"><span data-stu-id="aaffa-116">Basic knowledge about logic apps</span></span>](logic-apps-what-are-logic-apps.md)

## <a name="add-a-switch-statement-tooyour-workflow"></a><span data-ttu-id="aaffa-117">Een switch-instructie tooyour-werkstroom toevoegen</span><span class="sxs-lookup"><span data-stu-id="aaffa-117">Add a switch statement tooyour workflow</span></span>

<span data-ttu-id="aaffa-118">tooshow de werking van een switch-instructie, in dit voorbeeld wordt een logische app dat monitors bestanden tooDropbox geüpload.</span><span class="sxs-lookup"><span data-stu-id="aaffa-118">tooshow how a switch statement works, this example creates a logic app that monitors files uploaded tooDropbox.</span></span> <span data-ttu-id="aaffa-119">Wanneer nieuwe Hallo-bestanden zijn geüpload, Hallo logische app verzendt e-mail tooan goedkeurder die u kiest of tootransfer die tooSharePoint bestanden.</span><span class="sxs-lookup"><span data-stu-id="aaffa-119">When hello new files are uploaded, hello logic app sends email tooan approver who chooses whether tootransfer those files tooSharePoint.</span></span> <span data-ttu-id="aaffa-120">Hallo app gebruikmaakt van een switchinstructie die verschillende acties uitvoert op basis van de Hallo die Hallo goedkeurder worden geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="aaffa-120">hello app uses a switch statement that performs different actions based on hello value that hello approver selects.</span></span>

1. <span data-ttu-id="aaffa-121">Een logische app maken en selecteer deze trigger: **Dropbox - wanneer een bestand wordt gemaakt**.</span><span class="sxs-lookup"><span data-stu-id="aaffa-121">Create a logic app, and select this trigger: **Dropbox - When a file is created**.</span></span>

   ![Dropbox - gebruiken wanneer een bestand trigger wordt gemaakt](./media/logic-apps-switch-case/dropbox-trigger.jpg)

2. <span data-ttu-id="aaffa-123">Deze actie onder Hallo-trigger toevoegen: **Outlook.com - e-mailbericht verzenden-goedkeuring**</span><span class="sxs-lookup"><span data-stu-id="aaffa-123">Under hello trigger, add this action: **Outlook.com - Send approval email**</span></span>

   > [!TIP]
   > <span data-ttu-id="aaffa-124">Logische apps ondersteunen ook verzenden goedkeuring e-scenario's uit een Outlook van Office 365-account.</span><span class="sxs-lookup"><span data-stu-id="aaffa-124">Logic apps also support sending approval email scenarios from an Office 365 Outlook account.</span></span>

   - <span data-ttu-id="aaffa-125">Als u een bestaande verbinding geen hebt, wordt u gevraagd toocreate een.</span><span class="sxs-lookup"><span data-stu-id="aaffa-125">If you don't have an existing connection, you're prompted toocreate one.</span></span>
   - <span data-ttu-id="aaffa-126">Vul de velden Hallo vereist.</span><span class="sxs-lookup"><span data-stu-id="aaffa-126">Fill in hello required fields.</span></span> <span data-ttu-id="aaffa-127">Bijvoorbeeld onder **naar**, Hallo e-mailadres voor het verzenden van Hallo goedkeurder e-mailadres opgeven.</span><span class="sxs-lookup"><span data-stu-id="aaffa-127">For example, under **To**, specify hello email address for sending hello approver email.</span></span>
   - <span data-ttu-id="aaffa-128">Onder **gebruikersopties**, voer `Approve, Reject`.</span><span class="sxs-lookup"><span data-stu-id="aaffa-128">Under **User Options**, enter `Approve, Reject`.</span></span>

   ![Configureer de verbinding](./media/logic-apps-switch-case/send-approval-email-action.jpg)

3. <span data-ttu-id="aaffa-130">Toevoegen van een switchinstructie.</span><span class="sxs-lookup"><span data-stu-id="aaffa-130">Add a switch statement.</span></span>

   - <span data-ttu-id="aaffa-131">Selecteer **+ een nieuwe stap** > **... Meer** > **toevoegen van een case**.</span><span class="sxs-lookup"><span data-stu-id="aaffa-131">Select **+ New step** > **... More** > **Add a switch case**.</span></span> 
   - <span data-ttu-id="aaffa-132">Nu we tooselect Hallo actie tooperform op basis van Hallo willen `SelectedOptions` de uitvoer van Hallo *goedkeuring per E-mail* in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="aaffa-132">Now we want tooselect hello action tooperform based on hello `SelectedOptions` output from hello *Send approval email* action.</span></span> 
   <span data-ttu-id="aaffa-133">U vindt dit veld in Hallo **dynamische inhoud toevoegen** selector.</span><span class="sxs-lookup"><span data-stu-id="aaffa-133">You can find this field in hello **Add dynamic content** selector.</span></span>
   - <span data-ttu-id="aaffa-134">Gebruik *geval 1* toohandle wanneer Hallo goedkeurder selecteert `Approve`.</span><span class="sxs-lookup"><span data-stu-id="aaffa-134">Use *Case 1* toohandle when hello approver selects `Approve`.</span></span>
     - <span data-ttu-id="aaffa-135">Als goedgekeurd, kopieert u Hallo oorspronkelijke bestand tooSharePoint Online Hello [ **SharePoint Online - bestand maken** actie](../connectors/connectors-create-api-sharepointonline.md).</span><span class="sxs-lookup"><span data-stu-id="aaffa-135">If approved, copy hello original file tooSharePoint Online with hello [**SharePoint Online - Create file** action](../connectors/connectors-create-api-sharepointonline.md).</span></span>
     - <span data-ttu-id="aaffa-136">Voeg een andere actie Hallo case toonotify gebruikers een nieuw bestand is beschikbaar in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="aaffa-136">Add another action within hello case toonotify users that a new file is available on SharePoint.</span></span>
   - <span data-ttu-id="aaffa-137">Toevoegen van een andere aanvraag toohandle wanneer gebruiker selecteert `Reject`.</span><span class="sxs-lookup"><span data-stu-id="aaffa-137">Add another case toohandle when user selects `Reject`.</span></span>
     - <span data-ttu-id="aaffa-138">Als afgewezen, verzendt u een e-mailmelding andere goedkeurders wordt geïnformeerd dat Hallo-bestand wordt geweigerd en geen verdere actie vereist is.</span><span class="sxs-lookup"><span data-stu-id="aaffa-138">If rejected, send a notification email informing other approvers that hello file is rejected and no further action is required.</span></span>
   - <span data-ttu-id="aaffa-139">`SelectedOptions`biedt slechts twee opties, zodat we Hallo kunt laten **standaard** geval leeg.</span><span class="sxs-lookup"><span data-stu-id="aaffa-139">`SelectedOptions` provides only two options, so we can leave hello **Default** case empty.</span></span>

   ![Switch-instructie](./media/logic-apps-switch-case/switch.jpg)

   > [!NOTE]
   > <span data-ttu-id="aaffa-141">Switch-instructie moet minimaal één letter in geval van toevoeging toohello standaard.</span><span class="sxs-lookup"><span data-stu-id="aaffa-141">A switch statement needs at least one case in addition toohello default case.</span></span>

4. <span data-ttu-id="aaffa-142">Na het Hallo-switch-instructie het oorspronkelijke bestand geüpload tooDropbox Hallo worden verwijderd door deze actie toe te voegen: **Dropbox - bestand verwijderen**</span><span class="sxs-lookup"><span data-stu-id="aaffa-142">After hello switch statement, delete hello original file uploaded tooDropbox by adding this action: **Dropbox - Delete file**</span></span>

5. <span data-ttu-id="aaffa-143">Sla uw logische app.</span><span class="sxs-lookup"><span data-stu-id="aaffa-143">Save your logic app.</span></span> <span data-ttu-id="aaffa-144">Uw app testen door een tooDropbox bestand uploaden.</span><span class="sxs-lookup"><span data-stu-id="aaffa-144">Test your app by uploading a file tooDropbox.</span></span> <span data-ttu-id="aaffa-145">U ontvangt binnenkort een e-mailbericht goedkeuring.</span><span class="sxs-lookup"><span data-stu-id="aaffa-145">You should receive an approval email shortly.</span></span> <span data-ttu-id="aaffa-146">Selecteer een optie en Hallo gedrag observeren.</span><span class="sxs-lookup"><span data-stu-id="aaffa-146">Select an option, and observe hello behavior.</span></span>

   > [!TIP]
   > <span data-ttu-id="aaffa-147">Te zoeken over[uw logische apps bewaken](logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="aaffa-147">Check out how too[monitor your logic apps](logic-apps-monitor-your-logic-apps.md).</span></span>

## <a name="understand-hello-code-behind-switch-statements"></a><span data-ttu-id="aaffa-148">Hallo code achter switch instructies begrijpen</span><span class="sxs-lookup"><span data-stu-id="aaffa-148">Understand hello code behind switch statements</span></span>

<span data-ttu-id="aaffa-149">Nu dat u een logische app met een switchinstructie is gemaakt, bekijken we de definitie van Hallo achter Hallo switch-instructie.</span><span class="sxs-lookup"><span data-stu-id="aaffa-149">Now that you successfully created a logic app using a switch statement, let's look at hello code definition behind hello switch statement.</span></span>

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

* <span data-ttu-id="aaffa-150">`"Switch"`Hallo naam is van de switch-instructie hello, die u kunt de naam voor de leesbaarheid.</span><span class="sxs-lookup"><span data-stu-id="aaffa-150">`"Switch"` is hello name of hello switch statement, which you can rename for readability.</span></span> 
* <span data-ttu-id="aaffa-151">`"type": "Switch"`Geeft aan dat de actie Hallo een switch-instructie.</span><span class="sxs-lookup"><span data-stu-id="aaffa-151">`"type": "Switch"` indicates that hello action is a switch statement.</span></span> 
* <span data-ttu-id="aaffa-152">`"expression"`Hallo goedkeurder van geselecteerde optie in dit voorbeeld is en geëvalueerd op basis van elk geval later in Hallo definitie is gedeclareerd.</span><span class="sxs-lookup"><span data-stu-id="aaffa-152">`"expression"` is hello approver's selected option in this example and is evaluated against each case declared later in hello definition.</span></span> 
* <span data-ttu-id="aaffa-153">`"cases"`kan een onbeperkt aantal gevallen bevatten.</span><span class="sxs-lookup"><span data-stu-id="aaffa-153">`"cases"` can contain any number of cases.</span></span> <span data-ttu-id="aaffa-154">Voor elk geval `"Case *"` is de standaardnaam hello van geval Hallo die u kunt de naam voor de leesbaarheid.</span><span class="sxs-lookup"><span data-stu-id="aaffa-154">For each case, `"Case *"` is hello default name of hello case, which you can rename for readability.</span></span> 
<span data-ttu-id="aaffa-155">`"case"`Hiermee geeft u Hallo case-label, waarvoor de switch-expressie gebruikt voor vergelijking Hallo en moet een constante en unieke waarde.</span><span class="sxs-lookup"><span data-stu-id="aaffa-155">`"case"` specifies hello case label, which hello switch expression uses for comparison, and must be a constant and unique value.</span></span> <span data-ttu-id="aaffa-156">Als geen van de gevallen Hallo overeenkomt met de Hallo schakelexpressie, acties onder `"default"` worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="aaffa-156">If none of hello cases match hello switch expression, actions under `"default"` are executed.</span></span>

## <a name="get-help"></a><span data-ttu-id="aaffa-157">Help opvragen</span><span class="sxs-lookup"><span data-stu-id="aaffa-157">Get help</span></span>

<span data-ttu-id="aaffa-158">tooask vragen, antwoorden op vragen, en zien welke andere Azure Logic Apps-gebruikers doen, gaat u naar Hallo [Azure Logic Apps-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="aaffa-158">tooask questions, answer questions, and see what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="aaffa-159">toohelp Azure Logic Apps en connectors verbeteren, stem of ideeën op Hallo indienen [Azure Logic Apps gebruiker feedback site](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="aaffa-159">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="aaffa-160">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="aaffa-160">Next steps</span></span>

- <span data-ttu-id="aaffa-161">Meer informatie over hoe te[voorwaarden toevoegen](logic-apps-use-logic-app-features.md)</span><span class="sxs-lookup"><span data-stu-id="aaffa-161">Learn how too[add conditions](logic-apps-use-logic-app-features.md)</span></span>
- <span data-ttu-id="aaffa-162">Meer informatie over [fout en uitzonderingsverwerking](logic-apps-exception-handling.md)</span><span class="sxs-lookup"><span data-stu-id="aaffa-162">Learn about [error and exception handling](logic-apps-exception-handling.md)</span></span>
- <span data-ttu-id="aaffa-163">Ontdek meer [werkstroom taal mogelijkheden](logic-apps-author-definitions.md)</span><span class="sxs-lookup"><span data-stu-id="aaffa-163">Explore more [workflow language capabilities](logic-apps-author-definitions.md)</span></span>