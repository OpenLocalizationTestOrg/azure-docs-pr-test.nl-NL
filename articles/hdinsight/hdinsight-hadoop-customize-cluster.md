---
title: acties - Azure HDInsight-Clusters met behulp van aaaCustomize script | Microsoft Docs
description: Meer informatie over hoe toocustomize HDInsight-clusters met behulp van de scriptactie.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 3a63e216-4163-40c1-aa04-6b42fd0162ad
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 076fff23e016db47bc7e9963582a545ad638e691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="customize-windows-based-hdinsight-clusters-using-script-action"></a>HDInsight op basis van Windows-clusters met behulp van de scriptactie aanpassen
**Actie script** mag gebruikte tooinvoke [aangepaste scripts](hdinsight-hadoop-script-actions.md) tijdens het Hallo-cluster maken voor het installeren van extra software op een cluster.

Hallo-informatie in dit artikel is een specifieke tooWindows gebaseerde HDInsight-clusters. Zie voor Linux gebaseerde clusters [aanpassen Linux gebaseerde HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster-linux.md).

> [!IMPORTANT]
> Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

HDInsight-clusters kunnen worden aangepast op tal van andere manieren zoals inclusief extra Azure Storage-accounts, Hallo Hadoop wijzigen configuratiebestanden (core site.xml, hive-site.xml, enz.) of toe te voegen gedeeld bibliotheken (bijvoorbeeld Hive, Oozie) algemene locaties in het Hallo-cluster. Deze aanpassingen kunnen doen via Azure PowerShell hello Azure HDInsight .NET SDK of hello Azure-portal. Zie voor meer informatie [maken Hadoop-clusters in HDInsight][hdinsight-provision-cluster].

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell-cli-and-dotnet-sdk.md)]

## <a name="script-action-in-hello-cluster-creation-process"></a>Scriptactie in het proces voor het Hallo-cluster maken
Scriptactie wordt alleen gebruikt terwijl een cluster wordt Hallo proces wordt gemaakt. Hallo volgende diagram wordt weergegeven wanneer het Script wordt uitgevoerd tijdens het maken van een Hallo:

![Aanpassing van HDInsight-cluster en fasen tijdens het maken van het cluster][img-hdi-cluster-states]

Wanneer het Hallo-script wordt uitgevoerd, Hallo cluster Hallo ingevoerd **ClusterCustomization** fase. Opgegeven parallel op Hallo van alle knooppunten in cluster Hallo en biedt volledige beheerdersbevoegdheden op Hallo knooppunten in dit stadium Hallo script met Hallo beheerder systeemaccount wordt uitgevoerd.

> [!NOTE]
> Hebt u beheerdersbevoegdheden op de clusterknooppunten Hallo tijdens de **ClusterCustomization** fase, kunt u Hallo script tooperform bewerkingen zoals het stoppen en starten van services, met inbegrip van Hadoop-gerelateerde services. Dus als onderdeel van het Hallo-script, moet u ervoor zorgen zijn dat Hallo Ambari-services en andere Hadoop-gerelateerde services actief voordat het Hallo-script is voltooid. Deze services zijn vereist toosuccessfully vast Hallo gezondheid en status van de cluster Hallo terwijl deze wordt gemaakt. Als u een willekeurige configuratie op het cluster dat betrekking heeft op deze services wijzigt, moet u Hallo hulpfuncties die beschikbaar zijn. Zie voor meer informatie over hulpfuncties [scriptactie ontwikkelen scripts voor HDInsight][hdinsight-write-script].
>
>

Hallo-uitvoer en Hallo foutenlogboeken voor Hallo script worden opgeslagen in Hallo standaardopslagaccount die u hebt opgegeven voor het Hallo-cluster. Hallo logboeken worden opgeslagen in een tabel met naam Hallo **u < \cluster-name-fragment >< \time-stamp > bestand**. Dit zijn de cumulatieve logboeken van Hallo-script uitvoeren op alle Hallo knooppunten (hoofdknooppunt en worker-knooppunten) in Hallo-cluster.

Elk cluster kan accepteren meerdere scriptacties die worden aangeroepen in Hallo volgorde waarin ze worden opgegeven. Een script kan worden uitgevoerd op het hoofdknooppunt hello, Hallo worker-knooppunten of beide.

HDInsight biedt verschillende scripts tooinstall Hallo onderdelen op HDInsight-clusters te volgen:

| Naam | Script |
| --- | --- |
| **Spark installeren** |https://hdiconfigactions.BLOB.Core.Windows.NET/sparkconfigactionv03/Spark-Installer-v03.ps1. Zie [installeert en gebruikt Spark in HDInsight-clusters][hdinsight-install-spark]. |
| **R installeren** |https://hdiconfigactions.BLOB.Core.Windows.NET/rconfigactionv02/r-Installer-v02.ps1. Zie [installeert en gebruikt R op HDInsight-clusters][hdinsight-install-r]. |
| **Solr installeren** |https://hdiconfigactions.BLOB.Core.Windows.NET/solrconfigactionv01/solr-Installer-v01.ps1. Zie [installeert en gebruikt Solr op HDInsight-clusters](hdinsight-hadoop-solr-install.md). |
| - **Giraph installeren** |https://hdiconfigactions.BLOB.Core.Windows.NET/giraphconfigactionv01/giraph-Installer-v01.ps1. Zie [installeert en gebruikt Giraph op HDInsight-clusters](hdinsight-hadoop-giraph-install.md). |
| **Vooraf laden Hive-bibliotheken** |https://hdiconfigactions.BLOB.Core.Windows.NET/setupcustomhivelibsv01/Setup-customhivelibs-v01.ps1. Zie [toevoegen Hive-bibliotheken op HDInsight-clusters](hdinsight-hadoop-add-hive-libraries.md) |

## <a name="call-scripts-using-hello-azure-portal"></a>Aanroepen van scripts met hello Azure-portal
**Van hello Azure-portal**

1. Beginnen met het maken van een cluster, zoals beschreven op [maken Hadoop-clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).
2. Onder optionele configuratie voor Hallo **scriptacties** blade, klikt u op **toevoegen scriptactie** tooprovide om details over de scriptactie hello, zoals hieronder wordt weergegeven:

    ![Gebruik scriptactie toocustomize een cluster](./media/hdinsight-hadoop-customize-cluster/HDI.CreateCluster.8.png "toocustomize scriptactie gebruik een cluster")

    <table border='1'>
        <tr><th>Eigenschap</th><th>Waarde</th></tr>
        <tr><td>Naam</td>
            <td>Geef een naam voor de scriptactie Hallo.</td></tr>
        <tr><td>Script-URI</td>
            <td>Geef Hallo URI toohello script is aangeroepen toocustomize Hallo-cluster. s</td></tr>
        <tr><td>HEAD/Worker</td>
            <td>Hallo-knooppunten opgeven (**Head** of **Worker**) op waarin aanpassing Hallo script wordt uitgevoerd.</b>.
        <tr><td>Parameters</td>
            <td>Geef parameters op Hallo, indien vereist door het Hallo-script.</td></tr>
    </table>

    Druk op ENTER tooadd meer dan één script actie tooinstall meerdere onderdelen op Hallo-cluster.
3. Klik op **Selecteer** toosave Hallo script actie configuratie en doorgaan met het maken van het cluster.

## <a name="call-scripts-using-azure-powershell"></a>Aanroep scripts met Azure PowerShell
Deze volgende PowerShell-script laat zien hoe tooinstall Spark op Windows gebaseerd HDInsight-cluster.  

    # Provide values for these variables
    $subscriptionID = "<Azure Suscription ID>" # After "Login-AzureRmAccount", use "Get-AzureRmSubscription" toolist IDs.

    $nameToken = "<Enter A Name Token>"  # hello token is use toocreate Azure service names.
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2" # used for creating resource group, storage account, and HDInsight cluster.

    $hdinsightClusterName = $namePrefix + "spark"
    $httpUserName = "admin"
    $httpPassword = "<Enter a Password>"

    $defaultStorageAccountName = "$namePrefix" + "store"
    $defaultBlobContainerName = $hdinsightClusterName

    #############################################################
    # Connect tooAzure
    #############################################################

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }
    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #############################################################
    # Prepare hello dependent components
    #############################################################

    # Create resource group
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_GRS
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                    -StorageAccountName $defaultStorageAccountName `
                                    -StorageAccountKey $storageAccountKey  
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext

    #############################################################
    # Create cluster with ApacheSpark
    #############################################################

    # Specify hello configuration options
    $config = New-AzureRmHDInsightClusterConfig `
                -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
                -DefaultStorageAccountKey $defaultStorageAccountKey


    # Add a script action toohello cluster configuration
    $config = Add-AzureRmHDInsightScriptAction `
                -Config $config `
                -Name "Install Spark" `
                -NodeType HeadNode `
                -Uri https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1 `

    # Start creating a cluster with Spark installed
    New-AzureRmHDInsightCluster `
            -ResourceGroupName $resourceGroupName `
            -ClusterName $hdinsightClusterName `
            -Location $location `
            -ClusterSizeInNodes 2 `
            -ClusterType Hadoop `
            -OSType Windows `
            -DefaultStorageContainer $defaultBlobContainerName `
            -Config $config


tooinstall andere software, moet u het Hallo-scriptbestand tooreplace in Hallo script:

Wanneer u wordt gevraagd, voert u Hallo referenties voor Hallo cluster. Het kan enkele minuten duren voordat Hallo-cluster is gemaakt.

## <a name="call-scripts-using-net-sdk"></a>Aanroepen van scripts die met .NET SDK
Hallo volgende voorbeeld laat zien hoe tooinstall Spark op Windows gebaseerd HDInsight-cluster. tooinstall andere software, moet u het Hallo-scriptbestand tooreplace in Hallo-code.

**een HDInsight-cluster met Spark toocreate**

1. Maak een C#-consoletoepassing in Visual Studio.
2. Voer Hallo volgende opdracht uit op Hallo Nuget Package Manager-Console.

        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
        Install-Package Microsoft.Azure.Management.ResourceManager -Pre
        Install-Package Microsoft.Azure.Management.HDInsight
3. Gebruik Hallo using-instructies in het bestand Program.cs hello te volgen:

        using System;
        using System.Security;
        using Microsoft.Azure;
        using Microsoft.Azure.Management.HDInsight;
        using Microsoft.Azure.Management.HDInsight.Models;
        using Microsoft.Azure.Management.ResourceManager;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest;
        using Microsoft.Rest.Azure.Authentication;
4. Hallo code in de klasse met de volgende Hallo Hallo plaatsen:

        private static HDInsightManagementClient _hdiManagementClient;

        // Replace with your AAD tenant ID if necessary
        private const string TenantId = UserTokenProvider.CommonTenantId;
        private const string SubscriptionId = "<Your Azure Subscription ID>";
        // This is hello GUID for hello PowerShell client. Used for interactive logins in this example.
        private const string ClientId = "1950a258-227b-4e31-a9cf-717495945fc2";
        private const string ResourceGroupName = "<ExistingAzureResourceGroupName>";
        private const string NewClusterName = "<NewAzureHDInsightClusterName>";
        private const int NewClusterNumWorkerNodes = 2;
        private const string NewClusterLocation = "East US";
        private const string NewClusterVersion = "3.2";
        private const string ExistingStorageName = "<ExistingAzureStorageAccountName>";
        private const string ExistingStorageKey = "<ExistingAzureStorageAccountKey>";
        private const string ExistingContainer = "<ExistingAzureBlobStorageContainer>";
        private const string NewClusterType = "Hadoop";
        private const OSType NewClusterOSType = OSType.Windows;
        private const string NewClusterUsername = "<HttpUserName>";
        private const string NewClusterPassword = "<HttpUserPassword>";

        static void Main(string[] args)
        {
            System.Console.WriteLine("Running");

            // Authenticate and get a token
            var authToken = Authenticate(TenantId, ClientId, SubscriptionId);
            // Flag subscription for HDInsight, if it isn't already.
            EnableHDInsight(authToken);
            // Get an HDInsight management client
            _hdiManagementClient = new HDInsightManagementClient(authToken);

            CreateCluster();
        }

        private static void CreateCluster()
        {
            var parameters = new ClusterCreateParameters
            {
                ClusterSizeInNodes = NewClusterNumWorkerNodes,
                Location = NewClusterLocation,
                ClusterType = NewClusterType,
                OSType = NewClusterOSType,
                Version = NewClusterVersion,
                DefaultStorageInfo = new AzureStorageInfo(ExistingStorageName, ExistingStorageKey, ExistingContainer),
                UserName = NewClusterUsername,
                Password = NewClusterPassword,
            };

            ScriptAction sparkScriptAction = new ScriptAction("Install Spark",
                new Uri("https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1"), "");

            parameters.ScriptActions.Add(ClusterNodeType.HeadNode, new System.Collections.Generic.List<ScriptAction> { sparkScriptAction });
            parameters.ScriptActions.Add(ClusterNodeType.WorkerNode, new System.Collections.Generic.List<ScriptAction> { sparkScriptAction });

            _hdiManagementClient.Clusters.Create(ResourceGroupName, NewClusterName, parameters);
        }

        /// <summary>
        /// Authenticate tooan Azure subscription and retrieve an authentication token
        /// </summary>
        /// <param name="TenantId">hello AAD tenant ID</param>
        /// <param name="ClientId">hello AAD client ID</param>
        /// <param name="SubscriptionId">hello Azure subscription ID</param>
        /// <returns></returns>
        static TokenCloudCredentials Authenticate(string TenantId, string ClientId, string SubscriptionId)
        {
            var authContext = new AuthenticationContext("https://login.microsoftonline.com/" + TenantId);
            var tokenAuthResult = authContext.AcquireToken("https://management.core.windows.net/",
                ClientId,
                new Uri("urn:ietf:wg:oauth:2.0:oob"),
                PromptBehavior.Always,
                UserIdentifier.AnyUser);
            return new TokenCloudCredentials(SubscriptionId, tokenAuthResult.AccessToken);
        }
        /// <summary>
        /// Marks your subscription as one that can use HDInsight, if it has not already been marked as such.
        /// </summary>
        /// <remarks>This is essentially a one-time action; if you have already done something with HDInsight
        /// on your subscription, then this isn't needed at all and will do nothing.</remarks>
        /// <param name="authToken">An authentication token for your Azure subscription</param>
        static void EnableHDInsight(TokenCloudCredentials authToken)
        {
            // Create a client for hello Resource manager and set hello subscription ID
            var resourceManagementClient = new ResourceManagementClient(new TokenCredentials(authToken.Token));
            resourceManagementClient.SubscriptionId = SubscriptionId;
            // Register hello HDInsight provider
            var rpResult = resourceManagementClient.Providers.Register("Microsoft.HDInsight");
        }
5. Druk op **F5** toorun Hallo-toepassing.

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a>Ondersteuning voor open-source software gebruikt op HDInsight-clusters
Hallo Microsoft Azure HDInsight-service is een flexibel platform waarmee u toobuild big data-toepassingen in Hallo cloud met behulp van een ecosysteem van open-source technologieën gevormd rond Hadoop. Microsoft Azure biedt een algemeen niveau van ondersteuning voor open-source technologieën, zoals beschreven in Hallo **ondersteunen bereik** sectie Hallo <a href="http://azure.microsoft.com/support/faq/" target="_blank">ondersteunen Veelgestelde vragen over Azure-website</a>. Hallo HDInsight-service biedt een extra verificatieniveau van ondersteuning voor een aantal Hallo-onderdelen, zoals hieronder wordt beschreven.

Er zijn twee soorten open source-onderdelen die beschikbaar in Hallo HDInsight-service zijn:

* **Ingebouwde onderdelen** -deze onderdelen vooraf zijn geïnstalleerd op HDInsight-clusters en geef de kernfunctionaliteit van Hallo-cluster. YARN ResourceManager Hallo Hive query language (HiveQL) en Hallo Mahout bibliotheek bijvoorbeeld behoren toothis categorie. Een volledige lijst met clusteronderdelen is beschikbaar in [wat is er nieuw in Hallo Hadoop-clusterversies geleverd door HDInsight?](hdinsight-component-versioning.md) </a>.
* **Aangepaste onderdelen** -u, als een gebruiker van het Hallo-cluster kunt installeren of gebruiken in uw werkbelasting een onderdeel is beschikbaar in Hallo community of door u gemaakte.

Ingebouwde-onderdelen worden volledig ondersteund en Microsoft Support wordt tooisolate help en oplossen van problemen met gerelateerde toothese onderdelen.

> [!WARNING]
> Onderdelen van Hallo HDInsight-cluster worden volledig ondersteund en Microsoft Support zal helpen tooisolate en oplossen van problemen met gerelateerde toothese onderdelen.
>
> Aangepaste onderdelen ontvangen binnen commercieel redelijke ondersteuning toohelp u toofurther Hallo probleem op te lossen. Dit kan leiden tot het oplossen van Hallo probleem of vragen dat u tooengage beschikbare kanalen voor Hallo openen bron technologieën waar grondige kennis van deze technologie kan worden gevonden. Bijvoorbeeld: Er zijn veel community-sites die kunnen worden gebruikt, zoals: [MSDN-forum voor HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Ook hebben Apache projecten project-sites op [http://apache.org](http://apache.org), bijvoorbeeld: [Hadoop](http://hadoop.apache.org/), [Spark](http://spark.apache.org/).
>
>

Hallo HDInsight-service biedt verschillende manieren toouse aangepaste onderdelen. Ongeacht hoe een onderdeel gebruikt of geïnstalleerd op Hallo-cluster, hello hetzelfde niveau van de ondersteuning van toepassing is. Hieronder volgt een lijst van de meest voorkomende manieren Hallo dat aangepaste onderdelen op HDInsight-clusters kunnen worden gebruikt:

1. Verzending van taak - Hadoop- of andere typen taken die worden uitgevoerd of het gebruik van aangepaste onderdelen kan worden verzonden toohello cluster.
2. Aanpassing van de cluster - tijdens het maken van het cluster, kunt u aanvullende instellingen en aangepaste onderdelen die worden geïnstalleerd op de clusterknooppunten Hallo opgeven.
3. Steekproeven - voor populaire aangepaste onderdelen, Microsoft en anderen kunnen voorbeelden van hoe deze onderdelen kunnen worden gebruikt op Hallo HDInsight-clusters bieden. Deze voorbeelden worden geleverd zonder ondersteuning.

## <a name="develop-script-action-scripts"></a>Scriptactie-scripts ontwikkelen
Zie [scriptactie ontwikkelen scripts voor HDInsight][hdinsight-write-script].

## <a name="see-also"></a>Zie ook
* [Hadoop-clusters maken in HDInsight] [ hdinsight-provision-cluster] vindt u instructies voor hoe toocreate een HDInsight-cluster met behulp van andere aangepaste opties.
* [Scriptactie-scripts ontwikkelen voor HDInsight][hdinsight-write-script]
* [Installeren en gebruiken van Spark in HDInsight-clusters][hdinsight-install-spark]
* [Installeren en gebruiken van R op HDInsight-clusters][hdinsight-install-r]
* [Installeren en gebruiken van Solr op HDInsight-clusters](hdinsight-hadoop-solr-install.md).
* [Installeren en gebruiken van Giraph op HDInsight-clusters](hdinsight-hadoop-giraph-install.md).

[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-write-script]: hdinsight-hadoop-script-actions.md
[hdinsight-provision-cluster]: hdinsight-hadoop-provision-linux-clusters.md
[powershell-install-configure]: /powershell/azureps-cmdlets-docs


[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "Fasen tijdens het maken van het cluster"
