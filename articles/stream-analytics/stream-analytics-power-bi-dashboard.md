---
title: aaaPower BI-dashboard op Azure Stream Analytics | Microsoft Docs
description: Gebruik een realtime streaming Power BI-dashboard toogather business intelligence en analyseren van grote hoeveelheden gegevens uit een Stream Analytics-taak.
keywords: dashboard met analytische, realtime dashboard
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: fe8db732-4397-4e58-9313-fec9537aa2ad
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: jeffstok
ms.openlocfilehash: cb9127576230e9d327b437b674f31cc23869bfff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-and-power-bi-a-real-time-analytics-dashboard-for-streaming-data"></a><span data-ttu-id="cc91d-104">Stream Analytics en Power BI: een realtime analytics-dashboard voor het streamen van gegevens</span><span class="sxs-lookup"><span data-stu-id="cc91d-104">Stream Analytics and Power BI: A real-time analytics dashboard for streaming data</span></span>
<span data-ttu-id="cc91d-105">Azure Stream Analytics kunt u profiteren van een van de hulpprogramma's voor bedrijfsinformatie, voorloopspaties Hallo tootake [Microsoft Power BI](https://powerbi.com/).</span><span class="sxs-lookup"><span data-stu-id="cc91d-105">Azure Stream Analytics enables you tootake advantage of one of hello leading business intelligence tools, [Microsoft Power BI](https://powerbi.com/).</span></span> <span data-ttu-id="cc91d-106">In dit artikel leert u hoe hulpprogramma's voor bedrijfsinformatie te maken met behulp van Power BI als uitvoer voor uw Azure Stream Analytics-taken.</span><span class="sxs-lookup"><span data-stu-id="cc91d-106">In this article, you learn how create business intelligence tools by using Power BI as an output for your Azure Stream Analytics jobs.</span></span> <span data-ttu-id="cc91d-107">U leert ook hoe toocreate en gebruiken van een realtime dashboard.</span><span class="sxs-lookup"><span data-stu-id="cc91d-107">You also learn how toocreate and use a real-time dashboard.</span></span>

<span data-ttu-id="cc91d-108">In dit artikel wordt voortgezet vanaf Hallo Stream Analytics [realtime-fraudedetectie](stream-analytics-real-time-fraud-detection.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="cc91d-108">This article continues from hello Stream Analytics [real-time fraud detection](stream-analytics-real-time-fraud-detection.md) tutorial.</span></span> <span data-ttu-id="cc91d-109">Het is gebaseerd op Hallo-werkstroom gemaakt in deze zelfstudie en voegt een Power BI zodat u kunt visualiseren frauduleuze telefoongesprekken die zijn gedetecteerd door een Streaming Analytics-taak uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="cc91d-109">It builds on hello workflow created in that tutorial and adds a Power BI output so that you can visualize fraudulent phone calls that are detected by a Streaming Analytics job.</span></span> 

<span data-ttu-id="cc91d-110">U kunt bekijken [video](https://www.youtube.com/watch?v=SGUpT-a99MA) die dit scenario laat zien.</span><span class="sxs-lookup"><span data-stu-id="cc91d-110">You can watch [a video](https://www.youtube.com/watch?v=SGUpT-a99MA)  that illustrates this scenario.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="cc91d-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="cc91d-111">Prerequisites</span></span>

<span data-ttu-id="cc91d-112">Zorg voordat u begint, hebt u de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="cc91d-112">Before you start, make sure you have hello following:</span></span>

* <span data-ttu-id="cc91d-113">Een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="cc91d-113">An Azure account.</span></span>
* <span data-ttu-id="cc91d-114">Een account voor Power BI.</span><span class="sxs-lookup"><span data-stu-id="cc91d-114">An account for Power BI.</span></span> <span data-ttu-id="cc91d-115">U kunt een werk- of een schoolaccount gebruiken.</span><span class="sxs-lookup"><span data-stu-id="cc91d-115">You can use a work account or a school account.</span></span>
* <span data-ttu-id="cc91d-116">Een voltooide versie van Hallo [realtime-fraudedetectie](stream-analytics-real-time-fraud-detection.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="cc91d-116">A completed version of hello [real-time fraud detection](stream-analytics-real-time-fraud-detection.md) tutorial.</span></span> <span data-ttu-id="cc91d-117">Hallo-zelfstudie omvat een app die fictieve telefoongesprek metagegevens genereert.</span><span class="sxs-lookup"><span data-stu-id="cc91d-117">hello tutorial includes an app that generates fictitious telephone-call metadata.</span></span> <span data-ttu-id="cc91d-118">In de zelfstudie hello, een event hub maken en verzenden Hallo streaming telefoongesprek gegevens toohello event hub.</span><span class="sxs-lookup"><span data-stu-id="cc91d-118">In hello tutorial, you create an event hub and send hello streaming phone call data toohello event hub.</span></span> <span data-ttu-id="cc91d-119">U een query schrijven waarmee frauduleuze aanroepen detecteert (aanroepen vanuit dezelfde number op Hallo Hallo dezelfde periode in verschillende locaties).</span><span class="sxs-lookup"><span data-stu-id="cc91d-119">You write a query that detects fraudulent calls (calls from hello same number at hello same time in different locations).</span></span> 


## <a name="add-power-bi-output"></a><span data-ttu-id="cc91d-120">Power BI-uitvoer toevoegen</span><span class="sxs-lookup"><span data-stu-id="cc91d-120">Add Power BI output</span></span>
<span data-ttu-id="cc91d-121">In Hallo realtime fraude detectie zelfstudie Hallo uitvoer tooAzure blobopslag verzonden.</span><span class="sxs-lookup"><span data-stu-id="cc91d-121">In hello real-time fraud detection tutorial, hello output is sent tooAzure Blob storage.</span></span> <span data-ttu-id="cc91d-122">In deze sectie voegt u een uitvoer die informatie tooPower BI verzendt.</span><span class="sxs-lookup"><span data-stu-id="cc91d-122">In this section, you add an output that sends information tooPower BI.</span></span>

1. <span data-ttu-id="cc91d-123">Open in hello Azure-portal, Hallo Streaming Analytics-taak die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="cc91d-123">In hello Azure portal, open hello Streaming Analytics job that you created earlier.</span></span> <span data-ttu-id="cc91d-124">Als u de voorgestelde naam Hallo gebruikt, Hallo taak heet `sa_frauddetection_job_demo`.</span><span class="sxs-lookup"><span data-stu-id="cc91d-124">If you used hello suggested name, hello job is named `sa_frauddetection_job_demo`.</span></span>

2. <span data-ttu-id="cc91d-125">Selecteer Hallo **uitvoer** in het midden van Hallo taak dashboard Hallo vak en selecteer vervolgens **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="cc91d-125">Select hello **Outputs** box in hello middle of hello job dashboard and then select **+ Add**.</span></span>

3. <span data-ttu-id="cc91d-126">Voor **Uitvoeraliassen**, voer `CallStream-PowerBI`.</span><span class="sxs-lookup"><span data-stu-id="cc91d-126">For **Output Alias**, enter `CallStream-PowerBI`.</span></span> <span data-ttu-id="cc91d-127">U kunt een andere naam gebruiken.</span><span class="sxs-lookup"><span data-stu-id="cc91d-127">You can use a different name.</span></span> <span data-ttu-id="cc91d-128">Als u dit doet, noteer, omdat u de naam van de hello later nodig.</span><span class="sxs-lookup"><span data-stu-id="cc91d-128">If you do, make a note of it, because you need hello name later.</span></span> 

4. <span data-ttu-id="cc91d-129">Onder **Sink**, selecteer **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="cc91d-129">Under **Sink**, select **Power BI**.</span></span>

   ![Maken van een uitvoer voor Power BI](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut.png)

5. <span data-ttu-id="cc91d-131">Klik op **autoriseren**.</span><span class="sxs-lookup"><span data-stu-id="cc91d-131">Click **Authorize**.</span></span>

    <span data-ttu-id="cc91d-132">Een venster wordt geopend waarin u uw Azure-referenties voor een werk- of schoolaccount account kunt opgeven.</span><span class="sxs-lookup"><span data-stu-id="cc91d-132">A window opens where you can provide your Azure credentials for a work or school account.</span></span> 

    ![Geef referenties voor toegang tot tooPower BI](./media/stream-analytics-power-bi-dashboard/authorize-area.png)

6. <span data-ttu-id="cc91d-134">Geef uw referenties.</span><span class="sxs-lookup"><span data-stu-id="cc91d-134">Enter your credentials.</span></span> <span data-ttu-id="cc91d-135">Let en wanneer u uw referenties invoeren, geeft u bent ook beschermd machtiging toohello Streaming Analytics-taak tooaccess uw Power BI-gebied.</span><span class="sxs-lookup"><span data-stu-id="cc91d-135">Be aware then when you enter your credentials, you're also giving permission toohello Streaming Analytics job tooaccess your Power BI area.</span></span>

7. <span data-ttu-id="cc91d-136">Wanneer u wordt teruggeleid toohello **nieuwe uitvoer** blade Voer Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="cc91d-136">When you're returned toohello **New output** blade, enter hello following information:</span></span>

    * <span data-ttu-id="cc91d-137">**Werkruimte groep**: Selecteer een werkruimte in uw Power BI-tenant waar u toocreate Hallo gegevensset.</span><span class="sxs-lookup"><span data-stu-id="cc91d-137">**Group Workspace**: Select a workspace in your Power BI tenant where you want toocreate hello dataset.</span></span>
    * <span data-ttu-id="cc91d-138">**Naam van DataSet**: Voer `sa-dataset`.</span><span class="sxs-lookup"><span data-stu-id="cc91d-138">**Dataset Name**:  Enter `sa-dataset`.</span></span> <span data-ttu-id="cc91d-139">U kunt een andere naam gebruiken.</span><span class="sxs-lookup"><span data-stu-id="cc91d-139">You can use a different name.</span></span> <span data-ttu-id="cc91d-140">Als u dit doet, noteer deze later.</span><span class="sxs-lookup"><span data-stu-id="cc91d-140">If you do, make a note of it for later.</span></span>
    * <span data-ttu-id="cc91d-141">**Tabelnaam**: Voer `fraudulent-calls`.</span><span class="sxs-lookup"><span data-stu-id="cc91d-141">**Table Name**: Enter `fraudulent-calls`.</span></span> <span data-ttu-id="cc91d-142">Power BI-uitvoer van de Stream Analytics-taken zijn op dit moment slechts één tabel in een dataset.</span><span class="sxs-lookup"><span data-stu-id="cc91d-142">Currently, Power BI output from Stream Analytics jobs can have only one table in a dataset.</span></span>

    ![PBI-werkruimte](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut-with-dataset-table.png)

    > [!WARNING]
    > <span data-ttu-id="cc91d-144">Als Power BI een gegevensset heeft en tabel met dezelfde naam als Hallo Hallo die u opgeeft in de Stream Analytics-taak hello, worden bestaande toepassingsgroepen hallo overschreven.</span><span class="sxs-lookup"><span data-stu-id="cc91d-144">If Power BI has a dataset and table that have hello same names as hello ones that you specify in hello Stream Analytics job, hello existing ones are overwritten.</span></span>
    > <span data-ttu-id="cc91d-145">U wordt aangeraden dat u niet expliciet deze gegevensset en de tabel in uw Power BI-account maakt.</span><span class="sxs-lookup"><span data-stu-id="cc91d-145">We recommend that you do not explicitly create this dataset and table in your Power BI account.</span></span> <span data-ttu-id="cc91d-146">Ze worden automatisch gemaakt wanneer u uw Stream Analytics-taak start en Hallo taak gemalen uitvoer naar Power BI begint.</span><span class="sxs-lookup"><span data-stu-id="cc91d-146">They are automatically created when you start your Stream Analytics job and hello job starts pumping output into Power BI.</span></span> <span data-ttu-id="cc91d-147">Als de taak query geen resultaten oplevert, Hallo gegevensset en de tabel niet gemaakt.</span><span class="sxs-lookup"><span data-stu-id="cc91d-147">If your job query doesn't return any results, hello dataset and table are not  created.</span></span>
    >

8. <span data-ttu-id="cc91d-148">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="cc91d-148">Click **Create**.</span></span>

<span data-ttu-id="cc91d-149">Hallo gegevensset is gemaakt met Hallo volgende instellingen:</span><span class="sxs-lookup"><span data-stu-id="cc91d-149">hello dataset is created with hello following settings:</span></span>

* <span data-ttu-id="cc91d-150">**defaultRetentionPolicy: BasicFIFO**: gegevens zijn FIFO, met een maximum van 200.000 rijen.</span><span class="sxs-lookup"><span data-stu-id="cc91d-150">**defaultRetentionPolicy: BasicFIFO**: Data is FIFO, with a maximum of 200,000 rows.</span></span>
* <span data-ttu-id="cc91d-151">**defaultMode: pushStreaming**: Hallo dataset ondersteunt streaming tegels en traditionele op basis van een rapport visuele elementen (ook</span><span class="sxs-lookup"><span data-stu-id="cc91d-151">**defaultMode: pushStreaming**: hello dataset supports both streaming tiles and traditional report-based visuals (a.k.a.</span></span> <span data-ttu-id="cc91d-152">push).</span><span class="sxs-lookup"><span data-stu-id="cc91d-152">push).</span></span>

<span data-ttu-id="cc91d-153">U kunt op dit moment gegevenssets maken met andere vlaggen.</span><span class="sxs-lookup"><span data-stu-id="cc91d-153">Currently, you can't create datasets with other flags.</span></span>

<span data-ttu-id="cc91d-154">Zie voor meer informatie over Power BI-gegevenssets Hallo [Power BI REST-API](https://msdn.microsoft.com/library/mt203562.aspx) verwijzing.</span><span class="sxs-lookup"><span data-stu-id="cc91d-154">For more information about Power BI datasets, see hello [Power BI REST API](https://msdn.microsoft.com/library/mt203562.aspx) reference.</span></span>


## <a name="write-hello-query"></a><span data-ttu-id="cc91d-155">Hallo-query schrijven</span><span class="sxs-lookup"><span data-stu-id="cc91d-155">Write hello query</span></span>

1. <span data-ttu-id="cc91d-156">Sluit Hallo **uitvoer** blade en return toohello taakblade.</span><span class="sxs-lookup"><span data-stu-id="cc91d-156">Close hello **Outputs** blade and return toohello job blade.</span></span>

2. <span data-ttu-id="cc91d-157">Klik op Hallo **Query** vak.</span><span class="sxs-lookup"><span data-stu-id="cc91d-157">Click hello **Query** box.</span></span> 

3. <span data-ttu-id="cc91d-158">Voer Hallo query te volgen.</span><span class="sxs-lookup"><span data-stu-id="cc91d-158">Enter hello following query.</span></span> <span data-ttu-id="cc91d-159">Deze query is vergelijkbaar toohello zelf join-query die u in Hallo fraudedetectie zelfstudie hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="cc91d-159">This query is similar toohello self-join query you created in hello fraud-detection tutorial.</span></span> <span data-ttu-id="cc91d-160">Hallo verschil is dat deze query verzendt resultaten toohello nieuwe uitvoer u hebt gemaakt (`CallStream-PowerBI`).</span><span class="sxs-lookup"><span data-stu-id="cc91d-160">hello difference is that this query sends results toohello new output you created (`CallStream-PowerBI`).</span></span> 

    >[!NOTE]
    ><span data-ttu-id="cc91d-161">Als u hebt niet de naam Hallo invoer `CallStream` vervangen door uw naam in de zelfstudie voor het detecteren van fraude van Hallo `CallStream` in Hallo **FROM** en **JOIN** componenten in Hallo-query.</span><span class="sxs-lookup"><span data-stu-id="cc91d-161">If you did not name hello input `CallStream` in hello fraud-detection tutorial, substitute your name for `CallStream` in hello **FROM** and **JOIN** clauses in hello query.</span></span>

        /* Our criteria for fraud:
        Calls made from hello same caller tootwo phone switches in different locations (for example, Australia and Europe) within five seconds */

        SELECT System.Timestamp AS WindowEnd, COUNT(*) AS FraudulentCalls
        INTO "CallStream-PowerBI"
        FROM "CallStream" CS1 TIMESTAMP BY CallRecTime
        JOIN "CallStream" CS2 TIMESTAMP BY CallRecTime

        /* Where hello caller is hello same, as indicated by IMSI (International Mobile Subscriber Identity) */
        ON CS1.CallingIMSI = CS2.CallingIMSI

        /* ...and date between CS1 and CS2 is between one and five seconds */
        AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5

        /* Where hello switch location is different */
        WHERE CS1.SwitchNum != CS2.SwitchNum
        GROUP BY TumblingWindow(Duration(second, 1))

4. <span data-ttu-id="cc91d-162">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="cc91d-162">Click **Save**.</span></span>


## <a name="test-hello-query"></a><span data-ttu-id="cc91d-163">Hallo-testquery</span><span class="sxs-lookup"><span data-stu-id="cc91d-163">Test hello query</span></span>
<span data-ttu-id="cc91d-164">Deze sectie is optioneel maar aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="cc91d-164">This section is optional, but recommended.</span></span> 

1. <span data-ttu-id="cc91d-165">Als Hallo TelcoStreaming app niet wordt uitgevoerd, start u deze met de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="cc91d-165">If hello TelcoStreaming app is not currently running, start it by following these steps:</span></span>

    * <span data-ttu-id="cc91d-166">Open een opdrachtvenster.</span><span class="sxs-lookup"><span data-stu-id="cc91d-166">Open a command window.</span></span>
    * <span data-ttu-id="cc91d-167">Ga toohello map waarin Hallo telcogenerator.exe en telcodatagen.exe.config gewijzigde bestanden zijn.</span><span class="sxs-lookup"><span data-stu-id="cc91d-167">Go toohello folder where hello telcogenerator.exe and modified telcodatagen.exe.config files are.</span></span>
    * <span data-ttu-id="cc91d-168">Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="cc91d-168">Run hello following command:</span></span>

            telcodatagen.exe 1000 .2 2

2. <span data-ttu-id="cc91d-169">In Hallo **Query** blade, klikt u op Hallo punten volgende toohello `CallStream` invoer- en selecteer vervolgens **voorbeeldgegevens uit de invoer**.</span><span class="sxs-lookup"><span data-stu-id="cc91d-169">In hello **Query** blade, click hello dots next toohello `CallStream` input and then select **Sample data from input**.</span></span>

3. <span data-ttu-id="cc91d-170">U wilt opgeven dat drie minuten aan gegevens en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="cc91d-170">Specify that you want three minutes' worth of data and click **OK**.</span></span> <span data-ttu-id="cc91d-171">Wacht totdat u een bericht dat Hallo gegevens steekproefgewijs verkregen.</span><span class="sxs-lookup"><span data-stu-id="cc91d-171">Wait until you're notified that hello data has been sampled.</span></span>

4. <span data-ttu-id="cc91d-172">Klik op **Test** en zorg ervoor dat u resultaten krijgt.</span><span class="sxs-lookup"><span data-stu-id="cc91d-172">Click **Test** and make sure you're getting results.</span></span>


## <a name="run-hello-job"></a><span data-ttu-id="cc91d-173">Hallo-taak uitvoeren</span><span class="sxs-lookup"><span data-stu-id="cc91d-173">Run hello job</span></span>

1. <span data-ttu-id="cc91d-174">Zorg ervoor dat Hallo TelcoStreaming app wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="cc91d-174">Make sure that hello TelcoStreaming app is running.</span></span>

2. <span data-ttu-id="cc91d-175">Sluit Hallo **Query** blade.</span><span class="sxs-lookup"><span data-stu-id="cc91d-175">Close hello **Query** blade.</span></span>

3. <span data-ttu-id="cc91d-176">Klik op Hallo taakblade **Start**.</span><span class="sxs-lookup"><span data-stu-id="cc91d-176">In hello job blade, click **Start**.</span></span>

    ![Hallo Stream Analytics-taak starten](./media/stream-analytics-power-bi-dashboard/stream-analytics-sa-job-start-output.png)

<span data-ttu-id="cc91d-178">Uw Streaming Analytics-taak wordt gestart frauduleuze aanroepen in de stroom voor inkomende hello zoekt.</span><span class="sxs-lookup"><span data-stu-id="cc91d-178">Your Streaming Analytics job starts looking for fraudulent calls in hello incoming stream.</span></span> <span data-ttu-id="cc91d-179">Hallo taak ook Hallo gegevensset en de tabel in Power BI maakt en begint met het verzenden van gegevens over Hallo frauduleuze aanroepen toothem.</span><span class="sxs-lookup"><span data-stu-id="cc91d-179">hello job also creates hello dataset and table in Power BI and starts sending data about hello fraudulent calls toothem.</span></span>


## <a name="create-hello-dashboard-in-power-bi"></a><span data-ttu-id="cc91d-180">Hallo-dashboard maken in Power BI</span><span class="sxs-lookup"><span data-stu-id="cc91d-180">Create hello dashboard in Power BI</span></span>

1. <span data-ttu-id="cc91d-181">Ga te[Powerbi.com](https://powerbi.com) en meld u aan met uw werk of school-account.</span><span class="sxs-lookup"><span data-stu-id="cc91d-181">Go too[Powerbi.com](https://powerbi.com) and sign in with your work or school account.</span></span> <span data-ttu-id="cc91d-182">Als Hallo Stream Analytics-taak query worden de resultaten, ziet u dat uw gegevensset al is gemaakt:</span><span class="sxs-lookup"><span data-stu-id="cc91d-182">If hello Stream Analytics job query outputs results, you see that your dataset is already created:</span></span>

    ![Streaming gegevensset in Power BI](./media/stream-analytics-power-bi-dashboard/streaming-dataset.png)

2. <span data-ttu-id="cc91d-184">Klik in de werkruimte op  **+ &nbsp;maken**.</span><span class="sxs-lookup"><span data-stu-id="cc91d-184">In your workspace, click **+&nbsp;Create**.</span></span>

    ![Hallo-knop maken klikt in Power BI-werkruimte](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard.png)

3. <span data-ttu-id="cc91d-186">Maak een nieuw dashboard en noem deze `Fraudulent Calls`.</span><span class="sxs-lookup"><span data-stu-id="cc91d-186">Create a new dashboard and name it `Fraudulent Calls`.</span></span>

    ![Een dashboard maken en hieraan een naam in Power BI-werkruimte](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard-name.png)

4. <span data-ttu-id="cc91d-188">Bovenaan Hallo Hallo-venster, klikt u op **toevoegen tegel**, selecteer **aangepaste STREAMINGGEGEVENS**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="cc91d-188">At hello top of hello window, click **Add tile**, select **CUSTOM STREAMING DATA**, and then click **Next**.</span></span>

    ![Aangepaste gegevensset streaming](./media/stream-analytics-power-bi-dashboard/custom-streaming-data.png)

5. <span data-ttu-id="cc91d-190">Onder **uw DATSETS**, selecteer uw gegevensset en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="cc91d-190">Under **YOUR DATSETS**, select your dataset and then click **Next**.</span></span>

    ![Uw streaminggegevensset](./media/stream-analytics-power-bi-dashboard/your-streaming-dataset.png)

6. <span data-ttu-id="cc91d-192">Onder **visualisatie Type**, selecteer **kaart**, en klik vervolgens in Hallo **velden** selecteert **fraudulentcalls**.</span><span class="sxs-lookup"><span data-stu-id="cc91d-192">Under **Visualization Type**, select **Card**, and then in hello **Fields** list, select **fraudulentcalls**.</span></span>

    ![Details van de visualisatie voor nieuwe tegel](./media/stream-analytics-power-bi-dashboard/add-fraud.png)

7. <span data-ttu-id="cc91d-194">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="cc91d-194">Click **Next**.</span></span>

8. <span data-ttu-id="cc91d-195">Vul in de tegel-gegevens, zoals een titel en subtitel.</span><span class="sxs-lookup"><span data-stu-id="cc91d-195">Fill in tile details like a title and subtitle.</span></span>

    ![Titel en subtitel voor nieuwe tegel](./media/stream-analytics-power-bi-dashboard/pbi-new-tile-details.png)

9. <span data-ttu-id="cc91d-197">Klik op **Toepassen**.</span><span class="sxs-lookup"><span data-stu-id="cc91d-197">Click **Apply**.</span></span>

    <span data-ttu-id="cc91d-198">U hebt nu een teller fraude.</span><span class="sxs-lookup"><span data-stu-id="cc91d-198">Now you have a fraud counter!</span></span>

    ![Fraude teller](./media/stream-analytics-power-bi-dashboard/fraud-counter.png)

8. <span data-ttu-id="cc91d-200">Volg Hallo stappen opnieuw tooadd een tegel (te beginnen bij stap 4).</span><span class="sxs-lookup"><span data-stu-id="cc91d-200">Follow hello steps again tooadd a tile (starting with step 4).</span></span> <span data-ttu-id="cc91d-201">Deze tijd Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="cc91d-201">This time, do hello following:</span></span>

    * <span data-ttu-id="cc91d-202">Als u krijgt te**visualisatie Type**, selecteer **lijndiagram**.</span><span class="sxs-lookup"><span data-stu-id="cc91d-202">When you get too**Visualization Type**, select **Line chart**.</span></span> 
    * <span data-ttu-id="cc91d-203">Een as toevoegen en selecteer **windowend**.</span><span class="sxs-lookup"><span data-stu-id="cc91d-203">Add an axis and select **windowend**.</span></span> 
    * <span data-ttu-id="cc91d-204">Een waarde toevoegen en selecteer **fraudulentcalls**.</span><span class="sxs-lookup"><span data-stu-id="cc91d-204">Add a value and select **fraudulentcalls**.</span></span>
    * <span data-ttu-id="cc91d-205">Voor **tijd venster toodisplay**, selecteer Hallo van afgelopen 10 minuten.</span><span class="sxs-lookup"><span data-stu-id="cc91d-205">For **Time window toodisplay**, select hello last 10 minutes.</span></span>

    ![Tegel lijndiagram maken](./media/stream-analytics-power-bi-dashboard/pbi-create-tile-line-chart.png)

9. <span data-ttu-id="cc91d-207">Klik op **volgende**, het toevoegen van een titel en subtitel en klikt u op **toepassen**.</span><span class="sxs-lookup"><span data-stu-id="cc91d-207">Click **Next**, add a title and subtitle, and click **Apply**.</span></span>

    <span data-ttu-id="cc91d-208">Hallo Power BI-dashboard kunt u nu twee weergaven van gegevens over frauduleuze aanroepen als gedetecteerd in Hallo gegevensstromen.</span><span class="sxs-lookup"><span data-stu-id="cc91d-208">hello Power BI dashboard now gives you two views of data about fraudulent calls as detected in hello streaming data.</span></span>

    ![Klaar met Power BI-dashboard met twee tegels voor frauduleuze aanroepen](./media/stream-analytics-power-bi-dashboard/pbi-dashboard-fraudulent-calls-finished.png)


## <a name="learn-more-about-power-bi"></a><span data-ttu-id="cc91d-210">Meer informatie over Power BI</span><span class="sxs-lookup"><span data-stu-id="cc91d-210">Learn more about Power BI</span></span>

<span data-ttu-id="cc91d-211">Deze zelfstudie laat zien hoe toocreate alleen enkele soorten visualisaties voor een dataset.</span><span class="sxs-lookup"><span data-stu-id="cc91d-211">This tutorial demonstrates how toocreate only a few kinds of visualizations for a dataset.</span></span> <span data-ttu-id="cc91d-212">Power BI kunt u andere klant hulpprogramma's voor bedrijfsinformatie voor uw organisatie te maken.</span><span class="sxs-lookup"><span data-stu-id="cc91d-212">Power BI can help you create other customer business intelligence tools for your organization.</span></span> <span data-ttu-id="cc91d-213">Zie voor meer ideeën Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="cc91d-213">For more ideas, see hello following resources:</span></span>

* <span data-ttu-id="cc91d-214">Voor een ander voorbeeld van een Power BI-dashboard bekijkt hello [aan de slag met Power BI](https://youtu.be/L-Z_6P56aas?t=1m58s) video.</span><span class="sxs-lookup"><span data-stu-id="cc91d-214">For another example of a Power BI dashboard, watch hello [Getting Started with Power BI](https://youtu.be/L-Z_6P56aas?t=1m58s) video.</span></span>
* <span data-ttu-id="cc91d-215">Taak voor meer informatie over het configureren van Streaming Analytics uitvoer tooPower BI en u Power BI-groepen bekijken Hallo [Power BI](stream-analytics-define-outputs.md#power-bi) sectie Hallo [Stream Analytics levert](stream-analytics-define-outputs.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="cc91d-215">For more information about configuring Streaming Analytics job output tooPower BI and using Power BI groups, review hello [Power BI](stream-analytics-define-outputs.md#power-bi) section of hello [Stream Analytics outputs](stream-analytics-define-outputs.md) article.</span></span> 
* <span data-ttu-id="cc91d-216">Zie voor meer informatie over het gebruik van Power BI in het algemeen [Dashboards in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/).</span><span class="sxs-lookup"><span data-stu-id="cc91d-216">For information about using Power BI generally, see [Dashboards in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/).</span></span>


## <a name="learn-about-limitations-and-best-practices"></a><span data-ttu-id="cc91d-217">Meer informatie over de beperkingen en best practices</span><span class="sxs-lookup"><span data-stu-id="cc91d-217">Learn about limitations and best practices</span></span>
<span data-ttu-id="cc91d-218">Op dit moment kunnen Power BI ongeveer één keer per seconde worden aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="cc91d-218">Currently, Power BI can be called roughly once per second.</span></span> <span data-ttu-id="cc91d-219">Streaming visuele elementen ondersteuning bieden voor pakketten van 15 KB.</span><span class="sxs-lookup"><span data-stu-id="cc91d-219">Streaming visuals support packets of 15 KB.</span></span> <span data-ttu-id="cc91d-220">Daarna streaming visuele elementen mislukken (maar push blijft toowork).</span><span class="sxs-lookup"><span data-stu-id="cc91d-220">Beyond that, streaming visuals fail (but push continues toowork).</span></span> <span data-ttu-id="cc91d-221">Vanwege deze beperkingen Power BI gepaard meest natuurlijk toocases waar Azure Stream Analytics een aanzienlijke hoeveelheid gegevens laden beperken biedt.</span><span class="sxs-lookup"><span data-stu-id="cc91d-221">Because of these limitations, Power BI lends itself most naturally toocases where Azure Stream Analytics does a significant data load reduction.</span></span> <span data-ttu-id="cc91d-222">U wordt aangeraden een tumblingvenster of Hopping venster tooensure gegevens-push is maximaal één push per seconde is en of uw query belandt binnen Hallo doorvoer vereisten.</span><span class="sxs-lookup"><span data-stu-id="cc91d-222">We recommend using a Tumbling window or Hopping window tooensure that data push is at most one push per second, and that your query lands within hello throughput requirements.</span></span>

<span data-ttu-id="cc91d-223">Kunt u Hallo vergelijking toocompute Hallo waarde toogive na het venster (in seconden):</span><span class="sxs-lookup"><span data-stu-id="cc91d-223">You can use hello following equation toocompute hello value toogive your window in seconds:</span></span>

![Equation1](./media/stream-analytics-power-bi-dashboard/equation1.png)  

<span data-ttu-id="cc91d-225">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="cc91d-225">For example:</span></span>

* <span data-ttu-id="cc91d-226">U hebt 1000 apparaten verzenden van gegevens met een interval van één seconde.</span><span class="sxs-lookup"><span data-stu-id="cc91d-226">You have 1,000 devices sending data at one-second intervals.</span></span>
* <span data-ttu-id="cc91d-227">U gebruikt Hallo Power BI Pro SKU die ondersteuning biedt voor 1.000.000 rijen per uur.</span><span class="sxs-lookup"><span data-stu-id="cc91d-227">You are using hello Power BI Pro SKU that supports 1,000,000 rows per hour.</span></span>
* <span data-ttu-id="cc91d-228">Wilt u toopublish Hallo hoeveelheid gemiddelde gegevens per apparaat tooPower BI.</span><span class="sxs-lookup"><span data-stu-id="cc91d-228">You want toopublish hello amount of average data per device tooPower BI.</span></span>

<span data-ttu-id="cc91d-229">Als gevolg hiervan wordt het Hallo vergelijking:</span><span class="sxs-lookup"><span data-stu-id="cc91d-229">As a result, hello equation becomes:</span></span>

![Equation2](./media/stream-analytics-power-bi-dashboard/equation2.png)  

<span data-ttu-id="cc91d-231">In deze configuratie kunt u Hallo oorspronkelijke query toohello volgende wijzigen:</span><span class="sxs-lookup"><span data-stu-id="cc91d-231">Given this configuration, you can change hello original query toohello following:</span></span>

    SELECT
        MAX(hmdt) AS hmdt,
        MAX(temp) AS temp,
        System.TimeStamp AS time,
        dspl
    INTO "CallStream-PowerBI"
    FROM
        Input TIMESTAMP BY time
    GROUP BY
        TUMBLINGWINDOW(ss,4),
        dspl


### <a name="renew-authorization"></a><span data-ttu-id="cc91d-232">Verificatie vernieuwen</span><span class="sxs-lookup"><span data-stu-id="cc91d-232">Renew authorization</span></span>
<span data-ttu-id="cc91d-233">Als het Hallo-wachtwoord is gewijzigd sinds de taak is gemaakt of laatst geverifieerd, moet u tooreauthenticate uw Power BI-account.</span><span class="sxs-lookup"><span data-stu-id="cc91d-233">If hello password has changed since your job was created or last authenticated, you need tooreauthenticate your Power BI account.</span></span> <span data-ttu-id="cc91d-234">Als Azure multi-factor Authentication is geconfigureerd op de tenant van uw Azure Active Directory (Azure AD), moet u ook toorenew Power BI autorisatie elke twee weken.</span><span class="sxs-lookup"><span data-stu-id="cc91d-234">If Azure Multi-Factor Authentication is configured on your Azure Active Directory (Azure AD) tenant, you also need toorenew Power BI authorization every two weeks.</span></span> <span data-ttu-id="cc91d-235">Als u niet verlengt, kan er problemen zoals een gebrek aan taakuitvoer of een `Authenticate user error` in Hallo bewerkingslogboeken.</span><span class="sxs-lookup"><span data-stu-id="cc91d-235">If you don't renew, you could see symptoms such as a lack of job output or an `Authenticate user error` in hello operation logs.</span></span>

<span data-ttu-id="cc91d-236">Als een taak wordt gestart nadat het Hallo-token is verlopen, een fout optreedt en Hallo taak mislukt.</span><span class="sxs-lookup"><span data-stu-id="cc91d-236">Similarly, if a job starts after hello token has expired, an error occurs and hello job fails.</span></span> <span data-ttu-id="cc91d-237">tooresolve dit probleem stoppen Hallo-taak die wordt uitgevoerd, en gaat u tooyour Power BI-uitvoer.</span><span class="sxs-lookup"><span data-stu-id="cc91d-237">tooresolve this issue, stop hello job that's running and go tooyour Power BI output.</span></span> <span data-ttu-id="cc91d-238">tooavoid gegevensverlies, selecteer Hallo **vernieuwen autorisatie** koppelen en start de taak in Hallo **laatste tijd geëindigd**.</span><span class="sxs-lookup"><span data-stu-id="cc91d-238">tooavoid data loss, select hello **Renew authorization** link, and then restart your job from hello **Last Stopped Time**.</span></span>

<span data-ttu-id="cc91d-239">Nadat het Hallo-autorisatie is vernieuwd met Power BI, een groene waarschuwing wordt weergegeven in Hallo autorisatie gebied tooreflect Hallo probleem is opgelost.</span><span class="sxs-lookup"><span data-stu-id="cc91d-239">After hello authorization has been refreshed with Power BI, a green alert appears in hello authorization area tooreflect that hello issue has been resolved.</span></span>

## <a name="get-help"></a><span data-ttu-id="cc91d-240">Help opvragen</span><span class="sxs-lookup"><span data-stu-id="cc91d-240">Get help</span></span>
<span data-ttu-id="cc91d-241">Voor verdere hulp kunt u proberen onze [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="cc91d-241">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc91d-242">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cc91d-242">Next steps</span></span>
* [<span data-ttu-id="cc91d-243">Inleiding tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="cc91d-243">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="cc91d-244">Aan de slag met Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="cc91d-244">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="cc91d-245">Azure Stream Analytics-taken schalen</span><span class="sxs-lookup"><span data-stu-id="cc91d-245">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="cc91d-246">Azure Stream Analytics query language reference</span><span class="sxs-lookup"><span data-stu-id="cc91d-246">Azure Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="cc91d-247">Naslaginformatie over Azure Stream Analytics Management REST-API</span><span class="sxs-lookup"><span data-stu-id="cc91d-247">Azure Stream Analytics Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
