---
title: aaaGet de slag met Azure DNS met Azure CLI 2.0 | Microsoft Docs
description: Meer informatie over hoe toocreate een DNS-zone en een record in Azure DNS. Dit is een stapsgewijze handleiding toocreate en beheren van uw eerste DNS-zone en een record met behulp van hello Azure CLI 2.0.
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: 8a894941e9910d5cc35394a1be9dbca9792613f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-azure-cli-20"></a><span data-ttu-id="55ba7-104">Aan de slag met Azure DNS met behulp van Azure-CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="55ba7-104">Get started with Azure DNS using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="55ba7-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="55ba7-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="55ba7-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="55ba7-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="55ba7-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="55ba7-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="55ba7-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="55ba7-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="55ba7-109">Dit artikel begeleidt u bij Hallo stappen toocreate uw eerste DNS-zone en platformoverschrijdende Azure CLI 2.0, met behulp van record Hallo die beschikbaar is voor Windows, Mac en Linux.</span><span class="sxs-lookup"><span data-stu-id="55ba7-109">This article walks you through hello steps toocreate your first DNS zone and record using hello cross-platform Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="55ba7-110">U kunt deze stappen met hello Azure-portal of Azure PowerShell ook uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="55ba7-110">You can also perform these steps using hello Azure portal or Azure PowerShell.</span></span>

<span data-ttu-id="55ba7-111">Een DNS-zone is gebruikte toohost Hallo DNS-records voor een bepaald domein.</span><span class="sxs-lookup"><span data-stu-id="55ba7-111">A DNS zone is used toohost hello DNS records for a particular domain.</span></span> <span data-ttu-id="55ba7-112">toostart die als host fungeert voor uw domein in Azure DNS, moet u een DNS-zone toocreate voor die domeinnaam.</span><span class="sxs-lookup"><span data-stu-id="55ba7-112">toostart hosting your domain in Azure DNS, you need toocreate a DNS zone for that domain name.</span></span> <span data-ttu-id="55ba7-113">Alle DNS-records voor uw domein worden vervolgens gemaakt binnen deze DNS-zone.</span><span class="sxs-lookup"><span data-stu-id="55ba7-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="55ba7-114">Ten slotte toopublish uw DNS-zone-toohello Internet, moet u tooconfigure Hallo-naamservers voor Hallo-domein.</span><span class="sxs-lookup"><span data-stu-id="55ba7-114">Finally, toopublish your DNS zone toohello Internet, you need tooconfigure hello name servers for hello domain.</span></span> <span data-ttu-id="55ba7-115">Deze stappen worden hieronder allemaal beschreven.</span><span class="sxs-lookup"><span data-stu-id="55ba7-115">Each of these steps is described below.</span></span>

<span data-ttu-id="55ba7-116">Deze instructies wordt ervan uitgegaan dat u al hebt geïnstalleerd en aangemeld tooAzure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="55ba7-116">These instructions assume you have already installed and signed in tooAzure CLI 2.0.</span></span> <span data-ttu-id="55ba7-117">Zie voor informatie over [hoe toomanage DNS zones met Azure CLI 2.0](dns-operations-dnszones-cli.md).</span><span class="sxs-lookup"><span data-stu-id="55ba7-117">For help, see [How toomanage DNS zones using Azure CLI 2.0](dns-operations-dnszones-cli.md).</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="55ba7-118">Hallo resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="55ba7-118">Create hello resource group</span></span>

<span data-ttu-id="55ba7-119">Voordat u Hallo DNS-zone maakt, wordt een resourcegroep toocontain Hallo DNS-Zone gemaakt.</span><span class="sxs-lookup"><span data-stu-id="55ba7-119">Before creating hello DNS zone, a resource group is created toocontain hello DNS Zone.</span></span> <span data-ttu-id="55ba7-120">Hallo hieronder vindt u Hallo-opdracht.</span><span class="sxs-lookup"><span data-stu-id="55ba7-120">hello following shows hello command.</span></span>

```azurecli
az group create --name MyResourceGroup --location "West US"
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="55ba7-121">Een DNS-zone maken</span><span class="sxs-lookup"><span data-stu-id="55ba7-121">Create a DNS zone</span></span>

<span data-ttu-id="55ba7-122">Een DNS-zone wordt gemaakt met Hallo `az network dns zone create` opdracht.</span><span class="sxs-lookup"><span data-stu-id="55ba7-122">A DNS zone is created using hello `az network dns zone create` command.</span></span> <span data-ttu-id="55ba7-123">help voor deze opdracht toosee plaatst `az network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="55ba7-123">toosee help for this command, type `az network dns zone create -h`.</span></span>

<span data-ttu-id="55ba7-124">Hallo volgende voorbeeld maakt u een DNS-zone aangeroepen *contoso.com* in de resourcegroep Hallo *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="55ba7-124">hello following example creates a DNS zone called *contoso.com* in hello resource group *MyResourceGroup*.</span></span> <span data-ttu-id="55ba7-125">Hallo voorbeeld toocreate een DNS-zone, vervangen door Hallo waarden voor uw eigen gebruik.</span><span class="sxs-lookup"><span data-stu-id="55ba7-125">Use hello example toocreate a DNS zone, substituting hello values for your own.</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n contoso.com
```


## <a name="create-a-dns-record"></a><span data-ttu-id="55ba7-126">Een DNS-record maken</span><span class="sxs-lookup"><span data-stu-id="55ba7-126">Create a DNS record</span></span>

<span data-ttu-id="55ba7-127">toocreate een DNS-record gebruiken Hallo `az network dns record-set [record type] add-record` opdracht.</span><span class="sxs-lookup"><span data-stu-id="55ba7-127">toocreate a DNS record, use hello `az network dns record-set [record type] add-record` command.</span></span> <span data-ttu-id="55ba7-128">Voor hulp, bijvoorbeeld voor A-records, raadpleegt u `azure network dns record-set A add-record -h`.</span><span class="sxs-lookup"><span data-stu-id="55ba7-128">For help, for A records for example, see `azure network dns record-set A add-record -h`.</span></span>

<span data-ttu-id="55ba7-129">Hallo volgende voorbeeld wordt een record met Hallo relatieve naam 'www' in de DNS-Zone 'contoso.com' in de resourcegroep 'MyResourceGroup' Hallo.</span><span class="sxs-lookup"><span data-stu-id="55ba7-129">hello following example creates a record with hello relative name "www" in hello DNS Zone "contoso.com", in resource group "MyResourceGroup".</span></span> <span data-ttu-id="55ba7-130">Hallo volledig gekwalificeerde naam van de recordset Hallo is 'www.contoso.com'.</span><span class="sxs-lookup"><span data-stu-id="55ba7-130">hello fully-qualified name of hello record set is "www.contoso.com".</span></span> <span data-ttu-id="55ba7-131">Hallo-recordtype is "A", met IP-adres '1.2.3.4' en een standaard-TTL van 3600 seconden (1 uur) wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="55ba7-131">hello record type is "A", with IP address "1.2.3.4", and a default TTL of 3600 seconds (1 hour) is used.</span></span>

```azurecli
az network dns record-set a add-record -g MyResourceGroup -z contoso.com -n www -a 1.2.3.4
```

<span data-ttu-id="55ba7-132">Voor andere recordtypen voor recordsets met meer dan één record, voor alternatieve TTL waarden en toomodify bestaande records, Zie [beheren DNS-records en recordsets met behulp van Azure CLI 2.0 Hallo](dns-operations-recordsets-cli.md).</span><span class="sxs-lookup"><span data-stu-id="55ba7-132">For other record types, for record sets with more than one record, for alternative TTL values, and toomodify existing records, see [Manage DNS records and record sets using hello Azure CLI 2.0](dns-operations-recordsets-cli.md).</span></span>


## <a name="view-records"></a><span data-ttu-id="55ba7-133">Records weergeven</span><span class="sxs-lookup"><span data-stu-id="55ba7-133">View records</span></span>

<span data-ttu-id="55ba7-134">toolist hello DNS-records in de zone gebruiken:</span><span class="sxs-lookup"><span data-stu-id="55ba7-134">toolist hello DNS records in your zone, use:</span></span>

```azurecli
az network dns record-set list -g MyResourceGroup -z contoso.com
```


## <a name="update-name-servers"></a><span data-ttu-id="55ba7-135">Naamservers bijwerken</span><span class="sxs-lookup"><span data-stu-id="55ba7-135">Update name servers</span></span>

<span data-ttu-id="55ba7-136">Wanneer u zich ervan overtuigd dat uw DNS-zone en records hebben is ingesteld, moet u tooconfigure uw domeinnaam toouse hello Azure DNS-naamservers.</span><span class="sxs-lookup"><span data-stu-id="55ba7-136">Once you are satisfied that your DNS zone and records have been set up correctly, you need tooconfigure your domain name toouse hello Azure DNS name servers.</span></span> <span data-ttu-id="55ba7-137">Hierdoor kunnen andere gebruikers op Hallo Internet toofind de DNS-records.</span><span class="sxs-lookup"><span data-stu-id="55ba7-137">This enables other users on hello Internet toofind your DNS records.</span></span>

<span data-ttu-id="55ba7-138">Hallo-naamservers voor uw zone worden gegeven voor Hallo `az network dns zone show` opdracht.</span><span class="sxs-lookup"><span data-stu-id="55ba7-138">hello name servers for your zone are given by hello `az network dns zone show` command.</span></span> <span data-ttu-id="55ba7-139">toosee hello naamservernamen, gebruik JSON-uitvoer, zoals getoond in Hallo voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="55ba7-139">toosee hello name server names, use JSON output, as shown in hello following example.</span></span>

```azurecli
az network dns zone show -g MyResourceGroup -n contoso.com -o json

{
  "etag": "00000003-0000-0000-b40d-0996b97ed101",
  "id": "/subscriptions/a385a691-bd93-41b0-8084-8213ebc5bff7/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "contoso.com",
  "nameServers": [
    "ns1-01.azure-dns.com.",
    "ns2-01.azure-dns.net.",
    "ns3-01.azure-dns.org.",
    "ns4-01.azure-dns.info."
  ],
  "numberOfRecordSets": 3,
  "resourceGroup": "myresourcegroup",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

<span data-ttu-id="55ba7-140">Deze naamservers moeten worden geconfigureerd met Hallo domeinnaamregistrar (waarbij u hebt aangeschaft Hallo-domeinnaam).</span><span class="sxs-lookup"><span data-stu-id="55ba7-140">These name servers should be configured with hello domain name registrar (where you purchased hello domain name).</span></span> <span data-ttu-id="55ba7-141">Uw registrar bieden Hallo optie tooset up Hallo naamservers voor Hallo-domein.</span><span class="sxs-lookup"><span data-stu-id="55ba7-141">Your registrar will offer hello option tooset up hello name servers for hello domain.</span></span> <span data-ttu-id="55ba7-142">Zie voor meer informatie [delegeren van uw domein tooAzure DNS-](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="55ba7-142">For more information, see [Delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="55ba7-143">Alle resources verwijderen</span><span class="sxs-lookup"><span data-stu-id="55ba7-143">Delete all resources</span></span>
 
<span data-ttu-id="55ba7-144">toodelete alle resources die worden gemaakt in dit artikel nemen Hallo stap:</span><span class="sxs-lookup"><span data-stu-id="55ba7-144">toodelete all resources created in this article, take hello following step:</span></span>

```azurecli
az group delete --name MyResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="55ba7-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="55ba7-145">Next steps</span></span>

<span data-ttu-id="55ba7-146">Zie toolearn meer informatie over Azure DNS [Azure DNS-overzicht](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="55ba7-146">toolearn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="55ba7-147">Zie toolearn meer informatie over het beheren van DNS-zones in Azure DNS [beheren DNS-zones in Azure DNS met Azure CLI 2.0](dns-operations-dnszones-cli.md).</span><span class="sxs-lookup"><span data-stu-id="55ba7-147">toolearn more about managing DNS zones in Azure DNS, see [Manage DNS zones in Azure DNS using Azure CLI 2.0](dns-operations-dnszones-cli.md).</span></span>

<span data-ttu-id="55ba7-148">Zie toolearn meer informatie over het beheren van DNS-records in Azure DNS [beheren DNS-records en -recordsets stelt u in Azure DNS met Azure CLI 2.0](dns-operations-recordsets-cli.md).</span><span class="sxs-lookup"><span data-stu-id="55ba7-148">toolearn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets in Azure DNS using Azure CLI 2.0](dns-operations-recordsets-cli.md).</span></span>
