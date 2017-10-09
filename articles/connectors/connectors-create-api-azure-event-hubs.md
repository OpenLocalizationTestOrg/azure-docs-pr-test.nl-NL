---
title: aaaSet up controleprogramma voor gebeurtenissen met Azure Event Hubs voor Azure Logic Apps | Microsoft Docs
description: Gegevensstromen tooreceive gebeurtenissen bewaken en verzenden van gebeurtenissen voor Azure Logic Apps met Azure Event Hubs
services: logic-apps
keywords: gegevensstroom, controleprogramma voor gebeurtenissen van event hubs
author: ecfan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/31/2017
ms.author: estfan; LADocs
ms.openlocfilehash: 4aad2c2ac1134b4d4d440019b4773559e49be122
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-receive-and-send-events-with-hello-event-hubs-connector"></a><span data-ttu-id="66069-104">Bewaken, ontvangen en verzenden van gebeurtenissen met de Hallo Event Hubs-connector</span><span class="sxs-lookup"><span data-stu-id="66069-104">Monitor, receive, and send events with hello Event Hubs connector</span></span>

<span data-ttu-id="66069-105">tooset up controleprogramma voor gebeurtenissen, zodat uw logische app kunt detecteren van gebeurtenissen, gebeurtenissen ontvangen en verzenden van gebeurtenissen, verbinding tooan [Azure Event Hub](https://azure.microsoft.com/services/event-hubs) van uw logische app.</span><span class="sxs-lookup"><span data-stu-id="66069-105">tooset up an event monitor so that your logic app can detect events, receive events, and send events, connect tooan [Azure Event Hub](https://azure.microsoft.com/services/event-hubs) from your logic app.</span></span> <span data-ttu-id="66069-106">Meer informatie over [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="66069-106">Learn more about [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>

## <a name="requirements"></a><span data-ttu-id="66069-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="66069-107">Requirements</span></span>

* <span data-ttu-id="66069-108">U hebt toohave een [Event Hubs-naamruimte en Event Hub](../event-hubs/event-hubs-create.md) in Azure.</span><span class="sxs-lookup"><span data-stu-id="66069-108">You have toohave an [Event Hubs namespace and Event Hub](../event-hubs/event-hubs-create.md) in Azure.</span></span> <span data-ttu-id="66069-109">Meer informatie over [hoe toocreate een Event Hubs-naamruimte en Event Hub](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="66069-109">Learn [how toocreate an Event Hubs namespace and Event Hub](../event-hubs/event-hubs-create.md).</span></span> 

* <span data-ttu-id="66069-110">toouse [elke connector](https://docs.microsoft.com/azure/connectors/apis-list) in uw logische app, hebt u toocreate een logische app eerst.</span><span class="sxs-lookup"><span data-stu-id="66069-110">toouse [any connector](https://docs.microsoft.com/azure/connectors/apis-list) in your logic app, you have toocreate a logic app first.</span></span> <span data-ttu-id="66069-111">Meer informatie over [hoe toocreate een logische app](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="66069-111">Learn [how toocreate a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

<a name="permissions-connection-string"></a>
## <a name="check-event-hubs-namespace-permissions-and-find-hello-connection-string"></a><span data-ttu-id="66069-112">Controleer machtigingen voor Event Hubs-naamruimte en Hallo verbindingsreeks vinden</span><span class="sxs-lookup"><span data-stu-id="66069-112">Check Event Hubs namespace permissions and find hello connection string</span></span>

<span data-ttu-id="66069-113">Een service voor uw logische app tooaccess, hebt u toocreate een [ *verbinding* ](./connectors-overview.md) tussen uw logische app en Hallo service, als u dat nog niet gedaan hebt.</span><span class="sxs-lookup"><span data-stu-id="66069-113">For your logic app tooaccess any service, you have toocreate a [*connection*](./connectors-overview.md) between your logic app and hello service, if you haven't already.</span></span> <span data-ttu-id="66069-114">Deze verbinding toestaat uw logische app tooaccess-gegevens.</span><span class="sxs-lookup"><span data-stu-id="66069-114">This connection authorizes your logic app tooaccess data.</span></span>
<span data-ttu-id="66069-115">Voor uw logische app tooaccess uw Event Hub, hebt u toohave **beheren** machtigingen en Hallo-verbindingsreeks voor de naamruimte van uw Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="66069-115">For your logic app tooaccess your Event Hub, you have toohave **Manage** permissions and hello connection string for your Event Hubs namespace.</span></span>

<span data-ttu-id="66069-116">toocheck uw machtigingen en de verbindingsreeks voor get hello, als volgt te werk.</span><span class="sxs-lookup"><span data-stu-id="66069-116">toocheck your permissions and get hello connection string, follow these steps.</span></span>

1.  <span data-ttu-id="66069-117">Meld u aan toohello [Azure-portal](https://portal.azure.com "Azure-portal").</span><span class="sxs-lookup"><span data-stu-id="66069-117">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span> 

2.  <span data-ttu-id="66069-118">Ga tooyour Event Hubs *naamruimte*, niet Hallo specifieke Event Hub.</span><span class="sxs-lookup"><span data-stu-id="66069-118">Go tooyour Event Hubs *namespace*, not hello specific Event Hub.</span></span> <span data-ttu-id="66069-119">Op Hallo naamruimte blade onder **instellingen**, kies **gedeeld toegangsbeleid**.</span><span class="sxs-lookup"><span data-stu-id="66069-119">On hello namespace blade, under **Settings**, choose **Shared access policies**.</span></span> <span data-ttu-id="66069-120">Onder **Claims**, Controleer of u hebt **beheren** machtigingen voor die naamruimte.</span><span class="sxs-lookup"><span data-stu-id="66069-120">Under **Claims**, check that you have **Manage** permissions for that namespace.</span></span>

    ![Machtigingen voor uw Event Hub-naamruimte beheren](./media/connectors-create-api-azure-event-hubs/event-hubs-namespace.png)

3.  <span data-ttu-id="66069-122">toocopy Hallo-verbindingsreeks voor de naamruimte van de Event Hubs hello, kies **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="66069-122">toocopy hello connection string for hello Event Hubs namespace, choose **RootManageSharedAccessKey**.</span></span> <span data-ttu-id="66069-123">Volgende tooyour primaire sleutel van de verbindingsreeks, kiest u de knop kopiëren Hallo.</span><span class="sxs-lookup"><span data-stu-id="66069-123">Next tooyour primary key connection string, choose hello copy button.</span></span>

    ![Kopieer de verbindingsreeks voor Event Hubs-naamruimte](media/connectors-create-api-azure-event-hubs/find-event-hub-namespace-connection-string.png)

    > [!TIP]
    > <span data-ttu-id="66069-125">tooconfirm of de verbindingsreeks is gekoppeld aan de naamruimte van uw Event Hubs of met een specifieke Event Hub, Controleer de verbindingsreeks Hallo voor Hallo `EntityPath` parameter.</span><span class="sxs-lookup"><span data-stu-id="66069-125">tooconfirm whether your connection string is associated with your Event Hubs namespace or with a specific Event Hub, check hello connection string for hello `EntityPath` parameter.</span></span> <span data-ttu-id="66069-126">Als u deze parameter vinden, Hallo-verbindingsreeks is voor een specifieke Event Hub 'entiteit' en is geen Hallo juiste tekenreeks toouse met uw logische app.</span><span class="sxs-lookup"><span data-stu-id="66069-126">If you find this parameter, hello connection string is for a specific Event Hub "entity", and is not hello correct string toouse with your logic app.</span></span>

4.  <span data-ttu-id="66069-127">Wanneer u wordt gevraagd om referenties na het toevoegen van een Event Hubs trigger of actie tooyour logische app, kunt u nu tooyour Event Hubs naamruimte verbinding.</span><span class="sxs-lookup"><span data-stu-id="66069-127">Now when you're prompted for credentials after adding an Event Hubs trigger or action tooyour logic app, you can connect tooyour Event Hubs namespace.</span></span> <span data-ttu-id="66069-128">Geef een naam op voor de verbinding, voert u Hallo verbindingsreeks die u hebt gekopieerd en kies **maken**.</span><span class="sxs-lookup"><span data-stu-id="66069-128">Give your connection a name, enter hello connection string that you copied, and choose **Create**.</span></span>

    ![Geef de verbindingsreeks voor Event Hubs-naamruimte](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    <span data-ttu-id="66069-130">Nadat u uw verbinding maakt, wordt in Hallo Event Hubs trigger of actie Hallo verbindingsnaam weergegeven.</span><span class="sxs-lookup"><span data-stu-id="66069-130">After you create your connection, hello connection name should appear in hello Event Hubs trigger or action.</span></span> 
    <span data-ttu-id="66069-131">Vervolgens kunt u doorgaan met de overige stappen in uw logische app Hallo.</span><span class="sxs-lookup"><span data-stu-id="66069-131">You can then continue with hello other steps in your logic app.</span></span>

    ![Event Hubs naamruimte verbinding is gemaakt](./media/connectors-create-api-azure-event-hubs/event-hubs-connection-created.png)

## <a name="start-workflow-when-your-event-hub-receives-new-events"></a><span data-ttu-id="66069-133">Werkstroom starten wanneer uw Event Hub nieuwe gebeurtenissen ontvangt</span><span class="sxs-lookup"><span data-stu-id="66069-133">Start workflow when your Event Hub receives new events</span></span>

<span data-ttu-id="66069-134">Een [ *trigger* ](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) is een gebeurtenis die een werkstroom in uw logische app start.</span><span class="sxs-lookup"><span data-stu-id="66069-134">A [*trigger*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) is an event that starts a workflow in your logic app.</span></span> <span data-ttu-id="66069-135">Volg deze stappen voor het Hallo-trigger die deze gebeurtenis detecteert toevoegen voor het starten van een werkstroom wanneer nieuwe gebeurtenissen tooyour Event Hub worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="66069-135">To start a workflow when new events are sent tooyour Event Hub, follow these steps for adding hello trigger that detects this event.</span></span>

1.  <span data-ttu-id="66069-136">In Hallo [Azure-portal](https://portal.azure.com "Azure-portal"), gaat u het bestaande logische app tooyour of een lege logische app maken.</span><span class="sxs-lookup"><span data-stu-id="66069-136">In hello [Azure portal](https://portal.azure.com "Azure portal"), go tooyour existing logic app or create a blank logic app.</span></span>

2.  <span data-ttu-id="66069-137">Voer in het zoekvak voor Hallo Logic App-ontwerper Hallo `event hubs` voor uw filter.</span><span class="sxs-lookup"><span data-stu-id="66069-137">In hello search box for hello Logic App Designer, enter `event hubs` for your filter.</span></span> <span data-ttu-id="66069-138">Selecteer deze trigger: **wanneer gebeurtenissen zijn beschikbaar in de Event Hub**</span><span class="sxs-lookup"><span data-stu-id="66069-138">Select this trigger: **When events are available in Event Hub**</span></span>

    ![Selecteer de trigger voor wanneer de nieuwe gebeurtenissen voor het ontvangen van uw Event Hub](./media/connectors-create-api-azure-event-hubs/find-event-hubs-trigger.png)

    <span data-ttu-id="66069-140">Als u nog een verbinding tooyour Event Hubs-naamruimte hebt, wordt u gevraagd toocreate nu deze verbinding.</span><span class="sxs-lookup"><span data-stu-id="66069-140">If you don't already have a connection tooyour Event Hubs namespace, you're prompted toocreate this connection now.</span></span> <span data-ttu-id="66069-141">Geef een naam op voor uw verbinding en Voer Hallo-verbindingsreeks voor de naamruimte van uw Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="66069-141">Give your connection a name, and enter hello connection string for your Event Hubs namespace.</span></span> 
    <span data-ttu-id="66069-142">Indien nodig, meer [hoe toofind de verbindingsreeks](#permissions-connection-string).</span><span class="sxs-lookup"><span data-stu-id="66069-142">If necessary, learn [how toofind your connection string](#permissions-connection-string).</span></span>

    ![Geef de verbindingsreeks voor Event Hubs-naamruimte](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    <span data-ttu-id="66069-144">Nadat u Hallo verbinding maakt, instellingen voor Hallo Hallo **wanneer een gebeurtenis in beschikbaar zijn in een Event Hub** trigger worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="66069-144">After you create hello connection, hello settings for hello **When an event in available in an Event Hub** trigger appear.</span></span>

    ![De instellingen van de trigger voor wanneer de nieuwe gebeurtenissen voor het ontvangen van uw Event Hub](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger.png)

3.  <span data-ttu-id="66069-146">Typ of Selecteer de naam Hallo voor Hallo Event Hub die u toomonitor wilt.</span><span class="sxs-lookup"><span data-stu-id="66069-146">Enter or select hello name for hello Event Hub that you want toomonitor.</span></span> <span data-ttu-id="66069-147">Selecteer Hallo frequentie en het interval voor hoe vaak toocheck Hallo Event Hub.</span><span class="sxs-lookup"><span data-stu-id="66069-147">Select hello frequency and interval for how often you want toocheck hello Event Hub.</span></span>

    > [!TIP]
    > <span data-ttu-id="66069-148">toooptionally een consumergroep selecteert voor het lezen van gebeurtenissen, kiest u **geavanceerde opties weergeven**.</span><span class="sxs-lookup"><span data-stu-id="66069-148">toooptionally select a consumer group for reading events, choose **Show advanced options**.</span></span> 

    ![Geef een Event Hub of klantengroep](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger-details.png)

    <span data-ttu-id="66069-150">U hebt nu ingesteld een trigger toostart een werkstroom voor uw logische app.</span><span class="sxs-lookup"><span data-stu-id="66069-150">You've now set up a trigger toostart a workflow for your logic app.</span></span> 
    <span data-ttu-id="66069-151">Uw logische app controleert Hallo opgegeven Event Hub, op basis van Hallo door u ingesteld schema.</span><span class="sxs-lookup"><span data-stu-id="66069-151">Your logic app checks hello specified Event Hub based on hello schedule that you set.</span></span> 
    <span data-ttu-id="66069-152">Als uw app vindt de nieuwe gebeurtenissen in Hallo Event Hub, voert Hallo trigger andere acties of triggers op uw logische app.</span><span class="sxs-lookup"><span data-stu-id="66069-152">If your app finds new events in hello Event Hub, hello trigger runs other actions or triggers in your logic app.</span></span>

## <a name="send-events-tooyour-event-hub-from-your-logic-app"></a><span data-ttu-id="66069-153">Gebeurtenissen tooyour Event Hub van uw logische app verzenden</span><span class="sxs-lookup"><span data-stu-id="66069-153">Send events tooyour Event Hub from your logic app</span></span>

<span data-ttu-id="66069-154">Een [*actie*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) is een taak die wordt uitgevoerd tijdens de werkstroom voor de logische app.</span><span class="sxs-lookup"><span data-stu-id="66069-154">An [*action*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) is a task performed by your logic app workflow.</span></span> <span data-ttu-id="66069-155">Nadat u een trigger tooyour logische app hebt toegevoegd, kunt u een actie tooperform bewerkingen kunt toevoegen met gegevens die zijn gegenereerd door deze trigger.</span><span class="sxs-lookup"><span data-stu-id="66069-155">After you add a trigger tooyour logic app, you can add an action tooperform operations with data generated by that trigger.</span></span> <span data-ttu-id="66069-156">toosend een gebeurtenis tooyour Event Hub van uw logische app, volg deze stappen.</span><span class="sxs-lookup"><span data-stu-id="66069-156">toosend an event tooyour Event Hub from your logic app, follow these steps.</span></span>

1.  <span data-ttu-id="66069-157">In Logic App Designer onder uw logische app worden geactiveerd, kies **nieuwe stap** > **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="66069-157">In Logic App Designer, under your logic app trigger, choose **New step** > **Add an action**.</span></span>

    ![Kies 'Nieuwe stap' vervolgens 'Een actie toevoegen'](./media/connectors-create-api-azure-event-hubs/add-action.png)

    <span data-ttu-id="66069-159">U kunt nu Zoek en selecteer een actie tooperform.</span><span class="sxs-lookup"><span data-stu-id="66069-159">Now you can find and select an action tooperform.</span></span> 
    <span data-ttu-id="66069-160">Hoewel u geen actie, bijvoorbeeld, willen we Hallo Event Hubs actie toosend gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="66069-160">Although you can select any action, for this example, we want hello Event Hubs action toosend events.</span></span>

2.  <span data-ttu-id="66069-161">Voer in het zoekvak Hallo `event hubs` voor uw filter.</span><span class="sxs-lookup"><span data-stu-id="66069-161">In hello search box, enter `event hubs` for your filter.</span></span>
<span data-ttu-id="66069-162">Deze actie selecteert: **verzendgebeurtenis**</span><span class="sxs-lookup"><span data-stu-id="66069-162">Select this action: **Send event**</span></span>

    ![Selecteer 'Event Hubs - verzendgebeurtenis' actie](./media/connectors-create-api-azure-event-hubs/find-event-hubs-action.png)

3.  <span data-ttu-id="66069-164">Voer Hallo vereist voor Hallo gebeurtenis, zoals de naam van de Hallo voor Hallo Event Hub waar u toosend Hallo gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="66069-164">Enter hello required details for hello event, such as hello name for hello Event Hub where you want toosend hello event.</span></span> <span data-ttu-id="66069-165">Voer een optionele details over Hallo gebeurtenis, zoals inhoud voor die gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="66069-165">Enter any other optional details about hello event, such as content for that event.</span></span>

    > [!TIP]
    > <span data-ttu-id="66069-166">toooptionally opgeven Hallo Event Hub-partitie waar toosend Hallo gebeurtenis, kies **geavanceerde opties weergeven**.</span><span class="sxs-lookup"><span data-stu-id="66069-166">toooptionally specify hello Event Hub partition where toosend hello event, choose **Show advanced options**.</span></span> 

    ![Event Hub-naam en optionele Gebeurtenisdetails invoeren](./media/connectors-create-api-azure-event-hubs/event-hubs-send-event-action.png)

6.  <span data-ttu-id="66069-168">Sla uw wijzigingen op.</span><span class="sxs-lookup"><span data-stu-id="66069-168">Save your changes.</span></span>

    ![Uw logische app opslaan](./media/connectors-create-api-azure-event-hubs/save-logic-app.png)

    <span data-ttu-id="66069-170">U hebt nu een actie toosend gebeurtenissen instellen van uw logische app.</span><span class="sxs-lookup"><span data-stu-id="66069-170">You've now set up an action toosend events from your logic app.</span></span> 

## <a name="connector-specific-details"></a><span data-ttu-id="66069-171">Connector-specifieke details</span><span class="sxs-lookup"><span data-stu-id="66069-171">Connector-specific details</span></span>

<span data-ttu-id="66069-172">Alle triggers en acties die zijn gedefinieerd in swagger Hallo bekijken en ook bekijken in Hallo beperkingen [connector details](/connectors/eventhubs/).</span><span class="sxs-lookup"><span data-stu-id="66069-172">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/eventhubs/).</span></span> 

## <a name="get-help"></a><span data-ttu-id="66069-173">Help opvragen</span><span class="sxs-lookup"><span data-stu-id="66069-173">Get help</span></span>

<span data-ttu-id="66069-174">tooask vragen, antwoorden op vragen, en zien welke andere Azure Logic Apps-gebruikers doen, gaat u naar Hallo [Azure Logic Apps-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="66069-174">tooask questions, answer questions, and see what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="66069-175">toohelp Logic Apps en connectors verbeteren, stem of ideeën op Hallo indienen [Logic Apps gebruiker feedback site](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="66069-175">toohelp improve Logic Apps and connectors, vote on or submit ideas at hello [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="66069-176">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="66069-176">Next steps</span></span>

*  [<span data-ttu-id="66069-177">Andere connectors voor Azure Logic apps zoeken</span><span class="sxs-lookup"><span data-stu-id="66069-177">Find other connectors for Azure Logic apps</span></span>](./apis-list.md)