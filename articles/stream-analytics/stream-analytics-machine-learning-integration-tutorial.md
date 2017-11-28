---
title: aaaAzure Stream Analytics en Machine Learning-integratie | Microsoft Docs
description: Hoe toouse een gebruiker gedefinieerde functie en Machine Learning in een Stream Analytics-taak
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: cfced01f-ccaa-4bc6-81e2-c03d1470a7a2
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 07/06/2017
ms.author: jeffstok
ms.openlocfilehash: e1ba7ab51ece80719839793e1320a7666cfc4181
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="performing-sentiment-analysis-by-using-azure-stream-analytics-and-azure-machine-learning"></a><span data-ttu-id="600f2-103">Gevoel analyse uitvoeren met behulp van Azure Stream Analytics en Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="600f2-103">Performing sentiment analysis by using Azure Stream Analytics and Azure Machine Learning</span></span>
<span data-ttu-id="600f2-104">Dit artikel wordt beschreven hoe een eenvoudige Azure Stream Analytics-taak die Azure Machine Learning integreert tooquickly ingesteld.</span><span class="sxs-lookup"><span data-stu-id="600f2-104">This article describes how tooquickly set up a simple Azure Stream Analytics job that integrates Azure Machine Learning.</span></span> <span data-ttu-id="600f2-105">U gebruikt een Machine Learning gevoel analytics-model uit Hallo Cortana Intelligence Gallery tooanalyze streaming tekstgegevens en Hallo gevoel score in realtime te bepalen.</span><span class="sxs-lookup"><span data-stu-id="600f2-105">You use a Machine Learning sentiment analytics model from hello Cortana Intelligence Gallery tooanalyze streaming text data and determine hello sentiment score in real time.</span></span> <span data-ttu-id="600f2-106">Hallo Cortana Intelligence Suite kunt u deze taak uitvoeren zonder dat u Hallo gecompliceerde aspecten van het bouwen van een gevoel analytics-model.</span><span class="sxs-lookup"><span data-stu-id="600f2-106">Using hello Cortana Intelligence Suite lets you accomplish this task without worrying about hello intricacies of building a sentiment analytics model.</span></span>

<span data-ttu-id="600f2-107">U kunt toepassen wat u leert van dit artikel tooscenarios zoals deze:</span><span class="sxs-lookup"><span data-stu-id="600f2-107">You can apply what you learn from this article tooscenarios such as these:</span></span>

* <span data-ttu-id="600f2-108">Analyse van realtime gevoel op Twitter gegevensstromen.</span><span class="sxs-lookup"><span data-stu-id="600f2-108">Analyzing real-time sentiment on streaming Twitter data.</span></span>
* <span data-ttu-id="600f2-109">Records van de klant analyseren chats met het ondersteunend personeel.</span><span class="sxs-lookup"><span data-stu-id="600f2-109">Analyzing records of customer chats with support staff.</span></span>
* <span data-ttu-id="600f2-110">Evalueren van opmerkingen over forums, blogs en video's.</span><span class="sxs-lookup"><span data-stu-id="600f2-110">Evaluating comments on forums, blogs, and videos.</span></span> 
* <span data-ttu-id="600f2-111">Veel andere realtime, voorspellende scoreprofiel scenario's.</span><span class="sxs-lookup"><span data-stu-id="600f2-111">Many other real-time, predictive scoring scenarios.</span></span>

<span data-ttu-id="600f2-112">In een Praktijkscenario krijgt u rechtstreeks vanuit een gegevensstroom Twitter Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="600f2-112">In a real-world scenario, you would get hello data directly from a Twitter data stream.</span></span> <span data-ttu-id="600f2-113">toosimplify hello zelfstudie we hebt geschreven zodat hello Streaming Analytics-taak opgehaald tweets uit een CSV-bestand in Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="600f2-113">toosimplify hello tutorial, we've written it so that hello Streaming Analytics job gets tweets from a CSV file in Azure Blob storage.</span></span> <span data-ttu-id="600f2-114">U kunt uw eigen CSV-bestand maken of u kunt een CSV-voorbeeldbestand, zoals wordt weergegeven in Hallo installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="600f2-114">You can create your own CSV file, or you can use a sample CSV file, as shown in hello following image:</span></span>

![voorbeeld tweets in een CSV-bestand](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-2.png)  

<span data-ttu-id="600f2-116">Hallo Streaming Analytics-taak die u maakt is van toepassing hello gevoel analytics-model als een gebruiker gedefinieerde functie (UDF) op de voorbeeldgegevens tekst hello van Hallo bloblarchief.</span><span class="sxs-lookup"><span data-stu-id="600f2-116">hello Streaming Analytics job that you create applies hello sentiment analytics model as a user-defined function (UDF) on hello sample text data from hello blob store.</span></span> <span data-ttu-id="600f2-117">Hallo-uitvoer (Hallo resultaat van Hallo gevoel analyse) geschreven toohello dezelfde blob-opslag in een ander CSV-bestand.</span><span class="sxs-lookup"><span data-stu-id="600f2-117">hello output (hello result of hello sentiment analysis) is written toohello same blob store in a different CSV file.</span></span> 

<span data-ttu-id="600f2-118">Hallo volgende afbeelding ziet u deze configuratie.</span><span class="sxs-lookup"><span data-stu-id="600f2-118">hello following figure demonstrates this configuration.</span></span> <span data-ttu-id="600f2-119">Zoals aangegeven voor een meer realistische scenario kunt u de blob-opslag met Twitter-gegevens uit Azure Event Hubs invoer streaming vervangen.</span><span class="sxs-lookup"><span data-stu-id="600f2-119">As noted, for a more realistic scenario, you can replace blob storage with streaming Twitter data from an Azure Event Hubs input.</span></span> <span data-ttu-id="600f2-120">Bovendien kan u samenstellen een [Microsoft Power BI](https://powerbi.microsoft.com/) realtime visualisatie van cumulatieve gevoel Hallo.</span><span class="sxs-lookup"><span data-stu-id="600f2-120">Additionally, you could build a [Microsoft Power BI](https://powerbi.microsoft.com/) real-time visualization of hello aggregate sentiment.</span></span>    

![Overzicht van stream Analytics Machine Learning-integratie](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-1.png)  

## <a name="prerequisites"></a><span data-ttu-id="600f2-122">Vereisten</span><span class="sxs-lookup"><span data-stu-id="600f2-122">Prerequisites</span></span>
<span data-ttu-id="600f2-123">Zorg voordat u begint, hebt u de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="600f2-123">Before you start, make sure you have hello following:</span></span>

* <span data-ttu-id="600f2-124">Een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="600f2-124">An active Azure subscription.</span></span>
* <span data-ttu-id="600f2-125">Een CSV-bestand met sommige gegevens in het.</span><span class="sxs-lookup"><span data-stu-id="600f2-125">A CSV file with some data in it.</span></span> <span data-ttu-id="600f2-126">U kunt eerder weergegeven uit Hallo-bestand downloaden [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv), of u kunt uw eigen bestand maken.</span><span class="sxs-lookup"><span data-stu-id="600f2-126">You can download hello file shown earlier from [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv), or you can create your own file.</span></span> <span data-ttu-id="600f2-127">Voor dit artikel nemen we aan dat u Hallo bestand vanuit GitHub.</span><span class="sxs-lookup"><span data-stu-id="600f2-127">For this article, we assume that you're using hello file from GitHub.</span></span>

<span data-ttu-id="600f2-128">Op een hoog niveau toocomplete Hallo taken in dit artikel wordt uitgelegd u Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="600f2-128">At a high level, toocomplete hello tasks demonstrated in this article, you do hello following:</span></span>

1. <span data-ttu-id="600f2-129">Een Azure storage-account en een blob storage-container maken en uploaden van een CSV-indeling invoerbestand toohello-container.</span><span class="sxs-lookup"><span data-stu-id="600f2-129">Create an Azure storage account and a blob storage container, and upload a CSV-formatted input file toohello container.</span></span>
3. <span data-ttu-id="600f2-130">Een gevoel analytics-model van Hallo Cortana Intelligence Gallery tooyour Azure Machine Learning-werkruimte toevoegen en dit model implementeren als een webservice in Hallo Machine Learning-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="600f2-130">Add a sentiment analytics model from hello Cortana Intelligence Gallery tooyour Azure Machine Learning workspace and deploy this model as a web service in hello Machine Learning workspace.</span></span>
5. <span data-ttu-id="600f2-131">Een Stream Analytics-taak die deze webservice als een functie in volgorde toodetermine gevoel voor tekstinvoer Hallo aanroepen maken.</span><span class="sxs-lookup"><span data-stu-id="600f2-131">Create a Stream Analytics job that calls this web service as a function in order toodetermine sentiment for hello text input.</span></span>
6. <span data-ttu-id="600f2-132">Hallo Stream Analytics-taak starten en controleer Hallo uitvoer.</span><span class="sxs-lookup"><span data-stu-id="600f2-132">Start hello Stream Analytics job and check hello output.</span></span>

## <a name="create-a-storage-container-and-upload-hello-csv-input-file"></a><span data-ttu-id="600f2-133">Een opslagcontainer maken en uploaden Hallo CSV-bestand voor invoer</span><span class="sxs-lookup"><span data-stu-id="600f2-133">Create a storage container and upload hello CSV input file</span></span>
<span data-ttu-id="600f2-134">Voor deze stap kunt u een CSV-bestand, zoals Hallo een beschikbaar is via GitHub.</span><span class="sxs-lookup"><span data-stu-id="600f2-134">For this step, you can use any CSV file, such as hello one available from GitHub.</span></span>

1. <span data-ttu-id="600f2-135">Klik in hello Azure-portal, op **nieuw** &gt; **opslag** &gt; **opslagaccount**.</span><span class="sxs-lookup"><span data-stu-id="600f2-135">In hello Azure portal, click **New** &gt; **Storage** &gt; **Storage account**.</span></span>

   ![Nieuw opslagaccount maken](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-create-storage-account.png)

2. <span data-ttu-id="600f2-137">Geef een naam (`samldemo` in Hallo voorbeeld).</span><span class="sxs-lookup"><span data-stu-id="600f2-137">Provide a name (`samldemo` in hello example).</span></span> <span data-ttu-id="600f2-138">Hallo-naam kan gebruiken die alleen kleine letters en cijfers en deze uniek zijn binnen Azure.</span><span class="sxs-lookup"><span data-stu-id="600f2-138">hello name can use only lowercase letters and numbers, and it must be unique across Azure.</span></span> 

3. <span data-ttu-id="600f2-139">Geef een bestaande resourcegroep en locatie opgeven.</span><span class="sxs-lookup"><span data-stu-id="600f2-139">Specify an existing resource group and specify a location.</span></span> <span data-ttu-id="600f2-140">Locatie voor het is raadzaam alle Hallo resources die zijn gemaakt in deze zelfstudie gebruik Hallo dezelfde locatie.</span><span class="sxs-lookup"><span data-stu-id="600f2-140">For location, we recommend that all hello resources created in this tutorial use hello same location.</span></span>

    ![Geef details op storage-account](./media/stream-analytics-machine-learning-integration-tutorial/create-sa1.png)

4. <span data-ttu-id="600f2-142">Selecteer in hello Azure-portal, Hallo storage-account.</span><span class="sxs-lookup"><span data-stu-id="600f2-142">In hello Azure portal, select hello storage account.</span></span> <span data-ttu-id="600f2-143">Klik in de blade opslagaccount hello **Containers** en klik vervolgens op  **+ &nbsp;Container** toocreate blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="600f2-143">In hello storage account blade, click **Containers** and then click **+&nbsp;Container** toocreate blob storage.</span></span>

    ![blob-container maken](./media/stream-analytics-machine-learning-integration-tutorial/create-sa2.png)

5. <span data-ttu-id="600f2-145">Geef een naam voor het Hallo-container (`azuresamldemoblob` in Hallo voorbeeld) en controleer of **toegangstype** te is ingesteld**Blob**.</span><span class="sxs-lookup"><span data-stu-id="600f2-145">Provide a name for hello container (`azuresamldemoblob` in hello example) and verify that **Access type** is set too**Blob**.</span></span> <span data-ttu-id="600f2-146">Wanneer u klaar bent, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="600f2-146">When you're done, click **OK**.</span></span>

    ![Geef details van blob-container](./media/stream-analytics-machine-learning-integration-tutorial/create-sa3.png)

6. <span data-ttu-id="600f2-148">In Hallo **Containers** blade, selecteer Hallo nieuwe container, Hallo blade voor die container te openen.</span><span class="sxs-lookup"><span data-stu-id="600f2-148">In hello **Containers** blade, select hello new container, which opens hello blade for that container.</span></span>

7. <span data-ttu-id="600f2-149">Klik op **Uploaden**.</span><span class="sxs-lookup"><span data-stu-id="600f2-149">Click **Upload**.</span></span>

    ![Knop voor een container uploaden](./media/stream-analytics-machine-learning-integration-tutorial/create-sa-upload-button.png)

8. <span data-ttu-id="600f2-151">In Hallo **blob uploaden** blade Hallo CSV-bestand dat u voor deze zelfstudie toouse wilt opgeven.</span><span class="sxs-lookup"><span data-stu-id="600f2-151">In hello **Upload blob** blade, specify hello CSV file that you want toouse for this tutorial.</span></span> <span data-ttu-id="600f2-152">Voor **type Blob**, selecteer **blok-blob** en set Hallo blok grootte too4 MB, hetgeen voldoende is voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="600f2-152">For **Blob type**, select **Block blob** and set hello block size too4 MB, which is sufficient for this tutorial.</span></span>

    ![blob-bestand uploaden](./media/stream-analytics-machine-learning-integration-tutorial/create-sa4.png)

9. <span data-ttu-id="600f2-154">Klik op Hallo **uploaden** knop Hallo Hallo blade onderaan in.</span><span class="sxs-lookup"><span data-stu-id="600f2-154">Click hello **Upload** button at hello bottom of hello blade.</span></span>

## <a name="add-hello-sentiment-analytics-model-from-hello-cortana-intelligence-gallery"></a><span data-ttu-id="600f2-155">Hallo gevoel analytics-model van Hallo Cortana Intelligence Gallery toevoegen</span><span class="sxs-lookup"><span data-stu-id="600f2-155">Add hello sentiment analytics model from hello Cortana Intelligence Gallery</span></span>

<span data-ttu-id="600f2-156">Nu dat Hallo voorbeeldgegevens in een blob, kunt u Hallo gevoel Analytics-model in de Cortana Intelligence Gallery inschakelen.</span><span class="sxs-lookup"><span data-stu-id="600f2-156">Now that hello sample data is in a blob, you can enable hello sentiment analysis model in Cortana Intelligence Gallery.</span></span>

1. <span data-ttu-id="600f2-157">Ga toohello [gevoel predictive analytics-model](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) pagina in Cortana Intelligence Gallery Hallo.</span><span class="sxs-lookup"><span data-stu-id="600f2-157">Go toohello [predictive sentiment analytics model](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) page in hello Cortana Intelligence Gallery.</span></span>  

2. <span data-ttu-id="600f2-158">Klik op **openen in Studio**.</span><span class="sxs-lookup"><span data-stu-id="600f2-158">Click **Open in Studio**.</span></span>  
   
   ![Stream Analytics Machine Learning, open Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-open-ml-studio.png)  

3. <span data-ttu-id="600f2-160">Meld u aan toogo toohello werkruimte.</span><span class="sxs-lookup"><span data-stu-id="600f2-160">Sign in toogo toohello workspace.</span></span> <span data-ttu-id="600f2-161">Selecteer een locatie.</span><span class="sxs-lookup"><span data-stu-id="600f2-161">Select a location.</span></span>

4. <span data-ttu-id="600f2-162">Klik op **uitvoeren** Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="600f2-162">Click **Run** at hello bottom of hello page.</span></span> <span data-ttu-id="600f2-163">Hallo-proces wordt uitgevoerd, wat duurt ongeveer een minuut.</span><span class="sxs-lookup"><span data-stu-id="600f2-163">hello process runs, which takes about a minute.</span></span>

   ![Voer experiment in Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-run-experiment.png)  

5. <span data-ttu-id="600f2-165">Nadat het Hallo-proces met succes is uitgevoerd, selecteert u **webservice implementeren** Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="600f2-165">After hello process has run successfully, select **Deploy Web Service** at hello bottom of hello page.</span></span>

   ![experiment in Machine Learning Studio implementeren als een webservice](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-deploy-web-service.png)  

6. <span data-ttu-id="600f2-167">toovalidate die Hallo gevoel analytics-model is gereed toouse, klikt u op Hallo **Test** knop.</span><span class="sxs-lookup"><span data-stu-id="600f2-167">toovalidate that hello sentiment analytics model is ready toouse, click hello **Test** button.</span></span> <span data-ttu-id="600f2-168">Tekst invoeren, zoals 'Ik hou Microsoft' opgeven.</span><span class="sxs-lookup"><span data-stu-id="600f2-168">Provide text input such as "I love Microsoft".</span></span> 

   ![Test-experiment in Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test.png)  

    <span data-ttu-id="600f2-170">Als de test Hallo werkt, ziet u een resultaat vergelijkbaar toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="600f2-170">If hello test works, you see a result similar toohello following example:</span></span>

   ![testresultaten in Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test-results.png)  

7. <span data-ttu-id="600f2-172">In Hallo **Apps** kolom, klikt u op Hallo **Excel 2010 of ouder werkmap** koppeling toodownload een Excel-werkmap.</span><span class="sxs-lookup"><span data-stu-id="600f2-172">In hello **Apps** column, click hello **Excel 2010 or earlier workbook** link toodownload an Excel workbook.</span></span> <span data-ttu-id="600f2-173">Hallo-werkmap bevat Hallo een API-sleutel en Hallo-URL moet u later tooset up Hallo Stream Analytics-taak.</span><span class="sxs-lookup"><span data-stu-id="600f2-173">hello workbook contains hello an API key and hello URL that you need later tooset up hello Stream Analytics job.</span></span>

    ![Stream Analytics, Machine Learning, snelle weergave](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-quick-glance.png)  


## <a name="create-a-stream-analytics-job-that-uses-hello-machine-learning-model"></a><span data-ttu-id="600f2-175">Maken van een Stream Analytics-taak die gebruikmaakt van Hallo Machine Learning-model</span><span class="sxs-lookup"><span data-stu-id="600f2-175">Create a Stream Analytics job that uses hello Machine Learning model</span></span>

<span data-ttu-id="600f2-176">U kunt nu een Stream Analytics-taak die Hallo voorbeeld tweets uit Hallo CSV-bestand in blob-opslag leest maken.</span><span class="sxs-lookup"><span data-stu-id="600f2-176">You can now create a Stream Analytics job that reads hello sample tweets from hello CSV file in blob storage.</span></span> 

### <a name="create-hello-job"></a><span data-ttu-id="600f2-177">Hallo-taak maken</span><span class="sxs-lookup"><span data-stu-id="600f2-177">Create hello job</span></span>

1. <span data-ttu-id="600f2-178">Ga toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="600f2-178">Go toohello [Azure portal](https://portal.azure.com).</span></span>  

2. <span data-ttu-id="600f2-179">Klik op **nieuw** > **Internet der dingen** > **Stream Analytics-taak**.</span><span class="sxs-lookup"><span data-stu-id="600f2-179">Click **New** > **Internet of Things** > **Stream Analytics job**.</span></span> 

   ![Azure portal pad voor het ophalen van tooa nieuwe Stream Analytics-taak](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-new-iot-sa-job.png)
   
3. <span data-ttu-id="600f2-181">Naam Hallo taak `azure-sa-ml-demo`, Geef een abonnement op, Geef een bestaande resourcegroep of maak een nieuwe en selecteer de locatie Hallo voor Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="600f2-181">Name hello job `azure-sa-ml-demo`, specify a subscription, specify an existing resource group or create a new one, and select hello location for hello job.</span></span>

   ![instellingen opgeven voor nieuwe Stream Analytics-taak](./media/stream-analytics-machine-learning-integration-tutorial/create-job-1.png)
   

### <a name="configure-hello-job-input"></a><span data-ttu-id="600f2-183">Hallo taak invoer configureren</span><span class="sxs-lookup"><span data-stu-id="600f2-183">Configure hello job input</span></span>
<span data-ttu-id="600f2-184">de invoer Hallo taak opgehaald uit Hallo CSV-bestand dat u eerder tooblob opslag geüpload.</span><span class="sxs-lookup"><span data-stu-id="600f2-184">hello job gets its input from hello CSV file that you uploaded earlier tooblob storage.</span></span>

1. <span data-ttu-id="600f2-185">Nadat het Hallo-taak is gemaakt, klikt u onder **taak topologie** Klik Hallo Hallo taakblade **invoer** vak.</span><span class="sxs-lookup"><span data-stu-id="600f2-185">After hello job has been created, under **Job Topology** in hello job blade, click hello **Inputs** box.</span></span>  
   
   ![Het selectievakje 'Invoer' in de blade voor Stream Analytics-taak](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input.png)  

2. <span data-ttu-id="600f2-187">In Hallo **invoer** blade, klikt u op **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="600f2-187">In hello **Inputs** blade, click **+ Add**.</span></span>

   ![Knop voor het toevoegen van een invoer toohello Stream Analytics-taak toevoegen](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input-button.png)  

3. <span data-ttu-id="600f2-189">Hallo invullen **nieuwe invoer** blade met deze waarden:</span><span class="sxs-lookup"><span data-stu-id="600f2-189">Fill out hello **New input** blade with these values:</span></span>

    * <span data-ttu-id="600f2-190">**Invoeralias**: Gebruik de naam van Hallo `datainput`.</span><span class="sxs-lookup"><span data-stu-id="600f2-190">**Input alias**: Use hello name `datainput`.</span></span>
    * <span data-ttu-id="600f2-191">**Gegevensbrontype**: Selecteer **gegevensstroom**.</span><span class="sxs-lookup"><span data-stu-id="600f2-191">**Source type**: Select **Data stream**.</span></span>
    * <span data-ttu-id="600f2-192">**Bron**: Selecteer **Blob storage**.</span><span class="sxs-lookup"><span data-stu-id="600f2-192">**Source**: Select **Blob storage**.</span></span>
    * <span data-ttu-id="600f2-193">**Optie importeren**: Selecteer **gebruik blob storage uit het huidige abonnement**.</span><span class="sxs-lookup"><span data-stu-id="600f2-193">**Import option**: Select **Use blob storage from current subscription**.</span></span> 
    * <span data-ttu-id="600f2-194">**Storage-account**.</span><span class="sxs-lookup"><span data-stu-id="600f2-194">**Storage account**.</span></span> <span data-ttu-id="600f2-195">Selecteer Hallo-opslagaccount die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="600f2-195">Select hello storage account you created earlier.</span></span>
    * <span data-ttu-id="600f2-196">**Container**.</span><span class="sxs-lookup"><span data-stu-id="600f2-196">**Container**.</span></span> <span data-ttu-id="600f2-197">Selecteer Hallo-container die u eerder hebt gemaakt (`azuresamldemoblob`).</span><span class="sxs-lookup"><span data-stu-id="600f2-197">Select hello container you created earlier (`azuresamldemoblob`).</span></span>
    * <span data-ttu-id="600f2-198">**Gebeurtenis serialisatie-indeling**.</span><span class="sxs-lookup"><span data-stu-id="600f2-198">**Event serialization format**.</span></span> <span data-ttu-id="600f2-199">Selecteer **CSV**.</span><span class="sxs-lookup"><span data-stu-id="600f2-199">Select **CSV**.</span></span>

    ![Instellingen voor nieuwe taak invoer](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-create-sa-input-new-portal.png)

4. <span data-ttu-id="600f2-201">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="600f2-201">Click **Create**.</span></span>

### <a name="configure-hello-job-output"></a><span data-ttu-id="600f2-202">Hallo taakuitvoer configureren</span><span class="sxs-lookup"><span data-stu-id="600f2-202">Configure hello job output</span></span>
<span data-ttu-id="600f2-203">Hallo taak verzendt resultaten toohello dezelfde blobopslag waar deze invoer opgehaald.</span><span class="sxs-lookup"><span data-stu-id="600f2-203">hello job sends results toohello same blob storage where it gets input.</span></span> 

1. <span data-ttu-id="600f2-204">Onder **taak topologie** Klik Hallo Hallo taakblade **uitvoer** vak.</span><span class="sxs-lookup"><span data-stu-id="600f2-204">Under **Job Topology** in hello job blade, click hello **Outputs** box.</span></span>  
  
   ![Nieuwe uitvoer voor Streaming Analytics-taak maken](./media/stream-analytics-machine-learning-integration-tutorial/create-output.png)  

2. <span data-ttu-id="600f2-206">In Hallo **uitvoer** blade, klikt u op **+ toevoegen**, en voeg vervolgens een uitvoer met de Hallo alias `datamloutput`.</span><span class="sxs-lookup"><span data-stu-id="600f2-206">In hello **Outputs** blade, click **+ Add**, and then add an output with hello alias `datamloutput`.</span></span> 

3. <span data-ttu-id="600f2-207">Voor **Sink**, selecteer **Blob storage**.</span><span class="sxs-lookup"><span data-stu-id="600f2-207">For **Sink**, select **Blob storage**.</span></span> <span data-ttu-id="600f2-208">Vult Hallo rest Hallo uitvoer instellingen met behulp van dezelfde waarden die u hebt gebruikt voor blob-opslag voor invoer Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="600f2-208">Then fill in hello rest of hello output settings using hello same values that you used for hello blob storage for input:</span></span>

    * <span data-ttu-id="600f2-209">**Storage-account**.</span><span class="sxs-lookup"><span data-stu-id="600f2-209">**Storage account**.</span></span> <span data-ttu-id="600f2-210">Selecteer Hallo-opslagaccount die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="600f2-210">Select hello storage account you created earlier.</span></span>
    * <span data-ttu-id="600f2-211">**Container**.</span><span class="sxs-lookup"><span data-stu-id="600f2-211">**Container**.</span></span> <span data-ttu-id="600f2-212">Selecteer Hallo-container die u eerder hebt gemaakt (`azuresamldemoblob`).</span><span class="sxs-lookup"><span data-stu-id="600f2-212">Select hello container you created earlier (`azuresamldemoblob`).</span></span>
    * <span data-ttu-id="600f2-213">**Gebeurtenis serialisatie-indeling**.</span><span class="sxs-lookup"><span data-stu-id="600f2-213">**Event serialization format**.</span></span> <span data-ttu-id="600f2-214">Selecteer **CSV**.</span><span class="sxs-lookup"><span data-stu-id="600f2-214">Select **CSV**.</span></span>

   ![Instellingen voor nieuwe taakuitvoer](./media/stream-analytics-machine-learning-integration-tutorial/create-output2.png) 

4. <span data-ttu-id="600f2-216">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="600f2-216">Click **Create**.</span></span>   


### <a name="add-hello-machine-learning-function"></a><span data-ttu-id="600f2-217">Hallo Machine Learning-functie toevoegen</span><span class="sxs-lookup"><span data-stu-id="600f2-217">Add hello Machine Learning function</span></span> 
<span data-ttu-id="600f2-218">U hebt gepubliceerd eerder een Machine Learning-model tooa-webservice.</span><span class="sxs-lookup"><span data-stu-id="600f2-218">Earlier you published a Machine Learning model tooa web service.</span></span> <span data-ttu-id="600f2-219">In ons scenario wanneer Hallo stroom Analysis taak wordt uitgevoerd, stuurt elke tweet voorbeeld van Hallo invoer toohello webservice voor gevoel analyse.</span><span class="sxs-lookup"><span data-stu-id="600f2-219">In our scenario, when hello Stream Analysis job runs, it sends each sample tweet from hello input toohello web service for sentiment analysis.</span></span> <span data-ttu-id="600f2-220">Hallo Machine Learning-webservice retourneert een gevoel (`positive`, `neutral`, of `negative`) en de kans op Hallo tweet wordt positief.</span><span class="sxs-lookup"><span data-stu-id="600f2-220">hello Machine Learning web service returns a sentiment (`positive`, `neutral`, or `negative`) and a probability of hello tweet being positive.</span></span> 

<span data-ttu-id="600f2-221">In deze sectie van de zelfstudie hello, moet u een functie in Hallo stroom Analysis taak definiëren.</span><span class="sxs-lookup"><span data-stu-id="600f2-221">In this section of hello tutorial, you define a function in hello Stream Analysis job.</span></span> <span data-ttu-id="600f2-222">Hallo-functie kan worden aangeroepen toosend een tweet toohello-webservice en terughalen antwoord Hallo.</span><span class="sxs-lookup"><span data-stu-id="600f2-222">hello function can be invoked toosend a tweet toohello web service and get hello response back.</span></span> 

1. <span data-ttu-id="600f2-223">Zorg ervoor dat u hebt Hallo web service-URL en API-sleutel die u eerder in de Excel-werkmap Hallo gedownload.</span><span class="sxs-lookup"><span data-stu-id="600f2-223">Make sure you have hello web service URL and API key that you downloaded earlier in hello Excel workbook.</span></span>

2. <span data-ttu-id="600f2-224">Overzichtsblade van toohello taak retourneren.</span><span class="sxs-lookup"><span data-stu-id="600f2-224">Return toohello job overview blade.</span></span>

3. <span data-ttu-id="600f2-225">Onder **instellingen**, selecteer **functies** en klik vervolgens op **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="600f2-225">Under **Settings**, select **Functions** and then click **+ Add**.</span></span>

   ![Een functie toohello Stream Analytics-taak niet toevoegen](./media/stream-analytics-machine-learning-integration-tutorial/create-function1.png) 

4. <span data-ttu-id="600f2-227">Voer `sentiment` functioneren alias als Hallo en geef overige Hallo Hallo-blade met deze waarden:</span><span class="sxs-lookup"><span data-stu-id="600f2-227">Enter `sentiment` as hello function alias and fill out hello rest of hello blade using these values:</span></span>

    * <span data-ttu-id="600f2-228">**Type functie**: Selecteer **Azure ML**.</span><span class="sxs-lookup"><span data-stu-id="600f2-228">**Function type**: Select **Azure ML**.</span></span>
    * <span data-ttu-id="600f2-229">**Optie importeren**: Selecteer **importeren uit een ander abonnement**.</span><span class="sxs-lookup"><span data-stu-id="600f2-229">**Import option**: Select **Import from a different subscription**.</span></span> <span data-ttu-id="600f2-230">Hiermee krijgt u een kans tooenter Hallo-URL en de sleutel.</span><span class="sxs-lookup"><span data-stu-id="600f2-230">This gives you a chance tooenter hello URL and key.</span></span>
    * <span data-ttu-id="600f2-231">**URL**: plakken in Hallo webservice-URL.</span><span class="sxs-lookup"><span data-stu-id="600f2-231">**URL**: Paste in hello web service URL.</span></span>
    * <span data-ttu-id="600f2-232">**Sleutel**: plakken in Hallo API-sleutel.</span><span class="sxs-lookup"><span data-stu-id="600f2-232">**Key**: Paste in hello API key.</span></span>
  
    ![Instellingen voor het toevoegen van een Machine Learning functie toohello Stream Analytics-taak](./media/stream-analytics-machine-learning-integration-tutorial/add-function.png)  
    
5. <span data-ttu-id="600f2-234">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="600f2-234">Click **Create**.</span></span>

### <a name="create-a-query-tootransform-hello-data"></a><span data-ttu-id="600f2-235">Maken van een query tootransform Hallo-gegevens</span><span class="sxs-lookup"><span data-stu-id="600f2-235">Create a query tootransform hello data</span></span>

<span data-ttu-id="600f2-236">Stream Analytics maakt gebruik van een declaratieve, op basis van SQL-query tooexamine Hallo-invoer en verwerkt.</span><span class="sxs-lookup"><span data-stu-id="600f2-236">Stream Analytics uses a declarative, SQL-based query tooexamine hello input and process it.</span></span> <span data-ttu-id="600f2-237">In deze sectie maakt maken u een query waarmee elke tweet uit invoer gelezen en roept vervolgens Hallo Machine Learning functie tooperform gevoel analysis.</span><span class="sxs-lookup"><span data-stu-id="600f2-237">In this section, you create a query that reads each tweet from input and then invokes hello Machine Learning function tooperform sentiment analysis.</span></span> <span data-ttu-id="600f2-238">Hallo-query verzendt vervolgens Hallo resultaat toohello uitvoer die u hebt gedefinieerd (blobopslag).</span><span class="sxs-lookup"><span data-stu-id="600f2-238">hello query then sends hello result toohello output that you defined (blob storage).</span></span>

1. <span data-ttu-id="600f2-239">Overzichtsblade van toohello taak retourneren.</span><span class="sxs-lookup"><span data-stu-id="600f2-239">Return toohello job overview blade.</span></span>

2.  <span data-ttu-id="600f2-240">Onder **taak topologie**, klikt u op Hallo **Query** vak.</span><span class="sxs-lookup"><span data-stu-id="600f2-240">Under **Job Topology**, click hello **Query** box.</span></span>

    ![Een query voor Streaming Analytics-taak maken](./media/stream-analytics-machine-learning-integration-tutorial/create-query.png)  

3. <span data-ttu-id="600f2-242">Voer Hallo query te volgen:</span><span class="sxs-lookup"><span data-stu-id="600f2-242">Enter hello following query:</span></span>

    ```
    WITH sentiment AS (  
    SELECT text, sentiment(text) as result from datainput  
    )  

    Select text, result.[Score]  
    Into datamloutput
    From sentiment  
    ```    

    <span data-ttu-id="600f2-243">Hallo query roept Hallo-functie die u eerder hebt gemaakt (`sentiment`) in volgorde tooperform gevoel analyse op elke tweet in Hallo-invoer.</span><span class="sxs-lookup"><span data-stu-id="600f2-243">hello query invokes hello function you created earlier (`sentiment`) in order tooperform sentiment analysis on each tweet in hello input.</span></span> 

4. <span data-ttu-id="600f2-244">Klik op **opslaan** toosave Hallo query.</span><span class="sxs-lookup"><span data-stu-id="600f2-244">Click **Save** toosave hello query.</span></span>


## <a name="start-hello-stream-analytics-job-and-check-hello-output"></a><span data-ttu-id="600f2-245">Hallo Stream Analytics-taak starten en controleer Hallo-uitvoer</span><span class="sxs-lookup"><span data-stu-id="600f2-245">Start hello Stream Analytics job and check hello output</span></span>

<span data-ttu-id="600f2-246">U kunt nu Hallo Stream Analytics-taak starten.</span><span class="sxs-lookup"><span data-stu-id="600f2-246">You can now start hello Stream Analytics job.</span></span>

### <a name="start-hello-job"></a><span data-ttu-id="600f2-247">Hallo taak starten</span><span class="sxs-lookup"><span data-stu-id="600f2-247">Start hello job</span></span>
1. <span data-ttu-id="600f2-248">Overzichtsblade van toohello taak retourneren.</span><span class="sxs-lookup"><span data-stu-id="600f2-248">Return toohello job overview blade.</span></span>

2. <span data-ttu-id="600f2-249">Klik op **Start** Hallo boven aan het Hallo-blade.</span><span class="sxs-lookup"><span data-stu-id="600f2-249">Click **Start** at hello top of hello blade.</span></span>

    ![Een query voor Streaming Analytics-taak maken](./media/stream-analytics-machine-learning-integration-tutorial/start-job.png)  

3. <span data-ttu-id="600f2-251">In Hallo **starttaak**, selecteer **aangepaste**, en selecteer vervolgens een dag van de voorafgaande toowhen Hallo CSV-bestand tooblob opslag die u hebt geüpload.</span><span class="sxs-lookup"><span data-stu-id="600f2-251">In hello **Start job**, select **Custom**, and then select one day prior toowhen you uploaded hello CSV file tooblob storage.</span></span> <span data-ttu-id="600f2-252">Wanneer u bent klaar, klikt u op **Start**.</span><span class="sxs-lookup"><span data-stu-id="600f2-252">When you're done, click **Start**.</span></span>  


### <a name="check-hello-output"></a><span data-ttu-id="600f2-253">Hallo uitvoer controleren</span><span class="sxs-lookup"><span data-stu-id="600f2-253">Check hello output</span></span>
1. <span data-ttu-id="600f2-254">Laat Hallo taak uitvoeren voor een paar minuten totdat er activiteit in Hallo **bewaking** vak.</span><span class="sxs-lookup"><span data-stu-id="600f2-254">Let hello job run for a few minutes until you see activity in hello **Monitoring** box.</span></span> 

2. <span data-ttu-id="600f2-255">Als u een hulpprogramma hebt dat u gewoonlijk tooexamine Hallo inhoud van de blob-opslag gebruikt, gebruiken die hulpprogramma tooexamine hello `azuresamldemoblob` container.</span><span class="sxs-lookup"><span data-stu-id="600f2-255">If you have a tool that you normally use tooexamine hello contents of blob storage, use that tool tooexamine hello `azuresamldemoblob` container.</span></span> <span data-ttu-id="600f2-256">U kunt ook Hallo stappen te volgen in hello Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="600f2-256">Alternatively, do hello following steps in hello Azure portal:</span></span>

    1. <span data-ttu-id="600f2-257">In de portal Hallo Hallo zoeken `samldemo` storage account en Hallo binnen Hallo-account zoeken `azuresamldemoblob` container.</span><span class="sxs-lookup"><span data-stu-id="600f2-257">In hello portal, find hello `samldemo` storage account, and within hello account, find hello `azuresamldemoblob` container.</span></span> <span data-ttu-id="600f2-258">Ziet u twee bestanden in de container Hallo: Hallo bestand Hallo voorbeeld tweets met en een CSV-bestand dat is gegenereerd door Hallo Stream Analytics-taak.</span><span class="sxs-lookup"><span data-stu-id="600f2-258">You see two files in hello container: hello file that contains hello sample tweets and a CSV file generated by hello Stream Analytics job.</span></span>
    2. <span data-ttu-id="600f2-259">Hallo gegenereerd bestand met de rechtermuisknop en selecteer vervolgens **downloaden**.</span><span class="sxs-lookup"><span data-stu-id="600f2-259">Right-click hello generated file and then select **Download**.</span></span> 

   ![CSV-taakuitvoer downloaden uit Blob-opslag](./media/stream-analytics-machine-learning-integration-tutorial/download-output-csv-file.png)  

3. <span data-ttu-id="600f2-261">Open Hallo gegenereerd CSV-bestand.</span><span class="sxs-lookup"><span data-stu-id="600f2-261">Open hello generated CSV file.</span></span> <span data-ttu-id="600f2-262">U ziet ongeveer Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="600f2-262">You see something like hello following example:</span></span>  
   
   ![Stream Analytics, Machine Learning, CSV weergeven](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-csv-view.png)  


### <a name="view-metrics"></a><span data-ttu-id="600f2-264">Metrische gegevens weergeven</span><span class="sxs-lookup"><span data-stu-id="600f2-264">View metrics</span></span>
<span data-ttu-id="600f2-265">U kunt ook Azure Machine Learning functie-gerelateerde metrische gegevens weergeven.</span><span class="sxs-lookup"><span data-stu-id="600f2-265">You also can view Azure Machine Learning function-related metrics.</span></span> <span data-ttu-id="600f2-266">Hallo volgende functie-gerelateerde metrische gegevens worden weergegeven in Hallo **bewaking** vak in de blade taak Hallo:</span><span class="sxs-lookup"><span data-stu-id="600f2-266">hello following function-related metrics are displayed in hello **Monitoring** box in hello job blade:</span></span>

* <span data-ttu-id="600f2-267">**Functie aanvragen** geeft het aantal aanvragen dat is verzonden tooa Machine Learning-webservice Hallo.</span><span class="sxs-lookup"><span data-stu-id="600f2-267">**Function Requests** indicates hello number of requests sent tooa Machine Learning web service.</span></span>  
* <span data-ttu-id="600f2-268">**Gebeurtenissen werken** geeft het aantal gebeurtenissen in de aanvraag Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="600f2-268">**Function Events** indicates hello number of events in hello request.</span></span> <span data-ttu-id="600f2-269">Standaard bevat elke aanvraag tooa Machine Learning-webservice up too1, 000 gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="600f2-269">By default, each request tooa Machine Learning web service contains up too1,000 events.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="600f2-270">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="600f2-270">Next steps</span></span>

* [<span data-ttu-id="600f2-271">Inleiding tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="600f2-271">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="600f2-272">Naslaggids voor Azure Stream Analytics Query</span><span class="sxs-lookup"><span data-stu-id="600f2-272">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="600f2-273">REST-API integreren en Machine Learning</span><span class="sxs-lookup"><span data-stu-id="600f2-273">Integrate REST API and Machine Learning</span></span>](stream-analytics-how-to-configure-azure-machine-learning-endpoints-in-stream-analytics.md)
* [<span data-ttu-id="600f2-274">REST API-naslaggids voor Azure Stream Analytics Management</span><span class="sxs-lookup"><span data-stu-id="600f2-274">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)



