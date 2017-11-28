---
title: aaaMove gegevens tooand uit Azure Blob Storage | Microsoft Docs
description: Verplaatsen van gegevens tooand uit Azure Blob Storage
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d6681e30-ab45-45ea-a9fb-ac8acefe544d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;sachouks
ms.openlocfilehash: e12b8c157955195e826f8b108075afaf25ca7bd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage"></a><span data-ttu-id="857ec-103">Verplaatsen van gegevens tooand uit Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="857ec-103">Move data tooand from Azure Blob Storage</span></span>
[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<!-- just in case, adding this tooseparate these two include references -->

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

<span data-ttu-id="857ec-104">Welke methode voor u het beste is, is afhankelijk van uw scenario.</span><span class="sxs-lookup"><span data-stu-id="857ec-104">Which method is best for you depends on your scenario.</span></span> <span data-ttu-id="857ec-105">Hallo [scenario's voor geavanceerde analyses in Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md) artikel kunt u beter bepalen Hallo-resources die u nodig voor een verscheidenheid aan gegevens wetenschappelijke werkstromen in Hallo advanced analytics proces gebruikt.</span><span class="sxs-lookup"><span data-stu-id="857ec-105">hello [Scenarios for advanced analytics in Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md) article helps you determine hello resources you need for a variety of data science workflows used in hello advanced analytics process.</span></span>

> [!NOTE]
> <span data-ttu-id="857ec-106">Voor een volledige inleiding tooAzure blob-opslag te verwijzen[basisbeginselen van Azure Blob](../storage/blobs/storage-dotnet-how-to-use-blobs.md) en te[Azure Blob-Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="857ec-106">For a complete introduction tooAzure blob storage, refer too[Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and too[Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

<span data-ttu-id="857ec-107">Als alternatief kunt u [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) naar:</span><span class="sxs-lookup"><span data-stu-id="857ec-107">As an alternative, you can use [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) to:</span></span> 

* <span data-ttu-id="857ec-108">maken en een pijplijn die gegevens gedownload uit Azure blob-opslag plannen</span><span class="sxs-lookup"><span data-stu-id="857ec-108">create and schedule a pipeline that downloads data from Azure blob storage,</span></span> 
* <span data-ttu-id="857ec-109">Geef dit tooa gepubliceerd Azure Machine Learning-webservice</span><span class="sxs-lookup"><span data-stu-id="857ec-109">pass it tooa published Azure Machine Learning web service,</span></span> 
* <span data-ttu-id="857ec-110">Hallo predictive analytics-resultaten, ontvangen en</span><span class="sxs-lookup"><span data-stu-id="857ec-110">receive hello predictive analytics results, and</span></span> 
* <span data-ttu-id="857ec-111">Hallo resultaten toostorage uploaden.</span><span class="sxs-lookup"><span data-stu-id="857ec-111">upload hello results toostorage.</span></span> 

<span data-ttu-id="857ec-112">Zie voor meer informatie [voorspellende pijplijnen met behulp van Azure Data Factory en Azure Machine Learning maken](../data-factory/data-factory-azure-ml-batch-execution-activity.md).</span><span class="sxs-lookup"><span data-stu-id="857ec-112">For more information, see [Create predictive pipelines using Azure Data Factory and Azure Machine Learning](../data-factory/data-factory-azure-ml-batch-execution-activity.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="857ec-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="857ec-113">Prerequisites</span></span>
<span data-ttu-id="857ec-114">Dit document wordt ervan uitgegaan dat u een Azure-abonnement, een opslagaccount en de bijbehorende opslagsleutel Hallo voor dat account hebt.</span><span class="sxs-lookup"><span data-stu-id="857ec-114">This document assumes that you have an Azure subscription, a storage account, and hello corresponding storage key for that account.</span></span> <span data-ttu-id="857ec-115">Voordat u gaat gegevens uploaden/downloaden, moet u weten Azure naam en sleutel van uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="857ec-115">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="857ec-116">Zie tooset van een Azure-abonnement [gratis proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="857ec-116">tooset up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="857ec-117">Zie voor instructies over het maken van een opslagaccount en voor het ophalen van de account en sleutelgegevens [over Azure storage-accounts](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="857ec-117">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

