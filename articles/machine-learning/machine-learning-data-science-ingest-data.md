---
title: Gegevens laden in Azure storage-omgevingen voor analyses | Microsoft Docs
description: Gegevens verplaatsen van en naar Azure Blob-opslag
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
ms.openlocfilehash: 7fbf3bfedca8fa57a5e9428c9399558992b4acbd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-into-storage-environments-for-analytics"></a><span data-ttu-id="171a9-103">Gegevens voor analysedoeleinden in opslagomgevingen laden</span><span class="sxs-lookup"><span data-stu-id="171a9-103">Load data into storage environments for analytics</span></span>
<span data-ttu-id="171a9-104">Het Team gegevens wetenschap proces vereist dat gegevens worden ingenomen of in verschillende omgevingen voor andere opslag worden verwerkt of geanalyseerd in het meest geschikt in elke fase van het proces van geladen.</span><span class="sxs-lookup"><span data-stu-id="171a9-104">The Team Data Science Process requires that data be ingested or loaded into a variety of different storage environments to be processed or analyzed in the most appropriate way in each stage of the process.</span></span> <span data-ttu-id="171a9-105">Gegevensbestemmingen meestal gebruikt voor verwerking bevatten Azure Blob Storage, Azure SQL-databases en SQL Server op virtuele machine in Azure HDInsight (Hadoop) en Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="171a9-105">Data destinations commonly used for processing include Azure Blob Storage, SQL Azure databases, SQL Server on Azure VM, HDInsight (Hadoop), and Azure Machine Learning.</span></span> 

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<span data-ttu-id="171a9-106">Dit **menu** koppelingen naar onderwerpen waarin wordt beschreven hoe u opnemen van gegevens in deze omgevingen waarin de gegevens worden opgeslagen en verwerkt als doel.</span><span class="sxs-lookup"><span data-stu-id="171a9-106">This **menu** links to topics that describe how to ingest data into these target environments where the data is stored and processed.</span></span>

<span data-ttu-id="171a9-107">Technische en zakelijke behoeften, evenals de initiële locatie opmaken en de doel-omgevingen waarin de gegevens worden ingenomen moeten zodat de doelstellingen van uw analyse wordt bepaald door de grootte van uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="171a9-107">Technical and business needs, as well as the initial location, format and size of your data will determine the target environments into which the data needs to be ingested to achieve the goals of your analysis.</span></span> <span data-ttu-id="171a9-108">Het is niet ongewoon is voor een scenario dat gegevens worden verplaatst tussen de verschillende omgevingen voor de verschillende taken die zijn vereist om een Voorspellend model samen te stellen.</span><span class="sxs-lookup"><span data-stu-id="171a9-108">It is not uncommon for a scenario to require data to be moved between several environments to achieve the variety of tasks required to construct a predictive model.</span></span> <span data-ttu-id="171a9-109">Deze reeks taken kan bijvoorbeeld bevatten gegevensverkenning, vooraf verwerken, opruimen, omlaag steekproeven en training model.</span><span class="sxs-lookup"><span data-stu-id="171a9-109">This sequence of tasks can include, for example, data exploration, pre-processing, cleaning, down-sampling, and model training.</span></span>

