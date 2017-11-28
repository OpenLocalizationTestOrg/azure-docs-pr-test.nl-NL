---
title: aaaManage DNS-zones in Azure DNS - Azure CLI 1.0 | Microsoft Docs
description: U kunt DNS-zones met behulp van Azure CLI 1.0 beheren. Dit artikel laat zien hoe tooupdate, verwijderen en DNS-zones maken op Azure DNS.
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
ms.openlocfilehash: cb9790cc46626ef7f38a43edb57511104fe6057e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-azure-dns-using-hello-azure-cli-10"></a><span data-ttu-id="2c499-104">Hoe toomanage DNS-Zones in Azure DNS met behulp van Azure CLI 1.0 Hallo</span><span class="sxs-lookup"><span data-stu-id="2c499-104">How toomanage DNS Zones in Azure DNS using hello Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2c499-105">Portal</span><span class="sxs-lookup"><span data-stu-id="2c499-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="2c499-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2c499-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="2c499-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="2c499-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="2c499-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="2c499-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="2c499-109">Deze handleiding wordt getoond hoe toomanage uw DNS-zones met behulp van Hallo platformoverschrijdende Azure CLI 1.0, die beschikbaar is voor Windows, Mac en Linux.</span><span class="sxs-lookup"><span data-stu-id="2c499-109">This guide shows how toomanage your DNS zones by using hello cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="2c499-110">U kunt ook beheren met behulp van DNS-zones [Azure PowerShell](dns-operations-dnszones.md) of hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="2c499-110">You can also manage your DNS zones using [Azure PowerShell](dns-operations-dnszones.md) or hello Azure portal.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="2c499-111">CLI-versies toocomplete Hallo taak</span><span class="sxs-lookup"><span data-stu-id="2c499-111">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="2c499-112">U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="2c499-112">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="2c499-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) -onze CLI voor Hallo klassieke en resource management implementatiemodellen.</span><span class="sxs-lookup"><span data-stu-id="2c499-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) - our CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="2c499-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="2c499-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) - our next generation CLI for hello resource management deployment model.</span></span>

## <a name="introduction"></a><span data-ttu-id="2c499-115">Inleiding</span><span class="sxs-lookup"><span data-stu-id="2c499-115">Introduction</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-cli-setup](../../includes/dns-cli-setup-include.md)]

## <a name="getting-help"></a><span data-ttu-id="2c499-116">Help opvragen</span><span class="sxs-lookup"><span data-stu-id="2c499-116">Getting help</span></span>

<span data-ttu-id="2c499-117">Alle betreffende tooAzure DNS CLI 1.0-opdrachten starten met `azure network dns`.</span><span class="sxs-lookup"><span data-stu-id="2c499-117">All CLI 1.0 commands relating tooAzure DNS start with `azure network dns`.</span></span> <span data-ttu-id="2c499-118">Help beschikbaar is voor elke opdracht met Hallo `--help` optie (korte versie `-h`).</span><span class="sxs-lookup"><span data-stu-id="2c499-118">Help is available for each command using hello `--help` option (short form `-h`).</span></span>  <span data-ttu-id="2c499-119">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2c499-119">For example:</span></span>

```azurecli
azure network dns -h
azure network dns zone -h
azure network dns zone create -h
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="2c499-120">Een DNS-zone maken</span><span class="sxs-lookup"><span data-stu-id="2c499-120">Create a DNS zone</span></span>

<span data-ttu-id="2c499-121">Een DNS-zone wordt gemaakt met Hallo `azure network dns zone create` opdracht.</span><span class="sxs-lookup"><span data-stu-id="2c499-121">A DNS zone is created using hello `azure network dns zone create` command.</span></span> <span data-ttu-id="2c499-122">Zie `azure network dns zone create -h` voor help.</span><span class="sxs-lookup"><span data-stu-id="2c499-122">For help, see `azure network dns zone create -h`.</span></span>

<span data-ttu-id="2c499-123">Hallo volgende voorbeeld maakt u een DNS-zone aangeroepen *contoso.com* in de resourcegroep Hallo aangeroepen *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="2c499-123">hello following example creates a DNS zone called *contoso.com* in hello resource group called *MyResourceGroup*:</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```

### <a name="toocreate-a-dns-zone-with-tags"></a><span data-ttu-id="2c499-124">toocreate een DNS-zone met labels</span><span class="sxs-lookup"><span data-stu-id="2c499-124">toocreate a DNS zone with tags</span></span>

<span data-ttu-id="2c499-125">Hallo volgende voorbeeld laat zien hoe toocreate een DNS-zone met twee [Azure Resource Manager-tags](dns-zones-records.md#tags), *project = demo* en *env = test*, met behulp van Hallo `--tags` parameter (korte versie `-t`):</span><span class="sxs-lookup"><span data-stu-id="2c499-125">hello following example shows how toocreate a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*, by using hello `--tags` parameter (short form `-t`):</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com -t "project=demo";"env=test"
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="2c499-126">Ophalen van een DNS-zone</span><span class="sxs-lookup"><span data-stu-id="2c499-126">Get a DNS zone</span></span>

<span data-ttu-id="2c499-127">gebruik van een DNS-zone tooretrieve `azure network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="2c499-127">tooretrieve a DNS zone, use `azure network dns zone show`.</span></span> <span data-ttu-id="2c499-128">Zie `azure network dns zone show -h` voor help.</span><span class="sxs-lookup"><span data-stu-id="2c499-128">For help, see `azure network dns zone show -h`.</span></span>

<span data-ttu-id="2c499-129">Hallo volgende voorbeeld retourneert Hallo DNS-zone *contoso.com* en de bijbehorende gegevens van de resourcegroep *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="2c499-129">hello following example returns hello DNS zone *contoso.com* and its associated data from resource group *MyResourceGroup*.</span></span> 

```azurecli
azure network dns zone show MyResourceGroup contoso.com
```

<span data-ttu-id="2c499-130">Hallo volgende voorbeeld is Hallo antwoord.</span><span class="sxs-lookup"><span data-stu-id="2c499-130">hello following example is hello response.</span></span>

```
info:    Executing command network dns zone show
+ Looking up hello dns zone "contoso.com"
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

<span data-ttu-id="2c499-131">Houd er rekening mee dat DNS-records worden niet geretourneerd door `azure network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="2c499-131">Note that DNS records are not returned by `azure network dns zone show`.</span></span> <span data-ttu-id="2c499-132">gebruik van DNS-records van toolist `azure network dns record-set list`.</span><span class="sxs-lookup"><span data-stu-id="2c499-132">toolist DNS records, use `azure network dns record-set list`.</span></span>


## <a name="list-dns-zones"></a><span data-ttu-id="2c499-133">Lijst met DNS-zones</span><span class="sxs-lookup"><span data-stu-id="2c499-133">List DNS zones</span></span>

<span data-ttu-id="2c499-134">tooenumerate DNS-zones, gebruik `azure network dns zone list`.</span><span class="sxs-lookup"><span data-stu-id="2c499-134">tooenumerate DNS zones, use `azure network dns zone list`.</span></span> <span data-ttu-id="2c499-135">Zie `azure network dns zone list -h` voor help.</span><span class="sxs-lookup"><span data-stu-id="2c499-135">For help, see `azure network dns zone list -h`.</span></span>

<span data-ttu-id="2c499-136">Het opgeven van het Hallo-resourcegroep bevat alleen deze zones in de resourcegroep Hallo:</span><span class="sxs-lookup"><span data-stu-id="2c499-136">Specifying hello resource group lists only those zones within hello resource group:</span></span>

```azurecli
azure network dns zone list MyResourceGroup
```

<span data-ttu-id="2c499-137">Hallo resourcegroep als weggelaten een lijst met alle zones in abonnement Hallo:</span><span class="sxs-lookup"><span data-stu-id="2c499-137">Omitting hello resource group lists all zones in hello subscription:</span></span>

```azurecli
azure network dns zone list 
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="2c499-138">Bijwerken van een DNS-zone</span><span class="sxs-lookup"><span data-stu-id="2c499-138">Update a DNS zone</span></span>

<span data-ttu-id="2c499-139">Wijzigingen tooa DNS-zoneresource kan worden gemaakt met behulp van `azure network dns zone set`.</span><span class="sxs-lookup"><span data-stu-id="2c499-139">Changes tooa DNS zone resource can be made using `azure network dns zone set`.</span></span> <span data-ttu-id="2c499-140">Zie `azure network dns zone set -h` voor help.</span><span class="sxs-lookup"><span data-stu-id="2c499-140">For help, see `azure network dns zone set -h`.</span></span>

<span data-ttu-id="2c499-141">Met deze opdracht wordt niet Hallo DNS-recordsets binnen de zone Hallo bijgewerkt (Zie [hoe tooManage DNS-records](dns-operations-recordsets-cli-nodejs.md)).</span><span class="sxs-lookup"><span data-stu-id="2c499-141">This command does not update any of hello DNS record sets within hello zone (see [How tooManage DNS records](dns-operations-recordsets-cli-nodejs.md)).</span></span> <span data-ttu-id="2c499-142">Alleen gebruikte tooupdate eigenschappen van Hallo zoneresource zelf is.</span><span class="sxs-lookup"><span data-stu-id="2c499-142">It is only used tooupdate properties of hello zone resource itself.</span></span> <span data-ttu-id="2c499-143">Deze eigenschappen zijn momenteel beperkt toohello [Azure Resource Manager 'labels'](dns-zones-records.md#tags) voor Hallo zoneresource.</span><span class="sxs-lookup"><span data-stu-id="2c499-143">These properties are currently limited toohello [Azure Resource Manager 'tags'](dns-zones-records.md#tags) for hello zone resource.</span></span>

<span data-ttu-id="2c499-144">Hallo volgende voorbeeld ziet u hoe tooupdate Hallo codes op een DNS-zone.</span><span class="sxs-lookup"><span data-stu-id="2c499-144">hello following example shows how tooupdate hello tags on a DNS zone.</span></span> <span data-ttu-id="2c499-145">Hallo bestaande labels worden vervangen door Hallo waarde die is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="2c499-145">hello existing tags are replaced by hello value specified.</span></span>

```azurecli
azure network dns zone set MyResourceGroup contoso.com -t "team=support"
```

## <a name="delete-a-dns-zone"></a><span data-ttu-id="2c499-146">Een DNS-Zone verwijderen</span><span class="sxs-lookup"><span data-stu-id="2c499-146">Delete a DNS Zone</span></span>

<span data-ttu-id="2c499-147">DNS-zones worden verwijderd met een `azure network dns zone delete`.</span><span class="sxs-lookup"><span data-stu-id="2c499-147">DNS zones can be deleted using `azure network dns zone delete`.</span></span> <span data-ttu-id="2c499-148">Zie `azure network dns zone delete -h` voor help.</span><span class="sxs-lookup"><span data-stu-id="2c499-148">For help, see `azure network dns zone delete -h`.</span></span>

> [!NOTE]
> <span data-ttu-id="2c499-149">Een DNS-zone verwijderen, verwijdert tevens alle DNS-records in Hallo zone.</span><span class="sxs-lookup"><span data-stu-id="2c499-149">Deleting a DNS zone also deletes all DNS records within hello zone.</span></span> <span data-ttu-id="2c499-150">Deze bewerking kan niet ongedaan worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2c499-150">This operation cannot be undone.</span></span> <span data-ttu-id="2c499-151">Als Hallo DNS-zone gebruikt wordt, mislukt services met behulp van de zone Hallo wanneer Hallo zone wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="2c499-151">If hello DNS zone is in use, services using hello zone will fail when hello zone is deleted.</span></span>
>
><span data-ttu-id="2c499-152">tooprotect tegen het onbedoeld zone verwijderen, Zie [hoe tooprotect DNS-zones en registreert](dns-protect-zones-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="2c499-152">tooprotect against accidental zone deletion, see [How tooprotect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>

<span data-ttu-id="2c499-153">Met deze opdracht vraagt om bevestiging.</span><span class="sxs-lookup"><span data-stu-id="2c499-153">This command prompts for confirmation.</span></span> <span data-ttu-id="2c499-154">Hallo optionele `--quiet` gaan (korte versie `-q`) deze prompt onderdrukt.</span><span class="sxs-lookup"><span data-stu-id="2c499-154">hello optional `--quiet` switch (short form `-q`) suppresses this prompt.</span></span>

<span data-ttu-id="2c499-155">Hallo volgende voorbeeld laat zien hoe toodelete zone Hallo *contoso.com* uit resourcegroep *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="2c499-155">hello following example shows how toodelete hello zone *contoso.com* from resource group *MyResourceGroup*.</span></span>

```azurecli
azure network dns zone delete MyResourceGroup contoso.com
```

## <a name="next-steps"></a><span data-ttu-id="2c499-156">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2c499-156">Next steps</span></span>

<span data-ttu-id="2c499-157">Meer informatie over hoe te[beheren recordsets en records](dns-getstarted-create-recordset-cli-nodejs.md) in uw DNS-zone.</span><span class="sxs-lookup"><span data-stu-id="2c499-157">Learn how too[manage record sets and records](dns-getstarted-create-recordset-cli-nodejs.md) in your DNS zone.</span></span>

<span data-ttu-id="2c499-158">Meer informatie over hoe te[delegeren van uw domein tooAzure DNS-](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="2c499-158">Learn how too[delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>

