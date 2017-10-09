---
title: aaaGet de slag met Azure Data Lake Analytics met Azure PowerShell | Microsoft Docs
description: 'Azure PowerShell toocreate een Data Lake Analytics-account gebruiken, maken van een Data Lake Analytics-taak met U-SQL en verzenden van Hallo-taak. '
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 8a4e901e-9656-4a60-90d0-d78ff2f00656
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/04/2017
ms.author: edmaca
ms.openlocfilehash: cb9b35352d1cc9a78337448b1d6835875a212e08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-powershell"></a><span data-ttu-id="64775-103">Aan de slag met Azure Data Lake Analytics met Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="64775-103">Get started with Azure Data Lake Analytics using Azure PowerShell</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="64775-104">Informatie over hoe toouse Azure PowerShell toocreate Azure Data Lake Analytics-accounts en vervolgens verzenden en U-SQL-taken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="64775-104">Learn how toouse Azure PowerShell toocreate Azure Data Lake Analytics accounts and then submit and run U-SQL jobs.</span></span> <span data-ttu-id="64775-105">Zie [Overzicht van Azure Data Lake Analytics](data-lake-analytics-overview.md) voor meer informatie over Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="64775-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="64775-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="64775-106">Prerequisites</span></span>

<span data-ttu-id="64775-107">Voordat u deze zelfstudie begint, hebt u de volgende informatie Hallo:</span><span class="sxs-lookup"><span data-stu-id="64775-107">Before you begin this tutorial, you must have hello following information:</span></span>

* <span data-ttu-id="64775-108">**Een Azure Data Lake Analytics-account**.</span><span class="sxs-lookup"><span data-stu-id="64775-108">**An Azure Data Lake Analytics account**.</span></span> <span data-ttu-id="64775-109">Zie [Aan de slag met Data Lake Analytics](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-get-started-portal).</span><span class="sxs-lookup"><span data-stu-id="64775-109">See [Get started with Data Lake Analytics](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-get-started-portal).</span></span>
* <span data-ttu-id="64775-110">**Een werkstation met Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="64775-110">**A workstation with Azure PowerShell**.</span></span> <span data-ttu-id="64775-111">Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="64775-111">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="64775-112">Meld u bij tooAzure</span><span class="sxs-lookup"><span data-stu-id="64775-112">Log in tooAzure</span></span>

<span data-ttu-id="64775-113">In deze zelfstudie wordt ervan uitgegaan dat u al bekend bent met het gebruik van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="64775-113">This tutorial assumes you are already familiar with using Azure PowerShell.</span></span> <span data-ttu-id="64775-114">In het bijzonder, moet u tooknow hoe toolog in tooAzure.</span><span class="sxs-lookup"><span data-stu-id="64775-114">In particular, you need tooknow how toolog in tooAzure.</span></span> <span data-ttu-id="64775-115">Zie Hallo [aan de slag met Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps) als u hulp nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="64775-115">See hello [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps) if you need help.</span></span>

<span data-ttu-id="64775-116">toolog met de abonnementsnaam van een:</span><span class="sxs-lookup"><span data-stu-id="64775-116">toolog in with a subscription name:</span></span>

```
Login-AzureRmAccount -SubscriptionName "ContosoSubscription"
```

<span data-ttu-id="64775-117">U kunt ook een abonnement-id toolog in gebruiken in plaats van de naam van Hallo abonnement:</span><span class="sxs-lookup"><span data-stu-id="64775-117">Instead of hello subscription name, you can also use a subscription id toolog in:</span></span>

```
Login-AzureRmAccount -SubscriptionId "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
```

<span data-ttu-id="64775-118">Als dit lukt, ziet er Hallo-uitvoer van deze opdracht Hallo volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="64775-118">If  successful, hello output of this command looks like hello following text:</span></span>

```
Environment           : AzureCloud
Account               : joe@contoso.com
TenantId              : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionId        : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionName      : ContosoSubscription
CurrentStorageAccount :
```

## <a name="preparing-for-hello-tutorial"></a><span data-ttu-id="64775-119">Hallo-zelfstudie voorbereiden</span><span class="sxs-lookup"><span data-stu-id="64775-119">Preparing for hello tutorial</span></span>

<span data-ttu-id="64775-120">Hallo PowerShell codefragmenten in deze zelfstudie gebruikt u deze variabelen toostore deze informatie:</span><span class="sxs-lookup"><span data-stu-id="64775-120">hello PowerShell snippets in this tutorial use these variables toostore this information:</span></span>

```
$rg = "<ResourceGroupName>"
$adls = "<DataLakeStoreAccountName>"
$adla = "<DataLakeAnalyticsAccountName>"
$location = "East US 2"
```

## <a name="get-information-about-a-data-lake-analytics-account"></a><span data-ttu-id="64775-121">Informatie krijgen over een Data Lake Analytics-account</span><span class="sxs-lookup"><span data-stu-id="64775-121">Get information about a Data Lake Analytics account</span></span>

```
Get-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla  
```

## <a name="submit-a-u-sql-job"></a><span data-ttu-id="64775-122">Een U-SQL-taak verzenden</span><span class="sxs-lookup"><span data-stu-id="64775-122">Submit a U-SQL job</span></span>

<span data-ttu-id="64775-123">Maak een PowerShell-script variabele toohold Hallo U-SQL.</span><span class="sxs-lookup"><span data-stu-id="64775-123">Create a PowerShell variable toohold hello U-SQL script.</span></span>

```
$script = @"
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();

"@
```

<span data-ttu-id="64775-124">Hallo script verzenden.</span><span class="sxs-lookup"><span data-stu-id="64775-124">Submit hello script.</span></span>

```
$job = Submit-AdlJob -AccountName $adla –Script $script
```

<span data-ttu-id="64775-125">U kunt ook Hallo script als een bestand opslaan en verzenden met de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="64775-125">Alternatively, you could save hello script as a file and submit with hello following command:</span></span>

```
$filename = "d:\test.usql"
$script | out-File $filename
$job = Submit-AdlJob -AccountName $adla –ScriptPath $filename
```


<span data-ttu-id="64775-126">Hallo-status van een bepaalde taak ophalen.</span><span class="sxs-lookup"><span data-stu-id="64775-126">Get hello status of a specific job.</span></span> <span data-ttu-id="64775-127">Deze cmdlet blijven worden gebruiken totdat er Hallo-taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="64775-127">Keep using this cmdlet until you see hello job is done.</span></span>

```
$job = Get-AdlJob -AccountName $adla -JobId $job.JobId
```

<span data-ttu-id="64775-128">In plaats van het aanroepen van Get-AdlAnalyticsJob steeds totdat een taak is voltooid, kunt u Hallo wacht AdlJob cmdlet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="64775-128">Instead of calling Get-AdlAnalyticsJob over and over until a job finishes, you can use hello Wait-AdlJob cmdlet.</span></span>

```
Wait-AdlJob -Account $adla -JobId $job.JobId
```

<span data-ttu-id="64775-129">Hallo-uitvoerbestand downloaden.</span><span class="sxs-lookup"><span data-stu-id="64775-129">Download hello output file.</span></span>

```
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "C:\data.csv"
```

## <a name="see-also"></a><span data-ttu-id="64775-130">Zie ook</span><span class="sxs-lookup"><span data-stu-id="64775-130">See also</span></span>
* <span data-ttu-id="64775-131">toosee Hallo dezelfde zelfstudie met een ander hulpprogramma, klikt u op Hallo-tabselectors op Hallo Hallo pagina bovenaan.</span><span class="sxs-lookup"><span data-stu-id="64775-131">toosee hello same tutorial using other tools, click hello tab selectors on hello top of hello page.</span></span>
* <span data-ttu-id="64775-132">toolearn U-SQL, Zie [aan de slag met Azure Data Lake Analytics U-SQL-taal](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="64775-132">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="64775-133">Zie [Azure Data Lake Analytics beheren met Azure Portal](data-lake-analytics-manage-use-portal.md) voor informatie over beheertaken.</span><span class="sxs-lookup"><span data-stu-id="64775-133">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
