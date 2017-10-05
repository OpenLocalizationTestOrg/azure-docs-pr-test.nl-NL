---
title: Apache Sqoop taken uitvoeren met Azure HDInsight (Hadoop) | Microsoft Docs
description: Informatie over het gebruik van Azure PowerShell vanaf een werkstation voor het uitvoeren van Sqoop importeren en exporteren tussen een Hadoop-cluster en een Azure SQL database.
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 2fdcc6b7-6ad5-4397-a30b-e7e389b66c7a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 8e77153493b6f37f5f48116b86bad6b25a50d1a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-sqoop-with-hadoop-in-hdinsight"></a><span data-ttu-id="ef97b-103">Sqoop gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="ef97b-103">Use Sqoop with Hadoop in HDInsight</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="ef97b-104">Informatie over het Sqoop in HDInsight gebruiken om te importeren en exporteren tussen een HDInsight-cluster en Azure SQL database of SQL Server-database.</span><span class="sxs-lookup"><span data-stu-id="ef97b-104">Learn how to use Sqoop in HDInsight to import and export between HDInsight cluster and Azure SQL database or SQL Server database.</span></span>

<span data-ttu-id="ef97b-105">Hoewel Hadoop een natuurlijke keuze voor het verwerken van ongestructureerde en semigestructureerde gegevens, zoals Logboeken en bestanden, is er mogelijk ook nodig om gestructureerde gegevens die zijn opgeslagen in de relationele databases te verwerken.</span><span class="sxs-lookup"><span data-stu-id="ef97b-105">Although Hadoop is a natural choice for processing unstructured and semistructured data, such as logs and files, there may also be a need to process structured data that is stored in relational databases.</span></span>

<span data-ttu-id="ef97b-106">[Sqoop] [ sqoop-user-guide-1.4.4] is een hulpprogramma waarmee gegevens worden overgebracht tussen Hadoop-clusters en relationele databases.</span><span class="sxs-lookup"><span data-stu-id="ef97b-106">[Sqoop][sqoop-user-guide-1.4.4] is a tool designed to transfer data between Hadoop clusters and relational databases.</span></span> <span data-ttu-id="ef97b-107">U kunt deze gebruiken om gegevens te importeren uit een relationele databasebeheersysteem (RDBMS), zoals SQL Server, MySQL of Oracle in het Hadoop distributed file system (HDFS), de gegevens in Hadoop met MapReduce of Hive transformeren en de gegevens vervolgens exporteren naar een RDBMS.</span><span class="sxs-lookup"><span data-stu-id="ef97b-107">You can use it to import data from a relational database management system (RDBMS) such as SQL Server, MySQL, or Oracle into the Hadoop distributed file system (HDFS), transform the data in Hadoop with MapReduce or Hive, and then export the data back into an RDBMS.</span></span> <span data-ttu-id="ef97b-108">In deze zelfstudie maakt u een SQL Server-database gebruikt voor de relationele database.</span><span class="sxs-lookup"><span data-stu-id="ef97b-108">In this tutorial, you are using a SQL Server database for your relational database.</span></span>

<span data-ttu-id="ef97b-109">Zie voor versies die worden ondersteund op HDInsight-clusters Sqoop [wat is er nieuw in de clusterversies geleverd door HDInsight?][hdinsight-versions]</span><span class="sxs-lookup"><span data-stu-id="ef97b-109">For Sqoop versions that are supported on HDInsight clusters, see [What's new in the cluster versions provided by HDInsight?][hdinsight-versions]</span></span>

## <a name="understand-the-scenario"></a><span data-ttu-id="ef97b-110">Inzicht in het scenario</span><span class="sxs-lookup"><span data-stu-id="ef97b-110">Understand the scenario</span></span>

<span data-ttu-id="ef97b-111">HDInsight-cluster wordt geleverd met voorbeeldgegevens.</span><span class="sxs-lookup"><span data-stu-id="ef97b-111">HDInsight cluster comes with some sample data.</span></span> <span data-ttu-id="ef97b-112">U gebruikt de volgende twee voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="ef97b-112">You use the following two samples:</span></span>

* <span data-ttu-id="ef97b-113">Een logboekbestand log4j, bevindt zich op */example/data/sample.log*.</span><span class="sxs-lookup"><span data-stu-id="ef97b-113">A log4j log file, which is located at */example/data/sample.log*.</span></span> <span data-ttu-id="ef97b-114">De volgende logboeken worden opgehaald uit het bestand:</span><span class="sxs-lookup"><span data-stu-id="ef97b-114">The following logs are extracted from the file:</span></span>
  
        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...
* <span data-ttu-id="ef97b-115">Een Hive-tabel met de naam *hivesampletable*, die verwijst naar het bestand zich bevindt op */hive/warehouse/hivesampletable*.</span><span class="sxs-lookup"><span data-stu-id="ef97b-115">A Hive table named *hivesampletable*, which references the data file located at */hive/warehouse/hivesampletable*.</span></span> <span data-ttu-id="ef97b-116">De tabel bevat de gegevens van sommige mobiele apparaten.</span><span class="sxs-lookup"><span data-stu-id="ef97b-116">The table contains some mobile device data.</span></span> 
  
  | <span data-ttu-id="ef97b-117">Veld</span><span class="sxs-lookup"><span data-stu-id="ef97b-117">Field</span></span> | <span data-ttu-id="ef97b-118">Gegevenstype</span><span class="sxs-lookup"><span data-stu-id="ef97b-118">Data type</span></span> |
  | --- | --- |
  | <span data-ttu-id="ef97b-119">clientid</span><span class="sxs-lookup"><span data-stu-id="ef97b-119">clientid</span></span> |<span data-ttu-id="ef97b-120">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="ef97b-120">string</span></span> |
  | <span data-ttu-id="ef97b-121">querytime</span><span class="sxs-lookup"><span data-stu-id="ef97b-121">querytime</span></span> |<span data-ttu-id="ef97b-122">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="ef97b-122">string</span></span> |
  | <span data-ttu-id="ef97b-123">markt</span><span class="sxs-lookup"><span data-stu-id="ef97b-123">market</span></span> |<span data-ttu-id="ef97b-124">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="ef97b-124">string</span></span> |
  | <span data-ttu-id="ef97b-125">deviceplatform</span><span class="sxs-lookup"><span data-stu-id="ef97b-125">deviceplatform</span></span> |<span data-ttu-id="ef97b-126">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="ef97b-126">string</span></span> |
  | <span data-ttu-id="ef97b-127">devicemake</span><span class="sxs-lookup"><span data-stu-id="ef97b-127">devicemake</span></span> |<span data-ttu-id="ef97b-128">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="ef97b-128">string</span></span> |
  | <span data-ttu-id="ef97b-129">devicemodel</span><span class="sxs-lookup"><span data-stu-id="ef97b-129">devicemodel</span></span> |<span data-ttu-id="ef97b-130">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="ef97b-130">string</span></span> |
  | <span data-ttu-id="ef97b-131">state</span><span class="sxs-lookup"><span data-stu-id="ef97b-131">state</span></span> |<span data-ttu-id="ef97b-132">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="ef97b-132">string</span></span> |
  | <span data-ttu-id="ef97b-133">Land</span><span class="sxs-lookup"><span data-stu-id="ef97b-133">country</span></span> |<span data-ttu-id="ef97b-134">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="ef97b-134">string</span></span> |
  | <span data-ttu-id="ef97b-135">querydwelltime</span><span class="sxs-lookup"><span data-stu-id="ef97b-135">querydwelltime</span></span> |<span data-ttu-id="ef97b-136">dubbele</span><span class="sxs-lookup"><span data-stu-id="ef97b-136">double</span></span> |
  | <span data-ttu-id="ef97b-137">sessie-id</span><span class="sxs-lookup"><span data-stu-id="ef97b-137">sessionid</span></span> |<span data-ttu-id="ef97b-138">bigint</span><span class="sxs-lookup"><span data-stu-id="ef97b-138">bigint</span></span> |
  | <span data-ttu-id="ef97b-139">sessionpagevieworder</span><span class="sxs-lookup"><span data-stu-id="ef97b-139">sessionpagevieworder</span></span> |<span data-ttu-id="ef97b-140">bigint</span><span class="sxs-lookup"><span data-stu-id="ef97b-140">bigint</span></span> |

<span data-ttu-id="ef97b-141">Exporteer eerst *sample.log* en *hivesampletable* aan de Azure SQL database of SQL Server en vervolgens importeren in de tabel met de gegevens van het mobiele apparaat terug naar HDInsight met behulp van het volgende pad:</span><span class="sxs-lookup"><span data-stu-id="ef97b-141">First, you export *sample.log* and *hivesampletable* to the Azure SQL database or to SQL Server, and then import the table that contains the mobile device data back to HDInsight by using the following path:</span></span>

    /tutorials/usesqoop/importeddata

## <a name="create-cluster-and-sql-database"></a><span data-ttu-id="ef97b-142">Cluster- en SQL-database maken</span><span class="sxs-lookup"><span data-stu-id="ef97b-142">Create cluster and SQL database</span></span>
<span data-ttu-id="ef97b-143">Deze sectie wordt beschreven hoe u een cluster, een SQL-Database en de SQL-database schema's voor het uitvoeren van de zelfstudie met behulp van de Azure-portal en een Azure Resource Manager-sjabloon maken.</span><span class="sxs-lookup"><span data-stu-id="ef97b-143">This section shows you how to create a cluster, a SQL Database, and the SQL database schemas for running the tutorial using the Azure portal and an Azure Resource Manager template.</span></span> <span data-ttu-id="ef97b-144">De sjabloon kan worden gevonden in [Azure-Snelstartsjablonen](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-sql-database/).</span><span class="sxs-lookup"><span data-stu-id="ef97b-144">The template can be found in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-sql-database/).</span></span> <span data-ttu-id="ef97b-145">De Resource Manager-sjabloon roept een Bacpac-pakket voor het implementeren van het tabelschema met SQL-database.</span><span class="sxs-lookup"><span data-stu-id="ef97b-145">The Resource Manager template calls a bacpac package to deploy the table schemas to SQL database.</span></span>  <span data-ttu-id="ef97b-146">Het Bacpac-pakket bevindt zich in een openbare blobcontainer, https://hditutorialdata.blob.core.windows.net/usesqoop/SqoopTutorial-2016-2-23-11-2.bacpac.</span><span class="sxs-lookup"><span data-stu-id="ef97b-146">The bacpac package is located in a public blob container, https://hditutorialdata.blob.core.windows.net/usesqoop/SqoopTutorial-2016-2-23-11-2.bacpac.</span></span> <span data-ttu-id="ef97b-147">Als u een persoonlijke container gebruiken voor het Bacpac-bestanden wilt, gebruikt u de volgende waarden in de sjabloon:</span><span class="sxs-lookup"><span data-stu-id="ef97b-147">If you want to use a private container for the bacpac files, use the following values in the template:</span></span>
   
        "storageKeyType": "Primary",
        "storageKey": "<TheAzureStorageAccountKey>",

<span data-ttu-id="ef97b-148">Als u liever Azure PowerShell gebruiken voor het maken van het cluster en de SQL-Database, Zie [bijlage A](#appendix-a---a-powershell-sample).</span><span class="sxs-lookup"><span data-stu-id="ef97b-148">If you prefer to use Azure PowerShell to create the cluster and the SQL Database, see [Appendix A](#appendix-a---a-powershell-sample).</span></span>

1. <span data-ttu-id="ef97b-149">Klik op de volgende afbeelding om te openen van een Resource Manager-sjabloon in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ef97b-149">Click the following image to open a Resource Manager template in the Azure portal.</span></span>         
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-sql-database%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-use-sqoop/deploy-to-azure.png" alt="Deploy to Azure"></a>
   

2. <span data-ttu-id="ef97b-150">Voer de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="ef97b-150">Enter the following properties:</span></span>

    - <span data-ttu-id="ef97b-151">**Abonnement**: Voer uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="ef97b-151">**Subscription**: Enter your Azure subscription.</span></span>
    - <span data-ttu-id="ef97b-152">**Resourcegroep**: Maak een nieuwe Azure-resourcegroep of Selecteer een bestaande resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="ef97b-152">**Resource Group**: Create a new Azure Resource Group, or select an existing Resource Group.</span></span>  <span data-ttu-id="ef97b-153">Een resourcegroep is voor management doel.</span><span class="sxs-lookup"><span data-stu-id="ef97b-153">A Resource Group is for management purpose.</span></span>  <span data-ttu-id="ef97b-154">Er is een container voor objecten.</span><span class="sxs-lookup"><span data-stu-id="ef97b-154">It is a container for objects.</span></span>
    - <span data-ttu-id="ef97b-155">**Locatie**: Selecteer een regio.</span><span class="sxs-lookup"><span data-stu-id="ef97b-155">**Location**: Select a region.</span></span>
    - <span data-ttu-id="ef97b-156">**Clusternaam**: Voer een naam voor het Hadoop-cluster.</span><span class="sxs-lookup"><span data-stu-id="ef97b-156">**ClusterName**: Enter a name for the Hadoop cluster.</span></span>
    - <span data-ttu-id="ef97b-157">**Clusteraanmeldgegevens**: de standaardaanmeldnaam is admin.</span><span class="sxs-lookup"><span data-stu-id="ef97b-157">**Cluster login name and password**: The default login name is admin.</span></span>
    - <span data-ttu-id="ef97b-158">**SSH-aanmeldgegevens**.</span><span class="sxs-lookup"><span data-stu-id="ef97b-158">**SSH user name and password**.</span></span>
    - <span data-ttu-id="ef97b-159">**SQL server-aanmeldingsnaam en wachtwoord van de database**.</span><span class="sxs-lookup"><span data-stu-id="ef97b-159">**SQL database server login name and password**.</span></span>
    - <span data-ttu-id="ef97b-160">**_artifacts locatie**: Gebruik de standaardwaarde, tenzij u het gebruik van uw eigen backpac-bestand in een andere locatie wilt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="ef97b-160">**_artifacts Location**: Use the default value unless you want to use your own backpac file in a different location.</span></span>
    - <span data-ttu-id="ef97b-161">**locatie Sas-Token _artifacts**: laat dit veld leeg.</span><span class="sxs-lookup"><span data-stu-id="ef97b-161">**_artifacts Location Sas Token**: Leave it blank.</span></span>
    - <span data-ttu-id="ef97b-162">**De bestandsnaam Bacpac-**: Gebruik de standaardwaarde, tenzij u wilt gebruiken van uw eigen backpac-bestand.</span><span class="sxs-lookup"><span data-stu-id="ef97b-162">**Bacpac File Name**: Use the default value unless you want to use your own backpac file.</span></span>
     
     <span data-ttu-id="ef97b-163">De volgende waarden zijn vastgelegd in het gedeelte variabelen:</span><span class="sxs-lookup"><span data-stu-id="ef97b-163">The following values are hardcoded in the variables section:</span></span>
     
     | <span data-ttu-id="ef97b-164">Naam van het standaardopslagaccount</span><span class="sxs-lookup"><span data-stu-id="ef97b-164">Default storage account name</span></span> | <span data-ttu-id="ef97b-165"><CluterName>opslaan</span><span class="sxs-lookup"><span data-stu-id="ef97b-165"><CluterName>store</span></span> |
     | --- | --- |
     | <span data-ttu-id="ef97b-166">Azure SQL database-servernaam</span><span class="sxs-lookup"><span data-stu-id="ef97b-166">Azure SQL database server name</span></span> |<span data-ttu-id="ef97b-167"><ClusterName>dbserver</span><span class="sxs-lookup"><span data-stu-id="ef97b-167"><ClusterName>dbserver</span></span> |
     | <span data-ttu-id="ef97b-168">Naam van een Azure SQL-database</span><span class="sxs-lookup"><span data-stu-id="ef97b-168">Azure SQL database name</span></span> |<span data-ttu-id="ef97b-169"><ClusterName>DB</span><span class="sxs-lookup"><span data-stu-id="ef97b-169"><ClusterName>db</span></span> |
     
     <span data-ttu-id="ef97b-170">Noteer deze waarden.</span><span class="sxs-lookup"><span data-stu-id="ef97b-170">Please write down these values.</span></span>  <span data-ttu-id="ef97b-171">U hebt ze later in de zelfstudie nodig.</span><span class="sxs-lookup"><span data-stu-id="ef97b-171">You need them later in the tutorial.</span></span>

<span data-ttu-id="ef97b-172">3. Klik op **OK** om de parameters op te slaan.</span><span class="sxs-lookup"><span data-stu-id="ef97b-172">3.Click **OK** to save the parameters.</span></span>

<span data-ttu-id="ef97b-173">4. Klik vanuit de blade **Aangepaste implementatie** op de vervolgkeuzelijst **Resourcegroep**. Klik vervolgens op **Nieuw** om een nieuwe resourcegroep te maken.</span><span class="sxs-lookup"><span data-stu-id="ef97b-173">4.From the **Custom deployment** blade, click **Resource group** dropdown box, and then click **New** to create a new resource group.</span></span> <span data-ttu-id="ef97b-174">De resourcegroep is een container waarin het cluster, het afhankelijke opslagaccount en andere gekoppelde resources zijn gegroepeerd.</span><span class="sxs-lookup"><span data-stu-id="ef97b-174">The resource group is a container that groups the cluster, the dependent storage account and other linked resource.</span></span>

<span data-ttu-id="ef97b-175">5. Klik op **Juridische voorwaarden** en vervolgens op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="ef97b-175">5.Click **Legal terms**, and then click **Create**.</span></span>

<span data-ttu-id="ef97b-176">6. Klik op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="ef97b-176">6.Click **Create**.</span></span> <span data-ttu-id="ef97b-177">U ziet een nieuwe tegel met de titel implementatie indienen voor sjabloonimplementatie.</span><span class="sxs-lookup"><span data-stu-id="ef97b-177">You see a new tile titled Submitting deployment for Template deployment.</span></span> <span data-ttu-id="ef97b-178">Het duurt ongeveer 20 minuten om het cluster en de SQL-database te maken.</span><span class="sxs-lookup"><span data-stu-id="ef97b-178">It takes about around 20 minutes to create the cluster and SQL database.</span></span>

<span data-ttu-id="ef97b-179">Als u ervoor kiest om bestaande Azure SQL database of Microsoft SQL Server te gebruiken</span><span class="sxs-lookup"><span data-stu-id="ef97b-179">If you choose to use existing Azure SQL database or Microsoft SQL Server</span></span>

* <span data-ttu-id="ef97b-180">**Azure SQL-database**: U moet een firewallregel voor de Azure SQL database-server toegang toestaan via uw werkstation configureren.</span><span class="sxs-lookup"><span data-stu-id="ef97b-180">**Azure SQL database**: You must configure a firewall rule for the Azure SQL database server to allow access from your workstation.</span></span> <span data-ttu-id="ef97b-181">Zie voor instructies over het maken van een Azure SQL database en het configureren van de firewall [aan de slag met Azure SQL-database][sqldatabase-get-started].</span><span class="sxs-lookup"><span data-stu-id="ef97b-181">For instructions about creating an Azure SQL database and configuring the firewall, see [Get started using Azure SQL database][sqldatabase-get-started].</span></span> 
  
  > [!NOTE]
  > <span data-ttu-id="ef97b-182">Standaard kan een Azure SQL database verbindingen van Azure-services, zoals Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ef97b-182">By default an Azure SQL database allows connections from Azure services, such as Azure HDInsight.</span></span> <span data-ttu-id="ef97b-183">Als deze firewallinstelling is uitgeschakeld, moet u het inschakelen van de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="ef97b-183">If this firewall setting is disabled, you need to enable it from the Azure portal.</span></span> <span data-ttu-id="ef97b-184">Zie voor instructies over het maken van een Azure SQL database en firewallregels configureren [maken en configureren van de SQL-Database][sqldatabase-create-configue].</span><span class="sxs-lookup"><span data-stu-id="ef97b-184">For instruction about creating an Azure SQL database and configuring firewall rules, see [Create and Configure SQL Database][sqldatabase-create-configue].</span></span>
  > 
  > 
* <span data-ttu-id="ef97b-185">**SQL Server**: als uw HDInsight-cluster zich op hetzelfde virtuele netwerk in Azure SQL-Server, kunt u de stappen in dit artikel gebruiken om te importeren en exporteren van gegevens naar een SQL Server-database.</span><span class="sxs-lookup"><span data-stu-id="ef97b-185">**SQL Server**: If your HDInsight cluster is on the same virtual network in Azure as SQL Server, you can use the steps in this article to import and export data to a SQL Server database.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="ef97b-186">HDInsight ondersteunt alleen op basis van locatie virtuele netwerken en het werkt momenteel niet met virtuele netwerken op basis van een affiniteitsgroep.</span><span class="sxs-lookup"><span data-stu-id="ef97b-186">HDInsight supports only location-based virtual networks, and it does not currently work with affinity group-based virtual networks.</span></span>
  > 
  > 
  
  * <span data-ttu-id="ef97b-187">Als u wilt maken en configureren van een virtueel netwerk, Zie [een virtueel netwerk maken met de Azure-portal](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="ef97b-187">To create and configure a virtual network, see [Create a virtual network using the Azure portal](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>
    
    * <span data-ttu-id="ef97b-188">Wanneer u SQL Server in uw datacenter gebruikt, moet u het virtuele netwerk als configureren *site-naar-site* of *punt-naar-site*.</span><span class="sxs-lookup"><span data-stu-id="ef97b-188">When you are using SQL Server in your datacenter, you must configure the virtual network as *site-to-site* or *point-to-site*.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="ef97b-189">Voor **punt-naar-site** virtuele netwerken, SQL Server moeten worden uitgevoerd de VPN-client configuration toepassing, die beschikbaar via is de **Dashboard** van de configuratie van uw virtuele Azure-netwerk.</span><span class="sxs-lookup"><span data-stu-id="ef97b-189">For **point-to-site** virtual networks, SQL Server must be running the VPN client configuration application, which is available from the **Dashboard** of your Azure virtual network configuration.</span></span>
      > 
      > 
    * <span data-ttu-id="ef97b-190">Wanneer u SQL Server op Azure een virtuele machine gebruikt, kan de configuratie van een virtueel netwerk worden gebruikt als de virtuele machine die als host fungeert voor SQL Server een lid van hetzelfde virtuele netwerk als HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ef97b-190">When you are using SQL Server on an Azure virtual machine, any virtual network configuration can be used if the virtual machine hosting SQL Server is a member of the same virtual network as HDInsight.</span></span>
  * <span data-ttu-id="ef97b-191">Zie voor informatie over het maken van een HDInsight-cluster op een virtueel netwerk [maken Hadoop-clusters in HDInsight met aangepaste opties](hdinsight-hadoop-provision-linux-clusters.md)</span><span class="sxs-lookup"><span data-stu-id="ef97b-191">To create an HDInsight cluster on a virtual network, see [Create Hadoop clusters in HDInsight using custom options](hdinsight-hadoop-provision-linux-clusters.md)</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="ef97b-192">SQL Server moet ook authenticatie toestaan.</span><span class="sxs-lookup"><span data-stu-id="ef97b-192">SQL Server must also allow authentication.</span></span> <span data-ttu-id="ef97b-193">Een SQL Server-aanmelding moet u de stappen in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="ef97b-193">You must use a SQL Server login to complete the steps in this article.</span></span>
    > 
    > 

## <a name="run-sqoop-jobs"></a><span data-ttu-id="ef97b-194">Sqoop taken uitvoeren</span><span class="sxs-lookup"><span data-stu-id="ef97b-194">Run Sqoop jobs</span></span>
<span data-ttu-id="ef97b-195">HDInsight kunt Sqoop taken uitvoeren met behulp van een aantal methoden.</span><span class="sxs-lookup"><span data-stu-id="ef97b-195">HDInsight can run Sqoop jobs by using a variety of methods.</span></span> <span data-ttu-id="ef97b-196">Gebruik de volgende tabel om te bepalen welke methode is geschikt voor u en volg de koppeling voor een overzicht.</span><span class="sxs-lookup"><span data-stu-id="ef97b-196">Use the following table to decide which method is right for you, then follow the link for a walkthrough.</span></span>

| <span data-ttu-id="ef97b-197">**Gebruik deze** als u wilt dat...</span><span class="sxs-lookup"><span data-stu-id="ef97b-197">**Use this** if you want...</span></span> | <span data-ttu-id="ef97b-198">.. .an **interactieve** shell</span><span class="sxs-lookup"><span data-stu-id="ef97b-198">...an **interactive** shell</span></span> | <span data-ttu-id="ef97b-199">... **batch** verwerken</span><span class="sxs-lookup"><span data-stu-id="ef97b-199">...**batch** processing</span></span> | <span data-ttu-id="ef97b-200">.. .door dit **cluster-besturingssysteem**</span><span class="sxs-lookup"><span data-stu-id="ef97b-200">...with this **cluster operating system**</span></span> | <span data-ttu-id="ef97b-201">.. .from dit **clientbesturingssysteem**</span><span class="sxs-lookup"><span data-stu-id="ef97b-201">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="ef97b-202">SSH</span><span class="sxs-lookup"><span data-stu-id="ef97b-202">SSH</span></span>](hdinsight-use-sqoop-mac-linux.md) |<span data-ttu-id="ef97b-203">✔</span><span class="sxs-lookup"><span data-stu-id="ef97b-203">✔</span></span> |<span data-ttu-id="ef97b-204">✔</span><span class="sxs-lookup"><span data-stu-id="ef97b-204">✔</span></span> |<span data-ttu-id="ef97b-205">Linux</span><span class="sxs-lookup"><span data-stu-id="ef97b-205">Linux</span></span> |<span data-ttu-id="ef97b-206">Linux, Unix, Mac OS X of Windows</span><span class="sxs-lookup"><span data-stu-id="ef97b-206">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="ef97b-207">.NET-SDK voor Hadoop</span><span class="sxs-lookup"><span data-stu-id="ef97b-207">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-sqoop-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="ef97b-208">✔</span><span class="sxs-lookup"><span data-stu-id="ef97b-208">✔</span></span> |<span data-ttu-id="ef97b-209">Linux- of Windows</span><span class="sxs-lookup"><span data-stu-id="ef97b-209">Linux or Windows</span></span> |<span data-ttu-id="ef97b-210">Windows (voor nu)</span><span class="sxs-lookup"><span data-stu-id="ef97b-210">Windows (for now)</span></span> |
| [<span data-ttu-id="ef97b-211">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef97b-211">Azure PowerShell</span></span>](hdinsight-hadoop-use-sqoop-powershell.md) |&nbsp; |<span data-ttu-id="ef97b-212">✔</span><span class="sxs-lookup"><span data-stu-id="ef97b-212">✔</span></span> |<span data-ttu-id="ef97b-213">Linux- of Windows</span><span class="sxs-lookup"><span data-stu-id="ef97b-213">Linux or Windows</span></span> |<span data-ttu-id="ef97b-214">Windows</span><span class="sxs-lookup"><span data-stu-id="ef97b-214">Windows</span></span> |

## <a name="limitations"></a><span data-ttu-id="ef97b-215">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="ef97b-215">Limitations</span></span>
* <span data-ttu-id="ef97b-216">Bulksgewijs export - met Linux gebaseerde HDInsight, de Sqoop-connector gebruikt voor het exporteren van gegevens naar Microsoft SQL Server of Azure SQL Database biedt momenteel geen ondersteuning voor bulksgewijs invoegen.</span><span class="sxs-lookup"><span data-stu-id="ef97b-216">Bulk export - With Linux-based HDInsight, the Sqoop connector used to export data to Microsoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="ef97b-217">Batchverwerking - met HDInsight op basis van Linux, wanneer u de `-batch` bij het uitvoeren van invoeg-switch, Sqoop meerdere invoegen in plaats van de bewerkingen insert batchverwerking wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ef97b-217">Batching - With Linux-based HDInsight, When using the `-batch` switch when performing inserts, Sqoop performs multiple inserts instead of batching the insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef97b-218">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ef97b-218">Next steps</span></span>
<span data-ttu-id="ef97b-219">Nu hebt u geleerd hoe Sqoop gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ef97b-219">Now you have learned how to use Sqoop.</span></span> <span data-ttu-id="ef97b-220">Voor meer informatie zie:</span><span class="sxs-lookup"><span data-stu-id="ef97b-220">To learn more, see:</span></span>

* [<span data-ttu-id="ef97b-221">Hive gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="ef97b-221">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="ef97b-222">Pig gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="ef97b-222">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* <span data-ttu-id="ef97b-223">[Oozie gebruiken met HDInsight][hdinsight-use-oozie]: Sqoop gebruiken in een werkstroom Oozie in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="ef97b-223">[Use Oozie with HDInsight][hdinsight-use-oozie]: Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="ef97b-224">[Vertraging vluchtgegevens met HDInsight analyseren][hdinsight-analyze-flight-data]: Hive gebruiken voor het analyseren van vlucht gegevens uit te stellen en vervolgens Sqoop gebruiken om gegevens te exporteren naar een Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="ef97b-224">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]: Use Hive to analyze flight delay data, and then use Sqoop to export data to an Azure SQL database.</span></span>
* <span data-ttu-id="ef97b-225">[Gegevens uploaden naar HDInsight][hdinsight-upload-data]: vinden van andere methoden voor het uploaden van gegevens naar HDInsight/Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="ef97b-225">[Upload data to HDInsight][hdinsight-upload-data]: Find other methods for uploading data to HDInsight/Azure Blob storage.</span></span>

## <a name="appendix-a---a-powershell-sample"></a><span data-ttu-id="ef97b-226">Bijlage A - een PowerShell-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="ef97b-226">Appendix A - a PowerShell sample</span></span>
<span data-ttu-id="ef97b-227">De PowerShell-voorbeeld voert de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="ef97b-227">The PowerShell sample performs the following steps:</span></span>

1. <span data-ttu-id="ef97b-228">Verbinding maken met Azure.</span><span class="sxs-lookup"><span data-stu-id="ef97b-228">Connect to Azure.</span></span>
2. <span data-ttu-id="ef97b-229">Maak een Azure-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="ef97b-229">Create an Azure resource group.</span></span> <span data-ttu-id="ef97b-230">Zie voor meer informatie [Azure PowerShell gebruiken met Azure Resource Manager](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="ef97b-230">For more information, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md)</span></span>
3. <span data-ttu-id="ef97b-231">Een Azure SQL Database-server, een Azure SQL database en twee tabellen maken.</span><span class="sxs-lookup"><span data-stu-id="ef97b-231">Create an Azure SQL Database server, an Azure SQL database, and two tables.</span></span> 
   
    <span data-ttu-id="ef97b-232">Als u SQL Server in plaats daarvan gebruikt, gebruikt u de volgende instructies om de tabellen te maken:</span><span class="sxs-lookup"><span data-stu-id="ef97b-232">If you use SQL Server instead, use the following statements to create the tables:</span></span>
   
        CREATE TABLE [dbo].[log4jlogs](
         [t1] [nvarchar](50),
         [t2] [nvarchar](50),
         [t3] [nvarchar](50),
         [t4] [nvarchar](50),
         [t5] [nvarchar](50),
         [t6] [nvarchar](50),
         [t7] [nvarchar](50))
   
        CREATE TABLE [dbo].[mobiledata](
         [clientid] [nvarchar](50),
         [querytime] [nvarchar](50),
         [market] [nvarchar](50),
         [deviceplatform] [nvarchar](50),
         [devicemake] [nvarchar](50),
         [devicemodel] [nvarchar](50),
         [state] [nvarchar](50),
         [country] [nvarchar](50),
         [querydwelltime] [float],
         [sessionid] [bigint],
         [sessionpagevieworder][bigint])
   
    <span data-ttu-id="ef97b-233">De eenvoudigste manier om te onderzoeken van de database en tabellen is Visual Studio gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ef97b-233">The easiest way to examine the database and tables is to use Visual Studio.</span></span> <span data-ttu-id="ef97b-234">De databaseserver en de database kunnen worden gecontroleerd met de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="ef97b-234">The database server and the database can be examined using the Azure portal.</span></span>
4. <span data-ttu-id="ef97b-235">Maak een HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="ef97b-235">Create an HDInsight cluster.</span></span>
   
    <span data-ttu-id="ef97b-236">Als u wilt onderzoeken van het cluster, kunt u de Azure portal of Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ef97b-236">To examine the cluster, you can use the Azure portal or Azure PowerShell.</span></span>
5. <span data-ttu-id="ef97b-237">Het bronbestand van de gegevens vooraf verwerken.</span><span class="sxs-lookup"><span data-stu-id="ef97b-237">Pre-process the source data file.</span></span>
   
    <span data-ttu-id="ef97b-238">In deze zelfstudie maakt u een een logboekbestand log4j (een bestand met scheidingstekens) en een Hive-tabel exporteren naar een Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="ef97b-238">In this tutorial, you export a log4j log file (a delimited file) and a Hive table to an Azure SQL database.</span></span> <span data-ttu-id="ef97b-239">Het bestand met scheidingstekens heet */example/data/sample.log*.</span><span class="sxs-lookup"><span data-stu-id="ef97b-239">The delimited file is called */example/data/sample.log*.</span></span> <span data-ttu-id="ef97b-240">Eerder in de zelfstudie hebt u enkele voorbeelden van log4j logboeken gezien.</span><span class="sxs-lookup"><span data-stu-id="ef97b-240">Earlier in the tutorial, you saw a few samples of log4j logs.</span></span> <span data-ttu-id="ef97b-241">In het logboekbestand zijn er enkele lege regels en sommige regels zoals de volgende:</span><span class="sxs-lookup"><span data-stu-id="ef97b-241">In the log file, there are some empty lines and some lines similar to these:</span></span>
   
        java.lang.Exception: 2012-02-03 20:11:35 SampleClass2 [FATAL] unrecoverable system problem at id 609774657
            at com.osa.mocklogger.MockLogger$2.run(MockLogger.java:83)
   
    <span data-ttu-id="ef97b-242">Dit is andere voorbeelden die deze gegevens gebruiken, maar deze uitzonderingen moet worden verwijderd voordat we in de Azure SQL-database of SQL Server kunt importeren.</span><span class="sxs-lookup"><span data-stu-id="ef97b-242">This is fine for other examples that use this data, but we must remove these exceptions before we can import into the Azure SQL database or SQL Server.</span></span> <span data-ttu-id="ef97b-243">Sqoop exporteren niet worden uitgevoerd als er een lege tekenreeks of een regel met een minder-elementen dan het aantal velden die zijn gedefinieerd in de Azure SQL database-tabel.</span><span class="sxs-lookup"><span data-stu-id="ef97b-243">Sqoop export  fails if there is an empty string or a line with a fewer elements than the number of fields defined in the Azure SQL database table.</span></span> <span data-ttu-id="ef97b-244">De tabel log4jlogs heeft 7 type string-velden.</span><span class="sxs-lookup"><span data-stu-id="ef97b-244">The log4jlogs table has 7 string-type fields.</span></span>
   
    <span data-ttu-id="ef97b-245">Deze procedure maakt u een nieuw bestand op het cluster: tutorials/usesqoop/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="ef97b-245">This procedure creates a new file on the cluster: tutorials/usesqoop/data/sample.log.</span></span> <span data-ttu-id="ef97b-246">Als u wilt onderzoeken het gewijzigde bestand, kunt u de Azure-portal, een hulpprogramma voor Azure Storage explorer of Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ef97b-246">To examine the modified data file, you can use the Azure portal, an Azure Storage explorer tool, or Azure PowerShell.</span></span> <span data-ttu-id="ef97b-247">[Aan de slag met HDInsight] [ hdinsight-get-started] is een voorbeeld van code voor het gebruik van Azure PowerShell te downloaden van een bestand en inhoud van het bestand weer te geven.</span><span class="sxs-lookup"><span data-stu-id="ef97b-247">[Get started with HDInsight][hdinsight-get-started] has a code sample for using Azure PowerShell to download a file and display the file content.</span></span>
6. <span data-ttu-id="ef97b-248">Een gegevensbestand exporteren naar de Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="ef97b-248">Export a data file to the Azure SQL database.</span></span>
   
    <span data-ttu-id="ef97b-249">Het bronbestand is tutorials/usesqoop/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="ef97b-249">The source file is tutorials/usesqoop/data/sample.log.</span></span> <span data-ttu-id="ef97b-250">De tabel waar de gegevens worden geëxporteerd naar heet log4jlogs.</span><span class="sxs-lookup"><span data-stu-id="ef97b-250">The table where the data is exported to is called log4jlogs.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ef97b-251">Anders dan de verbindingsinformatie werken de stappen in deze sectie moeten voor een Azure SQL database of SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ef97b-251">Other than connection string information, the steps in this section should work for an Azure SQL database or for SQL Server.</span></span> <span data-ttu-id="ef97b-252">Deze stappen zijn getest met behulp van de volgende configuratie:</span><span class="sxs-lookup"><span data-stu-id="ef97b-252">These steps were tested by using the following configuration:</span></span>
   > 
   > * <span data-ttu-id="ef97b-253">**Punt-naar-site-configuratie voor virtuele Azure-netwerk**: een virtueel netwerk het HDInsight-cluster verbonden met een SQL-Server in een particulier datacenter.</span><span class="sxs-lookup"><span data-stu-id="ef97b-253">**Azure virtual network point-to-site configuration**: A virtual network connected the HDInsight cluster to a SQL Server in a private datacenter.</span></span> <span data-ttu-id="ef97b-254">Zie [een punt-naar-Site-VPN configureren in de beheerportal](../vpn-gateway/vpn-gateway-point-to-site-create.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ef97b-254">See [Configure a Point-to-Site VPN in the Management Portal](../vpn-gateway/vpn-gateway-point-to-site-create.md) for more information.</span></span>
   > * <span data-ttu-id="ef97b-255">**Azure HDInsight 3.1**: Zie [maken Hadoop-clusters in HDInsight met aangepaste opties](hdinsight-hadoop-provision-linux-clusters.md) voor informatie over het maken van een cluster in een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="ef97b-255">**Azure HDInsight 3.1**: See [Create Hadoop clusters in HDInsight using custom options](hdinsight-hadoop-provision-linux-clusters.md) for information about creating a cluster on a virtual network.</span></span>
   > * <span data-ttu-id="ef97b-256">**SQL Server 2014**: is geconfigureerd voor verificatie en de VPN-client uitgevoerd configuratiepakket naar een veilige verbinding met het virtuele netwerk toestaan.</span><span class="sxs-lookup"><span data-stu-id="ef97b-256">**SQL Server 2014**: Configured to allow authentication and running the VPN client configuration package to connect securely to the virtual network.</span></span>
   > 
   > 
7. <span data-ttu-id="ef97b-257">Een Hive-tabel exporteren naar de Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="ef97b-257">Export a Hive table to the Azure SQL database.</span></span>
8. <span data-ttu-id="ef97b-258">De tabel mobiledata importeren naar het HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="ef97b-258">Import the mobiledata table to the HDInsight cluster.</span></span>
   
    <span data-ttu-id="ef97b-259">Als u wilt onderzoeken het gewijzigde bestand, kunt u de Azure-portal, een hulpprogramma voor Azure Storage explorer of Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ef97b-259">To examine the modified data file, you can use the Azure portal, an Azure Storage explorer tool, or Azure PowerShell.</span></span>  <span data-ttu-id="ef97b-260">[Aan de slag met HDInsight] [ hdinsight-get-started] is een voorbeeld van code over het gebruik van Azure PowerShell te downloaden van een bestand en inhoud van het bestand weer te geven.</span><span class="sxs-lookup"><span data-stu-id="ef97b-260">[Get started with HDInsight][hdinsight-get-started] has a code sample about using Azure PowerShell to download a file and display the file content.</span></span>

### <a name="the-powershell-sample"></a><span data-ttu-id="ef97b-261">De PowerShell-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="ef97b-261">The PowerShell sample</span></span>
    # Prepare an Azure SQL database to be used by the Sqoop tutorial

    #region - provide the following values

    $subscriptionID = "<Enter your Azure Subscription ID>"

    $sqlDatabaseLogin = "<Enter a SQL Database Login name>" #SQL Database server login
    $sqlDatabasePassword = "<Enter a Password>"

    $httpUserName = "admin"  #HDInsight cluster username
    $httpPassword = "<Enter a Password>"

    # used for creating Azure service names
    $nameToken = "<Enter an alias>" 
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")
    #endregion

    #region - variables

    # Resource group variables
    $resourceGroupName = $namePrefix + "rg"
    $location = "East US 2" # used by all Azure services defined in this tutorial

    # SQL database varialbes
    $sqlDatabaseServerName = $namePrefix + "sqldbserver"
    $sqlDatabaseName = $namePrefix + "sqldb"
    $sqlDatabaseConnectionString = "Data Source=$sqlDatabaseServerName.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $sqlDatabaseMaxSizeGB = 10

    # Used for retrieving external IP address and creating firewall rules
    $ipAddressRestService = "http://bot.whatismyipaddress.com"
    $fireWallRuleName = "UseSqoop"

    # Used for creating tables and clustered indexes
    $cmdCreateLog4jTable = "CREATE TABLE [dbo].[log4jlogs](
        [t1] [nvarchar](50),
        [t2] [nvarchar](50),
        [t3] [nvarchar](50),
        [t4] [nvarchar](50),
        [t5] [nvarchar](50),
        [t6] [nvarchar](50),
        [t7] [nvarchar](50))"

    $cmdCreateLog4jClusteredIndex = "CREATE CLUSTERED INDEX log4jlogs_clustered_index on log4jlogs(t1)"

    $cmdCreateMobileTable = " CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder][bigint])"

    $cmdCreateMobileDataClusteredIndex = "CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(clientid)"

    # HDInsight variables
    $hdinsightClusterName = $namePrefix + "hdi"
    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $hdinsightClusterName
    #endregion

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    #region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #endregion

    #region - Create Azure resouce group
    Write-Host "`nCreating an Azure resource group ..." -ForegroundColor Green
    try{
        Get-AzureRmResourceGroup -Name $resourceGroupName
    }
    catch{
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    }
    #endregion

    #region - Create Azure SQL database server
    Write-Host "`nCreating an Azure SQL Database server ..." -ForegroundColor Green
    try{
        Get-AzureRmSqlServer -ServerName $sqlDatabaseServerName -ResourceGroupName $resourceGroupName}
    catch{
        Write-Host "`nCreating SQL Database server ..."  -ForegroundColor Green

        $sqlDatabasePW = ConvertTo-SecureString -String $sqlDatabasePassword -AsPlainText -Force
        $credential = New-Object System.Management.Automation.PSCredential($sqlDatabaseLogin,$sqlDatabasePW)

        $sqlDatabaseServerName = (New-AzureRmSqlServer `
                                    -ResourceGroupName $resourceGroupName `
                                    -ServerName $sqlDatabaseServerName `
                                    -SqlAdministratorCredentials $credential `
                                    -Location $location).ServerName
        Write-Host "`tThe new SQL database server name is $sqlDatabaseServerName." -ForegroundColor Cyan

        Write-Host "`nCreating firewall rule, $fireWallRuleName ..." -ForegroundColor Green
        $workstationIPAddress = Invoke-RestMethod $ipAddressRestService
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-workstation" `
            -StartIpAddress $workstationIPAddress `
            -EndIpAddress $workstationIPAddress

        #To allow other Azure services to access the server add a firewall rule and set both the StartIpAddress and EndIpAddress to 0.0.0.0. 
        #Note that this allows Azure traffic from any Azure subscription to access the server.
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-Azureservices" `
            -StartIpAddress "0.0.0.0" `
            -EndIpAddress "0.0.0.0"
    }

    #endregion

    #region - Create and validate Azure SQL database
    Write-Host "`nCreating an Azure SQL database ..." -ForegroundColor Green

    try {
        Get-AzureRmSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName
    }
    catch {
        Write-Host "`nCreating SQL Database, $sqlDatabaseName ..."  -ForegroundColor Green
        New-AzureRMSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName `
            -Edition "Standard" `
            -RequestedServiceObjectiveName "S1"
    }

    #endregion

    #region - Create tables
    Write-Host "Creating the log4jlogs table and the mobiledata table ..." -ForegroundColor Green

    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = $sqlDatabaseConnectionString
    $conn.Open()

    # Create the log4jlogs table and index
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.Connection = $conn
    $cmd.CommandText = $cmdCreateLog4jTable
    $ret = $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateLog4jClusteredIndex
    $cmd.ExecuteNonQuery()

    # Create the mobiledata table and index
    $cmd.CommandText = $cmdCreateMobileTable
    $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateMobileDataClusteredIndex
    $cmd.ExecuteNonQuery()

    $conn.close()

    #endregion


    #region - Create HDInsight cluster

    Write-Host "Creating the HDInsight cluster and the dependent services ..." -ForegroundColor Green

    # Create the default storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_LRS

    # Create the default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                        -StorageAccountName $defaultStorageAccountName `
                                        -StorageAccountKey $defaultStorageAccountKey 
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext 

    # Create the HDInsight cluster
    $pw = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -Location $location `
        -ClusterType Hadoop `
        -OSType Windows `
        -ClusterSizeInNodes 2 `
        -HttpCredential $httpCredential `
        -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultStorageContainer $defaultBlobContainerName 

    # Validate the cluster
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName
    #endregion

    #region - pre-process the source file

    Write-Host "Preprocessing the source file ..." -ForegroundColor Green

    # This procedure creates a new file with $destBlobName
    $sourceBlobName = "example/data/sample.log"
    $destBlobName = "tutorials/usesqoop/data/sample.log"

    # Define the connection string
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    # Create block blob objects referencing the source and destination blob.
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $sourceBlob = $storageContainer.GetBlockBlobReference($sourceBlobName)
    $destBlob = $storageContainer.GetBlockBlobReference($destBlobName)

    # Define a MemoryStream and a StreamReader for reading from the source file
    $stream = New-Object System.IO.MemoryStream
    $stream = $sourceBlob.OpenRead()
    $sReader = New-Object System.IO.StreamReader($stream)

    # Define a MemoryStream and a StreamWriter for writing into the destination file
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream

    # Pre-process the source blob
    $exString = "java.lang.Exception:"
    while(-Not $sReader.EndOfStream){
        $line = $sReader.ReadLine()
        $split = $line.Split(" ")

        # remove the "java.lang.Exception" from the first element of the array
        # for example: java.lang.Exception: 2012-02-03 19:11:02 SampleClass8 [WARN] problem finding id 153454612
        if ($split[0] -eq $exString){
            #create a new ArrayList to remove $split[0]
            $newArray = [System.Collections.ArrayList] $split
            $newArray.Remove($exString)

            # update $split and $line
            $split = $newArray
            $line = $newArray -join(" ")
        }

        # remove the lines that has less than 7 elements
        if ($split.count -ge 7){
            write-host $line
            $writeStream.WriteLine($line)
        }
    }

    # Write to the destination blob
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    #endregion

    #region - export a log file from the cluster to the SQL database

    Write-Host "Preprocessing the source file ..." -ForegroundColor Green

    $tableName_log4j = "log4jlogs"

    # Connection string for Azure SQL Database.
    # Comment if using SQL Server
    $connectionString = "jdbc:sqlserver://$sqlDatabaseServerName.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServerName;password=$sqlDatabasePassword;database=$sqlDatabaseName"
    # Connection string for SQL Server.
    # Uncomment if using SQL Server.
    #$connectionString = "jdbc:sqlserver://$sqlDatabaseServerName;user=$sqlDatabaseLogin;password=$sqlDatabasePassword;database=$sqlDatabaseName"

    $exportDir_log4j = "/tutorials/usesqoop/data"

    # Submit a Sqoop job
    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "export --connect $connectionString --table $tableName_log4j --export-dir $exportDir_log4j --input-fields-terminated-by \0x20 -m 1"
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose
    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -HttpCredential $httpCredential -JobId $sqoopJob.JobId -DisplayOutputType StandardError
    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -HttpCredential $httpCredential -JobId $sqoopJob.JobId -DisplayOutputType StandardOutput

    #endregion

    #region - export a Hive table

    $tableName_mobile = "mobiledata"
    $exportDir_mobile = "/hive/warehouse/hivesampletable"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "export --connect $connectionString --table $tableName_mobile --export-dir $exportDir_mobile --fields-terminated-by \t -m 1"
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardOutput

    #endregion

    #region - import a database

    $targetDir_mobile = "/tutorials/usesqoop/importeddata/"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "import --connect $connectionString --table $tableName_mobile --target-dir $targetDir_mobile --fields-terminated-by \t --lines-terminated-by \n -m 1"

    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardOutput

    #endregion



[azure-management-portal]: https://portal.azure.com/

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[sqldatabase-get-started]: ../sql-database/sql-database-get-started.md
[sqldatabase-create-configue]: ../sql-database/sql-database-get-started.md

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[sqoop-user-guide-1.4.4]: https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html
