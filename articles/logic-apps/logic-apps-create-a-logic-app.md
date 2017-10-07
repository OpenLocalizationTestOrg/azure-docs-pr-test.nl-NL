---
title: aaaCreate uw eerste werkstroom tussen cloud-apps & cloudservices - Azure Logic Apps | Microsoft Docs
description: Bedrijfsprocessen voor systeemintegratie en EAI-scenario's (Enterprise Application Integration) automatiseren door werkstromen te maken en uit te voeren in Azure Logic Apps
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
keywords: werkstroom, cloud-apps, cloudservices, bedrijfsprocessen, systeemintegratie, enterprise application integration, EAI
documentationcenter: 
ms.assetid: ce3582b5-9c58-4637-9379-75ff99878dcd
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/31/2017
ms.author: LADocs; jehollan; estfan
ms.openlocfilehash: 17ec589b1c8923b5ad3e6479fc856b6ac81754ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-logic-app-workflow-tooautomate-processes-between-cloud-apps-and-cloud-services"></a><span data-ttu-id="364e6-104">Uw eerste logische app tooautomate workflowprocessen tussen cloud-apps en cloudservices maken</span><span class="sxs-lookup"><span data-stu-id="364e6-104">Create your first logic app workflow tooautomate processes between cloud apps and cloud services</span></span>

<span data-ttu-id="364e6-105">Zonder dat u code hoeft te schrijven, kunt u bedrijfsprocessen eenvoudiger en sneller automatiseren door werkstromen te maken en uit te voeren met [Azure Logic Apps](logic-apps-what-are-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="364e6-105">Without writing any code, you can automate business processes more easily and quickly when you create and run workflows with [Azure Logic Apps](logic-apps-what-are-logic-apps.md).</span></span> <span data-ttu-id="364e6-106">Het eerste voorbeeld ziet hoe toocreate een basic logic app-werkstroom waarmee wordt gecontroleerd of een RSS-feed voor nieuwe inhoud op een website.</span><span class="sxs-lookup"><span data-stu-id="364e6-106">This first example shows how toocreate a basic logic app workflow that checks an RSS feed for new content on a website.</span></span> <span data-ttu-id="364e6-107">Wanneer nieuwe items worden weergegeven in de feed Hallo-website, verzendt Hallo logische app e-mail van een account met Outlook of Gmail.</span><span class="sxs-lookup"><span data-stu-id="364e6-107">When new items appear in hello website's feed, hello logic app sends email from an Outlook or Gmail account.</span></span>

<span data-ttu-id="364e6-108">toocreate en voer een logische app, moet u deze items:</span><span class="sxs-lookup"><span data-stu-id="364e6-108">toocreate and run a logic app, you need these items:</span></span>

* <span data-ttu-id="364e6-109">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="364e6-109">An Azure subscription.</span></span> <span data-ttu-id="364e6-110">Als u geen abonnement hebt, kunt u [beginnen met een gratis Azure-account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="364e6-110">If you don't have a subscription, you can [start with a free Azure account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="364e6-111">U kunt eventueel ook direct kiezen voor [een Betalen per gebruik-abonnement](https://azure.microsoft.com/pricing/purchase-options/).</span><span class="sxs-lookup"><span data-stu-id="364e6-111">Otherwise, you can [sign up for a Pay-As-You-Go subscription](https://azure.microsoft.com/pricing/purchase-options/).</span></span>

  <span data-ttu-id="364e6-112">Uw Azure-abonnement wordt gebruikt voor facturering van het gebruik van de logische app.</span><span class="sxs-lookup"><span data-stu-id="364e6-112">Your Azure subscription is used for billing logic app usage.</span></span> <span data-ttu-id="364e6-113">Lees hier meer informatie over [meten van gebruik](../logic-apps/logic-apps-pricing.md) en [prijzen](https://azure.microsoft.com/pricing/details/logic-apps) voor Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="364e6-113">Learn how [usage metering](../logic-apps/logic-apps-pricing.md) and [pricing](https://azure.microsoft.com/pricing/details/logic-apps) work for Azure Logic Apps.</span></span>

<span data-ttu-id="364e6-114">Verder zijn nog deze items nodig voor het voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="364e6-114">Also, this example requires these items:</span></span>

* <span data-ttu-id="364e6-115">Een account van Outlook.com, Office 365 Outlook of Gmail</span><span class="sxs-lookup"><span data-stu-id="364e6-115">An Outlook.com, Office 365 Outlook, or Gmail account</span></span>

    > [!TIP]
    > <span data-ttu-id="364e6-116">Als u een persoonlijk [Microsoft-account](https://account.microsoft.com/account) hebt, beschikt u over een Outlook.com-account.</span><span class="sxs-lookup"><span data-stu-id="364e6-116">If you have a personal [Microsoft account](https://account.microsoft.com/account), you have an Outlook.com account.</span></span> <span data-ttu-id="364e6-117">Als u een werk- of schoolaccount hebt van Azure, hebt u een **Office 365 Outlook**-account.</span><span class="sxs-lookup"><span data-stu-id="364e6-117">Otherwise, if you have an Azure work or school account, you have an **Office 365 Outlook** account.</span></span>

* <span data-ttu-id="364e6-118">Een koppeling tooa van de website RSS-feed.</span><span class="sxs-lookup"><span data-stu-id="364e6-118">A link tooa website's RSS feed.</span></span> <span data-ttu-id="364e6-119">In dit voorbeeld wordt Hallo [RSS-feed voor bovenste artikelen van Hallo CNN.com website](http://rss.cnn.com/rss/cnn_topstories.rss):`http://rss.cnn.com/rss/cnn_topstories.rss`</span><span class="sxs-lookup"><span data-stu-id="364e6-119">This example uses hello [RSS feed for top stories from hello CNN.com website](http://rss.cnn.com/rss/cnn_topstories.rss): `http://rss.cnn.com/rss/cnn_topstories.rss`</span></span>

## <a name="add-a-trigger-that-starts-your-workflow"></a><span data-ttu-id="364e6-120">Een trigger toevoegen voor het starten van de werkstroom</span><span class="sxs-lookup"><span data-stu-id="364e6-120">Add a trigger that starts your workflow</span></span>

<span data-ttu-id="364e6-121">Een [ *trigger* ](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is een gebeurtenis die uw logische app werkstroom start en eerste Hallo-item die behoeften van uw logische app.</span><span class="sxs-lookup"><span data-stu-id="364e6-121">A [*trigger*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is an event that starts your logic app workflow and is hello first item that your logic app needs.</span></span>

1. <span data-ttu-id="364e6-122">Meld u aan toohello [Azure-portal](https://portal.azure.com "Azure-portal").</span><span class="sxs-lookup"><span data-stu-id="364e6-122">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span>

2. <span data-ttu-id="364e6-123">Kies in het linkermenu Hallo **nieuw** > **Enterprise Integration** > **logische App** als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="364e6-123">From hello left menu, choose **New** > **Enterprise Integration** > **Logic App** as shown here:</span></span>

     ![Azure Portal, Nieuw, Enterprise Integration, Logische app](media/logic-apps-create-a-logic-app/azure-portal-create-logic-app.png)

   > [!TIP]
   > <span data-ttu-id="364e6-125">U kunt ook **nieuw**, typt u vervolgens in het zoekvak Hallo `logic app`, en druk op Enter.</span><span class="sxs-lookup"><span data-stu-id="364e6-125">You can also choose **New**, then in hello search box, type `logic app`, and press Enter.</span></span> <span data-ttu-id="364e6-126">Kies vervolgens **Logische app** > **Maken**.</span><span class="sxs-lookup"><span data-stu-id="364e6-126">Then choose **Logic App** > **Create**.</span></span>

3. <span data-ttu-id="364e6-127">Voer een naam in voor de logische app en selecteer uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="364e6-127">Name your logic app and select your Azure subscription.</span></span> <span data-ttu-id="364e6-128">Maak of selecteer vervolgens een Azure-resourcegroep, zodat u gerelateerde Azure-resources makkelijker kunt organiseren en beheren.</span><span class="sxs-lookup"><span data-stu-id="364e6-128">Now create or select an Azure resource group, which helps you organize and manage related Azure resources.</span></span> <span data-ttu-id="364e6-129">Ten slotte Selecteer Hallo datacenter locatie voor het hosten van uw logische app.</span><span class="sxs-lookup"><span data-stu-id="364e6-129">Finally, select hello datacenter location for hosting your logic app.</span></span> <span data-ttu-id="364e6-130">Als u klaar bent, kiest u **pincode toodashboard** en vervolgens **maken**.</span><span class="sxs-lookup"><span data-stu-id="364e6-130">When you're ready, choose **Pin toodashboard** and then **Create**.</span></span>

     ![Details van logische app](media/logic-apps-create-a-logic-app/logic-app-settings.png)

   > [!NOTE]
   > <span data-ttu-id="364e6-132">Wanneer u selecteert **pincode toodashboard**, uw logische app wordt weergegeven op Hallo Azure-dashboard na de implementatie en wordt automatisch geopend.</span><span class="sxs-lookup"><span data-stu-id="364e6-132">When you select **Pin toodashboard**, your logic app appears on hello Azure dashboard after deployment, and opens automatically.</span></span> <span data-ttu-id="364e6-133">Als uw logische app niet wordt weergegeven op Hallo-dashboard op Hallo **alle resources** tegel, kiest u **meer**, en selecteer uw logische app.</span><span class="sxs-lookup"><span data-stu-id="364e6-133">If your logic app doesn't appear on hello dashboard, on hello **All resources** tile, choose **See More**, and select your logic app.</span></span> <span data-ttu-id="364e6-134">Of Kies op Hallo linkermenu **meer services**.</span><span class="sxs-lookup"><span data-stu-id="364e6-134">Or on hello left menu, choose **More services**.</span></span> <span data-ttu-id="364e6-135">Kies vervolgens **Logische apps** onder **Enterprise Integration** en selecteer dan de logische app.</span><span class="sxs-lookup"><span data-stu-id="364e6-135">Under **Enterprise Integration**, choose **Logic Apps**, and select your logic app.</span></span>

4. <span data-ttu-id="364e6-136">Wanneer u uw logische app voor Hallo eerste keer opent, ziet Hallo Logic App-ontwerper voor sjablonen waarmee u tooget gestart kunt.</span><span class="sxs-lookup"><span data-stu-id="364e6-136">When you open your logic app for hello first time, hello Logic App Designer shows templates that you can use tooget started.</span></span> <span data-ttu-id="364e6-137">Kies voor dit voorbeeld **Lege logische app**, zodat u de logische app helemaal zelf kunt ontwerpen.</span><span class="sxs-lookup"><span data-stu-id="364e6-137">For now, choose **Blank Logic App** so you can build your logic app from scratch.</span></span>

    <span data-ttu-id="364e6-138">Hallo Logic App-ontwerper wordt geopend en ziet u beschikbare services en *triggers* die u in uw logische app kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="364e6-138">hello Logic App Designer opens and shows  available services and *triggers* that  you can use in your logic app.</span></span>

5. <span data-ttu-id="364e6-139">Typ in het zoekvak Hallo `RSS`, en selecteert u deze trigger: **RSS - wanneer een item van de feed wordt gepubliceerd**</span><span class="sxs-lookup"><span data-stu-id="364e6-139">In hello search box, type `RSS`, and select this trigger: **RSS - When a feed item is published**</span></span> 

    ![RSS-trigger](media/logic-apps-create-a-logic-app/rss-trigger.png)

6. <span data-ttu-id="364e6-141">Hallo-koppeling voor RSS-feed Hallo-website die u wilt dat tootrack invoeren.</span><span class="sxs-lookup"><span data-stu-id="364e6-141">Enter hello link for hello website's RSS feed that you want tootrack.</span></span> 

     <span data-ttu-id="364e6-142">U kunt ook andere waarden opgeven voor **Frequentie** en **Interval**.</span><span class="sxs-lookup"><span data-stu-id="364e6-142">You can also change **Frequency** and **Interval**.</span></span> 
     <span data-ttu-id="364e6-143">Deze instellingen bepalen hoe vaak de logische app op nieuwe items controleert. Alle gevonden items tijdens die periode worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="364e6-143">These settings determine how often your logic app checks for new items and returns all items found during that time span.</span></span>

     <span data-ttu-id="364e6-144">In dit voorbeeld gaan we Controleer voor elke dag voor bovenste artikelen geboekt toohello CNN website.</span><span class="sxs-lookup"><span data-stu-id="364e6-144">For this example, let's check every day for   top stories posted toohello CNN website.</span></span>

     ![Trigger instellen met RSS-feed, frequentie en interval](media/logic-apps-create-a-logic-app/rss-trigger-setup.png)

7. <span data-ttu-id="364e6-146">Sla uw werk nu op.</span><span class="sxs-lookup"><span data-stu-id="364e6-146">Save your work for now.</span></span> <span data-ttu-id="364e6-147">(Op Hallo designer opdrachtbalk, kiest u **opslaan**.)</span><span class="sxs-lookup"><span data-stu-id="364e6-147">(On hello designer command bar, choose **Save**.)</span></span>

   ![Uw logische app opslaan](media/logic-apps-create-a-logic-app/save-logic-app.png)

   <span data-ttu-id="364e6-149">Als u opslaan, uw logische app live gaat, maar momenteel uw logische app alleen controleert op nieuwe items in opgegeven Hallo RSS-feed.</span><span class="sxs-lookup"><span data-stu-id="364e6-149">When you save, your logic app goes live, but currently, your logic app only checks for new items in hello specified RSS feed.</span></span> 
   <span data-ttu-id="364e6-150">toomake nuttiger, dat we een actie die uw logische app na de trigger uitvoert toevoegen voorbeeld wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="364e6-150">toomake this example more useful, we add an action that your logic app performs after your trigger fires.</span></span>

## <a name="add-an-action-that-responds-tooyour-trigger"></a><span data-ttu-id="364e6-151">Een actie die tooyour trigger reageert toevoegen</span><span class="sxs-lookup"><span data-stu-id="364e6-151">Add an action that responds tooyour trigger</span></span>

<span data-ttu-id="364e6-152">Een [*actie*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is een taak die wordt uitgevoerd tijdens de werkstroom voor de logische app.</span><span class="sxs-lookup"><span data-stu-id="364e6-152">An [*action*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is a task performed by your logic app workflow.</span></span> <span data-ttu-id="364e6-153">Nadat u een trigger tooyour logische app hebt toegevoegd, kunt u een actie tooperform bewerkingen kunt toevoegen met gegevens die zijn gegenereerd door deze trigger.</span><span class="sxs-lookup"><span data-stu-id="364e6-153">After you add a trigger tooyour logic app, you can add an action tooperform operations with data generated by that trigger.</span></span> <span data-ttu-id="364e6-154">In ons voorbeeld toevoegen we nu een actie die e-mailbericht verzendt wanneer nieuwe items worden weergegeven in de RSS-feed Hallo-website.</span><span class="sxs-lookup"><span data-stu-id="364e6-154">For our example, we now add an action that sends email when new items appear in hello website's RSS feed.</span></span>

1. <span data-ttu-id="364e6-155">Kies in de ontwerpfunctie voor Hallo onder de trigger **nieuwe stap** > **een actie toevoegen** als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="364e6-155">In hello designer, under your trigger, choose **New step** > **Add an action** as shown here:</span></span>

   ![Een actie toevoegen](media/logic-apps-create-a-logic-app/add-new-action.png)

   <span data-ttu-id="364e6-157">Hallo designer toont [beschikbare connectors](../connectors/apis-list.md) zodat u een tooperform actie selecteren kunt als de trigger wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="364e6-157">hello designer shows [available connectors](../connectors/apis-list.md) so that you can select an action tooperform when your trigger fires.</span></span>

2. <span data-ttu-id="364e6-158">Op basis van uw e-mailaccount, stappen Hallo voor Outlook of Gmail.</span><span class="sxs-lookup"><span data-stu-id="364e6-158">Based on your email account, follow hello steps for Outlook or Gmail.</span></span>

   * <span data-ttu-id="364e6-159">toosend e-mail van uw Outlook-account in het zoekvak hello, voer `outlook`.</span><span class="sxs-lookup"><span data-stu-id="364e6-159">toosend email from your Outlook account, in hello search box, enter `outlook`.</span></span> <span data-ttu-id="364e6-160">Kies onder **Services** **Outlook.com** voor persoonlijke Microsoft-accounts of **Office 365 Outlook** voor werk- of schoolaccount van Azure.</span><span class="sxs-lookup"><span data-stu-id="364e6-160">Under **Services**, choose **Outlook.com** for personal Microsoft accounts, or choose **Office 365 Outlook** for Azure work or school accounts.</span></span> 
   <span data-ttu-id="364e6-161">Selecteer **Een e-mail verzenden** onder **Acties**.</span><span class="sxs-lookup"><span data-stu-id="364e6-161">Under **Actions**, select **Send an email**.</span></span>

       ![De actie Een e-mail verzenden voor Outlook](media/logic-apps-create-a-logic-app/actions.png)

   * <span data-ttu-id="364e6-163">toosend e-mail van uw account Gmail in het zoekvak hello, voer `gmail`.</span><span class="sxs-lookup"><span data-stu-id="364e6-163">toosend email from your Gmail account, in hello search box, enter `gmail`.</span></span> 
   <span data-ttu-id="364e6-164">Selecteer **E-mail verzenden** onder **Acties**.</span><span class="sxs-lookup"><span data-stu-id="364e6-164">Under **Actions**, select **Send email**.</span></span>

       ![De actie E-mail verzenden voor Gmail](media/logic-apps-create-a-logic-app/actions-gmail.png)

3. <span data-ttu-id="364e6-166">Wanneer u wordt gevraagd om referenties, moet u aanmelden met Hallo gebruikersnaam en wachtwoord voor uw e-mailaccount.</span><span class="sxs-lookup"><span data-stu-id="364e6-166">When you're prompted for credentials, sign in with hello username and password for your email account.</span></span> 

4. <span data-ttu-id="364e6-167">Hallo-informatie opgeven voor deze actie, zoals Hallo bestemming e-mailadres en Hallo parameters voor Hallo gegevens tooinclude in Hallo e-mailbericht, bijvoorbeeld kiezen:</span><span class="sxs-lookup"><span data-stu-id="364e6-167">Provide hello details for this action, like hello destination email address, and choose hello parameters for hello data tooinclude in hello email, for example:</span></span>

   ![Selecteer gegevens tooinclude in e-mailbericht](media/logic-apps-create-a-logic-app/rss-action-setup.png)

    <span data-ttu-id="364e6-169">Als u Outlook hebt gekozen, kan uw logische app eruitzien zoals in dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="364e6-169">So if you chose Outlook,  your logic app might look like this example:</span></span>

    ![Logische app die klaar is](media/logic-apps-create-a-logic-app/save-run-complete-logic-app.png)

5.  <span data-ttu-id="364e6-171">Sla uw wijzigingen op.</span><span class="sxs-lookup"><span data-stu-id="364e6-171">Save your changes.</span></span> <span data-ttu-id="364e6-172">(Op Hallo designer opdrachtbalk, kiest u **opslaan**.)</span><span class="sxs-lookup"><span data-stu-id="364e6-172">(On hello designer command bar, choose **Save**.)</span></span>

6. <span data-ttu-id="364e6-173">U kunt de logische app nu handmatig uitvoeren om te kijken of alles werkt zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="364e6-173">You can now manually run your logic app for testing.</span></span> <span data-ttu-id="364e6-174">Kies op de ontwerpfunctie opdrachtbalk Hallo, **uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="364e6-174">On hello designer command bar, choose **Run**.</span></span> <span data-ttu-id="364e6-175">Anders kunt u uw logische app controleren Hallo opgegeven RSS-feed op basis van Hallo planning die u hebt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="364e6-175">Otherwise, you can let your logic app check hello specified RSS feed based on hello schedule that you set up.</span></span>

   <span data-ttu-id="364e6-176">Als uw logische app vindt de nieuwe items, verzendt Hallo logische app e-mailbericht met de geselecteerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="364e6-176">If your logic app finds new items, hello logic app sends email that includes your selected data.</span></span> 
   <span data-ttu-id="364e6-177">Als er geen nieuwe objecten zijn gevonden, slaat uw logische app Hallo-actie die e-mailbericht verzendt.</span><span class="sxs-lookup"><span data-stu-id="364e6-177">If no new items are found, your logic app skips hello action that sends email.</span></span>

7. <span data-ttu-id="364e6-178">Kies toomonitor en controleer uw logische app de uitgevoerd en de geschiedenis, op uw logische app-menu activeren **overzicht**.</span><span class="sxs-lookup"><span data-stu-id="364e6-178">toomonitor and check your logic app's run and trigger history, on your logic app menu, choose **Overview**.</span></span>

   ![Uitvoerings- en triggergeschiedenis van de logische app controleren en bekijken](media/logic-apps-create-a-logic-app/logic-app-run-trigger-history.png)

   > [!TIP]
   > <span data-ttu-id="364e6-180">Als u niet kunt Hallo-gegevens die u verwacht vinden, op de opdrachtbalk hello, kies **vernieuwen**.</span><span class="sxs-lookup"><span data-stu-id="364e6-180">If you don't find hello data that you expect, on hello command bar, try choosing **Refresh**.</span></span>

   <span data-ttu-id="364e6-181">meer over de status van uw logische app toolearn of voer en geschiedenis of toodiagnose uw logische app activeren, Zie [problemen met uw logische app](logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="364e6-181">toolearn more about your logic app's status or run and trigger history, or toodiagnose your logic app, see [Troubleshoot your logic app](logic-apps-diagnosing-failures.md).</span></span>

      > [!NOTE]
      > <span data-ttu-id="364e6-182">De logische app wordt uitgevoerd totdat u de app uitschakelt.</span><span class="sxs-lookup"><span data-stu-id="364e6-182">Your logic app continues running until you turn off your app.</span></span> <span data-ttu-id="364e6-183">Kies tooturn uit uw app nu op uw logische app-menu **overzicht**.</span><span class="sxs-lookup"><span data-stu-id="364e6-183">tooturn off your app for now, on your logic app menu, choose **Overview**.</span></span> <span data-ttu-id="364e6-184">Kies op de opdrachtbalk Hallo **uitschakelen**.</span><span class="sxs-lookup"><span data-stu-id="364e6-184">On hello command bar, choose **Disable**.</span></span>

<span data-ttu-id="364e6-185">U weet nu hoe u een logische app kunt maken en uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="364e6-185">Congratulations, you just set up and run your first basic logic app.</span></span> <span data-ttu-id="364e6-186">Daarnaast hebt u geleerd hoe eenvoudig het is om werkstromen te maken voor het automatiseren van processen en hoe u cloud-apps en cloudservices kunt integreren. Allemaal zonder één regel code te hoeven schrijven.</span><span class="sxs-lookup"><span data-stu-id="364e6-186">You also learned how easily you can create workflows that automate processes, and integrate cloud apps and cloud services - all without code.</span></span>

## <a name="manage-your-logic-app"></a><span data-ttu-id="364e6-187">Uw logische app beheren</span><span class="sxs-lookup"><span data-stu-id="364e6-187">Manage your logic app</span></span>

<span data-ttu-id="364e6-188">toomanage uw app kunt u taken zoals het Hallo-status controleren, bewerken, weergeven, uitschakelen of verwijderen van uw logische app uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="364e6-188">toomanage your app, you can perform tasks like check hello status, edit, view history, turn off, or delete your logic app.</span></span>

1. <span data-ttu-id="364e6-189">Meld u aan toohello [Azure-portal](https://portal.azure.com "Azure-portal").</span><span class="sxs-lookup"><span data-stu-id="364e6-189">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span>

2. <span data-ttu-id="364e6-190">Kies op het linkermenu Hallo, **meer services**.</span><span class="sxs-lookup"><span data-stu-id="364e6-190">On hello left menu, choose **More services**.</span></span> <span data-ttu-id="364e6-191">Kies onder **Enterprise Integration** de optie **Logic Apps**.</span><span class="sxs-lookup"><span data-stu-id="364e6-191">Under **Enterprise Integration**, choose **Logic Apps**.</span></span> <span data-ttu-id="364e6-192">Selecteer uw logische app.</span><span class="sxs-lookup"><span data-stu-id="364e6-192">Select your logic app.</span></span> 

   <span data-ttu-id="364e6-193">U vindt in Hallo logic app-menu deze beheertaken voor logic app:</span><span class="sxs-lookup"><span data-stu-id="364e6-193">In hello logic app menu, you can find these logic app management tasks:</span></span>

   |<span data-ttu-id="364e6-194">Taak</span><span class="sxs-lookup"><span data-stu-id="364e6-194">Task</span></span>|<span data-ttu-id="364e6-195">Stappen</span><span class="sxs-lookup"><span data-stu-id="364e6-195">Steps</span></span>| 
   |:---|:---| 
   | <span data-ttu-id="364e6-196">De status, uitvoeringsgeschiedenis en algemene informatie voor uw app bekijken</span><span class="sxs-lookup"><span data-stu-id="364e6-196">View your app's status, execution history, and general information</span></span>| <span data-ttu-id="364e6-197">Kies **Overzicht**.</span><span class="sxs-lookup"><span data-stu-id="364e6-197">Choose **Overview**.</span></span>| 
   | <span data-ttu-id="364e6-198">De app bewerken</span><span class="sxs-lookup"><span data-stu-id="364e6-198">Edit your app</span></span> | <span data-ttu-id="364e6-199">Kies **Logic App Designer**.</span><span class="sxs-lookup"><span data-stu-id="364e6-199">Choose **Logic App Designer**.</span></span> | 
   | <span data-ttu-id="364e6-200">De JSON-definitie van de werkstroom van uw app bekijken</span><span class="sxs-lookup"><span data-stu-id="364e6-200">View your app's workflow JSON definition</span></span> | <span data-ttu-id="364e6-201">Kies **Codeweergave van logische app**.</span><span class="sxs-lookup"><span data-stu-id="364e6-201">Choose **Logic App Code View**.</span></span> | 
   | <span data-ttu-id="364e6-202">Bewerkingen bekijken die zijn uitgevoerd in uw logische app</span><span class="sxs-lookup"><span data-stu-id="364e6-202">View operations performed on your logic app</span></span> | <span data-ttu-id="364e6-203">Kies **Activiteitenlogboek**.</span><span class="sxs-lookup"><span data-stu-id="364e6-203">Choose **Activity log**.</span></span> | 
   | <span data-ttu-id="364e6-204">Eerdere versies voor uw logische app weergeven</span><span class="sxs-lookup"><span data-stu-id="364e6-204">View past versions for your logic app</span></span> | <span data-ttu-id="364e6-205">Kies **Versies**.</span><span class="sxs-lookup"><span data-stu-id="364e6-205">Choose **Versions**.</span></span> | 
   | <span data-ttu-id="364e6-206">Uw app tijdelijk uitschakelen</span><span class="sxs-lookup"><span data-stu-id="364e6-206">Turn off your app temporarily</span></span> | <span data-ttu-id="364e6-207">Kies **overzicht**, kiest op de opdrachtbalk Hallo **uitschakelen**.</span><span class="sxs-lookup"><span data-stu-id="364e6-207">Choose **Overview**, then on hello command bar, choose **Disable**.</span></span> | 
   | <span data-ttu-id="364e6-208">De app verwijderen</span><span class="sxs-lookup"><span data-stu-id="364e6-208">Delete your app</span></span> | <span data-ttu-id="364e6-209">Kies **overzicht**, kiest op de opdrachtbalk Hallo **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="364e6-209">Choose **Overview**, then on hello command bar, choose **Delete**.</span></span> <span data-ttu-id="364e6-210">Voer de naam van de logische app in en kies **Verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="364e6-210">Enter your logic app's name, and choose **Delete**.</span></span> | 

## <a name="get-help"></a><span data-ttu-id="364e6-211">Help opvragen</span><span class="sxs-lookup"><span data-stu-id="364e6-211">Get help</span></span>

<span data-ttu-id="364e6-212">tooask vragen beantwoorden van vragen en meer informatie over welke andere Azure Logic Apps gebruikers doen, gaat u naar Hallo [Azure Logic Apps-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="364e6-212">tooask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="364e6-213">toohelp Azure Logic Apps en connectors verbeteren, stem of ideeën op Hallo indienen [Azure Logic Apps gebruiker feedback site](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="364e6-213">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="364e6-214">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="364e6-214">Next steps</span></span>

*  [<span data-ttu-id="364e6-215">Voorwaarden toevoegen en werkstromen uitvoeren</span><span class="sxs-lookup"><span data-stu-id="364e6-215">Add conditions and run workflows</span></span>](../logic-apps/logic-apps-use-logic-app-features.md)
*    [<span data-ttu-id="364e6-216">Sjablonen voor logische app</span><span class="sxs-lookup"><span data-stu-id="364e6-216">Logic app templates</span></span>](../logic-apps/logic-apps-use-logic-app-templates.md)
*  [<span data-ttu-id="364e6-217">Logische apps maken van Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="364e6-217">Create logic apps from Azure Resource Manager templates</span></span>](../logic-apps/logic-apps-arm-provision.md)
