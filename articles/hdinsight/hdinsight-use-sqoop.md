---
title: Apache Sqoop aaaRun voor taken met een Azure HDInsight (Hadoop) | Microsoft Docs
description: Informatie over hoe Azure PowerShell toouse van een werkstation toorun Sqoop importeren en exporteren tussen een Hadoop-cluster en een Azure SQL database.
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
ms.openlocfilehash: bdac507704937d77921c9c13d70aa2434c7e3be4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-sqoop-with-hadoop-in-hdinsight"></a>Sqoop gebruiken met Hadoop in HDInsight
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

Meer informatie over hoe toouse Sqoop in HDInsight tooimport en exporteren tussen een HDInsight-cluster en Azure SQL database of SQL Server-database.

Hoewel Hadoop een natuurlijke keuze voor het verwerken van ongestructureerde en semigestructureerde gegevens, zoals Logboeken en bestanden, is er mogelijk ook een noodzaak tooprocess gestructureerde gegevens die zijn opgeslagen in de relationele databases.

[Sqoop] [ sqoop-user-guide-1.4.4] is een hulpprogramma waarmee u tootransfer gegevens tussen Hadoop-clusters en relationele databases. U kunt deze tooimport gegevens uit een relationele databasebeheersysteem (RDBMS), zoals SQL Server, MySQL of Oracle in Hallo Hadoop distributed file system (HDFS) gegevens in Hadoop met MapReduce of Hive Hallo transformeren en vervolgens exporteren Hallo gegevens terug in een RDBMS. In deze zelfstudie maakt u een SQL Server-database gebruikt voor de relationele database.

Zie voor versies die worden ondersteund op HDInsight-clusters Sqoop [wat is er nieuw in Hallo-clusterversies geleverd door HDInsight?][hdinsight-versions]

## <a name="understand-hello-scenario"></a>Hallo scenario begrijpen

HDInsight-cluster wordt geleverd met voorbeeldgegevens. U na twee voorbeelden hello gebruiken:

* Een logboekbestand log4j, bevindt zich op */example/data/sample.log*. Hallo na logboeken worden opgehaald uit bestand Hallo:
  
        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...
* Een Hive-tabel met de naam *hivesampletable*, die verwijzingen Hallo gegevensbestand zich bevindt op */hive/warehouse/hivesampletable*. Hallo tabel bevat de gegevens van sommige mobiele apparaten. 
  
  | Veld | Gegevenstype |
  | --- | --- |
  | clientid |Tekenreeks |
  | querytime |Tekenreeks |
  | markt |Tekenreeks |
  | deviceplatform |Tekenreeks |
  | devicemake |Tekenreeks |
  | devicemodel |Tekenreeks |
  | state |Tekenreeks |
  | Land |Tekenreeks |
  | querydwelltime |dubbele |
  | sessie-id |bigint |
  | sessionpagevieworder |bigint |

Exporteer eerst *sample.log* en *hivesampletable* toohello Azure SQL database of Server tooSQL en importtabel Hallo Hallo gegevens op mobiele apparaten met back-tooHDInsight met behulp van Hallo volgende pad:

    /tutorials/usesqoop/importeddata

## <a name="create-cluster-and-sql-database"></a>Cluster- en SQL-database maken
Deze sectie leest u hoe toocreate een cluster, een SQL-Database en Hallo SQL database, schema voor het actieve Hallo zelfstudie gebruik hello Azure portal en een Azure Resource Manager-sjabloon. Hallo-sjabloon kunt u vinden in [Azure-Snelstartsjablonen](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-sql-database/). Hallo Resource Manager-sjabloon roept een Bacpac-pakket toodeploy Hallo tabel schema's tooSQL-database.  Hallo Bacpac-pakket bevindt zich in een openbare blobcontainer, https://hditutorialdata.blob.core.windows.net/usesqoop/SqoopTutorial-2016-2-23-11-2.bacpac. Als u toouse een privé-container voor Hallo Bacpac-bestanden wilt, gebruikt u Hallo waarden in de sjabloon hello te volgen:
   
        "storageKeyType": "Primary",
        "storageKey": "<TheAzureStorageAccountKey>",

Als u liever toouse Azure PowerShell toocreate Hallo cluster en Hallo SQL-Database, Zie [bijlage A](#appendix-a---a-powershell-sample).

1. Klik op Hallo installatiekopie tooopen Resource Manager-sjabloon in hello Azure-portal te volgen.         
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-sql-database%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-use-sqoop/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   

2. Voer de volgende eigenschappen Hallo:

    - **Abonnement**: Voer uw Azure-abonnement.
    - **Resourcegroep**: Maak een nieuwe Azure-resourcegroep of Selecteer een bestaande resourcegroep.  Een resourcegroep is voor management doel.  Er is een container voor objecten.
    - **Locatie**: Selecteer een regio.
    - **Clusternaam**: Voer een naam voor Hallo Hadoop-cluster.
    - **Cluster-aanmeldingsnaam en wachtwoord**: Hallo standaardaanmeldnaam is admin.
    - **SSH-aanmeldgegevens**.
    - **SQL server-aanmeldingsnaam en wachtwoord van de database**.
    - **_artifacts locatie**: Hallo standaardwaarde gebruikt, tenzij u uw eigen backpac-bestand op een andere locatie toouse wilt.
    - **locatie Sas-Token _artifacts**: laat dit veld leeg.
    - **De bestandsnaam Bacpac-**: Hallo standaardwaarde gebruikt, tenzij u uw eigen bestand backpac toouse wilt.
     
     Hallo volgende waarden zijn vastgelegd in de sectie met sjabloonvariabelen Hallo:
     
     | Naam van het standaardopslagaccount | <CluterName>opslaan |
     | --- | --- |
     | Azure SQL database-servernaam |<ClusterName>dbserver |
     | Naam van een Azure SQL-database |<ClusterName>DB |
     
     Noteer deze waarden.  U moet ze later in de zelfstudie Hallo.

3. Klik op **OK** toosave Hallo parameters.

4. Klik vanuit Hallo **aangepaste implementatie** blade, klikt u op **resourcegroep** dropdown vak en klik vervolgens op **nieuw** toocreate een nieuwe resourcegroep. Hallo-resourcegroep is een container waarin Hallo-cluster, Hallo afhankelijke opslagaccount en andere gekoppelde resources zijn gegroepeerd.

5. Klik op **Juridische voorwaarden** en vervolgens op **Maken**.

6. Klik op **Maken**. U ziet een nieuwe tegel met de titel implementatie indienen voor sjabloonimplementatie. Het duurt ongeveer 20 minuten toocreate Hallo cluster en de SQL-database.

Als u ervoor toouse bestaande Azure SQL database of Microsoft SQL Server kiest

* **Azure SQL-database**: U moet een firewallregel voor toegang tot de Azure SQL database-server tooallow Hallo configureren vanuit uw werkstation. Zie voor instructies over het maken van een Azure SQL database en configureren van Hallo firewall [aan de slag met Azure SQL-database][sqldatabase-get-started]. 
  
  > [!NOTE]
  > Standaard kan een Azure SQL database verbindingen van Azure-services, zoals Azure HDInsight. Als deze firewallinstelling is uitgeschakeld, moet u tooenable uit hello Azure-portal. Zie voor instructies over het maken van een Azure SQL database en firewallregels configureren [maken en configureren van de SQL-Database][sqldatabase-create-configue].
  > 
  > 
* **SQL Server**: als uw HDInsight-cluster op Hallo hetzelfde virtuele netwerk in Azure SQL-Server, kunt u Hallo stappen in dit artikel tooimport en exporteren van gegevens tooa SQL Server-database.
  
  > [!NOTE]
  > HDInsight ondersteunt alleen op basis van locatie virtuele netwerken en het werkt momenteel niet met virtuele netwerken op basis van een affiniteitsgroep.
  > 
  > 
  
  * toocreate en een virtueel netwerk configureren, Zie [een virtueel netwerk maken met Azure-portal Hallo](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).
    
    * Wanneer u SQL Server in uw datacenter gebruikt, moet u configureren Hallo virtuele netwerk als *site-naar-site* of *punt-naar-site*.
      
      > [!NOTE]
      > Voor **punt-naar-site** virtuele netwerken, SQL Server moeten worden uitgevoerd Hallo VPN-client configuration toepassing, die beschikbaar via Hallo is **Dashboard** van de configuratie van uw virtuele Azure-netwerk.
      > 
      > 
    * Wanneer u SQL Server op Azure een virtuele machine gebruikt, de configuratie van een virtueel netwerk kan worden gebruikt als Hallo virtuele machine die als host fungeert voor SQL Server deel uit van Hallo maakt hetzelfde virtuele netwerk als HDInsight.
  * Zie toocreate een HDInsight-cluster op een virtueel netwerk [maken Hadoop-clusters in HDInsight met aangepaste opties](hdinsight-hadoop-provision-linux-clusters.md)
    
    > [!NOTE]
    > SQL Server moet ook authenticatie toestaan. U moet een SQL-Server aanmelding toocomplete Hallo in dit artikel stappen gebruiken.
    > 
    > 

## <a name="run-sqoop-jobs"></a>Sqoop taken uitvoeren
HDInsight kunt Sqoop taken uitvoeren met behulp van een aantal methoden. Gebruik Hallo tabel toodecide methode die geschikt voor u is te volgen en Hallo-koppeling voor de procedure volgen.

| **Gebruik deze** als u wilt dat... | .. .an **interactieve** shell | ... **batch** verwerken | .. .door dit **cluster-besturingssysteem** | .. .from dit **clientbesturingssysteem** |
|:--- |:---:|:---:|:--- |:--- |
| [SSH](hdinsight-use-sqoop-mac-linux.md) |✔ |✔ |Linux |Linux, Unix, Mac OS X of Windows |
| [.NET-SDK voor Hadoop](hdinsight-hadoop-use-sqoop-dotnet-sdk.md) |&nbsp; |✔ |Linux- of Windows |Windows (voor nu) |
| [Azure PowerShell](hdinsight-hadoop-use-sqoop-powershell.md) |&nbsp; |✔ |Linux- of Windows |Windows |

## <a name="limitations"></a>Beperkingen
* Bulk-export - met Linux gebaseerde HDInsight, Hallo Sqoop connector die wordt gebruikt tooexport gegevens tooMicrosoft SQL Server of Azure SQL Database biedt momenteel geen ondersteuning voor bulksgewijs invoegen.
* Batchverwerking - met HDInsight op basis van Linux bij gebruik van Hallo `-batch` bij het uitvoeren van invoeg-switch, Sqoop meerdere invoegen in plaats van batchverwerking Hallo insert-bewerkingen uitvoert.

## <a name="next-steps"></a>Volgende stappen
Nu u hebt geleerd hoe toouse Sqoop. toolearn meer, Zie:

* [Hive gebruiken met HDInsight](hdinsight-use-hive.md)
* [Pig gebruiken met HDInsight](hdinsight-use-pig.md)
* [Oozie gebruiken met HDInsight][hdinsight-use-oozie]: Sqoop gebruiken in een werkstroom Oozie in te grijpen.
* [Vertraging vluchtgegevens met HDInsight analyseren][hdinsight-analyze-flight-data]: tooanalyze vlucht Hive gebruiken gegevens uit te stellen en vervolgens Sqoop tooexport tooan Azure SQL database te gebruiken.
* [Uploaden van gegevens tooHDInsight][hdinsight-upload-data]: vinden van andere methoden voor het uploaden van gegevens tooHDInsight/Azure Blob-opslag.

## <a name="appendix-a---a-powershell-sample"></a>Bijlage A - een PowerShell-voorbeeld
Hallo PowerShell-voorbeeld voert Hallo stappen te volgen:

1. Verbinding maken met tooAzure.
2. Maak een Azure-resourcegroep. Zie voor meer informatie [Azure PowerShell gebruiken met Azure Resource Manager](../powershell-azure-resource-manager.md)
3. Een Azure SQL Database-server, een Azure SQL database en twee tabellen maken. 
   
    Als u SQL Server in plaats daarvan gebruiken, gebruikt u Hallo instructies toocreate Hallo tabellen na:
   
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
   
    Hallo gemakkelijkste manier tooexamine Hallo database en tabellen is toouse Visual Studio. Hallo-databaseserver en hello database kunnen worden gecontroleerd met hello Azure-portal.
4. Maak een HDInsight-cluster.
   
    tooexamine hello cluster, kunt u hello Azure-portal of Azure PowerShell gebruiken.
5. Hallo brongegevensbestand vooraf verwerken.
   
    In deze zelfstudie maakt exporteren u een logboekbestand log4j (een bestand met scheidingstekens) en een Hive-tabel tooan Azure SQL database. Hallo gescheiden bestand heet */example/data/sample.log*. Eerder in Hallo-zelfstudie hebt u enkele voorbeelden van log4j logboeken gezien. Hallo-logboekbestand zijn sommige lege regels en sommige regels vergelijkbare toothese:
   
        java.lang.Exception: 2012-02-03 20:11:35 SampleClass2 [FATAL] unrecoverable system problem at id 609774657
            at com.osa.mocklogger.MockLogger$2.run(MockLogger.java:83)
   
    Dit is andere voorbeelden die deze gegevens gebruiken, maar deze uitzonderingen moet worden verwijderd voordat we in hello Azure SQL database of SQL Server kunt importeren. Sqoop exporteren niet worden uitgevoerd als er een lege tekenreeks of een regel met een minder-elementen dan het aantal velden in Azure SQL-databasetabel Hallo Hallo. Hallo log4jlogs tabel heeft 7 type string-velden.
   
    Deze procedure maakt u een nieuw bestand op Hallo-cluster: tutorials/usesqoop/data/sample.log. tooexamine hello gewijzigde gegevensbestand, kunt u hello Azure-portal, een hulpprogramma voor Azure Storage explorer of Azure PowerShell. [Aan de slag met HDInsight] [ hdinsight-get-started] heeft een code voorbeeld voor het gebruik van Azure PowerShell toodownload een bestand en de bestandsinhoud Hallo weer te geven.
6. Exporteren van een bestand toohello Azure SQL-database.
   
    Hallo-bronbestand is tutorials/usesqoop/data/sample.log. Hallo tabel Hallo gegevens geëxporteerde toois log4jlogs genoemd.
   
   > [!NOTE]
   > Hallo stappen in deze sectie moeten dan de verbindingsinformatie samenwerken voor een Azure SQL database of SQL Server. Deze stappen zijn getest met behulp van Hallo volgende configuratie:
   > 
   > * **Punt-naar-site-configuratie voor virtuele Azure-netwerk**: een virtueel netwerk verbonden Hallo HDInsight-cluster tooa SQL Server in een particulier datacenter. Zie [een punt-naar-Site-VPN configureren in Hallo-beheerportal](../vpn-gateway/vpn-gateway-point-to-site-create.md) voor meer informatie.
   > * **Azure HDInsight 3.1**: Zie [maken Hadoop-clusters in HDInsight met aangepaste opties](hdinsight-hadoop-provision-linux-clusters.md) voor informatie over het maken van een cluster in een virtueel netwerk.
   > * **SQL Server 2014**: tooallow verificatie en actieve Hallo VPN-client configuration pakket tooconnect veilig geconfigureerd toohello virtueel netwerk.
   > 
   > 
7. Exporteren van een Hive-tabel toohello Azure SQL database.
8. Importeer Hallo mobiledata tabel toohello HDInsight-cluster.
   
    tooexamine hello gewijzigde gegevensbestand, kunt u hello Azure-portal, een hulpprogramma voor Azure Storage explorer of Azure PowerShell.  [Aan de slag met HDInsight] [ hdinsight-get-started] heeft een code voorbeeld over het gebruik van Azure PowerShell toodownload een bestand en de bestandsinhoud Hallo weer te geven.

### <a name="hello-powershell-sample"></a>Hallo PowerShell-voorbeeld
    # Prepare an Azure SQL database toobe used by hello Sqoop tutorial

    #region - provide hello following values

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

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
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

        #tooallow other Azure services tooaccess hello server add a firewall rule and set both hello StartIpAddress and EndIpAddress too0.0.0.0. 
        #Note that this allows Azure traffic from any Azure subscription tooaccess hello server.
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
    Write-Host "Creating hello log4jlogs table and hello mobiledata table ..." -ForegroundColor Green

    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = $sqlDatabaseConnectionString
    $conn.Open()

    # Create hello log4jlogs table and index
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.Connection = $conn
    $cmd.CommandText = $cmdCreateLog4jTable
    $ret = $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateLog4jClusteredIndex
    $cmd.ExecuteNonQuery()

    # Create hello mobiledata table and index
    $cmd.CommandText = $cmdCreateMobileTable
    $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateMobileDataClusteredIndex
    $cmd.ExecuteNonQuery()

    $conn.close()

    #endregion


    #region - Create HDInsight cluster

    Write-Host "Creating hello HDInsight cluster and hello dependent services ..." -ForegroundColor Green

    # Create hello default storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_LRS

    # Create hello default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                        -StorageAccountName $defaultStorageAccountName `
                                        -StorageAccountKey $defaultStorageAccountKey 
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext 

    # Create hello HDInsight cluster
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

    # Validate hello cluster
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName
    #endregion

    #region - pre-process hello source file

    Write-Host "Preprocessing hello source file ..." -ForegroundColor Green

    # This procedure creates a new file with $destBlobName
    $sourceBlobName = "example/data/sample.log"
    $destBlobName = "tutorials/usesqoop/data/sample.log"

    # Define hello connection string
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    # Create block blob objects referencing hello source and destination blob.
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $sourceBlob = $storageContainer.GetBlockBlobReference($sourceBlobName)
    $destBlob = $storageContainer.GetBlockBlobReference($destBlobName)

    # Define a MemoryStream and a StreamReader for reading from hello source file
    $stream = New-Object System.IO.MemoryStream
    $stream = $sourceBlob.OpenRead()
    $sReader = New-Object System.IO.StreamReader($stream)

    # Define a MemoryStream and a StreamWriter for writing into hello destination file
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream

    # Pre-process hello source blob
    $exString = "java.lang.Exception:"
    while(-Not $sReader.EndOfStream){
        $line = $sReader.ReadLine()
        $split = $line.Split(" ")

        # remove hello "java.lang.Exception" from hello first element of hello array
        # for example: java.lang.Exception: 2012-02-03 19:11:02 SampleClass8 [WARN] problem finding id 153454612
        if ($split[0] -eq $exString){
            #create a new ArrayList tooremove $split[0]
            $newArray = [System.Collections.ArrayList] $split
            $newArray.Remove($exString)

            # update $split and $line
            $split = $newArray
            $line = $newArray -join(" ")
        }

        # remove hello lines that has less than 7 elements
        if ($split.count -ge 7){
            write-host $line
            $writeStream.WriteLine($line)
        }
    }

    # Write toohello destination blob
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    #endregion

    #region - export a log file from hello cluster toohello SQL database

    Write-Host "Preprocessing hello source file ..." -ForegroundColor Green

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
