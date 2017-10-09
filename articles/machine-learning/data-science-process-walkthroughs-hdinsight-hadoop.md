---
title: aaaHDInsight Hadoop gegevens wetenschap-scenario's met Hive in Azure | Microsoft Docs
description: Voorbeelden van Hallo Team gegevens wetenschappelijke processen die u bij het gebruik van Hive Hallo op Azure HDInsight Hadoop toodo predictive analytics helpt.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: bradsev
ms.openlocfilehash: 77efbe4ea6377f309987849d9f44e8b2b859ae9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="hdinsight-hadoop-data-science-walkthroughs-using-hive-on-azure"></a><span data-ttu-id="4b3a6-103">HDInsight Hadoop-gegevens wetenschappelijke scenario's met Hive in Azure</span><span class="sxs-lookup"><span data-stu-id="4b3a6-103">HDInsight Hadoop data science walkthroughs using Hive on Azure</span></span> 

<span data-ttu-id="4b3a6-104">Deze scenario's Hive gebruiken met een HDInsight Hadoop-cluster toodo predictive analytics.</span><span class="sxs-lookup"><span data-stu-id="4b3a6-104">These walkthroughs use Hive with an HDInsight Hadoop cluster toodo predictive analytics.</span></span> <span data-ttu-id="4b3a6-105">Deze stappen Hallo die worden beschreven in Hallo Team gegevens wetenschappelijke processen.</span><span class="sxs-lookup"><span data-stu-id="4b3a6-105">They follow hello steps outlined in hello Team Data Science Process.</span></span> <span data-ttu-id="4b3a6-106">Zie voor een overzicht van Hallo Team gegevens wetenschap proces [gegevens wetenschap proces](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4b3a6-106">For an overview of hello Team Data Science Process, see [Data Science Process](data-science-process-overview.md).</span></span> <span data-ttu-id="4b3a6-107">Zie voor een inleiding tooAzure HDInsight, [inleiding tooAzure HDInsight worden Hadoop-technologiestack en Hadoop-clusters Hallo](../hdinsight/hdinsight-hadoop-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4b3a6-107">For an introduction tooAzure HDInsight, see [Introduction tooAzure HDInsight, hello Hadoop technology stack, and Hadoop clusters](../hdinsight/hdinsight-hadoop-introduction.md).</span></span>

<span data-ttu-id="4b3a6-108">Aanvullende gegevens wetenschap-scenario's die worden uitgevoerd Hallo Team gegevens wetenschappelijke processen zijn gegroepeerd op Hallo **platform** die ze gebruiken:</span><span class="sxs-lookup"><span data-stu-id="4b3a6-108">Additional data science walkthroughs that execute hello Team Data Science Process are grouped by hello **platform** that they use:</span></span> 

[!INCLUDE [tdsp-walkthroughs-by-platform](../../includes/tdsp-walkthroughs-by-platform.md)]


## <a name="predict-taxi-tips-using-hive-with-hdinsight-hadoop"></a><span data-ttu-id="4b3a6-109">Voorspellen taxi tips voor het gebruik van Hive met HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="4b3a6-109">Predict taxi tips using Hive with HDInsight Hadoop</span></span>

<span data-ttu-id="4b3a6-110">Hallo [gebruik HDInsight Hadoop-clusters](machine-learning-data-science-process-hive-walkthrough.md) Stapsgewijze instructies wordt gebruikgemaakt van gegevens van de New York taxi's toopredict:</span><span class="sxs-lookup"><span data-stu-id="4b3a6-110">hello [Use HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md) walkthrough uses data from New York taxis toopredict:</span></span> 

- <span data-ttu-id="4b3a6-111">Hiermee wordt aangegeven of een tip wordt betaald</span><span class="sxs-lookup"><span data-stu-id="4b3a6-111">Whether a tip is paid</span></span> 
- <span data-ttu-id="4b3a6-112">Hallo-distributie van tip bedragen</span><span class="sxs-lookup"><span data-stu-id="4b3a6-112">hello distribution of tip amounts</span></span>

<span data-ttu-id="4b3a6-113">Hallo-scenario is geïmplementeerd met behulp van Hive met een [Azure HDInsight Hadoop-cluster](https://azure.microsoft.com/services/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="4b3a6-113">hello scenario is implemented using Hive with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/).</span></span> <span data-ttu-id="4b3a6-114">U leert hoe toostore, verkennen, en functie-engineering-gegevens van een openbaar NYC taxi reis en ritbedrag gegevensset.</span><span class="sxs-lookup"><span data-stu-id="4b3a6-114">You learn how toostore, explore, and feature engineer data from a publicly available NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="4b3a6-115">U ook gebruik van Azure Machine Learning toobuild en Hallo modellen implementeren.</span><span class="sxs-lookup"><span data-stu-id="4b3a6-115">You also use Azure Machine Learning toobuild and deploy hello models.</span></span>

## <a name="predict-advertisement-clicks-using-hive-with-hdinsight-hadoop"></a><span data-ttu-id="4b3a6-116">Aankondiging klikt op het gebruik van Hive met HDInsight Hadoop voorspellen</span><span class="sxs-lookup"><span data-stu-id="4b3a6-116">Predict advertisement clicks using Hive with HDInsight Hadoop</span></span>

<span data-ttu-id="4b3a6-117">Hallo [gebruik Azure HDInsight Hadoop-Clusters op een gegevensset 1 TB](machine-learning-data-science-process-hive-criteo-walkthrough.md) scenario maakt gebruik van een openbaar beschikbare [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) gegevensset toopredict klikt u op of een tip wordt betaald en Hallo diverse bedragen verwacht.</span><span class="sxs-lookup"><span data-stu-id="4b3a6-117">hello [Use Azure HDInsight Hadoop Clusters on a 1-TB dataset](machine-learning-data-science-process-hive-criteo-walkthrough.md) walkthrough uses a publicly available [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) click dataset toopredict whether a tip is paid and hello range of amounts expected.</span></span> <span data-ttu-id="4b3a6-118">Hallo-scenario is geïmplementeerd met behulp van Hive met een [Azure HDInsight Hadoop-cluster](https://azure.microsoft.com/services/hdinsight/) toostore, verkennen, functie engineer van en naar beneden voorbeeldgegevens.</span><span class="sxs-lookup"><span data-stu-id="4b3a6-118">hello scenario is implemented using Hive with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) toostore, explore, feature engineer, and down sample data.</span></span> <span data-ttu-id="4b3a6-119">Azure Machine Learning toobuild wordt gebruikt, te trainen en beoordelen van een binaire indeling model voorspellen of een gebruiker op een advertentie klikt.</span><span class="sxs-lookup"><span data-stu-id="4b3a6-119">It uses Azure Machine Learning toobuild, train, and score a binary classification model predicting whether a user clicks on an advertisement.</span></span> <span data-ttu-id="4b3a6-120">Hallo scenario concludeert de domeincontroller die weergeeft hoe toopublish een van deze modellen als een webservice.</span><span class="sxs-lookup"><span data-stu-id="4b3a6-120">hello walkthrough concludes showing how toopublish one of these models as a Web service.</span></span>


## <a name="next-steps"></a><span data-ttu-id="4b3a6-121">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4b3a6-121">Next steps</span></span>

<span data-ttu-id="4b3a6-122">Zie voor een beschrijving van de belangrijke onderdelen Hallo waaruit Hallo Team gegevens wetenschappelijke processen, [Team gegevens wetenschappelijke procesoverzicht](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4b3a6-122">For a discussion of hello key components that comprise hello Team Data Science Process, see [Team Data Science Process overview](data-science-process-overview.md).</span></span>

<span data-ttu-id="4b3a6-123">Zie voor een beschrijving van de levenscyclus van Hallo Team gegevens wetenschappelijke processen waarmee u toostructure kunt gegevens wetenschappelijke projecten, [Team gegevens wetenschap proces lifecycle](data-science-process-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="4b3a6-123">For a discussion of hello Team Data Science Process lifecycle that you can use toostructure your data science projects, see [Team Data Science Process lifecycle](data-science-process-lifecycle.md).</span></span> <span data-ttu-id="4b3a6-124">Hallo lifecycle bevat een overzicht van Hallo stappen van de start-toofinish die projecten meestal volgt wanneer ze worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4b3a6-124">hello lifecycle outlines hello steps, from start toofinish, that projects usually follow when they are executed.</span></span> 

