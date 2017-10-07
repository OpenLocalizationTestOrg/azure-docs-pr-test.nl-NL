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
# <a name="connect-excel-toohadoop-in-azure-hdinsight-with-hello-microsoft-hive-odbc-driver"></a><span data-ttu-id="7823b-104">Excel-tooHadoop in Azure HDInsight verbinden met Hallo Microsoft Hive ODBC-stuurprogramma</span><span class="sxs-lookup"><span data-stu-id="7823b-104">Connect Excel tooHadoop in Azure HDInsight with hello Microsoft Hive ODBC driver</span></span>

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

<span data-ttu-id="7823b-105">Microsoft Business Intelligence (BI) onderdelen Big Data-oplossing van Microsoft geïntegreerd met Apache Hadoop-clusters die zijn geïmplementeerd door hello Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7823b-105">Microsoft's Big Data solution integrates Microsoft Business Intelligence (BI) components with Apache Hadoop clusters that have been deployed by hello Azure HDInsight.</span></span> <span data-ttu-id="7823b-106">Een voorbeeld van deze integratie is Hallo mogelijkheid tooconnect Excel toohello Hive datawarehouse van een Hadoop-cluster in HDInsight met behulp van Hallo stuurprogramma Microsoft Hive Open Database Connectivity (ODBC).</span><span class="sxs-lookup"><span data-stu-id="7823b-106">An example of this integration is hello ability tooconnect Excel toohello Hive data warehouse of a Hadoop cluster in HDInsight using hello Microsoft Hive Open Database Connectivity (ODBC) Driver.</span></span>

<span data-ttu-id="7823b-107">Het is ook mogelijk tooconnect Hallo gegevens die zijn gekoppeld aan een HDInsight-cluster en andere gegevensbronnen, inclusief andere (niet-HDInsight) Hadoop-clusters, vanuit Excel Hallo met Microsoft Power Query-invoegtoepassing voor Excel.</span><span class="sxs-lookup"><span data-stu-id="7823b-107">It is also possible tooconnect hello data associated with an HDInsight cluster and other data sources, including other (non-HDInsight) Hadoop clusters, from Excel using hello Microsoft Power Query add-in for Excel.</span></span> <span data-ttu-id="7823b-108">Zie voor meer informatie over het installeren en gebruiken van Power Query [tooHDInsight Excel verbinding maken met Power Query][hdinsight-power-query].</span><span class="sxs-lookup"><span data-stu-id="7823b-108">For information on installing and using Power Query, see [Connect Excel tooHDInsight with Power Query][hdinsight-power-query].</span></span>

> [!NOTE]
> <span data-ttu-id="7823b-109">Terwijl Hallo stappen in dit artikel kan worden gebruikt met beide Linux of cluster in HDInsight op basis van Windows, Windows is vereist voor Hallo clientwerkstation.</span><span class="sxs-lookup"><span data-stu-id="7823b-109">While hello steps in this article can be used with either a Linux or Windows-based HDInsight cluster, Windows is required for hello client workstation.</span></span>
> 
> 

<span data-ttu-id="7823b-110">**Vereisten**:</span><span class="sxs-lookup"><span data-stu-id="7823b-110">**Prerequisites**:</span></span>

<span data-ttu-id="7823b-111">Voordat u dit artikel, moet u de volgende items Hallo hebben:</span><span class="sxs-lookup"><span data-stu-id="7823b-111">Before you begin this article, you must have hello following items:</span></span>

* <span data-ttu-id="7823b-112">**Een HDInsight-cluster**.</span><span class="sxs-lookup"><span data-stu-id="7823b-112">**An HDInsight cluster**.</span></span> <span data-ttu-id="7823b-113">toocreate, Zie [aan de slag met Azure HDInsight][hdinsight-get-started].</span><span class="sxs-lookup"><span data-stu-id="7823b-113">toocreate one, see [Get started with Azure HDInsight][hdinsight-get-started].</span></span>
* <span data-ttu-id="7823b-114">**Een werkstation** met Office 2013 Professional Plus, Office 365 Pro Plus, zelfstandige versie van Excel 2013 of Office 2010 Professional Plus.</span><span class="sxs-lookup"><span data-stu-id="7823b-114">**A workstation** with Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone, or Office 2010 Professional Plus.</span></span>

## <a name="install-microsoft-hive-odbc-driver"></a><span data-ttu-id="7823b-115">Installeer Microsoft Hive ODBC-stuurprogramma</span><span class="sxs-lookup"><span data-stu-id="7823b-115">Install Microsoft Hive ODBC driver</span></span>
<span data-ttu-id="7823b-116">Download en installeer Microsoft Hive ODBC-stuurprogramma van Hallo [Downloadcentrum][hive-odbc-driver-download].</span><span class="sxs-lookup"><span data-stu-id="7823b-116">Download and install Microsoft Hive ODBC Driver from hello [Download Center][hive-odbc-driver-download].</span></span>

<span data-ttu-id="7823b-117">Dit stuurprogramma kan worden geïnstalleerd op een 32-bits of 64-bits versies van Windows 7, Windows 8, Windows 10, Windows Server 2008 R2 en Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="7823b-117">This driver can be installed on 32-bit or 64-bit versions of Windows 7, Windows 8, Windows 10, Windows Server 2008 R2, and Windows Server 2012.</span></span> <span data-ttu-id="7823b-118">Hallo stuurprogramma kan verbinding tooAzure HDInsight (versie 1.6 of hoger) en Azure HDInsight-Emulator (v.1.0.0.0 en hoger).</span><span class="sxs-lookup"><span data-stu-id="7823b-118">hello driver allows connection tooAzure HDInsight (version 1.6 and later) and Azure HDInsight Emulator (v.1.0.0.0 and later).</span></span> <span data-ttu-id="7823b-119">U dient Hallo-versie die overeenkomt met de versie Hallo van waarbij u gebruikmaakt van het ODBC-stuurprogramma Hallo Hallo-toepassing installeren.</span><span class="sxs-lookup"><span data-stu-id="7823b-119">You shall install hello version that matches hello version of hello application where you use hello ODBC driver.</span></span> <span data-ttu-id="7823b-120">Hallo-stuurprogramma wordt voor deze zelfstudie gebruikt vanuit Office Excel.</span><span class="sxs-lookup"><span data-stu-id="7823b-120">For this tutorial, hello driver is used from Office Excel.</span></span>

## <a name="create-hive-odbc-data-source"></a><span data-ttu-id="7823b-121">Hive ODBC-gegevensbron maken</span><span class="sxs-lookup"><span data-stu-id="7823b-121">Create Hive ODBC data source</span></span>
<span data-ttu-id="7823b-122">Hallo volgende stappen ziet u hoe toocreate Hive ODBC-gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="7823b-122">hello following steps show you how toocreate a Hive ODBC Data Source.</span></span>

1. <span data-ttu-id="7823b-123">Druk op Hallo Windows key tooopen Hallo-startscherm van Windows 8 of Windows 10 en typ vervolgens **gegevensbronnen**.</span><span class="sxs-lookup"><span data-stu-id="7823b-123">From Windows 8 or Windows 10, press hello Windows key tooopen hello Start screen, and then type **data sources**.</span></span>
2. <span data-ttu-id="7823b-124">Klik op **instellen van ODBC-gegevensbronnen (32-bits)** of **instellen van ODBC-gegevensbronnen (64-bits)** , afhankelijk van uw Office-versie.</span><span class="sxs-lookup"><span data-stu-id="7823b-124">Click **Set up ODBC Data sources (32-bit)** or **Set up ODBC Data Sources (64-bit)** depending on your Office version.</span></span> <span data-ttu-id="7823b-125">Als u van Windows 7 gebruikmaakt, kiest u **ODBC-gegevensbronnen (32 bits)** of **ODBC-gegevensbronnen (64 bits)** van **Systeembeheer**.</span><span class="sxs-lookup"><span data-stu-id="7823b-125">If you are using Windows 7, choose **ODBC Data Sources (32 bit)** or **ODBC Data Sources (64 bit)** from **Administrative Tools**.</span></span> <span data-ttu-id="7823b-126">U ziet Hallo **ODBC Data Source Administrator** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7823b-126">You shall see hello **ODBC Data Source Administrator** dialog.</span></span>
   
    <span data-ttu-id="7823b-127">![Gegevensbronbeheer OBDC](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.DataSourceAdmin1.png "een met ODBC-gegevensbronbeheer DSN configureren")</span><span class="sxs-lookup"><span data-stu-id="7823b-127">![OBDC data source administrator](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.DataSourceAdmin1.png "Configure a DSN using ODBC Data Source Administrator")</span></span>

3. <span data-ttu-id="7823b-128">DNS van de gebruiker, klik op **toevoegen** tooopen hello **nieuwe gegevensbron maken** wizard.</span><span class="sxs-lookup"><span data-stu-id="7823b-128">From User DNS, click **Add** tooopen hello **Create New Data Source** wizard.</span></span>
4. <span data-ttu-id="7823b-129">Selecteer **stuurprogramma Microsoft Hive ODBC**, en klik vervolgens op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="7823b-129">Select **Microsoft Hive ODBC Driver**, and then click **Finish**.</span></span> <span data-ttu-id="7823b-130">U ziet Hallo **Microsoft Hive ODBC-stuurprogramma DNS-instellingen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7823b-130">You shall see hello **Microsoft Hive ODBC Driver DNS Setup** dialog.</span></span>
5. <span data-ttu-id="7823b-131">Typ of selecteer Hallo volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="7823b-131">Type or select hello following values:</span></span>
   
   | <span data-ttu-id="7823b-132">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="7823b-132">Property</span></span> | <span data-ttu-id="7823b-133">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="7823b-133">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="7823b-134">Naam van de gegevensbron</span><span class="sxs-lookup"><span data-stu-id="7823b-134">Data Source Name</span></span> |<span data-ttu-id="7823b-135">Geef een naam tooyour-gegevensbron</span><span class="sxs-lookup"><span data-stu-id="7823b-135">Give a name tooyour data source</span></span> |
   |  <span data-ttu-id="7823b-136">Host</span><span class="sxs-lookup"><span data-stu-id="7823b-136">Host</span></span> |<span data-ttu-id="7823b-137">Voer &lt;HDInsightClusterName>.azurehdinsight.net in.</span><span class="sxs-lookup"><span data-stu-id="7823b-137">Enter &lt;HDInsightClusterName>.azurehdinsight.net.</span></span> <span data-ttu-id="7823b-138">Bijvoorbeeld: myHDICluster.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="7823b-138">For example, myHDICluster.azurehdinsight.net</span></span> |
   |  <span data-ttu-id="7823b-139">Poort</span><span class="sxs-lookup"><span data-stu-id="7823b-139">Port</span></span> |<span data-ttu-id="7823b-140">Gebruik <strong>443</strong>.</span><span class="sxs-lookup"><span data-stu-id="7823b-140">Use <strong>443</strong>.</span></span> <span data-ttu-id="7823b-141">(Deze poort is gewijzigd van 563 too443.)</span><span class="sxs-lookup"><span data-stu-id="7823b-141">(This port has been changed from 563 too443.)</span></span> |
   |  <span data-ttu-id="7823b-142">Database</span><span class="sxs-lookup"><span data-stu-id="7823b-142">Database</span></span> |<span data-ttu-id="7823b-143">Gebruik <strong>Standaard</strong>.</span><span class="sxs-lookup"><span data-stu-id="7823b-143">Use <strong>Default</strong>.</span></span> |
   |  <span data-ttu-id="7823b-144">Mechanisme</span><span class="sxs-lookup"><span data-stu-id="7823b-144">Mechanism</span></span> |<span data-ttu-id="7823b-145">Selecteer <strong>Azure HDInsight Service</strong></span><span class="sxs-lookup"><span data-stu-id="7823b-145">Select <strong>Azure HDInsight Service</strong></span></span> |
   |  <span data-ttu-id="7823b-146">Gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="7823b-146">User Name</span></span> |<span data-ttu-id="7823b-147">Voer de gebruikersnaam van HDInsight-cluster HTTP.</span><span class="sxs-lookup"><span data-stu-id="7823b-147">Enter HDInsight cluster HTTP user username.</span></span> <span data-ttu-id="7823b-148">Hallo standaardgebruikersnaam <strong>admin</strong>.</span><span class="sxs-lookup"><span data-stu-id="7823b-148">hello default username is <strong>admin</strong>.</span></span> |
   |  <span data-ttu-id="7823b-149">Wachtwoord</span><span class="sxs-lookup"><span data-stu-id="7823b-149">Password</span></span> |<span data-ttu-id="7823b-150">Voer gebruikerswachtwoord HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="7823b-150">Enter HDInsight cluster user password.</span></span> |
   
    </table>
   
    <span data-ttu-id="7823b-151">Er zijn een aantal belangrijke parameters toobe op de hoogte van wanneer u klikt op **geavanceerde opties**:</span><span class="sxs-lookup"><span data-stu-id="7823b-151">There are some important parameters toobe aware of when you click **Advanced Options**:</span></span>
   
   | <span data-ttu-id="7823b-152">Parameter</span><span class="sxs-lookup"><span data-stu-id="7823b-152">Parameter</span></span> | <span data-ttu-id="7823b-153">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="7823b-153">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="7823b-154">Gebruik systeemeigen Query</span><span class="sxs-lookup"><span data-stu-id="7823b-154">Use Native Query</span></span> |<span data-ttu-id="7823b-155">Wanneer deze optie is geselecteerd, probeert de ODBC-stuurprogramma Hallo tooconvert TSQL niet in HiveQL.</span><span class="sxs-lookup"><span data-stu-id="7823b-155">When it is selected, hello ODBC driver does NOT try tooconvert TSQL into HiveQL.</span></span> <span data-ttu-id="7823b-156">U dient alleen te gebruiken als u 100% zeker dat u verzendt pure HiveQL-instructies zijn.</span><span class="sxs-lookup"><span data-stu-id="7823b-156">You shall use it only if you are 100% sure you are submitting pure HiveQL statements.</span></span> <span data-ttu-id="7823b-157">Wanneer u verbinding maakt tooSQL Server of Azure SQL Database, laat u het vakje uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="7823b-157">When connecting tooSQL Server or Azure SQL Database, you should leave it unchecked.</span></span> |
   |  <span data-ttu-id="7823b-158">Rijen per blok opgehaald</span><span class="sxs-lookup"><span data-stu-id="7823b-158">Rows fetched per block</span></span> |<span data-ttu-id="7823b-159">Tijdens het ophalen van een groot aantal records, afstemming van deze parameter mogelijk vereist tooensure optimale prestaties.</span><span class="sxs-lookup"><span data-stu-id="7823b-159">When fetching a large number of records, tuning this parameter may be required tooensure optimal performances.</span></span> |
   |  <span data-ttu-id="7823b-160">Standaard-tekenreekslengte kolom, binaire kolomlengte, decimaal kolomschaal</span><span class="sxs-lookup"><span data-stu-id="7823b-160">Default string column length, Binary column length, Decimal column scale</span></span> |<span data-ttu-id="7823b-161">Hallo-gegevenstype lengten en Precision-systemen kunnen beïnvloeden hoe gegevens worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="7823b-161">hello data type lengths and precisions may affect how data is returned.</span></span> <span data-ttu-id="7823b-162">Ze leiden tot onjuiste gegevens toobe geretourneerd vanwege tooloss van precision en/of moet worden afgekapt.</span><span class="sxs-lookup"><span data-stu-id="7823b-162">They cause incorrect information toobe returned due tooloss of precision and/or truncation.</span></span> |

    <span data-ttu-id="7823b-163">![Geavanceerde opties voor](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.HiveOdbc.DataSource.AdvancedOptions1.png "DSN geavanceerde configuratieopties")</span><span class="sxs-lookup"><span data-stu-id="7823b-163">![Advanced options](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.HiveOdbc.DataSource.AdvancedOptions1.png "Advanced DSN configuration options")</span></span>

1. <span data-ttu-id="7823b-164">Klik op **Test** tootest Hallo-gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="7823b-164">Click **Test** tootest hello data source.</span></span> <span data-ttu-id="7823b-165">Wanneer het Hallo-gegevensbron correct is geconfigureerd, worden *TESTS voltooid!*.</span><span class="sxs-lookup"><span data-stu-id="7823b-165">When hello data source is configured correctly, it shows *TESTS COMPLETED SUCCESSFULLY!*.</span></span>
2. <span data-ttu-id="7823b-166">Klik op **OK** tooclose Hallo Test dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7823b-166">Click **OK** tooclose hello Test dialog.</span></span> <span data-ttu-id="7823b-167">een nieuwe gegevensbron Hallo worden vermeld op Hallo **ODBC Data Source Administrator**.</span><span class="sxs-lookup"><span data-stu-id="7823b-167">hello new data source shall be listed on hello **ODBC Data Source Administrator**.</span></span>
3. <span data-ttu-id="7823b-168">Klik op **OK** tooexit Hallo-wizard.</span><span class="sxs-lookup"><span data-stu-id="7823b-168">Click **OK** tooexit hello wizard.</span></span>

## <a name="import-data-into-excel-from-hdinsight"></a><span data-ttu-id="7823b-169">Gegevens in Excel importeren vanuit HDInsight</span><span class="sxs-lookup"><span data-stu-id="7823b-169">Import data into Excel from HDInsight</span></span>
<span data-ttu-id="7823b-170">Hallo volgende stappen beschrijven Hallo manier tooimport gegevens van een Hive-tabel in een Excel-werkmap Hallo ODBC-gegevensbron die u hebt gemaakt in de vorige sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="7823b-170">hello following steps describe hello way tooimport data from a Hive table into an Excel workbook using hello ODBC data source that you created in hello previous section.</span></span>

1. <span data-ttu-id="7823b-171">Open een nieuwe of bestaande werkmap in Excel.</span><span class="sxs-lookup"><span data-stu-id="7823b-171">Open a new or existing workbook in Excel.</span></span>
2. <span data-ttu-id="7823b-172">Van Hallo **gegevens** tabblad **gegevens ophalen**, klikt u op **van andere bronnen**, en klik vervolgens op **van ODBC** toolaunch hello  **Wizard Gegevensverbinding**.</span><span class="sxs-lookup"><span data-stu-id="7823b-172">From hello **Data** tab, click **Get Data**, click **From Other Sources**, and then click **From ODBC** toolaunch hello **Data Connection Wizard**.</span></span>
   
    <span data-ttu-id="7823b-173">![Wizard Gegevensverbinding Open](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.Excel.DataConnection1.png "wizard Gegevensverbinding openen")</span><span class="sxs-lookup"><span data-stu-id="7823b-173">![Open data connection wizard](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.Excel.DataConnection1.png "Open data connection wizard")</span></span>
4. <span data-ttu-id="7823b-174">Selecteer Hallo gegevensbron naam die u hebt gemaakt in de laatste sectie Hallo en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="7823b-174">Select hello data source name that you created in hello last section, and then click **OK**.</span></span>
5. <span data-ttu-id="7823b-175">Voer de naam van de gebruiker Hadoop (de standaardnaam Hallo is admin) Hallo wachtwoord en klik vervolgens op **Connect**.</span><span class="sxs-lookup"><span data-stu-id="7823b-175">Enter Hadoop user name (hello default name is admin) and hello password, and then click **Connect**.</span></span>
6. <span data-ttu-id="7823b-176">Vouw op de Navigator **HIVE**, vouw **standaard**, klikt u op **hivesampletable**, en klik vervolgens op **Load**.</span><span class="sxs-lookup"><span data-stu-id="7823b-176">On Navigator, expand **HIVE**, expand **default**, click **hivesampletable**, and then click **Load**.</span></span> <span data-ttu-id="7823b-177">Het duurt een paar seconden voordat gegevens geïmporteerde tooExcel opgehaald.</span><span class="sxs-lookup"><span data-stu-id="7823b-177">It takes a few seconds before data gets imported tooExcel.</span></span>

    <span data-ttu-id="7823b-178">![HDInsight Hive ODBC navigator](./media/hdinsight-connect-excel-hive-ODBC-driver/hdinsight.hive.odbc.navigator.png "wizard Gegevensverbinding openen")</span><span class="sxs-lookup"><span data-stu-id="7823b-178">![HDInsight Hive ODBC navigator](./media/hdinsight-connect-excel-hive-ODBC-driver/hdinsight.hive.odbc.navigator.png "Open data connection wizard")</span></span>


## <a name="next-steps"></a><span data-ttu-id="7823b-179">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7823b-179">Next steps</span></span>
<span data-ttu-id="7823b-180">In dit artikel hebt u geleerd hoe toouse Microsoft Hive ODBC-stuurprogramma tooretrieve gegevens van HDInsight-Service Hallo Hallo in Excel.</span><span class="sxs-lookup"><span data-stu-id="7823b-180">In this article, you learned how toouse hello Microsoft Hive ODBC driver tooretrieve data from hello HDInsight Service into Excel.</span></span> <span data-ttu-id="7823b-181">Op deze manier kunt u gegevens ophalen uit Hallo HDInsight-Service in SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="7823b-181">Similarly, you can retrieve data from hello HDInsight Service into SQL Database.</span></span> <span data-ttu-id="7823b-182">Het is ook mogelijk tooupload gegevens in een HDInsight-Service.</span><span class="sxs-lookup"><span data-stu-id="7823b-182">It is also possible tooupload data into an HDInsight Service.</span></span> <span data-ttu-id="7823b-183">toolearn meer, Zie:</span><span class="sxs-lookup"><span data-stu-id="7823b-183">toolearn more, see:</span></span>

* <span data-ttu-id="7823b-184">[Vertraging vluchtgegevens met HDInsight analyseren][hdinsight-analyze-flight-data]</span><span class="sxs-lookup"><span data-stu-id="7823b-184">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]</span></span>
* <span data-ttu-id="7823b-185">[Uploaden van gegevens tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="7823b-185">[Upload Data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="7823b-186">[Sqoop gebruiken met HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="7823b-186">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-get-started]: hdinsight-hadoop-tutorial-get-started-windows.md

[hive-odbc-driver-download]: http://go.microsoft.com/fwlink/?LinkID=286698


