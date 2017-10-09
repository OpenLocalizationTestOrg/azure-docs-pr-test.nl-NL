---
title: aaaGet slag met Azure Data Lake Analytics met Azure portal | Microsoft Docs
description: 'Informatie over hoe toouse hello Azure portal toocreate een Data Lake Analytics-account maken van een Data Lake Analytics-taak met U-SQL, en het Hallo-taak verzenden. '
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: b1584d16-e0d2-4019-ad1f-f04be8c5b430
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/21/2017
ms.author: edmaca
ms.openlocfilehash: 6bb54404fa42cfed25b18bc2bfb7c72e6c361149
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-portal"></a><span data-ttu-id="0547a-103">Aan de slag met Azure Data Lake Analytics met Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0547a-103">Get started with Azure Data Lake Analytics using Azure portal</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="0547a-104">Meer informatie over hoe toouse hello Azure portal toocreate Azure Data Lake Analytics-accounts, het definiëren van taken in [U-SQL](data-lake-analytics-u-sql-get-started.md), en het verzenden van taken toohello Data Lake Analytics-service.</span><span class="sxs-lookup"><span data-stu-id="0547a-104">Learn how toouse hello Azure portal toocreate Azure Data Lake Analytics accounts, define jobs in [U-SQL](data-lake-analytics-u-sql-get-started.md), and submit jobs toohello Data Lake Analytics service.</span></span> <span data-ttu-id="0547a-105">Zie [Overzicht van Azure Data Lake Analytics](data-lake-analytics-overview.md) voor meer informatie over Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="0547a-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0547a-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="0547a-106">Prerequisites</span></span>

<span data-ttu-id="0547a-107">Voordat u met deze zelfstudie begint, moet u een **Azure-abonnement** hebben.</span><span class="sxs-lookup"><span data-stu-id="0547a-107">Before you begin this tutorial, you must have an **Azure subscription**.</span></span> <span data-ttu-id="0547a-108">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0547a-108">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="0547a-109">Een Data Lake Analytics-account maken</span><span class="sxs-lookup"><span data-stu-id="0547a-109">Create a Data Lake Analytics account</span></span>

<span data-ttu-id="0547a-110">Nu u een Data Lake Analytics maakt en een Data Lake Store-account op Hallo dezelfde tijd.</span><span class="sxs-lookup"><span data-stu-id="0547a-110">Now, you will create a Data Lake Analytics and a Data Lake Store account at hello same time.</span></span>  <span data-ttu-id="0547a-111">Deze stap is eenvoudig en alleen toofinish 60 seconden duurt.</span><span class="sxs-lookup"><span data-stu-id="0547a-111">This step is simple and only takes about 60 seconds toofinish.</span></span>

1. <span data-ttu-id="0547a-112">Meld u aan bij toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0547a-112">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0547a-113">Klik op **Nieuw** >  **Gegevens + analyse** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="0547a-113">Click **New** >  **Data + Analytics** > **Data Lake Analytics**.</span></span>
3. <span data-ttu-id="0547a-114">Waarden selecteren voor Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="0547a-114">Select values for hello following items:</span></span>
   * <span data-ttu-id="0547a-115">**Naam**: geef uw Data Lake Analytics-account een naam (alleen kleine letters en cijfers zijn toegestaan).</span><span class="sxs-lookup"><span data-stu-id="0547a-115">**Name**: Name your Data Lake Analytics account (Only lower case letters and numbers allowed).</span></span>
   * <span data-ttu-id="0547a-116">**Abonnement**: Kies hello Azure-abonnement gebruikt voor Hallo Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="0547a-116">**Subscription**: Choose hello Azure subscription used for hello Analytics account.</span></span>
   * <span data-ttu-id="0547a-117">**Resourcegroep**.</span><span class="sxs-lookup"><span data-stu-id="0547a-117">**Resource Group**.</span></span> <span data-ttu-id="0547a-118">Selecteer een bestaande Azure-resourcegroep of maak een nieuwe.</span><span class="sxs-lookup"><span data-stu-id="0547a-118">Select an existing Azure Resource Group or create a new one.</span></span>
   * <span data-ttu-id="0547a-119">**Locatie**.</span><span class="sxs-lookup"><span data-stu-id="0547a-119">**Location**.</span></span> <span data-ttu-id="0547a-120">Selecteer een Azure-Datacenter voor Hallo Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="0547a-120">Select an Azure data center for hello Data Lake Analytics account.</span></span>
   * <span data-ttu-id="0547a-121">**Data Lake Store**: Volg Hallo instructie toocreate een nieuw Data Lake Store-account of een bestaande set selecteren.</span><span class="sxs-lookup"><span data-stu-id="0547a-121">**Data Lake Store**: Follow hello instruction toocreate a new Data Lake Store account, or select an existing one.</span></span> 
4. <span data-ttu-id="0547a-122">U kunt ervoor kiezen om een prijscategorie te selecteren voor uw Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="0547a-122">Optionally, select a pricing tier for your Data Lake Analytics account.</span></span>
5. <span data-ttu-id="0547a-123">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="0547a-123">Click **Create**.</span></span> 


## <a name="your-first-u-sql-script"></a><span data-ttu-id="0547a-124">Uw eerste U-SQL-script</span><span class="sxs-lookup"><span data-stu-id="0547a-124">Your first U-SQL script</span></span>

<span data-ttu-id="0547a-125">na de tekst Hello is een zeer eenvoudige U-SQL-script.</span><span class="sxs-lookup"><span data-stu-id="0547a-125">hello following text is a very simple U-SQL script.</span></span> <span data-ttu-id="0547a-126">Deze methode wordt een kleine gegevensset binnen Hallo script definiëren en vervolgens deze gegevensset uit toohello default Data Lake Store niet schrijven als een bestand met de naam `/data.csv`.</span><span class="sxs-lookup"><span data-stu-id="0547a-126">All it does is define a small dataset within hello script and then write that dataset out toohello default Data Lake Store as a file called `/data.csv`.</span></span>

```
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
```

## <a name="submit-a-u-sql-job"></a><span data-ttu-id="0547a-127">Een U-SQL-taak verzenden</span><span class="sxs-lookup"><span data-stu-id="0547a-127">Submit a U-SQL job</span></span>

1. <span data-ttu-id="0547a-128">Hallo Data Lake Analytics-account, klik op **nieuwe taak**.</span><span class="sxs-lookup"><span data-stu-id="0547a-128">From hello Data Lake Analytics account, click **New Job**.</span></span>
2. <span data-ttu-id="0547a-129">U-SQL-script hierboven weergegeven in de tekst hello Hallo plakken.</span><span class="sxs-lookup"><span data-stu-id="0547a-129">Paste in hello text of hello U-SQL script shown above.</span></span> 
3. <span data-ttu-id="0547a-130">Klik op **Taak verzenden**.</span><span class="sxs-lookup"><span data-stu-id="0547a-130">Click **Submit Job**.</span></span>   
4. <span data-ttu-id="0547a-131">Wachten tot Hallo taakstatuswijzigingen te**geslaagd**.</span><span class="sxs-lookup"><span data-stu-id="0547a-131">Wait until hello job status changes too**Succeeded**.</span></span>
5. <span data-ttu-id="0547a-132">Als het Hallo-taak is mislukt, raadpleegt u [Monitor en Data Lake Analytics-taken oplossen](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="0547a-132">If hello job failed, see [Monitor and troubleshoot Data Lake Analytics jobs](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span></span>
6. <span data-ttu-id="0547a-133">Klik op Hallo **uitvoer** tabblad en klik vervolgens op `data.csv`.</span><span class="sxs-lookup"><span data-stu-id="0547a-133">Click hello **Output** tab, and then click `data.csv`.</span></span> 

## <a name="see-also"></a><span data-ttu-id="0547a-134">Zie ook</span><span class="sxs-lookup"><span data-stu-id="0547a-134">See also</span></span>

* <span data-ttu-id="0547a-135">tooget gestart met het ontwikkelen van U-SQL-toepassingen, Zie [U-SQL-scripts ontwikkelen met Data Lake Tools voor Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0547a-135">tooget started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="0547a-136">toolearn U-SQL, Zie [aan de slag met Azure Data Lake Analytics U-SQL-taal](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0547a-136">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="0547a-137">Zie [Azure Data Lake Analytics beheren met Azure Portal](data-lake-analytics-manage-use-portal.md) voor informatie over beheertaken.</span><span class="sxs-lookup"><span data-stu-id="0547a-137">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
