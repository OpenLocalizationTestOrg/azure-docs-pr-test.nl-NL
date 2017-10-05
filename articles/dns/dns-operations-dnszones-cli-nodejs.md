---
title: DNS-zones in Azure DNS - Azure CLI 1.0 beheren | Microsoft Docs
description: U kunt DNS-zones met behulp van Azure CLI 1.0 beheren. In dit artikel laat zien hoe bijwerken, verwijderen en DNS-zones maken op Azure DNS.
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 8ab63bc4-5135-4ed8-8c0b-5f0712b9afed
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/21/2016
ms.author: gwallace
ms.openlocfilehash: 588c87749f049eff5b9e0729f6769c8367ba41e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-dns-zones-in-azure-dns-using-the-azure-cli-10"></a><span data-ttu-id="e5df6-104">Het beheren van DNS-Zones in Azure DNS met de Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="e5df6-104">How to manage DNS Zones in Azure DNS using the Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e5df6-105">Portal</span><span class="sxs-lookup"><span data-stu-id="e5df6-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="e5df6-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e5df6-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="e5df6-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="e5df6-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="e5df6-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e5df6-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="e5df6-109">Deze handleiding laat zien hoe uw DNS-zones beheren met behulp van de platformoverschrijdende Azure CLI 1.0, die beschikbaar is voor Windows, Mac en Linux.</span><span class="sxs-lookup"><span data-stu-id="e5df6-109">This guide shows how to manage your DNS zones by using the cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="e5df6-110">U kunt ook beheren met behulp van DNS-zones [Azure PowerShell](dns-operations-dnszones.md) of de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e5df6-110">You can also manage your DNS zones using [Azure PowerShell](dns-operations-dnszones.md) or the Azure portal.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="e5df6-111">CLI-versies om de taak uit te voeren</span><span class="sxs-lookup"><span data-stu-id="e5df6-111">CLI versions to complete the task</span></span>

<span data-ttu-id="e5df6-112">U kunt de taak uitvoeren met behulp van een van de volgende CLI-versies:</span><span class="sxs-lookup"><span data-stu-id="e5df6-112">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="e5df6-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md): onze CLI voor het klassieke implementatiemodel en het Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="e5df6-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="e5df6-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md): onze CLI van de volgende generatie voor het Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="e5df6-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) - our next generation CLI for the resource management deployment model.</span></span>

## <a name="introduction"></a><span data-ttu-id="e5df6-115">Inleiding</span><span class="sxs-lookup"><span data-stu-id="e5df6-115">Introduction</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-cli-setup](../../includes/dns-cli-setup-include.md)]

## <a name="getting-help"></a><span data-ttu-id="e5df6-116">Help opvragen</span><span class="sxs-lookup"><span data-stu-id="e5df6-116">Getting help</span></span>

<span data-ttu-id="e5df6-117">Alle 1.0 CLI-opdrachten met betrekking tot de Azure DNS beginnen met `azure network dns`.</span><span class="sxs-lookup"><span data-stu-id="e5df6-117">All CLI 1.0 commands relating to Azure DNS start with `azure network dns`.</span></span> <span data-ttu-id="e5df6-118">Help beschikbaar is voor elke opdracht met behulp van de `--help` optie (korte versie `-h`).</span><span class="sxs-lookup"><span data-stu-id="e5df6-118">Help is available for each command using the `--help` option (short form `-h`).</span></span>  <span data-ttu-id="e5df6-119">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e5df6-119">For example:</span></span>

```azurecli
azure network dns -h
azure network dns zone -h
azure network dns zone create -h
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="e5df6-120">Een DNS-zone maken</span><span class="sxs-lookup"><span data-stu-id="e5df6-120">Create a DNS zone</span></span>

<span data-ttu-id="e5df6-121">Een DNS-zone wordt gemaakt met de opdracht `azure network dns zone create`.</span><span class="sxs-lookup"><span data-stu-id="e5df6-121">A DNS zone is created using the `azure network dns zone create` command.</span></span> <span data-ttu-id="e5df6-122">Zie `azure network dns zone create -h` voor help.</span><span class="sxs-lookup"><span data-stu-id="e5df6-122">For help, see `azure network dns zone create -h`.</span></span>

<span data-ttu-id="e5df6-123">Het volgende voorbeeld wordt een DNS-zone aangeroepen *contoso.com* aangeroepen in de resourcegroep *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="e5df6-123">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*:</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```

### <a name="to-create-a-dns-zone-with-tags"></a><span data-ttu-id="e5df6-124">Een DNS-zone maken met labels</span><span class="sxs-lookup"><span data-stu-id="e5df6-124">To create a DNS zone with tags</span></span>

<span data-ttu-id="e5df6-125">Het volgende voorbeeld laat zien hoe een DNS-zone maken met twee [Azure Resource Manager-tags](dns-zones-records.md#tags), *project = demo* en *env = test*, met behulp van de `--tags` parameter (korte versie `-t`):</span><span class="sxs-lookup"><span data-stu-id="e5df6-125">The following example shows how to create a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*, by using the `--tags` parameter (short form `-t`):</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com -t "project=demo";"env=test"
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="e5df6-126">Ophalen van een DNS-zone</span><span class="sxs-lookup"><span data-stu-id="e5df6-126">Get a DNS zone</span></span>

<span data-ttu-id="e5df6-127">Gebruik voor het ophalen van een DNS-zone `azure network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="e5df6-127">To retrieve a DNS zone, use `azure network dns zone show`.</span></span> <span data-ttu-id="e5df6-128">Zie `azure network dns zone show -h` voor help.</span><span class="sxs-lookup"><span data-stu-id="e5df6-128">For help, see `azure network dns zone show -h`.</span></span>

<span data-ttu-id="e5df6-129">Het volgende voorbeeld retourneert de DNS-zone *contoso.com* en de bijbehorende gegevens van de resourcegroep *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="e5df6-129">The following example returns the DNS zone *contoso.com* and its associated data from resource group *MyResourceGroup*.</span></span> 

```azurecli
azure network dns zone show MyResourceGroup contoso.com
```

<span data-ttu-id="e5df6-130">Het volgende voorbeeld is het antwoord.</span><span class="sxs-lookup"><span data-stu-id="e5df6-130">The following example is the response.</span></span>

```
info:    Executing command network dns zone show
+ Looking up the dns zone "contoso.com"
data:    Id                              : /subscriptions/.../contoso.com
data:    Name                            : contoso.com
data:    Type                            : Microsoft.Network/dnszones
data:    Location                        : global
data:    Number of record sets           : 2
data:    Max number of record sets       : 5000
data:    Name servers:
data:        ns1-01.azure-dns.com.
data:        ns2-01.azure-dns.net.
data:        ns3-01.azure-dns.org.
data:        ns4-01.azure-dns.info.
data:    Tags                            : project=demo;env=test
info:    network dns zone show command OK
```

<span data-ttu-id="e5df6-131">Houd er rekening mee dat DNS-records worden niet geretourneerd door `azure network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="e5df6-131">Note that DNS records are not returned by `azure network dns zone show`.</span></span> <span data-ttu-id="e5df6-132">DNS-records weergeven door gebruiken `azure network dns record-set list`.</span><span class="sxs-lookup"><span data-stu-id="e5df6-132">To list DNS records, use `azure network dns record-set list`.</span></span>


## <a name="list-dns-zones"></a><span data-ttu-id="e5df6-133">Lijst met DNS-zones</span><span class="sxs-lookup"><span data-stu-id="e5df6-133">List DNS zones</span></span>

<span data-ttu-id="e5df6-134">Gebruik voor het inventariseren van DNS-zones `azure network dns zone list`.</span><span class="sxs-lookup"><span data-stu-id="e5df6-134">To enumerate DNS zones, use `azure network dns zone list`.</span></span> <span data-ttu-id="e5df6-135">Zie `azure network dns zone list -h` voor help.</span><span class="sxs-lookup"><span data-stu-id="e5df6-135">For help, see `azure network dns zone list -h`.</span></span>

<span data-ttu-id="e5df6-136">Het opgeven van de resourcegroep bevat alleen deze zones binnen de resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="e5df6-136">Specifying the resource group lists only those zones within the resource group:</span></span>

```azurecli
azure network dns zone list MyResourceGroup
```

<span data-ttu-id="e5df6-137">Als de resourcegroep wordt weggelaten, worden alle zones in het abonnement:</span><span class="sxs-lookup"><span data-stu-id="e5df6-137">Omitting the resource group lists all zones in the subscription:</span></span>

```azurecli
azure network dns zone list 
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="e5df6-138">Bijwerken van een DNS-zone</span><span class="sxs-lookup"><span data-stu-id="e5df6-138">Update a DNS zone</span></span>

<span data-ttu-id="e5df6-139">Een DNS-zone-bron kan worden gewijzigd met behulp van `azure network dns zone set`.</span><span class="sxs-lookup"><span data-stu-id="e5df6-139">Changes to a DNS zone resource can be made using `azure network dns zone set`.</span></span> <span data-ttu-id="e5df6-140">Zie `azure network dns zone set -h` voor help.</span><span class="sxs-lookup"><span data-stu-id="e5df6-140">For help, see `azure network dns zone set -h`.</span></span>

<span data-ttu-id="e5df6-141">Met deze opdracht wordt de DNS-recordsets binnen de zone niet bijgewerkt (Zie [het beheren van DNS-records](dns-operations-recordsets-cli-nodejs.md)).</span><span class="sxs-lookup"><span data-stu-id="e5df6-141">This command does not update any of the DNS record sets within the zone (see [How to Manage DNS records](dns-operations-recordsets-cli-nodejs.md)).</span></span> <span data-ttu-id="e5df6-142">Het wordt alleen gebruikt om de eigenschappen van de bron van de zone zelf te werken.</span><span class="sxs-lookup"><span data-stu-id="e5df6-142">It is only used to update properties of the zone resource itself.</span></span> <span data-ttu-id="e5df6-143">Deze eigenschappen zijn momenteel beperkt tot de [Azure Resource Manager 'labels'](dns-zones-records.md#tags) voor de zoneresource.</span><span class="sxs-lookup"><span data-stu-id="e5df6-143">These properties are currently limited to the [Azure Resource Manager 'tags'](dns-zones-records.md#tags) for the zone resource.</span></span>

<span data-ttu-id="e5df6-144">Het volgende voorbeeld laat zien hoe de labels voor een DNS-zone bijwerken.</span><span class="sxs-lookup"><span data-stu-id="e5df6-144">The following example shows how to update the tags on a DNS zone.</span></span> <span data-ttu-id="e5df6-145">De bestaande labels worden vervangen door de opgegeven waarde.</span><span class="sxs-lookup"><span data-stu-id="e5df6-145">The existing tags are replaced by the value specified.</span></span>

```azurecli
azure network dns zone set MyResourceGroup contoso.com -t "team=support"
```

## <a name="delete-a-dns-zone"></a><span data-ttu-id="e5df6-146">Een DNS-Zone verwijderen</span><span class="sxs-lookup"><span data-stu-id="e5df6-146">Delete a DNS Zone</span></span>

<span data-ttu-id="e5df6-147">DNS-zones worden verwijderd met een `azure network dns zone delete`.</span><span class="sxs-lookup"><span data-stu-id="e5df6-147">DNS zones can be deleted using `azure network dns zone delete`.</span></span> <span data-ttu-id="e5df6-148">Zie `azure network dns zone delete -h` voor help.</span><span class="sxs-lookup"><span data-stu-id="e5df6-148">For help, see `azure network dns zone delete -h`.</span></span>

> [!NOTE]
> <span data-ttu-id="e5df6-149">Een DNS-zone verwijderen, verwijdert tevens alle DNS-records in de zone.</span><span class="sxs-lookup"><span data-stu-id="e5df6-149">Deleting a DNS zone also deletes all DNS records within the zone.</span></span> <span data-ttu-id="e5df6-150">Deze bewerking kan niet ongedaan worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e5df6-150">This operation cannot be undone.</span></span> <span data-ttu-id="e5df6-151">Als de DNS-zone gebruikt wordt, worden services met behulp van de zone mislukt wanneer de zone wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="e5df6-151">If the DNS zone is in use, services using the zone will fail when the zone is deleted.</span></span>
>
><span data-ttu-id="e5df6-152">Als u wilt beveiligen tegen het onbedoeld zone verwijderen, Zie [het beveiligen van DNS-zones en records](dns-protect-zones-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="e5df6-152">To protect against accidental zone deletion, see [How to protect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>

<span data-ttu-id="e5df6-153">Met deze opdracht vraagt om bevestiging.</span><span class="sxs-lookup"><span data-stu-id="e5df6-153">This command prompts for confirmation.</span></span> <span data-ttu-id="e5df6-154">De optionele `--quiet` gaan (korte versie `-q`) deze prompt onderdrukt.</span><span class="sxs-lookup"><span data-stu-id="e5df6-154">The optional `--quiet` switch (short form `-q`) suppresses this prompt.</span></span>

<span data-ttu-id="e5df6-155">Het volgende voorbeeld laat zien hoe de zone verwijderen *contoso.com* uit resourcegroep *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="e5df6-155">The following example shows how to delete the zone *contoso.com* from resource group *MyResourceGroup*.</span></span>

```azurecli
azure network dns zone delete MyResourceGroup contoso.com
```

## <a name="next-steps"></a><span data-ttu-id="e5df6-156">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e5df6-156">Next steps</span></span>

<span data-ttu-id="e5df6-157">Meer informatie over hoe [beheren recordsets en records](dns-getstarted-create-recordset-cli-nodejs.md) in uw DNS-zone.</span><span class="sxs-lookup"><span data-stu-id="e5df6-157">Learn how to [manage record sets and records](dns-getstarted-create-recordset-cli-nodejs.md) in your DNS zone.</span></span>

<span data-ttu-id="e5df6-158">Meer informatie over hoe [uw domein delegeren naar Azure DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="e5df6-158">Learn how to [delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>

