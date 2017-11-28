---
title: aaaDropbox-connector in Azure Logic Apps | Microsoft Docs
description: Logic apps maken met Azure App service. Verbinding maken met uw bestanden tooDropbox toomanage. U kunt uitvoeren van verschillende acties zoals het uploaden, bijwerken, ophalen en verwijderen van bestanden in Dropbox.
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
ms.openlocfilehash: 1f307477836104c0bc0008341604a1400860987f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-dropbox-connector"></a><span data-ttu-id="f1b89-105">Aan de slag met Hallo Dropbox-connector</span><span class="sxs-lookup"><span data-stu-id="f1b89-105">Get started with hello Dropbox connector</span></span>
<span data-ttu-id="f1b89-106">Verbinding maken met uw bestanden tooDropbox toomanage.</span><span class="sxs-lookup"><span data-stu-id="f1b89-106">Connect tooDropbox toomanage your files.</span></span> <span data-ttu-id="f1b89-107">U kunt uitvoeren van verschillende acties zoals het uploaden, bijwerken, ophalen en verwijderen van bestanden in Dropbox.</span><span class="sxs-lookup"><span data-stu-id="f1b89-107">You can perform various actions such as upload, update, get, and delete files in Dropbox.</span></span>

<span data-ttu-id="f1b89-108">toouse [elke connector](apis-list.md), moet u eerst toocreate een logische app.</span><span class="sxs-lookup"><span data-stu-id="f1b89-108">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="f1b89-109">U kunt aan de slag door [maken van een logische app nu](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="f1b89-109">You can get started by [creating a Logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toodropbox"></a><span data-ttu-id="f1b89-110">Verbinding maken met tooDropbox</span><span class="sxs-lookup"><span data-stu-id="f1b89-110">Connect tooDropbox</span></span>
<span data-ttu-id="f1b89-111">Om uw logische app toegang alle services tot, moet u eerst toocreate een *verbinding* toohello service.</span><span class="sxs-lookup"><span data-stu-id="f1b89-111">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="f1b89-112">Een verbinding biedt connectiviteit tussen een logische app en een andere service.</span><span class="sxs-lookup"><span data-stu-id="f1b89-112">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="f1b89-113">Bijvoorbeeld, in volgorde tooconnect tooDropbox, moet u eerst een Dropbox *verbinding*.</span><span class="sxs-lookup"><span data-stu-id="f1b89-113">For example, in order tooconnect tooDropbox, you first need a Dropbox *connection*.</span></span> <span data-ttu-id="f1b89-114">toocreate een verbinding, moet u tooprovide Hallo referenties u normaal gesproken tooaccess Hallo service tooconnect te gewenste gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f1b89-114">toocreate a connection, you would need tooprovide hello credentials you normally use tooaccess hello service you wish tooconnect to.</span></span> <span data-ttu-id="f1b89-115">In voorbeeld Hallo Dropbox moet u dus Hallo referenties tooyour Dropbox-account in volgorde toocreate Hallo verbinding tooDropbox.</span><span class="sxs-lookup"><span data-stu-id="f1b89-115">So, in hello Dropbox example, you would need hello credentials tooyour Dropbox account in order toocreate hello connection tooDropbox.</span></span> [<span data-ttu-id="f1b89-116">Meer informatie over verbindingen</span><span class="sxs-lookup"><span data-stu-id="f1b89-116">Learn more about connections</span></span>]()

### <a name="create-a-connection-toodropbox"></a><span data-ttu-id="f1b89-117">Een tooDropbox verbinding maken</span><span class="sxs-lookup"><span data-stu-id="f1b89-117">Create a connection tooDropbox</span></span>
> [!INCLUDE [Steps toocreate a connection tooDropbox](../../includes/connectors-create-api-dropbox.md)]
> 
> 

## <a name="use-a-dropbox-trigger"></a><span data-ttu-id="f1b89-118">Gebruik een trigger Dropbox</span><span class="sxs-lookup"><span data-stu-id="f1b89-118">Use a Dropbox trigger</span></span>
<span data-ttu-id="f1b89-119">Een trigger is een gebeurtenis die gebruikt toostart Hallo werkstroom gedefinieerd in een logische app worden kan.</span><span class="sxs-lookup"><span data-stu-id="f1b89-119">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="f1b89-120">[Meer informatie over triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="f1b89-120">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="f1b89-121">In dit voorbeeld gebruiken we Hallo **wanneer een bestand wordt gemaakt** trigger.</span><span class="sxs-lookup"><span data-stu-id="f1b89-121">In this example, we will use hello **When a file is created** trigger.</span></span> <span data-ttu-id="f1b89-122">Wanneer deze trigger optreedt, noemen we Hallo **ophalen met behulp van pad bestandsinhoud** Dropbox-actie.</span><span class="sxs-lookup"><span data-stu-id="f1b89-122">When this trigger occurs, we will call hello **Get file content using path** Dropbox action.</span></span> 

1. <span data-ttu-id="f1b89-123">Voer *dropbox* in het zoekvak Hallo op Hallo Logic Apps designer, selecteer vervolgens Hallo **Dropbox - wanneer een bestand wordt gemaakt** trigger.</span><span class="sxs-lookup"><span data-stu-id="f1b89-123">Enter *dropbox* in hello search box on hello Logic Apps designer, then select hello **Dropbox - When a file is created** trigger.</span></span>      
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger.PNG)  
2. <span data-ttu-id="f1b89-124">Hallo-map die u maken van het bestand tootrack wilt selecteren.</span><span class="sxs-lookup"><span data-stu-id="f1b89-124">Select hello folder in which you want tootrack file creation.</span></span> <span data-ttu-id="f1b89-125">Selecteren... (aangeduid in rood Hallo vak) en bladeren toohello map die u wenst tooselect voor Hallo trigger de invoer.</span><span class="sxs-lookup"><span data-stu-id="f1b89-125">Select ... (identified in hello red box) and browse toohello folder you wish tooselect for hello trigger's input.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger-2.PNG)  

## <a name="use-a-dropbox-action"></a><span data-ttu-id="f1b89-126">Gebruik een Dropbox-actie</span><span class="sxs-lookup"><span data-stu-id="f1b89-126">Use a Dropbox action</span></span>
<span data-ttu-id="f1b89-127">Een actie is een bewerking uitgevoerd door Hallo werkstroom gedefinieerd in een logische app.</span><span class="sxs-lookup"><span data-stu-id="f1b89-127">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="f1b89-128">[Meer informatie over acties](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="f1b89-128">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="f1b89-129">Nu hello trigger is toegevoegd, volgt u deze stappen tooadd een actie die Hallo nieuwe inhoud van bestand krijgen.</span><span class="sxs-lookup"><span data-stu-id="f1b89-129">Now that hello trigger has been added, follow these steps tooadd an action that will get hello new file's content.</span></span>

1. <span data-ttu-id="f1b89-130">Selecteer **+ een nieuwe stap** tooadd Hallo actie u wilt dat tootake wanneer een nieuw bestand wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f1b89-130">Select **+ New Step** tooadd hello action you would like tootake when a new file is created.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action.PNG)
2. <span data-ttu-id="f1b89-131">Selecteer **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="f1b89-131">Select **Add an action**.</span></span> <span data-ttu-id="f1b89-132">Dit wordt geopend Hallo zoekvak waarin u naar elke actie u zoeken kunt graag tootake.</span><span class="sxs-lookup"><span data-stu-id="f1b89-132">This opens hello search box where you can search for any action you would like tootake.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-2.PNG)
3. <span data-ttu-id="f1b89-133">Voer *dropbox* toosearch voor verwante tooDropbox acties.</span><span class="sxs-lookup"><span data-stu-id="f1b89-133">Enter *dropbox* toosearch for actions related tooDropbox.</span></span>  
4. <span data-ttu-id="f1b89-134">Selecteer **Dropbox - bestandsinhoud ophalen met behulp van pad** zoals actie tootake Hallo wanneer een nieuw bestand wordt gemaakt in Hallo Dropbox-map geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="f1b89-134">Select **Dropbox - Get file content using path** as hello action tootake when a new file is created in hello selected Dropbox folder.</span></span> <span data-ttu-id="f1b89-135">Hallo actie besturingselement blok wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="f1b89-135">hello action control block opens.</span></span> <span data-ttu-id="f1b89-136">U na vragen aan gebruiker tooauthorize uw logische app tooaccess uw Dropbox-account als u dit eerder niet hebt gedaan worden.</span><span class="sxs-lookup"><span data-stu-id="f1b89-136">You will be prompted tooauthorize your logic app tooaccess your Dropbox account if you have not done so previously.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-3.PNG)  
5. <span data-ttu-id="f1b89-137">Selecteren... (zich aan de rechterkant Hallo Hallo **bestandspad** besturingselement) en het bestandspad toohello u toouse wilt bladeren.</span><span class="sxs-lookup"><span data-stu-id="f1b89-137">Select ... (located at hello right side of hello **File Path** control) and browse toohello file path you would like toouse.</span></span> <span data-ttu-id="f1b89-138">Of gebruik Hallo **bestandspad** token toospeed van uw logische app maken.</span><span class="sxs-lookup"><span data-stu-id="f1b89-138">Or, use hello **file path** token toospeed up your logic app creation.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-4.PNG)  
6. <span data-ttu-id="f1b89-139">Sla uw werk op en maak een nieuw bestand in Dropbox tooactivate uw werkstroom.</span><span class="sxs-lookup"><span data-stu-id="f1b89-139">Save your work and create a new file in Dropbox tooactivate your workflow.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="f1b89-140">Connector-specifieke details</span><span class="sxs-lookup"><span data-stu-id="f1b89-140">Connector-specific details</span></span>

<span data-ttu-id="f1b89-141">Alle triggers en acties die zijn gedefinieerd in swagger Hallo bekijken en ook bekijken in Hallo beperkingen [connector details](/connectors/dropbox/).</span><span class="sxs-lookup"><span data-stu-id="f1b89-141">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/dropbox/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="f1b89-142">Meer connectors</span><span class="sxs-lookup"><span data-stu-id="f1b89-142">More connectors</span></span>
<span data-ttu-id="f1b89-143">Ga terug toohello [API's lijst](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="f1b89-143">Go back toohello [APIs list](apis-list.md).</span></span>
