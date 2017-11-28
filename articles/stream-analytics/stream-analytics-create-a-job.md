---
title: Het maken van een taak analytics verwerking voor Stream Analytics | Microsoft Docs
description: Maken van een taak analytics verwerking voor Stream Analytics | leren padsegment.
keywords: gegevensverwerking analytics
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: e825fbcf-69e9-443f-b402-3b7a4568f415
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 05fdf1e20efd129cdfc27e1d37bc9e124edf5dcd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-create-a-data-analytics-processing-job-for-stream-analytics"></a><span data-ttu-id="e5083-104">Het maken van een taak analytics verwerking voor Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="e5083-104">How to create a data analytics processing job for Stream Analytics</span></span>
<span data-ttu-id="e5083-105">De resource op het hoogste niveau in Azure Stream Analytics is een Stream Analytics-taak.</span><span class="sxs-lookup"><span data-stu-id="e5083-105">The top-level resource in Azure Stream Analytics is a Stream Analytics Job.</span></span>  <span data-ttu-id="e5083-106">Bestaat uit een of meer invoer gegevensbronnen, een query uitdrukken van de gegevenstransformatie en een of meer uitvoer-doelen die resultaten naar worden geschreven.</span><span class="sxs-lookup"><span data-stu-id="e5083-106">It consists of one or more input data sources, a query expressing the data transformation, and one or more output targets that results are written to.</span></span> <span data-ttu-id="e5083-107">Samen kunnen deze gebruikers verwerken voor streaming gegevensscenario data-analyses uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="e5083-107">Together these enable the user to perform data analytics processing for streaming data scenarios.</span></span>

<span data-ttu-id="e5083-108">Om te starten met Stream Analytics, te beginnen met het maken van een nieuwe Stream Analytics-taak.</span><span class="sxs-lookup"><span data-stu-id="e5083-108">To start using Stream Analytics, begin by creating a new Stream Analytics job.</span></span>  <span data-ttu-id="e5083-109">Houd er rekening mee dat deze actie heeft geen gevolgen voor facturering totdat de taak is gestart.</span><span class="sxs-lookup"><span data-stu-id="e5083-109">Note this action has no billing implications until the job is started.</span></span>

1. <span data-ttu-id="e5083-110">Meld u aan bij de online [klassieke Azure-portal](http://manage.windowsazure.com) of de [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e5083-110">Sign in on the online [Azure classic portal](http://manage.windowsazure.com) or the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="e5083-111">In de portal: **op nieuw**, klikt u vervolgens op **Data Services** of **gegevensanalyse** afhankelijk van uw portal en klik vervolgens op **Azure Stream Analytics**of **Stream Analytics** en vervolgens **snelle invoer**.</span><span class="sxs-lookup"><span data-stu-id="e5083-111">In the portal: **Click New**, then click **Data Services** or **Data Analytics** depending on your portal and then click **Azure Stream Analytics** or **Stream Analytics** and then **Quick Create**.</span></span>
   
   ![Wizard gegevensverwerking analytics-taak](./media/stream-analytics-create-a-job/1-stream-analytics-create-a-job.png)  
   
   ![Gegevensanalyse taakverwerking maken](./media/stream-analytics-create-a-job/4-stream-analytics-create-a-job.png)  
3. <span data-ttu-id="e5083-114">Geef de gewenste configuratie voor de Stream Analytics-taak.</span><span class="sxs-lookup"><span data-stu-id="e5083-114">Specify the desired configuration for the Stream Analytics job.</span></span>
   
   * <span data-ttu-id="e5083-115">In de **taaknaam** Voer een unieke naam voor de Stream Analytics-taak.</span><span class="sxs-lookup"><span data-stu-id="e5083-115">In the **Job Name** box, enter a name to identify the Stream Analytics job.</span></span> <span data-ttu-id="e5083-116">Wanneer de **taaknaam** is gevalideerd, verschijnt een groen vinkje in het vak de naam van de taak.</span><span class="sxs-lookup"><span data-stu-id="e5083-116">When the **Job Name** is validated, a green check mark appears in the Job Name box.</span></span> <span data-ttu-id="e5083-117">De **taaknaam** mag alleen alfanumerieke tekens bevatten en de '-' bevatten, en moet tussen 3 en 63 tekens.</span><span class="sxs-lookup"><span data-stu-id="e5083-117">The **Job Name** may contain only alphanumeric characters and the '-' character, and must be between 3 and 63 characters.</span></span>
   * <span data-ttu-id="e5083-118">Gebruik **regio** in de Azure portal of **locatie** in de Azure portal om op te geven van de geografische locatie waar u de taak uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="e5083-118">Use **Region** in the Azure portal or **Location** in the Azure portal to specify the geographic location where you want to run the job.</span></span>
   * <span data-ttu-id="e5083-119">Als u de Azure-portal, selecteer of maak een opslagaccount wilt gebruiken als de **Opslagaccount regionale controle**.</span><span class="sxs-lookup"><span data-stu-id="e5083-119">If using the Azure portal, select or create a storage account to use as the **Regional Monitoring Storage Account**.</span></span> <span data-ttu-id="e5083-120">Dit opslagaccount wordt gebruikt voor het opslaan van de bewakingsgegevens voor alle Stream Analytics-taken die in deze regio worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e5083-120">This storage account is used to store monitoring data for all Stream Analytics jobs running in this region.</span></span>
   * <span data-ttu-id="e5083-121">Als de Azure-portal, geeft u een nieuwe of bestaande **resourcegroep** voor verwante resources voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="e5083-121">If using the Azure portal, specify a new or existing **Resource Group** to hold related resources for your application.</span></span>
4. <span data-ttu-id="e5083-122">Nadat de nieuwe opties voor de Stream Analytics-taak zijn geconfigureerd, klikt u op **Stream Analytics-taak maken**.</span><span class="sxs-lookup"><span data-stu-id="e5083-122">Once the new Stream Analytics job options are configured, click **Create Stream Analytics Job**.</span></span> <span data-ttu-id="e5083-123">Het kan enkele minuten duren voordat de Stream Analytics-taak moet worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e5083-123">It can take a few minutes for the Stream Analytics job to be created.</span></span> <span data-ttu-id="e5083-124">U kunt de status kunt u de voortgang in Notification hubs.</span><span class="sxs-lookup"><span data-stu-id="e5083-124">To check the status, you can monitor the progress in the Notifications hub.</span></span>
   
   ![Gegevens analytics verwerking taak Notification hubs](./media/stream-analytics-create-a-job/2-stream-analytics-create-a-job.png)  
   
   ![Azure portal gegevensanalyse verwerken taak taak maken](./media/stream-analytics-create-a-job/5-stream-analytics-create-a-job.png)  
5. <span data-ttu-id="e5083-127">De nieuwe taak wordt de status weergegeven **gemaakt**.</span><span class="sxs-lookup"><span data-stu-id="e5083-127">The new job will show a status of **Created**.</span></span> <span data-ttu-id="e5083-128">U ziet dat de **Start** knop is uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="e5083-128">Notice that the **Start** button is disabled.</span></span> <span data-ttu-id="e5083-129">De invoer van de taak, de query en de uitvoer configureren voordat u begint met de taak.</span><span class="sxs-lookup"><span data-stu-id="e5083-129">Configure the job input, query, and output before you start the job.</span></span>
   
   ![Gegevensverwerking analytics-taak Status](./media/stream-analytics-create-a-job/3-stream-analytics-create-a-job.png)  
   
   ![Azure portal gegevensanalyse taakstatus verwerken](./media/stream-analytics-create-a-job/6-stream-analytics-create-a-job.png)  

## <a name="get-help"></a><span data-ttu-id="e5083-132">Help opvragen</span><span class="sxs-lookup"><span data-stu-id="e5083-132">Get help</span></span>
<span data-ttu-id="e5083-133">Voor verdere hulp kunt u mogelijk terecht op het [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="e5083-133">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5083-134">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e5083-134">Next steps</span></span>
* [<span data-ttu-id="e5083-135">Inleiding tot Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="e5083-135">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="e5083-136">Aan de slag met Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="e5083-136">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="e5083-137">Azure Stream Analytics-taken schalen</span><span class="sxs-lookup"><span data-stu-id="e5083-137">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="e5083-138">Naslaggids voor Azure Stream Analytics Query</span><span class="sxs-lookup"><span data-stu-id="e5083-138">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="e5083-139">REST API-naslaggids voor Azure Stream Analytics Management</span><span class="sxs-lookup"><span data-stu-id="e5083-139">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

