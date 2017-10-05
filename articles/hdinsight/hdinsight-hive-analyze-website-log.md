---
title: Hive gebruiken met Hadoop voor websitelogboekanalyse - Azure HDInsight | Microsoft Docs
description: Informatie over het gebruik van Hive met HDInsight websitelogboeken analyseren. U hebt een logboekbestand gebruiken als invoer in een tabel met HDInsight en HiveQL gebruiken voor het opvragen van de gegevens.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6fb7b5c2-8df4-40b1-a9e2-6815080004f9
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/17/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: e1cdb786bb6049980aafc0213abf53013e342618
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-hive-with-windows-based-hdinsight-to-analyze-logs-from-websites"></a><span data-ttu-id="b0f7e-104">Hive gebruiken met HDInsight op basis van Windows logboeken van websites te analyseren</span><span class="sxs-lookup"><span data-stu-id="b0f7e-104">Use Hive with Windows-based HDInsight to analyze logs from websites</span></span>
<span data-ttu-id="b0f7e-105">Informatie over het HiveQL gebruiken met HDInsight voor het analyseren van Logboeken vanaf een website.</span><span class="sxs-lookup"><span data-stu-id="b0f7e-105">Learn how to use HiveQL with HDInsight to analyze logs from a website.</span></span> <span data-ttu-id="b0f7e-106">Websitelogboekanalyse kan worden gebruikt om segmenteren van uw doelgroep op basis van soortgelijke activiteiten, demografische gegevens van bezoekers categoriseren en wilt weten de inhoud ze weergeven, de websites die ze afkomstig zijn van, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="b0f7e-106">Website log analysis can be used to segment your audience based on similar activities, categorize site visitors by demographics, and to find out the content they view, the websites they come from, and so on.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b0f7e-107">De stappen in dit document wordt alleen werken met HDInsight op basis van Windows-clusters.</span><span class="sxs-lookup"><span data-stu-id="b0f7e-107">The steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="b0f7e-108">HDInsight is alleen beschikbaar in Windows voor versies lager is dan HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="b0f7e-108">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="b0f7e-109">Linux is het enige besturingssysteem dat wordt gebruikt in HDInsight-versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="b0f7e-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="b0f7e-110">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="b0f7e-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="b0f7e-111">In dit voorbeeld gebruikt u een HDInsight-cluster voor het analyseren van de logboekbestanden van de website om inzicht te krijgen in de frequentie van bezoeken van externe websites in een dag naar de website.</span><span class="sxs-lookup"><span data-stu-id="b0f7e-111">In this sample, you will use an HDInsight cluster to analyze website log files to get insight into the frequency of visits to the website from external websites in a day.</span></span> <span data-ttu-id="b0f7e-112">Ook genereert u een overzicht van website-fouten die optreden van de gebruikers.</span><span class="sxs-lookup"><span data-stu-id="b0f7e-112">You'll also generate a summary of website errors that the users experience.</span></span> <span data-ttu-id="b0f7e-113">U leert hoe:</span><span class="sxs-lookup"><span data-stu-id="b0f7e-113">You will learn how to:</span></span>

* <span data-ttu-id="b0f7e-114">Verbinding maken met een Azure Blob storage, bevat de logboekbestanden van de website.</span><span class="sxs-lookup"><span data-stu-id="b0f7e-114">Connect to a Azure Blob storage, which contains website log files.</span></span>
* <span data-ttu-id="b0f7e-115">HIVE-tabellen om op te vragen deze logboeken maken.</span><span class="sxs-lookup"><span data-stu-id="b0f7e-115">Create HIVE tables to query those logs.</span></span>
* <span data-ttu-id="b0f7e-116">Maak HIVE-query's om de gegevens te analyseren.</span><span class="sxs-lookup"><span data-stu-id="b0f7e-116">Create HIVE queries to analyze the data.</span></span>
* <span data-ttu-id="b0f7e-117">Microsoft Excel gebruiken voor verbinding met HDInsight (met behulp van (ODBC) open database connectivity geanalyseerde gegevens ophalen.</span><span class="sxs-lookup"><span data-stu-id="b0f7e-117">Use Microsoft Excel to connect to HDInsight (by using open database connectivity (ODBC) to retrieve the analyzed data.</span></span>

![HDI. Samples.Website.Log.Analysis][img-hdi-weblogs-sample]

## <a name="prerequisites"></a><span data-ttu-id="b0f7e-119">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b0f7e-119">Prerequisites</span></span>
* <span data-ttu-id="b0f7e-120">U moet een Hadoop-cluster in Azure HDInsight hebt ingericht.</span><span class="sxs-lookup"><span data-stu-id="b0f7e-120">You must have provisioned a Hadoop cluster on Azure HDInsight.</span></span> <span data-ttu-id="b0f7e-121">Zie voor instructies [HDInsight-Clusters inrichten][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="b0f7e-121">For instructions, see [Provision HDInsight Clusters][hdinsight-provision].</span></span>
* <span data-ttu-id="b0f7e-122">U moet Microsoft Excel 2013 of Excel 2010 is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="b0f7e-122">You must have Microsoft Excel 2013 or Excel 2010 installed.</span></span>
* <span data-ttu-id="b0f7e-123">U moet hebben [stuurprogramma Microsoft Hive ODBC](http://www.microsoft.com/download/details.aspx?id=40886) gegevens importeren uit Hive in Excel.</span><span class="sxs-lookup"><span data-stu-id="b0f7e-123">You must have [Microsoft Hive ODBC Driver](http://www.microsoft.com/download/details.aspx?id=40886) to import data from Hive into Excel.</span></span>

## <a name="to-run-the-sample"></a><span data-ttu-id="b0f7e-124">Het voorbeeld uitvoeren</span><span class="sxs-lookup"><span data-stu-id="b0f7e-124">To run the sample</span></span>
1. <span data-ttu-id="b0f7e-125">Van de [Azure Portal](https://portal.azure.com/), vanaf het Startboard (als u er in het cluster hebt vastgemaakt), klik op de tegel van het cluster waarop u wilt uitvoeren van het voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="b0f7e-125">From the [Azure Portal](https://portal.azure.com/), from the Startboard (if you pinned the cluster there), click the cluster tile on which you want to run the sample.</span></span>
2. <span data-ttu-id="b0f7e-126">De cluster-blade onder **snelkoppelingen**, klikt u op **Cluster-Dashboard**, en vervolgens naar de **Cluster-Dashboard** blade, klikt u op **HDInsight-Cluster Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="b0f7e-126">From the cluster blade, under **Quick Links**, click **Cluster Dashboard**, and then from the **Cluster Dashboard** blade, click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="b0f7e-127">U kunt het dashboard ook rechtstreeks openen met behulp van de volgende URL:</span><span class="sxs-lookup"><span data-stu-id="b0f7e-127">Alternatively, you can directly open the dashboard by using the following URL:</span></span>

         https://<clustername>.azurehdinsight.net

    <span data-ttu-id="b0f7e-128">Wanneer u wordt gevraagd, worden geverifieerd met behulp van de administrator-gebruikersnaam en wachtwoord waarmee u bij het inrichten van het cluster.</span><span class="sxs-lookup"><span data-stu-id="b0f7e-128">When prompted, authenticate by using the administrator user name and password you used when provisioning the cluster.</span></span>
3. <span data-ttu-id="b0f7e-129">Op de webpagina klikt u op de **Getting Started galerie** tabblad en klik vervolgens onder de **oplossingen met voorbeeldgegevens** categorie, klikt u op de **Websitelogboekanalyse** voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="b0f7e-129">From the web page that opens, click the **Getting Started Gallery** tab, and then under the **Solutions with Sample Data** category, click the **Website Log Analysis** sample.</span></span>
4. <span data-ttu-id="b0f7e-130">Volg de instructies op de pagina voor het voltooien van de steekproef.</span><span class="sxs-lookup"><span data-stu-id="b0f7e-130">Follow the instructions provided on the web page to finish the sample.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b0f7e-131">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b0f7e-131">Next steps</span></span>
<span data-ttu-id="b0f7e-132">Probeer het volgende voorbeeld: [analyseren van sensorgegevens met Hive met HDInsight](hdinsight-hive-analyze-sensor-data.md).</span><span class="sxs-lookup"><span data-stu-id="b0f7e-132">Try the following sample: [Analyzing sensor data using Hive with HDInsight](hdinsight-hive-analyze-sensor-data.md).</span></span>

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-sensor-data-sample]: ../hdinsight-use-hive-sensor-data-analysis.md

[img-hdi-weblogs-sample]: ./media/hdinsight-hive-analyze-website-log/hdinsight-weblogs-sample.png
