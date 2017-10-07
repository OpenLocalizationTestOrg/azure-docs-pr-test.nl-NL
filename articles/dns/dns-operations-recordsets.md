---
title: aaaManage DNS registreert in Azure DNS met Azure PowerShell | Microsoft Docs
description: Het beheren van DNS-recordsets en records op Azure DNS bij het hosten van uw Azure DNS-domein. Alle PowerShell-opdrachten voor bewerkingen op recordsets en records.
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 7136a373-0682-471c-9c28-9e00d2add9c2
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 12/21/2016
ms.author: gwallace
ms.openlocfilehash: bfdf116e174d06db0514abdc0ec3f4fc4ee0a079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-and-recordsets-in-azure-dns-using-azure-powershell"></a><span data-ttu-id="f91a4-104">DNS-records en recordsets in Azure DNS met Azure PowerShell beheren</span><span class="sxs-lookup"><span data-stu-id="f91a4-104">Manage DNS records and recordsets in Azure DNS using Azure PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f91a4-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f91a4-105">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="f91a4-106">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="f91a4-106">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="f91a4-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f91a4-107">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="f91a4-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f91a4-108">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="f91a4-109">Dit artikel laat zien hoe toomanage DNS registreert voor uw DNS-zone met behulp van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f91a4-109">This article shows you how toomanage DNS records for your DNS zone by using Azure PowerShell.</span></span> <span data-ttu-id="f91a4-110">DNS-records kunnen ook worden beheerd met behulp van de platformoverschrijdende Hallo [Azure CLI](dns-operations-recordsets-cli.md) of Hallo [Azure-portal](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f91a4-110">DNS records can also be managed by using hello cross-platform [Azure CLI](dns-operations-recordsets-cli.md) or hello [Azure portal](dns-operations-recordsets-portal.md).</span></span>

<span data-ttu-id="f91a4-111">Hallo-voorbeelden in dit artikel wordt ervan uitgegaan dat u al hebt [Azure PowerShell aangemeld, geïnstalleerd en wordt gemaakt van een DNS-zone](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="f91a4-111">hello examples in this article assume you have already [installed Azure PowerShell, signed in, and created a DNS zone](dns-operations-dnszones.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="f91a4-112">Inleiding</span><span class="sxs-lookup"><span data-stu-id="f91a4-112">Introduction</span></span>

<span data-ttu-id="f91a4-113">Voordat u DNS-records in Azure DNS maakt, moet u eerst de toounderstand hoe organiseert van DNS-records in DNS-recordsets in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="f91a4-113">Before creating DNS records in Azure DNS, you first need toounderstand how Azure DNS organizes DNS records into DNS record sets.</span></span>

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

<span data-ttu-id="f91a4-114">Zie [DNS-zones en -records](dns-zones-records.md) voor meer informatie over DNS-records in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="f91a4-114">For more information about DNS records in Azure DNS, see [DNS zones and records](dns-zones-records.md).</span></span>


## <a name="create-a-new-dns-record"></a><span data-ttu-id="f91a4-115">Maak een nieuwe DNS-record</span><span class="sxs-lookup"><span data-stu-id="f91a4-115">Create a new DNS record</span></span>

<span data-ttu-id="f91a4-116">Als uw nieuwe record Hallo dezelfde naam geven en typt u als een bestaande record heeft, moet u deze te[toe te voegen de bestaande recordset toohello](#add-a-record-to-an-existing-record-set).</span><span class="sxs-lookup"><span data-stu-id="f91a4-116">If your new record has hello same name and type as an existing record, you need too[add it toohello existing record set](#add-a-record-to-an-existing-record-set).</span></span> <span data-ttu-id="f91a4-117">Als uw nieuwe record een andere naam en type tooall bestaande records heeft, moet u een nieuwe recordset toocreate.</span><span class="sxs-lookup"><span data-stu-id="f91a4-117">If your new record has a different name and type tooall existing records, you need toocreate a new record set.</span></span> 

### <a name="create-a-records-in-a-new-record-set"></a><span data-ttu-id="f91a4-118">"A" records in een nieuwe recordset maken</span><span class="sxs-lookup"><span data-stu-id="f91a4-118">Create 'A' records in a new record set</span></span>

<span data-ttu-id="f91a4-119">U recordsets maakt met behulp van Hallo `New-AzureRmDnsRecordSet` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f91a4-119">You create record sets by using hello `New-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="f91a4-120">Bij het maken van een recordset moet u de naam van de recordset toospecify hello, Hallo zone, Hallo tijd toolive (TTL), het recordtype Hallo en Hallo records toobe gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f91a4-120">When creating a record set, you need toospecify hello record set name, hello zone, hello time toolive (TTL), hello record type, and hello records toobe created.</span></span>

<span data-ttu-id="f91a4-121">Hallo-parameters voor het toevoegen van records tooa recordset is afhankelijk van Hallo type Hallo Recordset.</span><span class="sxs-lookup"><span data-stu-id="f91a4-121">hello parameters for adding records tooa record set vary depending on hello type of hello record set.</span></span> <span data-ttu-id="f91a4-122">Bijvoorbeeld, wanneer u een recordset van het type "A", moet u toospecify Hallo IP-adres met de parameter Hallo `-IPv4Address`.</span><span class="sxs-lookup"><span data-stu-id="f91a4-122">For example, when using a record set of type 'A', you need toospecify hello IP address using hello parameter `-IPv4Address`.</span></span> <span data-ttu-id="f91a4-123">Andere parameters worden gebruikt voor andere typen records.</span><span class="sxs-lookup"><span data-stu-id="f91a4-123">Other parameters are used for other record types.</span></span> <span data-ttu-id="f91a4-124">Zie [voorbeelden van recordtypen aanvullende](#additional-record-type-examples) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f91a4-124">See [Additional record type examples](#additional-record-type-examples) for details.</span></span>

<span data-ttu-id="f91a4-125">Hallo wordt volgende voorbeeld een recordset met Hallo relatieve naam 'www' Hallo 'contoso.com' van DNS-Zone.</span><span class="sxs-lookup"><span data-stu-id="f91a4-125">hello following example creates a record set with hello relative name 'www' in hello DNS Zone 'contoso.com'.</span></span> <span data-ttu-id="f91a4-126">Hallo volledig gekwalificeerde naam van de recordset Hallo is 'www.contoso.com'.</span><span class="sxs-lookup"><span data-stu-id="f91a4-126">hello fully-qualified name of hello record set is 'www.contoso.com'.</span></span> <span data-ttu-id="f91a4-127">Hallo recordtype is "A" en Hallo TTL 3600 seconden is.</span><span class="sxs-lookup"><span data-stu-id="f91a4-127">hello record type is 'A', and hello TTL is 3600 seconds.</span></span> <span data-ttu-id="f91a4-128">Hallo-Recordset bevat één record, met IP-adres '1.2.3.4'.</span><span class="sxs-lookup"><span data-stu-id="f91a4-128">hello record set contains a single record, with IP address '1.2.3.4'.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

<span data-ttu-id="f91a4-129">toocreate een recordset op Hallo 'top' van een zone (in dit geval 'contoso.com'), gebruik de naam van Hallo Recordset ' @' (zonder aanhalingstekens):</span><span class="sxs-lookup"><span data-stu-id="f91a4-129">toocreate a record set at hello 'apex' of a zone (in this case, 'contoso.com'), use hello record set name '@' (excluding quotation marks):</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

<span data-ttu-id="f91a4-130">Als u een recordset met meer dan één record toocreate nodig, maakt eerst een lokale matrix en Hallo records toevoegen en Hallo matrix te geven`New-AzureRmDnsRecordSet` als volgt:</span><span class="sxs-lookup"><span data-stu-id="f91a4-130">If you need toocreate a record set containing more than one record, first create a local array and add hello records, then pass hello array too`New-AzureRmDnsRecordSet` as follows:</span></span>

```powershell
$aRecords = @()
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4"
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "2.3.4.5"
New-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName MyResourceGroup -Ttl 3600 -RecordType A -DnsRecords $aRecords
```

<span data-ttu-id="f91a4-131">[Metagegevens van de recordset](dns-zones-records.md#tags-and-metadata) mag gebruikte tooassociate toepassingsspecifieke gegevens met elke recordset als sleutel-waardeparen.</span><span class="sxs-lookup"><span data-stu-id="f91a4-131">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used tooassociate application-specific data with each record set, as key-value pairs.</span></span> <span data-ttu-id="f91a4-132">Hallo volgende voorbeeld laat zien hoe toocreate een recordset met twee metagegevensvermeldingen ' afdeling Financiën =' en ' omgeving productie ='.</span><span class="sxs-lookup"><span data-stu-id="f91a4-132">hello following example shows how toocreate a record set with two metadata entries, 'dept=finance' and 'environment=production'.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") -Metadata @{ dept="finance"; environment="production" } 
```

<span data-ttu-id="f91a4-133">Azure DNS ondersteunt ook 'empty' recordsets die als een tijdelijke aanduiding voor tooreserve een DNS-naam optreden kunnen voor het maken van DNS-records.</span><span class="sxs-lookup"><span data-stu-id="f91a4-133">Azure DNS also supports 'empty' record sets, which can act as a placeholder tooreserve a DNS name before creating DNS records.</span></span> <span data-ttu-id="f91a4-134">Lege recordsets zijn zichtbaar in hello Azure DNS besturingselement vlak, maar worden weergegeven op Hallo Azure DNS-naamservers.</span><span class="sxs-lookup"><span data-stu-id="f91a4-134">Empty record sets are visible in hello Azure DNS control plane, but do appear on hello Azure DNS name servers.</span></span> <span data-ttu-id="f91a4-135">Hallo volgende voorbeeld wordt een lege recordset gemaakt:</span><span class="sxs-lookup"><span data-stu-id="f91a4-135">hello following example creates an empty record set:</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords @()
```

## <a name="create-records-of-other-types"></a><span data-ttu-id="f91a4-136">Records van andere typen maken</span><span class="sxs-lookup"><span data-stu-id="f91a4-136">Create records of other types</span></span>

<span data-ttu-id="f91a4-137">Hebben gezien in detail hoe toocreate "A" registreert, Hallo volgen voorbeelden kunt u zien hoe toocreate records van andere typen die worden ondersteund door Azure DNS registreren.</span><span class="sxs-lookup"><span data-stu-id="f91a4-137">Having seen in detail how toocreate 'A' records, hello following examples show how toocreate records of other record types supported by Azure DNS.</span></span>

<span data-ttu-id="f91a4-138">In elk geval laten we zien hoe een record toocreate instelt met een enkel record.</span><span class="sxs-lookup"><span data-stu-id="f91a4-138">In each case, we show how toocreate a record set containing a single record.</span></span> <span data-ttu-id="f91a4-139">Hallo eerdere voorbeelden voor "A" records kunnen worden aangepast toocreate recordsets van andere typen met meerdere records met metagegevens, of lege record toocreate ingesteld.</span><span class="sxs-lookup"><span data-stu-id="f91a4-139">hello earlier examples for 'A' records can be adapted toocreate record sets of other types containing multiple records, with metadata, or toocreate empty record sets.</span></span>

<span data-ttu-id="f91a4-140">We geven geen een toocreate bijvoorbeeld een recordset SOA-sinds SOA's zijn gemaakt en verwijderd met elke DNS-zone en kan niet worden gemaakt of afzonderlijk worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="f91a4-140">We do not give an example toocreate an SOA record set, since SOAs are created and deleted with each DNS zone and cannot be created or deleted separately.</span></span> <span data-ttu-id="f91a4-141">Echter, [Hallo SOA kan worden gewijzigd, zoals wordt weergegeven in het voorbeeld van een hoger](#to-modify-an-SOA-record).</span><span class="sxs-lookup"><span data-stu-id="f91a4-141">However, [hello SOA can be modified, as shown in a later example](#to-modify-an-SOA-record).</span></span>

### <a name="create-an-aaaa-record-set-with-a-single-record"></a><span data-ttu-id="f91a4-142">Een AAAA-recordset met één record maken</span><span class="sxs-lookup"><span data-stu-id="f91a4-142">Create an AAAA record set with a single record</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-aaaa" -RecordType AAAA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ipv6Address "2607:f8b0:4009:1803::1005") 
```

### <a name="create-a-cname-record-set-with-a-single-record"></a><span data-ttu-id="f91a4-143">Een CNAME-recordset met één record maken</span><span class="sxs-lookup"><span data-stu-id="f91a4-143">Create a CNAME record set with a single record</span></span>

> [!NOTE]
> <span data-ttu-id="f91a4-144">Hallo DNS-standaarden staan niet toe dat CNAME-records in het toppunt van Hallo van een zone (`-Name '@'`), noch staan ze recordsets met meer dan één record.</span><span class="sxs-lookup"><span data-stu-id="f91a4-144">hello DNS standards do not permit CNAME records at hello apex of a zone (`-Name '@'`), nor do they permit record sets containing more than one record.</span></span>
> 
> <span data-ttu-id="f91a4-145">Zie voor meer informatie [CNAME-records](dns-zones-records.md#cname-records).</span><span class="sxs-lookup"><span data-stu-id="f91a4-145">For more information, see [CNAME records](dns-zones-records.md#cname-records).</span></span>


```powershell
New-AzureRmDnsRecordSet -Name "test-cname" -RecordType CNAME -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Cname "www.contoso.com") 
```

### <a name="create-an-mx-record-set-with-a-single-record"></a><span data-ttu-id="f91a4-146">Een MX-recordset met één record maken</span><span class="sxs-lookup"><span data-stu-id="f91a4-146">Create an MX record set with a single record</span></span>

<span data-ttu-id="f91a4-147">In dit voorbeeld gebruiken we Hallo recordnaam ' @' toocreate een MX-record in het toppunt Hallo zone (in dit geval 'contoso.com').</span><span class="sxs-lookup"><span data-stu-id="f91a4-147">In this example, we use hello record set name '@' toocreate an MX record at hello zone apex (in this case, 'contoso.com').</span></span>


```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType MX -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Exchange "mail.contoso.com" -Preference 5) 
```

### <a name="create-an-ns-record-set-with-a-single-record"></a><span data-ttu-id="f91a4-148">Een NS-recordset met één record maken</span><span class="sxs-lookup"><span data-stu-id="f91a4-148">Create an NS record set with a single record</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-ns" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Nsdname "ns1.contoso.com") 
```

### <a name="create-a-ptr-record-set-with-a-single-record"></a><span data-ttu-id="f91a4-149">Een PTR-recordset met één record maken</span><span class="sxs-lookup"><span data-stu-id="f91a4-149">Create a PTR record set with a single record</span></span>

<span data-ttu-id="f91a4-150">In dit geval ' Mijn-arpa-zone.com' vertegenwoordigt Hallo ARPA zone voor reverse lookup voor uw IP-adresbereik.</span><span class="sxs-lookup"><span data-stu-id="f91a4-150">In this case, 'my-arpa-zone.com' represents hello ARPA reverse lookup zone representing your IP range.</span></span> <span data-ttu-id="f91a4-151">Elke PTR-recordset in deze zone komt overeen tooan IP-adres binnen deze IP-adresbereik.</span><span class="sxs-lookup"><span data-stu-id="f91a4-151">Each PTR record set in this zone corresponds tooan IP address within this IP range.</span></span> <span data-ttu-id="f91a4-152">Hallo recordnaam "10" is de laatste octet Hallo van Hallo IP-adres binnen deze IP-bereik dat wordt vertegenwoordigd door deze record.</span><span class="sxs-lookup"><span data-stu-id="f91a4-152">hello record name '10' is hello last octet of hello IP address within this IP range represented by this record.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name 10 -RecordType PTR -ZoneName "my-arpa-zone.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "myservice.contoso.com") 
```

### <a name="create-an-srv-record-set-with-a-single-record"></a><span data-ttu-id="f91a4-153">Een SRV-recordset met één record maken</span><span class="sxs-lookup"><span data-stu-id="f91a4-153">Create an SRV record set with a single record</span></span>

<span data-ttu-id="f91a4-154">Bij het maken van een [SRV-Recordset](dns-zones-records.md#srv-records), geef Hallo  *\_service* en  *\_protocol* in Hallo-of RecordsetNaam.</span><span class="sxs-lookup"><span data-stu-id="f91a4-154">When creating an [SRV record set](dns-zones-records.md#srv-records), specify hello *\_service* and *\_protocol* in hello record set name.</span></span> <span data-ttu-id="f91a4-155">Er is geen tooinclude moet ' @' in hello RecordsetNaam wanneer een SRV-record maken in het toppunt zone Hallo ingesteld.</span><span class="sxs-lookup"><span data-stu-id="f91a4-155">There is no need tooinclude '@' in hello record set name when creating an SRV record set at hello zone apex.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "_sip._tls" -RecordType SRV -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Priority 0 -Weight 5 -Port 8080 -Target "sip.contoso.com") 
```


### <a name="create-a-txt-record-set-with-a-single-record"></a><span data-ttu-id="f91a4-156">Een TXT-recordset met één record maken</span><span class="sxs-lookup"><span data-stu-id="f91a4-156">Create a TXT record set with a single record</span></span>

<span data-ttu-id="f91a4-157">Hallo volgende voorbeeld ziet u hoe een TXT-toocreate opnemen.</span><span class="sxs-lookup"><span data-stu-id="f91a4-157">hello following example shows how toocreate a TXT record.</span></span> <span data-ttu-id="f91a4-158">Zie voor meer informatie over de maximale tekenreekslengte hello wordt ondersteund in de TXT-records [TXT-records](dns-zones-records.md#txt-records).</span><span class="sxs-lookup"><span data-stu-id="f91a4-158">For more information about hello maximum string length supported in TXT records, see [TXT records](dns-zones-records.md#txt-records).</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-txt" -RecordType TXT -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Value "This is a TXT record") 
```


## <a name="get-a-record-set"></a><span data-ttu-id="f91a4-159">Een recordset ophalen</span><span class="sxs-lookup"><span data-stu-id="f91a4-159">Get a record set</span></span>

<span data-ttu-id="f91a4-160">Gebruik een bestaande recordset tooretrieve `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="f91a4-160">tooretrieve an existing record set, use `Get-AzureRmDnsRecordSet`.</span></span> <span data-ttu-id="f91a4-161">Deze cmdlet retourneert een lokaal object met Hallo-recordset in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="f91a4-161">This cmdlet returns a local object that represents hello record set in Azure DNS.</span></span>

<span data-ttu-id="f91a4-162">Net als bij `New-AzureRmDnsRecordSet`, krijgt de naam van de Hallo recordset moet een *relatieve* naam, wat betekent dat het Hallo-zonenaam moet uitsluiten.</span><span class="sxs-lookup"><span data-stu-id="f91a4-162">As with `New-AzureRmDnsRecordSet`, hello record set name given must be a *relative* name, meaning it must exclude hello zone name.</span></span> <span data-ttu-id="f91a4-163">U moet ook toospecify Hallo recordtype en Hallo-recordset met Hallo-zone.</span><span class="sxs-lookup"><span data-stu-id="f91a4-163">You also need toospecify hello record type, and hello zone containing hello record set.</span></span>

<span data-ttu-id="f91a4-164">Hallo ziet volgende voorbeeld u hoe tooretrieve een record instellen.</span><span class="sxs-lookup"><span data-stu-id="f91a4-164">hello following example shows how tooretrieve a record set.</span></span> <span data-ttu-id="f91a4-165">In dit voorbeeld Hallo zone is opgegeven met behulp van Hallo `-ZoneName` en `-ResourceGroupName` parameters.</span><span class="sxs-lookup"><span data-stu-id="f91a4-165">In this example, hello zone is specified using hello `-ZoneName` and `-ResourceGroupName` parameters.</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="f91a4-166">U kunt ook u kunt ook opgeven met behulp van een zone-object dat is doorgegeven met Hallo Hallo-zone `-Zone` parameter.</span><span class="sxs-lookup"><span data-stu-id="f91a4-166">Alternatively, you can also specify hello zone using a zone object, passed using hello `-Zone` parameter.</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

## <a name="list-record-sets"></a><span data-ttu-id="f91a4-167">Lijst met recordsets</span><span class="sxs-lookup"><span data-stu-id="f91a4-167">List record sets</span></span>

<span data-ttu-id="f91a4-168">U kunt ook `Get-AzureRmDnsZone` toolist recordsets in een zone door Hallo weg te laten `-Name` en/of `-RecordType` parameters.</span><span class="sxs-lookup"><span data-stu-id="f91a4-168">You can also use `Get-AzureRmDnsZone` toolist record sets in a zone, by omitting hello `-Name` and/or `-RecordType` parameters.</span></span>

<span data-ttu-id="f91a4-169">Hallo retourneert volgende voorbeeld alle recordsets in Hallo zone:</span><span class="sxs-lookup"><span data-stu-id="f91a4-169">hello following example returns all record sets in hello zone:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="f91a4-170">Hallo volgende voorbeeld ziet u hoe-alle recordsets van een bepaald type kunnen worden opgehaald door te geven Hallo recordtype terwijl weglaten Hallo record naam instellen:</span><span class="sxs-lookup"><span data-stu-id="f91a4-170">hello following example shows how all record sets of a given type can be retrieved by specifying hello record type while omitting hello record set name:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="f91a4-171">alle recordsets met een opgegeven naam tooretrieve over recordtypen, moet u tooretrieve alle recordsets en vervolgens filter Hallo resultaten:</span><span class="sxs-lookup"><span data-stu-id="f91a4-171">tooretrieve all record sets with a given name, across record types, you need tooretrieve all record sets and then filter hello results:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | where {$_.Name.Equals("www")}
```

<span data-ttu-id="f91a4-172">In alle Hallo bovenstaande voorbeelden Hallo zone worden opgegeven met behulp van Hallo `-ZoneName` en `-ResourceGroupName`parameters (zoals weergegeven), of door te geven van een zone-object:</span><span class="sxs-lookup"><span data-stu-id="f91a4-172">In all hello above examples, hello zone can be specified either by using hello `-ZoneName` and `-ResourceGroupName`parameters (as shown), or by specifying a zone object:</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$recordsets = Get-AzureRmDnsRecordSet -Zone $zone
```

## <a name="add-a-record-tooan-existing-record-set"></a><span data-ttu-id="f91a4-173">Een record tooan bestaande recordset toevoegen</span><span class="sxs-lookup"><span data-stu-id="f91a4-173">Add a record tooan existing record set</span></span>

<span data-ttu-id="f91a4-174">een bestaande record record tooan tooadd instellen, voert u Hallo drie stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f91a4-174">tooadd a record tooan existing record set, follow hello following three steps:</span></span>

1. <span data-ttu-id="f91a4-175">De bestaande recordset Hallo ophalen</span><span class="sxs-lookup"><span data-stu-id="f91a4-175">Get hello existing record set</span></span>

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. <span data-ttu-id="f91a4-176">Hallo nieuwe records toohello lokale recordset toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f91a4-176">Add hello new record toohello local record set.</span></span> <span data-ttu-id="f91a4-177">Dit is een offline-bewerking.</span><span class="sxs-lookup"><span data-stu-id="f91a4-177">This is an off-line operation.</span></span>

    ```powershell
    Add-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. <span data-ttu-id="f91a4-178">Hallo wijziging back toohello Azure DNS-service worden doorgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f91a4-178">Commit hello change back toohello Azure DNS service.</span></span> 

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $rs
    ```

<span data-ttu-id="f91a4-179">Met behulp van `Set-AzureRmDnsRecordSet` *vervangt* Hallo bestaande recordset in Azure DNS (en alle records die deze bevat) met opgegeven Hallo-Recordset.</span><span class="sxs-lookup"><span data-stu-id="f91a4-179">Using `Set-AzureRmDnsRecordSet` *replaces* hello existing record set in Azure DNS (and all records it contains) with hello record set specified.</span></span> <span data-ttu-id="f91a4-180">[ETag controles](dns-zones-records.md#etags) worden gebruikt tooensure gelijktijdige wijzigingen worden niet overschreven.</span><span class="sxs-lookup"><span data-stu-id="f91a4-180">[Etag checks](dns-zones-records.md#etags) are used tooensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="f91a4-181">U kunt optioneel Hallo `-Overwrite` overschakelen toosuppress deze controles.</span><span class="sxs-lookup"><span data-stu-id="f91a4-181">You can use hello optional `-Overwrite` switch toosuppress these checks.</span></span>

<span data-ttu-id="f91a4-182">Deze reeks bewerkingen kan ook worden *doorgesluisd*, wat betekent dat u Hallo Recordset object Hallo pipe gebruiken in plaats van deze doorgegeven als parameter doorgeven:</span><span class="sxs-lookup"><span data-stu-id="f91a4-182">This sequence of operations can also be *piped*, meaning you pass hello record set object by using hello pipe rather than passing it as a parameter:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name "www" –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Add-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

<span data-ttu-id="f91a4-183">Hallo voorbeelden bovenstaande van hoe tooadd een "A" bestaande record tooan-record van het type "A" instellen.</span><span class="sxs-lookup"><span data-stu-id="f91a4-183">hello examples above show how tooadd an 'A' record tooan existing record set of type 'A'.</span></span> <span data-ttu-id="f91a4-184">Een vergelijkbare reeks bewerkingen is gebruikte tooadd recordsets toorecord van andere typen, vervangen door Hallo `-Ipv4Address` parameter van `Add-AzureRmDnsRecordConfig` met andere parameters specifieke tooeach-recordtype.</span><span class="sxs-lookup"><span data-stu-id="f91a4-184">A similar sequence of operations is used tooadd records toorecord sets of other types, substituting hello `-Ipv4Address` parameter of `Add-AzureRmDnsRecordConfig` with other parameters specific tooeach record type.</span></span> <span data-ttu-id="f91a4-185">Hallo parameters voor elk recordtype zijn Hallo dezelfde als voor Hallo `New-AzureRmDnsRecordConfig` cmdlet, zoals wordt weergegeven in [voorbeelden van recordtypen aanvullende](#additional-record-type-examples) hierboven.</span><span class="sxs-lookup"><span data-stu-id="f91a4-185">hello parameters for each record type are hello same as for hello `New-AzureRmDnsRecordConfig` cmdlet, as shown in [Additional record type examples](#additional-record-type-examples) above.</span></span>

<span data-ttu-id="f91a4-186">Recordsets van het type 'CNAME-' of 'SOA' mag niet meer dan een record bevatten.</span><span class="sxs-lookup"><span data-stu-id="f91a4-186">Record sets of type 'CNAME' or 'SOA' cannot contain more than one record.</span></span> <span data-ttu-id="f91a4-187">Deze beperking voortvloeit uit Hallo DNS-standaarden.</span><span class="sxs-lookup"><span data-stu-id="f91a4-187">This constraint arises from hello DNS standards.</span></span> <span data-ttu-id="f91a4-188">Het is niet een beperking van Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="f91a4-188">It is not a limitation of Azure DNS.</span></span>

## <a name="remove-a-record-from-an-existing-record-set"></a><span data-ttu-id="f91a4-189">Een record verwijderen uit een bestaande recordset</span><span class="sxs-lookup"><span data-stu-id="f91a4-189">Remove a record from an existing record set</span></span>

<span data-ttu-id="f91a4-190">Hallo proces tooremove een record van een recordset is vergelijkbaar toohello proces tooadd een record tooan bestaande recordset:</span><span class="sxs-lookup"><span data-stu-id="f91a4-190">hello process tooremove a record from a record set is similar toohello process tooadd a record tooan existing record set:</span></span>

1. <span data-ttu-id="f91a4-191">De bestaande recordset Hallo ophalen</span><span class="sxs-lookup"><span data-stu-id="f91a4-191">Get hello existing record set</span></span>

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. <span data-ttu-id="f91a4-192">Hallo-record verwijderen uit het Hallo lokale Recordset-object.</span><span class="sxs-lookup"><span data-stu-id="f91a4-192">Remove hello record from hello local record set object.</span></span> <span data-ttu-id="f91a4-193">Dit is een offline-bewerking.</span><span class="sxs-lookup"><span data-stu-id="f91a4-193">This is an off-line operation.</span></span> <span data-ttu-id="f91a4-194">Hallo-record die wordt verwijderd moet een exacte overeenkomst aan een bestaande record binnen alle parameters.</span><span class="sxs-lookup"><span data-stu-id="f91a4-194">hello record that's being removed must be an exact match with an existing record across all parameters.</span></span>

    ```powershell
    Remove-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. <span data-ttu-id="f91a4-195">Hallo wijziging back toohello Azure DNS-service worden doorgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f91a4-195">Commit hello change back toohello Azure DNS service.</span></span> <span data-ttu-id="f91a4-196">Gebruik Hallo optionele `-Overwrite` overschakelen toosuppress [Etag controleert](dns-zones-records.md#etags) voor gelijktijdige wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="f91a4-196">Use hello optional `-Overwrite` switch toosuppress [Etag checks](dns-zones-records.md#etags) for concurrent changes.</span></span>

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $Rs
    ```

<span data-ttu-id="f91a4-197">Met behulp van Hallo hierboven sequence tooremove Hallo laatste record van een recordset Hallo recordset niet verwijderen, in plaats daarvan het verlaten van een lege recordset.</span><span class="sxs-lookup"><span data-stu-id="f91a4-197">Using hello above sequence tooremove hello last record from a record set does not delete hello record set, rather it leaves an empty record set.</span></span> <span data-ttu-id="f91a4-198">een recordset volledig, tooremove Zie [verwijderen van een recordset](#delete-a-record-set).</span><span class="sxs-lookup"><span data-stu-id="f91a4-198">tooremove a record set entirely, see [Delete a record set](#delete-a-record-set).</span></span>

<span data-ttu-id="f91a4-199">Op dezelfde manier Recordset tooadding records tooa, Hallo reeks operations tooremove een recordset kan ook worden doorgesluisd:</span><span class="sxs-lookup"><span data-stu-id="f91a4-199">Similarly tooadding records tooa record set, hello sequence of operations tooremove a record set can also be piped:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Remove-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

<span data-ttu-id="f91a4-200">Verschillende recordtypen worden ondersteund door het doorgeven van het juiste type-specifieke parameters hello te`Remove-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="f91a4-200">Different record types are supported by passing hello appropriate type-specific parameters too`Remove-AzureRmDnsRecordSet`.</span></span> <span data-ttu-id="f91a4-201">Hallo parameters voor elk recordtype zijn Hallo dezelfde als voor Hallo `New-AzureRmDnsRecordConfig` cmdlet, zoals wordt weergegeven in [voorbeelden van recordtypen aanvullende](#additional-record-type-examples) hierboven.</span><span class="sxs-lookup"><span data-stu-id="f91a4-201">hello parameters for each record type are hello same as for hello `New-AzureRmDnsRecordConfig` cmdlet, as shown in [Additional record type examples](#additional-record-type-examples) above.</span></span>


## <a name="modify-an-existing-record-set"></a><span data-ttu-id="f91a4-202">Een bestaande recordset wijzigen</span><span class="sxs-lookup"><span data-stu-id="f91a4-202">Modify an existing record set</span></span>

<span data-ttu-id="f91a4-203">Hallo-stappen voor het wijzigen van een bestaande recordset zijn vergelijkbaar toohello stappen bij het toevoegen of verwijderen van records uit een Recordset:</span><span class="sxs-lookup"><span data-stu-id="f91a4-203">hello steps for modifying an existing record set are similar toohello steps you take when adding or removing records from a record set:</span></span>

1. <span data-ttu-id="f91a4-204">Ophalen van de bestaande record Hallo ingesteld met behulp van `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="f91a4-204">Retrieve hello existing record set by using `Get-AzureRmDnsRecordSet`.</span></span>
2. <span data-ttu-id="f91a4-205">Hallo lokale Recordset object door te wijzigen:</span><span class="sxs-lookup"><span data-stu-id="f91a4-205">Modify hello local record set object by:</span></span>
    * <span data-ttu-id="f91a4-206">Het toevoegen of verwijderen van records</span><span class="sxs-lookup"><span data-stu-id="f91a4-206">Adding or removing records</span></span>
    * <span data-ttu-id="f91a4-207">Hallo-parameters van bestaande records wijzigen</span><span class="sxs-lookup"><span data-stu-id="f91a4-207">Changing hello parameters of existing records</span></span>
    * <span data-ttu-id="f91a4-208">Het wijzigen van de record Hallo ingesteld metagegevens en toolive TTL (time)</span><span class="sxs-lookup"><span data-stu-id="f91a4-208">Changing hello record set metadata and time toolive (TTL)</span></span>
3. <span data-ttu-id="f91a4-209">Uw wijzigingen met behulp van Hallo `Set-AzureRmDnsRecordSet` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f91a4-209">Commit your changes by using hello `Set-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="f91a4-210">Dit *vervangt* Hallo bestaande recordset in Azure DNS met Hallo-recordset is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="f91a4-210">This *replaces* hello existing record set in Azure DNS with hello record set specified.</span></span>

<span data-ttu-id="f91a4-211">Wanneer u `Set-AzureRmDnsRecordSet`, [Etag controleert](dns-zones-records.md#etags) worden gebruikt tooensure gelijktijdige wijzigingen worden niet overschreven.</span><span class="sxs-lookup"><span data-stu-id="f91a4-211">When using `Set-AzureRmDnsRecordSet`, [Etag checks](dns-zones-records.md#etags) are used tooensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="f91a4-212">U kunt optioneel Hallo `-Overwrite` overschakelen toosuppress deze controles.</span><span class="sxs-lookup"><span data-stu-id="f91a4-212">You can use hello optional `-Overwrite` switch toosuppress these checks.</span></span>

### <a name="tooupdate-a-record-in-an-existing-record-set"></a><span data-ttu-id="f91a4-213">een record in een bestaande record tooupdate instellen</span><span class="sxs-lookup"><span data-stu-id="f91a4-213">tooupdate a record in an existing record set</span></span>

<span data-ttu-id="f91a4-214">In dit voorbeeld wijzigen we Hallo IP-adres van een bestaande "A" record:</span><span class="sxs-lookup"><span data-stu-id="f91a4-214">In this example, we change hello IP address of an existing 'A' record:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Ipv4Address = "9.8.7.6"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-an-soa-record"></a><span data-ttu-id="f91a4-215">toomodify SOA-record</span><span class="sxs-lookup"><span data-stu-id="f91a4-215">toomodify an SOA record</span></span>

<span data-ttu-id="f91a4-216">U kunt toevoegen of verwijderen van records uit Hallo automatisch gemaakt SOA-record is ingesteld in het toppunt Hallo zone (`-Name "@"`, inclusief de aanhalingstekens).</span><span class="sxs-lookup"><span data-stu-id="f91a4-216">You cannot add or remove records from hello automatically created SOA record set at hello zone apex (`-Name "@"`, including quote marks).</span></span> <span data-ttu-id="f91a4-217">Echter kunt u een van de parameters Hallo binnen Hallo SOA-record (met uitzondering van de "Host") en de TTL van de recordset Hallo.</span><span class="sxs-lookup"><span data-stu-id="f91a4-217">However, you can modify any of hello parameters within hello SOA record (except "Host") and hello record set TTL.</span></span>

<span data-ttu-id="f91a4-218">Hallo volgende voorbeeld wordt getoond hoe toochange hello *e* eigenschap Hallo SOA-record:</span><span class="sxs-lookup"><span data-stu-id="f91a4-218">hello following example shows how toochange hello *Email* property of hello SOA record:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType SOA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Email = "admin.contoso.com"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-ns-records-at-hello-zone-apex"></a><span data-ttu-id="f91a4-219">toomodify NS-records in het toppunt Hallo zone</span><span class="sxs-lookup"><span data-stu-id="f91a4-219">toomodify NS records at hello zone apex</span></span>

<span data-ttu-id="f91a4-220">Hallo NS-recordset in het toppunt Hallo zone wordt automatisch gemaakt met elke DNS-zone.</span><span class="sxs-lookup"><span data-stu-id="f91a4-220">hello NS record set at hello zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="f91a4-221">Het bevat Hallo-namen van hello Azure DNS-naam servers toegewezen toohello zone.</span><span class="sxs-lookup"><span data-stu-id="f91a4-221">It contains hello names of hello Azure DNS name servers assigned toohello zone.</span></span>

<span data-ttu-id="f91a4-222">U kunt de naam van de aanvullende servers toothis NS-recordset, toosupport CO domeinen met meer dan één DNS-provider host toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f91a4-222">You can add additional name servers toothis NS record set, toosupport co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="f91a4-223">U kunt ook wijzigen Hallo TTL en metagegevens voor deze recordset.</span><span class="sxs-lookup"><span data-stu-id="f91a4-223">You can also modify hello TTL and metadata for this record set.</span></span> <span data-ttu-id="f91a4-224">U kan echter verwijderen of wijzigen Hallo vooraf ingestelde Azure DNS-naamservers.</span><span class="sxs-lookup"><span data-stu-id="f91a4-224">However, you cannot remove or modify hello pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="f91a4-225">Houd er rekening mee dat dit alleen toohello NS recordset in het toppunt zone Hallo geldt.</span><span class="sxs-lookup"><span data-stu-id="f91a4-225">Note that this applies only toohello NS record set at hello zone apex.</span></span> <span data-ttu-id="f91a4-226">Andere NS recordsets in de zone (als gebruikte toodelegate onderliggende zones) kunnen worden gewijzigd zonder beperking.</span><span class="sxs-lookup"><span data-stu-id="f91a4-226">Other NS record sets in your zone (as used toodelegate child zones) can be modified without constraint.</span></span>

<span data-ttu-id="f91a4-227">Hallo volgende voorbeeld ziet u hoe tooadd een extra naam server toohello NS-record instellen in het toppunt Hallo zone:</span><span class="sxs-lookup"><span data-stu-id="f91a4-227">hello following example shows how tooadd an additional name server toohello NS record set at hello zone apex:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Add-AzureRmDnsRecordConfig -RecordSet $rs -Nsdname ns1.myotherdnsprovider.com
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-record-set-metadata"></a><span data-ttu-id="f91a4-228">metagegevens van de recordset toomodify</span><span class="sxs-lookup"><span data-stu-id="f91a4-228">toomodify record set metadata</span></span>

<span data-ttu-id="f91a4-229">[Metagegevens van de recordset](dns-zones-records.md#tags-and-metadata) mag gebruikte tooassociate toepassingsspecifieke gegevens met elke recordset als sleutel-waardeparen.</span><span class="sxs-lookup"><span data-stu-id="f91a4-229">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used tooassociate application-specific data with each record set, as key-value pairs.</span></span>

<span data-ttu-id="f91a4-230">Hallo ziet volgende voorbeeld u hoe toomodify Hallo metagegevens van een bestaande record instellen:</span><span class="sxs-lookup"><span data-stu-id="f91a4-230">hello following example shows how toomodify hello metadata of an existing record set:</span></span>

```powershell
# Get hello record set
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"

# Add 'dept=finance' name-value pair
$rs.Metadata.Add('dept', 'finance') 

# Remove metadata item named 'environment'
$rs.Metadata.Remove('environment')  

# Commit changes
Set-AzureRmDnsRecordSet -RecordSet $rs
```


## <a name="delete-a-record-set"></a><span data-ttu-id="f91a4-231">Een recordset verwijderen</span><span class="sxs-lookup"><span data-stu-id="f91a4-231">Delete a record set</span></span>

<span data-ttu-id="f91a4-232">Recordsets kunnen worden verwijderd met behulp van Hallo `Remove-AzureRmDnsRecordSet` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f91a4-232">Record sets can be deleted by using hello `Remove-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="f91a4-233">Een recordset te verwijderen, verwijdert tevens alle records in de recordset Hallo.</span><span class="sxs-lookup"><span data-stu-id="f91a4-233">Deleting a record set also deletes all records within hello record set.</span></span>

> [!NOTE]
> <span data-ttu-id="f91a4-234">U kunt geen Hallo SOA- en NS-recordsets in het toppunt Hallo zone verwijderen (`-Name '@'`).</span><span class="sxs-lookup"><span data-stu-id="f91a4-234">You cannot delete hello SOA and NS record sets at hello zone apex (`-Name '@'`).</span></span>  <span data-ttu-id="f91a4-235">Deze wordt automatisch door Azure DNS gemaakt wanneer Hallo zone is gemaakt en worden automatisch verwijderd wanneer Hallo zone wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="f91a4-235">Azure DNS created these automatically when hello zone was created, and deletes them automatically when hello zone is deleted.</span></span>

<span data-ttu-id="f91a4-236">Hallo ziet volgende voorbeeld u hoe toodelete een record instellen.</span><span class="sxs-lookup"><span data-stu-id="f91a4-236">hello following example shows how toodelete a record set.</span></span> <span data-ttu-id="f91a4-237">In dit voorbeeld worden Hallo Recordset naam, type recordset zonenaam en resourcegroep elk expliciet opgegeven.</span><span class="sxs-lookup"><span data-stu-id="f91a4-237">In this example, hello record set name, record set type, zone name, and resource group are each specified explicitly.</span></span>

```powershell
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="f91a4-238">U kunt ook Hallo recordset kan worden opgegeven met de naam en type en Hallo zone opgegeven met behulp van een object:</span><span class="sxs-lookup"><span data-stu-id="f91a4-238">Alternatively, hello record set can be specified by name and type, and hello zone specified using an object:</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

<span data-ttu-id="f91a4-239">Als een derde optie Hallo-Recordset zelf, worden opgegeven met behulp van een Recordset-object:</span><span class="sxs-lookup"><span data-stu-id="f91a4-239">As a third option, hello record set itself can be specified using a record set object:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -RecordSet $rs
```

<span data-ttu-id="f91a4-240">Wanneer u Hallo Recordset toobe verwijderd opgeeft met behulp van een object Recordset [Etag controleert](dns-zones-records.md#etags) worden gebruikt tooensure gelijktijdige wijzigingen worden niet verwijderd.</span><span class="sxs-lookup"><span data-stu-id="f91a4-240">When you specify hello record set toobe deleted by using a record set object, [Etag checks](dns-zones-records.md#etags) are used tooensure concurrent changes are not deleted.</span></span> <span data-ttu-id="f91a4-241">U kunt optioneel Hallo `-Overwrite` overschakelen toosuppress deze controles.</span><span class="sxs-lookup"><span data-stu-id="f91a4-241">You can use hello optional `-Overwrite` switch toosuppress these checks.</span></span>

<span data-ttu-id="f91a4-242">Hallo Recordset object kan ook worden doorgesluisd in plaats van dat wordt doorgegeven als parameter:</span><span class="sxs-lookup"><span data-stu-id="f91a4-242">hello record set object can also be piped instead of being passed as a parameter:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | Remove-AzureRmDnsRecordSet
```

## <a name="confirmation-prompts"></a><span data-ttu-id="f91a4-243">Bevestiging vragen</span><span class="sxs-lookup"><span data-stu-id="f91a4-243">Confirmation prompts</span></span>

<span data-ttu-id="f91a4-244">Hallo `New-AzureRmDnsRecordSet`, `Set-AzureRmDnsRecordSet`, en `Remove-AzureRmDnsRecordSet` cmdlets alle bevestiging vragen ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="f91a4-244">hello `New-AzureRmDnsRecordSet`, `Set-AzureRmDnsRecordSet`, and `Remove-AzureRmDnsRecordSet` cmdlets all support confirmation prompts.</span></span>

<span data-ttu-id="f91a4-245">Elke cmdlet vraagt om bevestiging als hello `$ConfirmPreference` PowerShell voorkeursvariabele een waarde heeft van `Medium` of lager.</span><span class="sxs-lookup"><span data-stu-id="f91a4-245">Each cmdlet prompts for confirmation if hello `$ConfirmPreference` PowerShell preference variable has a value of `Medium` or lower.</span></span> <span data-ttu-id="f91a4-246">Sinds de standaardwaarde Hallo voor `$ConfirmPreference` is `High`, deze vragen zijn niet opgegeven voor het met de standaardinstellingen voor PowerShell Hallo.</span><span class="sxs-lookup"><span data-stu-id="f91a4-246">Since hello default value for `$ConfirmPreference` is `High`, these prompts are not given when using hello default PowerShell settings.</span></span>

<span data-ttu-id="f91a4-247">U kunt de huidige Hallo overschrijven `$ConfirmPreference` instelling met de Hallo `-Confirm` parameter.</span><span class="sxs-lookup"><span data-stu-id="f91a4-247">You can override hello current `$ConfirmPreference` setting using hello `-Confirm` parameter.</span></span> <span data-ttu-id="f91a4-248">Als u opgeeft `-Confirm` of `-Confirm:$True` , Hallo cmdlet vraagt u om bevestiging voordat deze wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f91a4-248">If you specify `-Confirm` or `-Confirm:$True` , hello cmdlet prompts you for confirmation before it runs.</span></span> <span data-ttu-id="f91a4-249">Als u opgeeft `-Confirm:$False` , Hallo cmdlet wordt u niet gevraagd om bevestiging.</span><span class="sxs-lookup"><span data-stu-id="f91a4-249">If you specify `-Confirm:$False` , hello cmdlet does not prompt you for confirmation.</span></span> 

<span data-ttu-id="f91a4-250">Voor meer informatie over `-Confirm` en `$ConfirmPreference`, Zie [over Voorkeursvariabelen](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span><span class="sxs-lookup"><span data-stu-id="f91a4-250">For more information about `-Confirm` and `$ConfirmPreference`, see [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f91a4-251">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f91a4-251">Next steps</span></span>

<span data-ttu-id="f91a4-252">Meer informatie over [zones en -records in Azure DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="f91a4-252">Learn more about [zones and records in Azure DNS](dns-zones-records.md).</span></span>
<br>
<span data-ttu-id="f91a4-253">Meer informatie over hoe te[beveiligen van uw zones en records](dns-protect-zones-recordsets.md) bij gebruik van Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="f91a4-253">Learn how too[protect your zones and records](dns-protect-zones-recordsets.md) when using Azure DNS.</span></span>
<br>
<span data-ttu-id="f91a4-254">Bekijk Hallo [Azure DNS PowerShell-naslagdocumentatie](/powershell/module/azurerm.dns).</span><span class="sxs-lookup"><span data-stu-id="f91a4-254">Review hello [Azure DNS PowerShell reference documentation](/powershell/module/azurerm.dns).</span></span>
