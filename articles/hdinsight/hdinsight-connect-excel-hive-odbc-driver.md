---
title: Excel en Hadoop koppelen met het Hive ODBC-stuurprogramma - Azure HDInsight | Microsoft Docs
description: Informatie over het instellen en gebruiken van het Microsoft Hive ODBC-stuurprogramma voor Excel query uitvoeren op gegevens in HDInsight-clusters van Microsoft Excel.
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
ms.openlocfilehash: 7818093e42c34ee671a035cde783a6622fb2a798
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="connect-excel-to-hadoop-in-azure-hdinsight-with-the-microsoft-hive-odbc-driver"></a><span data-ttu-id="a6cb3-104">Excel verbinden met Hadoop in Azure HDInsight met het Microsoft Hive ODBC-stuurprogramma</span><span class="sxs-lookup"><span data-stu-id="a6cb3-104">Connect Excel to Hadoop in Azure HDInsight with the Microsoft Hive ODBC driver</span></span>

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

<span data-ttu-id="a6cb3-105">Microsoft Business Intelligence (BI) onderdelen Big Data-oplossing van Microsoft geïntegreerd met Apache Hadoop-clusters die zijn geïmplementeerd door de Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a6cb3-105">Microsoft's Big Data solution integrates Microsoft Business Intelligence (BI) components with Apache Hadoop clusters that have been deployed by the Azure HDInsight.</span></span> <span data-ttu-id="a6cb3-106">Een voorbeeld van deze integratie is de mogelijkheid Excel verbindt met het Hive-datawarehouse van een Hadoop-cluster in HDInsight met behulp van het stuurprogramma Microsoft Hive Open Database Connectivity (ODBC).</span><span class="sxs-lookup"><span data-stu-id="a6cb3-106">An example of this integration is the ability to connect Excel to the Hive data warehouse of a Hadoop cluster in HDInsight using the Microsoft Hive Open Database Connectivity (ODBC) Driver.</span></span>

<span data-ttu-id="a6cb3-107">Het is ook mogelijk om de gegevens die zijn gekoppeld aan een HDInsight-cluster en andere gegevensbronnen, met inbegrip van andere (niet-HDInsight) Hadoop-clusters van Excel met de Microsoft Power Query-invoegtoepassing voor Excel te verbinden.</span><span class="sxs-lookup"><span data-stu-id="a6cb3-107">It is also possible to connect the data associated with an HDInsight cluster and other data sources, including other (non-HDInsight) Hadoop clusters, from Excel using the Microsoft Power Query add-in for Excel.</span></span> <span data-ttu-id="a6cb3-108">Zie voor meer informatie over het installeren en gebruiken van Power Query [Excel verbinding naar HDInsight met Power Query][hdinsight-power-query].</span><span class="sxs-lookup"><span data-stu-id="a6cb3-108">For information on installing and using Power Query, see [Connect Excel to HDInsight with Power Query][hdinsight-power-query].</span></span>

> [!NOTE]
> <span data-ttu-id="a6cb3-109">Terwijl de stappen in dit artikel kunnen worden gebruikt met een Linux- of Windows gebaseerde HDInsight-cluster, is Windows vereist voor de clientwerkstation.</span><span class="sxs-lookup"><span data-stu-id="a6cb3-109">While the steps in this article can be used with either a Linux or Windows-based HDInsight cluster, Windows is required for the client workstation.</span></span>
> 
> 

<span data-ttu-id="a6cb3-110">**Vereisten**:</span><span class="sxs-lookup"><span data-stu-id="a6cb3-110">**Prerequisites**:</span></span>

<span data-ttu-id="a6cb3-111">Voordat u dit artikel, hebt u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="a6cb3-111">Before you begin this article, you must have the following items:</span></span>

* <span data-ttu-id="a6cb3-112">**Een HDInsight-cluster**.</span><span class="sxs-lookup"><span data-stu-id="a6cb3-112">**An HDInsight cluster**.</span></span> <span data-ttu-id="a6cb3-113">Als u wilt maken, Zie [aan de slag met Azure HDInsight][hdinsight-get-started].</span><span class="sxs-lookup"><span data-stu-id="a6cb3-113">To create one, see [Get started with Azure HDInsight][hdinsight-get-started].</span></span>
* <span data-ttu-id="a6cb3-114">**Een werkstation** met Office 2013 Professional Plus, Office 365 Pro Plus, zelfstandige versie van Excel 2013 of Office 2010 Professional Plus.</span><span class="sxs-lookup"><span data-stu-id="a6cb3-114">**A workstation** with Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone, or Office 2010 Professional Plus.</span></span>

## <a name="install-microsoft-hive-odbc-driver"></a><span data-ttu-id="a6cb3-115">Installeer Microsoft Hive ODBC-stuurprogramma</span><span class="sxs-lookup"><span data-stu-id="a6cb3-115">Install Microsoft Hive ODBC driver</span></span>
<span data-ttu-id="a6cb3-116">Download en installeer Microsoft Hive ODBC-stuurprogramma van de [Downloadcentrum][hive-odbc-driver-download].</span><span class="sxs-lookup"><span data-stu-id="a6cb3-116">Download and install Microsoft Hive ODBC Driver from the [Download Center][hive-odbc-driver-download].</span></span>

<span data-ttu-id="a6cb3-117">Dit stuurprogramma kan worden geïnstalleerd op een 32-bits of 64-bits versies van Windows 7, Windows 8, Windows 10, Windows Server 2008 R2 en Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="a6cb3-117">This driver can be installed on 32-bit or 64-bit versions of Windows 7, Windows 8, Windows 10, Windows Server 2008 R2, and Windows Server 2012.</span></span> <span data-ttu-id="a6cb3-118">Het stuurprogramma kan verbinding maken met Azure HDInsight (versie 1.6 of hoger) en Azure HDInsight-Emulator (v.1.0.0.0 en hoger).</span><span class="sxs-lookup"><span data-stu-id="a6cb3-118">The driver allows connection to Azure HDInsight (version 1.6 and later) and Azure HDInsight Emulator (v.1.0.0.0 and later).</span></span> <span data-ttu-id="a6cb3-119">U moet de versie die overeenkomt met de versie van de toepassing waarbij u gebruikmaakt van het ODBC-stuurprogramma installeren.</span><span class="sxs-lookup"><span data-stu-id="a6cb3-119">You shall install the version that matches the version of the application where you use the ODBC driver.</span></span> <span data-ttu-id="a6cb3-120">Het stuurprogramma wordt gebruikt voor deze zelfstudie uit Office Excel.</span><span class="sxs-lookup"><span data-stu-id="a6cb3-120">For this tutorial, the driver is used from Office Excel.</span></span>

## <a name="create-hive-odbc-data-source"></a><span data-ttu-id="a6cb3-121">Hive ODBC-gegevensbron maken</span><span class="sxs-lookup"><span data-stu-id="a6cb3-121">Create Hive ODBC data source</span></span>
<span data-ttu-id="a6cb3-122">De volgende stappen ziet u het maken van een Hive ODBC-gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="a6cb3-122">The following steps show you how to create a Hive ODBC Data Source.</span></span>

1. <span data-ttu-id="a6cb3-123">Druk op de Windows-toets op het startscherm openen vanuit Windows 8 of Windows 10, en typ vervolgens **gegevensbronnen**.</span><span class="sxs-lookup"><span data-stu-id="a6cb3-123">From Windows 8 or Windows 10, press the Windows key to open the Start screen, and then type **data sources**.</span></span>
2. <span data-ttu-id="a6cb3-124">Klik op **instellen van ODBC-gegevensbronnen (32-bits)** of **instellen van ODBC-gegevensbronnen (64-bits)** , afhankelijk van uw Office-versie.</span><span class="sxs-lookup"><span data-stu-id="a6cb3-124">Click **Set up ODBC Data sources (32-bit)** or **Set up ODBC Data Sources (64-bit)** depending on your Office version.</span></span> <span data-ttu-id="a6cb3-125">Als u van Windows 7 gebruikmaakt, kiest u **ODBC-gegevensbronnen (32 bits)** of **ODBC-gegevensbronnen (64 bits)** van **Systeembeheer**.</span><span class="sxs-lookup"><span data-stu-id="a6cb3-125">If you are using Windows 7, choose **ODBC Data Sources (32 bit)** or **ODBC Data Sources (64 bit)** from **Administrative Tools**.</span></span> <span data-ttu-id="a6cb3-126">U ziet de **ODBC Data Source Administrator** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a6cb3-126">You shall see the **ODBC Data Source Administrator** dialog.</span></span>
   
    <span data-ttu-id="a6cb3-127">![Gegevensbronbeheer OBDC](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.DataSourceAdmin1.png "een met ODBC-gegevensbronbeheer DSN configureren")</span><span class="sxs-lookup"><span data-stu-id="a6cb3-127">![OBDC data source administrator](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.DataSourceAdmin1.png "Configure a DSN using ODBC Data Source Administrator")</span></span>

3. <span data-ttu-id="a6cb3-128">DNS van de gebruiker, klik op **toevoegen** openen de **nieuwe gegevensbron maken** wizard.</span><span class="sxs-lookup"><span data-stu-id="a6cb3-128">From User DNS, click **Add** to open the **Create New Data Source** wizard.</span></span>
4. <span data-ttu-id="a6cb3-129">Selecteer **stuurprogramma Microsoft Hive ODBC**, en klik vervolgens op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="a6cb3-129">Select **Microsoft Hive ODBC Driver**, and then click **Finish**.</span></span> <span data-ttu-id="a6cb3-130">U ziet de **Microsoft Hive ODBC-stuurprogramma DNS-instellingen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a6cb3-130">You shall see the **Microsoft Hive ODBC Driver DNS Setup** dialog.</span></span>
5. <span data-ttu-id="a6cb3-131">Typ of selecteer de volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="a6cb3-131">Type or select the following values:</span></span>
   
   | <span data-ttu-id="a6cb3-132">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="a6cb3-132">Property</span></span> | <span data-ttu-id="a6cb3-133">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a6cb3-133">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="a6cb3-134">Naam van de gegevensbron</span><span class="sxs-lookup"><span data-stu-id="a6cb3-134">Data Source Name</span></span> |<span data-ttu-id="a6cb3-135">Geef uw gegevensbron een naam</span><span class="sxs-lookup"><span data-stu-id="a6cb3-135">Give a name to your data source</span></span> |
   |  <span data-ttu-id="a6cb3-136">Host</span><span class="sxs-lookup"><span data-stu-id="a6cb3-136">Host</span></span> |<span data-ttu-id="a6cb3-137">Voer &lt;HDInsightClusterName>.azurehdinsight.net in.</span><span class="sxs-lookup"><span data-stu-id="a6cb3-137">Enter &lt;HDInsightClusterName>.azurehdinsight.net.</span></span> <span data-ttu-id="a6cb3-138">Bijvoorbeeld: myHDICluster.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="a6cb3-138">For example, myHDICluster.azurehdinsight.net</span></span> |
   |  <span data-ttu-id="a6cb3-139">Poort</span><span class="sxs-lookup"><span data-stu-id="a6cb3-139">Port</span></span> |<span data-ttu-id="a6cb3-140">Gebruik <strong>443</strong>.</span><span class="sxs-lookup"><span data-stu-id="a6cb3-140">Use <strong>443</strong>.</span></span> <span data-ttu-id="a6cb3-141">(Deze poort is gewijzigd van 563 in 443.)</span><span class="sxs-lookup"><span data-stu-id="a6cb3-141">(This port has been changed from 563 to 443.)</span></span> |
   |  <span data-ttu-id="a6cb3-142">Database</span><span class="sxs-lookup"><span data-stu-id="a6cb3-142">Database</span></span> |<span data-ttu-id="a6cb3-143">Gebruik <strong>Standaard</strong>.</span><span class="sxs-lookup"><span data-stu-id="a6cb3-143">Use <strong>Default</strong>.</span></span> |
   |  <span data-ttu-id="a6cb3-144">Mechanisme</span><span class="sxs-lookup"><span data-stu-id="a6cb3-144">Mechanism</span></span> |<span data-ttu-id="a6cb3-145">Selecteer <strong>Azure HDInsight Service</strong></span><span class="sxs-lookup"><span data-stu-id="a6cb3-145">Select <strong>Azure HDInsight Service</strong></span></span> |
   |  <span data-ttu-id="a6cb3-146">Gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="a6cb3-146">User Name</span></span> |<span data-ttu-id="a6cb3-147">Voer de gebruikersnaam van HDInsight-cluster HTTP.</span><span class="sxs-lookup"><span data-stu-id="a6cb3-147">Enter HDInsight cluster HTTP user username.</span></span> <span data-ttu-id="a6cb3-148">De standaardgebruikersnaam <strong>admin</strong>.</span><span class="sxs-lookup"><span data-stu-id="a6cb3-148">The default username is <strong>admin</strong>.</span></span> |
   |  <span data-ttu-id="a6cb3-149">Wachtwoord</span><span class="sxs-lookup"><span data-stu-id="a6cb3-149">Password</span></span> |<span data-ttu-id="a6cb3-150">Voer gebruikerswachtwoord HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="a6cb3-150">Enter HDInsight cluster user password.</span></span> |
   
    </table>
   
    <span data-ttu-id="a6cb3-151">Er zijn een aantal belangrijke parameters moet denken wanneer u klikt op **geavanceerde opties**:</span><span class="sxs-lookup"><span data-stu-id="a6cb3-151">There are some important parameters to be aware of when you click **Advanced Options**:</span></span>
   
   | <span data-ttu-id="a6cb3-152">Parameter</span><span class="sxs-lookup"><span data-stu-id="a6cb3-152">Parameter</span></span> | <span data-ttu-id="a6cb3-153">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a6cb3-153">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="a6cb3-154">Gebruik systeemeigen Query</span><span class="sxs-lookup"><span data-stu-id="a6cb3-154">Use Native Query</span></span> |<span data-ttu-id="a6cb3-155">Wanneer deze optie is geselecteerd, probeert het ODBC-stuurprogramma niet TSQL converteren naar HiveQL.</span><span class="sxs-lookup"><span data-stu-id="a6cb3-155">When it is selected, the ODBC driver does NOT try to convert TSQL into HiveQL.</span></span> <span data-ttu-id="a6cb3-156">U dient alleen te gebruiken als u 100% zeker dat u verzendt pure HiveQL-instructies zijn.</span><span class="sxs-lookup"><span data-stu-id="a6cb3-156">You shall use it only if you are 100% sure you are submitting pure HiveQL statements.</span></span> <span data-ttu-id="a6cb3-157">Wanneer u verbinding maakt met SQL Server of Azure SQL Database, laat u het vakje uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="a6cb3-157">When connecting to SQL Server or Azure SQL Database, you should leave it unchecked.</span></span> |
   |  <span data-ttu-id="a6cb3-158">Rijen per blok opgehaald</span><span class="sxs-lookup"><span data-stu-id="a6cb3-158">Rows fetched per block</span></span> |<span data-ttu-id="a6cb3-159">Tijdens ophalen van een groot aantal records kan afstemming van deze parameter worden vereist om ervoor te zorgen optimale prestaties.</span><span class="sxs-lookup"><span data-stu-id="a6cb3-159">When fetching a large number of records, tuning this parameter may be required to ensure optimal performances.</span></span> |
   |  <span data-ttu-id="a6cb3-160">Standaard-tekenreekslengte kolom, binaire kolomlengte, decimaal kolomschaal</span><span class="sxs-lookup"><span data-stu-id="a6cb3-160">Default string column length, Binary column length, Decimal column scale</span></span> |<span data-ttu-id="a6cb3-161">De lengte van het gegevenstype en Precision-systemen kunnen beïnvloeden hoe gegevens worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="a6cb3-161">The data type lengths and precisions may affect how data is returned.</span></span> <span data-ttu-id="a6cb3-162">Deze leiden tot onjuiste gegevens moeten worden opgehaald vanwege verlies van precisie en/of moet worden afgekapt.</span><span class="sxs-lookup"><span data-stu-id="a6cb3-162">They cause incorrect information to be returned due to loss of precision and/or truncation.</span></span> |

    <span data-ttu-id="a6cb3-163">![Geavanceerde opties voor](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.HiveOdbc.DataSource.AdvancedOptions1.png "DSN geavanceerde configuratieopties")</span><span class="sxs-lookup"><span data-stu-id="a6cb3-163">![Advanced options](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.HiveOdbc.DataSource.AdvancedOptions1.png "Advanced DSN configuration options")</span></span>

1. <span data-ttu-id="a6cb3-164">Klik op **testen** voor het testen van de gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="a6cb3-164">Click **Test** to test the data source.</span></span> <span data-ttu-id="a6cb3-165">Wanneer de gegevensbron correct is geconfigureerd, worden *TESTS voltooid!*.</span><span class="sxs-lookup"><span data-stu-id="a6cb3-165">When the data source is configured correctly, it shows *TESTS COMPLETED SUCCESSFULLY!*.</span></span>
2. <span data-ttu-id="a6cb3-166">Klik op **OK** om de Test-dialoogvenster te sluiten.</span><span class="sxs-lookup"><span data-stu-id="a6cb3-166">Click **OK** to close the Test dialog.</span></span> <span data-ttu-id="a6cb3-167">De nieuwe gegevensbron worden vermeld op de **ODBC Data Source Administrator**.</span><span class="sxs-lookup"><span data-stu-id="a6cb3-167">The new data source shall be listed on the **ODBC Data Source Administrator**.</span></span>
3. <span data-ttu-id="a6cb3-168">Klik op **OK** de wizard wilt afsluiten.</span><span class="sxs-lookup"><span data-stu-id="a6cb3-168">Click **OK** to exit the wizard.</span></span>

## <a name="import-data-into-excel-from-hdinsight"></a><span data-ttu-id="a6cb3-169">Gegevens in Excel importeren vanuit HDInsight</span><span class="sxs-lookup"><span data-stu-id="a6cb3-169">Import data into Excel from HDInsight</span></span>
<span data-ttu-id="a6cb3-170">De volgende stappen beschrijven de manier waarop gegevens importeren uit een Hive-tabel in een Excel-werkmap met behulp van de ODBC-gegevensbron die u hebt gemaakt in de vorige sectie.</span><span class="sxs-lookup"><span data-stu-id="a6cb3-170">The following steps describe the way to import data from a Hive table into an Excel workbook using the ODBC data source that you created in the previous section.</span></span>

1. <span data-ttu-id="a6cb3-171">Open een nieuwe of bestaande werkmap in Excel.</span><span class="sxs-lookup"><span data-stu-id="a6cb3-171">Open a new or existing workbook in Excel.</span></span>
2. <span data-ttu-id="a6cb3-172">Van de **gegevens** tabblad **gegevens ophalen**, klikt u op **van andere bronnen**, en klik vervolgens op **van ODBC** starten de **gegevens Wizard verbinding**.</span><span class="sxs-lookup"><span data-stu-id="a6cb3-172">From the **Data** tab, click **Get Data**, click **From Other Sources**, and then click **From ODBC** to launch the **Data Connection Wizard**.</span></span>
   
    <span data-ttu-id="a6cb3-173">![Wizard Gegevensverbinding Open](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.Excel.DataConnection1.png "wizard Gegevensverbinding openen")</span><span class="sxs-lookup"><span data-stu-id="a6cb3-173">![Open data connection wizard](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.Excel.DataConnection1.png "Open data connection wizard")</span></span>
4. <span data-ttu-id="a6cb3-174">Selecteer de naam van de gegevensbron die u in de laatste sectie hebt gemaakt en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="a6cb3-174">Select the data source name that you created in the last section, and then click **OK**.</span></span>
5. <span data-ttu-id="a6cb3-175">Voer de naam van de gebruiker Hadoop (de standaardnaam is admin) en het wachtwoord en klik vervolgens op **Connect**.</span><span class="sxs-lookup"><span data-stu-id="a6cb3-175">Enter Hadoop user name (the default name is admin) and the password, and then click **Connect**.</span></span>
6. <span data-ttu-id="a6cb3-176">Vouw op de Navigator **HIVE**, vouw **standaard**, klikt u op **hivesampletable**, en klik vervolgens op **Load**.</span><span class="sxs-lookup"><span data-stu-id="a6cb3-176">On Navigator, expand **HIVE**, expand **default**, click **hivesampletable**, and then click **Load**.</span></span> <span data-ttu-id="a6cb3-177">Het duurt een paar seconden voordat de gegevens naar Excel worden geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="a6cb3-177">It takes a few seconds before data gets imported to Excel.</span></span>

    <span data-ttu-id="a6cb3-178">![HDInsight Hive ODBC navigator](./media/hdinsight-connect-excel-hive-ODBC-driver/hdinsight.hive.odbc.navigator.png "wizard Gegevensverbinding openen")</span><span class="sxs-lookup"><span data-stu-id="a6cb3-178">![HDInsight Hive ODBC navigator](./media/hdinsight-connect-excel-hive-ODBC-driver/hdinsight.hive.odbc.navigator.png "Open data connection wizard")</span></span>


## <a name="next-steps"></a><span data-ttu-id="a6cb3-179">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a6cb3-179">Next steps</span></span>
<span data-ttu-id="a6cb3-180">In dit artikel hebt u geleerd hoe gebruikmaken van het stuurprogramma Microsoft Hive ODBC-gegevens ophalen van de HDInsight-Service in Excel.</span><span class="sxs-lookup"><span data-stu-id="a6cb3-180">In this article, you learned how to use the Microsoft Hive ODBC driver to retrieve data from the HDInsight Service into Excel.</span></span> <span data-ttu-id="a6cb3-181">Op deze manier kunt u gegevens ophalen uit de HDInsight-Service in SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="a6cb3-181">Similarly, you can retrieve data from the HDInsight Service into SQL Database.</span></span> <span data-ttu-id="a6cb3-182">Het is ook mogelijk om gegevens te uploaden naar HDInsight-Service.</span><span class="sxs-lookup"><span data-stu-id="a6cb3-182">It is also possible to upload data into an HDInsight Service.</span></span> <span data-ttu-id="a6cb3-183">Voor meer informatie zie:</span><span class="sxs-lookup"><span data-stu-id="a6cb3-183">To learn more, see:</span></span>

* <span data-ttu-id="a6cb3-184">[Vertraging vluchtgegevens met HDInsight analyseren][hdinsight-analyze-flight-data]</span><span class="sxs-lookup"><span data-stu-id="a6cb3-184">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]</span></span>
* <span data-ttu-id="a6cb3-185">[Gegevens uploaden naar HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="a6cb3-185">[Upload Data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="a6cb3-186">[Sqoop gebruiken met HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="a6cb3-186">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-get-started]: hdinsight-hadoop-tutorial-get-started-windows.md

[hive-odbc-driver-download]: http://go.microsoft.com/fwlink/?LinkID=286698


