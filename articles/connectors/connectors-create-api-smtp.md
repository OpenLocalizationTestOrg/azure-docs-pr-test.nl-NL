---
title: aaaSMTP-connector in Azure Logic Apps | Microsoft Docs
description: Logic apps maken met Azure App service. Verbinding maken met tooSMTP toosend e-mailbericht.
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
ms.openlocfilehash: 36bb836851014d24f2e069fda8376ad7a08c943b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-smtp-connector"></a><span data-ttu-id="3e024-104">Aan de slag met Hallo SMTP-connector</span><span class="sxs-lookup"><span data-stu-id="3e024-104">Get started with hello SMTP connector</span></span>
<span data-ttu-id="3e024-105">Verbinding maken met tooSMTP toosend e-mailbericht.</span><span class="sxs-lookup"><span data-stu-id="3e024-105">Connect tooSMTP toosend email.</span></span>

<span data-ttu-id="3e024-106">toouse [elke connector](apis-list.md), moet u eerst toocreate een logische app.</span><span class="sxs-lookup"><span data-stu-id="3e024-106">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="3e024-107">U kunt aan de slag door [maken van een logische app nu](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="3e024-107">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toosmtp"></a><span data-ttu-id="3e024-108">Verbinding maken met tooSMTP</span><span class="sxs-lookup"><span data-stu-id="3e024-108">Connect tooSMTP</span></span>
<span data-ttu-id="3e024-109">Om uw logische app toegang alle services tot, moet u eerst toocreate een *verbinding* toohello service.</span><span class="sxs-lookup"><span data-stu-id="3e024-109">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="3e024-110">Een [verbinding](connectors-overview.md) biedt connectiviteit tussen een logische app en een andere service.</span><span class="sxs-lookup"><span data-stu-id="3e024-110">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="3e024-111">Bijvoorbeeld, tooconnect tooSMTP, moet u eerst een SMTP *verbinding*.</span><span class="sxs-lookup"><span data-stu-id="3e024-111">For example, tooconnect tooSMTP, you first need an SMTP *connection*.</span></span> <span data-ttu-id="3e024-112">een verbinding toocreate Geef referenties op Hallo u normaal gesproken tooaccess Hallo service u verbinding met maken.</span><span class="sxs-lookup"><span data-stu-id="3e024-112">toocreate a connection, enter hello credentials you normally use tooaccess hello service you connect to.</span></span> <span data-ttu-id="3e024-113">Voer dus in Hallo SMTP bijvoorbeeld Hallo referenties tooyour verbindingsnaam SMTP-serveradres en gebruiker aanmelding informatie toocreate Hallo verbinding tooSMTP.</span><span class="sxs-lookup"><span data-stu-id="3e024-113">So, in hello SMTP example, enter hello credentials tooyour connection name, SMTP server address, and user login information toocreate hello connection tooSMTP.</span></span>  

### <a name="create-a-connection-toosmtp"></a><span data-ttu-id="3e024-114">Een tooSMTP verbinding maken</span><span class="sxs-lookup"><span data-stu-id="3e024-114">Create a connection tooSMTP</span></span>
> [!INCLUDE [Steps toocreate a connection tooSMTP](../../includes/connectors-create-api-smtp.md)]
> 
> 

## <a name="use-an-smtp-trigger"></a><span data-ttu-id="3e024-115">Gebruik een SMTP-trigger</span><span class="sxs-lookup"><span data-stu-id="3e024-115">Use an SMTP trigger</span></span>
<span data-ttu-id="3e024-116">Een trigger is een gebeurtenis die gebruikt toostart Hallo werkstroom gedefinieerd in een logische app worden kan.</span><span class="sxs-lookup"><span data-stu-id="3e024-116">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="3e024-117">[Meer informatie over triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="3e024-117">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="3e024-118">In dit voorbeeld omdat SMTP niet over een trigger van een eigen beschikt, gebruiken we Hallo **Salesforce - wanneer een object wordt gemaakt** trigger.</span><span class="sxs-lookup"><span data-stu-id="3e024-118">In this example, because SMTP does not have a trigger of its own, we'll use hello **Salesforce - When an object is created** trigger.</span></span> <span data-ttu-id="3e024-119">Deze trigger wordt geactiveerd wanneer een nieuw object in Salesforce maakt.</span><span class="sxs-lookup"><span data-stu-id="3e024-119">This trigger activates when a new object is created in Salesforce.</span></span> <span data-ttu-id="3e024-120">In ons voorbeeld stellen we het zo dat elke keer wanneer een nieuwe lead wordt gemaakt in Salesforce, een *e-mail verzenden* actie plaatsvindt via Hallo SMTP-connector met een melding van de nieuwe lead hello wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3e024-120">For our example, we'll set it up such that every time a new lead is created in Salesforce, a *send email* action occurs via hello SMTP connector with a notification of hello new lead being created.</span></span>

1. <span data-ttu-id="3e024-121">Voer *salesforce* Selecteer in het zoekvak Hallo op Hallo logic apps designer Hallo **Salesforce - wanneer een object wordt gemaakt** trigger.</span><span class="sxs-lookup"><span data-stu-id="3e024-121">Enter *salesforce* in hello search box on hello logic apps designer then select hello **Salesforce - When an object is created** trigger.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-1.png)  
2. <span data-ttu-id="3e024-122">Hallo **wanneer een object wordt gemaakt** besturingselement wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3e024-122">hello **When an object is created** control is displayed.</span></span>
   ![](../../includes/media/connectors-create-api-salesforce/trigger-2.png)  
3. <span data-ttu-id="3e024-123">Selecteer Hallo **objecttype** Selecteer *leiden* uit Hallo lijst met objecten.</span><span class="sxs-lookup"><span data-stu-id="3e024-123">Select hello **Object Type** then select *Lead* from hello list of objects.</span></span> <span data-ttu-id="3e024-124">In deze stap geeft u aan dat u een trigger die uw logische app ontvangt een melding maakt wanneer er een nieuwe lead wordt gemaakt in Salesforce.</span><span class="sxs-lookup"><span data-stu-id="3e024-124">In this step you are indicating that you are creating a trigger that will notify your logic app whenever a new lead is created in Salesforce.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger3.png)  
4. <span data-ttu-id="3e024-125">Hallo-trigger is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3e024-125">hello trigger has been created.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-4.png)  

## <a name="use-an-smtp-action"></a><span data-ttu-id="3e024-126">Gebruik een SMTP-actie</span><span class="sxs-lookup"><span data-stu-id="3e024-126">Use an SMTP action</span></span>
<span data-ttu-id="3e024-127">Een actie is een bewerking uitgevoerd door Hallo werkstroom gedefinieerd in een logische app.</span><span class="sxs-lookup"><span data-stu-id="3e024-127">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="3e024-128">[Meer informatie over acties](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="3e024-128">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="3e024-129">Nu hello trigger is toegevoegd, volgt u deze stappen tooadd een SMTP-actie die wordt uitgevoerd wanneer een nieuwe lead in Salesforce wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3e024-129">Now that hello trigger has been added, follow these steps tooadd an SMTP action that will occur when a new lead is created in Salesforce.</span></span>

1. <span data-ttu-id="3e024-130">Selecteer **+ een nieuwe stap** tooadd Hallo actie u wilt dat tootake wanneer een nieuwe lead wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3e024-130">Select **+ New Step** tooadd hello action you would like tootake when a new lead is created.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger4.png)  
2. <span data-ttu-id="3e024-131">Selecteer **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="3e024-131">Select **Add an action**.</span></span> <span data-ttu-id="3e024-132">Dit wordt geopend Hallo zoekvak waarin u naar elke actie u zoeken kunt graag tootake.</span><span class="sxs-lookup"><span data-stu-id="3e024-132">This opens hello search box where you can search for any action you would like tootake.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-2.png)  
3. <span data-ttu-id="3e024-133">Voer *smtp* toosearch voor verwante tooSMTP acties.</span><span class="sxs-lookup"><span data-stu-id="3e024-133">Enter *smtp* toosearch for actions related tooSMTP.</span></span>  
4. <span data-ttu-id="3e024-134">Selecteer **SMTP - e-mailbericht verzenden** zoals actie tootake Hallo wanneer nieuwe lead hello wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3e024-134">Select **SMTP - Send Email** as hello action tootake when hello new lead is created.</span></span> <span data-ttu-id="3e024-135">Hallo actie besturingselement blok wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="3e024-135">hello action control block opens.</span></span> <span data-ttu-id="3e024-136">U hebt tooestablish uw SMTP-verbinding in de ontwerpfunctie blok Hallo als u dit eerder niet hebt gedaan.</span><span class="sxs-lookup"><span data-stu-id="3e024-136">You will have tooestablish your smtp connection in hello designer block if you have not done so previously.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/smtp-2.png)    
5. <span data-ttu-id="3e024-137">Voer uw gewenste e-informatie in Hallo **SMTP - e-mailbericht verzenden** blok.</span><span class="sxs-lookup"><span data-stu-id="3e024-137">Input your desired email information in hello **SMTP - Send Email** block.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-4.PNG)  
6. <span data-ttu-id="3e024-138">Sla uw werk in volgorde tooactivate uw werkstroom.</span><span class="sxs-lookup"><span data-stu-id="3e024-138">Save your work in order tooactivate your workflow.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="3e024-139">Connector-specifieke details</span><span class="sxs-lookup"><span data-stu-id="3e024-139">Connector-specific details</span></span>

<span data-ttu-id="3e024-140">Alle triggers en acties die zijn gedefinieerd in swagger Hallo bekijken en ook bekijken in Hallo beperkingen [connector details](/connectors/smtpconnector/).</span><span class="sxs-lookup"><span data-stu-id="3e024-140">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/smtpconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="3e024-141">Meer connectors</span><span class="sxs-lookup"><span data-stu-id="3e024-141">More connectors</span></span>
<span data-ttu-id="3e024-142">Ga terug toohello [API's lijst](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="3e024-142">Go back toohello [APIs list](apis-list.md).</span></span>
