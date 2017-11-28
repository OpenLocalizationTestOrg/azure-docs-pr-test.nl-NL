---
title: Controleprogramma voor gebeurtenissen met Azure Event Hubs instellen voor Azure Logic Apps | Microsoft Docs
description: Gebeurtenissen ontvangen en verzenden van gebeurtenissen voor Azure Logic Apps met Azure Event Hubs-gegevensstromen bewaken
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
ms.openlocfilehash: 2ca27fb8269d1796fb1181fc4d0a8744a592d548
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-receive-and-send-events-with-the-event-hubs-connector"></a><span data-ttu-id="1d833-104">Bewaken, ontvangen en verzenden van gebeurtenissen met de Event Hubs-connector</span><span class="sxs-lookup"><span data-stu-id="1d833-104">Monitor, receive, and send events with the Event Hubs connector</span></span>

<span data-ttu-id="1d833-105">Als u wilt een controleprogramma voor gebeurtenissen zo instellen dat uw logische app kunt detecteren van gebeurtenissen, gebeurtenissen ontvangen en verzenden van gebeurtenissen, verbinding maken met een [Azure Event Hub](https://azure.microsoft.com/services/event-hubs) van uw logische app.</span><span class="sxs-lookup"><span data-stu-id="1d833-105">To set up an event monitor so that your logic app can detect events, receive events, and send events, connect to an [Azure Event Hub](https://azure.microsoft.com/services/event-hubs) from your logic app.</span></span> <span data-ttu-id="1d833-106">Meer informatie over [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="1d833-106">Learn more about [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>

## <a name="requirements"></a><span data-ttu-id="1d833-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1d833-107">Requirements</span></span>

* <span data-ttu-id="1d833-108">Er moeten een [Event Hubs-naamruimte en Event Hub](../event-hubs/event-hubs-create.md) in Azure.</span><span class="sxs-lookup"><span data-stu-id="1d833-108">You have to have an [Event Hubs namespace and Event Hub](../event-hubs/event-hubs-create.md) in Azure.</span></span> <span data-ttu-id="1d833-109">Meer informatie over [het maken van een Event Hubs-naamruimte en Event Hub](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="1d833-109">Learn [how to create an Event Hubs namespace and Event Hub](../event-hubs/event-hubs-create.md).</span></span> 

* <span data-ttu-id="1d833-110">Gebruik [elke connector](https://docs.microsoft.com/azure/connectors/apis-list) in uw logische app, hebt u eerst een logische app maken.</span><span class="sxs-lookup"><span data-stu-id="1d833-110">To use [any connector](https://docs.microsoft.com/azure/connectors/apis-list) in your logic app, you have to create a logic app first.</span></span> <span data-ttu-id="1d833-111">Meer informatie over [het maken van een logische app](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="1d833-111">Learn [how to create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

<a name="permissions-connection-string"></a>
## <a name="check-event-hubs-namespace-permissions-and-find-the-connection-string"></a><span data-ttu-id="1d833-112">Controleer machtigingen voor Event Hubs-naamruimte en de verbindingsreeks vinden</span><span class="sxs-lookup"><span data-stu-id="1d833-112">Check Event Hubs namespace permissions and find the connection string</span></span>

<span data-ttu-id="1d833-113">Voor uw app logica voor toegang tot alle services die u hebt gemaakt een [ *verbinding* ](./connectors-overview.md) tussen uw logische app en de service, als u dat nog niet gedaan hebt.</span><span class="sxs-lookup"><span data-stu-id="1d833-113">For your logic app to access any service, you have to create a [*connection*](./connectors-overview.md) between your logic app and the service, if you haven't already.</span></span> <span data-ttu-id="1d833-114">Deze verbinding toestaat uw logische app te krijgen tot gegevens.</span><span class="sxs-lookup"><span data-stu-id="1d833-114">This connection authorizes your logic app to access data.</span></span>
<span data-ttu-id="1d833-115">Voor uw logische app toegang tot uw Event Hub, hebt u hebben **beheren** machtigingen en de verbindingsreeks voor de naamruimte van uw Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="1d833-115">For your logic app to access your Event Hub, you have to have **Manage** permissions and the connection string for your Event Hubs namespace.</span></span>

<span data-ttu-id="1d833-116">Controleer uw machtigingen en de verbindingsreeks ophalen, als volgt te werk.</span><span class="sxs-lookup"><span data-stu-id="1d833-116">To check your permissions and get the connection string, follow these steps.</span></span>

1.  <span data-ttu-id="1d833-117">Meld u aan bij [Azure Portal](https://portal.azure.com "Azure Portal").</span><span class="sxs-lookup"><span data-stu-id="1d833-117">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span></span> 

2.  <span data-ttu-id="1d833-118">Ga naar de Event Hubs *naamruimte*, niet de specifieke Event Hub.</span><span class="sxs-lookup"><span data-stu-id="1d833-118">Go to your Event Hubs *namespace*, not the specific Event Hub.</span></span> <span data-ttu-id="1d833-119">Op de blade naamruimte onder **instellingen**, kies **gedeeld toegangsbeleid**.</span><span class="sxs-lookup"><span data-stu-id="1d833-119">On the namespace blade, under **Settings**, choose **Shared access policies**.</span></span> <span data-ttu-id="1d833-120">Onder **Claims**, Controleer of u hebt **beheren** machtigingen voor die naamruimte.</span><span class="sxs-lookup"><span data-stu-id="1d833-120">Under **Claims**, check that you have **Manage** permissions for that namespace.</span></span>

    ![Machtigingen voor uw Event Hub-naamruimte beheren](./media/connectors-create-api-azure-event-hubs/event-hubs-namespace.png)

3.  <span data-ttu-id="1d833-122">Als u wilt kopiëren van de verbindingsreeks voor de naamruimte van Event Hubs, kies **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="1d833-122">To copy the connection string for the Event Hubs namespace, choose **RootManageSharedAccessKey**.</span></span> <span data-ttu-id="1d833-123">Naast de primaire sleutel verbindingsreeks, kies de knop kopiëren.</span><span class="sxs-lookup"><span data-stu-id="1d833-123">Next to your primary key connection string, choose the copy button.</span></span>

    ![Kopieer de verbindingsreeks voor Event Hubs-naamruimte](media/connectors-create-api-azure-event-hubs/find-event-hub-namespace-connection-string.png)

    > [!TIP]
    > <span data-ttu-id="1d833-125">Om te controleren of de verbindingsreeks gekoppeld aan de naamruimte van uw Event Hubs of met een specifieke Event Hub is, Controleer de verbindingsreeks voor de `EntityPath` parameter.</span><span class="sxs-lookup"><span data-stu-id="1d833-125">To confirm whether your connection string is associated with your Event Hubs namespace or with a specific Event Hub, check the connection string for the `EntityPath` parameter.</span></span> <span data-ttu-id="1d833-126">Als u deze parameter vinden, de verbindingsreeks is voor een specifieke Event Hub 'entiteit' en is niet de juiste tekenreeks voor gebruik met uw logische app.</span><span class="sxs-lookup"><span data-stu-id="1d833-126">If you find this parameter, the connection string is for a specific Event Hub "entity", and is not the correct string to use with your logic app.</span></span>

4.  <span data-ttu-id="1d833-127">Wanneer u wordt gevraagd om referenties na een trigger voor Event Hubs of actie toe te voegen aan uw logische app, kunt u kunt nu voor verbinding met uw naamruimte Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="1d833-127">Now when you're prompted for credentials after adding an Event Hubs trigger or action to your logic app, you can connect to your Event Hubs namespace.</span></span> <span data-ttu-id="1d833-128">Geef een naam op voor de verbinding, voert u de verbindingsreeks die u hebt gekopieerd en kies **maken**.</span><span class="sxs-lookup"><span data-stu-id="1d833-128">Give your connection a name, enter the connection string that you copied, and choose **Create**.</span></span>

    ![Geef de verbindingsreeks voor Event Hubs-naamruimte](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    <span data-ttu-id="1d833-130">Nadat u uw verbinding maakt, de naam van de verbinding moet worden weergegeven in de Event Hubs trigger of actie.</span><span class="sxs-lookup"><span data-stu-id="1d833-130">After you create your connection, the connection name should appear in the Event Hubs trigger or action.</span></span> 
    <span data-ttu-id="1d833-131">Vervolgens kunt u doorgaan met de overige stappen in uw logische app.</span><span class="sxs-lookup"><span data-stu-id="1d833-131">You can then continue with the other steps in your logic app.</span></span>

    ![Event Hubs naamruimte verbinding is gemaakt](./media/connectors-create-api-azure-event-hubs/event-hubs-connection-created.png)

## <a name="start-workflow-when-your-event-hub-receives-new-events"></a><span data-ttu-id="1d833-133">Werkstroom starten wanneer uw Event Hub nieuwe gebeurtenissen ontvangt</span><span class="sxs-lookup"><span data-stu-id="1d833-133">Start workflow when your Event Hub receives new events</span></span>

<span data-ttu-id="1d833-134">Een [ *trigger* ](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) is een gebeurtenis die een werkstroom in uw logische app start.</span><span class="sxs-lookup"><span data-stu-id="1d833-134">A [*trigger*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) is an event that starts a workflow in your logic app.</span></span> <span data-ttu-id="1d833-135">U start een werkstroom wanneer nieuwe gebeurtenissen worden verzonden naar uw Event Hub, volg deze stappen voor het toevoegen van de trigger die deze gebeurtenis wordt gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="1d833-135">To start a workflow when new events are sent to your Event Hub, follow these steps for adding the trigger that detects this event.</span></span>

1.  <span data-ttu-id="1d833-136">In de [Azure-portal](https://portal.azure.com "Azure-portal"), gaat u naar uw bestaande logische app of een lege logische app maken.</span><span class="sxs-lookup"><span data-stu-id="1d833-136">In the [Azure portal](https://portal.azure.com "Azure portal"), go to your existing logic app or create a blank logic app.</span></span>

2.  <span data-ttu-id="1d833-137">Voer in het zoekvak voor Logic App Designer `event hubs` voor uw filter.</span><span class="sxs-lookup"><span data-stu-id="1d833-137">In the search box for the Logic App Designer, enter `event hubs` for your filter.</span></span> <span data-ttu-id="1d833-138">Selecteer deze trigger: **wanneer gebeurtenissen zijn beschikbaar in de Event Hub**</span><span class="sxs-lookup"><span data-stu-id="1d833-138">Select this trigger: **When events are available in Event Hub**</span></span>

    ![Selecteer de trigger voor wanneer de nieuwe gebeurtenissen voor het ontvangen van uw Event Hub](./media/connectors-create-api-azure-event-hubs/find-event-hubs-trigger.png)

    <span data-ttu-id="1d833-140">Als u nog een verbinding met de naamruimte van uw Event Hubs hebt, wordt u gevraagd om deze verbinding nu te maken.</span><span class="sxs-lookup"><span data-stu-id="1d833-140">If you don't already have a connection to your Event Hubs namespace, you're prompted to create this connection now.</span></span> <span data-ttu-id="1d833-141">Geef een naam op voor uw verbinding en geef de verbindingsreeks voor de naamruimte van uw Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="1d833-141">Give your connection a name, and enter the connection string for your Event Hubs namespace.</span></span> 
    <span data-ttu-id="1d833-142">Indien nodig, meer [het zoeken van de verbindingsreeks](#permissions-connection-string).</span><span class="sxs-lookup"><span data-stu-id="1d833-142">If necessary, learn [how to find your connection string](#permissions-connection-string).</span></span>

    ![Geef de verbindingsreeks voor Event Hubs-naamruimte](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    <span data-ttu-id="1d833-144">Nadat u de verbinding van de instellingen voor de **wanneer een gebeurtenis in beschikbaar zijn in een Event Hub** trigger worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="1d833-144">After you create the connection, the settings for the **When an event in available in an Event Hub** trigger appear.</span></span>

    ![De instellingen van de trigger voor wanneer de nieuwe gebeurtenissen voor het ontvangen van uw Event Hub](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger.png)

3.  <span data-ttu-id="1d833-146">Typ of Selecteer de naam voor de Event Hub die u wilt bewaken.</span><span class="sxs-lookup"><span data-stu-id="1d833-146">Enter or select the name for the Event Hub that you want to monitor.</span></span> <span data-ttu-id="1d833-147">Selecteer de frequentie en het interval voor hoe vaak u wilt controleren van de Event Hub.</span><span class="sxs-lookup"><span data-stu-id="1d833-147">Select the frequency and interval for how often you want to check the Event Hub.</span></span>

    > [!TIP]
    > <span data-ttu-id="1d833-148">Schakel eventueel een consumergroep voor het lezen van gebeurtenissen, kies **geavanceerde opties weergeven**.</span><span class="sxs-lookup"><span data-stu-id="1d833-148">To optionally select a consumer group for reading events, choose **Show advanced options**.</span></span> 

    ![Geef een Event Hub of klantengroep](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger-details.png)

    <span data-ttu-id="1d833-150">U hebt nu een trigger ingesteld geen werkstroom starten voor uw logische app.</span><span class="sxs-lookup"><span data-stu-id="1d833-150">You've now set up a trigger to start a workflow for your logic app.</span></span> 
    <span data-ttu-id="1d833-151">Uw logische app controleert de opgegeven Event Hub op basis van de door u ingesteld schema.</span><span class="sxs-lookup"><span data-stu-id="1d833-151">Your logic app checks the specified Event Hub based on the schedule that you set.</span></span> 
    <span data-ttu-id="1d833-152">Als uw app vindt de nieuwe gebeurtenissen in de Event Hub, de trigger andere acties uitgevoerd of in uw logische app getriggerd.</span><span class="sxs-lookup"><span data-stu-id="1d833-152">If your app finds new events in the Event Hub, the trigger runs other actions or triggers in your logic app.</span></span>

## <a name="send-events-to-your-event-hub-from-your-logic-app"></a><span data-ttu-id="1d833-153">Gebeurtenissen verzenden naar uw Event Hub van uw logische app</span><span class="sxs-lookup"><span data-stu-id="1d833-153">Send events to your Event Hub from your logic app</span></span>

<span data-ttu-id="1d833-154">Een [*actie*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) is een taak die wordt uitgevoerd tijdens de werkstroom voor de logische app.</span><span class="sxs-lookup"><span data-stu-id="1d833-154">An [*action*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) is a task performed by your logic app workflow.</span></span> <span data-ttu-id="1d833-155">Nadat u een trigger hebt toegevoegd aan uw logische app, kunt u een actie toevoegen om bewerkingen uit te voeren op gegevens die met deze trigger worden gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="1d833-155">After you add a trigger to your logic app, you can add an action to perform operations with data generated by that trigger.</span></span> <span data-ttu-id="1d833-156">Volg deze stappen om een gebeurtenis verzenden naar uw Event Hub van uw logische app.</span><span class="sxs-lookup"><span data-stu-id="1d833-156">To send an event to your Event Hub from your logic app, follow these steps.</span></span>

1.  <span data-ttu-id="1d833-157">In Logic App Designer onder uw logische app worden geactiveerd, kies **nieuwe stap** > **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="1d833-157">In Logic App Designer, under your logic app trigger, choose **New step** > **Add an action**.</span></span>

    ![Kies 'Nieuwe stap' vervolgens 'Een actie toevoegen'](./media/connectors-create-api-azure-event-hubs/add-action.png)

    <span data-ttu-id="1d833-159">U kunt nu vinden en selecteer een actie om uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="1d833-159">Now you can find and select an action to perform.</span></span> 
    <span data-ttu-id="1d833-160">Hoewel u geen actie, bijvoorbeeld, willen we de Event Hubs-actie voor het verzenden van gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="1d833-160">Although you can select any action, for this example, we want the Event Hubs action to send events.</span></span>

2.  <span data-ttu-id="1d833-161">Voer in het zoekvak `event hubs` voor uw filter.</span><span class="sxs-lookup"><span data-stu-id="1d833-161">In the search box, enter `event hubs` for your filter.</span></span>
<span data-ttu-id="1d833-162">Deze actie selecteert: **verzendgebeurtenis**</span><span class="sxs-lookup"><span data-stu-id="1d833-162">Select this action: **Send event**</span></span>

    ![Selecteer 'Event Hubs - verzendgebeurtenis' actie](./media/connectors-create-api-azure-event-hubs/find-event-hubs-action.png)

3.  <span data-ttu-id="1d833-164">Voer de vereiste gegevens voor de gebeurtenis, zoals de naam voor de Event Hub waar u de gebeurtenis te verzenden.</span><span class="sxs-lookup"><span data-stu-id="1d833-164">Enter the required details for the event, such as the name for the Event Hub where you want to send the event.</span></span> <span data-ttu-id="1d833-165">Voer een optionele details over de gebeurtenis, zoals inhoud voor die gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="1d833-165">Enter any other optional details about the event, such as content for that event.</span></span>

    > [!TIP]
    > <span data-ttu-id="1d833-166">Als eventueel opgeven waar de gebeurtenis de Event Hub-partitie, kiest u **geavanceerde opties weergeven**.</span><span class="sxs-lookup"><span data-stu-id="1d833-166">To optionally specify the Event Hub partition where to send the event, choose **Show advanced options**.</span></span> 

    ![Event Hub-naam en optionele Gebeurtenisdetails invoeren](./media/connectors-create-api-azure-event-hubs/event-hubs-send-event-action.png)

6.  <span data-ttu-id="1d833-168">Sla uw wijzigingen op.</span><span class="sxs-lookup"><span data-stu-id="1d833-168">Save your changes.</span></span>

    ![Uw logische app opslaan](./media/connectors-create-api-azure-event-hubs/save-logic-app.png)

    <span data-ttu-id="1d833-170">U hebt nu een actie ingesteld voor het verzenden van gebeurtenissen vanuit uw logische app.</span><span class="sxs-lookup"><span data-stu-id="1d833-170">You've now set up an action to send events from your logic app.</span></span> 

## <a name="connector-specific-details"></a><span data-ttu-id="1d833-171">Connector-specifieke details</span><span class="sxs-lookup"><span data-stu-id="1d833-171">Connector-specific details</span></span>

<span data-ttu-id="1d833-172">Alle triggers en acties die zijn gedefinieerd in de swagger bekijken en ziet u ook de beperkingen in de [connector details](/connectors/eventhubs/).</span><span class="sxs-lookup"><span data-stu-id="1d833-172">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/eventhubs/).</span></span> 

## <a name="get-help"></a><span data-ttu-id="1d833-173">Help opvragen</span><span class="sxs-lookup"><span data-stu-id="1d833-173">Get help</span></span>

<span data-ttu-id="1d833-174">Ga naar het [forum voor Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) om vragen te stellen, vragen te beantwoorden en te zien wat andere gebruikers van Azure Logic Apps aan het doen zijn.</span><span class="sxs-lookup"><span data-stu-id="1d833-174">To ask questions, answer questions, and see what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="1d833-175">Ter verbetering van Logic Apps en connectors kunt u stemmen op ideeën of ideeën indienen op de [site voor gebruikersfeedback van Logic Apps](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="1d833-175">To help improve Logic Apps and connectors, vote on or submit ideas at the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1d833-176">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1d833-176">Next steps</span></span>

*  [<span data-ttu-id="1d833-177">Andere connectors voor Azure Logic apps zoeken</span><span class="sxs-lookup"><span data-stu-id="1d833-177">Find other connectors for Azure Logic apps</span></span>](./apis-list.md)