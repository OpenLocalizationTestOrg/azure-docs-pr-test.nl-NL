---
title: aaaManage Hadoop-clusters in HDInsight met .NET SDK - Azure | Microsoft Docs
description: Meer informatie over hoe tooperform administratieve taken voor het Hallo Hadoop-clusters in HDInsight met behulp van HDInsight .NET SDK.
services: hdinsight
editor: cgronlun
manager: jhubbard
tags: azure-portal
author: mumian
documentationcenter: 
ms.assetid: fd134765-c2a0-488a-bca6-184d814d78e9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: d8bbf966b7eba3e943dfb2f764d15d8e52b9be71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-net-sdk"></a>Hadoop-clusters in HDInsight beheren met behulp van de .NET SDK
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

Meer informatie over hoe toomanage HDInsight-clusters met behulp van [HDInsight.NET SDK](https://msdn.microsoft.com/library/mt271028.aspx).

**Vereisten**

Voordat u dit artikel, moet u de volgende Hallo hebben:

* **Een Azure-abonnement**. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

## <a name="connect-tooazure-hdinsight"></a>Verbinding maken met tooAzure HDInsight

U moet Hallo Nuget-pakketten te volgen:

    Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
    Install-Package Microsoft.Azure.Management.ResourceManager -Pre
    Install-Package Microsoft.Azure.Management.HDInsight

Hallo volgende codevoorbeeld ziet u hoe tooconnect tooAzure voordat u HDInsight beheren kunt-clusters onder uw Azure-abonnement.

    using System;
    using Microsoft.Azure;
    using Microsoft.Azure.Management.HDInsight;
    using Microsoft.Azure.Management.HDInsight.Models;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    using Microsoft.Rest.Azure.Authentication;

    namespace HDInsightManagement
    {
        class Program
        {
            private static HDInsightManagementClient _hdiManagementClient;
            // Replace with your AAD tenant ID if necessary
            private const string TenantId = UserTokenProvider.CommonTenantId; 
            private const string SubscriptionId = "<Your Azure Subscription ID>";
            // This is hello GUID for hello PowerShell client. Used for interactive logins in this example.
            private const string ClientId = "1950a258-227b-4e31-a9cf-717495945fc2";

            static void Main(string[] args)
            {
                // Authenticate and get a token
                var authToken = Authenticate(TenantId, ClientId, SubscriptionId);
                // Flag subscription for HDInsight, if it isn't already.
                EnableHDInsight(authToken);
                // Get an HDInsight management client
                _hdiManagementClient = new HDInsightManagementClient(authToken);

                // insert code here

                System.Console.WriteLine("Press ENTER toocontinue");
                System.Console.ReadLine();
            }

            /// <summary>
            /// Authenticate tooan Azure subscription and retrieve an authentication token
            /// </summary>
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
        }
    }

U wordt gevraagd wanneer dit programma wordt uitgevoerd.  Als u niet toosee Hallo prompt wilt, Zie [niet-interactieve verificatie .NET HDInsight-toepassingen maken](hdinsight-create-non-interactive-authentication-dotnet-applications.md).

## <a name="create-clusters"></a>Clusters maken
Zie [maken Linux gebaseerde clusters in HDInsight met behulp Hallo .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)

## <a name="list-clusters"></a>Lijst met clusters
Hallo bevat volgende codefragment clusters en sommige eigenschappen:

    var results = _hdiManagementClient.Clusters.List();
    foreach (var name in results.Clusters) {
        Console.WriteLine("Cluster Name: " + name.Name);
        Console.WriteLine("\t Cluster type: " + name.Properties.ClusterDefinition.ClusterType);
        Console.WriteLine("\t Cluster location: " + name.Location);
        Console.WriteLine("\t Cluster version: " + name.Properties.ClusterVersion);
    }

## <a name="delete-clusters"></a>Clusters verwijderen
Gebruik Hallo volgende code codefragment toodelete een cluster synchroon of asynchroon: 

    _hdiManagementClient.Clusters.Delete("<Resource Group Name>", "<Cluster Name>");
    _hdiManagementClient.Clusters.DeleteAsync("<Resource Group Name>", "<Cluster Name>");

## <a name="scale-clusters"></a>Clusters schalen
Hallo-cluster schalen van functie kunt u toochange Hallo aantal worker-knooppunten gebruikt door een cluster dat wordt uitgevoerd in Azure HDInsight zonder toore-Hallo cluster maken.

> [!NOTE]
> Alleen clusters met HDInsight versie 3.1.3 of hoger worden ondersteund. Als u niet zeker Hallo versie van het cluster weet, kunt u de eigenschappenpagina Hallo controleren.  Zie [lijst en geeft weer clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).
> 
> 

Hallo gevolgen van het aantal gegevensknooppunten voor elk type ondersteund door HDInsight cluster Hallo wijzigen:

* Hadoop
  
    Hallo aantal worker-knooppunten van een Hadoop-cluster dat wordt uitgevoerd zonder enige impact op alle taken die in behandeling of wordt uitgevoerd, kunt u naadloos verhogen. Nieuwe taken kunnen ook worden verzonden tijdens het Hallo-bewerking wordt uitgevoerd. Fouten in een bewerking voor schaal worden probleemloos verwerkt zodat hello cluster altijd functioneel is overblijft.
  
    Wanneer een Hadoop-cluster wordt verkleind door het aantal gegevensknooppunten hello te verminderen, worden sommige services in de cluster Hallo Hallo opnieuw gestart. Dit zorgt ervoor dat alle actieve en in behandeling zijnde taken toofail op Hallo Hallo schalen van de bewerking is voltooid. U kunt echter Hallo taken verzenden zodra Hallo-bewerking voltooid is.
* HBase
  
    U kunt naadloos toevoegen of verwijderen van knooppunten tooyour HBase-cluster, terwijl deze wordt uitgevoerd. Regionale Servers worden automatisch verdeeld binnen een paar minuten na voltooiing van Hallo bewerking schalen. U kunt echter ook handmatig Hallo regionale servers verdelen door logboekregistratie in Hallo headnode van het cluster en actieve Hallo volgende opdrachten uit een opdrachtpromptvenster:
  
        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* Storm
  
    U kunt naadloos toevoegen of verwijderen van gegevens knooppunten tooyour Storm-cluster, terwijl deze wordt uitgevoerd. Maar nadat de bewerking schalen Hallo installatie is voltooid, moet u toorebalance Hallo topologie.
  
    Herverdeling kan worden uitgevoerd op twee manieren:
  
  * Storm-webgebruikersinterface
  * Hulpprogramma voor opdrachtregelinterface (CLI)
    
    Raadpleeg toohello [Apache Storm documentatie](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) voor meer informatie.
    
    Hallo Storm-webgebruikersinterface is beschikbaar op Hallo HDInsight-cluster:
    
    ![HDInsight Storm scale deel opnieuw](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)
    
    Hier volgt een voorbeeld hoe toouse Hallo CLI toorebalance Hallo Storm-topologie opdracht:
    
        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

Hallo code codefragment wordt getoond hoe na een cluster tooresize synchroon of asynchroon:

    _hdiManagementClient.Clusters.Resize("<Resource Group Name>", "<Cluster Name>", <New Size>);   
    _hdiManagementClient.Clusters.ResizeAsync("<Resource Group Name>", "<Cluster Name>", <New Size>);   


## <a name="grantrevoke-access"></a>Toegang verlenen of in te trekken
HDInsight-clusters hebben Hallo HTTP-webservices (al deze services hebt RESTful eindpunten) te volgen:

* ODBC
* JDBC
* Ambari
* Oozie
* Templeton

Standaard worden deze services verleend om toegang te krijgen. U kunt in te trekken/grant Hallo toegang. toorevoke:

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = false,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);

toogrant:

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = enable,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);


> [!NOTE]
> Door het Hallo toegang verlenen/intrekken, wordt u opnieuw ingesteld Hallo cluster-gebruikersnaam en wachtwoord.
> 
> 

Dit kan ook worden gedaan via Hallo Portal. Zie [HDInsight beheren met behulp van Azure-portal Hallo][hdinsight-admin-portal].

## <a name="update-http-user-credentials"></a>HTTP-gebruikersreferenties updaten
Is Hallo dezelfde procedure als [Grant/revoke HTTP toegang](#grant/revoke-access). Als het cluster Hallo Hallo HTTP-toegang is verleend, moet u het eerst intrekken.  Vervolgens toegang verlenen en Hallo met nieuwe HTTP gebruikersgegevens.

## <a name="find-hello-default-storage-account"></a>Hallo standaardopslagaccount vinden
Hallo volgende codefragment laat zien hoe tooget Hallo naam van het standaardopslagaccount en Hallo standaard opslagaccountsleutel voor een cluster.

    var results = _hdiManagementClient.Clusters.GetClusterConfigurations(<Resource Group Name>, <Cluster Name>, "core-site");
    foreach (var key in results.Configuration.Keys)
    {
        Console.WriteLine(String.Format("{0} => {1}", key, results.Configuration[key]));
    }


## <a name="submit-jobs"></a>Verzenden van taken
**toosubmit MapReduce-taken**

Zie [uitvoeren Hadoop-MapReduce-voorbeelden in HDInsight](hdinsight-hadoop-run-samples-linux.md).

**toosubmit Hive-taken** 

Zie [uitvoeren Hive-query's met .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).

**toosubmit Pig-taken**

Zie [uitvoeren Pig-taken met .NET SDK](hdinsight-hadoop-use-pig-dotnet-sdk.md).

**toosubmit Sqoop taken**

Zie [Sqoop gebruiken met HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md).

**toosubmit Oozie taken**

Zie [Oozie gebruiken met Hadoop toodefine en voer een werkstroom in HDInsight](hdinsight-use-oozie-linux-mac.md).

## <a name="upload-data-tooazure-blob-storage"></a>Uploaden van gegevens tooAzure Blob-opslag
Zie [uploaden van gegevens tooHDInsight][hdinsight-upload-data].

## <a name="see-also"></a>Zie ook
* [HDInsight .NET SDK-documentatie](https://msdn.microsoft.com/library/mt271028.aspx)
* [HDInsight beheren met behulp van hello Azure-portal][hdinsight-admin-portal]
* [HDInsight met behulp van een opdrachtregelinterface beheren][hdinsight-admin-cli]
* [HDInsight-clusters maken][hdinsight-provision]
* [Uploaden van gegevens tooHDInsight][hdinsight-upload-data]
* [Aan de slag met Azure HDInsight][hdinsight-get-started]

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-provision-custom-options]: hdinsight-hadoop-provision-linux-clusters.md#configuration
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-admin-portal]: hdinsight-administer-use-portal-linux.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-flight]: hdinsight-analyze-flight-delay-data.md


