---
title: aaaAdd hello OneDrive-connector in uw logische Apps | Microsoft Docs
description: Overzicht van Hallo OneDrive connector met de parameters van de REST-API
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
ms.openlocfilehash: 8303794bb3c2844de288f87f40639abb84c160fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-onedrive-connector"></a><span data-ttu-id="e5716-103">Aan de slag met Hallo OneDrive-connector</span><span class="sxs-lookup"><span data-stu-id="e5716-103">Get started with hello OneDrive connector</span></span>
<span data-ttu-id="e5716-104">Verbinding maken met de bestanden, waaronder het uploaden, ophalen en verwijder bestanden tooOneDrive toomanage.</span><span class="sxs-lookup"><span data-stu-id="e5716-104">Connect tooOneDrive toomanage your files, including upload, get, delete files, and more.</span></span> 

<span data-ttu-id="e5716-105">Met OneDrive, u:</span><span class="sxs-lookup"><span data-stu-id="e5716-105">With OneDrive, you:</span></span> 

* <span data-ttu-id="e5716-106">Het bouwen van uw werkstroom door het opslaan van bestanden in OneDrive of bijwerken van bestaande bestanden in OneDrive.</span><span class="sxs-lookup"><span data-stu-id="e5716-106">Build your workflow by storing files in OneDrive, or update existing files in OneDrive.</span></span> 
* <span data-ttu-id="e5716-107">Triggers toostart uw werkstroom gebruiken wanneer een bestand wordt gemaakt of binnen uw OneDrive bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="e5716-107">Use triggers toostart your workflow when a file is created or updated within your OneDrive.</span></span>
* <span data-ttu-id="e5716-108">Acties toocreate een bestand gebruiken en verwijderen van een bestand en meer.</span><span class="sxs-lookup"><span data-stu-id="e5716-108">Use actions toocreate a file, delete a file, and more.</span></span> <span data-ttu-id="e5716-109">Bijvoorbeeld wanneer een nieuwe Office 365-e-mail is ontvangen met een bijlage (een trigger), maakt u een nieuw bestand in OneDrive (een actie).</span><span class="sxs-lookup"><span data-stu-id="e5716-109">For example, when a new Office 365 email is received with an attachment (a trigger), create a new file in OneDrive (an action).</span></span>

<span data-ttu-id="e5716-110">Dit onderwerp leest u hoe toouse OneDrive-connector in een logische app Hallo en ook een lijst met Hallo triggers en acties.</span><span class="sxs-lookup"><span data-stu-id="e5716-110">This topic shows you how toouse hello OneDrive connector in a logic app, and also lists hello triggers and actions.</span></span>

<span data-ttu-id="e5716-111">toolearn meer informatie over Logic Apps, Zie [wat zijn logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) en [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="e5716-111">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooonedrive"></a><span data-ttu-id="e5716-112">Verbinding maken met tooOneDrive</span><span class="sxs-lookup"><span data-stu-id="e5716-112">Connect tooOneDrive</span></span>
<span data-ttu-id="e5716-113">Om uw logische app toegang alle services tot, maakt u eerst een *verbinding* toohello service.</span><span class="sxs-lookup"><span data-stu-id="e5716-113">Before your logic app can access any service, you first create a *connection* toohello service.</span></span> <span data-ttu-id="e5716-114">Een verbinding biedt connectiviteit tussen een logische app en een andere service.</span><span class="sxs-lookup"><span data-stu-id="e5716-114">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="e5716-115">Bijvoorbeeld, tooconnect tooOneDrive, moet u eerst een OneDrive *verbinding*.</span><span class="sxs-lookup"><span data-stu-id="e5716-115">For example, tooconnect tooOneDrive, you first need a OneDrive *connection*.</span></span> <span data-ttu-id="e5716-116">een verbinding toocreate Geef referenties op Hallo u normaal gesproken tooaccess Hallo service tooconnect te gewenste gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e5716-116">toocreate a connection, enter hello credentials you normally use tooaccess hello service you wish tooconnect to.</span></span> <span data-ttu-id="e5716-117">Voer dus met OneDrive, Hallo referenties tooyour OneDrive-account toocreate Hallo verbinding.</span><span class="sxs-lookup"><span data-stu-id="e5716-117">So, with OneDrive, enter hello credentials tooyour OneDrive account  toocreate hello connection.</span></span>

### <a name="create-hello-connection"></a><span data-ttu-id="e5716-118">Hallo verbinding maken</span><span class="sxs-lookup"><span data-stu-id="e5716-118">Create hello connection</span></span>
> [!INCLUDE [Steps toocreate a connection tooOneDrive](../../includes/connectors-create-api-onedrive.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="e5716-119">Een trigger te gebruiken</span><span class="sxs-lookup"><span data-stu-id="e5716-119">Use a trigger</span></span>
<span data-ttu-id="e5716-120">Een trigger is een gebeurtenis die gebruikt toostart Hallo werkstroom gedefinieerd in een logische app worden kan.</span><span class="sxs-lookup"><span data-stu-id="e5716-120">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="e5716-121">Triggers pollen' ' Hallo-service op het interval en de gewenste frequentie.</span><span class="sxs-lookup"><span data-stu-id="e5716-121">Triggers "poll" hello service at an interval and frequency that you want.</span></span> <span data-ttu-id="e5716-122">[Meer informatie over triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="e5716-122">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="e5716-123">Typ in Hallo logische app, 'onedrive' tooget een lijst met Hallo-triggers:</span><span class="sxs-lookup"><span data-stu-id="e5716-123">In hello logic app, type "onedrive" tooget a list of hello triggers:</span></span>  
   
    ![](./media/connectors-create-api-onedrive/onedrive-1.png)
2. <span data-ttu-id="e5716-124">Selecteer **wanneer een bestand wordt gewijzigd**.</span><span class="sxs-lookup"><span data-stu-id="e5716-124">Select **When a file is modified**.</span></span> <span data-ttu-id="e5716-125">Als er al een verbinding bestaat, selecteert u Hallo objectkiezer tonen knop tooselect een map.</span><span class="sxs-lookup"><span data-stu-id="e5716-125">If a connection already exists, then select hello Show Picker button tooselect a folder.</span></span>
   
    ![](./media/connectors-create-api-onedrive/sample-folder.png)
   
    <span data-ttu-id="e5716-126">Als u na vragen aan gebruiker toosign in, voert u Hallo aanmelding in details toocreate Hallo verbinding.</span><span class="sxs-lookup"><span data-stu-id="e5716-126">If you are prompted toosign in, then enter hello sign in details toocreate hello connection.</span></span> <span data-ttu-id="e5716-127">[Hallo verbinding maken](connectors-create-api-onedrive.md#create-the-connection) in dit onderwerp vindt u Hallo stappen.</span><span class="sxs-lookup"><span data-stu-id="e5716-127">[Create hello connection](connectors-create-api-onedrive.md#create-the-connection) in this topic lists hello steps.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="e5716-128">In dit voorbeeld Hallo logische app wordt uitgevoerd als een bestand in Hallo-map die u kiest, wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="e5716-128">In this example, hello logic app runs when a file in hello folder you choose is updated.</span></span> <span data-ttu-id="e5716-129">toosee hello resultaten van deze trigger toevoegen nog een actie die u een e-mailbericht verzendt.</span><span class="sxs-lookup"><span data-stu-id="e5716-129">toosee hello results of this trigger, add another action that sends you an email.</span></span> <span data-ttu-id="e5716-130">Bijvoorbeeld, voeg Hallo Outlook van Office 365 *e-mailbericht verzenden* actie die u e-mailberichten wanneer een bestand wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="e5716-130">For example, add hello Office 365 Outlook *Send an email* action that emails you when a file is updated.</span></span> 

3. <span data-ttu-id="e5716-131">Selecteer Hallo **bewerken** knop en stel Hallo **frequentie** en **Interval** waarden.</span><span class="sxs-lookup"><span data-stu-id="e5716-131">Select hello **Edit** button and set hello **Frequency** and **Interval** values.</span></span> <span data-ttu-id="e5716-132">Bijvoorbeeld, als u wilt dat Hallo trigger toopoll om de 15 minuten, wordt ingesteld Hallo **frequentie** te**minuut**, en set Hallo **Interval** te**15**.</span><span class="sxs-lookup"><span data-stu-id="e5716-132">For example, if you want hello trigger toopoll every 15 minutes, then set hello **Frequency** too**Minute**, and set hello **Interval** too**15**.</span></span> 
   
    ![](./media/connectors-create-api-onedrive/trigger-properties.png)
4. <span data-ttu-id="e5716-133">**Sla** uw wijzigingen (linksboven Hallo werkbalk).</span><span class="sxs-lookup"><span data-stu-id="e5716-133">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="e5716-134">Uw logische app wordt opgeslagen en automatisch kan worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="e5716-134">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="e5716-135">Gebruik een actie</span><span class="sxs-lookup"><span data-stu-id="e5716-135">Use an action</span></span>
<span data-ttu-id="e5716-136">Een actie is een bewerking uitgevoerd door Hallo werkstroom gedefinieerd in een logische app.</span><span class="sxs-lookup"><span data-stu-id="e5716-136">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="e5716-137">[Meer informatie over acties](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="e5716-137">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="e5716-138">Selecteer Hallo plus -teken.</span><span class="sxs-lookup"><span data-stu-id="e5716-138">Select hello plus sign.</span></span> <span data-ttu-id="e5716-139">Ziet u verschillende mogelijkheden: **een actie toevoegen**, **een voorwaarde toevoegen**, of een van de Hallo **meer** opties.</span><span class="sxs-lookup"><span data-stu-id="e5716-139">You see several choices: **Add an action**, **Add a condition**, or one of hello **More** options.</span></span>
   
    ![](./media/connectors-create-api-onedrive/add-action.png)
2. <span data-ttu-id="e5716-140">Kies **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="e5716-140">Choose **Add an action**.</span></span>
3. <span data-ttu-id="e5716-141">Typ in het tekstvak hello, 'onedrive' tooget een lijst met alle beschikbare Hallo-acties.</span><span class="sxs-lookup"><span data-stu-id="e5716-141">In hello text box, type “onedrive” tooget a list of all hello available actions.</span></span>
   
    ![](./media/connectors-create-api-onedrive/onedrive-actions.png) 
4. <span data-ttu-id="e5716-142">Kies in ons voorbeeld **OneDrive - bestand maken**.</span><span class="sxs-lookup"><span data-stu-id="e5716-142">In our example, choose **OneDrive - Create file**.</span></span> <span data-ttu-id="e5716-143">Als er al een verbinding bestaat, selecteert u Hallo **mappad** tooput Hallo bestand, Voer Hallo **bestandsnaam**, en kies Hallo **bestandsinhoud** gewenste:</span><span class="sxs-lookup"><span data-stu-id="e5716-143">If a connection already exists, then select hello **Folder Path** tooput hello file, enter hello **File Name**, and choose hello **File Content** you want:</span></span>  
   
    ![](./media/connectors-create-api-onedrive/sample-action.png)
   
    <span data-ttu-id="e5716-144">Als u wordt gevraagd om de verbindingsgegevens hello, voert u Hallo details toocreate Hallo verbinding.</span><span class="sxs-lookup"><span data-stu-id="e5716-144">If you are prompted for hello connection information, then enter hello details toocreate hello connection.</span></span> <span data-ttu-id="e5716-145">[Hallo verbinding maken](connectors-create-api-onedrive.md#create-the-connection) in dit onderwerp beschrijft deze eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="e5716-145">[Create hello connection](connectors-create-api-onedrive.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="e5716-146">In dit voorbeeld maken we een nieuw bestand in een map OneDrive.</span><span class="sxs-lookup"><span data-stu-id="e5716-146">In this example, we create a new file in a OneDrive folder.</span></span> <span data-ttu-id="e5716-147">U kunt uitvoer vanuit een ander trigger toocreate hello OneDrive-bestand.</span><span class="sxs-lookup"><span data-stu-id="e5716-147">You can use output from another trigger toocreate hello OneDrive file.</span></span> <span data-ttu-id="e5716-148">Bijvoorbeeld, voeg Hallo Outlook van Office 365 *wanneer een nieuw e-mailadres binnenkomt* trigger.</span><span class="sxs-lookup"><span data-stu-id="e5716-148">For example, add hello Office 365 Outlook *When a new email arrives* trigger.</span></span> <span data-ttu-id="e5716-149">Voeg vervolgens Hallo OneDrive *Create file* actie die gebruikmaakt van de Content-Type-velden en Hallo bijlagen binnen een ForEach toocreate Hallo nieuw bestand in OneDrive.</span><span class="sxs-lookup"><span data-stu-id="e5716-149">Then add hello OneDrive *Create file* action that uses hello Attachments and Content-Type fields within a ForEach toocreate hello new file in OneDrive.</span></span> 
   > 
   > ![](./media/connectors-create-api-onedrive/foreach-action.png)

5. <span data-ttu-id="e5716-150">**Sla** uw wijzigingen (linksboven Hallo werkbalk).</span><span class="sxs-lookup"><span data-stu-id="e5716-150">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="e5716-151">Uw logische app wordt opgeslagen en automatisch kan worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="e5716-151">Your logic app is saved and may be automatically enabled.</span></span>


## <a name="connector-specific-details"></a><span data-ttu-id="e5716-152">Connector-specifieke details</span><span class="sxs-lookup"><span data-stu-id="e5716-152">Connector-specific details</span></span>

<span data-ttu-id="e5716-153">Alle triggers en acties die zijn gedefinieerd in swagger Hallo bekijken en ook bekijken in Hallo beperkingen [connector details](/connectors/onedriveconnector/).</span><span class="sxs-lookup"><span data-stu-id="e5716-153">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/onedriveconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="e5716-154">Meer connectors</span><span class="sxs-lookup"><span data-stu-id="e5716-154">More connectors</span></span>
<span data-ttu-id="e5716-155">Ga terug toohello [API's lijst](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="e5716-155">Go back toohello [APIs list](apis-list.md).</span></span>
