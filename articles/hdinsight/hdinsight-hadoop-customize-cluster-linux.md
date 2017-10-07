---
title: aaaCustomize HDInsight-clusters met behulp van scriptacties - Azure | Microsoft Docs
description: Aangepaste onderdelen die toolinux gebaseerde HDInsight-clusters met behulp van scriptacties toevoegen. Scriptacties zijn Bash-scripts die kunnen worden gebruikt toocustomize Hallo clusterconfiguratie of toevoegen van extra services en hulpprogramma's zoals Hue, Solr of R.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 48e85f53-87c1-474f-b767-ca772238cc13
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: ff22680a8a50b21985f6941f1edaf1dcf863d13f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="customize-linux-based-hdinsight-clusters-using-script-action"></a>Linux gebaseerde HDInsight-clusters met behulp van de scriptactie aanpassen

HDInsight biedt een configuratieoptie aangeroepen **scriptactie** die wordt aangeroepen met aangepaste scripts die Hallo cluster aanpassen. Deze scripts zijn gebruikte tooinstall extra onderdelen en configuratie-instellingen wijzigen. Scriptacties kunnen worden gebruikt tijdens of na het maken van het cluster.

> [!IMPORTANT]
> Hallo mogelijkheid toouse scriptacties op een cluster al actief is alleen beschikbaar voor Linux gebaseerde HDInsight-clusters.
>
> Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

Scriptacties kunnen ook gepubliceerde toohello Azure Marketplace worden als een HDInsight-toepassing. Aantal Hallo voorbeelden in dit document laten zien hoe u een HDInsight-toepassing met behulp van actie-scriptopdrachten van PowerShell en .NET SDK Hallo kunt installeren. Zie voor meer informatie over HDInsight-toepassingen [publiceren HDInsight-toepassingen in Azure Marketplace Hallo](hdinsight-apps-publish-applications.md).

## <a name="permissions"></a>Machtigingen

Als u van een domein HDInsight-cluster gebruikmaakt, zijn er twee Ambari-machtigingen die vereist zijn wanneer met behulp van scriptacties met Hallo-cluster:

* **AMBARI. Voer\_aangepaste\_opdracht**: Hallo Ambari beheerdersrol beschikt over deze machtiging standaard.
* **HET CLUSTER. Voer\_aangepaste\_opdracht**: beide Hallo HDInsight Clusterbeheer en Ambari beheerder hebben deze machtiging standaard.

Zie voor meer informatie over het werken met machtigingen met HDInsight domein [domein HDInsight-clusters beheren](hdinsight-domain-joined-manage.md).

## <a name="access-control"></a>Toegangsbeheer

Als u niet Hallo beheerder of eigenaar van uw Azure-abonnement, uw account moet er ten minste **Inzender** toegang toohello resourcegroep die Hallo HDInsight-cluster bevat.

Bovendien, als u een HDInsight-cluster iemand met ten minste maakt **Inzender** toegang toohello Azure-abonnement moet hebben eerder Hallo-provider geregistreerd voor HDInsight. Registratie van de provider wordt uitgevoerd wanneer een gebruiker met Inzender toegang toohello abonnement een resource voor Hallo eerst op Hallo-abonnement maakt. Dit kan ook worden bereikt zonder dat er een resource wordt gemaakt door [een provider te registreren met behulp van REST](https://msdn.microsoft.com/library/azure/dn790548.aspx).

Zie voor meer informatie over het werken met toegangsbeheer Hallo documenten te volgen:

* [Aan de slag met toegangsbeheer in hello Azure-portal](../active-directory/role-based-access-control-what-is.md)
* [Rol toewijzingen toomanage toegang tooyour Azure-abonnementresources gebruiken](../active-directory/role-based-access-control-configure.md)

## <a name="understanding-script-actions"></a>Understanding scriptacties

Een scriptactie is gewoon een Bash-script dat u een URI te bieden en parameters voor. Hallo-script wordt uitgevoerd op knooppunten in Hallo HDInsight-cluster. Hallo volgen kenmerken en functies van scriptacties.

* Moet worden opgeslagen op een URI die toegankelijk is vanaf Hallo HDInsight-cluster. Hallo volgen mogelijke opslaglocaties:

    * Een **Azure Data Lake Store** account die toegankelijk is voor Hallo HDInsight-cluster. Zie voor meer informatie over het gebruik van Azure Data Lake Store met HDInsight [een HDInsight-cluster maken met Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

        Wanneer u een script dat is opgeslagen in Data Lake Store, Hallo URI-indeling is `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.

        > [!NOTE]
        > Hallo service principal HDInsight maakt gebruik van tooaccess Data Lake Store moet leestoegang toohello script hebben.

    * Een blob in een **Azure Storage-account** die beide accounts Hallo primaire of extra opslag voor Hallo HDInsight-cluster is. HDInsight krijgt toegang tot tooboth van deze typen opslagaccounts tijdens het maken van het cluster.

    * Bestand met een openbare sharing-service zoals Azure Blob, GitHub, OneDrive, Dropbox, enz.

        Bijvoorbeeld URI's, Zie Hallo [voorbeeldscripts script actie](#example-script-action-scripts) sectie.

        > [!WARNING]
        > HDInsight biedt alleen ondersteuning voor __algemeen__ Azure Storage-accounts. Het ondersteunt momenteel geen Hallo __Blob storage__ accounttype.

* Kan worden beperkt te**uitvoeren op alleen bepaalde knooppunttypen**voor voorbeeld hoofdknooppunten of worker-knooppunten.

  > [!NOTE]
  > Gebruikt in combinatie met HDInsight Premium, kunt u opgeven dat Hallo script op Hallo edge-knooppunt moet worden gebruikt.

* Kan **persistent** of **ad hoc**.

    **Persistent** scripts zijn toegepaste tooworker knooppunten toegevoegde toohello cluster na het Hallo-script wordt uitgevoerd. Bijvoorbeeld tijdens het Hallo-cluster schalen.

    Een persistent script mogelijk ook van toepassing zijn wijzigingen tooanother knooppunttype, zoals een hoofdknooppunt.

  > [!IMPORTANT]
  > Persistente scriptacties moeten een unieke naam hebben.

    **Ad hoc** scripts blijven niet bestaan. Ze zijn niet toegepast tooworker knooppunten toegevoegde toohello cluster na het Hallo-script is uitgevoerd. U kunt vervolgens een ad-hoc script tooa promoveren persistent script of degraderen van een persistent script tooan ad-hoc-script.

  > [!IMPORTANT]
  > Scriptacties gebruikt tijdens het maken van het cluster worden automatisch doorgevoerd.
  >
  > Scripts die mislukken niet persistent hebt gemaakt, zelfs als u specifiek aangeeft dat ze moeten worden.

* Kan accepteren **parameters** die worden gebruikt door Hallo script tijdens de uitvoering.
* Voer met **root bevoegdheden** op Hallo clusterknooppunten.
* Kan worden gebruikt via Hallo **Azure-portal**, **Azure PowerShell**, **Azure CLI**, of **HDInsight .NET SDK**

Hallo cluster houdt een geschiedenis van alle scripts die hebben is uitgevoerd. Hallo-geschiedenis is nuttig wanneer u toofind Hallo-ID van een script nodig hebt voor promotie of degradatie bewerkingen.

> [!IMPORTANT]
> Er is geen automatische manier tooundo Hallo wijzigingen die door een script in te grijpen. Hallo wijzigingen handmatig ongedaan te maken of een script dat wordt teruggedraaid ze bieden.


### <a name="script-action-in-hello-cluster-creation-process"></a>Scriptactie in het proces voor het Hallo-cluster maken

Scriptacties gebruikt tijdens het maken van het cluster zijn enigszins afwijken van het script acties worden uitgevoerd op een bestaand cluster:

* Hallo-script is **automatisch persistente**.
* Een **fout** in Hallo script Hallo cluster maken van het proces toofail kan veroorzaken.

Hallo volgende diagram wordt weergegeven wanneer het Script wordt uitgevoerd tijdens het maken van een Hallo:

![Aanpassing van HDInsight-cluster en fasen tijdens het maken van het cluster][img-hdi-cluster-states]

Hallo-script wordt uitgevoerd terwijl HDInsight wordt geconfigureerd. In deze fase Hallo Hallo script wordt parallel uitgevoerd in alle opgegeven knooppunten in cluster Hallo en wordt uitgevoerd met basis-bevoegdheden op Hallo knooppunten.

> [!NOTE]
> Omdat het Hallo-script wordt uitgevoerd met het niveau bevoegdheid hoofdmap op Hallo clusterknooppunten, kunt u bewerkingen zoals het stoppen en starten van services, met inbegrip van Hadoop-gerelateerde services uitvoeren. Als u services stoppen, moet u ervoor zorgen dat Hallo Ambari-service en andere Hadoop-gerelateerde services actief zijn voordat het Hallo-script is voltooid. Deze services zijn vereist toosuccessfully bepalen Hallo gezondheid en status van de cluster Hallo terwijl deze wordt gemaakt.


U kunt meerdere scriptacties tegelijk gebruiken tijdens het maken van het cluster. Deze scripts worden aangeroepen in Hallo volgorde waarin ze zijn opgegeven.

> [!IMPORTANT]
> Scriptacties moeten binnen 60 minuten of time-out voltooien. Tijdens de clusterinrichting, voert Hallo script tegelijk met andere processen installatie en configuratie. Concurrentie voor resources, zoals CPU-tijd of netwerk bandbreedte mogelijk Hallo script tootake langer toofinish dan in uw ontwikkelomgeving.
>
> toominimize Hallo tijd het duurt toorun Hallo script, taken zoals het downloaden en toepassingen van bron compileren voorkomen. Toepassingen vooraf gecompileerd en Hallo binair in Azure Storage opslaat.


### <a name="script-action-on-a-running-cluster"></a>Scriptactie op een actief cluster

In tegenstelling tot script acties die worden gebruikt tijdens het maken van het cluster een fout in een script uitgevoerd op een al actief cluster tot niet automatisch toochange Hallo-tooa mislukt clusterstatus. Zodra een script is voltooid, moet tooa status ' actief' hello cluster worden geretourneerd.

> [!IMPORTANT]
> Zelfs als Hallo cluster heeft een status 'actief', bevatten hello mislukte script verbroken dingen. Een script kan bijvoorbeeld bestanden die nodig zijn door Hallo cluster verwijderen.
>
> Scripts acties uitgevoerd met bevoegdheden van de hoofdmap, dus moet u ervoor zorgen dat u wat een script doet begrijpt voordat u het cluster tooyour toepast.

Bij het toepassen van een script tooa cluster Hallo clusterstatus toofrom wijzigingen **met** te**geaccepteerde**, klikt u vervolgens **HDInsight configuratie**, en ten slotte terug te**Met** voor geslaagde scripts. Hallo scriptstatus wordt geregistreerd in de geschiedenis van de scriptactie hello en u kunt deze informatie toodetermine of Hallo-script is geslaagd of mislukt. Bijvoorbeeld, Hallo `Get-AzureRmHDInsightScriptActionHistory` PowerShell-cmdlet kan worden gebruikt tooview Hallo status van een script. Deze retourneert informatie vergelijkbare toohello volgende tekst:

    ScriptExecutionId : 635918532516474303
    StartTime         : 8/14/2017 7:40:55 PM
    EndTime           : 8/14/2017 7:41:05 PM
    Status            : Succeeded

> [!NOTE]
> Als u hebt Hallo cluster (admin) gebruikerswachtwoord gewijzigd nadat het Hallo-cluster is gemaakt, mislukken script acties uitgevoerd op dit cluster. Als u een persistente scriptacties die doel worker-knooppunten hebt, mislukken deze scripts wanneer u Hallo-cluster schaalt.

## <a name="example-script-action-scripts"></a>Voorbeeld van de scriptactie scripts

Script actie scripts kunnen worden gebruikt via Hallo hulpprogramma's te volgen:

* Azure Portal
* Azure PowerShell
* Azure CLI
* HDInsight .NET-SDK

HDInsight biedt scripts tooinstall Hallo onderdelen op HDInsight-clusters te volgen:

| Naam | Script |
| --- | --- |
| **Een Azure Storage-account toevoegen** |https://hdiconfigactions.BLOB.Core.Windows.NET/linuxaddstorageaccountv01/Add-Storage-account-v01.sh. Zie [toevoegen extra opslagruimte tooan HDInsight-cluster](hdinsight-hadoop-add-storage.md). |
| **Hue installeren** |https://hdiconfigactions.BLOB.Core.Windows.NET/linuxhueconfigactionv02/Install-HUE-uber-v02.sh. Zie [installeert en gebruikt Hue op HDInsight-clusters](hdinsight-hadoop-hue-linux.md). |
| **Functie installeren** |https://RAW.githubusercontent.com/hdinsight/Presto-hdinsight/master/installpresto.sh. Zie [installeert en gebruikt de functie op HDInsight-clusters](hdinsight-hadoop-install-presto.md). |
| **Solr installeren** |https://hdiconfigactions.BLOB.Core.Windows.NET/linuxsolrconfigactionv01/solr-Installer-v01.sh. Zie [installeert en gebruikt Solr op HDInsight-clusters](hdinsight-hadoop-solr-install-linux.md). |
| **Giraph installeren** |https://hdiconfigactions.BLOB.Core.Windows.NET/linuxgiraphconfigactionv01/giraph-Installer-v01.sh. Zie [installeert en gebruikt Giraph op HDInsight-clusters](hdinsight-hadoop-giraph-install-linux.md). |
| **Vooraf laden Hive-bibliotheken** |https://hdiconfigactions.BLOB.Core.Windows.NET/linuxsetupcustomhivelibsv01/Setup-customhivelibs-v01.sh. Zie [toevoegen Hive-bibliotheken op HDInsight-clusters](hdinsight-hadoop-add-hive-libraries.md). |
| **Mono installeren of bijwerken** | https://hdiconfigactions.BLOB.Core.Windows.NET/Install-mono/Install-mono.Bash. Zie [installeren of update Mono op HDInsight](hdinsight-hadoop-install-mono.md). |

## <a name="use-a-script-action-during-cluster-creation"></a>Een actie Script gebruiken tijdens het maken van het cluster

Deze sectie bevat voorbeelden op Hallo van de verschillende manieren kunt met scriptacties bij het maken van een HDInsight-cluster.

### <a name="use-a-script-action-during-cluster-creation-from-hello-azure-portal"></a>Een actie Script gebruiken tijdens het maken van hello Azure-portal

1. Beginnen met het maken van een cluster, zoals beschreven op [maken Hadoop-clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md). Wanneer u Hallo bereiken stoppen __Cluster samenvatting__ sectie.

2. Van Hallo __Cluster samenvatting__ sectie, selecteer Hallo __bewerken__ koppelen voor __geavanceerde instellingen__.

    ![Koppeling van de geavanceerde instellingen](./media/hdinsight-hadoop-customize-cluster-linux/advanced-settings-link.png)

3. Van Hallo __geavanceerde instellingen__ sectie __acties Script__. Van Hallo __acties Script__ sectie __+ nieuw verzenden__

    ![Een nieuwe scriptactie verzenden](./media/hdinsight-hadoop-customize-cluster-linux/add-script-action.png)

4. Gebruik Hallo __selecteert u een script__ vermelding tooselect een vooraf gemaakte script. selecteert u een aangepast script toouse __aangepaste__ en geef vervolgens Hallo __naam__ en __Bash script URI__ voor uw script.

    ![Een script in een select script Hallo toevoegen](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    Hallo volgende tabel beschrijft Hallo elementen op Hallo formulier:

    | Eigenschap | Waarde |
    | --- | --- |
    | Selecteer een script | toouse uw eigen script, selecteer __aangepaste__. Selecteer een van de Hallo is aangeleverd scripts. |
    | Naam |Geef een naam voor de scriptactie Hallo. |
    | Bash script URI |Geef Hallo URI toohello script is aangeroepen toocustomize Hallo-cluster. |
    | Worker-HEAD/Zookeeper |Hallo-knooppunten opgeven (**Head**, **Worker**, of **ZooKeeper**) op waarin aanpassing Hallo script wordt uitgevoerd. |
    | Parameters |Geef parameters op Hallo, indien vereist door het Hallo-script. |

    Gebruik Hallo __deze scriptactie__ vermelding tooensure die Hallo script wordt toegepast tijdens het schalen van bewerkingen.

5. Selecteer __maken__ toosave Hallo script. Vervolgens kunt u __+ indienen nieuwe__ tooadd een ander script.

    ![Meerdere scriptacties](./media/hdinsight-hadoop-customize-cluster-linux/multiple-scripts.png)

    Wanneer u klaar bent met het toe te voegen scripts gebruiken Hallo __Selecteer__ knop en vervolgens Hallo __volgende__ knop tooreturn toohello __Cluster samenvatting__ sectie.

3. toocreate hello cluster, selecteer __maken__ van Hallo __Cluster samenvatting__ selectie.

### <a name="use-a-script-action-from-azure-resource-manager-templates"></a>Gebruik de actie van een Script van Azure Resource Manager-sjablonen

Hallo-voorbeelden in deze sectie laten zien hoe toouse script acties met Azure Resource Manager-sjablonen.

#### <a name="before-you-begin"></a>Voordat u begint

* Zie voor meer informatie over het configureren van een werkstation toorun HDInsight Powershell-cmdlets [installeren en configureren van Azure PowerShell](/powershell/azure/overview).
* Voor instructies over het toocreate sjablonen, Zie [Azure Resource Manager-sjablonen samenstellen](../azure-resource-manager/resource-group-authoring-templates.md).
* Als u niet eerder hebt gebruikt Azure PowerShell met Resource Manager, raadpleegt u [Azure PowerShell gebruiken met Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).

#### <a name="create-clusters-using-script-action"></a>Maken van clusters met behulp van de scriptactie

1. Hallo sjabloon tooa locatie volgen op uw computer kopiëren. Deze sjabloon installeert Giraph op Hallo headnodes en worker-knooppunten in Hallo-cluster. U kunt ook controleren of de JSON-sjabloon Hallo geldig is. Plak de inhoud in sjabloon [JSONLint](http://jsonlint.com/), een online JSON-validatiehulpprogramma.

            {
            "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
            "contentVersion": "1.0.0.0",
            "parameters": {
                "clusterLocation": {
                    "type": "string",
                    "defaultValue": "West US",
                    "allowedValues": [ "West US" ]
                },
                "clusterName": {
                    "type": "string"
                },
                "clusterUserName": {
                    "type": "string",
                    "defaultValue": "admin"
                },
                "clusterUserPassword": {
                    "type": "securestring"
                },
                "sshUserName": {
                    "type": "string",
                    "defaultValue": "username"
                },
                "sshPassword": {
                    "type": "securestring"
                },
                "clusterStorageAccountName": {
                    "type": "string"
                },
                "clusterStorageAccountResourceGroup": {
                    "type": "string"
                },
                "clusterStorageType": {
                    "type": "string",
                    "defaultValue": "Standard_LRS",
                    "allowedValues": [
                        "Standard_LRS",
                        "Standard_GRS",
                        "Standard_ZRS"
                    ]
                },
                "clusterStorageAccountContainer": {
                    "type": "string"
                },
                "clusterHeadNodeCount": {
                    "type": "int",
                    "defaultValue": 1
                },
                "clusterWorkerNodeCount": {
                    "type": "int",
                    "defaultValue": 2
                }
            },
            "variables": {
            },
            "resources": [
                {
                    "name": "[parameters('clusterStorageAccountName')]",
                    "type": "Microsoft.Storage/storageAccounts",
                    "location": "[parameters('clusterLocation')]",
                    "apiVersion": "2015-05-01-preview",
                    "dependsOn": [ ],
                    "tags": { },
                    "properties": {
                        "accountType": "[parameters('clusterStorageType')]"
                    }
                },
                {
                    "name": "[parameters('clusterName')]",
                    "type": "Microsoft.HDInsight/clusters",
                    "location": "[parameters('clusterLocation')]",
                    "apiVersion": "2015-03-01-preview",
                    "dependsOn": [
                        "[concat('Microsoft.Storage/storageAccounts/', parameters('clusterStorageAccountName'))]"
                    ],
                    "tags": { },
                    "properties": {
                        "clusterVersion": "3.2",
                        "osType": "Linux",
                        "clusterDefinition": {
                            "kind": "hadoop",
                            "configurations": {
                                "gateway": {
                                    "restAuthCredential.isEnabled": true,
                                    "restAuthCredential.username": "[parameters('clusterUserName')]",
                                    "restAuthCredential.password": "[parameters('clusterUserPassword')]"
                                }
                            }
                        },
                        "storageProfile": {
                            "storageaccounts": [
                                {
                                    "name": "[concat(parameters('clusterStorageAccountName'),'.blob.core.windows.net')]",
                                    "isDefault": true,
                                    "container": "[parameters('clusterStorageAccountContainer')]",
                                    "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('clusterStorageAccountName')), '2015-05-01-preview').key1]"
                                }
                            ]
                        },
                        "computeProfile": {
                            "roles": [
                                {
                                    "name": "headnode",
                                    "targetInstanceCount": "[parameters('clusterHeadNodeCount')]",
                                    "hardwareProfile": {
                                        "vmSize": "Large"
                                    },
                                    "osProfile": {
                                        "linuxOperatingSystemProfile": {
                                            "username": "[parameters('sshUserName')]",
                                            "password": "[parameters('sshPassword')]"
                                        }
                                    },
                                    "scriptActions": [
                                        {
                                            "name": "installGiraph",
                                            "uri": "https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh",
                                            "parameters": ""
                                        }
                                    ]
                                },
                                {
                                    "name": "workernode",
                                    "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                                    "hardwareProfile": {
                                        "vmSize": "Large"
                                    },
                                    "osProfile": {
                                        "linuxOperatingSystemProfile": {
                                            "username": "[parameters('sshUserName')]",
                                            "password": "[parameters('sshPassword')]"
                                        }
                                    },
                                    "scriptActions": [
                                        {
                                            "name": "installR",
                                            "uri": "https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh",
                                            "parameters": ""
                                        }
                                    ]
                                }
                            ]
                        }
                    }
                }
            ],
            "outputs": {
                "cluster":{
                    "type" : "object",
                    "value" : "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
                }
            }
        }
2. Open Azure PowerShell en tooyour aanmelden met Azure-account. Na het opgeven van referenties van uw retourneert Hallo opdracht informatie over uw account.

        Add-AzureRmAccount

        Id                             Type       ...
        --                             ----
        someone@example.com            User       ...
3. Als u meerdere abonnementen, bieden Hallo abonnements-ID hebt willen toouse voor implementatie.

        Select-AzureRmSubscription -SubscriptionID <YourSubscriptionId>

    > [!NOTE]
    > U kunt `Get-AzureRmSubscription` tooget een lijst met alle abonnementen die zijn gekoppeld aan je account, waaronder Hallo abonnements-ID voor elk criterium.

4. Als u een bestaande resourcegroep niet hebt, kunt u een resourcegroep maken. Geef de naam op Hallo van Hallo resourcegroep en locatie die u nodig hebt voor uw oplossing. Een samenvatting van de nieuwe resourcegroep hello wordt geretourneerd.

        New-AzureRmResourceGroup -Name myresourcegroup -Location "West US"

        ResourceGroupName : myresourcegroup
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/######/resourceGroups/ExampleResourceGroup

5. toocreate een implementatie voor de resourcegroep, Voer Hallo **New-AzureRmResourceGroupDeployment** opdracht in en geef parameters op Hallo die nodig zijn. Hallo-parameters zijn Hallo gegevens te volgen:

    * Een naam voor uw implementatie
    * Hallo-naam van de resourcegroep
    * Hallo-pad of de URL toohello sjabloon die u hebt gemaakt.

  Als de sjabloon parameters vereist, moet u ook deze parameters doorgeven. In dit geval is Hallo script actie tooinstall R op Hallo cluster geen parameters vereist.

        New-AzureRmResourceGroupDeployment -Name mydeployment -ResourceGroupName myresourcegroup -TemplateFile <PathOrLinkToTemplate>

    Bent u na vragen aan gebruiker tooprovide waarden voor Hallo-parameters in Hallo sjabloon worden gedefinieerd.

1. Wanneer het Hallo-resourcegroep is geïmplementeerd, wordt een overzicht van Hallo implementatie weergegeven.

          DeploymentName    : mydeployment
          ResourceGroupName : myresourcegroup
          ProvisioningState : Succeeded
          Timestamp         : 8/14/2017 7:00:27 PM
          Mode              : Incremental
          ...

2. Als uw implementatie mislukt, kunt u de volgende cmdlets tooget informatie over mislukte Hallo Hallo kunt gebruiken.

        Get-AzureRmResourceGroupDeployment -ResourceGroupName myresourcegroup -ProvisioningState Failed

### <a name="use-a-script-action-during-cluster-creation-from-azure-powershell"></a>Een actie Script gebruiken tijdens het maken van Azure PowerShell

In deze sectie gebruiken we Hallo [toevoegen AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) cmdlet tooinvoke scripts met behulp van de scriptactie toocustomize een cluster. Voordat u doorgaat, zorg ervoor dat u hebt geïnstalleerd en geconfigureerd Azure PowerShell. Zie voor meer informatie over het configureren van een werkstation toorun HDInsight PowerShell-cmdlets [installeren en configureren van Azure PowerShell](/powershell/azure/overview).

Hallo volgende script laat zien hoe tooapply een scriptactie bij het maken van een cluster met behulp van PowerShell:

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=5-90)]

Het kan enkele minuten duren voordat Hallo-cluster is gemaakt.

### <a name="use-a-script-action-during-cluster-creation-from-hello-hdinsight-net-sdk"></a>Een actie Script gebruiken tijdens het maken van Hallo HDInsight .NET SDK

Hallo HDInsight .NET SDK biedt clientbibliotheken die het eenvoudiger toowork met HDInsight vanuit een .NET-toepassing maakt. Zie voor een voorbeeld van code [maken Linux gebaseerde clusters in HDInsight met behulp Hallo .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).

## <a name="apply-a-script-action-tooa-running-cluster"></a>Toepassen van een scriptactie tooa met cluster

In deze sectie meer informatie over hoe tooapply acties tooa cluster met een script.

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-azure-portal"></a>Toepassen van een scriptactie tooa cluster uitvoert vanuit hello Azure-portal

1. Van Hallo [Azure-portal](https://portal.azure.com), selecteer uw HDInsight-cluster.

2. Selecteer uit Hallo HDInsight-cluster overzicht Hallo **scriptacties** tegel.

    ![Script acties tegel](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > U kunt ook selecteren **alle instellingen** en selecteer vervolgens **scriptacties** van Hallo gedeelte instellingen.

3. Vanaf de bovenkant van de Hallo Hallo scriptacties sectie, selecteer **indienen nieuwe**.

    ![Toevoegen van een script tooa met cluster](./media/hdinsight-hadoop-customize-cluster-linux/add-script-running-cluster.png)

4. Gebruik Hallo __selecteert u een script__ vermelding tooselect een vooraf gemaakte script. selecteert u een aangepast script toouse __aangepaste__ en geef vervolgens Hallo __naam__ en __Bash script URI__ voor uw script.

    ![Een script in een select script Hallo toevoegen](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    Hallo volgende tabel beschrijft Hallo elementen op Hallo formulier:

    | Eigenschap | Waarde |
    | --- | --- |
    | Selecteer een script | toouse uw eigen script, selecteer __aangepaste__. Anders selecteert u een geleverde script. |
    | Naam |Geef een naam voor de scriptactie Hallo. |
    | Bash script URI |Geef Hallo URI toohello script is aangeroepen toocustomize Hallo-cluster. |
    | Worker-HEAD/Zookeeper |Hallo-knooppunten opgeven (**Head**, **Worker**, of **ZooKeeper**) op waarin aanpassing Hallo script wordt uitgevoerd. |
    | Parameters |Geef parameters op Hallo, indien vereist door het Hallo-script. |

    Gebruik Hallo __deze scriptactie__ vermelding toomake ervoor Hallo script wordt toegepast tijdens het schalen van bewerkingen.

5. Gebruik tot slot Hallo **maken** knop tooapply Hallo script toohello cluster.

### <a name="apply-a-script-action-tooa-running-cluster-from-azure-powershell"></a>Toepassen van een scriptactie tooa cluster uitvoeren vanaf Azure PowerShell

Voordat u doorgaat, zorg ervoor dat u hebt geïnstalleerd en geconfigureerd Azure PowerShell. Zie voor meer informatie over het configureren van een werkstation toorun HDInsight PowerShell-cmdlets [installeren en configureren van Azure PowerShell](/powershell/azure/overview).

Hallo volgende voorbeeld laat zien hoe tooapply een script actie tooa actief cluster:

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=105-117)]

Zodra het Hallo-bewerking is voltooid, wordt informatie vergelijkbare toohello volgende tekst:

    OperationState  : Succeeded
    ErrorMessage    :
    Name            : Giraph
    Uri             : https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh
    Parameters      :
    NodeTypes       : {HeadNode, WorkerNode}

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-azure-cli"></a>Toepassen van een scriptactie tooa cluster uitvoert vanuit hello Azure CLI

Voordat u doorgaat, zorg ervoor dat u hebt geïnstalleerd en geconfigureerd hello Azure CLI. Zie voor meer informatie [installeren hello Azure CLI](../cli-install-nodejs.md).

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. tooswitch tooAzure modus Resource Manager, gebruikt u na de opdracht op de opdrachtregel Hallo Hallo:

        azure config mode arm

2. Gebruik hello tooauthenticate tooyour Azure-abonnement te volgen.

        azure login

3. Hallo opdracht tooapply na een script actie tooa actief cluster gebruiken

        azure hdinsight script-action create <clustername> -g <resourcegroupname> -n <scriptname> -u <scriptURI> -t <nodetypes>

    Als u de parameters voor deze opdracht weglaat, wordt u gevraagd deze. Als script die u met opgeeft Hallo `-u` accepteert parameters, kunt u ze met behulp van Hallo `-p` parameter.

    Geldige knooppunt-typen zijn `headnode`, `workernode`, en `zookeeper`. Als Hallo script knooppunttypen toegepaste toomultiple moet, geef Hallo typen gescheiden door een ';'. Bijvoorbeeld `-n headnode;workernode`.

    toopersist Hallo script, Hallo toevoegen `--persistOnSuccess`. U kunt ook deze persistent maken Hallo script later met behulp van `azure hdinsight script-action persisted set`.

    Zodra het Hallo-taak is voltooid, wordt uitvoer vergelijkbare toohello volgende tekst:

        info:    Executing command hdinsight script-action create
        + Executing Script Action on HDInsight cluster
        data:    Operation Info
        data:    ---------------
        data:    Operation status:
        data:    Operation ID:  b707b10e-e633-45c0-baa9-8aed3d348c13
        info:    hdinsight script-action create command OK

### <a name="apply-a-script-action-tooa-running-cluster-using-rest-api"></a>Toepassen van een scriptactie tooa actief cluster met behulp van REST-API

Zie [scriptacties uitvoeren op een actief cluster](https://msdn.microsoft.com/library/azure/mt668441.aspx).

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-hdinsight-net-sdk"></a>Toepassen van een scriptactie tooa cluster uitvoert vanuit Hallo HDInsight .NET SDK

Zie voor een voorbeeld van het gebruik van Hallo .NET SDK tooapply scripts tooa cluster [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).

## <a name="view-history-promote-and-demote-script-actions"></a>Geschiedenis weergeven en degraderen scriptacties promoveren

### <a name="using-hello-azure-portal"></a>Met behulp van hello Azure-portal

1. Van Hallo [Azure-portal](https://portal.azure.com), selecteer uw HDInsight-cluster.

2. Selecteer uit Hallo HDInsight-cluster overzicht Hallo **scriptacties** tegel.

    ![Script acties tegel](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > U kunt ook selecteren **alle instellingen** en selecteer vervolgens **scriptacties** van Hallo gedeelte instellingen.

4. Een geschiedenis van scripts voor dit cluster wordt weergegeven op Hallo scriptacties sectie. Deze informatie omvat een lijst met persistente scripts. Hallo onderstaande schermafbeelding ziet u dat Hallo Solr script is uitgevoerd op dit cluster. Hallo schermopname weergegeven de persistente scripts niet.

    ![De sectie Acties script](./media/hdinsight-hadoop-customize-cluster-linux/script-action-history.png)

5. Sectie met eigenschappen voor dit script Hallo selecteren van een script uit Hallo geschiedenis worden weergegeven. U kunt vanaf de bovenkant van de Hallo van welkomstscherm, Hallo script opnieuw uitvoeren of promoveer deze.

    ![Eigenschappen van de script-acties](./media/hdinsight-hadoop-customize-cluster-linux/promote-script-actions.png)

6. U kunt ook Hallo **...**  toohello rechts van de vermeldingen op Hallo scriptacties sectie tooperform acties.

    ![Acties... script gebruik](./media/hdinsight-hadoop-customize-cluster-linux/deletepromoted.png)

### <a name="using-azure-powershell"></a>Azure PowerShell gebruiken

| Gebruik de volgende Hallo... | te... |
| --- | --- |
| Get-AzureRmHDInsightPersistedScriptAction |Informatie over persistente scriptacties ophalen |
| Get-AzureRmHDInsightScriptActionHistory |Een geschiedenis van script acties toegepast toohello cluster of details voor een specifiek script ophalen |
| Set-AzureRmHDInsightPersistedScriptAction |Bijdraagt aan een ad-hoc script actie tooa persistent scriptactie |
| Remove-AzureRmHDInsightPersistedScriptAction |Selecteert, wordt een persistent script actie tooan ad-hoc-actie |

> [!IMPORTANT]
> Met behulp van `Remove-AzureRmHDInsightPersistedScriptAction` wordt niet ongedaan gemaakt Hallo-bewerkingen worden uitgevoerd door een script. Deze cmdlet worden alleen persistent gemaakte vlag Hallo verwijderd.

Hallo volgende voorbeeldscript wordt gedemonstreerd met behulp van Hallo cmdlets toopromote vervolgens degraderen van een script.

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=123-140)]

### <a name="using-hello-azure-cli"></a>Hello Azure CLI gebruiken

| Gebruik de volgende Hallo... | te... |
| --- | --- |
| `azure hdinsight script-action persisted list <clustername>` |Een lijst met persistente scriptacties ophalen |
| `azure hdinsight script-action persisted show <clustername> <scriptname>` |Ophalen van gegevens op een specifieke persistente scriptacties actie |
| `azure hdinsight script-action history list <clustername>` |Een geschiedenis van script acties toegepast toohello cluster ophalen |
| `azure hdinsight script-action history show <clustername> <scriptname>` |Ophalen van informatie over een specifiek script-actie |
| `azure hdinsight script action persisted set <clustername> <scriptexecutionid>` |Bijdraagt aan een ad-hoc script actie tooa persistent scriptactie |
| `azure hdinsight script-action persisted delete <clustername> <scriptname>` |Selecteert, wordt een persistent script actie tooan ad-hoc-actie |

> [!IMPORTANT]
> Met behulp van `azure hdinsight script-action persisted delete` wordt niet ongedaan gemaakt Hallo-bewerkingen worden uitgevoerd door een script. Deze cmdlet worden alleen persistent gemaakte vlag Hallo verwijderd.

### <a name="using-hello-hdinsight-net-sdk"></a>Met behulp van Hallo HDInsight .NET SDK

Voor een voorbeeld van het gebruik van Hallo .NET SDK tooretrieve script geschiedenis van een cluster promoten of degraderen van scripts, Zie [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).

> [!NOTE]
> Dit voorbeeld wordt ook hoe een HDInsight-toepassing gebruikt tooinstall Hallo .NET SDK.

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a>Ondersteuning voor open-source software gebruikt op HDInsight-clusters

Hallo Microsoft Azure HDInsight-service gebruikt een ecosysteem van open-source technologieën gevormd rond Hadoop. Microsoft Azure biedt een algemeen niveau van ondersteuning voor de open source-technologieën. Zie voor meer informatie, Hallo **ondersteuning bereik** sectie Hallo [ondersteuning Veelgestelde vragen over Azure-website](https://azure.microsoft.com/support/faq/). Hallo HDInsight-service biedt een extra verificatieniveau van ondersteuning voor ingebouwde onderdelen.

Er zijn twee soorten open source-onderdelen die beschikbaar in Hallo HDInsight-service zijn:

* **Ingebouwde onderdelen** -deze onderdelen vooraf zijn geïnstalleerd op HDInsight-clusters en geef de kernfunctionaliteit van Hallo-cluster. YARN ResourceManager Hallo Hive query language (HiveQL) en Hallo Mahout bibliotheek bijvoorbeeld behoren toothis categorie. Een volledige lijst met clusteronderdelen is beschikbaar in [wat is er nieuw in Hallo Hadoop-clusterversies geleverd door HDInsight](hdinsight-component-versioning.md).
* **Aangepaste onderdelen** -u, als een gebruiker van het Hallo-cluster kunt installeren of gebruiken in uw werkbelasting een onderdeel is beschikbaar in Hallo community of door u gemaakte.

> [!WARNING]
> Onderdelen van Hallo HDInsight-cluster worden volledig ondersteund. Microsoft Support helpt tooisolate en oplossen van problemen met gerelateerde toothese onderdelen.
>
> Aangepaste onderdelen ontvangen binnen commercieel redelijke ondersteuning toohelp u toofurther Hallo probleem op te lossen. Microsoft ondersteuning mogelijk kunnen tooresolve Hallo probleem of ze kunnen u vragen tooengage beschikbare kanalen voor Hallo open-source technologieën waar grondige kennis van deze technologie kan worden gevonden. Bijvoorbeeld: Er zijn veel community-sites die kunnen worden gebruikt, zoals: [MSDN-forum voor HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Ook hebben Apache projecten project-sites op [http://apache.org](http://apache.org), bijvoorbeeld: [Hadoop](http://hadoop.apache.org/).

Hallo HDInsight-service biedt verschillende manieren toouse aangepaste onderdelen. Hallo hetzelfde niveau van de ondersteuning van toepassing is, ongeacht hoe een onderdeel gebruikt of is geïnstalleerd op Hallo-cluster. Hallo volgende lijst bevat de meest voorkomende manieren Hallo dat aangepaste onderdelen kunnen worden gebruikt op HDInsight-clusters:

1. Verzending van taak - Hadoop- of andere typen taken die worden uitgevoerd of het gebruik van aangepaste onderdelen kan worden verzonden toohello cluster.

2. Aanpassing van de cluster - tijdens het maken van het cluster, kunt u aanvullende instellingen en aangepaste onderdelen die zijn geïnstalleerd op de clusterknooppunten Hallo opgeven.

3. Steekproeven - voor populaire aangepaste onderdelen, Microsoft en anderen kunnen voorbeelden van hoe deze onderdelen kunnen worden gebruikt op Hallo HDInsight-clusters bieden. Deze voorbeelden worden geleverd zonder ondersteuning.

## <a name="troubleshooting"></a>Problemen oplossen

Hier kunt u Ambari web UI tooview informatie die wordt geregistreerd door scriptacties. Als Hallo-script is mislukt tijdens maken van het cluster, zijn Hallo Logboeken ook beschikbaar in Hallo standaardopslagaccount die zijn gekoppeld aan het Hallo-cluster. Deze sectie bevat informatie over hoe tooretrieve Hallo registreert met behulp van deze beide opties.

### <a name="using-hello-ambari-web-ui"></a>Met behulp van Hallo Ambari-Webgebruikersinterface

1. Navigeer in uw browser toohttps://CLUSTERNAME.azurehdinsight.net. Vervang CLUSTERNAME door Hallo-naam van uw HDInsight-cluster.

    Voer desgevraagd Hallo beheerder naam (admin) en het wachtwoord voor Hallo-cluster. Mogelijk hebt u tooreenter Hallo beheerdersreferenties in een webformulier.

2. Selecteer in de balk Hallo bovenaan Hallo Hallo pagina Hallo **ops** vermelding. Een lijst met huidige en vorige bewerkingen die worden uitgevoerd op Hallo cluster door Ambari wordt weergegeven.

    ![Ambari web UI-balk met ops geselecteerd](./media/hdinsight-hadoop-customize-cluster-linux/ambari-nav.png)

3. Zoeken naar Hallo vermeldingen waarvoor **uitvoeren\_customscriptaction** in Hallo **Operations** kolom. Deze vermeldingen worden gemaakt als Hallo scriptacties uitvoert.

    ![Schermopname van bewerkingen](./media/hdinsight-hadoop-customize-cluster-linux/ambariscriptaction.png)

    tooview hello STDOUT en STDERR uitvoer, selecteer Hallo run\customscriptaction post en detailanalyse Hallo koppelingen. Deze uitvoer wordt gegenereerd wanneer het Hallo-script wordt uitgevoerd, en mogelijk bevatten nuttige informatie.

### <a name="access-logs-from-hello-default-storage-account"></a>Toegang tot logboeken van het standaardopslagaccount Hallo

Als Hallo cluster maken vanwege fout in tooa script actie mislukt, zijn Hallo logboeken toegankelijk vanuit Hallo cluster storage-account.

* Hallo opslag logboeken zijn beschikbaar op `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.

    ![Schermopname van bewerkingen](./media/hdinsight-hadoop-customize-cluster-linux/script_action_logs_in_storage.png)

    In deze map Hallo logboeken afzonderlijk ingedeeld voor headnode, workernode en zookeeper-knooppunten. Een aantal voorbeelden:

    * **Headnode** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`

    * **Werkrolknooppunt** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`

    * **Zookeeper-knooppunt** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`

* Alle stdout en stderr van de bijbehorende host Hallo is geüpload toohello storage-account. Er is een **uitvoer -\*.txt** en **fouten -\*.txt** voor elke scriptactie. Hallo uitvoer-txt-bestand bevat informatie over Hallo URI van Hallo-script dat is uitgevoerd op Hallo host. Bijvoorbeeld

        'Start downloading script locally: ', u'https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh'

* Het is mogelijk dat u een script actie cluster herhaaldelijk met de Hallo maken dezelfde naam. In dat geval kunt u de relevante Hallo-logboeken op basis van datum-mapnaam Hallo onderscheiden. Hallo-mapstructuur voor een cluster (mijncluster) gemaakt op verschillende datums verschijnt bijvoorbeeld vergelijkbare toohello logboekvermeldingen te volgen:

    `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04` `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`

* Als u een script actie cluster met de Hallo maakt dezelfde naam op Hallo dezelfde dag, kunt u Hallo uniek voorvoegsel tooidentify Hallo relevante logboekbestanden.

* Als u een cluster in de buurt van 12:00 AM (middernacht) maakt, is het mogelijk dat de logboekbestanden Hallo twee dagen overbruggen. In dergelijke gevallen kunt u twee andere datum mappen voor Hallo Zie hetzelfde cluster.

* Uploaden logboek bestanden toohello standaardcontainer kan een too5 minuten, met name voor grote clusters in beslag nemen. Dus als u tooaccess Hallo logboeken wilt, moet u niet onmiddellijk verwijderen Hallo cluster als een scriptactie is mislukt.

### <a name="ambari-watchdog"></a>Ambari watchdog

> [!WARNING]
> Hallo-wachtwoord voor Hallo Ambari Watchdog (hdinsightwatchdog) op uw Linux gebaseerde HDInsight-cluster niet wijzigen. Wijzigen van Hallo het wachtwoord voor dit account wordt verbroken Hallo mogelijkheid toorun nieuwe scriptacties op Hallo HDInsight-cluster.

### <a name="cant-import-name-blobservice"></a>Naam BlobService kan niet worden geïmporteerd.

__Symptomen__: Hallo script actie mislukt. Wanneer u hello bewerking in Ambari bekijkt tekst vergelijkbare toohello volgende fout weergegeven:

```
Traceback (most recent call list):
  File "/var/lib/ambari-agent/cache/custom_actions/scripts/run_customscriptaction.py", line 21, in <module>
    from azure.storage.blob import BlobService
ImportError: cannot import name BlobService
```

__Oorzaak__: deze fout treedt op als Hallo Python Azure Storage client bijwerkt die is opgenomen in Hallo HDInsight-cluster. HDInsight verwacht Azure Storage client 0.20.0.

__Resolutie__: tooresolve deze fout handmatig verbinding maken met behulp van tooeach cluster knooppunt `ssh` en Hallo gebruik de volgende opdracht tooreinstall Hallo juiste opslag-clientversie:

```
sudo pip install azure-storage==0.20.0
```

Zie voor informatie over het maken van verbinding toohello cluster met SSH, [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

### <a name="history-doesnt-show-scripts-used-during-cluster-creation"></a>Geschiedenis van niet wordt scripts die worden gebruikt tijdens het maken van het cluster weergegeven

Als uw cluster is gemaakt voordat 15 maart 2016, ziet u mogelijk niet een vermelding in de geschiedenis van de scriptactie. Als u het formaat van Hallo cluster na 15 maart 2016 Hallo scripts met behulp van tijdens het maken van het cluster worden weergegeven in de geschiedenis zoals die worden toegepast toonew knooppunten in cluster als onderdeel van Hallo Hallo vergroten of verkleinen van de bewerking.

Er zijn twee uitzonderingen:

* Als uw cluster is gemaakt vóór 1 September 2015. Deze datum is wanneer scriptacties zijn geïntroduceerd. Een cluster is gemaakt voor deze datum kan niet hebben gebruikt scriptacties voor maken van het cluster.

* Als u meerdere scriptacties gebruikt tijdens het maken van het cluster en Hallo dezelfde naam voor meerdere scripts of Hallo gebruikt naam dezelfde, dezelfde URI, maar verschillende parameters voor meerdere scripts. In dergelijke gevallen wordt u Hallo volgende fout:

    Op dit cluster vanwege tooconflicting scriptnamen in bestaande scripts worden geen nieuwe script acties kunnen worden uitgevoerd. Scriptnamen die zijn opgegeven bij het cluster moet maken allemaal uniek zijn. Bestaande scripts worden uitgevoerd op formaat.

## <a name="next-steps"></a>Volgende stappen

* [Scriptactie-scripts ontwikkelen voor HDInsight](hdinsight-hadoop-script-actions-linux.md)
* [Installeren en gebruiken van Solr op HDInsight-clusters](hdinsight-hadoop-solr-install-linux.md)
* [Installeren en gebruiken van Giraph op HDInsight-clusters](hdinsight-hadoop-giraph-install-linux.md)
* [Extra opslagruimte tooan HDInsight-cluster toevoegen](hdinsight-hadoop-add-storage.md)

[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster-linux/HDI-Cluster-state.png "Fasen tijdens het maken van het cluster"
