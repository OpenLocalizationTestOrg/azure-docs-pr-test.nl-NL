---
title: Azure Redis-Cache met behulp van Azure CLI aaaManage | Microsoft Docs
description: Meer informatie over hoe tooinstall hello Azure CLI op elk platform hoe toouse het tooconnect tooyour Azure-account, en hoe toocreate en een Redis-cache beheren vanaf hello Azure CLI.
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 964ff245-859d-4bc1-bccf-62e4b3c1169f
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: e8ee30090133e6b4edea93dcd13fd171e75989bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-azure-redis-cache-using-hello-azure-command-line-interface-azure-cli"></a><span data-ttu-id="0abe2-103">Hoe toocreate en beheren van Azure Redis-Cache met behulp van hello Azure-opdrachtregelinterface (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="0abe2-103">How toocreate and manage Azure Redis Cache using hello Azure Command-Line Interface (Azure CLI)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0abe2-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0abe2-104">PowerShell</span></span>](cache-howto-manage-redis-cache-powershell.md)
> * [<span data-ttu-id="0abe2-105">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="0abe2-105">Azure CLI</span></span>](cache-manage-cli.md)
>
>

<span data-ttu-id="0abe2-106">Hello Azure CLI is een uitstekende manier toomanage uw Azure-infrastructuur van een willekeurig platform.</span><span class="sxs-lookup"><span data-stu-id="0abe2-106">hello Azure CLI is a great way toomanage your Azure infrastructure from any platform.</span></span> <span data-ttu-id="0abe2-107">Dit artikel ziet u hoe toocreate en beheren van uw Azure Redis-Cache-exemplaren die gebruikmaken van hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="0abe2-107">This article shows you how toocreate and manage your Azure Redis Cache instances using hello Azure CLI.</span></span>

> [!NOTE]
> <span data-ttu-id="0abe2-108">In dit artikel is van toepassing tooa eerdere versie van Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="0abe2-108">This article applies tooa previous version of Azure CLI.</span></span> <span data-ttu-id="0abe2-109">Zie voor Hallo nieuwste Azure CLI 2.0 voorbeeldscripts [CLI van Azure Redis-cache-voorbeelden](cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="0abe2-109">For hello latest Azure CLI 2.0 sample scripts, see [Azure CLI Redis cache samples](cli-samples.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="0abe2-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="0abe2-110">Prerequisites</span></span>
<span data-ttu-id="0abe2-111">toocreate en beheren van Azure Redis-Cache-exemplaren die gebruikmaken van Azure CLI, moet u Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="0abe2-111">toocreate and manage Azure Redis Cache instances using Azure CLI, you must complete hello following steps.</span></span>

* <span data-ttu-id="0abe2-112">U moet een Azure-account hebben.</span><span class="sxs-lookup"><span data-stu-id="0abe2-112">You must have an Azure account.</span></span> <span data-ttu-id="0abe2-113">Als u niet hebt, kunt u een [gratis account](https://azure.microsoft.com/pricing/free-trial/) in slechts enkele ogenblikken.</span><span class="sxs-lookup"><span data-stu-id="0abe2-113">If you don't have one, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a few moments.</span></span>
* <span data-ttu-id="0abe2-114">[Hello Azure CLI installeren](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="0abe2-114">[Install hello Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="0abe2-115">Verbinding maken met de Azure CLI-installatie met een persoonlijke Azure-account of met een werk of school Azure-account en zich aanmelden vanaf hello Azure CLI met Hallo `azure login` opdracht.</span><span class="sxs-lookup"><span data-stu-id="0abe2-115">Connect your Azure CLI installation with a personal Azure account, or with a work or school Azure account, and log in from hello Azure CLI using hello `azure login` command.</span></span> <span data-ttu-id="0abe2-116">toounderstand Hallo verschillen en kies, Zie [tooan Azure-abonnement van hello Azure-opdrachtregelinterface (Azure CLI) verbinding](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="0abe2-116">toounderstand hello differences and choose, see [Connect tooan Azure subscription from hello Azure Command-Line Interface (Azure CLI)](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="0abe2-117">Voordat met een van de volgende opdrachten Hallo, hello Azure CLI in de modus Resource Manager-switch door te voeren Hallo `azure config mode arm` opdracht.</span><span class="sxs-lookup"><span data-stu-id="0abe2-117">Before running any of hello following commands, switch hello Azure CLI into Resource Manager mode by running hello `azure config mode arm` command.</span></span> <span data-ttu-id="0abe2-118">Zie voor meer informatie [hello Azure CLI toomanage Azure gebruiken resources en resourcegroepen](../xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="0abe2-118">For more information, see [Use hello Azure CLI toomanage Azure resources and resource groups](../xplat-cli-azure-resource-manager.md).</span></span>

## <a name="redis-cache-properties"></a><span data-ttu-id="0abe2-119">Redis-Cache-eigenschappen</span><span class="sxs-lookup"><span data-stu-id="0abe2-119">Redis Cache properties</span></span>
<span data-ttu-id="0abe2-120">Hallo worden volgende eigenschappen gebruikt bij het maken en bijwerken van Redis-Cache-exemplaren.</span><span class="sxs-lookup"><span data-stu-id="0abe2-120">hello following properties are used when creating and updating Redis Cache instances.</span></span>

| <span data-ttu-id="0abe2-121">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="0abe2-121">Property</span></span> | <span data-ttu-id="0abe2-122">Switch</span><span class="sxs-lookup"><span data-stu-id="0abe2-122">Switch</span></span> | <span data-ttu-id="0abe2-123">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0abe2-123">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0abe2-124">naam</span><span class="sxs-lookup"><span data-stu-id="0abe2-124">name</span></span> |<span data-ttu-id="0abe2-125">-n,--naam</span><span class="sxs-lookup"><span data-stu-id="0abe2-125">-n, --name</span></span> |<span data-ttu-id="0abe2-126">Naam van Hallo Redis-Cache.</span><span class="sxs-lookup"><span data-stu-id="0abe2-126">Name of hello Redis Cache.</span></span> |
| <span data-ttu-id="0abe2-127">resourcegroep</span><span class="sxs-lookup"><span data-stu-id="0abe2-127">resource group</span></span> |<span data-ttu-id="0abe2-128">-g,--resourcegroep</span><span class="sxs-lookup"><span data-stu-id="0abe2-128">-g, --resource-group</span></span> |<span data-ttu-id="0abe2-129">Naam van Hallo resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="0abe2-129">Name of hello Resource Group.</span></span> |
| <span data-ttu-id="0abe2-130">location</span><span class="sxs-lookup"><span data-stu-id="0abe2-130">location</span></span> |<span data-ttu-id="0abe2-131">-l,--locatie</span><span class="sxs-lookup"><span data-stu-id="0abe2-131">-l, --location</span></span> |<span data-ttu-id="0abe2-132">Locatie toocreate cache.</span><span class="sxs-lookup"><span data-stu-id="0abe2-132">Location toocreate cache.</span></span> |
| <span data-ttu-id="0abe2-133">Grootte</span><span class="sxs-lookup"><span data-stu-id="0abe2-133">size</span></span> |<span data-ttu-id="0abe2-134">-z,--grootte</span><span class="sxs-lookup"><span data-stu-id="0abe2-134">-z, --size</span></span> |<span data-ttu-id="0abe2-135">Grootte van Hallo Redis-Cache.</span><span class="sxs-lookup"><span data-stu-id="0abe2-135">Size of hello Redis Cache.</span></span> <span data-ttu-id="0abe2-136">Geldige waarden: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]</span><span class="sxs-lookup"><span data-stu-id="0abe2-136">Valid values: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]</span></span> |
| <span data-ttu-id="0abe2-137">SKU</span><span class="sxs-lookup"><span data-stu-id="0abe2-137">sku</span></span> |<span data-ttu-id="0abe2-138">-x--sku</span><span class="sxs-lookup"><span data-stu-id="0abe2-138">-x, --sku</span></span> |<span data-ttu-id="0abe2-139">Redis SKU.</span><span class="sxs-lookup"><span data-stu-id="0abe2-139">Redis SKU.</span></span> <span data-ttu-id="0abe2-140">Moet een van: [Basic, Standard, Premium]</span><span class="sxs-lookup"><span data-stu-id="0abe2-140">Should be one of : [Basic, Standard, Premium]</span></span> |
| <span data-ttu-id="0abe2-141">EnableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="0abe2-141">EnableNonSslPort</span></span> |<span data-ttu-id="0abe2-142">-e,--enable-niet-ssl-poort</span><span class="sxs-lookup"><span data-stu-id="0abe2-142">-e, --enable-non-ssl-port</span></span> |<span data-ttu-id="0abe2-143">De eigenschap EnableNonSslPort Hallo Redis-Cache.</span><span class="sxs-lookup"><span data-stu-id="0abe2-143">EnableNonSslPort property of hello Redis Cache.</span></span> <span data-ttu-id="0abe2-144">Deze markering toevoegen als u wilt dat tooenable Hallo niet-SSL-poort voor uw cache</span><span class="sxs-lookup"><span data-stu-id="0abe2-144">Add this flag if you want tooenable hello Non SSL Port for your cache</span></span> |
| <span data-ttu-id="0abe2-145">Configuratie van redis</span><span class="sxs-lookup"><span data-stu-id="0abe2-145">Redis Configuration</span></span> |<span data-ttu-id="0abe2-146">-c,--redis-configuratie</span><span class="sxs-lookup"><span data-stu-id="0abe2-146">-c, --redis-configuration</span></span> |<span data-ttu-id="0abe2-147">Redis-configuratie.</span><span class="sxs-lookup"><span data-stu-id="0abe2-147">Redis Configuration.</span></span> <span data-ttu-id="0abe2-148">Geef een string in JSON-indeling van de van configuratiesleutels en waarden die hier.</span><span class="sxs-lookup"><span data-stu-id="0abe2-148">Enter a JSON formatted string of configuration keys and values here.</span></span> <span data-ttu-id="0abe2-149">Indeling: ' {' ': "","": ""} "</span><span class="sxs-lookup"><span data-stu-id="0abe2-149">Format:"{"":"","":""}"</span></span> |
| <span data-ttu-id="0abe2-150">Configuratie van redis</span><span class="sxs-lookup"><span data-stu-id="0abe2-150">Redis Configuration</span></span> |<span data-ttu-id="0abe2-151">-f,--redis-configuratiebestand</span><span class="sxs-lookup"><span data-stu-id="0abe2-151">-f, --redis-configuration-file</span></span> |<span data-ttu-id="0abe2-152">Redis-configuratie.</span><span class="sxs-lookup"><span data-stu-id="0abe2-152">Redis Configuration.</span></span> <span data-ttu-id="0abe2-153">Hallo-pad van een bestand met configuratiesleutels en waarden die hier invoeren.</span><span class="sxs-lookup"><span data-stu-id="0abe2-153">Enter hello path of a file containing configuration keys and values here.</span></span> <span data-ttu-id="0abe2-154">Indeling voor de vermelding in het Hallo: {"": "","": ""}</span><span class="sxs-lookup"><span data-stu-id="0abe2-154">Format for hello file entry: {"":"","":""}</span></span> |
| <span data-ttu-id="0abe2-155">Aantal shard</span><span class="sxs-lookup"><span data-stu-id="0abe2-155">Shard Count</span></span> |<span data-ttu-id="0abe2-156">-r,--shard-telling</span><span class="sxs-lookup"><span data-stu-id="0abe2-156">-r, --shard-count</span></span> |<span data-ttu-id="0abe2-157">Het aantal Shards toocreate op een Cluster Premium Cache met clustering.</span><span class="sxs-lookup"><span data-stu-id="0abe2-157">Number of Shards toocreate on a Premium Cluster Cache with clustering.</span></span> |
| <span data-ttu-id="0abe2-158">Virtual Network</span><span class="sxs-lookup"><span data-stu-id="0abe2-158">Virtual Network</span></span> |<span data-ttu-id="0abe2-159">-v,--virtueel netwerk</span><span class="sxs-lookup"><span data-stu-id="0abe2-159">-v, --virtual-network</span></span> |<span data-ttu-id="0abe2-160">Bij het hosten van uw cache in een VNET Hallo exacte ARM bron-ID van Hallo virtueel netwerk toodeploy hello redis-cache in.</span><span class="sxs-lookup"><span data-stu-id="0abe2-160">When hosting your cache in a VNET, specifies hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in.</span></span> <span data-ttu-id="0abe2-161">Voorbeeld van de indeling: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span><span class="sxs-lookup"><span data-stu-id="0abe2-161">Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span></span> |
| <span data-ttu-id="0abe2-162">sleuteltype</span><span class="sxs-lookup"><span data-stu-id="0abe2-162">key type</span></span> |<span data-ttu-id="0abe2-163">-t,--sleutel-type</span><span class="sxs-lookup"><span data-stu-id="0abe2-163">-t, --key-type</span></span> |<span data-ttu-id="0abe2-164">Het type van de belangrijkste toorenew.</span><span class="sxs-lookup"><span data-stu-id="0abe2-164">Type of key toorenew.</span></span> <span data-ttu-id="0abe2-165">Geldige waarden: [primaire, secundaire]</span><span class="sxs-lookup"><span data-stu-id="0abe2-165">Valid values: [Primary, Secondary]</span></span> |
| <span data-ttu-id="0abe2-166">StaticIP</span><span class="sxs-lookup"><span data-stu-id="0abe2-166">StaticIP</span></span> |<span data-ttu-id="0abe2-167">-p,--statisch ip-< statisch ip-></span><span class="sxs-lookup"><span data-stu-id="0abe2-167">-p, --static-ip <static-ip></span></span> |<span data-ttu-id="0abe2-168">Bij het hosten van uw cache in een VNET, geeft een uniek IP-adres in Hallo-subnet voor Hallo-cache.</span><span class="sxs-lookup"><span data-stu-id="0abe2-168">When hosting your cache in a VNET, specifies a unique IP address in hello subnet for hello cache.</span></span> <span data-ttu-id="0abe2-169">Als niet wordt opgegeven, wordt een gekozen voor u van Hallo subnet.</span><span class="sxs-lookup"><span data-stu-id="0abe2-169">If not provided, one is chosen for you from hello subnet.</span></span> |
| <span data-ttu-id="0abe2-170">Subnet</span><span class="sxs-lookup"><span data-stu-id="0abe2-170">Subnet</span></span> |<span data-ttu-id="0abe2-171">t,--subnet<subnet></span><span class="sxs-lookup"><span data-stu-id="0abe2-171">t, --subnet <subnet></span></span> |<span data-ttu-id="0abe2-172">Bij het hosten van uw cache in een VNET, geeft Hallo-naam van Hallo subnet in welke toodeploy Hallo-cache.</span><span class="sxs-lookup"><span data-stu-id="0abe2-172">When hosting your cache in a VNET, specifies hello name of hello subnet in which toodeploy hello cache.</span></span> |
| <span data-ttu-id="0abe2-173">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="0abe2-173">VirtualNetwork</span></span> |<span data-ttu-id="0abe2-174">-v,--virtueel netwerk < virtuele-netwerk ></span><span class="sxs-lookup"><span data-stu-id="0abe2-174">-v, --virtual-network <virtual-network></span></span> |<span data-ttu-id="0abe2-175">Bij het hosten van uw cache in een VNET Hallo exacte ARM bron-ID van Hallo virtueel netwerk toodeploy hello redis-cache in.</span><span class="sxs-lookup"><span data-stu-id="0abe2-175">When hosting your cache in a VNET, specifies hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in.</span></span> <span data-ttu-id="0abe2-176">Voorbeeld van de indeling: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span><span class="sxs-lookup"><span data-stu-id="0abe2-176">Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span></span> |
| <span data-ttu-id="0abe2-177">Abonnement</span><span class="sxs-lookup"><span data-stu-id="0abe2-177">Subscription</span></span> |<span data-ttu-id="0abe2-178">-s,--abonnement</span><span class="sxs-lookup"><span data-stu-id="0abe2-178">-s, --subscription</span></span> |<span data-ttu-id="0abe2-179">Hallo abonnements-id.</span><span class="sxs-lookup"><span data-stu-id="0abe2-179">hello subscription identifier.</span></span> |

## <a name="see-all-redis-cache-commands"></a><span data-ttu-id="0abe2-180">Zie alle opdrachten voor Redis-Cache</span><span class="sxs-lookup"><span data-stu-id="0abe2-180">See all Redis Cache commands</span></span>
<span data-ttu-id="0abe2-181">toosee alle opdrachten voor Redis-Cache en de bijbehorende parameters gebruiken Hallo `azure rediscache -h` opdracht.</span><span class="sxs-lookup"><span data-stu-id="0abe2-181">toosee all Redis Cache commands and their parameters, use hello `azure rediscache -h` command.</span></span>

    C:\>azure rediscache -h
    help:    Commands toomanage your Azure Redis Cache(s)
    help:
    help:    Create a Redis Cache
    help:      rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]
    help:
    help:    Delete an existing Redis Cache
    help:      rediscache delete [--name <name> --resource-group <resource-group> ]
    help:
    help:    List all Redis Caches within your Subscription or Resource Group
    help:      rediscache list [options]
    help:
    help:    Show properties of an existing Redis Cache
    help:      rediscache show [--name <name> --resource-group <resource-group>]
    help:
    help:    Change settings of an existing Redis Cache
    help:      rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]
    help:
    help:    Renew hello authentication key for an existing Redis Cache
    help:      rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Lists Primary and Secondary key of an existing Redis Cache
    help:      rediscache list-keys [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help  output usage information
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="create-a-redis-cache"></a><span data-ttu-id="0abe2-182">Een Redis-cache maken</span><span class="sxs-lookup"><span data-stu-id="0abe2-182">Create a Redis Cache</span></span>
<span data-ttu-id="0abe2-183">toocreate Redis-Cache gebruiken Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="0abe2-183">toocreate a Redis Cache, use hello following command:</span></span>

    azure rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]

<span data-ttu-id="0abe2-184">Voor meer informatie over deze opdracht uitvoeren Hallo `azure rediscache create -h` opdracht.</span><span class="sxs-lookup"><span data-stu-id="0abe2-184">For more information about this command, run hello `azure rediscache create -h` command.</span></span>

    C:\>azure rediscache create -h
    help:    Create a Redis Cache
    help:
    help:    Usage: rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]
    help:
    help:    Options:
    help:      -h, --help                                               output usage information
    help:      -v, --verbose                                            use verbose output
    help:      -vv                                                      more verbose with debug output
    help:      --json                                                   use json output
    help:      -n, --name <name>                                        Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of hello Resource Group
    help:      -l, --location <location>                                Location toocreate cache.
    help:      -z, --size <size>                                        Size of hello Redis Cache. Valid values: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]
    help:      -x, --sku <sku>                                          Redis SKU. Should be one of : [Basic, Standard, Premium]
    help:      -e, --enable-non-ssl-port                                EnableNonSslPort property of hello Redis Cache. Add this flag if you want tooenable hello Non SSL Port for your cache
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here. Format:"{"<key1>":"<value1>","<key2>":"<value2>"}"
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter hello path of a file containing configuration keys and values here. Format for hello file entry: {"<key1>":"<value1>","<key2>":"<value2>"}
    help:      -r, --shard-count <shard-count>                          Number of Shards toocreate on a Premium Cluster Cache
    help:      -v, --virtual-network <virtual-network>                  hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in. Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1
    help:      -t, --subnet <subnet>                                    Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -p, --static-ip <static-ip>                              Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -s, --subscription <id>                                  hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="delete-an-existing-redis-cache"></a><span data-ttu-id="0abe2-185">Verwijderen van een bestaande Redis-Cache</span><span class="sxs-lookup"><span data-stu-id="0abe2-185">Delete an existing Redis Cache</span></span>
<span data-ttu-id="0abe2-186">toodelete Redis-Cache gebruiken Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="0abe2-186">toodelete a Redis Cache, use hello following command:</span></span>

    azure rediscache delete [--name <name> --resource-group <resource-group> ]

<span data-ttu-id="0abe2-187">Voor meer informatie over deze opdracht uitvoeren Hallo `azure rediscache delete -h` opdracht.</span><span class="sxs-lookup"><span data-stu-id="0abe2-187">For more information about this command, run hello `azure rediscache delete -h` command.</span></span>

    C:\>azure rediscache delete -h
    help:    Delete an existing Redis Cache
    help:
    help:    Usage: rediscache delete [--name <name> --resource-group <resource-group> ]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which hello cache exists
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-all-redis-caches-within-your-subscription-or-resource-group"></a><span data-ttu-id="0abe2-188">Lijst van alle Redis-Caches binnen uw abonnement of resourcegroep</span><span class="sxs-lookup"><span data-stu-id="0abe2-188">List all Redis Caches within your Subscription or Resource Group</span></span>
<span data-ttu-id="0abe2-189">alle Redis-Caches binnen uw abonnement of resourcegroep, gebruikt u toolist Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="0abe2-189">toolist all Redis Caches within your Subscription or Resource Group, use hello following command:</span></span>

    azure rediscache list [options]

<span data-ttu-id="0abe2-190">Voor meer informatie over deze opdracht uitvoeren Hallo `azure rediscache list -h` opdracht.</span><span class="sxs-lookup"><span data-stu-id="0abe2-190">For more information about this command, run hello `azure rediscache list -h` command.</span></span>

    C:\>azure rediscache list -h
    help:    List all Redis Caches within your Subscription or Resource Group
    help:
    help:    Usage: rediscache list [options]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="show-properties-of-an-existing-redis-cache"></a><span data-ttu-id="0abe2-191">Eigenschappen van een bestaande Redis-Cache weergeven</span><span class="sxs-lookup"><span data-stu-id="0abe2-191">Show properties of an existing Redis Cache</span></span>
<span data-ttu-id="0abe2-192">tooshow eigenschappen van een bestaande Redis-Cache, Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="0abe2-192">tooshow properties of an existing Redis Cache, use hello following command:</span></span>

    azure rediscache show [--name <name> --resource-group <resource-group>]

<span data-ttu-id="0abe2-193">Voor meer informatie over deze opdracht uitvoeren Hallo `azure rediscache show -h` opdracht.</span><span class="sxs-lookup"><span data-stu-id="0abe2-193">For more information about this command, run hello `azure rediscache show -h` command.</span></span>

    C:\>azure rediscache show -h
    help:    Show properties of an existing Redis Cache
    help:
    help:    Usage: rediscache show [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

<a name="scale"></a>

## <a name="change-settings-of-an-existing-redis-cache"></a><span data-ttu-id="0abe2-194">Instellingen van een bestaande Redis-Cache wijzigen</span><span class="sxs-lookup"><span data-stu-id="0abe2-194">Change settings of an existing Redis Cache</span></span>
<span data-ttu-id="0abe2-195">toochange instellingen van een bestaande Redis-Cache, gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="0abe2-195">toochange settings of an existing Redis Cache, use hello following command:</span></span>

    azure rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]

<span data-ttu-id="0abe2-196">Voor meer informatie over deze opdracht uitvoeren Hallo `azure rediscache set -h` opdracht.</span><span class="sxs-lookup"><span data-stu-id="0abe2-196">For more information about this command, run hello `azure rediscache set -h` command.</span></span>

    C:\>azure rediscache set -h
    help:    Change settings of an existing Redis Cache
    help:
    help:    Usage: rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]
    help:
    help:    Options:
    help:      -h, --help                                               output usage information
    help:      -v, --verbose                                            use verbose output
    help:      -vv                                                      more verbose with debug output
    help:      --json                                                   use json output
    help:      -n, --name <name>                                        Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of hello Resource Group
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here.
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter hello path of a file containing configuration keys and values here.
    help:      -s, --subscription <subscription>                        hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="renew-hello-authentication-key-for-an-existing-redis-cache"></a><span data-ttu-id="0abe2-197">Hallo-verificatiesleutel vernieuwen voor een bestaande Redis-Cache</span><span class="sxs-lookup"><span data-stu-id="0abe2-197">Renew hello authentication key for an existing Redis Cache</span></span>
<span data-ttu-id="0abe2-198">toorenew Hallo-verificatiesleutel voor een bestaande Redis-Cache, gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="0abe2-198">toorenew hello authentication key for an existing Redis Cache, use hello following command:</span></span>

    azure rediscache renew-key [--name <name> --resource-group <resource-group> --key-type <key-type>]

<span data-ttu-id="0abe2-199">Geef `Primary` of `Secondary` voor `key-type`.</span><span class="sxs-lookup"><span data-stu-id="0abe2-199">Specify `Primary` or `Secondary` for `key-type`.</span></span>

<span data-ttu-id="0abe2-200">Voor meer informatie over deze opdracht uitvoeren Hallo `azure rediscache renew-key -h` opdracht.</span><span class="sxs-lookup"><span data-stu-id="0abe2-200">For more information about this command, run hello `azure rediscache renew-key -h` command.</span></span>

    C:\>azure rediscache renew-key -h
    help:    Renew hello authentication key for an existing Redis Cache
    help:
    help:    Usage: rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which cache exists
    help:      -t, --key-type <key-type>              type of key toorenew. Valid values are: 'Primary', 'Secondary'.
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-primary-and-secondary-keys-of-an-existing-redis-cache"></a><span data-ttu-id="0abe2-201">Lijst met primaire en secundaire sleutels van een bestaande Redis-Cache</span><span class="sxs-lookup"><span data-stu-id="0abe2-201">List Primary and Secondary keys of an existing Redis Cache</span></span>
<span data-ttu-id="0abe2-202">de primaire en secundaire sleutels toolist van een bestaande Redis-Cache, Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="0abe2-202">toolist Primary and Secondary keys of an existing Redis Cache, use hello following command:</span></span>

    azure rediscache list-keys [--name <name> --resource-group <resource-group>]

<span data-ttu-id="0abe2-203">Voor meer informatie over deze opdracht uitvoeren Hallo `azure rediscache list-keys -h` opdracht.</span><span class="sxs-lookup"><span data-stu-id="0abe2-203">For more information about this command, run hello `azure rediscache list-keys -h` command.</span></span>

    C:\>azure rediscache list-keys -h
    help:    Lists Primary and Secondary key of an existing Redis Cache
    help:
    help:    Usage: rediscache list-keys [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which Cache exists
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)
