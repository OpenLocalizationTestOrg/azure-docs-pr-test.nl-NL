---
title: Aan de slag met Azure DNS met behulp van Azure CLI 1.0 | Microsoft Docs
description: Informatie over het maken van een DNS-zone en -record in Azure DNS. Dit is een stapsgewijze handleiding voor het maken en beheren van uw eerste DNS-zone en -record met behulp van de Azure CLI 1.0.
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: f7943b71bbd16c36df09436973d92539eb62b210
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-dns-using-azure-cli-10"></a><span data-ttu-id="90304-104">Aan de slag met Azure DNS met behulp van Azure-CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="90304-104">Get started with Azure DNS using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="90304-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="90304-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="90304-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="90304-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="90304-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="90304-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="90304-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="90304-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="90304-109">Dit artikel begeleidt u stapsgewijs door de procedure voor het maken van uw eerste DNS-zone en -record met behulp van de platformoverschrijdende Azure-CLI 1.0 die beschikbaar is voor Windows, Mac en Linux.</span><span class="sxs-lookup"><span data-stu-id="90304-109">This article walks you through the steps to create your first DNS zone and record using the cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="90304-110">U kunt deze stappen ook uitvoeren met de Azure-portal of Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="90304-110">You can also perform these steps using the Azure portal or Azure PowerShell.</span></span>

<span data-ttu-id="90304-111">Een DNS-zone wordt gebruikt om de DNS-records voor een bepaald domein te hosten.</span><span class="sxs-lookup"><span data-stu-id="90304-111">A DNS zone is used to host the DNS records for a particular domain.</span></span> <span data-ttu-id="90304-112">Als u uw domein wilt hosten in Azure DNS, moet u een DNS-zone maken voor die domeinnaam.</span><span class="sxs-lookup"><span data-stu-id="90304-112">To start hosting your domain in Azure DNS, you need to create a DNS zone for that domain name.</span></span> <span data-ttu-id="90304-113">Alle DNS-records voor uw domein worden vervolgens gemaakt binnen deze DNS-zone.</span><span class="sxs-lookup"><span data-stu-id="90304-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="90304-114">Tot slot moet u de naamservers voor het domein configureren om de DNS-zone te publiceren naar internet.</span><span class="sxs-lookup"><span data-stu-id="90304-114">Finally, to publish your DNS zone to the Internet, you need to configure the name servers for the domain.</span></span> <span data-ttu-id="90304-115">Deze stappen worden hieronder allemaal beschreven.</span><span class="sxs-lookup"><span data-stu-id="90304-115">Each of these steps is described below.</span></span>

<span data-ttu-id="90304-116">Bij deze instructies wordt ervan uitgegaan dat u Azure CLI 1.0 al hebt geïnstalleerd en bent aangemeld.</span><span class="sxs-lookup"><span data-stu-id="90304-116">These instructions assume you have already installed and signed in to Azure CLI 1.0.</span></span> <span data-ttu-id="90304-117">Zie [How to manage DNS zones using Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) (DNS-zones beheren met behulp van Azure CLI 1.0) voor hulp.</span><span class="sxs-lookup"><span data-stu-id="90304-117">For help, see [How to manage DNS zones using Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="90304-118">De resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="90304-118">Create the resource group</span></span>

<span data-ttu-id="90304-119">Voordat u de DNS-zone maakt, wordt er een resourcegroep gemaakt waartoe de DNS-zone gaat behoren.</span><span class="sxs-lookup"><span data-stu-id="90304-119">Before creating the DNS zone, a resource group is created to contain the DNS Zone.</span></span> <span data-ttu-id="90304-120">Hieronder ziet u de opdracht.</span><span class="sxs-lookup"><span data-stu-id="90304-120">The following shows the command.</span></span>

```azurecli
azure group create --name MyResourceGroup --location "West US"
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="90304-121">Een DNS-zone maken</span><span class="sxs-lookup"><span data-stu-id="90304-121">Create a DNS zone</span></span>

<span data-ttu-id="90304-122">Een DNS-zone wordt gemaakt met de opdracht `azure network dns zone create`.</span><span class="sxs-lookup"><span data-stu-id="90304-122">A DNS zone is created using the `azure network dns zone create` command.</span></span> <span data-ttu-id="90304-123">Typ `azure network dns zone create -h` om Help weer te geven voor deze opdracht.</span><span class="sxs-lookup"><span data-stu-id="90304-123">To see help for this command, type `azure network dns zone create -h`.</span></span>

<span data-ttu-id="90304-124">In het volgende voorbeeld maakt u een DNS-zone met de naam *contoso.com* in de resourcegroep *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="90304-124">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*.</span></span> <span data-ttu-id="90304-125">Gebruik het voorbeeld om een DNS-zone te maken door de waarden te vervangen door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="90304-125">Use the example to create a DNS zone, substituting the values for your own.</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```


## <a name="create-a-dns-record"></a><span data-ttu-id="90304-126">Een DNS-record maken</span><span class="sxs-lookup"><span data-stu-id="90304-126">Create a DNS record</span></span>

<span data-ttu-id="90304-127">Gebruik de opdracht `azure network dns record-set add-record` om een DNS-record te maken.</span><span class="sxs-lookup"><span data-stu-id="90304-127">To create a DNS record, use the `azure network dns record-set add-record` command.</span></span> <span data-ttu-id="90304-128">Zie `azure network dns record-set add-record -h` voor help.</span><span class="sxs-lookup"><span data-stu-id="90304-128">For help, see `azure network dns record-set add-record -h`.</span></span>

<span data-ttu-id="90304-129">In het volgende voorbeeld maakt u een record met de relatieve naam 'www' in de DNS-zone 'contoso.com' in de resourcegroep 'MyResourceGroup'.</span><span class="sxs-lookup"><span data-stu-id="90304-129">The following example creates a record with the relative name "www" in the DNS Zone "contoso.com", in resource group "MyResourceGroup".</span></span> <span data-ttu-id="90304-130">De volledig gekwalificeerde naam van de recordset is 'www.contoso.com'.</span><span class="sxs-lookup"><span data-stu-id="90304-130">The fully-qualified name of the record set is "www.contoso.com".</span></span> <span data-ttu-id="90304-131">Het recordtype is 'A', met IP-adres '1.2.3.4' en een standaard-TTL van 3600 seconden (1 uur).</span><span class="sxs-lookup"><span data-stu-id="90304-131">The record type is "A", with IP address "1.2.3.4", and a default TTL of 3600 seconds (1 hour) is used.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

<span data-ttu-id="90304-132">Voor andere recordtypen, voor recordsets met meerdere records, voor andere TTL-waarden, en als u bestaande records wilt wijzigen, raadpleegt u [Manage DNS records and record sets using Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) (DNS-records en -recordsets beheren met behulp van Azure CLI 1.0).</span><span class="sxs-lookup"><span data-stu-id="90304-132">For other record types, for record sets with more than one record, for alternative TTL values, and to modify existing records, see [Manage DNS records and record sets using the Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).</span></span>


## <a name="view-records"></a><span data-ttu-id="90304-133">Records weergeven</span><span class="sxs-lookup"><span data-stu-id="90304-133">View records</span></span>

<span data-ttu-id="90304-134">Als u de DNS-records wilt weergeven in uw zone, gebruikt u:</span><span class="sxs-lookup"><span data-stu-id="90304-134">To list the DNS records in your zone, use:</span></span>

```azurecli
azure network dns record-set list MyResourceGroup contoso.com
```


## <a name="update-name-servers"></a><span data-ttu-id="90304-135">Naamservers bijwerken</span><span class="sxs-lookup"><span data-stu-id="90304-135">Update name servers</span></span>

<span data-ttu-id="90304-136">Wanneer uw DNS-zone en -records correct zijn ingesteld, moet u uw domeinnaam configureren voor het gebruik van de Azure DNS-naamservers .</span><span class="sxs-lookup"><span data-stu-id="90304-136">Once you are satisfied that your DNS zone and records have been set up correctly, you need to configure your domain name to use the Azure DNS name servers.</span></span> <span data-ttu-id="90304-137">Op die manier kunnen andere gebruikers op internet uw DNS-records vinden.</span><span class="sxs-lookup"><span data-stu-id="90304-137">This enables other users on the Internet to find your DNS records.</span></span>

<span data-ttu-id="90304-138">De naamservers voor uw zone zijn gegeven door de opdracht `azure network dns zone show`:</span><span class="sxs-lookup"><span data-stu-id="90304-138">The name servers for your zone are given by the `azure network dns zone show` command:</span></span>

```azurecli
azure network dns zone show MyResourceGroup contoso.com

info:    Executing command network dns zone show
+ Looking up the dns zone "contoso.com"
data:    Id                              : /subscriptions/a385a691-bd93-41b0-8084-8213ebc5bff7/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com
data:    Name                            : contoso.com
data:    Type                            : Microsoft.Network/dnszones
data:    Location                        : global
data:    Number of record sets           : 3
data:    Max number of record sets       : 5000
data:    Name servers:
data:        ns1-01.azure-dns.com.
data:        ns2-01.azure-dns.net.
data:        ns3-01.azure-dns.org.
data:        ns4-01.azure-dns.info.
data:    Tags                            :
info:    network dns zone show command OK
```

<span data-ttu-id="90304-139">Deze naamservers moeten worden geconfigureerd met de domeinnaamregistrar (waar u de domeinnaam hebt gekocht).</span><span class="sxs-lookup"><span data-stu-id="90304-139">These name servers should be configured with the domain name registrar (where you purchased the domain name).</span></span> <span data-ttu-id="90304-140">Uw registrar zal u de mogelijkheid bieden om de naamservers voor het domein in te stellen.</span><span class="sxs-lookup"><span data-stu-id="90304-140">Your registrar will offer the option to set up the name servers for the domain.</span></span> <span data-ttu-id="90304-141">Zie [Uw domein delegeren naar Azure DNS](dns-domain-delegation.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="90304-141">For more information, see [Delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="90304-142">Alle resources verwijderen</span><span class="sxs-lookup"><span data-stu-id="90304-142">Delete all resources</span></span>
 
<span data-ttu-id="90304-143">Als u alle resources wilt verwijderen die u in dit artikel hebt gemaakt, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="90304-143">To delete all resources created in this article, take the following step:</span></span>

```azurecli
azure group delete --name MyResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="90304-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="90304-144">Next steps</span></span>

<span data-ttu-id="90304-145">Zie [Azure DNS Overview](dns-overview.md) (Overzicht van Azure DNS) voor meer informatie over Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="90304-145">To learn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="90304-146">Zie [Manage DNS zones in Azure DNS using Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) (DNS-zones in Azure DNS beheren met behulp van Azure CLI 1.0) voor meer informatie over het beheren van DNS-zones in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="90304-146">To learn more about managing DNS zones in Azure DNS, see [Manage DNS zones in Azure DNS using Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).</span></span>

<span data-ttu-id="90304-147">Zie [Manage DNS records and record sets in Azure DNS using Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) (DNS-records en -recordsets in Azure DNS beheren met behulp van Azure CLI 1.0) voor meer informatie over het beheren van DNS-records in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="90304-147">To learn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets in Azure DNS using Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).</span></span>

