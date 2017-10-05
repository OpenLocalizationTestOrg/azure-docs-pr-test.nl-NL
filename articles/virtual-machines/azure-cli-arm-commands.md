---
title: Azure CLI-opdrachten in de modus Resource Manager | Microsoft Docs
description: Azure opdrachtregelinterface (CLI)-opdrachten voor het beheren van resources in het Resource Manager-implementatiemodel
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
ms.openlocfilehash: be957651af78519f678321aec511b71cb18a85f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cli-commands-in-resource-manager-mode"></a><span data-ttu-id="409a9-103">Azure CLI-opdrachten in de modus Resource Manager</span><span class="sxs-lookup"><span data-stu-id="409a9-103">Azure CLI commands in Resource Manager mode</span></span>
<span data-ttu-id="409a9-104">Dit artikel bevat syntaxis en opties voor Azure-opdrachtregelinterface (CLI)-opdrachten die u meestal gebruikt maken en beheren van Azure-resources in het Azure Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="409a9-104">This article provides syntax and options for Azure command-line interface (CLI) commands you'd commonly use to create and manage Azure resources in the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="409a9-105">U toegang tot deze opdrachten door de CLI in de modus Resource Manager (arm).</span><span class="sxs-lookup"><span data-stu-id="409a9-105">You access these commands by running the CLI in Resource Manager (arm) mode.</span></span> <span data-ttu-id="409a9-106">Dit is niet een volledig overzicht en uw versie van de CLI kan enigszins verschillen opdrachten of parameters weergeven.</span><span class="sxs-lookup"><span data-stu-id="409a9-106">This is not a complete reference, and your CLI version may show slightly different commands or parameters.</span></span> <span data-ttu-id="409a9-107">Zie voor een algemeen overzicht van Azure-resources en resourcegroepen [overzicht van Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="409a9-107">For a general overview of Azure resources and resource groups, see [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>  

> [!NOTE]
> <span data-ttu-id="409a9-108">Dit artikel laat zien Resource Manager opdrachten in de modus in de Azure CLI, ook wel Azure CLI 1.0 genoemd.</span><span class="sxs-lookup"><span data-stu-id="409a9-108">This article shows Resource Manager mode commands in the Azure CLI, sometimes called Azure CLI 1.0.</span></span> <span data-ttu-id="409a9-109">Om te werken in het Resource Manager-model, u kunt ook proberen de [Azure CLI 2.0](/cli/azure/install-az-cli2), de volgende generatie meerdere platforms CLI.</span><span class="sxs-lookup"><span data-stu-id="409a9-109">To work in the Resource Manager model, you can also try the [Azure CLI 2.0](/cli/azure/install-az-cli2), our next generation multi-platform CLI.</span></span>
><span data-ttu-id="409a9-110">Meer informatie over de [oude en nieuwe Azure CLIs](/cli/azure/old-and-new-clis).</span><span class="sxs-lookup"><span data-stu-id="409a9-110">Find out more about the [old and new Azure CLIs](/cli/azure/old-and-new-clis).</span></span>
>

<span data-ttu-id="409a9-111">Aan de slag eerst [Azure CLI installeren](../cli-install-nodejs.md) en [verbinding maken met uw Azure-abonnement](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="409a9-111">To get started, first [install the Azure CLI](../cli-install-nodejs.md) and [connect to your Azure subscription](../xplat-cli-connect.md).</span></span>

<span data-ttu-id="409a9-112">Typ voor de huidige opdrachtsyntaxis en -opties op de opdrachtregel in de modus Resource Manager `azure help` of help weergeven voor een specifieke opdracht `azure help [command]`.</span><span class="sxs-lookup"><span data-stu-id="409a9-112">For current command syntax and options at the command line in Resource Manager mode, type `azure help` or, to display help for a specific command, `azure help [command]`.</span></span> <span data-ttu-id="409a9-113">CLI-voorbeelden in de documentatie ook vinden voor het maken en beheren van specifieke Azure-services.</span><span class="sxs-lookup"><span data-stu-id="409a9-113">Also find CLI examples in the documentation for creating and managing specific Azure services.</span></span>

<span data-ttu-id="409a9-114">Optionele parameters staan tussen vierkante haken (bijvoorbeeld `[parameter]`).</span><span class="sxs-lookup"><span data-stu-id="409a9-114">Optional parameters are shown in square brackets (for example, `[parameter]`).</span></span> <span data-ttu-id="409a9-115">Alle andere parameters zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="409a9-115">All other parameters are required.</span></span>

<span data-ttu-id="409a9-116">Naast de optionele parameters opdracht-specifieke ze hier zijn beschreven, zijn er drie optionele parameters die kunnen worden gebruikt om gedetailleerde uitvoer zoals opties voor aanvraag- en statuscodes weer te geven.</span><span class="sxs-lookup"><span data-stu-id="409a9-116">In addition to command-specific optional parameters documented here, there are three optional parameters that can be used to display detailed output such as request options and status codes.</span></span> <span data-ttu-id="409a9-117">De `-v` parameter biedt uitgebreide uitvoer en de `-vv` parameter biedt nog meer gedetailleerde uitgebreide uitvoer.</span><span class="sxs-lookup"><span data-stu-id="409a9-117">The `-v` parameter provides verbose output, and the `-vv` parameter provides even more detailed verbose output.</span></span> <span data-ttu-id="409a9-118">De `--json` optie wordt het resultaat in de onbewerkte json-indeling.</span><span class="sxs-lookup"><span data-stu-id="409a9-118">The `--json` option outputs the result in raw json format.</span></span>

## <a name="setting-the-resource-manager-mode"></a><span data-ttu-id="409a9-119">De modus Resource Manager instellen</span><span class="sxs-lookup"><span data-stu-id="409a9-119">Setting the Resource Manager mode</span></span>
<span data-ttu-id="409a9-120">Gebruik de volgende opdracht om in te schakelen van opdrachten in de modus Azure CLI Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="409a9-120">Use the following command to enable Azure CLI Resource Manager mode commands.</span></span>

    azure config mode arm

> [!NOTE]
> <span data-ttu-id="409a9-121">De modus Azure Resource Manager en Azure Service Management-modus van de CLI elkaar wederzijds uit.</span><span class="sxs-lookup"><span data-stu-id="409a9-121">The CLI's Azure Resource Manager mode and Azure Service Management mode are mutually exclusive.</span></span> <span data-ttu-id="409a9-122">Dat wil zeggen, kunnen niet resources die zijn gemaakt in de modus voor één worden beheerd vanaf de andere modus.</span><span class="sxs-lookup"><span data-stu-id="409a9-122">That is, resources created in one mode cannot be managed from the other mode.</span></span>
> 
> 

## <a name="azure-account-manage-your-account-information"></a><span data-ttu-id="409a9-123">Azure-account: gegevens over uw account beheren</span><span class="sxs-lookup"><span data-stu-id="409a9-123">azure account: Manage your account information</span></span>
<span data-ttu-id="409a9-124">De informatie van uw Azure-abonnement wordt gebruikt door het hulpprogramma verbinding maken met uw account.</span><span class="sxs-lookup"><span data-stu-id="409a9-124">Your Azure subscription information is used by the tool to connect to your account.</span></span>

<span data-ttu-id="409a9-125">**Lijst van de geïmporteerde abonnementen**</span><span class="sxs-lookup"><span data-stu-id="409a9-125">**List the imported subscriptions**</span></span>

    account list [options]

<span data-ttu-id="409a9-126">**Details weergeven over een abonnement op**</span><span class="sxs-lookup"><span data-stu-id="409a9-126">**Show details about a subscription**</span></span>  

    account show [options] [subscriptionNameOrId]

<span data-ttu-id="409a9-127">**Instellen van het huidige abonnement**</span><span class="sxs-lookup"><span data-stu-id="409a9-127">**Set the current subscription**</span></span>

    account set [options] <subscriptionNameOrId>

<span data-ttu-id="409a9-128">**Verwijderen van een abonnement of de omgeving of wis dan alle opgeslagen gegevens van de account en de omgeving**</span><span class="sxs-lookup"><span data-stu-id="409a9-128">**Remove a subscription or environment, or clear all of the stored account and environment info**</span></span>  

    account clear [options]

<span data-ttu-id="409a9-129">**Opdrachten voor het beheren van uw account-omgeving**</span><span class="sxs-lookup"><span data-stu-id="409a9-129">**Commands to manage your account environment**</span></span>  

    account env list [options]
    account env show [options] [environment]
    account env add [options] [environment]
    account env set [options] [environment]
    account env delete [options] [environment]

## <a name="azure-ad-commands-to-display-active-directory-objects"></a><span data-ttu-id="409a9-130">Azure ad: opdrachten voor het Active Directory-objecten weergeven</span><span class="sxs-lookup"><span data-stu-id="409a9-130">azure ad: Commands to display Active Directory objects</span></span>
<span data-ttu-id="409a9-131">**Opdrachten voor het weergeven van active directory-toepassingen**</span><span class="sxs-lookup"><span data-stu-id="409a9-131">**Commands to display active directory applications**</span></span>

    ad app create [options]
    ad app delete [options] <object-id>

<span data-ttu-id="409a9-132">**Opdrachten voor het weergeven van active directory-groepen**</span><span class="sxs-lookup"><span data-stu-id="409a9-132">**Commands to display active directory groups**</span></span>

    ad group list [options]
    ad group show [options]

<span data-ttu-id="409a9-133">**Opdrachten voor het bieden van een active directory-sub groeps- of -info**</span><span class="sxs-lookup"><span data-stu-id="409a9-133">**Commands to provide an active directory sub group or member info**</span></span>

    ad group member list [options] [objectId]

<span data-ttu-id="409a9-134">**Opdrachten voor het weergeven van active directory-service-principals**</span><span class="sxs-lookup"><span data-stu-id="409a9-134">**Commands to display active directory service principals**</span></span>

    ad sp list [options]
    ad sp show [options]
    ad sp create [options] <application-id>
    ad sp delete [options] <object-id>

<span data-ttu-id="409a9-135">**Opdrachten voor het weergeven van active directory-gebruikers**</span><span class="sxs-lookup"><span data-stu-id="409a9-135">**Commands to display active directory users**</span></span>

    ad user list [options]
    ad user show [options]

## <a name="azure-availset-commands-to-manage-your-availability-sets"></a><span data-ttu-id="409a9-136">Azure availset: opdrachten voor het beheren van uw beschikbaarheidssets</span><span class="sxs-lookup"><span data-stu-id="409a9-136">azure availset: commands to manage your availability sets</span></span>
<span data-ttu-id="409a9-137">**Hiermee maakt u een beschikbaarheidsset binnen een resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="409a9-137">**Creates an availability set within a resource group**</span></span>

    availset create [options] <resource-group> <name> <location> [tags]

<span data-ttu-id="409a9-138">**Geeft een lijst van de beschikbaarheidssets in de resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="409a9-138">**Lists the availability sets within a resource group**</span></span>

    availset list [options] <resource-group>

<span data-ttu-id="409a9-139">**Een beschikbaarheidsset binnen een resourcegroep opgehaald**</span><span class="sxs-lookup"><span data-stu-id="409a9-139">**Gets one availability set within a resource group**</span></span>

    availset show [options] <resource-group> <name>

<span data-ttu-id="409a9-140">**Hiermee verwijdert u één beschikbaarheidsset binnen een resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="409a9-140">**Deletes one availability set within a resource group**</span></span>

    availset delete [options] <resource-group> <name>

## <a name="azure-config-commands-to-manage-your-local-settings"></a><span data-ttu-id="409a9-141">Azure config: opdrachten voor het beheren van uw lokale instellingen</span><span class="sxs-lookup"><span data-stu-id="409a9-141">azure config: commands to manage your local settings</span></span>
<span data-ttu-id="409a9-142">**Configuratie-instellingen van lijst met Azure CLI**</span><span class="sxs-lookup"><span data-stu-id="409a9-142">**List Azure CLI configuration settings**</span></span>

    config list [options]

<span data-ttu-id="409a9-143">**Een configuratie-instelling niet verwijderen**</span><span class="sxs-lookup"><span data-stu-id="409a9-143">**Delete a config setting**</span></span>

    config delete [options] <name>

<span data-ttu-id="409a9-144">**Bijwerken van een configuratie-instelling**</span><span class="sxs-lookup"><span data-stu-id="409a9-144">**Update a config setting**</span></span>

    config set <name> <value>

<span data-ttu-id="409a9-145">**Hiermee stelt u de Azure CLI-modus werken op een `arm` of`asm`**</span><span class="sxs-lookup"><span data-stu-id="409a9-145">**Sets the Azure CLI working mode to either `arm` or `asm`**</span></span>

    config mode [options] <modename>


## <a name="azure-feature-commands-to-manage-account-features"></a><span data-ttu-id="409a9-146">functie van Azure: opdrachten voor het beheren van account-functies</span><span class="sxs-lookup"><span data-stu-id="409a9-146">azure feature: commands to manage account features</span></span>
<span data-ttu-id="409a9-147">**Lijst van alle functies die beschikbaar zijn voor uw abonnement**</span><span class="sxs-lookup"><span data-stu-id="409a9-147">**List all features available for your subscription**</span></span>

    feature list [options]

<span data-ttu-id="409a9-148">**Bevat een functie**</span><span class="sxs-lookup"><span data-stu-id="409a9-148">**Shows a feature**</span></span>

    feature show [options] <providerName> <featureName>

<span data-ttu-id="409a9-149">**Een voorbeeld functie van een resourceprovider geregistreerd**</span><span class="sxs-lookup"><span data-stu-id="409a9-149">**Registers a previewed feature of a resource provider**</span></span>

    feature register [options] <providerName> <featureName>

## <a name="azure-group-commands-to-manage-your-resource-groups"></a><span data-ttu-id="409a9-150">Azure-groep: opdrachten voor het beheren van uw resourcegroepen</span><span class="sxs-lookup"><span data-stu-id="409a9-150">azure group: Commands to manage your resource groups</span></span>
<span data-ttu-id="409a9-151">**Maakt een resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="409a9-151">**Creates a resource group**</span></span>

    group create [options] <name> <location>

<span data-ttu-id="409a9-152">**Set-codes voor een resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="409a9-152">**Set tags to a resource group**</span></span>

    group set [options] <name> <tags>

<span data-ttu-id="409a9-153">**Hiermee verwijdert u een resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="409a9-153">**Deletes a resource group**</span></span>

    group delete [options] <name>

<span data-ttu-id="409a9-154">**Geeft een lijst van de resourcegroepen voor uw abonnement**</span><span class="sxs-lookup"><span data-stu-id="409a9-154">**Lists the resource groups for your subscription**</span></span>

    group list [options]

<span data-ttu-id="409a9-155">**Ziet u een resourcegroep voor uw abonnement**</span><span class="sxs-lookup"><span data-stu-id="409a9-155">**Shows a resource group for your subscription**</span></span>

    group show [options] <name>

<span data-ttu-id="409a9-156">**Opdrachten voor het beheren van resource groep zich aanmeldt**</span><span class="sxs-lookup"><span data-stu-id="409a9-156">**Commands to manage resource group logs**</span></span>

    group log show [options] [name]

<span data-ttu-id="409a9-157">**Opdrachten voor het beheren van uw implementatie in een resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="409a9-157">**Commands to manage your deployment in a resource group**</span></span>

    group deployment create [options] [resource-group] [name]
    group deployment list [options] <resource-group> [state]
    group deployment show [options] <resource-group> [deployment-name]
    group deployment stop [options] <resource-group> [deployment-name]

<span data-ttu-id="409a9-158">**Opdrachten voor het beheren van uw lokale of gallery resource groep-sjabloon**</span><span class="sxs-lookup"><span data-stu-id="409a9-158">**Commands to manage your local or gallery resource group template**</span></span>

    group template list [options]
    group template show [options] <name>
    group template download [options] [name] [file]
    group template validate [options] <resource-group>

## <a name="azure-hdinsight-commands-to-manage-your-hdinsight-clusters"></a><span data-ttu-id="409a9-159">Azure hdinsight: opdrachten voor het beheren van uw HDInsight-clusters</span><span class="sxs-lookup"><span data-stu-id="409a9-159">azure hdinsight: Commands to manage your HDInsight clusters</span></span>
<span data-ttu-id="409a9-160">**Opdrachten voor het maken of toevoegen aan een cluster-configuratiebestand**</span><span class="sxs-lookup"><span data-stu-id="409a9-160">**Commands to create or add to a cluster configuration file**</span></span>

    hdinsight config create [options] <configFilePath> <overwrite>
    hdinsight config add-config-values [options] <configFilePath>
    hdinsight config add-script-action [options] <configFilePath>

<span data-ttu-id="409a9-161">Voorbeeld: Maak een configuratiebestand met een scriptactie om uit te voeren bij het maken van een cluster.</span><span class="sxs-lookup"><span data-stu-id="409a9-161">Example: Create a configuration file that contains a script action to run when creating a cluster.</span></span>

    hdinsight config create "C:\myFiles\configFile.config"
    hdinsight config add-script-action --configFilePath "C:\myFiles\configFile.config" --nodeType HeadNode --uri <scriptActionURI> --name myScriptAction --parameters "-param value"

<span data-ttu-id="409a9-162">**Opdracht voor het maken van een cluster in een resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="409a9-162">**Command to create a cluster in a resource group**</span></span>

    hdinsight cluster create [options] <clusterName>

<span data-ttu-id="409a9-163">Voorbeeld: Een Storm op Linux-cluster maken</span><span class="sxs-lookup"><span data-stu-id="409a9-163">Example: Create a Storm on Linux cluster</span></span>

    azure hdinsight cluster create -g myarmgroup -l westus -y Linux --clusterType Storm --version 3.2 --defaultStorageAccountName mystorageaccount --defaultStorageAccountKey <defaultStorageAccountKey> --defaultStorageContainer mycontainer --userName admin --password <clusterPassword> --sshUserName sshuser --sshPassword <sshPassword> --workerNodeCount 1 myNewCluster01

    info:    Executing command hdinsight cluster create
    + Submitting the request to create cluster...
    info:    hdinsight cluster create command OK

<span data-ttu-id="409a9-164">Voorbeeld: Een cluster maken met een scriptactie</span><span class="sxs-lookup"><span data-stu-id="409a9-164">Example: Create a cluster with a script action</span></span>

    azure hdinsight cluster create -g myarmgroup -l westus -y Linux --clusterType Hadoop --version 3.2 --defaultStorageAccountName mystorageaccount --defaultStorageAccountKey <defaultStorageAccountKey> --defaultStorageContainer mycontainer --userName admin --password <clusterPassword> --sshUserName sshuser --sshPassword <sshPassword> --workerNodeCount 1 –configurationPath "C:\myFiles\configFile.config" myNewCluster01

    info:    Executing command hdinsight cluster create
    + Submitting the request to create cluster...
    info:    hdinsight cluster create command OK

<span data-ttu-id="409a9-165">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="409a9-165">Parameter options:</span></span>

    -h, --help                                                 output usage information
    -v, --verbose                                              use verbose output
    -vv                                                        more verbose with debug output
    --json                                                     use json output
    -g --resource-group <resource-group>                       The name of the resource group
    -c, --clusterName <clusterName>                            HDInsight cluster name
    -l, --location <location>                                  Data center location for the cluster
    -y, --osType <osType>                                      HDInsight cluster operating system
    'Windows' or 'Linux'
    --version <version>                                        HDInsight cluster version
    --clusterType <clusterType>                                HDInsight cluster type.
    Hadoop | HBase | Spark | Storm
    --defaultStorageAccountName <storageAccountName>           Storage account url to use for default HDInsight storage
    --defaultStorageAccountKey <storageAccountKey>             Key to the storage account to use for default HDInsight storage
    --defaultStorageContainer <storageContainer>               Container in the storage account to use for HDInsight default storage
    --headNodeSize <headNodeSize>                              (Optional) Head node size for the cluster
    --workerNodeCount <workerNodeCount>                        Number of worker nodes to use for the cluster
    --workerNodeSize <workerNodeSize>                          (Optional) Worker node size for the cluster)
    --zookeeperNodeSize <zookeeperNodeSize>                    (Optional) Zookeeper node size for the cluster
    --userName <userName>                                      Cluster username
    --password <password>                                      Cluster password
    --sshUserName <sshUserName>                                SSH username (only for Linux clusters)
    --sshPassword <sshPassword>                                SSH password (only for Linux clusters)
    --sshPublicKey <sshPublicKey>                              SSH public key (only for Linux clusters)
    --rdpUserName <rdpUserName>                                RDP username (only for Windows clusters)
    --rdpPassword <rdpPassword>                                RDP password (only for Windows clusters)
    --rdpAccessExpiry <rdpAccessExpiry>                        RDP access expiry.
    For example 12/12/2015 (only for Windows clusters)
    --virtualNetworkId <virtualNetworkId>                      (Optional) Virtual network ID for the cluster.
    Value is a GUID for Windows cluster and ARM resource ID for Linux cluster)
    --subnetName <subnetName>                                  (Optional) Subnet for the cluster
    --additionalStorageAccounts <additionalStorageAccounts>    (Optional) Additional storage accounts.
    Can be multiple.
    In the format of 'accountName#accountKey'.
    For example, --additionalStorageAccounts "acc1#key1;acc2#key2"
    --hiveMetastoreServerName <hiveMetastoreServerName>        (Optional) SQL Server name for the external metastore for Hive
    --hiveMetastoreDatabaseName <hiveMetastoreDatabaseName>    (Optional) Database name for the external metastore for Hive
    --hiveMetastoreUserName <hiveMetastoreUserName>            (Optional) Database username for the external metastore for Hive
    --hiveMetastorePassword <hiveMetastorePassword>            (Optional) Database password for the external metastore for Hive
    --oozieMetastoreServerName <oozieMetastoreServerName>      (Optional) SQL Server name for the external metastore for Oozie
    --oozieMetastoreDatabaseName <oozieMetastoreDatabaseName>  (Optional) Database name for the external metastore for Oozie
    --oozieMetastoreUserName <oozieMetastoreUserName>          (Optional) Database username for the external metastore for Oozie
    --oozieMetastorePassword <oozieMetastorePassword>          (Optional) Database password for the external metastore for Oozie
    --configurationPath <configurationPath>                    (Optional) HDInsight cluster configuration file path
    -s, --subscription <id>                                    The subscription id
    --tags <tags>                                              Tags to set to the cluster.
    Can be multiple.
    In the format of 'name=value'.
    Name is required and value is optional.
    For example, --tags tag1=value1;tag2


<span data-ttu-id="409a9-166">**Opdracht voor het verwijderen van een cluster**</span><span class="sxs-lookup"><span data-stu-id="409a9-166">**Command to delete a cluster**</span></span>

    hdinsight cluster delete [options] <clusterName>

<span data-ttu-id="409a9-167">**Opdracht voor het clusterdetails weergeven**</span><span class="sxs-lookup"><span data-stu-id="409a9-167">**Command to show cluster details**</span></span>

    hdinsight cluster show [options] <clusterName>

<span data-ttu-id="409a9-168">**Opdracht voor een lijst met alle clusters (in een specifieke resourcegroep, indien opgegeven)**</span><span class="sxs-lookup"><span data-stu-id="409a9-168">**Command to list all clusters (in a specific resource group, if provided)**</span></span>

    hdinsight cluster list [options]

<span data-ttu-id="409a9-169">**Opdracht voor het vergroten of verkleinen van een cluster**</span><span class="sxs-lookup"><span data-stu-id="409a9-169">**Command to resize a cluster**</span></span>

    hdinsight cluster resize [options] <clusterName> <targetInstanceCount>

<span data-ttu-id="409a9-170">**Opdracht voor het HTTP-toegang voor een cluster**</span><span class="sxs-lookup"><span data-stu-id="409a9-170">**Command to enable HTTP access for a cluster**</span></span>

    hdinsight cluster enable-http-access [options] <clusterName> <userName> <password>

<span data-ttu-id="409a9-171">**Opdracht voor het uitschakelen van HTTP-toegang voor een cluster**</span><span class="sxs-lookup"><span data-stu-id="409a9-171">**Command to disable HTTP access for a cluster**</span></span>

    hdinsight cluster disable-http-access [options] <clusterName>

<span data-ttu-id="409a9-172">**Opdracht voor het RDP-toegang voor een cluster**</span><span class="sxs-lookup"><span data-stu-id="409a9-172">**Command to enable RDP access for a cluster**</span></span>

    hdinsight cluster enable-rdp-access [options] <clusterName> <rdpUserName> <rdpPassword> <rdpExpiryDate>

<span data-ttu-id="409a9-173">**Opdracht voor het uitschakelen van HTTP-toegang voor een cluster**</span><span class="sxs-lookup"><span data-stu-id="409a9-173">**Command to disable HTTP access for a cluster**</span></span>

    hdinsight cluster disable-rdp-access [options] <clusterName>

## <a name="azure-insights-commands-related-to-monitoring-insights-events-alert-rules-autoscale-settings-metrics"></a><span data-ttu-id="409a9-174">inzicht van Azure: opdrachten gerelateerd aan de bewaking van Insights (gebeurtenissen, waarschuwingsregels, instellingen voor automatisch schalen, metrische gegevens)</span><span class="sxs-lookup"><span data-stu-id="409a9-174">azure insights: Commands related to monitoring Insights (events, alert rules, autoscale settings, metrics)</span></span>
<span data-ttu-id="409a9-175">**Bewerkingslogboeken voor een abonnement, een correlationId, een resourcegroep, resource of resourceprovider ophalen**</span><span class="sxs-lookup"><span data-stu-id="409a9-175">**Retrieve operation logs for a subscription, a correlationId, a resource group, resource, or resource provider**</span></span>

    insights logs list [options]

## <a name="azure-location-commands-to-get-the-available-locations-for-all-resource-types"></a><span data-ttu-id="409a9-176">Azure-locatie: opdrachten voor het ophalen van de beschikbare locaties voor alle resourcetypen</span><span class="sxs-lookup"><span data-stu-id="409a9-176">azure location: Commands to get the available locations for all resource types</span></span>
<span data-ttu-id="409a9-177">**Lijst van de beschikbare locaties**</span><span class="sxs-lookup"><span data-stu-id="409a9-177">**List the available locations**</span></span>

    location list [options]

## <a name="azure-network-commands-to-manage-network-resources"></a><span data-ttu-id="409a9-178">Azure-netwerk: opdrachten voor het beheren van netwerkbronnen</span><span class="sxs-lookup"><span data-stu-id="409a9-178">azure network: Commands to manage network resources</span></span>
<span data-ttu-id="409a9-179">**Opdrachten voor het beheren van virtuele netwerken**</span><span class="sxs-lookup"><span data-stu-id="409a9-179">**Commands to manage virtual networks**</span></span>

    network vnet create [options] <resource-group> <name> <location>
<span data-ttu-id="409a9-180">Hiermee maakt u een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="409a9-180">Creates a virtual network.</span></span> <span data-ttu-id="409a9-181">In het volgende voorbeeld maken we een virtueel netwerk met de naam newvnet voor resource groep myresourcegroup in de regio VS-West.</span><span class="sxs-lookup"><span data-stu-id="409a9-181">In the following example we create a virtual network named newvnet for resource group myresourcegroup in the West US region.</span></span>

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


<span data-ttu-id="409a9-182">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="409a9-182">Parameter options:</span></span>

     -h, --help                                 output usage information
     -v, --verbose                              use verbose output
    --json                                     use json output
     -g, --resource-group <resource-group>      the name of the resource group
     -n, --name <name>                          the name of the virtual network
     -l, --location <location>                  the location
     -a, --address-prefixes <address-prefixes>  the comma separated list of address prefixes for this virtual network
      For example -a 10.0.0.0/24,10.0.1.0/24.
      Default value is 10.0.0.0/8

    -d, --dns-servers <dns-servers>            the comma separated list of DNS servers IP addresses
     -t, --tags <tags>                          the tags set on this virtual network.
      Can be multiple. In the format of "name=value".
      Name is required and value is optional.
      For example, -t tag1=value1;tag2
     -s, --subscription <subscription>          the subscription identifier
<BR>

    network vnet set [options] <resource-group> <name>

<span data-ttu-id="409a9-183">De configuratie van een virtueel netwerk in de resourcegroep-updates.</span><span class="sxs-lookup"><span data-stu-id="409a9-183">Updates a virtual network configuration within a resource group.</span></span>

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

<span data-ttu-id="409a9-184">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="409a9-184">Parameter options:</span></span>

       -h, --help                                 output usage information
       -v, --verbose                              use verbose output
       --json                                     use json output
       -g, --resource-group <resource-group>      the name of the resource group
       -n, --name <name>                          the name of the virtual network
       -a, --address-prefixes <address-prefixes>  the comma separated list of address prefixes for this virtual network.
        For example -a 10.0.0.0/24,10.0.1.0/24.
        This list will be appended to the current list of address prefixes.
        The address prefixes in this list should not overlap between them.
        The address prefixes in this list should not overlap with existing address prefixes in the vnet.

       -d, --dns-servers [dns-servers]            the comma separated list of DNS servers IP addresses.
        This list will be appended to the current list of DNS server IP addresses.

       -t, --tags <tags>                          the tags set on this virtual network.
        Can be multiple. In the format of "name=value".
        Name is required and value is optional. For example, -t tag1=value1;tag2.
        This list will be appended to the current list of tags

       --no-tags                                  remove all existing tags
       -s, --subscription <subscription>          the subscription identifier
<BR>

    network vnet list [options] <resource-group>

<span data-ttu-id="409a9-185">De opdracht worden alle virtuele netwerken in een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="409a9-185">The command lists all virtual networks in a resource group.</span></span>

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

<span data-ttu-id="409a9-186">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="409a9-186">Parameter options:</span></span>

      -h, --help                             output usage information
      -v, --verbose                          use verbose output
      --json                                 use json output
      -g, --resource-group <resource-group>  the name of the resource group
      -s, --subscription <subscription>      the subscription identifier

<BR>

    network vnet show [options] <resource-group> <name>
<span data-ttu-id="409a9-187">De opdracht ziet u de eigenschappen van het virtuele netwerk in een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="409a9-187">The command shows the virtual network properties in a resource group.</span></span>

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
<span data-ttu-id="409a9-188">De opdracht verwijdert een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="409a9-188">The command removes a virtual network.</span></span>

    azure network vnet delete myresourcegroup newvnetX

    info:    Executing command network vnet delete
    + Looking up virtual network "newvnetX"
    Delete virtual network newvnetX? [y/n] y
    + Deleting virtual network "newvnetX"
    info:    network vnet delete command OK

<span data-ttu-id="409a9-189">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="409a9-189">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  the name of the resource group
     -n, --name <name>                      the name of the virtual network
     -q, --quiet                            quiet mode, do not ask for delete confirmation
     -s, --subscription <subscription>      the subscription identifier


<span data-ttu-id="409a9-190">**Opdrachten voor het beheren van virtueel netwerk subnetten**</span><span class="sxs-lookup"><span data-stu-id="409a9-190">**Commands to manage virtual network subnets**</span></span>

    network vnet subnet create [options] <resource-group> <vnet-name> <name>

<span data-ttu-id="409a9-191">Voegt een ander subnet toe aan een bestaand virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="409a9-191">Adds another subnet to an existing virtual network.</span></span>

    azure network vnet subnet create -g myresourcegroup --vnet-name newvnet -n subnet --address-prefix 10.0.1.0/24

    info:    Executing command network vnet subnet create
    + Looking up the subnet "subnet"
    + Creating subnet "subnet"
    + Looking up the subnet "subnet"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet/subnets/subnet
    data:    Name:                      subnet
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet create command OK

<span data-ttu-id="409a9-192">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="409a9-192">Parameter options:</span></span>

     -h, --help                                                       output usage information
     -v, --verbose                                                    use verbose output
         --json                                                           use json output
     -g, --resource-group <resource-group>                            the name of the resource group
     -e, --vnet-name <vnet-name>                                      the name of the virtual network
     -n, --name <name>                                                the name of the subnet
     -a, --address-prefix <address-prefix>                            the address prefix
     -w, --network-security-group-id <network-security-group-id>      the network security group identifier.
           e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/networkSecurityGroups/<nsg-name>
     -o, --network-security-group-name <network-security-group-name>  the network security group name
     -s, --subscription <subscription>                                the subscription identifier

<BR>

    network vnet subnet set [options] <resource-group> <vnet-name> <name>

<span data-ttu-id="409a9-193">Hiermee stelt u een specifiek virtueel netwerksubnet binnen een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="409a9-193">Sets a specific virtual network subnet within a resource group.</span></span>

    C:\>azure network vnet subnet set -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet set
    + Looking up the subnet "subnet1"
    + Setting subnet "subnet1"
    + Looking up the subnet "subnet1"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet/subnets/subnet1
    data:    Name:                      subnet1
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet set command OK
<BR>

    network vnet subnet list [options] <resource-group> <vnet-name>

<span data-ttu-id="409a9-194">Een lijst met alle subnetten van een virtueel netwerk voor een specifieke virtuele netwerk binnen een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="409a9-194">Lists all the virtual network subnets for a specific virtual network within a resource group.</span></span>

    azure network vnet subnet set -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet set
    + Looking up the subnet "subnet1"
    + Setting subnet "subnet1"
    + Looking up the subnet "subnet1"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet/subnets/subnet1
    data:    Name:                      subnet1
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet set command OK
<BR>

    network vnet subnet show [options] <resource-group> <vnet-name> <name>
<span data-ttu-id="409a9-195">Eigenschappen van virtueel netwerk subnet</span><span class="sxs-lookup"><span data-stu-id="409a9-195">Displays virtual network subnet properties</span></span>

    azure network vnet subnet show -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet show
    + Looking up the subnet "subnet1"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft
    .Network/virtualNetworks/newvnet/subnets/subnet1
    data:    Name:                      subnet1
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet show command OK

<span data-ttu-id="409a9-196">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="409a9-196">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -e, --vnet-name <vnet-name>            the name of the virtual network
    -n, --name <name>                      the name of the subnet
    -s, --subscription <subscription>      the subscription identifier
<BR>

    network vnet subnet delete [options] <resource-group> <vnet-name> <subnet-name>
<span data-ttu-id="409a9-197">Hiermee verwijdert u een subnet van een bestaand virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="409a9-197">Removes a subnet from an existing virtual network.</span></span>

    azure network vnet subnet delete -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet delete
    + Looking up the subnet "subnet1"
    Delete subnet "subnet1"? [y/n] y
    + Deleting subnet "subnet1"
    info:    network vnet subnet delete command OK

<span data-ttu-id="409a9-198">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="409a9-198">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  the name of the resource group
     -e, --vnet-name <vnet-name>            the name of the virtual network
     -n, --name <name>                      the subnet name
     -s, --subscription <subscription>      the subscription identifier
     -q, --quiet                            quiet mode, do not ask for delete confirmation

<span data-ttu-id="409a9-199">**Opdrachten voor het beheer van netwerktaakverdeling**</span><span class="sxs-lookup"><span data-stu-id="409a9-199">**Commands to manage load balancers**</span></span>

    network lb create [options] <resource-group> <name> <location>
<span data-ttu-id="409a9-200">Hiermee maakt u een load balancer.</span><span class="sxs-lookup"><span data-stu-id="409a9-200">Creates a load balancer set.</span></span>

    azure network lb create -g myresourcegroup -n mylb -l westus

    info:    Executing command network lb create
    + Looking up the load balancer "mylb"
    + Creating load balancer "mylb"
    + Looking up the load balancer "mylb"
    data:    Id:                           /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb
    data:    Name:                         mylb
    data:    Type:                         Microsoft.Network/loadBalancers
    data:    Location:                     westus
    data:    Provisioning state:           Succeeded
    info:    network lb create command OK

<span data-ttu-id="409a9-201">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="409a9-201">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -n, --name <name>                      the name of the load balancer
    -l, --location <location>              the location
    -t, --tags <tags>                      the list of tags.
     Can be multiple. In the format of "name=value".
     Name is required and value is optional. For example, -t tag1=value1;tag2
    -s, --subscription <subscription>      the subscription identifier
<BR>

    network lb list [options] <resource-group>
<span data-ttu-id="409a9-202">Bevat Load balancer bronnen binnen een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="409a9-202">Lists Load balancer resources within a resource group.</span></span>

    azure network lb list myresourcegroup

    info:    Executing command network lb list
    + Getting the load balancers
    data:    Name  Location
    data:    ----  --------
    data:    mylb  westus
    info:    network lb list command OK

<span data-ttu-id="409a9-203">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="409a9-203">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -s, --subscription <subscription>      the subscription identifier
<BR>

    network lb show [options] <resource-group> <name>

<span data-ttu-id="409a9-204">Geeft load balancer-gegevens van een specifieke load balancer binnen een resourcegroep</span><span class="sxs-lookup"><span data-stu-id="409a9-204">Displays load balancer information of a specific load balancer within a resource group</span></span>

    azure network lb show myresourcegroup mylb -v

    info:    Executing command network lb show
    verbose: Looking up the load balancer "mylb"
    data:    Id:                           /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb
    data:    Name:                         mylb
    data:    Type:                         Microsoft.Network/loadBalancers
    data:    Location:                     westus
    data:    Provisioning state:           Succeeded
    info:    network lb show command OK

<span data-ttu-id="409a9-205">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="409a9-205">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -n, --name <name>                      the name of the load balancer
    -s, --subscription <subscription>      the subscription identifier

<BR>

    network lb delete [options] <resource-group> <name>

<span data-ttu-id="409a9-206">Load balancer-resources verwijderen.</span><span class="sxs-lookup"><span data-stu-id="409a9-206">Delete load balancer resources.</span></span>

    azure network lb delete  myresourcegroup mylb

    info:    Executing command network lb delete
    + Looking up the load balancer "mylb"
    Delete load balancer "mylb"? [y/n] y
    + Deleting load balancer "mylb"
    info:    network lb delete command OK

<span data-ttu-id="409a9-207">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="409a9-207">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  the name of the resource group
     -n, --name <name>                      the name of the load balancer
     -q, --quiet                            quiet mode, do not ask for delete confirmation
     -s, --subscription <subscription>      the subscription identifier

<span data-ttu-id="409a9-208">**Opdrachten voor het beheren van de tests van een load balancer**</span><span class="sxs-lookup"><span data-stu-id="409a9-208">**Commands to manage probes of a load balancer**</span></span>

    network lb probe create [options] <resource-group> <lb-name> <name>

<span data-ttu-id="409a9-209">Maak de test-configuratie voor de health-status in de load balancer.</span><span class="sxs-lookup"><span data-stu-id="409a9-209">Create the probe configuration for health status in the load balancer.</span></span> <span data-ttu-id="409a9-210">Houd er rekening mee deze opdracht uit te voeren, de load balancer vereist een frontend-ip-resource (Controleer de opdracht 'azure-netwerk frontend-ip' een IP-adres toewijzen aan de load balancer).</span><span class="sxs-lookup"><span data-stu-id="409a9-210">Keep in mind to run this command, your load balancer requires a frontend-ip resource (Check out command "azure network frontend-ip" to assign an ip address to load balancer).</span></span>

    azure network lb probe create -g myresourcegroup --lb-name mylb -n mylbprobe --protocol tcp --port 80 -i 300

    info:    Executing command network lb probe create
    + Looking up the load balancer "mylb"
    + Updating load balancer "mylb"
    info:    network lb probe create command OK

<span data-ttu-id="409a9-211">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="409a9-211">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -l, --lb-name <lb-name>                the name of the load balancer
    -n, --name <name>                      the name of the probe
    -p, --protocol <protocol>              the probe protocol
    -o, --port <port>                      the probe port
    -f, --path <path>                      the probe path
    -i, --interval <interval>              the probe interval in seconds
    -c, --count <count>                    the number of probes
    -s, --subscription <subscription>      the subscription identifier

<BR>

    network lb probe set [options] <resource-group> <lb-name> <name>

<span data-ttu-id="409a9-212">Een bestaande load balancer-test met nieuwe waarden voor deze bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="409a9-212">Updates an existing load balancer probe with new values for it.</span></span>

    azure network lb probe set -g myresourcegroup -l mylb -n mylbprobe -p mylbprobe1 -p TCP -o 443 -i 300

    info:    Executing command network lb probe set
        + Looking up the load balancer "mylb"
    + Updating load balancer "mylb"
    info:    network lb probe set command OK

<span data-ttu-id="409a9-213">De parameteropties</span><span class="sxs-lookup"><span data-stu-id="409a9-213">Parameter options</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -l, --lb-name <lb-name>                the name of the load balancer
    -n, --name <name>                      the name of the probe
    -e, --new-probe-name <new-probe-name>  the new name of the probe
    -p, --protocol <protocol>              the new value for probe protocol
    -o, --port <port>                      the new value for probe port
    -f, --path <path>                      the new value for probe path
    -i, --interval <interval>              the new value for probe interval in seconds
    -c, --count <count>                    the new value for number of probes
    -s, --subscription <subscription>      the subscription identifier
<BR>

    network lb probe list [options] <resource-group> <lb-name>

<span data-ttu-id="409a9-214">Lijst van de test-eigenschappen voor een load balancer-set.</span><span class="sxs-lookup"><span data-stu-id="409a9-214">List the probe properties for a load balancer set.</span></span>

    C:\>azure network lb probe list -g myresourcegroup -l mylb

    info:    Executing command network lb probe list
    + Looking up the load balancer "mylb"
    data:    Name       Protocol  Port  Path  Interval  Count
    data:    ---------  --------  ----  ----  --------  -----
    data:    mylbprobe  Tcp       443         300       2
    info:    network lb probe list command OK

<span data-ttu-id="409a9-215">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="409a9-215">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -l, --lb-name <lb-name>                the name of the load balancer
    -s, --subscription <subscription>      the subscription identifier


    network lb probe delete [options] <resource-group> <lb-name> <name>
<span data-ttu-id="409a9-216">Hiermee verwijdert u de gemaakt voor de load balancer-test.</span><span class="sxs-lookup"><span data-stu-id="409a9-216">Removes the probe created for the load balancer.</span></span>

    azure network lb probe delete -g myresourcegroup -l mylb -n mylbprobe

    info:    Executing command network lb probe delete
    + Looking up the load balancer "mylb"
    Delete a probe "mylbprobe?" [y/n] y
    + Updating load balancer "mylb"
    info:    network lb probe delete command OK

<span data-ttu-id="409a9-217">**Opdrachten voor het beheren van frontend-IP-configuraties van een load balancer**</span><span class="sxs-lookup"><span data-stu-id="409a9-217">**Commands to manage frontend ip configurations of a load balancer**</span></span>

    network lb frontend-ip create [options] <resource-group> <lb-name> <name>
<span data-ttu-id="409a9-218">Maakt een frontend-IP-configuratie aan een bestaande load balancer-set.</span><span class="sxs-lookup"><span data-stu-id="409a9-218">Creates a frontend IP configuration to an existing load balancer set.</span></span>

    azure network lb frontend-ip create -g myresourcegroup --lb-name mylb -n myfrontendip -o Dynamic -e subnet -m newvnet

    info:    Executing command network lb frontend-ip create
    + Looking up the load balancer "mylb"
    + Looking up the subnet "subnet"
    + Creating frontend IP configuration "myfrontendip"
    + Looking up the load balancer "mylb"
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

<span data-ttu-id="409a9-219">Een bestaande configuratie van een frontend-IP-updates. De onderstaande opdracht voegt een openbaar IP-adres mypubip5 naar een bestaande load balancer frontend-IP-met de naam myfrontendip aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="409a9-219">Updates an existing configuration of a frontend IP.The command below adds a public IP called mypubip5 to an existing load balancer frontend IP named myfrontendip.</span></span>

    azure network lb frontend-ip set -g myresourcegroup --lb-name mylb -n myfrontendip -i mypubip5

    info:    Executing command network lb frontend-ip set
    + Looking up the load balancer "mylb"
    + Looking up the public ip "mypubip5"
    + Updating load balancer "mylb"
    + Looking up the load balancer "mylb"
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

<span data-ttu-id="409a9-220">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="409a9-220">Parameter options:</span></span>

    -h, --help                                                         output usage information
    -v, --verbose                                                      use verbose output
    --json                                                             use json output
    -g, --resource-group <resource-group>                              the name of the resource group
    -l, --lb-name <lb-name>                                            the name of the load balancer
    -n, --name <name>                                                  the name of the frontend ip configuration
    -a, --private-ip-address <private-ip-address>                      the private ip address
    -o, --private-ip-allocation-method <private-ip-allocation-method>  the private ip allocation method [Static, Dynamic]
    -u, --public-ip-id <public-ip-id>                                  the public ip identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/publicIPAddresses/<public-ip-name>
    -i, --public-ip-name <public-ip-name>                              the public ip name.
    This public ip must exist in the same resource group as the lb.
    Please use public-ip-id if that is not the case.
    -b, --subnet-id <subnet-id>                                        the subnet id.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/VirtualNetworks/<vnet-name>/subnets/<subnet-name>
    -e, --subnet-name <subnet-name>                                    the subnet name
    -m, --vnet-name <vnet-name>                                        the virtual network name.
    This virtual network must exist in the same resource group as the lb.
    Please use subnet-id if that is not the case.
    -s, --subscription <subscription>                                  the subscription identifier

<BR>

    network lb frontend-ip list [options] <resource-group> <lb-name>

<span data-ttu-id="409a9-221">Geeft een lijst van alle frontend IP-resources die zijn geconfigureerd voor de load balancer.</span><span class="sxs-lookup"><span data-stu-id="409a9-221">Lists all the frontend IP resources configured for the load balancer.</span></span>

    azure network lb frontend-ip list -g myresourcegroup -l mylb

    info:    Executing command network lb frontend-ip list
    + Looking up the load balancer "mylb"
    data:    Name         Provisioning state  Private IP allocation method  Subnet
    data:    -----------  ------------------  ----------------------------  ------
    data:    myprivateip  Succeeded           Dynamic
    info:    network lb frontend-ip list command OK

<span data-ttu-id="409a9-222">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="409a9-222">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -l, --lb-name <lb-name>                the name of the load balancer
    -s, --subscription <subscription>      the subscription identifier
<BR>

    network lb frontend-ip delete [options] <resource-group> <lb-name> <name>
<span data-ttu-id="409a9-223">Hiermee verwijdert u de frontend-IP-object die zijn gekoppeld aan de load balancer</span><span class="sxs-lookup"><span data-stu-id="409a9-223">Deletes the frontend IP object associated to load balancer</span></span>

    network lb frontend-ip delete -g myresourcegroup -l mylb -n myfrontendip
    info:    Executing command network lb frontend-ip delete
    + Looking up the load balancer "mylb"
    Delete frontend ip configuration "myfrontendip"? [y/n] y
    + Updating load balancer "mylb"

<span data-ttu-id="409a9-224">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="409a9-224">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -l, --lb-name <lb-name>                the name of the load balancer
    -n, --name <name>                      the name of the frontend ip configuration
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      the subscription identifier

<span data-ttu-id="409a9-225">**Opdrachten voor het beheren van back-end-adresgroepen van een load balancer**</span><span class="sxs-lookup"><span data-stu-id="409a9-225">**Commands to manage backend address pools of a load balancer**</span></span>

    network lb address-pool create [options] <resource-group> <lb-name> <name>

<span data-ttu-id="409a9-226">Maak een back-end-adresgroep voor een load balancer.</span><span class="sxs-lookup"><span data-stu-id="409a9-226">Create a backend address pool for a load balancer.</span></span>

    azure network lb address-pool create -g myresourcegroup --lb-name mylb -n myaddresspool

    info:    Executing command network lb address-pool create
    + Looking up the load balancer "mylb"
    + Updating load balancer "mylb"
    + Looking up the load balancer "mylb"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourgroup/providers/Microso.Network/loadBalancers/mylb/backendAddressPools/myaddresspool
    data:    Name:                      myaddresspool
    data:    Type:                      Microsoft.Network/loadBalancers/backendAddressPools
    data:    Provisioning state:        Succeeded
    data:    Backend IP configurations:
    data:    Load balancing rules:
    data:
    info:    network lb address-pool create command OK

<span data-ttu-id="409a9-227">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="409a9-227">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -l, --lb-name <lb-name>                the name of the load balancer
    -n, --name <name>                      the name of the backend address pool
    -s, --subscription <subscription>      the subscription identifier

<BR>

    network lb address-pool list [options] <resource-group> <lb-name>

<span data-ttu-id="409a9-228">Lijst met back-end IP-adresgroep adresbereik voor een specifieke resourcegroep</span><span class="sxs-lookup"><span data-stu-id="409a9-228">List backend IP address pool range for a specific resource group</span></span>

    azure network lb address-pool list -g myresourcegroup -l mylb

    info:    Executing command network lb address-pool list
    + Looking up the load balancer "mylb"
    data:    Name           Provisioning state
    data:    -------------  ------------------
    data:    mybackendpool  Succeeded
    info:    network lb address-pool list command OK

<span data-ttu-id="409a9-229">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="409a9-229">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  the name of the resource group
     -l, --lb-name <lb-name>                the name of the load balancer
     -s, --subscription <subscription>      the subscription identifier

<BR>
    <span data-ttu-id="409a9-230">lb-netwerkadresgroep verwijderen [opties] < resourcegroep >< lb-naam ><name></span><span class="sxs-lookup"><span data-stu-id="409a9-230">network lb address-pool delete [options] <resource-group> <lb-name> <name></span></span>

<span data-ttu-id="409a9-231">Hiermee verwijdert u de back-end IP-adresgroep bereik resource uit de load balancer.</span><span class="sxs-lookup"><span data-stu-id="409a9-231">Removes the backend IP pool range resource from load balancer.</span></span>

    azure network lb address-pool delete -g myresourcegroup -l mylb -n mybackendpool

    info:    Executing command network lb address-pool delete
    + Looking up the load balancer "mylb"
    Delete backend address pool "mybackendpool"? [y/n] y
    + Updating load balancer "mylb"
    info:    network lb address-pool delete command OK

<span data-ttu-id="409a9-232">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="409a9-232">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -l, --lb-name <lb-name>                the name of the load balancer
    -n, --name <name>                      the name of the backend address pool
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      the subscription identifier

<span data-ttu-id="409a9-233">**Opdrachten voor het beheren van load-balancerregels**</span><span class="sxs-lookup"><span data-stu-id="409a9-233">**Commands to manage load balancer rules**</span></span>

    network lb rule create [options] <resource-group> <lb-name> <name>
<span data-ttu-id="409a9-234">Load balancer-regels maken.</span><span class="sxs-lookup"><span data-stu-id="409a9-234">Create load balancer rules.</span></span>

<span data-ttu-id="409a9-235">U kunt een load balancer-regel voor het configureren van de frontend-eindpunt voor de load balancer en het back-end-pool adresbereik voor het ontvangen van het binnenkomende netwerkverkeer maken.</span><span class="sxs-lookup"><span data-stu-id="409a9-235">You can create a load balancer rule configuring the frontend endpoint for the load balancer and the backend address pool range to receive the incoming network traffic.</span></span> <span data-ttu-id="409a9-236">Instellingen omvatten ook de poorten voor de frontend-IP-eindpunt en de poorten voor de back-end-pool adresbereik.</span><span class="sxs-lookup"><span data-stu-id="409a9-236">Settings also include the ports for frontend IP endpoint and ports for the backend address pool range.</span></span>

<span data-ttu-id="409a9-237">Het volgende voorbeeld ziet het maken van een regel voor load balancer, het frontend-eindpunt luisteren op poort 80 TCP en load balancing netwerkverkeer voor de back-end-pool adresbereik naar poort 8080 verzenden.</span><span class="sxs-lookup"><span data-stu-id="409a9-237">The following example shows how to create a load balancer rule,  the frontend endpoint listening to port 80 TCP and load balancing network traffic sending to port 8080 for the backend address pool range.</span></span>

    azure network lb rule create -g myresourcegroup -l mylb -n mylbrule -p tcp -f 80 -b 8080 -i 10


    info:    Executing command network lb rule create
    + Looking up the load balancer "mylb"
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

<span data-ttu-id="409a9-238">Updates van een bestaande load balancer-regel instellen in een specifieke resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="409a9-238">Updates an existing load balancer rule set in a specific resource group.</span></span> <span data-ttu-id="409a9-239">In het volgende voorbeeld wordt de regelnaam van mylbrule gewijzigd in mynewlbrule.</span><span class="sxs-lookup"><span data-stu-id="409a9-239">In the following example, we changed the rule name from mylbrule to mynewlbrule.</span></span>

    azure network lb rule set -g myresourcegroup -l mylb -n mylbrule -r mynewlbrule -p tcp -f 80 -b 8080 -i 10 -t myfrontendip -o mybackendpool

    info:    Executing command network lb rule set
    + Looking up the load balancer "mylb"
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

<span data-ttu-id="409a9-240">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="409a9-240">Parameter options:</span></span>

    -h, --help                                         output usage information
    -v, --verbose                                      use verbose output
    --json                                             use json output
    -g, --resource-group <resource-group>              the name of the resource group
    -l, --lb-name <lb-name>                            the name of the load balancer
    -n, --name <name>                                  the name of the rule
    -r, --new-rule-name <new-rule-name>                new rule name
    -p, --protocol <protocol>                          the rule protocol
    -f, --frontend-port <frontend-port>                the frontend port
    -b, --backend-port <backend-port>                  the backend port
    -e, --enable-floating-ip <enable-floating-ip>      enable floating point ip
    -i, --idle-timeout <idle-timeout>                  the idle timeout in minutes
    -a, --probe-name [probe-name]                      the name of the probe defined in the same load balancer
    -t, --frontend-ip-name <frontend-ip-name>          the name of the frontend ip configuration in the same load balancer
    -o, --backend-address-pool <backend-address-pool>  name of the backend address pool defined in the same load balancer
    -s, --subscription <subscription>                  the subscription identifier


    network lb rule list [options] <resource-group> <lb-name>

<span data-ttu-id="409a9-241">Een lijst met alle taakverdelingsregels zijn geconfigureerd voor een load balancer in een specifieke resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="409a9-241">Lists all load balancer rules configured for a load balancer in a specific resource group.</span></span>

    azure network lb rule list -g myresourcegroup -l mylb

    info:    Executing command network lb rule list
    + Looking up the load balancer "mylb"
    data:    Name         Provisioning state  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes  Backend address pool  Probe data

    data:    mynewlbrule  Succeeded           Tcp       80             8080          false               10                       /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/mybackendpool
    info:    network lb rule list command OK

<span data-ttu-id="409a9-242">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="409a9-242">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -l, --lb-name <lb-name>                the name of the load balancer
    -s, --subscription <subscription>      the subscription identifier

    network lb rule delete [options] <resource-group> <lb-name> <name>

<span data-ttu-id="409a9-243">Hiermee verwijdert u een load balancer-regel.</span><span class="sxs-lookup"><span data-stu-id="409a9-243">Deletes a load balancer rule.</span></span>

    azure network lb rule delete -g myresourcegroup -l mylb -n mynewlbrule

    info:    Executing command network lb rule delete
    + Looking up the load balancer "mylb"
    Delete load balancing rule mynewlbrule? [y/n] y
    + Updating load balancer "mylb"
    info:    network lb rule delete command OK

<span data-ttu-id="409a9-244">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="409a9-244">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -l, --lb-name <lb-name>                the name of the load balancer
    -n, --name <name>                      the name of the rule
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      the subscription identifier

<span data-ttu-id="409a9-245">**Opdrachten voor het beheren van de load balancer inkomende NAT-regels**</span><span class="sxs-lookup"><span data-stu-id="409a9-245">**Commands to manage load balancer inbound NAT rules**</span></span>

    network lb inbound-nat-rule create [options] <resource-group> <lb-name> <name>
<span data-ttu-id="409a9-246">Maakt een binnenkomende NAT-regel voor load balancer.</span><span class="sxs-lookup"><span data-stu-id="409a9-246">Creates an inbound NAT rule for load balancer.</span></span>

<span data-ttu-id="409a9-247">In het volgende voorbeeld wordt een NAT-regel van frontend-IP (die is eerder gedefinieerd met de opdracht 'azure-netwerk frontend-ip') gemaakt met een luisterpoort binnenkomende en uitgaande poort die de load balancer wordt gebruikt om het netwerkverkeer te verzenden.</span><span class="sxs-lookup"><span data-stu-id="409a9-247">In the following example  we created a NAT rule from frontend IP (which was previously defined using the "azure network frontend-ip" command) with an inbound listening port and outbound port that the load balancer uses to send the network traffic.</span></span>

    azure network lb inbound-nat-rule create -g myresourcegroup -l mylb -n myinboundnat -p tcp -f 80 -b 8080 -i myfrontendip

    info:    Executing command network lb inbound-nat-rule create
    + Looking up the load balancer "mylb"
    + Updating load balancer "mylb"
    + Looking up the load balancer "mylb"
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

<span data-ttu-id="409a9-248">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="409a9-248">Parameter options:</span></span>

    -h, --help                                     output usage information
    -v, --verbose                                  use verbose output
    --json                                         use json output
    -g, --resource-group <resource-group>          the name of the resource group
    -l, --lb-name <lb-name>                        the name of the load balancer
    -n, --name <name>                              the name of the inbound NAT rule
    -p, --protocol <protocol>                      the rule protocol [tcp,udp]
    -f, --frontend-port <frontend-port>            the frontend port [0-65535]
    -b, --backend-port <backend-port>              the backend port [0-65535]
    -e, --enable-floating-ip <enable-floating-ip>  enable floating point ip [true,false]
    -i, --frontend-ip <frontend-ip>                the name of the frontend ip configuration
    -m, --vm-id <vm-id>                            the VM id.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Compute/virtualMachines/<vm-name>
    -a, --vm-name <vm-name>                        the VM name.This VM must exist in the same resource group as the lb.
    Please use vm-id if that is not the case.
    this parameter will be ignored if --vm-id is specified
    -s, --subscription <subscription>              the subscription identifier
<BR>

    network lb inbound-nat-rule set [options] <resource-group> <lb-name> <name>
<span data-ttu-id="409a9-249">Updates van een bestaande binnenkomende nat-regel.</span><span class="sxs-lookup"><span data-stu-id="409a9-249">Updates an existing inbound nat rule.</span></span> <span data-ttu-id="409a9-250">In het volgende voorbeeld wordt de inkomende luisterpoort van 80 gewijzigd in 81.</span><span class="sxs-lookup"><span data-stu-id="409a9-250">In the following example, we changed the inbound listening port from 80 to 81.</span></span>

    azure network lb inbound-nat-rule set -g group-1 -l mylb -n myinboundnat -p tcp -f 81 -b 8080 -i myfrontendip

    info:    Executing command network lb inbound-nat-rule set
    + Looking up the load balancer "mylb"
    + Updating load balancer "mylb"
    + Looking up the load balancer "mylb"
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

<span data-ttu-id="409a9-251">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="409a9-251">Parameter options:</span></span>

    -h, --help                                     output usage information
    -v, --verbose                                  use verbose output
    --json                                         use json output
    -g, --resource-group <resource-group>          the name of the resource group
    -l, --lb-name <lb-name>                        the name of the load balancer
    -n, --name <name>                              the name of the inbound NAT rule
    -p, --protocol <protocol>                      the rule protocol [tcp,udp]
    -f, --frontend-port <frontend-port>            the frontend port [0-65535]
    -b, --backend-port <backend-port>              the backend port [0-65535]
    -e, --enable-floating-ip <enable-floating-ip>  enable floating point ip [true,false]
    -i, --frontend-ip <frontend-ip>                the name of the frontend ip configuration
    -m, --vm-id [vm-id]                            the VM id.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Compute/virtualMachines/<vm-name>
    -a, --vm-name <vm-name>                        the VM name.
    This virtual machine must exist in the same resource group as the lb.
    Please use vm-id if that is not the case
    -s, --subscription <subscription>              the subscription identifier
<BR>

    network lb inbound-nat-rule list [options] <resource-group> <lb-name>

<span data-ttu-id="409a9-252">Hier worden alle binnenkomende nat-regels voor de load balancer.</span><span class="sxs-lookup"><span data-stu-id="409a9-252">Lists all inbound nat rules for load balancer.</span></span>

    azure network lb inbound-nat-rule list -g myresourcegroup -l mylb

    info:    Executing command network lb inbound-nat-rule list
    + Looking up the load balancer "mylb"
    data:    Name          Provisioning state  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes  Backend IP configuration
    data:    ------------  ------------------  --------  -------------  ------------  ------------------  -----------------------  ---
    ---------------------
    data:    myinboundnat  Succeeded           Tcp       81             8080          false               4

    info:    network lb inbound-nat-rule list command OK

<span data-ttu-id="409a9-253">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="409a9-253">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -l, --lb-name <lb-name>                the name of the load balancer
    -s, --subscription <subscription>      the subscription identifier
<BR>

    network lb inbound-nat-rule delete [options] <resource-group> <lb-name> <name>

<span data-ttu-id="409a9-254">NAT-regel voor de load balancer in een specifieke resourcegroep verwijderen.</span><span class="sxs-lookup"><span data-stu-id="409a9-254">Deletes NAT rule for the load balancer in a specific resource group.</span></span>

    azure network lb inbound-nat-rule delete -g myresourcegroup -l mylb -n myinboundnat

    info:    Executing command network lb inbound-nat-rule delete
    + Looking up the load balancer "mylb"
    Delete inbound NAT rule "myinboundnat?" [y/n] y
    + Updating load balancer "mylb"
    info:    network lb inbound-nat-rule delete command OK

<span data-ttu-id="409a9-255">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="409a9-255">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -l, --lb-name <lb-name>                the name of the load balancer
    -n, --name <name>                      the name of the inbound NAT rule
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      the subscription identifier

<span data-ttu-id="409a9-256">**Opdrachten voor het openbare IP-adressen beheren**</span><span class="sxs-lookup"><span data-stu-id="409a9-256">**Commands to manage public ip addresses**</span></span>

    network public-ip create [options] <resource-group> <name> <location>
<span data-ttu-id="409a9-257">Maakt een openbaar IP-resource.</span><span class="sxs-lookup"><span data-stu-id="409a9-257">Creates a public ip resource.</span></span> <span data-ttu-id="409a9-258">U de openbare ip-resource maken en koppelen aan een domein.</span><span class="sxs-lookup"><span data-stu-id="409a9-258">You will create the public ip resource and associate to a domain name.</span></span>

    azure network public-ip create -g myresourcegroup -n mytestpublicip1 -l eastus -d azureclitest -a "Dynamic"
    info:    Executing command network public-ip create
    + Looking up the public ip "mytestpublicip1"
    + Creating public ip address "mytestpublicip1"
    + Looking up the public ip "mytestpublicip1"
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


<span data-ttu-id="409a9-259">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="409a9-259">Parameter options:</span></span>

    -h, --help                                   output usage information
    -v, --verbose                                use verbose output
    --json                                       use json output
    -g, --resource-group <resource-group>        the name of the resource group
    -n, --name <name>                            the name of the public ip
    -l, --location <location>                    the location
    -d, --domain-name-label <domain-name-label>  the domain name label.
    This set DNS to <domain-name-label>.<location>.cloudapp.azure.com
    -a, --allocation-method <allocation-method>  the allocation method [Static][Dynamic]
    -i, --idletimeout <idletimeout>              the idle timeout in minutes
    -f, --reverse-fqdn <reverse-fqdn>            the reverse fqdn
    -t, --tags <tags>                            the list of tags.
    Can be multiple. In the format of "name=value".
    Name is required and value is optional.
    For example, -t tag1=value1;tag2
    -s, --subscription <subscription>            the subscription identifier
<br>

    network public-ip set [options] <resource-group> <name>
<span data-ttu-id="409a9-260">De eigenschappen van een bestaande openbare IP-resource-updates.</span><span class="sxs-lookup"><span data-stu-id="409a9-260">Updates the properties of an existing public ip resource.</span></span> <span data-ttu-id="409a9-261">In het volgende voorbeeld wordt het openbare IP-adres van dynamisch gewijzigd naar statisch.</span><span class="sxs-lookup"><span data-stu-id="409a9-261">In the following example we changed the public IP address from Dynamic to Static.</span></span>

    azure network public-ip set -g group-1 -n mytestpublicip1 -d azureclitest -a "Static"
    info:    Executing command network public-ip set
    + Looking up the public ip "mytestpublicip1"
    + Updating public ip address "mytestpublicip1"
    + Looking up the public ip "mytestpublicip1"
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

<span data-ttu-id="409a9-262">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="409a9-262">Parameter options:</span></span>

    -h, --help                                   output usage information
    -v, --verbose                                use verbose output
    --json                                       use json output
    -g, --resource-group <resource-group>        the name of the resource group
    -n, --name <name>                            the name of the public ip
    -d, --domain-name-label [domain-name-label]  the domain name label.
    This set DNS to <domain-name-label>.<location>.cloudapp.azure.com
    -a, --allocation-method <allocation-method>  the allocation method [Static][Dynamic]
    -i, --idletimeout <idletimeout>              the idle timeout in minutes
    -f, --reverse-fqdn [reverse-fqdn]            the reverse fqdn
    -t, --tags <tags>                            the list of tags.
    Can be multiple. In the format of "name=value".
    Name is required and value is optional.
    For example, -t tag1=value1;tag2
    --no-tags                                    remove all existing tags
    -s, --subscription <subscription>            the subscription identifier

<br>
    <span data-ttu-id="409a9-263">lijst met openbare ip-netwerken [opties] < resource-group > geeft een lijst van alle openbare IP-resources binnen een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="409a9-263">network public-ip list [options] <resource-group> Lists all public IP resources within a resource group.</span></span>

    azure network public-ip list -g myresourcegroup

    info:    Executing command network public-ip list
    + Getting the public ip addresses
    data:    Name             Location  Allocation  IP Address    Idle timeout  DNS Name
    data:    ---------------  --------  ----------  ------------  ------------  -------------------------------------------
    data:    mypubip5         westus    Dynamic                   4             "domain name".westus.cloudapp.azure.com
    data:    myPublicIP       eastus    Dynamic                   4             "domain name".eastus.cloudapp.azure.com
    data:    mytestpublicip   eastus    Dynamic                   4             "domain name".eastus.cloudapp.azure.com
    data:    mytestpublicip1  eastus   Static (Static IP address) 4             azureclitest.eastus.cloudapp.azure.com

<span data-ttu-id="409a9-264">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="409a9-264">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -s, --subscription <subscription>      the subscription identifier
<BR>
    <span data-ttu-id="409a9-265">openbaar netwerk-IP-weergeven [opties] < resource-group ><name></span><span class="sxs-lookup"><span data-stu-id="409a9-265">network public-ip show [options] <resource-group> <name></span></span>

<span data-ttu-id="409a9-266">Openbare IP-eigenschappen van een openbaar IP-bron binnen een resourcegroep weergeven</span><span class="sxs-lookup"><span data-stu-id="409a9-266">Displays public ip properties for a public ip resource within a resource group.</span></span>

    azure network public-ip show -g myresourcegroup -n mytestpublicip

    info:    Executing command network public-ip show
    + Looking up the public ip "mytestpublicip1"
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

<span data-ttu-id="409a9-267">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="409a9-267">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -n, --name <name>                      the name of the public IP
    -s, --subscription <subscription>      the subscription identifier


    network public-ip delete [options] <resource-group> <name>

<span data-ttu-id="409a9-268">Hiermee verwijdert u een openbaar IP-resource.</span><span class="sxs-lookup"><span data-stu-id="409a9-268">Deletes public ip resource.</span></span>

    azure network public-ip delete -g group-1 -n mypublicipname
    info:    Executing command network public-ip delete
    + Looking up the public ip "mypublicipname"
    Delete public ip address "mypublicipname"? [y/n] y
    + Deleting public ip address "mypublicipname"
    info:    network public-ip delete command OK

<span data-ttu-id="409a9-269">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="409a9-269">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -n, --name <name>                      the name of the public IP
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      the subscription identifier


<span data-ttu-id="409a9-270">**Opdrachten voor het beheren van netwerkinterfaces**</span><span class="sxs-lookup"><span data-stu-id="409a9-270">**Commands to manage network interfaces**</span></span>

    network nic create [options] <resource-group> <name> <location>
<span data-ttu-id="409a9-271">Maakt een resource netwerkinterface (NIC) die kan worden gebruikt voor load balancers of koppelen aan een virtuele Machine genoemd.</span><span class="sxs-lookup"><span data-stu-id="409a9-271">Creates a resource called network interface (NIC) which can be used for load balancers or associate to a Virtual Machine.</span></span>

    azure network nic create -g myresourcegroup -l eastus -n testnic1 --subnet-name subnet-1 --subnet-vnet-name myvnet

    info:    Executing command network nic create
    + Looking up the network interface "testnic1"
    + Looking up the subnet "subnet-1"
    + Creating network interface "testnic1"
    + Looking up the network interface "testnic1"
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

<span data-ttu-id="409a9-272">De parameteropties:</span><span class="sxs-lookup"><span data-stu-id="409a9-272">Parameter options:</span></span>

    -h, --help                                                       output usage information
    -v, --verbose                                                    use verbose output
    --json                                                           use json output
    -g, --resource-group <resource-group>                            the name of the resource group
    -n, --name <name>                                                the name of the network interface
    -l, --location <location>                                        the location
    -w, --network-security-group-id <network-security-group-id>      the network security group identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/networkSecurityGroups/<nsg-name>
    -o, --network-security-group-name <network-security-group-name>  the network security group name.
    This network security group must exist in the same resource group as the nic.
    Please use network-security-group-id if that is not the case.
    -i, --public-ip-id <public-ip-id>                                the public IP identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/publicIPAddresses/<public-ip-name>
    -p, --public-ip-name <public-ip-name>                            the public IP name.
    This public ip must exist in the same resource group as the nic.
    Please use public-ip-id if that is not the case.
    -a, --private-ip-address <private-ip-address>                    the private IP address
    -u, --subnet-id <subnet-id>                                      the subnet identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<vnet-name>/subnets/<subnet-name>
    --subnet-name <subnet-name>                                  the subnet name
    -m, --subnet-vnet-name <subnet-vnet-name>                        the vnet name under which subnet-name exists
    -t, --tags <tags>                                                the comma seperated list of tags.
    Can be multiple. In the format of "name=value".
    Name is required and value is optional.
    For example, -t tag1=value1;tag2
    -s, --subscription <subscription>                                the subscription identifier
    data:
    info:    network nic create command OK

<BR>

    network nic set [options] <resource-group> <name>

    network nic list [options] <resource-group>
    network nic show [options] <resource-group> <name>
    network nic delete [options] <resource-group> <name>

<span data-ttu-id="409a9-273">**Opdrachten voor het beheren van netwerkbeveiligingsgroepen**</span><span class="sxs-lookup"><span data-stu-id="409a9-273">**Commands to manage network security groups**</span></span>

    network nsg create [options] <resource-group> <name> <location>
    network nsg set [options] <resource-group> <name>
    network nsg list [options] <resource-group>
    network nsg show [options] <resource-group> <name>
    network nsg delete [options] <resource-group> <name>

<span data-ttu-id="409a9-274">**Opdrachten voor het beheren van netwerk-beveiligingsregels voor groep**</span><span class="sxs-lookup"><span data-stu-id="409a9-274">**Commands to manage network security group rules**</span></span>

    network nsg rule create [options] <resource-group> <nsg-name> <name>
    network nsg rule set [options] <resource-group> <nsg-name> <name>
    network nsg rule list [options] <resource-group> <nsg-name>
    network nsg rule show [options] <resource-group> <nsg-name> <name>
    network nsg rule delete [options] <resource-group> <nsg-name> <name>

<span data-ttu-id="409a9-275">**Opdrachten voor het beheren van traffic manager-profiel**</span><span class="sxs-lookup"><span data-stu-id="409a9-275">**Commands to manage traffic manager profile**</span></span>

    network traffic-manager profile create [options] <resource-group> <name>
    network traffic-manager profile set [options] <resource-group> <name>
    network traffic-manager profile list [options] <resource-group>
    network traffic-manager profile show [options] <resource-group> <name>
    network traffic-manager profile delete [options] <resource-group> <name>
    network traffic-manager profile is-dns-available [options] <resource-group> <relative-dns-name>

<span data-ttu-id="409a9-276">**Opdrachten voor het traffic manager-eindpunten beheren**</span><span class="sxs-lookup"><span data-stu-id="409a9-276">**Commands to manage traffic manager endpoints**</span></span>

    network traffic-manager profile endpoint create [options] <resource-group> <profile-name> <name> <endpoint-location>
    network traffic-manager profile endpoint set [options] <resource-group> <profile-name> <name>
    network traffic-manager profile endpoint delete [options] <resource-group> <profile-name> <name>

<span data-ttu-id="409a9-277">**Opdrachten voor het beheren van virtueel netwerk gateways**</span><span class="sxs-lookup"><span data-stu-id="409a9-277">**Commands to manage virtual network gateways**</span></span>

    network gateway list [options] <resource-group>

## <a name="azure-provider-commands-to-manage-resource-provider-registrations"></a><span data-ttu-id="409a9-278">Azure-provider: opdrachten voor het beheren van resource provider registraties</span><span class="sxs-lookup"><span data-stu-id="409a9-278">azure provider: Commands to manage resource provider registrations</span></span>
<span data-ttu-id="409a9-279">**Lijst van de momenteel geregistreerde providers in Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="409a9-279">**List currently registered providers in Resource Manager**</span></span>

    provider list [options]

<span data-ttu-id="409a9-280">**Details weergeven over de naamruimte van de aangevraagde provider**</span><span class="sxs-lookup"><span data-stu-id="409a9-280">**Show details about the requested provider namespace**</span></span>

    provider show [options] <namespace>

<span data-ttu-id="409a9-281">**Registreer provider bij het abonnement**</span><span class="sxs-lookup"><span data-stu-id="409a9-281">**Register provider with the subscription**</span></span>

    provider register [options] <namespace>

<span data-ttu-id="409a9-282">**Hef de registratie van provider met het abonnement**</span><span class="sxs-lookup"><span data-stu-id="409a9-282">**Unregister provider with the subscription**</span></span>

    provider unregister [options] <namespace>

## <a name="azure-resource-commands-to-manage-your-resources"></a><span data-ttu-id="409a9-283">Azure-resource: opdrachten om uw resources te beheren</span><span class="sxs-lookup"><span data-stu-id="409a9-283">azure resource: Commands to manage your resources</span></span>
<span data-ttu-id="409a9-284">**Maakt een resource in een resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="409a9-284">**Creates a resource in a resource group**</span></span>

    resource create [options] <resource-group> <name> <resource-type> <location> <api-version>

<span data-ttu-id="409a9-285">**Updates van een resource in een resourcegroep zonder parameters of sjablonen**</span><span class="sxs-lookup"><span data-stu-id="409a9-285">**Updates a resource in a resource group without any templates or parameters**</span></span>

    resource set [options] <resource-group> <name> <resource-type> <properties> <api-version>

<span data-ttu-id="409a9-286">**Geeft een lijst van de resources**</span><span class="sxs-lookup"><span data-stu-id="409a9-286">**Lists the resources**</span></span>

    resource list [options] [resource-group]

<span data-ttu-id="409a9-287">**Een bron binnen een resourcegroep of abonnement opgehaald**</span><span class="sxs-lookup"><span data-stu-id="409a9-287">**Gets one resource within a resource group or subscription**</span></span>

    resource show [options] <resource-group> <name> <resource-type> <api-version>

<span data-ttu-id="409a9-288">**Hiermee verwijdert u een resource in een resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="409a9-288">**Deletes a resource in a resource group**</span></span>

    resource delete [options] <resource-group> <name> <resource-type> <api-version>

## <a name="azure-role-commands-to-manage-your-azure-roles"></a><span data-ttu-id="409a9-289">Azure-functie: opdrachten voor het beheren van uw Azure-functies</span><span class="sxs-lookup"><span data-stu-id="409a9-289">azure role: Commands to manage your Azure roles</span></span>
<span data-ttu-id="409a9-290">**Alle beschikbare roldefinities ophalen**</span><span class="sxs-lookup"><span data-stu-id="409a9-290">**Get all available role definitions**</span></span>

    role list [options]

<span data-ttu-id="409a9-291">**Een beschikbare roldefinitie ophalen**</span><span class="sxs-lookup"><span data-stu-id="409a9-291">**Get an available role definition**</span></span>

    role show [options] [name]

<span data-ttu-id="409a9-292">**Opdrachten voor het beheren van uw roltoewijzing**</span><span class="sxs-lookup"><span data-stu-id="409a9-292">**Commands to manage your role assignment**</span></span>

    role assignment create [options] [objectId] [upn] [mail] [spn] [role] [scope] [resource-group] [resource-type] [resource-name]
    role assignment list [options] [objectId] [upn] [mail] [spn] [role] [scope] [resource-group] [resource-type] [resource-name]
    role assignment delete [options] [objectId] [upn] [mail] [spn] [role] [scope] [resource-group] [resource-type] [resource-name]

## <a name="azure-storage-commands-to-manage-your-storage-objects"></a><span data-ttu-id="409a9-293">Azure-opslag: opdrachten voor het beheren van uw Storage-objecten</span><span class="sxs-lookup"><span data-stu-id="409a9-293">azure storage: Commands to manage your Storage objects</span></span>
<span data-ttu-id="409a9-294">**Opdrachten voor het beheren van uw Storage-accounts**</span><span class="sxs-lookup"><span data-stu-id="409a9-294">**Commands to manage your Storage accounts**</span></span>

    storage account list [options]
    storage account show [options] <name>
    storage account create [options] <name>
    storage account set [options] <name>
    storage account delete [options] <name>

<span data-ttu-id="409a9-295">**Opdrachten voor het beheren van uw toegangscodes voor opslag**</span><span class="sxs-lookup"><span data-stu-id="409a9-295">**Commands to manage your Storage account keys**</span></span>

    storage account keys list [options] <name>
    storage account keys renew [options] <name>

<span data-ttu-id="409a9-296">**Opdrachten voor het weergeven van de verbindingsreeks voor opslag**</span><span class="sxs-lookup"><span data-stu-id="409a9-296">**Commands to show your Storage connection string**</span></span>

    storage account connectionstring show [options] <name>

<span data-ttu-id="409a9-297">**Opdrachten voor het beheren van uw Storage-containers**</span><span class="sxs-lookup"><span data-stu-id="409a9-297">**Commands to manage your Storage containers**</span></span>

    storage container list [options] [prefix]
    storage container show [options] [container]
    storage container create [options] [container]
    storage container delete [options] [container]
    storage container set [options] [container]

<span data-ttu-id="409a9-298">**Opdrachten voor het beheren van gedeelde toegang tot de handtekeningen van uw Storage-container**</span><span class="sxs-lookup"><span data-stu-id="409a9-298">**Commands to manage shared access signatures of your Storage container**</span></span>

    storage container sas create [options] [container] [permissions] [expiry]

<span data-ttu-id="409a9-299">**Opdrachten voor het beheren van opgeslagen-beleid van uw Storage-container**</span><span class="sxs-lookup"><span data-stu-id="409a9-299">**Commands to manage stored access policies of your Storage container**</span></span>

    storage container policy create [options] [container] [name]
    storage container policy show [options] [container] [name]
    storage container policy list [options] [container]
    storage container policy set [options] [container] [name]
    storage container policy delete [options] [container] [name]

<span data-ttu-id="409a9-300">**Opdrachten voor het beheren van uw Storage-blobs**</span><span class="sxs-lookup"><span data-stu-id="409a9-300">**Commands to manage your Storage blobs**</span></span>

    storage blob list [options] [container] [prefix]
    storage blob show [options] [container] [blob]
    storage blob delete [options] [container] [blob]
    storage blob upload [options] [file] [container] [blob]
    storage blob download [options] [container] [blob] [destination]

<span data-ttu-id="409a9-301">**Opdrachten voor het beheren van uw blob kopiëren bewerkingen**</span><span class="sxs-lookup"><span data-stu-id="409a9-301">**Commands to manage your blob copy operations**</span></span>

    storage blob copy start [options] [sourceUri] [destContainer]
    storage blob copy show [options] [container] [blob]
    storage blob copy stop [options] [container] [blob] [copyid]

<span data-ttu-id="409a9-302">**Opdrachten voor het beheren van gedeelde toegang tot de handtekening van uw Storage-blob**</span><span class="sxs-lookup"><span data-stu-id="409a9-302">**Commands to manage shared access signature of your Storage blob**</span></span>

    storage blob sas create [options] [container] [blob] [permissions] [expiry]

<span data-ttu-id="409a9-303">**Opdrachten voor het beheren van uw bestandsshares voor opslag**</span><span class="sxs-lookup"><span data-stu-id="409a9-303">**Commands to manage your Storage file shares**</span></span>

    storage share create [options] [share]
    storage share show [options] [share]
    storage share delete [options] [share]
    storage share list [options] [prefix]

<span data-ttu-id="409a9-304">**Opdrachten voor het beheren van uw opslag-bestanden**</span><span class="sxs-lookup"><span data-stu-id="409a9-304">**Commands to manage your Storage files**</span></span>

    storage file list [options] [share] [path]
    storage file delete [options] [share] [path]
    storage file upload [options] [source] [share] [path]
    storage file download [options] [share] [path] [destination]

<span data-ttu-id="409a9-305">**Opdrachten voor het beheren van uw bestand opslagmap**</span><span class="sxs-lookup"><span data-stu-id="409a9-305">**Commands to manage your Storage file directory**</span></span>

    storage directory create [options] [share] [path]
    storage directory delete [options] [share] [path]

<span data-ttu-id="409a9-306">**Opdrachten voor het beheren van uw opslagwachtrijen**</span><span class="sxs-lookup"><span data-stu-id="409a9-306">**Commands to manage your Storage queues**</span></span>

    storage queue create [options] [queue]
    storage queue list [options] [prefix]
    storage queue show [options] [queue]
    storage queue delete [options] [queue]

<span data-ttu-id="409a9-307">**Opdrachten voor het beheren van gedeelde toegang tot de handtekeningen van uw Storage-wachtrij**</span><span class="sxs-lookup"><span data-stu-id="409a9-307">**Commands to manage shared access signatures of your Storage queue**</span></span>

    storage queue sas create [options] [queue] [permissions] [expiry]

<span data-ttu-id="409a9-308">**Opdrachten voor het beheren van opgeslagen toegangsbeleid van de wachtrij van uw opslag**</span><span class="sxs-lookup"><span data-stu-id="409a9-308">**Commands to manage stored access policies of your Storage queue**</span></span>

    storage queue policy create [options] [queue] [name]
    storage queue policy show [options] [queue] [name]
    storage queue policy list [options] [queue]
    storage queue policy set [options] [queue] [name]
    storage queue policy delete [options] [queue] [name]

<span data-ttu-id="409a9-309">**Opdrachten voor het beheren van uw opslag logboekregistratie-eigenschappen**</span><span class="sxs-lookup"><span data-stu-id="409a9-309">**Commands to manage your Storage logging properties**</span></span>

    storage logging show [options]
    storage logging set [options]

<span data-ttu-id="409a9-310">**Opdrachten voor het beheren van de eigenschappen van de metrische gegevens van uw opslag**</span><span class="sxs-lookup"><span data-stu-id="409a9-310">**Commands to manage your Storage metrics properties**</span></span>

    storage metrics show [options]
    storage metrics set [options]

<span data-ttu-id="409a9-311">**Opdrachten voor het beheren van uw Storage-tabellen**</span><span class="sxs-lookup"><span data-stu-id="409a9-311">**Commands to manage your Storage tables**</span></span>

    storage table create [options] [table]
    storage table list [options] [prefix]
    storage table show [options] [table]
    storage table delete [options] [table]

<span data-ttu-id="409a9-312">**Opdrachten voor het beheren van gedeelde toegang tot de handtekeningen van de tabel opslag**</span><span class="sxs-lookup"><span data-stu-id="409a9-312">**Commands to manage shared access signatures of your Storage table**</span></span>

    storage table sas create [options] [table] [permissions] [expiry]

<span data-ttu-id="409a9-313">**Opdrachten voor het beheren van opgeslagen toegangsbeleid van de tabel opslag**</span><span class="sxs-lookup"><span data-stu-id="409a9-313">**Commands to manage stored access policies of your Storage table**</span></span>

    storage table policy create [options] [table] [name]
    storage table policy show [options] [table] [name]
    storage table policy list [options] [table]
    storage table policy set [options] [table] [name]
    storage table policy delete [options] [table] [name]

## <a name="azure-tag-commands-to-manage-your-resource-manager-tag"></a><span data-ttu-id="409a9-314">Azure-tag: opdrachten voor het beheren van het resource manager-label</span><span class="sxs-lookup"><span data-stu-id="409a9-314">azure tag: Commands to manage your resource manager tag</span></span>
<span data-ttu-id="409a9-315">**Een label toevoegen**</span><span class="sxs-lookup"><span data-stu-id="409a9-315">**Add a tag**</span></span>

    tag create [options] <name> <value>

<span data-ttu-id="409a9-316">**Een HTML-code of een tagwaarde verwijderen**</span><span class="sxs-lookup"><span data-stu-id="409a9-316">**Remove an entire tag or a tag value**</span></span>

    tag delete [options] <name> <value>

<span data-ttu-id="409a9-317">**Geeft een lijst van de tag-informatie**</span><span class="sxs-lookup"><span data-stu-id="409a9-317">**Lists the tag information**</span></span>

    tag list [options]

<span data-ttu-id="409a9-318">**Een label ophalen**</span><span class="sxs-lookup"><span data-stu-id="409a9-318">**Get a tag**</span></span>

    tag show [options] [name]

## <a name="azure-vm-commands-to-manage-your-azure-virtual-machines"></a><span data-ttu-id="409a9-319">Azure vm: opdrachten voor het beheren van uw Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="409a9-319">azure vm: Commands to manage your Azure Virtual Machines</span></span>
<span data-ttu-id="409a9-320">**Een virtuele machine maken**</span><span class="sxs-lookup"><span data-stu-id="409a9-320">**Create a VM**</span></span>

    vm create [options] <resource-group> <name> <location> <os-type>

<span data-ttu-id="409a9-321">**Een virtuele machine maken met de standaardresources**</span><span class="sxs-lookup"><span data-stu-id="409a9-321">**Create a VM with default resources**</span></span>

    vm quick-create [options] <resource-group> <name> <location> <os-type> <image-urn> <admin-username> <admin-password

> [!TIP]
> <span data-ttu-id="409a9-322">Beginnen met CLI versie 0.10, kunt u een korte alias zoals 'UbuntuLTS' of 'Win2012R2Datacenter' opgeven als de `image-urn` voor bepaalde populaire Marketplace-installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="409a9-322">Starting with CLI version 0.10, you can provide a short alias such as "UbuntuLTS" or "Win2012R2Datacenter" as the `image-urn` for some popular Marketplace images.</span></span> <span data-ttu-id="409a9-323">Voer `azure help vm quick-create` voor opties.</span><span class="sxs-lookup"><span data-stu-id="409a9-323">Run `azure help vm quick-create` for options.</span></span> <span data-ttu-id="409a9-324">Bovendien vanaf versie 0.10, `azure vm quick-create` premium-opslag wordt standaard gebruikt als deze beschikbaar in de geselecteerde regio is.</span><span class="sxs-lookup"><span data-stu-id="409a9-324">Additionally, starting with version 0.10, `azure vm quick-create` uses premium storage by default if it's available in the selected region.</span></span>
> 
> 

<span data-ttu-id="409a9-325">**Lijst van de virtuele machines binnen een account**</span><span class="sxs-lookup"><span data-stu-id="409a9-325">**List the virtual machines within an account**</span></span>

    vm list [options]

<span data-ttu-id="409a9-326">**Ophalen van een virtuele machine binnen een resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="409a9-326">**Get one virtual machine within a resource group**</span></span>

    vm show [options] <resource-group> <name>

<span data-ttu-id="409a9-327">**Een virtuele machine in de resourcegroep verwijderen**</span><span class="sxs-lookup"><span data-stu-id="409a9-327">**Delete one virtual machine within a resource group**</span></span>

    vm delete [options] <resource-group> <name>

<span data-ttu-id="409a9-328">**Een virtuele machine afsluiten binnen een resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="409a9-328">**Shutdown one virtual machine within a resource group**</span></span>

    vm stop [options] <resource-group> <name>

<span data-ttu-id="409a9-329">**Een virtuele machine binnen een resourcegroep opnieuw starten**</span><span class="sxs-lookup"><span data-stu-id="409a9-329">**Restart one virtual machine within a resource group**</span></span>

    vm restart [options] <resource-group> <name>

<span data-ttu-id="409a9-330">**Start één virtuele machine binnen een resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="409a9-330">**Start one virtual machine within a resource group**</span></span>

    vm start [options] <resource-group> <name>

<span data-ttu-id="409a9-331">**Een virtuele machine afsluiten binnen een resourcegroep en worden de rekenresources vrijgegeven**</span><span class="sxs-lookup"><span data-stu-id="409a9-331">**Shutdown one virtual machine within a resource group and releases the compute resources**</span></span>

    vm deallocate [options] <resource-group> <name>

<span data-ttu-id="409a9-332">**Lijst met beschikbare virtuele machine grootten**</span><span class="sxs-lookup"><span data-stu-id="409a9-332">**List available virtual machine sizes**</span></span>

    vm sizes [options]

<span data-ttu-id="409a9-333">**De virtuele machine als de installatiekopie van het besturingssysteem of VM-installatiekopie vastleggen**</span><span class="sxs-lookup"><span data-stu-id="409a9-333">**Capture the VM as OS Image or VM Image**</span></span>

    vm capture [options] <resource-group> <name> <vhd-name-prefix>

<span data-ttu-id="409a9-334">**De status van de virtuele machine ingesteld op gegeneraliseerd**</span><span class="sxs-lookup"><span data-stu-id="409a9-334">**Set the state of the VM to Generalized**</span></span>

    vm generalize [options] <resource-group> <name>

<span data-ttu-id="409a9-335">**Instantieweergave van de virtuele machine ophalen**</span><span class="sxs-lookup"><span data-stu-id="409a9-335">**Get instance view of the VM**</span></span>

    vm get-instance-view [options] <resource-group> <name>

<span data-ttu-id="409a9-336">**Kunt u instellingen voor externe toegang tot het bureaublad of SSH op een virtuele Machine herstellen en in te stellen van het wachtwoord voor het account dat beheerder of sudo-instantie is**</span><span class="sxs-lookup"><span data-stu-id="409a9-336">**Enable you to reset Remote Desktop Access or SSH settings on a Virtual Machine and to reset the password for the account that has administrator or sudo authority**</span></span>

    vm reset-access [options] <resource-group> <name>

<span data-ttu-id="409a9-337">**Virtuele machine bijwerken met nieuwe gegevens**</span><span class="sxs-lookup"><span data-stu-id="409a9-337">**Update VM with new data**</span></span>

    vm set [options] <resource-group> <name>

<span data-ttu-id="409a9-338">**Opdrachten voor het beheren van uw virtuele Machine gegevensschijven**</span><span class="sxs-lookup"><span data-stu-id="409a9-338">**Commands to manage your Virtual Machine data disks**</span></span>

    vm disk attach-new [options] <resource-group> <vm-name> <size-in-gb> [vhd-name]
    vm disk detach [options] <resource-group> <vm-name> <lun>
    vm disk attach [options] <resource-group> <vm-name> [vhd-url]

<span data-ttu-id="409a9-339">**Opdrachten voor het VM-resource-uitbreidingen beheren**</span><span class="sxs-lookup"><span data-stu-id="409a9-339">**Commands to manage VM resource extensions**</span></span>

    vm extension set [options] <resource-group> <vm-name> <name> <publisher-name> <version>
    vm extension get [options] <resource-group> <vm-name>

<span data-ttu-id="409a9-340">**Opdrachten voor het beheren van uw Docker virtuele Machine**</span><span class="sxs-lookup"><span data-stu-id="409a9-340">**Commands to manage your Docker Virtual Machine**</span></span>

    vm docker create [options] <resource-group> <name> <location> <os-type>

<span data-ttu-id="409a9-341">**Opdrachten voor het beheren van VM-installatiekopieën**</span><span class="sxs-lookup"><span data-stu-id="409a9-341">**Commands to manage VM images**</span></span>

    vm image list-publishers [options] <location>
    vm image list-offers [options] <location> <publisher>
    vm image list-skus [options] <location> <publisher> <offer>
    vm image list [options] <location> <publisher> [offer] [sku]
