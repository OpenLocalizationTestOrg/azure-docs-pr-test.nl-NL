---
title: aaaGet de slag met Azure DNS met behulp van PowerShell | Microsoft Docs
description: Meer informatie over hoe toocreate een DNS-zone en een record in Azure DNS. Dit is een stapsgewijze handleiding toocreate en beheren van uw eerste DNS-zone en vastleggen met behulp van PowerShell.
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
ms.openlocfilehash: 0f9dead1e4b44fcc74c84a024c41cdfaeb02b5d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-powershell"></a><span data-ttu-id="8c766-104">Aan de slag met Azure DNS met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="8c766-104">Get Started with Azure DNS using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8c766-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="8c766-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="8c766-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8c766-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="8c766-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="8c766-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="8c766-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8c766-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="8c766-109">Dit artikel begeleidt u bij Hallo stappen toocreate, uw eerste DNS-zone en een record met behulp van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8c766-109">This article walks you through hello steps toocreate your first DNS zone and record using Azure PowerShell.</span></span> <span data-ttu-id="8c766-110">U kunt ook u deze stappen uitvoert met behulp van hello Azure-portal of Hallo platformoverschrijdende Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="8c766-110">You can also perform these steps using hello Azure portal or hello cross-platform Azure CLI.</span></span>

<span data-ttu-id="8c766-111">Een DNS-zone is gebruikte toohost Hallo DNS-records voor een bepaald domein.</span><span class="sxs-lookup"><span data-stu-id="8c766-111">A DNS zone is used toohost hello DNS records for a particular domain.</span></span> <span data-ttu-id="8c766-112">toostart die als host fungeert voor uw domein in Azure DNS, moet u een DNS-zone toocreate voor die domeinnaam.</span><span class="sxs-lookup"><span data-stu-id="8c766-112">toostart hosting your domain in Azure DNS, you need toocreate a DNS zone for that domain name.</span></span> <span data-ttu-id="8c766-113">Alle DNS-records voor uw domein worden vervolgens gemaakt binnen deze DNS-zone.</span><span class="sxs-lookup"><span data-stu-id="8c766-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="8c766-114">Ten slotte toopublish uw DNS-zone-toohello Internet, moet u tooconfigure Hallo-naamservers voor Hallo-domein.</span><span class="sxs-lookup"><span data-stu-id="8c766-114">Finally, toopublish your DNS zone toohello Internet, you need tooconfigure hello name servers for hello domain.</span></span> <span data-ttu-id="8c766-115">Deze stappen worden hieronder allemaal beschreven.</span><span class="sxs-lookup"><span data-stu-id="8c766-115">Each of these steps is described below.</span></span>

<span data-ttu-id="8c766-116">Deze instructies wordt ervan uitgegaan dat u al hebt geïnstalleerd en tooAzure PowerShell aangemeld.</span><span class="sxs-lookup"><span data-stu-id="8c766-116">These instructions assume you have already installed and signed in tooAzure PowerShell.</span></span> <span data-ttu-id="8c766-117">Zie voor informatie over [hoe toomanage DNS zones met behulp van PowerShell](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="8c766-117">For help, see [How toomanage DNS zones using PowerShell](dns-operations-dnszones.md).</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="8c766-118">Hallo resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="8c766-118">Create hello resource group</span></span>

<span data-ttu-id="8c766-119">Voordat u Hallo DNS-zone maakt, wordt een resourcegroep toocontain Hallo DNS-Zone gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8c766-119">Before creating hello DNS zone, a resource group is created toocontain hello DNS Zone.</span></span> <span data-ttu-id="8c766-120">Hallo hieronder vindt u Hallo-opdracht.</span><span class="sxs-lookup"><span data-stu-id="8c766-120">hello following shows hello command.</span></span>

```powershell
New-AzureRMResourceGroup -name MyResourceGroup -location "westus"
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="8c766-121">Een DNS-zone maken</span><span class="sxs-lookup"><span data-stu-id="8c766-121">Create a DNS zone</span></span>

<span data-ttu-id="8c766-122">Een DNS-zone wordt gemaakt met behulp van Hallo `New-AzureRmDnsZone` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8c766-122">A DNS zone is created by using hello `New-AzureRmDnsZone` cmdlet.</span></span> <span data-ttu-id="8c766-123">Hallo volgende voorbeeld maakt u een DNS-zone aangeroepen *contoso.com* in de resourcegroep Hallo aangeroepen *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="8c766-123">hello following example creates a DNS zone called *contoso.com* in hello resource group called *MyResourceGroup*.</span></span> <span data-ttu-id="8c766-124">Hallo voorbeeld toocreate een DNS-zone, vervangen door Hallo waarden voor uw eigen gebruik.</span><span class="sxs-lookup"><span data-stu-id="8c766-124">Use hello example toocreate a DNS zone, substituting hello values for your own.</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyResourceGroup
```

## <a name="create-a-dns-record"></a><span data-ttu-id="8c766-125">Een DNS-record maken</span><span class="sxs-lookup"><span data-stu-id="8c766-125">Create a DNS record</span></span>

<span data-ttu-id="8c766-126">U recordsets maakt met behulp van Hallo `New-AzureRmDnsRecordSet` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8c766-126">You create record sets by using hello `New-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="8c766-127">Hallo volgende voorbeeld wordt een record met Hallo relatieve naam 'www' in de DNS-Zone 'contoso.com' in de resourcegroep 'MyResourceGroup' Hallo.</span><span class="sxs-lookup"><span data-stu-id="8c766-127">hello following example creates a record with hello relative name "www" in hello DNS Zone "contoso.com", in resource group "MyResourceGroup".</span></span> <span data-ttu-id="8c766-128">Hallo volledig gekwalificeerde naam van de recordset Hallo is 'www.contoso.com'.</span><span class="sxs-lookup"><span data-stu-id="8c766-128">hello fully-qualified name of hello record set is "www.contoso.com".</span></span> <span data-ttu-id="8c766-129">Hallo-recordtype is "A", met IP-adres '1.2.3.4' en Hallo TTL 3600 seconden is.</span><span class="sxs-lookup"><span data-stu-id="8c766-129">hello record type is "A", with IP address "1.2.3.4", and hello TTL is 3600 seconds.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName contoso.com -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4")
```

<span data-ttu-id="8c766-130">Voor andere recordtypen voor recordsets met meer dan een record en bestaande records toomodify, Zie [beheren DNS-records en recordsets met Azure PowerShell](dns-operations-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="8c766-130">For other record types, for record sets with more than one record, and toomodify existing records, see [Manage DNS records and record sets using Azure PowerShell](dns-operations-recordsets.md).</span></span> 


## <a name="view-records"></a><span data-ttu-id="8c766-131">Records weergeven</span><span class="sxs-lookup"><span data-stu-id="8c766-131">View records</span></span>

<span data-ttu-id="8c766-132">toolist hello DNS-records in de zone gebruiken:</span><span class="sxs-lookup"><span data-stu-id="8c766-132">toolist hello DNS records in your zone, use:</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName contoso.com -ResourceGroupName MyResourceGroup
```


## <a name="update-name-servers"></a><span data-ttu-id="8c766-133">Naamservers bijwerken</span><span class="sxs-lookup"><span data-stu-id="8c766-133">Update name servers</span></span>

<span data-ttu-id="8c766-134">Wanneer u zich ervan overtuigd dat uw DNS-zone en records hebben is ingesteld, moet u tooconfigure uw domeinnaam toouse hello Azure DNS-naamservers.</span><span class="sxs-lookup"><span data-stu-id="8c766-134">Once you are satisfied that your DNS zone and records have been set up correctly, you need tooconfigure your domain name toouse hello Azure DNS name servers.</span></span> <span data-ttu-id="8c766-135">Hierdoor kunnen andere gebruikers op Hallo Internet toofind de DNS-records.</span><span class="sxs-lookup"><span data-stu-id="8c766-135">This enables other users on hello Internet toofind your DNS records.</span></span>

<span data-ttu-id="8c766-136">Hallo-naamservers voor uw zone worden gegeven voor Hallo `Get-AzureRmDnsZone` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="8c766-136">hello name servers for your zone are given by hello `Get-AzureRmDnsZone` cmdlet:</span></span>

```powershell
Get-AzureRmDnsZone -ZoneName contoso.com -ResourceGroupName MyResourceGroup

Name                  : contoso.com
ResourceGroupName     : myresourcegroup
Etag                  : 00000003-0000-0000-b40d-0996b97ed101
Tags                  : {}
NameServers           : {ns1-01.azure-dns.com., ns2-01.azure-dns.net., ns3-01.azure-dns.org., ns4-01.azure-dns.info.}
NumberOfRecordSets    : 3
MaxNumberOfRecordSets : 5000
```

<span data-ttu-id="8c766-137">Deze naamservers moeten worden geconfigureerd met Hallo domeinnaamregistrar (waarbij u hebt aangeschaft Hallo-domeinnaam).</span><span class="sxs-lookup"><span data-stu-id="8c766-137">These name servers should be configured with hello domain name registrar (where you purchased hello domain name).</span></span> <span data-ttu-id="8c766-138">Uw registrar bieden Hallo optie tooset up Hallo naamservers voor Hallo-domein.</span><span class="sxs-lookup"><span data-stu-id="8c766-138">Your registrar will offer hello option tooset up hello name servers for hello domain.</span></span> <span data-ttu-id="8c766-139">Zie voor meer informatie [delegeren van uw domein tooAzure DNS-](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="8c766-139">For more information, see [Delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="8c766-140">Alle resources verwijderen</span><span class="sxs-lookup"><span data-stu-id="8c766-140">Delete all resources</span></span>

<span data-ttu-id="8c766-141">toodelete alle resources die worden gemaakt in dit artikel nemen Hallo stap:</span><span class="sxs-lookup"><span data-stu-id="8c766-141">toodelete all resources created in this article, take hello following step:</span></span>

```powershell
Remove-AzureRMResourceGroup -Name MyResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="8c766-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8c766-142">Next steps</span></span>

<span data-ttu-id="8c766-143">Zie toolearn meer informatie over Azure DNS [Azure DNS-overzicht](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8c766-143">toolearn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="8c766-144">Zie toolearn meer informatie over het beheren van DNS-zones in Azure DNS [beheren DNS-zones in Azure DNS met behulp van PowerShell](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="8c766-144">toolearn more about managing DNS zones in Azure DNS, see [Manage DNS zones in Azure DNS using PowerShell](dns-operations-dnszones.md).</span></span>

<span data-ttu-id="8c766-145">Zie toolearn meer informatie over het beheren van DNS-records in Azure DNS [beheren DNS-records en -recordsets stelt u in Azure DNS met behulp van PowerShell](dns-operations-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="8c766-145">toolearn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets in Azure DNS using PowerShell](dns-operations-recordsets.md).</span></span>

