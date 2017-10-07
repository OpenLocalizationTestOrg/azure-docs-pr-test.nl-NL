---
title: aaaCreate Hadoop-clusters met behulp van sjablonen - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe toocreate clusters voor HDInsight met behulp van Resource Manager-sjablonen
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00a80dea-011f-44f0-92a4-25d09db9d996
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/30/2017
ms.author: jgao
ms.openlocfilehash: 92a6c1d888e401a11537dba34f188245ac17f448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-clusters-in-hdinsight-by-using-resource-manager-templates"></a>Hadoop-clusters maken in HDInsight met behulp van Resource Manager-sjablonen
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

In dit artikel leert u op verschillende manieren toocreate Azure HDInsight-clusters met Azure Resource Manager-sjablonen. Zie voor meer informatie [Implementeer een toepassing met Azure Resource Manager-sjabloon](../azure-resource-manager/resource-group-template-deploy.md). toolearn over andere hulpmiddelen voor het cluster maken en de functies, klikt u op de tabselector Hallo op Hallo boven aan deze pagina of Zie [methoden voor het maken van Cluster](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods).

## <a name="prerequisites"></a>Vereisten
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

toofollow Hallo-instructies in dit artikel hebt u nodig:

* Een [Azure-abonnement](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Azure PowerShell en/of Azure CLI.

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell-and-cli.md)]

### <a name="resource-manager-templates"></a>Resource Manager-sjablonen
Resource Manager-sjabloon maakt het eenvoudig toocreate Hallo voor uw toepassing in een enkele, gecoördineerde bewerking te volgen:
* HDInsight-clusters en hun afhankelijke bronnen (zoals Hallo standaardopslagaccount)
* Andere bronnen (zoals Azure SQL Database toouse Apache Sqoop)

In de sjabloon hello definieert u Hallo-resources die nodig zijn voor de toepassing hello. U wordt ook implementatie parameters tooinput waarden voor verschillende omgevingen. Hallo sjabloon bestaat uit JSON en uitdrukkingen tooconstruct waarden te gebruiken voor uw implementatie.

Vindt u voorbeelden van HDInsight-sjabloon op [Azure-Snelstartsjablonen](https://azure.microsoft.com/resources/templates/?term=hdinsight). Cross-platform gebruiken [Visual Studio Code](https://code.visualstudio.com/#alt-downloads) Hello [Resource Manager-extensie](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) of een tekst-editor toosave Hallo sjabloon naar een bestand op uw werkstation. U leert hoe toocall sjabloon Hallo via andere methoden.

Zie voor meer informatie over de Resource Manager-sjablonen, Hallo artikelen te volgen:

* [De auteur van Azure Resource Manager-sjablonen](../azure-resource-manager/resource-group-authoring-templates.md)
* [Implementeer een toepassing met Azure Resource Manager-sjablonen](../azure-resource-manager/resource-group-template-deploy.md)

## <a name="generate-templates"></a>Genereren van sjablonen

U kunt met behulp van hello Azure-portal alle Hallo-eigenschappen van een cluster configureren en vervolgens Hallo sjabloon opslaan voordat u deze implementeert. Vervolgens kunt u de sjabloon Hallo hergebruiken.

**toogenerate een sjabloon met hello Azure-portal**

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Klik op **nieuw** op Hallo menu links, klikt u op **Intelligence en analyse**, en klik vervolgens op **HDInsight**.
3. Ga als volgt Hallo instructies tooenter eigenschappen. U kunt beide Hallo **snelle invoer** of Hallo **aangepaste** optie.
4. Op Hallo **samenvatting** tabblad **sjabloon en parameters downloaden**:

    ![Maken van HDInsight Hadoop cluster Resource Manager-sjabloon downloaden](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download.png)

    U ziet een lijst met sjabloonbestand hello, parameterbestand en de code steekproeven toodeploy Hallo sjabloon:

    ![HDInsight Hadoop maken-cluster Downloadinstellingen voor Resource Manager-sjabloon](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download-options.png)

    Hier kunt kunt u Hallo sjabloon downloaden, tooyour sjabloonbibliotheek opslaan of Hallo sjabloon implementeren.

    tooaccess een sjabloon in de bibliotheek, klikt u op **meer services** van Hallo menu aan de linkerkant en klik vervolgens op **sjablonen** (onder Hallo **andere** categorie).

    > [!Note]
    > Hallo-sjabloon en de parameters-bestand moet samen worden gebruikt. Anders krijgt u mogelijk onverwachte resultaten. Bijvoorbeeld, Hallo standaard **clusterKind** is altijd de waarde van de eigenschap **hadoop**, ondanks wat u opgeven voordat u Hallo sjabloon downloaden.



## <a name="deploy-with-powershell"></a>Implementeren met PowerShell

Deze procedure maakt u een Hadoop-cluster in HDInsight.

1. Hallo JSON-bestand opslaan in Hallo [bijlage](#appx-a-arm-template) tooyour werkstation. In Hallo PowerShell-script, is het Hallo-bestandsnaam `C:\HDITutorials-ARM\hdinsight-arm-template.json`.
2. Hallo-parameters en variabelen instellen indien nodig.
3. Hallo sjabloon uitvoeren met behulp van PowerShell-script volgen Hallo:

        ####################################
        # Set these variables
        ####################################
        #region - used for creating Azure service names
        $nameToken = "<Enter an Alias>"
        $templateFile = "C:\HDITutorials-ARM\hdinsight-arm-template.json"
        #endregion

        ####################################
        # Service names and variables
        ####################################
        #region - service names
        $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

        $resourceGroupName = $namePrefix + "rg"
        $hdinsightClusterName = $namePrefix + "hdi"
        $defaultStorageAccountName = $namePrefix + "store"
        $defaultBlobContainerName = $hdinsightClusterName

        $location = "East US 2"

        $armDeploymentName = $namePrefix
        #endregion

        ####################################
        # Connect tooAzure
        ####################################
        #region - Connect tooAzure subscription
        Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
        try{Get-AzureRmContext}
        catch{Login-AzureRmAccount}
        #endregion

        # Create a resource group
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $Location

        # Create cluster and hello dependent storage account
        $parameters = @{clusterName="$hdinsightClusterName"}

        New-AzureRmResourceGroupDeployment `
            -Name $armDeploymentName `
            -ResourceGroupName $resourceGroupName `
            -TemplateFile $templateFile `
            -TemplateParameterObject $parameters

        # List cluster
        Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName

    Hallo PowerShell-script configureert alleen Hallo clusternaam. Hallo opslagaccountnaam is vastgelegd in Hallo-sjabloon. U bent na vragen aan gebruiker tooenter Hallo cluster gebruikerswachtwoord. (de standaardgebruikersnaam Hallo **admin**.) Bent u ook na vragen aan gebruiker tooenter Hallo SSH gebruiker-wachtwoord. (de standaardgebruikersnaam SSH Hallo **sshuser**.)  

Zie voor meer informatie [implementeren met PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).

## <a name="deploy-with-cli"></a>Implementeren met CLI
Hallo volgende voorbeeld maakt gebruik van Azure-opdrachtregelinterface (CLI). Er wordt een cluster en het afhankelijke opslagaccount en container gemaakt door het aanroepen van Resource Manager-sjabloon:

    azure login
    azure config mode arm
    azure group create -n hdi1229rg -l "East US"
    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "C:\HDITutorials-ARM\hdinsight-arm-template.json"

U bent tooenter na vragen aan gebruiker:
* Hallo clusternaam.
* Hallo cluster gebruikerswachtwoord. (de standaardgebruikersnaam Hallo **admin**.)
* Hallo SSH gebruiker-wachtwoord. (de standaardgebruikersnaam SSH Hallo **sshuser**.)

Hallo na code levert inline-parameters:

    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "c:\Tutorials\HDInsightARM\create-linux-based-hadoop-cluster-in-hdinsight.json" --parameters '{\"clusterName\":{\"value\":\"hdi1229\"},\"clusterLoginPassword\":{\"value\":\"Pass@word1\"},\"sshPassword\":{\"value\":\"Pass@word1\"}}'

## <a name="deploy-with-hello-rest-api"></a>Met de Hallo REST-API implementeren
Zie [implementeren met Hallo REST-API](../azure-resource-manager/resource-group-template-deploy-rest.md).

## <a name="deploy-with-visual-studio"></a>Implementeren met Visual Studio
 Gebruik Visual Studio toocreate een resourcegroepproject en tooAzure via de gebruikersinterface Hallo implementeren. U selecteren Hallo type resources tooinclude in uw project. Deze resources worden automatisch toegevoegd aan toohello Resource Manager-sjabloon. Hallo-project bevat ook een PowerShell-script toodeploy Hallo-sjabloon.

Zie voor een inleiding toousing Visual Studio aan resourcegroepen, [maken en implementeren van Azure-resourcegroepen met Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).

## <a name="troubleshoot"></a>Problemen oplossen

Zie [Vereisten voor toegangsbeheer](hdinsight-administer-use-portal-linux.md#create-clusters) als u problemen ondervindt met het maken van HDInsight-clusters.

## <a name="next-steps"></a>Volgende stappen
In dit artikel hebt u geleerd toocreate met verschillende manieren een HDInsight-cluster. toolearn Zie meer Hallo artikelen te volgen:

* Zie voor een voorbeeld van het implementeren van resources via de .NET-clientbibliotheek Hallo [resources implementeren met behulp van .NET-bibliotheken en een sjabloon](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Zie voor een gedetailleerd voorbeeld van een toepassing implementeren, [inrichten en implementeren van microservices zoals verwacht in Azure](../app-service-web/app-service-deploy-complex-application-predictably.md).
* Zie voor instructies over het implementeren van uw oplossing toodifferent omgevingen [ontwikkel- en testomgevingen in Microsoft Azure](../solution-dev-test-environments.md).
* toolearn hello secties van hello Azure Resource Manager-sjabloon, Zie [sjablonen](../azure-resource-manager/resource-group-authoring-templates.md).
* Zie voor een lijst met Hallo-functies kunt u in een Azure Resource Manager-sjabloon, [sjabloonfuncties](../azure-resource-manager/resource-group-template-functions.md).

## <a name="appendix-resource-manager-template-toocreate-a-hadoop-cluster"></a>Bijlage: Resource Manager sjabloon toocreate een Hadoop-cluster
Hallo maakt volgende Azure Resource Manager-sjabloon een Linux gebaseerde Hadoop-cluster met Hallo afhankelijke Azure storage-account.

> [!NOTE]
> Dit voorbeeld bevat configuratie-informatie voor Hive-metastore en Oozie-metastore. Hallo sectie verwijderen of Hallo sectie configureren voordat u Hallo-sjabloon.
>
>

    {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "clusterName": {
        "type": "string",
        "metadata": {
            "description": "hello name of hello HDInsight cluster toocreate."
        }
        },
        "clusterLoginUserName": {
        "type": "string",
        "defaultValue": "admin",
        "metadata": {
            "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
        }
        },
        "clusterLoginPassword": {
        "type": "securestring",
        "metadata": {
            "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "sshUserName": {
        "type": "string",
        "defaultValue": "sshuser",
        "metadata": {
            "description": "These credentials can be used tooremotely access hello cluster."
        }
        },
        "sshPassword": {
        "type": "securestring",
        "metadata": {
            "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "location": {
        "type": "string",
        "defaultValue": "East US",
        "allowedValues": [
            "East US",
            "East US 2",
            "North Central US",
            "South Central US",
            "West US",
            "North Europe",
            "West Europe",
            "East Asia",
            "Southeast Asia",
            "Japan East",
            "Japan West",
            "Australia East",
            "Australia Southeast"
        ],
        "metadata": {
            "description": "hello location where all azure resources will be deployed."
        }
        },
        "clusterType": {
        "type": "string",
        "defaultValue": "hadoop",
        "allowedValues": [
            "hadoop",
            "hbase",
            "storm",
            "spark"
        ],
        "metadata": {
            "description": "hello type of hello HDInsight cluster toocreate."
        }
        },
        "clusterWorkerNodeCount": {
        "type": "int",
        "defaultValue": 2,
        "metadata": {
            "description": "hello number of nodes in hello HDInsight cluster."
        }
        }
    },
    "variables": {
        "defaultApiVersion": "2015-05-01-preview",
        "clusterApiVersion": "2015-03-01-preview",
        "clusterStorageAccountName": "[concat(parameters('clusterName'),'store')]"
    },
    "resources": [
        {
        "name": "[variables('clusterStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": { },
        "properties": {
            "accountType": "Standard_LRS"
        }
        },
        {
        "name": "[parameters('clusterName')]",
        "type": "Microsoft.HDInsight/clusters",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('clusterApiVersion')]",
        "dependsOn": [ "[concat('Microsoft.Storage/storageAccounts/',variables('clusterStorageAccountName'))]" ],
        "tags": {

        },
        "properties": {
            "clusterVersion": "3.4",
            "osType": "Linux",
            "tier": "standard",
            "clusterDefinition": {
            "kind": "[parameters('clusterType')]",
            "configurations": {
                "gateway": {
                "restAuthCredential.isEnabled": true,
                "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                },
                "hive-site": {
                    "javax.jdo.option.ConnectionDriverName": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
                    "javax.jdo.option.ConnectionURL": "jdbc:sqlserver://myadla0901dbserver.database.windows.net;database=myhive20160901;encrypt=true;trustServerCertificate=true;create=false;loginTimeout=300",
                    "javax.jdo.option.ConnectionUserName": "johndole",
                    "javax.jdo.option.ConnectionPassword": "myPassword$"
                },
                "hive-env": {
                    "hive_database": "Existing MSSQL Server database with SQL authentication",
                    "hive_database_name": "myhive20160901",
                    "hive_database_type": "mssql",
                    "hive_existing_mssql_server_database": "myhive20160901",
                    "hive_existing_mssql_server_host": "myadla0901dbserver.database.windows.net",
                    "hive_hostname": "myadla0901dbserver.database.windows.net"
                },
                "oozie-site": {
                    "oozie.service.JPAService.jdbc.driver": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
                    "oozie.service.JPAService.jdbc.url": "jdbc:sqlserver://myadla0901dbserver.database.windows.net;database=myhive20160901;encrypt=true;trustServerCertificate=true;create=false;loginTimeout=300",
                    "oozie.service.JPAService.jdbc.username": "johndole",
                    "oozie.service.JPAService.jdbc.password": "myPassword$",
                    "oozie.db.schema.name": "oozie"
                },
                "oozie-env": {
                    "oozie_database": "Existing MSSQL Server database with SQL authentication",
                    "oozie_database_name": "myhive20160901",
                    "oozie_database_type": "mssql",
                    "oozie_existing_mssql_server_database": "myhive20160901",
                    "oozie_existing_mssql_server_host": "myadla0901dbserver.database.windows.net",
                    "oozie_hostname": "myadla0901dbserver.database.windows.net"
                }            
            }
            },
            "storageProfile": {
            "storageaccounts": [
                {
                "name": "[concat(variables('clusterStorageAccountName'),'.blob.core.windows.net')]",
                "isDefault": true,
                "container": "[parameters('clusterName')]",
                "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('clusterStorageAccountName')), variables('defaultApiVersion')).keys[0].value]"
                }
            ]
            },
            "computeProfile": {
            "roles": [
                {
                "name": "headnode",
                "targetInstanceCount": "2",
                "hardwareProfile": {
                    "vmSize": "Standard_D3"
                },
                "osProfile": {
                    "linuxOperatingSystemProfile": {
                    "username": "[parameters('sshUserName')]",
                    "password": "[parameters('sshPassword')]"
                    }
                }
                },
                {
                "name": "workernode",
                "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                "hardwareProfile": {
                    "vmSize": "Standard_D3"
                },
                "osProfile": {
                    "linuxOperatingSystemProfile": {
                    "username": "[parameters('sshUserName')]",
                    "password": "[parameters('sshPassword')]"
                    }
                }
                }
            ]
            }
        }
        }
    ],
    "outputs": {
        "cluster": {
        "type": "object",
        "value": "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
        }
    }
    }

## <a name="appendix-resource-manager-template-toocreate-a-spark-cluster"></a>Bijlage: Resource Manager sjabloon toocreate een Spark-cluster

Deze sectie vindt u een Resource Manager-sjabloon waarmee u toocreate een HDInsight Spark-cluster kunt. Deze sjabloon bevat configuraties voor `spark-defaults` en `spark-thrift-sparkconf` (voor Spark 1.6-clusters) en `spark2-defaults` en `spark2-thrift-sparkconf` (voor 2 Spark-clusters). Bovendien toothis, HDInsight berekend en ingesteld configuraties, zoals `spark.executor.instances`, `spark.executor.memory`, en `spark.executor.cores` op basis van Hallo clustergrootte. 

Als u een één parameter ingesteld in een sectie als onderdeel van het Hallo-sjabloon zelf, HDInsight niet berekenen en andere parameters Hallo Hallo instellen hetzelfde gedeelte. Bijvoorbeeld: parameter `spark.executor.instances` bevindt zich in Hallo `spark-defaults` configuratie. Als u een andere parameter ingesteld (bijvoorbeeld `spark.yarn.exector.memoryOverhead`) in Hallo `spark-defaults` configuratie, HDInsight niet berekenen en stel de Hallo `spark.executor.instances` ook de parameter.

    {
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "0.9.0.0",
    "parameters": {
        "clusterName": {
            "type": "string",
            "metadata": {
                "description": "hello name of hello HDInsight cluster toocreate."
            }
        },
        "clusterLoginUserName": {
            "type": "string",
            "defaultValue": "admin",
            "metadata": {
                "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
            }
        },
        "clusterLoginPassword": {
            "type": "securestring",
            "metadata": {
                "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        },
        "location": {
            "type": "string",
            "defaultValue": "southcentralus",
            "metadata": {
                "description": "hello location where all azure resources will be deployed."
            }
        },
        "clusterVersion": {
            "type": "string",
            "defaultValue": "3.5",
            "metadata": {
                "description": "HDInsight cluster version."
            }
        },
        "clusterWorkerNodeCount": {
            "type": "int",
            "defaultValue": 4,
            "metadata": {
                "description": "hello number of nodes in hello HDInsight cluster."
            }
        },
        "clusterKind": {
            "type": "string",
            "defaultValue": "SPARK",
            "metadata": {
                "description": "hello type of hello HDInsight cluster toocreate."
            }
        },
        "sshUserName": {
            "type": "string",
            "defaultValue": "sshuser",
            "metadata": {
                "description": "These credentials can be used tooremotely access hello cluster."
            }
        },
        "sshPassword": {
            "type": "securestring",
            "metadata": {
                "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        }
    },
    "variables": {
        "defaultApiVersion": "2017-06-01",
        "clusterStorageAccountName": "[concat(parameters('clusterName'),'store')]"
    },
    "resources": [
        {
        "name": "[variables('clusterStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": { },
        "properties": {
            "accountType": "Standard_LRS"
        }
        },
    {
            "apiVersion": "2015-03-01-preview",
            "name": "[parameters('clusterName')]",
            "type": "Microsoft.HDInsight/clusters",
            "location": "[parameters('location')]",
            "dependsOn": [],
            "properties": {
                "clusterVersion": "[parameters('clusterVersion')]",
                "osType": "Linux",
                "tier": "standard",
                "clusterDefinition": {
                    "kind": "[parameters('clusterKind')]",
                    "configurations": {
                        "gateway": {
                            "restAuthCredential.isEnabled": true,
                            "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                            "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                        },
                        "spark-defaults": {
                            "spark.executor.cores": "2"
                        },
                        "spark-thrift-sparkconf": {
                            "spark.yarn.executor.memoryOverhead": "896"
                        }
                    }
                },
                "storageProfile": {
                    "storageaccounts": [
                        {
                            "name": "[concat(variables('clusterStorageAccountName'),'.blob.core.windows.net')]",
                            "isDefault": true,
                            "container": "[parameters('clusterName')]",
                            "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('clusterStorageAccountName')), variables('defaultApiVersion')).keys[0].value]"
                        }
                    ]
                },
                "computeProfile": {
                    "roles": [
                        {
                            "name": "headnode",
                            "minInstanceCount": 1,
                            "targetInstanceCount": 2,
                            "hardwareProfile": {
                                "vmSize": "Standard_D12"
                            },
                            "osProfile": {
                                "linuxOperatingSystemProfile": {
                                    "username": "[parameters('sshUserName')]",
                                    "password": "[parameters('sshPassword')]"
                                }
                            },
                            "virtualNetworkProfile": null,
                            "scriptActions": []
                        },
                        {
                            "name": "workernode",
                            "minInstanceCount": 1,
                            "targetInstanceCount": 4,
                            "hardwareProfile": {
                                "vmSize": "Standard_D4"
                            },
                            "osProfile": {
                                "linuxOperatingSystemProfile": {
                                    "username": "[parameters('sshUserName')]",
                                    "password": "[parameters('sshPassword')]"
                                    }
                                },
                                "virtualNetworkProfile": null,
                                "scriptActions": []
                            }
                        ]
                    }
                }
            }
        ]
    }
