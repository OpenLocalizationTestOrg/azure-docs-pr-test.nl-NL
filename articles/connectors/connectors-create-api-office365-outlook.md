---
title: aaaAdd hello Outlook van Office 365-connector in uw logische Apps | Microsoft Docs
description: 'Logische apps maken met Office 365-connector tooenable interactie met Office 365. Bijvoorbeeld: maken, bewerken en bijwerken van contactpersonen en agenda-items.'
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b2f6cc2c-bba2-493a-b0ba-841785462a80
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 86a573c9c54701de3d3f0500d19eaf545e0710ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-office-365-outlook-connector"></a><span data-ttu-id="eb9dc-104">Aan de slag met Hallo Outlook van Office 365-connector</span><span class="sxs-lookup"><span data-stu-id="eb9dc-104">Get started with hello Office 365 Outlook connector</span></span>
<span data-ttu-id="eb9dc-105">Hallo Outlook van Office 365-connector kan interactie met Outlook in Office 365.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-105">hello Office 365 Outlook connector enables interaction with Outlook in Office 365.</span></span> <span data-ttu-id="eb9dc-106">Gebruik deze connector toocreate, bewerken, en update contactpersonen en agenda-items, en ook ophalen, verzenden en antwoorden tooemail.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-106">Use this connector toocreate, edit, and update contacts and calendar items, and also get, send, and reply tooemail.</span></span>

<span data-ttu-id="eb9dc-107">Met Office 365 Outlook u:</span><span class="sxs-lookup"><span data-stu-id="eb9dc-107">With Office 365 Outlook, you:</span></span>

* <span data-ttu-id="eb9dc-108">Bouw uw werkstroom met behulp van Hallo e-mail en agenda-functies in Office 365.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-108">Build your workflow using hello email and calendar features within Office 365.</span></span> 
* <span data-ttu-id="eb9dc-109">Gebruik activeert toostart uw werkstroom wanneer er een nieuw e-mailadres, wanneer een agenda-item wordt bijgewerkt en meer.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-109">Use triggers toostart your workflow when there is a new email, when a calendar item is updated, and more.</span></span>
* <span data-ttu-id="eb9dc-110">Acties toosend een e-mailbericht gebruikmaken, maakt u een nieuwe gebeurtenis en meer.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-110">Use actions toosend an email, create a new calendar event, and more.</span></span> <span data-ttu-id="eb9dc-111">Bijvoorbeeld, wanneer er een nieuw object in Salesforce (een trigger), een e-mail sturen tooyour Outlook van Office 365 (een actie).</span><span class="sxs-lookup"><span data-stu-id="eb9dc-111">For example, when there is a new object in Salesforce (a trigger), send an email tooyour Office 365 Outlook (an action).</span></span> 

<span data-ttu-id="eb9dc-112">Dit onderwerp leest u hoe toouse Outlook van Office 365-connector in een logische app Hallo en ook een lijst met Hallo triggers en acties.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-112">This topic shows you how toouse hello Office 365 Outlook connector in a logic app, and also lists hello triggers and actions.</span></span>

> [!NOTE]
> <span data-ttu-id="eb9dc-113">Deze versie van Hallo artikel geldt tooLogic Apps algemene beschikbaarheid (GA).</span><span class="sxs-lookup"><span data-stu-id="eb9dc-113">This version of hello article applies tooLogic Apps general availability (GA).</span></span>
> 
> 

<span data-ttu-id="eb9dc-114">toolearn meer informatie over Logic Apps, Zie [wat zijn logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) en [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="eb9dc-114">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toooffice-365"></a><span data-ttu-id="eb9dc-115">Verbinding maken met tooOffice 365</span><span class="sxs-lookup"><span data-stu-id="eb9dc-115">Connect tooOffice 365</span></span>
<span data-ttu-id="eb9dc-116">Om uw logische app toegang alle services tot, maakt u eerst een *verbinding* toohello service.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-116">Before your logic app can access any service, you first create a *connection* toohello service.</span></span> <span data-ttu-id="eb9dc-117">Een verbinding biedt connectiviteit tussen een logische app en een andere service.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-117">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="eb9dc-118">Bijvoorbeeld: tooconnect tooOffice 365 Outlook, moet u eerst een Office 365 *verbinding*.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-118">For example, tooconnect tooOffice 365 Outlook, you first need an Office 365 *connection*.</span></span> <span data-ttu-id="eb9dc-119">een verbinding toocreate Geef referenties op Hallo u normaal gesproken tooaccess Hallo service tooconnect te gewenste gebruiken.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-119">toocreate a connection, enter hello credentials you normally use tooaccess hello service you wish tooconnect to.</span></span> <span data-ttu-id="eb9dc-120">Voer dus Hallo referenties tooyour Office 365-account toocreate Hallo verbinding met Office 365 Outlook.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-120">So with Office 365 Outlook, enter hello credentials tooyour Office 365 account toocreate hello connection.</span></span>

## <a name="create-hello-connection"></a><span data-ttu-id="eb9dc-121">Hallo verbinding maken</span><span class="sxs-lookup"><span data-stu-id="eb9dc-121">Create hello connection</span></span>
> [!INCLUDE [Steps toocreate a connection tooOffice 365](../../includes/connectors-create-api-office365-outlook.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="eb9dc-122">Een trigger te gebruiken</span><span class="sxs-lookup"><span data-stu-id="eb9dc-122">Use a trigger</span></span>
<span data-ttu-id="eb9dc-123">Een trigger is een gebeurtenis die gebruikt toostart Hallo werkstroom gedefinieerd in een logische app worden kan.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-123">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="eb9dc-124">Triggers pollen' ' Hallo-service op het interval en de gewenste frequentie.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-124">Triggers "poll" hello service at an interval and frequency that you want.</span></span> <span data-ttu-id="eb9dc-125">[Meer informatie over triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="eb9dc-125">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="eb9dc-126">Typ 'office 365' tooget een lijst met Hallo triggers in Hallo logic app:</span><span class="sxs-lookup"><span data-stu-id="eb9dc-126">In hello logic app, type "office 365" tooget a list of hello triggers:</span></span>  
   
    ![](./media/connectors-create-api-office365-outlook/office365-trigger.png)
2. <span data-ttu-id="eb9dc-127">Selecteer **Office 365 Outlook - bij het snel starten van een aanstaande gebeurtenis**.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-127">Select **Office 365 Outlook - When an upcoming event is starting soon**.</span></span> <span data-ttu-id="eb9dc-128">Als er al een verbinding bestaat, selecteert u een kalender uit de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-128">If a connection already exists, then select a calendar from hello drop-down list.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/sample-calendar.png)
   
    <span data-ttu-id="eb9dc-129">Als u na vragen aan gebruiker toosign in, voert u Hallo aanmelding in details toocreate Hallo verbinding.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-129">If you are prompted toosign in, then enter hello sign in details toocreate hello connection.</span></span> <span data-ttu-id="eb9dc-130">[Hallo verbinding maken](connectors-create-api-office365-outlook.md#create-the-connection) in dit onderwerp vindt u Hallo stappen.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-130">[Create hello connection](connectors-create-api-office365-outlook.md#create-the-connection) in this topic lists hello steps.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="eb9dc-131">In dit voorbeeld wordt Hallo logische app uitgevoerd wanneer een gebeurtenis wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-131">In this example, hello logic app runs when a calendar event is updated.</span></span> <span data-ttu-id="eb9dc-132">toosee hello resultaten van deze trigger toevoegen nog een actie die u een SMS-bericht verzonden.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-132">toosee hello results of this trigger, add another action that sends you a text message.</span></span> <span data-ttu-id="eb9dc-133">Bijvoorbeeld, voeg Hallo Twilio *bericht verzenden* actie die de tekst die u als hello agenda-gebeurtenis wordt gestart binnen 15 minuten.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-133">For example, add hello Twilio *Send message* action that texts you when hello calendar event is starting in 15 minutes.</span></span> 
   > 
   > 
3. <span data-ttu-id="eb9dc-134">Selecteer Hallo **bewerken** knop en stel Hallo **frequentie** en **Interval** waarden.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-134">Select hello **Edit** button and set hello **Frequency** and **Interval** values.</span></span> <span data-ttu-id="eb9dc-135">Bijvoorbeeld, als u wilt dat Hallo trigger toopoll om de 15 minuten, wordt ingesteld Hallo **frequentie** te**minuut**, en set Hallo **Interval** te**15**.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-135">For example, if you want hello trigger toopoll every 15 minutes, then set hello **Frequency** too**Minute**, and set hello **Interval** too**15**.</span></span> 
   
    ![](./media/connectors-create-api-office365-outlook/calendar-settings.png)
4. <span data-ttu-id="eb9dc-136">**Sla** uw wijzigingen (linksboven Hallo werkbalk).</span><span class="sxs-lookup"><span data-stu-id="eb9dc-136">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="eb9dc-137">Uw logische app wordt opgeslagen en automatisch kan worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-137">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="eb9dc-138">Gebruik een actie</span><span class="sxs-lookup"><span data-stu-id="eb9dc-138">Use an action</span></span>
<span data-ttu-id="eb9dc-139">Een actie is een bewerking uitgevoerd door Hallo werkstroom gedefinieerd in een logische app.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-139">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="eb9dc-140">[Meer informatie over acties](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="eb9dc-140">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="eb9dc-141">Selecteer Hallo plus -teken.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-141">Select hello plus sign.</span></span> <span data-ttu-id="eb9dc-142">Ziet u verschillende mogelijkheden: **een actie toevoegen**, **een voorwaarde toevoegen**, of een van de Hallo **meer** opties.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-142">You see several choices: **Add an action**, **Add a condition**, or one of hello **More** options.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/add-action.png)
2. <span data-ttu-id="eb9dc-143">Kies **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-143">Choose **Add an action**.</span></span>
3. <span data-ttu-id="eb9dc-144">Typ in het tekstvak hello, 'office 365' tooget een lijst met alle beschikbare Hallo-acties.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-144">In hello text box, type “office 365” tooget a list of all hello available actions.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/office365-actions.png) 
4. <span data-ttu-id="eb9dc-145">Kies in ons voorbeeld **Outlook van Office 365 - maken contact op met**.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-145">In our example, choose **Office 365 Outlook - Create contact**.</span></span> <span data-ttu-id="eb9dc-146">Als er al een verbinding bestaat, kiest u Hallo **map-ID**, **voornaam**, en andere eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="eb9dc-146">If a connection already exists, then choose hello **Folder ID**, **Given Name**, and other properties:</span></span>  
   
    ![](./media/connectors-create-api-office365-outlook/office365-sampleaction.png)
   
    <span data-ttu-id="eb9dc-147">Als u wordt gevraagd om de verbindingsgegevens hello, voert u Hallo details toocreate Hallo verbinding.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-147">If you are prompted for hello connection information, then enter hello details toocreate hello connection.</span></span> <span data-ttu-id="eb9dc-148">[Hallo verbinding maken](connectors-create-api-office365-outlook.md#create-the-connection) in dit onderwerp beschrijft deze eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-148">[Create hello connection](connectors-create-api-office365-outlook.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="eb9dc-149">In dit voorbeeld maken we een nieuwe contactpersoon in Outlook van Office 365.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-149">In this example, we create a new contact in Office 365 Outlook.</span></span> <span data-ttu-id="eb9dc-150">U kunt de uitvoer van een andere trigger toocreate Hallo contactpersoon.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-150">You can use output from another trigger toocreate hello contact.</span></span> <span data-ttu-id="eb9dc-151">Bijvoorbeeld, voeg Hallo SalesForce *wanneer een object wordt gemaakt* trigger.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-151">For example, add hello SalesForce *When an object is created* trigger.</span></span> <span data-ttu-id="eb9dc-152">Voeg vervolgens Hallo Outlook van Office 365 *maken contact op met* actie die gebruikmaakt van Hallo SalesForce velden toocreate Hallo nieuwe nieuwe contactpersoon in Office 365.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-152">Then add hello Office 365 Outlook *Create contact* action that uses hello SalesForce fields toocreate hello new new contact in Office 365.</span></span> 
   > 
   > 
5. <span data-ttu-id="eb9dc-153">**Sla** uw wijzigingen (linksboven Hallo werkbalk).</span><span class="sxs-lookup"><span data-stu-id="eb9dc-153">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="eb9dc-154">Uw logische app wordt opgeslagen en automatisch kan worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-154">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="eb9dc-155">Connector-specifieke details</span><span class="sxs-lookup"><span data-stu-id="eb9dc-155">Connector-specific details</span></span>

<span data-ttu-id="eb9dc-156">Alle triggers en acties die zijn gedefinieerd in swagger Hallo bekijken en ook bekijken in Hallo beperkingen [connector details](/connectors/office365connector/).</span><span class="sxs-lookup"><span data-stu-id="eb9dc-156">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/office365connector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="eb9dc-157">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="eb9dc-157">Next Steps</span></span>
<span data-ttu-id="eb9dc-158">[Een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="eb9dc-158">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="eb9dc-159">Verken Hallo van andere beschikbare connectors in Logic Apps op onze [API's lijst](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="eb9dc-159">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

