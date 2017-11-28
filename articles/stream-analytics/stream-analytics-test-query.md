---
title: Azure Stream Analytics query testen | Microsoft Docs
description: Klik hier voor meer informatie over het testen van uw query's in de Stream Analytics-taken.
keywords: query testen, query oplossen
documentation center: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 16bb3f26ec3a69e5204162db9e54a186cf1ec6a6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="test-azure-stream-analytics-queries-in-the-azure-portal"></a><span data-ttu-id="98cea-104">Azure Stream Analytics query's testen in de Azure-portal</span><span class="sxs-lookup"><span data-stu-id="98cea-104">Test Azure Stream Analytics queries in the Azure portal</span></span>

<span data-ttu-id="98cea-105">U kunt met Azure Stream Analytics query's testen in de Azure portal zonder starten of stoppen van een taak.</span><span class="sxs-lookup"><span data-stu-id="98cea-105">With Azure Stream Analytics, you can test queries in the Azure portal without needing to start or stop a job.</span></span>

## <a name="test-the-input"></a><span data-ttu-id="98cea-106">De invoer testen</span><span class="sxs-lookup"><span data-stu-id="98cea-106">Test the input</span></span>

1. <span data-ttu-id="98cea-107">Als u wilt testen met invoer voorbeeldgegevens, met de rechtermuisknop op een van uw invoer en selecteer vervolgens **voorbeeldgegevens uit bestand uploaden**.</span><span class="sxs-lookup"><span data-stu-id="98cea-107">To test with sample input data, right-click any of your inputs, and then select **Upload sample data from file**.</span></span>

    ![query voor stream analytics query-editor testen](media/stream-analytics-test-query/stream-analytics-test-query-editor-upload.png)

2. <span data-ttu-id="98cea-109">Nadat het uploaden voltooid is, klikt u op **testen** voor het testen van deze query op de voorbeeldgegevens die u hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="98cea-109">After the upload is complete, click **Test** to test this query against the sample data you have provided.</span></span>

    ![Stream analytics query-editor test voorbeeldgegevens](media/stream-analytics-test-query/stream-analytics-test-query-editor-test.png)

<span data-ttu-id="98cea-111">De uitvoer van de query wordt weergegeven in de browser, met resultaten downloadkoppeling moet u de testuitvoer voor later gebruik opslaan.</span><span class="sxs-lookup"><span data-stu-id="98cea-111">The output of your query is displayed in the browser, with Download results link should you want to save the test output for later use.</span></span> <span data-ttu-id="98cea-112">U kunt nu eenvoudig en iteratief uw query te wijzigen en testen herhaaldelijk om te zien hoe de uitvoer wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="98cea-112">You can now easily and iteratively modify your query and test it repeatedly to see how the output changes.</span></span>

![Voorbeelduitvoer van stream Analytics query-editor](media/stream-analytics-test-query/stream-analytics-test-query-editor-samples-output.png)

<span data-ttu-id="98cea-114">U kunt met meerdere Uitvoerbronnen dat wordt gebruikt in een query, zien de resultaten voor beide uitvoer afzonderlijk en schakelen tussen deze twee.</span><span class="sxs-lookup"><span data-stu-id="98cea-114">With multiple outputs used in a query, you can see the results for both outputs separately and easily toggle between them.</span></span>

<span data-ttu-id="98cea-115">Nadat u tevreden bent met de resultaten weergegeven in de browser uw query opslaan, start de taak en kunt deze gebeurtenissen zonder fouten verwerken.</span><span class="sxs-lookup"><span data-stu-id="98cea-115">After you are satisfied with the results shown in the browser, you can save your query, start your job, and let it process events without error.</span></span>

## <a name="get-help"></a><span data-ttu-id="98cea-116">Help opvragen</span><span class="sxs-lookup"><span data-stu-id="98cea-116">Get help</span></span>

<span data-ttu-id="98cea-117">Voor verdere hulp kunt u proberen onze [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="98cea-117">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="98cea-118">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="98cea-118">Next steps</span></span>

* [<span data-ttu-id="98cea-119">Inleiding tot Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="98cea-119">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="98cea-120">Aan de slag met Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="98cea-120">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="98cea-121">Azure Stream Analytics-taken schalen</span><span class="sxs-lookup"><span data-stu-id="98cea-121">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="98cea-122">Naslaggids voor Azure Stream Analytics Query</span><span class="sxs-lookup"><span data-stu-id="98cea-122">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="98cea-123">REST API-naslaggids voor Azure Stream Analytics Management</span><span class="sxs-lookup"><span data-stu-id="98cea-123">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
