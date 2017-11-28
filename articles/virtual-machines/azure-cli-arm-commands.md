---
title: aaaAzure CLI-opdrachten in de modus Resource Manager | Microsoft Docs
description: Azure opdrachtregelinterface (CLI) opdrachten toomanage resources Hallo Resource Manager-implementatiemodel
services: virtual-machines-linux,virtual-machines-windows,virtual-network,mobile-services,cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: be37da5b-72fe-41a1-9fa0-8937b69464ec
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: command-line-interface
ms.devlang: na
ms.topic: article
ms.date: 04/18/2017
ms.author: danlep
ms.openlocfilehash: 49539655f7b24511e219f982819bcb59c9305d33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-commands-in-resource-manager-mode"></a><span data-ttu-id="e9e77-103">Azure CLI-opdrachten in de modus Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e9e77-103">Azure CLI commands in Resource Manager mode</span></span>
<span data-ttu-id="e9e77-104">Dit artikel bevat syntaxis en opties voor Azure-opdrachtregelinterface (CLI) opdrachten dat u vaak zou toocreate gebruiken en beheren van Azure-resources in hello Azure Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="e9e77-104">This article provides syntax and options for Azure command-line interface (CLI) commands you'd commonly use toocreate and manage Azure resources in hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="e9e77-105">U toegang tot deze opdrachten door Hallo CLI in de modus Resource Manager (arm).</span><span class="sxs-lookup"><span data-stu-id="e9e77-105">You access these commands by running hello CLI in Resource Manager (arm) mode.</span></span> <span data-ttu-id="e9e77-106">Dit is niet een volledig overzicht en uw versie van de CLI kan enigszins verschillen opdrachten of parameters weergeven.</span><span class="sxs-lookup"><span data-stu-id="e9e77-106">This is not a complete reference, and your CLI version may show slightly different commands or parameters.</span></span> <span data-ttu-id="e9e77-107">Zie voor een algemeen overzicht van Azure-resources en resourcegroepen [overzicht van Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e9e77-107">For a general overview of Azure resources and resource groups, see [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>  

> [!NOTE]
> <span data-ttu-id="e9e77-108">Dit artikel laat zien Resource Manager opdrachten in de modus in hello Azure CLI, Azure CLI 1.0 soms genoemd.</span><span class="sxs-lookup"><span data-stu-id="e9e77-108">This article shows Resource Manager mode commands in hello Azure CLI, sometimes called Azure CLI 1.0.</span></span> <span data-ttu-id="e9e77-109">toowork in Hallo Resource Manager-model, u kunt ook Hallo [Azure CLI 2.0](/cli/azure/install-az-cli2), de volgende generatie meerdere platforms CLI.</span><span class="sxs-lookup"><span data-stu-id="e9e77-109">toowork in hello Resource Manager model, you can also try hello [Azure CLI 2.0](/cli/azure/install-az-cli2), our next generation multi-platform CLI.</span></span>
><span data-ttu-id="e9e77-110">Meer informatie over Hallo [oude en nieuwe Azure CLIs](/cli/azure/old-and-new-clis).</span><span class="sxs-lookup"><span data-stu-id="e9e77-110">Find out more about hello [old and new Azure CLIs](/cli/azure/old-and-new-clis).</span></span>
>

<span data-ttu-id="e9e77-111">tooget gestart, eerst [hello Azure CLI installeren](../cli-install-nodejs.md) en [tooyour Azure-abonnement verbinden](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="e9e77-111">tooget started, first [install hello Azure CLI](../cli-install-nodejs.md) and [connect tooyour Azure subscription](../xplat-cli-connect.md).</span></span>

<span data-ttu-id="e9e77-112">Typ voor de huidige opdrachtsyntaxis en -opties op de opdrachtregel Hallo in de modus Resource Manager `azure help` of toodisplay help voor een specifieke opdracht `azure help [command]`.</span><span class="sxs-lookup"><span data-stu-id="e9e77-112">For current command syntax and options at hello command line in Resource Manager mode, type `azure help` or, toodisplay help for a specific command, `azure help [command]`.</span></span> <span data-ttu-id="e9e77-113">CLI-voorbeelden in Hallo documentatie ook vinden voor het maken en beheren van specifieke Azure-services.</span><span class="sxs-lookup"><span data-stu-id="e9e77-113">Also find CLI examples in hello documentation for creating and managing specific Azure services.</span></span>

<span data-ttu-id="e9e77-114">Optionele parameters staan tussen vierkante haken (bijvoorbeeld `[parameter]`).</span><span class="sxs-lookup"><span data-stu-id="e9e77-114">Optional parameters are shown in square brackets (for example, `[parameter]`).</span></span> <span data-ttu-id="e9e77-115">Alle andere parameters zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="e9e77-115">All other parameters are required.</span></span>

<span data-ttu-id="e9e77-116">In aanvulling toocommand-specifieke optionele parameters beschreven, zijn er drie optionele parameters die gebruikt toodisplay worden kunnen gedetailleerde output zoals opties voor aanvraag- en statuscodes.</span><span class="sxs-lookup"><span data-stu-id="e9e77-116">In addition toocommand-specific optional parameters documented here, there are three optional parameters that can be used toodisplay detailed output such as request options and status codes.</span></span> <span data-ttu-id="e9e77-117">Hallo `-v` parameter biedt uitgebreide uitvoer en Hallo `-vv` parameter biedt nog meer gedetailleerde uitgebreide uitvoer.</span><span class="sxs-lookup"><span data-stu-id="e9e77-117">hello `-v` parameter provides verbose output, and hello `-vv` parameter provides even more detailed verbose output.</span></span> <span data-ttu-id="e9e77-118">Hallo `--json` optie levert resultaat Hallo onbewerkte json-indeling.</span><span class="sxs-lookup"><span data-stu-id="e9e77-118">hello `--json` option outputs hello result in raw json format.</span></span>

## <a name="setting-hello-resource-manager-mode"></a><span data-ttu-id="e9e77-119">Instelling Hallo Resource Manager-modus</span><span class="sxs-lookup"><span data-stu-id="e9e77-119">Setting hello Resource Manager mode</span></span>
<span data-ttu-id="e9e77-120">Gebruik hello opdracht tooenable Azure CLI Resource Manager-modusopdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="e9e77-120">Use hello following command tooenable Azure CLI Resource Manager mode commands.</span></span>

    azure config mode arm

> [!NOTE]
> <span data-ttu-id="e9e77-121">Hallo CLI van Azure Resource Manager en Azure Service Management modus elkaar wederzijds uit.</span><span class="sxs-lookup"><span data-stu-id="e9e77-121">hello CLI's Azure Resource Manager mode and Azure Service Management mode are mutually exclusive.</span></span> <span data-ttu-id="e9e77-122">Dat wil zeggen, resources die zijn gemaakt in de modus voor één kunnen niet worden beheerd vanaf Hallo andere modus.</span><span class="sxs-lookup"><span data-stu-id="e9e77-122">That is, resources created in one mode cannot be managed from hello other mode.</span></span>
> 
> 

## <a name="azure-account-manage-your-account-information"></a><span data-ttu-id="e9e77-123">Azure-account: gegevens over uw account beheren</span><span class="sxs-lookup"><span data-stu-id="e9e77-123">azure account: Manage your account information</span></span>
<span data-ttu-id="e9e77-124">De informatie van uw Azure-abonnement wordt gebruikt door Hallo hulpprogramma tooconnect tooyour account.</span><span class="sxs-lookup"><span data-stu-id="e9e77-124">Your Azure subscription information is used by hello tool tooconnect tooyour account.</span></span>

<span data-ttu-id="e9e77-125">**Lijst Hallo geïmporteerd abonnementen**</span><span class="sxs-lookup"><span data-stu-id="e9e77-125">**List hello imported subscriptions**</span></span>

    account list [options]

<span data-ttu-id="e9e77-126">**Details weergeven over een abonnement op**</span><span class="sxs-lookup"><span data-stu-id="e9e77-126">**Show details about a subscription**</span></span>  

    account show [options] [subscriptionNameOrId]

<span data-ttu-id="e9e77-127">**Het huidige abonnement Hallo instellen**</span><span class="sxs-lookup"><span data-stu-id="e9e77-127">**Set hello current subscription**</span></span>

    account set [options] <subscriptionNameOrId>

<span data-ttu-id="e9e77-128">**Verwijderen van een abonnement of de omgeving of wis dan alle Hallo opgeslagen en de omgeving info**</span><span class="sxs-lookup"><span data-stu-id="e9e77-128">**Remove a subscription or environment, or clear all of hello stored account and environment info**</span></span>  

    account clear [options]

<span data-ttu-id="e9e77-129">**Opdrachten toomanage uw account-omgeving**</span><span class="sxs-lookup"><span data-stu-id="e9e77-129">**Commands toomanage your account environment**</span></span>  

    account env list [options]
    account env show [options] [environment]
    account env add [options] [environment]
    account env set [options] [environment]
    account env delete [options] [environment]

## <a name="azure-ad-commands-toodisplay-active-directory-objects"></a><span data-ttu-id="e9e77-130">Azure ad: opdrachten toodisplay Active Directory-objecten</span><span class="sxs-lookup"><span data-stu-id="e9e77-130">azure ad: Commands toodisplay Active Directory objects</span></span>
<span data-ttu-id="e9e77-131">**Opdrachten toodisplay active directory-toepassingen**</span><span class="sxs-lookup"><span data-stu-id="e9e77-131">**Commands toodisplay active directory applications**</span></span>

    ad app create [options]
    ad app delete [options] <object-id>

<span data-ttu-id="e9e77-132">**Opdrachten toodisplay active directory-groepen**</span><span class="sxs-lookup"><span data-stu-id="e9e77-132">**Commands toodisplay active directory groups**</span></span>

    ad group list [options]
    ad group show [options]

<span data-ttu-id="e9e77-133">**Opdrachten tooprovide een active directory-sub groeps- of -info**</span><span class="sxs-lookup"><span data-stu-id="e9e77-133">**Commands tooprovide an active directory sub group or member info**</span></span>

    ad group member list [options] [objectId]

<span data-ttu-id="e9e77-134">**Opdrachten toodisplay active directory service-principals**</span><span class="sxs-lookup"><span data-stu-id="e9e77-134">**Commands toodisplay active directory service principals**</span></span>

    ad sp list [options]
    ad sp show [options]
    ad sp create [options] <application-id>
    ad sp delete [options] <object-id>

<span data-ttu-id="e9e77-135">**Opdrachten toodisplay active directory-gebruikers**</span><span class="sxs-lookup"><span data-stu-id="e9e77-135">**Commands toodisplay active directory users**</span></span>

    ad user list [options]
    ad user show [options]

## <a name="azure-availset-commands-toomanage-your-availability-sets"></a><span data-ttu-id="e9e77-136">Azure availset: opdrachten toomanage uw beschikbaarheidssets</span><span class="sxs-lookup"><span data-stu-id="e9e77-136">azure availset: commands toomanage your availability sets</span></span>
<span data-ttu-id="e9e77-137">**Hiermee maakt u een beschikbaarheidsset binnen een resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="e9e77-137">**Creates an availability set within a resource group**</span></span>

    availset create [options] <resource-group> <name> <location> [tags]

<span data-ttu-id="e9e77-138">**Een lijst met Hallo beschikbaarheidssets binnen een resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="e9e77-138">**Lists hello availability sets within a resource group**</span></span>

    availset list [options] <resource-group>

<span data-ttu-id="e9e77-139">**Een beschikbaarheidsset binnen een resourcegroep opgehaald**</span><span class="sxs-lookup"><span data-stu-id="e9e77-139">**Gets one availability set within a resource group**</span></span>

    availset show [options] <resource-group> <name>

<span data-ttu-id="e9e77-140">**Hiermee verwijdert u één beschikbaarheidsset binnen een resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="e9e77-140">**Deletes one availability set within a resource group**</span></span>

    availset delete [options] <resource-group> <name>

## <a name="azure-config-commands-toomanage-your-local-settings"></a><span data-ttu-id="e9e77-141">Azure config: toomanage-opdrachten uit uw lokale instellingen</span><span class="sxs-lookup"><span data-stu-id="e9e77-141">azure config: commands toomanage your local settings</span></span>
<span data-ttu-id="e9e77-142">**Configuratie-instellingen van lijst met Azure CLI**</span><span class="sxs-lookup"><span data-stu-id="e9e77-142">**List Azure CLI configuration settings**</span></span>

    config list [options]

<span data-ttu-id="e9e77-143">**Een configuratie-instelling niet verwijderen**</span><span class="sxs-lookup"><span data-stu-id="e9e77-143">**Delete a config setting**</span></span>

    config delete [options] <name>

<span data-ttu-id="e9e77-144">**Bijwerken van een configuratie-instelling**</span><span class="sxs-lookup"><span data-stu-id="e9e77-144">**Update a config setting**</span></span>

    config set <name> <value>

<span data-ttu-id="e9e77-145">**Sets hello Azure CLI-modus tooeither werken `arm` of`asm`**</span><span class="sxs-lookup"><span data-stu-id="e9e77-145">**Sets hello Azure CLI working mode tooeither `arm` or `asm`**</span></span>

    config mode [options] <modename>


## <a name="azure-feature-commands-toomanage-account-features"></a><span data-ttu-id="e9e77-146">functie van Azure: opdrachten toomanage account functies</span><span class="sxs-lookup"><span data-stu-id="e9e77-146">azure feature: commands toomanage account features</span></span>
<span data-ttu-id="e9e77-147">**Lijst van alle functies die beschikbaar zijn voor uw abonnement**</span><span class="sxs-lookup"><span data-stu-id="e9e77-147">**List all features available for your subscription**</span></span>

    feature list [options]

<span data-ttu-id="e9e77-148">**Bevat een functie**</span><span class="sxs-lookup"><span data-stu-id="e9e77-148">**Shows a feature**</span></span>

    feature show [options] <providerName> <featureName>

<span data-ttu-id="e9e77-149">**Een voorbeeld functie van een resourceprovider geregistreerd**</span><span class="sxs-lookup"><span data-stu-id="e9e77-149">**Registers a previewed feature of a resource provider**</span></span>

    feature register [options] <providerName> <featureName>

## <a name="azure-group-commands-toomanage-your-resource-groups"></a><span data-ttu-id="e9e77-150">Azure-groep: opdrachten toomanage uw resourcegroepen</span><span class="sxs-lookup"><span data-stu-id="e9e77-150">azure group: Commands toomanage your resource groups</span></span>
<span data-ttu-id="e9e77-151">**Maakt een resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="e9e77-151">**Creates a resource group**</span></span>

    group create [options] <name> <location>

<span data-ttu-id="e9e77-152">**Set labels tooa resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="e9e77-152">**Set tags tooa resource group**</span></span>

    group set [options] <name> <tags>

<span data-ttu-id="e9e77-153">**Hiermee verwijdert u een resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="e9e77-153">**Deletes a resource group**</span></span>

    group delete [options] <name>

<span data-ttu-id="e9e77-154">**Een lijst met resourcegroepen Hallo voor uw abonnement**</span><span class="sxs-lookup"><span data-stu-id="e9e77-154">**Lists hello resource groups for your subscription**</span></span>

    group list [options]

<span data-ttu-id="e9e77-155">**Ziet u een resourcegroep voor uw abonnement**</span><span class="sxs-lookup"><span data-stu-id="e9e77-155">**Shows a resource group for your subscription**</span></span>

    group show [options] <name>

<span data-ttu-id="e9e77-156">**Opdrachten toomanage resource groep zich aanmeldt**</span><span class="sxs-lookup"><span data-stu-id="e9e77-156">**Commands toomanage resource group logs**</span></span>

    group log show [options] [name]

<span data-ttu-id="e9e77-157">**Opdrachten toomanage uw implementatie in een resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="e9e77-157">**Commands toomanage your deployment in a resource group**</span></span>

    group deployment create [options] [resource-group] [name]
    group deployment list [options] <resource-group> [state]
    group deployment show [options] <resource-group> [deployment-name]
    group deployment stop [options] <resource-group> [deployment-name]

<span data-ttu-id="e9e77-158">**Opdrachten toomanage uw lokaal of galerie resource group-sjabloon**</span><span class="sxs-lookup"><span data-stu-id="e9e77-158">**Commands toomanage your local or gallery resource group template**</span></span>

    group template list [options]
    group template show [options] <name>
    group template download [options] [name] [file]
    group template validate [options] <resource-group>

## <a name="azure-hdinsight-commands-toomanage-your-hdinsight-clusters"></a><span data-ttu-id="e9e77-159">Azure hdinsight: opdrachten toomanage uw HDInsight-clusters</span><span class="sxs-lookup"><span data-stu-id="e9e77-159">azure hdinsight: Commands toomanage your HDInsight clusters</span></span>
<span data-ttu-id="e9e77-160">**Opdrachten toocreate of tooa cluster configuratiebestand toevoegen**</span><span class="sxs-lookup"><span data-stu-id="e9e77-160">**Commands toocreate or add tooa cluster configuration file**</span></span>

    hdinsight config create [options] <configFilePath> <overwrite>
    hdinsight config add-config-values [options] <configFilePath>
    hdinsight config add-script-action [options] <configFilePath>

<span data-ttu-id="e9e77-161">Voorbeeld: Maak een configuratiebestand met een script actie toorun bij het maken van een cluster.</span><span class="sxs-lookup"><span data-stu-id="e9e77-161">Example: Create a configuration file that contains a script action toorun when creating a cluster.</span></span>

    hdinsight config create "C:\myFiles\configFile.config"
    hdinsight config add-script-action --configFilePath "C:\myFiles\configFile.config" --nodeType HeadNode --uri <scriptActionURI> --name myScriptAction --parameters "-param value"

<span data-ttu-id="e9e77-162">**Opdracht toocreate een cluster in een resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="e9e77-162">**Command toocreate a cluster in a resource group**</span></span>

    hdinsight cluster create [options] <clusterName>

<span data-ttu-id="e9e77-163">Voorbeeld: Een Storm op Linux-cluster maken</span><span class="sxs-lookup"><span data-stu-id="e9e77-163">Example: Create a Storm on Linux cluster</span></span>

    azure hdinsight cluster create -g myarmgroup -l westus -y Linux --clusterType Storm --version 3.2 --defaultStorageAccountName mystorageaccount --defaultStorageAccountKey <defaultStorageAccountKey> --defaultStorageContainer mycontainer --userName admin --password <clusterPassword> --sshUserName sshuser --sshPassword <sshPassword> --workerNodeCount 1 myNewCluster01

    info:    Executing command hdinsight cluster create
    + Submitting hello request toocreate cluster...
    info:    hdinsight cluster create command OK

<span data-ttu-id="e9e77-164">Voorbeeld: Een cluster maken met een scriptactie</span><span class="sxs-lookup"><span data-stu-id="e9e77-164">Example: Create a cluster with a script action</span></span>

    azure hdinsight cluster create -g myarmgroup -l westus -y Linux --clusterType Hadoop --version 3.2 --defaultStorageAccountName mystorageaccount --defaultStorageAccountKey <defaultStorageAccountKey> --defaultStorageContainer mycontainer --userName admin --password <clusterPassword> --sshUserName sshuser --sshPassword <sshPassword> --workerNodeCount 1 –configurationPath "C:\myFiles\configFile.config" myNewCluster01

    info:    Executing command hdinsight cluster create
    + Submitting hello request toocreate cluster...
    info:    hdinsight cluster create command OK

<span data-ttu-id="e9e77-165">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="e9e77-165">Parameter options:</span></span>

    -h, --help                                                 output usage information
    -v, --verbose                                              use verbose output
    -vv                                                        more verbose with debug output
    --json                                                     use json output
    -g --resource-group <resource-group>                       hello name of hello resource group
    -c, --clusterName <clusterName>                            HDInsight cluster name
    -l, --location <location>                                  Data center location for hello cluster
    -y, --osType <osType>                                      HDInsight cluster operating system
    'Windows' or 'Linux'
    --version <version>                                        HDInsight cluster version
    --clusterType <clusterType>                                HDInsight cluster type.
    Hadoop | HBase | Spark | Storm
    --defaultStorageAccountName <storageAccountName>           Storage account url toouse for default HDInsight storage
    --defaultStorageAccountKey <storageAccountKey>             Key toohello storage account toouse for default HDInsight storage
    --defaultStorageContainer <storageContainer>               Container in hello storage account toouse for HDInsight default storage
    --headNodeSize <headNodeSize>                              (Optional) Head node size for hello cluster
    --workerNodeCount <workerNodeCount>                        Number of worker nodes toouse for hello cluster
    --workerNodeSize <workerNodeSize>                          (Optional) Worker node size for hello cluster)
    --zookeeperNodeSize <zookeeperNodeSize>                    (Optional) Zookeeper node size for hello cluster
    --userName <userName>                                      Cluster username
    --password <password>                                      Cluster password
    --sshUserName <sshUserName>                                SSH username (only for Linux clusters)
    --sshPassword <sshPassword>                                SSH password (only for Linux clusters)
    --sshPublicKey <sshPublicKey>                              SSH public key (only for Linux clusters)
    --rdpUserName <rdpUserName>                                RDP username (only for Windows clusters)
    --rdpPassword <rdpPassword>                                RDP password (only for Windows clusters)
    --rdpAccessExpiry <rdpAccessExpiry>                        RDP access expiry.
    For example 12/12/2015 (only for Windows clusters)
    --virtualNetworkId <virtualNetworkId>                      (Optional) Virtual network ID for hello cluster.
    Value is a GUID for Windows cluster and ARM resource ID for Linux cluster)
    --subnetName <subnetName>                                  (Optional) Subnet for hello cluster
    --additionalStorageAccounts <additionalStorageAccounts>    (Optional) Additional storage accounts.
    Can be multiple.
    In hello format of 'accountName#accountKey'.
    For example, --additionalStorageAccounts "acc1#key1;acc2#key2"
    --hiveMetastoreServerName <hiveMetastoreServerName>        (Optional) SQL Server name for hello external metastore for Hive
    --hiveMetastoreDatabaseName <hiveMetastoreDatabaseName>    (Optional) Database name for hello external metastore for Hive
    --hiveMetastoreUserName <hiveMetastoreUserName>            (Optional) Database username for hello external metastore for Hive
    --hiveMetastorePassword <hiveMetastorePassword>            (Optional) Database password for hello external metastore for Hive
    --oozieMetastoreServerName <oozieMetastoreServerName>      (Optional) SQL Server name for hello external metastore for Oozie
    --oozieMetastoreDatabaseName <oozieMetastoreDatabaseName>  (Optional) Database name for hello external metastore for Oozie
    --oozieMetastoreUserName <oozieMetastoreUserName>          (Optional) Database username for hello external metastore for Oozie
    --oozieMetastorePassword <oozieMetastorePassword>          (Optional) Database password for hello external metastore for Oozie
    --configurationPath <configurationPath>                    (Optional) HDInsight cluster configuration file path
    -s, --subscription <id>                                    hello subscription id
    --tags <tags>                                              Tags tooset toohello cluster.
    Can be multiple.
    In hello format of 'name=value'.
    Name is required and value is optional.
    For example, --tags tag1=value1;tag2


<span data-ttu-id="e9e77-166">**Opdracht toodelete een cluster**</span><span class="sxs-lookup"><span data-stu-id="e9e77-166">**Command toodelete a cluster**</span></span>

    hdinsight cluster delete [options] <clusterName>

<span data-ttu-id="e9e77-167">**Opdracht tooshow clusterdetails**</span><span class="sxs-lookup"><span data-stu-id="e9e77-167">**Command tooshow cluster details**</span></span>

    hdinsight cluster show [options] <clusterName>

<span data-ttu-id="e9e77-168">**Opdracht toolist alle clusters (in een specifieke resourcegroep, indien opgegeven)**</span><span class="sxs-lookup"><span data-stu-id="e9e77-168">**Command toolist all clusters (in a specific resource group, if provided)**</span></span>

    hdinsight cluster list [options]

<span data-ttu-id="e9e77-169">**Opdracht tooresize een cluster**</span><span class="sxs-lookup"><span data-stu-id="e9e77-169">**Command tooresize a cluster**</span></span>

    hdinsight cluster resize [options] <clusterName> <targetInstanceCount>

<span data-ttu-id="e9e77-170">**Opdracht tooenable HTTP-toegang voor een cluster**</span><span class="sxs-lookup"><span data-stu-id="e9e77-170">**Command tooenable HTTP access for a cluster**</span></span>

    hdinsight cluster enable-http-access [options] <clusterName> <userName> <password>

<span data-ttu-id="e9e77-171">**Opdracht toodisable HTTP-toegang voor een cluster**</span><span class="sxs-lookup"><span data-stu-id="e9e77-171">**Command toodisable HTTP access for a cluster**</span></span>

    hdinsight cluster disable-http-access [options] <clusterName>

<span data-ttu-id="e9e77-172">**Opdracht tooenable RDP-toegang voor een cluster**</span><span class="sxs-lookup"><span data-stu-id="e9e77-172">**Command tooenable RDP access for a cluster**</span></span>

    hdinsight cluster enable-rdp-access [options] <clusterName> <rdpUserName> <rdpPassword> <rdpExpiryDate>

<span data-ttu-id="e9e77-173">**Opdracht toodisable HTTP-toegang voor een cluster**</span><span class="sxs-lookup"><span data-stu-id="e9e77-173">**Command toodisable HTTP access for a cluster**</span></span>

    hdinsight cluster disable-rdp-access [options] <clusterName>

## <a name="azure-insights-commands-related-toomonitoring-insights-events-alert-rules-autoscale-settings-metrics"></a><span data-ttu-id="e9e77-174">inzicht van Azure: opdrachten gerelateerde toomonitoring Insights (gebeurtenissen, waarschuwingsregels, instellingen voor automatisch schalen, metrische gegevens)</span><span class="sxs-lookup"><span data-stu-id="e9e77-174">azure insights: Commands related toomonitoring Insights (events, alert rules, autoscale settings, metrics)</span></span>
<span data-ttu-id="e9e77-175">**Bewerkingslogboeken voor een abonnement, een correlationId, een resourcegroep, resource of resourceprovider ophalen**</span><span class="sxs-lookup"><span data-stu-id="e9e77-175">**Retrieve operation logs for a subscription, a correlationId, a resource group, resource, or resource provider**</span></span>

    insights logs list [options]

## <a name="azure-location-commands-tooget-hello-available-locations-for-all-resource-types"></a><span data-ttu-id="e9e77-176">Azure-locatie: tooget Hallo beschikbare locaties voor alle resourcetypen opdrachten</span><span class="sxs-lookup"><span data-stu-id="e9e77-176">azure location: Commands tooget hello available locations for all resource types</span></span>
<span data-ttu-id="e9e77-177">**Lijst Hallo beschikbare locaties**</span><span class="sxs-lookup"><span data-stu-id="e9e77-177">**List hello available locations**</span></span>

    location list [options]

## <a name="azure-network-commands-toomanage-network-resources"></a><span data-ttu-id="e9e77-178">Azure-netwerk: opdrachten toomanage netwerkbronnen</span><span class="sxs-lookup"><span data-stu-id="e9e77-178">azure network: Commands toomanage network resources</span></span>
<span data-ttu-id="e9e77-179">**Opdrachten toomanage virtuele netwerken**</span><span class="sxs-lookup"><span data-stu-id="e9e77-179">**Commands toomanage virtual networks**</span></span>

    network vnet create [options] <resource-group> <name> <location>
<span data-ttu-id="e9e77-180">Hiermee maakt u een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="e9e77-180">Creates a virtual network.</span></span> <span data-ttu-id="e9e77-181">In Hallo de volgende voorbeeld wordt een virtueel netwerk maken newvnet voor resource groep myresourcegroup in de regio VS-West Hallo naam.</span><span class="sxs-lookup"><span data-stu-id="e9e77-181">In hello following example we create a virtual network named newvnet for resource group myresourcegroup in hello West US region.</span></span>

    azure network vnet create myresourcegroup newvnet "west us"
    info:    Executing command network vnet create
    + Looking up virtual network "newvnet"
    + Creating virtual network "newvnet"
     Loading virtual network state
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet
    data:    Name:                 newvnet
    data:    Type:                 Microsoft.Network/virtualNetworks
    data:    Location:             westus
    data:    Tags:
    data:    Provisioning state:   Succeeded
    data:    Address prefixes:
    data:     10.0.0.0/8
    data:    DNS servers:
    data:    Subnets:
    data:
    info:    network vnet create command OK


<span data-ttu-id="e9e77-182">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="e9e77-182">Parameter options:</span></span>

     -h, --help                                 output usage information
     -v, --verbose                              use verbose output
    --json                                     use json output
     -g, --resource-group <resource-group>      hello name of hello resource group
     -n, --name <name>                          hello name of hello virtual network
     -l, --location <location>                  hello location
     -a, --address-prefixes <address-prefixes>  hello comma separated list of address prefixes for this virtual network
      For example -a 10.0.0.0/24,10.0.1.0/24.
      Default value is 10.0.0.0/8

    -d, --dns-servers <dns-servers>            hello comma separated list of DNS servers IP addresses
     -t, --tags <tags>                          hello tags set on this virtual network.
      Can be multiple. In hello format of "name=value".
      Name is required and value is optional.
      For example, -t tag1=value1;tag2
     -s, --subscription <subscription>          hello subscription identifier
<BR>

    network vnet set [options] <resource-group> <name>

<span data-ttu-id="e9e77-183">De configuratie van een virtueel netwerk in de resourcegroep-updates.</span><span class="sxs-lookup"><span data-stu-id="e9e77-183">Updates a virtual network configuration within a resource group.</span></span>

    azure network vnet set myresourcegroup newvnet

    info:    Executing command network vnet set
    + Looking up virtual network "newvnet"
    + Updating virtual network "newvnet"
    + Loading virtual network state
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet
    data:    Name:                 newvnet
    data:    Type:                 Microsoft.Network/virtualNetworks
    data:    Location:             westus
    data:    Tags:
    data:    Provisioning state:   Succeeded
    data:    Address prefixes:
    data:     10.0.0.0/8
    data:    DNS servers:
    data:    Subnets:
    data:
    info:    network vnet set command OK

<span data-ttu-id="e9e77-184">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="e9e77-184">Parameter options:</span></span>

       -h, --help                                 output usage information
       -v, --verbose                              use verbose output
       --json                                     use json output
       -g, --resource-group <resource-group>      hello name of hello resource group
       -n, --name <name>                          hello name of hello virtual network
       -a, --address-prefixes <address-prefixes>  hello comma separated list of address prefixes for this virtual network.
        For example -a 10.0.0.0/24,10.0.1.0/24.
        This list will be appended toohello current list of address prefixes.
        hello address prefixes in this list should not overlap between them.
        hello address prefixes in this list should not overlap with existing address prefixes in hello vnet.

       -d, --dns-servers [dns-servers]            hello comma separated list of DNS servers IP addresses.
        This list will be appended toohello current list of DNS server IP addresses.

       -t, --tags <tags>                          hello tags set on this virtual network.
        Can be multiple. In hello format of "name=value".
        Name is required and value is optional. For example, -t tag1=value1;tag2.
        This list will be appended toohello current list of tags

       --no-tags                                  remove all existing tags
       -s, --subscription <subscription>          hello subscription identifier
<BR>

    network vnet list [options] <resource-group>

<span data-ttu-id="e9e77-185">Hallo-opdracht worden alle virtuele netwerken in een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="e9e77-185">hello command lists all virtual networks in a resource group.</span></span>

    C:\>azure network vnet list myresourcegroup

    info:    Executing command network vnet list
    + Listing virtual networks
        data:    ID
       Name      Location  Address prefixes  DNS servers
    data:    -------------------------------------------------------------------
    ------  --------  --------  ----------------  -----------
    data:    /subscriptions/###############################/resourceGroups/
    wvnet   newvnet   westus    10.0.0.0/8
    info:    network vnet list command OK

<span data-ttu-id="e9e77-186">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="e9e77-186">Parameter options:</span></span>

      -h, --help                             output usage information
      -v, --verbose                          use verbose output
      --json                                 use json output
      -g, --resource-group <resource-group>  hello name of hello resource group
      -s, --subscription <subscription>      hello subscription identifier

<BR>

    network vnet show [options] <resource-group> <name>
<span data-ttu-id="e9e77-187">Hallo-opdracht ziet Hallo virtueel netwerkeigenschappen in een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="e9e77-187">hello command shows hello virtual network properties in a resource group.</span></span>

    azure network vnet show -g myresourcegroup -n newvnet

    info:    Executing command network vnet show
    + Looking up virtual network "newvnet"
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet
    data:    Name:                 newvnet
    data:    Type:                 Microsoft.Network/virtualNetworks
    data:    Location:             westus
    data:    Tags:
    data:    Provisioning state:   Succeeded
    data:    Address prefixes:
    data:     10.0.0.0/8
    data:    DNS servers:
    data:    Subnets:
    data:
    info:    network vnet show command OK
<BR>

    network vnet delete [options] <resource-group> <name>
<span data-ttu-id="e9e77-188">Hallo-opdracht verwijdert u een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="e9e77-188">hello command removes a virtual network.</span></span>

    azure network vnet delete myresourcegroup newvnetX

    info:    Executing command network vnet delete
    + Looking up virtual network "newvnetX"
    Delete virtual network newvnetX? [y/n] y
    + Deleting virtual network "newvnetX"
    info:    network vnet delete command OK

<span data-ttu-id="e9e77-189">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="e9e77-189">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  hello name of hello resource group
     -n, --name <name>                      hello name of hello virtual network
     -q, --quiet                            quiet mode, do not ask for delete confirmation
     -s, --subscription <subscription>      hello subscription identifier


<span data-ttu-id="e9e77-190">**Opdrachten toomanage virtuele subnetten**</span><span class="sxs-lookup"><span data-stu-id="e9e77-190">**Commands toomanage virtual network subnets**</span></span>

    network vnet subnet create [options] <resource-group> <vnet-name> <name>

<span data-ttu-id="e9e77-191">Voegt een ander subnet tooan bestaand virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="e9e77-191">Adds another subnet tooan existing virtual network.</span></span>

    azure network vnet subnet create -g myresourcegroup --vnet-name newvnet -n subnet --address-prefix 10.0.1.0/24

    info:    Executing command network vnet subnet create
    + Looking up hello subnet "subnet"
    + Creating subnet "subnet"
    + Looking up hello subnet "subnet"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet/subnets/subnet
    data:    Name:                      subnet
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet create command OK

<span data-ttu-id="e9e77-192">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="e9e77-192">Parameter options:</span></span>

     -h, --help                                                       output usage information
     -v, --verbose                                                    use verbose output
         --json                                                           use json output
     -g, --resource-group <resource-group>                            hello name of hello resource group
     -e, --vnet-name <vnet-name>                                      hello name of hello virtual network
     -n, --name <name>                                                hello name of hello subnet
     -a, --address-prefix <address-prefix>                            hello address prefix
     -w, --network-security-group-id <network-security-group-id>      hello network security group identifier.
           e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/networkSecurityGroups/<nsg-name>
     -o, --network-security-group-name <network-security-group-name>  hello network security group name
     -s, --subscription <subscription>                                hello subscription identifier

<BR>

    network vnet subnet set [options] <resource-group> <vnet-name> <name>

<span data-ttu-id="e9e77-193">Hiermee stelt u een specifiek virtueel netwerksubnet binnen een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="e9e77-193">Sets a specific virtual network subnet within a resource group.</span></span>

    C:\>azure network vnet subnet set -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet set
    + Looking up hello subnet "subnet1"
    + Setting subnet "subnet1"
    + Looking up hello subnet "subnet1"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet/subnets/subnet1
    data:    Name:                      subnet1
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet set command OK
<BR>

    network vnet subnet list [options] <resource-group> <vnet-name>

<span data-ttu-id="e9e77-194">Een lijst met alle subnetten van Hallo virtueel netwerk voor een specifieke virtuele netwerk binnen een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="e9e77-194">Lists all hello virtual network subnets for a specific virtual network within a resource group.</span></span>

    azure network vnet subnet set -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet set
    + Looking up hello subnet "subnet1"
    + Setting subnet "subnet1"
    + Looking up hello subnet "subnet1"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet/subnets/subnet1
    data:    Name:                      subnet1
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet set command OK
<BR>

    network vnet subnet show [options] <resource-group> <vnet-name> <name>
<span data-ttu-id="e9e77-195">Eigenschappen van virtueel netwerk subnet</span><span class="sxs-lookup"><span data-stu-id="e9e77-195">Displays virtual network subnet properties</span></span>

    azure network vnet subnet show -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet show
    + Looking up hello subnet "subnet1"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft
    .Network/virtualNetworks/newvnet/subnets/subnet1
    data:    Name:                      subnet1
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet show command OK

<span data-ttu-id="e9e77-196">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="e9e77-196">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -e, --vnet-name <vnet-name>            hello name of hello virtual network
    -n, --name <name>                      hello name of hello subnet
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network vnet subnet delete [options] <resource-group> <vnet-name> <subnet-name>
<span data-ttu-id="e9e77-197">Hiermee verwijdert u een subnet van een bestaand virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="e9e77-197">Removes a subnet from an existing virtual network.</span></span>

    azure network vnet subnet delete -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet delete
    + Looking up hello subnet "subnet1"
    Delete subnet "subnet1"? [y/n] y
    + Deleting subnet "subnet1"
    info:    network vnet subnet delete command OK

<span data-ttu-id="e9e77-198">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="e9e77-198">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  hello name of hello resource group
     -e, --vnet-name <vnet-name>            hello name of hello virtual network
     -n, --name <name>                      hello subnet name
     -s, --subscription <subscription>      hello subscription identifier
     -q, --quiet                            quiet mode, do not ask for delete confirmation

<span data-ttu-id="e9e77-199">**Opdrachten toomanage netwerktaakverdelers**</span><span class="sxs-lookup"><span data-stu-id="e9e77-199">**Commands toomanage load balancers**</span></span>

    network lb create [options] <resource-group> <name> <location>
<span data-ttu-id="e9e77-200">Hiermee maakt u een load balancer.</span><span class="sxs-lookup"><span data-stu-id="e9e77-200">Creates a load balancer set.</span></span>

    azure network lb create -g myresourcegroup -n mylb -l westus

    info:    Executing command network lb create
    + Looking up hello load balancer "mylb"
    + Creating load balancer "mylb"
    + Looking up hello load balancer "mylb"
    data:    Id:                           /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb
    data:    Name:                         mylb
    data:    Type:                         Microsoft.Network/loadBalancers
    data:    Location:                     westus
    data:    Provisioning state:           Succeeded
    info:    network lb create command OK

<span data-ttu-id="e9e77-201">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="e9e77-201">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -n, --name <name>                      hello name of hello load balancer
    -l, --location <location>              hello location
    -t, --tags <tags>                      hello list of tags.
     Can be multiple. In hello format of "name=value".
     Name is required and value is optional. For example, -t tag1=value1;tag2
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network lb list [options] <resource-group>
<span data-ttu-id="e9e77-202">Bevat Load balancer bronnen binnen een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="e9e77-202">Lists Load balancer resources within a resource group.</span></span>

    azure network lb list myresourcegroup

    info:    Executing command network lb list
    + Getting hello load balancers
    data:    Name  Location
    data:    ----  --------
    data:    mylb  westus
    info:    network lb list command OK

<span data-ttu-id="e9e77-203">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="e9e77-203">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network lb show [options] <resource-group> <name>

<span data-ttu-id="e9e77-204">Geeft load balancer-gegevens van een specifieke load balancer binnen een resourcegroep</span><span class="sxs-lookup"><span data-stu-id="e9e77-204">Displays load balancer information of a specific load balancer within a resource group</span></span>

    azure network lb show myresourcegroup mylb -v

    info:    Executing command network lb show
    verbose: Looking up hello load balancer "mylb"
    data:    Id:                           /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb
    data:    Name:                         mylb
    data:    Type:                         Microsoft.Network/loadBalancers
    data:    Location:                     westus
    data:    Provisioning state:           Succeeded
    info:    network lb show command OK

<span data-ttu-id="e9e77-205">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="e9e77-205">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -n, --name <name>                      hello name of hello load balancer
    -s, --subscription <subscription>      hello subscription identifier

<BR>

    network lb delete [options] <resource-group> <name>

<span data-ttu-id="e9e77-206">Load balancer-resources verwijderen.</span><span class="sxs-lookup"><span data-stu-id="e9e77-206">Delete load balancer resources.</span></span>

    azure network lb delete  myresourcegroup mylb

    info:    Executing command network lb delete
    + Looking up hello load balancer "mylb"
    Delete load balancer "mylb"? [y/n] y
    + Deleting load balancer "mylb"
    info:    network lb delete command OK

<span data-ttu-id="e9e77-207">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="e9e77-207">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  hello name of hello resource group
     -n, --name <name>                      hello name of hello load balancer
     -q, --quiet                            quiet mode, do not ask for delete confirmation
     -s, --subscription <subscription>      hello subscription identifier

<span data-ttu-id="e9e77-208">**Opdrachten toomanage tests van een load balancer**</span><span class="sxs-lookup"><span data-stu-id="e9e77-208">**Commands toomanage probes of a load balancer**</span></span>

    network lb probe create [options] <resource-group> <lb-name> <name>

<span data-ttu-id="e9e77-209">Hallo-test de configuratie voor gezondheidsstatus in Hallo load balancer maken.</span><span class="sxs-lookup"><span data-stu-id="e9e77-209">Create hello probe configuration for health status in hello load balancer.</span></span> <span data-ttu-id="e9e77-210">Houd er rekening mee toorun met deze opdracht, de load balancer vereist een frontend-ip-resource (uitchecken opdracht 'azure-netwerk frontend-ip' tooassign een IP-adres tooload balancer).</span><span class="sxs-lookup"><span data-stu-id="e9e77-210">Keep in mind toorun this command, your load balancer requires a frontend-ip resource (Check out command "azure network frontend-ip" tooassign an ip address tooload balancer).</span></span>

    azure network lb probe create -g myresourcegroup --lb-name mylb -n mylbprobe --protocol tcp --port 80 -i 300

    info:    Executing command network lb probe create
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    info:    network lb probe create command OK

<span data-ttu-id="e9e77-211">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="e9e77-211">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello probe
    -p, --protocol <protocol>              hello probe protocol
    -o, --port <port>                      hello probe port
    -f, --path <path>                      hello probe path
    -i, --interval <interval>              hello probe interval in seconds
    -c, --count <count>                    hello number of probes
    -s, --subscription <subscription>      hello subscription identifier

<BR>

    network lb probe set [options] <resource-group> <lb-name> <name>

<span data-ttu-id="e9e77-212">Een bestaande load balancer-test met nieuwe waarden voor deze bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="e9e77-212">Updates an existing load balancer probe with new values for it.</span></span>

    azure network lb probe set -g myresourcegroup -l mylb -n mylbprobe -p mylbprobe1 -p TCP -o 443 -i 300

    info:    Executing command network lb probe set
        + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    info:    network lb probe set command OK

<span data-ttu-id="e9e77-213">De parameteropties</span><span class="sxs-lookup"><span data-stu-id="e9e77-213">Parameter options</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello probe
    -e, --new-probe-name <new-probe-name>  hello new name of hello probe
    -p, --protocol <protocol>              hello new value for probe protocol
    -o, --port <port>                      hello new value for probe port
    -f, --path <path>                      hello new value for probe path
    -i, --interval <interval>              hello new value for probe interval in seconds
    -c, --count <count>                    hello new value for number of probes
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network lb probe list [options] <resource-group> <lb-name>

<span data-ttu-id="e9e77-214">Lijst Hallo test eigenschappen voor een load balancer-set.</span><span class="sxs-lookup"><span data-stu-id="e9e77-214">List hello probe properties for a load balancer set.</span></span>

    C:\>azure network lb probe list -g myresourcegroup -l mylb

    info:    Executing command network lb probe list
    + Looking up hello load balancer "mylb"
    data:    Name       Protocol  Port  Path  Interval  Count
    data:    ---------  --------  ----  ----  --------  -----
    data:    mylbprobe  Tcp       443         300       2
    info:    network lb probe list command OK

<span data-ttu-id="e9e77-215">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="e9e77-215">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -s, --subscription <subscription>      hello subscription identifier


    network lb probe delete [options] <resource-group> <lb-name> <name>
<span data-ttu-id="e9e77-216">Hiermee verwijdert u Hallo test gemaakt voor Hallo load balancer.</span><span class="sxs-lookup"><span data-stu-id="e9e77-216">Removes hello probe created for hello load balancer.</span></span>

    azure network lb probe delete -g myresourcegroup -l mylb -n mylbprobe

    info:    Executing command network lb probe delete
    + Looking up hello load balancer "mylb"
    Delete a probe "mylbprobe?" [y/n] y
    + Updating load balancer "mylb"
    info:    network lb probe delete command OK

<span data-ttu-id="e9e77-217">**Opdrachten toomanage frontend-IP-configuraties van een load balancer**</span><span class="sxs-lookup"><span data-stu-id="e9e77-217">**Commands toomanage frontend ip configurations of a load balancer**</span></span>

    network lb frontend-ip create [options] <resource-group> <lb-name> <name>
<span data-ttu-id="e9e77-218">Maakt een frontend IP-configuratie tooan bestaande load balancer-set.</span><span class="sxs-lookup"><span data-stu-id="e9e77-218">Creates a frontend IP configuration tooan existing load balancer set.</span></span>

    azure network lb frontend-ip create -g myresourcegroup --lb-name mylb -n myfrontendip -o Dynamic -e subnet -m newvnet

    info:    Executing command network lb frontend-ip create
    + Looking up hello load balancer "mylb"
    + Looking up hello subnet "subnet"
    + Creating frontend IP configuration "myfrontendip"
    + Looking up hello load balancer "mylb"
    data:    Id:                           /subscriptions/###############################/resourceGroups/Myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb
    /frontendIPConfigurations/myfrontendip
    data:    Name:                         myfrontendip
    data:    Type:                         Microsoft.Network/loadBalancers/frontendIPConfigurations
    data:    Provisioning state:           Succeeded
    data:    Private IP allocation method: Dynamic
    data:    Private IP address:           10.0.1.4
    data:    Subnet:                       id=/subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet/subnets/subnet
    data:    Public IP address:
    data:    Inbound NAT rules
    data:    Outbound NAT rules
    data:    Load balancing rules
    data:
    info:    network lb frontend-ip create command OK

<BR>

    network lb frontend-ip set [options] <resource-group> <lb-name> <name>

<span data-ttu-id="e9e77-219">Updates in een bestaande configuratie van een frontend IP.hello onderstaande opdracht voegt een openbaar IP-adres mypubip5 tooan bestaande load balancer frontend-IP-met de naam myfrontendip aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="e9e77-219">Updates an existing configuration of a frontend IP.hello command below adds a public IP called mypubip5 tooan existing load balancer frontend IP named myfrontendip.</span></span>

    azure network lb frontend-ip set -g myresourcegroup --lb-name mylb -n myfrontendip -i mypubip5

    info:    Executing command network lb frontend-ip set
    + Looking up hello load balancer "mylb"
    + Looking up hello public ip "mypubip5"
    + Updating load balancer "mylb"
    + Looking up hello load balancer "mylb"
    data:    Id:                           /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/frontendIPConfigurations/myfrontendip
    data:    Name:                         myfrontendip
    data:    Type:                         Microsoft.Network/loadBalancers/frontendIPConfigurations
    data:    Provisioning state:           Succeeded
    data:    Private IP allocation method: Dynamic
    data:    Private IP address:
    data:    Subnet:
    data:    Public IP address:            id=/subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/publicIPAddresses/mypubip5
    data:    Inbound NAT rules
    data:    Outbound NAT rules
    data:    Load balancing rules
    data:
    info:    network lb frontend-ip set command OK

<span data-ttu-id="e9e77-220">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="e9e77-220">Parameter options:</span></span>

    -h, --help                                                         output usage information
    -v, --verbose                                                      use verbose output
    --json                                                             use json output
    -g, --resource-group <resource-group>                              hello name of hello resource group
    -l, --lb-name <lb-name>                                            hello name of hello load balancer
    -n, --name <name>                                                  hello name of hello frontend ip configuration
    -a, --private-ip-address <private-ip-address>                      hello private ip address
    -o, --private-ip-allocation-method <private-ip-allocation-method>  hello private ip allocation method [Static, Dynamic]
    -u, --public-ip-id <public-ip-id>                                  hello public ip identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/publicIPAddresses/<public-ip-name>
    -i, --public-ip-name <public-ip-name>                              hello public ip name.
    This public ip must exist in hello same resource group as hello lb.
    Please use public-ip-id if that is not hello case.
    -b, --subnet-id <subnet-id>                                        hello subnet id.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/VirtualNetworks/<vnet-name>/subnets/<subnet-name>
    -e, --subnet-name <subnet-name>                                    hello subnet name
    -m, --vnet-name <vnet-name>                                        hello virtual network name.
    This virtual network must exist in hello same resource group as hello lb.
    Please use subnet-id if that is not hello case.
    -s, --subscription <subscription>                                  hello subscription identifier

<BR>

    network lb frontend-ip list [options] <resource-group> <lb-name>

<span data-ttu-id="e9e77-221">Geeft een lijst van alle Hallo frontend IP-netwerkbronnen geconfigureerd voor Hallo load balancer.</span><span class="sxs-lookup"><span data-stu-id="e9e77-221">Lists all hello frontend IP resources configured for hello load balancer.</span></span>

    azure network lb frontend-ip list -g myresourcegroup -l mylb

    info:    Executing command network lb frontend-ip list
    + Looking up hello load balancer "mylb"
    data:    Name         Provisioning state  Private IP allocation method  Subnet
    data:    -----------  ------------------  ----------------------------  ------
    data:    myprivateip  Succeeded           Dynamic
    info:    network lb frontend-ip list command OK

<span data-ttu-id="e9e77-222">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="e9e77-222">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network lb frontend-ip delete [options] <resource-group> <lb-name> <name>
<span data-ttu-id="e9e77-223">Hallo frontend-IP-object dat is gekoppeld tooload balancer verwijderen</span><span class="sxs-lookup"><span data-stu-id="e9e77-223">Deletes hello frontend IP object associated tooload balancer</span></span>

    network lb frontend-ip delete -g myresourcegroup -l mylb -n myfrontendip
    info:    Executing command network lb frontend-ip delete
    + Looking up hello load balancer "mylb"
    Delete frontend ip configuration "myfrontendip"? [y/n] y
    + Updating load balancer "mylb"

<span data-ttu-id="e9e77-224">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="e9e77-224">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello frontend ip configuration
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      hello subscription identifier

<span data-ttu-id="e9e77-225">**Opdrachten toomanage back-end-adresgroepen van een load balancer**</span><span class="sxs-lookup"><span data-stu-id="e9e77-225">**Commands toomanage backend address pools of a load balancer**</span></span>

    network lb address-pool create [options] <resource-group> <lb-name> <name>

<span data-ttu-id="e9e77-226">Maak een back-end-adresgroep voor een load balancer.</span><span class="sxs-lookup"><span data-stu-id="e9e77-226">Create a backend address pool for a load balancer.</span></span>

    azure network lb address-pool create -g myresourcegroup --lb-name mylb -n myaddresspool

    info:    Executing command network lb address-pool create
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    + Looking up hello load balancer "mylb"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourgroup/providers/Microso.Network/loadBalancers/mylb/backendAddressPools/myaddresspool
    data:    Name:                      myaddresspool
    data:    Type:                      Microsoft.Network/loadBalancers/backendAddressPools
    data:    Provisioning state:        Succeeded
    data:    Backend IP configurations:
    data:    Load balancing rules:
    data:
    info:    network lb address-pool create command OK

<span data-ttu-id="e9e77-227">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="e9e77-227">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello backend address pool
    -s, --subscription <subscription>      hello subscription identifier

<BR>

    network lb address-pool list [options] <resource-group> <lb-name>

<span data-ttu-id="e9e77-228">Lijst met back-end IP-adresgroep adresbereik voor een specifieke resourcegroep</span><span class="sxs-lookup"><span data-stu-id="e9e77-228">List backend IP address pool range for a specific resource group</span></span>

    azure network lb address-pool list -g myresourcegroup -l mylb

    info:    Executing command network lb address-pool list
    + Looking up hello load balancer "mylb"
    data:    Name           Provisioning state
    data:    -------------  ------------------
    data:    mybackendpool  Succeeded
    info:    network lb address-pool list command OK

<span data-ttu-id="e9e77-229">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="e9e77-229">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  hello name of hello resource group
     -l, --lb-name <lb-name>                hello name of hello load balancer
     -s, --subscription <subscription>      hello subscription identifier

<BR>
    <span data-ttu-id="e9e77-230">lb-netwerkadresgroep verwijderen [opties] < resourcegroep >< lb-naam ><name></span><span class="sxs-lookup"><span data-stu-id="e9e77-230">network lb address-pool delete [options] <resource-group> <lb-name> <name></span></span>

<span data-ttu-id="e9e77-231">Hallo back-end IP-adresgroep bereik resource verwijdert uit de load balancer.</span><span class="sxs-lookup"><span data-stu-id="e9e77-231">Removes hello backend IP pool range resource from load balancer.</span></span>

    azure network lb address-pool delete -g myresourcegroup -l mylb -n mybackendpool

    info:    Executing command network lb address-pool delete
    + Looking up hello load balancer "mylb"
    Delete backend address pool "mybackendpool"? [y/n] y
    + Updating load balancer "mylb"
    info:    network lb address-pool delete command OK

<span data-ttu-id="e9e77-232">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="e9e77-232">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello backend address pool
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      hello subscription identifier

<span data-ttu-id="e9e77-233">**Opdrachten toomanage load balancer-regels**</span><span class="sxs-lookup"><span data-stu-id="e9e77-233">**Commands toomanage load balancer rules**</span></span>

    network lb rule create [options] <resource-group> <lb-name> <name>
<span data-ttu-id="e9e77-234">Load balancer-regels maken.</span><span class="sxs-lookup"><span data-stu-id="e9e77-234">Create load balancer rules.</span></span>

<span data-ttu-id="e9e77-235">U kunt een regel voor load balancer configureren Hallo frontend-eindpunt voor Hallo load balancer en Hallo back-end adresgroep bereik tooreceive Hallo binnenkomend netwerkverkeer maken.</span><span class="sxs-lookup"><span data-stu-id="e9e77-235">You can create a load balancer rule configuring hello frontend endpoint for hello load balancer and hello backend address pool range tooreceive hello incoming network traffic.</span></span> <span data-ttu-id="e9e77-236">Instellingen omvatten ook Hallo poorten voor de frontend-IP-eindpunt en poorten voor Hallo back-end-pool adresbereik.</span><span class="sxs-lookup"><span data-stu-id="e9e77-236">Settings also include hello ports for frontend IP endpoint and ports for hello backend address pool range.</span></span>

<span data-ttu-id="e9e77-237">Hallo volgende voorbeeld laat zien hoe toocreate een load balancer-regel, Hallo frontend eindpunt luisteren tooport 80 netwerkverkeer TCP en taakverdeling tooport 8080 voor Hallo back-end-pool adresbereik verzenden.</span><span class="sxs-lookup"><span data-stu-id="e9e77-237">hello following example shows how toocreate a load balancer rule,  hello frontend endpoint listening tooport 80 TCP and load balancing network traffic sending tooport 8080 for hello backend address pool range.</span></span>

    azure network lb rule create -g myresourcegroup -l mylb -n mylbrule -p tcp -f 80 -b 8080 -i 10


    info:    Executing command network lb rule create
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    + Loading rule state
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/loadBalancingRules/mylbrule
    data:    Name:                      mylbrule
    data:    Type:                      Microsoft.Network/loadBalancers/loadBalancingRules
    data:    Provisioning state:        Succeeded
    data:    Frontend IP configuration: /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/frontendIPConfigurations/myfrontendip
    data:    Backend address pool:      id=/subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/mybackendpool
    data:    Protocol:                  Tcp
    data:    Frontend port:             80
    data:    Backend port:              8080
    data:    Enable floating IP:        false
    data:    Idle timeout in minutes:   10
    data:    Probes
    data:
    info:    network lb rule create command OK

<BR>

    network lb rule set [options] <resource-group> <lb-name> <name>

<span data-ttu-id="e9e77-238">Updates van een bestaande load balancer-regel instellen in een specifieke resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="e9e77-238">Updates an existing load balancer rule set in a specific resource group.</span></span> <span data-ttu-id="e9e77-239">In Hallo voorbeeld te volgen, we regelnaam Hallo van mylbrule toomynewlbrule gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="e9e77-239">In hello following example, we changed hello rule name from mylbrule toomynewlbrule.</span></span>

    azure network lb rule set -g myresourcegroup -l mylb -n mylbrule -r mynewlbrule -p tcp -f 80 -b 8080 -i 10 -t myfrontendip -o mybackendpool

    info:    Executing command network lb rule set
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    + Loading rule state
    data:    Id:                        /subscriptions/###############################/resourceGroups/yresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/loadBalancingRules/mynewlbrule
    data:    Name:                      mynewlbrule
    data:    Type:                      Microsoft.Network/loadBalancers/loadBalancingRules
    data:    Provisioning state:        Succeeded
    data:    Frontend IP configuration: /subscriptions/###############################/resourceGroups/yresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/frontendIPConfigurations/myfrontendip
    data:    Backend address pool:      id=/subscriptions/###############################/resourceGroups/yresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/mybackendpool
    data:    Protocol:                  Tcp
    data:    Frontend port:             80
    data:    Backend port:              8080
    data:    Enable floating IP:        false
    data:    Idle timeout in minutes:   10
    data:    Probes
    data:
    info:    network lb rule set command OK

<span data-ttu-id="e9e77-240">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="e9e77-240">Parameter options:</span></span>

    -h, --help                                         output usage information
    -v, --verbose                                      use verbose output
    --json                                             use json output
    -g, --resource-group <resource-group>              hello name of hello resource group
    -l, --lb-name <lb-name>                            hello name of hello load balancer
    -n, --name <name>                                  hello name of hello rule
    -r, --new-rule-name <new-rule-name>                new rule name
    -p, --protocol <protocol>                          hello rule protocol
    -f, --frontend-port <frontend-port>                hello frontend port
    -b, --backend-port <backend-port>                  hello backend port
    -e, --enable-floating-ip <enable-floating-ip>      enable floating point ip
    -i, --idle-timeout <idle-timeout>                  hello idle timeout in minutes
    -a, --probe-name [probe-name]                      hello name of hello probe defined in hello same load balancer
    -t, --frontend-ip-name <frontend-ip-name>          hello name of hello frontend ip configuration in hello same load balancer
    -o, --backend-address-pool <backend-address-pool>  name of hello backend address pool defined in hello same load balancer
    -s, --subscription <subscription>                  hello subscription identifier


    network lb rule list [options] <resource-group> <lb-name>

<span data-ttu-id="e9e77-241">Een lijst met alle taakverdelingsregels zijn geconfigureerd voor een load balancer in een specifieke resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="e9e77-241">Lists all load balancer rules configured for a load balancer in a specific resource group.</span></span>

    azure network lb rule list -g myresourcegroup -l mylb

    info:    Executing command network lb rule list
    + Looking up hello load balancer "mylb"
    data:    Name         Provisioning state  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes  Backend address pool  Probe data

    data:    mynewlbrule  Succeeded           Tcp       80             8080          false               10                       /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/mybackendpool
    info:    network lb rule list command OK

<span data-ttu-id="e9e77-242">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="e9e77-242">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -s, --subscription <subscription>      hello subscription identifier

    network lb rule delete [options] <resource-group> <lb-name> <name>

<span data-ttu-id="e9e77-243">Hiermee verwijdert u een load balancer-regel.</span><span class="sxs-lookup"><span data-stu-id="e9e77-243">Deletes a load balancer rule.</span></span>

    azure network lb rule delete -g myresourcegroup -l mylb -n mynewlbrule

    info:    Executing command network lb rule delete
    + Looking up hello load balancer "mylb"
    Delete load balancing rule mynewlbrule? [y/n] y
    + Updating load balancer "mylb"
    info:    network lb rule delete command OK

<span data-ttu-id="e9e77-244">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="e9e77-244">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello rule
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      hello subscription identifier

<span data-ttu-id="e9e77-245">**Binnenkomende NAT-regels opdrachten toomanage load balancer**</span><span class="sxs-lookup"><span data-stu-id="e9e77-245">**Commands toomanage load balancer inbound NAT rules**</span></span>

    network lb inbound-nat-rule create [options] <resource-group> <lb-name> <name>
<span data-ttu-id="e9e77-246">Maakt een binnenkomende NAT-regel voor load balancer.</span><span class="sxs-lookup"><span data-stu-id="e9e77-246">Creates an inbound NAT rule for load balancer.</span></span>

<span data-ttu-id="e9e77-247">In Hallo gebruikt de volgende voorbeeld wordt gemaakt een NAT-regel van frontend-IP (die is eerder gedefinieerd met de opdracht 'azure-netwerk frontend-ip' hello) met een luisterpoort binnenkomende en uitgaande poort die Hallo load balancer toosend Hallo-netwerkverkeer.</span><span class="sxs-lookup"><span data-stu-id="e9e77-247">In hello following example  we created a NAT rule from frontend IP (which was previously defined using hello "azure network frontend-ip" command) with an inbound listening port and outbound port that hello load balancer uses toosend hello network traffic.</span></span>

    azure network lb inbound-nat-rule create -g myresourcegroup -l mylb -n myinboundnat -p tcp -f 80 -b 8080 -i myfrontendip

    info:    Executing command network lb inbound-nat-rule create
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    + Looking up hello load balancer "mylb"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/inboundNatRules/myinboundnat
    data:    Name:                      myinboundnat
    data:    Type:                      Microsoft.Network/loadBalancers/inboundNatRules
    data:    Provisioning state:        Succeeded
    data:    Frontend IP Configuration: id=/subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/frontendIPConfigurations/myfrontendip
    data:    Backend IP configuration
    data:    Protocol                   Tcp
    data:    Frontend port              80
    data:    Backend port               8080
    data:    Enable floating IP         false
    info:    network lb inbound-nat-rule create command OK

<span data-ttu-id="e9e77-248">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="e9e77-248">Parameter options:</span></span>

    -h, --help                                     output usage information
    -v, --verbose                                  use verbose output
    --json                                         use json output
    -g, --resource-group <resource-group>          hello name of hello resource group
    -l, --lb-name <lb-name>                        hello name of hello load balancer
    -n, --name <name>                              hello name of hello inbound NAT rule
    -p, --protocol <protocol>                      hello rule protocol [tcp,udp]
    -f, --frontend-port <frontend-port>            hello frontend port [0-65535]
    -b, --backend-port <backend-port>              hello backend port [0-65535]
    -e, --enable-floating-ip <enable-floating-ip>  enable floating point ip [true,false]
    -i, --frontend-ip <frontend-ip>                hello name of hello frontend ip configuration
    -m, --vm-id <vm-id>                            hello VM id.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Compute/virtualMachines/<vm-name>
    -a, --vm-name <vm-name>                        hello VM name.This VM must exist in hello same resource group as hello lb.
    Please use vm-id if that is not hello case.
    this parameter will be ignored if --vm-id is specified
    -s, --subscription <subscription>              hello subscription identifier
<BR>

    network lb inbound-nat-rule set [options] <resource-group> <lb-name> <name>
<span data-ttu-id="e9e77-249">Updates van een bestaande binnenkomende nat-regel.</span><span class="sxs-lookup"><span data-stu-id="e9e77-249">Updates an existing inbound nat rule.</span></span> <span data-ttu-id="e9e77-250">In de Hallo voorbeeld te volgen, we Hallo gewijzigd inkomende luisterpoort van 80 too81.</span><span class="sxs-lookup"><span data-stu-id="e9e77-250">In hello following example, we changed hello inbound listening port from 80 too81.</span></span>

    azure network lb inbound-nat-rule set -g group-1 -l mylb -n myinboundnat -p tcp -f 81 -b 8080 -i myfrontendip

    info:    Executing command network lb inbound-nat-rule set
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    + Looking up hello load balancer "mylb"
    data:    Id:                        /subscriptions/###############################/resourceGroups/group-1/providers/Microsoft.Network/loadBalancers/mylb/inboundNatRules/myinboundnat
    data:    Name:                      myinboundnat
    data:    Type:                      Microsoft.Network/loadBalancers/inboundNatRules
    data:    Provisioning state:        Succeeded
    data:    Frontend IP Configuration: id=/subscriptions/###############################/resourceGroups/group-1/providers/Microsoft.Network/loadBalancers/mylb/frontendIPConfigurations/myfrontendip
    data:    Backend IP configuration
    data:    Protocol                   Tcp
    data:    Frontend port              81
    data:    Backend port               8080
    data:    Enable floating IP         false
    info:    network lb inbound-nat-rule set command OK

<span data-ttu-id="e9e77-251">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="e9e77-251">Parameter options:</span></span>

    -h, --help                                     output usage information
    -v, --verbose                                  use verbose output
    --json                                         use json output
    -g, --resource-group <resource-group>          hello name of hello resource group
    -l, --lb-name <lb-name>                        hello name of hello load balancer
    -n, --name <name>                              hello name of hello inbound NAT rule
    -p, --protocol <protocol>                      hello rule protocol [tcp,udp]
    -f, --frontend-port <frontend-port>            hello frontend port [0-65535]
    -b, --backend-port <backend-port>              hello backend port [0-65535]
    -e, --enable-floating-ip <enable-floating-ip>  enable floating point ip [true,false]
    -i, --frontend-ip <frontend-ip>                hello name of hello frontend ip configuration
    -m, --vm-id [vm-id]                            hello VM id.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Compute/virtualMachines/<vm-name>
    -a, --vm-name <vm-name>                        hello VM name.
    This virtual machine must exist in hello same resource group as hello lb.
    Please use vm-id if that is not hello case
    -s, --subscription <subscription>              hello subscription identifier
<BR>

    network lb inbound-nat-rule list [options] <resource-group> <lb-name>

<span data-ttu-id="e9e77-252">Hier worden alle binnenkomende nat-regels voor de load balancer.</span><span class="sxs-lookup"><span data-stu-id="e9e77-252">Lists all inbound nat rules for load balancer.</span></span>

    azure network lb inbound-nat-rule list -g myresourcegroup -l mylb

    info:    Executing command network lb inbound-nat-rule list
    + Looking up hello load balancer "mylb"
    data:    Name          Provisioning state  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes  Backend IP configuration
    data:    ------------  ------------------  --------  -------------  ------------  ------------------  -----------------------  ---
    ---------------------
    data:    myinboundnat  Succeeded           Tcp       81             8080          false               4

    info:    network lb inbound-nat-rule list command OK

<span data-ttu-id="e9e77-253">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="e9e77-253">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network lb inbound-nat-rule delete [options] <resource-group> <lb-name> <name>

<span data-ttu-id="e9e77-254">NAT-regel voor load balancer Hallo in een specifieke resourcegroep verwijderen.</span><span class="sxs-lookup"><span data-stu-id="e9e77-254">Deletes NAT rule for hello load balancer in a specific resource group.</span></span>

    azure network lb inbound-nat-rule delete -g myresourcegroup -l mylb -n myinboundnat

    info:    Executing command network lb inbound-nat-rule delete
    + Looking up hello load balancer "mylb"
    Delete inbound NAT rule "myinboundnat?" [y/n] y
    + Updating load balancer "mylb"
    info:    network lb inbound-nat-rule delete command OK

<span data-ttu-id="e9e77-255">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="e9e77-255">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello inbound NAT rule
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      hello subscription identifier

<span data-ttu-id="e9e77-256">**Opdrachten toomanage openbare IP-adressen**</span><span class="sxs-lookup"><span data-stu-id="e9e77-256">**Commands toomanage public ip addresses**</span></span>

    network public-ip create [options] <resource-group> <name> <location>
<span data-ttu-id="e9e77-257">Maakt een openbaar IP-resource.</span><span class="sxs-lookup"><span data-stu-id="e9e77-257">Creates a public ip resource.</span></span> <span data-ttu-id="e9e77-258">U maakt Hallo openbare IP-resource en domeinnaam tooa koppelen.</span><span class="sxs-lookup"><span data-stu-id="e9e77-258">You will create hello public ip resource and associate tooa domain name.</span></span>

    azure network public-ip create -g myresourcegroup -n mytestpublicip1 -l eastus -d azureclitest -a "Dynamic"
    info:    Executing command network public-ip create
    + Looking up hello public ip "mytestpublicip1"
    + Creating public ip address "mytestpublicip1"
    + Looking up hello public ip "mytestpublicip1"
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/publicIPAddresses/mytestpublicip1
    data:    Name:                 mytestpublicip1
    data:    Type:                 Microsoft.Network/publicIPAddresses
    data:    Location:             eastus
    data:    Provisioning state:   Succeeded
    data:    Allocation method:    Dynamic
    data:    Idle timeout:         4
    data:    Domain name label:    azureclitest
    data:    FQDN:                 azureclitest.eastus.cloudapp.azure.com
    info:    network public-ip create command OK


<span data-ttu-id="e9e77-259">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="e9e77-259">Parameter options:</span></span>

    -h, --help                                   output usage information
    -v, --verbose                                use verbose output
    --json                                       use json output
    -g, --resource-group <resource-group>        hello name of hello resource group
    -n, --name <name>                            hello name of hello public ip
    -l, --location <location>                    hello location
    -d, --domain-name-label <domain-name-label>  hello domain name label.
    This set DNS too<domain-name-label>.<location>.cloudapp.azure.com
    -a, --allocation-method <allocation-method>  hello allocation method [Static][Dynamic]
    -i, --idletimeout <idletimeout>              hello idle timeout in minutes
    -f, --reverse-fqdn <reverse-fqdn>            hello reverse fqdn
    -t, --tags <tags>                            hello list of tags.
    Can be multiple. In hello format of "name=value".
    Name is required and value is optional.
    For example, -t tag1=value1;tag2
    -s, --subscription <subscription>            hello subscription identifier
<br>

    network public-ip set [options] <resource-group> <name>
<span data-ttu-id="e9e77-260">Updates Hallo eigenschappen van een bestaande openbare IP-resource.</span><span class="sxs-lookup"><span data-stu-id="e9e77-260">Updates hello properties of an existing public ip resource.</span></span> <span data-ttu-id="e9e77-261">In het volgende voorbeeld Hallo gewijzigd we Hallo openbaar IP-adres van de dynamische tooStatic.</span><span class="sxs-lookup"><span data-stu-id="e9e77-261">In hello following example we changed hello public IP address from Dynamic tooStatic.</span></span>

    azure network public-ip set -g group-1 -n mytestpublicip1 -d azureclitest -a "Static"
    info:    Executing command network public-ip set
    + Looking up hello public ip "mytestpublicip1"
    + Updating public ip address "mytestpublicip1"
    + Looking up hello public ip "mytestpublicip1"
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/publicIPAddresses/mytestpublicip1
    data:    Name:                 mytestpublicip1
    data:    Type:                 Microsoft.Network/publicIPAddresses
    data:    Location:             eastus
    data:    Provisioning state:   Succeeded
    data:    Allocation method:    Static
    data:    Idle timeout:         4
    data:    IP Address:           (static IP address)
    data:    Domain name label:    azureclitest
    data:    FQDN:                 azureclitest.eastus.cloudapp.azure.com
    info:    network public-ip set command OK

<span data-ttu-id="e9e77-262">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="e9e77-262">Parameter options:</span></span>

    -h, --help                                   output usage information
    -v, --verbose                                use verbose output
    --json                                       use json output
    -g, --resource-group <resource-group>        hello name of hello resource group
    -n, --name <name>                            hello name of hello public ip
    -d, --domain-name-label [domain-name-label]  hello domain name label.
    This set DNS too<domain-name-label>.<location>.cloudapp.azure.com
    -a, --allocation-method <allocation-method>  hello allocation method [Static][Dynamic]
    -i, --idletimeout <idletimeout>              hello idle timeout in minutes
    -f, --reverse-fqdn [reverse-fqdn]            hello reverse fqdn
    -t, --tags <tags>                            hello list of tags.
    Can be multiple. In hello format of "name=value".
    Name is required and value is optional.
    For example, -t tag1=value1;tag2
    --no-tags                                    remove all existing tags
    -s, --subscription <subscription>            hello subscription identifier

<br>
    <span data-ttu-id="e9e77-263">lijst met openbare ip-netwerken [opties] < resource-group > geeft een lijst van alle openbare IP-resources binnen een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="e9e77-263">network public-ip list [options] <resource-group> Lists all public IP resources within a resource group.</span></span>

    azure network public-ip list -g myresourcegroup

    info:    Executing command network public-ip list
    + Getting hello public ip addresses
    data:    Name             Location  Allocation  IP Address    Idle timeout  DNS Name
    data:    ---------------  --------  ----------  ------------  ------------  -------------------------------------------
    data:    mypubip5         westus    Dynamic                   4             "domain name".westus.cloudapp.azure.com
    data:    myPublicIP       eastus    Dynamic                   4             "domain name".eastus.cloudapp.azure.com
    data:    mytestpublicip   eastus    Dynamic                   4             "domain name".eastus.cloudapp.azure.com
    data:    mytestpublicip1  eastus   Static (Static IP address) 4             azureclitest.eastus.cloudapp.azure.com

<span data-ttu-id="e9e77-264">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="e9e77-264">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -s, --subscription <subscription>      hello subscription identifier
<BR>
    <span data-ttu-id="e9e77-265">openbaar netwerk-IP-weergeven [opties] < resource-group ><name></span><span class="sxs-lookup"><span data-stu-id="e9e77-265">network public-ip show [options] <resource-group> <name></span></span>

<span data-ttu-id="e9e77-266">Openbare IP-eigenschappen van een openbaar IP-bron binnen een resourcegroep weergeven</span><span class="sxs-lookup"><span data-stu-id="e9e77-266">Displays public ip properties for a public ip resource within a resource group.</span></span>

    azure network public-ip show -g myresourcegroup -n mytestpublicip

    info:    Executing command network public-ip show
    + Looking up hello public ip "mytestpublicip1"
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/publicIPAddresses/mytestpublicip
    data:    Name:                 mytestpublicip
    data:    Type:                 Microsoft.Network/publicIPAddresses
    data:    Location:             eastus
    data:    Provisioning state:   Succeeded
    data:    Allocation method:    Static
    data:    Idle timeout:         4
    data:    IP Address:           (static IP address)
    data:    Domain name label:    azureclitest
    data:    FQDN:                 azureclitest.eastus.cloudapp.azure.com
    info:    network public-ip show command OK

<span data-ttu-id="e9e77-267">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="e9e77-267">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -n, --name <name>                      hello name of hello public IP
    -s, --subscription <subscription>      hello subscription identifier


    network public-ip delete [options] <resource-group> <name>

<span data-ttu-id="e9e77-268">Hiermee verwijdert u een openbaar IP-resource.</span><span class="sxs-lookup"><span data-stu-id="e9e77-268">Deletes public ip resource.</span></span>

    azure network public-ip delete -g group-1 -n mypublicipname
    info:    Executing command network public-ip delete
    + Looking up hello public ip "mypublicipname"
    Delete public ip address "mypublicipname"? [y/n] y
    + Deleting public ip address "mypublicipname"
    info:    network public-ip delete command OK

<span data-ttu-id="e9e77-269">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="e9e77-269">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -n, --name <name>                      hello name of hello public IP
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      hello subscription identifier


<span data-ttu-id="e9e77-270">**Opdrachten toomanage netwerkinterfaces**</span><span class="sxs-lookup"><span data-stu-id="e9e77-270">**Commands toomanage network interfaces**</span></span>

    network nic create [options] <resource-group> <name> <location>
<span data-ttu-id="e9e77-271">Maakt een resource aangeroepen netwerkinterface (NIC) die kan worden gebruikt voor load balancers of tooa virtuele Machine te koppelen.</span><span class="sxs-lookup"><span data-stu-id="e9e77-271">Creates a resource called network interface (NIC) which can be used for load balancers or associate tooa Virtual Machine.</span></span>

    azure network nic create -g myresourcegroup -l eastus -n testnic1 --subnet-name subnet-1 --subnet-vnet-name myvnet

    info:    Executing command network nic create
    + Looking up hello network interface "testnic1"
    + Looking up hello subnet "subnet-1"
    + Creating network interface "testnic1"
    + Looking up hello network interface "testnic1"
    data:    Id:                     /subscriptions/c4a17ddf-aa84-491c-b6f9-b90d882299f7/resourceGroups/group-1/providers/Microsoft.Network/networkInterfaces/testnic1
    data:    Name:                   testnic1
    data:    Type:                   Microsoft.Network/networkInterfaces
    data:    Location:               eastus
    data:    Provisioning state:     Succeeded
    data:    IP configurations:
    data:       Name:                         NIC-config
    data:       Provisioning state:           Succeeded
    data:       Private IP address:           10.0.0.5
    data:       Private IP Allocation Method: Dynamic
    data:       Subnet:                       /subscriptions/c4a17ddf-aa84-491c-b6f9-b90d882299f7/resourceGroups/group-1/providers/Microsoft.Network/virtualNetworks/myVNET/subnets/Subnet-1

<span data-ttu-id="e9e77-272">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="e9e77-272">Parameter options:</span></span>

    -h, --help                                                       output usage information
    -v, --verbose                                                    use verbose output
    --json                                                           use json output
    -g, --resource-group <resource-group>                            hello name of hello resource group
    -n, --name <name>                                                hello name of hello network interface
    -l, --location <location>                                        hello location
    -w, --network-security-group-id <network-security-group-id>      hello network security group identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/networkSecurityGroups/<nsg-name>
    -o, --network-security-group-name <network-security-group-name>  hello network security group name.
    This network security group must exist in hello same resource group as hello nic.
    Please use network-security-group-id if that is not hello case.
    -i, --public-ip-id <public-ip-id>                                hello public IP identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/publicIPAddresses/<public-ip-name>
    -p, --public-ip-name <public-ip-name>                            hello public IP name.
    This public ip must exist in hello same resource group as hello nic.
    Please use public-ip-id if that is not hello case.
    -a, --private-ip-address <private-ip-address>                    hello private IP address
    -u, --subnet-id <subnet-id>                                      hello subnet identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<vnet-name>/subnets/<subnet-name>
    --subnet-name <subnet-name>                                  hello subnet name
    -m, --subnet-vnet-name <subnet-vnet-name>                        hello vnet name under which subnet-name exists
    -t, --tags <tags>                                                hello comma seperated list of tags.
    Can be multiple. In hello format of "name=value".
    Name is required and value is optional.
    For example, -t tag1=value1;tag2
    -s, --subscription <subscription>                                hello subscription identifier
    data:
    info:    network nic create command OK

<BR>

    network nic set [options] <resource-group> <name>

    network nic list [options] <resource-group>
    network nic show [options] <resource-group> <name>
    network nic delete [options] <resource-group> <name>

<span data-ttu-id="e9e77-273">**Opdrachten toomanage netwerkbeveiligingsgroepen**</span><span class="sxs-lookup"><span data-stu-id="e9e77-273">**Commands toomanage network security groups**</span></span>

    network nsg create [options] <resource-group> <name> <location>
    network nsg set [options] <resource-group> <name>
    network nsg list [options] <resource-group>
    network nsg show [options] <resource-group> <name>
    network nsg delete [options] <resource-group> <name>

<span data-ttu-id="e9e77-274">**Opdrachten toomanage netwerkbeveiligingsgroepen**</span><span class="sxs-lookup"><span data-stu-id="e9e77-274">**Commands toomanage network security group rules**</span></span>

    network nsg rule create [options] <resource-group> <nsg-name> <name>
    network nsg rule set [options] <resource-group> <nsg-name> <name>
    network nsg rule list [options] <resource-group> <nsg-name>
    network nsg rule show [options] <resource-group> <nsg-name> <name>
    network nsg rule delete [options] <resource-group> <nsg-name> <name>

<span data-ttu-id="e9e77-275">**Opdrachten toomanage traffic manager-profiel**</span><span class="sxs-lookup"><span data-stu-id="e9e77-275">**Commands toomanage traffic manager profile**</span></span>

    network traffic-manager profile create [options] <resource-group> <name>
    network traffic-manager profile set [options] <resource-group> <name>
    network traffic-manager profile list [options] <resource-group>
    network traffic-manager profile show [options] <resource-group> <name>
    network traffic-manager profile delete [options] <resource-group> <name>
    network traffic-manager profile is-dns-available [options] <resource-group> <relative-dns-name>

<span data-ttu-id="e9e77-276">**Opdrachten toomanage traffic manager-eindpunten**</span><span class="sxs-lookup"><span data-stu-id="e9e77-276">**Commands toomanage traffic manager endpoints**</span></span>

    network traffic-manager profile endpoint create [options] <resource-group> <profile-name> <name> <endpoint-location>
    network traffic-manager profile endpoint set [options] <resource-group> <profile-name> <name>
    network traffic-manager profile endpoint delete [options] <resource-group> <profile-name> <name>

<span data-ttu-id="e9e77-277">**Opdrachten toomanage virtuele netwerkgateways**</span><span class="sxs-lookup"><span data-stu-id="e9e77-277">**Commands toomanage virtual network gateways**</span></span>

    network gateway list [options] <resource-group>

## <a name="azure-provider-commands-toomanage-resource-provider-registrations"></a><span data-ttu-id="e9e77-278">Azure-provider: toomanage resource provider registraties opdrachten</span><span class="sxs-lookup"><span data-stu-id="e9e77-278">azure provider: Commands toomanage resource provider registrations</span></span>
<span data-ttu-id="e9e77-279">**Lijst van de momenteel geregistreerde providers in Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="e9e77-279">**List currently registered providers in Resource Manager**</span></span>

    provider list [options]

<span data-ttu-id="e9e77-280">**Details weergeven over Hallo aangevraagd providernaamruimte**</span><span class="sxs-lookup"><span data-stu-id="e9e77-280">**Show details about hello requested provider namespace**</span></span>

    provider show [options] <namespace>

<span data-ttu-id="e9e77-281">**Registreer provider bij Hallo-abonnement**</span><span class="sxs-lookup"><span data-stu-id="e9e77-281">**Register provider with hello subscription**</span></span>

    provider register [options] <namespace>

<span data-ttu-id="e9e77-282">**Hef de registratie van provider met Hallo-abonnement**</span><span class="sxs-lookup"><span data-stu-id="e9e77-282">**Unregister provider with hello subscription**</span></span>

    provider unregister [options] <namespace>

## <a name="azure-resource-commands-toomanage-your-resources"></a><span data-ttu-id="e9e77-283">Azure-resource: opdrachten toomanage uw resources</span><span class="sxs-lookup"><span data-stu-id="e9e77-283">azure resource: Commands toomanage your resources</span></span>
<span data-ttu-id="e9e77-284">**Maakt een resource in een resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="e9e77-284">**Creates a resource in a resource group**</span></span>

    resource create [options] <resource-group> <name> <resource-type> <location> <api-version>

<span data-ttu-id="e9e77-285">**Updates van een resource in een resourcegroep zonder parameters of sjablonen**</span><span class="sxs-lookup"><span data-stu-id="e9e77-285">**Updates a resource in a resource group without any templates or parameters**</span></span>

    resource set [options] <resource-group> <name> <resource-type> <properties> <api-version>

<span data-ttu-id="e9e77-286">**Een lijst met Hallo resources**</span><span class="sxs-lookup"><span data-stu-id="e9e77-286">**Lists hello resources**</span></span>

    resource list [options] [resource-group]

<span data-ttu-id="e9e77-287">**Een bron binnen een resourcegroep of abonnement opgehaald**</span><span class="sxs-lookup"><span data-stu-id="e9e77-287">**Gets one resource within a resource group or subscription**</span></span>

    resource show [options] <resource-group> <name> <resource-type> <api-version>

<span data-ttu-id="e9e77-288">**Hiermee verwijdert u een resource in een resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="e9e77-288">**Deletes a resource in a resource group**</span></span>

    resource delete [options] <resource-group> <name> <resource-type> <api-version>

## <a name="azure-role-commands-toomanage-your-azure-roles"></a><span data-ttu-id="e9e77-289">Azure-functie: opdrachten toomanage uw Azure-functies</span><span class="sxs-lookup"><span data-stu-id="e9e77-289">azure role: Commands toomanage your Azure roles</span></span>
<span data-ttu-id="e9e77-290">**Alle beschikbare roldefinities ophalen**</span><span class="sxs-lookup"><span data-stu-id="e9e77-290">**Get all available role definitions**</span></span>

    role list [options]

<span data-ttu-id="e9e77-291">**Een beschikbare roldefinitie ophalen**</span><span class="sxs-lookup"><span data-stu-id="e9e77-291">**Get an available role definition**</span></span>

    role show [options] [name]

<span data-ttu-id="e9e77-292">**Opdrachten toomanage toegewezen rollen**</span><span class="sxs-lookup"><span data-stu-id="e9e77-292">**Commands toomanage your role assignment**</span></span>

    role assignment create [options] [objectId] [upn] [mail] [spn] [role] [scope] [resource-group] [resource-type] [resource-name]
    role assignment list [options] [objectId] [upn] [mail] [spn] [role] [scope] [resource-group] [resource-type] [resource-name]
    role assignment delete [options] [objectId] [upn] [mail] [spn] [role] [scope] [resource-group] [resource-type] [resource-name]

## <a name="azure-storage-commands-toomanage-your-storage-objects"></a><span data-ttu-id="e9e77-293">Azure-opslag: opdrachten toomanage uw opslagobjecten</span><span class="sxs-lookup"><span data-stu-id="e9e77-293">azure storage: Commands toomanage your Storage objects</span></span>
<span data-ttu-id="e9e77-294">**Opdrachten toomanage uw Storage-accounts**</span><span class="sxs-lookup"><span data-stu-id="e9e77-294">**Commands toomanage your Storage accounts**</span></span>

    storage account list [options]
    storage account show [options] <name>
    storage account create [options] <name>
    storage account set [options] <name>
    storage account delete [options] <name>

<span data-ttu-id="e9e77-295">**Opdrachten toomanage uw toegangscodes voor opslag**</span><span class="sxs-lookup"><span data-stu-id="e9e77-295">**Commands toomanage your Storage account keys**</span></span>

    storage account keys list [options] <name>
    storage account keys renew [options] <name>

<span data-ttu-id="e9e77-296">**Opdrachten tooshow uw verbindingsreeks voor opslag**</span><span class="sxs-lookup"><span data-stu-id="e9e77-296">**Commands tooshow your Storage connection string**</span></span>

    storage account connectionstring show [options] <name>

<span data-ttu-id="e9e77-297">**Opdrachten toomanage uw Storage-containers**</span><span class="sxs-lookup"><span data-stu-id="e9e77-297">**Commands toomanage your Storage containers**</span></span>

    storage container list [options] [prefix]
    storage container show [options] [container]
    storage container create [options] [container]
    storage container delete [options] [container]
    storage container set [options] [container]

<span data-ttu-id="e9e77-298">**Handtekeningen voor opdrachten toomanage gedeelde toegang van uw Storage-container**</span><span class="sxs-lookup"><span data-stu-id="e9e77-298">**Commands toomanage shared access signatures of your Storage container**</span></span>

    storage container sas create [options] [container] [permissions] [expiry]

<span data-ttu-id="e9e77-299">**Opdrachten toomanage opgeslagen-beleid van uw Storage-container**</span><span class="sxs-lookup"><span data-stu-id="e9e77-299">**Commands toomanage stored access policies of your Storage container**</span></span>

    storage container policy create [options] [container] [name]
    storage container policy show [options] [container] [name]
    storage container policy list [options] [container]
    storage container policy set [options] [container] [name]
    storage container policy delete [options] [container] [name]

<span data-ttu-id="e9e77-300">**Opdrachten toomanage uw Storage-blobs**</span><span class="sxs-lookup"><span data-stu-id="e9e77-300">**Commands toomanage your Storage blobs**</span></span>

    storage blob list [options] [container] [prefix]
    storage blob show [options] [container] [blob]
    storage blob delete [options] [container] [blob]
    storage blob upload [options] [file] [container] [blob]
    storage blob download [options] [container] [blob] [destination]

<span data-ttu-id="e9e77-301">**Opdrachten toomanage uw kopieerbewerkingen blob**</span><span class="sxs-lookup"><span data-stu-id="e9e77-301">**Commands toomanage your blob copy operations**</span></span>

    storage blob copy start [options] [sourceUri] [destContainer]
    storage blob copy show [options] [container] [blob]
    storage blob copy stop [options] [container] [blob] [copyid]

<span data-ttu-id="e9e77-302">**Shared access signature voor opdrachten toomanage van uw Storage-blob**</span><span class="sxs-lookup"><span data-stu-id="e9e77-302">**Commands toomanage shared access signature of your Storage blob**</span></span>

    storage blob sas create [options] [container] [blob] [permissions] [expiry]

<span data-ttu-id="e9e77-303">**Opdrachten toomanage uw bestandsshares voor opslag**</span><span class="sxs-lookup"><span data-stu-id="e9e77-303">**Commands toomanage your Storage file shares**</span></span>

    storage share create [options] [share]
    storage share show [options] [share]
    storage share delete [options] [share]
    storage share list [options] [prefix]

<span data-ttu-id="e9e77-304">**Opdrachten toomanage uw opslag-bestanden**</span><span class="sxs-lookup"><span data-stu-id="e9e77-304">**Commands toomanage your Storage files**</span></span>

    storage file list [options] [share] [path]
    storage file delete [options] [share] [path]
    storage file upload [options] [source] [share] [path]
    storage file download [options] [share] [path] [destination]

<span data-ttu-id="e9e77-305">**Opdrachten toomanage map van uw opslag**</span><span class="sxs-lookup"><span data-stu-id="e9e77-305">**Commands toomanage your Storage file directory**</span></span>

    storage directory create [options] [share] [path]
    storage directory delete [options] [share] [path]

<span data-ttu-id="e9e77-306">**Opdrachten toomanage uw opslagwachtrijen**</span><span class="sxs-lookup"><span data-stu-id="e9e77-306">**Commands toomanage your Storage queues**</span></span>

    storage queue create [options] [queue]
    storage queue list [options] [prefix]
    storage queue show [options] [queue]
    storage queue delete [options] [queue]

<span data-ttu-id="e9e77-307">**Handtekeningen voor opdrachten toomanage gedeelde toegang van uw Storage-wachtrij**</span><span class="sxs-lookup"><span data-stu-id="e9e77-307">**Commands toomanage shared access signatures of your Storage queue**</span></span>

    storage queue sas create [options] [queue] [permissions] [expiry]

<span data-ttu-id="e9e77-308">**Opdrachten toomanage opgeslagen-beleid van uw Storage-wachtrij**</span><span class="sxs-lookup"><span data-stu-id="e9e77-308">**Commands toomanage stored access policies of your Storage queue**</span></span>

    storage queue policy create [options] [queue] [name]
    storage queue policy show [options] [queue] [name]
    storage queue policy list [options] [queue]
    storage queue policy set [options] [queue] [name]
    storage queue policy delete [options] [queue] [name]

<span data-ttu-id="e9e77-309">**Opdrachten toomanage uw opslag logboekregistratie-eigenschappen**</span><span class="sxs-lookup"><span data-stu-id="e9e77-309">**Commands toomanage your Storage logging properties**</span></span>

    storage logging show [options]
    storage logging set [options]

<span data-ttu-id="e9e77-310">**Opdrachten toomanage de eigenschappen van de metrische gegevens van uw opslag**</span><span class="sxs-lookup"><span data-stu-id="e9e77-310">**Commands toomanage your Storage metrics properties**</span></span>

    storage metrics show [options]
    storage metrics set [options]

<span data-ttu-id="e9e77-311">**Opdrachten toomanage uw Storage-tabellen**</span><span class="sxs-lookup"><span data-stu-id="e9e77-311">**Commands toomanage your Storage tables**</span></span>

    storage table create [options] [table]
    storage table list [options] [prefix]
    storage table show [options] [table]
    storage table delete [options] [table]

<span data-ttu-id="e9e77-312">**Handtekeningen voor opdrachten toomanage gedeelde toegang van de tabel opslag**</span><span class="sxs-lookup"><span data-stu-id="e9e77-312">**Commands toomanage shared access signatures of your Storage table**</span></span>

    storage table sas create [options] [table] [permissions] [expiry]

<span data-ttu-id="e9e77-313">**Opdrachten toomanage opgeslagen toegangsbeleid van de tabel opslag**</span><span class="sxs-lookup"><span data-stu-id="e9e77-313">**Commands toomanage stored access policies of your Storage table**</span></span>

    storage table policy create [options] [table] [name]
    storage table policy show [options] [table] [name]
    storage table policy list [options] [table]
    storage table policy set [options] [table] [name]
    storage table policy delete [options] [table] [name]

## <a name="azure-tag-commands-toomanage-your-resource-manager-tag"></a><span data-ttu-id="e9e77-314">Azure-tag: het label van resource manager-toomanage opdrachten</span><span class="sxs-lookup"><span data-stu-id="e9e77-314">azure tag: Commands toomanage your resource manager tag</span></span>
<span data-ttu-id="e9e77-315">**Een label toevoegen**</span><span class="sxs-lookup"><span data-stu-id="e9e77-315">**Add a tag**</span></span>

    tag create [options] <name> <value>

<span data-ttu-id="e9e77-316">**Een HTML-code of een tagwaarde verwijderen**</span><span class="sxs-lookup"><span data-stu-id="e9e77-316">**Remove an entire tag or a tag value**</span></span>

    tag delete [options] <name> <value>

<span data-ttu-id="e9e77-317">**Een lijst met Hallo-tag-informatie**</span><span class="sxs-lookup"><span data-stu-id="e9e77-317">**Lists hello tag information**</span></span>

    tag list [options]

<span data-ttu-id="e9e77-318">**Een label ophalen**</span><span class="sxs-lookup"><span data-stu-id="e9e77-318">**Get a tag**</span></span>

    tag show [options] [name]

## <a name="azure-vm-commands-toomanage-your-azure-virtual-machines"></a><span data-ttu-id="e9e77-319">Azure vm: opdrachten toomanage uw Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="e9e77-319">azure vm: Commands toomanage your Azure Virtual Machines</span></span>
<span data-ttu-id="e9e77-320">**Een virtuele machine maken**</span><span class="sxs-lookup"><span data-stu-id="e9e77-320">**Create a VM**</span></span>

    vm create [options] <resource-group> <name> <location> <os-type>

<span data-ttu-id="e9e77-321">**Een virtuele machine maken met de standaardresources**</span><span class="sxs-lookup"><span data-stu-id="e9e77-321">**Create a VM with default resources**</span></span>

    vm quick-create [options] <resource-group> <name> <location> <os-type> <image-urn> <admin-username> <admin-password

> [!TIP]
> <span data-ttu-id="e9e77-322">Beginnen met CLI versie 0.10, kunt u een korte alias zoals 'UbuntuLTS' of 'Win2012R2Datacenter' als Hallo bieden `image-urn` voor bepaalde populaire Marketplace-installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="e9e77-322">Starting with CLI version 0.10, you can provide a short alias such as "UbuntuLTS" or "Win2012R2Datacenter" as hello `image-urn` for some popular Marketplace images.</span></span> <span data-ttu-id="e9e77-323">Voer `azure help vm quick-create` voor opties.</span><span class="sxs-lookup"><span data-stu-id="e9e77-323">Run `azure help vm quick-create` for options.</span></span> <span data-ttu-id="e9e77-324">Bovendien vanaf versie 0.10, `azure vm quick-create` premium-opslag wordt standaard gebruikt als deze beschikbaar in de geselecteerde regio Hallo is.</span><span class="sxs-lookup"><span data-stu-id="e9e77-324">Additionally, starting with version 0.10, `azure vm quick-create` uses premium storage by default if it's available in hello selected region.</span></span>
> 
> 

<span data-ttu-id="e9e77-325">**Lijst Hallo virtuele machines binnen een account**</span><span class="sxs-lookup"><span data-stu-id="e9e77-325">**List hello virtual machines within an account**</span></span>

    vm list [options]

<span data-ttu-id="e9e77-326">**Ophalen van een virtuele machine binnen een resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="e9e77-326">**Get one virtual machine within a resource group**</span></span>

    vm show [options] <resource-group> <name>

<span data-ttu-id="e9e77-327">**Een virtuele machine in de resourcegroep verwijderen**</span><span class="sxs-lookup"><span data-stu-id="e9e77-327">**Delete one virtual machine within a resource group**</span></span>

    vm delete [options] <resource-group> <name>

<span data-ttu-id="e9e77-328">**Een virtuele machine afsluiten binnen een resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="e9e77-328">**Shutdown one virtual machine within a resource group**</span></span>

    vm stop [options] <resource-group> <name>

<span data-ttu-id="e9e77-329">**Een virtuele machine binnen een resourcegroep opnieuw starten**</span><span class="sxs-lookup"><span data-stu-id="e9e77-329">**Restart one virtual machine within a resource group**</span></span>

    vm restart [options] <resource-group> <name>

<span data-ttu-id="e9e77-330">**Start één virtuele machine binnen een resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="e9e77-330">**Start one virtual machine within a resource group**</span></span>

    vm start [options] <resource-group> <name>

<span data-ttu-id="e9e77-331">**Afsluiten één virtuele machine binnen een resource-groep en releases Hallo bronnen berekenen**</span><span class="sxs-lookup"><span data-stu-id="e9e77-331">**Shutdown one virtual machine within a resource group and releases hello compute resources**</span></span>

    vm deallocate [options] <resource-group> <name>

<span data-ttu-id="e9e77-332">**Lijst met beschikbare virtuele machine grootten**</span><span class="sxs-lookup"><span data-stu-id="e9e77-332">**List available virtual machine sizes**</span></span>

    vm sizes [options]

<span data-ttu-id="e9e77-333">**Hallo VM als de installatiekopie van het besturingssysteem of VM-installatiekopie vastleggen**</span><span class="sxs-lookup"><span data-stu-id="e9e77-333">**Capture hello VM as OS Image or VM Image**</span></span>

    vm capture [options] <resource-group> <name> <vhd-name-prefix>

<span data-ttu-id="e9e77-334">**Hallo-status van Hallo VM tooGeneralized instellen**</span><span class="sxs-lookup"><span data-stu-id="e9e77-334">**Set hello state of hello VM tooGeneralized**</span></span>

    vm generalize [options] <resource-group> <name>

<span data-ttu-id="e9e77-335">**Instantieweergave van Hallo VM ophalen**</span><span class="sxs-lookup"><span data-stu-id="e9e77-335">**Get instance view of hello VM**</span></span>

    vm get-instance-view [options] <resource-group> <name>

<span data-ttu-id="e9e77-336">**Kunt u tooreset externe toegang tot het bureaublad of SSH-instellingen op een virtuele Machine en tooreset Hallo wachtwoord voor Hallo-account met administrator of sudo-instantie**</span><span class="sxs-lookup"><span data-stu-id="e9e77-336">**Enable you tooreset Remote Desktop Access or SSH settings on a Virtual Machine and tooreset hello password for hello account that has administrator or sudo authority**</span></span>

    vm reset-access [options] <resource-group> <name>

<span data-ttu-id="e9e77-337">**Virtuele machine bijwerken met nieuwe gegevens**</span><span class="sxs-lookup"><span data-stu-id="e9e77-337">**Update VM with new data**</span></span>

    vm set [options] <resource-group> <name>

<span data-ttu-id="e9e77-338">**Opdrachten toomanage de gegevensschijven van de virtuele Machine**</span><span class="sxs-lookup"><span data-stu-id="e9e77-338">**Commands toomanage your Virtual Machine data disks**</span></span>

    vm disk attach-new [options] <resource-group> <vm-name> <size-in-gb> [vhd-name]
    vm disk detach [options] <resource-group> <vm-name> <lun>
    vm disk attach [options] <resource-group> <vm-name> [vhd-url]

<span data-ttu-id="e9e77-339">**Opdrachten toomanage VM resource-uitbreidingen**</span><span class="sxs-lookup"><span data-stu-id="e9e77-339">**Commands toomanage VM resource extensions**</span></span>

    vm extension set [options] <resource-group> <vm-name> <name> <publisher-name> <version>
    vm extension get [options] <resource-group> <vm-name>

<span data-ttu-id="e9e77-340">**De virtuele Machine van Docker-toomanage opdrachten**</span><span class="sxs-lookup"><span data-stu-id="e9e77-340">**Commands toomanage your Docker Virtual Machine**</span></span>

    vm docker create [options] <resource-group> <name> <location> <os-type>

<span data-ttu-id="e9e77-341">**Opdrachten toomanage VM-installatiekopieën**</span><span class="sxs-lookup"><span data-stu-id="e9e77-341">**Commands toomanage VM images**</span></span>

    vm image list-publishers [options] <location>
    vm image list-offers [options] <location> <publisher>
    vm image list-skus [options] <location> <publisher> <offer>
    vm image list [options] <location> <publisher> [offer] [sku]
