---
title: SMTP-connector in Azure Logic Apps | Microsoft Docs
description: Logic apps maken met Azure App service. Verbinding maken met SMTP om een e-mail te verzenden.
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d4141c08-88d7-4e59-a757-c06d0dc74300
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/15/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 1cf96bbf8bd215d7ddb3c99860a5cb4e668be3c2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-smtp-connector"></a><span data-ttu-id="427e6-104">Aan de slag met de SMTP-connector</span><span class="sxs-lookup"><span data-stu-id="427e6-104">Get started with the SMTP connector</span></span>
<span data-ttu-id="427e6-105">Verbinding maken met SMTP om een e-mail te verzenden.</span><span class="sxs-lookup"><span data-stu-id="427e6-105">Connect to SMTP to send email.</span></span>

<span data-ttu-id="427e6-106">Gebruik [elke connector](apis-list.md), moet u eerst een logische app maken.</span><span class="sxs-lookup"><span data-stu-id="427e6-106">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="427e6-107">U kunt aan de slag door [maken van een logische app nu](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="427e6-107">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-smtp"></a><span data-ttu-id="427e6-108">Verbinding maken met SMTP</span><span class="sxs-lookup"><span data-stu-id="427e6-108">Connect to SMTP</span></span>
<span data-ttu-id="427e6-109">Om uw logische app toegang alle services tot, moet u eerst maken een *verbinding* naar de service.</span><span class="sxs-lookup"><span data-stu-id="427e6-109">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="427e6-110">Een [verbinding](connectors-overview.md) biedt connectiviteit tussen een logische app en een andere service.</span><span class="sxs-lookup"><span data-stu-id="427e6-110">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="427e6-111">Bijvoorbeeld, als u wilt verbinding maken met SMTP, moet u eerst een SMTP *verbinding*.</span><span class="sxs-lookup"><span data-stu-id="427e6-111">For example, to connect to SMTP, you first need an SMTP *connection*.</span></span> <span data-ttu-id="427e6-112">Voer de referenties die u gebruikt om toegang tot de service die u verbinding met maakt een verbinding wilt maken.</span><span class="sxs-lookup"><span data-stu-id="427e6-112">To create a connection, enter the credentials you normally use to access the service you connect to.</span></span> <span data-ttu-id="427e6-113">Voer dus de referenties in het voorbeeld SMTP uw verbindingsnaam, het SMTP-serveradres en de aanmeldingsgegevens voor gebruiker voor het maken van de verbinding met de SMTP.</span><span class="sxs-lookup"><span data-stu-id="427e6-113">So, in the SMTP example, enter the credentials to your connection name, SMTP server address, and user login information to create the connection to SMTP.</span></span>  

### <a name="create-a-connection-to-smtp"></a><span data-ttu-id="427e6-114">Maak een verbinding met de SMTP</span><span class="sxs-lookup"><span data-stu-id="427e6-114">Create a connection to SMTP</span></span>
> [!INCLUDE [Steps to create a connection to SMTP](../../includes/connectors-create-api-smtp.md)]
> 
> 

## <a name="use-an-smtp-trigger"></a><span data-ttu-id="427e6-115">Gebruik een SMTP-trigger</span><span class="sxs-lookup"><span data-stu-id="427e6-115">Use an SMTP trigger</span></span>
<span data-ttu-id="427e6-116">Een trigger is een gebeurtenis die kan worden gebruikt om de werkstroom die is gedefinieerd in een logische app te starten.</span><span class="sxs-lookup"><span data-stu-id="427e6-116">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="427e6-117">[Meer informatie over triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="427e6-117">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="427e6-118">In dit voorbeeld omdat SMTP niet over een trigger van een eigen beschikt, gebruiken we de **Salesforce - wanneer een object wordt gemaakt** trigger.</span><span class="sxs-lookup"><span data-stu-id="427e6-118">In this example, because SMTP does not have a trigger of its own, we'll use the **Salesforce - When an object is created** trigger.</span></span> <span data-ttu-id="427e6-119">Deze trigger wordt geactiveerd wanneer een nieuw object in Salesforce maakt.</span><span class="sxs-lookup"><span data-stu-id="427e6-119">This trigger activates when a new object is created in Salesforce.</span></span> <span data-ttu-id="427e6-120">In ons voorbeeld stellen we het zo dat elke keer wanneer een nieuwe lead wordt gemaakt in Salesforce, een *e-mail verzenden* actie plaatsvindt via de SMTP-connector met een melding van de nieuwe lead wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="427e6-120">For our example, we'll set it up such that every time a new lead is created in Salesforce, a *send email* action occurs via the SMTP connector with a notification of the new lead being created.</span></span>

1. <span data-ttu-id="427e6-121">Voer *salesforce* in het zoekvak op de ontwerpfunctie van logic apps selecteert u vervolgens de **Salesforce - wanneer een object wordt gemaakt** trigger.</span><span class="sxs-lookup"><span data-stu-id="427e6-121">Enter *salesforce* in the search box on the logic apps designer then select the **Salesforce - When an object is created** trigger.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-1.png)  
2. <span data-ttu-id="427e6-122">De **wanneer een object wordt gemaakt** besturingselement wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="427e6-122">The **When an object is created** control is displayed.</span></span>
   ![](../../includes/media/connectors-create-api-salesforce/trigger-2.png)  
3. <span data-ttu-id="427e6-123">Selecteer de **objecttype** Selecteer *leiden* uit de lijst met objecten.</span><span class="sxs-lookup"><span data-stu-id="427e6-123">Select the **Object Type** then select *Lead* from the list of objects.</span></span> <span data-ttu-id="427e6-124">In deze stap geeft u aan dat u een trigger die uw logische app ontvangt een melding maakt wanneer er een nieuwe lead wordt gemaakt in Salesforce.</span><span class="sxs-lookup"><span data-stu-id="427e6-124">In this step you are indicating that you are creating a trigger that will notify your logic app whenever a new lead is created in Salesforce.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger3.png)  
4. <span data-ttu-id="427e6-125">De trigger is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="427e6-125">The trigger has been created.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-4.png)  

## <a name="use-an-smtp-action"></a><span data-ttu-id="427e6-126">Gebruik een SMTP-actie</span><span class="sxs-lookup"><span data-stu-id="427e6-126">Use an SMTP action</span></span>
<span data-ttu-id="427e6-127">Een actie is een bewerking uitgevoerd door de werkstroom die is gedefinieerd in een logische app.</span><span class="sxs-lookup"><span data-stu-id="427e6-127">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="427e6-128">[Meer informatie over acties](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="427e6-128">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="427e6-129">Nu dat de trigger is toegevoegd, volg deze stappen uit om een SMTP-actie die wordt uitgevoerd wanneer een nieuwe lead in Salesforce wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="427e6-129">Now that the trigger has been added, follow these steps to add an SMTP action that will occur when a new lead is created in Salesforce.</span></span>

1. <span data-ttu-id="427e6-130">Selecteer **+ een nieuwe stap** om toe te voegen van de actie die u uitvoeren wilt wanneer een nieuwe lead wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="427e6-130">Select **+ New Step** to add the action you would like to take when a new lead is created.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger4.png)  
2. <span data-ttu-id="427e6-131">Selecteer **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="427e6-131">Select **Add an action**.</span></span> <span data-ttu-id="427e6-132">Deze wordt geopend het zoekvak waarin u naar elke actie u zoeken kunt wilt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="427e6-132">This opens the search box where you can search for any action you would like to take.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-2.png)  
3. <span data-ttu-id="427e6-133">Voer *smtp* om te zoeken naar acties met betrekking tot SMTP.</span><span class="sxs-lookup"><span data-stu-id="427e6-133">Enter *smtp* to search for actions related to SMTP.</span></span>  
4. <span data-ttu-id="427e6-134">Selecteer **SMTP - e-mailbericht verzenden** als de actie moet worden uitgevoerd wanneer de nieuwe lead wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="427e6-134">Select **SMTP - Send Email** as the action to take when the new lead is created.</span></span> <span data-ttu-id="427e6-135">Hiermee opent u de actie in het Configuratiescherm.</span><span class="sxs-lookup"><span data-stu-id="427e6-135">The action control block opens.</span></span> <span data-ttu-id="427e6-136">U moet uw SMTP-om verbinding te maken in de ontwerpfunctie blok als u dit eerder niet hebt gedaan.</span><span class="sxs-lookup"><span data-stu-id="427e6-136">You will have to establish your smtp connection in the designer block if you have not done so previously.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/smtp-2.png)    
5. <span data-ttu-id="427e6-137">Voer uw gewenste e-informatie in de **SMTP - e-mailbericht verzenden** blok.</span><span class="sxs-lookup"><span data-stu-id="427e6-137">Input your desired email information in the **SMTP - Send Email** block.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-4.PNG)  
6. <span data-ttu-id="427e6-138">Sla uw werk op om de werkstroom activeren.</span><span class="sxs-lookup"><span data-stu-id="427e6-138">Save your work in order to activate your workflow.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="427e6-139">Connector-specifieke details</span><span class="sxs-lookup"><span data-stu-id="427e6-139">Connector-specific details</span></span>

<span data-ttu-id="427e6-140">Alle triggers en acties die zijn gedefinieerd in de swagger bekijken en ziet u ook de beperkingen in de [connector details](/connectors/smtpconnector/).</span><span class="sxs-lookup"><span data-stu-id="427e6-140">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/smtpconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="427e6-141">Meer connectors</span><span class="sxs-lookup"><span data-stu-id="427e6-141">More connectors</span></span>
<span data-ttu-id="427e6-142">Ga terug naar de [API's lijst](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="427e6-142">Go back to the [APIs list](apis-list.md).</span></span>