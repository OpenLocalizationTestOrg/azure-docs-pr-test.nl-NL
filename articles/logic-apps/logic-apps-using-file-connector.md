---
title: aaaConnect tooon-premises-bestandssystemen vanuit Azure Logic Apps | Microsoft Docs
description: Verbinding maken met lokale tooon bestandssystemen van uw werkstroom logic app via Hallo lokale gegevensgateway en File System-connector
keywords: Bestandssystemen
services: logic-apps
author: derek1ee
manager: anneta
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/27/2017
ms.author: LADocs; deli
ms.openlocfilehash: beb5565293def4aba81f63f19e77d7498aac38c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooon-premises-file-systems-from-logic-apps-with-hello-file-system-connector"></a><span data-ttu-id="639af-104">Verbinding maken met lokale tooon bestandssystemen vanuit logic apps met Hallo File System-connector</span><span class="sxs-lookup"><span data-stu-id="639af-104">Connect tooon-premises file systems from logic apps with hello File System connector</span></span>

<span data-ttu-id="639af-105">Hybride cloud-verbindingen is centrale toologic apps, gegevens in dat geval toomanage en veilig toegang tot on-premises resources, uw logische apps Hallo lokale gegevensgateway kunnen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="639af-105">Hybrid cloud connectivity is central toologic apps, so toomanage data and securely access on-premises resources, your logic apps can use hello on-premises data gateway.</span></span> <span data-ttu-id="639af-106">In dit artikel wordt gedemonstreerd hoe tooconnect tooan on-premises bestandssysteem met een eenvoudige scenario: Kopieer een bestand dat geüploade tooDropbox tooa bestandsshare en vervolgens een e-mailbericht verzenden.</span><span class="sxs-lookup"><span data-stu-id="639af-106">In this article, we show how tooconnect tooan on-premises file system with a basic scenario: copy a file that's uploaded tooDropbox tooa file share, then send an email.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="639af-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="639af-107">Prerequisites</span></span>

- <span data-ttu-id="639af-108">Installeer en configureer Hallo nieuwste [lokale gegevensgateway](https://www.microsoft.com/download/details.aspx?id=53127).</span><span class="sxs-lookup"><span data-stu-id="639af-108">Install and configure hello latest [on-premises data gateway](https://www.microsoft.com/download/details.aspx?id=53127).</span></span>
- <span data-ttu-id="639af-109">Hallo nieuwste lokale gegevensgateway installeren, versie 1.15.6150.1 of hoger.</span><span class="sxs-lookup"><span data-stu-id="639af-109">Install hello latest on-premises data gateway, version 1.15.6150.1 or above.</span></span> <span data-ttu-id="639af-110">[Verbinding maken met toohello lokale gegevensgateway](http://aka.ms/logicapps-gateway) lijsten Hallo stappen.</span><span class="sxs-lookup"><span data-stu-id="639af-110">[Connect toohello on-premises data gateway](http://aka.ms/logicapps-gateway) lists hello steps.</span></span> <span data-ttu-id="639af-111">Hallo-gateway moet worden geïnstalleerd op een on-premises machine voordat u kunt doorgaan met de rest Hallo van Hallo stappen.</span><span class="sxs-lookup"><span data-stu-id="639af-111">hello gateway must be installed on an on-premises machine before you can continue with hello rest of hello steps.</span></span>

## <a name="add-trigger-and-actions-for-connecting-tooyour-file-system"></a><span data-ttu-id="639af-112">Trigger en acties voor het verbinden van bestandssysteem tooyour toevoegen</span><span class="sxs-lookup"><span data-stu-id="639af-112">Add trigger and actions for connecting tooyour file system</span></span>

1. <span data-ttu-id="639af-113">Een logische app maken en deze Dropbox-trigger toevoegen: **wanneer een bestand wordt gemaakt**</span><span class="sxs-lookup"><span data-stu-id="639af-113">Create a logic app, and add this Dropbox trigger: **When a file is created**</span></span> 
2. <span data-ttu-id="639af-114">Kies onder Hallo-trigger **doornemen** > **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="639af-114">Under hello trigger, choose **Next Step** > **Add an action**.</span></span> 
3. <span data-ttu-id="639af-115">Voer in het zoekvak Hallo `file system` zodat u alle ondersteunde acties voor Hallo File System-connector kunt bekijken.</span><span class="sxs-lookup"><span data-stu-id="639af-115">In hello search box, enter `file system` so you can view all supported actions for hello File System connector.</span></span>

   ![Zoeken naar bestand connector](media/logic-apps-using-file-connector/search-file-connector.png)

2. <span data-ttu-id="639af-117">Kies Hallo **Create file** actie, en maak een verbinding tooyour-bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="639af-117">Choose hello **Create file** action, and create a connection tooyour file system.</span></span>

   <span data-ttu-id="639af-118">Als u een bestaande verbinding geen hebt, bent u na vragen aan gebruiker toocreate een.</span><span class="sxs-lookup"><span data-stu-id="639af-118">If you don't have an existing connection, you are prompted toocreate one.</span></span>

   1. <span data-ttu-id="639af-119">Kies **verbinden via lokale gegevensgateway**.</span><span class="sxs-lookup"><span data-stu-id="639af-119">Choose **Connect via on-premises data gateway**.</span></span> <span data-ttu-id="639af-120">Meer eigenschappen worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="639af-120">More properties appear.</span></span>
   2. <span data-ttu-id="639af-121">Selecteer de hoofdmap naar het bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="639af-121">Select your root folder for your file system.</span></span>
      
       > [!NOTE]
       > <span data-ttu-id="639af-122">Er is een fout opgetreden in de hoofdmap Hallo Hallo belangrijkste bovenliggende map, die wordt gebruikt voor het relatieve paden voor alle bestand-gerelateerde acties.</span><span class="sxs-lookup"><span data-stu-id="639af-122">hello root folder is hello main parent folder, which is used for relative paths for all file-related actions.</span></span> <span data-ttu-id="639af-123">U kunt een lokale map op de machine Hallo waarbij Hallo lokale data gateway is geïnstalleerd of Hallo map kan zich een netwerkshare die Hallo machine toegang heeft tot opgeven.</span><span class="sxs-lookup"><span data-stu-id="639af-123">You can specify a local folder on hello machine where hello on-premises data gateway is installed, or hello folder can be a network share that hello machine can access.</span></span>

   3. <span data-ttu-id="639af-124">Hallo-gebruikersnaam en wachtwoord invoeren voor Hallo-gateway.</span><span class="sxs-lookup"><span data-stu-id="639af-124">Enter hello username and password for hello gateway.</span></span>
   4. <span data-ttu-id="639af-125">Selecteer Hallo-gateway die u eerder hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="639af-125">Select hello gateway that you previously installed.</span></span>

       ![Configureer de verbinding](media/logic-apps-using-file-connector/create-file.png)

3. <span data-ttu-id="639af-127">Nadat u alle Hallo gegevens verstrekken, kiest u **maken**.</span><span class="sxs-lookup"><span data-stu-id="639af-127">After you provide all hello details, choose **Create**.</span></span> 

   <span data-ttu-id="639af-128">Logic Apps configureert en test uw verbinding, om ervoor te zorgen dat connection Hallo goed werkt.</span><span class="sxs-lookup"><span data-stu-id="639af-128">Logic Apps configures and tests your connection, making sure that hello connection works properly.</span></span> 
   <span data-ttu-id="639af-129">Als het Hallo-verbinding juist is ingesteld, ziet u opties voor het Hallo-actie die u eerder hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="639af-129">If hello connection is set up correctly, you see options for hello action that you previously selected.</span></span> 
   <span data-ttu-id="639af-130">Hallo file system-connector is nu klaar voor gebruik.</span><span class="sxs-lookup"><span data-stu-id="639af-130">hello file system connector is now ready for use.</span></span>

4. <span data-ttu-id="639af-131">Opgeven dat u toocopy bestanden vanuit Dropbox toohello-hoofdmap voor uw lokale bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="639af-131">Specify that you want toocopy files from Dropbox toohello root folder for your on-premises file share.</span></span>

   ![Bestandsactie maken](media/logic-apps-using-file-connector/create-file-filled.png)

5. <span data-ttu-id="639af-133">Na uw logische app kopieën Hallo-bestand toevoegen een Outlook-actie die een e-mailbericht verzendt, zodat relevante gebruikers over nieuwe Hallo-bestand weten.</span><span class="sxs-lookup"><span data-stu-id="639af-133">After your logic app copies hello file, add an Outlook action that sends an email so relevant users know about hello new file.</span></span> <span data-ttu-id="639af-134">Hallo ontvangers, titel en hoofdtekst Hallo e-mailadres invoeren.</span><span class="sxs-lookup"><span data-stu-id="639af-134">Enter hello recipients, title, and body of hello email.</span></span> 

   <span data-ttu-id="639af-135">In dynamische inhoud selector hello, kunt u uitvoer van de gegevens van Hallo bestand-connector zodat u meer details toohello e kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="639af-135">In hello dynamic content selector, you can choose data outputs from hello file connector so you can add more details toohello email.</span></span>

   ![Verzenden van e-actie](media/logic-apps-using-file-connector/send-email.png)

6. <span data-ttu-id="639af-137">Sla uw logische app.</span><span class="sxs-lookup"><span data-stu-id="639af-137">Save your logic app.</span></span> <span data-ttu-id="639af-138">Uw app testen door een tooDropbox bestand uploaden.</span><span class="sxs-lookup"><span data-stu-id="639af-138">Test your app by uploading a file tooDropbox.</span></span> <span data-ttu-id="639af-139">Hallo-bestand krijgt de gekopieerde toohello lokale bestandsshare en u ontvangt een e-mailbericht over Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="639af-139">hello file should get copied toohello on-premises file share, and you should receive an email about hello operation.</span></span>

   > [!TIP] 
   > <span data-ttu-id="639af-140">Meer informatie over hoe te[uw logische apps bewaken](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="639af-140">Learn how too[monitor your logic apps](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span></span>

<span data-ttu-id="639af-141">Gefeliciteerd, u hebt nu een werkende logische app die verbinding van tooyour on-premises bestandssysteem maken kan.</span><span class="sxs-lookup"><span data-stu-id="639af-141">Congratulations, you now have a working logic app that can connect tooyour on-premises file system.</span></span> <span data-ttu-id="639af-142">Probeer een andere functionaliteiten die connector biedt, bijvoorbeeld Hallo verkennen:</span><span class="sxs-lookup"><span data-stu-id="639af-142">Try exploring other functionalities that hello connector offers, for example:</span></span>

- <span data-ttu-id="639af-143">Bestand maken</span><span class="sxs-lookup"><span data-stu-id="639af-143">Create file</span></span>
- <span data-ttu-id="639af-144">Bestanden in de map weergeven</span><span class="sxs-lookup"><span data-stu-id="639af-144">List files in folder</span></span>
- <span data-ttu-id="639af-145">Bestand toevoegen</span><span class="sxs-lookup"><span data-stu-id="639af-145">Append file</span></span>
- <span data-ttu-id="639af-146">Bestand verwijderen</span><span class="sxs-lookup"><span data-stu-id="639af-146">Delete file</span></span>
- <span data-ttu-id="639af-147">Bestandsinhoud ophalen</span><span class="sxs-lookup"><span data-stu-id="639af-147">Get file content</span></span>
- <span data-ttu-id="639af-148">Bestandsinhoud ophalen via het pad</span><span class="sxs-lookup"><span data-stu-id="639af-148">Get file content using path</span></span>
- <span data-ttu-id="639af-149">Ophalen van metagegevens van bestand</span><span class="sxs-lookup"><span data-stu-id="639af-149">Get file metadata</span></span>
- <span data-ttu-id="639af-150">De metagegevens van het bestand ophalen via het pad</span><span class="sxs-lookup"><span data-stu-id="639af-150">Get file metadata using path</span></span>
- <span data-ttu-id="639af-151">Bestanden in de hoofdmap weergeven</span><span class="sxs-lookup"><span data-stu-id="639af-151">List files in root folder</span></span>
- <span data-ttu-id="639af-152">Bestand bijwerken</span><span class="sxs-lookup"><span data-stu-id="639af-152">Update file</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="639af-153">Weergave Hallo swagger</span><span class="sxs-lookup"><span data-stu-id="639af-153">View hello swagger</span></span>
<span data-ttu-id="639af-154">Zie Hallo [swagger details](/connectors/fileconnector/).</span><span class="sxs-lookup"><span data-stu-id="639af-154">See hello [swagger details](/connectors/fileconnector/).</span></span> 

## <a name="get-help"></a><span data-ttu-id="639af-155">Help opvragen</span><span class="sxs-lookup"><span data-stu-id="639af-155">Get help</span></span>

<span data-ttu-id="639af-156">tooask vragen beantwoorden van vragen en meer informatie over welke andere Azure Logic Apps gebruikers doen, gaat u naar Hallo [Azure Logic Apps-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="639af-156">tooask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="639af-157">toohelp Azure Logic Apps en connectors verbeteren, stem of ideeën op Hallo indienen [Azure Logic Apps gebruiker feedback site](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="639af-157">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="639af-158">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="639af-158">Next steps</span></span>

- <span data-ttu-id="639af-159">[Verbinding maken met tooon-premises gegevens](../logic-apps/logic-apps-gateway-connection.md) vanuit logic apps</span><span class="sxs-lookup"><span data-stu-id="639af-159">[Connect tooon-premises data](../logic-apps/logic-apps-gateway-connection.md) from logic apps</span></span>
- <span data-ttu-id="639af-160">Meer informatie over [integratie in de onderneming](../logic-apps/logic-apps-enterprise-integration-overview.md)</span><span class="sxs-lookup"><span data-stu-id="639af-160">Learn about [enterprise integration](../logic-apps/logic-apps-enterprise-integration-overview.md)</span></span>
