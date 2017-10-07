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
# <a name="manage-dns-records-and-recordsets-in-azure-dns-using-hello-azure-cli-20"></a>DNS-records en recordsets in Azure DNS met Azure CLI 2.0 Hallo beheren

> [!div class="op_single_selector"]
> * [Azure Portal](dns-operations-recordsets-portal.md)
> * [Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-recordsets-cli.md)
> * [PowerShell](dns-operations-recordsets.md)

Dit artikel laat zien hoe toomanage DNS-records voor de DNS-zone met behulp van Hallo platformoverschrijdende Azure-opdrachtregelinterface (CLI) 2.0, die beschikbaar voor Windows, Mac en Linux is. U kunt ook de DNS-records met beheren [Azure PowerShell](dns-operations-recordsets.md) of Hallo [Azure-portal](dns-operations-recordsets-portal.md).

## <a name="cli-versions-toocomplete-hello-task"></a>CLI-versies toocomplete Hallo taak

U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:

* [Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) -onze CLI voor Hallo klassieke en resource management implementatiemodellen.
* [Azure CLI 2.0](dns-operations-recordsets-cli.md) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel.

Hallo-voorbeelden in dit artikel wordt ervan uitgegaan dat u al hebt [hello Azure CLI 2.0, aangemeld, geïnstalleerd en wordt gemaakt van een DNS-zone](dns-operations-dnszones-cli.md).

## <a name="introduction"></a>Inleiding

Voordat u DNS-records in Azure DNS maakt, moet u eerst de toounderstand hoe organiseert van DNS-records in DNS-recordsets in Azure DNS.

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

Zie [DNS-zones en -records](dns-zones-records.md) voor meer informatie over DNS-records in Azure DNS.

## <a name="create-a-dns-record"></a>Een DNS-record maken

toocreate een DNS-record gebruiken Hallo `az network dns record-set <record-type> set-record` opdracht (waarbij `<record-type>` is Hallo type record, Internet Explorer een, srv, txt, enz.) Zie `az network dns record-set --help` voor help.

Wanneer een record te maken, moet u toospecify Hallo Resourcegroepnaam, zonenaam, recordset naam, Hallo recordtype en Hallo-details van Hallo-record wordt gemaakt. Hallo Recordset naam moet een *relatieve* naam, wat betekent dat het Hallo-zonenaam moet uitsluiten.

Als de recordset Hallo niet al bestaat, wordt deze opdracht het voor u gemaakt. Als het Hallo-Recordset al bestaat, wordt met deze opdracht Hallo record opgeven van de bestaande recordset toohello toegevoegd.

Als er een nieuwe recordset wordt gemaakt, wordt een standaard time-to-live (TTL) van 3600 gebruikt. Voor instructies over hoe toouse verschillende TTLs zien [maken van een DNS-Recordset](#create-a-dns-record-set).

Hallo volgende voorbeeld maakt u een A-record genoemd *www* in Hallo zone *contoso.com* in de resourcegroep Hallo *MyResourceGroup*. IP-adres van een record is Hallo Hallo *1.2.3.4*.

```azurecli
az network dns record-set a set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name www --ipv4-address 1.2.3.4
```

toocreate een record in Hallo apex van Hallo zone instellen (in dit geval 'contoso.com'), gebruik Hallo recordnaam ' @ ', inclusief de aanhalingstekens Hallo:

```azurecli
az network dns record-set a set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "@" --ipv4-address 1.2.3.4
```

## <a name="create-a-dns-record-set"></a>Een DNS-recordset maken

Hallo bovenstaande voorbeelden Hallo DNS-record is de toegevoegde tooan bestaande recordset of Hallo recordset is gemaakt *impliciet*. U kunt ook Hallo-recordset maken *expliciet* voordat tooit toe te voegen registreert. Azure DNS ondersteunt 'empty' recordsets die als een tijdelijke aanduiding voor tooreserve een DNS-naam optreden kunnen voor het maken van DNS-records. Lege recordsets zijn zichtbaar in hello Azure DNS vlak besturingselement, maar worden niet weergegeven op Hallo Azure DNS-naamservers.

Recordsets zijn gemaakt met behulp van Hallo `az network dns record-set <record-type> create` opdracht. Zie `az network dns record-set <record-type> create --help` voor help.

Hallo-Recordset expliciet maakt, kunt u toospecify Recordset eigenschappen zoals Hallo [Time To Live (TTL)](dns-zones-records.md#time-to-live) en metagegevens. [Metagegevens van de recordset](dns-zones-records.md#tags-and-metadata) mag gebruikte tooassociate toepassingsspecifieke gegevens met elke recordset als sleutel-waardeparen.

Hallo volgende voorbeeld wordt een lege recordset van het type "A" met een TTL 60 seconden met behulp van Hallo `--ttl` parameter (korte versie `-l`):

```azurecli
az network dns record-set a create --resource-group myresourcegroup --zone-name contoso.com --name www --ttl 60
```

Hallo volgende voorbeeld maakt u een recordset met twee metagegevensvermeldingen ' afdeling Financiën = ' en ' omgeving = productie ', met behulp van Hallo `--metadata` parameter:

```azurecli
az network dns record-set a create --resource-group myresourcegroup --zone-name contoso.com --name www --metadata "dept=finance" "environment=production"
```

Gemaakt van een lege recordset records kunnen worden toegevoegd met behulp van `azure network dns record-set <record-type> set-record` zoals beschreven in [maken van een DNS-record](#create-a-dns-record).

## <a name="create-records-of-other-types"></a>Records van andere typen maken

Hebben gezien in detail hoe toocreate "A" registreert, Hallo volgen voorbeelden kunt u zien hoe toocreate record van andere recordtypen worden ondersteund door Azure DNS.

Hallo-parameters gebruikt toospecify Hallo record gegevens, is afhankelijk van Hallo type Hallo record. Bijvoorbeeld, opgeven u voor een record van het type "A" hello IPv4-adres met de parameter Hallo `--ipv4-address <IPv4 address>`. Hallo parameters voor elk recordtype kunt vermeld met `az network dns record-set <record-type> set-record --help`.

In elk geval laten we zien hoe toocreate één record. Hallo-record is toegevoegd toohello bestaande recordset of een recordset impliciet gemaakt. Voor meer informatie over het maken van recordsets en definiëren van record parameter expliciet, raadpleegt u [maken van een DNS-Recordset](#create-a-dns-record-set).

We geven geen een toocreate bijvoorbeeld een recordset SOA-sinds SOA's zijn gemaakt en verwijderd met elke DNS-zone en kan niet worden gemaakt of afzonderlijk worden verwijderd. Echter, [Hallo SOA kan worden gewijzigd, zoals wordt weergegeven in het voorbeeld van een hoger](#to-modify-an-SOA-record).

### <a name="create-an-aaaa-record"></a>Een AAAA-record maken

```azurecli
az network dns record-set aaaa set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-aaaa --ipv6-address 2607:f8b0:4009:1803::1005
```

### <a name="create-a-cname-record"></a>Een CNAME-record maken

> [!NOTE]
> Hallo DNS-standaarden staan niet toe dat CNAME-records in het toppunt van Hallo van een zone (`--Name "@"`), noch staan ze recordsets met meer dan één record.
> 
> Zie voor meer informatie [CNAME-records](dns-zones-records.md#cname-records).

```azurecli
az network dns record-set cname set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-cname --cname www.contoso.com
```

### <a name="create-an-mx-record"></a>Een MX-record maken

In dit voorbeeld gebruiken we Hallo recordnaam "@" toocreate Hallo MX-record in het toppunt Hallo zone (in dit geval 'contoso.com').

```azurecli
az network dns record-set mx set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "@" --exchange mail.contoso.com --preference 5
```

### <a name="create-an-ns-record"></a>Een NS-record maken

```azurecli
az network dns record-set ns set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-ns --nsdname ns1.contoso.com
```

### <a name="create-a-ptr-record"></a>PTR-record maken

In dit geval ' Mijn-arpa-zone.com' vertegenwoordigt Hallo ARPA-zone die uw IP-adresbereik vertegenwoordigt. Elke PTR-recordset in deze zone komt overeen tooan IP-adres binnen deze IP-adresbereik.  Hallo recordnaam "10" is de laatste octet Hallo van Hallo IP-adres binnen deze IP-bereik dat wordt vertegenwoordigd door deze record.

```azurecli
az network dns record-set ptr set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name my-arpa.zone.com --ptrdname myservice.contoso.com
```

### <a name="create-an-srv-record"></a>Een SRV-record maken

Bij het maken van een [SRV-Recordset](dns-zones-records.md#srv-records), geef Hallo  *\_service* en  *\_protocol* in Hallo-of RecordsetNaam. Er is geen tooinclude moet ' @ ' in hello RecordsetNaam wanneer een SRV-record maken in het toppunt zone Hallo ingesteld.

```azurecli
az network dns record-set srv set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name _sip._tls --priority 10 --weight 5 --port 8080 --target sip.contoso.com
```

### <a name="create-a-txt-record"></a>Een TXT-record maken

Hallo volgende voorbeeld ziet u hoe een TXT-toocreate opnemen. Zie voor meer informatie over de maximale tekenreekslengte hello wordt ondersteund in de TXT-records [TXT-records](dns-zones-records.md#txt-records).

```azurecli
az network dns record-set txt set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-txt --value "This is a TXT record"
```

## <a name="get-a-record-set"></a>Een recordset ophalen

Gebruik een bestaande recordset tooretrieve `az network dns record-set <record-type> show`. Zie `az network dns record-set <record-type> show --help` voor help.

Als bij het maken van een record of een recordset Hallo RecordsetNaam gegeven moet een *relatieve* naam, wat betekent dat het Hallo-zonenaam moet uitsluiten. Moet u ook toospecify Hallo recordtype, Hallo zone met Hallo record ingesteld en Hallo resourcegroep met Hallo-zone.

Hallo volgende voorbeeld wordt opgehaald Hallo record *www* van type A uit zone *contoso.com* in de resourcegroep *MyResourceGroup*:

```azurecli
az network dns record-set a show --resource-group myresourcegroup --zone-name contoso.com --name www
```

## <a name="list-record-sets"></a>Lijst met recordsets

U kunt alle records in een DNS-zone weergeven met behulp van Hallo `az network dns record-set list` opdracht. Zie `az network dns record-set list --help` voor help.

In dit voorbeeld retourneert alle recordsets in de zone Hallo *contoso.com*, in de resourcegroep *MyResourceGroup*, ongeacht of het recordtype:

```azurecli
az network dns record-set list --resource-group myresourcegroup --zone-name contoso.com
```

In dit voorbeeld retourneert alle recordsets die overeenkomen met de Hallo gegeven recordtype (in dit geval "A" records):

```azurecli
az network dns record-set a list --resource-group myresourcegroup --zone-name contoso.com 
```

## <a name="add-a-record-tooan-existing-record-set"></a>Een record tooan bestaande recordset toevoegen

U kunt `az network dns record-set <record-type> set-record` zowel toocreate een record in een nieuwe record instellen of tooadd een record tooan bestaande recordset.

Zie voor meer informatie [maken van een DNS-record](#create-a-dns-record) en [records maken van andere typen](#create-records-of-other-types) hierboven.

## <a name="remove-a-record-from-an-existing-record-set"></a>Een record verwijderen uit een bestaande recordset.

tooremove een DNS-server registreren van een bestaande recordset gebruik `az network dns record-set <record-type> remove-record`. Zie `az network dns record-set <record-type> remove-record -h` voor help.

Deze opdracht wordt een DNS-record verwijderd uit een recordset. Als de laatste record Hallo in een recordset is verwijderd, wordt Hallo-Recordset zelf ook verwijderd. tookeep hello lege recordset gebruiken in plaats daarvan Hallo `--keep-empty-record-set` optie.

U moet toospecify Hallo record toobe verwijderd en Hallo zone moet worden verwijderd uit met dezelfde parameters als Hallo bij het maken van een record met `az network dns record-set <record-type> set-record`. Deze parameters worden beschreven in [maken van een DNS-record](#create-a-dns-record) en [records maken van andere typen](#create-records-of-other-types) hierboven.

Hallo volgende voorbeeld verwijdert een record met waarde '1.2.3.4' uit de record Hallo set met de naam Hallo *www* in Hallo zone *contoso.com*, in de resourcegroep Hallo *MyResourceGroup*.

```azurecli
az network dns record-set a remove-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "www" --ipv4-address 1.2.3.4
```

## <a name="modify-an-existing-record-set"></a>Een bestaande recordset wijzigen

Elke recordset bevat een [time to live (TTL)](dns-zones-records.md#time-to-live), [metagegevens](dns-zones-records.md#tags-and-metadata), en DNS-records. Hallo volgende secties wordt uitgelegd hoe toomodify van deze eigenschappen.

### <a name="toomodify-an-a-aaaa-mx-ns-ptr-srv-or-txt-record"></a>toomodify A, AAAA, MX, NS, PTR, SRV- of TXT-record

toomodify een bestaande record van type A, AAAA, MX, NS, PTR, SRV- of TXT, moet u eerst een nieuwe record en toevoegen vervolgens verwijderen Hallo bestaande record. Voor gedetailleerde instructies voor het toodelete en records toevoegen, Zie Hallo eerdere secties van dit artikel.

Hallo volgende voorbeeld ziet u hoe een record "A", van IP-adres 1.2.3.4 tooIP toomodify 5.6.7.8 aanpakken:

```azurecli
az network dns record-set a set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name www --ipv4-address 5.6.7.8
az network dns record-set a remove-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name www --ipv4-address 1.2.3.4
```

U kan niet toevoegen, verwijderen of wijzigen van de records in Hallo automatisch gemaakt NS-recordset in het toppunt zone Hallo Hallo (`--Name "@"`, inclusief de aanhalingstekens). Hallo alleen wijzigingen toegestaan zijn voor deze recordset toomodify Hallo Recordset TTL en metagegevens.

### <a name="toomodify-a-cname-record"></a>toomodify een CNAME-record

In tegenstelling tot de meeste andere recordtypen mag een CNAME-Recordset alleen één record.  U kunt de Hallo huidige waarde daarom niet vervangen door een nieuwe record toevoegen en verwijderen van de bestaande record Hallo als voor andere typen records.

In plaats daarvan gebruikt u een CNAME-record toomodify `az network dns record-set cname set-record`. Zie voor meer informatie`az network dns record-set cname set-record --help`

Hallo voorbeeld wijzigt Hallo CNAME-Recordset *www* in Hallo zone *contoso.com*, in de resourcegroep *MyResourceGroup*, toopoint te 'www.fabrikam.net' in plaats van de bestaande waarde:

```azurecli
az network dns record-set cname set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-cname --cname www.fabrikam.net
``` 

### <a name="toomodify-an-soa-record"></a>toomodify SOA-record

In tegenstelling tot de meeste andere recordtypen mag een CNAME-Recordset alleen één record.  U kunt de Hallo huidige waarde daarom niet vervangen door een nieuwe record toevoegen en verwijderen van de bestaande record Hallo als voor andere typen records.

In plaats daarvan toomodify Hallo SOA-record gebruiken `az network dns record-set soa update`. Zie `az network dns record-set soa update --help` voor help.

Hallo volgende voorbeeld ziet u hoe de eigenschap tooset Hallo 'e' Hallo SOA legt voor Hallo zone *contoso.com* in de resourcegroep Hallo *MyResourceGroup*:

```azurecli
az network dns record-set soa update --resource-group myresourcegroup --zone-name contoso.com --email admin.contoso.com
```

### <a name="toomodify-ns-records-at-hello-zone-apex"></a>toomodify NS-records in het toppunt Hallo zone

Hallo NS-recordset in het toppunt Hallo zone wordt automatisch gemaakt met elke DNS-zone. Het bevat Hallo-namen van hello Azure DNS-naam servers toegewezen toohello zone.

U kunt de naam van de aanvullende servers toothis NS-recordset, toosupport CO domeinen met meer dan één DNS-provider host toevoegen. U kunt ook wijzigen Hallo TTL en metagegevens voor deze recordset. U kan echter verwijderen of wijzigen Hallo vooraf ingestelde Azure DNS-naamservers.

Houd er rekening mee dat dit alleen toohello NS recordset in het toppunt zone Hallo geldt. Andere NS recordsets in de zone (als gebruikte toodelegate onderliggende zones) kunnen worden gewijzigd zonder beperking.

Hallo volgende voorbeeld ziet u hoe tooadd een extra naam server toohello NS-record instellen in het toppunt Hallo zone:

```azurecli
az network dns record-set ns set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "@" --nsdname ns1.myotherdnsprovider.com 
```

### <a name="toomodify-hello-ttl-of-an-existing-record-set"></a>toomodify hello TTL van een bestaande record instellen

toomodify hello TTL van een bestaande record instellen, gebruikt u `azure network dns record-set <record-type> update`. Zie `azure network dns record-set <record-type> update --help` voor help.

Hallo volgende voorbeeld ziet u hoe toomodify een recordset TTL, in dit geval too60 seconden:

```azurecli
az network dns record-set a update --resource-group myresourcegroup --zone-name contoso.com --name www --set ttl=60
```

### <a name="toomodify-hello-metadata-of-an-existing-record-set"></a>toomodify hello metagegevens van een bestaande record ingesteld

[Metagegevens van de recordset](dns-zones-records.md#tags-and-metadata) mag gebruikte tooassociate toepassingsspecifieke gegevens met elke recordset als sleutel-waardeparen. toomodify hello metagegevens van een bestaande record ingesteld, gebruikt u `az network dns record-set <record-type> update`. Zie `az network dns record-set <record-type> update --help` voor help.

Hallo volgende voorbeeld laat zien hoe toomodify een recordset met twee metagegevensvermeldingen ' afdeling Financiën = ' en ' omgeving productie = '. Merk op dat alle bestaande metagegevens is *vervangen* door Hallo waarden op basis van.

```azurecli
az network dns record-set a update --resource-group myresourcegroup --zone-name contoso.com --name www --set metadata.dept=finance metadata.environment=production
```

## <a name="delete-a-record-set"></a>Een recordset verwijderen

Recordsets kunnen worden verwijderd met behulp van Hallo `az network dns record-set <record-type> delete` opdracht. Zie `azure network dns record-set <record-type> delete --help` voor help. Een recordset te verwijderen, verwijdert tevens alle records in de recordset Hallo.

> [!NOTE]
> U kunt geen Hallo SOA- en NS-recordsets in het toppunt Hallo zone verwijderen (`--name "@"`).  Deze worden automatisch gemaakt wanneer de zone Hallo is gemaakt en worden automatisch verwijderd wanneer de zone hello wordt verwijderd.

Hallo volgende voorbeeld wordt verwijderd Hallo-recordset met de naam *www* van type A uit Hallo zone *contoso.com* in de resourcegroep *MyResourceGroup*:

```azurecli
az network dns record-set a delete --resource-group myresourcegroup --zone-name contoso.com --name www
```

U bent na vragen aan gebruiker tooconfirm Hallo delete-bewerking. Dit vragen toosuppress gebruiken Hallo `--yes` overschakelen.

## <a name="next-steps"></a>Volgende stappen

Meer informatie over [zones en -records in Azure DNS](dns-zones-records.md).
<br>
Meer informatie over hoe te[beveiligen van uw zones en records](dns-protect-zones-recordsets.md) bij gebruik van Azure DNS.
