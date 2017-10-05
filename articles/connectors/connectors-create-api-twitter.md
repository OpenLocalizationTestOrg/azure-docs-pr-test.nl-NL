---
title: Informatie over het gebruik van de Twitter-connector in logic apps | Microsoft Docs
description: Overzicht van Twitter-connector met de parameters van de REST-API
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 8bce2183-544d-4668-a2dc-9a62c152d9fa
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: be8163043535833ce45b3d50939a537406cf8152
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-twitter-connector"></a><span data-ttu-id="9add1-103">Aan de slag met de Twitter-connector</span><span class="sxs-lookup"><span data-stu-id="9add1-103">Get started with the Twitter connector</span></span>
<span data-ttu-id="9add1-104">Met de Twitter-connector kunt u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="9add1-104">With the Twitter connector you can:</span></span>

* <span data-ttu-id="9add1-105">Tweets post en get-tweets</span><span class="sxs-lookup"><span data-stu-id="9add1-105">Post tweets and get tweets</span></span>
* <span data-ttu-id="9add1-106">Pc-gebruikers en toegang tijdlijnen, vrienden</span><span class="sxs-lookup"><span data-stu-id="9add1-106">Access timelines, friends and followers</span></span>
* <span data-ttu-id="9add1-107">Voer één van de andere bewerkingen en triggers die hieronder wordt beschreven</span><span class="sxs-lookup"><span data-stu-id="9add1-107">Perform any of the other actions and triggers described below</span></span>  

<span data-ttu-id="9add1-108">Gebruik [elke connector](apis-list.md), moet u eerst een logische app maken.</span><span class="sxs-lookup"><span data-stu-id="9add1-108">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="9add1-109">U kunt aan de slag door [maken van een logische app nu](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="9add1-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>  

## <a name="connect-to-twitter"></a><span data-ttu-id="9add1-110">Verbinding maken met Twitter</span><span class="sxs-lookup"><span data-stu-id="9add1-110">Connect to Twitter</span></span>
<span data-ttu-id="9add1-111">Om uw logische app toegang alle services tot, moet u eerst maken een *verbinding* naar de service.</span><span class="sxs-lookup"><span data-stu-id="9add1-111">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="9add1-112">Een [verbinding](connectors-overview.md) biedt connectiviteit tussen een logische app en een andere service.</span><span class="sxs-lookup"><span data-stu-id="9add1-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-twitter"></a><span data-ttu-id="9add1-113">Maak een verbinding met Twitter</span><span class="sxs-lookup"><span data-stu-id="9add1-113">Create a connection to Twitter</span></span>
> [!INCLUDE [Steps to create a connection to Twitter](../../includes/connectors-create-api-twitter.md)]
> 
> 

## <a name="use-a-twitter-trigger"></a><span data-ttu-id="9add1-114">Gebruik een trigger Twitter</span><span class="sxs-lookup"><span data-stu-id="9add1-114">Use a Twitter trigger</span></span>
<span data-ttu-id="9add1-115">Een trigger is een gebeurtenis die kan worden gebruikt om de werkstroom die is gedefinieerd in een logische app te starten.</span><span class="sxs-lookup"><span data-stu-id="9add1-115">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="9add1-116">[Meer informatie over triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="9add1-116">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="9add1-117">In dit voorbeeld leest u het gebruik van de **wanneer een nieuwe tweet wordt gepost** trigger zoeken naar #Seattle en, als #Seattle wordt gevonden, het bijwerken van een bestand in Dropbox met de tekst van de tweet.</span><span class="sxs-lookup"><span data-stu-id="9add1-117">In this example, I will show you how to use the **When a new tweet is posted**  trigger to search for #Seattle and, if #Seattle is found, update a file in Dropbox with the text from the tweet.</span></span> <span data-ttu-id="9add1-118">In een enterprise-voorbeeld, kan u de naam van uw bedrijf zoeken en een SQL-database bijwerken met de tekst van de tweet.</span><span class="sxs-lookup"><span data-stu-id="9add1-118">In an enterprise example, you could search for the name of your company and update a SQL database with the text from the tweet.</span></span>

1. <span data-ttu-id="9add1-119">Voer *twitter* in het zoekvak op de ontwerpfunctie van logic apps selecteert u vervolgens de **Twitter - wanneer een nieuwe tweet wordt teruggepost** trigger</span><span class="sxs-lookup"><span data-stu-id="9add1-119">Enter *twitter* in the search box on the logic apps designer then select the **Twitter - When a new tweet is posted**  trigger</span></span>   
   <span data-ttu-id="9add1-120">![Twitter triggerafbeelding 1](./media/connectors-create-api-twitter/trigger-1.png)</span><span class="sxs-lookup"><span data-stu-id="9add1-120">![Twitter trigger image 1](./media/connectors-create-api-twitter/trigger-1.png)</span></span>  
2. <span data-ttu-id="9add1-121">Voer *#Seattle* in de **zoektekst** besturingselement</span><span class="sxs-lookup"><span data-stu-id="9add1-121">Enter *#Seattle* in the **Search Text** control</span></span>  
   <span data-ttu-id="9add1-122">![Afbeelding van de trigger Twitter 2](./media/connectors-create-api-twitter/trigger-2.png)</span><span class="sxs-lookup"><span data-stu-id="9add1-122">![Twitter trigger image 2](./media/connectors-create-api-twitter/trigger-2.png)</span></span> 

<span data-ttu-id="9add1-123">Op dit moment is uw logische app geconfigureerd met een trigger die een uitvoering van de andere triggers en acties in de werkstroom wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="9add1-123">At this point, your logic app has been configured with a trigger that will begin a run of the other triggers and actions in the workflow.</span></span> 

> [!NOTE]
> <span data-ttu-id="9add1-124">Voor een logische app wilt gebruiken, moet er ten minste één trigger en één actie bevatten.</span><span class="sxs-lookup"><span data-stu-id="9add1-124">For a logic app to be functional, it must contain at least one trigger and one action.</span></span> <span data-ttu-id="9add1-125">Volg de stappen in de volgende sectie voor een actie toevoegen.</span><span class="sxs-lookup"><span data-stu-id="9add1-125">Follow the steps in the next section to add an action.</span></span>  
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="9add1-126">Een voorwaarde toevoegen</span><span class="sxs-lookup"><span data-stu-id="9add1-126">Add a condition</span></span>
<span data-ttu-id="9add1-127">Omdat we alleen geïnteresseerd in tweets van gebruikers met meer dan 50 van gebruikers bent, moet eerst een voorwaarde waarmee wordt bevestigd het aantal pc-gebruikers dat worden toegevoegd aan de logische app.</span><span class="sxs-lookup"><span data-stu-id="9add1-127">Since we are only interested in tweets from users with more than 50 users, a condition that confirms the number of followers must first be added to the logic app.</span></span>  

1. <span data-ttu-id="9add1-128">Selecteer **+ een nieuwe stap** om toe te voegen van de actie die u uitvoeren wilt wanneer #Seattle in een nieuwe tweet wordt gevonden</span><span class="sxs-lookup"><span data-stu-id="9add1-128">Select **+ New step** to add the action you would like to take when #Seattle is found in a new tweet</span></span>  
   <span data-ttu-id="9add1-129">![Afbeelding 1 Twitter](../../includes/media/connectors-create-api-twitter/action-1.png)</span><span class="sxs-lookup"><span data-stu-id="9add1-129">![Twitter action image 1](../../includes/media/connectors-create-api-twitter/action-1.png)</span></span>  
2. <span data-ttu-id="9add1-130">Selecteer de **een voorwaarde toevoegen** koppeling.</span><span class="sxs-lookup"><span data-stu-id="9add1-130">Select the **Add a condition** link.</span></span>  
   <span data-ttu-id="9add1-131">![Twitter voorwaarde afbeelding 1](../../includes/media/connectors-create-api-twitter/condition-1.png) </span><span class="sxs-lookup"><span data-stu-id="9add1-131">![Twitter condition image 1](../../includes/media/connectors-create-api-twitter/condition-1.png) </span></span>  
   <span data-ttu-id="9add1-132">Hiermee opent u de **voorwaarde** besturingselement waarin kunt u voorwaarden zoals controleren *gelijk is aan*, *is minder dan*, *is groter dan*, *bevat*, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="9add1-132">This opens the **Condition** control where you can check conditions such as *is equal to*, *is less than*, *is greater than*, *contains*, etc.</span></span>  
   <span data-ttu-id="9add1-133">![Afbeelding van de voorwaarde Twitter 2](../../includes/media/connectors-create-api-twitter/condition-2.png)</span><span class="sxs-lookup"><span data-stu-id="9add1-133">![Twitter condition image 2](../../includes/media/connectors-create-api-twitter/condition-2.png)</span></span>   
3. <span data-ttu-id="9add1-134">Selecteer de **kiest u een waarde** besturingselement.</span><span class="sxs-lookup"><span data-stu-id="9add1-134">Select the **Choose a value** control.</span></span>  
   <span data-ttu-id="9add1-135">In dit besturingselement kunt u een of meer van de eigenschappen van de vorige acties of triggers als de waarde waarvan voorwaarde wordt geëvalueerd als waar of ONWAAR.</span><span class="sxs-lookup"><span data-stu-id="9add1-135">In this control, you can select one or more of the properties from any previous actions or triggers as the value whose condition will be evaluated to true or false.</span></span>
   <span data-ttu-id="9add1-136">![Twitter voorwaarde afbeelding 3](../../includes/media/connectors-create-api-twitter/condition-3.png)</span><span class="sxs-lookup"><span data-stu-id="9add1-136">![Twitter condition image 3](../../includes/media/connectors-create-api-twitter/condition-3.png)</span></span>   
4. <span data-ttu-id="9add1-137">Selecteer de **...**  uitbreiden van de lijst met eigenschappen, zodat u kunt zien dat alle eigenschappen die beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="9add1-137">Select the **...** to expand the list of properties so you can see all the properties that are available.</span></span>        
   <span data-ttu-id="9add1-138">![Twitter voorwaarde afbeelding 4](../../includes/media/connectors-create-api-twitter/condition-4.png)</span><span class="sxs-lookup"><span data-stu-id="9add1-138">![Twitter condition image 4](../../includes/media/connectors-create-api-twitter/condition-4.png)</span></span>   
5. <span data-ttu-id="9add1-139">Selecteer de **pc-gebruikers aantal** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="9add1-139">Select the **Followers count** property.</span></span>    
   <span data-ttu-id="9add1-140">![Twitter voorwaarde afbeelding 5](../../includes/media/connectors-create-api-twitter/condition-5.png)</span><span class="sxs-lookup"><span data-stu-id="9add1-140">![Twitter condition image 5](../../includes/media/connectors-create-api-twitter/condition-5.png)</span></span>   
6. <span data-ttu-id="9add1-141">Let op de pc-gebruikers count-eigenschap is nu in het besturingselement waarde.</span><span class="sxs-lookup"><span data-stu-id="9add1-141">Notice the Followers count property is now in the value control.</span></span>    
   ![Twitter voorwaarde afbeelding 6](../../includes/media/connectors-create-api-twitter/condition-6.png)   
7. <span data-ttu-id="9add1-143">Selecteer **is groter dan** uit de lijst operators.</span><span class="sxs-lookup"><span data-stu-id="9add1-143">Select **is greater than** from the operators list.</span></span>    
   <span data-ttu-id="9add1-144">![Twitter voorwaarde afbeelding 7](../../includes/media/connectors-create-api-twitter/condition-7.png)</span><span class="sxs-lookup"><span data-stu-id="9add1-144">![Twitter condition image 7](../../includes/media/connectors-create-api-twitter/condition-7.png)</span></span>   
8. <span data-ttu-id="9add1-145">50 invoeren als de operand voor de *is groter dan* operator.</span><span class="sxs-lookup"><span data-stu-id="9add1-145">Enter 50 as the operand for the *is greater than* operator.</span></span>  
   <span data-ttu-id="9add1-146">De voorwaarde is nu toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="9add1-146">The condition is now added.</span></span> <span data-ttu-id="9add1-147">Sla uw werk met de **opslaan** koppeling in het menu hierboven.</span><span class="sxs-lookup"><span data-stu-id="9add1-147">Save your work using the **Save** link on the menu above.</span></span>    
   <span data-ttu-id="9add1-148">![Twitter voorwaarde afbeelding 8](../../includes/media/connectors-create-api-twitter/condition-8.png)</span><span class="sxs-lookup"><span data-stu-id="9add1-148">![Twitter condition image 8](../../includes/media/connectors-create-api-twitter/condition-8.png)</span></span>   

## <a name="use-a-twitter-action"></a><span data-ttu-id="9add1-149">Gebruik een Twitter-actie</span><span class="sxs-lookup"><span data-stu-id="9add1-149">Use a Twitter action</span></span>
<span data-ttu-id="9add1-150">Een actie is een bewerking uitgevoerd door de werkstroom die is gedefinieerd in een logische app.</span><span class="sxs-lookup"><span data-stu-id="9add1-150">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="9add1-151">[Meer informatie over acties](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="9add1-151">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="9add1-152">Nu dat u een trigger hebt toegevoegd, volg deze stappen uit om een actie die een nieuwe tweet met de inhoud van de tweets gevonden door de trigger wordt geplaatst.</span><span class="sxs-lookup"><span data-stu-id="9add1-152">Now that you have added a trigger, follow these steps to add an action that will post a new tweet with the contents of the tweets found by the trigger.</span></span> <span data-ttu-id="9add1-153">Voor de doeleinden van deze procedure wordt alleen tweets van gebruikers met meer dan 50 pc-gebruikers worden geplaatst.</span><span class="sxs-lookup"><span data-stu-id="9add1-153">For the purposes of this walk-through only tweets from users with more than 50 followers will be posted.</span></span>  

<span data-ttu-id="9add1-154">In de volgende stap voegt u een Twitter-actie die een tweet gebruikmakend van de eigenschappen van elke tweet die is geplaatst door een gebruiker die meer dan 50 pc-gebruikers heeft wordt geplaatst.</span><span class="sxs-lookup"><span data-stu-id="9add1-154">In the next step, you will add a Twitter action that will post a tweet using some of the properties of each tweet that has been posted by a user who has more than 50 followers.</span></span>  

1. <span data-ttu-id="9add1-155">Selecteer **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="9add1-155">Select **Add an action**.</span></span> <span data-ttu-id="9add1-156">Hiermee opent u de zoekbesturing waar u naar andere acties en triggers zoeken kunt.</span><span class="sxs-lookup"><span data-stu-id="9add1-156">This opens the search control where you can search for other actions and triggers.</span></span>  
   <span data-ttu-id="9add1-157">![Twitter voorwaarde afbeelding 9](../../includes/media/connectors-create-api-twitter/condition-9.png)</span><span class="sxs-lookup"><span data-stu-id="9add1-157">![Twitter condition image 9](../../includes/media/connectors-create-api-twitter/condition-9.png)</span></span>   
2. <span data-ttu-id="9add1-158">Voer *twitter* in het zoekvak selecteert de **Twitter - een tweet boeken** in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="9add1-158">Enter *twitter* into the search box then select the **Twitter - Post a tweet** action.</span></span> <span data-ttu-id="9add1-159">Hiermee opent u de **een tweet boeken** bepalen waar u alle details wordt invoeren voor de tweet wordt geplaatst.</span><span class="sxs-lookup"><span data-stu-id="9add1-159">This opens the **Post a tweet** control where you will enter all details for the tweet being posted.</span></span>      
   <span data-ttu-id="9add1-160">![Actie afbeelding 1-5 Twitter](../../includes/media/connectors-create-api-twitter/action-1-5.png)</span><span class="sxs-lookup"><span data-stu-id="9add1-160">![Twitter action image 1-5](../../includes/media/connectors-create-api-twitter/action-1-5.png)</span></span>   
3. <span data-ttu-id="9add1-161">Selecteer de **Tweet tekst** besturingselement.</span><span class="sxs-lookup"><span data-stu-id="9add1-161">Select the **Tweet text** control.</span></span> <span data-ttu-id="9add1-162">Alle uitvoerwaarden van de vorige acties en triggers in de logische app worden nu weergegeven.</span><span class="sxs-lookup"><span data-stu-id="9add1-162">All outputs from previous actions and triggers in the logic app are now visible.</span></span> <span data-ttu-id="9add1-163">U kunt een van deze selecteren en ze als onderdeel van de tekst tweet van de nieuwe tweet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9add1-163">You can select any of these and use them as part of the tweet text of the new tweet.</span></span>     
   <span data-ttu-id="9add1-164">![Afbeelding 2 Twitter](../../includes/media/connectors-create-api-twitter/action-2.png)</span><span class="sxs-lookup"><span data-stu-id="9add1-164">![Twitter action image 2](../../includes/media/connectors-create-api-twitter/action-2.png)</span></span>   
4. <span data-ttu-id="9add1-165">Selecteer **gebruikersnaam**</span><span class="sxs-lookup"><span data-stu-id="9add1-165">Select **User name**</span></span>   
5. <span data-ttu-id="9add1-166">Voer *zegt:* in het tekstvak tweet.</span><span class="sxs-lookup"><span data-stu-id="9add1-166">Enter *says:* in the tweet text control.</span></span> <span data-ttu-id="9add1-167">Doe dit direct na de gebruikersnaam.</span><span class="sxs-lookup"><span data-stu-id="9add1-167">Do this just after User name.</span></span>  
6. <span data-ttu-id="9add1-168">Selecteer *Tweet tekst*.</span><span class="sxs-lookup"><span data-stu-id="9add1-168">Select *Tweet text*.</span></span>       
   <span data-ttu-id="9add1-169">![Afbeelding 3 Twitter](../../includes/media/connectors-create-api-twitter/action-3.png)</span><span class="sxs-lookup"><span data-stu-id="9add1-169">![Twitter action image 3](../../includes/media/connectors-create-api-twitter/action-3.png)</span></span>   
7. <span data-ttu-id="9add1-170">Sla uw werk en een tweet met de hashtag #Seattle voor het activeren van de werkstroom wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="9add1-170">Save your work and send a tweet with the #Seattle hashtag to activate your workflow.</span></span>  


## <a name="connector-specific-details"></a><span data-ttu-id="9add1-171">Connector-specifieke details</span><span class="sxs-lookup"><span data-stu-id="9add1-171">Connector-specific details</span></span>

<span data-ttu-id="9add1-172">Alle triggers en acties die zijn gedefinieerd in de swagger bekijken en ziet u ook de beperkingen in de [connector details](/connectors/twitterconnector/).</span><span class="sxs-lookup"><span data-stu-id="9add1-172">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/twitterconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9add1-173">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9add1-173">Next steps</span></span>
[<span data-ttu-id="9add1-174">Een logische app maken</span><span class="sxs-lookup"><span data-stu-id="9add1-174">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

