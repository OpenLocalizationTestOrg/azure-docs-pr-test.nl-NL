---
title: Voorbeeldgegevens in Azure blob-containers, SQL Server en Hive-tabellen | Microsoft Docs
description: Hoe gegevens die zijn opgeslagen in verschillende Azure enviromnents verkennen.
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
ms.openlocfilehash: 0683be564a88ef54882e8d882d196851ecac243d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="be022-103"><a name="heading"></a>Voorbeeldgegevens in Azure blob-containers, SQL Server en Hive-tabellen</span><span class="sxs-lookup"><span data-stu-id="be022-103"><a name="heading"></a>Sample data in Azure blob containers, SQL Server, and Hive tables</span></span>
<span data-ttu-id="be022-104">Dit bevat documentkoppelingen naar onderwerpen die wordt beschreven hoe u voorbeeldgegevens die zijn opgeslagen in een van drie verschillende Azure locaties:</span><span class="sxs-lookup"><span data-stu-id="be022-104">This document links to topics that covers how to sample data that is stored in one of three different Azure locations:</span></span>

* <span data-ttu-id="be022-105">**Azure blob-containergegevens** is door actieve programmatisch downloaden en deze vervolgens een steekproef met Python voorbeeldcode.</span><span class="sxs-lookup"><span data-stu-id="be022-105">**Azure blob container data** is sampled by downloading it programmatically and then sampling it with sample Python code.</span></span>
* <span data-ttu-id="be022-106">**SQL Server-gegevens** is door actieve met zowel SQL als de taal voor het programmeren van Python.</span><span class="sxs-lookup"><span data-stu-id="be022-106">**SQL Server data** is sampled using both SQL and the Python Programming Language.</span></span> 
* <span data-ttu-id="be022-107">**Hive-tabelgegevens** is door actieve met behulp van Hive-query's.</span><span class="sxs-lookup"><span data-stu-id="be022-107">**Hive table data** is sampled using Hive queries.</span></span>

<span data-ttu-id="be022-108">De volgende **menu** koppelingen naar de onderwerpen waarin wordt beschreven hoe u voorbeeldgegevens van elk van deze Azure-opslag-omgevingen.</span><span class="sxs-lookup"><span data-stu-id="be022-108">The following **menu** links to the topics that describe how to sample data from each of these Azure storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="be022-109">Deze taak steekproeven is een stap in de [Team gegevens wetenschap proces (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="be022-109">This sampling task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

<span data-ttu-id="be022-110">**Waarom voorbeeldgegevens?**</span><span class="sxs-lookup"><span data-stu-id="be022-110">**Why sample data?**</span></span>

<span data-ttu-id="be022-111">Als de gegevensset die u wilt analyseren groot is, is het meestal een goed idee om de gegevens om deze aan de grootte van een kleinere maar representatief en gemakkelijker down-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="be022-111">If the dataset you plan to analyze is large, it's usually a good idea to down-sample the data to reduce it to a smaller but representative and more manageable size.</span></span> <span data-ttu-id="be022-112">Dit vereenvoudigt het begrip van de gegevens, exploratie en functie-engineering.</span><span class="sxs-lookup"><span data-stu-id="be022-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="be022-113">De rol in de Cortana-Analytics-proces is om in te schakelen snel maken van een prototype van de functies voor het verwerken van gegevens en machine learning-modellen.</span><span class="sxs-lookup"><span data-stu-id="be022-113">Its role in the Cortana Analytics Process is to enable fast prototyping of the data processing functions and machine learning models.</span></span>

