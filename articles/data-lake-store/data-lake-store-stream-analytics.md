---
title: Gegevens van de Stream Analytics stream in Data Lake Store | Microsoft Docs
description: Azure Stream Analytics gebruikt om gegevens van de stream naar het Azure Data Lake Store
services: data-lake-store,stream-analytics
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: edb58e0b-311f-44b0-a499-04d7e6c07a90
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 90104aaacf24a5a7156900fc3848a27f60329814
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="stream-data-from-azure-storage-blob-into-data-lake-store-using-azure-stream-analytics"></a><span data-ttu-id="64e36-103">Gegevens streamen van Azure Storage Blob naar Data Lake Store met behulp van Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="64e36-103">Stream data from Azure Storage Blob into Data Lake Store using Azure Stream Analytics</span></span>
<span data-ttu-id="64e36-104">In dit artikel leert u hoe u Azure Data Lake Store als uitvoer voor een Azure Stream Analytics-taak.</span><span class="sxs-lookup"><span data-stu-id="64e36-104">In this article you will learn how to use Azure Data Lake Store as an output for an Azure Stream Analytics job.</span></span> <span data-ttu-id="64e36-105">In dit artikel wordt een eenvoudig scenario voor die gegevens van een Azure Storage-blob (invoer) leest en schrijft de gegevens naar Data Lake Store (uitvoer).</span><span class="sxs-lookup"><span data-stu-id="64e36-105">This article demonstrates a simple scenario that reads data from an Azure Storage blob (input) and writes the data to Data Lake Store (output).</span></span>

> [!NOTE]
> <span data-ttu-id="64e36-106">Op dit moment kunt maken en de configuratie van Data Lake Store voert voor Stream Analytics wordt alleen ondersteund in de [klassieke Azure-Portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="64e36-106">At this time, creation and configuration of Data Lake Store outputs for Stream Analytics is supported only in the [Azure Classic Portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="64e36-107">Sommige onderdelen van deze zelfstudie wordt daarom de klassieke Azure Portal gebruiken.</span><span class="sxs-lookup"><span data-stu-id="64e36-107">Hence, some parts of this tutorial will use the Azure Classic Portal.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="64e36-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="64e36-108">Prerequisites</span></span>
<span data-ttu-id="64e36-109">Voordat u met deze zelfstudie begint, moet u het volgende hebben of hebben gedaan:</span><span class="sxs-lookup"><span data-stu-id="64e36-109">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="64e36-110">**Een Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="64e36-110">**An Azure subscription**.</span></span> <span data-ttu-id="64e36-111">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="64e36-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="64e36-112">**Azure Storage-account**.</span><span class="sxs-lookup"><span data-stu-id="64e36-112">**Azure Storage account**.</span></span> <span data-ttu-id="64e36-113">U gebruikt een blob-container van dit account voor het invoeren van gegevens voor een Stream Analytics-taak.</span><span class="sxs-lookup"><span data-stu-id="64e36-113">You will use a blob container from this account to input data for a Stream Analytics job.</span></span> <span data-ttu-id="64e36-114">Voor deze zelfstudie wordt ervan uitgegaan er een opslagaccount die is aangeroepen **storageforasa** en een container binnen het account met de naam **storageforasacontainer**.</span><span class="sxs-lookup"><span data-stu-id="64e36-114">For this tutorial, assume you have a storage account called **storageforasa** and a container within the account called **storageforasacontainer**.</span></span> <span data-ttu-id="64e36-115">Nadat u de container hebt gemaakt, moet u een Voorbeeldgegevensbestand uploaden naar het.</span><span class="sxs-lookup"><span data-stu-id="64e36-115">Once you have created the container, upload a sample data file to it.</span></span> 
  
* <span data-ttu-id="64e36-116">**Azure Data Lake Store-account**.</span><span class="sxs-lookup"><span data-stu-id="64e36-116">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="64e36-117">Volg de instructies in [Aan de slag met Azure Data Lake Store met Azure Portal](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="64e36-117">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](data-lake-store-get-started-portal.md).</span></span> <span data-ttu-id="64e36-118">Stel u hebt een Data Lake Store-account genoemd **asadatalakestore**.</span><span class="sxs-lookup"><span data-stu-id="64e36-118">Let's assume you have a Data Lake Store account called **asadatalakestore**.</span></span> 

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="64e36-119">Een Stream Analytics-taak maken</span><span class="sxs-lookup"><span data-stu-id="64e36-119">Create a Stream Analytics Job</span></span>
<span data-ttu-id="64e36-120">U begint met het maken van een Stream Analytics-taak die bestaat uit een invoerbron en een bestemming voor de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="64e36-120">You start by creating a Stream Analytics job that includes an input source and an output destination.</span></span> <span data-ttu-id="64e36-121">Voor deze zelfstudie, de bron is een Azure blob-container en de bestemming is Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="64e36-121">For this tutorial, the source is an Azure blob container and the destination is Data Lake Store.</span></span>

1. <span data-ttu-id="64e36-122">Meld u aan bij de [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="64e36-122">Sign on to the [Azure Portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="64e36-123">Klik in het linkerdeelvenster op **Stream Analytics-taken**, en klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="64e36-123">From the left pane, click **Stream Analytics jobs**, and then click **Add**.</span></span>

    <span data-ttu-id="64e36-124">![Maken van een Stream Analytics-taak](./media/data-lake-store-stream-analytics/create.job.png "een Stream Analytics-taak maken")</span><span class="sxs-lookup"><span data-stu-id="64e36-124">![Create a Stream Analytics Job](./media/data-lake-store-stream-analytics/create.job.png "Create a Stream Analytics job")</span></span>

    > [!NOTE]
    > <span data-ttu-id="64e36-125">Zorg ervoor dat u taak maken in dezelfde regio als het opslagaccount of u extra kosten van het verplaatsen van gegevens tussen regio's, worden.</span><span class="sxs-lookup"><span data-stu-id="64e36-125">Make sure you create job in the same region as the storage account or you will incur additional cost of moving data between regions.</span></span>
    >

## <a name="create-a-blob-input-for-the-job"></a><span data-ttu-id="64e36-126">Een Blob-invoer voor de taak maken</span><span class="sxs-lookup"><span data-stu-id="64e36-126">Create a Blob input for the job</span></span>

1. <span data-ttu-id="64e36-127">Open de pagina voor de Stream Analytics-taak in het linkerdeelvenster klikt u op de **invoer** tabblad en klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="64e36-127">Open the page for the Stream Analytics job, from the left pane click the **Inputs** tab, and then click **Add**.</span></span>

    <span data-ttu-id="64e36-128">![Een invoer toevoegen aan uw taak](./media/data-lake-store-stream-analytics/create.input.1.png "invoer aan uw project toevoegen")</span><span class="sxs-lookup"><span data-stu-id="64e36-128">![Add an input to your job](./media/data-lake-store-stream-analytics/create.input.1.png "Add an input to your job")</span></span>

2. <span data-ttu-id="64e36-129">Op de **nieuwe invoer** blade bieden de volgende waarden.</span><span class="sxs-lookup"><span data-stu-id="64e36-129">On the **New input** blade, provide the following values.</span></span>

    <span data-ttu-id="64e36-130">![Een invoer toevoegen aan uw taak](./media/data-lake-store-stream-analytics/create.input.2.png "invoer aan uw project toevoegen")</span><span class="sxs-lookup"><span data-stu-id="64e36-130">![Add an input to your job](./media/data-lake-store-stream-analytics/create.input.2.png "Add an input to your job")</span></span>

    * <span data-ttu-id="64e36-131">Voor **invoer alias**, voer een unieke naam voor de taak invoeren.</span><span class="sxs-lookup"><span data-stu-id="64e36-131">For **Input alias**, enter a unique name for the job input.</span></span>
    * <span data-ttu-id="64e36-132">Voor **gegevensbrontype**, selecteer **gegevensstroom**.</span><span class="sxs-lookup"><span data-stu-id="64e36-132">For **Source type**, select **Data stream**.</span></span>
    * <span data-ttu-id="64e36-133">Voor **bron**, selecteer **Blob storage**.</span><span class="sxs-lookup"><span data-stu-id="64e36-133">For **Source**, select **Blob storage**.</span></span>
    * <span data-ttu-id="64e36-134">Voor **abonnement**, selecteer **gebruik blob storage uit het huidige abonnement**.</span><span class="sxs-lookup"><span data-stu-id="64e36-134">For **Subscription**, select **Use blob storage from current subscription**.</span></span>
    * <span data-ttu-id="64e36-135">Voor **opslagaccount**, selecteer het opslagaccount dat u hebt gemaakt als onderdeel van de vereisten.</span><span class="sxs-lookup"><span data-stu-id="64e36-135">For **Storage account**, select the storage account that you created as part of the prerequisites.</span></span> 
    * <span data-ttu-id="64e36-136">Voor **Container**, selecteert u de container die u hebt gemaakt in het geselecteerde opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="64e36-136">For **Container**, select the container that you created in the selected storage account.</span></span>
    * <span data-ttu-id="64e36-137">Voor **gebeurtenis serialisatie-indeling**, selecteer **CSV**.</span><span class="sxs-lookup"><span data-stu-id="64e36-137">For **Event serialization format**, select **CSV**.</span></span>
    * <span data-ttu-id="64e36-138">Voor **scheidingsteken**, selecteer **tabblad**.</span><span class="sxs-lookup"><span data-stu-id="64e36-138">For **Delimiter**, select **tab**.</span></span>
    * <span data-ttu-id="64e36-139">Voor **codering**, selecteer **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="64e36-139">For **Encoding**, select **UTF-8**.</span></span>

    <span data-ttu-id="64e36-140">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="64e36-140">Click **Create**.</span></span> <span data-ttu-id="64e36-141">De portal wordt nu voegt de invoer en test de verbinding met het.</span><span class="sxs-lookup"><span data-stu-id="64e36-141">The portal now adds the input and tests the connection to it.</span></span>


## <a name="create-a-data-lake-store-output-for-the-job"></a><span data-ttu-id="64e36-142">Een Data Lake Store-uitvoer voor de taak maken</span><span class="sxs-lookup"><span data-stu-id="64e36-142">Create a Data Lake Store output for the job</span></span>

1. <span data-ttu-id="64e36-143">Open de pagina voor de Stream Analytics-taak, klikt u op de **uitvoer** tabblad en klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="64e36-143">Open the page for the Stream Analytics job, click the **Outputs** tab, and then click **Add**.</span></span>

    <span data-ttu-id="64e36-144">![Uitvoer toevoegen aan uw job](./media/data-lake-store-stream-analytics/create.output.1.png "uitvoer toevoegen aan uw project")</span><span class="sxs-lookup"><span data-stu-id="64e36-144">![Add an output to your job](./media/data-lake-store-stream-analytics/create.output.1.png "Add an output to your job")</span></span>

2. <span data-ttu-id="64e36-145">Op de **nieuwe uitvoer** blade bieden de volgende waarden.</span><span class="sxs-lookup"><span data-stu-id="64e36-145">On the **New output** blade, provide the following values.</span></span>

    <span data-ttu-id="64e36-146">![Uitvoer toevoegen aan uw job](./media/data-lake-store-stream-analytics/create.output.2.png "uitvoer toevoegen aan uw project")</span><span class="sxs-lookup"><span data-stu-id="64e36-146">![Add an output to your job](./media/data-lake-store-stream-analytics/create.output.2.png "Add an output to your job")</span></span>

    * <span data-ttu-id="64e36-147">Voor **uitvoeraliassen**, voer een unieke naam op voor de taakuitvoer.</span><span class="sxs-lookup"><span data-stu-id="64e36-147">For **Output alias**, enter a a unique name for the job output.</span></span> <span data-ttu-id="64e36-148">Dit is een beschrijvende naam die is gebruikt in query's om de queryuitvoer naar Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="64e36-148">This is a friendly name used in queries to direct the query output to this Data Lake Store.</span></span>
    * <span data-ttu-id="64e36-149">Voor **Sink**, selecteer **Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="64e36-149">For **Sink**, select **Data Lake Store**.</span></span>
    * <span data-ttu-id="64e36-150">U wordt gevraagd toegang verlenen aan Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="64e36-150">You will be prompted to authorize access to Data Lake Store account.</span></span> <span data-ttu-id="64e36-151">Klik op **autoriseren**.</span><span class="sxs-lookup"><span data-stu-id="64e36-151">Click **Authorize**.</span></span>

3. <span data-ttu-id="64e36-152">Op de **nieuwe uitvoer** blade doorgaan met de volgende waarden op te geven.</span><span class="sxs-lookup"><span data-stu-id="64e36-152">On the **New output** blade, continue to provide the following values.</span></span>

    <span data-ttu-id="64e36-153">![Uitvoer toevoegen aan uw job](./media/data-lake-store-stream-analytics/create.output.3.png "uitvoer toevoegen aan uw project")</span><span class="sxs-lookup"><span data-stu-id="64e36-153">![Add an output to your job](./media/data-lake-store-stream-analytics/create.output.3.png "Add an output to your job")</span></span>

    * <span data-ttu-id="64e36-154">Voor **accountnaam**, selecteert u de Data Lake Store-account dat u al waar u de taak wordt verzonden gemaakt naar de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="64e36-154">For **Account name**, select the Data Lake Store account you already created where you want the job output to be sent to.</span></span>
    * <span data-ttu-id="64e36-155">Voor **pad voorvoegselpatroon**, voer een pad dat wordt gebruikt om uw bestanden binnen de opgegeven Data Lake Store-account te schrijven.</span><span class="sxs-lookup"><span data-stu-id="64e36-155">For **Path prefix pattern**, enter a file path used to write your files within the specified Data Lake Store account.</span></span>
    * <span data-ttu-id="64e36-156">Voor **datumnotatie**, als u een datum-token in het pad van het voorvoegsel gebruikt, kunt u de datumnotatie waarin de bestanden zijn ingedeeld.</span><span class="sxs-lookup"><span data-stu-id="64e36-156">For **Date format**, if you used a date token in the prefix path, you can select the date format in which your files are organized.</span></span>
    * <span data-ttu-id="64e36-157">Voor **tijdnotatie**, als u een token tijd in het pad naar het voorvoegsel van gebruikt de tijdindeling op waarin de bestanden zijn ingedeeld opgeven.</span><span class="sxs-lookup"><span data-stu-id="64e36-157">For **Time format**, if you used a time token in the prefix path, specify the time format in which your files are organized.</span></span>
    * <span data-ttu-id="64e36-158">Voor **gebeurtenis serialisatie-indeling**, selecteer **CSV**.</span><span class="sxs-lookup"><span data-stu-id="64e36-158">For **Event serialization format**, select **CSV**.</span></span>
    * <span data-ttu-id="64e36-159">Voor **scheidingsteken**, selecteer **tabblad**.</span><span class="sxs-lookup"><span data-stu-id="64e36-159">For **Delimiter**, select **tab**.</span></span>
    * <span data-ttu-id="64e36-160">Voor **codering**, selecteer **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="64e36-160">For **Encoding**, select **UTF-8**.</span></span>
    
    <span data-ttu-id="64e36-161">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="64e36-161">Click **Create**.</span></span> <span data-ttu-id="64e36-162">De portal wordt nu voegt de uitvoer en test de verbinding met het.</span><span class="sxs-lookup"><span data-stu-id="64e36-162">The portal now adds the output and tests the connection to it.</span></span>
    
## <a name="run-the-stream-analytics-job"></a><span data-ttu-id="64e36-163">De Stream Analytics-taak uitvoeren</span><span class="sxs-lookup"><span data-stu-id="64e36-163">Run the Stream Analytics job</span></span>

1. <span data-ttu-id="64e36-164">U moet een query uit een Stream Analytics-taak uit te voeren de **Query** tabblad.</span><span class="sxs-lookup"><span data-stu-id="64e36-164">To run a Stream Analytics job, you must run a query from the **Query** tab.</span></span> <span data-ttu-id="64e36-165">Voor deze zelfstudie kunt u de voorbeeldquery uitvoeren door te vervangen de tijdelijke aanduidingen door de taak invoer en uitvoer aliassen, zoals wordt weergegeven in onderstaande schermafbeelding.</span><span class="sxs-lookup"><span data-stu-id="64e36-165">For this tutorial, you can run the sample query by replacing the placeholders with the job input and output aliases, as shown in the screen capture below.</span></span>

    <span data-ttu-id="64e36-166">![Voer query](./media/data-lake-store-stream-analytics/run.query.png "query uitvoeren")</span><span class="sxs-lookup"><span data-stu-id="64e36-166">![Run query](./media/data-lake-store-stream-analytics/run.query.png "Run query")</span></span>

2. <span data-ttu-id="64e36-167">Klik op **opslaan** vanaf de bovenkant van het scherm en klik vervolgens vanaf de **overzicht** tabblad **Start**.</span><span class="sxs-lookup"><span data-stu-id="64e36-167">Click **Save** from the top of the screen, and then from the **Overview** tab, click **Start**.</span></span> <span data-ttu-id="64e36-168">Selecteer in het dialoogvenster **aangepaste tijd**, en stel vervolgens de huidige datum en tijd.</span><span class="sxs-lookup"><span data-stu-id="64e36-168">From the dialog box, select **Custom Time**, and then set the current date and time.</span></span>

    <span data-ttu-id="64e36-169">![Taaktijd instellen](./media/data-lake-store-stream-analytics/run.query.2.png "taaktijd instellen")</span><span class="sxs-lookup"><span data-stu-id="64e36-169">![Set job time](./media/data-lake-store-stream-analytics/run.query.2.png "Set job time")</span></span>

    <span data-ttu-id="64e36-170">Klik op **Start** om de taak te starten.</span><span class="sxs-lookup"><span data-stu-id="64e36-170">Click **Start** to start the job.</span></span> <span data-ttu-id="64e36-171">Het kan enkele minuten duren start de taak.</span><span class="sxs-lookup"><span data-stu-id="64e36-171">It can take up to a couple minutes to start the job.</span></span>

3. <span data-ttu-id="64e36-172">Kopieer een voorbeeldbestand van gegevens naar de blob-container zodat de taak voor het kiezen van de gegevens van de blob.</span><span class="sxs-lookup"><span data-stu-id="64e36-172">To trigger the job to pick the data from the blob, copy a sample data file to the blob container.</span></span> <span data-ttu-id="64e36-173">U krijgt een voorbeeldgegevensbestand van de [Azure Data Lake Git-opslagplaats](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).</span><span class="sxs-lookup"><span data-stu-id="64e36-173">You can get a sample data file from the [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).</span></span> <span data-ttu-id="64e36-174">Kopieer het bestand voor deze zelfstudie **vehicle1_09142014.csv**.</span><span class="sxs-lookup"><span data-stu-id="64e36-174">For this tutorial, let's copy the file **vehicle1_09142014.csv**.</span></span> <span data-ttu-id="64e36-175">U kunt verschillende clients, zoals [Azure Opslagverkenner](http://storageexplorer.com/), gegevens te uploaden naar een blob-container.</span><span class="sxs-lookup"><span data-stu-id="64e36-175">You can use various clients, such as [Azure Storage Explorer](http://storageexplorer.com/), to upload data to a blob container.</span></span>

4. <span data-ttu-id="64e36-176">Van de **overzicht** tabblad onder **bewaking**, Zie hoe de gegevens is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="64e36-176">From the **Overview** tab, under **Monitoring**, see how the data was processed.</span></span>

    <span data-ttu-id="64e36-177">![Monitor taak](./media/data-lake-store-stream-analytics/run.query.3.png "Monitor taak")</span><span class="sxs-lookup"><span data-stu-id="64e36-177">![Monitor job](./media/data-lake-store-stream-analytics/run.query.3.png "Monitor job")</span></span>

5. <span data-ttu-id="64e36-178">Ten slotte kunt u controleren dat de uitvoergegevens van de taak beschikbaar in de Data Lake Store-account is.</span><span class="sxs-lookup"><span data-stu-id="64e36-178">Finally, you can verify that the job output data is available in the Data Lake Store account.</span></span> 

    <span data-ttu-id="64e36-179">![Controleer of de uitvoer](./media/data-lake-store-stream-analytics/run.query.4.png "uitvoer controleren")</span><span class="sxs-lookup"><span data-stu-id="64e36-179">![Verify output](./media/data-lake-store-stream-analytics/run.query.4.png "Verify output")</span></span>

    <span data-ttu-id="64e36-180">In het deelvenster Data Explorer u ziet dat de uitvoer wordt geschreven naar het pad naar een map zoals opgegeven in de Data Lake Store uitvoerinstellingen (`streamanalytics/job/output/{date}/{time}`).</span><span class="sxs-lookup"><span data-stu-id="64e36-180">In the Data Explorer pane, notice that the output is written to a folder path as specified in the Data Lake Store output settings (`streamanalytics/job/output/{date}/{time}`).</span></span>  

## <a name="see-also"></a><span data-ttu-id="64e36-181">Zie ook</span><span class="sxs-lookup"><span data-stu-id="64e36-181">See also</span></span>
* [<span data-ttu-id="64e36-182">Maken van een HDInsight-cluster voor het gebruik van Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="64e36-182">Create an HDInsight cluster to use Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
