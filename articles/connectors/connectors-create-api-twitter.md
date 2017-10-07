---
title: aaaLearn hoe toouse Hallo Twitter-connector in logic apps | Microsoft Docs
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
ms.openlocfilehash: ead4e4dc95bf894fd72b908c5375b407ba27642d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-twitter-connector"></a><span data-ttu-id="a2d7f-103">Aan de slag met Hallo Twitter-connector</span><span class="sxs-lookup"><span data-stu-id="a2d7f-103">Get started with hello Twitter connector</span></span>
<span data-ttu-id="a2d7f-104">U kunt met Hallo Twitter-connector:</span><span class="sxs-lookup"><span data-stu-id="a2d7f-104">With hello Twitter connector you can:</span></span>

* <span data-ttu-id="a2d7f-105">Tweets post en get-tweets</span><span class="sxs-lookup"><span data-stu-id="a2d7f-105">Post tweets and get tweets</span></span>
* <span data-ttu-id="a2d7f-106">Pc-gebruikers en toegang tijdlijnen, vrienden</span><span class="sxs-lookup"><span data-stu-id="a2d7f-106">Access timelines, friends and followers</span></span>
* <span data-ttu-id="a2d7f-107">Uitvoeren van Hallo andere acties en de triggers die hieronder wordt beschreven</span><span class="sxs-lookup"><span data-stu-id="a2d7f-107">Perform any of hello other actions and triggers described below</span></span>  

<span data-ttu-id="a2d7f-108">toouse [elke connector](apis-list.md), moet u eerst toocreate een logische app.</span><span class="sxs-lookup"><span data-stu-id="a2d7f-108">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="a2d7f-109">U kunt aan de slag door [maken van een logische app nu](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="a2d7f-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>  

## <a name="connect-tootwitter"></a><span data-ttu-id="a2d7f-110">Verbinding maken met tooTwitter</span><span class="sxs-lookup"><span data-stu-id="a2d7f-110">Connect tooTwitter</span></span>
<span data-ttu-id="a2d7f-111">Om uw logische app toegang alle services tot, moet u eerst toocreate een *verbinding* toohello service.</span><span class="sxs-lookup"><span data-stu-id="a2d7f-111">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="a2d7f-112">Een [verbinding](connectors-overview.md) biedt connectiviteit tussen een logische app en een andere service.</span><span class="sxs-lookup"><span data-stu-id="a2d7f-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-tootwitter"></a><span data-ttu-id="a2d7f-113">Een tooTwitter verbinding maken</span><span class="sxs-lookup"><span data-stu-id="a2d7f-113">Create a connection tooTwitter</span></span>
> [!INCLUDE [Steps toocreate a connection tooTwitter](../../includes/connectors-create-api-twitter.md)]
> 
> 

## <a name="use-a-twitter-trigger"></a><span data-ttu-id="a2d7f-114">Gebruik een trigger Twitter</span><span class="sxs-lookup"><span data-stu-id="a2d7f-114">Use a Twitter trigger</span></span>
<span data-ttu-id="a2d7f-115">Een trigger is een gebeurtenis die gebruikt toostart Hallo werkstroom gedefinieerd in een logische app worden kan.</span><span class="sxs-lookup"><span data-stu-id="a2d7f-115">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="a2d7f-116">[Meer informatie over triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="a2d7f-116">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="a2d7f-117">In dit voorbeeld, leest u hoe toouse hello **wanneer een nieuwe tweet wordt gepost** toosearch voor #Seattle activeren en, als #Seattle wordt gevonden, een bestand in Dropbox bijwerken met de tekst hello uit Hallo tweet.</span><span class="sxs-lookup"><span data-stu-id="a2d7f-117">In this example, I will show you how toouse hello **When a new tweet is posted**  trigger toosearch for #Seattle and, if #Seattle is found, update a file in Dropbox with hello text from hello tweet.</span></span> <span data-ttu-id="a2d7f-118">In een enterprise-voorbeeld, kan u Hallo-naam van uw bedrijf zoeken en een SQL-database bijwerken met de tekst hello van Hallo tweet.</span><span class="sxs-lookup"><span data-stu-id="a2d7f-118">In an enterprise example, you could search for hello name of your company and update a SQL database with hello text from hello tweet.</span></span>

1. <span data-ttu-id="a2d7f-119">Voer *twitter* Selecteer in het zoekvak Hallo op Hallo logic apps designer Hallo **Twitter - wanneer een nieuwe tweet wordt teruggepost** trigger</span><span class="sxs-lookup"><span data-stu-id="a2d7f-119">Enter *twitter* in hello search box on hello logic apps designer then select hello **Twitter - When a new tweet is posted**  trigger</span></span>   
   <span data-ttu-id="a2d7f-120">![Twitter triggerafbeelding 1](./media/connectors-create-api-twitter/trigger-1.png)</span><span class="sxs-lookup"><span data-stu-id="a2d7f-120">![Twitter trigger image 1](./media/connectors-create-api-twitter/trigger-1.png)</span></span>  
2. <span data-ttu-id="a2d7f-121">Voer *#Seattle* in Hallo **zoektekst** besturingselement</span><span class="sxs-lookup"><span data-stu-id="a2d7f-121">Enter *#Seattle* in hello **Search Text** control</span></span>  
   <span data-ttu-id="a2d7f-122">![Afbeelding van de trigger Twitter 2](./media/connectors-create-api-twitter/trigger-2.png)</span><span class="sxs-lookup"><span data-stu-id="a2d7f-122">![Twitter trigger image 2](./media/connectors-create-api-twitter/trigger-2.png)</span></span> 

<span data-ttu-id="a2d7f-123">Op dit moment is uw logische app geconfigureerd met een trigger die een uitvoering van Hallo andere triggers en acties in Hallo-werkstroom begint.</span><span class="sxs-lookup"><span data-stu-id="a2d7f-123">At this point, your logic app has been configured with a trigger that will begin a run of hello other triggers and actions in hello workflow.</span></span> 

> [!NOTE]
> <span data-ttu-id="a2d7f-124">Voor een logische app toobe functionele, moet er ten minste één trigger en één actie bevatten.</span><span class="sxs-lookup"><span data-stu-id="a2d7f-124">For a logic app toobe functional, it must contain at least one trigger and one action.</span></span> <span data-ttu-id="a2d7f-125">Hallo stappen in de volgende sectie tooadd een actie van Hallo.</span><span class="sxs-lookup"><span data-stu-id="a2d7f-125">Follow hello steps in hello next section tooadd an action.</span></span>  
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="a2d7f-126">Een voorwaarde toevoegen</span><span class="sxs-lookup"><span data-stu-id="a2d7f-126">Add a condition</span></span>
<span data-ttu-id="a2d7f-127">Omdat we alleen geïnteresseerd in tweets van gebruikers met meer dan 50 van gebruikers bent, moet een voorwaarde waarmee wordt bevestigd Hallo aantal pc-gebruikers dat eerst worden toegevoegd toohello logische app.</span><span class="sxs-lookup"><span data-stu-id="a2d7f-127">Since we are only interested in tweets from users with more than 50 users, a condition that confirms hello number of followers must first be added toohello logic app.</span></span>  

1. <span data-ttu-id="a2d7f-128">Selecteer **+ een nieuwe stap** tooadd Hallo actie u wilt dat tootake wanneer #Seattle in een nieuwe tweet wordt gevonden</span><span class="sxs-lookup"><span data-stu-id="a2d7f-128">Select **+ New step** tooadd hello action you would like tootake when #Seattle is found in a new tweet</span></span>  
   <span data-ttu-id="a2d7f-129">![Afbeelding 1 Twitter](../../includes/media/connectors-create-api-twitter/action-1.png)</span><span class="sxs-lookup"><span data-stu-id="a2d7f-129">![Twitter action image 1](../../includes/media/connectors-create-api-twitter/action-1.png)</span></span>  
2. <span data-ttu-id="a2d7f-130">Selecteer Hallo **een voorwaarde toevoegen** koppeling.</span><span class="sxs-lookup"><span data-stu-id="a2d7f-130">Select hello **Add a condition** link.</span></span>  
   <span data-ttu-id="a2d7f-131">![Twitter voorwaarde afbeelding 1](../../includes/media/connectors-create-api-twitter/condition-1.png) </span><span class="sxs-lookup"><span data-stu-id="a2d7f-131">![Twitter condition image 1](../../includes/media/connectors-create-api-twitter/condition-1.png) </span></span>  
   <span data-ttu-id="a2d7f-132">Hiermee opent u Hallo **voorwaarde** besturingselement waarin kunt u voorwaarden zoals controleren *gelijk is aan*, *is minder dan*, *is groter dan*, *bevat*, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="a2d7f-132">This opens hello **Condition** control where you can check conditions such as *is equal to*, *is less than*, *is greater than*, *contains*, etc.</span></span>  
   <span data-ttu-id="a2d7f-133">![Afbeelding van de voorwaarde Twitter 2](../../includes/media/connectors-create-api-twitter/condition-2.png)</span><span class="sxs-lookup"><span data-stu-id="a2d7f-133">![Twitter condition image 2](../../includes/media/connectors-create-api-twitter/condition-2.png)</span></span>   
3. <span data-ttu-id="a2d7f-134">Selecteer Hallo **kiest u een waarde** besturingselement.</span><span class="sxs-lookup"><span data-stu-id="a2d7f-134">Select hello **Choose a value** control.</span></span>  
   <span data-ttu-id="a2d7f-135">In dit besturingselement kunt u een of meer van de Hallo eigenschappen van de vorige acties of triggers als Hallo waarde waarvan de voorwaarde geëvalueerd tootrue of ONWAAR is.</span><span class="sxs-lookup"><span data-stu-id="a2d7f-135">In this control, you can select one or more of hello properties from any previous actions or triggers as hello value whose condition will be evaluated tootrue or false.</span></span>
   <span data-ttu-id="a2d7f-136">![Twitter voorwaarde afbeelding 3](../../includes/media/connectors-create-api-twitter/condition-3.png)</span><span class="sxs-lookup"><span data-stu-id="a2d7f-136">![Twitter condition image 3](../../includes/media/connectors-create-api-twitter/condition-3.png)</span></span>   
4. <span data-ttu-id="a2d7f-137">Selecteer Hallo **...**  tooexpand Hallo lijst met eigenschappen zodat u ziet alle Hallo-eigenschappen die beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="a2d7f-137">Select hello **...** tooexpand hello list of properties so you can see all hello properties that are available.</span></span>        
   <span data-ttu-id="a2d7f-138">![Twitter voorwaarde afbeelding 4](../../includes/media/connectors-create-api-twitter/condition-4.png)</span><span class="sxs-lookup"><span data-stu-id="a2d7f-138">![Twitter condition image 4](../../includes/media/connectors-create-api-twitter/condition-4.png)</span></span>   
5. <span data-ttu-id="a2d7f-139">Selecteer Hallo **pc-gebruikers aantal** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="a2d7f-139">Select hello **Followers count** property.</span></span>    
   <span data-ttu-id="a2d7f-140">![Twitter voorwaarde afbeelding 5](../../includes/media/connectors-create-api-twitter/condition-5.png)</span><span class="sxs-lookup"><span data-stu-id="a2d7f-140">![Twitter condition image 5](../../includes/media/connectors-create-api-twitter/condition-5.png)</span></span>   
6. <span data-ttu-id="a2d7f-141">U ziet Hallo pc-gebruikers eigenschap count nu in Hallo waarde besturingselement is.</span><span class="sxs-lookup"><span data-stu-id="a2d7f-141">Notice hello Followers count property is now in hello value control.</span></span>    
   ![Twitter voorwaarde afbeelding 6](../../includes/media/connectors-create-api-twitter/condition-6.png)   
7. <span data-ttu-id="a2d7f-143">Selecteer **is groter dan** uit Hallo operators lijst.</span><span class="sxs-lookup"><span data-stu-id="a2d7f-143">Select **is greater than** from hello operators list.</span></span>    
   <span data-ttu-id="a2d7f-144">![Twitter voorwaarde afbeelding 7](../../includes/media/connectors-create-api-twitter/condition-7.png)</span><span class="sxs-lookup"><span data-stu-id="a2d7f-144">![Twitter condition image 7](../../includes/media/connectors-create-api-twitter/condition-7.png)</span></span>   
8. <span data-ttu-id="a2d7f-145">Voer 50 zoals operand voor Hallo Hallo *is groter dan* operator.</span><span class="sxs-lookup"><span data-stu-id="a2d7f-145">Enter 50 as hello operand for hello *is greater than* operator.</span></span>  
   <span data-ttu-id="a2d7f-146">Hallo-voorwaarde is nu toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="a2d7f-146">hello condition is now added.</span></span> <span data-ttu-id="a2d7f-147">Sla uw werk met Hallo **opslaan** op Hallo menu bovenstaande koppeling.</span><span class="sxs-lookup"><span data-stu-id="a2d7f-147">Save your work using hello **Save** link on hello menu above.</span></span>    
   <span data-ttu-id="a2d7f-148">![Twitter voorwaarde afbeelding 8](../../includes/media/connectors-create-api-twitter/condition-8.png)</span><span class="sxs-lookup"><span data-stu-id="a2d7f-148">![Twitter condition image 8](../../includes/media/connectors-create-api-twitter/condition-8.png)</span></span>   

## <a name="use-a-twitter-action"></a><span data-ttu-id="a2d7f-149">Gebruik een Twitter-actie</span><span class="sxs-lookup"><span data-stu-id="a2d7f-149">Use a Twitter action</span></span>
<span data-ttu-id="a2d7f-150">Een actie is een bewerking uitgevoerd door Hallo werkstroom gedefinieerd in een logische app.</span><span class="sxs-lookup"><span data-stu-id="a2d7f-150">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="a2d7f-151">[Meer informatie over acties](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="a2d7f-151">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="a2d7f-152">Nu u een trigger hebt toegevoegd, volgt u deze stappen tooadd een actie die een nieuwe tweet met inhoud Hallo Hallo tweets gevonden door Hallo trigger wordt geplaatst.</span><span class="sxs-lookup"><span data-stu-id="a2d7f-152">Now that you have added a trigger, follow these steps tooadd an action that will post a new tweet with hello contents of hello tweets found by hello trigger.</span></span> <span data-ttu-id="a2d7f-153">Voor de toepassing hello van deze procedure wordt alleen tweets van gebruikers met meer dan 50 pc-gebruikers worden geplaatst.</span><span class="sxs-lookup"><span data-stu-id="a2d7f-153">For hello purposes of this walk-through only tweets from users with more than 50 followers will be posted.</span></span>  

<span data-ttu-id="a2d7f-154">In de volgende stap hello voegt u een Twitter-actie die een tweet gebruikmakend van Hallo eigenschappen van elke tweet die is geplaatst door een gebruiker die meer dan 50 pc-gebruikers heeft wordt geplaatst.</span><span class="sxs-lookup"><span data-stu-id="a2d7f-154">In hello next step, you will add a Twitter action that will post a tweet using some of hello properties of each tweet that has been posted by a user who has more than 50 followers.</span></span>  

1. <span data-ttu-id="a2d7f-155">Selecteer **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="a2d7f-155">Select **Add an action**.</span></span> <span data-ttu-id="a2d7f-156">Hiermee opent u Hallo zoekbesturing waar u naar andere acties en triggers zoeken kunt.</span><span class="sxs-lookup"><span data-stu-id="a2d7f-156">This opens hello search control where you can search for other actions and triggers.</span></span>  
   <span data-ttu-id="a2d7f-157">![Twitter voorwaarde afbeelding 9](../../includes/media/connectors-create-api-twitter/condition-9.png)</span><span class="sxs-lookup"><span data-stu-id="a2d7f-157">![Twitter condition image 9](../../includes/media/connectors-create-api-twitter/condition-9.png)</span></span>   
2. <span data-ttu-id="a2d7f-158">Voer *twitter* selecteert in het zoekvak Hallo Hallo **Twitter - een tweet boeken** in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="a2d7f-158">Enter *twitter* into hello search box then select hello **Twitter - Post a tweet** action.</span></span> <span data-ttu-id="a2d7f-159">Hiermee opent u Hallo **een tweet boeken** bepalen waar u alle details wordt invoeren voor Hallo tweet wordt geplaatst.</span><span class="sxs-lookup"><span data-stu-id="a2d7f-159">This opens hello **Post a tweet** control where you will enter all details for hello tweet being posted.</span></span>      
   <span data-ttu-id="a2d7f-160">![Actie afbeelding 1-5 Twitter](../../includes/media/connectors-create-api-twitter/action-1-5.png)</span><span class="sxs-lookup"><span data-stu-id="a2d7f-160">![Twitter action image 1-5](../../includes/media/connectors-create-api-twitter/action-1-5.png)</span></span>   
3. <span data-ttu-id="a2d7f-161">Selecteer Hallo **Tweet tekst** besturingselement.</span><span class="sxs-lookup"><span data-stu-id="a2d7f-161">Select hello **Tweet text** control.</span></span> <span data-ttu-id="a2d7f-162">Alle uitvoerwaarden van de vorige acties en triggers in Hallo logische app worden nu weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a2d7f-162">All outputs from previous actions and triggers in hello logic app are now visible.</span></span> <span data-ttu-id="a2d7f-163">U kunt een van deze selecteren en ze als onderdeel van Hallo tweet tekst van de nieuwe tweet hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a2d7f-163">You can select any of these and use them as part of hello tweet text of hello new tweet.</span></span>     
   <span data-ttu-id="a2d7f-164">![Afbeelding 2 Twitter](../../includes/media/connectors-create-api-twitter/action-2.png)</span><span class="sxs-lookup"><span data-stu-id="a2d7f-164">![Twitter action image 2](../../includes/media/connectors-create-api-twitter/action-2.png)</span></span>   
4. <span data-ttu-id="a2d7f-165">Selecteer **gebruikersnaam**</span><span class="sxs-lookup"><span data-stu-id="a2d7f-165">Select **User name**</span></span>   
5. <span data-ttu-id="a2d7f-166">Voer *zegt:* in Hallo tweet tekstbesturingselement.</span><span class="sxs-lookup"><span data-stu-id="a2d7f-166">Enter *says:* in hello tweet text control.</span></span> <span data-ttu-id="a2d7f-167">Doe dit direct na de gebruikersnaam.</span><span class="sxs-lookup"><span data-stu-id="a2d7f-167">Do this just after User name.</span></span>  
6. <span data-ttu-id="a2d7f-168">Selecteer *Tweet tekst*.</span><span class="sxs-lookup"><span data-stu-id="a2d7f-168">Select *Tweet text*.</span></span>       
   <span data-ttu-id="a2d7f-169">![Afbeelding 3 Twitter](../../includes/media/connectors-create-api-twitter/action-3.png)</span><span class="sxs-lookup"><span data-stu-id="a2d7f-169">![Twitter action image 3](../../includes/media/connectors-create-api-twitter/action-3.png)</span></span>   
7. <span data-ttu-id="a2d7f-170">Sla uw werk en verzend een tweet met Hallo #Seattle hashtag tooactivate uw werkstroom.</span><span class="sxs-lookup"><span data-stu-id="a2d7f-170">Save your work and send a tweet with hello #Seattle hashtag tooactivate your workflow.</span></span>  


## <a name="connector-specific-details"></a><span data-ttu-id="a2d7f-171">Connector-specifieke details</span><span class="sxs-lookup"><span data-stu-id="a2d7f-171">Connector-specific details</span></span>

<span data-ttu-id="a2d7f-172">Alle triggers en acties die zijn gedefinieerd in swagger Hallo bekijken en ook bekijken in Hallo beperkingen [connector details](/connectors/twitterconnector/).</span><span class="sxs-lookup"><span data-stu-id="a2d7f-172">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/twitterconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a2d7f-173">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a2d7f-173">Next steps</span></span>
[<span data-ttu-id="a2d7f-174">Een logische app maken</span><span class="sxs-lookup"><span data-stu-id="a2d7f-174">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

