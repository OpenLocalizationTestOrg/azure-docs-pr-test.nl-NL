---
title: De OneDrive-connector in uw logische Apps toevoegen | Microsoft Docs
description: Overzicht van de connector OneDrive met parameters van de REST-API
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 47a8582a-1b1a-4fc3-beb5-97c60c4306fe
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 63bd33bf4e09b98aa53dcfec9fcc4a0109204952
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-onedrive-connector"></a><span data-ttu-id="b8260-103">Aan de slag met de OneDrive-connector</span><span class="sxs-lookup"><span data-stu-id="b8260-103">Get started with the OneDrive connector</span></span>
<span data-ttu-id="b8260-104">Verbinding maken met OneDrive voor het beheren van de bestanden, waaronder het uploaden, ophalen en verwijderen van bestanden en meer.</span><span class="sxs-lookup"><span data-stu-id="b8260-104">Connect to OneDrive to manage your files, including upload, get, delete files, and more.</span></span> 

<span data-ttu-id="b8260-105">Met OneDrive, u:</span><span class="sxs-lookup"><span data-stu-id="b8260-105">With OneDrive, you:</span></span> 

* <span data-ttu-id="b8260-106">Het bouwen van uw werkstroom door het opslaan van bestanden in OneDrive of bijwerken van bestaande bestanden in OneDrive.</span><span class="sxs-lookup"><span data-stu-id="b8260-106">Build your workflow by storing files in OneDrive, or update existing files in OneDrive.</span></span> 
* <span data-ttu-id="b8260-107">Met triggers kunt u uw werkstroom te starten wanneer een bestand wordt gemaakt of binnen uw OneDrive bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="b8260-107">Use triggers to start your workflow when a file is created or updated within your OneDrive.</span></span>
* <span data-ttu-id="b8260-108">Acties gebruiken om te maken van een bestand, verwijderen van een bestand en meer.</span><span class="sxs-lookup"><span data-stu-id="b8260-108">Use actions to create a file, delete a file, and more.</span></span> <span data-ttu-id="b8260-109">Bijvoorbeeld wanneer een nieuwe Office 365-e-mail is ontvangen met een bijlage (een trigger), maakt u een nieuw bestand in OneDrive (een actie).</span><span class="sxs-lookup"><span data-stu-id="b8260-109">For example, when a new Office 365 email is received with an attachment (a trigger), create a new file in OneDrive (an action).</span></span>

<span data-ttu-id="b8260-110">In dit onderwerp leest u hoe de OneDrive-connector gebruiken in een logische app en vermeldt tevens de triggers en acties.</span><span class="sxs-lookup"><span data-stu-id="b8260-110">This topic shows you how to use the OneDrive connector in a logic app, and also lists the triggers and actions.</span></span>

<span data-ttu-id="b8260-111">Zie voor meer informatie over Logic Apps, [wat zijn logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) en [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="b8260-111">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-onedrive"></a><span data-ttu-id="b8260-112">Verbinding maken met OneDrive</span><span class="sxs-lookup"><span data-stu-id="b8260-112">Connect to OneDrive</span></span>
<span data-ttu-id="b8260-113">Om uw logische app toegang alle services tot, maakt u eerst een *verbinding* naar de service.</span><span class="sxs-lookup"><span data-stu-id="b8260-113">Before your logic app can access any service, you first create a *connection* to the service.</span></span> <span data-ttu-id="b8260-114">Een verbinding biedt connectiviteit tussen een logische app en een andere service.</span><span class="sxs-lookup"><span data-stu-id="b8260-114">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="b8260-115">Bijvoorbeeld, als u wilt verbinding maken met OneDrive, moet u eerst een OneDrive *verbinding*.</span><span class="sxs-lookup"><span data-stu-id="b8260-115">For example, to connect to OneDrive, you first need a OneDrive *connection*.</span></span> <span data-ttu-id="b8260-116">Voer de referenties die u gebruikt om toegang tot de service die u verbinding maken wilt met een verbinding wilt maken.</span><span class="sxs-lookup"><span data-stu-id="b8260-116">To create a connection, enter the credentials you normally use to access the service you wish to connect to.</span></span> <span data-ttu-id="b8260-117">Voer dus met OneDrive, de referenties naar uw OneDrive-account om de verbinding te maken.</span><span class="sxs-lookup"><span data-stu-id="b8260-117">So, with OneDrive, enter the credentials to your OneDrive account  to create the connection.</span></span>

### <a name="create-the-connection"></a><span data-ttu-id="b8260-118">De verbinding maken</span><span class="sxs-lookup"><span data-stu-id="b8260-118">Create the connection</span></span>
> [!INCLUDE [Steps to create a connection to OneDrive](../../includes/connectors-create-api-onedrive.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="b8260-119">Een trigger te gebruiken</span><span class="sxs-lookup"><span data-stu-id="b8260-119">Use a trigger</span></span>
<span data-ttu-id="b8260-120">Een trigger is een gebeurtenis die kan worden gebruikt om de werkstroom die is gedefinieerd in een logische app te starten.</span><span class="sxs-lookup"><span data-stu-id="b8260-120">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="b8260-121">Triggers pollen' ' de service op het interval en de gewenste frequentie.</span><span class="sxs-lookup"><span data-stu-id="b8260-121">Triggers "poll" the service at an interval and frequency that you want.</span></span> <span data-ttu-id="b8260-122">[Meer informatie over triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="b8260-122">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="b8260-123">Typ in de logische app, 'onedrive' om een lijst van de triggers:</span><span class="sxs-lookup"><span data-stu-id="b8260-123">In the logic app, type "onedrive" to get a list of the triggers:</span></span>  
   
    ![](./media/connectors-create-api-onedrive/onedrive-1.png)
2. <span data-ttu-id="b8260-124">Selecteer **wanneer een bestand wordt gewijzigd**.</span><span class="sxs-lookup"><span data-stu-id="b8260-124">Select **When a file is modified**.</span></span> <span data-ttu-id="b8260-125">Als er al een verbinding bestaat, selecteert u de objectkiezer tonen knop om een map te selecteren.</span><span class="sxs-lookup"><span data-stu-id="b8260-125">If a connection already exists, then select the Show Picker button to select a folder.</span></span>
   
    ![](./media/connectors-create-api-onedrive/sample-folder.png)
   
    <span data-ttu-id="b8260-126">Als u wordt gevraagd aan te melden, voert u het teken in details om de verbinding te maken.</span><span class="sxs-lookup"><span data-stu-id="b8260-126">If you are prompted to sign in, then enter the sign in details to create the connection.</span></span> <span data-ttu-id="b8260-127">[De verbinding](connectors-create-api-onedrive.md#create-the-connection) vermeldt de stappen in dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="b8260-127">[Create the connection](connectors-create-api-onedrive.md#create-the-connection) in this topic lists the steps.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="b8260-128">In dit voorbeeld wordt de logische app wordt uitgevoerd als een bestand in de map die u kiest, wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="b8260-128">In this example, the logic app runs when a file in the folder you choose is updated.</span></span> <span data-ttu-id="b8260-129">U kunt de resultaten van deze trigger toevoegen nog een actie die u een e-mailbericht verzendt.</span><span class="sxs-lookup"><span data-stu-id="b8260-129">To see the results of this trigger, add another action that sends you an email.</span></span> <span data-ttu-id="b8260-130">Bijvoorbeeld, voeg de Office 365 Outlook *e-mailbericht verzenden* actie die u e-mailberichten wanneer een bestand wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="b8260-130">For example, add the Office 365 Outlook *Send an email* action that emails you when a file is updated.</span></span> 

3. <span data-ttu-id="b8260-131">Selecteer de **bewerken** knop en stel de **frequentie** en **Interval** waarden.</span><span class="sxs-lookup"><span data-stu-id="b8260-131">Select the **Edit** button and set the **Frequency** and **Interval** values.</span></span> <span data-ttu-id="b8260-132">Bijvoorbeeld, als u wilt dat de trigger voor het pollen van elke 15 minuten, wordt ingesteld de **frequentie** naar **minuut**, en stel de **Interval** naar **15**.</span><span class="sxs-lookup"><span data-stu-id="b8260-132">For example, if you want the trigger to poll every 15 minutes, then set the **Frequency** to **Minute**, and set the **Interval** to **15**.</span></span> 
   
    ![](./media/connectors-create-api-onedrive/trigger-properties.png)
4. <span data-ttu-id="b8260-133">**Sla** uw wijzigingen (linkerbovenhoek van de werkbalk).</span><span class="sxs-lookup"><span data-stu-id="b8260-133">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="b8260-134">Uw logische app wordt opgeslagen en automatisch kan worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="b8260-134">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="b8260-135">Gebruik een actie</span><span class="sxs-lookup"><span data-stu-id="b8260-135">Use an action</span></span>
<span data-ttu-id="b8260-136">Een actie is een bewerking uitgevoerd door de werkstroom die is gedefinieerd in een logische app.</span><span class="sxs-lookup"><span data-stu-id="b8260-136">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="b8260-137">[Meer informatie over acties](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="b8260-137">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="b8260-138">Selecteer het plusteken.</span><span class="sxs-lookup"><span data-stu-id="b8260-138">Select the plus sign.</span></span> <span data-ttu-id="b8260-139">Ziet u verschillende mogelijkheden: **een actie toevoegen**, **een voorwaarde toevoegen**, of een van de **meer** opties.</span><span class="sxs-lookup"><span data-stu-id="b8260-139">You see several choices: **Add an action**, **Add a condition**, or one of the **More** options.</span></span>
   
    ![](./media/connectors-create-api-onedrive/add-action.png)
2. <span data-ttu-id="b8260-140">Kies **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b8260-140">Choose **Add an action**.</span></span>
3. <span data-ttu-id="b8260-141">Typ in het tekstvak 'onedrive' om een lijst met alle beschikbare acties.</span><span class="sxs-lookup"><span data-stu-id="b8260-141">In the text box, type “onedrive” to get a list of all the available actions.</span></span>
   
    ![](./media/connectors-create-api-onedrive/onedrive-actions.png) 
4. <span data-ttu-id="b8260-142">Kies in ons voorbeeld **OneDrive - bestand maken**.</span><span class="sxs-lookup"><span data-stu-id="b8260-142">In our example, choose **OneDrive - Create file**.</span></span> <span data-ttu-id="b8260-143">Als er al een verbinding bestaat, selecteert u de **mappad** invoeren om het bestand de **bestandsnaam**, en kies de **bestandsinhoud** gewenste:</span><span class="sxs-lookup"><span data-stu-id="b8260-143">If a connection already exists, then select the **Folder Path** to put the file, enter the **File Name**, and choose the **File Content** you want:</span></span>  
   
    ![](./media/connectors-create-api-onedrive/sample-action.png)
   
    <span data-ttu-id="b8260-144">Als u wordt gevraagd om de verbindingsinformatie, voert u de details om de verbinding te maken.</span><span class="sxs-lookup"><span data-stu-id="b8260-144">If you are prompted for the connection information, then enter the details to create the connection.</span></span> <span data-ttu-id="b8260-145">[De verbinding](connectors-create-api-onedrive.md#create-the-connection) in dit onderwerp beschrijft deze eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="b8260-145">[Create the connection](connectors-create-api-onedrive.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="b8260-146">In dit voorbeeld maken we een nieuw bestand in een map OneDrive.</span><span class="sxs-lookup"><span data-stu-id="b8260-146">In this example, we create a new file in a OneDrive folder.</span></span> <span data-ttu-id="b8260-147">Uitvoer van een andere trigger kunt u het bestand OneDrive te maken.</span><span class="sxs-lookup"><span data-stu-id="b8260-147">You can use output from another trigger to create the OneDrive file.</span></span> <span data-ttu-id="b8260-148">Bijvoorbeeld, voeg de Office 365 Outlook *wanneer een nieuw e-mailadres binnenkomt* trigger.</span><span class="sxs-lookup"><span data-stu-id="b8260-148">For example, add the Office 365 Outlook *When a new email arrives* trigger.</span></span> <span data-ttu-id="b8260-149">Voeg vervolgens de OneDrive *Create file* actie die u de bijlagen en de Content-Type gebruikt velden binnen een ForEach maken van het nieuwe bestand in OneDrive.</span><span class="sxs-lookup"><span data-stu-id="b8260-149">Then add the OneDrive *Create file* action that uses the Attachments and Content-Type fields within a ForEach to create the new file in OneDrive.</span></span> 
   > 
   > ![](./media/connectors-create-api-onedrive/foreach-action.png)

5. <span data-ttu-id="b8260-150">**Sla** uw wijzigingen (linkerbovenhoek van de werkbalk).</span><span class="sxs-lookup"><span data-stu-id="b8260-150">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="b8260-151">Uw logische app wordt opgeslagen en automatisch kan worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="b8260-151">Your logic app is saved and may be automatically enabled.</span></span>


## <a name="connector-specific-details"></a><span data-ttu-id="b8260-152">Connector-specifieke details</span><span class="sxs-lookup"><span data-stu-id="b8260-152">Connector-specific details</span></span>

<span data-ttu-id="b8260-153">Alle triggers en acties die zijn gedefinieerd in de swagger bekijken en ziet u ook de beperkingen in de [connector details](/connectors/onedriveconnector/).</span><span class="sxs-lookup"><span data-stu-id="b8260-153">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/onedriveconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="b8260-154">Meer connectors</span><span class="sxs-lookup"><span data-stu-id="b8260-154">More connectors</span></span>
<span data-ttu-id="b8260-155">Ga terug naar de [API's lijst](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="b8260-155">Go back to the [APIs list](apis-list.md).</span></span>