---
title: Aan de slag met Azure Data Lake Analytics met Azure PowerShell | Microsoft Docs
description: 'Gebruik Azure PowerShell om een Data Lake Analytics-account te maken, een Data Lake Analytics-taak te maken met U-SQL en de taak te verzenden. '
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
ms.openlocfilehash: 4f73e27c733edae658d1ea3bdabe48076328279b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-powershell"></a><span data-ttu-id="82e35-103">Aan de slag met Azure Data Lake Analytics met Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="82e35-103">Get started with Azure Data Lake Analytics using Azure PowerShell</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="82e35-104">Informatie over het gebruik van Azure PowerShell om Azure Data Lake Analytics-accounts te maken en vervolgens U SQL-taken te verzenden en uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="82e35-104">Learn how to use Azure PowerShell to create Azure Data Lake Analytics accounts and then submit and run U-SQL jobs.</span></span> <span data-ttu-id="82e35-105">Zie [Overzicht van Azure Data Lake Analytics](data-lake-analytics-overview.md) voor meer informatie over Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="82e35-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="82e35-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="82e35-106">Prerequisites</span></span>

<span data-ttu-id="82e35-107">Voordat u met deze zelfstudie begint, moet u beschikken over de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="82e35-107">Before you begin this tutorial, you must have the following information:</span></span>

* <span data-ttu-id="82e35-108">**Een Azure Data Lake Analytics-account**.</span><span class="sxs-lookup"><span data-stu-id="82e35-108">**An Azure Data Lake Analytics account**.</span></span> <span data-ttu-id="82e35-109">Zie [Aan de slag met Data Lake Analytics](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-get-started-portal).</span><span class="sxs-lookup"><span data-stu-id="82e35-109">See [Get started with Data Lake Analytics](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-get-started-portal).</span></span>
* <span data-ttu-id="82e35-110">**Een werkstation met Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="82e35-110">**A workstation with Azure PowerShell**.</span></span> <span data-ttu-id="82e35-111">Zie [Azure PowerShell installeren en configureren](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="82e35-111">See [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="82e35-112">Meld u aan bij Azure.</span><span class="sxs-lookup"><span data-stu-id="82e35-112">Log in to Azure</span></span>

<span data-ttu-id="82e35-113">In deze zelfstudie wordt ervan uitgegaan dat u al bekend bent met het gebruik van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="82e35-113">This tutorial assumes you are already familiar with using Azure PowerShell.</span></span> <span data-ttu-id="82e35-114">Het is voornamelijk belangrijk dat u weet hoe u zich aanmeldt bij Azure.</span><span class="sxs-lookup"><span data-stu-id="82e35-114">In particular, you need to know how to log in to Azure.</span></span> <span data-ttu-id="82e35-115">Zie [Aan de slag met Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps) als u hulp nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="82e35-115">See the [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps) if you need help.</span></span>

<span data-ttu-id="82e35-116">Aanmelden met de naam van een abonnement:</span><span class="sxs-lookup"><span data-stu-id="82e35-116">To log in with a subscription name:</span></span>

```
Login-AzureRmAccount -SubscriptionName "ContosoSubscription"
```

<span data-ttu-id="82e35-117">In plaats van de abonnementsnaam, kunt u ook een abonnements-id gebruiken om u aan te melden:</span><span class="sxs-lookup"><span data-stu-id="82e35-117">Instead of the subscription name, you can also use a subscription id to log in:</span></span>

```
Login-AzureRmAccount -SubscriptionId "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
```

<span data-ttu-id="82e35-118">Als dit lukt, ziet de uitvoer van deze opdracht er  uit als de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="82e35-118">If  successful, the output of this command looks like the following text:</span></span>

```
Environment           : AzureCloud
Account               : joe@contoso.com
TenantId              : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionId        : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionName      : ContosoSubscription
CurrentStorageAccount :
```

## <a name="preparing-for-the-tutorial"></a><span data-ttu-id="82e35-119">Voorbereiding voor de zelfstudie</span><span class="sxs-lookup"><span data-stu-id="82e35-119">Preparing for the tutorial</span></span>

<span data-ttu-id="82e35-120">De PowerShell-fragmenten in deze zelfstudie gebruiken deze variabelen om deze informatie op te slaan:</span><span class="sxs-lookup"><span data-stu-id="82e35-120">The PowerShell snippets in this tutorial use these variables to store this information:</span></span>

```
$rg = "<ResourceGroupName>"
$adls = "<DataLakeStoreAccountName>"
$adla = "<DataLakeAnalyticsAccountName>"
$location = "East US 2"
```

## <a name="get-information-about-a-data-lake-analytics-account"></a><span data-ttu-id="82e35-121">Informatie krijgen over een Data Lake Analytics-account</span><span class="sxs-lookup"><span data-stu-id="82e35-121">Get information about a Data Lake Analytics account</span></span>

```
Get-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla  
```

## <a name="submit-a-u-sql-job"></a><span data-ttu-id="82e35-122">Een U-SQL-taak verzenden</span><span class="sxs-lookup"><span data-stu-id="82e35-122">Submit a U-SQL job</span></span>

<span data-ttu-id="82e35-123">Maak een PowerShell-variabele om het U-SQL-script op te slaan.</span><span class="sxs-lookup"><span data-stu-id="82e35-123">Create a PowerShell variable to hold the U-SQL script.</span></span>

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
    TO "/data.csv"
    USING Outputters.Csv();

"@
```

<span data-ttu-id="82e35-124">Verzend het script.</span><span class="sxs-lookup"><span data-stu-id="82e35-124">Submit the script.</span></span>

```
$job = Submit-AdlJob -AccountName $adla –Script $script
```

<span data-ttu-id="82e35-125">U kunt het script ook opslaan als een bestand en verzenden met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="82e35-125">Alternatively, you could save the script as a file and submit with the following command:</span></span>

```
$filename = "d:\test.usql"
$script | out-File $filename
$job = Submit-AdlJob -AccountName $adla –ScriptPath $filename
```


<span data-ttu-id="82e35-126">Haal de status van een bepaalde taak op.</span><span class="sxs-lookup"><span data-stu-id="82e35-126">Get the status of a specific job.</span></span> <span data-ttu-id="82e35-127">Blijf deze cmdlet gebruiken totdat de taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="82e35-127">Keep using this cmdlet until you see the job is done.</span></span>

```
$job = Get-AdlJob -AccountName $adla -JobId $job.JobId
```

<span data-ttu-id="82e35-128">U hoeft niet steeds Get-AdlAnalyticsJob aan te roepen tot een taak is voltooid als u de cmdlet Wait-AdlJob gebruikt.</span><span class="sxs-lookup"><span data-stu-id="82e35-128">Instead of calling Get-AdlAnalyticsJob over and over until a job finishes, you can use the Wait-AdlJob cmdlet.</span></span>

```
Wait-AdlJob -Account $adla -JobId $job.JobId
```

<span data-ttu-id="82e35-129">Download het uitvoerbestand.</span><span class="sxs-lookup"><span data-stu-id="82e35-129">Download the output file.</span></span>

```
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "C:\data.csv"
```

## <a name="see-also"></a><span data-ttu-id="82e35-130">Zie ook</span><span class="sxs-lookup"><span data-stu-id="82e35-130">See also</span></span>
* <span data-ttu-id="82e35-131">Als u dezelfde zelfstudie wilt bekijken met een ander hulpprogramma, klikt u op de tabselectors boven aan de pagina.</span><span class="sxs-lookup"><span data-stu-id="82e35-131">To see the same tutorial using other tools, click the tab selectors on the top of the page.</span></span>
* <span data-ttu-id="82e35-132">Zie [Aan de slag met de Azure Data Lake Analytics U-SQL-taal](data-lake-analytics-u-sql-get-started.md) om U-SQL te leren.</span><span class="sxs-lookup"><span data-stu-id="82e35-132">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="82e35-133">Zie [Azure Data Lake Analytics beheren met Azure Portal](data-lake-analytics-manage-use-portal.md) voor informatie over beheertaken.</span><span class="sxs-lookup"><span data-stu-id="82e35-133">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
