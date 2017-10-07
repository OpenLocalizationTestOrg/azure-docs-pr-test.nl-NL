---
title: aaaHosting zones voor reverse DNS-lookup in Azure DNS | Microsoft Docs
description: Meer informatie over hoe toouse Azure DNS toohost Hallo zones voor reverse DNS-lookup voor uw IP-adresbereiken
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
ms.openlocfilehash: 24feb8ef1c75a7d91938867f348fed1190046e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="hosting-reverse-dns-lookup-zones-in-azure-dns"></a><span data-ttu-id="d34bb-103">Zones voor reverse DNS-lookup in Azure DNS hosten</span><span class="sxs-lookup"><span data-stu-id="d34bb-103">Hosting reverse DNS lookup zones in Azure DNS</span></span>

<span data-ttu-id="d34bb-104">Dit artikel wordt uitgelegd hoe toohost Hallo zones voor reverse DNS-lookup voor uw toegewezen IP-adresbereiken in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="d34bb-104">This article explains how toohost hello reverse DNS lookup zones for your assigned IP ranges in Azure DNS.</span></span> <span data-ttu-id="d34bb-105">Hallo IP-adresbereiken dat wordt vertegenwoordigd door een zone voor reverse lookup Hallo moeten worden toegewezen tooyour organisatie, doorgaans door uw Internetprovider.</span><span class="sxs-lookup"><span data-stu-id="d34bb-105">hello IP ranges represented by hello reverse lookup zone must be assigned tooyour organization, typically by your ISP.</span></span>

<span data-ttu-id="d34bb-106">tooconfigure omgekeerde DNS voor Azure die eigendom zijn van IP-adres toegewezen tooyour Azure-service, raadpleegt u [Hallo reverse lookup configureren voor Hallo IP-adressen tooyour Azure service toegewezen](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="d34bb-106">tooconfigure reverse DNS for Azure-owned IP address assigned tooyour Azure service, see [configure hello reverse lookup for hello IP addresses allocated tooyour Azure service](dns-reverse-dns-for-azure-services.md).</span></span>

<span data-ttu-id="d34bb-107">Voordat u dit artikel leest, moet u bekend bent met dit [overzicht van de reverse DNS- en biedt ondersteuning in Azure](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d34bb-107">Before reading this article, you should be familiar with this [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>

<span data-ttu-id="d34bb-108">Dit artikel begeleidt u bij Hallo stappen toocreate, uw eerste DNS-zone voor reverse lookup en de record met behulp van hello Azure-portal, Azure PowerShell, Azure CLI 1.0 of 2.0 voor Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="d34bb-108">This article walks you through hello steps toocreate your first reverse lookup DNS zone and record using hello Azure portal, Azure PowerShell, Azure CLI 1.0 or Azure CLI 2.0.</span></span>

## <a name="create-a-reverse-lookup-dns-zone"></a><span data-ttu-id="d34bb-109">DNS-zone voor reverse lookup te maken</span><span class="sxs-lookup"><span data-stu-id="d34bb-109">Create a reverse lookup DNS zone</span></span>

1. <span data-ttu-id="d34bb-110">Meld u aan toohello [Azure-portal](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="d34bb-110">Sign in toohello [Azure portal](https://portal.azure.com)</span></span>
1. <span data-ttu-id="d34bb-111">Klik op Hallo Hub-menu en klik op **nieuw** > **netwerken** > en klik vervolgens op **DNS-zone** tooopen Hallo **maken DNS-zone**blade.</span><span class="sxs-lookup"><span data-stu-id="d34bb-111">On hello Hub menu, click and click **New** > **Networking** > and then click **DNS zone** tooopen hello **Create DNS zone** blade.</span></span>

   ![DNS-zone](./media/dns-reverse-dns-hosting/figure1.png)

1. <span data-ttu-id="d34bb-113">Op Hallo **maken DNS-zone** blade naam van uw DNS-zone.</span><span class="sxs-lookup"><span data-stu-id="d34bb-113">On hello **Create DNS zone** blade, name your DNS zone.</span></span> <span data-ttu-id="d34bb-114">Hallo-naam van Hallo zone worden anders gemanipuleerd voor IPv4 en IPv6-voorvoegsels.</span><span class="sxs-lookup"><span data-stu-id="d34bb-114">hello name of hello zone is crafted differently for IPv4 and IPv6 prefixes.</span></span> <span data-ttu-id="d34bb-115">Beide Hallo-instructies voor het gebruik [IPV4](#ipv4) of [IPv6](#ipv6) tooname uw zone.</span><span class="sxs-lookup"><span data-stu-id="d34bb-115">Use either hello instructions for [IPV4](#ipv4) or [IPv6](#ipv6) tooname your zone.</span></span> <span data-ttu-id="d34bb-116">Klik wanneer u klaar **maken** toocreate Hallo zone.</span><span class="sxs-lookup"><span data-stu-id="d34bb-116">When complete click **Create** toocreate hello zone.</span></span>

### <a name="ipv4"></a><span data-ttu-id="d34bb-117">IPv4</span><span class="sxs-lookup"><span data-stu-id="d34bb-117">IPv4</span></span>

<span data-ttu-id="d34bb-118">Hallo-naam van een IPv4-zone voor reverse lookup is gebaseerd op Hallo IP-adresbereik vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="d34bb-118">hello name of an IPv4 reverse lookup zone is based on hello IP range it represents.</span></span> <span data-ttu-id="d34bb-119">Deze moet Hallo volgende indeling: `<IPv4 network prefix in reverse order>.in-addr.arpa`.</span><span class="sxs-lookup"><span data-stu-id="d34bb-119">It should be in hello following format: `<IPv4 network prefix in reverse order>.in-addr.arpa`.</span></span> <span data-ttu-id="d34bb-120">Zie voor voorbeelden [overzicht van de reverse DNS- en biedt ondersteuning in Azure](dns-reverse-dns-overview.md#ipv4).</span><span class="sxs-lookup"><span data-stu-id="d34bb-120">For examples, see [overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md#ipv4).</span></span>

> [!NOTE]
> <span data-ttu-id="d34bb-121">Wanneer u een omgekeerde DNS-lookup-zones in Azure DNS maakt, moet u een koppelteken (`-`) in plaats van met een slash ('/ ') in Hallo zonenaam.</span><span class="sxs-lookup"><span data-stu-id="d34bb-121">When creating classless reverse DNS lookup zones in Azure DNS, you must use a hyphen (`-`) rather than a forward slash ('/') in hello zone name.</span></span>
>
> <span data-ttu-id="d34bb-122">Bijvoorbeeld: voor Hallo IP-bereik 192.0.2.128/26, moet u `128-26.2.0.192.in-addr.arpa` als Hallo zonenaam in plaats van `128/26.2.0.192.in-addr.arpa`.</span><span class="sxs-lookup"><span data-stu-id="d34bb-122">For example, for hello IP range 192.0.2.128/26, you must use `128-26.2.0.192.in-addr.arpa` as hello zone name instead of `128/26.2.0.192.in-addr.arpa`.</span></span>
>
> <span data-ttu-id="d34bb-123">Dit is omdat beide worden wel ondersteund door Hallo DNS-standaarden, DNS-zone-namen met een slash hello (`/`) tekens worden niet ondersteund in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="d34bb-123">This is because, while both are supported by hello DNS standards, DNS zone names containing hello forward slash (`/`) character are not supported in Azure DNS.</span></span>

<span data-ttu-id="d34bb-124">Hallo volgende voorbeeld laat zien hoe toocreate een klasse C reverse DNS-zone met de naam `2.0.192.in-addr.arpa` in Azure DNS via hello Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="d34bb-124">hello following example shows how toocreate a 'Class C' reverse DNS zone named `2.0.192.in-addr.arpa` in Azure DNS via hello Azure portal:</span></span>

 ![DNS-zone maken](./media/dns-reverse-dns-hosting/figure2.png)

<span data-ttu-id="d34bb-126">Hallo 'Locatie voor resourcegroep' Hallo-locatie voor de resourcegroep Hallo definieert, en heeft geen invloed op Hallo DNS-zone.</span><span class="sxs-lookup"><span data-stu-id="d34bb-126">hello 'Resource group location' defines hello location for hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="d34bb-127">Hallo DNS-zone locatie is altijd 'global' en niet wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d34bb-127">hello DNS zone location is always 'global', and is not shown.</span></span>

<span data-ttu-id="d34bb-128">Hallo volgende voorbeelden ziet u hoe toocomplete dit taak met Azure PowerShell en Azure CLI Hallo:</span><span class="sxs-lookup"><span data-stu-id="d34bb-128">hello following examples show how toocomplete this task with Azure PowerShell and hello Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="d34bb-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d34bb-129">PowerShell</span></span>

```powershell
New-AzureRmDnsZone -Name 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="d34bb-130">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d34bb-130">Azure CLI 1.0</span></span>

```azurecli
azure network dns zone create MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="d34bb-131">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d34bb-131">Azure CLI 2.0</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a><span data-ttu-id="d34bb-132">IPv6</span><span class="sxs-lookup"><span data-stu-id="d34bb-132">IPv6</span></span>

<span data-ttu-id="d34bb-133">Hallo-naam van een IPv6-zone voor reverse lookup moet in Hallo volgende vorm: `<IPv6 network prefix in reverse order>.ip6.arpa`.</span><span class="sxs-lookup"><span data-stu-id="d34bb-133">hello name of an IPv6 reverse lookup zone should be in hello following form: `<IPv6 network prefix in reverse order>.ip6.arpa`.</span></span>  <span data-ttu-id="d34bb-134">Zie voor voorbeelden [overzicht van de reverse DNS- en biedt ondersteuning in Azure](dns-reverse-dns-overview.md#ipv6).</span><span class="sxs-lookup"><span data-stu-id="d34bb-134">For examples, see [overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md#ipv6).</span></span>


<span data-ttu-id="d34bb-135">Hallo volgende voorbeeld laat zien hoe toocreate een IPv6 reverse DNS-lookup zone met de naam `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` in Azure DNS via hello Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="d34bb-135">hello following example shows how toocreate an IPv6 reverse DNS lookup zone named `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` in Azure DNS via hello Azure portal:</span></span>

 ![DNS-zone maken](./media/dns-reverse-dns-hosting/figure3.png)

<span data-ttu-id="d34bb-137">Hallo 'Locatie voor resourcegroep' Hallo-locatie voor de resourcegroep Hallo definieert, en heeft geen invloed op Hallo DNS-zone.</span><span class="sxs-lookup"><span data-stu-id="d34bb-137">hello 'Resource group location' defines hello location for hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="d34bb-138">Hallo DNS-zone locatie is altijd 'global' en niet wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d34bb-138">hello DNS zone location is always 'global', and is not shown.</span></span>

<span data-ttu-id="d34bb-139">Hallo volgende voorbeelden ziet u hoe toocomplete dit taak met Azure PowerShell en Azure CLI Hallo:</span><span class="sxs-lookup"><span data-stu-id="d34bb-139">hello following examples show how toocomplete this task with Azure PowerShell and hello Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="d34bb-140">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d34bb-140">PowerShell</span></span>

```powershell
New-AzureRmDnsZone -Name 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azurecli-10"></a><span data-ttu-id="d34bb-141">AzureCLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d34bb-141">AzureCLI 1.0</span></span>

```azurecli
azure network dns zone create MyResourceGroup 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azurecli-20"></a><span data-ttu-id="d34bb-142">AzureCLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d34bb-142">AzureCLI 2.0</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="delegate-a-reverse-dns-lookup-zone"></a><span data-ttu-id="d34bb-143">Een DNS-zone voor reverse lookup delegeren</span><span class="sxs-lookup"><span data-stu-id="d34bb-143">Delegate a reverse DNS lookup zone</span></span>

<span data-ttu-id="d34bb-144">Uw DNS-zone voor reverse lookup die worden gemaakt, moet u ervoor zorgen dat zone Hallo Hallo bovenliggende zone wordt gedelegeerd.</span><span class="sxs-lookup"><span data-stu-id="d34bb-144">Having created your reverse DNS lookup zone, you must ensure that hello zone is delegated from hello parent zone.</span></span> <span data-ttu-id="d34bb-145">DNS-delegering kunt Hallo DNS-proces toofind Hallo naam naamomzettingsservers die als host fungeert voor uw DNS-zone voor reverse lookup.</span><span class="sxs-lookup"><span data-stu-id="d34bb-145">DNS delegation enables hello DNS name resolution process toofind hello name servers hosting your reverse DNS lookup zone.</span></span> <span data-ttu-id="d34bb-146">Hierdoor is de naam servers tooanswer DNS-omgekeerde query's voor Hallo IP-adressen in uw-adresbereik.</span><span class="sxs-lookup"><span data-stu-id="d34bb-146">This enables those name servers tooanswer DNS reverse queries for hello IP addresses in your address range.</span></span>

<span data-ttu-id="d34bb-147">Voor zones voor forward lookup Hallo-proces voor het delegeren van een DNS-zone wordt beschreven in [delegeren van uw domein tooAzure DNS-](dns-delegate-domain-azure-dns.md).</span><span class="sxs-lookup"><span data-stu-id="d34bb-147">For forward lookup zones, hello process of delegating a DNS zone is described in [Delegate your domain tooAzure DNS](dns-delegate-domain-azure-dns.md).</span></span> <span data-ttu-id="d34bb-148">Zones voor reverse lookup-delegatie werkt Hallo dezelfde manier.</span><span class="sxs-lookup"><span data-stu-id="d34bb-148">Delegation for reverse lookup zones works hello same way.</span></span> <span data-ttu-id="d34bb-149">Hallo enige verschil is dat u moet het Hallo-naamservers tooconfigure Hello ISP die uw IP-adresbereik, in plaats van uw domeinnaamregistrar.</span><span class="sxs-lookup"><span data-stu-id="d34bb-149">hello only difference is that you need tooconfigure hello name servers with hello ISP who provided your IP range, rather than your domain name registrar.</span></span>

## <a name="create-a-dns-ptr-record"></a><span data-ttu-id="d34bb-150">Een DNS PTR-record maken</span><span class="sxs-lookup"><span data-stu-id="d34bb-150">Create a DNS PTR record</span></span>

### <a name="ipv4"></a><span data-ttu-id="d34bb-151">IPv4</span><span class="sxs-lookup"><span data-stu-id="d34bb-151">IPv4</span></span>

<span data-ttu-id="d34bb-152">Hallo wordt volgende voorbeeld u begeleid Hallo-proces voor het maken van een PTR-record in een reverse DNS-zone in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="d34bb-152">hello following example walks you through hello process of creating a PTR record in a reverse DNS zone in Azure DNS.</span></span> <span data-ttu-id="d34bb-153">Zie voor andere typen records en records van bestaande toomodify [beheren DNS-records en recordsets met behulp van Azure-portal Hallo](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d34bb-153">For other record types and toomodify existing records, see [Manage DNS records and record sets by using hello Azure portal](dns-operations-recordsets-portal.md).</span></span>

1.  <span data-ttu-id="d34bb-154">Hallo boven aan het Hallo **DNS-zone** blade Selecteer **+ Recordset** tooopen hello **recordset toevoegen** blade.</span><span class="sxs-lookup"><span data-stu-id="d34bb-154">At hello top of hello **DNS zone** blade, select **+ Record set** tooopen hello **Add record set** blade.</span></span>

 ![DNS-zone](./media/dns-reverse-dns-hosting/figure4.png)

1. <span data-ttu-id="d34bb-156">Op Hallo **recordset toevoegen** blade.</span><span class="sxs-lookup"><span data-stu-id="d34bb-156">On hello **Add record set** blade.</span></span> 
1. <span data-ttu-id="d34bb-157">Selecteer **PTR** uit Hallo record '**Type**' menu.</span><span class="sxs-lookup"><span data-stu-id="d34bb-157">Select **PTR** from hello record "**Type**" menu.</span></span>  
1. <span data-ttu-id="d34bb-158">Hallo de naam van de recordset Hallo voor een PTR-record moet toobe Hallo rest Hallo IPv4-adres in omgekeerde volgorde.</span><span class="sxs-lookup"><span data-stu-id="d34bb-158">hello name of hello record set for a PTR record needs toobe hello rest of hello IPv4 address in reverse order.</span></span> <span data-ttu-id="d34bb-159">In dit voorbeeld zijn hello eerste drie octetten al ingevuld als onderdeel van de naam van de zone hello (.2.0.192).</span><span class="sxs-lookup"><span data-stu-id="d34bb-159">In this example, hello first three octets are already populated as part of hello zone name (.2.0.192).</span></span> <span data-ttu-id="d34bb-160">Daarom wordt alleen Hallo laatste octet verstrekt in het naamveld Hallo.</span><span class="sxs-lookup"><span data-stu-id="d34bb-160">Therefore, only hello last octet is supplied in hello name field.</span></span> <span data-ttu-id="d34bb-161">U kunt uw recordset bijvoorbeeld de naam '**15**' voor een resource waarvan IP-adres 192.0.2.15 is.</span><span class="sxs-lookup"><span data-stu-id="d34bb-161">For example, you could name your record set "**15**" for a resource whose IP address is 192.0.2.15.</span></span>  
1. <span data-ttu-id="d34bb-162">In Hallo '**domeinnaam**' Voer Hallo volledig gekwalificeerde domeinnaam (FQDN) van Hallo resource via Hallo IP.</span><span class="sxs-lookup"><span data-stu-id="d34bb-162">In hello "**Domain Name**" field, enter hello fully qualified domain name (FQDN) of hello resource using hello IP.</span></span>
1. <span data-ttu-id="d34bb-163">Selecteer **OK** onderaan Hallo Hallo blade toocreate Hallo DNS-record.</span><span class="sxs-lookup"><span data-stu-id="d34bb-163">Select **OK** at hello bottom of hello blade toocreate hello DNS record.</span></span>

 ![recordset toevoegen](./media/dns-reverse-dns-hosting/figure5.png)

<span data-ttu-id="d34bb-165">Hallo hieronder vindt u voorbeelden van hoe toocomplete deze taak met PowerShell en Hallo AzureCLI:</span><span class="sxs-lookup"><span data-stu-id="d34bb-165">hello following are examples on how toocomplete this task with PowerShell and hello AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="d34bb-166">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d34bb-166">PowerShell</span></span>

```powershell
New-AzureRmDnsRecordSet -Name 15 -RecordType PTR -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc1.contoso.com")
```
#### <a name="azurecli-10"></a><span data-ttu-id="d34bb-167">AzureCLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d34bb-167">AzureCLI 1.0</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup 2.0.192.in-addr.arpa 15 PTR --ptrdname dc1.contoso.com  
```

#### <a name="azurecli-20"></a><span data-ttu-id="d34bb-168">AzureCLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d34bb-168">AzureCLI 2.0</span></span>

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 2.0.192.in-addr.arpa -n 15 --ptrdname dc1.contoso.com
```

### <a name="ipv6"></a><span data-ttu-id="d34bb-169">IPv6</span><span class="sxs-lookup"><span data-stu-id="d34bb-169">IPv6</span></span>

<span data-ttu-id="d34bb-170">Hallo volgende voorbeeld wordt u begeleid Hallo-proces voor het maken van nieuwe 'PTR-record.</span><span class="sxs-lookup"><span data-stu-id="d34bb-170">hello following example walks you through hello process of creating new 'PTR' record.</span></span> <span data-ttu-id="d34bb-171">Zie voor andere typen records en records van bestaande toomodify [beheren DNS-records en recordsets met behulp van Azure-portal Hallo](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d34bb-171">For other record types and toomodify existing records, see [Manage DNS records and record sets by using hello Azure portal](dns-operations-recordsets-portal.md).</span></span>

1. <span data-ttu-id="d34bb-172">Hallo boven aan het Hallo **DNS-zone blade**, selecteer **+ Recordset** tooopen hello **recordset toevoegen** blade.</span><span class="sxs-lookup"><span data-stu-id="d34bb-172">At hello top of hello **DNS zone blade**, select **+ Record set** tooopen hello **Add record set** blade.</span></span>

  ![DNS-zone-blade](./media/dns-reverse-dns-hosting/figure6.png)

2. <span data-ttu-id="d34bb-174">Op Hallo **recordset toevoegen** blade.</span><span class="sxs-lookup"><span data-stu-id="d34bb-174">On hello **Add record set** blade.</span></span> 
3. <span data-ttu-id="d34bb-175">Selecteer **PTR** uit Hallo record '**Type**' menu.</span><span class="sxs-lookup"><span data-stu-id="d34bb-175">Select **PTR** from hello record "**Type**" menu.</span></span>  
4. <span data-ttu-id="d34bb-176">Hallo de naam van de recordset Hallo voor een PTR-record moet toobe Hallo rest Hallo IPv6-adres in omgekeerde volgorde.</span><span class="sxs-lookup"><span data-stu-id="d34bb-176">hello name of hello record set for a PTR record needs toobe hello rest of hello IPv6 address in reverse order.</span></span> <span data-ttu-id="d34bb-177">Het mag geen nul gecomprimeerd bevatten.</span><span class="sxs-lookup"><span data-stu-id="d34bb-177">It must not include any zero compression.</span></span> <span data-ttu-id="d34bb-178">In dit voorbeeld Hallo eerste 64-bits Hallo IPv6 al zijn ingevuld als onderdeel van de naam van de zone hello (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa).</span><span class="sxs-lookup"><span data-stu-id="d34bb-178">In this example, hello first 64 bits of hello IPv6 are already populated as part of hello zone name (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa).</span></span> <span data-ttu-id="d34bb-179">Daarom alleen Hallo laatste 64 bits zijn opgegeven in het naamveld Hallo.</span><span class="sxs-lookup"><span data-stu-id="d34bb-179">Therefore, only hello last 64 bits are supplied in hello name field.</span></span> <span data-ttu-id="d34bb-180">Hallo laatste 64 bits van Hallo IP-adres worden ingevoerd in omgekeerde volgorde, met een punt als Hallo als scheidingsteken tussen elke hexadecimaal getal.</span><span class="sxs-lookup"><span data-stu-id="d34bb-180">hello last 64 bits of hello IP address are entered in reverse order, using a period as hello delimiter between each hexadecimal number.</span></span> <span data-ttu-id="d34bb-181">U kunt uw recordset bijvoorbeeld de naam '**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**' voor een resource waarvan IP-adres 2001:0db8:abdc:0000:f524:10bc:1af9:405e is.</span><span class="sxs-lookup"><span data-stu-id="d34bb-181">For example, you could name your record set "**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**" for a resource whose IP address is 2001:0db8:abdc:0000:f524:10bc:1af9:405e.</span></span>  
5. <span data-ttu-id="d34bb-182">In Hallo '**domeinnaam**' Voer Hallo volledig gekwalificeerde domeinnaam (FQDN) van Hallo resource via Hallo IP.</span><span class="sxs-lookup"><span data-stu-id="d34bb-182">In hello "**Domain Name**" field, enter hello fully qualified domain name (FQDN) of hello resource using hello IP.</span></span>
6. <span data-ttu-id="d34bb-183">Selecteer **OK** onderaan Hallo Hallo blade toocreate Hallo DNS-record.</span><span class="sxs-lookup"><span data-stu-id="d34bb-183">Select **OK** at hello bottom of hello blade toocreate hello DNS record.</span></span>

![Recordset blade toevoegen](./media/dns-reverse-dns-hosting/figure7.png)

<span data-ttu-id="d34bb-185">Hallo hieronder vindt u voorbeelden van hoe toocomplete deze taak met PowerShell en Hallo AzureCLI:</span><span class="sxs-lookup"><span data-stu-id="d34bb-185">hello following are examples on how toocomplete this task with PowerShell and hello AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="d34bb-186">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d34bb-186">PowerShell</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f" -RecordType PTR -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc2.contoso.com")
```

#### <a name="azurecli-10"></a><span data-ttu-id="d34bb-187">AzureCLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d34bb-187">AzureCLI 1.0</span></span>

```
azure network dns record-set add-record MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f PTR --ptrdname dc2.contoso.com 
```
 
#### <a name="azurecli-20"></a><span data-ttu-id="d34bb-188">AzureCLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d34bb-188">AzureCLI 2.0</span></span>

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -n e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f --ptrdname dc2.contoso.com
```

## <a name="view-records"></a><span data-ttu-id="d34bb-189">Records weergeven</span><span class="sxs-lookup"><span data-stu-id="d34bb-189">View Records</span></span>

<span data-ttu-id="d34bb-190">tooview hello records die u hebt gemaakt, gaat u tooyour DNS-zone in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="d34bb-190">tooview hello records you created, navigate tooyour DNS zone in hello Azure portal.</span></span> <span data-ttu-id="d34bb-191">In Hallo verlagen deel uit van Hallo **DNS-zone** blade ziet u Hallo-records voor Hallo DNS-zone.</span><span class="sxs-lookup"><span data-stu-id="d34bb-191">In hello lower part of hello **DNS zone** blade, you can see hello records for hello DNS zone.</span></span> <span data-ttu-id="d34bb-192">U ziet Hallo standaard NS en SOA-records, dat in elke zone worden gemaakt, plus eventuele nieuwe records die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d34bb-192">You should see hello default NS and SOA records, which are created in every zone, plus any new records you have created.</span></span>

### <a name="ipv4"></a><span data-ttu-id="d34bb-193">IPv4</span><span class="sxs-lookup"><span data-stu-id="d34bb-193">IPv4</span></span>

<span data-ttu-id="d34bb-194">DNS-zone blade IPv4 PTR-records worden weergegeven:</span><span class="sxs-lookup"><span data-stu-id="d34bb-194">DNS zone blade, showing IPv4 PTR records:</span></span>

![DNS-zone-blade](./media/dns-reverse-dns-hosting/figure8.png)

<span data-ttu-id="d34bb-196">Hello volgende voorbeelden laten zien hoe tooview Hallo PTR-records met PowerShell of Azure CLI Hallo:</span><span class="sxs-lookup"><span data-stu-id="d34bb-196">hello following examples show how tooview hello PTR records using PowerShell or hello Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="d34bb-197">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d34bb-197">PowerShell</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="d34bb-198">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d34bb-198">Azure CLI 1.0</span></span>

```azurecli
    azure network dns record-set list MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="d34bb-199">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d34bb-199">Azure CLI 2.0</span></span>

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a><span data-ttu-id="d34bb-200">IPv6</span><span class="sxs-lookup"><span data-stu-id="d34bb-200">IPv6</span></span>

<span data-ttu-id="d34bb-201">DNS-zone blade IPv6 PTR-records worden weergegeven:</span><span class="sxs-lookup"><span data-stu-id="d34bb-201">DNS zone blade, showing IPv6 PTR records:</span></span>

![DNS-zone-blade](./media/dns-reverse-dns-hosting/figure9.png)

<span data-ttu-id="d34bb-203">Hallo hieronder vindt u voorbeelden van hoe tooview Hallo met PowerShell en Hallo AzureCLI registreert:</span><span class="sxs-lookup"><span data-stu-id="d34bb-203">hello following are examples on how tooview hello records with PowerShell and hello AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="d34bb-204">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d34bb-204">PowerShell</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="d34bb-205">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d34bb-205">Azure CLI 1.0</span></span>

```azurecli
    azure network dns record-set list MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="d34bb-206">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d34bb-206">Azure CLI 2.0</span></span>

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="faq"></a><span data-ttu-id="d34bb-207">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="d34bb-207">FAQ</span></span>

### <a name="can-i-host-reverse-dns-lookup-zones-for-my-isp-assigned-ip-blocks-on-azure-dns"></a><span data-ttu-id="d34bb-208">Kan ik voor mijn ISP toegewezen IP-adresblokken op Azure DNS zones voor reverse DNS-lookup hosten?</span><span class="sxs-lookup"><span data-stu-id="d34bb-208">Can I host reverse DNS lookup zones for my ISP-assigned IP blocks on Azure DNS?</span></span>

<span data-ttu-id="d34bb-209">Ja.</span><span class="sxs-lookup"><span data-stu-id="d34bb-209">Yes.</span></span> <span data-ttu-id="d34bb-210">Zones voor reverse lookup (ARPA) Hallo maken voor uw eigen IP-adresbereiken in Azure DNS hosten wordt volledig ondersteund.</span><span class="sxs-lookup"><span data-stu-id="d34bb-210">Hosting hello reverse lookup (ARPA) zones for your own IP ranges in Azure DNS is fully supported.</span></span>

<span data-ttu-id="d34bb-211">Hallo-zone voor reverse lookup maakt in Azure DNS in dit artikel uitgelegd en vervolgens te werken met uw Internetprovider[gemachtigde Hallo zone](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="d34bb-211">Create hello reverse lookup zone in Azure DNS as explained in this article, then work with your ISP too[delegate hello zone](dns-domain-delegation.md).</span></span>  <span data-ttu-id="d34bb-212">U kunt Hallo PTR-records beheren voor elke reverse lookup in Hallo dezelfde manier als andere recordtypen.</span><span class="sxs-lookup"><span data-stu-id="d34bb-212">You can then manage hello PTR records for each reverse lookup in hello same way as other record types.</span></span>

### <a name="how-much-does-hosting-my-reverse-dns-lookup-zone-cost"></a><span data-ttu-id="d34bb-213">Hoeveel gebruikt die als host fungeert voor mijn omgekeerde DNS-lookup zone kosten?</span><span class="sxs-lookup"><span data-stu-id="d34bb-213">How much does hosting my reverse DNS lookup zone cost?</span></span>

<span data-ttu-id="d34bb-214">Hallo omgekeerde DNS-lookup zone als host fungeert voor uw Internetprovider toegewezen IP-Adresblok in Azure DNS in rekening volgens gebracht [standaardtarieven Azure DNS](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="d34bb-214">Hosting hello reverse DNS lookup zone for your ISP-assigned IP block in Azure DNS is charged at [standard Azure DNS rates](https://azure.microsoft.com/pricing/details/dns/).</span></span>

### <a name="can-i-host-reverse-dns-lookup-zones-for-both-ipv4-and-ipv6-addresses-in-azure-dns"></a><span data-ttu-id="d34bb-215">Kan ik zones voor reverse DNS-lookup voor IPv4 en IPv6-adressen in Azure DNS hosten?</span><span class="sxs-lookup"><span data-stu-id="d34bb-215">Can I host reverse DNS lookup zones for both IPv4 and IPv6 addresses in Azure DNS?</span></span>

<span data-ttu-id="d34bb-216">Ja.</span><span class="sxs-lookup"><span data-stu-id="d34bb-216">Yes.</span></span> <span data-ttu-id="d34bb-217">Dit artikel wordt uitgelegd hoe toocreate zowel IPv4 als IPv6-zones voor reverse DNS-lookup in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="d34bb-217">This article explains how toocreate both IPv4 and IPv6 reverse DNS lookup zones in Azure DNS.</span></span>

### <a name="can-i-import-an-existing-reverse-dns-lookup-zone"></a><span data-ttu-id="d34bb-218">Kan ik een bestaande zone voor reverse DNS-lookup importeren?</span><span class="sxs-lookup"><span data-stu-id="d34bb-218">Can I import an existing reverse DNS lookup zone?</span></span>

<span data-ttu-id="d34bb-219">Ja.</span><span class="sxs-lookup"><span data-stu-id="d34bb-219">Yes.</span></span> <span data-ttu-id="d34bb-220">U kunt hello Azure CLI tooimport bestaande DNS-zones in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="d34bb-220">You can use hello Azure CLI tooimport existing DNS zones into Azure DNS.</span></span> <span data-ttu-id="d34bb-221">Dit werkt voor zowel zones voor forward lookup en zones voor reverse lookup.</span><span class="sxs-lookup"><span data-stu-id="d34bb-221">This works for both forward lookup zones and reverse lookup zones.</span></span>

<span data-ttu-id="d34bb-222">Zie voor meer informatie [importeren en exporteren een DNS-zone-bestand met de Azure CLI Hallo](dns-import-export.md).</span><span class="sxs-lookup"><span data-stu-id="d34bb-222">For more information, see [Import and export a DNS zone file using hello Azure CLI](dns-import-export.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d34bb-223">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d34bb-223">Next steps</span></span>

<span data-ttu-id="d34bb-224">Zie voor meer informatie over omgekeerde DNS [achterwaartse DNS-zoekopdracht op Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span><span class="sxs-lookup"><span data-stu-id="d34bb-224">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="d34bb-225">Meer informatie over hoe te[omgekeerde DNS-records voor uw Azure-services beheren](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="d34bb-225">Learn how too[manage reverse DNS records for your Azure services](dns-reverse-dns-for-azure-services.md).</span></span>
