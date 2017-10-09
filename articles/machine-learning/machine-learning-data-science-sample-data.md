---
title: aaaSample gegevens in Azure blob-containers, SQL Server en Hive-tabellen | Microsoft Docs
description: Hoe tooexplore gegevens opgeslagen in verschillende Azure enviromnents.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 80a9dfae-e3a6-4cfb-aecc-5701cfc7e39d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: 5a5295b59fa02f91da680fc7495a92ca135e26c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="b1e21-103"><a name="heading"></a>Voorbeeldgegevens in Azure blob-containers, SQL Server en Hive-tabellen</span><span class="sxs-lookup"><span data-stu-id="b1e21-103"><a name="heading"></a>Sample data in Azure blob containers, SQL Server, and Hive tables</span></span>
<span data-ttu-id="b1e21-104">Dit document koppelingen tootopics die betrekking heeft op hoe toosample gegevens die zijn opgeslagen in een van drie verschillende Azure locaties:</span><span class="sxs-lookup"><span data-stu-id="b1e21-104">This document links tootopics that covers how toosample data that is stored in one of three different Azure locations:</span></span>

* <span data-ttu-id="b1e21-105">**Azure blob-containergegevens** is door actieve programmatisch downloaden en deze vervolgens een steekproef met Python voorbeeldcode.</span><span class="sxs-lookup"><span data-stu-id="b1e21-105">**Azure blob container data** is sampled by downloading it programmatically and then sampling it with sample Python code.</span></span>
* <span data-ttu-id="b1e21-106">**SQL Server-gegevens** is door actieve met behulp van SQL- en Hallo Python Programming taal.</span><span class="sxs-lookup"><span data-stu-id="b1e21-106">**SQL Server data** is sampled using both SQL and hello Python Programming Language.</span></span> 
* <span data-ttu-id="b1e21-107">**Hive-tabelgegevens** is door actieve met behulp van Hive-query's.</span><span class="sxs-lookup"><span data-stu-id="b1e21-107">**Hive table data** is sampled using Hive queries.</span></span>

<span data-ttu-id="b1e21-108">Hallo volgende **menu** koppelingen toohello onderwerpen waarin wordt beschreven hoe toosample gegevens van elk van deze Azure-opslag-omgevingen.</span><span class="sxs-lookup"><span data-stu-id="b1e21-108">hello following **menu** links toohello topics that describe how toosample data from each of these Azure storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="b1e21-109">Deze taak steekproeven is een stap in Hallo [Team gegevens wetenschap proces (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="b1e21-109">This sampling task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

<span data-ttu-id="b1e21-110">**Waarom voorbeeldgegevens?**</span><span class="sxs-lookup"><span data-stu-id="b1e21-110">**Why sample data?**</span></span>

<span data-ttu-id="b1e21-111">Als u van plan bent tooanalyze Hallo-gegevensset te groot is, is het meestal een goed idee Hallo toodown-sample data tooreduce het tooa kleiner, maar representatief en gemakkelijker grootte.</span><span class="sxs-lookup"><span data-stu-id="b1e21-111">If hello dataset you plan tooanalyze is large, it's usually a good idea toodown-sample hello data tooreduce it tooa smaller but representative and more manageable size.</span></span> <span data-ttu-id="b1e21-112">Dit vereenvoudigt het begrip van de gegevens, exploratie en functie-engineering.</span><span class="sxs-lookup"><span data-stu-id="b1e21-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="b1e21-113">De rol in Hallo Cortana-Analytics-proces is tooenable snel maken van een prototype van Hallo gegevensverwerking functies en machine learning-modellen.</span><span class="sxs-lookup"><span data-stu-id="b1e21-113">Its role in hello Cortana Analytics Process is tooenable fast prototyping of hello data processing functions and machine learning models.</span></span>

