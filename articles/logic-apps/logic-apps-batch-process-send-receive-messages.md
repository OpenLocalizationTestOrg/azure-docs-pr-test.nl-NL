---
title: Batch-berichten verwerken als een groep of een verzameling - Azure Logic Apps | Microsoft Docs
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
ms.openlocfilehash: 480ffce5dbe7c25181bb0ba5639de884e98ff4e6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="send-receive-and-batch-process-messages-in-logic-apps"></a><span data-ttu-id="0d7a9-104">Verzenden, ontvangen en verwerken van berichten in logic apps batch</span><span class="sxs-lookup"><span data-stu-id="0d7a9-104">Send, receive, and batch process messages in logic apps</span></span>

<span data-ttu-id="0d7a9-105">Voor het verwerken van berichten samen in groepen, u kunt verzenden gegevensitems of berichten naar een *batch*, en vervolgens deze items als een batch te verwerken.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-105">To process messages together in groups, you can send data items, or messages, to a *batch*, and then process those items as a batch.</span></span> <span data-ttu-id="0d7a9-106">Deze methode is handig als u wilt controleren of gegevensitems worden gegroepeerd in een bepaalde manier en samen worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-106">This approach is useful when you want to make sure data items are grouped in a specific way and are processed together.</span></span> 

<span data-ttu-id="0d7a9-107">Kunt u logic apps die items als een batch met behulp van ontvangen de **Batch** trigger.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-107">You can create logic apps that receive items as a batch by using the **Batch** trigger.</span></span> <span data-ttu-id="0d7a9-108">Vervolgens kunt u maken logic apps die items naar een batch te met behulp van verzenden de **Batch** in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-108">You can then create logic apps that send items to a batch by using the **Batch** action.</span></span>

<span data-ttu-id="0d7a9-109">Dit onderwerp wordt beschreven hoe u een batchen oplossing kunt maken met het uitvoeren van deze taken:</span><span class="sxs-lookup"><span data-stu-id="0d7a9-109">This topic shows how you can build a batching solution by performing these tasks:</span></span> 

* <span data-ttu-id="0d7a9-110">[Maken van een logische app dat ontvangt en verzamelt items als batch](#batch-receiver).</span><span class="sxs-lookup"><span data-stu-id="0d7a9-110">[Create a logic app that receives and collects items as a batch](#batch-receiver).</span></span> <span data-ttu-id="0d7a9-111">Deze 'batch ontvanger' logische app geeft de batch-naam en release criteria om te voldoen aan voordat u de ontvanger logische app vrijgegeven en worden items verwerkt.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-111">This "batch receiver" logic app specifies the batch name and release criteria to meet before the receiver logic app releases and processes items.</span></span> 

* <span data-ttu-id="0d7a9-112">[Maken van een logische app waarmee items worden verzonden naar een batch](#batch-sender).</span><span class="sxs-lookup"><span data-stu-id="0d7a9-112">[Create a logic app that sends items to a batch](#batch-sender).</span></span> <span data-ttu-id="0d7a9-113">Deze 'batch afzender' logische app geeft aan waar items, die een bestaande batch ontvanger logic app moet verzenden.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-113">This "batch sender" logic app specifies where to send items, which must be an existing batch receiver logic app.</span></span> <span data-ttu-id="0d7a9-114">U kunt ook een unieke sleutel, zoals een klantnummer 'partitie' of delen, de doel-batch in subsets op basis van die sleutel opgeven.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-114">You can also specify a unique key, like a customer number, to "partition", or divide, the target batch into subsets based on that key.</span></span> <span data-ttu-id="0d7a9-115">Op die manier worden alle items met die sleutel verzameld en verwerkt samen.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-115">That way, all items with that key are collected and processed together.</span></span> 

## <a name="requirements"></a><span data-ttu-id="0d7a9-116">Vereisten</span><span class="sxs-lookup"><span data-stu-id="0d7a9-116">Requirements</span></span>

<span data-ttu-id="0d7a9-117">Wilt u dit voorbeeld gebruiken, moet u deze items:</span><span class="sxs-lookup"><span data-stu-id="0d7a9-117">To follow this example, you need these items:</span></span>

* <span data-ttu-id="0d7a9-118">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-118">An Azure subscription.</span></span> <span data-ttu-id="0d7a9-119">Als u geen abonnement hebt, kunt u [beginnen met een gratis Azure-account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="0d7a9-119">If you don't have a subscription, you can [start with a free Azure account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="0d7a9-120">U kunt eventueel ook direct kiezen voor [een Betalen per gebruik-abonnement](https://azure.microsoft.com/pricing/purchase-options/).</span><span class="sxs-lookup"><span data-stu-id="0d7a9-120">Otherwise, you can [sign up for a Pay-As-You-Go subscription](https://azure.microsoft.com/pricing/purchase-options/).</span></span>

* <span data-ttu-id="0d7a9-121">Elementaire kennis over [logic apps maken](../logic-apps/logic-apps-create-a-logic-app.md)</span><span class="sxs-lookup"><span data-stu-id="0d7a9-121">Basic knowledge about [how to create logic apps](../logic-apps/logic-apps-create-a-logic-app.md)</span></span> 

* <span data-ttu-id="0d7a9-122">Een e-mailaccount met een [e-provider wordt ondersteund door Azure Logic Apps](../connectors/apis-list.md)</span><span class="sxs-lookup"><span data-stu-id="0d7a9-122">An email account with any [email provider supported by Azure Logic Apps](../connectors/apis-list.md)</span></span>

<a name="batch-receiver"></a>

## <a name="create-logic-apps-that-receive-messages-as-a-batch"></a><span data-ttu-id="0d7a9-123">Logic apps die berichten te als een batch ontvangen maken</span><span class="sxs-lookup"><span data-stu-id="0d7a9-123">Create logic apps that receive messages as a batch</span></span>

<span data-ttu-id="0d7a9-124">Voordat u berichten naar een batch verzenden kunt, moet u eerst een 'batch ontvanger' logische app met maken de **Batch** trigger.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-124">Before you can send messages to a batch, you must first create a "batch receiver" logic app with the **Batch** trigger.</span></span> <span data-ttu-id="0d7a9-125">Op die manier kunt u deze ontvanger logic app bij het maken van de afzender logische app.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-125">That way, you can select this receiver logic app when you create the sender logic app.</span></span> <span data-ttu-id="0d7a9-126">Voor de ontvanger geeft u de batchnaam van de, release criteria en andere instellingen.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-126">For the receiver, you specify the batch name, release criteria, and other settings.</span></span> 

<span data-ttu-id="0d7a9-127">Afzender logische apps moeten weten waar items, terwijl de ontvanger logische apps hoeft niet te weten over de afzenders.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-127">Sender logic apps need know where to send items, while receiver logic apps don't need to know anything about the senders.</span></span>

1. <span data-ttu-id="0d7a9-128">In de [Azure-portal](https://portal.azure.com), een logische app maken met deze naam: 'BatchReceiver'</span><span class="sxs-lookup"><span data-stu-id="0d7a9-128">In the [Azure portal](https://portal.azure.com), create a logic app with this name: "BatchReceiver"</span></span> 

2. <span data-ttu-id="0d7a9-129">In Logic Apps Designer, voegt u de **Batch** trigger uw logische app-werkstroom op te starten.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-129">In Logic Apps Designer, add the **Batch** trigger, which starts your logic app workflow.</span></span> <span data-ttu-id="0d7a9-130">Voer in het zoekvak 'batch' als filter.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-130">In the search box, enter "batch" as your filter.</span></span> <span data-ttu-id="0d7a9-131">Selecteer deze trigger: **Batch: Batch-berichten**</span><span class="sxs-lookup"><span data-stu-id="0d7a9-131">Select this trigger: **Batch – Batch messages**</span></span>

   ![Batch-trigger toevoegen](./media/logic-apps-batch-process-send-receive-messages/add-batch-receiver-trigger.png)

3. <span data-ttu-id="0d7a9-133">Geef een naam voor de batch en Geef criteria op voor het vrijgeven van de batch, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="0d7a9-133">Provide a name for the batch, and specify criteria for releasing the batch, for example:</span></span>

   * <span data-ttu-id="0d7a9-134">**Batch-naam**: de naam die wordt gebruikt voor het identificeren van de batch is 'TestBatch' in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-134">**Batch Name**: The name used to identify the batch, which is "TestBatch" in this example.</span></span>
   * <span data-ttu-id="0d7a9-135">**Aantal berichten**: het aantal berichten voor het opslaan als een batch voordat voor verwerking, namelijk '5' in dit voorbeeld zijn vrijgegeven.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-135">**Message Count**: The number of messages to hold as a batch before releasing for processing, which is "5" in this example.</span></span>

   ![Geef details op Batch trigger](./media/logic-apps-batch-process-send-receive-messages/receive-batch-trigger-details.png)

4. <span data-ttu-id="0d7a9-137">Voeg een andere actie die een e-mailbericht wordt verzonden wanneer de batch-trigger wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-137">Add another action that sends an email when the batch trigger fires.</span></span> <span data-ttu-id="0d7a9-138">Telkens wanneer die de batch vijf items heeft in de logische app verzendt een e-mailbericht.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-138">Each time the batch has five items, the logic app sends an email.</span></span>

   1. <span data-ttu-id="0d7a9-139">Kies onder de trigger batch **+ een nieuwe stap** > **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-139">Under the batch trigger, choose **+ New Step** > **Add an action**.</span></span>

   2. <span data-ttu-id="0d7a9-140">Voer in het zoekvak 'e' als filter.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-140">In the search box, enter "email" as your filter.</span></span>
   <span data-ttu-id="0d7a9-141">Op basis van uw e-mailprovider, selecteert u een e-connector.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-141">Based on your email provider, select an email connector.</span></span>
   
      <span data-ttu-id="0d7a9-142">Als u een account voor werk of school hebt, Selecteer bijvoorbeeld de Outlook van Office 365-connector.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-142">For example, if you have a work or school account, select the Office 365 Outlook connector.</span></span> 
      <span data-ttu-id="0d7a9-143">Als u een Gmail-account hebt, selecteert u de connector Gmail.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-143">If you have a Gmail account, select the Gmail connector.</span></span>

   3. <span data-ttu-id="0d7a9-144">Deze actie voor de connector selecteert:  **{*e-mailprovider*}-sturen een e-mail **</span><span class="sxs-lookup"><span data-stu-id="0d7a9-144">Select this action for your connector: **{*email provider*} - Send an email**</span></span>

      <span data-ttu-id="0d7a9-145">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="0d7a9-145">For example:</span></span>

      ![Selecteer de actie 'E-mailbericht verzenden' voor uw e-mailprovider](./media/logic-apps-batch-process-send-receive-messages/add-send-email-action.png)

5. <span data-ttu-id="0d7a9-147">Als u niet eerder verbinding kunt voor uw e-mailprovider maken, moet u uw e-referenties opgeven voor verificatie wanneer u wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-147">If you didn't previously create a connection for your email provider, provide your email credentials for authentication when prompted.</span></span> <span data-ttu-id="0d7a9-148">Meer informatie over [verifiëren van de referenties van uw e-mailadres](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="0d7a9-148">Learn more about [authenticating your email credentials](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

6. <span data-ttu-id="0d7a9-149">Stel de eigenschappen voor de actie die u zojuist hebt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-149">Set the properties for the action you just added.</span></span>

   * <span data-ttu-id="0d7a9-150">In de **naar** Voer het e-mailadres van de geadresseerde.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-150">In the **To** box, enter the recipient's email address.</span></span> 
   <span data-ttu-id="0d7a9-151">U kunt uw eigen e-mailadres gebruiken voor testdoeleinden.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-151">For testing purposes, you can use your own email address.</span></span>

   * <span data-ttu-id="0d7a9-152">In de **onderwerp** vak, wanneer de **dynamische inhoud** lijst wordt weergegeven, selecteert u de **partitienaam** veld.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-152">In the **Subject** box, when the **Dynamic content** list appears, select the **Partition Name** field.</span></span>

     ![Selecteer in de lijst 'Dynamische inhoud', 'Partitienaam'](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details.png)

     <span data-ttu-id="0d7a9-154">In een volgende sectie, kunt u een unieke partitiesleutel die verdeelt de doel-batch in logische groepen waarbij u kunt om berichten te verzenden.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-154">In a later section, you can specify a unique partition key that divides the target batch into logical sets to where you can send messages.</span></span> 
     <span data-ttu-id="0d7a9-155">Elke set heeft een uniek nummer dat wordt gegenereerd door de afzender logische app.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-155">Each set has a unique number that's generated by the sender logic app.</span></span> 
     <span data-ttu-id="0d7a9-156">Deze mogelijkheid kunt u één batch met meerdere subsets gebruikt, en elke subset met de naam die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-156">This capability lets you use a single batch with multiple subsets and define each subset with the name that you provide.</span></span>

   * <span data-ttu-id="0d7a9-157">In de **hoofdtekst** vak, wanneer de **dynamische inhoud** lijst wordt weergegeven, selecteert u de **bericht-Id** veld.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-157">In the **Body** box, when the **Dynamic content** list appears, select the **Message Id** field.</span></span>

     ![Selecteer voor 'Hoofdtekst', 'bericht-Id](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details-for-each.png)

     <span data-ttu-id="0d7a9-159">Omdat de invoer voor de e-mailbericht verzendactie een matrix is, voegt de ontwerpfunctie automatisch een **voor elk** lus rond de **e-mailbericht verzenden** in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-159">Because the input for the send email action is an array, the designer automatically adds a **For each** loop around the **Send an email** action.</span></span> 
     <span data-ttu-id="0d7a9-160">Deze lus voert de interne actie op elk item in de batch.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-160">This loop performs the inner action on each item in the batch.</span></span> 
     <span data-ttu-id="0d7a9-161">Dus met de batch-trigger is ingesteld op vijf items, beschikt u over tijd vijf e-mails die de trigger wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-161">So, with the batch trigger set to five items, you get five emails each time the trigger fires.</span></span>

7.  <span data-ttu-id="0d7a9-162">Nu dat u een batch ontvanger logische app hebt gemaakt, sla uw logische app.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-162">Now that you created a batch receiver logic app, save your logic app.</span></span>

    ![Uw logische app opslaan](./media/logic-apps-batch-process-send-receive-messages/save-batch-receiver-logic-app.png)

<a name="batch-sender"></a>

## <a name="create-logic-apps-that-send-messages-to-a-batch"></a><span data-ttu-id="0d7a9-164">Logic apps die berichten naar een batch verzenden maken</span><span class="sxs-lookup"><span data-stu-id="0d7a9-164">Create logic apps that send messages to a batch</span></span>

<span data-ttu-id="0d7a9-165">Maak nu een of meer logische apps die items naar de batch gedefinieerd door de ontvanger logische app verzendt.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-165">Now create one or more logic apps that send items to the batch defined by the receiver logic app.</span></span> <span data-ttu-id="0d7a9-166">Voor de afzender geeft u de ontvanger logische app en de batchnaam van de, inhoud van het bericht en eventuele andere instellingen.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-166">For the sender, you specify the receiver logic app and batch name, message content, and any other settings.</span></span> <span data-ttu-id="0d7a9-167">U kunt eventueel een unieke partitiesleutel voor het delen van de batch in deelverzamelingen voor het verzamelen van items met die sleutel opgeven.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-167">You can optionally provide a unique partition key to divide the batch into subsets to collect items with that key.</span></span>

<span data-ttu-id="0d7a9-168">Afzender logische apps moeten weten waar items, terwijl de ontvanger logische apps hoeft niet te weten over de afzenders.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-168">Sender logic apps need know where to send items, while receiver logic apps don't need to know anything about the senders.</span></span>

1. <span data-ttu-id="0d7a9-169">Een andere logische app maken met deze naam: 'BatchSender'</span><span class="sxs-lookup"><span data-stu-id="0d7a9-169">Create another logic app with this name: "BatchSender"</span></span>

   1. <span data-ttu-id="0d7a9-170">Voer in het zoekvak "recurrence" als filter.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-170">In the search box, enter "recurrence" as your filter.</span></span> 
   <span data-ttu-id="0d7a9-171">Selecteer deze trigger: **schema - terugkeerpatroon**</span><span class="sxs-lookup"><span data-stu-id="0d7a9-171">Select this trigger: **Schedule - Recurrence**</span></span>

      ![Toevoegen van de trigger "Terugkeerpatroon plannen"](./media/logic-apps-batch-process-send-receive-messages/add-schedule-trigger-batch-receiver.png)

   2. <span data-ttu-id="0d7a9-173">Stel de frequentie en het interval om uit te voeren van de afzender logische app elke minuut.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-173">Set the frequency and interval to run the sender logic app every minute.</span></span>

      ![Frequentie en het interval voor de trigger terugkeerpatroon ingesteld](./media/logic-apps-batch-process-send-receive-messages/recurrence-trigger-batch-receiver-details.png)

2. <span data-ttu-id="0d7a9-175">Voeg een nieuwe stap voor het verzenden van berichten naar een batch.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-175">Add a new step for sending messages to a batch.</span></span>

   1. <span data-ttu-id="0d7a9-176">Kies onder de trigger terugkeerpatroon **+ een nieuwe stap** > **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-176">Under the recurrence trigger, choose **+ New Step** > **Add an action**.</span></span>

   2. <span data-ttu-id="0d7a9-177">Voer in het zoekvak 'batch' als filter.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-177">In the search box, enter "batch" as your filter.</span></span> 

   3. <span data-ttu-id="0d7a9-178">Deze actie selecteert: **berichten verzenden naar batch: Kies een werkstroom Logic Apps met batch-trigger**</span><span class="sxs-lookup"><span data-stu-id="0d7a9-178">Select this action: **Send messages to batch – Choose a Logic Apps workflow with batch trigger**</span></span>

      ![Selecteer 'Verzenden van berichten in een batch moet'](./media/logic-apps-batch-process-send-receive-messages/send-messages-batch-action.png)

   4. <span data-ttu-id="0d7a9-180">Nu uw 'BatchReceiver' logische app die u eerder hebt gemaakt, die nu wordt weergegeven als een actie selecteren.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-180">Now select your "BatchReceiver" logic app that you previously created, which now appears as an action.</span></span>

      !['Batch ontvanger' logische app selecteren](./media/logic-apps-batch-process-send-receive-messages/send-batch-select-batch-receiver.png)

      > [!NOTE]
      > <span data-ttu-id="0d7a9-182">De lijst bevat ook andere logic apps waarvoor de batch-triggers.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-182">The list also shows any other logic apps that have batch triggers.</span></span>

3. <span data-ttu-id="0d7a9-183">De Batcheigenschappen instellen.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-183">Set the batch properties.</span></span>

   * <span data-ttu-id="0d7a9-184">**Batch-naam**: de batchnaam gedefinieerd door de ontvanger logische app, die 'TestBatch' in dit voorbeeld en wordt gevalideerd tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-184">**Batch Name**: The batch name defined by the receiver logic app, which is "TestBatch" in this example and is validated at runtime.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="0d7a9-185">Zorg ervoor dat u de batchnaam, die moet overeenkomen met de batchnaam die wordt opgegeven door de ontvanger logische app niet te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-185">Make sure that you don't change the batch name, which must match the batch name that's specified by the receiver logic app.</span></span>
     > <span data-ttu-id="0d7a9-186">Als de batchnaam van de wijzigt, wordt de afzender logische app mislukken.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-186">Changing the batch name causes the sender logic app to fail.</span></span>

   * <span data-ttu-id="0d7a9-187">**Inhoud bericht**: de inhoud van het bericht dat u wilt verzenden.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-187">**Message Content**: The message content that you want to send.</span></span> 
   <span data-ttu-id="0d7a9-188">Voor dit voorbeeld voegen deze expressie die de huidige datum en tijd worden ingevoegd in de inhoud van het bericht dat u de batch verzenden:</span><span class="sxs-lookup"><span data-stu-id="0d7a9-188">For this example, add this expression that inserts the current date and time into the message content that you send to the batch:</span></span>

     1. <span data-ttu-id="0d7a9-189">Wanneer de **dynamische inhoud** lijst wordt weergegeven, kies **expressie**.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-189">When the **Dynamic content** list appears, choose **Expression**.</span></span> 
     2. <span data-ttu-id="0d7a9-190">Voer de expressie **utcnow()**, en kies **OK**.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-190">Enter the expression **utcnow()**, and choose **OK**.</span></span> 

        ![Kies in 'Bericht inhoud', 'Expressie'.](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details.png)

4. <span data-ttu-id="0d7a9-193">Nu ingesteld op een partitie voor de batch.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-193">Now set up a partition for the batch.</span></span> <span data-ttu-id="0d7a9-194">Kies in de actie 'BatchReceiver' **geavanceerde opties weergeven**.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-194">In the "BatchReceiver" action, choose **Show advanced options**.</span></span>

   * <span data-ttu-id="0d7a9-195">**De naam van partitie**: een optionele unieke partitiesleutel moet worden gebruikt voor het verdelen van de doel-batch.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-195">**Partition Name**: An optional unique partition key to use for dividing the target batch.</span></span> <span data-ttu-id="0d7a9-196">Voor dit voorbeeld voegt u een expressie die een willekeurig getal tussen een en vijf genereert.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-196">For this example, add an expression that generates a random number between one and five.</span></span>
   
     1. <span data-ttu-id="0d7a9-197">Wanneer de **dynamische inhoud** lijst wordt weergegeven, kies **expressie**.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-197">When the **Dynamic content** list appears, choose **Expression**.</span></span>
     2. <span data-ttu-id="0d7a9-198">Voer deze expressie: **rand(1,6)**</span><span class="sxs-lookup"><span data-stu-id="0d7a9-198">Enter this expression: **rand(1,6)**</span></span>

        ![Instellen van een partitie voor de doel-batch](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-partition-advanced-options.png)

        <span data-ttu-id="0d7a9-200">Dit **RNG** functie genereert een getal tussen 1 en 5.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-200">This **rand** function generates a number between one and five.</span></span> 
        <span data-ttu-id="0d7a9-201">U zijn zodat deze batch verdelen in vijf genummerde partities, waarmee deze expressie voor het dynamisch wordt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-201">So you are dividing this batch into five numbered partitions, which this expression dynamically sets.</span></span>

   * <span data-ttu-id="0d7a9-202">**Bericht-Id**: een optionele bericht-id en een gegenereerde GUID wanneer leeg is.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-202">**Message Id**: An optional message identifier and is a generated GUID when empty.</span></span> 
   <span data-ttu-id="0d7a9-203">In dit voorbeeld laat u dit vak leeg.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-203">For this example, leave this box blank.</span></span>

5. <span data-ttu-id="0d7a9-204">Sla uw logische app.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-204">Save your logic app.</span></span> <span data-ttu-id="0d7a9-205">Uw afzender logische app nu er ongeveer als volgt in dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="0d7a9-205">Your sender logic app now looks similar to this example:</span></span>

   ![Sla uw logische app van afzender](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details-finished.png)

## <a name="test-your-logic-apps"></a><span data-ttu-id="0d7a9-207">Uw logische apps testen</span><span class="sxs-lookup"><span data-stu-id="0d7a9-207">Test your logic apps</span></span>

<span data-ttu-id="0d7a9-208">Laat uw logische apps uitgevoerd voor een paar minuten voor het testen van uw batchen oplossing.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-208">To test your batching solution, leave your logic apps running for a few minutes.</span></span> <span data-ttu-id="0d7a9-209">U start binnenkort opvragen van e-mailberichten in groepen van vijf allemaal met dezelfde partitiesleutel.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-209">Soon, you start getting emails in groups of five, all with the same partition key.</span></span>

<span data-ttu-id="0d7a9-210">Uw BatchSender logische app uitgevoerd elke minuut, genereert een willekeurig getal tussen 1 en 5 en maakt gebruik van deze gegenereerd nummer als de partitiesleutel voor de doel-batch waarin berichten worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-210">Your BatchSender logic app runs every minute, generates a random number between one and five, and uses this generated number as the partition key for the target batch where messages are sent.</span></span> <span data-ttu-id="0d7a9-211">Telkens wanneer die de batch vijf items met dezelfde partitiesleutel bevat uw BatchReceiver logische app wordt gestart en e-mail voor elk bericht verzendt.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-211">Each time the batch has five items with the same partition key, your BatchReceiver logic app fires and sends mail for each message.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0d7a9-212">Wanneer u klaar bent testen, zorg ervoor dat de BatchSender logische app om te stoppen met het verzenden van berichten en te voorkomen dat uw postvak in overbelasting uit te schakelen.</span><span class="sxs-lookup"><span data-stu-id="0d7a9-212">When you're done testing, make sure that you disable the BatchSender logic app to stop sending messages and avoid overloading your inbox.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d7a9-213">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0d7a9-213">Next steps</span></span>

* [<span data-ttu-id="0d7a9-214">Maken van logic app-definities met behulp van JSON</span><span class="sxs-lookup"><span data-stu-id="0d7a9-214">Build on logic app definitions by using JSON</span></span>](../logic-apps/logic-apps-author-definitions.md)
* [<span data-ttu-id="0d7a9-215">Een zonder server-App in Visual Studio met Azure Logic Apps en functies</span><span class="sxs-lookup"><span data-stu-id="0d7a9-215">Build a serverless app in Visual Studio with Azure Logic Apps and Functions</span></span>](../logic-apps/logic-apps-serverless-get-started-vs.md)
* [<span data-ttu-id="0d7a9-216">Afhandeling van uitzonderingen en foutenregistratie voor logic apps</span><span class="sxs-lookup"><span data-stu-id="0d7a9-216">Exception handling and error logging for logic apps</span></span>](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
