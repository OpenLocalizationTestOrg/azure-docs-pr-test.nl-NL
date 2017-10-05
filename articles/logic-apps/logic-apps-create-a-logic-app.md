---
title: Uw eerste werkstroom maken tussen cloud-apps en cloudservices - Azure Logic Apps | Microsoft Docs
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
ms.openlocfilehash: 204bf123509729b60b55c306050cef54aa7fecc5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-first-logic-app-workflow-to-automate-processes-between-cloud-apps-and-cloud-services"></a><span data-ttu-id="640d4-104">Uw eerste werkstroom voor logische apps maken om processen tussen cloud-apps en cloudservices te automatiseren</span><span class="sxs-lookup"><span data-stu-id="640d4-104">Create your first logic app workflow to automate processes between cloud apps and cloud services</span></span>

<span data-ttu-id="640d4-105">Zonder dat u code hoeft te schrijven, kunt u bedrijfsprocessen eenvoudiger en sneller automatiseren door werkstromen te maken en uit te voeren met [Azure Logic Apps](logic-apps-what-are-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="640d4-105">Without writing any code, you can automate business processes more easily and quickly when you create and run workflows with [Azure Logic Apps](logic-apps-what-are-logic-apps.md).</span></span> <span data-ttu-id="640d4-106">Het eerste voorbeeld laat zien hoe u een eenvoudige werkstroom voor logische apps maakt waarmee een RSS-feed wordt gecontroleerd op nieuwe inhoud op een website.</span><span class="sxs-lookup"><span data-stu-id="640d4-106">This first example shows how to create a basic logic app workflow that checks an RSS feed for new content on a website.</span></span> <span data-ttu-id="640d4-107">Als er nieuwe items worden weergegeven in de feed van de website, verstuurt de logische app een e-mail vanuit een account van Outlook of Gmail.</span><span class="sxs-lookup"><span data-stu-id="640d4-107">When new items appear in the website's feed, the logic app sends email from an Outlook or Gmail account.</span></span>

<span data-ttu-id="640d4-108">U hebt deze items nodig om een logische app te maken en uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="640d4-108">To create and run a logic app, you need these items:</span></span>

* <span data-ttu-id="640d4-109">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="640d4-109">An Azure subscription.</span></span> <span data-ttu-id="640d4-110">Als u geen abonnement hebt, kunt u [beginnen met een gratis Azure-account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="640d4-110">If you don't have a subscription, you can [start with a free Azure account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="640d4-111">U kunt eventueel ook direct kiezen voor [een Betalen per gebruik-abonnement](https://azure.microsoft.com/pricing/purchase-options/).</span><span class="sxs-lookup"><span data-stu-id="640d4-111">Otherwise, you can [sign up for a Pay-As-You-Go subscription](https://azure.microsoft.com/pricing/purchase-options/).</span></span>

  <span data-ttu-id="640d4-112">Uw Azure-abonnement wordt gebruikt voor facturering van het gebruik van de logische app.</span><span class="sxs-lookup"><span data-stu-id="640d4-112">Your Azure subscription is used for billing logic app usage.</span></span> <span data-ttu-id="640d4-113">Lees hier meer informatie over [meten van gebruik](../logic-apps/logic-apps-pricing.md) en [prijzen](https://azure.microsoft.com/pricing/details/logic-apps) voor Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="640d4-113">Learn how [usage metering](../logic-apps/logic-apps-pricing.md) and [pricing](https://azure.microsoft.com/pricing/details/logic-apps) work for Azure Logic Apps.</span></span>

<span data-ttu-id="640d4-114">Verder zijn nog deze items nodig voor het voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="640d4-114">Also, this example requires these items:</span></span>

* <span data-ttu-id="640d4-115">Een account van Outlook.com, Office 365 Outlook of Gmail</span><span class="sxs-lookup"><span data-stu-id="640d4-115">An Outlook.com, Office 365 Outlook, or Gmail account</span></span>

    > [!TIP]
    > <span data-ttu-id="640d4-116">Als u een persoonlijk [Microsoft-account](https://account.microsoft.com/account) hebt, beschikt u over een Outlook.com-account.</span><span class="sxs-lookup"><span data-stu-id="640d4-116">If you have a personal [Microsoft account](https://account.microsoft.com/account), you have an Outlook.com account.</span></span> <span data-ttu-id="640d4-117">Als u een werk- of schoolaccount hebt van Azure, hebt u een **Office 365 Outlook**-account.</span><span class="sxs-lookup"><span data-stu-id="640d4-117">Otherwise, if you have an Azure work or school account, you have an **Office 365 Outlook** account.</span></span>

* <span data-ttu-id="640d4-118">Een koppeling naar de RSS-feed van een website.</span><span class="sxs-lookup"><span data-stu-id="640d4-118">A link to a website's RSS feed.</span></span> <span data-ttu-id="640d4-119">In dit voorbeeld wordt de [RSS-feed voor de populairste artikelen van de website CNN.com](http://rss.cnn.com/rss/cnn_topstories.rss) gebruikt: `http://rss.cnn.com/rss/cnn_topstories.rss`</span><span class="sxs-lookup"><span data-stu-id="640d4-119">This example uses the [RSS feed for top stories from the CNN.com website](http://rss.cnn.com/rss/cnn_topstories.rss): `http://rss.cnn.com/rss/cnn_topstories.rss`</span></span>

## <a name="add-a-trigger-that-starts-your-workflow"></a><span data-ttu-id="640d4-120">Een trigger toevoegen voor het starten van de werkstroom</span><span class="sxs-lookup"><span data-stu-id="640d4-120">Add a trigger that starts your workflow</span></span>

<span data-ttu-id="640d4-121">Een [*trigger*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is een gebeurtenis waardoor de werkstroom voor uw logische app wordt gestart. Het is ook het eerste item dat uw logische app nodig heeft.</span><span class="sxs-lookup"><span data-stu-id="640d4-121">A [*trigger*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is an event that starts your logic app workflow and is the first item that your logic app needs.</span></span>

1. <span data-ttu-id="640d4-122">Meld u aan bij [Azure Portal](https://portal.azure.com "Azure Portal").</span><span class="sxs-lookup"><span data-stu-id="640d4-122">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span></span>

2. <span data-ttu-id="640d4-123">Kies in het menu links de optie **Nieuw** > **Enterprise Integration** > **Logische app** (zie hieronder):</span><span class="sxs-lookup"><span data-stu-id="640d4-123">From the left menu, choose **New** > **Enterprise Integration** > **Logic App** as shown here:</span></span>

     ![Azure Portal, Nieuw, Enterprise Integration, Logische app](media/logic-apps-create-a-logic-app/azure-portal-create-logic-app.png)

   > [!TIP]
   > <span data-ttu-id="640d4-125">U kunt ook **Nieuw** kiezen, `logic app` in het zoekvak invoeren en op Enter drukken.</span><span class="sxs-lookup"><span data-stu-id="640d4-125">You can also choose **New**, then in the search box, type `logic app`, and press Enter.</span></span> <span data-ttu-id="640d4-126">Kies vervolgens **Logische app** > **Maken**.</span><span class="sxs-lookup"><span data-stu-id="640d4-126">Then choose **Logic App** > **Create**.</span></span>

3. <span data-ttu-id="640d4-127">Voer een naam in voor de logische app en selecteer uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="640d4-127">Name your logic app and select your Azure subscription.</span></span> <span data-ttu-id="640d4-128">Maak of selecteer vervolgens een Azure-resourcegroep, zodat u gerelateerde Azure-resources makkelijker kunt organiseren en beheren.</span><span class="sxs-lookup"><span data-stu-id="640d4-128">Now create or select an Azure resource group, which helps you organize and manage related Azure resources.</span></span> <span data-ttu-id="640d4-129">Selecteer ten slotte de locatie van het datacenter voor het hosten van uw logische app.</span><span class="sxs-lookup"><span data-stu-id="640d4-129">Finally, select the datacenter location for hosting your logic app.</span></span> <span data-ttu-id="640d4-130">Als u hiermee klaar bent, selecteert u **Vastmaken aan dashboard** en klikt u op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="640d4-130">When you're ready, choose **Pin to dashboard** and then **Create**.</span></span>

     ![Details van logische app](media/logic-apps-create-a-logic-app/logic-app-settings.png)

   > [!NOTE]
   > <span data-ttu-id="640d4-132">Wanneer u **Vastmaken aan dashboard** selecteert, wordt de logische app na implementatie weergegeven in het Azure-dashboard. Bovendien wordt de app dan automatisch geopend.</span><span class="sxs-lookup"><span data-stu-id="640d4-132">When you select **Pin to dashboard**, your logic app appears on the Azure dashboard after deployment, and opens automatically.</span></span> <span data-ttu-id="640d4-133">Als uw logische app niet in het dashboard wordt weergegeven, kiest u **Meer weergeven** op de tegel **Alle resources** en selecteert u de logische app.</span><span class="sxs-lookup"><span data-stu-id="640d4-133">If your logic app doesn't appear on the dashboard, on the **All resources** tile, choose **See More**, and select your logic app.</span></span> <span data-ttu-id="640d4-134">U kunt ook in het menu aan de linkerkant **Meer services** kiezen.</span><span class="sxs-lookup"><span data-stu-id="640d4-134">Or on the left menu, choose **More services**.</span></span> <span data-ttu-id="640d4-135">Kies vervolgens **Logische apps** onder **Enterprise Integration** en selecteer dan de logische app.</span><span class="sxs-lookup"><span data-stu-id="640d4-135">Under **Enterprise Integration**, choose **Logic Apps**, and select your logic app.</span></span>

4. <span data-ttu-id="640d4-136">Wanneer u een logische app voor het eerst opent, ziet u in Logic App Designer sjablonen die u als uitgangspunt kunt nemen.</span><span class="sxs-lookup"><span data-stu-id="640d4-136">When you open your logic app for the first time, the Logic App Designer shows templates that you can use to get started.</span></span> <span data-ttu-id="640d4-137">Kies voor dit voorbeeld **Lege logische app**, zodat u de logische app helemaal zelf kunt ontwerpen.</span><span class="sxs-lookup"><span data-stu-id="640d4-137">For now, choose **Blank Logic App** so you can build your logic app from scratch.</span></span>

    <span data-ttu-id="640d4-138">De ontwerpfunctie voor Logic App wordt geopend en ziet u beschikbare services en *triggers* die u in uw logische app kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="640d4-138">The Logic App Designer opens and shows  available services and *triggers* that  you can use in your logic app.</span></span>

5. <span data-ttu-id="640d4-139">Typ `RSS` in het zoekvak en selecteer deze trigger: **RSS - Wanneer een feeditem wordt gepubliceerd**.</span><span class="sxs-lookup"><span data-stu-id="640d4-139">In the search box, type `RSS`, and select this trigger: **RSS - When a feed item is published**</span></span> 

    ![RSS-trigger](media/logic-apps-create-a-logic-app/rss-trigger.png)

6. <span data-ttu-id="640d4-141">Voer de koppeling in voor de RSS-feed van de website die u wilt bijhouden.</span><span class="sxs-lookup"><span data-stu-id="640d4-141">Enter the link for the website's RSS feed that you want to track.</span></span> 

     <span data-ttu-id="640d4-142">U kunt ook andere waarden opgeven voor **Frequentie** en **Interval**.</span><span class="sxs-lookup"><span data-stu-id="640d4-142">You can also change **Frequency** and **Interval**.</span></span> 
     <span data-ttu-id="640d4-143">Deze instellingen bepalen hoe vaak de logische app op nieuwe items controleert. Alle gevonden items tijdens die periode worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="640d4-143">These settings determine how often your logic app checks for new items and returns all items found during that time span.</span></span>

     <span data-ttu-id="640d4-144">In dit voorbeeld gaan we elke dag controleren of er populaire artikelen zijn gepost op de CNN-website.</span><span class="sxs-lookup"><span data-stu-id="640d4-144">For this example, let's check every day for   top stories posted to the CNN website.</span></span>

     ![Trigger instellen met RSS-feed, frequentie en interval](media/logic-apps-create-a-logic-app/rss-trigger-setup.png)

7. <span data-ttu-id="640d4-146">Sla uw werk nu op.</span><span class="sxs-lookup"><span data-stu-id="640d4-146">Save your work for now.</span></span> <span data-ttu-id="640d4-147">(Kies hiervoor **Opslaan** op de opdrachtbalk.)</span><span class="sxs-lookup"><span data-stu-id="640d4-147">(On the designer command bar, choose **Save**.)</span></span>

   ![Uw logische app opslaan](media/logic-apps-create-a-logic-app/save-logic-app.png)

   <span data-ttu-id="640d4-149">Wanneer u de app opslaat, is de app meteen live. Op dit moment controleert de logische app alleen op nieuwe items in de opgegeven RSS-feed.</span><span class="sxs-lookup"><span data-stu-id="640d4-149">When you save, your logic app goes live, but currently, your logic app only checks for new items in the specified RSS feed.</span></span> 
   <span data-ttu-id="640d4-150">We gaan dit voorbeeld zinvoller maken door een actie toe te voegen die de logische app uitvoert nadat de trigger is geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="640d4-150">To make this example more useful, we add an action that your logic app performs after your trigger fires.</span></span>

## <a name="add-an-action-that-responds-to-your-trigger"></a><span data-ttu-id="640d4-151">Een actie toevoegen die op de trigger reageert</span><span class="sxs-lookup"><span data-stu-id="640d4-151">Add an action that responds to your trigger</span></span>

<span data-ttu-id="640d4-152">Een [*actie*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is een taak die wordt uitgevoerd tijdens de werkstroom voor de logische app.</span><span class="sxs-lookup"><span data-stu-id="640d4-152">An [*action*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is a task performed by your logic app workflow.</span></span> <span data-ttu-id="640d4-153">Nadat u een trigger hebt toegevoegd aan uw logische app, kunt u een actie toevoegen om bewerkingen uit te voeren op gegevens die met deze trigger worden gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="640d4-153">After you add a trigger to your logic app, you can add an action to perform operations with data generated by that trigger.</span></span> <span data-ttu-id="640d4-154">In ons voorbeeld gaan we nu een actie toevoegen waarmee een e-mail wordt verstuurd wanneer er nieuwe items in de RSS-feed van de website staan.</span><span class="sxs-lookup"><span data-stu-id="640d4-154">For our example, we now add an action that sends email when new items appear in the website's RSS feed.</span></span>

1. <span data-ttu-id="640d4-155">Kies in Logic App Designer **Nieuwe stap** > **Een actie toevoegen** onder de trigger (zie hieronder):</span><span class="sxs-lookup"><span data-stu-id="640d4-155">In the designer, under your trigger, choose **New step** > **Add an action** as shown here:</span></span>

   ![Een actie toevoegen](media/logic-apps-create-a-logic-app/add-new-action.png)

   <span data-ttu-id="640d4-157">In Logic App Designer ziet u de [beschikbare connectors](../connectors/apis-list.md), zodat u een actie kunt kiezen die moet worden uitgevoerd wanneer de trigger wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="640d4-157">The designer shows [available connectors](../connectors/apis-list.md) so that you can select an action to perform when your trigger fires.</span></span>

2. <span data-ttu-id="640d4-158">Volg afhankelijk van uw e-mailaccount de stappen voor Outlook of Gmail.</span><span class="sxs-lookup"><span data-stu-id="640d4-158">Based on your email account, follow the steps for Outlook or Gmail.</span></span>

   * <span data-ttu-id="640d4-159">Als u een e-mail wilt verzenden met uw Outlook-account, typt u `outlook` in het zoekvak.</span><span class="sxs-lookup"><span data-stu-id="640d4-159">To send email from your Outlook account, in the search box, enter `outlook`.</span></span> <span data-ttu-id="640d4-160">Kies onder **Services** **Outlook.com** voor persoonlijke Microsoft-accounts of **Office 365 Outlook** voor werk- of schoolaccount van Azure.</span><span class="sxs-lookup"><span data-stu-id="640d4-160">Under **Services**, choose **Outlook.com** for personal Microsoft accounts, or choose **Office 365 Outlook** for Azure work or school accounts.</span></span> 
   <span data-ttu-id="640d4-161">Selecteer **Een e-mail verzenden** onder **Acties**.</span><span class="sxs-lookup"><span data-stu-id="640d4-161">Under **Actions**, select **Send an email**.</span></span>

       ![De actie Een e-mail verzenden voor Outlook](media/logic-apps-create-a-logic-app/actions.png)

   * <span data-ttu-id="640d4-163">Als u een e-mail wilt verzenden met uw Gmail-account, typt u `gmail` in het zoekvak.</span><span class="sxs-lookup"><span data-stu-id="640d4-163">To send email from your Gmail account, in the search box, enter `gmail`.</span></span> 
   <span data-ttu-id="640d4-164">Selecteer **E-mail verzenden** onder **Acties**.</span><span class="sxs-lookup"><span data-stu-id="640d4-164">Under **Actions**, select **Send email**.</span></span>

       ![De actie E-mail verzenden voor Gmail](media/logic-apps-create-a-logic-app/actions-gmail.png)

3. <span data-ttu-id="640d4-166">Wanneer u wordt gevraagd om referenties, meldt u zich aan met de gebruikersnaam en het wachtwoord voor uw e-mailaccount.</span><span class="sxs-lookup"><span data-stu-id="640d4-166">When you're prompted for credentials, sign in with the username and password for your email account.</span></span> 

4. <span data-ttu-id="640d4-167">Geef de details op voor deze actie, zoals het e-mailadres waarnaar de e-mail moet worden verstuurd, en kies de parameters voor de gegevens die u wilt opnemen in de e-mail, zoals:</span><span class="sxs-lookup"><span data-stu-id="640d4-167">Provide the details for this action, like the destination email address, and choose the parameters for the data to include in the email, for example:</span></span>

   ![Selecteer de gegevens die u in het e-mailbericht wilt opnemen](media/logic-apps-create-a-logic-app/rss-action-setup.png)

    <span data-ttu-id="640d4-169">Als u Outlook hebt gekozen, kan uw logische app eruitzien zoals in dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="640d4-169">So if you chose Outlook,  your logic app might look like this example:</span></span>

    ![Logische app die klaar is](media/logic-apps-create-a-logic-app/save-run-complete-logic-app.png)

5.  <span data-ttu-id="640d4-171">Sla uw wijzigingen op.</span><span class="sxs-lookup"><span data-stu-id="640d4-171">Save your changes.</span></span> <span data-ttu-id="640d4-172">(Kies hiervoor **Opslaan** op de opdrachtbalk.)</span><span class="sxs-lookup"><span data-stu-id="640d4-172">(On the designer command bar, choose **Save**.)</span></span>

6. <span data-ttu-id="640d4-173">U kunt de logische app nu handmatig uitvoeren om te kijken of alles werkt zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="640d4-173">You can now manually run your logic app for testing.</span></span> <span data-ttu-id="640d4-174">Kies hiervoor **Uitvoeren** op de opdrachtbalk.</span><span class="sxs-lookup"><span data-stu-id="640d4-174">On the designer command bar, choose **Run**.</span></span> <span data-ttu-id="640d4-175">U kunt ook wachten totdat de logische app de opgegeven RSS-feed controleert volgens het schema dat u hebt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="640d4-175">Otherwise, you can let your logic app check the specified RSS feed based on the schedule that you set up.</span></span>

   <span data-ttu-id="640d4-176">Als de logische app nieuwe items vindt, wordt er door de app een e-mail verstuurd met de gegevens die u eerder hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="640d4-176">If your logic app finds new items, the logic app sends email that includes your selected data.</span></span> 
   <span data-ttu-id="640d4-177">Als er geen nieuwe items worden gevonden, wordt de actie voor het versturen van een e-mail overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="640d4-177">If no new items are found, your logic app skips the action that sends email.</span></span>

7. <span data-ttu-id="640d4-178">Als u de uitvoerings- en triggergeschiedenis van de logische app wilt controleren, kiest u **Overzicht** in het menu van de logische app.</span><span class="sxs-lookup"><span data-stu-id="640d4-178">To monitor and check your logic app's run and trigger history, on your logic app menu, choose **Overview**.</span></span>

   ![Uitvoerings- en triggergeschiedenis van de logische app controleren en bekijken](media/logic-apps-create-a-logic-app/logic-app-run-trigger-history.png)

   > [!TIP]
   > <span data-ttu-id="640d4-180">Als de verwachte gegevens niet worden weergegeven, klikt u op de opdrachtbalk op **Vernieuwen**.</span><span class="sxs-lookup"><span data-stu-id="640d4-180">If you don't find the data that you expect, on the command bar, try choosing **Refresh**.</span></span>

   <span data-ttu-id="640d4-181">Als u meer wilt weten over de status van uw logische app of over de uitvoerings- en triggergeschiedenis, raadpleegt u [Diagnose logic app failures](logic-apps-diagnosing-failures.md) (Problemen met logische app oplossen).</span><span class="sxs-lookup"><span data-stu-id="640d4-181">To learn more about your logic app's status or run and trigger history, or to diagnose your logic app, see [Troubleshoot your logic app](logic-apps-diagnosing-failures.md).</span></span>

      > [!NOTE]
      > <span data-ttu-id="640d4-182">De logische app wordt uitgevoerd totdat u de app uitschakelt.</span><span class="sxs-lookup"><span data-stu-id="640d4-182">Your logic app continues running until you turn off your app.</span></span> <span data-ttu-id="640d4-183">Als u de app voorlopig wilt uitschakelen, kiest u **Overzicht** in het menu van de logische app.</span><span class="sxs-lookup"><span data-stu-id="640d4-183">To turn off your app for now, on your logic app menu, choose **Overview**.</span></span> <span data-ttu-id="640d4-184">Kies op de opdrachtbalk de optie **Uitschakelen**.</span><span class="sxs-lookup"><span data-stu-id="640d4-184">On the command bar, choose **Disable**.</span></span>

<span data-ttu-id="640d4-185">U weet nu hoe u een logische app kunt maken en uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="640d4-185">Congratulations, you just set up and run your first basic logic app.</span></span> <span data-ttu-id="640d4-186">Daarnaast hebt u geleerd hoe eenvoudig het is om werkstromen te maken voor het automatiseren van processen en hoe u cloud-apps en cloudservices kunt integreren. Allemaal zonder één regel code te hoeven schrijven.</span><span class="sxs-lookup"><span data-stu-id="640d4-186">You also learned how easily you can create workflows that automate processes, and integrate cloud apps and cloud services - all without code.</span></span>

## <a name="manage-your-logic-app"></a><span data-ttu-id="640d4-187">Uw logische app beheren</span><span class="sxs-lookup"><span data-stu-id="640d4-187">Manage your logic app</span></span>

<span data-ttu-id="640d4-188">Voorbeelden van taken om uw app te beheren, zijn het controleren van de status, het bewerken van instellingen, het bekijken van de geschiedenis, en het uitschakelen of zelfs verwijderen van de app.</span><span class="sxs-lookup"><span data-stu-id="640d4-188">To manage your app, you can perform tasks like check the status, edit, view history, turn off, or delete your logic app.</span></span>

1. <span data-ttu-id="640d4-189">Meld u aan bij [Azure Portal](https://portal.azure.com "Azure Portal").</span><span class="sxs-lookup"><span data-stu-id="640d4-189">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span></span>

2. <span data-ttu-id="640d4-190">Kies **Meer services** in het menu aan de linkerkant.</span><span class="sxs-lookup"><span data-stu-id="640d4-190">On the left menu, choose **More services**.</span></span> <span data-ttu-id="640d4-191">Kies onder **Enterprise Integration** de optie **Logic Apps**.</span><span class="sxs-lookup"><span data-stu-id="640d4-191">Under **Enterprise Integration**, choose **Logic Apps**.</span></span> <span data-ttu-id="640d4-192">Selecteer uw logische app.</span><span class="sxs-lookup"><span data-stu-id="640d4-192">Select your logic app.</span></span> 

   <span data-ttu-id="640d4-193">In het menu van de logische app vindt u deze beheertaken:</span><span class="sxs-lookup"><span data-stu-id="640d4-193">In the logic app menu, you can find these logic app management tasks:</span></span>

   |<span data-ttu-id="640d4-194">Taak</span><span class="sxs-lookup"><span data-stu-id="640d4-194">Task</span></span>|<span data-ttu-id="640d4-195">Stappen</span><span class="sxs-lookup"><span data-stu-id="640d4-195">Steps</span></span>| 
   |:---|:---| 
   | <span data-ttu-id="640d4-196">De status, uitvoeringsgeschiedenis en algemene informatie voor uw app bekijken</span><span class="sxs-lookup"><span data-stu-id="640d4-196">View your app's status, execution history, and general information</span></span>| <span data-ttu-id="640d4-197">Kies **Overzicht**.</span><span class="sxs-lookup"><span data-stu-id="640d4-197">Choose **Overview**.</span></span>| 
   | <span data-ttu-id="640d4-198">De app bewerken</span><span class="sxs-lookup"><span data-stu-id="640d4-198">Edit your app</span></span> | <span data-ttu-id="640d4-199">Kies **Logic App Designer**.</span><span class="sxs-lookup"><span data-stu-id="640d4-199">Choose **Logic App Designer**.</span></span> | 
   | <span data-ttu-id="640d4-200">De JSON-definitie van de werkstroom van uw app bekijken</span><span class="sxs-lookup"><span data-stu-id="640d4-200">View your app's workflow JSON definition</span></span> | <span data-ttu-id="640d4-201">Kies **Codeweergave van logische app**.</span><span class="sxs-lookup"><span data-stu-id="640d4-201">Choose **Logic App Code View**.</span></span> | 
   | <span data-ttu-id="640d4-202">Bewerkingen bekijken die zijn uitgevoerd in uw logische app</span><span class="sxs-lookup"><span data-stu-id="640d4-202">View operations performed on your logic app</span></span> | <span data-ttu-id="640d4-203">Kies **Activiteitenlogboek**.</span><span class="sxs-lookup"><span data-stu-id="640d4-203">Choose **Activity log**.</span></span> | 
   | <span data-ttu-id="640d4-204">Eerdere versies voor uw logische app weergeven</span><span class="sxs-lookup"><span data-stu-id="640d4-204">View past versions for your logic app</span></span> | <span data-ttu-id="640d4-205">Kies **Versies**.</span><span class="sxs-lookup"><span data-stu-id="640d4-205">Choose **Versions**.</span></span> | 
   | <span data-ttu-id="640d4-206">Uw app tijdelijk uitschakelen</span><span class="sxs-lookup"><span data-stu-id="640d4-206">Turn off your app temporarily</span></span> | <span data-ttu-id="640d4-207">Kies **Overzicht** en kies vervolgens **Uitschakelen** op de opdrachtbalk.</span><span class="sxs-lookup"><span data-stu-id="640d4-207">Choose **Overview**, then on the command bar, choose **Disable**.</span></span> | 
   | <span data-ttu-id="640d4-208">De app verwijderen</span><span class="sxs-lookup"><span data-stu-id="640d4-208">Delete your app</span></span> | <span data-ttu-id="640d4-209">Kies **Overzicht** en kies vervolgens **Verwijderen** op de opdrachtbalk.</span><span class="sxs-lookup"><span data-stu-id="640d4-209">Choose **Overview**, then on the command bar, choose **Delete**.</span></span> <span data-ttu-id="640d4-210">Voer de naam van de logische app in en kies **Verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="640d4-210">Enter your logic app's name, and choose **Delete**.</span></span> | 

## <a name="get-help"></a><span data-ttu-id="640d4-211">Help opvragen</span><span class="sxs-lookup"><span data-stu-id="640d4-211">Get help</span></span>

<span data-ttu-id="640d4-212">Ga naar het [Forum voor Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) om vragen te stellen, vragen te beantwoorden en te zien wat andere gebruikers van Azure Logic Apps aan het doen zijn.</span><span class="sxs-lookup"><span data-stu-id="640d4-212">To ask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="640d4-213">Ter verbetering van Azure Logic Apps en connectors kunt u stemmen op ideeën of ideeën indien op de [site voor gebruikersfeedback van Azure Logic Apps](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="640d4-213">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="640d4-214">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="640d4-214">Next steps</span></span>

*  [<span data-ttu-id="640d4-215">Voorwaarden toevoegen en werkstromen uitvoeren</span><span class="sxs-lookup"><span data-stu-id="640d4-215">Add conditions and run workflows</span></span>](../logic-apps/logic-apps-use-logic-app-features.md)
*    [<span data-ttu-id="640d4-216">Sjablonen voor logische app</span><span class="sxs-lookup"><span data-stu-id="640d4-216">Logic app templates</span></span>](../logic-apps/logic-apps-use-logic-app-templates.md)
*  [<span data-ttu-id="640d4-217">Logische apps maken van Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="640d4-217">Create logic apps from Azure Resource Manager templates</span></span>](../logic-apps/logic-apps-arm-provision.md)
