---
title: aaaStream gegevens van de Stream Analytics in Data Lake Store | Microsoft Docs
description: Azure Stream Analytics toostream gegevens worden gebruikt in Azure Data Lake Store
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
ms.openlocfilehash: 68c727d4807db0abe6efa90145d68c78902eb789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="stream-data-from-azure-storage-blob-into-data-lake-store-using-azure-stream-analytics"></a><span data-ttu-id="3326c-103">Gegevens streamen van Azure Storage Blob naar Data Lake Store met behulp van Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3326c-103">Stream data from Azure Storage Blob into Data Lake Store using Azure Stream Analytics</span></span>
<span data-ttu-id="3326c-104">In dit artikel leert u hoe toouse Azure Data Lake opslaan als uitvoer voor een Azure Stream Analytics-taak.</span><span class="sxs-lookup"><span data-stu-id="3326c-104">In this article you will learn how toouse Azure Data Lake Store as an output for an Azure Stream Analytics job.</span></span> <span data-ttu-id="3326c-105">In dit artikel ziet u een eenvoudig scenario die gegevens uit een Azure Storage-blob (invoer leest) en schrijfbewerkingen Hallo data tooData Lake Store (uitvoer).</span><span class="sxs-lookup"><span data-stu-id="3326c-105">This article demonstrates a simple scenario that reads data from an Azure Storage blob (input) and writes hello data tooData Lake Store (output).</span></span>

> [!NOTE]
> <span data-ttu-id="3326c-106">Op dit moment kunt maken en de configuratie van Data Lake Store voert voor Stream Analytics wordt alleen ondersteund in Hallo [klassieke Azure-Portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="3326c-106">At this time, creation and configuration of Data Lake Store outputs for Stream Analytics is supported only in hello [Azure Classic Portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="3326c-107">Sommige onderdelen van deze zelfstudie wordt daarom Hallo klassieke Azure-Portal gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3326c-107">Hence, some parts of this tutorial will use hello Azure Classic Portal.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="3326c-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3326c-108">Prerequisites</span></span>
<span data-ttu-id="3326c-109">Voordat u deze zelfstudie begint, moet u de volgende Hallo hebben:</span><span class="sxs-lookup"><span data-stu-id="3326c-109">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="3326c-110">**Een Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="3326c-110">**An Azure subscription**.</span></span> <span data-ttu-id="3326c-111">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3326c-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="3326c-112">**Azure Storage-account**.</span><span class="sxs-lookup"><span data-stu-id="3326c-112">**Azure Storage account**.</span></span> <span data-ttu-id="3326c-113">U gebruikt een blob-container van deze account tooinput-gegevens voor een Stream Analytics-taak.</span><span class="sxs-lookup"><span data-stu-id="3326c-113">You will use a blob container from this account tooinput data for a Stream Analytics job.</span></span> <span data-ttu-id="3326c-114">Voor deze zelfstudie wordt ervan uitgegaan er een opslagaccount die is aangeroepen **storageforasa** en een container in Hallo rekening met de naam **storageforasacontainer**.</span><span class="sxs-lookup"><span data-stu-id="3326c-114">For this tutorial, assume you have a storage account called **storageforasa** and a container within hello account called **storageforasacontainer**.</span></span> <span data-ttu-id="3326c-115">Nadat u Hallo container hebt gemaakt, uploadt u een voorbeeld gegevens bestand tooit.</span><span class="sxs-lookup"><span data-stu-id="3326c-115">Once you have created hello container, upload a sample data file tooit.</span></span> 
  
* <span data-ttu-id="3326c-116">**Azure Data Lake Store-account**.</span><span class="sxs-lookup"><span data-stu-id="3326c-116">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="3326c-117">Volg de instructies Hallo voor [aan de slag met Azure Data Lake Store met Azure Portal Hallo](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3326c-117">Follow hello instructions at [Get started with Azure Data Lake Store using hello Azure Portal](data-lake-store-get-started-portal.md).</span></span> <span data-ttu-id="3326c-118">Stel u hebt een Data Lake Store-account genoemd **asadatalakestore**.</span><span class="sxs-lookup"><span data-stu-id="3326c-118">Let's assume you have a Data Lake Store account called **asadatalakestore**.</span></span> 

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="3326c-119">Een Stream Analytics-taak maken</span><span class="sxs-lookup"><span data-stu-id="3326c-119">Create a Stream Analytics Job</span></span>
<span data-ttu-id="3326c-120">U begint met het maken van een Stream Analytics-taak die bestaat uit een invoerbron en een bestemming voor de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="3326c-120">You start by creating a Stream Analytics job that includes an input source and an output destination.</span></span> <span data-ttu-id="3326c-121">Voor deze zelfstudie Hallo-bron is een Azure blob-container en Hallo bestemming is Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="3326c-121">For this tutorial, hello source is an Azure blob container and hello destination is Data Lake Store.</span></span>

1. <span data-ttu-id="3326c-122">Meld u aan bij toohello [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3326c-122">Sign on toohello [Azure Portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="3326c-123">Klik in het linkerdeelvenster hello, **Stream Analytics-taken**, en klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="3326c-123">From hello left pane, click **Stream Analytics jobs**, and then click **Add**.</span></span>

    <span data-ttu-id="3326c-124">![Maken van een Stream Analytics-taak](./media/data-lake-store-stream-analytics/create.job.png "een Stream Analytics-taak maken")</span><span class="sxs-lookup"><span data-stu-id="3326c-124">![Create a Stream Analytics Job](./media/data-lake-store-stream-analytics/create.job.png "Create a Stream Analytics job")</span></span>

    > [!NOTE]
    > <span data-ttu-id="3326c-125">Zorg ervoor dat u taak maken in Hallo dezelfde regio bevinden als het Hallo-opslagaccount of u, worden extra kosten van het verplaatsen van gegevens tussen regio's.</span><span class="sxs-lookup"><span data-stu-id="3326c-125">Make sure you create job in hello same region as hello storage account or you will incur additional cost of moving data between regions.</span></span>
    >

## <a name="create-a-blob-input-for-hello-job"></a><span data-ttu-id="3326c-126">Een Blob-invoer voor Hallo-taak maken</span><span class="sxs-lookup"><span data-stu-id="3326c-126">Create a Blob input for hello job</span></span>

1. <span data-ttu-id="3326c-127">Open Hallo-pagina voor Hallo Stream Analytics-taak in het linkerdeelvenster Hallo klikt u op Hallo **invoer** tabblad en klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="3326c-127">Open hello page for hello Stream Analytics job, from hello left pane click hello **Inputs** tab, and then click **Add**.</span></span>

    <span data-ttu-id="3326c-128">![Toevoegen van een taak invoer tooyour](./media/data-lake-store-stream-analytics/create.input.1.png "een taak invoer tooyour toevoegen")</span><span class="sxs-lookup"><span data-stu-id="3326c-128">![Add an input tooyour job](./media/data-lake-store-stream-analytics/create.input.1.png "Add an input tooyour job")</span></span>

2. <span data-ttu-id="3326c-129">Op Hallo **nieuwe invoer** blade Hallo volgende waarden bevatten.</span><span class="sxs-lookup"><span data-stu-id="3326c-129">On hello **New input** blade, provide hello following values.</span></span>

    <span data-ttu-id="3326c-130">![Toevoegen van een taak invoer tooyour](./media/data-lake-store-stream-analytics/create.input.2.png "een taak invoer tooyour toevoegen")</span><span class="sxs-lookup"><span data-stu-id="3326c-130">![Add an input tooyour job](./media/data-lake-store-stream-analytics/create.input.2.png "Add an input tooyour job")</span></span>

    * <span data-ttu-id="3326c-131">Voor **invoer alias**, voer een unieke naam voor Hallo taak invoer.</span><span class="sxs-lookup"><span data-stu-id="3326c-131">For **Input alias**, enter a unique name for hello job input.</span></span>
    * <span data-ttu-id="3326c-132">Voor **gegevensbrontype**, selecteer **gegevensstroom**.</span><span class="sxs-lookup"><span data-stu-id="3326c-132">For **Source type**, select **Data stream**.</span></span>
    * <span data-ttu-id="3326c-133">Voor **bron**, selecteer **Blob storage**.</span><span class="sxs-lookup"><span data-stu-id="3326c-133">For **Source**, select **Blob storage**.</span></span>
    * <span data-ttu-id="3326c-134">Voor **abonnement**, selecteer **gebruik blob storage uit het huidige abonnement**.</span><span class="sxs-lookup"><span data-stu-id="3326c-134">For **Subscription**, select **Use blob storage from current subscription**.</span></span>
    * <span data-ttu-id="3326c-135">Voor **opslagaccount**, selecteer Hallo storage-account dat u hebt gemaakt als onderdeel van Hallo vereisten.</span><span class="sxs-lookup"><span data-stu-id="3326c-135">For **Storage account**, select hello storage account that you created as part of hello prerequisites.</span></span> 
    * <span data-ttu-id="3326c-136">Voor **Container**, selecteer Hallo-container die u hebt gemaakt in Hallo storage-account geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="3326c-136">For **Container**, select hello container that you created in hello selected storage account.</span></span>
    * <span data-ttu-id="3326c-137">Voor **gebeurtenis serialisatie-indeling**, selecteer **CSV**.</span><span class="sxs-lookup"><span data-stu-id="3326c-137">For **Event serialization format**, select **CSV**.</span></span>
    * <span data-ttu-id="3326c-138">Voor **scheidingsteken**, selecteer **tabblad**.</span><span class="sxs-lookup"><span data-stu-id="3326c-138">For **Delimiter**, select **tab**.</span></span>
    * <span data-ttu-id="3326c-139">Voor **codering**, selecteer **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="3326c-139">For **Encoding**, select **UTF-8**.</span></span>

    <span data-ttu-id="3326c-140">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="3326c-140">Click **Create**.</span></span> <span data-ttu-id="3326c-141">Hallo portal nu voegt Hallo invoer en Hallo verbinding tooit wordt getest.</span><span class="sxs-lookup"><span data-stu-id="3326c-141">hello portal now adds hello input and tests hello connection tooit.</span></span>


## <a name="create-a-data-lake-store-output-for-hello-job"></a><span data-ttu-id="3326c-142">De uitvoer van een Data Lake Store voor Hallo-taak maken</span><span class="sxs-lookup"><span data-stu-id="3326c-142">Create a Data Lake Store output for hello job</span></span>

1. <span data-ttu-id="3326c-143">Open de pagina Hallo voor Hallo Stream Analytics-taak, klikt u op Hallo **uitvoer** tabblad en klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="3326c-143">Open hello page for hello Stream Analytics job, click hello **Outputs** tab, and then click **Add**.</span></span>

    <span data-ttu-id="3326c-144">![Toevoegen van een taak van uitvoer tooyour](./media/data-lake-store-stream-analytics/create.output.1.png "een tooyour uitvoer taak toevoegen")</span><span class="sxs-lookup"><span data-stu-id="3326c-144">![Add an output tooyour job](./media/data-lake-store-stream-analytics/create.output.1.png "Add an output tooyour job")</span></span>

2. <span data-ttu-id="3326c-145">Op Hallo **nieuwe uitvoer** blade Hallo volgende waarden bevatten.</span><span class="sxs-lookup"><span data-stu-id="3326c-145">On hello **New output** blade, provide hello following values.</span></span>

    <span data-ttu-id="3326c-146">![Toevoegen van een taak van uitvoer tooyour](./media/data-lake-store-stream-analytics/create.output.2.png "een tooyour uitvoer taak toevoegen")</span><span class="sxs-lookup"><span data-stu-id="3326c-146">![Add an output tooyour job](./media/data-lake-store-stream-analytics/create.output.2.png "Add an output tooyour job")</span></span>

    * <span data-ttu-id="3326c-147">Voor **uitvoeraliassen**, voer een een unieke naam voor de taakuitvoer Hallo.</span><span class="sxs-lookup"><span data-stu-id="3326c-147">For **Output alias**, enter a a unique name for hello job output.</span></span> <span data-ttu-id="3326c-148">Dit is een beschrijvende naam die is gebruikt in query's toodirect Hallo query uitvoer toothis Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="3326c-148">This is a friendly name used in queries toodirect hello query output toothis Data Lake Store.</span></span>
    * <span data-ttu-id="3326c-149">Voor **Sink**, selecteer **Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="3326c-149">For **Sink**, select **Data Lake Store**.</span></span>
    * <span data-ttu-id="3326c-150">U zult de vraag tooauthorize toegang tot tooData Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="3326c-150">You will be prompted tooauthorize access tooData Lake Store account.</span></span> <span data-ttu-id="3326c-151">Klik op **autoriseren**.</span><span class="sxs-lookup"><span data-stu-id="3326c-151">Click **Authorize**.</span></span>

3. <span data-ttu-id="3326c-152">Op Hallo **nieuwe uitvoer** blade tooprovide Hallo waarden na te gaan.</span><span class="sxs-lookup"><span data-stu-id="3326c-152">On hello **New output** blade, continue tooprovide hello following values.</span></span>

    <span data-ttu-id="3326c-153">![Toevoegen van een taak van uitvoer tooyour](./media/data-lake-store-stream-analytics/create.output.3.png "een tooyour uitvoer taak toevoegen")</span><span class="sxs-lookup"><span data-stu-id="3326c-153">![Add an output tooyour job](./media/data-lake-store-stream-analytics/create.output.3.png "Add an output tooyour job")</span></span>

    * <span data-ttu-id="3326c-154">Voor **accountnaam**, Hallo u al waar u Hallo taak uitvoer toobe verzonden gemaakt naar Data Lake Store-account selecteren.</span><span class="sxs-lookup"><span data-stu-id="3326c-154">For **Account name**, select hello Data Lake Store account you already created where you want hello job output toobe sent to.</span></span>
    * <span data-ttu-id="3326c-155">Voor **pad voorvoegselpatroon**, voer een pad dat wordt gebruikt bestand toowrite uw bestanden binnen Hallo Data Lake Store-account opgegeven.</span><span class="sxs-lookup"><span data-stu-id="3326c-155">For **Path prefix pattern**, enter a file path used toowrite your files within hello specified Data Lake Store account.</span></span>
    * <span data-ttu-id="3326c-156">Voor **datumnotatie**, als u een datum-token in Hallo voorvoegsel pad gebruikt, kunt u Hallo datumnotatie waarin de bestanden zijn ingedeeld.</span><span class="sxs-lookup"><span data-stu-id="3326c-156">For **Date format**, if you used a date token in hello prefix path, you can select hello date format in which your files are organized.</span></span>
    * <span data-ttu-id="3326c-157">Voor **tijdnotatie**, als u een token tijd in het pad naar het voorvoegsel van de hello gebruikt, geef Hallo tijdnotatie waarin de bestanden zijn ingedeeld.</span><span class="sxs-lookup"><span data-stu-id="3326c-157">For **Time format**, if you used a time token in hello prefix path, specify hello time format in which your files are organized.</span></span>
    * <span data-ttu-id="3326c-158">Voor **gebeurtenis serialisatie-indeling**, selecteer **CSV**.</span><span class="sxs-lookup"><span data-stu-id="3326c-158">For **Event serialization format**, select **CSV**.</span></span>
    * <span data-ttu-id="3326c-159">Voor **scheidingsteken**, selecteer **tabblad**.</span><span class="sxs-lookup"><span data-stu-id="3326c-159">For **Delimiter**, select **tab**.</span></span>
    * <span data-ttu-id="3326c-160">Voor **codering**, selecteer **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="3326c-160">For **Encoding**, select **UTF-8**.</span></span>
    
    <span data-ttu-id="3326c-161">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="3326c-161">Click **Create**.</span></span> <span data-ttu-id="3326c-162">Hallo portal nu Hallo uitvoer toegevoegd en Hallo verbinding tooit wordt getest.</span><span class="sxs-lookup"><span data-stu-id="3326c-162">hello portal now adds hello output and tests hello connection tooit.</span></span>
    
## <a name="run-hello-stream-analytics-job"></a><span data-ttu-id="3326c-163">Hallo Stream Analytics-taak uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="3326c-163">Run hello Stream Analytics job</span></span>

1. <span data-ttu-id="3326c-164">toorun een Stream Analytics-taak, moet u een query uitvoeren vanaf Hallo **Query** tabblad. U kunt voor deze zelfstudie Hallo voorbeeldquery uitvoeren door te vervangen Hallo tijdelijke aanduidingen door Hallo taak aliassen invoer en uitvoer, zoals wordt weergegeven in onderstaande Hallo schermafbeelding.</span><span class="sxs-lookup"><span data-stu-id="3326c-164">toorun a Stream Analytics job, you must run a query from hello **Query** tab. For this tutorial, you can run hello sample query by replacing hello placeholders with hello job input and output aliases, as shown in hello screen capture below.</span></span>

    <span data-ttu-id="3326c-165">![Voer query](./media/data-lake-store-stream-analytics/run.query.png "query uitvoeren")</span><span class="sxs-lookup"><span data-stu-id="3326c-165">![Run query](./media/data-lake-store-stream-analytics/run.query.png "Run query")</span></span>

2. <span data-ttu-id="3326c-166">Klik op **opslaan** vanaf de bovenkant Hallo van welkomstscherm en vervolgens van Hallo **overzicht** tabblad **Start**.</span><span class="sxs-lookup"><span data-stu-id="3326c-166">Click **Save** from hello top of hello screen, and then from hello **Overview** tab, click **Start**.</span></span> <span data-ttu-id="3326c-167">Selecteer in het dialoogvenster Hallo **aangepaste tijd**, en stel vervolgens Hallo huidige datum en tijd.</span><span class="sxs-lookup"><span data-stu-id="3326c-167">From hello dialog box, select **Custom Time**, and then set hello current date and time.</span></span>

    <span data-ttu-id="3326c-168">![Taaktijd instellen](./media/data-lake-store-stream-analytics/run.query.2.png "taaktijd instellen")</span><span class="sxs-lookup"><span data-stu-id="3326c-168">![Set job time](./media/data-lake-store-stream-analytics/run.query.2.png "Set job time")</span></span>

    <span data-ttu-id="3326c-169">Klik op **Start** toostart Hallo taak.</span><span class="sxs-lookup"><span data-stu-id="3326c-169">Click **Start** toostart hello job.</span></span> <span data-ttu-id="3326c-170">Tooa paar minuten toostart Hallo taak kan duren.</span><span class="sxs-lookup"><span data-stu-id="3326c-170">It can take up tooa couple minutes toostart hello job.</span></span>

3. <span data-ttu-id="3326c-171">tootrigger hello toopick Hallo taakgegevens van Hallo-blob kopiëren een sample data bestand toohello blob-container.</span><span class="sxs-lookup"><span data-stu-id="3326c-171">tootrigger hello job toopick hello data from hello blob, copy a sample data file toohello blob container.</span></span> <span data-ttu-id="3326c-172">U krijgt een voorbeeldgegevensbestand van Hallo [Azure Data Lake Git-opslagplaats](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).</span><span class="sxs-lookup"><span data-stu-id="3326c-172">You can get a sample data file from hello [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).</span></span> <span data-ttu-id="3326c-173">Kopieer Hallo-bestand voor deze zelfstudie **vehicle1_09142014.csv**.</span><span class="sxs-lookup"><span data-stu-id="3326c-173">For this tutorial, let's copy hello file **vehicle1_09142014.csv**.</span></span> <span data-ttu-id="3326c-174">U kunt verschillende clients, zoals [Azure Opslagverkenner](http://storageexplorer.com/), tooupload gegevens tooa blob-container.</span><span class="sxs-lookup"><span data-stu-id="3326c-174">You can use various clients, such as [Azure Storage Explorer](http://storageexplorer.com/), tooupload data tooa blob container.</span></span>

4. <span data-ttu-id="3326c-175">Van Hallo **overzicht** tabblad onder **bewaking**, Zie hoe Hallo gegevens is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="3326c-175">From hello **Overview** tab, under **Monitoring**, see how hello data was processed.</span></span>

    <span data-ttu-id="3326c-176">![Monitor taak](./media/data-lake-store-stream-analytics/run.query.3.png "Monitor taak")</span><span class="sxs-lookup"><span data-stu-id="3326c-176">![Monitor job](./media/data-lake-store-stream-analytics/run.query.3.png "Monitor job")</span></span>

5. <span data-ttu-id="3326c-177">Ten slotte kunt u controleren dat Hallo taak uitvoergegevens beschikbaar in Data Lake Store-account voor Hallo is.</span><span class="sxs-lookup"><span data-stu-id="3326c-177">Finally, you can verify that hello job output data is available in hello Data Lake Store account.</span></span> 

    <span data-ttu-id="3326c-178">![Controleer of de uitvoer](./media/data-lake-store-stream-analytics/run.query.4.png "uitvoer controleren")</span><span class="sxs-lookup"><span data-stu-id="3326c-178">![Verify output](./media/data-lake-store-stream-analytics/run.query.4.png "Verify output")</span></span>

    <span data-ttu-id="3326c-179">In Hallo Data Explorer deelvenster ziet u dat Hallo uitvoer is geschreven tooa pad als opgegeven in Hallo uitvoerinstellingen Data Lake Store (`streamanalytics/job/output/{date}/{time}`).</span><span class="sxs-lookup"><span data-stu-id="3326c-179">In hello Data Explorer pane, notice that hello output is written tooa folder path as specified in hello Data Lake Store output settings (`streamanalytics/job/output/{date}/{time}`).</span></span>  

## <a name="see-also"></a><span data-ttu-id="3326c-180">Zie ook</span><span class="sxs-lookup"><span data-stu-id="3326c-180">See also</span></span>
* [<span data-ttu-id="3326c-181">Maken van een HDInsight-cluster toouse Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="3326c-181">Create an HDInsight cluster toouse Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
