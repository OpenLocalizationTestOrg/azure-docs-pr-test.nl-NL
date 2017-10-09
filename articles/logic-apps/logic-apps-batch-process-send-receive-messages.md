---
title: verwerken van berichten aaaBatch als een groep of een verzameling - Azure Logic Apps | Microsoft Docs
description: Verzenden en ontvangen van berichten voor batchverwerking in logic apps
keywords: batch, batchproces
author: jonfancey
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/7/2017
ms.author: LADocs; estfan; jonfan
ms.openlocfilehash: 2603db71ee0659d5b6bf5ce3d32f1b0d13c34194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="send-receive-and-batch-process-messages-in-logic-apps"></a><span data-ttu-id="e983e-104">Verzenden, ontvangen en verwerken van berichten in logic apps batch</span><span class="sxs-lookup"><span data-stu-id="e983e-104">Send, receive, and batch process messages in logic apps</span></span>

<span data-ttu-id="e983e-105">tooprocess berichten samen in groepen, kunt u gegevens items of berichten, tooa verzenden *batch*, en vervolgens deze items als een batch te verwerken.</span><span class="sxs-lookup"><span data-stu-id="e983e-105">tooprocess messages together in groups, you can send data items, or messages, tooa *batch*, and then process those items as a batch.</span></span> <span data-ttu-id="e983e-106">Deze methode is handig als u wilt ervoor gegevensitems toomake zijn gegroepeerd in een bepaalde manier en samen worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="e983e-106">This approach is useful when you want toomake sure data items are grouped in a specific way and are processed together.</span></span> 

<span data-ttu-id="e983e-107">U kunt logische apps die items als een batch ontvangen met behulp van Hallo maken **Batch** trigger.</span><span class="sxs-lookup"><span data-stu-id="e983e-107">You can create logic apps that receive items as a batch by using hello **Batch** trigger.</span></span> <span data-ttu-id="e983e-108">Vervolgens kunt u logische apps die items tooa batch verzenden met behulp van Hallo maken **Batch** in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="e983e-108">You can then create logic apps that send items tooa batch by using hello **Batch** action.</span></span>

<span data-ttu-id="e983e-109">Dit onderwerp wordt beschreven hoe u een batchen oplossing kunt maken met het uitvoeren van deze taken:</span><span class="sxs-lookup"><span data-stu-id="e983e-109">This topic shows how you can build a batching solution by performing these tasks:</span></span> 

* <span data-ttu-id="e983e-110">[Maken van een logische app dat ontvangt en verzamelt items als batch](#batch-receiver).</span><span class="sxs-lookup"><span data-stu-id="e983e-110">[Create a logic app that receives and collects items as a batch](#batch-receiver).</span></span> <span data-ttu-id="e983e-111">Deze 'batch ontvanger' logische app geeft Hallo batch naam en release criteria toomeet voor Hallo ontvanger logische app vrijgegeven en worden items verwerkt.</span><span class="sxs-lookup"><span data-stu-id="e983e-111">This "batch receiver" logic app specifies hello batch name and release criteria toomeet before hello receiver logic app releases and processes items.</span></span> 

* <span data-ttu-id="e983e-112">[Maken van een logische app die u items tooa batch verzendt](#batch-sender).</span><span class="sxs-lookup"><span data-stu-id="e983e-112">[Create a logic app that sends items tooa batch](#batch-sender).</span></span> <span data-ttu-id="e983e-113">Deze 'batch afzender' logische app geeft aan waar toosend-items een bestaande batch ontvanger logic app moeten.</span><span class="sxs-lookup"><span data-stu-id="e983e-113">This "batch sender" logic app specifies where toosend items, which must be an existing batch receiver logic app.</span></span> <span data-ttu-id="e983e-114">U kunt ook een unieke sleutel, zoals een klantnummer opgeven, te 'partitie' of delen, Hallo doel batch in subsets op basis van die sleutel.</span><span class="sxs-lookup"><span data-stu-id="e983e-114">You can also specify a unique key, like a customer number, too"partition", or divide, hello target batch into subsets based on that key.</span></span> <span data-ttu-id="e983e-115">Op die manier worden alle items met die sleutel verzameld en verwerkt samen.</span><span class="sxs-lookup"><span data-stu-id="e983e-115">That way, all items with that key are collected and processed together.</span></span> 

## <a name="requirements"></a><span data-ttu-id="e983e-116">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e983e-116">Requirements</span></span>

<span data-ttu-id="e983e-117">toofollow in dit voorbeeld moet u deze items:</span><span class="sxs-lookup"><span data-stu-id="e983e-117">toofollow this example, you need these items:</span></span>

* <span data-ttu-id="e983e-118">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="e983e-118">An Azure subscription.</span></span> <span data-ttu-id="e983e-119">Als u geen abonnement hebt, kunt u [beginnen met een gratis Azure-account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="e983e-119">If you don't have a subscription, you can [start with a free Azure account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="e983e-120">U kunt eventueel ook direct kiezen voor [een Betalen per gebruik-abonnement](https://azure.microsoft.com/pricing/purchase-options/).</span><span class="sxs-lookup"><span data-stu-id="e983e-120">Otherwise, you can [sign up for a Pay-As-You-Go subscription](https://azure.microsoft.com/pricing/purchase-options/).</span></span>

* <span data-ttu-id="e983e-121">Elementaire kennis over [hoe toocreate logic apps](../logic-apps/logic-apps-create-a-logic-app.md)</span><span class="sxs-lookup"><span data-stu-id="e983e-121">Basic knowledge about [how toocreate logic apps](../logic-apps/logic-apps-create-a-logic-app.md)</span></span> 

* <span data-ttu-id="e983e-122">Een e-mailaccount met een [e-provider wordt ondersteund door Azure Logic Apps](../connectors/apis-list.md)</span><span class="sxs-lookup"><span data-stu-id="e983e-122">An email account with any [email provider supported by Azure Logic Apps](../connectors/apis-list.md)</span></span>

<a name="batch-receiver"></a>

## <a name="create-logic-apps-that-receive-messages-as-a-batch"></a><span data-ttu-id="e983e-123">Logic apps die berichten te als een batch ontvangen maken</span><span class="sxs-lookup"><span data-stu-id="e983e-123">Create logic apps that receive messages as a batch</span></span>

<span data-ttu-id="e983e-124">Voordat u berichten tooa batch verzenden kunt, moet u eerst een 'batch ontvanger' logische app maken met de Hallo **Batch** trigger.</span><span class="sxs-lookup"><span data-stu-id="e983e-124">Before you can send messages tooa batch, you must first create a "batch receiver" logic app with hello **Batch** trigger.</span></span> <span data-ttu-id="e983e-125">Op die manier kunt u deze ontvanger logic app bij het maken van Hallo afzender logische app.</span><span class="sxs-lookup"><span data-stu-id="e983e-125">That way, you can select this receiver logic app when you create hello sender logic app.</span></span> <span data-ttu-id="e983e-126">Voor de ontvanger hello geeft u Hallo batchnaam, versie criteria en andere instellingen.</span><span class="sxs-lookup"><span data-stu-id="e983e-126">For hello receiver, you specify hello batch name, release criteria, and other settings.</span></span> 

<span data-ttu-id="e983e-127">Afzender logische apps moeten weten waar toosend items, terwijl de ontvanger logische apps tooknow alles over Hallo afzenders niet nodig.</span><span class="sxs-lookup"><span data-stu-id="e983e-127">Sender logic apps need know where toosend items, while receiver logic apps don't need tooknow anything about hello senders.</span></span>

1. <span data-ttu-id="e983e-128">In Hallo [Azure-portal](https://portal.azure.com), een logische app maken met deze naam: 'BatchReceiver'</span><span class="sxs-lookup"><span data-stu-id="e983e-128">In hello [Azure portal](https://portal.azure.com), create a logic app with this name: "BatchReceiver"</span></span> 

2. <span data-ttu-id="e983e-129">In Logic Apps Designer toevoegen Hallo **Batch** trigger uw logische app-werkstroom op te starten.</span><span class="sxs-lookup"><span data-stu-id="e983e-129">In Logic Apps Designer, add hello **Batch** trigger, which starts your logic app workflow.</span></span> <span data-ttu-id="e983e-130">Voer in het zoekvak hello, 'batch' als filter.</span><span class="sxs-lookup"><span data-stu-id="e983e-130">In hello search box, enter "batch" as your filter.</span></span> <span data-ttu-id="e983e-131">Selecteer deze trigger: **Batch: Batch-berichten**</span><span class="sxs-lookup"><span data-stu-id="e983e-131">Select this trigger: **Batch – Batch messages**</span></span>

   ![Batch-trigger toevoegen](./media/logic-apps-batch-process-send-receive-messages/add-batch-receiver-trigger.png)

3. <span data-ttu-id="e983e-133">Geef een naam voor de batch Hallo en Geef criteria op voor het vrijgeven van Hallo batch, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e983e-133">Provide a name for hello batch, and specify criteria for releasing hello batch, for example:</span></span>

   * <span data-ttu-id="e983e-134">**Batch-naam**: Hallo naam die wordt gebruikt tooidentify Hallo batch, namelijk 'TestBatch' in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="e983e-134">**Batch Name**: hello name used tooidentify hello batch, which is "TestBatch" in this example.</span></span>
   * <span data-ttu-id="e983e-135">**Aantal berichten**: het aantal berichten toohold Hallo als batch voordat vrijgegeven voor verwerking, namelijk '5' in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="e983e-135">**Message Count**: hello number of messages toohold as a batch before releasing for processing, which is "5" in this example.</span></span>

   ![Geef details op Batch trigger](./media/logic-apps-batch-process-send-receive-messages/receive-batch-trigger-details.png)

4. <span data-ttu-id="e983e-137">Voeg een andere actie die een e-mailbericht wordt verzonden wanneer Hallo batch trigger wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="e983e-137">Add another action that sends an email when hello batch trigger fires.</span></span> <span data-ttu-id="e983e-138">Elke keer Hallo-batch heeft vijf items, Hallo logic app stuurt een e-mailbericht.</span><span class="sxs-lookup"><span data-stu-id="e983e-138">Each time hello batch has five items, hello logic app sends an email.</span></span>

   1. <span data-ttu-id="e983e-139">Kies onder Hallo batch worden geactiveerd, **+ een nieuwe stap** > **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="e983e-139">Under hello batch trigger, choose **+ New Step** > **Add an action**.</span></span>

   2. <span data-ttu-id="e983e-140">Voer in het zoekvak hello, 'e' als filter.</span><span class="sxs-lookup"><span data-stu-id="e983e-140">In hello search box, enter "email" as your filter.</span></span>
   <span data-ttu-id="e983e-141">Op basis van uw e-mailprovider, selecteert u een e-connector.</span><span class="sxs-lookup"><span data-stu-id="e983e-141">Based on your email provider, select an email connector.</span></span>
   
      <span data-ttu-id="e983e-142">Als u een account voor werk of school hebt, Selecteer bijvoorbeeld Hallo Outlook van Office 365-connector.</span><span class="sxs-lookup"><span data-stu-id="e983e-142">For example, if you have a work or school account, select hello Office 365 Outlook connector.</span></span> 
      <span data-ttu-id="e983e-143">Als u een Gmail-account hebt, selecteert u Hallo Gmail connector.</span><span class="sxs-lookup"><span data-stu-id="e983e-143">If you have a Gmail account, select hello Gmail connector.</span></span>

   3. <span data-ttu-id="e983e-144">Deze actie voor de connector selecteert:  **{*e-mailprovider*}-sturen een e-mail **</span><span class="sxs-lookup"><span data-stu-id="e983e-144">Select this action for your connector: **{*email provider*} - Send an email**</span></span>

      <span data-ttu-id="e983e-145">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e983e-145">For example:</span></span>

      ![Selecteer de actie 'E-mailbericht verzenden' voor uw e-mailprovider](./media/logic-apps-batch-process-send-receive-messages/add-send-email-action.png)

5. <span data-ttu-id="e983e-147">Als u niet eerder verbinding kunt voor uw e-mailprovider maken, moet u uw e-referenties opgeven voor verificatie wanneer u wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="e983e-147">If you didn't previously create a connection for your email provider, provide your email credentials for authentication when prompted.</span></span> <span data-ttu-id="e983e-148">Meer informatie over [verifiëren van de referenties van uw e-mailadres](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="e983e-148">Learn more about [authenticating your email credentials](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

6. <span data-ttu-id="e983e-149">Hallo eigenschappen instellen voor Hallo-actie die u zojuist hebt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="e983e-149">Set hello properties for hello action you just added.</span></span>

   * <span data-ttu-id="e983e-150">In Hallo **naar** Voer Hallo ontvanger van e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="e983e-150">In hello **To** box, enter hello recipient's email address.</span></span> 
   <span data-ttu-id="e983e-151">U kunt uw eigen e-mailadres gebruiken voor testdoeleinden.</span><span class="sxs-lookup"><span data-stu-id="e983e-151">For testing purposes, you can use your own email address.</span></span>

   * <span data-ttu-id="e983e-152">In Hallo **onderwerp** vak wanneer hello **dynamische inhoud** lijst wordt weergegeven, selecteert u Hallo **partitienaam** veld.</span><span class="sxs-lookup"><span data-stu-id="e983e-152">In hello **Subject** box, when hello **Dynamic content** list appears, select hello **Partition Name** field.</span></span>

     ![Selecteer 'Partitienaam' Hallo 'Dynamische inhoud' lijst](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details.png)

     <span data-ttu-id="e983e-154">In een volgende sectie, kunt u opgeven dat delen doel batch Hallo in logische unieke partitiesleutel ingesteld toowhere kunt u berichten verzenden.</span><span class="sxs-lookup"><span data-stu-id="e983e-154">In a later section, you can specify a unique partition key that divides hello target batch into logical sets toowhere you can send messages.</span></span> 
     <span data-ttu-id="e983e-155">Elke set heeft een uniek nummer dat wordt gegenereerd door Hallo afzender logische app.</span><span class="sxs-lookup"><span data-stu-id="e983e-155">Each set has a unique number that's generated by hello sender logic app.</span></span> 
     <span data-ttu-id="e983e-156">Deze mogelijkheid kunt u één batch met meerdere subsets gebruikt, en elke subset met Hallo-naam die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="e983e-156">This capability lets you use a single batch with multiple subsets and define each subset with hello name that you provide.</span></span>

   * <span data-ttu-id="e983e-157">In Hallo **hoofdtekst** vak wanneer hello **dynamische inhoud** lijst wordt weergegeven, selecteert u Hallo **bericht-Id** veld.</span><span class="sxs-lookup"><span data-stu-id="e983e-157">In hello **Body** box, when hello **Dynamic content** list appears, select hello **Message Id** field.</span></span>

     ![Selecteer voor 'Hoofdtekst', 'bericht-Id](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details-for-each.png)

     <span data-ttu-id="e983e-159">Omdat het Hallo-invoer voor Hallo verzenden e-actie is een matrix, voegt Hallo designer automatisch een **voor elk** lus rond Hallo **e-mailbericht verzenden** in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="e983e-159">Because hello input for hello send email action is an array, hello designer automatically adds a **For each** loop around hello **Send an email** action.</span></span> 
     <span data-ttu-id="e983e-160">Deze lus voert Hallo binnenste actie op elk item in Hallo batch.</span><span class="sxs-lookup"><span data-stu-id="e983e-160">This loop performs hello inner action on each item in hello batch.</span></span> 
     <span data-ttu-id="e983e-161">Dus met Hallo batch trigger set toofive items krijgt u vijf e-mailberichten die elke keer Hallo trigger wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="e983e-161">So, with hello batch trigger set toofive items, you get five emails each time hello trigger fires.</span></span>

7.  <span data-ttu-id="e983e-162">Nu dat u een batch ontvanger logische app hebt gemaakt, sla uw logische app.</span><span class="sxs-lookup"><span data-stu-id="e983e-162">Now that you created a batch receiver logic app, save your logic app.</span></span>

    ![Uw logische app opslaan](./media/logic-apps-batch-process-send-receive-messages/save-batch-receiver-logic-app.png)

<a name="batch-sender"></a>

## <a name="create-logic-apps-that-send-messages-tooa-batch"></a><span data-ttu-id="e983e-164">Maken van logische apps die berichten tooa batch verzenden</span><span class="sxs-lookup"><span data-stu-id="e983e-164">Create logic apps that send messages tooa batch</span></span>

<span data-ttu-id="e983e-165">Maak nu een of meer logische apps die items toohello batch gedefinieerd door Hallo ontvanger logische app verzendt.</span><span class="sxs-lookup"><span data-stu-id="e983e-165">Now create one or more logic apps that send items toohello batch defined by hello receiver logic app.</span></span> <span data-ttu-id="e983e-166">Voor de afzender hello geeft u Hallo ontvanger logische app en de batchnaam van de, inhoud van het bericht en eventuele andere instellingen.</span><span class="sxs-lookup"><span data-stu-id="e983e-166">For hello sender, you specify hello receiver logic app and batch name, message content, and any other settings.</span></span> <span data-ttu-id="e983e-167">Desgewenst kunt u een unieke partitie sleutel toodivide Hallo batch in subsets toocollect items met die sleutel opgeven.</span><span class="sxs-lookup"><span data-stu-id="e983e-167">You can optionally provide a unique partition key toodivide hello batch into subsets toocollect items with that key.</span></span>

<span data-ttu-id="e983e-168">Afzender logische apps moeten weten waar toosend items, terwijl de ontvanger logische apps tooknow alles over Hallo afzenders niet nodig.</span><span class="sxs-lookup"><span data-stu-id="e983e-168">Sender logic apps need know where toosend items, while receiver logic apps don't need tooknow anything about hello senders.</span></span>

1. <span data-ttu-id="e983e-169">Een andere logische app maken met deze naam: 'BatchSender'</span><span class="sxs-lookup"><span data-stu-id="e983e-169">Create another logic app with this name: "BatchSender"</span></span>

   1. <span data-ttu-id="e983e-170">Voer in het zoekvak Hallo "recurrence" als filter.</span><span class="sxs-lookup"><span data-stu-id="e983e-170">In hello search box, enter "recurrence" as your filter.</span></span> 
   <span data-ttu-id="e983e-171">Selecteer deze trigger: **schema - terugkeerpatroon**</span><span class="sxs-lookup"><span data-stu-id="e983e-171">Select this trigger: **Schedule - Recurrence**</span></span>

      ![Hallo "Terugkeerpatroon plannen" trigger toevoegen](./media/logic-apps-batch-process-send-receive-messages/add-schedule-trigger-batch-receiver.png)

   2. <span data-ttu-id="e983e-173">Hallo-frequentie en interval toorun Hallo afzender logische app elke minuut instellen.</span><span class="sxs-lookup"><span data-stu-id="e983e-173">Set hello frequency and interval toorun hello sender logic app every minute.</span></span>

      ![Frequentie en het interval voor de trigger terugkeerpatroon ingesteld](./media/logic-apps-batch-process-send-receive-messages/recurrence-trigger-batch-receiver-details.png)

2. <span data-ttu-id="e983e-175">Voeg een nieuwe stap voor het verzenden van berichten tooa batch.</span><span class="sxs-lookup"><span data-stu-id="e983e-175">Add a new step for sending messages tooa batch.</span></span>

   1. <span data-ttu-id="e983e-176">Kies onder Hallo terugkeerpatroon trigger **+ een nieuwe stap** > **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="e983e-176">Under hello recurrence trigger, choose **+ New Step** > **Add an action**.</span></span>

   2. <span data-ttu-id="e983e-177">Voer in het zoekvak hello, 'batch' als filter.</span><span class="sxs-lookup"><span data-stu-id="e983e-177">In hello search box, enter "batch" as your filter.</span></span> 

   3. <span data-ttu-id="e983e-178">Deze actie selecteert: **verzenden van berichten toobatch: Kies een werkstroom Logic Apps met batch-trigger**</span><span class="sxs-lookup"><span data-stu-id="e983e-178">Select this action: **Send messages toobatch – Choose a Logic Apps workflow with batch trigger**</span></span>

      ![Selecteer 'Verzenden berichten toobatch'](./media/logic-apps-batch-process-send-receive-messages/send-messages-batch-action.png)

   4. <span data-ttu-id="e983e-180">Nu uw 'BatchReceiver' logische app die u eerder hebt gemaakt, die nu wordt weergegeven als een actie selecteren.</span><span class="sxs-lookup"><span data-stu-id="e983e-180">Now select your "BatchReceiver" logic app that you previously created, which now appears as an action.</span></span>

      !['Batch ontvanger' logische app selecteren](./media/logic-apps-batch-process-send-receive-messages/send-batch-select-batch-receiver.png)

      > [!NOTE]
      > <span data-ttu-id="e983e-182">Hallo-lijst bevat ook andere logic apps waarvoor de batch-triggers.</span><span class="sxs-lookup"><span data-stu-id="e983e-182">hello list also shows any other logic apps that have batch triggers.</span></span>

3. <span data-ttu-id="e983e-183">Hallo Batcheigenschappen instellen.</span><span class="sxs-lookup"><span data-stu-id="e983e-183">Set hello batch properties.</span></span>

   * <span data-ttu-id="e983e-184">**Batch-naam**: de naam van de batch Hallo gedefinieerd Hallo ontvanger logische app, die 'TestBatch' in dit voorbeeld en wordt gevalideerd tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="e983e-184">**Batch Name**: hello batch name defined by hello receiver logic app, which is "TestBatch" in this example and is validated at runtime.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="e983e-185">Zorg ervoor dat u Hallo batchnaam, die moet overeenkomen met Hallo batchnaam die opgegeven door Hallo ontvanger logische app niet te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="e983e-185">Make sure that you don't change hello batch name, which must match hello batch name that's specified by hello receiver logic app.</span></span>
     > <span data-ttu-id="e983e-186">Naam van de batch veranderende Hallo zorgt ervoor dat Hallo afzender logic app toofail.</span><span class="sxs-lookup"><span data-stu-id="e983e-186">Changing hello batch name causes hello sender logic app toofail.</span></span>

   * <span data-ttu-id="e983e-187">**Inhoud bericht**: inhoud van het bericht dat u wilt dat toosend Hallo.</span><span class="sxs-lookup"><span data-stu-id="e983e-187">**Message Content**: hello message content that you want toosend.</span></span> 
   <span data-ttu-id="e983e-188">Voor dit voorbeeld voegen deze expressie Hallo huidige datum en tijd van toevoegingen, in het Hallo-bericht inhoud die u toohello batch verzendt:</span><span class="sxs-lookup"><span data-stu-id="e983e-188">For this example, add this expression that inserts hello current date and time into hello message content that you send toohello batch:</span></span>

     1. <span data-ttu-id="e983e-189">Wanneer Hallo **dynamische inhoud** lijst wordt weergegeven, kies **expressie**.</span><span class="sxs-lookup"><span data-stu-id="e983e-189">When hello **Dynamic content** list appears, choose **Expression**.</span></span> 
     2. <span data-ttu-id="e983e-190">Voer Hallo expressie **utcnow()**, en kies **OK**.</span><span class="sxs-lookup"><span data-stu-id="e983e-190">Enter hello expression **utcnow()**, and choose **OK**.</span></span> 

        ![Kies in 'Bericht inhoud', 'Expressie'.](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details.png)

4. <span data-ttu-id="e983e-193">Nu ingesteld op een partitie voor Hallo batch.</span><span class="sxs-lookup"><span data-stu-id="e983e-193">Now set up a partition for hello batch.</span></span> <span data-ttu-id="e983e-194">Kies in de actie 'BatchReceiver' hello, **geavanceerde opties weergeven**.</span><span class="sxs-lookup"><span data-stu-id="e983e-194">In hello "BatchReceiver" action, choose **Show advanced options**.</span></span>

   * <span data-ttu-id="e983e-195">**De naam van partitie**: een optionele unieke partitie sleutel toouse voor het verdelen van Hallo doel batch.</span><span class="sxs-lookup"><span data-stu-id="e983e-195">**Partition Name**: An optional unique partition key toouse for dividing hello target batch.</span></span> <span data-ttu-id="e983e-196">Voor dit voorbeeld voegt u een expressie die een willekeurig getal tussen een en vijf genereert.</span><span class="sxs-lookup"><span data-stu-id="e983e-196">For this example, add an expression that generates a random number between one and five.</span></span>
   
     1. <span data-ttu-id="e983e-197">Wanneer Hallo **dynamische inhoud** lijst wordt weergegeven, kies **expressie**.</span><span class="sxs-lookup"><span data-stu-id="e983e-197">When hello **Dynamic content** list appears, choose **Expression**.</span></span>
     2. <span data-ttu-id="e983e-198">Voer deze expressie: **rand(1,6)**</span><span class="sxs-lookup"><span data-stu-id="e983e-198">Enter this expression: **rand(1,6)**</span></span>

        ![Instellen van een partitie voor de doel-batch](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-partition-advanced-options.png)

        <span data-ttu-id="e983e-200">Dit **RNG** functie genereert een getal tussen 1 en 5.</span><span class="sxs-lookup"><span data-stu-id="e983e-200">This **rand** function generates a number between one and five.</span></span> 
        <span data-ttu-id="e983e-201">U zijn zodat deze batch verdelen in vijf genummerde partities, waarmee deze expressie voor het dynamisch wordt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="e983e-201">So you are dividing this batch into five numbered partitions, which this expression dynamically sets.</span></span>

   * <span data-ttu-id="e983e-202">**Bericht-Id**: een optionele bericht-id en een gegenereerde GUID wanneer leeg is.</span><span class="sxs-lookup"><span data-stu-id="e983e-202">**Message Id**: An optional message identifier and is a generated GUID when empty.</span></span> 
   <span data-ttu-id="e983e-203">In dit voorbeeld laat u dit vak leeg.</span><span class="sxs-lookup"><span data-stu-id="e983e-203">For this example, leave this box blank.</span></span>

5. <span data-ttu-id="e983e-204">Sla uw logische app.</span><span class="sxs-lookup"><span data-stu-id="e983e-204">Save your logic app.</span></span> <span data-ttu-id="e983e-205">Uw afzender logische app zoekt nu vergelijkbaar toothis voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e983e-205">Your sender logic app now looks similar toothis example:</span></span>

   ![Sla uw logische app van afzender](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details-finished.png)

## <a name="test-your-logic-apps"></a><span data-ttu-id="e983e-207">Uw logische apps testen</span><span class="sxs-lookup"><span data-stu-id="e983e-207">Test your logic apps</span></span>

<span data-ttu-id="e983e-208">tootest uw oplossing, batchverwerking laat uw logische apps uitgevoerd voor een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="e983e-208">tootest your batching solution, leave your logic apps running for a few minutes.</span></span> <span data-ttu-id="e983e-209">Binnenkort u begint met het ophalen van e-mailberichten in groepen van vijf, Hallo met dezelfde sleutel partitie.</span><span class="sxs-lookup"><span data-stu-id="e983e-209">Soon, you start getting emails in groups of five, all with hello same partition key.</span></span>

<span data-ttu-id="e983e-210">Uw BatchSender logische app uitgevoerd elke minuut, genereert een willekeurig getal tussen 1 en 5 en maakt gebruik van deze gegenereerd nummer als partitiesleutel Hallo voor Hallo doel batch waarin berichten worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="e983e-210">Your BatchSender logic app runs every minute, generates a random number between one and five, and uses this generated number as hello partition key for hello target batch where messages are sent.</span></span> <span data-ttu-id="e983e-211">Telkens wanneer Hallo batch vijf items Hello bevat dezelfde partitiesleutel uw BatchReceiver logische app wordt geactiveerd en e-mail voor elk bericht verzendt.</span><span class="sxs-lookup"><span data-stu-id="e983e-211">Each time hello batch has five items with hello same partition key, your BatchReceiver logic app fires and sends mail for each message.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e983e-212">Wanneer u klaar bent testen, zorg ervoor dat Hallo BatchSender logic app toostop verzenden van berichten uit te schakelen en te voorkomen dat uw postvak in overbelasting.</span><span class="sxs-lookup"><span data-stu-id="e983e-212">When you're done testing, make sure that you disable hello BatchSender logic app toostop sending messages and avoid overloading your inbox.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e983e-213">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e983e-213">Next steps</span></span>

* [<span data-ttu-id="e983e-214">Maken van logic app-definities met behulp van JSON</span><span class="sxs-lookup"><span data-stu-id="e983e-214">Build on logic app definitions by using JSON</span></span>](../logic-apps/logic-apps-author-definitions.md)
* [<span data-ttu-id="e983e-215">Een zonder server-App in Visual Studio met Azure Logic Apps en functies</span><span class="sxs-lookup"><span data-stu-id="e983e-215">Build a serverless app in Visual Studio with Azure Logic Apps and Functions</span></span>](../logic-apps/logic-apps-serverless-get-started-vs.md)
* [<span data-ttu-id="e983e-216">Afhandeling van uitzonderingen en foutenregistratie voor logic apps</span><span class="sxs-lookup"><span data-stu-id="e983e-216">Exception handling and error logging for logic apps</span></span>](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
