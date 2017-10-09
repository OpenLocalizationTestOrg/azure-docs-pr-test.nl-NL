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
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-net-sdk"></a><span data-ttu-id="df4fc-103">Hadoop-clusters in HDInsight beheren met behulp van de .NET SDK</span><span class="sxs-lookup"><span data-stu-id="df4fc-103">Manage Hadoop clusters in HDInsight by using .NET SDK</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="df4fc-104">Meer informatie over hoe toomanage HDInsight-clusters met behulp van [HDInsight.NET SDK](https://msdn.microsoft.com/library/mt271028.aspx).</span><span class="sxs-lookup"><span data-stu-id="df4fc-104">Learn how toomanage HDInsight clusters using [HDInsight.NET SDK](https://msdn.microsoft.com/library/mt271028.aspx).</span></span>

<span data-ttu-id="df4fc-105">**Vereisten**</span><span class="sxs-lookup"><span data-stu-id="df4fc-105">**Prerequisites**</span></span>

<span data-ttu-id="df4fc-106">Voordat u dit artikel, moet u de volgende Hallo hebben:</span><span class="sxs-lookup"><span data-stu-id="df4fc-106">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="df4fc-107">**Een Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="df4fc-107">**An Azure subscription**.</span></span> <span data-ttu-id="df4fc-108">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="df4fc-108">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="connect-tooazure-hdinsight"></a><span data-ttu-id="df4fc-109">Verbinding maken met tooAzure HDInsight</span><span class="sxs-lookup"><span data-stu-id="df4fc-109">Connect tooAzure HDInsight</span></span>

<span data-ttu-id="df4fc-110">U moet Hallo Nuget-pakketten te volgen:</span><span class="sxs-lookup"><span data-stu-id="df4fc-110">You need hello following Nuget packages:</span></span>

    Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
    Install-Package Microsoft.Azure.Management.ResourceManager -Pre
    Install-Package Microsoft.Azure.Management.HDInsight

<span data-ttu-id="df4fc-111">Hallo volgende codevoorbeeld ziet u hoe tooconnect tooAzure voordat u HDInsight beheren kunt-clusters onder uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="df4fc-111">hello following code sample shows you how tooconnect tooAzure before you can administer HDInsight clusters under your Azure subscription.</span></span>

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

<span data-ttu-id="df4fc-112">U wordt gevraagd wanneer dit programma wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="df4fc-112">You shall see a prompt when you run this program.</span></span>  <span data-ttu-id="df4fc-113">Als u niet toosee Hallo prompt wilt, Zie [niet-interactieve verificatie .NET HDInsight-toepassingen maken](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span><span class="sxs-lookup"><span data-stu-id="df4fc-113">If you don't want toosee hello prompt, see [Create non-interactive authentication .NET HDInsight applications](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span></span>

## <a name="create-clusters"></a><span data-ttu-id="df4fc-114">Clusters maken</span><span class="sxs-lookup"><span data-stu-id="df4fc-114">Create clusters</span></span>
<span data-ttu-id="df4fc-115">Zie [maken Linux gebaseerde clusters in HDInsight met behulp Hallo .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="df4fc-115">See [Create Linux-based clusters in HDInsight using hello .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span>

## <a name="list-clusters"></a><span data-ttu-id="df4fc-116">Lijst met clusters</span><span class="sxs-lookup"><span data-stu-id="df4fc-116">List clusters</span></span>
<span data-ttu-id="df4fc-117">Hallo bevat volgende codefragment clusters en sommige eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="df4fc-117">hello following code snippet lists clusters and some properties:</span></span>

    var results = _hdiManagementClient.Clusters.List();
    foreach (var name in results.Clusters) {
        Console.WriteLine("Cluster Name: " + name.Name);
        Console.WriteLine("\t Cluster type: " + name.Properties.ClusterDefinition.ClusterType);
        Console.WriteLine("\t Cluster location: " + name.Location);
        Console.WriteLine("\t Cluster version: " + name.Properties.ClusterVersion);
    }

## <a name="delete-clusters"></a><span data-ttu-id="df4fc-118">Clusters verwijderen</span><span class="sxs-lookup"><span data-stu-id="df4fc-118">Delete clusters</span></span>
<span data-ttu-id="df4fc-119">Gebruik Hallo volgende code codefragment toodelete een cluster synchroon of asynchroon:</span><span class="sxs-lookup"><span data-stu-id="df4fc-119">Use hello following code snippet toodelete a cluster synchronously or asynchronously:</span></span> 

    _hdiManagementClient.Clusters.Delete("<Resource Group Name>", "<Cluster Name>");
    _hdiManagementClient.Clusters.DeleteAsync("<Resource Group Name>", "<Cluster Name>");

## <a name="scale-clusters"></a><span data-ttu-id="df4fc-120">Clusters schalen</span><span class="sxs-lookup"><span data-stu-id="df4fc-120">Scale clusters</span></span>
<span data-ttu-id="df4fc-121">Hallo-cluster schalen van functie kunt u toochange Hallo aantal worker-knooppunten gebruikt door een cluster dat wordt uitgevoerd in Azure HDInsight zonder toore-Hallo cluster maken.</span><span class="sxs-lookup"><span data-stu-id="df4fc-121">hello cluster scaling feature allows you toochange hello number of worker nodes used by a cluster that is running in Azure HDInsight without having toore-create hello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="df4fc-122">Alleen clusters met HDInsight versie 3.1.3 of hoger worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="df4fc-122">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="df4fc-123">Als u niet zeker Hallo versie van het cluster weet, kunt u de eigenschappenpagina Hallo controleren.</span><span class="sxs-lookup"><span data-stu-id="df4fc-123">If you are unsure of hello version of your cluster, you can check hello Properties page.</span></span>  <span data-ttu-id="df4fc-124">Zie [lijst en geeft weer clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="df4fc-124">See [List and show clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span></span>
> 
> 

<span data-ttu-id="df4fc-125">Hallo gevolgen van het aantal gegevensknooppunten voor elk type ondersteund door HDInsight cluster Hallo wijzigen:</span><span class="sxs-lookup"><span data-stu-id="df4fc-125">hello impact of changing hello number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="df4fc-126">Hadoop</span><span class="sxs-lookup"><span data-stu-id="df4fc-126">Hadoop</span></span>
  
    <span data-ttu-id="df4fc-127">Hallo aantal worker-knooppunten van een Hadoop-cluster dat wordt uitgevoerd zonder enige impact op alle taken die in behandeling of wordt uitgevoerd, kunt u naadloos verhogen.</span><span class="sxs-lookup"><span data-stu-id="df4fc-127">You can seamlessly increase hello number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="df4fc-128">Nieuwe taken kunnen ook worden verzonden tijdens het Hallo-bewerking wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="df4fc-128">New jobs can also be submitted while hello operation is in progress.</span></span> <span data-ttu-id="df4fc-129">Fouten in een bewerking voor schaal worden probleemloos verwerkt zodat hello cluster altijd functioneel is overblijft.</span><span class="sxs-lookup"><span data-stu-id="df4fc-129">Failures in a scaling operation are gracefully handled so that hello cluster is always left in a functional state.</span></span>
  
    <span data-ttu-id="df4fc-130">Wanneer een Hadoop-cluster wordt verkleind door het aantal gegevensknooppunten hello te verminderen, worden sommige services in de cluster Hallo Hallo opnieuw gestart.</span><span class="sxs-lookup"><span data-stu-id="df4fc-130">When a Hadoop cluster is scaled down by reducing hello number of data nodes, some of hello services in hello cluster are restarted.</span></span> <span data-ttu-id="df4fc-131">Dit zorgt ervoor dat alle actieve en in behandeling zijnde taken toofail op Hallo Hallo schalen van de bewerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="df4fc-131">This causes all running and pending jobs toofail at hello completion of hello scaling operation.</span></span> <span data-ttu-id="df4fc-132">U kunt echter Hallo taken verzenden zodra Hallo-bewerking voltooid is.</span><span class="sxs-lookup"><span data-stu-id="df4fc-132">You can, however, resubmit hello jobs once hello operation is complete.</span></span>
* <span data-ttu-id="df4fc-133">HBase</span><span class="sxs-lookup"><span data-stu-id="df4fc-133">HBase</span></span>
  
    <span data-ttu-id="df4fc-134">U kunt naadloos toevoegen of verwijderen van knooppunten tooyour HBase-cluster, terwijl deze wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="df4fc-134">You can seamlessly add or remove nodes tooyour HBase cluster while it is running.</span></span> <span data-ttu-id="df4fc-135">Regionale Servers worden automatisch verdeeld binnen een paar minuten na voltooiing van Hallo bewerking schalen.</span><span class="sxs-lookup"><span data-stu-id="df4fc-135">Regional Servers are automatically balanced within a few minutes of completing hello scaling operation.</span></span> <span data-ttu-id="df4fc-136">U kunt echter ook handmatig Hallo regionale servers verdelen door logboekregistratie in Hallo headnode van het cluster en actieve Hallo volgende opdrachten uit een opdrachtpromptvenster:</span><span class="sxs-lookup"><span data-stu-id="df4fc-136">However, you can also manually balance hello regional servers by logging into hello headnode of cluster and running hello following commands from a command prompt window:</span></span>
  
        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* <span data-ttu-id="df4fc-137">Storm</span><span class="sxs-lookup"><span data-stu-id="df4fc-137">Storm</span></span>
  
    <span data-ttu-id="df4fc-138">U kunt naadloos toevoegen of verwijderen van gegevens knooppunten tooyour Storm-cluster, terwijl deze wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="df4fc-138">You can seamlessly add or remove data nodes tooyour Storm cluster while it is running.</span></span> <span data-ttu-id="df4fc-139">Maar nadat de bewerking schalen Hallo installatie is voltooid, moet u toorebalance Hallo topologie.</span><span class="sxs-lookup"><span data-stu-id="df4fc-139">But after a successful completion of hello scaling operation, you will need toorebalance hello topology.</span></span>
  
    <span data-ttu-id="df4fc-140">Herverdeling kan worden uitgevoerd op twee manieren:</span><span class="sxs-lookup"><span data-stu-id="df4fc-140">Rebalancing can be accomplished in two ways:</span></span>
  
  * <span data-ttu-id="df4fc-141">Storm-webgebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="df4fc-141">Storm web UI</span></span>
  * <span data-ttu-id="df4fc-142">Hulpprogramma voor opdrachtregelinterface (CLI)</span><span class="sxs-lookup"><span data-stu-id="df4fc-142">Command-line interface (CLI) tool</span></span>
    
    <span data-ttu-id="df4fc-143">Raadpleeg toohello [Apache Storm documentatie](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="df4fc-143">Please refer toohello [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>
    
    <span data-ttu-id="df4fc-144">Hallo Storm-webgebruikersinterface is beschikbaar op Hallo HDInsight-cluster:</span><span class="sxs-lookup"><span data-stu-id="df4fc-144">hello Storm web UI is available on hello HDInsight cluster:</span></span>
    
    ![HDInsight Storm scale deel opnieuw](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)
    
    <span data-ttu-id="df4fc-146">Hier volgt een voorbeeld hoe toouse Hallo CLI toorebalance Hallo Storm-topologie opdracht:</span><span class="sxs-lookup"><span data-stu-id="df4fc-146">Here is an example how toouse hello CLI command toorebalance hello Storm topology:</span></span>
    
        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="df4fc-147">Hallo code codefragment wordt getoond hoe na een cluster tooresize synchroon of asynchroon:</span><span class="sxs-lookup"><span data-stu-id="df4fc-147">hello following code snippet shows how tooresize a cluster synchronously or asynchronously:</span></span>

    _hdiManagementClient.Clusters.Resize("<Resource Group Name>", "<Cluster Name>", <New Size>);   
    _hdiManagementClient.Clusters.ResizeAsync("<Resource Group Name>", "<Cluster Name>", <New Size>);   


## <a name="grantrevoke-access"></a><span data-ttu-id="df4fc-148">Toegang verlenen of in te trekken</span><span class="sxs-lookup"><span data-stu-id="df4fc-148">Grant/revoke access</span></span>
<span data-ttu-id="df4fc-149">HDInsight-clusters hebben Hallo HTTP-webservices (al deze services hebt RESTful eindpunten) te volgen:</span><span class="sxs-lookup"><span data-stu-id="df4fc-149">HDInsight clusters have hello following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="df4fc-150">ODBC</span><span class="sxs-lookup"><span data-stu-id="df4fc-150">ODBC</span></span>
* <span data-ttu-id="df4fc-151">JDBC</span><span class="sxs-lookup"><span data-stu-id="df4fc-151">JDBC</span></span>
* <span data-ttu-id="df4fc-152">Ambari</span><span class="sxs-lookup"><span data-stu-id="df4fc-152">Ambari</span></span>
* <span data-ttu-id="df4fc-153">Oozie</span><span class="sxs-lookup"><span data-stu-id="df4fc-153">Oozie</span></span>
* <span data-ttu-id="df4fc-154">Templeton</span><span class="sxs-lookup"><span data-stu-id="df4fc-154">Templeton</span></span>

<span data-ttu-id="df4fc-155">Standaard worden deze services verleend om toegang te krijgen.</span><span class="sxs-lookup"><span data-stu-id="df4fc-155">By default, these services are granted for access.</span></span> <span data-ttu-id="df4fc-156">U kunt in te trekken/grant Hallo toegang.</span><span class="sxs-lookup"><span data-stu-id="df4fc-156">You can revoke/grant hello access.</span></span> <span data-ttu-id="df4fc-157">toorevoke:</span><span class="sxs-lookup"><span data-stu-id="df4fc-157">toorevoke:</span></span>

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = false,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);

<span data-ttu-id="df4fc-158">toogrant:</span><span class="sxs-lookup"><span data-stu-id="df4fc-158">toogrant:</span></span>

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = enable,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);


> [!NOTE]
> <span data-ttu-id="df4fc-159">Door het Hallo toegang verlenen/intrekken, wordt u opnieuw ingesteld Hallo cluster-gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="df4fc-159">By granting/revoking hello access, you will reset hello cluster user name and password.</span></span>
> 
> 

<span data-ttu-id="df4fc-160">Dit kan ook worden gedaan via Hallo Portal.</span><span class="sxs-lookup"><span data-stu-id="df4fc-160">This can also be done via hello Portal.</span></span> <span data-ttu-id="df4fc-161">Zie [HDInsight beheren met behulp van Azure-portal Hallo][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="df4fc-161">See [Administer HDInsight by using hello Azure portal][hdinsight-admin-portal].</span></span>

## <a name="update-http-user-credentials"></a><span data-ttu-id="df4fc-162">HTTP-gebruikersreferenties updaten</span><span class="sxs-lookup"><span data-stu-id="df4fc-162">Update HTTP user credentials</span></span>
<span data-ttu-id="df4fc-163">Is Hallo dezelfde procedure als [Grant/revoke HTTP toegang](#grant/revoke-access). Als het cluster Hallo Hallo HTTP-toegang is verleend, moet u het eerst intrekken.</span><span class="sxs-lookup"><span data-stu-id="df4fc-163">It is hello same procedure as [Grant/revoke HTTP access](#grant/revoke-access).If hello cluster has been granted hello HTTP access, you must first revoke it.</span></span>  <span data-ttu-id="df4fc-164">Vervolgens toegang verlenen en Hallo met nieuwe HTTP gebruikersgegevens.</span><span class="sxs-lookup"><span data-stu-id="df4fc-164">And then grant hello access with new HTTP user credentials.</span></span>

## <a name="find-hello-default-storage-account"></a><span data-ttu-id="df4fc-165">Hallo standaardopslagaccount vinden</span><span class="sxs-lookup"><span data-stu-id="df4fc-165">Find hello default storage account</span></span>
<span data-ttu-id="df4fc-166">Hallo volgende codefragment laat zien hoe tooget Hallo naam van het standaardopslagaccount en Hallo standaard opslagaccountsleutel voor een cluster.</span><span class="sxs-lookup"><span data-stu-id="df4fc-166">hello following code snippet demonstrates how tooget hello default storage account name and hello default storage account key for a cluster.</span></span>

    var results = _hdiManagementClient.Clusters.GetClusterConfigurations(<Resource Group Name>, <Cluster Name>, "core-site");
    foreach (var key in results.Configuration.Keys)
    {
        Console.WriteLine(String.Format("{0} => {1}", key, results.Configuration[key]));
    }


## <a name="submit-jobs"></a><span data-ttu-id="df4fc-167">Verzenden van taken</span><span class="sxs-lookup"><span data-stu-id="df4fc-167">Submit jobs</span></span>
<span data-ttu-id="df4fc-168">**toosubmit MapReduce-taken**</span><span class="sxs-lookup"><span data-stu-id="df4fc-168">**toosubmit MapReduce jobs**</span></span>

<span data-ttu-id="df4fc-169">Zie [uitvoeren Hadoop-MapReduce-voorbeelden in HDInsight](hdinsight-hadoop-run-samples-linux.md).</span><span class="sxs-lookup"><span data-stu-id="df4fc-169">See [Run Hadoop MapReduce samples in HDInsight](hdinsight-hadoop-run-samples-linux.md).</span></span>

<span data-ttu-id="df4fc-170">**toosubmit Hive-taken**</span><span class="sxs-lookup"><span data-stu-id="df4fc-170">**toosubmit Hive jobs**</span></span> 

<span data-ttu-id="df4fc-171">Zie [uitvoeren Hive-query's met .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="df4fc-171">See [Run Hive queries using .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span>

<span data-ttu-id="df4fc-172">**toosubmit Pig-taken**</span><span class="sxs-lookup"><span data-stu-id="df4fc-172">**toosubmit Pig jobs**</span></span>

<span data-ttu-id="df4fc-173">Zie [uitvoeren Pig-taken met .NET SDK](hdinsight-hadoop-use-pig-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="df4fc-173">See [Run Pig jobs using .NET SDK](hdinsight-hadoop-use-pig-dotnet-sdk.md).</span></span>

<span data-ttu-id="df4fc-174">**toosubmit Sqoop taken**</span><span class="sxs-lookup"><span data-stu-id="df4fc-174">**toosubmit Sqoop jobs**</span></span>

<span data-ttu-id="df4fc-175">Zie [Sqoop gebruiken met HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="df4fc-175">See [Use Sqoop with HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md).</span></span>

<span data-ttu-id="df4fc-176">**toosubmit Oozie taken**</span><span class="sxs-lookup"><span data-stu-id="df4fc-176">**toosubmit Oozie jobs**</span></span>

<span data-ttu-id="df4fc-177">Zie [Oozie gebruiken met Hadoop toodefine en voer een werkstroom in HDInsight](hdinsight-use-oozie-linux-mac.md).</span><span class="sxs-lookup"><span data-stu-id="df4fc-177">See [Use Oozie with Hadoop toodefine and run a workflow in HDInsight](hdinsight-use-oozie-linux-mac.md).</span></span>

## <a name="upload-data-tooazure-blob-storage"></a><span data-ttu-id="df4fc-178">Uploaden van gegevens tooAzure Blob-opslag</span><span class="sxs-lookup"><span data-stu-id="df4fc-178">Upload data tooAzure Blob storage</span></span>
<span data-ttu-id="df4fc-179">Zie [uploaden van gegevens tooHDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="df4fc-179">See [Upload data tooHDInsight][hdinsight-upload-data].</span></span>

## <a name="see-also"></a><span data-ttu-id="df4fc-180">Zie ook</span><span class="sxs-lookup"><span data-stu-id="df4fc-180">See Also</span></span>
* [<span data-ttu-id="df4fc-181">HDInsight .NET SDK-documentatie</span><span class="sxs-lookup"><span data-stu-id="df4fc-181">HDInsight .NET SDK reference documentation</span></span>](https://msdn.microsoft.com/library/mt271028.aspx)
* <span data-ttu-id="df4fc-182">[HDInsight beheren met behulp van hello Azure-portal][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="df4fc-182">[Administer HDInsight by using hello Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="df4fc-183">[HDInsight met behulp van een opdrachtregelinterface beheren][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="df4fc-183">[Administer HDInsight using a command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="df4fc-184">[HDInsight-clusters maken][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="df4fc-184">[Create HDInsight clusters][hdinsight-provision]</span></span>
* <span data-ttu-id="df4fc-185">[Uploaden van gegevens tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="df4fc-185">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="df4fc-186">[Aan de slag met Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="df4fc-186">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>

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


