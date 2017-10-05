---
title: Vastleggen van gegevens uit Event Hubs in Azure Data Lake Store | Microsoft Docs
description: Azure Data Lake Store gebruiken voor het vastleggen van gegevens uit Event Hubs
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/28/2017
ms.author: nitinme
ms.openlocfilehash: a9e69576958ae96d22a4eb03d0df429f0b307298
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-data-lake-store-to-capture-data-from-event-hubs"></a><span data-ttu-id="64f32-103">Azure Data Lake Store gebruiken voor het vastleggen van gegevens uit Event Hubs</span><span class="sxs-lookup"><span data-stu-id="64f32-103">Use Azure Data Lake Store to capture data from Event Hubs</span></span>

<span data-ttu-id="64f32-104">Informatie over het gebruik van Azure Data Lake Store voor het vastleggen van gegevens die zijn ontvangen door Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="64f32-104">Learn how to use Azure Data Lake Store to capture data received by Azure Event Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="64f32-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="64f32-105">Prerequisites</span></span>

* <span data-ttu-id="64f32-106">**Een Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="64f32-106">**An Azure subscription**.</span></span> <span data-ttu-id="64f32-107">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="64f32-107">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="64f32-108">**Een Azure Data Lake Store-account**.</span><span class="sxs-lookup"><span data-stu-id="64f32-108">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="64f32-109">Zie voor instructies over het maken van een [aan de slag met Azure Data Lake Store](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="64f32-109">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md).</span></span>

*  <span data-ttu-id="64f32-110">**Een naamruimte Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="64f32-110">**An Event Hubs namespace**.</span></span> <span data-ttu-id="64f32-111">Zie voor instructies [maken van een naamruimte Event Hubs](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace).</span><span class="sxs-lookup"><span data-stu-id="64f32-111">For instructions, see [Create an Event Hubs namespace](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace).</span></span> <span data-ttu-id="64f32-112">Zorg ervoor dat de Data Lake Store-account en de naamruimte van Event Hubs zijn in dezelfde Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="64f32-112">Make sure the Data Lake Store account and the Event Hubs namespace are in the same Azure subscription.</span></span>


## <a name="assign-permissions-to-event-hubs"></a><span data-ttu-id="64f32-113">Wijs machtigingen toe aan de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="64f32-113">Assign permissions to Event Hubs</span></span>

<span data-ttu-id="64f32-114">In deze sectie maakt u een map in het account waarbij u wilt vastleggen van de gegevens uit Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="64f32-114">In this section, you create a folder within the account where you want to capture the data from Event Hubs.</span></span> <span data-ttu-id="64f32-115">U ook toewijzen machtigingen aan Event Hubs zodat van gegevens naar een Data Lake Store-account schrijven.</span><span class="sxs-lookup"><span data-stu-id="64f32-115">You also assign permissions to Event Hubs so that it can write data into a Data Lake Store account.</span></span> 

1. <span data-ttu-id="64f32-116">Open de Data Lake Store-account waar u wilt vastleggen van gegevens uit Event Hubs en klik vervolgens op **Data Explorer**.</span><span class="sxs-lookup"><span data-stu-id="64f32-116">Open the Data Lake Store account where you want to capture data from Event Hubs and then click on **Data Explorer**.</span></span>

    <span data-ttu-id="64f32-117">![Data Lake Store Gegevensverkenner](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Gegevensverkenner Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="64f32-117">![Data Lake Store data explorer](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Data Lake Store data explorer")</span></span>

2.  <span data-ttu-id="64f32-118">Klik op **nieuwe map** en voer een naam voor de map waar u de gegevens vastlegt.</span><span class="sxs-lookup"><span data-stu-id="64f32-118">Click **New Folder** and then enter a name for folder where you want to capture the data.</span></span>

    <span data-ttu-id="64f32-119">![Een nieuwe map maken in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "een nieuwe map maken in Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="64f32-119">![Create a new folder in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "Create a new folder in Data Lake Store")</span></span>

3. <span data-ttu-id="64f32-120">Wijs machtigingen in de hoofdmap van de Data Lake Store toe.</span><span class="sxs-lookup"><span data-stu-id="64f32-120">Assign permissions at the root of the Data Lake Store.</span></span> 

    <span data-ttu-id="64f32-121">a.</span><span class="sxs-lookup"><span data-stu-id="64f32-121">a.</span></span> <span data-ttu-id="64f32-122">Klik op **Data Explorer**, selecteer de hoofdmap van het Data Lake Store-account en klik vervolgens op **toegang**.</span><span class="sxs-lookup"><span data-stu-id="64f32-122">Click **Data Explorer**, select the root of the Data Lake Store account, and then click **Access**.</span></span>

    <span data-ttu-id="64f32-123">![Machtigingen voor Data Lake Store-basis toe te wijzen](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "toegangsrechten voor de hoofdmap van de Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="64f32-123">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "Assign permissions for Data Lake Store root")</span></span>

    <span data-ttu-id="64f32-124">b.</span><span class="sxs-lookup"><span data-stu-id="64f32-124">b.</span></span> <span data-ttu-id="64f32-125">Onder **toegang**, klikt u op **toevoegen**, klikt u op **gebruiker of groep selecteren**, en zoek vervolgens naar `Microsoft.EventHubs`.</span><span class="sxs-lookup"><span data-stu-id="64f32-125">Under **Access**, click **Add**, click **Select User or Group**, and then search for `Microsoft.EventHubs`.</span></span> 

    <span data-ttu-id="64f32-126">![Machtigingen voor Data Lake Store-basis toe te wijzen](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "toegangsrechten voor de hoofdmap van de Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="64f32-126">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assign permissions for Data Lake Store root")</span></span>
    
    <span data-ttu-id="64f32-127">Klik op **Selecteren**.</span><span class="sxs-lookup"><span data-stu-id="64f32-127">Click **Select**.</span></span>

    <span data-ttu-id="64f32-128">c.</span><span class="sxs-lookup"><span data-stu-id="64f32-128">c.</span></span> <span data-ttu-id="64f32-129">Onder **machtigingen toewijzen**, klikt u op **Selecteer machtigingen**.</span><span class="sxs-lookup"><span data-stu-id="64f32-129">Under **Assign Permissions**, click **Select Permissions**.</span></span> <span data-ttu-id="64f32-130">Stel **machtigingen** naar **uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="64f32-130">Set **Permissions** to **Execute**.</span></span> <span data-ttu-id="64f32-131">Stel **toevoegen aan** naar **deze map en alle onderliggende**.</span><span class="sxs-lookup"><span data-stu-id="64f32-131">Set **Add to** to **This folder and all children**.</span></span> <span data-ttu-id="64f32-132">Stel **toevoegen als** naar **een machtigingsvermelding toegang en een standaard machtigingsvermelding**.</span><span class="sxs-lookup"><span data-stu-id="64f32-132">Set **Add as** to **An access permission entry and a default permission entry**.</span></span>

    <span data-ttu-id="64f32-133">![Machtigingen voor Data Lake Store-basis toe te wijzen](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "toegangsrechten voor de hoofdmap van de Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="64f32-133">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "Assign permissions for Data Lake Store root")</span></span>

    <span data-ttu-id="64f32-134">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="64f32-134">Click **OK**.</span></span>

4. <span data-ttu-id="64f32-135">Wijs machtigingen voor de map in Data Lake Store-account waar u wilt vastleggen van gegevens.</span><span class="sxs-lookup"><span data-stu-id="64f32-135">Assign permissions for the folder under Data Lake Store account where you want to capture data.</span></span>

    <span data-ttu-id="64f32-136">a.</span><span class="sxs-lookup"><span data-stu-id="64f32-136">a.</span></span> <span data-ttu-id="64f32-137">Klik op **Data Explorer**, selecteer de map in de Data Lake Store-account en klik vervolgens op **toegang**.</span><span class="sxs-lookup"><span data-stu-id="64f32-137">Click **Data Explorer**, select the folder in the Data Lake Store account, and then click **Access**.</span></span>

    <span data-ttu-id="64f32-138">![Wijs machtigingen voor Data Lake Store-map](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "machtigingen voor Data Lake Store-map toewijzen")</span><span class="sxs-lookup"><span data-stu-id="64f32-138">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "Assign permissions for Data Lake Store folder")</span></span>

    <span data-ttu-id="64f32-139">b.</span><span class="sxs-lookup"><span data-stu-id="64f32-139">b.</span></span> <span data-ttu-id="64f32-140">Onder **toegang**, klikt u op **toevoegen**, klikt u op **gebruiker of groep selecteren**, en zoek vervolgens naar `Microsoft.EventHubs`.</span><span class="sxs-lookup"><span data-stu-id="64f32-140">Under **Access**, click **Add**, click **Select User or Group**, and then search for `Microsoft.EventHubs`.</span></span> 

    <span data-ttu-id="64f32-141">![Wijs machtigingen voor Data Lake Store-map](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "machtigingen voor Data Lake Store-map toewijzen")</span><span class="sxs-lookup"><span data-stu-id="64f32-141">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assign permissions for Data Lake Store folder")</span></span>
    
    <span data-ttu-id="64f32-142">Klik op **Selecteren**.</span><span class="sxs-lookup"><span data-stu-id="64f32-142">Click **Select**.</span></span>

    <span data-ttu-id="64f32-143">c.</span><span class="sxs-lookup"><span data-stu-id="64f32-143">c.</span></span> <span data-ttu-id="64f32-144">Onder **machtigingen toewijzen**, klikt u op **Selecteer machtigingen**.</span><span class="sxs-lookup"><span data-stu-id="64f32-144">Under **Assign Permissions**, click **Select Permissions**.</span></span> <span data-ttu-id="64f32-145">Stel **machtigingen** naar **lezen, schrijven,** en **uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="64f32-145">Set **Permissions** to **Read, Write,** and **Execute**.</span></span> <span data-ttu-id="64f32-146">Stel **toevoegen aan** naar **deze map en alle onderliggende**.</span><span class="sxs-lookup"><span data-stu-id="64f32-146">Set **Add to** to **This folder and all children**.</span></span> <span data-ttu-id="64f32-147">Tot slot stelt **toevoegen als** naar **een machtigingsvermelding toegang en een standaard machtigingsvermelding**.</span><span class="sxs-lookup"><span data-stu-id="64f32-147">Finally, set **Add as** to **An access permission entry and a default permission entry**.</span></span>

    <span data-ttu-id="64f32-148">![Wijs machtigingen voor Data Lake Store-map](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "machtigingen voor Data Lake Store-map toewijzen")</span><span class="sxs-lookup"><span data-stu-id="64f32-148">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "Assign permissions for Data Lake Store folder")</span></span>
    
    <span data-ttu-id="64f32-149">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="64f32-149">Click **OK**.</span></span> 

## <a name="configure-event-hubs-to-capture-data-to-data-lake-store"></a><span data-ttu-id="64f32-150">Event Hubs voor het vastleggen van gegevens naar Data Lake Store configureren</span><span class="sxs-lookup"><span data-stu-id="64f32-150">Configure Event Hubs to capture data to Data Lake Store</span></span>

<span data-ttu-id="64f32-151">In deze sectie maakt u een Event Hub in een Event Hubs-naamruimte.</span><span class="sxs-lookup"><span data-stu-id="64f32-151">In this section, you create an Event Hub within an Event Hubs namespace.</span></span> <span data-ttu-id="64f32-152">U ook configureren de Event Hub voor het vastleggen van gegevens naar een Azure Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="64f32-152">You also configure the Event Hub to capture data to an Azure Data Lake Store account.</span></span> <span data-ttu-id="64f32-153">Deze sectie wordt ervan uitgegaan dat u al een naamruimte Event Hubs hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="64f32-153">This section assumes that you have already created an Event Hubs namespace.</span></span>

2. <span data-ttu-id="64f32-154">Van de **overzicht** deelvenster van de naamruimte van Event Hubs, klikt u op **+ Event Hub**.</span><span class="sxs-lookup"><span data-stu-id="64f32-154">From the **Overview** pane of the Event Hubs namespace, click **+ Event Hub**.</span></span>

    <span data-ttu-id="64f32-155">![Event Hub maken](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "Event Hub maken")</span><span class="sxs-lookup"><span data-stu-id="64f32-155">![Create Event Hub](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "Create Event Hub")</span></span>

3. <span data-ttu-id="64f32-156">Geef de volgende waarden voor het configureren van Event Hubs voor het vastleggen van gegevens naar Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="64f32-156">Provide the following values to configure Event Hubs to capture data to Data Lake Store.</span></span>

    <span data-ttu-id="64f32-157">![Event Hub maken](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "Event Hub maken")</span><span class="sxs-lookup"><span data-stu-id="64f32-157">![Create Event Hub](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "Create Event Hub")</span></span>

    <span data-ttu-id="64f32-158">a.</span><span class="sxs-lookup"><span data-stu-id="64f32-158">a.</span></span> <span data-ttu-id="64f32-159">Geef een naam voor de Event Hub.</span><span class="sxs-lookup"><span data-stu-id="64f32-159">Provide a name for the Event Hub.</span></span>
    
    <span data-ttu-id="64f32-160">b.</span><span class="sxs-lookup"><span data-stu-id="64f32-160">b.</span></span> <span data-ttu-id="64f32-161">Voor deze zelfstudie stelt **aantal partities** en **bericht bewaren** op de standaardwaarden.</span><span class="sxs-lookup"><span data-stu-id="64f32-161">For this tutorial, set **Partition Count** and **Message Retention** to the default values.</span></span>
    
    <span data-ttu-id="64f32-162">c.</span><span class="sxs-lookup"><span data-stu-id="64f32-162">c.</span></span> <span data-ttu-id="64f32-163">Stel **vastleggen** naar **op**.</span><span class="sxs-lookup"><span data-stu-id="64f32-163">Set **Capture** to **On**.</span></span> <span data-ttu-id="64f32-164">Stel de **tijdvenster** (hoe vaak om vast te leggen) en **grootte venster** (gegevensgrootte voor het vastleggen van).</span><span class="sxs-lookup"><span data-stu-id="64f32-164">Set the **Time Window** (how frequently to capture) and **Size Window** (data size to capture).</span></span> 
    
    <span data-ttu-id="64f32-165">d.</span><span class="sxs-lookup"><span data-stu-id="64f32-165">d.</span></span> <span data-ttu-id="64f32-166">Voor **vastleggen Provider**, selecteer **Azure Data Lake Store** en het selecteren van de Data Lake Store u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="64f32-166">For **Capture Provider**, select **Azure Data Lake Store** and the select the Data Lake Store you created earlier.</span></span> <span data-ttu-id="64f32-167">Voor **pad naar de Data Lake**, voer de naam van de map die u hebt gemaakt in de Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="64f32-167">For **Data Lake Path**, enter the name of the folder you created in the Data Lake Store account.</span></span> <span data-ttu-id="64f32-168">U hoeft alleen te bieden het relatieve pad naar de map.</span><span class="sxs-lookup"><span data-stu-id="64f32-168">You only need to provide the relative path to the folder.</span></span>

    <span data-ttu-id="64f32-169">e.</span><span class="sxs-lookup"><span data-stu-id="64f32-169">e.</span></span> <span data-ttu-id="64f32-170">Laat de **voorbeeld vastleggen bestandsindelingen naam** op de standaardwaarde.</span><span class="sxs-lookup"><span data-stu-id="64f32-170">Leave the **Sample capture file name formats** to the default value.</span></span> <span data-ttu-id="64f32-171">Deze optie bepaalt de mapstructuur die wordt gemaakt onder de map vastleggen.</span><span class="sxs-lookup"><span data-stu-id="64f32-171">This option governs the folder structure that is created under the capture folder.</span></span>

    <span data-ttu-id="64f32-172">f.</span><span class="sxs-lookup"><span data-stu-id="64f32-172">f.</span></span> <span data-ttu-id="64f32-173">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="64f32-173">Click **Create**.</span></span>

## <a name="test-the-setup"></a><span data-ttu-id="64f32-174">De instellingen testen</span><span class="sxs-lookup"><span data-stu-id="64f32-174">Test the setup</span></span>

<span data-ttu-id="64f32-175">U kunt nu de oplossing testen door gegevens te verzenden naar de Azure Event Hub.</span><span class="sxs-lookup"><span data-stu-id="64f32-175">You can now test the solution by sending data to the Azure Event Hub.</span></span> <span data-ttu-id="64f32-176">Volg de instructies voor [gebeurtenissen verzenden naar Azure Event Hubs](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md).</span><span class="sxs-lookup"><span data-stu-id="64f32-176">Follow the instructions at [Send events to Azure Event Hubs](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md).</span></span> <span data-ttu-id="64f32-177">Wanneer u begint met het verzenden van de gegevens, ziet u de gegevens in Data Lake Store worden weergegeven met de mapstructuur die u hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="64f32-177">Once you start sending the data, you see the data reflected in Data Lake Store using the folder structure you specified.</span></span> <span data-ttu-id="64f32-178">Bijvoorbeeld, ziet u een mapstructuur, zoals wordt weergegeven in de volgende schermafbeelding, in uw Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="64f32-178">For example, you see a folder structure, as shown in the following screenshot, in your Data Lake Store.</span></span>

<span data-ttu-id="64f32-179">![Voorbeeld van EventHub-gegevens in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "Sample EventHub-gegevens in Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="64f32-179">![Sample EventHub data in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "Sample EventHub data in Data Lake Store")</span></span>

> [!NOTE]
> <span data-ttu-id="64f32-180">Zelfs als er geen inkomende berichten bij Event Hubs, schrijft Event Hubs leeg bestanden met alleen de kopteksten in de Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="64f32-180">Even if you do not have messages coming into Event Hubs, Event Hubs writes empty files with just the headers into the Data Lake Store account.</span></span> <span data-ttu-id="64f32-181">De bestanden zijn geschreven met de dezelfde tijdsinterval die u hebt opgegeven tijdens het maken van de Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="64f32-181">The files are written at the same time interval that you provided while creating the Event Hubs.</span></span>
> 
>

## <a name="analyze-data-in-data-lake-store"></a><span data-ttu-id="64f32-182">Gegevens analyseren in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="64f32-182">Analyze data in Data Lake Store</span></span>

<span data-ttu-id="64f32-183">Nadat de gegevens Data Lake Store is, kunt u analytische taken uitvoeren om te verwerken en crisis de gegevens.</span><span class="sxs-lookup"><span data-stu-id="64f32-183">Once the data is in Data Lake Store, you can run analytical jobs to process and crunch the data.</span></span> <span data-ttu-id="64f32-184">Zie [USQL Avro voorbeeld](https://github.com/Azure/usql/tree/master/Examples/AvroExamples) op hoe u kunt dit doen met Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="64f32-184">See [USQL Avro Example](https://github.com/Azure/usql/tree/master/Examples/AvroExamples) on how to do this using Azure Data Lake Analytics.</span></span>
  

## <a name="see-also"></a><span data-ttu-id="64f32-185">Zie ook</span><span class="sxs-lookup"><span data-stu-id="64f32-185">See also</span></span>
* [<span data-ttu-id="64f32-186">Gegevens in Data Lake Store beveiligen</span><span class="sxs-lookup"><span data-stu-id="64f32-186">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="64f32-187">Gegevens kopiëren van Azure Storage-Blobs naar Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="64f32-187">Copy data from Azure Storage Blobs to Data Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
