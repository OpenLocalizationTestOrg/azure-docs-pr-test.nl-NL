---
title: aaaConnect Excel tooHadoop Hello Hive ODBC-stuurprogramma - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe Hallo Microsoft Hive ODBC-stuurprogramma voor Excel tooquery-gegevens in HDInsight-clusters van Microsoft Excel tooset up en het gebruik.
keywords: hadoop, excel, hive excel, hive odbc
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
tags: azure-portal
editor: cgronlun
ms.assetid: a7665a14-0211-4521-b3e7-3b26e8029cc0
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/22/2017
ms.author: jgao
ms.openlocfilehash: f01f89e7d4203c739d56079dc589fc11f4aa2174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-excel-toohadoop-in-azure-hdinsight-with-hello-microsoft-hive-odbc-driver"></a>Excel-tooHadoop in Azure HDInsight verbinden met Hallo Microsoft Hive ODBC-stuurprogramma

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

Microsoft Business Intelligence (BI) onderdelen Big Data-oplossing van Microsoft geïntegreerd met Apache Hadoop-clusters die zijn geïmplementeerd door hello Azure HDInsight. Een voorbeeld van deze integratie is Hallo mogelijkheid tooconnect Excel toohello Hive datawarehouse van een Hadoop-cluster in HDInsight met behulp van Hallo stuurprogramma Microsoft Hive Open Database Connectivity (ODBC).

Het is ook mogelijk tooconnect Hallo gegevens die zijn gekoppeld aan een HDInsight-cluster en andere gegevensbronnen, inclusief andere (niet-HDInsight) Hadoop-clusters, vanuit Excel Hallo met Microsoft Power Query-invoegtoepassing voor Excel. Zie voor meer informatie over het installeren en gebruiken van Power Query [tooHDInsight Excel verbinding maken met Power Query][hdinsight-power-query].

> [!NOTE]
> Terwijl Hallo stappen in dit artikel kan worden gebruikt met beide Linux of cluster in HDInsight op basis van Windows, Windows is vereist voor Hallo clientwerkstation.
> 
> 

**Vereisten**:

Voordat u dit artikel, moet u de volgende items Hallo hebben:

* **Een HDInsight-cluster**. toocreate, Zie [aan de slag met Azure HDInsight][hdinsight-get-started].
* **Een werkstation** met Office 2013 Professional Plus, Office 365 Pro Plus, zelfstandige versie van Excel 2013 of Office 2010 Professional Plus.

## <a name="install-microsoft-hive-odbc-driver"></a>Installeer Microsoft Hive ODBC-stuurprogramma
Download en installeer Microsoft Hive ODBC-stuurprogramma van Hallo [Downloadcentrum][hive-odbc-driver-download].

Dit stuurprogramma kan worden geïnstalleerd op een 32-bits of 64-bits versies van Windows 7, Windows 8, Windows 10, Windows Server 2008 R2 en Windows Server 2012. Hallo stuurprogramma kan verbinding tooAzure HDInsight (versie 1.6 of hoger) en Azure HDInsight-Emulator (v.1.0.0.0 en hoger). U dient Hallo-versie die overeenkomt met de versie Hallo van waarbij u gebruikmaakt van het ODBC-stuurprogramma Hallo Hallo-toepassing installeren. Hallo-stuurprogramma wordt voor deze zelfstudie gebruikt vanuit Office Excel.

## <a name="create-hive-odbc-data-source"></a>Hive ODBC-gegevensbron maken
Hallo volgende stappen ziet u hoe toocreate Hive ODBC-gegevensbron.

1. Druk op Hallo Windows key tooopen Hallo-startscherm van Windows 8 of Windows 10 en typ vervolgens **gegevensbronnen**.
2. Klik op **instellen van ODBC-gegevensbronnen (32-bits)** of **instellen van ODBC-gegevensbronnen (64-bits)** , afhankelijk van uw Office-versie. Als u van Windows 7 gebruikmaakt, kiest u **ODBC-gegevensbronnen (32 bits)** of **ODBC-gegevensbronnen (64 bits)** van **Systeembeheer**. U ziet Hallo **ODBC Data Source Administrator** dialoogvenster.
   
    ![Gegevensbronbeheer OBDC](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.DataSourceAdmin1.png "een met ODBC-gegevensbronbeheer DSN configureren")

3. DNS van de gebruiker, klik op **toevoegen** tooopen hello **nieuwe gegevensbron maken** wizard.
4. Selecteer **stuurprogramma Microsoft Hive ODBC**, en klik vervolgens op **voltooien**. U ziet Hallo **Microsoft Hive ODBC-stuurprogramma DNS-instellingen** dialoogvenster.
5. Typ of selecteer Hallo volgende waarden:
   
   | Eigenschap | Beschrijving |
   | --- | --- |
   |  Naam van de gegevensbron |Geef een naam tooyour-gegevensbron |
   |  Host |Voer &lt;HDInsightClusterName>.azurehdinsight.net in. Bijvoorbeeld: myHDICluster.azurehdinsight.net |
   |  Poort |Gebruik <strong>443</strong>. (Deze poort is gewijzigd van 563 too443.) |
   |  Database |Gebruik <strong>Standaard</strong>. |
   |  Mechanisme |Selecteer <strong>Azure HDInsight Service</strong> |
   |  Gebruikersnaam |Voer de gebruikersnaam van HDInsight-cluster HTTP. Hallo standaardgebruikersnaam <strong>admin</strong>. |
   |  Wachtwoord |Voer gebruikerswachtwoord HDInsight-cluster. |
   
    </table>
   
    Er zijn een aantal belangrijke parameters toobe op de hoogte van wanneer u klikt op **geavanceerde opties**:
   
   | Parameter | Beschrijving |
   | --- | --- |
   |  Gebruik systeemeigen Query |Wanneer deze optie is geselecteerd, probeert de ODBC-stuurprogramma Hallo tooconvert TSQL niet in HiveQL. U dient alleen te gebruiken als u 100% zeker dat u verzendt pure HiveQL-instructies zijn. Wanneer u verbinding maakt tooSQL Server of Azure SQL Database, laat u het vakje uitgeschakeld. |
   |  Rijen per blok opgehaald |Tijdens het ophalen van een groot aantal records, afstemming van deze parameter mogelijk vereist tooensure optimale prestaties. |
   |  Standaard-tekenreekslengte kolom, binaire kolomlengte, decimaal kolomschaal |Hallo-gegevenstype lengten en Precision-systemen kunnen beïnvloeden hoe gegevens worden geretourneerd. Ze leiden tot onjuiste gegevens toobe geretourneerd vanwege tooloss van precision en/of moet worden afgekapt. |

    ![Geavanceerde opties voor](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.HiveOdbc.DataSource.AdvancedOptions1.png "DSN geavanceerde configuratieopties")

1. Klik op **Test** tootest Hallo-gegevensbron. Wanneer het Hallo-gegevensbron correct is geconfigureerd, worden *TESTS voltooid!*.
2. Klik op **OK** tooclose Hallo Test dialoogvenster. een nieuwe gegevensbron Hallo worden vermeld op Hallo **ODBC Data Source Administrator**.
3. Klik op **OK** tooexit Hallo-wizard.

## <a name="import-data-into-excel-from-hdinsight"></a>Gegevens in Excel importeren vanuit HDInsight
Hallo volgende stappen beschrijven Hallo manier tooimport gegevens van een Hive-tabel in een Excel-werkmap Hallo ODBC-gegevensbron die u hebt gemaakt in de vorige sectie Hallo.

1. Open een nieuwe of bestaande werkmap in Excel.
2. Van Hallo **gegevens** tabblad **gegevens ophalen**, klikt u op **van andere bronnen**, en klik vervolgens op **van ODBC** toolaunch hello  **Wizard Gegevensverbinding**.
   
    ![Wizard Gegevensverbinding Open](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.Excel.DataConnection1.png "wizard Gegevensverbinding openen")
4. Selecteer Hallo gegevensbron naam die u hebt gemaakt in de laatste sectie Hallo en klik vervolgens op **OK**.
5. Voer de naam van de gebruiker Hadoop (de standaardnaam Hallo is admin) Hallo wachtwoord en klik vervolgens op **Connect**.
6. Vouw op de Navigator **HIVE**, vouw **standaard**, klikt u op **hivesampletable**, en klik vervolgens op **Load**. Het duurt een paar seconden voordat gegevens geïmporteerde tooExcel opgehaald.

    ![HDInsight Hive ODBC navigator](./media/hdinsight-connect-excel-hive-ODBC-driver/hdinsight.hive.odbc.navigator.png "wizard Gegevensverbinding openen")


## <a name="next-steps"></a>Volgende stappen
In dit artikel hebt u geleerd hoe toouse Microsoft Hive ODBC-stuurprogramma tooretrieve gegevens van HDInsight-Service Hallo Hallo in Excel. Op deze manier kunt u gegevens ophalen uit Hallo HDInsight-Service in SQL-Database. Het is ook mogelijk tooupload gegevens in een HDInsight-Service. toolearn meer, Zie:

* [Vertraging vluchtgegevens met HDInsight analyseren][hdinsight-analyze-flight-data]
* [Uploaden van gegevens tooHDInsight][hdinsight-upload-data]
* [Sqoop gebruiken met HDInsight][hdinsight-use-sqoop]

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-get-started]: hdinsight-hadoop-tutorial-get-started-windows.md

[hive-odbc-driver-download]: http://go.microsoft.com/fwlink/?LinkID=286698


