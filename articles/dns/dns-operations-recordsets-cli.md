---
title: aaaManage DNS-records aan Azure DNS met Azure CLI 2.0 Hallo | Microsoft Docs
description: Het beheren van DNS-recordsets en records op Azure DNS bij het hosten van uw Azure DNS-domein. Alle 2.0 CLI-opdrachten voor bewerkingen voor recordsets en records.
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: 5356a3a5-8dec-44ac-9709-0c2b707f6cb5
ms.service: dns
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: jonatul
ms.openlocfilehash: 9d6f8e74ebad55ccd2381fd84a830d2c7bbb1f30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-and-recordsets-in-azure-dns-using-hello-azure-cli-20"></a><span data-ttu-id="c914b-104">DNS-records en recordsets in Azure DNS met Azure CLI 2.0 Hallo beheren</span><span class="sxs-lookup"><span data-stu-id="c914b-104">Manage DNS records and recordsets in Azure DNS using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c914b-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c914b-105">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="c914b-106">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="c914b-106">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="c914b-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c914b-107">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="c914b-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c914b-108">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="c914b-109">Dit artikel laat zien hoe toomanage DNS-records voor de DNS-zone met behulp van Hallo platformoverschrijdende Azure-opdrachtregelinterface (CLI) 2.0, die beschikbaar voor Windows, Mac en Linux is.</span><span class="sxs-lookup"><span data-stu-id="c914b-109">This article shows you how toomanage DNS records for your DNS zone by using hello cross-platform Azure command-line interface (CLI) 2.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="c914b-110">U kunt ook de DNS-records met beheren [Azure PowerShell](dns-operations-recordsets.md) of Hallo [Azure-portal](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c914b-110">You can also manage your DNS records using [Azure PowerShell](dns-operations-recordsets.md) or hello [Azure portal](dns-operations-recordsets-portal.md).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="c914b-111">CLI-versies toocomplete Hallo taak</span><span class="sxs-lookup"><span data-stu-id="c914b-111">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="c914b-112">U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="c914b-112">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="c914b-113">[Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) -onze CLI voor Hallo klassieke en resource management implementatiemodellen.</span><span class="sxs-lookup"><span data-stu-id="c914b-113">[Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) - our CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="c914b-114">[Azure CLI 2.0](dns-operations-recordsets-cli.md) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="c914b-114">[Azure CLI 2.0](dns-operations-recordsets-cli.md) - our next generation CLI for hello resource management deployment model.</span></span>

<span data-ttu-id="c914b-115">Hallo-voorbeelden in dit artikel wordt ervan uitgegaan dat u al hebt [hello Azure CLI 2.0, aangemeld, geïnstalleerd en wordt gemaakt van een DNS-zone](dns-operations-dnszones-cli.md).</span><span class="sxs-lookup"><span data-stu-id="c914b-115">hello examples in this article assume you have already [installed hello Azure CLI 2.0, signed in, and created a DNS zone](dns-operations-dnszones-cli.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="c914b-116">Inleiding</span><span class="sxs-lookup"><span data-stu-id="c914b-116">Introduction</span></span>

<span data-ttu-id="c914b-117">Voordat u DNS-records in Azure DNS maakt, moet u eerst de toounderstand hoe organiseert van DNS-records in DNS-recordsets in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="c914b-117">Before creating DNS records in Azure DNS, you first need toounderstand how Azure DNS organizes DNS records into DNS record sets.</span></span>

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

<span data-ttu-id="c914b-118">Zie [DNS-zones en -records](dns-zones-records.md) voor meer informatie over DNS-records in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="c914b-118">For more information about DNS records in Azure DNS, see [DNS zones and records](dns-zones-records.md).</span></span>

## <a name="create-a-dns-record"></a><span data-ttu-id="c914b-119">Een DNS-record maken</span><span class="sxs-lookup"><span data-stu-id="c914b-119">Create a DNS record</span></span>

<span data-ttu-id="c914b-120">toocreate een DNS-record gebruiken Hallo `az network dns record-set <record-type> set-record` opdracht (waarbij `<record-type>` is Hallo type record, Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="c914b-120">toocreate a DNS record, use hello `az network dns record-set <record-type> set-record` command (where `<record-type>` is hello type of record, i.e</span></span> <span data-ttu-id="c914b-121">een, srv, txt, enz.) Zie `az network dns record-set --help` voor help.</span><span class="sxs-lookup"><span data-stu-id="c914b-121">a, srv, txt, etc.) For help, see `az network dns record-set --help`.</span></span>

<span data-ttu-id="c914b-122">Wanneer een record te maken, moet u toospecify Hallo Resourcegroepnaam, zonenaam, recordset naam, Hallo recordtype en Hallo-details van Hallo-record wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c914b-122">When creating a record, you need toospecify hello resource group name, zone name, record set name, hello record type, and hello details of hello record being created.</span></span> <span data-ttu-id="c914b-123">Hallo Recordset naam moet een *relatieve* naam, wat betekent dat het Hallo-zonenaam moet uitsluiten.</span><span class="sxs-lookup"><span data-stu-id="c914b-123">hello record set name given must be a *relative* name, meaning it must exclude hello zone name.</span></span>

<span data-ttu-id="c914b-124">Als de recordset Hallo niet al bestaat, wordt deze opdracht het voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c914b-124">If hello record set does not already exist, this command creates it for you.</span></span> <span data-ttu-id="c914b-125">Als het Hallo-Recordset al bestaat, wordt met deze opdracht Hallo record opgeven van de bestaande recordset toohello toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="c914b-125">If hello record set already exists, this command adds hello record you specify toohello existing record set.</span></span>

<span data-ttu-id="c914b-126">Als er een nieuwe recordset wordt gemaakt, wordt een standaard time-to-live (TTL) van 3600 gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c914b-126">If a new record set is created, a default time-to-live (TTL) of 3600 is used.</span></span> <span data-ttu-id="c914b-127">Voor instructies over hoe toouse verschillende TTLs zien [maken van een DNS-Recordset](#create-a-dns-record-set).</span><span class="sxs-lookup"><span data-stu-id="c914b-127">For instructions on how toouse different TTLs, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="c914b-128">Hallo volgende voorbeeld maakt u een A-record genoemd *www* in Hallo zone *contoso.com* in de resourcegroep Hallo *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="c914b-128">hello following example creates an A record called *www* in hello zone *contoso.com* in hello resource group *MyResourceGroup*.</span></span> <span data-ttu-id="c914b-129">IP-adres van een record is Hallo Hallo *1.2.3.4*.</span><span class="sxs-lookup"><span data-stu-id="c914b-129">hello IP address of hello A record is *1.2.3.4*.</span></span>

```azurecli
az network dns record-set a set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name www --ipv4-address 1.2.3.4
```

<span data-ttu-id="c914b-130">toocreate een record in Hallo apex van Hallo zone instellen (in dit geval 'contoso.com'), gebruik Hallo recordnaam ' @ ', inclusief de aanhalingstekens Hallo:</span><span class="sxs-lookup"><span data-stu-id="c914b-130">toocreate a record set in hello apex of hello zone (in this case, "contoso.com"), use hello record name "@", including hello quotation marks:</span></span>

```azurecli
az network dns record-set a set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "@" --ipv4-address 1.2.3.4
```

## <a name="create-a-dns-record-set"></a><span data-ttu-id="c914b-131">Een DNS-recordset maken</span><span class="sxs-lookup"><span data-stu-id="c914b-131">Create a DNS record set</span></span>

<span data-ttu-id="c914b-132">Hallo bovenstaande voorbeelden Hallo DNS-record is de toegevoegde tooan bestaande recordset of Hallo recordset is gemaakt *impliciet*.</span><span class="sxs-lookup"><span data-stu-id="c914b-132">In hello above examples, hello DNS record was either added tooan existing record set, or hello record set was created *implicitly*.</span></span> <span data-ttu-id="c914b-133">U kunt ook Hallo-recordset maken *expliciet* voordat tooit toe te voegen registreert.</span><span class="sxs-lookup"><span data-stu-id="c914b-133">You can also create hello record set *explicitly* before adding records tooit.</span></span> <span data-ttu-id="c914b-134">Azure DNS ondersteunt 'empty' recordsets die als een tijdelijke aanduiding voor tooreserve een DNS-naam optreden kunnen voor het maken van DNS-records.</span><span class="sxs-lookup"><span data-stu-id="c914b-134">Azure DNS supports 'empty' record sets, which can act as a placeholder tooreserve a DNS name before creating DNS records.</span></span> <span data-ttu-id="c914b-135">Lege recordsets zijn zichtbaar in hello Azure DNS vlak besturingselement, maar worden niet weergegeven op Hallo Azure DNS-naamservers.</span><span class="sxs-lookup"><span data-stu-id="c914b-135">Empty record sets are visible in hello Azure DNS control plane, but do not appear on hello Azure DNS name servers.</span></span>

<span data-ttu-id="c914b-136">Recordsets zijn gemaakt met behulp van Hallo `az network dns record-set <record-type> create` opdracht.</span><span class="sxs-lookup"><span data-stu-id="c914b-136">Record sets are created using hello `az network dns record-set <record-type> create` command.</span></span> <span data-ttu-id="c914b-137">Zie `az network dns record-set <record-type> create --help` voor help.</span><span class="sxs-lookup"><span data-stu-id="c914b-137">For help, see `az network dns record-set <record-type> create --help`.</span></span>

<span data-ttu-id="c914b-138">Hallo-Recordset expliciet maakt, kunt u toospecify Recordset eigenschappen zoals Hallo [Time To Live (TTL)](dns-zones-records.md#time-to-live) en metagegevens.</span><span class="sxs-lookup"><span data-stu-id="c914b-138">Creating hello record set explicitly allows you toospecify record set properties such as hello [Time-To-Live (TTL)](dns-zones-records.md#time-to-live) and metadata.</span></span> <span data-ttu-id="c914b-139">[Metagegevens van de recordset](dns-zones-records.md#tags-and-metadata) mag gebruikte tooassociate toepassingsspecifieke gegevens met elke recordset als sleutel-waardeparen.</span><span class="sxs-lookup"><span data-stu-id="c914b-139">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used tooassociate application-specific data with each record set, as key-value pairs.</span></span>

<span data-ttu-id="c914b-140">Hallo volgende voorbeeld wordt een lege recordset van het type "A" met een TTL 60 seconden met behulp van Hallo `--ttl` parameter (korte versie `-l`):</span><span class="sxs-lookup"><span data-stu-id="c914b-140">hello following example creates an empty record set of type 'A' with a 60-second TTL, by using hello `--ttl` parameter (short form `-l`):</span></span>

```azurecli
az network dns record-set a create --resource-group myresourcegroup --zone-name contoso.com --name www --ttl 60
```

<span data-ttu-id="c914b-141">Hallo volgende voorbeeld maakt u een recordset met twee metagegevensvermeldingen ' afdeling Financiën = ' en ' omgeving = productie ', met behulp van Hallo `--metadata` parameter:</span><span class="sxs-lookup"><span data-stu-id="c914b-141">hello following example creates a record set with two metadata entries, "dept=finance" and "environment=production", by using hello `--metadata` parameter :</span></span>

```azurecli
az network dns record-set a create --resource-group myresourcegroup --zone-name contoso.com --name www --metadata "dept=finance" "environment=production"
```

<span data-ttu-id="c914b-142">Gemaakt van een lege recordset records kunnen worden toegevoegd met behulp van `azure network dns record-set <record-type> set-record` zoals beschreven in [maken van een DNS-record](#create-a-dns-record).</span><span class="sxs-lookup"><span data-stu-id="c914b-142">Having created an empty record set, records can be added using `azure network dns record-set <record-type> set-record` as described in [Create a DNS record](#create-a-dns-record).</span></span>

## <a name="create-records-of-other-types"></a><span data-ttu-id="c914b-143">Records van andere typen maken</span><span class="sxs-lookup"><span data-stu-id="c914b-143">Create records of other types</span></span>

<span data-ttu-id="c914b-144">Hebben gezien in detail hoe toocreate "A" registreert, Hallo volgen voorbeelden kunt u zien hoe toocreate record van andere recordtypen worden ondersteund door Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="c914b-144">Having seen in detail how toocreate 'A' records, hello following examples show how toocreate record of other record types supported by Azure DNS.</span></span>

<span data-ttu-id="c914b-145">Hallo-parameters gebruikt toospecify Hallo record gegevens, is afhankelijk van Hallo type Hallo record.</span><span class="sxs-lookup"><span data-stu-id="c914b-145">hello parameters used toospecify hello record data vary depending on hello type of hello record.</span></span> <span data-ttu-id="c914b-146">Bijvoorbeeld, opgeven u voor een record van het type "A" hello IPv4-adres met de parameter Hallo `--ipv4-address <IPv4 address>`.</span><span class="sxs-lookup"><span data-stu-id="c914b-146">For example, for a record of type "A", you specify hello IPv4 address with hello parameter `--ipv4-address <IPv4 address>`.</span></span> <span data-ttu-id="c914b-147">Hallo parameters voor elk recordtype kunt vermeld met `az network dns record-set <record-type> set-record --help`.</span><span class="sxs-lookup"><span data-stu-id="c914b-147">hello parameters for each record type can be listed using `az network dns record-set <record-type> set-record --help`.</span></span>

<span data-ttu-id="c914b-148">In elk geval laten we zien hoe toocreate één record.</span><span class="sxs-lookup"><span data-stu-id="c914b-148">In each case, we show how toocreate a single record.</span></span> <span data-ttu-id="c914b-149">Hallo-record is toegevoegd toohello bestaande recordset of een recordset impliciet gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c914b-149">hello record is added toohello existing record set, or a record set created implicitly.</span></span> <span data-ttu-id="c914b-150">Voor meer informatie over het maken van recordsets en definiëren van record parameter expliciet, raadpleegt u [maken van een DNS-Recordset](#create-a-dns-record-set).</span><span class="sxs-lookup"><span data-stu-id="c914b-150">For more information on creating record sets and defining record set parameter explicitly, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="c914b-151">We geven geen een toocreate bijvoorbeeld een recordset SOA-sinds SOA's zijn gemaakt en verwijderd met elke DNS-zone en kan niet worden gemaakt of afzonderlijk worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="c914b-151">We do not give an example toocreate an SOA record set, since SOAs are created and deleted with each DNS zone and cannot be created or deleted separately.</span></span> <span data-ttu-id="c914b-152">Echter, [Hallo SOA kan worden gewijzigd, zoals wordt weergegeven in het voorbeeld van een hoger](#to-modify-an-SOA-record).</span><span class="sxs-lookup"><span data-stu-id="c914b-152">However, [hello SOA can be modified, as shown in a later example](#to-modify-an-SOA-record).</span></span>

### <a name="create-an-aaaa-record"></a><span data-ttu-id="c914b-153">Een AAAA-record maken</span><span class="sxs-lookup"><span data-stu-id="c914b-153">Create an AAAA record</span></span>

```azurecli
az network dns record-set aaaa set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-aaaa --ipv6-address 2607:f8b0:4009:1803::1005
```

### <a name="create-a-cname-record"></a><span data-ttu-id="c914b-154">Een CNAME-record maken</span><span class="sxs-lookup"><span data-stu-id="c914b-154">Create a CNAME record</span></span>

> [!NOTE]
> <span data-ttu-id="c914b-155">Hallo DNS-standaarden staan niet toe dat CNAME-records in het toppunt van Hallo van een zone (`--Name "@"`), noch staan ze recordsets met meer dan één record.</span><span class="sxs-lookup"><span data-stu-id="c914b-155">hello DNS standards do not permit CNAME records at hello apex of a zone (`--Name "@"`), nor do they permit record sets containing more than one record.</span></span>
> 
> <span data-ttu-id="c914b-156">Zie voor meer informatie [CNAME-records](dns-zones-records.md#cname-records).</span><span class="sxs-lookup"><span data-stu-id="c914b-156">For more information, see [CNAME records](dns-zones-records.md#cname-records).</span></span>

```azurecli
az network dns record-set cname set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-cname --cname www.contoso.com
```

### <a name="create-an-mx-record"></a><span data-ttu-id="c914b-157">Een MX-record maken</span><span class="sxs-lookup"><span data-stu-id="c914b-157">Create an MX record</span></span>

<span data-ttu-id="c914b-158">In dit voorbeeld gebruiken we Hallo recordnaam "@" toocreate Hallo MX-record in het toppunt Hallo zone (in dit geval 'contoso.com').</span><span class="sxs-lookup"><span data-stu-id="c914b-158">In this example, we use hello record set name "@" toocreate hello MX record at hello zone apex (in this case, "contoso.com").</span></span>

```azurecli
az network dns record-set mx set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "@" --exchange mail.contoso.com --preference 5
```

### <a name="create-an-ns-record"></a><span data-ttu-id="c914b-159">Een NS-record maken</span><span class="sxs-lookup"><span data-stu-id="c914b-159">Create an NS record</span></span>

```azurecli
az network dns record-set ns set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-ns --nsdname ns1.contoso.com
```

### <a name="create-a-ptr-record"></a><span data-ttu-id="c914b-160">PTR-record maken</span><span class="sxs-lookup"><span data-stu-id="c914b-160">Create a PTR record</span></span>

<span data-ttu-id="c914b-161">In dit geval ' Mijn-arpa-zone.com' vertegenwoordigt Hallo ARPA-zone die uw IP-adresbereik vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="c914b-161">In this case, 'my-arpa-zone.com' represents hello ARPA zone representing your IP range.</span></span> <span data-ttu-id="c914b-162">Elke PTR-recordset in deze zone komt overeen tooan IP-adres binnen deze IP-adresbereik.</span><span class="sxs-lookup"><span data-stu-id="c914b-162">Each PTR record set in this zone corresponds tooan IP address within this IP range.</span></span>  <span data-ttu-id="c914b-163">Hallo recordnaam "10" is de laatste octet Hallo van Hallo IP-adres binnen deze IP-bereik dat wordt vertegenwoordigd door deze record.</span><span class="sxs-lookup"><span data-stu-id="c914b-163">hello record name '10' is hello last octet of hello IP address within this IP range represented by this record.</span></span>

```azurecli
az network dns record-set ptr set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name my-arpa.zone.com --ptrdname myservice.contoso.com
```

### <a name="create-an-srv-record"></a><span data-ttu-id="c914b-164">Een SRV-record maken</span><span class="sxs-lookup"><span data-stu-id="c914b-164">Create an SRV record</span></span>

<span data-ttu-id="c914b-165">Bij het maken van een [SRV-Recordset](dns-zones-records.md#srv-records), geef Hallo  *\_service* en  *\_protocol* in Hallo-of RecordsetNaam.</span><span class="sxs-lookup"><span data-stu-id="c914b-165">When creating an [SRV record set](dns-zones-records.md#srv-records), specify hello *\_service* and *\_protocol* in hello record set name.</span></span> <span data-ttu-id="c914b-166">Er is geen tooinclude moet ' @ ' in hello RecordsetNaam wanneer een SRV-record maken in het toppunt zone Hallo ingesteld.</span><span class="sxs-lookup"><span data-stu-id="c914b-166">There is no need tooinclude "@" in hello record set name when creating an SRV record set at hello zone apex.</span></span>

```azurecli
az network dns record-set srv set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name _sip._tls --priority 10 --weight 5 --port 8080 --target sip.contoso.com
```

### <a name="create-a-txt-record"></a><span data-ttu-id="c914b-167">Een TXT-record maken</span><span class="sxs-lookup"><span data-stu-id="c914b-167">Create a TXT record</span></span>

<span data-ttu-id="c914b-168">Hallo volgende voorbeeld ziet u hoe een TXT-toocreate opnemen.</span><span class="sxs-lookup"><span data-stu-id="c914b-168">hello following example shows how toocreate a TXT record.</span></span> <span data-ttu-id="c914b-169">Zie voor meer informatie over de maximale tekenreekslengte hello wordt ondersteund in de TXT-records [TXT-records](dns-zones-records.md#txt-records).</span><span class="sxs-lookup"><span data-stu-id="c914b-169">For more information about hello maximum string length supported in TXT records, see [TXT records](dns-zones-records.md#txt-records).</span></span>

```azurecli
az network dns record-set txt set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-txt --value "This is a TXT record"
```

## <a name="get-a-record-set"></a><span data-ttu-id="c914b-170">Een recordset ophalen</span><span class="sxs-lookup"><span data-stu-id="c914b-170">Get a record set</span></span>

<span data-ttu-id="c914b-171">Gebruik een bestaande recordset tooretrieve `az network dns record-set <record-type> show`.</span><span class="sxs-lookup"><span data-stu-id="c914b-171">tooretrieve an existing record set, use `az network dns record-set <record-type> show`.</span></span> <span data-ttu-id="c914b-172">Zie `az network dns record-set <record-type> show --help` voor help.</span><span class="sxs-lookup"><span data-stu-id="c914b-172">For help, see `az network dns record-set <record-type> show --help`.</span></span>

<span data-ttu-id="c914b-173">Als bij het maken van een record of een recordset Hallo RecordsetNaam gegeven moet een *relatieve* naam, wat betekent dat het Hallo-zonenaam moet uitsluiten.</span><span class="sxs-lookup"><span data-stu-id="c914b-173">As when creating a record or record set, hello record set name given must be a *relative* name, meaning it must exclude hello zone name.</span></span> <span data-ttu-id="c914b-174">Moet u ook toospecify Hallo recordtype, Hallo zone met Hallo record ingesteld en Hallo resourcegroep met Hallo-zone.</span><span class="sxs-lookup"><span data-stu-id="c914b-174">You also need toospecify hello record type, hello zone containing hello record set, and hello resource group containing hello zone.</span></span>

<span data-ttu-id="c914b-175">Hallo volgende voorbeeld wordt opgehaald Hallo record *www* van type A uit zone *contoso.com* in de resourcegroep *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="c914b-175">hello following example retrieves hello record *www* of type A from zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
az network dns record-set a show --resource-group myresourcegroup --zone-name contoso.com --name www
```

## <a name="list-record-sets"></a><span data-ttu-id="c914b-176">Lijst met recordsets</span><span class="sxs-lookup"><span data-stu-id="c914b-176">List record sets</span></span>

<span data-ttu-id="c914b-177">U kunt alle records in een DNS-zone weergeven met behulp van Hallo `az network dns record-set list` opdracht.</span><span class="sxs-lookup"><span data-stu-id="c914b-177">You can list all records in a DNS zone by using hello `az network dns record-set list` command.</span></span> <span data-ttu-id="c914b-178">Zie `az network dns record-set list --help` voor help.</span><span class="sxs-lookup"><span data-stu-id="c914b-178">For help, see `az network dns record-set list --help`.</span></span>

<span data-ttu-id="c914b-179">In dit voorbeeld retourneert alle recordsets in de zone Hallo *contoso.com*, in de resourcegroep *MyResourceGroup*, ongeacht of het recordtype:</span><span class="sxs-lookup"><span data-stu-id="c914b-179">This example returns all record sets in hello zone *contoso.com*, in resource group *MyResourceGroup*, regardless of name or record type:</span></span>

```azurecli
az network dns record-set list --resource-group myresourcegroup --zone-name contoso.com
```

<span data-ttu-id="c914b-180">In dit voorbeeld retourneert alle recordsets die overeenkomen met de Hallo gegeven recordtype (in dit geval "A" records):</span><span class="sxs-lookup"><span data-stu-id="c914b-180">This example returns all record sets that match hello given record type (in this case, 'A' records):</span></span>

```azurecli
az network dns record-set a list --resource-group myresourcegroup --zone-name contoso.com 
```

## <a name="add-a-record-tooan-existing-record-set"></a><span data-ttu-id="c914b-181">Een record tooan bestaande recordset toevoegen</span><span class="sxs-lookup"><span data-stu-id="c914b-181">Add a record tooan existing record set</span></span>

<span data-ttu-id="c914b-182">U kunt `az network dns record-set <record-type> set-record` zowel toocreate een record in een nieuwe record instellen of tooadd een record tooan bestaande recordset.</span><span class="sxs-lookup"><span data-stu-id="c914b-182">You can use `az network dns record-set <record-type> set-record` both toocreate a record in a new record set, or tooadd a record tooan existing record set.</span></span>

<span data-ttu-id="c914b-183">Zie voor meer informatie [maken van een DNS-record](#create-a-dns-record) en [records maken van andere typen](#create-records-of-other-types) hierboven.</span><span class="sxs-lookup"><span data-stu-id="c914b-183">For more information, see [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

## <a name="remove-a-record-from-an-existing-record-set"></a><span data-ttu-id="c914b-184">Een record verwijderen uit een bestaande recordset.</span><span class="sxs-lookup"><span data-stu-id="c914b-184">Remove a record from an existing record set.</span></span>

<span data-ttu-id="c914b-185">tooremove een DNS-server registreren van een bestaande recordset gebruik `az network dns record-set <record-type> remove-record`.</span><span class="sxs-lookup"><span data-stu-id="c914b-185">tooremove a DNS record from an existing record set, use `az network dns record-set <record-type> remove-record`.</span></span> <span data-ttu-id="c914b-186">Zie `az network dns record-set <record-type> remove-record -h` voor help.</span><span class="sxs-lookup"><span data-stu-id="c914b-186">For help, see `az network dns record-set <record-type> remove-record -h`.</span></span>

<span data-ttu-id="c914b-187">Deze opdracht wordt een DNS-record verwijderd uit een recordset.</span><span class="sxs-lookup"><span data-stu-id="c914b-187">This command deletes a DNS record from a record set.</span></span> <span data-ttu-id="c914b-188">Als de laatste record Hallo in een recordset is verwijderd, wordt Hallo-Recordset zelf ook verwijderd.</span><span class="sxs-lookup"><span data-stu-id="c914b-188">If hello last record in a record set is deleted, hello record set itself is also deleted.</span></span> <span data-ttu-id="c914b-189">tookeep hello lege recordset gebruiken in plaats daarvan Hallo `--keep-empty-record-set` optie.</span><span class="sxs-lookup"><span data-stu-id="c914b-189">tookeep hello empty record set instead, use hello `--keep-empty-record-set` option.</span></span>

<span data-ttu-id="c914b-190">U moet toospecify Hallo record toobe verwijderd en Hallo zone moet worden verwijderd uit met dezelfde parameters als Hallo bij het maken van een record met `az network dns record-set <record-type> set-record`.</span><span class="sxs-lookup"><span data-stu-id="c914b-190">You need toospecify hello record toobe deleted and hello zone it should be deleted from, using hello same parameters as when creating a record using `az network dns record-set <record-type> set-record`.</span></span> <span data-ttu-id="c914b-191">Deze parameters worden beschreven in [maken van een DNS-record](#create-a-dns-record) en [records maken van andere typen](#create-records-of-other-types) hierboven.</span><span class="sxs-lookup"><span data-stu-id="c914b-191">These parameters are described in [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

<span data-ttu-id="c914b-192">Hallo volgende voorbeeld verwijdert een record met waarde '1.2.3.4' uit de record Hallo set met de naam Hallo *www* in Hallo zone *contoso.com*, in de resourcegroep Hallo *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="c914b-192">hello following example deletes hello A record with value '1.2.3.4' from hello record set named *www* in hello zone *contoso.com*, in hello resource group *MyResourceGroup*.</span></span>

```azurecli
az network dns record-set a remove-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "www" --ipv4-address 1.2.3.4
```

## <a name="modify-an-existing-record-set"></a><span data-ttu-id="c914b-193">Een bestaande recordset wijzigen</span><span class="sxs-lookup"><span data-stu-id="c914b-193">Modify an existing record set</span></span>

<span data-ttu-id="c914b-194">Elke recordset bevat een [time to live (TTL)](dns-zones-records.md#time-to-live), [metagegevens](dns-zones-records.md#tags-and-metadata), en DNS-records.</span><span class="sxs-lookup"><span data-stu-id="c914b-194">Each record set contains a [time-to-live (TTL)](dns-zones-records.md#time-to-live), [metadata](dns-zones-records.md#tags-and-metadata), and DNS records.</span></span> <span data-ttu-id="c914b-195">Hallo volgende secties wordt uitgelegd hoe toomodify van deze eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="c914b-195">hello following sections explain how toomodify each of these properties.</span></span>

### <a name="toomodify-an-a-aaaa-mx-ns-ptr-srv-or-txt-record"></a><span data-ttu-id="c914b-196">toomodify A, AAAA, MX, NS, PTR, SRV- of TXT-record</span><span class="sxs-lookup"><span data-stu-id="c914b-196">toomodify an A, AAAA, MX, NS, PTR, SRV, or TXT record</span></span>

<span data-ttu-id="c914b-197">toomodify een bestaande record van type A, AAAA, MX, NS, PTR, SRV- of TXT, moet u eerst een nieuwe record en toevoegen vervolgens verwijderen Hallo bestaande record.</span><span class="sxs-lookup"><span data-stu-id="c914b-197">toomodify an existing record of type A, AAAA, MX, NS, PTR, SRV, or TXT, you should first add a new record and then delete hello existing record.</span></span> <span data-ttu-id="c914b-198">Voor gedetailleerde instructies voor het toodelete en records toevoegen, Zie Hallo eerdere secties van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="c914b-198">For detailed instructions on how toodelete and add records, see hello earlier sections of this article.</span></span>

<span data-ttu-id="c914b-199">Hallo volgende voorbeeld ziet u hoe een record "A", van IP-adres 1.2.3.4 tooIP toomodify 5.6.7.8 aanpakken:</span><span class="sxs-lookup"><span data-stu-id="c914b-199">hello following example shows how toomodify an 'A' record, from IP address 1.2.3.4 tooIP address 5.6.7.8:</span></span>

```azurecli
az network dns record-set a set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name www --ipv4-address 5.6.7.8
az network dns record-set a remove-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name www --ipv4-address 1.2.3.4
```

<span data-ttu-id="c914b-200">U kan niet toevoegen, verwijderen of wijzigen van de records in Hallo automatisch gemaakt NS-recordset in het toppunt zone Hallo Hallo (`--Name "@"`, inclusief de aanhalingstekens).</span><span class="sxs-lookup"><span data-stu-id="c914b-200">You cannot add, remove, or modify hello records in hello automatically created NS record set at hello zone apex (`--Name "@"`, including quote marks).</span></span> <span data-ttu-id="c914b-201">Hallo alleen wijzigingen toegestaan zijn voor deze recordset toomodify Hallo Recordset TTL en metagegevens.</span><span class="sxs-lookup"><span data-stu-id="c914b-201">For this record set, hello only changes permitted are toomodify hello record set TTL and metadata.</span></span>

### <a name="toomodify-a-cname-record"></a><span data-ttu-id="c914b-202">toomodify een CNAME-record</span><span class="sxs-lookup"><span data-stu-id="c914b-202">toomodify a CNAME record</span></span>

<span data-ttu-id="c914b-203">In tegenstelling tot de meeste andere recordtypen mag een CNAME-Recordset alleen één record.</span><span class="sxs-lookup"><span data-stu-id="c914b-203">Unlike most other record types, a CNAME record set can only contain a single record.</span></span>  <span data-ttu-id="c914b-204">U kunt de Hallo huidige waarde daarom niet vervangen door een nieuwe record toevoegen en verwijderen van de bestaande record Hallo als voor andere typen records.</span><span class="sxs-lookup"><span data-stu-id="c914b-204">Therefore, you cannot replace hello current value by adding a new record and removing hello existing record, as for other record types.</span></span>

<span data-ttu-id="c914b-205">In plaats daarvan gebruikt u een CNAME-record toomodify `az network dns record-set cname set-record`.</span><span class="sxs-lookup"><span data-stu-id="c914b-205">Instead, toomodify a CNAME record, use `az network dns record-set cname set-record`.</span></span> <span data-ttu-id="c914b-206">Zie voor meer informatie`az network dns record-set cname set-record --help`</span><span class="sxs-lookup"><span data-stu-id="c914b-206">For help, see `az network dns record-set cname set-record --help`</span></span>

<span data-ttu-id="c914b-207">Hallo voorbeeld wijzigt Hallo CNAME-Recordset *www* in Hallo zone *contoso.com*, in de resourcegroep *MyResourceGroup*, toopoint te 'www.fabrikam.net' in plaats van de bestaande waarde:</span><span class="sxs-lookup"><span data-stu-id="c914b-207">hello example modifies hello CNAME record set *www* in hello zone *contoso.com*, in resource group *MyResourceGroup*, toopoint too'www.fabrikam.net' instead of its existing value:</span></span>

```azurecli
az network dns record-set cname set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-cname --cname www.fabrikam.net
``` 

### <a name="toomodify-an-soa-record"></a><span data-ttu-id="c914b-208">toomodify SOA-record</span><span class="sxs-lookup"><span data-stu-id="c914b-208">toomodify an SOA record</span></span>

<span data-ttu-id="c914b-209">In tegenstelling tot de meeste andere recordtypen mag een CNAME-Recordset alleen één record.</span><span class="sxs-lookup"><span data-stu-id="c914b-209">Unlike most other record types, a CNAME record set can only contain a single record.</span></span>  <span data-ttu-id="c914b-210">U kunt de Hallo huidige waarde daarom niet vervangen door een nieuwe record toevoegen en verwijderen van de bestaande record Hallo als voor andere typen records.</span><span class="sxs-lookup"><span data-stu-id="c914b-210">Therefore, you cannot replace hello current value by adding a new record and removing hello existing record, as for other record types.</span></span>

<span data-ttu-id="c914b-211">In plaats daarvan toomodify Hallo SOA-record gebruiken `az network dns record-set soa update`.</span><span class="sxs-lookup"><span data-stu-id="c914b-211">Instead, toomodify hello SOA record, use `az network dns record-set soa update`.</span></span> <span data-ttu-id="c914b-212">Zie `az network dns record-set soa update --help` voor help.</span><span class="sxs-lookup"><span data-stu-id="c914b-212">For help, see `az network dns record-set soa update --help`.</span></span>

<span data-ttu-id="c914b-213">Hallo volgende voorbeeld ziet u hoe de eigenschap tooset Hallo 'e' Hallo SOA legt voor Hallo zone *contoso.com* in de resourcegroep Hallo *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="c914b-213">hello following example shows how tooset hello 'email' property of hello SOA record for hello zone *contoso.com* in hello resource group *MyResourceGroup*:</span></span>

```azurecli
az network dns record-set soa update --resource-group myresourcegroup --zone-name contoso.com --email admin.contoso.com
```

### <a name="toomodify-ns-records-at-hello-zone-apex"></a><span data-ttu-id="c914b-214">toomodify NS-records in het toppunt Hallo zone</span><span class="sxs-lookup"><span data-stu-id="c914b-214">toomodify NS records at hello zone apex</span></span>

<span data-ttu-id="c914b-215">Hallo NS-recordset in het toppunt Hallo zone wordt automatisch gemaakt met elke DNS-zone.</span><span class="sxs-lookup"><span data-stu-id="c914b-215">hello NS record set at hello zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="c914b-216">Het bevat Hallo-namen van hello Azure DNS-naam servers toegewezen toohello zone.</span><span class="sxs-lookup"><span data-stu-id="c914b-216">It contains hello names of hello Azure DNS name servers assigned toohello zone.</span></span>

<span data-ttu-id="c914b-217">U kunt de naam van de aanvullende servers toothis NS-recordset, toosupport CO domeinen met meer dan één DNS-provider host toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c914b-217">You can add additional name servers toothis NS record set, toosupport co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="c914b-218">U kunt ook wijzigen Hallo TTL en metagegevens voor deze recordset.</span><span class="sxs-lookup"><span data-stu-id="c914b-218">You can also modify hello TTL and metadata for this record set.</span></span> <span data-ttu-id="c914b-219">U kan echter verwijderen of wijzigen Hallo vooraf ingestelde Azure DNS-naamservers.</span><span class="sxs-lookup"><span data-stu-id="c914b-219">However, you cannot remove or modify hello pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="c914b-220">Houd er rekening mee dat dit alleen toohello NS recordset in het toppunt zone Hallo geldt.</span><span class="sxs-lookup"><span data-stu-id="c914b-220">Note that this applies only toohello NS record set at hello zone apex.</span></span> <span data-ttu-id="c914b-221">Andere NS recordsets in de zone (als gebruikte toodelegate onderliggende zones) kunnen worden gewijzigd zonder beperking.</span><span class="sxs-lookup"><span data-stu-id="c914b-221">Other NS record sets in your zone (as used toodelegate child zones) can be modified without constraint.</span></span>

<span data-ttu-id="c914b-222">Hallo volgende voorbeeld ziet u hoe tooadd een extra naam server toohello NS-record instellen in het toppunt Hallo zone:</span><span class="sxs-lookup"><span data-stu-id="c914b-222">hello following example shows how tooadd an additional name server toohello NS record set at hello zone apex:</span></span>

```azurecli
az network dns record-set ns set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "@" --nsdname ns1.myotherdnsprovider.com 
```

### <a name="toomodify-hello-ttl-of-an-existing-record-set"></a><span data-ttu-id="c914b-223">toomodify hello TTL van een bestaande record instellen</span><span class="sxs-lookup"><span data-stu-id="c914b-223">toomodify hello TTL of an existing record set</span></span>

<span data-ttu-id="c914b-224">toomodify hello TTL van een bestaande record instellen, gebruikt u `azure network dns record-set <record-type> update`.</span><span class="sxs-lookup"><span data-stu-id="c914b-224">toomodify hello TTL of an existing record set, use `azure network dns record-set <record-type> update`.</span></span> <span data-ttu-id="c914b-225">Zie `azure network dns record-set <record-type> update --help` voor help.</span><span class="sxs-lookup"><span data-stu-id="c914b-225">For help, see `azure network dns record-set <record-type> update --help`.</span></span>

<span data-ttu-id="c914b-226">Hallo volgende voorbeeld ziet u hoe toomodify een recordset TTL, in dit geval too60 seconden:</span><span class="sxs-lookup"><span data-stu-id="c914b-226">hello following example shows how toomodify a record set TTL, in this case too60 seconds:</span></span>

```azurecli
az network dns record-set a update --resource-group myresourcegroup --zone-name contoso.com --name www --set ttl=60
```

### <a name="toomodify-hello-metadata-of-an-existing-record-set"></a><span data-ttu-id="c914b-227">toomodify hello metagegevens van een bestaande record ingesteld</span><span class="sxs-lookup"><span data-stu-id="c914b-227">toomodify hello metadata of an existing record set</span></span>

<span data-ttu-id="c914b-228">[Metagegevens van de recordset](dns-zones-records.md#tags-and-metadata) mag gebruikte tooassociate toepassingsspecifieke gegevens met elke recordset als sleutel-waardeparen.</span><span class="sxs-lookup"><span data-stu-id="c914b-228">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used tooassociate application-specific data with each record set, as key-value pairs.</span></span> <span data-ttu-id="c914b-229">toomodify hello metagegevens van een bestaande record ingesteld, gebruikt u `az network dns record-set <record-type> update`.</span><span class="sxs-lookup"><span data-stu-id="c914b-229">toomodify hello metadata of an existing record set, use `az network dns record-set <record-type> update`.</span></span> <span data-ttu-id="c914b-230">Zie `az network dns record-set <record-type> update --help` voor help.</span><span class="sxs-lookup"><span data-stu-id="c914b-230">For help, see `az network dns record-set <record-type> update --help`.</span></span>

<span data-ttu-id="c914b-231">Hallo volgende voorbeeld laat zien hoe toomodify een recordset met twee metagegevensvermeldingen ' afdeling Financiën = ' en ' omgeving productie = '.</span><span class="sxs-lookup"><span data-stu-id="c914b-231">hello following example shows how toomodify a record set with two metadata entries, "dept=finance" and "environment=production".</span></span> <span data-ttu-id="c914b-232">Merk op dat alle bestaande metagegevens is *vervangen* door Hallo waarden op basis van.</span><span class="sxs-lookup"><span data-stu-id="c914b-232">Note that any existing metadata is *replaced* by hello values given.</span></span>

```azurecli
az network dns record-set a update --resource-group myresourcegroup --zone-name contoso.com --name www --set metadata.dept=finance metadata.environment=production
```

## <a name="delete-a-record-set"></a><span data-ttu-id="c914b-233">Een recordset verwijderen</span><span class="sxs-lookup"><span data-stu-id="c914b-233">Delete a record set</span></span>

<span data-ttu-id="c914b-234">Recordsets kunnen worden verwijderd met behulp van Hallo `az network dns record-set <record-type> delete` opdracht.</span><span class="sxs-lookup"><span data-stu-id="c914b-234">Record sets can be deleted by using hello `az network dns record-set <record-type> delete` command.</span></span> <span data-ttu-id="c914b-235">Zie `azure network dns record-set <record-type> delete --help` voor help.</span><span class="sxs-lookup"><span data-stu-id="c914b-235">For help, see `azure network dns record-set <record-type> delete --help`.</span></span> <span data-ttu-id="c914b-236">Een recordset te verwijderen, verwijdert tevens alle records in de recordset Hallo.</span><span class="sxs-lookup"><span data-stu-id="c914b-236">Deleting a record set also deletes all records within hello record set.</span></span>

> [!NOTE]
> <span data-ttu-id="c914b-237">U kunt geen Hallo SOA- en NS-recordsets in het toppunt Hallo zone verwijderen (`--name "@"`).</span><span class="sxs-lookup"><span data-stu-id="c914b-237">You cannot delete hello SOA and NS record sets at hello zone apex (`--name "@"`).</span></span>  <span data-ttu-id="c914b-238">Deze worden automatisch gemaakt wanneer de zone Hallo is gemaakt en worden automatisch verwijderd wanneer de zone hello wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="c914b-238">These are created automatically when hello zone was created, and are deleted automatically when hello zone is deleted.</span></span>

<span data-ttu-id="c914b-239">Hallo volgende voorbeeld wordt verwijderd Hallo-recordset met de naam *www* van type A uit Hallo zone *contoso.com* in de resourcegroep *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="c914b-239">hello following example deletes hello record set named *www* of type A from hello zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
az network dns record-set a delete --resource-group myresourcegroup --zone-name contoso.com --name www
```

<span data-ttu-id="c914b-240">U bent na vragen aan gebruiker tooconfirm Hallo delete-bewerking.</span><span class="sxs-lookup"><span data-stu-id="c914b-240">You are prompted tooconfirm hello delete operation.</span></span> <span data-ttu-id="c914b-241">Dit vragen toosuppress gebruiken Hallo `--yes` overschakelen.</span><span class="sxs-lookup"><span data-stu-id="c914b-241">toosuppress this prompt, use hello `--yes` switch.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c914b-242">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c914b-242">Next steps</span></span>

<span data-ttu-id="c914b-243">Meer informatie over [zones en -records in Azure DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="c914b-243">Learn more about [zones and records in Azure DNS](dns-zones-records.md).</span></span>
<br>
<span data-ttu-id="c914b-244">Meer informatie over hoe te[beveiligen van uw zones en records](dns-protect-zones-recordsets.md) bij gebruik van Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="c914b-244">Learn how too[protect your zones and records](dns-protect-zones-recordsets.md) when using Azure DNS.</span></span>
