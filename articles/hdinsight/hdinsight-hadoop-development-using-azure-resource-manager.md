---
title: Migreren naar Azure Resource Manager-hulpprogramma's voor HDInsight | Microsoft Docs
description: Migreren naar Azure Resource Manager ontwikkelprogramma's voor HDInsight-clusters
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
ms.openlocfilehash: 708d22b9ce53d4dbc07c6bcde0c46dcd238291bb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="migrating-to-azure-resource-manager-based-development-tools-for-hdinsight-clusters"></a><span data-ttu-id="9f552-103">Migreren naar Azure Resource Manager gebaseerde ontwikkelprogramma's voor HDInsight-clusters</span><span class="sxs-lookup"><span data-stu-id="9f552-103">Migrating to Azure Resource Manager-based development tools for HDInsight clusters</span></span>

<span data-ttu-id="9f552-104">HDInsight is het van Azure Service Manager ASM-hulpprogramma's voor HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9f552-104">HDInsight is deprecating Azure Service Manager (ASM)-based tools for HDInsight.</span></span> <span data-ttu-id="9f552-105">Als u hebt gebruikt Azure PowerShell, Azure CLI of de HDInsight .NET SDK werken met HDInsight-clusters, wordt u aangeraden de Azure Resource Manager ARM gebaseerde versies van PowerShell, CLI en .NET SDK gaan gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9f552-105">If you have been using Azure PowerShell, Azure CLI, or the HDInsight .NET SDK to work with HDInsight clusters, you are encouraged to use the Azure Resource Manager (ARM)-based versions of PowerShell, CLI, and .NET SDK going forward.</span></span> <span data-ttu-id="9f552-106">Dit artikel bevat verwijzingen over het migreren naar de nieuwe benadering van op basis van ARM.</span><span class="sxs-lookup"><span data-stu-id="9f552-106">This article provides pointers on how to migrate to the new ARM-based approach.</span></span> <span data-ttu-id="9f552-107">Waar van toepassing, wijst in dit artikel ook op de verschillen tussen de ARM en ASM benaderingen voor HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9f552-107">Wherever applicable, this article also points out the differences between the ASM and ARM approaches for HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9f552-108">De ondersteuning voor ASM op basis van PowerShell, CLI en .NET SDK af te breken op **1 januari 2017**.</span><span class="sxs-lookup"><span data-stu-id="9f552-108">The support for ASM based PowerShell, CLI, and .NET SDK will discontinue on **January 1, 2017**.</span></span>
> 
> 

## <a name="migrating-azure-cli-to-azure-resource-manager"></a><span data-ttu-id="9f552-109">Azure CLI migreren naar Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9f552-109">Migrating Azure CLI to Azure Resource Manager</span></span>
<span data-ttu-id="9f552-110">De Azure CLI nu standaard naar de modus Azure Resource Manager (ARM), tenzij u een upgrade van een vorige installatie uitvoert; u wilt in dit geval gebruiken de `azure config mode arm` opdracht overschakelen naar ARM-modus.</span><span class="sxs-lookup"><span data-stu-id="9f552-110">The Azure CLI now defaults to Azure Resource Manager (ARM) mode, unless you are upgrading from a previous installation; in this case, you may need to use the `azure config mode arm` command to switch to ARM mode.</span></span>

<span data-ttu-id="9f552-111">De basisopdrachten die de Azure CLI opgegeven om te werken met HDInsight met behulp van Azure Service Management (ASM) zijn hetzelfde als met ARM; Sommige parameters en schakelopties mogelijk wel nieuwe namen en er zijn veel nieuwe parameters beschikbaar wanneer u de ARM.</span><span class="sxs-lookup"><span data-stu-id="9f552-111">The basic commands that the Azure CLI provided to work with HDInsight using Azure Service Management (ASM) are the same when using ARM; however some parameters and switches may have new names, and there are many new parameters available when using ARM.</span></span> <span data-ttu-id="9f552-112">Bijvoorbeeld, u kunt nu gebruiken `azure hdinsight cluster create` de Azure-netwerk dat moet worden gemaakt in een cluster of Hive en Oozie-metastore informatie te geven.</span><span class="sxs-lookup"><span data-stu-id="9f552-112">For example, you can now use `azure hdinsight cluster create` to specify the Azure Virtual Network that a cluster should be created in, or Hive and Oozie metastore information.</span></span>

<span data-ttu-id="9f552-113">Basic-opdrachten voor het werken met HDInsight via Azure Resource Manager zijn:</span><span class="sxs-lookup"><span data-stu-id="9f552-113">Basic commands for working with HDInsight through Azure Resource Manager are:</span></span>

* <span data-ttu-id="9f552-114">`azure hdinsight cluster create`-maakt een nieuwe HDInsight-cluster</span><span class="sxs-lookup"><span data-stu-id="9f552-114">`azure hdinsight cluster create` - creates a new HDInsight cluster</span></span>
* <span data-ttu-id="9f552-115">`azure hdinsight cluster delete`-een bestaand HDInsight-cluster worden verwijderd</span><span class="sxs-lookup"><span data-stu-id="9f552-115">`azure hdinsight cluster delete` - deletes an existing HDInsight cluster</span></span>
* <span data-ttu-id="9f552-116">`azure hdinsight cluster show`-informatie weer over een bestaand cluster</span><span class="sxs-lookup"><span data-stu-id="9f552-116">`azure hdinsight cluster show` - display information about an existing cluster</span></span>
* <span data-ttu-id="9f552-117">`azure hdinsight cluster list`-een lijst met HDInsight-clusters voor uw Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="9f552-117">`azure hdinsight cluster list` - lists HDInsight clusters for your Azure subscription</span></span>

<span data-ttu-id="9f552-118">Gebruik de `-h` overschakelen naar het inspecteren van de parameters en switches beschikbaar zijn voor elke opdracht.</span><span class="sxs-lookup"><span data-stu-id="9f552-118">Use the `-h` switch to inspect the parameters and switches available for each command.</span></span>

### <a name="new-commands"></a><span data-ttu-id="9f552-119">Nieuwe opdrachten</span><span class="sxs-lookup"><span data-stu-id="9f552-119">New commands</span></span>
<span data-ttu-id="9f552-120">Nieuwe opdrachten die beschikbaar zijn met Azure Resource Manager zijn:</span><span class="sxs-lookup"><span data-stu-id="9f552-120">New commands available with Azure Resource Manager are:</span></span>

* <span data-ttu-id="9f552-121">`azure hdinsight cluster resize`-het aantal worker-knooppunten in het cluster dynamisch wordt gewijzigd</span><span class="sxs-lookup"><span data-stu-id="9f552-121">`azure hdinsight cluster resize` - dynamically changes the number of worker nodes in the cluster</span></span>
* <span data-ttu-id="9f552-122">`azure hdinsight cluster enable-http-access`-HTTPs toegang biedt tot het cluster (op standaard)</span><span class="sxs-lookup"><span data-stu-id="9f552-122">`azure hdinsight cluster enable-http-access` - enables HTTPs access to the cluster (on by default)</span></span>
* <span data-ttu-id="9f552-123">`azure hdinsight cluster disable-http-access`-HTTPs-toegang tot het cluster wordt uitgeschakeld</span><span class="sxs-lookup"><span data-stu-id="9f552-123">`azure hdinsight cluster disable-http-access` - disables HTTPs access to the cluster</span></span>
* <span data-ttu-id="9f552-124">`azure hdinsight script-action`-bevat opdrachten voor het maken/beheren scriptacties op een cluster</span><span class="sxs-lookup"><span data-stu-id="9f552-124">`azure hdinsight script-action` - provides commands for creating/managing Script Actions on a cluster</span></span>
* <span data-ttu-id="9f552-125">`azure hdinsight config`-bevat opdrachten voor het maken van een configuratiebestand dat kan worden gebruikt met de `hdinsight cluster create` opdracht om configuratie-informatie te geven.</span><span class="sxs-lookup"><span data-stu-id="9f552-125">`azure hdinsight config` - provides commands for creating a configuration file that can be used with the `hdinsight cluster create` command to provide configuration information.</span></span>

### <a name="deprecated-commands"></a><span data-ttu-id="9f552-126">Afgeschafte opdrachten</span><span class="sxs-lookup"><span data-stu-id="9f552-126">Deprecated commands</span></span>
<span data-ttu-id="9f552-127">Als u de `azure hdinsight job` opdrachten voor het verzenden van taken naar uw HDInsight-cluster deze zijn niet beschikbaar is via de ARM-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="9f552-127">If you use the `azure hdinsight job` commands to submit jobs to your HDInsight cluster, these are not available through the ARM commands.</span></span> <span data-ttu-id="9f552-128">Als u programmatisch verzenden van taken naar HDInsight van scripts wilt, moet u in plaats daarvan de REST-API's geleverd door HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9f552-128">If you need to programmatically submit jobs to HDInsight from scripts, you should instead use the REST APIs provided by HDInsight.</span></span> <span data-ttu-id="9f552-129">Zie de volgende documenten voor meer informatie over het verzenden van taken met REST API's.</span><span class="sxs-lookup"><span data-stu-id="9f552-129">For more information on submitting jobs using REST APIs, see the following documents.</span></span>

* [<span data-ttu-id="9f552-130">MapReduce-taken uitvoeren met Hadoop in HDInsight met cURL</span><span class="sxs-lookup"><span data-stu-id="9f552-130">Run MapReduce jobs with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-mapreduce-curl.md)
* [<span data-ttu-id="9f552-131">Hive-query's uitvoeren met Hadoop in HDInsight met cURL</span><span class="sxs-lookup"><span data-stu-id="9f552-131">Run Hive queries with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-hive-curl.md)
* [<span data-ttu-id="9f552-132">Pig-taken uitvoeren met Hadoop in HDInsight met cURL</span><span class="sxs-lookup"><span data-stu-id="9f552-132">Run Pig jobs with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-pig-curl.md)

<span data-ttu-id="9f552-133">Voor informatie over andere manieren om uit te voeren MapReduce, Hive, en interactief varkens, Zie [MapReduce gebruiken met Hadoop op HDInsight](hdinsight-use-mapreduce.md), [Hive gebruiken met Hadoop op HDInsight](hdinsight-use-hive.md), en [Pig gebruiken met Hadoop op HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="9f552-133">For information on other ways to run MapReduce, Hive, and Pig interactively, see [Use MapReduce with Hadoop on HDInsight](hdinsight-use-mapreduce.md), [Use Hive with Hadoop on HDInsight](hdinsight-use-hive.md), and [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

### <a name="examples"></a><span data-ttu-id="9f552-134">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="9f552-134">Examples</span></span>
<span data-ttu-id="9f552-135">**Maken van een cluster**</span><span class="sxs-lookup"><span data-stu-id="9f552-135">**Creating a cluster**</span></span>

* <span data-ttu-id="9f552-136">Vorige opdracht (ASM)-`azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`</span><span class="sxs-lookup"><span data-stu-id="9f552-136">Old command (ASM) - `azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`</span></span>
* <span data-ttu-id="9f552-137">Nieuwe opdracht (ARM)-`azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`</span><span class="sxs-lookup"><span data-stu-id="9f552-137">New command (ARM) - `azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`</span></span>

<span data-ttu-id="9f552-138">**Verwijderen van een cluster**</span><span class="sxs-lookup"><span data-stu-id="9f552-138">**Deleting a cluster**</span></span>

* <span data-ttu-id="9f552-139">Vorige opdracht (ASM)-`azure hdinsight cluster delete myhdicluster`</span><span class="sxs-lookup"><span data-stu-id="9f552-139">Old command (ASM) - `azure hdinsight cluster delete myhdicluster`</span></span>
* <span data-ttu-id="9f552-140">Nieuwe opdracht (ARM)-`azure hdinsight cluster delete mycluster -g myresourcegroup`</span><span class="sxs-lookup"><span data-stu-id="9f552-140">New command (ARM) - `azure hdinsight cluster delete mycluster -g myresourcegroup`</span></span>

<span data-ttu-id="9f552-141">**Lijst met clusters**</span><span class="sxs-lookup"><span data-stu-id="9f552-141">**List clusters**</span></span>

* <span data-ttu-id="9f552-142">Vorige opdracht (ASM)-`azure hdinsight cluster list`</span><span class="sxs-lookup"><span data-stu-id="9f552-142">Old command (ASM) - `azure hdinsight cluster list`</span></span>
* <span data-ttu-id="9f552-143">Nieuwe opdracht (ARM)-`azure hdinsight cluster list`</span><span class="sxs-lookup"><span data-stu-id="9f552-143">New command (ARM) - `azure hdinsight cluster list`</span></span>

> [!NOTE]
> <span data-ttu-id="9f552-144">Voor de opdracht lijst opgeven van de resource-groep met `-g` retourneert alleen de clusters in de opgegeven resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="9f552-144">For the list command, specifying the resource group using `-g` will return only the clusters in the specified resource group.</span></span>
> 
> 

<span data-ttu-id="9f552-145">**Cluster-informatie weergeven**</span><span class="sxs-lookup"><span data-stu-id="9f552-145">**Show cluster information**</span></span>

* <span data-ttu-id="9f552-146">Vorige opdracht (ASM)-`azure hdinsight cluster show myhdicluster`</span><span class="sxs-lookup"><span data-stu-id="9f552-146">Old command (ASM) - `azure hdinsight cluster show myhdicluster`</span></span>
* <span data-ttu-id="9f552-147">Nieuwe opdracht (ARM)-`azure hdinsight cluster show myhdicluster -g myresourcegroup`</span><span class="sxs-lookup"><span data-stu-id="9f552-147">New command (ARM) - `azure hdinsight cluster show myhdicluster -g myresourcegroup`</span></span>

## <a name="migrating-azure-powershell-to-azure-resource-manager"></a><span data-ttu-id="9f552-148">Azure PowerShell migreren naar Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9f552-148">Migrating Azure PowerShell to Azure Resource Manager</span></span>
<span data-ttu-id="9f552-149">Algemene informatie over Azure PowerShell in de modus Azure Resource Manager (ARM) kan worden gevonden op [Azure PowerShell gebruiken met Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="9f552-149">The general information about Azure PowerShell in the Azure Resource Manager (ARM) mode can be found at [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="9f552-150">De ARM van Azure PowerShell-cmdlets kunnen worden geïnstalleerd side-by-side met de ASM-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="9f552-150">The Azure PowerShell ARM cmdlets can be installed side-by-side with the ASM cmdlets.</span></span> <span data-ttu-id="9f552-151">De cmdlets van de twee modi kunnen worden onderscheiden door hun namen.</span><span class="sxs-lookup"><span data-stu-id="9f552-151">The cmdlets from the two modes can be distinguished by their names.</span></span>  <span data-ttu-id="9f552-152">De ARM-modus is *AzureRmHDInsight* in de namen van de cmdlets vergelijken met het *AzureHDInsight* in de ASM-modus.</span><span class="sxs-lookup"><span data-stu-id="9f552-152">The ARM mode has *AzureRmHDInsight* in the cmdlet names comparing to *AzureHDInsight* in the ASM mode.</span></span>  <span data-ttu-id="9f552-153">Bijvoorbeeld: *nieuw AzureRmHDInsightCluster* vs. *Nieuwe AzureHDInsightCluster*.</span><span class="sxs-lookup"><span data-stu-id="9f552-153">For example, *New-AzureRmHDInsightCluster* vs. *New-AzureHDInsightCluster*.</span></span> <span data-ttu-id="9f552-154">Parameters en switches wellicht nieuws namen en er zijn veel nieuwe parameters beschikbaar wanneer u ARM.</span><span class="sxs-lookup"><span data-stu-id="9f552-154">Parameters and switches may have news names, and there are many new parameters available when using ARM.</span></span>  <span data-ttu-id="9f552-155">Meerdere cmdlets vereisen bijvoorbeeld dat een nieuwe switch aangeroepen *- ResourceGroupName*.</span><span class="sxs-lookup"><span data-stu-id="9f552-155">For example, several cmdlets require a new switch called *-ResourceGroupName*.</span></span> 

<span data-ttu-id="9f552-156">Voordat u de HDInsight-cmdlets gebruiken kunt, moet u verbinding maken met uw Azure-account en een nieuwe resourcegroep maken:</span><span class="sxs-lookup"><span data-stu-id="9f552-156">Before you can use the HDInsight cmdlets, you must connect to your Azure account, and create a new resource group:</span></span>

* <span data-ttu-id="9f552-157">Login-AzureRmAccount of [Selecteer AzureRmProfile](https://msdn.microsoft.com/library/mt619310.aspx).</span><span class="sxs-lookup"><span data-stu-id="9f552-157">Login-AzureRmAccount or [Select-AzureRmProfile](https://msdn.microsoft.com/library/mt619310.aspx).</span></span> <span data-ttu-id="9f552-158">Zie [verifiëren van een service-principal met Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md)</span><span class="sxs-lookup"><span data-stu-id="9f552-158">See [Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md)</span></span>
* [<span data-ttu-id="9f552-159">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9f552-159">New-AzureRmResourceGroup</span></span>](https://msdn.microsoft.com/library/mt603739.aspx)

### <a name="renamed-cmdlets"></a><span data-ttu-id="9f552-160">Nieuwe naam cmdlets</span><span class="sxs-lookup"><span data-stu-id="9f552-160">Renamed cmdlets</span></span>
<span data-ttu-id="9f552-161">Overzicht van de HDInsight ASM-cmdlets in Windows PowerShell-console:</span><span class="sxs-lookup"><span data-stu-id="9f552-161">To list the HDInsight ASM cmdlets in Windows PowerShell console:</span></span>

    help *azurermhdinsight*

<span data-ttu-id="9f552-162">De volgende tabel bevat de ASM-cmdlets en hun namen in de ARM-modus:</span><span class="sxs-lookup"><span data-stu-id="9f552-162">The following table lists the ASM cmdlets and their names in the ARM mode:</span></span>

| <span data-ttu-id="9f552-163">ASM-cmdlets</span><span class="sxs-lookup"><span data-stu-id="9f552-163">ASM cmdlets</span></span> | <span data-ttu-id="9f552-164">ARM-cmdlets</span><span class="sxs-lookup"><span data-stu-id="9f552-164">ARM cmdlets</span></span> |
| --- | --- |
| <span data-ttu-id="9f552-165">Add-AzureHDInsightConfigValues</span><span class="sxs-lookup"><span data-stu-id="9f552-165">Add-AzureHDInsightConfigValues</span></span> |[<span data-ttu-id="9f552-166">Voeg AzureRmHDInsightConfigValues</span><span class="sxs-lookup"><span data-stu-id="9f552-166">Add-AzureRmHDInsightConfigValues</span></span>](https://msdn.microsoft.com/library/mt603530.aspx) |
| <span data-ttu-id="9f552-167">Add-AzureHDInsightMetastore</span><span class="sxs-lookup"><span data-stu-id="9f552-167">Add-AzureHDInsightMetastore</span></span> |[<span data-ttu-id="9f552-168">Voeg AzureRmHDInsightMetastore</span><span class="sxs-lookup"><span data-stu-id="9f552-168">Add-AzureRmHDInsightMetastore</span></span>](https://msdn.microsoft.com/library/mt603670.aspx) |
| <span data-ttu-id="9f552-169">Add-AzureHDInsightScriptAction</span><span class="sxs-lookup"><span data-stu-id="9f552-169">Add-AzureHDInsightScriptAction</span></span> |[<span data-ttu-id="9f552-170">Voeg AzureRmHDInsightScriptAction</span><span class="sxs-lookup"><span data-stu-id="9f552-170">Add-AzureRmHDInsightScriptAction</span></span>](https://msdn.microsoft.com/library/mt603527.aspx) |
| <span data-ttu-id="9f552-171">Add-AzureHDInsightStorage</span><span class="sxs-lookup"><span data-stu-id="9f552-171">Add-AzureHDInsightStorage</span></span> |[<span data-ttu-id="9f552-172">Voeg AzureRmHDInsightStorage</span><span class="sxs-lookup"><span data-stu-id="9f552-172">Add-AzureRmHDInsightStorage</span></span>](https://msdn.microsoft.com/library/mt619445.aspx) |
| <span data-ttu-id="9f552-173">Get-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="9f552-173">Get-AzureHDInsightCluster</span></span> |[<span data-ttu-id="9f552-174">Get-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="9f552-174">Get-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619371.aspx) |
| <span data-ttu-id="9f552-175">Get-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="9f552-175">Get-AzureHDInsightJob</span></span> |[<span data-ttu-id="9f552-176">Get-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="9f552-176">Get-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603590.aspx) |
| <span data-ttu-id="9f552-177">Get-AzureHDInsightJobOutput</span><span class="sxs-lookup"><span data-stu-id="9f552-177">Get-AzureHDInsightJobOutput</span></span> |[<span data-ttu-id="9f552-178">Get-AzureRmHDInsightJobOutput</span><span class="sxs-lookup"><span data-stu-id="9f552-178">Get-AzureRmHDInsightJobOutput</span></span>](https://msdn.microsoft.com/library/mt603793.aspx) |
| <span data-ttu-id="9f552-179">Get-AzureHDInsightProperties</span><span class="sxs-lookup"><span data-stu-id="9f552-179">Get-AzureHDInsightProperties</span></span> |[<span data-ttu-id="9f552-180">Get-AzureRmHDInsightProperties</span><span class="sxs-lookup"><span data-stu-id="9f552-180">Get-AzureRmHDInsightProperties</span></span>](https://msdn.microsoft.com/library/mt603546.aspx) |
| <span data-ttu-id="9f552-181">Grant-AzureHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="9f552-181">Grant-AzureHDInsightHttpServicesAccess</span></span> |[<span data-ttu-id="9f552-182">Verleen AzureRmHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="9f552-182">Grant-AzureRmHDInsightHttpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt619407.aspx) |
| <span data-ttu-id="9f552-183">Grant-AzureHdinsightRdpAccess</span><span class="sxs-lookup"><span data-stu-id="9f552-183">Grant-AzureHdinsightRdpAccess</span></span> |[<span data-ttu-id="9f552-184">Verleen AzureRmHDInsightRdpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="9f552-184">Grant-AzureRmHDInsightRdpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt603717.aspx) |
| <span data-ttu-id="9f552-185">Invoke-AzureHDInsightHiveJob</span><span class="sxs-lookup"><span data-stu-id="9f552-185">Invoke-AzureHDInsightHiveJob</span></span> |[<span data-ttu-id="9f552-186">Aanroepen AzureRmHDInsightHiveJob</span><span class="sxs-lookup"><span data-stu-id="9f552-186">Invoke-AzureRmHDInsightHiveJob</span></span>](https://msdn.microsoft.com/library/mt603593.aspx) |
| <span data-ttu-id="9f552-187">New-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="9f552-187">New-AzureHDInsightCluster</span></span> |[<span data-ttu-id="9f552-188">Nieuwe AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="9f552-188">New-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619331.aspx) |
| <span data-ttu-id="9f552-189">New-AzureHDInsightClusterConfig</span><span class="sxs-lookup"><span data-stu-id="9f552-189">New-AzureHDInsightClusterConfig</span></span> |[<span data-ttu-id="9f552-190">Nieuwe AzureRmHDInsightClusterConfig</span><span class="sxs-lookup"><span data-stu-id="9f552-190">New-AzureRmHDInsightClusterConfig</span></span>](https://msdn.microsoft.com/library/mt603700.aspx) |
| <span data-ttu-id="9f552-191">New-AzureHDInsightHiveJobDefinition</span><span class="sxs-lookup"><span data-stu-id="9f552-191">New-AzureHDInsightHiveJobDefinition</span></span> |[<span data-ttu-id="9f552-192">Nieuwe AzureRmHDInsightHiveJobDefinition</span><span class="sxs-lookup"><span data-stu-id="9f552-192">New-AzureRmHDInsightHiveJobDefinition</span></span>](https://msdn.microsoft.com/library/mt619448.aspx) |
| <span data-ttu-id="9f552-193">New-AzureHDInsightMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="9f552-193">New-AzureHDInsightMapReduceJobDefinition</span></span> |[<span data-ttu-id="9f552-194">Nieuwe AzureRmHDInsightMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="9f552-194">New-AzureRmHDInsightMapReduceJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603626.aspx) |
| <span data-ttu-id="9f552-195">New-AzureHDInsightPigJobDefinition</span><span class="sxs-lookup"><span data-stu-id="9f552-195">New-AzureHDInsightPigJobDefinition</span></span> |[<span data-ttu-id="9f552-196">Nieuwe AzureRmHDInsightPigJobDefinition</span><span class="sxs-lookup"><span data-stu-id="9f552-196">New-AzureRmHDInsightPigJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603671.aspx) |
| <span data-ttu-id="9f552-197">New-AzureHDInsightSqoopJobDefinition</span><span class="sxs-lookup"><span data-stu-id="9f552-197">New-AzureHDInsightSqoopJobDefinition</span></span> |[<span data-ttu-id="9f552-198">Nieuwe AzureRmHDInsightSqoopJobDefinition</span><span class="sxs-lookup"><span data-stu-id="9f552-198">New-AzureRmHDInsightSqoopJobDefinition</span></span>](https://msdn.microsoft.com/library/mt608551.aspx) |
| <span data-ttu-id="9f552-199">New-AzureHDInsightStreamingMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="9f552-199">New-AzureHDInsightStreamingMapReduceJobDefinition</span></span> |[<span data-ttu-id="9f552-200">Nieuwe AzureRmHDInsightStreamingMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="9f552-200">New-AzureRmHDInsightStreamingMapReduceJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603626.aspx) |
| <span data-ttu-id="9f552-201">Remove-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="9f552-201">Remove-AzureHDInsightCluster</span></span> |[<span data-ttu-id="9f552-202">Verwijder AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="9f552-202">Remove-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619431.aspx) |
| <span data-ttu-id="9f552-203">Revoke-AzureHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="9f552-203">Revoke-AzureHDInsightHttpServicesAccess</span></span> |[<span data-ttu-id="9f552-204">REVOKE AzureRmHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="9f552-204">Revoke-AzureRmHDInsightHttpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt619375.aspx) |
| <span data-ttu-id="9f552-205">Revoke-AzureHdinsightRdpAccess</span><span class="sxs-lookup"><span data-stu-id="9f552-205">Revoke-AzureHdinsightRdpAccess</span></span> |[<span data-ttu-id="9f552-206">REVOKE AzureRmHDInsightRdpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="9f552-206">Revoke-AzureRmHDInsightRdpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt603523.aspx) |
| <span data-ttu-id="9f552-207">Set-AzureHDInsightClusterSize</span><span class="sxs-lookup"><span data-stu-id="9f552-207">Set-AzureHDInsightClusterSize</span></span> |[<span data-ttu-id="9f552-208">Set-AzureRmHDInsightClusterSize</span><span class="sxs-lookup"><span data-stu-id="9f552-208">Set-AzureRmHDInsightClusterSize</span></span>](https://msdn.microsoft.com/library/mt603513.aspx) |
| <span data-ttu-id="9f552-209">Set-AzureHDInsightDefaultStorage</span><span class="sxs-lookup"><span data-stu-id="9f552-209">Set-AzureHDInsightDefaultStorage</span></span> |[<span data-ttu-id="9f552-210">Set-AzureRmHDInsightDefaultStorage</span><span class="sxs-lookup"><span data-stu-id="9f552-210">Set-AzureRmHDInsightDefaultStorage</span></span>](https://msdn.microsoft.com/library/mt603486.aspx) |
| <span data-ttu-id="9f552-211">Start-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="9f552-211">Start-AzureHDInsightJob</span></span> |[<span data-ttu-id="9f552-212">Start AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="9f552-212">Start-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603798.aspx) |
| <span data-ttu-id="9f552-213">Stop-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="9f552-213">Stop-AzureHDInsightJob</span></span> |[<span data-ttu-id="9f552-214">Stop AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="9f552-214">Stop-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt619424.aspx) |
| <span data-ttu-id="9f552-215">Use-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="9f552-215">Use-AzureHDInsightCluster</span></span> |[<span data-ttu-id="9f552-216">Gebruik AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="9f552-216">Use-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619442.aspx) |
| <span data-ttu-id="9f552-217">Wait-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="9f552-217">Wait-AzureHDInsightJob</span></span> |[<span data-ttu-id="9f552-218">Wacht AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="9f552-218">Wait-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603834.aspx) |

### <a name="new-cmdlets"></a><span data-ttu-id="9f552-219">Nieuwe cmdLets</span><span class="sxs-lookup"><span data-stu-id="9f552-219">New cmdlets</span></span>
<span data-ttu-id="9f552-220">Hieronder vindt u de nieuwe cmdlets die alleen beschikbaar in de ARM-modus.</span><span class="sxs-lookup"><span data-stu-id="9f552-220">The following are the new cmdlets that are only available in the ARM mode.</span></span> 

<span data-ttu-id="9f552-221">**Scriptactie verwante cmdlets:**</span><span class="sxs-lookup"><span data-stu-id="9f552-221">**Script action related cmdlets:**</span></span>

* <span data-ttu-id="9f552-222">**Get-AzureRmHDInsightPersistedScriptAction**: opgehaald van de persistente scriptacties voor een cluster en worden ze weergegeven in chronologische volgorde of details voor een opgegeven persistente scriptacties actie opgehaald.</span><span class="sxs-lookup"><span data-stu-id="9f552-222">**Get-AzureRmHDInsightPersistedScriptAction**: Gets the persisted script actions for a cluster and lists them in chronological order, or gets details for a specified persisted script action.</span></span> 
* <span data-ttu-id="9f552-223">**Get-AzureRmHDInsightScriptActionHistory**: opgehaald van de geschiedenis van de scriptactie voor een cluster en details van een eerder uitgevoerde scriptactie opgehaald, wordt weergegeven in omgekeerde volgorde.</span><span class="sxs-lookup"><span data-stu-id="9f552-223">**Get-AzureRmHDInsightScriptActionHistory**: Gets the script action history for a cluster and lists it in reverse chronological order, or gets details of a previously executed script action.</span></span> 
* <span data-ttu-id="9f552-224">**Verwijder AzureRmHDInsightPersistedScriptAction**: Hiermee verwijdert u een actie persistent script van een HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="9f552-224">**Remove-AzureRmHDInsightPersistedScriptAction**: Removes a persisted script action from an HDInsight cluster.</span></span>
* <span data-ttu-id="9f552-225">**Set-AzureRmHDInsightPersistedScriptAction**: Hiermee stelt u een eerder uitgevoerde scriptactie moet een persistent script in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="9f552-225">**Set-AzureRmHDInsightPersistedScriptAction**: Sets a previously executed script action to be a persisted script action.</span></span>
* <span data-ttu-id="9f552-226">**Indienen AzureRmHDInsightScriptAction**: een nieuwe scriptactie naar een Azure HDInsight-cluster worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="9f552-226">**Submit-AzureRmHDInsightScriptAction**: Submits a new script action to an Azure HDInsight cluster.</span></span> 

<span data-ttu-id="9f552-227">Zie voor meer informatie over het gebruiksinformatie [aanpassen Linux gebaseerde HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="9f552-227">For additional usage information, see [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="9f552-228">**Clsuter identiteit verwante cmdlets:**</span><span class="sxs-lookup"><span data-stu-id="9f552-228">**Clsuter identity related cmdlets:**</span></span>

* <span data-ttu-id="9f552-229">**Voeg AzureRmHDInsightClusterIdentity**: de identiteit van een cluster toegevoegd aan een configuratieobject cluster zodat het HDInsight-cluster, toegang Azure Data Lake Stores tot hebben.</span><span class="sxs-lookup"><span data-stu-id="9f552-229">**Add-AzureRmHDInsightClusterIdentity**: Adds a cluster identity to a cluster configuration object so that the HDInsight cluster can access Azure Data Lake Stores.</span></span> <span data-ttu-id="9f552-230">Zie [een HDInsight-cluster maken met Data Lake Store met Azure PowerShell](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="9f552-230">See [Create an HDInsight cluster with Data Lake Store using Azure PowerShell](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md).</span></span>

### <a name="examples"></a><span data-ttu-id="9f552-231">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="9f552-231">Examples</span></span>
<span data-ttu-id="9f552-232">**Cluster maken**</span><span class="sxs-lookup"><span data-stu-id="9f552-232">**Create cluster**</span></span>

<span data-ttu-id="9f552-233">Oude opdracht (ASM):</span><span class="sxs-lookup"><span data-stu-id="9f552-233">Old command (ASM):</span></span> 

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

<span data-ttu-id="9f552-234">Nieuwe opdracht (ARM):</span><span class="sxs-lookup"><span data-stu-id="9f552-234">New command (ARM):</span></span>

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


<span data-ttu-id="9f552-235">**Cluster verwijderen**</span><span class="sxs-lookup"><span data-stu-id="9f552-235">**Delete cluster**</span></span>

<span data-ttu-id="9f552-236">Oude opdracht (ASM):</span><span class="sxs-lookup"><span data-stu-id="9f552-236">Old command (ASM):</span></span>

    Remove-AzureHDInsightCluster -name $clusterName 

<span data-ttu-id="9f552-237">Nieuwe opdracht (ARM):</span><span class="sxs-lookup"><span data-stu-id="9f552-237">New command (ARM):</span></span>

    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName 

<span data-ttu-id="9f552-238">**Lijst met cluster**</span><span class="sxs-lookup"><span data-stu-id="9f552-238">**List cluster**</span></span>

<span data-ttu-id="9f552-239">Oude opdracht (ASM):</span><span class="sxs-lookup"><span data-stu-id="9f552-239">Old command (ASM):</span></span>

    Get-AzureHDInsightCluster

<span data-ttu-id="9f552-240">Nieuwe opdracht (ARM):</span><span class="sxs-lookup"><span data-stu-id="9f552-240">New command (ARM):</span></span>

    Get-AzureRmHDInsightCluster 

<span data-ttu-id="9f552-241">**Cluster weergeven**</span><span class="sxs-lookup"><span data-stu-id="9f552-241">**Show cluster**</span></span>

<span data-ttu-id="9f552-242">Oude opdracht (ASM):</span><span class="sxs-lookup"><span data-stu-id="9f552-242">Old command (ASM):</span></span>

    Get-AzureHDInsightCluster -Name $clusterName

<span data-ttu-id="9f552-243">Nieuwe opdracht (ARM):</span><span class="sxs-lookup"><span data-stu-id="9f552-243">New command (ARM):</span></span>

    Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -clusterName $clusterName


#### <a name="other-samples"></a><span data-ttu-id="9f552-244">Andere voorbeelden</span><span class="sxs-lookup"><span data-stu-id="9f552-244">Other samples</span></span>
* [<span data-ttu-id="9f552-245">HDInsight-clusters maken</span><span class="sxs-lookup"><span data-stu-id="9f552-245">Create HDInsight clusters</span></span>](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
* [<span data-ttu-id="9f552-246">Indienen van Hive-taken</span><span class="sxs-lookup"><span data-stu-id="9f552-246">Submit Hive jobs</span></span>](hdinsight-hadoop-use-hive-powershell.md)
* [<span data-ttu-id="9f552-247">Pig-taken verzenden</span><span class="sxs-lookup"><span data-stu-id="9f552-247">Submit Pig jobs</span></span>](hdinsight-hadoop-use-pig-powershell.md)
* [<span data-ttu-id="9f552-248">Sqoop taken verzenden</span><span class="sxs-lookup"><span data-stu-id="9f552-248">Submit Sqoop jobs</span></span>](hdinsight-hadoop-use-sqoop-powershell.md)

## <a name="migrating-to-the-arm-based-hdinsight-net-sdk"></a><span data-ttu-id="9f552-249">Migreren naar de HDInsight op basis van ARM .NET SDK</span><span class="sxs-lookup"><span data-stu-id="9f552-249">Migrating to the ARM-based HDInsight .NET SDK</span></span>
<span data-ttu-id="9f552-250">De Azure Service Management-gebaseerde [(ASM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt416619.aspx) is nu verouderd.</span><span class="sxs-lookup"><span data-stu-id="9f552-250">The Azure Service Management-based [(ASM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt416619.aspx) is now deprecated.</span></span> <span data-ttu-id="9f552-251">U wordt aangeraden gebruik van de Azure Resource Management-gebaseerde [(ARM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt271028.aspx).</span><span class="sxs-lookup"><span data-stu-id="9f552-251">You are encouraged to use the Azure Resource Management-based [(ARM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt271028.aspx).</span></span> <span data-ttu-id="9f552-252">De volgende HDInsight op basis van de ASM-pakketten worden afgeschaft.</span><span class="sxs-lookup"><span data-stu-id="9f552-252">The following ASM-based HDInsight packages are being deprecated.</span></span>

* `Microsoft.WindowsAzure.Management.HDInsight`
* `Microsoft.Hadoop.Client`

<span data-ttu-id="9f552-253">Deze sectie bevat koppelingen naar meer informatie over het uitvoeren van bepaalde taken met de SDK op basis van ARM.</span><span class="sxs-lookup"><span data-stu-id="9f552-253">This section provides pointers to more information on how to perform certain tasks using the ARM-based SDK.</span></span>

| <span data-ttu-id="9f552-254">Hoe... met behulp van de HDInsight op basis van ARM SDK</span><span class="sxs-lookup"><span data-stu-id="9f552-254">How to... using the ARM-based HDInsight SDK</span></span> | <span data-ttu-id="9f552-255">Koppelingen</span><span class="sxs-lookup"><span data-stu-id="9f552-255">Links</span></span> |
| --- | --- |
| <span data-ttu-id="9f552-256">Maken van HDInsight-clusters met .NET SDK</span><span class="sxs-lookup"><span data-stu-id="9f552-256">Create HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="9f552-257">Zie [HDInsight-clusters maken met .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="9f552-257">See [Create HDInsight clusters using .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="9f552-258">Aanpassen van een cluster met de scriptactie met .NET SDK</span><span class="sxs-lookup"><span data-stu-id="9f552-258">Customize a cluster using Script Action with .NET SDK</span></span> |<span data-ttu-id="9f552-259">Zie [aanpassen HDInsight Linux-clusters met behulp van de scriptactie](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action)</span><span class="sxs-lookup"><span data-stu-id="9f552-259">See [Customize HDInsight Linux clusters using Script Action](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action)</span></span> |
| <span data-ttu-id="9f552-260">Verifiëren van toepassingen die gebruikmaken van Azure Active Directory interactief met .NET SDK</span><span class="sxs-lookup"><span data-stu-id="9f552-260">Authenticate applications interactively using Azure Active Directory with .NET SDK</span></span> |<span data-ttu-id="9f552-261">Zie [uitvoeren Hive-query's met .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="9f552-261">See [Run Hive queries using .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span> <span data-ttu-id="9f552-262">Het volgende codefragment in dit artikel maakt gebruik van de aanpak voor interactieve verificatie.</span><span class="sxs-lookup"><span data-stu-id="9f552-262">The code snippet in this article uses the interactive authentication approach.</span></span> |
| <span data-ttu-id="9f552-263">Verifiëren van toepassingen die gebruikmaken van Azure Active Directory niet-interactief met .NET SDK</span><span class="sxs-lookup"><span data-stu-id="9f552-263">Authenticate applications non-interactively using Azure Active Directory with .NET SDK</span></span> |<span data-ttu-id="9f552-264">Zie [niet-interactieve toepassingen voor HDInsight maken](hdinsight-create-non-interactive-authentication-dotnet-applications.md)</span><span class="sxs-lookup"><span data-stu-id="9f552-264">See [Create non-interactive applications for HDInsight](hdinsight-create-non-interactive-authentication-dotnet-applications.md)</span></span> |
| <span data-ttu-id="9f552-265">Verzenden van een Hive-taak met .NET SDK</span><span class="sxs-lookup"><span data-stu-id="9f552-265">Submit a Hive job using .NET SDK</span></span> |<span data-ttu-id="9f552-266">Zie [indienen Hive-taken](hdinsight-hadoop-use-hive-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="9f552-266">See [Submit Hive jobs](hdinsight-hadoop-use-hive-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="9f552-267">Verzenden van een Pig-taak met .NET SDK</span><span class="sxs-lookup"><span data-stu-id="9f552-267">Submit a Pig job using .NET SDK</span></span> |<span data-ttu-id="9f552-268">Zie [verzenden van Pig-taken](hdinsight-hadoop-use-pig-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="9f552-268">See [Submit Pig jobs](hdinsight-hadoop-use-pig-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="9f552-269">Verzenden van een Sqoop taak met .NET SDK</span><span class="sxs-lookup"><span data-stu-id="9f552-269">Submit a Sqoop job using .NET SDK</span></span> |<span data-ttu-id="9f552-270">Zie [Sqoop verzenden van taken](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="9f552-270">See [Submit Sqoop jobs](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="9f552-271">Lijst met HDInsight-clusters met .NET SDK</span><span class="sxs-lookup"><span data-stu-id="9f552-271">List HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="9f552-272">Zie [lijst HDInsight-clusters](hdinsight-administer-use-dotnet-sdk.md#list-clusters)</span><span class="sxs-lookup"><span data-stu-id="9f552-272">See [List HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#list-clusters)</span></span> |
| <span data-ttu-id="9f552-273">Schalen van HDInsight-clusters met .NET SDK</span><span class="sxs-lookup"><span data-stu-id="9f552-273">Scale HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="9f552-274">Zie [Scale HDInsight-clusters](hdinsight-administer-use-dotnet-sdk.md#scale-clusters)</span><span class="sxs-lookup"><span data-stu-id="9f552-274">See [Scale HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#scale-clusters)</span></span> |
| <span data-ttu-id="9f552-275">GRANT/revoke toegang tot HDInsight-clusters met .NET SDK</span><span class="sxs-lookup"><span data-stu-id="9f552-275">Grant/revoke access to HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="9f552-276">Zie [Grant/revoke toegang tot HDInsight-clusters](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access)</span><span class="sxs-lookup"><span data-stu-id="9f552-276">See [Grant/revoke access to HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access)</span></span> |
| <span data-ttu-id="9f552-277">HTTP-gebruikersreferenties updaten voor HDInsight-clusters met .NET SDK</span><span class="sxs-lookup"><span data-stu-id="9f552-277">Update HTTP user credentials for HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="9f552-278">Zie [Update HTTP gebruikersreferenties voor HDInsight-clusters](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials)</span><span class="sxs-lookup"><span data-stu-id="9f552-278">See [Update HTTP user credentials for HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials)</span></span> |
| <span data-ttu-id="9f552-279">Het standaardopslagaccount vinden voor HDInsight-clusters met .NET SDK</span><span class="sxs-lookup"><span data-stu-id="9f552-279">Find the default storage account for HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="9f552-280">Zie [vinden van het standaardopslagaccount voor HDInsight-clusters](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account)</span><span class="sxs-lookup"><span data-stu-id="9f552-280">See [Find the default storage account for HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account)</span></span> |
| <span data-ttu-id="9f552-281">HDInsight-clusters met .NET SDK verwijderen</span><span class="sxs-lookup"><span data-stu-id="9f552-281">Delete HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="9f552-282">Zie [verwijderen HDInsight-clusters](hdinsight-administer-use-dotnet-sdk.md#delete-clusters)</span><span class="sxs-lookup"><span data-stu-id="9f552-282">See [Delete HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#delete-clusters)</span></span> |

### <a name="examples"></a><span data-ttu-id="9f552-283">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="9f552-283">Examples</span></span>
<span data-ttu-id="9f552-284">Hieronder volgen enkele voorbeelden van hoe een bewerking is uitgevoerd met behulp van de SDK op basis van ASM en de equivalente codefragment voor de SDK op basis van ARM.</span><span class="sxs-lookup"><span data-stu-id="9f552-284">Following are some examples on how an operation is performed using the ASM-based SDK and the equivalent code snippet for the ARM-based SDK.</span></span>

<span data-ttu-id="9f552-285">**Maken van een cluster CRUD-client**</span><span class="sxs-lookup"><span data-stu-id="9f552-285">**Creating a cluster CRUD client**</span></span>

* <span data-ttu-id="9f552-286">Vorige opdracht (ASM)</span><span class="sxs-lookup"><span data-stu-id="9f552-286">Old command (ASM)</span></span>
  
        //Certificate auth
        //This logs the application in using a subscription administration certificate, which is not offered in Azure Resource Manager (ARM)
  
        const string subid = "454467d4-60ca-4dfd-a556-216eeeeeeee1";
        var cred = new HDInsightCertificateCredential(new Guid(subid), new X509Certificate2(@"path\to\certificate.cer"));
        var client = HDInsightClient.Connect(cred);
* <span data-ttu-id="9f552-287">Nieuwe opdracht (ARM) (Service principal autorisatie)</span><span class="sxs-lookup"><span data-stu-id="9f552-287">New command (ARM) (Service principal authorization)</span></span>
  
        //Service principal auth
        //This will log the application in as itself, rather than on behalf of a specific user.
        //For details, including how to set up the application, see:
        //   https://azure.microsoft.com/en-us/documentation/articles/hdinsight-create-non-interactive-authentication-dotnet-applications/
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.ServicePrincipal, Id = clientId };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, tenantId, secretKey, ShowDialog.Never).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);
* <span data-ttu-id="9f552-288">Nieuwe opdracht (ARM) (gebruikersautorisatie)</span><span class="sxs-lookup"><span data-stu-id="9f552-288">New command (ARM) (User authorization)</span></span>
  
        //User auth
        //This will log the application in on behalf of the user.
        //The end-user will see a login popup.
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.User, Id = username };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, AuthenticationFactory.CommonAdTenant, password, ShowDialog.Auto).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);

<span data-ttu-id="9f552-289">**Maken van een cluster**</span><span class="sxs-lookup"><span data-stu-id="9f552-289">**Creating a cluster**</span></span>

* <span data-ttu-id="9f552-290">Vorige opdracht (ASM)</span><span class="sxs-lookup"><span data-stu-id="9f552-290">Old command (ASM)</span></span>
  
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
* <span data-ttu-id="9f552-291">Nieuwe opdracht (ARM)</span><span class="sxs-lookup"><span data-stu-id="9f552-291">New command (ARM)</span></span>
  
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

<span data-ttu-id="9f552-292">**HTTP-toegang inschakelen**</span><span class="sxs-lookup"><span data-stu-id="9f552-292">**Enabling HTTP access**</span></span>

* <span data-ttu-id="9f552-293">Vorige opdracht (ASM)</span><span class="sxs-lookup"><span data-stu-id="9f552-293">Old command (ASM)</span></span>
  
        client.EnableHttp(dnsName, "West US", "admin", "*******");
* <span data-ttu-id="9f552-294">Nieuwe opdracht (ARM)</span><span class="sxs-lookup"><span data-stu-id="9f552-294">New command (ARM)</span></span>
  
        var httpParams = new HttpSettingsParameters
        {
               HttpUserEnabled = true,
               HttpUsername = "admin",
               HttpPassword = "*******",
        };
        client.Clusters.ConfigureHttpSettings(resourceGroup, dnsname, httpParams);

<span data-ttu-id="9f552-295">**Verwijderen van een cluster**</span><span class="sxs-lookup"><span data-stu-id="9f552-295">**Deleting a cluster**</span></span>

* <span data-ttu-id="9f552-296">Vorige opdracht (ASM)</span><span class="sxs-lookup"><span data-stu-id="9f552-296">Old command (ASM)</span></span>
  
        client.DeleteCluster(dnsName);
* <span data-ttu-id="9f552-297">Nieuwe opdracht (ARM)</span><span class="sxs-lookup"><span data-stu-id="9f552-297">New command (ARM)</span></span>
  
        client.Clusters.Delete(resourceGroup, dnsname);

