---
title: aaaLoad gegevens in Azure storage-omgevingen voor analyses | Microsoft Docs
description: Verplaatsen van gegevens tooand uit Azure Blob Storage
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b8fbef77-3e80-4911-8e84-23dbf42c9bee
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 0fea2290991f9fa63d9e46c3a657000e27d95289
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-storage-environments-for-analytics"></a><span data-ttu-id="af8c8-103">Gegevens voor analysedoeleinden in opslagomgevingen laden</span><span class="sxs-lookup"><span data-stu-id="af8c8-103">Load data into storage environments for analytics</span></span>
<span data-ttu-id="af8c8-104">Hallo Team gegevens wetenschap proces vereist dat gegevens worden ingenomen of geladen in tal van andere opslag omgevingen toobe verwerkt of geanalyseerd op de meest geschikte manier Hallo in elke fase van het Hallo-proces.</span><span class="sxs-lookup"><span data-stu-id="af8c8-104">hello Team Data Science Process requires that data be ingested or loaded into a variety of different storage environments toobe processed or analyzed in hello most appropriate way in each stage of hello process.</span></span> <span data-ttu-id="af8c8-105">Gegevensbestemmingen meestal gebruikt voor verwerking bevatten Azure Blob Storage, Azure SQL-databases en SQL Server op virtuele machine in Azure HDInsight (Hadoop) en Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="af8c8-105">Data destinations commonly used for processing include Azure Blob Storage, SQL Azure databases, SQL Server on Azure VM, HDInsight (Hadoop), and Azure Machine Learning.</span></span> 

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<span data-ttu-id="af8c8-106">Dit **menu** tootopics waarin wordt beschreven hoe gegevens in een van deze tooingest omgevingen waar Hallo gegevens worden opgeslagen en verwerkt als doel is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="af8c8-106">This **menu** links tootopics that describe how tooingest data into these target environments where hello data is stored and processed.</span></span>

<span data-ttu-id="af8c8-107">Technische en zakelijke behoeften, evenals de initiële locatie hello, opmaken en de grootte van uw gegevens Hallo doel omgevingen in welke Hallo gegevens toobe ingenomen tooachieve Hallo doelstellingen van de analyse moeten wordt bepaald.</span><span class="sxs-lookup"><span data-stu-id="af8c8-107">Technical and business needs, as well as hello initial location, format and size of your data will determine hello target environments into which hello data needs toobe ingested tooachieve hello goals of your analysis.</span></span> <span data-ttu-id="af8c8-108">Het is niet ongewoon is voor een scenario toorequire gegevens toobe verplaatst tussen de verschillende omgevingen tooachieve Hallo diverse taken vereist tooconstruct een Voorspellend model.</span><span class="sxs-lookup"><span data-stu-id="af8c8-108">It is not uncommon for a scenario toorequire data toobe moved between several environments tooachieve hello variety of tasks required tooconstruct a predictive model.</span></span> <span data-ttu-id="af8c8-109">Deze reeks taken kan bijvoorbeeld bevatten gegevensverkenning, vooraf verwerken, opruimen, omlaag steekproeven en training model.</span><span class="sxs-lookup"><span data-stu-id="af8c8-109">This sequence of tasks can include, for example, data exploration, pre-processing, cleaning, down-sampling, and model training.</span></span>

