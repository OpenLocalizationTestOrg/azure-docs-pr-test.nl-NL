---
title: Informatie over het gebruik van de FTP-connector in logic apps | Microsoft Docs
description: Logic apps maken met Azure App service. Verbinding maken met de FTP-server om uw bestanden te beheren. U kunt uitvoeren van verschillende acties zoals het uploaden, bijwerken, ophalen en verwijderen van bestanden in de FTP-server.
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
ms.openlocfilehash: 61bfbedfd4f1e84b6976099323a32f3a720634c0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-ftp-connector"></a><span data-ttu-id="07f31-105">Aan de slag met de FTP-connector</span><span class="sxs-lookup"><span data-stu-id="07f31-105">Get started with the FTP connector</span></span>
<span data-ttu-id="07f31-106">De FTP-connector gebruiken om te controleren, beheren en bestanden op een FTP-server maken.</span><span class="sxs-lookup"><span data-stu-id="07f31-106">Use the FTP connector to monitor, manage and create files on an  FTP server.</span></span> 

<span data-ttu-id="07f31-107">Gebruik [elke connector](apis-list.md), moet u eerst een logische app maken.</span><span class="sxs-lookup"><span data-stu-id="07f31-107">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="07f31-108">U kunt aan de slag door [maken van een logische app nu](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="07f31-108">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-ftp"></a><span data-ttu-id="07f31-109">Verbinding maken met FTP</span><span class="sxs-lookup"><span data-stu-id="07f31-109">Connect to FTP</span></span>
<span data-ttu-id="07f31-110">Om uw logische app toegang alle services tot, moet u eerst maken een *verbinding* naar de service.</span><span class="sxs-lookup"><span data-stu-id="07f31-110">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="07f31-111">Een [verbinding](connectors-overview.md) biedt connectiviteit tussen een logische app en een andere service.</span><span class="sxs-lookup"><span data-stu-id="07f31-111">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-ftp"></a><span data-ttu-id="07f31-112">Maak een verbinding met FTP</span><span class="sxs-lookup"><span data-stu-id="07f31-112">Create a connection to FTP</span></span>
> [!INCLUDE [Steps to create a connection to FTP](../../includes/connectors-create-api-ftp.md)]
> 
> 

## <a name="use-a-ftp-trigger"></a><span data-ttu-id="07f31-113">Een FTP-trigger te gebruiken</span><span class="sxs-lookup"><span data-stu-id="07f31-113">Use a FTP trigger</span></span>
<span data-ttu-id="07f31-114">Een trigger is een gebeurtenis die kan worden gebruikt om de werkstroom die is gedefinieerd in een logische app te starten.</span><span class="sxs-lookup"><span data-stu-id="07f31-114">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="07f31-115">[Meer informatie over triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="07f31-115">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="07f31-116">De FTP-connector vereist een FTP-server die toegankelijk is vanaf het Internet en is geconfigureerd voor het werken met de passieve modus.</span><span class="sxs-lookup"><span data-stu-id="07f31-116">The FTP connector requires an FTP server that  is accessible from the Internet and is configured to operate with PASSIVE mode.</span></span> <span data-ttu-id="07f31-117">De FTP-connector is ook **niet compatibel met impliciete FTPS (FTP via SSL)**.</span><span class="sxs-lookup"><span data-stu-id="07f31-117">Also, the FTP connector is **not compatible with implicit FTPS (FTP over SSL)**.</span></span> <span data-ttu-id="07f31-118">De FTP-connector ondersteunt alleen expliciete FTPS (FTP via SSL).</span><span class="sxs-lookup"><span data-stu-id="07f31-118">The FTP connector only supports explicit FTPS (FTP over SSL).</span></span>  
> 
> 

<span data-ttu-id="07f31-119">In dit voorbeeld leest u het gebruik van de **FTP - wanneer een bestand wordt toegevoegd of gewijzigd** activeren voor het initiëren van een logische app werkstroom wanneer een bestand wordt toegevoegd aan of gewijzigd op een FTP-server.</span><span class="sxs-lookup"><span data-stu-id="07f31-119">In this example, I will show you how to use the **FTP - When a file is added or modified** trigger to initiate a logic app workflow when a file is added to, or modified on, an FTP server.</span></span> <span data-ttu-id="07f31-120">In een enterprise-voorbeeld: u kunt deze trigger voor het bewaken van een FTP-map voor nieuwe bestanden die die de orders van klanten vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="07f31-120">In an enterprise example, you could use this trigger to monitor an FTP folder for new files that represent orders from customers.</span></span>  <span data-ttu-id="07f31-121">U kunt vervolgens een FTP-connector actie, zoals **bestandsinhoud ophalen** ophalen van de inhoud van de volgorde voor verdere verwerking en opslag in uw orderdatabase.</span><span class="sxs-lookup"><span data-stu-id="07f31-121">You could then use an FTP connector action such as **Get file content** to get the contents of the order for further processing and storage in your orders database.</span></span>

1. <span data-ttu-id="07f31-122">Voer *ftp* in het zoekvak op de ontwerpfunctie van logic apps selecteert u vervolgens de **FTP - wanneer een bestand wordt toegevoegd of gewijzigd** trigger</span><span class="sxs-lookup"><span data-stu-id="07f31-122">Enter *ftp* in the search box on the logic apps designer then select the **FTP - When a file is added or modified**  trigger</span></span>   
   <span data-ttu-id="07f31-123">![FTP-triggerafbeelding 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)</span><span class="sxs-lookup"><span data-stu-id="07f31-123">![FTP trigger image 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)</span></span>  
   <span data-ttu-id="07f31-124">De **wanneer een bestand wordt toegevoegd of gewijzigd** besturingselement wordt geopend</span><span class="sxs-lookup"><span data-stu-id="07f31-124">The **When a file is added or modified** control opens up</span></span>  
   <span data-ttu-id="07f31-125">![FTP-triggerafbeelding 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)</span><span class="sxs-lookup"><span data-stu-id="07f31-125">![FTP trigger image 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)</span></span>  
2. <span data-ttu-id="07f31-126">Selecteer de **...**  zich aan de rechterkant van het besturingselement.</span><span class="sxs-lookup"><span data-stu-id="07f31-126">Select the **...** located on the right side of the control.</span></span> <span data-ttu-id="07f31-127">Hiermee opent u het kiezerbesturingselement map</span><span class="sxs-lookup"><span data-stu-id="07f31-127">This opens the folder picker control</span></span>  
   <span data-ttu-id="07f31-128">![FTP-triggerafbeelding 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)</span><span class="sxs-lookup"><span data-stu-id="07f31-128">![FTP trigger image 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)</span></span>  
3. <span data-ttu-id="07f31-129">Selecteer de  **>**  (pijl naar rechts) en Ga naar de map die u wilt controleren op nieuwe en gewijzigde bestanden.</span><span class="sxs-lookup"><span data-stu-id="07f31-129">Select the **>** (right arrow) and browse to find the folder that you want to monitor for new or modified files.</span></span> <span data-ttu-id="07f31-130">Selecteer de map en u ziet dat de map wordt nu weergegeven in de **map** besturingselement.</span><span class="sxs-lookup"><span data-stu-id="07f31-130">Select the folder and notice the folder is now displayed in the **Folder** control.</span></span>  
   <span data-ttu-id="07f31-131">![FTP-triggerafbeelding 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)</span><span class="sxs-lookup"><span data-stu-id="07f31-131">![FTP trigger image 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)</span></span>   

<span data-ttu-id="07f31-132">Op dit moment is uw logische app geconfigureerd met een trigger die een uitvoering van de andere triggers en acties in de werkstroom wordt gestart wanneer een bestand wordt gewijzigd of in een specifieke FTP-map gemaakt.</span><span class="sxs-lookup"><span data-stu-id="07f31-132">At this point, your logic app has been configured with a trigger that will begin a run of the other triggers and actions in the workflow when a file is either modified or created in the specific FTP folder.</span></span> 

> [!NOTE]
> <span data-ttu-id="07f31-133">Voor een logische app wilt gebruiken, moet er ten minste één trigger en één actie bevatten.</span><span class="sxs-lookup"><span data-stu-id="07f31-133">For a logic app to be functional, it must contain at least one trigger and one action.</span></span> <span data-ttu-id="07f31-134">Volg de stappen in de volgende sectie voor een actie toevoegen.</span><span class="sxs-lookup"><span data-stu-id="07f31-134">Follow the steps in the next section to add an action.</span></span>  
> 
> 

## <a name="use-a-ftp-action"></a><span data-ttu-id="07f31-135">Gebruik een FTP-actie</span><span class="sxs-lookup"><span data-stu-id="07f31-135">Use a FTP action</span></span>
<span data-ttu-id="07f31-136">Een actie is een bewerking uitgevoerd door de werkstroom die is gedefinieerd in een logische app.</span><span class="sxs-lookup"><span data-stu-id="07f31-136">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="07f31-137">[Meer informatie over acties](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="07f31-137">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="07f31-138">Nu dat u een trigger hebt toegevoegd, volg deze stappen uit om een actie die u krijgt de inhoud van de nieuwe of gewijzigde bestand gevonden door de trigger.</span><span class="sxs-lookup"><span data-stu-id="07f31-138">Now that you have added a trigger, follow these steps to add an action that will get the contents of the new or modified file found by the trigger.</span></span>    

1. <span data-ttu-id="07f31-139">Selecteer **+ een nieuwe stap** toevoegen de de actie voor het ophalen van de inhoud van het bestand op de FTP-server</span><span class="sxs-lookup"><span data-stu-id="07f31-139">Select **+ New step** to add the the action to get the contents of the file on the FTP server</span></span>  
2. <span data-ttu-id="07f31-140">Selecteer de **een actie toevoegen** koppeling.</span><span class="sxs-lookup"><span data-stu-id="07f31-140">Select the **Add an action** link.</span></span>  
   <span data-ttu-id="07f31-141">![FTP-afbeelding 1](./media/connectors-create-api-ftp/ftp-action-1.png)</span><span class="sxs-lookup"><span data-stu-id="07f31-141">![FTP action image 1](./media/connectors-create-api-ftp/ftp-action-1.png)</span></span>  
3. <span data-ttu-id="07f31-142">Voer *FTP* om te zoeken naar alle acties met betrekking tot FTP.</span><span class="sxs-lookup"><span data-stu-id="07f31-142">Enter *FTP* to search for all actions related to FTP.</span></span>
4. <span data-ttu-id="07f31-143">Selecteer **FTP - bestandsinhoud ophalen** als de actie moet worden uitgevoerd wanneer een nieuwe of gewijzigde bestand wordt gevonden in de FTP-map.</span><span class="sxs-lookup"><span data-stu-id="07f31-143">Select **FTP - Get file content**  as the action to take when a new or modified file is found in the FTP folder.</span></span>      
   <span data-ttu-id="07f31-144">![FTP-afbeelding 2](./media/connectors-create-api-ftp/ftp-action-2.png)</span><span class="sxs-lookup"><span data-stu-id="07f31-144">![FTP action image 2](./media/connectors-create-api-ftp/ftp-action-2.png)</span></span>  
   <span data-ttu-id="07f31-145">De **bestandsinhoud ophalen** beheren wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="07f31-145">The **Get file content** control opens.</span></span> <span data-ttu-id="07f31-146">**Opmerking**: u wordt gevraagd uw logische app toegang tot uw FTP-server-serviceaccount als u nog niet gedaan eerder autoriseren.</span><span class="sxs-lookup"><span data-stu-id="07f31-146">**Note**: you will be prompted to authorize your logic app to access your FTP server account if you have not done so previously.</span></span>  
   <span data-ttu-id="07f31-147">![FTP-afbeelding 3](./media/connectors-create-api-ftp/ftp-action-3.png)</span><span class="sxs-lookup"><span data-stu-id="07f31-147">![FTP action image 3](./media/connectors-create-api-ftp/ftp-action-3.png)</span></span>   
5. <span data-ttu-id="07f31-148">Selecteer de **bestand** control (de witruimte zich onder **bestand***).</span><span class="sxs-lookup"><span data-stu-id="07f31-148">Select the **File** control (the white space located below **FILE***).</span></span> <span data-ttu-id="07f31-149">Hier kunt u een van de verschillende eigenschappen van de nieuwe of gewijzigde bestand gevonden op de FTP-server.</span><span class="sxs-lookup"><span data-stu-id="07f31-149">Here, you can use any of the various properties from the new or modified file found on the FTP server.</span></span>  
6. <span data-ttu-id="07f31-150">Selecteer de **inhoud bestand** optie.</span><span class="sxs-lookup"><span data-stu-id="07f31-150">Select the **File content** option.</span></span>  
   <span data-ttu-id="07f31-151">![FTP-afbeelding 4](./media/connectors-create-api-ftp/ftp-action-4.png)</span><span class="sxs-lookup"><span data-stu-id="07f31-151">![FTP action image 4](./media/connectors-create-api-ftp/ftp-action-4.png)</span></span>   
7. <span data-ttu-id="07f31-152">Het besturingselement wordt bijgewerkt, ten teken dat de **FTP - bestandsinhoud ophalen** actie krijgt de *inhoud bestand* van het bestand nieuw of gewijzigd op de FTP-server.</span><span class="sxs-lookup"><span data-stu-id="07f31-152">The control is updated, indicating that the **FTP - Get file content** action will get the *file content* of the new or modified file on the FTP server.</span></span>      
   <span data-ttu-id="07f31-153">![FTP-afbeelding 5](./media/connectors-create-api-ftp/ftp-action-5.png)</span><span class="sxs-lookup"><span data-stu-id="07f31-153">![FTP action image 5](./media/connectors-create-api-ftp/ftp-action-5.png)</span></span>     
8. <span data-ttu-id="07f31-154">Sla uw werk op en voeg vervolgens een bestand naar de FTP-map voor het testen van uw werkstroom.</span><span class="sxs-lookup"><span data-stu-id="07f31-154">Save your work then add a file to the FTP folder to test your workflow.</span></span>    

<span data-ttu-id="07f31-155">De logische app op dit moment is geconfigureerd met een trigger voor het bewaken van een map op een FTP-server en de werkstroom starten als er een nieuw bestand of een gewijzigd bestand op de FTP-server.</span><span class="sxs-lookup"><span data-stu-id="07f31-155">At this point, the logic app has been configured with a trigger to monitor a folder on an FTP server and initiate the workflow when it finds either a new file or a modified file on the FTP server.</span></span> 

<span data-ttu-id="07f31-156">De logische app is ook geconfigureerd met een actie om op te halen van de inhoud van het bestand nieuw of gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="07f31-156">The logic app also has been configured with an action to get the contents of the new or modified file.</span></span>

<span data-ttu-id="07f31-157">U kunt nu een andere actie, zoals toevoegen de [SQL Server - invoegrij](connectors-create-api-sqlazure.md) actie de inhoud van het bestand nieuw of gewijzigd in een tabel met SQL-database invoegen.</span><span class="sxs-lookup"><span data-stu-id="07f31-157">You can now add another action such as the [SQL Server - insert row](connectors-create-api-sqlazure.md) action to insert the contents of the new or modified file into a SQL database table.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="07f31-158">Connector-specifieke details</span><span class="sxs-lookup"><span data-stu-id="07f31-158">Connector-specific details</span></span>

<span data-ttu-id="07f31-159">Alle triggers en acties die zijn gedefinieerd in de swagger bekijken en ziet u ook de beperkingen in de [connector details](/connectors/ftpconnector/).</span><span class="sxs-lookup"><span data-stu-id="07f31-159">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/ftpconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="07f31-160">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="07f31-160">Next Steps</span></span>
[<span data-ttu-id="07f31-161">Een logische app maken</span><span class="sxs-lookup"><span data-stu-id="07f31-161">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

