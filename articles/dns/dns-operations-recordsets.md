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
# <a name="manage-dns-records-and-recordsets-in-azure-dns-using-azure-powershell"></a>DNS-records en recordsets in Azure DNS met Azure PowerShell beheren

> [!div class="op_single_selector"]
> * [Azure Portal](dns-operations-recordsets-portal.md)
> * [Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-recordsets-cli.md)
> * [PowerShell](dns-operations-recordsets.md)

Dit artikel laat zien hoe toomanage DNS registreert voor uw DNS-zone met behulp van Azure PowerShell. DNS-records kunnen ook worden beheerd met behulp van de platformoverschrijdende Hallo [Azure CLI](dns-operations-recordsets-cli.md) of Hallo [Azure-portal](dns-operations-recordsets-portal.md).

Hallo-voorbeelden in dit artikel wordt ervan uitgegaan dat u al hebt [Azure PowerShell aangemeld, geïnstalleerd en wordt gemaakt van een DNS-zone](dns-operations-dnszones.md).

## <a name="introduction"></a>Inleiding

Voordat u DNS-records in Azure DNS maakt, moet u eerst de toounderstand hoe organiseert van DNS-records in DNS-recordsets in Azure DNS.

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

Zie [DNS-zones en -records](dns-zones-records.md) voor meer informatie over DNS-records in Azure DNS.


## <a name="create-a-new-dns-record"></a>Maak een nieuwe DNS-record

Als uw nieuwe record Hallo dezelfde naam geven en typt u als een bestaande record heeft, moet u deze te[toe te voegen de bestaande recordset toohello](#add-a-record-to-an-existing-record-set). Als uw nieuwe record een andere naam en type tooall bestaande records heeft, moet u een nieuwe recordset toocreate. 

### <a name="create-a-records-in-a-new-record-set"></a>"A" records in een nieuwe recordset maken

U recordsets maakt met behulp van Hallo `New-AzureRmDnsRecordSet` cmdlet. Bij het maken van een recordset moet u de naam van de recordset toospecify hello, Hallo zone, Hallo tijd toolive (TTL), het recordtype Hallo en Hallo records toobe gemaakt.

Hallo-parameters voor het toevoegen van records tooa recordset is afhankelijk van Hallo type Hallo Recordset. Bijvoorbeeld, wanneer u een recordset van het type "A", moet u toospecify Hallo IP-adres met de parameter Hallo `-IPv4Address`. Andere parameters worden gebruikt voor andere typen records. Zie [voorbeelden van recordtypen aanvullende](#additional-record-type-examples) voor meer informatie.

Hallo wordt volgende voorbeeld een recordset met Hallo relatieve naam 'www' Hallo 'contoso.com' van DNS-Zone. Hallo volledig gekwalificeerde naam van de recordset Hallo is 'www.contoso.com'. Hallo recordtype is "A" en Hallo TTL 3600 seconden is. Hallo-Recordset bevat één record, met IP-adres '1.2.3.4'.

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

toocreate een recordset op Hallo 'top' van een zone (in dit geval 'contoso.com'), gebruik de naam van Hallo Recordset ' @' (zonder aanhalingstekens):

```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

Als u een recordset met meer dan één record toocreate nodig, maakt eerst een lokale matrix en Hallo records toevoegen en Hallo matrix te geven`New-AzureRmDnsRecordSet` als volgt:

```powershell
$aRecords = @()
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4"
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "2.3.4.5"
New-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName MyResourceGroup -Ttl 3600 -RecordType A -DnsRecords $aRecords
```

[Metagegevens van de recordset](dns-zones-records.md#tags-and-metadata) mag gebruikte tooassociate toepassingsspecifieke gegevens met elke recordset als sleutel-waardeparen. Hallo volgende voorbeeld laat zien hoe toocreate een recordset met twee metagegevensvermeldingen ' afdeling Financiën =' en ' omgeving productie ='.

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") -Metadata @{ dept="finance"; environment="production" } 
```

Azure DNS ondersteunt ook 'empty' recordsets die als een tijdelijke aanduiding voor tooreserve een DNS-naam optreden kunnen voor het maken van DNS-records. Lege recordsets zijn zichtbaar in hello Azure DNS besturingselement vlak, maar worden weergegeven op Hallo Azure DNS-naamservers. Hallo volgende voorbeeld wordt een lege recordset gemaakt:

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords @()
```

## <a name="create-records-of-other-types"></a>Records van andere typen maken

Hebben gezien in detail hoe toocreate "A" registreert, Hallo volgen voorbeelden kunt u zien hoe toocreate records van andere typen die worden ondersteund door Azure DNS registreren.

In elk geval laten we zien hoe een record toocreate instelt met een enkel record. Hallo eerdere voorbeelden voor "A" records kunnen worden aangepast toocreate recordsets van andere typen met meerdere records met metagegevens, of lege record toocreate ingesteld.

We geven geen een toocreate bijvoorbeeld een recordset SOA-sinds SOA's zijn gemaakt en verwijderd met elke DNS-zone en kan niet worden gemaakt of afzonderlijk worden verwijderd. Echter, [Hallo SOA kan worden gewijzigd, zoals wordt weergegeven in het voorbeeld van een hoger](#to-modify-an-SOA-record).

### <a name="create-an-aaaa-record-set-with-a-single-record"></a>Een AAAA-recordset met één record maken

```powershell
New-AzureRmDnsRecordSet -Name "test-aaaa" -RecordType AAAA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ipv6Address "2607:f8b0:4009:1803::1005") 
```

### <a name="create-a-cname-record-set-with-a-single-record"></a>Een CNAME-recordset met één record maken

> [!NOTE]
> Hallo DNS-standaarden staan niet toe dat CNAME-records in het toppunt van Hallo van een zone (`-Name '@'`), noch staan ze recordsets met meer dan één record.
> 
> Zie voor meer informatie [CNAME-records](dns-zones-records.md#cname-records).


```powershell
New-AzureRmDnsRecordSet -Name "test-cname" -RecordType CNAME -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Cname "www.contoso.com") 
```

### <a name="create-an-mx-record-set-with-a-single-record"></a>Een MX-recordset met één record maken

In dit voorbeeld gebruiken we Hallo recordnaam ' @' toocreate een MX-record in het toppunt Hallo zone (in dit geval 'contoso.com').


```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType MX -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Exchange "mail.contoso.com" -Preference 5) 
```

### <a name="create-an-ns-record-set-with-a-single-record"></a>Een NS-recordset met één record maken

```powershell
New-AzureRmDnsRecordSet -Name "test-ns" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Nsdname "ns1.contoso.com") 
```

### <a name="create-a-ptr-record-set-with-a-single-record"></a>Een PTR-recordset met één record maken

In dit geval ' Mijn-arpa-zone.com' vertegenwoordigt Hallo ARPA zone voor reverse lookup voor uw IP-adresbereik. Elke PTR-recordset in deze zone komt overeen tooan IP-adres binnen deze IP-adresbereik. Hallo recordnaam "10" is de laatste octet Hallo van Hallo IP-adres binnen deze IP-bereik dat wordt vertegenwoordigd door deze record.

```powershell
New-AzureRmDnsRecordSet -Name 10 -RecordType PTR -ZoneName "my-arpa-zone.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "myservice.contoso.com") 
```

### <a name="create-an-srv-record-set-with-a-single-record"></a>Een SRV-recordset met één record maken

Bij het maken van een [SRV-Recordset](dns-zones-records.md#srv-records), geef Hallo  *\_service* en  *\_protocol* in Hallo-of RecordsetNaam. Er is geen tooinclude moet ' @' in hello RecordsetNaam wanneer een SRV-record maken in het toppunt zone Hallo ingesteld.

```powershell
New-AzureRmDnsRecordSet -Name "_sip._tls" -RecordType SRV -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Priority 0 -Weight 5 -Port 8080 -Target "sip.contoso.com") 
```


### <a name="create-a-txt-record-set-with-a-single-record"></a>Een TXT-recordset met één record maken

Hallo volgende voorbeeld ziet u hoe een TXT-toocreate opnemen. Zie voor meer informatie over de maximale tekenreekslengte hello wordt ondersteund in de TXT-records [TXT-records](dns-zones-records.md#txt-records).

```powershell
New-AzureRmDnsRecordSet -Name "test-txt" -RecordType TXT -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Value "This is a TXT record") 
```


## <a name="get-a-record-set"></a>Een recordset ophalen

Gebruik een bestaande recordset tooretrieve `Get-AzureRmDnsRecordSet`. Deze cmdlet retourneert een lokaal object met Hallo-recordset in Azure DNS.

Net als bij `New-AzureRmDnsRecordSet`, krijgt de naam van de Hallo recordset moet een *relatieve* naam, wat betekent dat het Hallo-zonenaam moet uitsluiten. U moet ook toospecify Hallo recordtype en Hallo-recordset met Hallo-zone.

Hallo ziet volgende voorbeeld u hoe tooretrieve een record instellen. In dit voorbeeld Hallo zone is opgegeven met behulp van Hallo `-ZoneName` en `-ResourceGroupName` parameters.

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

U kunt ook u kunt ook opgeven met behulp van een zone-object dat is doorgegeven met Hallo Hallo-zone `-Zone` parameter.

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

## <a name="list-record-sets"></a>Lijst met recordsets

U kunt ook `Get-AzureRmDnsZone` toolist recordsets in een zone door Hallo weg te laten `-Name` en/of `-RecordType` parameters.

Hallo retourneert volgende voorbeeld alle recordsets in Hallo zone:

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

Hallo volgende voorbeeld ziet u hoe-alle recordsets van een bepaald type kunnen worden opgehaald door te geven Hallo recordtype terwijl weglaten Hallo record naam instellen:

```powershell
$recordsets = Get-AzureRmDnsRecordSet -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

alle recordsets met een opgegeven naam tooretrieve over recordtypen, moet u tooretrieve alle recordsets en vervolgens filter Hallo resultaten:

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | where {$_.Name.Equals("www")}
```

In alle Hallo bovenstaande voorbeelden Hallo zone worden opgegeven met behulp van Hallo `-ZoneName` en `-ResourceGroupName`parameters (zoals weergegeven), of door te geven van een zone-object:

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$recordsets = Get-AzureRmDnsRecordSet -Zone $zone
```

## <a name="add-a-record-tooan-existing-record-set"></a>Een record tooan bestaande recordset toevoegen

een bestaande record record tooan tooadd instellen, voert u Hallo drie stappen te volgen:

1. De bestaande recordset Hallo ophalen

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. Hallo nieuwe records toohello lokale recordset toevoegen. Dit is een offline-bewerking.

    ```powershell
    Add-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. Hallo wijziging back toohello Azure DNS-service worden doorgevoerd. 

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $rs
    ```

Met behulp van `Set-AzureRmDnsRecordSet` *vervangt* Hallo bestaande recordset in Azure DNS (en alle records die deze bevat) met opgegeven Hallo-Recordset. [ETag controles](dns-zones-records.md#etags) worden gebruikt tooensure gelijktijdige wijzigingen worden niet overschreven. U kunt optioneel Hallo `-Overwrite` overschakelen toosuppress deze controles.

Deze reeks bewerkingen kan ook worden *doorgesluisd*, wat betekent dat u Hallo Recordset object Hallo pipe gebruiken in plaats van deze doorgegeven als parameter doorgeven:

```powershell
Get-AzureRmDnsRecordSet -Name "www" –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Add-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

Hallo voorbeelden bovenstaande van hoe tooadd een "A" bestaande record tooan-record van het type "A" instellen. Een vergelijkbare reeks bewerkingen is gebruikte tooadd recordsets toorecord van andere typen, vervangen door Hallo `-Ipv4Address` parameter van `Add-AzureRmDnsRecordConfig` met andere parameters specifieke tooeach-recordtype. Hallo parameters voor elk recordtype zijn Hallo dezelfde als voor Hallo `New-AzureRmDnsRecordConfig` cmdlet, zoals wordt weergegeven in [voorbeelden van recordtypen aanvullende](#additional-record-type-examples) hierboven.

Recordsets van het type 'CNAME-' of 'SOA' mag niet meer dan een record bevatten. Deze beperking voortvloeit uit Hallo DNS-standaarden. Het is niet een beperking van Azure DNS.

## <a name="remove-a-record-from-an-existing-record-set"></a>Een record verwijderen uit een bestaande recordset

Hallo proces tooremove een record van een recordset is vergelijkbaar toohello proces tooadd een record tooan bestaande recordset:

1. De bestaande recordset Hallo ophalen

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. Hallo-record verwijderen uit het Hallo lokale Recordset-object. Dit is een offline-bewerking. Hallo-record die wordt verwijderd moet een exacte overeenkomst aan een bestaande record binnen alle parameters.

    ```powershell
    Remove-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. Hallo wijziging back toohello Azure DNS-service worden doorgevoerd. Gebruik Hallo optionele `-Overwrite` overschakelen toosuppress [Etag controleert](dns-zones-records.md#etags) voor gelijktijdige wijzigingen.

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $Rs
    ```

Met behulp van Hallo hierboven sequence tooremove Hallo laatste record van een recordset Hallo recordset niet verwijderen, in plaats daarvan het verlaten van een lege recordset. een recordset volledig, tooremove Zie [verwijderen van een recordset](#delete-a-record-set).

Op dezelfde manier Recordset tooadding records tooa, Hallo reeks operations tooremove een recordset kan ook worden doorgesluisd:

```powershell
Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Remove-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

Verschillende recordtypen worden ondersteund door het doorgeven van het juiste type-specifieke parameters hello te`Remove-AzureRmDnsRecordSet`. Hallo parameters voor elk recordtype zijn Hallo dezelfde als voor Hallo `New-AzureRmDnsRecordConfig` cmdlet, zoals wordt weergegeven in [voorbeelden van recordtypen aanvullende](#additional-record-type-examples) hierboven.


## <a name="modify-an-existing-record-set"></a>Een bestaande recordset wijzigen

Hallo-stappen voor het wijzigen van een bestaande recordset zijn vergelijkbaar toohello stappen bij het toevoegen of verwijderen van records uit een Recordset:

1. Ophalen van de bestaande record Hallo ingesteld met behulp van `Get-AzureRmDnsRecordSet`.
2. Hallo lokale Recordset object door te wijzigen:
    * Het toevoegen of verwijderen van records
    * Hallo-parameters van bestaande records wijzigen
    * Het wijzigen van de record Hallo ingesteld metagegevens en toolive TTL (time)
3. Uw wijzigingen met behulp van Hallo `Set-AzureRmDnsRecordSet` cmdlet. Dit *vervangt* Hallo bestaande recordset in Azure DNS met Hallo-recordset is opgegeven.

Wanneer u `Set-AzureRmDnsRecordSet`, [Etag controleert](dns-zones-records.md#etags) worden gebruikt tooensure gelijktijdige wijzigingen worden niet overschreven. U kunt optioneel Hallo `-Overwrite` overschakelen toosuppress deze controles.

### <a name="tooupdate-a-record-in-an-existing-record-set"></a>een record in een bestaande record tooupdate instellen

In dit voorbeeld wijzigen we Hallo IP-adres van een bestaande "A" record:

```powershell
$rs = Get-AzureRmDnsRecordSet -name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Ipv4Address = "9.8.7.6"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-an-soa-record"></a>toomodify SOA-record

U kunt toevoegen of verwijderen van records uit Hallo automatisch gemaakt SOA-record is ingesteld in het toppunt Hallo zone (`-Name "@"`, inclusief de aanhalingstekens). Echter kunt u een van de parameters Hallo binnen Hallo SOA-record (met uitzondering van de "Host") en de TTL van de recordset Hallo.

Hallo volgende voorbeeld wordt getoond hoe toochange hello *e* eigenschap Hallo SOA-record:

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType SOA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Email = "admin.contoso.com"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-ns-records-at-hello-zone-apex"></a>toomodify NS-records in het toppunt Hallo zone

Hallo NS-recordset in het toppunt Hallo zone wordt automatisch gemaakt met elke DNS-zone. Het bevat Hallo-namen van hello Azure DNS-naam servers toegewezen toohello zone.

U kunt de naam van de aanvullende servers toothis NS-recordset, toosupport CO domeinen met meer dan één DNS-provider host toevoegen. U kunt ook wijzigen Hallo TTL en metagegevens voor deze recordset. U kan echter verwijderen of wijzigen Hallo vooraf ingestelde Azure DNS-naamservers.

Houd er rekening mee dat dit alleen toohello NS recordset in het toppunt zone Hallo geldt. Andere NS recordsets in de zone (als gebruikte toodelegate onderliggende zones) kunnen worden gewijzigd zonder beperking.

Hallo volgende voorbeeld ziet u hoe tooadd een extra naam server toohello NS-record instellen in het toppunt Hallo zone:

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Add-AzureRmDnsRecordConfig -RecordSet $rs -Nsdname ns1.myotherdnsprovider.com
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-record-set-metadata"></a>metagegevens van de recordset toomodify

[Metagegevens van de recordset](dns-zones-records.md#tags-and-metadata) mag gebruikte tooassociate toepassingsspecifieke gegevens met elke recordset als sleutel-waardeparen.

Hallo ziet volgende voorbeeld u hoe toomodify Hallo metagegevens van een bestaande record instellen:

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


## <a name="delete-a-record-set"></a>Een recordset verwijderen

Recordsets kunnen worden verwijderd met behulp van Hallo `Remove-AzureRmDnsRecordSet` cmdlet. Een recordset te verwijderen, verwijdert tevens alle records in de recordset Hallo.

> [!NOTE]
> U kunt geen Hallo SOA- en NS-recordsets in het toppunt Hallo zone verwijderen (`-Name '@'`).  Deze wordt automatisch door Azure DNS gemaakt wanneer Hallo zone is gemaakt en worden automatisch verwijderd wanneer Hallo zone wordt verwijderd.

Hallo ziet volgende voorbeeld u hoe toodelete een record instellen. In dit voorbeeld worden Hallo Recordset naam, type recordset zonenaam en resourcegroep elk expliciet opgegeven.

```powershell
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

U kunt ook Hallo recordset kan worden opgegeven met de naam en type en Hallo zone opgegeven met behulp van een object:

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

Als een derde optie Hallo-Recordset zelf, worden opgegeven met behulp van een Recordset-object:

```powershell
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -RecordSet $rs
```

Wanneer u Hallo Recordset toobe verwijderd opgeeft met behulp van een object Recordset [Etag controleert](dns-zones-records.md#etags) worden gebruikt tooensure gelijktijdige wijzigingen worden niet verwijderd. U kunt optioneel Hallo `-Overwrite` overschakelen toosuppress deze controles.

Hallo Recordset object kan ook worden doorgesluisd in plaats van dat wordt doorgegeven als parameter:

```powershell
Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | Remove-AzureRmDnsRecordSet
```

## <a name="confirmation-prompts"></a>Bevestiging vragen

Hallo `New-AzureRmDnsRecordSet`, `Set-AzureRmDnsRecordSet`, en `Remove-AzureRmDnsRecordSet` cmdlets alle bevestiging vragen ondersteunen.

Elke cmdlet vraagt om bevestiging als hello `$ConfirmPreference` PowerShell voorkeursvariabele een waarde heeft van `Medium` of lager. Sinds de standaardwaarde Hallo voor `$ConfirmPreference` is `High`, deze vragen zijn niet opgegeven voor het met de standaardinstellingen voor PowerShell Hallo.

U kunt de huidige Hallo overschrijven `$ConfirmPreference` instelling met de Hallo `-Confirm` parameter. Als u opgeeft `-Confirm` of `-Confirm:$True` , Hallo cmdlet vraagt u om bevestiging voordat deze wordt uitgevoerd. Als u opgeeft `-Confirm:$False` , Hallo cmdlet wordt u niet gevraagd om bevestiging. 

Voor meer informatie over `-Confirm` en `$ConfirmPreference`, Zie [over Voorkeursvariabelen](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).

## <a name="next-steps"></a>Volgende stappen

Meer informatie over [zones en -records in Azure DNS](dns-zones-records.md).
<br>
Meer informatie over hoe te[beveiligen van uw zones en records](dns-protect-zones-recordsets.md) bij gebruik van Azure DNS.
<br>
Bekijk Hallo [Azure DNS PowerShell-naslagdocumentatie](/powershell/module/azurerm.dns).
