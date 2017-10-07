---
title: aaaAzure quotalimieten voor Data Lake Analytics | Microsoft Docs
description: Meer informatie over hoe tooadjust en verhoging van het quotum beperkt in Azure Data Lake Analytics (ADLA)-accounts.
services: data-lake-analytics
keywords: Azure Data Lake Analytics
documentationcenter: 
author: omidm1
editor: omidm1
ms.assetid: 49416f38-fcc7-476f-a55e-d67f3f9c1d34
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: omidm
ms.openlocfilehash: 875c4d00e0c57414031e50754495c02162bdca48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-lake-analytics-quota-limits"></a><span data-ttu-id="ac9ce-104">De quotalimieten voor Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="ac9ce-104">Azure Data Lake Analytics Quota Limits</span></span>

<span data-ttu-id="ac9ce-105">Meer informatie over hoe tooadjust en verhoging van het quotum beperkt in Azure Data Lake Analytics (ADLA)-accounts.</span><span class="sxs-lookup"><span data-stu-id="ac9ce-105">Learn how tooadjust and increase quota limits in Azure Data Lake Analytics (ADLA) accounts.</span></span> <span data-ttu-id="ac9ce-106">Deze limieten weten, kunt u meer inzicht in uw U-SQL-taak gedrag.</span><span class="sxs-lookup"><span data-stu-id="ac9ce-106">Knowing these limits may help you understand your U-SQL job behavior.</span></span> <span data-ttu-id="ac9ce-107">Alle quotalimieten zijn zachte, zodat u maximaal Hallo-limieten verhogen kunt door toous bereikt.</span><span class="sxs-lookup"><span data-stu-id="ac9ce-107">All quota limits are soft, so you can increase hello maximum limits by reaching out toous.</span></span>

## <a name="azure-subscriptions-limits"></a><span data-ttu-id="ac9ce-108">Limieten voor Azure-abonnementen</span><span class="sxs-lookup"><span data-stu-id="ac9ce-108">Azure subscriptions limits</span></span>

<span data-ttu-id="ac9ce-109">**Maximum aantal ADLA accounts per abonnement:** 5</span><span class="sxs-lookup"><span data-stu-id="ac9ce-109">**Maximum number of ADLA accounts per subscription:**  5</span></span>

 <span data-ttu-id="ac9ce-110">Dit is Hallo kunt u het maximum aantal ADLA accounts die u per abonnement maken kunt.</span><span class="sxs-lookup"><span data-stu-id="ac9ce-110">This is hello maximum number of ADLA accounts you can create per subscription.</span></span> <span data-ttu-id="ac9ce-111">Als u een zesde toocreate ADLA account probeert, krijgt u een foutbericht 'U bereikt Hallo kunt u het maximum aantal Data Lake Analytics-accounts toegestaan (5) in regio onder de abonnementsnaam van het '.</span><span class="sxs-lookup"><span data-stu-id="ac9ce-111">If you try toocreate a sixth ADLA account, you will get an error "You have reached hello maximum number of Data Lake Analytics accounts allowed (5) in region under subscription name".</span></span> <span data-ttu-id="ac9ce-112">In dit geval Verwijder ongebruikte ADLA accounts of bereiken door toous [een ondersteuningsticket openen](#increase-maximum-quota-limits).</span><span class="sxs-lookup"><span data-stu-id="ac9ce-112">In this case, either delete any unused ADLA accounts, or reach out toous by [opening a support ticket](#increase-maximum-quota-limits).</span></span>

## <a name="adla-account-limits"></a><span data-ttu-id="ac9ce-113">Limieten van ADLA</span><span class="sxs-lookup"><span data-stu-id="ac9ce-113">ADLA account limits</span></span>

<span data-ttu-id="ac9ce-114">**Maximum aantal eenheden Analytics (AUs) per account:** 250</span><span class="sxs-lookup"><span data-stu-id="ac9ce-114">**Maximum number of Analytics Units (AUs) per account:** 250</span></span>

<span data-ttu-id="ac9ce-115">Dit is Hallo kunt u het maximum aantal AUs die tegelijkertijd kunnen worden uitgevoerd in uw account.</span><span class="sxs-lookup"><span data-stu-id="ac9ce-115">This is hello maximum number of AUs that can run concurrently in your account.</span></span> <span data-ttu-id="ac9ce-116">Als de totale AUs uitvoeren voor alle taken deze limiet overschrijdt, nieuwere taken in de wachtrij automatisch.</span><span class="sxs-lookup"><span data-stu-id="ac9ce-116">If your total running AUs across all jobs exceeds this limit, newer jobs are queued automatically.</span></span> <span data-ttu-id="ac9ce-117">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="ac9ce-117">For example:</span></span>

* <span data-ttu-id="ac9ce-118">Als u slechts één taak hebt uitgevoerd met 250 AUs, wanneer u een tweede indient taak deze in de taakwachtrij Hallo wacht totdat de eerste taak Hallo is voltooid.</span><span class="sxs-lookup"><span data-stu-id="ac9ce-118">If you have only one job running with 250 AUs, when you submit a second job it will wait in hello job queue until hello first job completes.</span></span>
* <span data-ttu-id="ac9ce-119">Als u hebt al vijf taken worden uitgevoerd en elk van 50 gebruikmaakt AUs, wanneer u een zesde taak die 20 moet stuurt deze in de taakwachtrij Hallo wacht totdat er 20 AUs AUs beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="ac9ce-119">If you already have five jobs running and each is using 50 AUs, when you submit a sixth job that needs 20 AUs it waits in hello job queue until there are 20 AUs available.</span></span>

<span data-ttu-id="ac9ce-120">**Maximum aantal gelijktijdige U-SQL-taken per account:** 20</span><span class="sxs-lookup"><span data-stu-id="ac9ce-120">**Maximum number of concurrent U-SQL jobs per account:** 20</span></span>

<span data-ttu-id="ac9ce-121">Dit is Hallo kunt u het maximum aantal taken dat gelijktijdig kan worden uitgevoerd in uw account.</span><span class="sxs-lookup"><span data-stu-id="ac9ce-121">This is hello maximum number of jobs that can run concurrently in your account.</span></span> <span data-ttu-id="ac9ce-122">Boven deze waarde nieuwere taken in de wachtrij automatisch.</span><span class="sxs-lookup"><span data-stu-id="ac9ce-122">Above this value, newer jobs are queued automatically.</span></span>

## <a name="adjust-adla-quota-limits-per-account"></a><span data-ttu-id="ac9ce-123">De quotalimieten ADLA per account aanpassen</span><span class="sxs-lookup"><span data-stu-id="ac9ce-123">Adjust ADLA quota limits per account</span></span>

1. <span data-ttu-id="ac9ce-124">Meld u aan bij toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ac9ce-124">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ac9ce-125">Kies een bestaand ADLA-account.</span><span class="sxs-lookup"><span data-stu-id="ac9ce-125">Choose an existing ADLA account.</span></span>
3. <span data-ttu-id="ac9ce-126">Klik op **Eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="ac9ce-126">Click **Properties**.</span></span>
4. <span data-ttu-id="ac9ce-127">Aanpassen **parallelle uitvoering** en **gelijktijdige taken** toosuit uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="ac9ce-127">Adjust **Parallelism** and **Concurrent Jobs** toosuit your needs.</span></span>

    ![Azure Data Lake Analytics-portalblade](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-properties.png)

## <a name="increase-maximum-quota-limits"></a><span data-ttu-id="ac9ce-129">Maximumquotum limieten verhogen</span><span class="sxs-lookup"><span data-stu-id="ac9ce-129">Increase maximum quota limits</span></span>

1. <span data-ttu-id="ac9ce-130">Open een ondersteuningsaanvraag in Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="ac9ce-130">Open a support request in Azure Portal.</span></span>

    ![Azure Data Lake Analytics-portalblade](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-help-support.png)

    ![Azure Data Lake Analytics-portalblade](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request.png)
2. <span data-ttu-id="ac9ce-133">Selecteer Hallo probleem type **quotum**.</span><span class="sxs-lookup"><span data-stu-id="ac9ce-133">Select hello issue type **Quota**.</span></span>
3. <span data-ttu-id="ac9ce-134">Selecteer uw **abonnement** (Zorg ervoor dat het is niet een ' ' proefabonnement).</span><span class="sxs-lookup"><span data-stu-id="ac9ce-134">Select your **Subscription** (make sure it is not a "trial" subscription).</span></span>
4. <span data-ttu-id="ac9ce-135">Selecteer quotatype **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="ac9ce-135">Select quota type **Data Lake Analytics**.</span></span>

    ![Azure Data Lake Analytics-portalblade](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-basics.png)

5. <span data-ttu-id="ac9ce-137">Hallo probleem blade uitgelegd uw limiet aangevraagde verhoging met **Details** van waarom u deze extra capaciteit nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="ac9ce-137">In hello problem blade, explain your requested increase limit with **Details** of why you need this extra capacity.</span></span>

    ![Azure Data Lake Analytics-portalblade](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-details.png)

6. <span data-ttu-id="ac9ce-139">Uw contactgegevens controleren en u Hallo ondersteuningsaanvraag wilt indienen.</span><span class="sxs-lookup"><span data-stu-id="ac9ce-139">Verify your contact information and create hello support request.</span></span>

<span data-ttu-id="ac9ce-140">Microsoft uw aanvraag beoordeelt en probeert tooaccommodate zo snel mogelijk de behoeften van uw bedrijf.</span><span class="sxs-lookup"><span data-stu-id="ac9ce-140">Microsoft reviews your request and tries tooaccommodate your business needs as soon as possible.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ac9ce-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ac9ce-141">Next steps</span></span>

* [<span data-ttu-id="ac9ce-142">Overzicht van Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="ac9ce-142">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="ac9ce-143">Azure Data Lake Analytics beheren met Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ac9ce-143">Manage Azure Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-manage-use-powershell.md)
* [<span data-ttu-id="ac9ce-144">Azure Data Lake Analytics-taken bewaken en problemen oplossen met Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ac9ce-144">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
