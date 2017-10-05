---
title: Aan de slag met Azure DNS met behulp van PowerShell | Microsoft Docs
description: Informatie over het maken van een DNS-zone en -record in Azure DNS. Dit is een stapsgewijze handleiding voor het maken en beheren van uw eerste DNS-zone en -record met behulp van PowerShell.
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
ms.openlocfilehash: 48f7ba325f61b4a91c0208b4c99058da801bee19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-dns-using-powershell"></a><span data-ttu-id="89e54-104">Aan de slag met Azure DNS met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="89e54-104">Get Started with Azure DNS using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="89e54-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="89e54-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="89e54-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="89e54-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="89e54-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="89e54-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="89e54-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="89e54-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="89e54-109">Dit artikel leidt u stapsgewijs door de procedure voor het maken van uw eerste DNS-zone en -record met behulp van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="89e54-109">This article walks you through the steps to create your first DNS zone and record using Azure PowerShell.</span></span> <span data-ttu-id="89e54-110">U kunt deze stappen ook uitvoeren met de Azure-portal of de platformoverschrijdende Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="89e54-110">You can also perform these steps using the Azure portal or the cross-platform Azure CLI.</span></span>

<span data-ttu-id="89e54-111">Een DNS-zone wordt gebruikt om de DNS-records voor een bepaald domein te hosten.</span><span class="sxs-lookup"><span data-stu-id="89e54-111">A DNS zone is used to host the DNS records for a particular domain.</span></span> <span data-ttu-id="89e54-112">Als u uw domein wilt hosten in Azure DNS, moet u een DNS-zone maken voor die domeinnaam.</span><span class="sxs-lookup"><span data-stu-id="89e54-112">To start hosting your domain in Azure DNS, you need to create a DNS zone for that domain name.</span></span> <span data-ttu-id="89e54-113">Alle DNS-records voor uw domein worden vervolgens gemaakt binnen deze DNS-zone.</span><span class="sxs-lookup"><span data-stu-id="89e54-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="89e54-114">Tot slot moet u de naamservers voor het domein configureren om de DNS-zone te publiceren naar internet.</span><span class="sxs-lookup"><span data-stu-id="89e54-114">Finally, to publish your DNS zone to the Internet, you need to configure the name servers for the domain.</span></span> <span data-ttu-id="89e54-115">Deze stappen worden hieronder allemaal beschreven.</span><span class="sxs-lookup"><span data-stu-id="89e54-115">Each of these steps is described below.</span></span>

<span data-ttu-id="89e54-116">Bij deze instructies wordt ervan uitgegaan dat u Azure PowerShell al hebt geïnstalleerd en bent aangemeld.</span><span class="sxs-lookup"><span data-stu-id="89e54-116">These instructions assume you have already installed and signed in to Azure PowerShell.</span></span> <span data-ttu-id="89e54-117">Zie [How to manage DNS zones using PowerShell](dns-operations-dnszones.md) (DNS-zones beheren met behulp van PowerShell) voor hulp.</span><span class="sxs-lookup"><span data-stu-id="89e54-117">For help, see [How to manage DNS zones using PowerShell](dns-operations-dnszones.md).</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="89e54-118">De resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="89e54-118">Create the resource group</span></span>

<span data-ttu-id="89e54-119">Voordat u de DNS-zone maakt, wordt er een resourcegroep gemaakt waartoe de DNS-zone gaat behoren.</span><span class="sxs-lookup"><span data-stu-id="89e54-119">Before creating the DNS zone, a resource group is created to contain the DNS Zone.</span></span> <span data-ttu-id="89e54-120">Hieronder ziet u de opdracht.</span><span class="sxs-lookup"><span data-stu-id="89e54-120">The following shows the command.</span></span>

```powershell
New-AzureRMResourceGroup -name MyResourceGroup -location "westus"
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="89e54-121">Een DNS-zone maken</span><span class="sxs-lookup"><span data-stu-id="89e54-121">Create a DNS zone</span></span>

<span data-ttu-id="89e54-122">Een DNS-zone wordt gemaakt met de cmdlet `New-AzureRmDnsZone`.</span><span class="sxs-lookup"><span data-stu-id="89e54-122">A DNS zone is created by using the `New-AzureRmDnsZone` cmdlet.</span></span> <span data-ttu-id="89e54-123">In het volgende voorbeeld maakt u een DNS-zone met de naam *contoso.com* in de resourcegroep *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="89e54-123">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*.</span></span> <span data-ttu-id="89e54-124">Gebruik het voorbeeld om een DNS-zone te maken door de waarden te vervangen door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="89e54-124">Use the example to create a DNS zone, substituting the values for your own.</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyResourceGroup
```

## <a name="create-a-dns-record"></a><span data-ttu-id="89e54-125">Een DNS-record maken</span><span class="sxs-lookup"><span data-stu-id="89e54-125">Create a DNS record</span></span>

<span data-ttu-id="89e54-126">U kunt recordsets maken met behulp van de cmdlet `New-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="89e54-126">You create record sets by using the `New-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="89e54-127">In het volgende voorbeeld maakt u een record met de relatieve naam 'www' in de DNS-zone 'contoso.com' in de resourcegroep 'MyResourceGroup'.</span><span class="sxs-lookup"><span data-stu-id="89e54-127">The following example creates a record with the relative name "www" in the DNS Zone "contoso.com", in resource group "MyResourceGroup".</span></span> <span data-ttu-id="89e54-128">De volledig gekwalificeerde naam van de recordset is 'www.contoso.com'.</span><span class="sxs-lookup"><span data-stu-id="89e54-128">The fully-qualified name of the record set is "www.contoso.com".</span></span> <span data-ttu-id="89e54-129">Het recordtype is 'A', met IP-adres '1.2.3.4', en de TTL is 3600 seconden.</span><span class="sxs-lookup"><span data-stu-id="89e54-129">The record type is "A", with IP address "1.2.3.4", and the TTL is 3600 seconds.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName contoso.com -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4")
```

<span data-ttu-id="89e54-130">Voor andere recordtypen, voor recordsets met meerdere records, en als u bestaande records wilt wijzigen, raadpleegt u [Manage DNS records and record sets using Azure PowerShell](dns-operations-recordsets.md) (DNS-records en -recordsets beheren met behulp van Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="89e54-130">For other record types, for record sets with more than one record, and to modify existing records, see [Manage DNS records and record sets using Azure PowerShell](dns-operations-recordsets.md).</span></span> 


## <a name="view-records"></a><span data-ttu-id="89e54-131">Records weergeven</span><span class="sxs-lookup"><span data-stu-id="89e54-131">View records</span></span>

<span data-ttu-id="89e54-132">Als u de DNS-records wilt weergeven in uw zone, gebruikt u:</span><span class="sxs-lookup"><span data-stu-id="89e54-132">To list the DNS records in your zone, use:</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName contoso.com -ResourceGroupName MyResourceGroup
```


## <a name="update-name-servers"></a><span data-ttu-id="89e54-133">Naamservers bijwerken</span><span class="sxs-lookup"><span data-stu-id="89e54-133">Update name servers</span></span>

<span data-ttu-id="89e54-134">Wanneer uw DNS-zone en -records correct zijn ingesteld, moet u uw domeinnaam configureren voor het gebruik van de Azure DNS-naamservers .</span><span class="sxs-lookup"><span data-stu-id="89e54-134">Once you are satisfied that your DNS zone and records have been set up correctly, you need to configure your domain name to use the Azure DNS name servers.</span></span> <span data-ttu-id="89e54-135">Op die manier kunnen andere gebruikers op internet uw DNS-records vinden.</span><span class="sxs-lookup"><span data-stu-id="89e54-135">This enables other users on the Internet to find your DNS records.</span></span>

<span data-ttu-id="89e54-136">De naamservers voor uw zone zijn gegeven door de cmdlet `Get-AzureRmDnsZone`:</span><span class="sxs-lookup"><span data-stu-id="89e54-136">The name servers for your zone are given by the `Get-AzureRmDnsZone` cmdlet:</span></span>

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

<span data-ttu-id="89e54-137">Deze naamservers moeten worden geconfigureerd met de domeinnaamregistrar (waar u de domeinnaam hebt gekocht).</span><span class="sxs-lookup"><span data-stu-id="89e54-137">These name servers should be configured with the domain name registrar (where you purchased the domain name).</span></span> <span data-ttu-id="89e54-138">Uw registrar zal u de mogelijkheid bieden om de naamservers voor het domein in te stellen.</span><span class="sxs-lookup"><span data-stu-id="89e54-138">Your registrar will offer the option to set up the name servers for the domain.</span></span> <span data-ttu-id="89e54-139">Zie [Uw domein delegeren naar Azure DNS](dns-domain-delegation.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="89e54-139">For more information, see [Delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="89e54-140">Alle resources verwijderen</span><span class="sxs-lookup"><span data-stu-id="89e54-140">Delete all resources</span></span>

<span data-ttu-id="89e54-141">Als u alle resources wilt verwijderen die u in dit artikel hebt gemaakt, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="89e54-141">To delete all resources created in this article, take the following step:</span></span>

```powershell
Remove-AzureRMResourceGroup -Name MyResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="89e54-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="89e54-142">Next steps</span></span>

<span data-ttu-id="89e54-143">Zie [Azure DNS Overview](dns-overview.md) (Overzicht van Azure DNS) voor meer informatie over Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="89e54-143">To learn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="89e54-144">Zie [Manage DNS zones in Azure DNS using PowerShell](dns-operations-dnszones.md) (DNS-zones in Azure DNS beheren met behulp van PowerShell) voor meer informatie over het beheren van DNS-zones in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="89e54-144">To learn more about managing DNS zones in Azure DNS, see [Manage DNS zones in Azure DNS using PowerShell](dns-operations-dnszones.md).</span></span>

<span data-ttu-id="89e54-145">Zie [Manage DNS records and record sets in Azure DNS using PowerShell](dns-operations-recordsets.md) (DNS-records en -recordsets in Azure DNS beheren met behulp van PowerShell) voor meer informatie over het beheren van DNS-records in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="89e54-145">To learn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets in Azure DNS using PowerShell](dns-operations-recordsets.md).</span></span>

