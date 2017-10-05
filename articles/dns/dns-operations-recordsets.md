---
title: DNS-records in Azure DNS met Azure PowerShell beheren | Microsoft Docs
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
ms.openlocfilehash: 2962e30e5d9c60b8e786e2ba79647cabfc5925cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-dns-records-and-recordsets-in-azure-dns-using-azure-powershell"></a><span data-ttu-id="09835-104">DNS-records en recordsets in Azure DNS met Azure PowerShell beheren</span><span class="sxs-lookup"><span data-stu-id="09835-104">Manage DNS records and recordsets in Azure DNS using Azure PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="09835-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="09835-105">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="09835-106">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="09835-106">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="09835-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="09835-107">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="09835-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="09835-108">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="09835-109">In dit artikel laat zien hoe DNS-records voor de DNS-zone beheren met behulp van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="09835-109">This article shows you how to manage DNS records for your DNS zone by using Azure PowerShell.</span></span> <span data-ttu-id="09835-110">DNS-records kunnen ook worden beheerd met behulp van de platformoverschrijdende [Azure CLI](dns-operations-recordsets-cli.md) of de [Azure-portal](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="09835-110">DNS records can also be managed by using the cross-platform [Azure CLI](dns-operations-recordsets-cli.md) or the [Azure portal](dns-operations-recordsets-portal.md).</span></span>

<span data-ttu-id="09835-111">De voorbeelden in dit artikel wordt ervan uitgegaan dat u al hebt [Azure PowerShell aangemeld, geïnstalleerd en wordt gemaakt van een DNS-zone](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="09835-111">The examples in this article assume you have already [installed Azure PowerShell, signed in, and created a DNS zone](dns-operations-dnszones.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="09835-112">Inleiding</span><span class="sxs-lookup"><span data-stu-id="09835-112">Introduction</span></span>

<span data-ttu-id="09835-113">Voordat u DNS-records in DNS Azure maakt, leest u eerst hoe Azure DNS DNS-records organiseert in DNS-recordsets.</span><span class="sxs-lookup"><span data-stu-id="09835-113">Before creating DNS records in Azure DNS, you first need to understand how Azure DNS organizes DNS records into DNS record sets.</span></span>

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

<span data-ttu-id="09835-114">Zie [DNS-zones en -records](dns-zones-records.md) voor meer informatie over DNS-records in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="09835-114">For more information about DNS records in Azure DNS, see [DNS zones and records](dns-zones-records.md).</span></span>


## <a name="create-a-new-dns-record"></a><span data-ttu-id="09835-115">Maak een nieuwe DNS-record</span><span class="sxs-lookup"><span data-stu-id="09835-115">Create a new DNS record</span></span>

<span data-ttu-id="09835-116">Als uw nieuwe record dezelfde naam en hetzelfde type als een bestaande record heeft, moet u [toe te voegen aan de bestaande recordset](#add-a-record-to-an-existing-record-set).</span><span class="sxs-lookup"><span data-stu-id="09835-116">If your new record has the same name and type as an existing record, you need to [add it to the existing record set](#add-a-record-to-an-existing-record-set).</span></span> <span data-ttu-id="09835-117">Als uw nieuwe record een andere naam en type alle bestaande records heeft, moet u een nieuwe recordset maken.</span><span class="sxs-lookup"><span data-stu-id="09835-117">If your new record has a different name and type to all existing records, you need to create a new record set.</span></span> 

### <a name="create-a-records-in-a-new-record-set"></a><span data-ttu-id="09835-118">"A" records in een nieuwe recordset maken</span><span class="sxs-lookup"><span data-stu-id="09835-118">Create 'A' records in a new record set</span></span>

<span data-ttu-id="09835-119">U kunt recordsets maken met behulp van de cmdlet `New-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="09835-119">You create record sets by using the `New-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="09835-120">Wanneer u een recordset, moet u aangeven dat de record naam, de zone, de tijd ingesteld op live (TTL), het recordtype en de records die moeten worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="09835-120">When creating a record set, you need to specify the record set name, the zone, the time to live (TTL), the record type, and the records to be created.</span></span>

<span data-ttu-id="09835-121">De parameters voor het toevoegen van records aan een recordset variëren afhankelijk van het type recordset.</span><span class="sxs-lookup"><span data-stu-id="09835-121">The parameters for adding records to a record set vary depending on the type of the record set.</span></span> <span data-ttu-id="09835-122">Bijvoorbeeld, wanneer u een recordset van het type "A", moet u het IP-adres met de parameter opgeven `-IPv4Address`.</span><span class="sxs-lookup"><span data-stu-id="09835-122">For example, when using a record set of type 'A', you need to specify the IP address using the parameter `-IPv4Address`.</span></span> <span data-ttu-id="09835-123">Andere parameters worden gebruikt voor andere typen records.</span><span class="sxs-lookup"><span data-stu-id="09835-123">Other parameters are used for other record types.</span></span> <span data-ttu-id="09835-124">Zie [voorbeelden van recordtypen aanvullende](#additional-record-type-examples) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="09835-124">See [Additional record type examples](#additional-record-type-examples) for details.</span></span>

<span data-ttu-id="09835-125">Het volgende voorbeeld maakt een recordset met de relatieve naam 'www' in de DNS-Zone 'contoso.com'.</span><span class="sxs-lookup"><span data-stu-id="09835-125">The following example creates a record set with the relative name 'www' in the DNS Zone 'contoso.com'.</span></span> <span data-ttu-id="09835-126">De volledig gekwalificeerde naam van de recordset is 'www.contoso.com'.</span><span class="sxs-lookup"><span data-stu-id="09835-126">The fully-qualified name of the record set is 'www.contoso.com'.</span></span> <span data-ttu-id="09835-127">Het recordtype is "A" en de TTL 3600 seconden.</span><span class="sxs-lookup"><span data-stu-id="09835-127">The record type is 'A', and the TTL is 3600 seconds.</span></span> <span data-ttu-id="09835-128">De recordset bevat één record, met IP-adres '1.2.3.4'.</span><span class="sxs-lookup"><span data-stu-id="09835-128">The record set contains a single record, with IP address '1.2.3.4'.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

<span data-ttu-id="09835-129">Maken van een recordset in de apex van een zone (in dit geval 'contoso.com'), gebruikt u de naam van de recordset ' @' (zonder aanhalingstekens):</span><span class="sxs-lookup"><span data-stu-id="09835-129">To create a record set at the 'apex' of a zone (in this case, 'contoso.com'), use the record set name '@' (excluding quotation marks):</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

<span data-ttu-id="09835-130">Als u een recordset met meer dan één record maken wilt, maakt eerst een lokale matrix en de records toevoegen en de matrix te geven `New-AzureRmDnsRecordSet` als volgt:</span><span class="sxs-lookup"><span data-stu-id="09835-130">If you need to create a record set containing more than one record, first create a local array and add the records, then pass the array to `New-AzureRmDnsRecordSet` as follows:</span></span>

```powershell
$aRecords = @()
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4"
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "2.3.4.5"
New-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName MyResourceGroup -Ttl 3600 -RecordType A -DnsRecords $aRecords
```

<span data-ttu-id="09835-131">[Metagegevens van de recordset](dns-zones-records.md#tags-and-metadata) kan worden gebruikt om toepassingsspecifieke gegevens koppelen aan elke recordset als sleutel-waardeparen.</span><span class="sxs-lookup"><span data-stu-id="09835-131">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span></span> <span data-ttu-id="09835-132">Het volgende voorbeeld ziet u hoe u een recordset met twee metagegevensvermeldingen maken ' afdeling Financiën =' en ' omgeving productie ='.</span><span class="sxs-lookup"><span data-stu-id="09835-132">The following example shows how to create a record set with two metadata entries, 'dept=finance' and 'environment=production'.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") -Metadata @{ dept="finance"; environment="production" } 
```

<span data-ttu-id="09835-133">Azure DNS ondersteunt ook 'empty' recordsets als een tijdelijke aanduiding voor een DNS-naam reserveren fungeren kunnen voordat u DNS-records maakt.</span><span class="sxs-lookup"><span data-stu-id="09835-133">Azure DNS also supports 'empty' record sets, which can act as a placeholder to reserve a DNS name before creating DNS records.</span></span> <span data-ttu-id="09835-134">Lege recordsets zijn zichtbaar in het vlak van Azure DNS-beheer, maar worden weergegeven op de Azure DNS-naamservers.</span><span class="sxs-lookup"><span data-stu-id="09835-134">Empty record sets are visible in the Azure DNS control plane, but do appear on the Azure DNS name servers.</span></span> <span data-ttu-id="09835-135">Het volgende voorbeeld wordt een lege recordset gemaakt:</span><span class="sxs-lookup"><span data-stu-id="09835-135">The following example creates an empty record set:</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords @()
```

## <a name="create-records-of-other-types"></a><span data-ttu-id="09835-136">Records van andere typen maken</span><span class="sxs-lookup"><span data-stu-id="09835-136">Create records of other types</span></span>

<span data-ttu-id="09835-137">Hebben gezien in detail "A" records maken, de volgende voorbeelden laten zien hoe andere recordtypen ondersteund door Azure DNS-records maken.</span><span class="sxs-lookup"><span data-stu-id="09835-137">Having seen in detail how to create 'A' records, the following examples show how to create records of other record types supported by Azure DNS.</span></span>

<span data-ttu-id="09835-138">In elk geval laten we zien hoe u een recordset met één record maken.</span><span class="sxs-lookup"><span data-stu-id="09835-138">In each case, we show how to create a record set containing a single record.</span></span> <span data-ttu-id="09835-139">De eerdere voorbeelden voor "A" records kunnen worden aangepast voor het maken van recordsets van andere typen met meerdere records met metagegevens, of leeg recordsets maken.</span><span class="sxs-lookup"><span data-stu-id="09835-139">The earlier examples for 'A' records can be adapted to create record sets of other types containing multiple records, with metadata, or to create empty record sets.</span></span>

<span data-ttu-id="09835-140">We geven geen bevoegdheden als een voorbeeld voor het maken van een recordset SOA sinds SOA's zijn gemaakt en verwijderd met elke DNS-zone en kan niet worden gemaakt of afzonderlijk worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="09835-140">We do not give an example to create an SOA record set, since SOAs are created and deleted with each DNS zone and cannot be created or deleted separately.</span></span> <span data-ttu-id="09835-141">Echter, [de SOA kan worden gewijzigd, zoals wordt weergegeven in het voorbeeld van een hoger](#to-modify-an-SOA-record).</span><span class="sxs-lookup"><span data-stu-id="09835-141">However, [the SOA can be modified, as shown in a later example](#to-modify-an-SOA-record).</span></span>

### <a name="create-an-aaaa-record-set-with-a-single-record"></a><span data-ttu-id="09835-142">Een AAAA-recordset met één record maken</span><span class="sxs-lookup"><span data-stu-id="09835-142">Create an AAAA record set with a single record</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-aaaa" -RecordType AAAA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ipv6Address "2607:f8b0:4009:1803::1005") 
```

### <a name="create-a-cname-record-set-with-a-single-record"></a><span data-ttu-id="09835-143">Een CNAME-recordset met één record maken</span><span class="sxs-lookup"><span data-stu-id="09835-143">Create a CNAME record set with a single record</span></span>

> [!NOTE]
> <span data-ttu-id="09835-144">De DNS-standaarden staan niet toe dat CNAME-records in de apex van een zone (`-Name '@'`), noch staan ze recordsets met meer dan één record.</span><span class="sxs-lookup"><span data-stu-id="09835-144">The DNS standards do not permit CNAME records at the apex of a zone (`-Name '@'`), nor do they permit record sets containing more than one record.</span></span>
> 
> <span data-ttu-id="09835-145">Zie voor meer informatie [CNAME-records](dns-zones-records.md#cname-records).</span><span class="sxs-lookup"><span data-stu-id="09835-145">For more information, see [CNAME records](dns-zones-records.md#cname-records).</span></span>


```powershell
New-AzureRmDnsRecordSet -Name "test-cname" -RecordType CNAME -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Cname "www.contoso.com") 
```

### <a name="create-an-mx-record-set-with-a-single-record"></a><span data-ttu-id="09835-146">Een MX-recordset met één record maken</span><span class="sxs-lookup"><span data-stu-id="09835-146">Create an MX record set with a single record</span></span>

<span data-ttu-id="09835-147">In dit voorbeeld gebruiken we de naam van de recordset ' @' een MX-record maken in het toppunt van de zone (in dit geval 'contoso.com').</span><span class="sxs-lookup"><span data-stu-id="09835-147">In this example, we use the record set name '@' to create an MX record at the zone apex (in this case, 'contoso.com').</span></span>


```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType MX -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Exchange "mail.contoso.com" -Preference 5) 
```

### <a name="create-an-ns-record-set-with-a-single-record"></a><span data-ttu-id="09835-148">Een NS-recordset met één record maken</span><span class="sxs-lookup"><span data-stu-id="09835-148">Create an NS record set with a single record</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-ns" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Nsdname "ns1.contoso.com") 
```

### <a name="create-a-ptr-record-set-with-a-single-record"></a><span data-ttu-id="09835-149">Een PTR-recordset met één record maken</span><span class="sxs-lookup"><span data-stu-id="09835-149">Create a PTR record set with a single record</span></span>

<span data-ttu-id="09835-150">In dit geval ' Mijn-arpa-zone.com' zone voor reverse lookup ARPA waarmee uw IP-bereik vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="09835-150">In this case, 'my-arpa-zone.com' represents the ARPA reverse lookup zone representing your IP range.</span></span> <span data-ttu-id="09835-151">Elke PTR-recordset die is ingesteld in deze zone komt overeen met een IP-adres in dit IP-bereik.</span><span class="sxs-lookup"><span data-stu-id="09835-151">Each PTR record set in this zone corresponds to an IP address within this IP range.</span></span> <span data-ttu-id="09835-152">De recordnaam "10" is het laatste octet van het IP-adres binnen deze IP-bereik dat wordt vertegenwoordigd door deze record.</span><span class="sxs-lookup"><span data-stu-id="09835-152">The record name '10' is the last octet of the IP address within this IP range represented by this record.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name 10 -RecordType PTR -ZoneName "my-arpa-zone.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "myservice.contoso.com") 
```

### <a name="create-an-srv-record-set-with-a-single-record"></a><span data-ttu-id="09835-153">Een SRV-recordset met één record maken</span><span class="sxs-lookup"><span data-stu-id="09835-153">Create an SRV record set with a single record</span></span>

<span data-ttu-id="09835-154">Bij het maken van een [SRV-Recordset](dns-zones-records.md#srv-records), geef de  *\_service* en  *\_protocol* in de naam van de recordset.</span><span class="sxs-lookup"><span data-stu-id="09835-154">When creating an [SRV record set](dns-zones-records.md#srv-records), specify the *\_service* and *\_protocol* in the record set name.</span></span> <span data-ttu-id="09835-155">Er is niet nodig om ' @' in de recordnaam bij het maken van een SRV-record in het toppunt van de zone.</span><span class="sxs-lookup"><span data-stu-id="09835-155">There is no need to include '@' in the record set name when creating an SRV record set at the zone apex.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "_sip._tls" -RecordType SRV -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Priority 0 -Weight 5 -Port 8080 -Target "sip.contoso.com") 
```


### <a name="create-a-txt-record-set-with-a-single-record"></a><span data-ttu-id="09835-156">Een TXT-recordset met één record maken</span><span class="sxs-lookup"><span data-stu-id="09835-156">Create a TXT record set with a single record</span></span>

<span data-ttu-id="09835-157">Het volgende voorbeeld laat zien hoe een TXT-record te maken.</span><span class="sxs-lookup"><span data-stu-id="09835-157">The following example shows how to create a TXT record.</span></span> <span data-ttu-id="09835-158">Zie voor meer informatie over de maximale tekenreekslengte ondersteund in de TXT-records [TXT-records](dns-zones-records.md#txt-records).</span><span class="sxs-lookup"><span data-stu-id="09835-158">For more information about the maximum string length supported in TXT records, see [TXT records](dns-zones-records.md#txt-records).</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-txt" -RecordType TXT -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Value "This is a TXT record") 
```


## <a name="get-a-record-set"></a><span data-ttu-id="09835-159">Een recordset ophalen</span><span class="sxs-lookup"><span data-stu-id="09835-159">Get a record set</span></span>

<span data-ttu-id="09835-160">Gebruik voor het ophalen van een bestaande recordset `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="09835-160">To retrieve an existing record set, use `Get-AzureRmDnsRecordSet`.</span></span> <span data-ttu-id="09835-161">Deze cmdlet retourneert een lokaal object met de recordset in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="09835-161">This cmdlet returns a local object that represents the record set in Azure DNS.</span></span>

<span data-ttu-id="09835-162">Net als bij `New-AzureRmDnsRecordSet`, de naam van de recordset gegeven moet een *relatieve* naam, wat betekent dat de naam van de zone moet worden uitgesloten.</span><span class="sxs-lookup"><span data-stu-id="09835-162">As with `New-AzureRmDnsRecordSet`, the record set name given must be a *relative* name, meaning it must exclude the zone name.</span></span> <span data-ttu-id="09835-163">U moet ook opgeven het recordtype en de zone met de record ingesteld.</span><span class="sxs-lookup"><span data-stu-id="09835-163">You also need to specify the record type, and the zone containing the record set.</span></span>

<span data-ttu-id="09835-164">Het volgende voorbeeld laat zien hoe een recordset ophalen.</span><span class="sxs-lookup"><span data-stu-id="09835-164">The following example shows how to retrieve a record set.</span></span> <span data-ttu-id="09835-165">In dit voorbeeld wordt de zone wordt opgegeven met de `-ZoneName` en `-ResourceGroupName` parameters.</span><span class="sxs-lookup"><span data-stu-id="09835-165">In this example, the zone is specified using the `-ZoneName` and `-ResourceGroupName` parameters.</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="09835-166">U kunt eventueel ook opgeven de zone met behulp van een zone-object dat is doorgegeven met behulp van de `-Zone` parameter.</span><span class="sxs-lookup"><span data-stu-id="09835-166">Alternatively, you can also specify the zone using a zone object, passed using the `-Zone` parameter.</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

## <a name="list-record-sets"></a><span data-ttu-id="09835-167">Lijst met recordsets</span><span class="sxs-lookup"><span data-stu-id="09835-167">List record sets</span></span>

<span data-ttu-id="09835-168">U kunt ook `Get-AzureRmDnsZone` aan de lijst met recordsets in een zone, zonder de `-Name` en/of `-RecordType` parameters.</span><span class="sxs-lookup"><span data-stu-id="09835-168">You can also use `Get-AzureRmDnsZone` to list record sets in a zone, by omitting the `-Name` and/or `-RecordType` parameters.</span></span>

<span data-ttu-id="09835-169">Het volgende voorbeeld retourneert alle recordsets in de zone:</span><span class="sxs-lookup"><span data-stu-id="09835-169">The following example returns all record sets in the zone:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="09835-170">Het volgende voorbeeld ziet u hoe-alle recordsets van een bepaald type kan worden opgehaald door het recordtype geven terwijl naam als de record wordt weggelaten instellen:</span><span class="sxs-lookup"><span data-stu-id="09835-170">The following example shows how all record sets of a given type can be retrieved by specifying the record type while omitting the record set name:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="09835-171">Voor het ophalen van alle recordsets met een opgegeven naam over recordtypen, moet u alle recordsets ophalen en vervolgens de resultaten te filteren:</span><span class="sxs-lookup"><span data-stu-id="09835-171">To retrieve all record sets with a given name, across record types, you need to retrieve all record sets and then filter the results:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | where {$_.Name.Equals("www")}
```

<span data-ttu-id="09835-172">In de bovenstaande voorbeelden de zone kan worden opgegeven via de `-ZoneName` en `-ResourceGroupName`parameters (zoals weergegeven), of door te geven van een zone-object:</span><span class="sxs-lookup"><span data-stu-id="09835-172">In all the above examples, the zone can be specified either by using the `-ZoneName` and `-ResourceGroupName`parameters (as shown), or by specifying a zone object:</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$recordsets = Get-AzureRmDnsRecordSet -Zone $zone
```

## <a name="add-a-record-to-an-existing-record-set"></a><span data-ttu-id="09835-173">Een record aan een bestaande recordset toevoegen</span><span class="sxs-lookup"><span data-stu-id="09835-173">Add a record to an existing record set</span></span>

<span data-ttu-id="09835-174">Als een record toevoegen aan een bestaande recordset, volgt u de volgende drie stappen:</span><span class="sxs-lookup"><span data-stu-id="09835-174">To add a record to an existing record set, follow the following three steps:</span></span>

1. <span data-ttu-id="09835-175">De bestaande recordset ophalen</span><span class="sxs-lookup"><span data-stu-id="09835-175">Get the existing record set</span></span>

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. <span data-ttu-id="09835-176">De nieuwe record toevoegen aan de lokale Recordset.</span><span class="sxs-lookup"><span data-stu-id="09835-176">Add the new record to the local record set.</span></span> <span data-ttu-id="09835-177">Dit is een offline-bewerking.</span><span class="sxs-lookup"><span data-stu-id="09835-177">This is an off-line operation.</span></span>

    ```powershell
    Add-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. <span data-ttu-id="09835-178">De wijziging doorvoeren terug naar de Azure DNS-service.</span><span class="sxs-lookup"><span data-stu-id="09835-178">Commit the change back to the Azure DNS service.</span></span> 

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $rs
    ```

<span data-ttu-id="09835-179">Met behulp van `Set-AzureRmDnsRecordSet` *vervangt* de bestaande recordset in Azure DNS (en alle records die deze bevat) met de opgegeven recordset.</span><span class="sxs-lookup"><span data-stu-id="09835-179">Using `Set-AzureRmDnsRecordSet` *replaces* the existing record set in Azure DNS (and all records it contains) with the record set specified.</span></span> <span data-ttu-id="09835-180">[ETag controles](dns-zones-records.md#etags) worden gebruikt om ervoor te zorgen gelijktijdige wijzigingen worden niet overschreven.</span><span class="sxs-lookup"><span data-stu-id="09835-180">[Etag checks](dns-zones-records.md#etags) are used to ensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="09835-181">U kunt de optionele `-Overwrite` overschakelen naar het onderdrukken van deze controles.</span><span class="sxs-lookup"><span data-stu-id="09835-181">You can use the optional `-Overwrite` switch to suppress these checks.</span></span>

<span data-ttu-id="09835-182">Deze reeks bewerkingen kan ook worden *doorgesluisd*, wat betekent dat u het object Recordset met behulp van de pipe in plaats van deze doorgegeven als parameter doorgeven:</span><span class="sxs-lookup"><span data-stu-id="09835-182">This sequence of operations can also be *piped*, meaning you pass the record set object by using the pipe rather than passing it as a parameter:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name "www" –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Add-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

<span data-ttu-id="09835-183">De bovenstaande voorbeelden laten zien hoe een 'A'-record toevoegen aan een bestaande recordset van het type "A".</span><span class="sxs-lookup"><span data-stu-id="09835-183">The examples above show how to add an 'A' record to an existing record set of type 'A'.</span></span> <span data-ttu-id="09835-184">Een vergelijkbare reeks bewerkingen wordt gebruikt voor het toevoegen van records aan de recordsets van andere typen, vervangen door de `-Ipv4Address` parameter van `Add-AzureRmDnsRecordConfig` met andere parameters die specifiek zijn voor elk recordtype.</span><span class="sxs-lookup"><span data-stu-id="09835-184">A similar sequence of operations is used to add records to record sets of other types, substituting the `-Ipv4Address` parameter of `Add-AzureRmDnsRecordConfig` with other parameters specific to each record type.</span></span> <span data-ttu-id="09835-185">De parameters voor elk recordtype zijn hetzelfde als voor de `New-AzureRmDnsRecordConfig` cmdlet, zoals wordt weergegeven in [voorbeelden van recordtypen aanvullende](#additional-record-type-examples) hierboven.</span><span class="sxs-lookup"><span data-stu-id="09835-185">The parameters for each record type are the same as for the `New-AzureRmDnsRecordConfig` cmdlet, as shown in [Additional record type examples](#additional-record-type-examples) above.</span></span>

<span data-ttu-id="09835-186">Recordsets van het type 'CNAME-' of 'SOA' mag niet meer dan een record bevatten.</span><span class="sxs-lookup"><span data-stu-id="09835-186">Record sets of type 'CNAME' or 'SOA' cannot contain more than one record.</span></span> <span data-ttu-id="09835-187">Deze beperking voortvloeit uit de DNS-standaarden.</span><span class="sxs-lookup"><span data-stu-id="09835-187">This constraint arises from the DNS standards.</span></span> <span data-ttu-id="09835-188">Het is niet een beperking van Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="09835-188">It is not a limitation of Azure DNS.</span></span>

## <a name="remove-a-record-from-an-existing-record-set"></a><span data-ttu-id="09835-189">Een record verwijderen uit een bestaande recordset</span><span class="sxs-lookup"><span data-stu-id="09835-189">Remove a record from an existing record set</span></span>

<span data-ttu-id="09835-190">Een record verwijderen uit een recordset van het proces is vergelijkbaar met het proces voor het toevoegen van een record aan een bestaande recordset:</span><span class="sxs-lookup"><span data-stu-id="09835-190">The process to remove a record from a record set is similar to the process to add a record to an existing record set:</span></span>

1. <span data-ttu-id="09835-191">De bestaande recordset ophalen</span><span class="sxs-lookup"><span data-stu-id="09835-191">Get the existing record set</span></span>

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. <span data-ttu-id="09835-192">De record verwijderen uit het lokale Recordset-object.</span><span class="sxs-lookup"><span data-stu-id="09835-192">Remove the record from the local record set object.</span></span> <span data-ttu-id="09835-193">Dit is een offline-bewerking.</span><span class="sxs-lookup"><span data-stu-id="09835-193">This is an off-line operation.</span></span> <span data-ttu-id="09835-194">De record die wordt verwijderd moet een exacte overeenkomst aan een bestaande record binnen alle parameters.</span><span class="sxs-lookup"><span data-stu-id="09835-194">The record that's being removed must be an exact match with an existing record across all parameters.</span></span>

    ```powershell
    Remove-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. <span data-ttu-id="09835-195">De wijziging doorvoeren terug naar de Azure DNS-service.</span><span class="sxs-lookup"><span data-stu-id="09835-195">Commit the change back to the Azure DNS service.</span></span> <span data-ttu-id="09835-196">Gebruik het optionele `-Overwrite` switch moet worden onderdrukt [Etag controleert](dns-zones-records.md#etags) voor gelijktijdige wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="09835-196">Use the optional `-Overwrite` switch to suppress [Etag checks](dns-zones-records.md#etags) for concurrent changes.</span></span>

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $Rs
    ```

<span data-ttu-id="09835-197">De laatste record verwijderen uit een recordset met behulp van de bovenstaande reeks de recordset niet verwijderen, in plaats daarvan het verlaten van een lege recordset.</span><span class="sxs-lookup"><span data-stu-id="09835-197">Using the above sequence to remove the last record from a record set does not delete the record set, rather it leaves an empty record set.</span></span> <span data-ttu-id="09835-198">Verwijdert u een recordset volledig [verwijderen van een recordset](#delete-a-record-set).</span><span class="sxs-lookup"><span data-stu-id="09835-198">To remove a record set entirely, see [Delete a record set](#delete-a-record-set).</span></span>

<span data-ttu-id="09835-199">Naar de records aan een recordset toe te voegen, kan de volgorde van bewerkingen voor het verwijderen van een recordset op dezelfde manier ook worden doorgesluisd:</span><span class="sxs-lookup"><span data-stu-id="09835-199">Similarly to adding records to a record set, the sequence of operations to remove a record set can also be piped:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Remove-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

<span data-ttu-id="09835-200">Verschillende recordtypen worden ondersteund door de juiste parameters typespecifieke voor `Remove-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="09835-200">Different record types are supported by passing the appropriate type-specific parameters to `Remove-AzureRmDnsRecordSet`.</span></span> <span data-ttu-id="09835-201">De parameters voor elk recordtype zijn hetzelfde als voor de `New-AzureRmDnsRecordConfig` cmdlet, zoals wordt weergegeven in [voorbeelden van recordtypen aanvullende](#additional-record-type-examples) hierboven.</span><span class="sxs-lookup"><span data-stu-id="09835-201">The parameters for each record type are the same as for the `New-AzureRmDnsRecordConfig` cmdlet, as shown in [Additional record type examples](#additional-record-type-examples) above.</span></span>


## <a name="modify-an-existing-record-set"></a><span data-ttu-id="09835-202">Een bestaande recordset wijzigen</span><span class="sxs-lookup"><span data-stu-id="09835-202">Modify an existing record set</span></span>

<span data-ttu-id="09835-203">De stappen voor het wijzigen van een bestaande recordset zijn vergelijkbaar met de stappen waarmee u bij het toevoegen of verwijderen van records uit een Recordset:</span><span class="sxs-lookup"><span data-stu-id="09835-203">The steps for modifying an existing record set are similar to the steps you take when adding or removing records from a record set:</span></span>

1. <span data-ttu-id="09835-204">Ophalen van de bestaande record ingesteld met behulp van `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="09835-204">Retrieve the existing record set by using `Get-AzureRmDnsRecordSet`.</span></span>
2. <span data-ttu-id="09835-205">Wijzig het lokale Recordset-object door:</span><span class="sxs-lookup"><span data-stu-id="09835-205">Modify the local record set object by:</span></span>
    * <span data-ttu-id="09835-206">Het toevoegen of verwijderen van records</span><span class="sxs-lookup"><span data-stu-id="09835-206">Adding or removing records</span></span>
    * <span data-ttu-id="09835-207">De parameters van bestaande records wijzigen</span><span class="sxs-lookup"><span data-stu-id="09835-207">Changing the parameters of existing records</span></span>
    * <span data-ttu-id="09835-208">Het wijzigen van de record metagegevens en de tijd ingesteld op live (TTL)</span><span class="sxs-lookup"><span data-stu-id="09835-208">Changing the record set metadata and time to live (TTL)</span></span>
3. <span data-ttu-id="09835-209">Uw wijzigingen met behulp van de `Set-AzureRmDnsRecordSet` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="09835-209">Commit your changes by using the `Set-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="09835-210">Dit *vervangt* de bestaande recordset in Azure DNS met de opgegeven recordset.</span><span class="sxs-lookup"><span data-stu-id="09835-210">This *replaces* the existing record set in Azure DNS with the record set specified.</span></span>

<span data-ttu-id="09835-211">Wanneer u `Set-AzureRmDnsRecordSet`, [Etag controleert](dns-zones-records.md#etags) worden gebruikt om ervoor te zorgen gelijktijdige wijzigingen worden niet overschreven.</span><span class="sxs-lookup"><span data-stu-id="09835-211">When using `Set-AzureRmDnsRecordSet`, [Etag checks](dns-zones-records.md#etags) are used to ensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="09835-212">U kunt de optionele `-Overwrite` overschakelen naar het onderdrukken van deze controles.</span><span class="sxs-lookup"><span data-stu-id="09835-212">You can use the optional `-Overwrite` switch to suppress these checks.</span></span>

### <a name="to-update-a-record-in-an-existing-record-set"></a><span data-ttu-id="09835-213">Een record in een bestaande recordset bij te werken</span><span class="sxs-lookup"><span data-stu-id="09835-213">To update a record in an existing record set</span></span>

<span data-ttu-id="09835-214">In dit voorbeeld wijzigen we het IP-adres van een bestaande "A" record:</span><span class="sxs-lookup"><span data-stu-id="09835-214">In this example, we change the IP address of an existing 'A' record:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Ipv4Address = "9.8.7.6"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="to-modify-an-soa-record"></a><span data-ttu-id="09835-215">Een SOA-record wijzigen</span><span class="sxs-lookup"><span data-stu-id="09835-215">To modify an SOA record</span></span>

<span data-ttu-id="09835-216">U kunt toevoegen of verwijderen van records uit de automatisch gemaakte SOA-record is ingesteld in het toppunt van de zone (`-Name "@"`, inclusief de aanhalingstekens).</span><span class="sxs-lookup"><span data-stu-id="09835-216">You cannot add or remove records from the automatically created SOA record set at the zone apex (`-Name "@"`, including quote marks).</span></span> <span data-ttu-id="09835-217">Echter, kunt u een van de parameters binnen de SOA-record (met uitzondering van de "Host") en de TTL-waarde van de recordset.</span><span class="sxs-lookup"><span data-stu-id="09835-217">However, you can modify any of the parameters within the SOA record (except "Host") and the record set TTL.</span></span>

<span data-ttu-id="09835-218">Het volgende voorbeeld ziet u het wijzigen van de *e* eigenschap van de SOA-record:</span><span class="sxs-lookup"><span data-stu-id="09835-218">The following example shows how to change the *Email* property of the SOA record:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType SOA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Email = "admin.contoso.com"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="to-modify-ns-records-at-the-zone-apex"></a><span data-ttu-id="09835-219">NS-records in het toppunt van de zone wijzigen</span><span class="sxs-lookup"><span data-stu-id="09835-219">To modify NS records at the zone apex</span></span>

<span data-ttu-id="09835-220">De NS-recordset in het toppunt van de zone wordt automatisch gemaakt met elke DNS-zone.</span><span class="sxs-lookup"><span data-stu-id="09835-220">The NS record set at the zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="09835-221">Het bevat de namen van de Azure DNS-naamservers toegewezen aan de zone.</span><span class="sxs-lookup"><span data-stu-id="09835-221">It contains the names of the Azure DNS name servers assigned to the zone.</span></span>

<span data-ttu-id="09835-222">U kunt extra naam ingesteld van servers aan deze NS-record, ter ondersteuning van collega hosting domeinen met meer dan één DNS-provider toevoegen.</span><span class="sxs-lookup"><span data-stu-id="09835-222">You can add additional name servers to this NS record set, to support co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="09835-223">U kunt ook de TTL-waarde en de metagegevens voor deze recordset wijzigen.</span><span class="sxs-lookup"><span data-stu-id="09835-223">You can also modify the TTL and metadata for this record set.</span></span> <span data-ttu-id="09835-224">U kan echter verwijderen of wijzigen van de vooraf ingestelde Azure DNS-naamservers.</span><span class="sxs-lookup"><span data-stu-id="09835-224">However, you cannot remove or modify the pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="09835-225">Houd er rekening mee dat dit alleen voor de NS-recordset in het toppunt van de zone geldt.</span><span class="sxs-lookup"><span data-stu-id="09835-225">Note that this applies only to the NS record set at the zone apex.</span></span> <span data-ttu-id="09835-226">Andere NS-recordsets in de zone (zoals gebruikt voor het delegeren van onderliggende zones) kunnen worden gewijzigd zonder beperking.</span><span class="sxs-lookup"><span data-stu-id="09835-226">Other NS record sets in your zone (as used to delegate child zones) can be modified without constraint.</span></span>

<span data-ttu-id="09835-227">Het volgende voorbeeld ziet u hoe een extra naamserver aan de NS-recordset in het toppunt van de zone toevoegen:</span><span class="sxs-lookup"><span data-stu-id="09835-227">The following example shows how to add an additional name server to the NS record set at the zone apex:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Add-AzureRmDnsRecordConfig -RecordSet $rs -Nsdname ns1.myotherdnsprovider.com
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="to-modify-record-set-metadata"></a><span data-ttu-id="09835-228">Recordset metagegevens wijzigen</span><span class="sxs-lookup"><span data-stu-id="09835-228">To modify record set metadata</span></span>

<span data-ttu-id="09835-229">[Metagegevens van de recordset](dns-zones-records.md#tags-and-metadata) kan worden gebruikt om toepassingsspecifieke gegevens koppelen aan elke recordset als sleutel-waardeparen.</span><span class="sxs-lookup"><span data-stu-id="09835-229">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span></span>

<span data-ttu-id="09835-230">Het volgende voorbeeld ziet u hoe de metagegevens van een bestaande recordset wijzigen:</span><span class="sxs-lookup"><span data-stu-id="09835-230">The following example shows how to modify the metadata of an existing record set:</span></span>

```powershell
# Get the record set
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"

# Add 'dept=finance' name-value pair
$rs.Metadata.Add('dept', 'finance') 

# Remove metadata item named 'environment'
$rs.Metadata.Remove('environment')  

# Commit changes
Set-AzureRmDnsRecordSet -RecordSet $rs
```


## <a name="delete-a-record-set"></a><span data-ttu-id="09835-231">Een recordset verwijderen</span><span class="sxs-lookup"><span data-stu-id="09835-231">Delete a record set</span></span>

<span data-ttu-id="09835-232">Recordsets kunnen worden verwijderd met behulp van de `Remove-AzureRmDnsRecordSet` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="09835-232">Record sets can be deleted by using the `Remove-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="09835-233">Een recordset te verwijderen, verwijdert tevens alle records in de recordset.</span><span class="sxs-lookup"><span data-stu-id="09835-233">Deleting a record set also deletes all records within the record set.</span></span>

> [!NOTE]
> <span data-ttu-id="09835-234">U kunt de SOA niet verwijderen en NS-record wordt ingesteld in het toppunt van de zone (`-Name '@'`).</span><span class="sxs-lookup"><span data-stu-id="09835-234">You cannot delete the SOA and NS record sets at the zone apex (`-Name '@'`).</span></span>  <span data-ttu-id="09835-235">Deze wordt automatisch door Azure DNS gemaakt wanneer de zone is gemaakt en worden automatisch verwijderd wanneer de zone wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="09835-235">Azure DNS created these automatically when the zone was created, and deletes them automatically when the zone is deleted.</span></span>

<span data-ttu-id="09835-236">Het volgende voorbeeld laat zien hoe een recordset te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="09835-236">The following example shows how to delete a record set.</span></span> <span data-ttu-id="09835-237">In dit voorbeeld wordt worden de naam van de recordset, type recordset, zonenaam en resourcegroep elk expliciet opgegeven.</span><span class="sxs-lookup"><span data-stu-id="09835-237">In this example, the record set name, record set type, zone name, and resource group are each specified explicitly.</span></span>

```powershell
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="09835-238">De recordset kan ook worden opgegeven door de naam en type en de zone die is opgegeven met behulp van een object:</span><span class="sxs-lookup"><span data-stu-id="09835-238">Alternatively, the record set can be specified by name and type, and the zone specified using an object:</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

<span data-ttu-id="09835-239">Een derde optie, kan de recordset zelf worden opgegeven met behulp van een Recordset-object:</span><span class="sxs-lookup"><span data-stu-id="09835-239">As a third option, the record set itself can be specified using a record set object:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -RecordSet $rs
```

<span data-ttu-id="09835-240">Wanneer u de recordset moet worden verwijderd met behulp van een object Recordset opgeeft [Etag controleert](dns-zones-records.md#etags) worden gebruikt om ervoor te zorgen gelijktijdige wijzigingen worden niet verwijderd.</span><span class="sxs-lookup"><span data-stu-id="09835-240">When you specify the record set to be deleted by using a record set object, [Etag checks](dns-zones-records.md#etags) are used to ensure concurrent changes are not deleted.</span></span> <span data-ttu-id="09835-241">U kunt de optionele `-Overwrite` overschakelen naar het onderdrukken van deze controles.</span><span class="sxs-lookup"><span data-stu-id="09835-241">You can use the optional `-Overwrite` switch to suppress these checks.</span></span>

<span data-ttu-id="09835-242">De Recordset-object kan ook worden doorgesluisd in plaats van dat wordt doorgegeven als parameter:</span><span class="sxs-lookup"><span data-stu-id="09835-242">The record set object can also be piped instead of being passed as a parameter:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | Remove-AzureRmDnsRecordSet
```

## <a name="confirmation-prompts"></a><span data-ttu-id="09835-243">Bevestiging vragen</span><span class="sxs-lookup"><span data-stu-id="09835-243">Confirmation prompts</span></span>

<span data-ttu-id="09835-244">De `New-AzureRmDnsRecordSet`, `Set-AzureRmDnsRecordSet`, en `Remove-AzureRmDnsRecordSet` cmdlets alle bevestiging vragen ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="09835-244">The `New-AzureRmDnsRecordSet`, `Set-AzureRmDnsRecordSet`, and `Remove-AzureRmDnsRecordSet` cmdlets all support confirmation prompts.</span></span>

<span data-ttu-id="09835-245">Elke cmdlet vraagt om bevestiging als de `$ConfirmPreference` PowerShell voorkeursvariabele een waarde heeft van `Medium` of lager.</span><span class="sxs-lookup"><span data-stu-id="09835-245">Each cmdlet prompts for confirmation if the `$ConfirmPreference` PowerShell preference variable has a value of `Medium` or lower.</span></span> <span data-ttu-id="09835-246">Sinds de standaardwaarde voor `$ConfirmPreference` is `High`, deze vragen zijn niet opgegeven voor het met de standaardinstellingen voor PowerShell.</span><span class="sxs-lookup"><span data-stu-id="09835-246">Since the default value for `$ConfirmPreference` is `High`, these prompts are not given when using the default PowerShell settings.</span></span>

<span data-ttu-id="09835-247">U kunt de huidige overschrijven `$ConfirmPreference` instellen met de `-Confirm` parameter.</span><span class="sxs-lookup"><span data-stu-id="09835-247">You can override the current `$ConfirmPreference` setting using the `-Confirm` parameter.</span></span> <span data-ttu-id="09835-248">Als u opgeeft `-Confirm` of `-Confirm:$True` , vraagt de cmdlet u om bevestiging voordat deze wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="09835-248">If you specify `-Confirm` or `-Confirm:$True` , the cmdlet prompts you for confirmation before it runs.</span></span> <span data-ttu-id="09835-249">Als u opgeeft `-Confirm:$False` , de cmdlet wordt u niet gevraagd om bevestiging.</span><span class="sxs-lookup"><span data-stu-id="09835-249">If you specify `-Confirm:$False` , the cmdlet does not prompt you for confirmation.</span></span> 

<span data-ttu-id="09835-250">Voor meer informatie over `-Confirm` en `$ConfirmPreference`, Zie [over Voorkeursvariabelen](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span><span class="sxs-lookup"><span data-stu-id="09835-250">For more information about `-Confirm` and `$ConfirmPreference`, see [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span></span>

## <a name="next-steps"></a><span data-ttu-id="09835-251">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="09835-251">Next steps</span></span>

<span data-ttu-id="09835-252">Meer informatie over [zones en -records in Azure DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="09835-252">Learn more about [zones and records in Azure DNS](dns-zones-records.md).</span></span>
<br>
<span data-ttu-id="09835-253">Meer informatie over hoe [beveiligen van uw zones en records](dns-protect-zones-recordsets.md) bij gebruik van Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="09835-253">Learn how to [protect your zones and records](dns-protect-zones-recordsets.md) when using Azure DNS.</span></span>
<br>
<span data-ttu-id="09835-254">Controleer de [Azure DNS PowerShell-naslagdocumentatie](/powershell/module/azurerm.dns).</span><span class="sxs-lookup"><span data-stu-id="09835-254">Review the [Azure DNS PowerShell reference documentation](/powershell/module/azurerm.dns).</span></span>
