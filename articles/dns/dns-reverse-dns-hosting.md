---
title: Hosting-zones voor reverse DNS-lookup in Azure DNS | Microsoft Docs
description: Informatie over het gebruik van Azure DNS voor het hosten van de zones voor reverse DNS-lookup voor uw IP-adresbereiken
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/29/2017
ms.author: jonatul
ms.openlocfilehash: 3e10b25d2f9b91c96af2958fef6dc6a4fdbff301
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="hosting-reverse-dns-lookup-zones-in-azure-dns"></a><span data-ttu-id="aa0c3-103">Zones voor reverse DNS-lookup in Azure DNS hosten</span><span class="sxs-lookup"><span data-stu-id="aa0c3-103">Hosting reverse DNS lookup zones in Azure DNS</span></span>

<span data-ttu-id="aa0c3-104">In dit artikel wordt uitgelegd hoe de zones voor reverse DNS-lookup voor uw toegewezen IP-adresbereiken in Azure DNS hosten.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-104">This article explains how to host the reverse DNS lookup zones for your assigned IP ranges in Azure DNS.</span></span> <span data-ttu-id="aa0c3-105">De IP-adresbereiken dat wordt vertegenwoordigd door de zone voor reverse lookup moeten worden toegewezen aan uw organisatie gewoonlijk door uw Internetprovider.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-105">The IP ranges represented by the reverse lookup zone must be assigned to your organization, typically by your ISP.</span></span>

<span data-ttu-id="aa0c3-106">Omgekeerde DNS-server voor Azure die eigendom zijn van IP-adres die zijn toegewezen aan uw Azure-service configureren, Zie [de reverse lookup voor de IP-adressen toegewezen aan uw Azure-service configureren](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="aa0c3-106">To configure reverse DNS for Azure-owned IP address assigned to your Azure service, see [configure the reverse lookup for the IP addresses allocated to your Azure service](dns-reverse-dns-for-azure-services.md).</span></span>

<span data-ttu-id="aa0c3-107">Voordat u dit artikel leest, moet u bekend bent met dit [overzicht van de reverse DNS- en biedt ondersteuning in Azure](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="aa0c3-107">Before reading this article, you should be familiar with this [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>

<span data-ttu-id="aa0c3-108">Dit artikel begeleidt u bij de stappen voor het maken van uw eerste reverse lookup DNS-zone en vastleggen met behulp van de Azure-portal, Azure PowerShell, Azure CLI 1.0 of 2.0 voor Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-108">This article walks you through the steps to create your first reverse lookup DNS zone and record using the Azure portal, Azure PowerShell, Azure CLI 1.0 or Azure CLI 2.0.</span></span>

## <a name="create-a-reverse-lookup-dns-zone"></a><span data-ttu-id="aa0c3-109">DNS-zone voor reverse lookup te maken</span><span class="sxs-lookup"><span data-stu-id="aa0c3-109">Create a reverse lookup DNS zone</span></span>

1. <span data-ttu-id="aa0c3-110">Aanmelden bij de [Azure-portal](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="aa0c3-110">Sign in to the [Azure portal](https://portal.azure.com)</span></span>
1. <span data-ttu-id="aa0c3-111">Klik in het menu Hub en op **nieuw** > **Networking** > en klik vervolgens op **DNS-zone** openen de **maken DNS-zone** blade.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-111">On the Hub menu, click and click **New** > **Networking** > and then click **DNS zone** to open the **Create DNS zone** blade.</span></span>

   ![DNS-zone](./media/dns-reverse-dns-hosting/figure1.png)

1. <span data-ttu-id="aa0c3-113">Op de **maken DNS-zone** blade naam van uw DNS-zone.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-113">On the **Create DNS zone** blade, name your DNS zone.</span></span> <span data-ttu-id="aa0c3-114">De naam van de zone is anders vervaardigde voor IPv4 en IPv6-voorvoegsels.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-114">The name of the zone is crafted differently for IPv4 and IPv6 prefixes.</span></span> <span data-ttu-id="aa0c3-115">Gebruik van de instructies voor [IPV4](#ipv4) of [IPv6](#ipv6) als naam voor uw zone.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-115">Use either the instructions for [IPV4](#ipv4) or [IPv6](#ipv6) to name your zone.</span></span> <span data-ttu-id="aa0c3-116">Klik wanneer u klaar **maken** om de zone te maken.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-116">When complete click **Create** to create the zone.</span></span>

### <a name="ipv4"></a><span data-ttu-id="aa0c3-117">IPv4</span><span class="sxs-lookup"><span data-stu-id="aa0c3-117">IPv4</span></span>

<span data-ttu-id="aa0c3-118">De naam van een IPv4-zone voor reverse lookup is gebaseerd op het IP-adresbereik dat wordt vertegenwoordigd.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-118">The name of an IPv4 reverse lookup zone is based on the IP range it represents.</span></span> <span data-ttu-id="aa0c3-119">Deze moet de volgende indeling: `<IPv4 network prefix in reverse order>.in-addr.arpa`.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-119">It should be in the following format: `<IPv4 network prefix in reverse order>.in-addr.arpa`.</span></span> <span data-ttu-id="aa0c3-120">Zie voor voorbeelden [overzicht van de reverse DNS- en biedt ondersteuning in Azure](dns-reverse-dns-overview.md#ipv4).</span><span class="sxs-lookup"><span data-stu-id="aa0c3-120">For examples, see [overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md#ipv4).</span></span>

> [!NOTE]
> <span data-ttu-id="aa0c3-121">Wanneer u een omgekeerde DNS-lookup-zones in Azure DNS maakt, moet u een koppelteken (`-`) in plaats van met een slash ('/ ') in de zonenaam.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-121">When creating classless reverse DNS lookup zones in Azure DNS, you must use a hyphen (`-`) rather than a forward slash ('/') in the zone name.</span></span>
>
> <span data-ttu-id="aa0c3-122">Bijvoorbeeld: voor het IP-bereik 192.0.2.128/26, moet u `128-26.2.0.192.in-addr.arpa` als de naam van de zone in plaats van `128/26.2.0.192.in-addr.arpa`.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-122">For example, for the IP range 192.0.2.128/26, you must use `128-26.2.0.192.in-addr.arpa` as the zone name instead of `128/26.2.0.192.in-addr.arpa`.</span></span>
>
> <span data-ttu-id="aa0c3-123">Dit is omdat beide worden wel ondersteund door de DNS-standaarden, DNS-zone-namen met een slash (`/`) tekens worden niet ondersteund in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-123">This is because, while both are supported by the DNS standards, DNS zone names containing the forward slash (`/`) character are not supported in Azure DNS.</span></span>

<span data-ttu-id="aa0c3-124">Het volgende voorbeeld laat zien hoe 'Klasse C' omgekeerde DNS-zone maken met de naam `2.0.192.in-addr.arpa` in Azure DNS via de Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="aa0c3-124">The following example shows how to create a 'Class C' reverse DNS zone named `2.0.192.in-addr.arpa` in Azure DNS via the Azure portal:</span></span>

 ![DNS-zone maken](./media/dns-reverse-dns-hosting/figure2.png)

<span data-ttu-id="aa0c3-126">'Locatie van de resourcegroep' definieert de locatie voor de resourcegroep en heeft geen invloed op de DNS-zone.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-126">The 'Resource group location' defines the location for the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="aa0c3-127">De DNS-zone-locatie is altijd 'global' en niet wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-127">The DNS zone location is always 'global', and is not shown.</span></span>

<span data-ttu-id="aa0c3-128">De volgende voorbeelden laten zien hoe u dit moet doen met Azure PowerShell en de Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="aa0c3-128">The following examples show how to complete this task with Azure PowerShell and the Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="aa0c3-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="aa0c3-129">PowerShell</span></span>

```powershell
New-AzureRmDnsZone -Name 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="aa0c3-130">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="aa0c3-130">Azure CLI 1.0</span></span>

```azurecli
azure network dns zone create MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="aa0c3-131">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="aa0c3-131">Azure CLI 2.0</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a><span data-ttu-id="aa0c3-132">IPv6</span><span class="sxs-lookup"><span data-stu-id="aa0c3-132">IPv6</span></span>

<span data-ttu-id="aa0c3-133">De naam van een IPv6-zone voor reverse lookup moet de volgende notatie: `<IPv6 network prefix in reverse order>.ip6.arpa`.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-133">The name of an IPv6 reverse lookup zone should be in the following form: `<IPv6 network prefix in reverse order>.ip6.arpa`.</span></span>  <span data-ttu-id="aa0c3-134">Zie voor voorbeelden [overzicht van de reverse DNS- en biedt ondersteuning in Azure](dns-reverse-dns-overview.md#ipv6).</span><span class="sxs-lookup"><span data-stu-id="aa0c3-134">For examples, see [overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md#ipv6).</span></span>


<span data-ttu-id="aa0c3-135">Het volgende voorbeeld laat zien hoe een IPv6 reverse DNS-lookup zone maken met de naam `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` in Azure DNS via de Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="aa0c3-135">The following example shows how to create an IPv6 reverse DNS lookup zone named `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` in Azure DNS via the Azure portal:</span></span>

 ![DNS-zone maken](./media/dns-reverse-dns-hosting/figure3.png)

<span data-ttu-id="aa0c3-137">'Locatie van de resourcegroep' definieert de locatie voor de resourcegroep en heeft geen invloed op de DNS-zone.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-137">The 'Resource group location' defines the location for the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="aa0c3-138">De DNS-zone-locatie is altijd 'global' en niet wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-138">The DNS zone location is always 'global', and is not shown.</span></span>

<span data-ttu-id="aa0c3-139">De volgende voorbeelden laten zien hoe u dit moet doen met Azure PowerShell en de Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="aa0c3-139">The following examples show how to complete this task with Azure PowerShell and the Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="aa0c3-140">PowerShell</span><span class="sxs-lookup"><span data-stu-id="aa0c3-140">PowerShell</span></span>

```powershell
New-AzureRmDnsZone -Name 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azurecli-10"></a><span data-ttu-id="aa0c3-141">AzureCLI 1.0</span><span class="sxs-lookup"><span data-stu-id="aa0c3-141">AzureCLI 1.0</span></span>

```azurecli
azure network dns zone create MyResourceGroup 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azurecli-20"></a><span data-ttu-id="aa0c3-142">AzureCLI 2.0</span><span class="sxs-lookup"><span data-stu-id="aa0c3-142">AzureCLI 2.0</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="delegate-a-reverse-dns-lookup-zone"></a><span data-ttu-id="aa0c3-143">Een DNS-zone voor reverse lookup delegeren</span><span class="sxs-lookup"><span data-stu-id="aa0c3-143">Delegate a reverse DNS lookup zone</span></span>

<span data-ttu-id="aa0c3-144">Uw DNS-zone voor reverse lookup die worden gemaakt, moet u ervoor zorgen dat de zone van de bovenliggende zone is overgedragen.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-144">Having created your reverse DNS lookup zone, you must ensure that the zone is delegated from the parent zone.</span></span> <span data-ttu-id="aa0c3-145">DNS-delegering kunt de DNS-naamomzettingsproces de naamservers die als host fungeert voor uw DNS-zone voor reverse lookup te vinden.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-145">DNS delegation enables the DNS name resolution process to find the name servers hosting your reverse DNS lookup zone.</span></span> <span data-ttu-id="aa0c3-146">Hierdoor kunnen deze naamservers om omgekeerde DNS-query's voor de IP-adressen in uw-adresbereik te beantwoorden.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-146">This enables those name servers to answer DNS reverse queries for the IP addresses in your address range.</span></span>

<span data-ttu-id="aa0c3-147">Het proces van het delegeren van een DNS-zone wordt voor zones voor forward lookup beschreven in [uw domein delegeren naar Azure DNS](dns-delegate-domain-azure-dns.md).</span><span class="sxs-lookup"><span data-stu-id="aa0c3-147">For forward lookup zones, the process of delegating a DNS zone is described in [Delegate your domain to Azure DNS](dns-delegate-domain-azure-dns.md).</span></span> <span data-ttu-id="aa0c3-148">Delegering voor zones voor reverse lookup werkt op dezelfde manier.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-148">Delegation for reverse lookup zones works the same way.</span></span> <span data-ttu-id="aa0c3-149">Het enige verschil is dat u de naamservers configureren met de ISP die uw IP-adresbereik, in plaats van uw domeinnaamregistrar.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-149">The only difference is that you need to configure the name servers with the ISP who provided your IP range, rather than your domain name registrar.</span></span>

## <a name="create-a-dns-ptr-record"></a><span data-ttu-id="aa0c3-150">Een DNS PTR-record maken</span><span class="sxs-lookup"><span data-stu-id="aa0c3-150">Create a DNS PTR record</span></span>

### <a name="ipv4"></a><span data-ttu-id="aa0c3-151">IPv4</span><span class="sxs-lookup"><span data-stu-id="aa0c3-151">IPv4</span></span>

<span data-ttu-id="aa0c3-152">Het volgende voorbeeld wordt uitgelegd hoe u een PTR-record maken in een reverse DNS-zone in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-152">The following example walks you through the process of creating a PTR record in a reverse DNS zone in Azure DNS.</span></span> <span data-ttu-id="aa0c3-153">Voor andere typen en voor het wijzigen van bestaande records, raadpleegt u [Manage DNS records and record sets by using the Azure portal](dns-operations-recordsets-portal.md) (DNS-records en -recordsets beheren met behulp van Azure Portal).</span><span class="sxs-lookup"><span data-stu-id="aa0c3-153">For other record types and to modify existing records, see [Manage DNS records and record sets by using the Azure portal](dns-operations-recordsets-portal.md).</span></span>

1.  <span data-ttu-id="aa0c3-154">Selecteer boven in de blade **DNS-zone** de optie **+ Recordset** om de blade **Recordset toevoegen** te openen.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-154">At the top of the **DNS zone** blade, select **+ Record set** to open the **Add record set** blade.</span></span>

 ![DNS-zone](./media/dns-reverse-dns-hosting/figure4.png)

1. <span data-ttu-id="aa0c3-156">Op de **recordset toevoegen** blade.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-156">On the **Add record set** blade.</span></span> 
1. <span data-ttu-id="aa0c3-157">Selecteer **PTR** uit de record '**Type**' menu.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-157">Select **PTR** from the record "**Type**" menu.</span></span>  
1. <span data-ttu-id="aa0c3-158">De naam van de recordset voor een PTR-record moet de rest van het IPv4-adres in omgekeerde volgorde.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-158">The name of the record set for a PTR record needs to be the rest of the IPv4 address in reverse order.</span></span> <span data-ttu-id="aa0c3-159">In dit voorbeeld worden de eerste drie octetten al ingevuld als onderdeel van de naam van de zone (.2.0.192).</span><span class="sxs-lookup"><span data-stu-id="aa0c3-159">In this example, the first three octets are already populated as part of the zone name (.2.0.192).</span></span> <span data-ttu-id="aa0c3-160">Daarom is alleen het laatste octet opgegeven in het naamveld.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-160">Therefore, only the last octet is supplied in the name field.</span></span> <span data-ttu-id="aa0c3-161">U kunt uw recordset bijvoorbeeld de naam '**15**' voor een resource waarvan IP-adres 192.0.2.15 is.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-161">For example, you could name your record set "**15**" for a resource whose IP address is 192.0.2.15.</span></span>  
1. <span data-ttu-id="aa0c3-162">In de '**domeinnaam**"en voer de volledig gekwalificeerde domeinnaam (FQDN) van de resource met behulp van het IP-adres.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-162">In the "**Domain Name**" field, enter the fully qualified domain name (FQDN) of the resource using the IP.</span></span>
1. <span data-ttu-id="aa0c3-163">Selecteer onder in de blade **OK** om de DNS-record te maken.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-163">Select **OK** at the bottom of the blade to create the DNS record.</span></span>

 ![recordset toevoegen](./media/dns-reverse-dns-hosting/figure5.png)

<span data-ttu-id="aa0c3-165">Hier volgen enkele voorbeelden voor het voltooien van deze taak met PowerShell en de AzureCLI:</span><span class="sxs-lookup"><span data-stu-id="aa0c3-165">The following are examples on how to complete this task with PowerShell and the AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="aa0c3-166">PowerShell</span><span class="sxs-lookup"><span data-stu-id="aa0c3-166">PowerShell</span></span>

```powershell
New-AzureRmDnsRecordSet -Name 15 -RecordType PTR -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc1.contoso.com")
```
#### <a name="azurecli-10"></a><span data-ttu-id="aa0c3-167">AzureCLI 1.0</span><span class="sxs-lookup"><span data-stu-id="aa0c3-167">AzureCLI 1.0</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup 2.0.192.in-addr.arpa 15 PTR --ptrdname dc1.contoso.com  
```

#### <a name="azurecli-20"></a><span data-ttu-id="aa0c3-168">AzureCLI 2.0</span><span class="sxs-lookup"><span data-stu-id="aa0c3-168">AzureCLI 2.0</span></span>

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 2.0.192.in-addr.arpa -n 15 --ptrdname dc1.contoso.com
```

### <a name="ipv6"></a><span data-ttu-id="aa0c3-169">IPv6</span><span class="sxs-lookup"><span data-stu-id="aa0c3-169">IPv6</span></span>

<span data-ttu-id="aa0c3-170">Het volgende voorbeeld wordt u begeleid het proces van het nieuwe 'PTR-record te maken.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-170">The following example walks you through the process of creating new 'PTR' record.</span></span> <span data-ttu-id="aa0c3-171">Voor andere typen en voor het wijzigen van bestaande records, raadpleegt u [Manage DNS records and record sets by using the Azure portal](dns-operations-recordsets-portal.md) (DNS-records en -recordsets beheren met behulp van Azure Portal).</span><span class="sxs-lookup"><span data-stu-id="aa0c3-171">For other record types and to modify existing records, see [Manage DNS records and record sets by using the Azure portal](dns-operations-recordsets-portal.md).</span></span>

1. <span data-ttu-id="aa0c3-172">Aan de bovenkant van de **DNS-zone blade**, selecteer **+ Recordset** openen de **recordset toevoegen** blade.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-172">At the top of the **DNS zone blade**, select **+ Record set** to open the **Add record set** blade.</span></span>

  ![DNS-zone-blade](./media/dns-reverse-dns-hosting/figure6.png)

2. <span data-ttu-id="aa0c3-174">Op de **recordset toevoegen** blade.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-174">On the **Add record set** blade.</span></span> 
3. <span data-ttu-id="aa0c3-175">Selecteer **PTR** uit de record '**Type**' menu.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-175">Select **PTR** from the record "**Type**" menu.</span></span>  
4. <span data-ttu-id="aa0c3-176">De naam van de recordset voor een PTR-record moet de rest van het IPv6-adres in omgekeerde volgorde.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-176">The name of the record set for a PTR record needs to be the rest of the IPv6 address in reverse order.</span></span> <span data-ttu-id="aa0c3-177">Het mag geen nul gecomprimeerd bevatten.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-177">It must not include any zero compression.</span></span> <span data-ttu-id="aa0c3-178">In dit voorbeeld worden de eerste 64 bits van het IPv6-al ingevuld als onderdeel van de naam van de zone (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa).</span><span class="sxs-lookup"><span data-stu-id="aa0c3-178">In this example, the first 64 bits of the IPv6 are already populated as part of the zone name (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa).</span></span> <span data-ttu-id="aa0c3-179">Daarom worden alleen de laatste 64 bits zijn opgegeven in het naamveld.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-179">Therefore, only the last 64 bits are supplied in the name field.</span></span> <span data-ttu-id="aa0c3-180">De laatste 64 bits van het IP-adres worden ingevoerd in omgekeerde volgorde, met een punt als scheidingsteken tussen elke hexadecimaal getal.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-180">The last 64 bits of the IP address are entered in reverse order, using a period as the delimiter between each hexadecimal number.</span></span> <span data-ttu-id="aa0c3-181">U kunt uw recordset bijvoorbeeld de naam '**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**' voor een resource waarvan IP-adres 2001:0db8:abdc:0000:f524:10bc:1af9:405e is.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-181">For example, you could name your record set "**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**" for a resource whose IP address is 2001:0db8:abdc:0000:f524:10bc:1af9:405e.</span></span>  
5. <span data-ttu-id="aa0c3-182">In de '**domeinnaam**"en voer de volledig gekwalificeerde domeinnaam (FQDN) van de resource met behulp van het IP-adres.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-182">In the "**Domain Name**" field, enter the fully qualified domain name (FQDN) of the resource using the IP.</span></span>
6. <span data-ttu-id="aa0c3-183">Selecteer onder in de blade **OK** om de DNS-record te maken.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-183">Select **OK** at the bottom of the blade to create the DNS record.</span></span>

![Recordset blade toevoegen](./media/dns-reverse-dns-hosting/figure7.png)

<span data-ttu-id="aa0c3-185">Hier volgen enkele voorbeelden voor het voltooien van deze taak met PowerShell en de AzureCLI:</span><span class="sxs-lookup"><span data-stu-id="aa0c3-185">The following are examples on how to complete this task with PowerShell and the AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="aa0c3-186">PowerShell</span><span class="sxs-lookup"><span data-stu-id="aa0c3-186">PowerShell</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f" -RecordType PTR -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc2.contoso.com")
```

#### <a name="azurecli-10"></a><span data-ttu-id="aa0c3-187">AzureCLI 1.0</span><span class="sxs-lookup"><span data-stu-id="aa0c3-187">AzureCLI 1.0</span></span>

```
azure network dns record-set add-record MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f PTR --ptrdname dc2.contoso.com 
```
 
#### <a name="azurecli-20"></a><span data-ttu-id="aa0c3-188">AzureCLI 2.0</span><span class="sxs-lookup"><span data-stu-id="aa0c3-188">AzureCLI 2.0</span></span>

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -n e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f --ptrdname dc2.contoso.com
```

## <a name="view-records"></a><span data-ttu-id="aa0c3-189">Records weergeven</span><span class="sxs-lookup"><span data-stu-id="aa0c3-189">View Records</span></span>

<span data-ttu-id="aa0c3-190">De records die u hebt gemaakt wilt weergeven, gaat u naar de DNS-zone in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-190">To view the records you created, navigate to your DNS zone in the Azure portal.</span></span> <span data-ttu-id="aa0c3-191">In het onderste gedeelte van de **DNS-zone** blade ziet u de records voor de DNS-zone.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-191">In the lower part of the **DNS zone** blade, you can see the records for the DNS zone.</span></span> <span data-ttu-id="aa0c3-192">U ziet de standaardrecords NS en SOA, die in elke zone worden gemaakt, plus alle nieuwe records die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-192">You should see the default NS and SOA records, which are created in every zone, plus any new records you have created.</span></span>

### <a name="ipv4"></a><span data-ttu-id="aa0c3-193">IPv4</span><span class="sxs-lookup"><span data-stu-id="aa0c3-193">IPv4</span></span>

<span data-ttu-id="aa0c3-194">DNS-zone blade IPv4 PTR-records worden weergegeven:</span><span class="sxs-lookup"><span data-stu-id="aa0c3-194">DNS zone blade, showing IPv4 PTR records:</span></span>

![DNS-zone-blade](./media/dns-reverse-dns-hosting/figure8.png)

<span data-ttu-id="aa0c3-196">De volgende voorbeelden laten zien hoe de PTR-records met PowerShell of Azure CLI weergeven:</span><span class="sxs-lookup"><span data-stu-id="aa0c3-196">The following examples show how to view the PTR records using PowerShell or the Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="aa0c3-197">PowerShell</span><span class="sxs-lookup"><span data-stu-id="aa0c3-197">PowerShell</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="aa0c3-198">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="aa0c3-198">Azure CLI 1.0</span></span>

```azurecli
    azure network dns record-set list MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="aa0c3-199">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="aa0c3-199">Azure CLI 2.0</span></span>

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a><span data-ttu-id="aa0c3-200">IPv6</span><span class="sxs-lookup"><span data-stu-id="aa0c3-200">IPv6</span></span>

<span data-ttu-id="aa0c3-201">DNS-zone blade IPv6 PTR-records worden weergegeven:</span><span class="sxs-lookup"><span data-stu-id="aa0c3-201">DNS zone blade, showing IPv6 PTR records:</span></span>

![DNS-zone-blade](./media/dns-reverse-dns-hosting/figure9.png)

<span data-ttu-id="aa0c3-203">Hier volgen enkele voorbeelden voor het weergeven van de records met PowerShell en de AzureCLI:</span><span class="sxs-lookup"><span data-stu-id="aa0c3-203">The following are examples on how to view the records with PowerShell and the AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="aa0c3-204">PowerShell</span><span class="sxs-lookup"><span data-stu-id="aa0c3-204">PowerShell</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="aa0c3-205">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="aa0c3-205">Azure CLI 1.0</span></span>

```azurecli
    azure network dns record-set list MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="aa0c3-206">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="aa0c3-206">Azure CLI 2.0</span></span>

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="faq"></a><span data-ttu-id="aa0c3-207">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="aa0c3-207">FAQ</span></span>

### <a name="can-i-host-reverse-dns-lookup-zones-for-my-isp-assigned-ip-blocks-on-azure-dns"></a><span data-ttu-id="aa0c3-208">Kan ik voor mijn ISP toegewezen IP-adresblokken op Azure DNS zones voor reverse DNS-lookup hosten?</span><span class="sxs-lookup"><span data-stu-id="aa0c3-208">Can I host reverse DNS lookup zones for my ISP-assigned IP blocks on Azure DNS?</span></span>

<span data-ttu-id="aa0c3-209">Ja.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-209">Yes.</span></span> <span data-ttu-id="aa0c3-210">De zones voor reverse lookup (ARPA) voor uw eigen IP-adresbereiken in Azure DNS hosten wordt volledig ondersteund.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-210">Hosting the reverse lookup (ARPA) zones for your own IP ranges in Azure DNS is fully supported.</span></span>

<span data-ttu-id="aa0c3-211">De zone voor reverse lookup maakt in Azure DNS als uiteengezet in dit artikel en werk uw internetprovider [de zone delegeren](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="aa0c3-211">Create the reverse lookup zone in Azure DNS as explained in this article, then work with your ISP to [delegate the zone](dns-domain-delegation.md).</span></span>  <span data-ttu-id="aa0c3-212">U kunt de PTR-records voor elke reverse lookup beheren op dezelfde manier als andere recordtypen.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-212">You can then manage the PTR records for each reverse lookup in the same way as other record types.</span></span>

### <a name="how-much-does-hosting-my-reverse-dns-lookup-zone-cost"></a><span data-ttu-id="aa0c3-213">Hoeveel gebruikt die als host fungeert voor mijn omgekeerde DNS-lookup zone kosten?</span><span class="sxs-lookup"><span data-stu-id="aa0c3-213">How much does hosting my reverse DNS lookup zone cost?</span></span>

<span data-ttu-id="aa0c3-214">De DNS-zone voor reverse lookup als host fungeert voor uw Internetprovider toegewezen IP-Adresblok in Azure DNS in rekening volgens gebracht [standaardtarieven Azure DNS](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="aa0c3-214">Hosting the reverse DNS lookup zone for your ISP-assigned IP block in Azure DNS is charged at [standard Azure DNS rates](https://azure.microsoft.com/pricing/details/dns/).</span></span>

### <a name="can-i-host-reverse-dns-lookup-zones-for-both-ipv4-and-ipv6-addresses-in-azure-dns"></a><span data-ttu-id="aa0c3-215">Kan ik zones voor reverse DNS-lookup voor IPv4 en IPv6-adressen in Azure DNS hosten?</span><span class="sxs-lookup"><span data-stu-id="aa0c3-215">Can I host reverse DNS lookup zones for both IPv4 and IPv6 addresses in Azure DNS?</span></span>

<span data-ttu-id="aa0c3-216">Ja.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-216">Yes.</span></span> <span data-ttu-id="aa0c3-217">Dit artikel wordt uitgelegd hoe u zowel IPv4 als IPv6 reverse DNS-zones lookup maakt in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-217">This article explains how to create both IPv4 and IPv6 reverse DNS lookup zones in Azure DNS.</span></span>

### <a name="can-i-import-an-existing-reverse-dns-lookup-zone"></a><span data-ttu-id="aa0c3-218">Kan ik een bestaande zone voor reverse DNS-lookup importeren?</span><span class="sxs-lookup"><span data-stu-id="aa0c3-218">Can I import an existing reverse DNS lookup zone?</span></span>

<span data-ttu-id="aa0c3-219">Ja.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-219">Yes.</span></span> <span data-ttu-id="aa0c3-220">Bestaande DNS-zones importeren in Azure DNS kunt u de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-220">You can use the Azure CLI to import existing DNS zones into Azure DNS.</span></span> <span data-ttu-id="aa0c3-221">Dit werkt voor zowel zones voor forward lookup en zones voor reverse lookup.</span><span class="sxs-lookup"><span data-stu-id="aa0c3-221">This works for both forward lookup zones and reverse lookup zones.</span></span>

<span data-ttu-id="aa0c3-222">Zie voor meer informatie [importeren en exporteren van een DNS-zone-bestand met de Azure CLI](dns-import-export.md).</span><span class="sxs-lookup"><span data-stu-id="aa0c3-222">For more information, see [Import and export a DNS zone file using the Azure CLI](dns-import-export.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa0c3-223">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="aa0c3-223">Next steps</span></span>

<span data-ttu-id="aa0c3-224">Zie voor meer informatie over omgekeerde DNS [achterwaartse DNS-zoekopdracht op Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span><span class="sxs-lookup"><span data-stu-id="aa0c3-224">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="aa0c3-225">Meer informatie over hoe [omgekeerde DNS-records voor uw Azure-services beheren](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="aa0c3-225">Learn how to [manage reverse DNS records for your Azure services](dns-reverse-dns-for-azure-services.md).</span></span>
