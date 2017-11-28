---
title: HDInsight Hadoop-gegevens wetenschappelijke scenario's met Hive in Azure | Microsoft Docs
description: Voorbeelden van het Team gegevens wetenschap proces om op Azure HDInsight Hadoop predictive analytics doen door het gebruik van Hive.
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
ms.openlocfilehash: fb06c3c1b1ae30d970a2e4d45a49e22e9d78b876
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="hdinsight-hadoop-data-science-walkthroughs-using-hive-on-azure"></a><span data-ttu-id="7590f-103">HDInsight Hadoop-gegevens wetenschappelijke scenario's met Hive in Azure</span><span class="sxs-lookup"><span data-stu-id="7590f-103">HDInsight Hadoop data science walkthroughs using Hive on Azure</span></span> 

<span data-ttu-id="7590f-104">Deze scenario's voor het gebruik van Hive met HDInsight Hadoop-cluster voor predictive analytics.</span><span class="sxs-lookup"><span data-stu-id="7590f-104">These walkthroughs use Hive with an HDInsight Hadoop cluster to do predictive analytics.</span></span> <span data-ttu-id="7590f-105">Ze stappen de die worden beschreven in de procedure voor wetenschappelijke gegevens Team.</span><span class="sxs-lookup"><span data-stu-id="7590f-105">They follow the steps outlined in the Team Data Science Process.</span></span> <span data-ttu-id="7590f-106">Zie voor een overzicht van het Team gegevens wetenschap proces [gegevens wetenschap proces](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7590f-106">For an overview of the Team Data Science Process, see [Data Science Process](data-science-process-overview.md).</span></span> <span data-ttu-id="7590f-107">Zie voor een inleiding tot Azure HDInsight, [Inleiding tot Azure HDInsight, het Hadoop-technologiestack en Hadoop-clusters](../hdinsight/hdinsight-hadoop-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7590f-107">For an introduction to Azure HDInsight, see [Introduction to Azure HDInsight, the Hadoop technology stack, and Hadoop clusters](../hdinsight/hdinsight-hadoop-introduction.md).</span></span>

<span data-ttu-id="7590f-108">Aanvullende gegevens wetenschap-scenario's die het Team gegevens wetenschap proces worden uitgevoerd zijn gegroepeerd op de **platform** die ze gebruiken:</span><span class="sxs-lookup"><span data-stu-id="7590f-108">Additional data science walkthroughs that execute the Team Data Science Process are grouped by the **platform** that they use:</span></span> 

[!INCLUDE [tdsp-walkthroughs-by-platform](../../includes/tdsp-walkthroughs-by-platform.md)]


## <a name="predict-taxi-tips-using-hive-with-hdinsight-hadoop"></a><span data-ttu-id="7590f-109">Voorspellen taxi tips voor het gebruik van Hive met HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="7590f-109">Predict taxi tips using Hive with HDInsight Hadoop</span></span>

<span data-ttu-id="7590f-110">De [gebruik HDInsight Hadoop-clusters](machine-learning-data-science-process-hive-walkthrough.md) Stapsgewijze instructies wordt gebruikgemaakt van gegevens van de New York taxi's te voorspellen:</span><span class="sxs-lookup"><span data-stu-id="7590f-110">The [Use HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md) walkthrough uses data from New York taxis to predict:</span></span> 

- <span data-ttu-id="7590f-111">Hiermee wordt aangegeven of een tip wordt betaald</span><span class="sxs-lookup"><span data-stu-id="7590f-111">Whether a tip is paid</span></span> 
- <span data-ttu-id="7590f-112">De verdeling van tip bedragen</span><span class="sxs-lookup"><span data-stu-id="7590f-112">The distribution of tip amounts</span></span>

<span data-ttu-id="7590f-113">Het scenario is geïmplementeerd met behulp van Hive met een [Azure HDInsight Hadoop-cluster](https://azure.microsoft.com/services/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="7590f-113">The scenario is implemented using Hive with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/).</span></span> <span data-ttu-id="7590f-114">U informatie over het verkennen om op te slaan en gegevens van de functie engineer van een openbaar NYC taxi reis en tarief gegevensset.</span><span class="sxs-lookup"><span data-stu-id="7590f-114">You learn how to store, explore, and feature engineer data from a publicly available NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="7590f-115">U kunt ook Azure Machine Learning gebruiken om te bouwen en implementeren van de modellen.</span><span class="sxs-lookup"><span data-stu-id="7590f-115">You also use Azure Machine Learning to build and deploy the models.</span></span>

## <a name="predict-advertisement-clicks-using-hive-with-hdinsight-hadoop"></a><span data-ttu-id="7590f-116">Aankondiging klikt op het gebruik van Hive met HDInsight Hadoop voorspellen</span><span class="sxs-lookup"><span data-stu-id="7590f-116">Predict advertisement clicks using Hive with HDInsight Hadoop</span></span>

<span data-ttu-id="7590f-117">De [gebruik Azure HDInsight Hadoop-Clusters op een gegevensset 1 TB](machine-learning-data-science-process-hive-criteo-walkthrough.md) scenario maakt gebruik van een openbaar beschikbare [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) klikt u op dataset om te voorspellen of een tip wordt betaald en het bereik van bedragen verwacht.</span><span class="sxs-lookup"><span data-stu-id="7590f-117">The [Use Azure HDInsight Hadoop Clusters on a 1-TB dataset](machine-learning-data-science-process-hive-criteo-walkthrough.md) walkthrough uses a publicly available [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) click dataset to predict whether a tip is paid and the range of amounts expected.</span></span> <span data-ttu-id="7590f-118">Het scenario is geïmplementeerd met behulp van Hive met een [Azure HDInsight Hadoop-cluster](https://azure.microsoft.com/services/hdinsight/) om op te slaan, verkennen, functie engineer van en naar beneden voorbeeldgegevens.</span><span class="sxs-lookup"><span data-stu-id="7590f-118">The scenario is implemented using Hive with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) to store, explore, feature engineer, and down sample data.</span></span> <span data-ttu-id="7590f-119">Azure Machine Learning wordt gebruikt om te bouwen, te trainen en te voorspellen of een gebruiker op een advertentie klikt binaire classificatie model beoordelen.</span><span class="sxs-lookup"><span data-stu-id="7590f-119">It uses Azure Machine Learning to build, train, and score a binary classification model predicting whether a user clicks on an advertisement.</span></span> <span data-ttu-id="7590f-120">Deze stapsgewijze Kennismaking concludeert de domeincontroller die laat zien hoe u een van deze modellen als een webservice publiceert.</span><span class="sxs-lookup"><span data-stu-id="7590f-120">The walkthrough concludes showing how to publish one of these models as a Web service.</span></span>


## <a name="next-steps"></a><span data-ttu-id="7590f-121">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7590f-121">Next steps</span></span>

<span data-ttu-id="7590f-122">Zie voor een bespreking van de belangrijke onderdelen waaruit het Team gegevens wetenschap proces [Team gegevens wetenschappelijke procesoverzicht](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7590f-122">For a discussion of the key components that comprise the Team Data Science Process, see [Team Data Science Process overview](data-science-process-overview.md).</span></span>

<span data-ttu-id="7590f-123">Zie voor een bespreking van de levensduur van het Team gegevens wetenschappelijke processen die u gebruiken kunt voor de structuur van uw gegevens wetenschappelijke projecten [Team gegevens wetenschap proces lifecycle](data-science-process-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="7590f-123">For a discussion of the Team Data Science Process lifecycle that you can use to structure your data science projects, see [Team Data Science Process lifecycle](data-science-process-lifecycle.md).</span></span> <span data-ttu-id="7590f-124">De levenscyclus van bevat de stappen, van begin tot eind, projecten meestal volgen wanneer ze worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7590f-124">The lifecycle outlines the steps, from start to finish, that projects usually follow when they are executed.</span></span> 

