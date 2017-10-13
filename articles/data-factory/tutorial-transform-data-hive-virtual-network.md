---
title: Gegevens transformeren met behulp van Hive in Azure Virtual Network | Microsoft Docs
description: Deze zelfstudie biedt stapsgewijze instructies voor het transformeren van gegevens met behulp van Hive-activiteit in Azure Data Factory.
services: data-factory
documentationcenter: 
author: shengcmsft
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 09/10/2017
ms.author: shengc
ms.openlocfilehash: ec472ea9f45a4c8bc18d065001eae381a275d185
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/11/2017
---
# <a name="transform-data-in-azure-virtual-network-using-hive-activity-in-azure-data-factory"></a>Gegevens transformeren in Azure Virtual Network met behulp van Hive-activiteit in Azure Data Factory
Azure Data Factory is een cloudgebaseerde gegevensintegratieservice waarmee u gegevensgestuurde werkstromen kunt maken in de cloud. Op deze manier kunt u de verplaatsing en transformatie van gegevens indelen en automatiseren. Met Azure Data Factory kunt u gegevensgestuurde werkstromen (ook wel pijplijnen) maken en plannen die gegevens uit verschillende gegevensarchieven kunnen opnemen en de gegevens kunnen verwerken/transformeren met behulp van rekenservices zoals Azure HDInsight Hadoop, Spark, Azure Data Lake Analytics en Azure Machine Learning. Daarnaast kunt u de uitvoergegevens publiceren naar gegevensarchieven zoals Azure SQL Data Warehouse, zodat BI-toepassingen (business intelligence) ze kunnen gebruiken. 

In deze zelfstudie gebruikt u Azure PowerShell om een Data Factory-pijplijn te maken waarmee gegevens worden getransformeerd met behulp van Hive-activiteit in een HDInsight-cluster in een virtueel Azure-netwerk. In deze zelfstudie voert u de volgende stappen uit:

> [!div class="checklist"]
> * Een gegevensfactory maken. 
> * Een zelf-hostende Integration Runtime maken en installeren.
> * Gekoppelde services maken en implementeren.
> * Een pijplijn die Hive-activiteit bevat, maken en implementeren.
> * Een pijplijnuitvoering starten.
> * De pijplijnuitvoering controleren. 
> * De uitvoer controleren. 


Als u nog geen Azure-abonnement hebt, maakt u een [gratis account](https://azure.microsoft.com/free/) voordat u begint.

## <a name="prerequisites"></a>Vereisten
- **Azure Storage-account**. U maakt een hive-script en uploadt dit script naar de Azure-opslag. De uitvoer van het Hive-script wordt opgeslagen in dit opslagaccount. In dit voorbeeld gebruikt HDInsight-cluster dit Azure Storage-account als primaire opslag. 
- **Azure Virtual Network.** Als u geen virtueel Azure-netwerk hebt, maakt u er een door [deze instructies](../virtual-network/virtual-network-get-started-vnet-subnet.md) te volgen. In dit voorbeeld is HDInsight in Azure Virtual Network. Hier volgt een voorbeeldconfiguratie van Azure Virtual Network. 

    ![Virtueel netwerk maken](media/tutorial-transform-data-using-hive-in-vnet/create-virtual-network.png)
- **HDInsight-cluster.** Maak een HDInsight-cluster en koppel dit aan het virtuele netwerk dat u in de vorige stap hebt gemaakt, door de instructies in dit artikel te volgen: [Azure HDInsight uitbreiden met behulp van een virtueel Azure-netwerk](../hdinsight/hdinsight-extend-hadoop-virtual-network.md). Hier volgt een voorbeeldconfiguratie van HDInsight in een virtueel netwerk. 

    ![HDInsight gebruiken in een virtueel netwerk](media/tutorial-transform-data-using-hive-in-vnet/hdinsight-in-vnet-configuration.png)
- **Azure PowerShell**. Volg de instructies in [How to install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps) (Azure PowerShell installeren en configureren).

### <a name="upload-hive-script-to-your-blob-storage-account"></a>Hive-script uploaden naar het Blob-opslagaccount

1. Maak een Hive SQL-bestand met de naam **hivescript.hql** met de volgende inhoud:

   ```sql
   DROP TABLE IF EXISTS HiveSampleOut; 
   CREATE EXTERNAL TABLE HiveSampleOut (clientid string, market string, devicemodel string, state string)
   ROW FORMAT DELIMITED FIELDS TERMINATED BY ' ' 
   STORED AS TEXTFILE LOCATION '${hiveconf:Output}';

   INSERT OVERWRITE TABLE HiveSampleOut
   Select 
       clientid,
       market,
       devicemodel,
       state
   FROM hivesampletable
   ```
2. Maak in de Azure Blob-opslag een container met de naam **adftutorial** als deze nog niet bestaat.
3. Maak een map met de naam `hivescripts`.
4. Upload het bestand `hivescript.hql` naar de submap`hivescripts`.

 

## <a name="create-a-data-factory"></a>Een data factory maken


1. Stel één voor één de variabelen in.

    ```powershell
    $subscriptionID = "<subscription ID>" # Your Azure subscription ID
    $resourceGroupName = "ADFTutorialResourceGroup" # Name of the resource group
    $dataFactoryName = "MyDataFactory09142017" # Globally unique name of the data factory
    $pipelineName = "MyHivePipeline" # Name of the pipeline
    $selfHostedIntegrationRuntimeName = "MySelfHostedIR09142017" # make it a unique name. 
    ```
2. Start **PowerShell**. Houd Azure PowerShell geopend tot het einde van deze snelstartgids. Als u het programma sluit en opnieuw opent, moet u de opdrachten opnieuw uitvoeren.

    Voer de volgende opdracht uit en geef de gebruikersnaam en het wachtwoord op waarmee u zich aanmeldt bij Azure Portal:
        
    ```powershell
    Login-AzureRmAccount
    ```        
    Voer de volgende opdracht uit om alle abonnementen voor dit account weer te geven:

    ```powershell
    Get-AzureRmSubscription
    ```
    Voer de volgende opdracht uit om het abonnement te selecteren waarmee u wilt werken. Vervang **SubscriptionId** door de id van uw Azure-abonnement:

    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<SubscriptionId>"    
    ```  
3. Maak de resourcegroep ADFTutorialResourceGroup, als deze nog niet bestaat in het abonnement. 

    ```powershell
    New-AzureRmResourceGroup -Name $resourceGroupName -Location "East Us" 
    ```
4. Maak de gegevensfactory. 

    ```powershell
     $df = Set-AzureRmDataFactoryV2 -Location EastUS -Name $dataFactoryName -ResourceGroupName $resourceGroupName
    ```

    Voer de volgende opdracht uit om de uitvoer te zien: 

    ```powershell
    $df
    ```

## <a name="create-self-hosted-ir"></a>Een zelf-hostende IR maken
In deze sectie maakt u een zelf-hostende Integration Runtime en koppelt u deze aan een virtuele Azure-machine in hetzelfde virtuele Azure-netwerk waarin het HDInsight-cluster zich bevindt.

1. Maak een zelf-hostende Integration Runtime. Gebruik een unieke naam voor het geval er al een Integration Runtime met dezelfde naam bestaat.

   ```powershell
   Set-AzureRmDataFactoryV2IntegrationRuntime -ResourceGroupName $resourceGroupName -DataFactoryName $dataFactoryName -Name $selfHostedIntegrationRuntimeName -Type SelfHosted
   ```
    Met deze opdracht maakt u een logische registratie van de zelf-hostende Integration Runtime. 
2. Gebruik PowerShell om verificatiesleutels op te halen voor het registreren van de zelf-hostende Integration Runtime. Kopieer een van de sleutels voor het registreren van de zelf-hostende Integration Runtime.

   ```powershell
   Get-AzureRmDataFactoryV2IntegrationRuntimeKey -ResourceGroupName $resourceGroupName -DataFactoryName $dataFactoryName -Name $selfHostedIntegrationRuntimeName | ConvertTo-Json
   ```

   Hier volgt een voorbeeld van uitvoer: 

   ```powershell
   {
       "AuthKey1":  "IR@0000000000000000000000000000000000000=",
       "AuthKey2":  "IR@0000000000000000000000000000000000000="
   }
   ```
    Noteer de waarde van **AuthKey1** zonder aanhalingstekens. 
3. Maak een Azure VM en koppel deze aan hetzelfde virtuele netwerk dat het HDInsight-cluster bevat. Zie [Virtuele machines maken](../virtual-network/virtual-network-get-started-vnet-subnet.md#create-vms) voor meer informatie. Koppel ze aan een virtueel Azure-netwerk. 
4. Download de [zelf-hostende Integration Runtime](https://www.microsoft.com/download/details.aspx?id=39717) op de virtuele Azure-machine. Gebruik de in de vorige stap verkregen verificatiesleutel om de zelf-hostende Integration Runtime handmatig te registreren. 

   ![Integration Runtime registreren](media/tutorial-transform-data-using-hive-in-vnet/register-integration-runtime.png)

   U ziet het volgende bericht wanneer de zelf-hostende Integration Runtime is geregistreerd: ![Geregistreerd](media/tutorial-transform-data-using-hive-in-vnet/registered-successfully.png)

   Wanneer het knooppunt is verbonden met de cloudservice, ziet u de volgende pagina: ![Knooppunt is verbonden](media/tutorial-transform-data-using-hive-in-vnet/node-is-connected.png).

## <a name="author-linked-services"></a>Gekoppelde services maken

In deze sectie maakt en implementeert u twee gekoppelde services:
- Een gekoppelde Azure Storage-service waarmee een Azure Storage-account wordt gekoppeld aan de gegevensfactory. Deze opslag is de primaire opslag die wordt gebruikt voor het HDInsight-cluster. In dit geval gebruiken we dit Azure Storage-account ook om het Hive-script en de uitvoer van het script te bewaren.
- Een gekoppelde HDInsight-service. Het Hive-script wordt via Azure Data Factory naar dit HDInsight-cluster verzonden om te worden uitgevoerd.

### <a name="azure-storage-linked-service"></a>Een gekoppelde Azure Storage-service

Maak een JSON-bestand met behulp van de gewenste editor, kopieer de volgende JSON-definitie van een gekoppelde Azure Storage-service en sla het bestand op als **MyStorageLinkedService.json**.

```json
{
    "name": "MyStorageLinkedService",
    "properties": {
      "type": "AzureStorage",
      "typeProperties": {
        "connectionString": {
          "value": "DefaultEndpointsProtocol=https;AccountName=<storageAccountName>;AccountKey=<storageAccountKey>",
          "type": "SecureString"
        }
      },
      "connectVia": {
        "referenceName": "MySelfhostedIR",
        "type": "IntegrationRuntimeReference"
      }  
    }
}
```

Vervang **&lt;accountname&gt; en &lt;accountkey&gt;** door de naam en de sleutel van uw Azure Storage-account.

### <a name="hdinsight-linked-service"></a>Gekoppelde HDInsight-service

Maak een JSON-bestand met behulp van de gewenste editor, kopieer de volgende JSON-definitie van een gekoppelde Azure HDInsight-service en sla het bestand op als **MyHDInsightLinkedService.json**.

```
{
  "name": "MyHDInsightLinkedService",
  "properties": {     
      "type": "HDInsight",
      "typeProperties": {
          "clusterUri": "https://<clustername>.azurehdinsight.net",
          "userName": "<username>",
          "password": {
            "value": "<password>",
            "type": "SecureString"
          },
          "linkedServiceName": {
            "referenceName": "MyStorageLinkedService",
            "type": "LinkedServiceReference"
          }
      },
      "connectVia": {
        "referenceName": "MySelfhostedIR",
        "type": "IntegrationRuntimeReference"
      }
  }
}
```

Werk de waarden voor de volgende eigenschappen bij in de definitie van de gekoppelde service:

- **userName**. Gebruikersnaam voor de clusteraanmelding die u hebt opgegeven toen u het cluster maakte. 
- **password**. Het wachtwoord voor de gebruiker.
- **clusterUri**. Geef de URL van het HDInsight-cluster op in de indeling https://<clustername>.azurehdinsight.net.  In dit artikel wordt ervan uitgegaan dat u via internet toegang hebt tot het cluster. Bijvoorbeeld, dat u verbinding met het cluster kunt maken op `https://clustername.azurehdinsight.net`. Dit adres maakt gebruik van de openbare gateway. Deze is niet beschikbaar als u NSG's (netwerkbeveiligingsgroepen) of door de gebruiker gedefinieerde routes hebt gebruikt om de toegang via internet te beperken. U moet het virtuele Azure-netwerk zo configureren dat de URL kan worden omgezet in een privé IP-adres of een privégateway voor HDInsight, om ervoor te zorgen dat Data Factory taken kan verzenden naar het HDInsight-cluster is Azure Virtual Network.

  1. Open in Azure Portal het virtuele netwerk waarin het HDInsight-cluster zich bevindt. Open de netwerkinterface met de naam die begint met `nic-gateway-0`. Noteer het bijbehorende privé IP-adres. Bijvoorbeeld: 10.6.0.15. 
  2. Als het virtuele Azure-netwerk een DNS-server heeft, werkt u de DNS-record bij zodat de URL van het HDInsight-cluster `https://<clustername>.azurehdinsight.net` kan worden omgezet in `10.6.0.15`. Dit is de aanbevolen methode. Als u geen DNS-server in het virtuele Azure-netwerk hebt, kunt u dit tijdelijk oplossen door het hostbestand (C:\Windows\System32\drivers\etc) te bewerken van alle VM‘s die als zelf-hostende Integration Runtime-knooppunten zijn geregistreerd. Dit doet u door een vermelding toe te voegen, zoals deze: 
  
        `10.6.0.15 myHDIClusterName.azurehdinsight.net`

Ga naar de map waarin u de JSON-bestanden hebt gemaakt, en voer de volgende opdracht uit om een gekoppelde service te implementeren: 


```powershell
Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "MyStorageLinkedService" -File "MyStorageLinkedService.json"

Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "MyHDILinkedService" -File "MyHDILinkedService.json"
```

## <a name="author-a-pipeline"></a>Een pijplijn maken
In deze stap maakt u een nieuwe pijplijn met een Hive-activiteit. Met deze activiteit wordt een Hive-script uitgevoerd om gegevens uit een voorbeeldtabel te retourneren en op te slaan in een pad dat u hebt gedefinieerd. Maak een JSON-bestand in de gewenste editor, kopieer de volgende JSON-definitie van een pijplijndefinitie en sla het bestand op als **MyHiveOnDemandPipeline.json**.


```json
{
  "name": "MyHivePipeline",
  "properties": {
    "activities": [
      {
        "name": "MyHiveActivity",
        "type": "HDInsightHive",
        "linkedServiceName": {
            "referenceName": "MyHDILinkedService",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
          "scriptPath": "adftutorial\\hivescripts\\hivescript.hql",
          "getDebugInfo": "Failure",
          "defines": {           
            "Output": "wasb://<Container>@<StorageAccount>.blob.core.windows.net/outputfolder/"
          },
          "scriptLinkedService": {
            "referenceName": "MyStorageLinkedService",
            "type": "LinkedServiceReference"
          }
        }
      }
    ]
  }
}

```

Houd rekening met de volgende punten:

- **scriptPath** verwijst naar het pad naar het Hive-script in het Azure Storage-account dat u hebt gebruikt voor MyStorageLinkedService. Het pad is hoofdlettergevoelig.
- **Uitvoer** is een argument dat wordt gebruikt in het Hive-script. Gebruik de indeling van `wasb://<Container>@<StorageAccount>.blob.core.windows.net/outputfolder/` om dit argument te laten verwijzen naar een bestaande map in de Azure-opslag. Het pad is hoofdlettergevoelig. 

Ga naar de map waarin u de JSON-bestanden hebt gemaakt, en voer de volgende opdracht uit om een pijplijn te implementeren: 


```powershell
Set-AzureRmDataFactoryV2Pipeline -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name $pipelineName -File "MyHivePipeline.json"
```

## <a name="start-the-pipeline"></a>Start de pijplijn 

1. Een pijplijnuitvoering starten. Ook wordt de id voor de pijplijnuitvoering vastgelegd voor toekomstige controle.

    ```powershell
    $runId = Invoke-AzureRmDataFactoryV2Pipeline -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -PipelineName $pipelineName
   ```
2. Voer het volgende script uit om continu de status van de pijplijnuitvoering te controleren totdat deze is voltooid.

    ```powershell
    while ($True) {
        $result = Get-AzureRmDataFactoryV2ActivityRun -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -PipelineRunId $runId -RunStartedAfter (Get-Date).AddMinutes(-30) -RunStartedBefore (Get-Date).AddMinutes(30)

        if(!$result) {
            Write-Host "Waiting for pipeline to start..." -foregroundcolor "Yellow"
        }
        elseif (($result | Where-Object { $_.Status -eq "InProgress" } | Measure-Object).count -ne 0) {
            Write-Host "Pipeline run status: In Progress" -foregroundcolor "Yellow"
        }
        else {
            Write-Host "Pipeline '"$pipelineName"' run finished. Result:" -foregroundcolor "Yellow"
            $result
            break
        }
        ($result | Format-List | Out-String)
        Start-Sleep -Seconds 15
    }
    
    Write-Host "Activity `Output` section:" -foregroundcolor "Yellow"
    $result.Output -join "`r`n"

    Write-Host "Activity `Error` section:" -foregroundcolor "Yellow"
    $result.Error -join "`r`n"
    ```

   Hier volgt een voorbeeld van de voorbeelduitvoer:

    ```json
    Pipeline run status: In Progress
    
    ResourceGroupName : ADFV2SampleRG2
    DataFactoryName   : SampleV2DataFactory2
    ActivityName      : MyHiveActivity
    PipelineRunId     : 000000000-0000-0000-000000000000000000
    PipelineName      : MyHivePipeline
    Input             : {getDebugInfo, scriptPath, scriptLinkedService, defines}
    Output            :
    LinkedServiceName :
    ActivityRunStart  : 9/18/2017 6:58:13 AM
    ActivityRunEnd    :
    DurationInMs      :
    Status            : InProgress
    Error             :
    
    Pipeline ' MyHivePipeline' run finished. Result:
    
    ResourceGroupName : ADFV2SampleRG2
    DataFactoryName   : SampleV2DataFactory2
    ActivityName      : MyHiveActivity
    PipelineRunId     : 0000000-0000-0000-0000-000000000000
    PipelineName      : MyHivePipeline
    Input             : {getDebugInfo, scriptPath, scriptLinkedService, defines}
    Output            : {logLocation, clusterInUse, jobId, ExecutionProgress...}
    LinkedServiceName :
    ActivityRunStart  : 9/18/2017 6:58:13 AM
    ActivityRunEnd    : 9/18/2017 6:59:16 AM
    DurationInMs      : 63636
    Status            : Succeeded
    Error             : {errorCode, message, failureType, target}
    
    Activity Output section:
    "logLocation": "wasbs://adfjobs@adfv2samplestor.blob.core.windows.net/HiveQueryJobs/000000000-0000-47c3-9b28-1cdc7f3f2ba2/18_09_2017_06_58_18_023/Status"
    "clusterInUse": "https://adfv2HivePrivate.azurehdinsight.net"
    "jobId": "job_1505387997356_0024"
    "ExecutionProgress": "Succeeded"
    "effectiveIntegrationRuntime": "MySelfhostedIR"
    Activity Error section:
    "errorCode": ""
    "message": ""
    "failureType": ""
    "target": "MyHiveActivity"
    ```
4. Ga in de map `outputfolder` naar het nieuwe bestand dat is gemaakt als resultaat van de Hive-query. Het bestand moet eruitzien als de volgende voorbeelduitvoer: 

   ```
   8 en-US SCH-i500 California
   23 en-US Incredible Pennsylvania
   212 en-US SCH-i500 New York
   212 en-US SCH-i500 New York
   212 en-US SCH-i500 New York
   212 en-US SCH-i500 New York
   212 en-US SCH-i500 New York
   212 en-US SCH-i500 New York
   212 en-US SCH-i500 New York
   212 en-US SCH-i500 New York
   212 en-US SCH-i500 New York
   212 en-US SCH-i500 New York
   212 en-US SCH-i500 New York
   212 en-US SCH-i500 New York
   246 en-US SCH-i500 District Of Columbia
   246 en-US SCH-i500 District Of Columbia
   ```

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie hebt u de volgende stappen uitgevoerd: 

> [!div class="checklist"]
> * Een gegevensfactory maken. 
> * Een zelf-hostende Integration Runtime maken en installeren.
> * Gekoppelde services maken en implementeren.
> * Een pijplijn die Hive-activiteit bevat, maken en implementeren.
> * Een pijplijnuitvoering starten.
> * De pijplijnuitvoering controleren. 
> * De uitvoer controleren. 

Ga naar de volgende zelfstudie voor meer informatie over het transformeren van gegevens met behulp van een Spark-cluster in Azure:

> [!div class="nextstepaction"]
>[Een vertakking en keten maken van een Data Factory-controlestroom](tutorial-control-flow.md)



