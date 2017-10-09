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
# <a name="explore-data-in-hive-tables-with-hive-queries"></a>Gegevens in Hive-tabellen verkennen met Hive-query's
Dit document bevat voorbeelden van Hive scripts die gebruikt tooexplore gegevens in de Hive-tabellen in een HDInsight Hadoop-cluster zijn.

Hallo volgende **menu** tootopics waarin wordt beschreven hoe toouse hulpprogramma's voor tooexplore gegevens uit verschillende omgevingen voor opslag is gekoppeld.

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a>Vereisten
In dit artikel wordt ervan uitgegaan dat u hebt:

* Een Azure storage-account gemaakt. Als u instructies nodig hebt, raadpleegt u [een Azure Storage-account maken](../storage/common/storage-create-storage-account.md#create-a-storage-account)
* Een aangepaste Hadoop-cluster met Hallo HDInsight-service wordt ingericht. Als u instructies nodig hebt, raadpleegt u [aanpassen Azure HDInsight Hadoop-Clusters voor geavanceerde analyses](machine-learning-data-science-customize-hadoop-cluster.md).
* Hallo-gegevens zijn geüpload tooHive tabellen in Azure HDInsight Hadoop-clusters. Als dit niet het geval is, volgt u de instructies Hallo in [maken en de belasting tooHive gegevenstabellen](machine-learning-data-science-move-hive-tables.md) tooupload gegevens tooHive eerst tabellen.
* Externe toegang toohello cluster ingeschakeld. Als u instructies nodig hebt, raadpleegt u [toegang Hallo Head knooppunt van Hadoop-Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).
* Als u de instructies voor het moet toosubmit Hive-query's, Zie [hoe tooSubmit Hive-query's](machine-learning-data-science-move-hive-tables.md#submit)

## <a name="example-hive-query-scripts-for-data-exploration"></a>Voorbeeld Hive query scripts voor gegevensverkenning
1. Hallo-telling van opmerkingen per partitie ophalen`SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`
2. Hallo-telling van metingen per dag`SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`
3. Hallo niveaus in een categorische kolom ophalen  
    `SELECT  distinct <column_name> from <databasename>.<tablename>`
4. Hallo aantal niveaus in de combinatie van twee categorische kolommen ophalen`SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`
5. Hallo-distributie voor numerieke kolommen ophalen  
    `SELECT <column_name>, count(*) from <databasename>.<tablename> group by <column_name>`
6. Haal de records uit twee tabellen samenvoegen
   
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

## <a name="additional-query-scripts-for-taxi-trip-data-scenarios"></a>Extra query scripts voor taxi reis gegevensscenario 's
Voorbeelden van query's die specifiek te zijn[NYC Taxi reis gegevens](http://chriswhong.com/open-data/foil_nyc_taxi/) scenario's zijn ook beschikbaar [GitHub-opslagplaats](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts). Deze query's al gegevensschema dat is opgegeven en zijn gereed toobe verzonden toorun.

