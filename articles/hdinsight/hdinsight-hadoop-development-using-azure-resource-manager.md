---
title: aaaMigrate tooAzure Resource Manager hulpprogramma's voor HDInsight | Microsoft Docs
description: Hoe toomigrate tooAzure Resource Manager development tools voor HDInsight-clusters
services: hdinsight
editor: cgronlun
manager: jhubbard
author: nitinme
documentationcenter: 
ms.assetid: 05efedb5-6456-4552-87ff-156d77fbe2e1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: c087ae63d2544e5badae6be9c258f783aa92e2ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-tooazure-resource-manager-based-development-tools-for-hdinsight-clusters"></a><span data-ttu-id="2d971-103">Migreren tooAzure ontwikkelen op basis van een Resource Manager-hulpprogramma's voor HDInsight-clusters</span><span class="sxs-lookup"><span data-stu-id="2d971-103">Migrating tooAzure Resource Manager-based development tools for HDInsight clusters</span></span>

<span data-ttu-id="2d971-104">HDInsight is het van Azure Service Manager ASM-hulpprogramma's voor HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2d971-104">HDInsight is deprecating Azure Service Manager (ASM)-based tools for HDInsight.</span></span> <span data-ttu-id="2d971-105">Als u hebt gebruikt Azure PowerShell of Azure CLI Hallo HDInsight .NET SDK toowork met HDInsight-clusters, bent u ten zeerste toouse hello Azure Resource Manager ARM gebaseerde versies van PowerShell, CLI en .NET SDK voortaan.</span><span class="sxs-lookup"><span data-stu-id="2d971-105">If you have been using Azure PowerShell, Azure CLI, or hello HDInsight .NET SDK toowork with HDInsight clusters, you are encouraged toouse hello Azure Resource Manager (ARM)-based versions of PowerShell, CLI, and .NET SDK going forward.</span></span> <span data-ttu-id="2d971-106">In dit artikel bevat verwijzingen over het toomigrate toohello nieuwe op basis van ARM benadering.</span><span class="sxs-lookup"><span data-stu-id="2d971-106">This article provides pointers on how toomigrate toohello new ARM-based approach.</span></span> <span data-ttu-id="2d971-107">Waar van toepassing, wijst dit artikel ook op Hallo verschillen tussen Hallo ASM- en ARM benaderingen voor HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2d971-107">Wherever applicable, this article also points out hello differences between hello ASM and ARM approaches for HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2d971-108">Hallo-ondersteuning voor ASM op basis van PowerShell, CLI en .NET SDK af te breken op **1 januari 2017**.</span><span class="sxs-lookup"><span data-stu-id="2d971-108">hello support for ASM based PowerShell, CLI, and .NET SDK will discontinue on **January 1, 2017**.</span></span>
> 
> 

## <a name="migrating-azure-cli-tooazure-resource-manager"></a><span data-ttu-id="2d971-109">Migreren Azure CLI tooAzure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2d971-109">Migrating Azure CLI tooAzure Resource Manager</span></span>
<span data-ttu-id="2d971-110">Hello Azure CLI standaardwaarden-modus Resource Manager (ARM) tooAzure nu tenzij u een upgrade van een vorige installatie uitvoert; in dit geval wordt u wellicht toouse hello `azure config mode arm` opdracht tooswitch tooARM modus.</span><span class="sxs-lookup"><span data-stu-id="2d971-110">hello Azure CLI now defaults tooAzure Resource Manager (ARM) mode, unless you are upgrading from a previous installation; in this case, you may need toouse hello `azure config mode arm` command tooswitch tooARM mode.</span></span>

<span data-ttu-id="2d971-111">Hallo-basisopdrachten die hello Azure CLI toowork voorzien in HDInsight met behulp van Azure Service Management (ASM) zijn Hallo dezelfde bij gebruik van ARM; Sommige parameters en schakelopties mogelijk wel nieuwe namen en er zijn veel nieuwe parameters beschikbaar wanneer u de ARM.</span><span class="sxs-lookup"><span data-stu-id="2d971-111">hello basic commands that hello Azure CLI provided toowork with HDInsight using Azure Service Management (ASM) are hello same when using ARM; however some parameters and switches may have new names, and there are many new parameters available when using ARM.</span></span> <span data-ttu-id="2d971-112">Bijvoorbeeld, u kunt nu gebruiken `azure hdinsight cluster create` toospecify hello Azure Virtual Network die moet worden gemaakt in een cluster of Hive en Oozie-metastore informatie.</span><span class="sxs-lookup"><span data-stu-id="2d971-112">For example, you can now use `azure hdinsight cluster create` toospecify hello Azure Virtual Network that a cluster should be created in, or Hive and Oozie metastore information.</span></span>

<span data-ttu-id="2d971-113">Basic-opdrachten voor het werken met HDInsight via Azure Resource Manager zijn:</span><span class="sxs-lookup"><span data-stu-id="2d971-113">Basic commands for working with HDInsight through Azure Resource Manager are:</span></span>

* <span data-ttu-id="2d971-114">`azure hdinsight cluster create`-maakt een nieuwe HDInsight-cluster</span><span class="sxs-lookup"><span data-stu-id="2d971-114">`azure hdinsight cluster create` - creates a new HDInsight cluster</span></span>
* <span data-ttu-id="2d971-115">`azure hdinsight cluster delete`-een bestaand HDInsight-cluster worden verwijderd</span><span class="sxs-lookup"><span data-stu-id="2d971-115">`azure hdinsight cluster delete` - deletes an existing HDInsight cluster</span></span>
* <span data-ttu-id="2d971-116">`azure hdinsight cluster show`-informatie weer over een bestaand cluster</span><span class="sxs-lookup"><span data-stu-id="2d971-116">`azure hdinsight cluster show` - display information about an existing cluster</span></span>
* <span data-ttu-id="2d971-117">`azure hdinsight cluster list`-een lijst met HDInsight-clusters voor uw Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="2d971-117">`azure hdinsight cluster list` - lists HDInsight clusters for your Azure subscription</span></span>

<span data-ttu-id="2d971-118">Gebruik Hallo `-h` overschakelen tooinspect Hallo parameters en switches beschikbaar zijn voor elke opdracht.</span><span class="sxs-lookup"><span data-stu-id="2d971-118">Use hello `-h` switch tooinspect hello parameters and switches available for each command.</span></span>

### <a name="new-commands"></a><span data-ttu-id="2d971-119">Nieuwe opdrachten</span><span class="sxs-lookup"><span data-stu-id="2d971-119">New commands</span></span>
<span data-ttu-id="2d971-120">Nieuwe opdrachten die beschikbaar zijn met Azure Resource Manager zijn:</span><span class="sxs-lookup"><span data-stu-id="2d971-120">New commands available with Azure Resource Manager are:</span></span>

* <span data-ttu-id="2d971-121">`azure hdinsight cluster resize`-dynamisch wijzigingen aantal worker-knooppunten in cluster Hallo Hallo</span><span class="sxs-lookup"><span data-stu-id="2d971-121">`azure hdinsight cluster resize` - dynamically changes hello number of worker nodes in hello cluster</span></span>
* <span data-ttu-id="2d971-122">`azure hdinsight cluster enable-http-access`-HTTPs-cluster-toegang toohello kunt (op standaard)</span><span class="sxs-lookup"><span data-stu-id="2d971-122">`azure hdinsight cluster enable-http-access` - enables HTTPs access toohello cluster (on by default)</span></span>
* <span data-ttu-id="2d971-123">`azure hdinsight cluster disable-http-access`-HTTPs-cluster-toegang toohello uitgeschakeld</span><span class="sxs-lookup"><span data-stu-id="2d971-123">`azure hdinsight cluster disable-http-access` - disables HTTPs access toohello cluster</span></span>
* <span data-ttu-id="2d971-124">`azure hdinsight script-action`-bevat opdrachten voor het maken/beheren scriptacties op een cluster</span><span class="sxs-lookup"><span data-stu-id="2d971-124">`azure hdinsight script-action` - provides commands for creating/managing Script Actions on a cluster</span></span>
* <span data-ttu-id="2d971-125">`azure hdinsight config`-bevat opdrachten voor het maken van een configuratiebestand dat kan worden gebruikt met Hallo `hdinsight cluster create` opdracht tooprovide configuratie-informatie.</span><span class="sxs-lookup"><span data-stu-id="2d971-125">`azure hdinsight config` - provides commands for creating a configuration file that can be used with hello `hdinsight cluster create` command tooprovide configuration information.</span></span>

### <a name="deprecated-commands"></a><span data-ttu-id="2d971-126">Afgeschafte opdrachten</span><span class="sxs-lookup"><span data-stu-id="2d971-126">Deprecated commands</span></span>
<span data-ttu-id="2d971-127">Als u Hallo `azure hdinsight job` opdrachten toosubmit taken tooyour HDInsight-cluster deze niet beschikbaar zijn via Hallo ARM-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="2d971-127">If you use hello `azure hdinsight job` commands toosubmit jobs tooyour HDInsight cluster, these are not available through hello ARM commands.</span></span> <span data-ttu-id="2d971-128">Als u tooprogrammatically indienen taken tooHDInsight van scripts moet, moet u in plaats daarvan Hallo geleverd door HDInsight REST-API's.</span><span class="sxs-lookup"><span data-stu-id="2d971-128">If you need tooprogrammatically submit jobs tooHDInsight from scripts, you should instead use hello REST APIs provided by HDInsight.</span></span> <span data-ttu-id="2d971-129">Zie voor meer informatie over het verzenden van taken met REST API's Hallo documenten te volgen.</span><span class="sxs-lookup"><span data-stu-id="2d971-129">For more information on submitting jobs using REST APIs, see hello following documents.</span></span>

* [<span data-ttu-id="2d971-130">MapReduce-taken uitvoeren met Hadoop in HDInsight met cURL</span><span class="sxs-lookup"><span data-stu-id="2d971-130">Run MapReduce jobs with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-mapreduce-curl.md)
* [<span data-ttu-id="2d971-131">Hive-query's uitvoeren met Hadoop in HDInsight met cURL</span><span class="sxs-lookup"><span data-stu-id="2d971-131">Run Hive queries with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-hive-curl.md)
* [<span data-ttu-id="2d971-132">Pig-taken uitvoeren met Hadoop in HDInsight met cURL</span><span class="sxs-lookup"><span data-stu-id="2d971-132">Run Pig jobs with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-pig-curl.md)

<span data-ttu-id="2d971-133">Voor informatie over andere manieren toorun MapReduce, Hive, en interactief varkens, Zie [MapReduce gebruiken met Hadoop op HDInsight](hdinsight-use-mapreduce.md), [Hive gebruiken met Hadoop op HDInsight](hdinsight-use-hive.md), en [Pig gebruiken met Hadoop op HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="2d971-133">For information on other ways toorun MapReduce, Hive, and Pig interactively, see [Use MapReduce with Hadoop on HDInsight](hdinsight-use-mapreduce.md), [Use Hive with Hadoop on HDInsight](hdinsight-use-hive.md), and [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

### <a name="examples"></a><span data-ttu-id="2d971-134">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="2d971-134">Examples</span></span>
<span data-ttu-id="2d971-135">**Maken van een cluster**</span><span class="sxs-lookup"><span data-stu-id="2d971-135">**Creating a cluster**</span></span>

* <span data-ttu-id="2d971-136">Vorige opdracht (ASM)-`azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`</span><span class="sxs-lookup"><span data-stu-id="2d971-136">Old command (ASM) - `azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`</span></span>
* <span data-ttu-id="2d971-137">Nieuwe opdracht (ARM)-`azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`</span><span class="sxs-lookup"><span data-stu-id="2d971-137">New command (ARM) - `azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`</span></span>

<span data-ttu-id="2d971-138">**Verwijderen van een cluster**</span><span class="sxs-lookup"><span data-stu-id="2d971-138">**Deleting a cluster**</span></span>

* <span data-ttu-id="2d971-139">Vorige opdracht (ASM)-`azure hdinsight cluster delete myhdicluster`</span><span class="sxs-lookup"><span data-stu-id="2d971-139">Old command (ASM) - `azure hdinsight cluster delete myhdicluster`</span></span>
* <span data-ttu-id="2d971-140">Nieuwe opdracht (ARM)-`azure hdinsight cluster delete mycluster -g myresourcegroup`</span><span class="sxs-lookup"><span data-stu-id="2d971-140">New command (ARM) - `azure hdinsight cluster delete mycluster -g myresourcegroup`</span></span>

<span data-ttu-id="2d971-141">**Lijst met clusters**</span><span class="sxs-lookup"><span data-stu-id="2d971-141">**List clusters**</span></span>

* <span data-ttu-id="2d971-142">Vorige opdracht (ASM)-`azure hdinsight cluster list`</span><span class="sxs-lookup"><span data-stu-id="2d971-142">Old command (ASM) - `azure hdinsight cluster list`</span></span>
* <span data-ttu-id="2d971-143">Nieuwe opdracht (ARM)-`azure hdinsight cluster list`</span><span class="sxs-lookup"><span data-stu-id="2d971-143">New command (ARM) - `azure hdinsight cluster list`</span></span>

> [!NOTE]
> <span data-ttu-id="2d971-144">Hallo lijst opdracht geven Hallo resource groep met `-g` Hallo-clusters in de opgegeven resourcegroep hello wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="2d971-144">For hello list command, specifying hello resource group using `-g` will return only hello clusters in hello specified resource group.</span></span>
> 
> 

<span data-ttu-id="2d971-145">**Cluster-informatie weergeven**</span><span class="sxs-lookup"><span data-stu-id="2d971-145">**Show cluster information**</span></span>

* <span data-ttu-id="2d971-146">Vorige opdracht (ASM)-`azure hdinsight cluster show myhdicluster`</span><span class="sxs-lookup"><span data-stu-id="2d971-146">Old command (ASM) - `azure hdinsight cluster show myhdicluster`</span></span>
* <span data-ttu-id="2d971-147">Nieuwe opdracht (ARM)-`azure hdinsight cluster show myhdicluster -g myresourcegroup`</span><span class="sxs-lookup"><span data-stu-id="2d971-147">New command (ARM) - `azure hdinsight cluster show myhdicluster -g myresourcegroup`</span></span>

## <a name="migrating-azure-powershell-tooazure-resource-manager"></a><span data-ttu-id="2d971-148">Migreren Azure PowerShell tooAzure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2d971-148">Migrating Azure PowerShell tooAzure Resource Manager</span></span>
<span data-ttu-id="2d971-149">Hallo algemene informatie over Azure PowerShell in de modus Azure Resource Manager (ARM) Hallo kan worden gevonden op [Azure PowerShell gebruiken met Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="2d971-149">hello general information about Azure PowerShell in hello Azure Resource Manager (ARM) mode can be found at [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="2d971-150">Hallo ARM van Azure PowerShell-cmdlets kan worden geïnstalleerd side-by-side Hello ASM-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="2d971-150">hello Azure PowerShell ARM cmdlets can be installed side-by-side with hello ASM cmdlets.</span></span> <span data-ttu-id="2d971-151">Hallo-cmdlets uit twee modi Hallo kunnen worden onderscheiden door hun namen.</span><span class="sxs-lookup"><span data-stu-id="2d971-151">hello cmdlets from hello two modes can be distinguished by their names.</span></span>  <span data-ttu-id="2d971-152">Hallo ARM-modus is *AzureRmHDInsight* Hallo cmdlet namen te vergelijken*AzureHDInsight* in Hallo ASM-modus.</span><span class="sxs-lookup"><span data-stu-id="2d971-152">hello ARM mode has *AzureRmHDInsight* in hello cmdlet names comparing too*AzureHDInsight* in hello ASM mode.</span></span>  <span data-ttu-id="2d971-153">Bijvoorbeeld: *nieuw AzureRmHDInsightCluster* vs. *Nieuwe AzureHDInsightCluster*.</span><span class="sxs-lookup"><span data-stu-id="2d971-153">For example, *New-AzureRmHDInsightCluster* vs. *New-AzureHDInsightCluster*.</span></span> <span data-ttu-id="2d971-154">Parameters en switches wellicht nieuws namen en er zijn veel nieuwe parameters beschikbaar wanneer u ARM.</span><span class="sxs-lookup"><span data-stu-id="2d971-154">Parameters and switches may have news names, and there are many new parameters available when using ARM.</span></span>  <span data-ttu-id="2d971-155">Meerdere cmdlets vereisen bijvoorbeeld dat een nieuwe switch aangeroepen *- ResourceGroupName*.</span><span class="sxs-lookup"><span data-stu-id="2d971-155">For example, several cmdlets require a new switch called *-ResourceGroupName*.</span></span> 

<span data-ttu-id="2d971-156">Voordat u Hallo HDInsight-cmdlets gebruiken kunt, moet u verbinding tooyour Azure-account en een nieuwe resourcegroep maken:</span><span class="sxs-lookup"><span data-stu-id="2d971-156">Before you can use hello HDInsight cmdlets, you must connect tooyour Azure account, and create a new resource group:</span></span>

* <span data-ttu-id="2d971-157">Login-AzureRmAccount of [Selecteer AzureRmProfile](https://msdn.microsoft.com/library/mt619310.aspx).</span><span class="sxs-lookup"><span data-stu-id="2d971-157">Login-AzureRmAccount or [Select-AzureRmProfile](https://msdn.microsoft.com/library/mt619310.aspx).</span></span> <span data-ttu-id="2d971-158">Zie [verifiëren van een service-principal met Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md)</span><span class="sxs-lookup"><span data-stu-id="2d971-158">See [Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md)</span></span>
* [<span data-ttu-id="2d971-159">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2d971-159">New-AzureRmResourceGroup</span></span>](https://msdn.microsoft.com/library/mt603739.aspx)

### <a name="renamed-cmdlets"></a><span data-ttu-id="2d971-160">Nieuwe naam cmdlets</span><span class="sxs-lookup"><span data-stu-id="2d971-160">Renamed cmdlets</span></span>
<span data-ttu-id="2d971-161">toolist hello HDInsight ASM-cmdlets in Windows PowerShell-console:</span><span class="sxs-lookup"><span data-stu-id="2d971-161">toolist hello HDInsight ASM cmdlets in Windows PowerShell console:</span></span>

    help *azurermhdinsight*

<span data-ttu-id="2d971-162">Hallo volgende tabel bevat Hallo ASM-cmdlets en hun namen in Hallo ARM-modus:</span><span class="sxs-lookup"><span data-stu-id="2d971-162">hello following table lists hello ASM cmdlets and their names in hello ARM mode:</span></span>

| <span data-ttu-id="2d971-163">ASM-cmdlets</span><span class="sxs-lookup"><span data-stu-id="2d971-163">ASM cmdlets</span></span> | <span data-ttu-id="2d971-164">ARM-cmdlets</span><span class="sxs-lookup"><span data-stu-id="2d971-164">ARM cmdlets</span></span> |
| --- | --- |
| <span data-ttu-id="2d971-165">Add-AzureHDInsightConfigValues</span><span class="sxs-lookup"><span data-stu-id="2d971-165">Add-AzureHDInsightConfigValues</span></span> |[<span data-ttu-id="2d971-166">Voeg AzureRmHDInsightConfigValues</span><span class="sxs-lookup"><span data-stu-id="2d971-166">Add-AzureRmHDInsightConfigValues</span></span>](https://msdn.microsoft.com/library/mt603530.aspx) |
| <span data-ttu-id="2d971-167">Add-AzureHDInsightMetastore</span><span class="sxs-lookup"><span data-stu-id="2d971-167">Add-AzureHDInsightMetastore</span></span> |[<span data-ttu-id="2d971-168">Voeg AzureRmHDInsightMetastore</span><span class="sxs-lookup"><span data-stu-id="2d971-168">Add-AzureRmHDInsightMetastore</span></span>](https://msdn.microsoft.com/library/mt603670.aspx) |
| <span data-ttu-id="2d971-169">Add-AzureHDInsightScriptAction</span><span class="sxs-lookup"><span data-stu-id="2d971-169">Add-AzureHDInsightScriptAction</span></span> |[<span data-ttu-id="2d971-170">Voeg AzureRmHDInsightScriptAction</span><span class="sxs-lookup"><span data-stu-id="2d971-170">Add-AzureRmHDInsightScriptAction</span></span>](https://msdn.microsoft.com/library/mt603527.aspx) |
| <span data-ttu-id="2d971-171">Add-AzureHDInsightStorage</span><span class="sxs-lookup"><span data-stu-id="2d971-171">Add-AzureHDInsightStorage</span></span> |[<span data-ttu-id="2d971-172">Voeg AzureRmHDInsightStorage</span><span class="sxs-lookup"><span data-stu-id="2d971-172">Add-AzureRmHDInsightStorage</span></span>](https://msdn.microsoft.com/library/mt619445.aspx) |
| <span data-ttu-id="2d971-173">Get-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="2d971-173">Get-AzureHDInsightCluster</span></span> |[<span data-ttu-id="2d971-174">Get-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="2d971-174">Get-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619371.aspx) |
| <span data-ttu-id="2d971-175">Get-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="2d971-175">Get-AzureHDInsightJob</span></span> |[<span data-ttu-id="2d971-176">Get-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="2d971-176">Get-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603590.aspx) |
| <span data-ttu-id="2d971-177">Get-AzureHDInsightJobOutput</span><span class="sxs-lookup"><span data-stu-id="2d971-177">Get-AzureHDInsightJobOutput</span></span> |[<span data-ttu-id="2d971-178">Get-AzureRmHDInsightJobOutput</span><span class="sxs-lookup"><span data-stu-id="2d971-178">Get-AzureRmHDInsightJobOutput</span></span>](https://msdn.microsoft.com/library/mt603793.aspx) |
| <span data-ttu-id="2d971-179">Get-AzureHDInsightProperties</span><span class="sxs-lookup"><span data-stu-id="2d971-179">Get-AzureHDInsightProperties</span></span> |[<span data-ttu-id="2d971-180">Get-AzureRmHDInsightProperties</span><span class="sxs-lookup"><span data-stu-id="2d971-180">Get-AzureRmHDInsightProperties</span></span>](https://msdn.microsoft.com/library/mt603546.aspx) |
| <span data-ttu-id="2d971-181">Grant-AzureHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="2d971-181">Grant-AzureHDInsightHttpServicesAccess</span></span> |[<span data-ttu-id="2d971-182">Verleen AzureRmHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="2d971-182">Grant-AzureRmHDInsightHttpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt619407.aspx) |
| <span data-ttu-id="2d971-183">Grant-AzureHdinsightRdpAccess</span><span class="sxs-lookup"><span data-stu-id="2d971-183">Grant-AzureHdinsightRdpAccess</span></span> |[<span data-ttu-id="2d971-184">Verleen AzureRmHDInsightRdpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="2d971-184">Grant-AzureRmHDInsightRdpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt603717.aspx) |
| <span data-ttu-id="2d971-185">Invoke-AzureHDInsightHiveJob</span><span class="sxs-lookup"><span data-stu-id="2d971-185">Invoke-AzureHDInsightHiveJob</span></span> |[<span data-ttu-id="2d971-186">Aanroepen AzureRmHDInsightHiveJob</span><span class="sxs-lookup"><span data-stu-id="2d971-186">Invoke-AzureRmHDInsightHiveJob</span></span>](https://msdn.microsoft.com/library/mt603593.aspx) |
| <span data-ttu-id="2d971-187">New-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="2d971-187">New-AzureHDInsightCluster</span></span> |[<span data-ttu-id="2d971-188">Nieuwe AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="2d971-188">New-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619331.aspx) |
| <span data-ttu-id="2d971-189">New-AzureHDInsightClusterConfig</span><span class="sxs-lookup"><span data-stu-id="2d971-189">New-AzureHDInsightClusterConfig</span></span> |[<span data-ttu-id="2d971-190">Nieuwe AzureRmHDInsightClusterConfig</span><span class="sxs-lookup"><span data-stu-id="2d971-190">New-AzureRmHDInsightClusterConfig</span></span>](https://msdn.microsoft.com/library/mt603700.aspx) |
| <span data-ttu-id="2d971-191">New-AzureHDInsightHiveJobDefinition</span><span class="sxs-lookup"><span data-stu-id="2d971-191">New-AzureHDInsightHiveJobDefinition</span></span> |[<span data-ttu-id="2d971-192">Nieuwe AzureRmHDInsightHiveJobDefinition</span><span class="sxs-lookup"><span data-stu-id="2d971-192">New-AzureRmHDInsightHiveJobDefinition</span></span>](https://msdn.microsoft.com/library/mt619448.aspx) |
| <span data-ttu-id="2d971-193">New-AzureHDInsightMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="2d971-193">New-AzureHDInsightMapReduceJobDefinition</span></span> |[<span data-ttu-id="2d971-194">Nieuwe AzureRmHDInsightMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="2d971-194">New-AzureRmHDInsightMapReduceJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603626.aspx) |
| <span data-ttu-id="2d971-195">New-AzureHDInsightPigJobDefinition</span><span class="sxs-lookup"><span data-stu-id="2d971-195">New-AzureHDInsightPigJobDefinition</span></span> |[<span data-ttu-id="2d971-196">Nieuwe AzureRmHDInsightPigJobDefinition</span><span class="sxs-lookup"><span data-stu-id="2d971-196">New-AzureRmHDInsightPigJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603671.aspx) |
| <span data-ttu-id="2d971-197">New-AzureHDInsightSqoopJobDefinition</span><span class="sxs-lookup"><span data-stu-id="2d971-197">New-AzureHDInsightSqoopJobDefinition</span></span> |[<span data-ttu-id="2d971-198">Nieuwe AzureRmHDInsightSqoopJobDefinition</span><span class="sxs-lookup"><span data-stu-id="2d971-198">New-AzureRmHDInsightSqoopJobDefinition</span></span>](https://msdn.microsoft.com/library/mt608551.aspx) |
| <span data-ttu-id="2d971-199">New-AzureHDInsightStreamingMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="2d971-199">New-AzureHDInsightStreamingMapReduceJobDefinition</span></span> |[<span data-ttu-id="2d971-200">Nieuwe AzureRmHDInsightStreamingMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="2d971-200">New-AzureRmHDInsightStreamingMapReduceJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603626.aspx) |
| <span data-ttu-id="2d971-201">Remove-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="2d971-201">Remove-AzureHDInsightCluster</span></span> |[<span data-ttu-id="2d971-202">Verwijder AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="2d971-202">Remove-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619431.aspx) |
| <span data-ttu-id="2d971-203">Revoke-AzureHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="2d971-203">Revoke-AzureHDInsightHttpServicesAccess</span></span> |[<span data-ttu-id="2d971-204">REVOKE AzureRmHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="2d971-204">Revoke-AzureRmHDInsightHttpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt619375.aspx) |
| <span data-ttu-id="2d971-205">Revoke-AzureHdinsightRdpAccess</span><span class="sxs-lookup"><span data-stu-id="2d971-205">Revoke-AzureHdinsightRdpAccess</span></span> |[<span data-ttu-id="2d971-206">REVOKE AzureRmHDInsightRdpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="2d971-206">Revoke-AzureRmHDInsightRdpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt603523.aspx) |
| <span data-ttu-id="2d971-207">Set-AzureHDInsightClusterSize</span><span class="sxs-lookup"><span data-stu-id="2d971-207">Set-AzureHDInsightClusterSize</span></span> |[<span data-ttu-id="2d971-208">Set-AzureRmHDInsightClusterSize</span><span class="sxs-lookup"><span data-stu-id="2d971-208">Set-AzureRmHDInsightClusterSize</span></span>](https://msdn.microsoft.com/library/mt603513.aspx) |
| <span data-ttu-id="2d971-209">Set-AzureHDInsightDefaultStorage</span><span class="sxs-lookup"><span data-stu-id="2d971-209">Set-AzureHDInsightDefaultStorage</span></span> |[<span data-ttu-id="2d971-210">Set-AzureRmHDInsightDefaultStorage</span><span class="sxs-lookup"><span data-stu-id="2d971-210">Set-AzureRmHDInsightDefaultStorage</span></span>](https://msdn.microsoft.com/library/mt603486.aspx) |
| <span data-ttu-id="2d971-211">Start-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="2d971-211">Start-AzureHDInsightJob</span></span> |[<span data-ttu-id="2d971-212">Start AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="2d971-212">Start-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603798.aspx) |
| <span data-ttu-id="2d971-213">Stop-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="2d971-213">Stop-AzureHDInsightJob</span></span> |[<span data-ttu-id="2d971-214">Stop AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="2d971-214">Stop-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt619424.aspx) |
| <span data-ttu-id="2d971-215">Use-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="2d971-215">Use-AzureHDInsightCluster</span></span> |[<span data-ttu-id="2d971-216">Gebruik AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="2d971-216">Use-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619442.aspx) |
| <span data-ttu-id="2d971-217">Wait-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="2d971-217">Wait-AzureHDInsightJob</span></span> |[<span data-ttu-id="2d971-218">Wacht AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="2d971-218">Wait-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603834.aspx) |

### <a name="new-cmdlets"></a><span data-ttu-id="2d971-219">Nieuwe cmdLets</span><span class="sxs-lookup"><span data-stu-id="2d971-219">New cmdlets</span></span>
<span data-ttu-id="2d971-220">Hallo volgen Hallo nieuwe cmdlets die alleen beschikbaar in Hallo ARM-modus zijn.</span><span class="sxs-lookup"><span data-stu-id="2d971-220">hello following are hello new cmdlets that are only available in hello ARM mode.</span></span> 

<span data-ttu-id="2d971-221">**Scriptactie verwante cmdlets:**</span><span class="sxs-lookup"><span data-stu-id="2d971-221">**Script action related cmdlets:**</span></span>

* <span data-ttu-id="2d971-222">**Get-AzureRmHDInsightPersistedScriptAction**: opgehaald Hallo persistent scriptacties voor een cluster en worden ze weergegeven in chronologische volgorde of details voor een opgegeven persistente scriptacties actie opgehaald.</span><span class="sxs-lookup"><span data-stu-id="2d971-222">**Get-AzureRmHDInsightPersistedScriptAction**: Gets hello persisted script actions for a cluster and lists them in chronological order, or gets details for a specified persisted script action.</span></span> 
* <span data-ttu-id="2d971-223">**Get-AzureRmHDInsightScriptActionHistory**: Geschiedenis van de scriptactie Hallo opgehaald voor een cluster en details van een eerder uitgevoerde scriptactie opgehaald, wordt weergegeven in omgekeerde volgorde.</span><span class="sxs-lookup"><span data-stu-id="2d971-223">**Get-AzureRmHDInsightScriptActionHistory**: Gets hello script action history for a cluster and lists it in reverse chronological order, or gets details of a previously executed script action.</span></span> 
* <span data-ttu-id="2d971-224">**Verwijder AzureRmHDInsightPersistedScriptAction**: Hiermee verwijdert u een actie persistent script van een HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="2d971-224">**Remove-AzureRmHDInsightPersistedScriptAction**: Removes a persisted script action from an HDInsight cluster.</span></span>
* <span data-ttu-id="2d971-225">**Set-AzureRmHDInsightPersistedScriptAction**: Hiermee stelt u een eerder uitgevoerde script actie toobe een persistent script in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="2d971-225">**Set-AzureRmHDInsightPersistedScriptAction**: Sets a previously executed script action toobe a persisted script action.</span></span>
* <span data-ttu-id="2d971-226">**Indienen AzureRmHDInsightScriptAction**: een nieuwe script actie tooan Azure HDInsight-cluster worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="2d971-226">**Submit-AzureRmHDInsightScriptAction**: Submits a new script action tooan Azure HDInsight cluster.</span></span> 

<span data-ttu-id="2d971-227">Zie voor meer informatie over het gebruiksinformatie [aanpassen Linux gebaseerde HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="2d971-227">For additional usage information, see [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="2d971-228">**Clsuter identiteit verwante cmdlets:**</span><span class="sxs-lookup"><span data-stu-id="2d971-228">**Clsuter identity related cmdlets:**</span></span>

* <span data-ttu-id="2d971-229">**Voeg AzureRmHDInsightClusterIdentity**: een cluster identiteit tooa cluster configuration-object toegevoegd zodat hello HDInsight-cluster toegang Azure Data Lake Stores tot hebben.</span><span class="sxs-lookup"><span data-stu-id="2d971-229">**Add-AzureRmHDInsightClusterIdentity**: Adds a cluster identity tooa cluster configuration object so that hello HDInsight cluster can access Azure Data Lake Stores.</span></span> <span data-ttu-id="2d971-230">Zie [een HDInsight-cluster maken met Data Lake Store met Azure PowerShell](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="2d971-230">See [Create an HDInsight cluster with Data Lake Store using Azure PowerShell](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md).</span></span>

### <a name="examples"></a><span data-ttu-id="2d971-231">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="2d971-231">Examples</span></span>
<span data-ttu-id="2d971-232">**Cluster maken**</span><span class="sxs-lookup"><span data-stu-id="2d971-232">**Create cluster**</span></span>

<span data-ttu-id="2d971-233">Oude opdracht (ASM):</span><span class="sxs-lookup"><span data-stu-id="2d971-233">Old command (ASM):</span></span> 

    New-AzureHDInsightCluster `
        -Name $clusterName `
        -Location $location `
        -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $storageAccountKey `
        -DefaultStorageContainerName $containerName `
        -ClusterSizeInNodes 2 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.2" `
        -Credential $httpCredential `
        -SshCredential $sshCredential

<span data-ttu-id="2d971-234">Nieuwe opdracht (ARM):</span><span class="sxs-lookup"><span data-stu-id="2d971-234">New command (ARM):</span></span>

    New-AzureRmHDInsightCluster `
        -ClusterName $clusterName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $storageAccountKey `
        -DefaultStorageContainer $containerName  `
        -ClusterSizeInNodes 2 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.2" `
        -HttpCredential $httpcredentials `
        -SshCredential $sshCredentials


<span data-ttu-id="2d971-235">**Cluster verwijderen**</span><span class="sxs-lookup"><span data-stu-id="2d971-235">**Delete cluster**</span></span>

<span data-ttu-id="2d971-236">Oude opdracht (ASM):</span><span class="sxs-lookup"><span data-stu-id="2d971-236">Old command (ASM):</span></span>

    Remove-AzureHDInsightCluster -name $clusterName 

<span data-ttu-id="2d971-237">Nieuwe opdracht (ARM):</span><span class="sxs-lookup"><span data-stu-id="2d971-237">New command (ARM):</span></span>

    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName 

<span data-ttu-id="2d971-238">**Lijst met cluster**</span><span class="sxs-lookup"><span data-stu-id="2d971-238">**List cluster**</span></span>

<span data-ttu-id="2d971-239">Oude opdracht (ASM):</span><span class="sxs-lookup"><span data-stu-id="2d971-239">Old command (ASM):</span></span>

    Get-AzureHDInsightCluster

<span data-ttu-id="2d971-240">Nieuwe opdracht (ARM):</span><span class="sxs-lookup"><span data-stu-id="2d971-240">New command (ARM):</span></span>

    Get-AzureRmHDInsightCluster 

<span data-ttu-id="2d971-241">**Cluster weergeven**</span><span class="sxs-lookup"><span data-stu-id="2d971-241">**Show cluster**</span></span>

<span data-ttu-id="2d971-242">Oude opdracht (ASM):</span><span class="sxs-lookup"><span data-stu-id="2d971-242">Old command (ASM):</span></span>

    Get-AzureHDInsightCluster -Name $clusterName

<span data-ttu-id="2d971-243">Nieuwe opdracht (ARM):</span><span class="sxs-lookup"><span data-stu-id="2d971-243">New command (ARM):</span></span>

    Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -clusterName $clusterName


#### <a name="other-samples"></a><span data-ttu-id="2d971-244">Andere voorbeelden</span><span class="sxs-lookup"><span data-stu-id="2d971-244">Other samples</span></span>
* [<span data-ttu-id="2d971-245">HDInsight-clusters maken</span><span class="sxs-lookup"><span data-stu-id="2d971-245">Create HDInsight clusters</span></span>](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
* [<span data-ttu-id="2d971-246">Indienen van Hive-taken</span><span class="sxs-lookup"><span data-stu-id="2d971-246">Submit Hive jobs</span></span>](hdinsight-hadoop-use-hive-powershell.md)
* [<span data-ttu-id="2d971-247">Pig-taken verzenden</span><span class="sxs-lookup"><span data-stu-id="2d971-247">Submit Pig jobs</span></span>](hdinsight-hadoop-use-pig-powershell.md)
* [<span data-ttu-id="2d971-248">Sqoop taken verzenden</span><span class="sxs-lookup"><span data-stu-id="2d971-248">Submit Sqoop jobs</span></span>](hdinsight-hadoop-use-sqoop-powershell.md)

## <a name="migrating-toohello-arm-based-hdinsight-net-sdk"></a><span data-ttu-id="2d971-249">Migreren toohello op basis van ARM HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="2d971-249">Migrating toohello ARM-based HDInsight .NET SDK</span></span>
<span data-ttu-id="2d971-250">Hallo op basis van Azure Service Management [(ASM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt416619.aspx) is nu verouderd.</span><span class="sxs-lookup"><span data-stu-id="2d971-250">hello Azure Service Management-based [(ASM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt416619.aspx) is now deprecated.</span></span> <span data-ttu-id="2d971-251">U wordt aangeraden toouse Hallo op basis van Azure Resource Management [(ARM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt271028.aspx).</span><span class="sxs-lookup"><span data-stu-id="2d971-251">You are encouraged toouse hello Azure Resource Management-based [(ARM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt271028.aspx).</span></span> <span data-ttu-id="2d971-252">Hallo worden volgende HDInsight op basis van de ASM-pakketten afgeschaft.</span><span class="sxs-lookup"><span data-stu-id="2d971-252">hello following ASM-based HDInsight packages are being deprecated.</span></span>

* `Microsoft.WindowsAzure.Management.HDInsight`
* `Microsoft.Hadoop.Client`

<span data-ttu-id="2d971-253">Deze sectie bevat verwijzingen toomore informatie over het tooperform bepaalde taken met Hallo op basis van ARM-SDK.</span><span class="sxs-lookup"><span data-stu-id="2d971-253">This section provides pointers toomore information on how tooperform certain tasks using hello ARM-based SDK.</span></span>

| <span data-ttu-id="2d971-254">Hoe... met behulp van HDInsight SDK op basis van ARM Hallo</span><span class="sxs-lookup"><span data-stu-id="2d971-254">How to... using hello ARM-based HDInsight SDK</span></span> | <span data-ttu-id="2d971-255">Koppelingen</span><span class="sxs-lookup"><span data-stu-id="2d971-255">Links</span></span> |
| --- | --- |
| <span data-ttu-id="2d971-256">Maken van HDInsight-clusters met .NET SDK</span><span class="sxs-lookup"><span data-stu-id="2d971-256">Create HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="2d971-257">Zie [HDInsight-clusters maken met .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="2d971-257">See [Create HDInsight clusters using .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="2d971-258">Aanpassen van een cluster met de scriptactie met .NET SDK</span><span class="sxs-lookup"><span data-stu-id="2d971-258">Customize a cluster using Script Action with .NET SDK</span></span> |<span data-ttu-id="2d971-259">Zie [aanpassen HDInsight Linux-clusters met behulp van de scriptactie](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action)</span><span class="sxs-lookup"><span data-stu-id="2d971-259">See [Customize HDInsight Linux clusters using Script Action](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action)</span></span> |
| <span data-ttu-id="2d971-260">Verifiëren van toepassingen die gebruikmaken van Azure Active Directory interactief met .NET SDK</span><span class="sxs-lookup"><span data-stu-id="2d971-260">Authenticate applications interactively using Azure Active Directory with .NET SDK</span></span> |<span data-ttu-id="2d971-261">Zie [uitvoeren Hive-query's met .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="2d971-261">See [Run Hive queries using .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span> <span data-ttu-id="2d971-262">Hallo-codefragment in dit artikel gebruikt Hallo interactieve verificatie benadering.</span><span class="sxs-lookup"><span data-stu-id="2d971-262">hello code snippet in this article uses hello interactive authentication approach.</span></span> |
| <span data-ttu-id="2d971-263">Verifiëren van toepassingen die gebruikmaken van Azure Active Directory niet-interactief met .NET SDK</span><span class="sxs-lookup"><span data-stu-id="2d971-263">Authenticate applications non-interactively using Azure Active Directory with .NET SDK</span></span> |<span data-ttu-id="2d971-264">Zie [niet-interactieve toepassingen voor HDInsight maken](hdinsight-create-non-interactive-authentication-dotnet-applications.md)</span><span class="sxs-lookup"><span data-stu-id="2d971-264">See [Create non-interactive applications for HDInsight](hdinsight-create-non-interactive-authentication-dotnet-applications.md)</span></span> |
| <span data-ttu-id="2d971-265">Verzenden van een Hive-taak met .NET SDK</span><span class="sxs-lookup"><span data-stu-id="2d971-265">Submit a Hive job using .NET SDK</span></span> |<span data-ttu-id="2d971-266">Zie [indienen Hive-taken](hdinsight-hadoop-use-hive-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="2d971-266">See [Submit Hive jobs](hdinsight-hadoop-use-hive-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="2d971-267">Verzenden van een Pig-taak met .NET SDK</span><span class="sxs-lookup"><span data-stu-id="2d971-267">Submit a Pig job using .NET SDK</span></span> |<span data-ttu-id="2d971-268">Zie [verzenden van Pig-taken](hdinsight-hadoop-use-pig-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="2d971-268">See [Submit Pig jobs](hdinsight-hadoop-use-pig-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="2d971-269">Verzenden van een Sqoop taak met .NET SDK</span><span class="sxs-lookup"><span data-stu-id="2d971-269">Submit a Sqoop job using .NET SDK</span></span> |<span data-ttu-id="2d971-270">Zie [Sqoop verzenden van taken](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="2d971-270">See [Submit Sqoop jobs](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="2d971-271">Lijst met HDInsight-clusters met .NET SDK</span><span class="sxs-lookup"><span data-stu-id="2d971-271">List HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="2d971-272">Zie [lijst HDInsight-clusters](hdinsight-administer-use-dotnet-sdk.md#list-clusters)</span><span class="sxs-lookup"><span data-stu-id="2d971-272">See [List HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#list-clusters)</span></span> |
| <span data-ttu-id="2d971-273">Schalen van HDInsight-clusters met .NET SDK</span><span class="sxs-lookup"><span data-stu-id="2d971-273">Scale HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="2d971-274">Zie [Scale HDInsight-clusters](hdinsight-administer-use-dotnet-sdk.md#scale-clusters)</span><span class="sxs-lookup"><span data-stu-id="2d971-274">See [Scale HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#scale-clusters)</span></span> |
| <span data-ttu-id="2d971-275">GRANT/revoke toegang tooHDInsight clusters met .NET SDK</span><span class="sxs-lookup"><span data-stu-id="2d971-275">Grant/revoke access tooHDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="2d971-276">Zie [Grant/revoke toegang tooHDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access)</span><span class="sxs-lookup"><span data-stu-id="2d971-276">See [Grant/revoke access tooHDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access)</span></span> |
| <span data-ttu-id="2d971-277">HTTP-gebruikersreferenties updaten voor HDInsight-clusters met .NET SDK</span><span class="sxs-lookup"><span data-stu-id="2d971-277">Update HTTP user credentials for HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="2d971-278">Zie [Update HTTP gebruikersreferenties voor HDInsight-clusters](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials)</span><span class="sxs-lookup"><span data-stu-id="2d971-278">See [Update HTTP user credentials for HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials)</span></span> |
| <span data-ttu-id="2d971-279">Hallo standaardopslagaccount vinden voor HDInsight-clusters met .NET SDK</span><span class="sxs-lookup"><span data-stu-id="2d971-279">Find hello default storage account for HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="2d971-280">Zie [hello standaardopslagaccount vinden voor HDInsight-clusters](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account)</span><span class="sxs-lookup"><span data-stu-id="2d971-280">See [Find hello default storage account for HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account)</span></span> |
| <span data-ttu-id="2d971-281">HDInsight-clusters met .NET SDK verwijderen</span><span class="sxs-lookup"><span data-stu-id="2d971-281">Delete HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="2d971-282">Zie [verwijderen HDInsight-clusters](hdinsight-administer-use-dotnet-sdk.md#delete-clusters)</span><span class="sxs-lookup"><span data-stu-id="2d971-282">See [Delete HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#delete-clusters)</span></span> |

### <a name="examples"></a><span data-ttu-id="2d971-283">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="2d971-283">Examples</span></span>
<span data-ttu-id="2d971-284">Hieronder volgen enkele voorbeelden van hoe een bewerking is uitgevoerd met behulp van Hallo ASM gebaseerde SDK en Hallo gelijkwaardige codefragment voor Hallo op basis van ARM-SDK.</span><span class="sxs-lookup"><span data-stu-id="2d971-284">Following are some examples on how an operation is performed using hello ASM-based SDK and hello equivalent code snippet for hello ARM-based SDK.</span></span>

<span data-ttu-id="2d971-285">**Maken van een cluster CRUD-client**</span><span class="sxs-lookup"><span data-stu-id="2d971-285">**Creating a cluster CRUD client**</span></span>

* <span data-ttu-id="2d971-286">Vorige opdracht (ASM)</span><span class="sxs-lookup"><span data-stu-id="2d971-286">Old command (ASM)</span></span>
  
        //Certificate auth
        //This logs hello application in using a subscription administration certificate, which is not offered in Azure Resource Manager (ARM)
  
        const string subid = "454467d4-60ca-4dfd-a556-216eeeeeeee1";
        var cred = new HDInsightCertificateCredential(new Guid(subid), new X509Certificate2(@"path\to\certificate.cer"));
        var client = HDInsightClient.Connect(cred);
* <span data-ttu-id="2d971-287">Nieuwe opdracht (ARM) (Service principal autorisatie)</span><span class="sxs-lookup"><span data-stu-id="2d971-287">New command (ARM) (Service principal authorization)</span></span>
  
        //Service principal auth
        //This will log hello application in as itself, rather than on behalf of a specific user.
        //For details, including how tooset up hello application, see:
        //   https://azure.microsoft.com/en-us/documentation/articles/hdinsight-create-non-interactive-authentication-dotnet-applications/
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.ServicePrincipal, Id = clientId };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, tenantId, secretKey, ShowDialog.Never).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);
* <span data-ttu-id="2d971-288">Nieuwe opdracht (ARM) (gebruikersautorisatie)</span><span class="sxs-lookup"><span data-stu-id="2d971-288">New command (ARM) (User authorization)</span></span>
  
        //User auth
        //This will log hello application in on behalf of hello user.
        //hello end-user will see a login popup.
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.User, Id = username };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, AuthenticationFactory.CommonAdTenant, password, ShowDialog.Auto).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);

<span data-ttu-id="2d971-289">**Maken van een cluster**</span><span class="sxs-lookup"><span data-stu-id="2d971-289">**Creating a cluster**</span></span>

* <span data-ttu-id="2d971-290">Vorige opdracht (ASM)</span><span class="sxs-lookup"><span data-stu-id="2d971-290">Old command (ASM)</span></span>
  
        var clusterInfo = new ClusterCreateParameters
                    {
                        Name = dnsName,
                        DefaultStorageAccountKey = key,
                        DefaultStorageContainer = defaultStorageContainer,
                        DefaultStorageAccountName = storageAccountDnsName,
                        ClusterSizeInNodes = 1,
                        ClusterType = type,
                        Location = "West US",
                        UserName = "admin",
                        Password = "*******",
                        Version = version,
                        HeadNodeSize = NodeVMSize.Large,
                    };
        clusterInfo.CoreConfiguration.Add(new KeyValuePair<string, string>("config1", "value1"));
        client.CreateCluster(clusterInfo);
* <span data-ttu-id="2d971-291">Nieuwe opdracht (ARM)</span><span class="sxs-lookup"><span data-stu-id="2d971-291">New command (ARM)</span></span>
  
        var clusterCreateParameters = new ClusterCreateParameters
            {
                Location = "West US",
                ClusterType = "Hadoop",
                Version = "3.1",
                OSType = OSType.Linux,
                DefaultStorageAccountName = "mystorage.blob.core.windows.net",
                DefaultStorageAccountKey =
                    "O9EQvp3A3AjXq/W27rst1GQfLllhp0gUeiUUn2D8zX2lU3taiXSSfqkZlcPv+nQcYUxYw==",
                UserName = "hadoopuser",
                Password = "*******",
                HeadNodeSize = "ExtraLarge",
                RdpUsername = "hdirp",
                RdpPassword = ""*******",
                RdpAccessExpiry = new DateTime(2025, 3, 1),
                ClusterSizeInNodes = 5
            };
        var coreConfigs = new Dictionary<string, string> {{"config1", "value1"}};
        clusterCreateParameters.Configurations.Add(ConfigurationKey.CoreSite, coreConfigs);

<span data-ttu-id="2d971-292">**HTTP-toegang inschakelen**</span><span class="sxs-lookup"><span data-stu-id="2d971-292">**Enabling HTTP access**</span></span>

* <span data-ttu-id="2d971-293">Vorige opdracht (ASM)</span><span class="sxs-lookup"><span data-stu-id="2d971-293">Old command (ASM)</span></span>
  
        client.EnableHttp(dnsName, "West US", "admin", "*******");
* <span data-ttu-id="2d971-294">Nieuwe opdracht (ARM)</span><span class="sxs-lookup"><span data-stu-id="2d971-294">New command (ARM)</span></span>
  
        var httpParams = new HttpSettingsParameters
        {
               HttpUserEnabled = true,
               HttpUsername = "admin",
               HttpPassword = "*******",
        };
        client.Clusters.ConfigureHttpSettings(resourceGroup, dnsname, httpParams);

<span data-ttu-id="2d971-295">**Verwijderen van een cluster**</span><span class="sxs-lookup"><span data-stu-id="2d971-295">**Deleting a cluster**</span></span>

* <span data-ttu-id="2d971-296">Vorige opdracht (ASM)</span><span class="sxs-lookup"><span data-stu-id="2d971-296">Old command (ASM)</span></span>
  
        client.DeleteCluster(dnsName);
* <span data-ttu-id="2d971-297">Nieuwe opdracht (ARM)</span><span class="sxs-lookup"><span data-stu-id="2d971-297">New command (ARM)</span></span>
  
        client.Clusters.Delete(resourceGroup, dnsname);

