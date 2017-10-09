---
title: aaaHow toocreate een taak analytics verwerking voor Stream Analytics | Microsoft Docs
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
ms.openlocfilehash: d4a3c89d8862d59688d06a1719b063efa2ab1c93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-data-analytics-processing-job-for-stream-analytics"></a><span data-ttu-id="ebacd-104">Hoe toocreate een analytics gegevensverwerking taak voor Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="ebacd-104">How toocreate a data analytics processing job for Stream Analytics</span></span>
<span data-ttu-id="ebacd-105">Hallo op het hoogste niveau resource in Azure Stream Analytics is een Stream Analytics-taak.</span><span class="sxs-lookup"><span data-stu-id="ebacd-105">hello top-level resource in Azure Stream Analytics is a Stream Analytics Job.</span></span>  <span data-ttu-id="ebacd-106">Deze bestaat uit een of meer gegevensbronnen, een query uitdrukken Hallo gegevenstransformatie en een of meer uitvoer-doelen die resultaten zijn geschreven voor invoer.</span><span class="sxs-lookup"><span data-stu-id="ebacd-106">It consists of one or more input data sources, a query expressing hello data transformation, and one or more output targets that results are written to.</span></span> <span data-ttu-id="ebacd-107">Bij elkaar op die manier kunnen Hallo gebruiker tooperform gegevensanalyse verwerken voor streaminggegevens scenario's.</span><span class="sxs-lookup"><span data-stu-id="ebacd-107">Together these enable hello user tooperform data analytics processing for streaming data scenarios.</span></span>

<span data-ttu-id="ebacd-108">toostart met Stream Analytics, begint u met het maken van een nieuwe Stream Analytics-taak.</span><span class="sxs-lookup"><span data-stu-id="ebacd-108">toostart using Stream Analytics, begin by creating a new Stream Analytics job.</span></span>  <span data-ttu-id="ebacd-109">Houd er rekening mee dat deze actie heeft geen gevolgen voor facturering totdat het Hallo-taak is gestart.</span><span class="sxs-lookup"><span data-stu-id="ebacd-109">Note this action has no billing implications until hello job is started.</span></span>

1. <span data-ttu-id="ebacd-110">Meld u aan bij de online Hallo [klassieke Azure-portal](http://manage.windowsazure.com) of Hallo [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ebacd-110">Sign in on hello online [Azure classic portal](http://manage.windowsazure.com) or hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="ebacd-111">In de portal Hallo: **op nieuw**, klikt u vervolgens op **Data Services** of **gegevensanalyse** afhankelijk van uw portal en klik vervolgens op **Azure Stream Analytics** of **Stream Analytics** en vervolgens **snelle invoer**.</span><span class="sxs-lookup"><span data-stu-id="ebacd-111">In hello portal: **Click New**, then click **Data Services** or **Data Analytics** depending on your portal and then click **Azure Stream Analytics** or **Stream Analytics** and then **Quick Create**.</span></span>
   
   ![Wizard gegevensverwerking analytics-taak](./media/stream-analytics-create-a-job/1-stream-analytics-create-a-job.png)  
   
   ![Gegevensanalyse taakverwerking maken](./media/stream-analytics-create-a-job/4-stream-analytics-create-a-job.png)  
3. <span data-ttu-id="ebacd-114">Hallo gewenste configuratie voor de Stream Analytics-taak Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="ebacd-114">Specify hello desired configuration for hello Stream Analytics job.</span></span>
   
   * <span data-ttu-id="ebacd-115">In Hallo **taaknaam** Voer een naam tooidentify Hallo Stream Analytics-taak.</span><span class="sxs-lookup"><span data-stu-id="ebacd-115">In hello **Job Name** box, enter a name tooidentify hello Stream Analytics job.</span></span> <span data-ttu-id="ebacd-116">Wanneer Hallo **taaknaam** is gevalideerd, verschijnt een groen vinkje in Hallo taaknaam vak.</span><span class="sxs-lookup"><span data-stu-id="ebacd-116">When hello **Job Name** is validated, a green check mark appears in hello Job Name box.</span></span> <span data-ttu-id="ebacd-117">Hallo **taaknaam** mag alleen alfanumerieke tekens bevatten en Hallo '-' bevatten, en moet tussen 3 en 63 tekens.</span><span class="sxs-lookup"><span data-stu-id="ebacd-117">hello **Job Name** may contain only alphanumeric characters and hello '-' character, and must be between 3 and 63 characters.</span></span>
   * <span data-ttu-id="ebacd-118">Gebruik **regio** in hello Azure-portal of **locatie** in hello Azure portal toospecify Hallo geografische locatie waar u toorun Hallo taak.</span><span class="sxs-lookup"><span data-stu-id="ebacd-118">Use **Region** in hello Azure portal or **Location** in hello Azure portal toospecify hello geographic location where you want toorun hello job.</span></span>
   * <span data-ttu-id="ebacd-119">Als u met behulp van hello Azure-portal, selecteer of maak een toouse storage-account als Hallo **Opslagaccount regionale controle**.</span><span class="sxs-lookup"><span data-stu-id="ebacd-119">If using hello Azure portal, select or create a storage account toouse as hello **Regional Monitoring Storage Account**.</span></span> <span data-ttu-id="ebacd-120">Dit opslagaccount wordt gebruikt toostore bewakingsgegevens voor alle Stream Analytics-taken die in deze regio worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ebacd-120">This storage account is used toostore monitoring data for all Stream Analytics jobs running in this region.</span></span>
   * <span data-ttu-id="ebacd-121">Als u met behulp van Azure-portal hello, geeft u een nieuwe of bestaande **resourcegroep** toohold verwante resources voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="ebacd-121">If using hello Azure portal, specify a new or existing **Resource Group** toohold related resources for your application.</span></span>
4. <span data-ttu-id="ebacd-122">Wanneer u nieuwe opties voor Stream Analytics-taak Hallo zijn geconfigureerd, klikt u op **Stream Analytics-taak maken**.</span><span class="sxs-lookup"><span data-stu-id="ebacd-122">Once hello new Stream Analytics job options are configured, click **Create Stream Analytics Job**.</span></span> <span data-ttu-id="ebacd-123">Het kan enkele minuten duren voordat Hallo Stream Analytics-taak toobe gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ebacd-123">It can take a few minutes for hello Stream Analytics job toobe created.</span></span> <span data-ttu-id="ebacd-124">toocheck hello status, kunt u voortgang Hallo in Hallo Notification hubs.</span><span class="sxs-lookup"><span data-stu-id="ebacd-124">toocheck hello status, you can monitor hello progress in hello Notifications hub.</span></span>
   
   ![Gegevens analytics verwerking taak Notification hubs](./media/stream-analytics-create-a-job/2-stream-analytics-create-a-job.png)  
   
   ![Azure portal gegevensanalyse verwerken taak taak maken](./media/stream-analytics-create-a-job/5-stream-analytics-create-a-job.png)  
5. <span data-ttu-id="ebacd-127">Hallo nieuwe taak wordt de status weergegeven **gemaakt**.</span><span class="sxs-lookup"><span data-stu-id="ebacd-127">hello new job will show a status of **Created**.</span></span> <span data-ttu-id="ebacd-128">U ziet dat Hallo **Start** knop is uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="ebacd-128">Notice that hello **Start** button is disabled.</span></span> <span data-ttu-id="ebacd-129">Hallo taak invoer-, query- en uitvoer configureren voordat u begint met Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="ebacd-129">Configure hello job input, query, and output before you start hello job.</span></span>
   
   ![Gegevensverwerking analytics-taak Status](./media/stream-analytics-create-a-job/3-stream-analytics-create-a-job.png)  
   
   ![Azure portal gegevensanalyse taakstatus verwerken](./media/stream-analytics-create-a-job/6-stream-analytics-create-a-job.png)  

## <a name="get-help"></a><span data-ttu-id="ebacd-132">Help opvragen</span><span class="sxs-lookup"><span data-stu-id="ebacd-132">Get help</span></span>
<span data-ttu-id="ebacd-133">Voor verdere hulp kunt u mogelijk terecht op het [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="ebacd-133">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="ebacd-134">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ebacd-134">Next steps</span></span>
* [<span data-ttu-id="ebacd-135">Inleiding tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="ebacd-135">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="ebacd-136">Aan de slag met Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="ebacd-136">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="ebacd-137">Azure Stream Analytics-taken schalen</span><span class="sxs-lookup"><span data-stu-id="ebacd-137">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="ebacd-138">Naslaggids voor Azure Stream Analytics Query</span><span class="sxs-lookup"><span data-stu-id="ebacd-138">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="ebacd-139">REST API-naslaggids voor Azure Stream Analytics Management</span><span class="sxs-lookup"><span data-stu-id="ebacd-139">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

