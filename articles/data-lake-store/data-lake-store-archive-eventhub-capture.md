---
title: aaaCapture gegevens uit Event Hubs in Azure Data Lake Store | Microsoft Docs
description: Gebruik Azure Data Lake Store toocapture gegevens uit Event Hubs
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
ms.openlocfilehash: 09b17bd0b47043bd2c83dba72c01a8064f206a0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-lake-store-toocapture-data-from-event-hubs"></a><span data-ttu-id="86724-103">Gebruik Azure Data Lake Store toocapture gegevens uit Event Hubs</span><span class="sxs-lookup"><span data-stu-id="86724-103">Use Azure Data Lake Store toocapture data from Event Hubs</span></span>

<span data-ttu-id="86724-104">Meer informatie over hoe toouse Azure Data Lake Store toocapture gegevens worden ontvangen door Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="86724-104">Learn how toouse Azure Data Lake Store toocapture data received by Azure Event Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="86724-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="86724-105">Prerequisites</span></span>

* <span data-ttu-id="86724-106">**Een Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="86724-106">**An Azure subscription**.</span></span> <span data-ttu-id="86724-107">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="86724-107">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="86724-108">**Een Azure Data Lake Store-account**.</span><span class="sxs-lookup"><span data-stu-id="86724-108">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="86724-109">Voor instructies over het toocreate één, Zie [aan de slag met Azure Data Lake Store](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="86724-109">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md).</span></span>

*  <span data-ttu-id="86724-110">**Een naamruimte Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="86724-110">**An Event Hubs namespace**.</span></span> <span data-ttu-id="86724-111">Zie voor instructies [maken van een naamruimte Event Hubs](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace).</span><span class="sxs-lookup"><span data-stu-id="86724-111">For instructions, see [Create an Event Hubs namespace](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace).</span></span> <span data-ttu-id="86724-112">Controleer of Hallo Data Lake Store-account en Hallo Event Hubs naamruimte in Hallo hetzelfde Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="86724-112">Make sure hello Data Lake Store account and hello Event Hubs namespace are in hello same Azure subscription.</span></span>


## <a name="assign-permissions-tooevent-hubs"></a><span data-ttu-id="86724-113">Machtigingen toewijzen aan tooEvent Hubs</span><span class="sxs-lookup"><span data-stu-id="86724-113">Assign permissions tooEvent Hubs</span></span>

<span data-ttu-id="86724-114">In deze sectie maakt maken u een map binnen Hallo account waar u toocapture Hallo gegevens uit Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="86724-114">In this section, you create a folder within hello account where you want toocapture hello data from Event Hubs.</span></span> <span data-ttu-id="86724-115">U ook toewijzen machtigingen tooEvent Hubs zodat van gegevens naar een Data Lake Store-account schrijven.</span><span class="sxs-lookup"><span data-stu-id="86724-115">You also assign permissions tooEvent Hubs so that it can write data into a Data Lake Store account.</span></span> 

1. <span data-ttu-id="86724-116">Open Hallo Data Lake Store-account waarin u wilt dat toocapture gegevens uit Event Hubs en klik vervolgens op **Data Explorer**.</span><span class="sxs-lookup"><span data-stu-id="86724-116">Open hello Data Lake Store account where you want toocapture data from Event Hubs and then click on **Data Explorer**.</span></span>

    <span data-ttu-id="86724-117">![Data Lake Store Gegevensverkenner](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Gegevensverkenner Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="86724-117">![Data Lake Store data explorer](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Data Lake Store data explorer")</span></span>

2.  <span data-ttu-id="86724-118">Klik op **nieuwe map** en voer een naam voor de map waar u toocapture Hallo gegevens.</span><span class="sxs-lookup"><span data-stu-id="86724-118">Click **New Folder** and then enter a name for folder where you want toocapture hello data.</span></span>

    <span data-ttu-id="86724-119">![Een nieuwe map maken in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "een nieuwe map maken in Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="86724-119">![Create a new folder in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "Create a new folder in Data Lake Store")</span></span>

3. <span data-ttu-id="86724-120">Wijs machtigingen in de hoofdmap van het Hallo Hallo Data Lake Store toe.</span><span class="sxs-lookup"><span data-stu-id="86724-120">Assign permissions at hello root of hello Data Lake Store.</span></span> 

    <span data-ttu-id="86724-121">a.</span><span class="sxs-lookup"><span data-stu-id="86724-121">a.</span></span> <span data-ttu-id="86724-122">Klik op **Data Explorer**Hallo hoofdmap Hallo Data Lake Store-account selecteren en klik vervolgens op **toegang**.</span><span class="sxs-lookup"><span data-stu-id="86724-122">Click **Data Explorer**, select hello root of hello Data Lake Store account, and then click **Access**.</span></span>

    <span data-ttu-id="86724-123">![Machtigingen voor Data Lake Store-basis toe te wijzen](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "toegangsrechten voor de hoofdmap van de Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="86724-123">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "Assign permissions for Data Lake Store root")</span></span>

    <span data-ttu-id="86724-124">b.</span><span class="sxs-lookup"><span data-stu-id="86724-124">b.</span></span> <span data-ttu-id="86724-125">Onder **toegang**, klikt u op **toevoegen**, klikt u op **gebruiker of groep selecteren**, en zoek vervolgens naar `Microsoft.EventHubs`.</span><span class="sxs-lookup"><span data-stu-id="86724-125">Under **Access**, click **Add**, click **Select User or Group**, and then search for `Microsoft.EventHubs`.</span></span> 

    <span data-ttu-id="86724-126">![Machtigingen voor Data Lake Store-basis toe te wijzen](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "toegangsrechten voor de hoofdmap van de Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="86724-126">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assign permissions for Data Lake Store root")</span></span>
    
    <span data-ttu-id="86724-127">Klik op **Selecteren**.</span><span class="sxs-lookup"><span data-stu-id="86724-127">Click **Select**.</span></span>

    <span data-ttu-id="86724-128">c.</span><span class="sxs-lookup"><span data-stu-id="86724-128">c.</span></span> <span data-ttu-id="86724-129">Onder **machtigingen toewijzen**, klikt u op **Selecteer machtigingen**.</span><span class="sxs-lookup"><span data-stu-id="86724-129">Under **Assign Permissions**, click **Select Permissions**.</span></span> <span data-ttu-id="86724-130">Stel **machtigingen** te**Execute**.</span><span class="sxs-lookup"><span data-stu-id="86724-130">Set **Permissions** too**Execute**.</span></span> <span data-ttu-id="86724-131">Stel **toevoegen aan** te**deze map en alle onderliggende**.</span><span class="sxs-lookup"><span data-stu-id="86724-131">Set **Add to** too**This folder and all children**.</span></span> <span data-ttu-id="86724-132">Stel **toevoegen als** te**een machtigingsvermelding toegang en een standaard machtigingsvermelding**.</span><span class="sxs-lookup"><span data-stu-id="86724-132">Set **Add as** too**An access permission entry and a default permission entry**.</span></span>

    <span data-ttu-id="86724-133">![Machtigingen voor Data Lake Store-basis toe te wijzen](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "toegangsrechten voor de hoofdmap van de Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="86724-133">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "Assign permissions for Data Lake Store root")</span></span>

    <span data-ttu-id="86724-134">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="86724-134">Click **OK**.</span></span>

4. <span data-ttu-id="86724-135">Machtigingen voor map van de Hallo onder Data Lake Store-account waarin u toocapture gegevens wilt toewijzen.</span><span class="sxs-lookup"><span data-stu-id="86724-135">Assign permissions for hello folder under Data Lake Store account where you want toocapture data.</span></span>

    <span data-ttu-id="86724-136">a.</span><span class="sxs-lookup"><span data-stu-id="86724-136">a.</span></span> <span data-ttu-id="86724-137">Klik op **Data Explorer**, selecteert u Hallo-map in Hallo Data Lake Store-account en klik op **toegang**.</span><span class="sxs-lookup"><span data-stu-id="86724-137">Click **Data Explorer**, select hello folder in hello Data Lake Store account, and then click **Access**.</span></span>

    <span data-ttu-id="86724-138">![Wijs machtigingen voor Data Lake Store-map](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "machtigingen voor Data Lake Store-map toewijzen")</span><span class="sxs-lookup"><span data-stu-id="86724-138">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "Assign permissions for Data Lake Store folder")</span></span>

    <span data-ttu-id="86724-139">b.</span><span class="sxs-lookup"><span data-stu-id="86724-139">b.</span></span> <span data-ttu-id="86724-140">Onder **toegang**, klikt u op **toevoegen**, klikt u op **gebruiker of groep selecteren**, en zoek vervolgens naar `Microsoft.EventHubs`.</span><span class="sxs-lookup"><span data-stu-id="86724-140">Under **Access**, click **Add**, click **Select User or Group**, and then search for `Microsoft.EventHubs`.</span></span> 

    <span data-ttu-id="86724-141">![Wijs machtigingen voor Data Lake Store-map](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "machtigingen voor Data Lake Store-map toewijzen")</span><span class="sxs-lookup"><span data-stu-id="86724-141">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assign permissions for Data Lake Store folder")</span></span>
    
    <span data-ttu-id="86724-142">Klik op **Selecteren**.</span><span class="sxs-lookup"><span data-stu-id="86724-142">Click **Select**.</span></span>

    <span data-ttu-id="86724-143">c.</span><span class="sxs-lookup"><span data-stu-id="86724-143">c.</span></span> <span data-ttu-id="86724-144">Onder **machtigingen toewijzen**, klikt u op **Selecteer machtigingen**.</span><span class="sxs-lookup"><span data-stu-id="86724-144">Under **Assign Permissions**, click **Select Permissions**.</span></span> <span data-ttu-id="86724-145">Stel **machtigingen** te**lezen, schrijven,** en **Execute**.</span><span class="sxs-lookup"><span data-stu-id="86724-145">Set **Permissions** too**Read, Write,** and **Execute**.</span></span> <span data-ttu-id="86724-146">Stel **toevoegen aan** te**deze map en alle onderliggende**.</span><span class="sxs-lookup"><span data-stu-id="86724-146">Set **Add to** too**This folder and all children**.</span></span> <span data-ttu-id="86724-147">Tot slot stelt **toevoegen als** te**een machtigingsvermelding toegang en een standaard machtigingsvermelding**.</span><span class="sxs-lookup"><span data-stu-id="86724-147">Finally, set **Add as** too**An access permission entry and a default permission entry**.</span></span>

    <span data-ttu-id="86724-148">![Wijs machtigingen voor Data Lake Store-map](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "machtigingen voor Data Lake Store-map toewijzen")</span><span class="sxs-lookup"><span data-stu-id="86724-148">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "Assign permissions for Data Lake Store folder")</span></span>
    
    <span data-ttu-id="86724-149">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="86724-149">Click **OK**.</span></span> 

## <a name="configure-event-hubs-toocapture-data-toodata-lake-store"></a><span data-ttu-id="86724-150">Event Hubs toocapture tooData Lake gegevensarchief configureren</span><span class="sxs-lookup"><span data-stu-id="86724-150">Configure Event Hubs toocapture data tooData Lake Store</span></span>

<span data-ttu-id="86724-151">In deze sectie maakt u een Event Hub in een Event Hubs-naamruimte.</span><span class="sxs-lookup"><span data-stu-id="86724-151">In this section, you create an Event Hub within an Event Hubs namespace.</span></span> <span data-ttu-id="86724-152">U ook configureren Hallo Event Hub toocapture gegevens tooan Azure Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="86724-152">You also configure hello Event Hub toocapture data tooan Azure Data Lake Store account.</span></span> <span data-ttu-id="86724-153">Deze sectie wordt ervan uitgegaan dat u al een naamruimte Event Hubs hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="86724-153">This section assumes that you have already created an Event Hubs namespace.</span></span>

2. <span data-ttu-id="86724-154">Van Hallo **overzicht** deelvenster van de naamruimte van de Event Hubs hello, klikt u op **+ Event Hub**.</span><span class="sxs-lookup"><span data-stu-id="86724-154">From hello **Overview** pane of hello Event Hubs namespace, click **+ Event Hub**.</span></span>

    <span data-ttu-id="86724-155">![Event Hub maken](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "Event Hub maken")</span><span class="sxs-lookup"><span data-stu-id="86724-155">![Create Event Hub](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "Create Event Hub")</span></span>

3. <span data-ttu-id="86724-156">Geef Hallo volgende waarden tooconfigure Event Hubs toocapture data tooData Lake Store.</span><span class="sxs-lookup"><span data-stu-id="86724-156">Provide hello following values tooconfigure Event Hubs toocapture data tooData Lake Store.</span></span>

    <span data-ttu-id="86724-157">![Event Hub maken](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "Event Hub maken")</span><span class="sxs-lookup"><span data-stu-id="86724-157">![Create Event Hub](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "Create Event Hub")</span></span>

    <span data-ttu-id="86724-158">a.</span><span class="sxs-lookup"><span data-stu-id="86724-158">a.</span></span> <span data-ttu-id="86724-159">Geef een naam voor Hallo Event Hub.</span><span class="sxs-lookup"><span data-stu-id="86724-159">Provide a name for hello Event Hub.</span></span>
    
    <span data-ttu-id="86724-160">b.</span><span class="sxs-lookup"><span data-stu-id="86724-160">b.</span></span> <span data-ttu-id="86724-161">Voor deze zelfstudie stelt **aantal partities** en **bericht bewaren** toohello standaardwaarden.</span><span class="sxs-lookup"><span data-stu-id="86724-161">For this tutorial, set **Partition Count** and **Message Retention** toohello default values.</span></span>
    
    <span data-ttu-id="86724-162">c.</span><span class="sxs-lookup"><span data-stu-id="86724-162">c.</span></span> <span data-ttu-id="86724-163">Stel **vastleggen** te**op**.</span><span class="sxs-lookup"><span data-stu-id="86724-163">Set **Capture** too**On**.</span></span> <span data-ttu-id="86724-164">Set Hallo **tijdvenster** (hoe vaak toocapture) en **grootte venster** (gegevens grootte toocapture).</span><span class="sxs-lookup"><span data-stu-id="86724-164">Set hello **Time Window** (how frequently toocapture) and **Size Window** (data size toocapture).</span></span> 
    
    <span data-ttu-id="86724-165">d.</span><span class="sxs-lookup"><span data-stu-id="86724-165">d.</span></span> <span data-ttu-id="86724-166">Voor **vastleggen Provider**, selecteer **Azure Data Lake Store** en hello Selecteer Hallo Data Lake Store die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="86724-166">For **Capture Provider**, select **Azure Data Lake Store** and hello select hello Data Lake Store you created earlier.</span></span> <span data-ttu-id="86724-167">Voor **pad naar de Data Lake**, Hallo-naam van het Hallo-map die u hebt gemaakt in Hallo Data Lake Store-account invoeren.</span><span class="sxs-lookup"><span data-stu-id="86724-167">For **Data Lake Path**, enter hello name of hello folder you created in hello Data Lake Store account.</span></span> <span data-ttu-id="86724-168">U hoeft alleen tooprovide Hallo relatief pad toohello map.</span><span class="sxs-lookup"><span data-stu-id="86724-168">You only need tooprovide hello relative path toohello folder.</span></span>

    <span data-ttu-id="86724-169">e.</span><span class="sxs-lookup"><span data-stu-id="86724-169">e.</span></span> <span data-ttu-id="86724-170">Hallo laat **voorbeeld vastleggen bestandsindelingen naam** toohello standaardwaarde.</span><span class="sxs-lookup"><span data-stu-id="86724-170">Leave hello **Sample capture file name formats** toohello default value.</span></span> <span data-ttu-id="86724-171">Deze optie bepaalt Hallo mapstructuur die wordt gemaakt onder Hallo vastleggen map.</span><span class="sxs-lookup"><span data-stu-id="86724-171">This option governs hello folder structure that is created under hello capture folder.</span></span>

    <span data-ttu-id="86724-172">f.</span><span class="sxs-lookup"><span data-stu-id="86724-172">f.</span></span> <span data-ttu-id="86724-173">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="86724-173">Click **Create**.</span></span>

## <a name="test-hello-setup"></a><span data-ttu-id="86724-174">Test Hallo setup</span><span class="sxs-lookup"><span data-stu-id="86724-174">Test hello setup</span></span>

<span data-ttu-id="86724-175">U kunt nu Hallo oplossing testen door te sturen gegevens toohello Azure Event Hub.</span><span class="sxs-lookup"><span data-stu-id="86724-175">You can now test hello solution by sending data toohello Azure Event Hub.</span></span> <span data-ttu-id="86724-176">Volg de instructies Hallo voor [gebeurtenissen verzenden tooAzure Event Hubs](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md).</span><span class="sxs-lookup"><span data-stu-id="86724-176">Follow hello instructions at [Send events tooAzure Event Hubs](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md).</span></span> <span data-ttu-id="86724-177">Wanneer u begint met het verzenden van gegevens hello, ziet u Hallo-gegevens in Data Lake Store worden weergegeven met behulp van Hallo-mapstructuur die u hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="86724-177">Once you start sending hello data, you see hello data reflected in Data Lake Store using hello folder structure you specified.</span></span> <span data-ttu-id="86724-178">Bijvoorbeeld, ziet u een mapstructuur, zoals wordt weergegeven in de volgende schermopname in uw Data Lake Store Hallo.</span><span class="sxs-lookup"><span data-stu-id="86724-178">For example, you see a folder structure, as shown in hello following screenshot, in your Data Lake Store.</span></span>

<span data-ttu-id="86724-179">![Voorbeeld van EventHub-gegevens in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "Sample EventHub-gegevens in Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="86724-179">![Sample EventHub data in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "Sample EventHub data in Data Lake Store")</span></span>

> [!NOTE]
> <span data-ttu-id="86724-180">Zelfs als er geen inkomende berichten bij Event Hubs, schrijft Event Hubs lege bestanden met NET Hallo kopteksten in Hallo Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="86724-180">Even if you do not have messages coming into Event Hubs, Event Hubs writes empty files with just hello headers into hello Data Lake Store account.</span></span> <span data-ttu-id="86724-181">Hallo-bestanden geschreven op Hallo dezelfde tijdsinterval die u hebt opgegeven tijdens het maken van Hallo Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="86724-181">hello files are written at hello same time interval that you provided while creating hello Event Hubs.</span></span>
> 
>

## <a name="analyze-data-in-data-lake-store"></a><span data-ttu-id="86724-182">Gegevens analyseren in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="86724-182">Analyze data in Data Lake Store</span></span>

<span data-ttu-id="86724-183">Nadat gegevens Hallo Data Lake Store is, kunt u tooprocess en crisis Hallo gegevens analytische taken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="86724-183">Once hello data is in Data Lake Store, you can run analytical jobs tooprocess and crunch hello data.</span></span> <span data-ttu-id="86724-184">Zie [USQL Avro voorbeeld](https://github.com/Azure/usql/tree/master/Examples/AvroExamples) over het toodo deze met Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="86724-184">See [USQL Avro Example](https://github.com/Azure/usql/tree/master/Examples/AvroExamples) on how toodo this using Azure Data Lake Analytics.</span></span>
  

## <a name="see-also"></a><span data-ttu-id="86724-185">Zie ook</span><span class="sxs-lookup"><span data-stu-id="86724-185">See also</span></span>
* [<span data-ttu-id="86724-186">Gegevens in Data Lake Store beveiligen</span><span class="sxs-lookup"><span data-stu-id="86724-186">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="86724-187">Gegevens kopiëren van Azure Storage Blobs tooData Lake Store</span><span class="sxs-lookup"><span data-stu-id="86724-187">Copy data from Azure Storage Blobs tooData Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
