---
title: aaaExplore gegevens in de Hive-tabellen met Hive-query's | Microsoft Docs
description: Verken de gegevens in de Hive-tabellen met Hive-query's.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 0d46cea5-2b4c-4384-9bfa-fa20f6f75148
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 2ede3d41682aa08ced19284f7a83ec95e0c2a93a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="explore-data-in-hive-tables-with-hive-queries"></a><span data-ttu-id="8c7cd-103">Gegevens in Hive-tabellen verkennen met Hive-query's</span><span class="sxs-lookup"><span data-stu-id="8c7cd-103">Explore data in Hive tables with Hive queries</span></span>
<span data-ttu-id="8c7cd-104">Dit document bevat voorbeelden van Hive scripts die gebruikt tooexplore gegevens in de Hive-tabellen in een HDInsight Hadoop-cluster zijn.</span><span class="sxs-lookup"><span data-stu-id="8c7cd-104">This document provides sample Hive scripts that are used tooexplore data in Hive tables in an HDInsight Hadoop cluster.</span></span>

<span data-ttu-id="8c7cd-105">Hallo volgende **menu** tootopics waarin wordt beschreven hoe toouse hulpprogramma's voor tooexplore gegevens uit verschillende omgevingen voor opslag is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="8c7cd-105">hello following **menu** links tootopics that describe how toouse tools tooexplore data from various storage environments.</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="8c7cd-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8c7cd-106">Prerequisites</span></span>
<span data-ttu-id="8c7cd-107">In dit artikel wordt ervan uitgegaan dat u hebt:</span><span class="sxs-lookup"><span data-stu-id="8c7cd-107">This article assumes that you have:</span></span>

* <span data-ttu-id="8c7cd-108">Een Azure storage-account gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8c7cd-108">Created an Azure storage account.</span></span> <span data-ttu-id="8c7cd-109">Als u instructies nodig hebt, raadpleegt u [een Azure Storage-account maken](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="8c7cd-109">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="8c7cd-110">Een aangepaste Hadoop-cluster met Hallo HDInsight-service wordt ingericht.</span><span class="sxs-lookup"><span data-stu-id="8c7cd-110">Provisioned a customized Hadoop cluster with hello HDInsight service.</span></span> <span data-ttu-id="8c7cd-111">Als u instructies nodig hebt, raadpleegt u [aanpassen Azure HDInsight Hadoop-Clusters voor geavanceerde analyses](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="8c7cd-111">If you need instructions, see [Customize Azure HDInsight Hadoop Clusters for Advanced Analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="8c7cd-112">Hallo-gegevens zijn geüpload tooHive tabellen in Azure HDInsight Hadoop-clusters.</span><span class="sxs-lookup"><span data-stu-id="8c7cd-112">hello data has been uploaded tooHive tables in Azure HDInsight Hadoop clusters.</span></span> <span data-ttu-id="8c7cd-113">Als dit niet het geval is, volgt u de instructies Hallo in [maken en de belasting tooHive gegevenstabellen](machine-learning-data-science-move-hive-tables.md) tooupload gegevens tooHive eerst tabellen.</span><span class="sxs-lookup"><span data-stu-id="8c7cd-113">If it has not, follow hello instructions in [Create and load data tooHive tables](machine-learning-data-science-move-hive-tables.md) tooupload data tooHive tables first.</span></span>
* <span data-ttu-id="8c7cd-114">Externe toegang toohello cluster ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="8c7cd-114">Enabled remote access toohello cluster.</span></span> <span data-ttu-id="8c7cd-115">Als u instructies nodig hebt, raadpleegt u [toegang Hallo Head knooppunt van Hadoop-Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="8c7cd-115">If you need instructions, see [Access hello Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>
* <span data-ttu-id="8c7cd-116">Als u de instructies voor het moet toosubmit Hive-query's, Zie [hoe tooSubmit Hive-query's](machine-learning-data-science-move-hive-tables.md#submit)</span><span class="sxs-lookup"><span data-stu-id="8c7cd-116">If you need instructions on how toosubmit Hive queries, see [How tooSubmit Hive Queries](machine-learning-data-science-move-hive-tables.md#submit)</span></span>

## <a name="example-hive-query-scripts-for-data-exploration"></a><span data-ttu-id="8c7cd-117">Voorbeeld Hive query scripts voor gegevensverkenning</span><span class="sxs-lookup"><span data-stu-id="8c7cd-117">Example Hive query scripts for data exploration</span></span>
1. <span data-ttu-id="8c7cd-118">Hallo-telling van opmerkingen per partitie ophalen`SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`</span><span class="sxs-lookup"><span data-stu-id="8c7cd-118">Get hello count of observations per partition  `SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`</span></span>
2. <span data-ttu-id="8c7cd-119">Hallo-telling van metingen per dag`SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`</span><span class="sxs-lookup"><span data-stu-id="8c7cd-119">Get hello count of observations per day  `SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`</span></span>
3. <span data-ttu-id="8c7cd-120">Hallo niveaus in een categorische kolom ophalen</span><span class="sxs-lookup"><span data-stu-id="8c7cd-120">Get hello levels in a categorical column</span></span>  
    `SELECT  distinct <column_name> from <databasename>.<tablename>`
4. <span data-ttu-id="8c7cd-121">Hallo aantal niveaus in de combinatie van twee categorische kolommen ophalen`SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`</span><span class="sxs-lookup"><span data-stu-id="8c7cd-121">Get hello number of levels in combination of two categorical columns  `SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`</span></span>
5. <span data-ttu-id="8c7cd-122">Hallo-distributie voor numerieke kolommen ophalen</span><span class="sxs-lookup"><span data-stu-id="8c7cd-122">Get hello distribution for numerical columns</span></span>  
    `SELECT <column_name>, count(*) from <databasename>.<tablename> group by <column_name>`
6. <span data-ttu-id="8c7cd-123">Haal de records uit twee tabellen samenvoegen</span><span class="sxs-lookup"><span data-stu-id="8c7cd-123">Extract records from joining two tables</span></span>
   
        SELECT
            a.<common_columnname1> as <new_name1>,
            a.<common_columnname2> as <new_name2>,
            a.<a_column_name1> as <new_name3>,
            a.<a_column_name2> as <new_name4>,
            b.<b_column_name1> as <new_name5>,
            b.<b_column_name2> as <new_name6>
        FROM
            (
            SELECT <common_columnname1>,
                <common_columnname2>,
                <a_column_name1>,
                <a_column_name2>,
            FROM <databasename>.<tablename1>
            ) a
            join
            (
            SELECT <common_columnname1>,
                <common_columnname2>,
                <b_column_name1>,
                <b_column_name2>,
            FROM <databasename>.<tablename2>
            ) b
            ON a.<common_columnname1>=b.<common_columnname1> and a.<common_columnname2>=b.<common_columnname2>

## <a name="additional-query-scripts-for-taxi-trip-data-scenarios"></a><span data-ttu-id="8c7cd-124">Extra query scripts voor taxi reis gegevensscenario 's</span><span class="sxs-lookup"><span data-stu-id="8c7cd-124">Additional query scripts for taxi trip data scenarios</span></span>
<span data-ttu-id="8c7cd-125">Voorbeelden van query's die specifiek te zijn[NYC Taxi reis gegevens](http://chriswhong.com/open-data/foil_nyc_taxi/) scenario's zijn ook beschikbaar [GitHub-opslagplaats](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span><span class="sxs-lookup"><span data-stu-id="8c7cd-125">Examples of queries that are specific too[NYC Taxi Trip Data](http://chriswhong.com/open-data/foil_nyc_taxi/) scenarios are also provided in [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span></span> <span data-ttu-id="8c7cd-126">Deze query's al gegevensschema dat is opgegeven en zijn gereed toobe verzonden toorun.</span><span class="sxs-lookup"><span data-stu-id="8c7cd-126">These queries already have data schema specified and are ready toobe submitted toorun.</span></span>

