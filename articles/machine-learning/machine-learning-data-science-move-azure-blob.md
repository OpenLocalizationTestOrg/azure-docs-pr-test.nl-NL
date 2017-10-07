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
# <a name="move-data-tooand-from-azure-blob-storage"></a>Verplaatsen van gegevens tooand uit Azure Blob Storage
[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<!-- just in case, adding this tooseparate these two include references -->

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

Welke methode voor u het beste is, is afhankelijk van uw scenario. Hallo [scenario's voor geavanceerde analyses in Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md) artikel kunt u beter bepalen Hallo-resources die u nodig voor een verscheidenheid aan gegevens wetenschappelijke werkstromen in Hallo advanced analytics proces gebruikt.

> [!NOTE]
> Voor een volledige inleiding tooAzure blob-opslag te verwijzen[basisbeginselen van Azure Blob](../storage/blobs/storage-dotnet-how-to-use-blobs.md) en te[Azure Blob-Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).
> 
> 

Als alternatief kunt u [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) naar: 

* maken en een pijplijn die gegevens gedownload uit Azure blob-opslag plannen 
* Geef dit tooa gepubliceerd Azure Machine Learning-webservice 
* Hallo predictive analytics-resultaten, ontvangen en 
* Hallo resultaten toostorage uploaden. 

Zie voor meer informatie [voorspellende pijplijnen met behulp van Azure Data Factory en Azure Machine Learning maken](../data-factory/data-factory-azure-ml-batch-execution-activity.md).

## <a name="prerequisites"></a>Vereisten
Dit document wordt ervan uitgegaan dat u een Azure-abonnement, een opslagaccount en de bijbehorende opslagsleutel Hallo voor dat account hebt. Voordat u gaat gegevens uploaden/downloaden, moet u weten Azure naam en sleutel van uw opslagaccount.

* Zie tooset van een Azure-abonnement [gratis proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).
* Zie voor instructies over het maken van een opslagaccount en voor het ophalen van de account en sleutelgegevens [over Azure storage-accounts](../storage/common/storage-create-storage-account.md).

