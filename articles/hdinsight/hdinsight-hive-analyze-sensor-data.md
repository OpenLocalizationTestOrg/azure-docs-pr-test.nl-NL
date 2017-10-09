---
title: aaaAnalyze sensorgegevens met behulp van Hive en Hadoop - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe tooanalyze sensorgegevens met behulp van Hallo Query Console Hive met HDInsight (Hadoop) en vervolgens visualiseren Hallo-gegevens in Microsoft Excel met PowerView.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: a8ac160c-1cef-45d9-bf36-7beb5a439105
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/14/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 70e595705c33d9835dc9809161f79c3ac5ece870
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-sensor-data-using-hello-hive-query-console-on-hadoop-in-hdinsight"></a><span data-ttu-id="490d6-103">Hallo Hive-Query-Console gebruiken met Hadoop in HDInsight-sensorgegevens analyseren</span><span class="sxs-lookup"><span data-stu-id="490d6-103">Analyze sensor data using hello Hive Query Console on Hadoop in HDInsight</span></span>

<span data-ttu-id="490d6-104">Meer informatie over hoe tooanalyze sensorgegevens met behulp van Hallo Query Console Hive met HDInsight (Hadoop) en vervolgens Hallo-gegevens in Microsoft Excel visualiseren met behulp van Power View.</span><span class="sxs-lookup"><span data-stu-id="490d6-104">Learn how tooanalyze sensor data by using hello Hive Query Console with HDInsight (Hadoop), then visualize hello data in Microsoft Excel by using Power View.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="490d6-105">Hallo stappen in dit document alleen werken met HDInsight op basis van Windows-clusters.</span><span class="sxs-lookup"><span data-stu-id="490d6-105">hello steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="490d6-106">HDInsight is alleen beschikbaar in Windows voor versies lager is dan HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="490d6-106">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="490d6-107">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="490d6-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="490d6-108">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="490d6-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>


<span data-ttu-id="490d6-109">In dit voorbeeld gebruikt u Hive tooprocess historische gegevens en identificeren van problemen met verwarming en airconditioning systemen.</span><span class="sxs-lookup"><span data-stu-id="490d6-109">In this sample, you use Hive tooprocess historical data and identify problems with heating and air conditioning systems.</span></span> <span data-ttu-id="490d6-110">In het bijzonder het identificeren van systemen zijn tooreliably kan niet een set temperaturen onderhouden door Hallo volgende taken uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="490d6-110">Specifically, you identify systems are not able tooreliably maintain a set temperature by performing hello following tasks:</span></span>

* <span data-ttu-id="490d6-111">Maken van HIVE-tabellen tooquery opgeslagen gegevens in bestanden met door komma's gescheiden waarden (CSV).</span><span class="sxs-lookup"><span data-stu-id="490d6-111">Create HIVE tables tooquery data stored in comma-separated value (CSV) files.</span></span>
* <span data-ttu-id="490d6-112">HIVE-query's tooanalyze Hallo gegevens maken.</span><span class="sxs-lookup"><span data-stu-id="490d6-112">Create HIVE queries tooanalyze hello data.</span></span>
* <span data-ttu-id="490d6-113">tooretrieve hello geanalyseerd gegevens, gebruikt u Microsoft Excel tooconnect tooHDInsight.</span><span class="sxs-lookup"><span data-stu-id="490d6-113">tooretrieve hello analyzed data, use Microsoft Excel tooconnect tooHDInsight.</span></span>
* <span data-ttu-id="490d6-114">toovisualize hello gegevens, gebruikt u Power View.</span><span class="sxs-lookup"><span data-stu-id="490d6-114">toovisualize hello data, use Power View.</span></span>

![Een diagram van architectuur Hallo-oplossing](./media/hdinsight-hive-analyze-sensor-data/hvac-architecture.png)

## <a name="prerequisites"></a><span data-ttu-id="490d6-116">Vereisten</span><span class="sxs-lookup"><span data-stu-id="490d6-116">Prerequisites</span></span>

* <span data-ttu-id="490d6-117">Een HDInsight (Hadoop)-cluster: Zie [maken Hadoop-clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md) voor meer informatie over het maken van een cluster.</span><span class="sxs-lookup"><span data-stu-id="490d6-117">An HDInsight (Hadoop) cluster: See [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md) for information about creating a cluster.</span></span>
* <span data-ttu-id="490d6-118">Microsoft Excel 2013</span><span class="sxs-lookup"><span data-stu-id="490d6-118">Microsoft Excel 2013</span></span>

  > [!NOTE]
  > <span data-ttu-id="490d6-119">Microsoft Excel wordt gebruikt voor gegevensvisualisatie met [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).</span><span class="sxs-lookup"><span data-stu-id="490d6-119">Microsoft Excel is used for data visualization with [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).</span></span>

* [<span data-ttu-id="490d6-120">Microsoft Hive ODBC-stuurprogramma</span><span class="sxs-lookup"><span data-stu-id="490d6-120">Microsoft Hive ODBC Driver</span></span>](http://www.microsoft.com/download/details.aspx?id=40886)

## <a name="toorun-hello-sample"></a><span data-ttu-id="490d6-121">toorun Hallo-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="490d6-121">toorun hello sample</span></span>

1. <span data-ttu-id="490d6-122">Navigeer vanuit de webbrowser toohello volgende URL:</span><span class="sxs-lookup"><span data-stu-id="490d6-122">From your web browser, navigate toohello following URL:</span></span> 

         https://<clustername>.azurehdinsight.net

    <span data-ttu-id="490d6-123">Vervang `<clustername>` met Hallo-naam van uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="490d6-123">Replace `<clustername>` with hello name of your HDInsight cluster.</span></span>

    <span data-ttu-id="490d6-124">Wanneer u wordt gevraagd, kunt u verifiëren met behulp van Hallo beheerder-gebruikersnaam en wachtwoord die u hebt gebruikt bij het inrichten van dit cluster.</span><span class="sxs-lookup"><span data-stu-id="490d6-124">When prompted, authenticate by using hello administrator user name and password you used when provisioning this cluster.</span></span>

2. <span data-ttu-id="490d6-125">Van de webpagina Hallo dat wordt geopend, klikt u op Hallo **Getting Started galerie** tabblad en klik vervolgens onder Hallo **oplossingen met voorbeeldgegevens** categorie, klikt u op Hallo **Sensor Data-analyse** voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="490d6-125">From hello web page that opens, click hello **Getting Started Gallery** tab, and then under hello **Solutions with Sample Data** category, click hello **Sensor Data Analysis** sample.</span></span>

    ![Gestarte afbeelding ophalen](./media/hdinsight-hive-analyze-sensor-data/getting-started-gallery.png)

3. <span data-ttu-id="490d6-127">Volg de aanwijzingen Hallo van Hallo webpagina toofinish Hallo steekproef.</span><span class="sxs-lookup"><span data-stu-id="490d6-127">Follow hello instructions provided on hello web page toofinish hello sample.</span></span>
