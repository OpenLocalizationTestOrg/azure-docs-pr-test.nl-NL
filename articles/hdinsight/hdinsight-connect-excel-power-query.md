---
title: aaaConnect Excel tooHadoop met Power Query - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe tootake profiteren van business intelligence-onderdelen en gebruik Power Query voor Excel tooaccess-gegevens worden opgeslagen in Hadoop op HDInsight.
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 01ad2f90-7520-44d9-8c16-4d936faaff9b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jgao
ms.openlocfilehash: 1213849f1bc04e0ed206750b80766ff2268664b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-excel-toohadoop-by-using-power-query"></a>Verbinding maken met Excel tooHadoop via Power Query
Een belangrijke functie van Microsoft-oplossing voor big data Hallo is Hallo integratie van Microsoft business intelligence (BI)-onderdelen met Hadoop-clusters in Azure HDInsight. Een voorbeeld van een primaire is Hallo mogelijkheid tooconnect Excel toohello Azure Storage-account met Hallo gegevens die zijn gekoppeld aan de Hadoop-cluster met behulp van Hallo Microsoft Power Query voor Excel-invoegtoepassing. In dit artikel leert u hoe tooset up en het gebruik Power Query tooquery gegevens die zijn gekoppeld aan een Hadoop-cluster met HDInsight beheerd.

### <a name="prerequisites"></a>Vereisten
Voordat u dit artikel, moet u de volgende items Hallo hebben:

* **Een HDInsight-cluster**. tooconfigure, Zie [aan de slag met Azure HDInsight][hdinsight-get-started].
* **Een werkstation** waarop Windows 7, Windows Server 2008 R2 of een nieuwer besturingssysteem wordt uitgevoerd.
* **Office 2016, Office 2013 Professional Plus Office 365 ProPlus, zelfstandige versie van Excel 2013 of Office 2010 Professional Plus**.

## <a name="install-power-query"></a>Power Query installeren
Power Query kunt importeren van gegevens die de uitvoer heeft zijn of die is gegenereerd door een Hadoop-taak uitgevoerd op een HDInsight-cluster.

In Excel 2016 is Power Query geïntegreerd in Hallo gegevens lint onder Hallo Get & sectie Transform. Voor oudere versies van Excel, downloadt u Microsoft Power Query voor Excel via Hallo [Microsoft Download Center] [ powerquery-download] en te installeren.

## <a name="import-hdinsight-data-into-excel"></a>HDInsight-gegevens importeren in Excel
Hallo Power Query-invoegtoepassing voor Excel maakt het eenvoudig tooimport gegevens van uw HDInsight-cluster in Excel, waarbij hulpprogramma's zoals PowerPivot en -toewijzing met Power BI kunnen gebruikte tooinspect worden, analyseren en Hallo gegevens aanwezig.

**tooimport gegevens van een HDInsight-cluster**

1. Open Excel.
2. Maak een nieuwe lege werkmap.
3. Volgende stappen uit op basis van de versie van Excel Hallo Hallo uitvoeren:

    - Excel 2016

        - Klik op Hallo **gegevens** menu, klikt u op **gegevens ophalen** van Hallo **transformeren gegevens & ophalen** lint, klikt u op **van Azure**, en klik vervolgens op  **Uit Azure HDInsight(HDFS)**.

        ![HDI. PowerQuery.SelectHdiSource](./media/hdinsight-connect-excel-power-query/hdi.powerquery.selecthdisource.excel2016.png)

    - Excel 2013/2010

        - Klik op Hallo **Power Query** menu, klikt u op **van Azure**, en klik vervolgens op **van Microsoft Azure HDInsight**.
   
        ![HDI. PowerQuery.SelectHdiSource][image-hdi-powerquery-hdi-source]
       
        **Opmerking:** als er geen Hallo **Power Query** menu te gaan**bestand** > **opties** > **-invoegtoepassingen**, en selecteer **COM-invoegtoepassingen** in de vervolgkeuzelijst Hallo **beheren** vak Hallo Hallo pagina onderaan in. Selecteer Hallo **gaan...**  knop en verifieer dat vak Hallo voor Hallo Power Query voor Excel-invoegtoepassing is gecontroleerd.
       
        **Opmerking:** Power Query kunt u ook tooimport gegevens uit HDFS door te klikken op **van andere bronnen**.
4. Voor **accountnaam**, voer de naam Hallo van hello Azure Blob storage-account die is gekoppeld aan het cluster en klik op **OK**. Dit account kan worden Hallo [standaard opslagaccount](hdinsight-administer-use-management-portal.md#find-the-default-storage-account) of een gekoppeld opslagaccount.  Hallo-indeling is *https://&lt;StorageAccountName >.blob.core.windows.net/*.
5. Voor **Accountsleutel**, geef Hallo-sleutel voor Hallo Blob storage-account en klik vervolgens op **opslaan**. (U moet tooenter Hallo account informatie alleen Hallo eerste keer dat u toegang dit archief tot.)
6. In Hallo **Navigator** deelvenster op Hallo links Hallo Query-Editor, dubbelklikt u op Hallo Blob storage-containernaam. Standaard containernaam hello, dezelfde is Hallo naam als de naam van de cluster Hallo.
7. Zoek **HiveSampleData.txt** in Hallo **naam** kolom (Hallo mappad is **... / hive/datawarehouse/hivesampletable/**), en klik vervolgens op **binaire** op Hallo links van HiveSampleData.txt. HiveSampleData.txt wordt geleverd met alle Hallo-cluster. Desgewenst kunt u uw eigen-bestand.
   
    ![HDI. PowerQuery.ImportData][image-hdi-powerquery-importdata]
8. Als u wilt, kunt u de kolomnamen Hallo kunt wijzigen. Wanneer u klaar bent, klikt u op **sluit & laden**.  Hallo-gegevens zijn geladen tooyour werkmap:
   
    ![HDI. PowerQuery.ImportedTable][image-hdi-powerquery-imported-table]

## <a name="next-steps"></a>Volgende stappen
In dit artikel hebt u geleerd hoe toouse Power Query tooretrieve gegevens uit HDInsight in Excel. Op deze manier kunt u gegevens ophalen uit HDInsight in Azure SQL Database. Het is ook mogelijk tooupload gegevens in HDInsight. toolearn Zie meer Hallo artikelen te volgen:

* [Verbinding maken met Excel tooHDInsight Hello Microsoft Hive ODBC-stuurprogramma][hdinsight-ODBC]
* [Uploaden van gegevens tooHDInsight][hdinsight-upload-data]

[hdinsight-ODBC]: hdinsight-connect-excel-hive-odbc-driver.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[image-hdi-powerquery-hdi-source]: ./media/hdinsight-connect-excel-power-query/hdi.powerquery.selecthdisource.png
[image-hdi-powerquery-importdata]: ./media/hdinsight-connect-excel-power-query/hdi.powerquery.importdata.png
[image-hdi-powerquery-imported-table]: ./media/hdinsight-connect-excel-power-query/hdi.powerquery.importedtable.PNG

[powerquery-download]: http://go.microsoft.com/fwlink/?LinkID=286689
