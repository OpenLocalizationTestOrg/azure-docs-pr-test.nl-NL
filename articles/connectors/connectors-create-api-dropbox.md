---
title: Dropbox-connector in Azure Logic Apps | Microsoft Docs
description: Logic apps maken met Azure App service. Verbinding maken met Dropbox voor het beheren van uw bestanden. U kunt uitvoeren van verschillende acties zoals het uploaden, bijwerken, ophalen en verwijderen van bestanden in Dropbox.
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: cb0ae033-aba7-4ac9-beaa-be561a0f0cac
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/15/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 0d09580c60fd620811b539147439d0922839fe7e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-dropbox-connector"></a><span data-ttu-id="fa469-105">Aan de slag met de Dropbox-connector</span><span class="sxs-lookup"><span data-stu-id="fa469-105">Get started with the Dropbox connector</span></span>
<span data-ttu-id="fa469-106">Verbinding maken met Dropbox voor het beheren van uw bestanden.</span><span class="sxs-lookup"><span data-stu-id="fa469-106">Connect to Dropbox to manage your files.</span></span> <span data-ttu-id="fa469-107">U kunt uitvoeren van verschillende acties zoals het uploaden, bijwerken, ophalen en verwijderen van bestanden in Dropbox.</span><span class="sxs-lookup"><span data-stu-id="fa469-107">You can perform various actions such as upload, update, get, and delete files in Dropbox.</span></span>

<span data-ttu-id="fa469-108">Gebruik [elke connector](apis-list.md), moet u eerst een logische app maken.</span><span class="sxs-lookup"><span data-stu-id="fa469-108">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="fa469-109">U kunt aan de slag door [maken van een logische app nu](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="fa469-109">You can get started by [creating a Logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-dropbox"></a><span data-ttu-id="fa469-110">Verbinding maken met Dropbox</span><span class="sxs-lookup"><span data-stu-id="fa469-110">Connect to Dropbox</span></span>
<span data-ttu-id="fa469-111">Om uw logische app toegang alle services tot, moet u eerst maken een *verbinding* naar de service.</span><span class="sxs-lookup"><span data-stu-id="fa469-111">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="fa469-112">Een verbinding biedt connectiviteit tussen een logische app en een andere service.</span><span class="sxs-lookup"><span data-stu-id="fa469-112">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="fa469-113">Bijvoorbeeld, om verbinding met Dropbox, moet u eerst een Dropbox *verbinding*.</span><span class="sxs-lookup"><span data-stu-id="fa469-113">For example, in order to connect to Dropbox, you first need a Dropbox *connection*.</span></span> <span data-ttu-id="fa469-114">Een verbinding wilt maken, moet u de referenties die u gebruikt om toegang tot de service die u verbinding wilt maken.</span><span class="sxs-lookup"><span data-stu-id="fa469-114">To create a connection, you would need to provide the credentials you normally use to access the service you wish to connect to.</span></span> <span data-ttu-id="fa469-115">Dus in het voorbeeld Dropbox moet u de referenties voor uw Dropbox-account om te kunnen maken van de verbinding met Dropbox.</span><span class="sxs-lookup"><span data-stu-id="fa469-115">So, in the Dropbox example, you would need the credentials to your Dropbox account in order to create the connection to Dropbox.</span></span> [<span data-ttu-id="fa469-116">Meer informatie over verbindingen</span><span class="sxs-lookup"><span data-stu-id="fa469-116">Learn more about connections</span></span>]()

### <a name="create-a-connection-to-dropbox"></a><span data-ttu-id="fa469-117">Maak een verbinding met Dropbox</span><span class="sxs-lookup"><span data-stu-id="fa469-117">Create a connection to Dropbox</span></span>
> [!INCLUDE [Steps to create a connection to Dropbox](../../includes/connectors-create-api-dropbox.md)]
> 
> 

## <a name="use-a-dropbox-trigger"></a><span data-ttu-id="fa469-118">Gebruik een trigger Dropbox</span><span class="sxs-lookup"><span data-stu-id="fa469-118">Use a Dropbox trigger</span></span>
<span data-ttu-id="fa469-119">Een trigger is een gebeurtenis die kan worden gebruikt om de werkstroom die is gedefinieerd in een logische app te starten.</span><span class="sxs-lookup"><span data-stu-id="fa469-119">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="fa469-120">[Meer informatie over triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="fa469-120">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="fa469-121">In dit voorbeeld gebruiken we de **wanneer een bestand wordt gemaakt** trigger.</span><span class="sxs-lookup"><span data-stu-id="fa469-121">In this example, we will use the **When a file is created** trigger.</span></span> <span data-ttu-id="fa469-122">Wanneer deze trigger optreedt, noemen we de **ophalen met behulp van pad bestandsinhoud** Dropbox-actie.</span><span class="sxs-lookup"><span data-stu-id="fa469-122">When this trigger occurs, we will call the **Get file content using path** Dropbox action.</span></span> 

1. <span data-ttu-id="fa469-123">Voer *dropbox* in het zoekvak op de ontwerpfunctie Logic Apps, selecteer de **Dropbox - wanneer een bestand wordt gemaakt** trigger.</span><span class="sxs-lookup"><span data-stu-id="fa469-123">Enter *dropbox* in the search box on the Logic Apps designer, then select the **Dropbox - When a file is created** trigger.</span></span>      
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger.PNG)  
2. <span data-ttu-id="fa469-124">Selecteer de map waarin u wilt maken van het bestand bijhouden.</span><span class="sxs-lookup"><span data-stu-id="fa469-124">Select the folder in which you want to track file creation.</span></span> <span data-ttu-id="fa469-125">Selecteren... (geïdentificeerd in het vak rood) en blader naar de map die u selecteren wilt voor de trigger de invoer.</span><span class="sxs-lookup"><span data-stu-id="fa469-125">Select ... (identified in the red box) and browse to the folder you wish to select for the trigger's input.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger-2.PNG)  

## <a name="use-a-dropbox-action"></a><span data-ttu-id="fa469-126">Gebruik een Dropbox-actie</span><span class="sxs-lookup"><span data-stu-id="fa469-126">Use a Dropbox action</span></span>
<span data-ttu-id="fa469-127">Een actie is een bewerking uitgevoerd door de werkstroom die is gedefinieerd in een logische app.</span><span class="sxs-lookup"><span data-stu-id="fa469-127">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="fa469-128">[Meer informatie over acties](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="fa469-128">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="fa469-129">Nu dat de trigger is toegevoegd, volg deze stappen uit om een actie die de inhoud van het nieuwe bestand krijgen.</span><span class="sxs-lookup"><span data-stu-id="fa469-129">Now that the trigger has been added, follow these steps to add an action that will get the new file's content.</span></span>

1. <span data-ttu-id="fa469-130">Selecteer **+ een nieuwe stap** om toe te voegen van de actie die u uitvoeren wilt wanneer een nieuw bestand wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="fa469-130">Select **+ New Step** to add the action you would like to take when a new file is created.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action.PNG)
2. <span data-ttu-id="fa469-131">Selecteer **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="fa469-131">Select **Add an action**.</span></span> <span data-ttu-id="fa469-132">Deze wordt geopend het zoekvak waarin u naar elke actie u zoeken kunt wilt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="fa469-132">This opens the search box where you can search for any action you would like to take.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-2.PNG)
3. <span data-ttu-id="fa469-133">Voer *dropbox* om te zoeken naar acties met betrekking tot Dropbox.</span><span class="sxs-lookup"><span data-stu-id="fa469-133">Enter *dropbox* to search for actions related to Dropbox.</span></span>  
4. <span data-ttu-id="fa469-134">Selecteer **Dropbox - bestandsinhoud ophalen met behulp van pad** als de actie moet worden uitgevoerd wanneer een nieuw bestand is gemaakt in de geselecteerde Dropbox-map.</span><span class="sxs-lookup"><span data-stu-id="fa469-134">Select **Dropbox - Get file content using path** as the action to take when a new file is created in the selected Dropbox folder.</span></span> <span data-ttu-id="fa469-135">Hiermee opent u de actie in het Configuratiescherm.</span><span class="sxs-lookup"><span data-stu-id="fa469-135">The action control block opens.</span></span> <span data-ttu-id="fa469-136">U wordt gevraagd uw logische app toegang tot uw Dropbox-account als u nog niet gedaan eerder autoriseren.</span><span class="sxs-lookup"><span data-stu-id="fa469-136">You will be prompted to authorize your logic app to access your Dropbox account if you have not done so previously.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-3.PNG)  
5. <span data-ttu-id="fa469-137">Selecteren... (te vinden op de rechterkant van de **bestandspad** besturingselement) en blader naar het bestandspad dat u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fa469-137">Select ... (located at the right side of the **File Path** control) and browse to the file path you would like to use.</span></span> <span data-ttu-id="fa469-138">Of gebruik de **bestandspad** token gebruikt voor het maken van uw logische app te versnellen.</span><span class="sxs-lookup"><span data-stu-id="fa469-138">Or, use the **file path** token to speed up your logic app creation.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-4.PNG)  
6. <span data-ttu-id="fa469-139">Sla uw werk op en maak een nieuw bestand in Dropbox voor het activeren van uw werkstroom.</span><span class="sxs-lookup"><span data-stu-id="fa469-139">Save your work and create a new file in Dropbox to activate your workflow.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="fa469-140">Connector-specifieke details</span><span class="sxs-lookup"><span data-stu-id="fa469-140">Connector-specific details</span></span>

<span data-ttu-id="fa469-141">Alle triggers en acties die zijn gedefinieerd in de swagger bekijken en ziet u ook de beperkingen in de [connector details](/connectors/dropbox/).</span><span class="sxs-lookup"><span data-stu-id="fa469-141">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/dropbox/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="fa469-142">Meer connectors</span><span class="sxs-lookup"><span data-stu-id="fa469-142">More connectors</span></span>
<span data-ttu-id="fa469-143">Ga terug naar de [API's lijst](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="fa469-143">Go back to the [APIs list](apis-list.md).</span></span>