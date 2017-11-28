---
title: aaaLearn hoe toouse Hallo FTP-connector in logic apps | Microsoft Docs
description: Logic apps maken met Azure App service. Verbinding maken met uw bestanden tooFTP server toomanage. U kunt uitvoeren van verschillende acties zoals het uploaden, bijwerken, ophalen en verwijderen van bestanden in de FTP-server.
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: 
tags: connectors
ms.assetid: d83c55fe-eb59-4b7b-a5ec-afac5c772616
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/22/2016
ms.author: mandia; ladocs
ms.openlocfilehash: a7020df2005ebb34fc569627ae0516b8528cc7a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-ftp-connector"></a><span data-ttu-id="3a313-105">Aan de slag met Hallo FTP-connector</span><span class="sxs-lookup"><span data-stu-id="3a313-105">Get started with hello FTP connector</span></span>
<span data-ttu-id="3a313-106">Hallo FTP-connector toomonitor gebruiken, beheren en bestanden op een FTP-server maken.</span><span class="sxs-lookup"><span data-stu-id="3a313-106">Use hello FTP connector toomonitor, manage and create files on an  FTP server.</span></span> 

<span data-ttu-id="3a313-107">toouse [elke connector](apis-list.md), moet u eerst toocreate een logische app.</span><span class="sxs-lookup"><span data-stu-id="3a313-107">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="3a313-108">U kunt aan de slag door [maken van een logische app nu](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="3a313-108">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooftp"></a><span data-ttu-id="3a313-109">Verbinding maken met tooFTP</span><span class="sxs-lookup"><span data-stu-id="3a313-109">Connect tooFTP</span></span>
<span data-ttu-id="3a313-110">Om uw logische app toegang alle services tot, moet u eerst toocreate een *verbinding* toohello service.</span><span class="sxs-lookup"><span data-stu-id="3a313-110">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="3a313-111">Een [verbinding](connectors-overview.md) biedt connectiviteit tussen een logische app en een andere service.</span><span class="sxs-lookup"><span data-stu-id="3a313-111">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-tooftp"></a><span data-ttu-id="3a313-112">Een tooFTP verbinding maken</span><span class="sxs-lookup"><span data-stu-id="3a313-112">Create a connection tooFTP</span></span>
> [!INCLUDE [Steps toocreate a connection tooFTP](../../includes/connectors-create-api-ftp.md)]
> 
> 

## <a name="use-a-ftp-trigger"></a><span data-ttu-id="3a313-113">Een FTP-trigger te gebruiken</span><span class="sxs-lookup"><span data-stu-id="3a313-113">Use a FTP trigger</span></span>
<span data-ttu-id="3a313-114">Een trigger is een gebeurtenis die gebruikt toostart Hallo werkstroom gedefinieerd in een logische app worden kan.</span><span class="sxs-lookup"><span data-stu-id="3a313-114">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="3a313-115">[Meer informatie over triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="3a313-115">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="3a313-116">Hallo FTP-connector vereist een FTP-server die toegankelijk is vanaf Internet Hallo en toooperate geconfigureerd met de passieve modus.</span><span class="sxs-lookup"><span data-stu-id="3a313-116">hello FTP connector requires an FTP server that  is accessible from hello Internet and is configured toooperate with PASSIVE mode.</span></span> <span data-ttu-id="3a313-117">Hallo FTP-connector is ook **niet compatibel met impliciete FTPS (FTP via SSL)**.</span><span class="sxs-lookup"><span data-stu-id="3a313-117">Also, hello FTP connector is **not compatible with implicit FTPS (FTP over SSL)**.</span></span> <span data-ttu-id="3a313-118">Hallo FTP-connector ondersteunt alleen expliciete FTPS (FTP via SSL).</span><span class="sxs-lookup"><span data-stu-id="3a313-118">hello FTP connector only supports explicit FTPS (FTP over SSL).</span></span>  
> 
> 

<span data-ttu-id="3a313-119">In dit voorbeeld, leest u hoe toouse hello **FTP - wanneer een bestand wordt toegevoegd of gewijzigd** tooinitiate een logic app-werkstroom wordt geactiveerd wanneer een bestand wordt toegevoegd aan of gewijzigd op een FTP-server.</span><span class="sxs-lookup"><span data-stu-id="3a313-119">In this example, I will show you how toouse hello **FTP - When a file is added or modified** trigger tooinitiate a logic app workflow when a file is added to, or modified on, an FTP server.</span></span> <span data-ttu-id="3a313-120">In een enterprise-voorbeeld: u kunt deze trigger toomonitor een FTP-map voor nieuwe bestanden die die de orders van klanten vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="3a313-120">In an enterprise example, you could use this trigger toomonitor an FTP folder for new files that represent orders from customers.</span></span>  <span data-ttu-id="3a313-121">U kunt vervolgens een FTP-connector actie, zoals **bestandsinhoud ophalen** tooget Hallo inhoud van Hallo order voor verdere verwerking en opslag in uw orderdatabase.</span><span class="sxs-lookup"><span data-stu-id="3a313-121">You could then use an FTP connector action such as **Get file content** tooget hello contents of hello order for further processing and storage in your orders database.</span></span>

1. <span data-ttu-id="3a313-122">Voer *ftp* Selecteer in het zoekvak Hallo op Hallo logic apps designer Hallo **FTP - wanneer een bestand wordt toegevoegd of gewijzigd** trigger</span><span class="sxs-lookup"><span data-stu-id="3a313-122">Enter *ftp* in hello search box on hello logic apps designer then select hello **FTP - When a file is added or modified**  trigger</span></span>   
   <span data-ttu-id="3a313-123">![FTP-triggerafbeelding 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)</span><span class="sxs-lookup"><span data-stu-id="3a313-123">![FTP trigger image 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)</span></span>  
   <span data-ttu-id="3a313-124">Hallo **wanneer een bestand wordt toegevoegd of gewijzigd** besturingselement wordt geopend</span><span class="sxs-lookup"><span data-stu-id="3a313-124">hello **When a file is added or modified** control opens up</span></span>  
   <span data-ttu-id="3a313-125">![FTP-triggerafbeelding 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)</span><span class="sxs-lookup"><span data-stu-id="3a313-125">![FTP trigger image 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)</span></span>  
2. <span data-ttu-id="3a313-126">Selecteer Hallo **...**  zich aan de rechterkant Hallo van Hallo-besturingselement.</span><span class="sxs-lookup"><span data-stu-id="3a313-126">Select hello **...** located on hello right side of hello control.</span></span> <span data-ttu-id="3a313-127">Hiermee opent u Hallo map kiezerbesturingselement</span><span class="sxs-lookup"><span data-stu-id="3a313-127">This opens hello folder picker control</span></span>  
   <span data-ttu-id="3a313-128">![FTP-triggerafbeelding 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)</span><span class="sxs-lookup"><span data-stu-id="3a313-128">![FTP trigger image 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)</span></span>  
3. <span data-ttu-id="3a313-129">Selecteer Hallo  **>**  (pijl naar rechts) en blader toofind Hallo map wilt u toomonitor voor nieuwe en gewijzigde bestanden.</span><span class="sxs-lookup"><span data-stu-id="3a313-129">Select hello **>** (right arrow) and browse toofind hello folder that you want toomonitor for new or modified files.</span></span> <span data-ttu-id="3a313-130">Selecteer Hallo-map en u ziet Hallo map wordt nu weergegeven in Hallo **map** besturingselement.</span><span class="sxs-lookup"><span data-stu-id="3a313-130">Select hello folder and notice hello folder is now displayed in hello **Folder** control.</span></span>  
   <span data-ttu-id="3a313-131">![FTP-triggerafbeelding 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)</span><span class="sxs-lookup"><span data-stu-id="3a313-131">![FTP trigger image 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)</span></span>   

<span data-ttu-id="3a313-132">Op dit moment is uw logische app geconfigureerd met een trigger die wordt gestart een uitvoering van Hallo andere triggers en acties in de werkstroom Hallo wanneer een bestand wordt gewijzigd of in Hallo specifieke FTP-map gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3a313-132">At this point, your logic app has been configured with a trigger that will begin a run of hello other triggers and actions in hello workflow when a file is either modified or created in hello specific FTP folder.</span></span> 

> [!NOTE]
> <span data-ttu-id="3a313-133">Voor een logische app toobe functionele, moet er ten minste één trigger en één actie bevatten.</span><span class="sxs-lookup"><span data-stu-id="3a313-133">For a logic app toobe functional, it must contain at least one trigger and one action.</span></span> <span data-ttu-id="3a313-134">Hallo stappen in de volgende sectie tooadd een actie van Hallo.</span><span class="sxs-lookup"><span data-stu-id="3a313-134">Follow hello steps in hello next section tooadd an action.</span></span>  
> 
> 

## <a name="use-a-ftp-action"></a><span data-ttu-id="3a313-135">Gebruik een FTP-actie</span><span class="sxs-lookup"><span data-stu-id="3a313-135">Use a FTP action</span></span>
<span data-ttu-id="3a313-136">Een actie is een bewerking uitgevoerd door Hallo werkstroom gedefinieerd in een logische app.</span><span class="sxs-lookup"><span data-stu-id="3a313-136">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="3a313-137">[Meer informatie over acties](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="3a313-137">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="3a313-138">Nu u een trigger hebt toegevoegd, volgt u deze stappen tooadd een actie die u krijgt Hallo inhoud van Hallo nieuwe of gewijzigde bestand door Hallo trigger gevonden.</span><span class="sxs-lookup"><span data-stu-id="3a313-138">Now that you have added a trigger, follow these steps tooadd an action that will get hello contents of hello new or modified file found by hello trigger.</span></span>    

1. <span data-ttu-id="3a313-139">Selecteer **+ een nieuwe stap** tooadd Hallo Hallo actie tooget Hallo inhoud van het Hallo-bestand op Hallo FTP-server</span><span class="sxs-lookup"><span data-stu-id="3a313-139">Select **+ New step** tooadd hello hello action tooget hello contents of hello file on hello FTP server</span></span>  
2. <span data-ttu-id="3a313-140">Selecteer Hallo **een actie toevoegen** koppeling.</span><span class="sxs-lookup"><span data-stu-id="3a313-140">Select hello **Add an action** link.</span></span>  
   <span data-ttu-id="3a313-141">![FTP-afbeelding 1](./media/connectors-create-api-ftp/ftp-action-1.png)</span><span class="sxs-lookup"><span data-stu-id="3a313-141">![FTP action image 1](./media/connectors-create-api-ftp/ftp-action-1.png)</span></span>  
3. <span data-ttu-id="3a313-142">Voer *FTP* toosearch voor alle acties tooFTP gerelateerd.</span><span class="sxs-lookup"><span data-stu-id="3a313-142">Enter *FTP* toosearch for all actions related tooFTP.</span></span>
4. <span data-ttu-id="3a313-143">Selecteer **FTP - bestandsinhoud ophalen** zoals actie tootake Hallo als een nieuwe of gewijzigde bestand wordt gevonden in Hallo FTP-map.</span><span class="sxs-lookup"><span data-stu-id="3a313-143">Select **FTP - Get file content**  as hello action tootake when a new or modified file is found in hello FTP folder.</span></span>      
   <span data-ttu-id="3a313-144">![FTP-afbeelding 2](./media/connectors-create-api-ftp/ftp-action-2.png)</span><span class="sxs-lookup"><span data-stu-id="3a313-144">![FTP action image 2](./media/connectors-create-api-ftp/ftp-action-2.png)</span></span>  
   <span data-ttu-id="3a313-145">Hallo **bestandsinhoud ophalen** beheren wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="3a313-145">hello **Get file content** control opens.</span></span> <span data-ttu-id="3a313-146">**Opmerking**: u na vragen aan gebruiker tooauthorize uw logische app tooaccess uw FTP-server als u nog niet gedaan eerder account zijn.</span><span class="sxs-lookup"><span data-stu-id="3a313-146">**Note**: you will be prompted tooauthorize your logic app tooaccess your FTP server account if you have not done so previously.</span></span>  
   <span data-ttu-id="3a313-147">![FTP-afbeelding 3](./media/connectors-create-api-ftp/ftp-action-3.png)</span><span class="sxs-lookup"><span data-stu-id="3a313-147">![FTP action image 3](./media/connectors-create-api-ftp/ftp-action-3.png)</span></span>   
5. <span data-ttu-id="3a313-148">Selecteer Hallo **bestand** besturingselement (Hallo witruimte zich onder **bestand***).</span><span class="sxs-lookup"><span data-stu-id="3a313-148">Select hello **File** control (hello white space located below **FILE***).</span></span> <span data-ttu-id="3a313-149">Hier kunt u een Hallo verschillende eigenschappen van Hallo nieuwe of gewijzigde bestand gevonden op Hallo FTP-server.</span><span class="sxs-lookup"><span data-stu-id="3a313-149">Here, you can use any of hello various properties from hello new or modified file found on hello FTP server.</span></span>  
6. <span data-ttu-id="3a313-150">Selecteer Hallo **inhoud bestand** optie.</span><span class="sxs-lookup"><span data-stu-id="3a313-150">Select hello **File content** option.</span></span>  
   <span data-ttu-id="3a313-151">![FTP-afbeelding 4](./media/connectors-create-api-ftp/ftp-action-4.png)</span><span class="sxs-lookup"><span data-stu-id="3a313-151">![FTP action image 4](./media/connectors-create-api-ftp/ftp-action-4.png)</span></span>   
7. <span data-ttu-id="3a313-152">Hallo-besturingselement wordt bijgewerkt, die aangeeft dat Hallo **FTP - bestandsinhoud ophalen** actie krijgt Hallo *inhoud bestand* van Hallo nieuwe of gewijzigde bestand op Hallo FTP-server.</span><span class="sxs-lookup"><span data-stu-id="3a313-152">hello control is updated, indicating that hello **FTP - Get file content** action will get hello *file content* of hello new or modified file on hello FTP server.</span></span>      
   <span data-ttu-id="3a313-153">![FTP-afbeelding 5](./media/connectors-create-api-ftp/ftp-action-5.png)</span><span class="sxs-lookup"><span data-stu-id="3a313-153">![FTP action image 5](./media/connectors-create-api-ftp/ftp-action-5.png)</span></span>     
8. <span data-ttu-id="3a313-154">Sla uw werk en vervolgens voegt u een bestand toohello FTP-map tootest uw werkstroom.</span><span class="sxs-lookup"><span data-stu-id="3a313-154">Save your work then add a file toohello FTP folder tootest your workflow.</span></span>    

<span data-ttu-id="3a313-155">Op dit moment Hallo logische app is geconfigureerd met een trigger toomonitor een map van een FTP-server en een werkstroom starten Hallo wanneer er een nieuw bestand of een gewijzigd bestand op Hallo FTP-server.</span><span class="sxs-lookup"><span data-stu-id="3a313-155">At this point, hello logic app has been configured with a trigger toomonitor a folder on an FTP server and initiate hello workflow when it finds either a new file or a modified file on hello FTP server.</span></span> 

<span data-ttu-id="3a313-156">Hallo logische app is ook geconfigureerd met een actie tooget Hallo inhoud van de nieuwe of gewijzigde bestand Hallo.</span><span class="sxs-lookup"><span data-stu-id="3a313-156">hello logic app also has been configured with an action tooget hello contents of hello new or modified file.</span></span>

<span data-ttu-id="3a313-157">U kunt nu een andere actie zoals Hallo toevoegen [SQL Server - invoegrij](connectors-create-api-sqlazure.md) actie tooinsert Hallo inhoud van Hallo nieuwe of gewijzigde bestand in een SQL-databasetabel.</span><span class="sxs-lookup"><span data-stu-id="3a313-157">You can now add another action such as hello [SQL Server - insert row](connectors-create-api-sqlazure.md) action tooinsert hello contents of hello new or modified file into a SQL database table.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="3a313-158">Connector-specifieke details</span><span class="sxs-lookup"><span data-stu-id="3a313-158">Connector-specific details</span></span>

<span data-ttu-id="3a313-159">Alle triggers en acties die zijn gedefinieerd in swagger Hallo bekijken en ook bekijken in Hallo beperkingen [connector details](/connectors/ftpconnector/).</span><span class="sxs-lookup"><span data-stu-id="3a313-159">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/ftpconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3a313-160">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3a313-160">Next Steps</span></span>
[<span data-ttu-id="3a313-161">Een logische app maken</span><span class="sxs-lookup"><span data-stu-id="3a313-161">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

