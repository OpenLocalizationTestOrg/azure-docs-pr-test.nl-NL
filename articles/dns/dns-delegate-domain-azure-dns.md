---
title: aaaDelegate uw domein tooAzure DNS | Microsoft Docs
description: Begrijpen hoe domeindelegering toochange en gebruik Azure DNS name servers tooprovide domeinen te hosten.
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 257da6ec-d6e2-4b6f-ad76-ee2dde4efbcc
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: gwallace
ms.openlocfilehash: f780bdaa416150e5e3afe6c6845dc75ba54b6203
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="delegate-a-domain-tooazure-dns"></a>Een domein tooAzure DNS overdragen

Azure DNS kunt u een DNS-zone toohost en Hallo DNS-records voor een domein in Azure beheren. Om DNS-query's voor een domein tooreach Azure DNS, Hallo domein toobe heeft gedelegeerd tooAzure DNS van Hallo bovenliggende domein. Houd er rekening mee Azure DNS is niet de domeinregistrar Hallo. Dit artikel wordt uitgelegd hoe toodelegate uw domein tooAzure DNS.

Voor domeinen die zijn aangeschaft bij een registrar, biedt uw registrar Hallo optie tooset van deze NS-records. U hoeft geen tooown een toocreate domein een DNS-zone met die domeinnaam in Azure DNS. U hoeft echter tooown Hallo domein tooset up Hallo delegering tooAzure DNS met Hallo registrar.

Stel dat u koopt Hallo domein 'contoso.net' en een zone met contoso.net' hello name' in Azure DNS maakt. Als de eigenaar van de Hallo van Hallo domein biedt uw registrar dat u hello optie tooconfigure Hallo serveradressen (dat wil zeggen, Hallo NS-records) voor uw domein. Hallo registrar slaat deze NS-records in Hallo bovenliggende domein in dit geval '.net'. Vervolgens kunnen clients Hallo wereld gerichte tooyour domein in Azure DNS-zone worden bij het tooresolve DNS-records in 'contoso.net'.

## <a name="create-a-dns-zone"></a>Een DNS-zone maken

1. Meld u aan toohello Azure-portal
1. Klik op Hallo Hub-menu en klik op **Nieuw > netwerken >** en klik vervolgens op **DNS-zone** tooopen Hallo maken DNS-zone blade.

    ![DNS-zone](./media/dns-domain-delegation/dns.png)

1. Op Hallo **maken DNS-zone** blade Voer Hallo volgende waarden en klik vervolgens op **maken**:

   | **Instelling** | **Waarde** | **Details** |
   |---|---|---|
   |**Naam**|contoso.net|Hallo-naam van Hallo DNS-zone|
   |**Abonnement**|[Uw abonnement]|Selecteer een abonnement toocreate Hallo toepassingsgateway in.|
   |**Resourcegroep**|**Nieuwe maken:** contosoRG|Maak een resourcegroep. de naam van resourcegroep Hallo moet uniek zijn binnen het Hallo-abonnement die u hebt geselecteerd. meer informatie over resourcegroepen lezen Hallo toolearn [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overzichtsartikel.|
   |**Locatie**|VS - west||

> [!NOTE]
> Hallo resourcegroep toohello locatie van resourcegroep Hallo verwijst, en heeft geen invloed op Hallo DNS-zone. Hallo DNS-zone locatie is altijd 'global' en niet wordt weergegeven.

## <a name="retrieve-name-servers"></a>Naamservers ophalen

Voordat u uw DNS-zone tooAzure DNS delegeren kunt, moet u eerst tooknow Hallo servernamen voor uw zone. Telkens wanneer er een zone wordt gemaakt, wijst Azure DNS naamservers uit een groep toe.

1. Met de Hallo DNS-zone in hello Azure-portal gemaakt **Favorieten** deelvenster, klikt u op **alle resources**. Klik op Hallo **contoso.net** DNS-zone in Hallo **alle resources** blade. Als u hebt geselecteerd al Hallo-abonnement verschillende resources heeft, kunt u **contoso.net** in Hallo Filter met de naam... vak tooeasily toegang Hallo toepassingsgateway. 

1. Hallo-naamservers ophalen met Hallo DNS-zone-blade. In dit voorbeeld Hallo zone 'contoso.net' is toegewezen naamservers ' ns1-01.azure-dns.com', 'ns2-01.', ' ns3-01.azure-Azure ', en ' ns4-01.azure-dns.info':

 ![DNS-naamserver](./media/dns-domain-delegation/viewzonens500.png)

Azure DNS maakt automatisch gezaghebbende NS-records in uw zone die Hallo toegewezen naamservers.  de namen van toosee Hallo naamserver via Azure PowerShell of Azure CLI, hoeft u alleen tooretrieve deze records.

Hallo bieden volgende voorbeelden ook Hallo stappen tooretrieve Hallo-naamservers voor een zone in Azure DNS met PowerShell en Azure CLI.

### <a name="powershell"></a>PowerShell

```powershell
# hello record name "@" is used toorefer toorecords at hello top of hello zone.
$zone = Get-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -Zone $zone
```

Hallo volgende voorbeeld is Hallo antwoord.

```
Name              : @
ZoneName          : contoso.net
ResourceGroupName : contosorg
Ttl               : 172800
Etag              : 03bff8f1-9c60-4a9b-ad9d-ac97366ee4d5
RecordType        : NS
Records           : {ns1-07.azure-dns.com., ns2-07.azure-dns.net., ns3-07.azure-dns.org.,
                    ns4-07.azure-dns.info.}
Metadata          :
```

### <a name="azure-cli"></a>Azure CLI

```azurecli
az network dns record-set show --resource-group contosoRG --zone-name contoso.net --type NS --name @
```

Hallo volgende voorbeeld is Hallo antwoord.

```json
{
  "etag": "03bff8f1-9c60-4a9b-ad9d-ac97366ee4d5",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/contosoRG/providers/Microsoft.Network/dnszones/contoso.net/NS/@",
  "metadata": null,
  "name": "@",
  "nsRecords": [
    {
      "nsdname": "ns1-07.azure-dns.com."
    },
    {
      "nsdname": "ns2-07.azure-dns.net."
    },
    {
      "nsdname": "ns3-07.azure-dns.org."
    },
    {
      "nsdname": "ns4-07.azure-dns.info."
    }
  ],
  "resourceGroup": "contosoRG",
  "ttl": 172800,
  "type": "Microsoft.Network/dnszones/NS"
}
```

## <a name="delegate-hello-domain"></a>Gemachtigde Hallo domein

Nu dat Hallo DNS-zone wordt gemaakt en u de naamservers Hallo hebt, moet Hallo bovenliggend domein toobe bijgewerkt met hello Azure DNS-naamservers. Elke registrar heeft eigen DNS-beheer extra toochange hello naamserverrecords voor een domein. Van Hallo registrar DNS-beheer pagina bewerken Hallo NS-records en vervang Hallo NS-records door Hallo die zijn gemaakt voor Azure DNS.

Wanneer u een domein tooAzure DNS, moet u Hallo naamservernamen verstrekt door Azure DNS. Het verdient aanbeveling toouse alle vier naam servernamen, ongeacht het Hallo-naam van uw domein. Domeindelegering vereist geen Hallo naam server name toouse Hallo van hetzelfde domein bevinden op het hoogste niveau als uw domein.

Gebruik niet 'glue records' toopoint toohello Azure DNS-naam server IP-adressen, aangezien deze IP-adressen in de toekomst kunnen worden gewijzigd. Delegeringen die gebruikmaken van de naamservernamen in uw eigen zone, ook wel vanity naamservers genoemd, worden momenteel niet ondersteund in Azure DNS.

## <a name="verify-name-resolution-is-working"></a>Controleren of de naamomzetting werkt

Na het voltooien van Hallo overdracht, kunt u controleren of naamomzetting werkt met behulp van een hulpprogramma zoals 'nslookup' tooquery Hallo SOA-record voor uw zone (die ook automatisch wordt gemaakt wanneer Hallo zone wordt gemaakt).

U hebt geen toospecify hello Azure DNS-naamservers, als Hallo overdracht is ingesteld correct Hallo normale DNS-omzettingsproces vindt de naamservers Hallo automatisch.

```
nslookup -type=SOA contoso.com
```

Hallo Hier volgt een voorbeeld van antwoord van de voorgaande opdracht Hallo:

```
Server: ns1-04.azure-dns.com
Address: 208.76.47.4

contoso.com
primary name server = ns1-04.azure-dns.com
responsible mail addr = msnhst.microsoft.com
serial = 1
refresh = 900 (15 mins)
retry = 300 (5 mins)
expire = 604800 (7 days)
default TTL = 300 (5 mins)
```

## <a name="delegate-sub-domains-in-azure-dns"></a>Subdomeinen delegeren in Azure DNS

Als u tooset van een afzonderlijke onderliggende zone wilt, kunt u een subdomein in Azure DNS kunt delegeren. Stel dat u wilt dat tooset van een afzonderlijke onderliggende zone, bijvoorbeeld hebt ingesteld en gedelegeerd 'contoso.net' in Azure DNS 'partners.contoso.net'.

1. Maak partners.contoso.net' hello onderliggende zone, in Azure DNS.
2. Hallo gezaghebbende NS-records in Hallo onderliggende zone tooobtain Hallo naamservers Hallo onderliggende zone in Azure DNS hosten opzoeken.
3. Hallo onderliggende zone door NS-records configureren in Hallo bovenliggende zone en wijst toohello onderliggende zone delegeren.

### <a name="create-a-dns-zone"></a>Een DNS-zone maken

1. Meld u aan toohello Azure-portal
1. Klik op Hallo Hub-menu en klik op **Nieuw > netwerken >** en klik vervolgens op **DNS-zone** tooopen Hallo maken DNS-zone blade.

    ![DNS-zone](./media/dns-domain-delegation/dns.png)

1. Op Hallo **maken DNS-zone** blade Voer Hallo volgende waarden en klik vervolgens op **maken**:

   | **Instelling** | **Waarde** | **Details** |
   |---|---|---|
   |**Naam**|partners.contoso.net|Hallo-naam van Hallo DNS-zone|
   |**Abonnement**|[Uw abonnement]|Selecteer een abonnement toocreate Hallo toepassingsgateway in.|
   |**Resourcegroep**|**Bestaande gebruiken:** contosoRG|Maak een resourcegroep. de naam van resourcegroep Hallo moet uniek zijn binnen het Hallo-abonnement die u hebt geselecteerd. meer informatie over resourcegroepen lezen Hallo toolearn [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overzichtsartikel.|
   |**Locatie**|VS - west||

> [!NOTE]
> Hallo resourcegroep toohello locatie van resourcegroep Hallo verwijst, en heeft geen invloed op Hallo DNS-zone. Hallo DNS-zone locatie is altijd 'global' en niet wordt weergegeven.

### <a name="retrieve-name-servers"></a>Naamservers ophalen

1. Met de Hallo DNS-zone in hello Azure-portal gemaakt **Favorieten** deelvenster, klikt u op **alle resources**. Klik op Hallo **partners.contoso.net** DNS-zone in Hallo **alle resources** blade. Als u hebt geselecteerd al Hallo-abonnement verschillende resources heeft, kunt u **partners.contoso.net** in Hallo Filter met de naam... vak tooeasily toegang Hallo DNS-zone.

1. Hallo-naamservers ophalen met Hallo DNS-zone-blade. In dit voorbeeld Hallo zone 'contoso.net' is toegewezen naamservers ' ns1-01.azure-dns.com', 'ns2-01.', ' ns3-01.azure-Azure ', en ' ns4-01.azure-dns.info':

 ![DNS-naamserver](./media/dns-domain-delegation/viewzonens500.png)

Azure DNS maakt automatisch gezaghebbende NS-records in uw zone die Hallo toegewezen naamservers.  de namen van toosee Hallo naamserver via Azure PowerShell of Azure CLI, hoeft u alleen tooretrieve deze records.

### <a name="create-name-server-record-in-parent-zone"></a>Een naamserverrecord maken in de bovenliggende zone

1. Navigeer toohello **contoso.net** DNS-zone in hello Azure-portal.
1. Klik op **Recordset toevoegen**
1. Op Hallo **recordset toevoegen** blade Voer Hallo volgende waarden en klik vervolgens op **OK**:

   | **Instelling** | **Waarde** | **Details** |
   |---|---|---|
   |**Naam**|partners|Hallo-naam van Hallo onderliggende DNS-zone|
   |**Type**|NS|Gebruik NS voor naamserverrecords.|
   |**TTL**|1|Tijd toolive.|
   |**TTL-eenheid**|Uren|Hiermee stelt u tijd toolive eenheid toohours|
   |**NAAMSERVER**|{naamservers van zone partners.contoso.net}|Voer alle 4 Hallo naamservers uit partners.contoso.net zone. |

   ![DNS-naamserver](./media/dns-domain-delegation/partnerzone.png)


### <a name="delegating-sub-domains-in-azure-dns-with-other-tools"></a>Subdomeinen in Azure DNS delegeren met andere hulpprogramma’s

Hallo bieden volgende voorbeelden Hallo stappen toodelegate subdomeinen in Azure DNS met PowerShell en CLI:

#### <a name="powershell"></a>PowerShell

Hallo volgende PowerShell-voorbeeld laat zien hoe dit werkt. Hallo dezelfde stappen kunnen worden uitgevoerd via hello Azure-portal of via Hallo platformoverschrijdende Azure CLI.

```powershell
# Create hello parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
$parent = New-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
$child = New-AzureRmDnsZone -Name partners.contoso.net -ResourceGroupName contosoRG

# Retrieve hello authoritative NS records from hello child zone as shown in hello next example. This contains hello name servers assigned toohello child zone.
$child_ns_recordset = Get-AzureRmDnsRecordSet -Zone $child -Name "@" -RecordType NS

# Create hello corresponding NS record set in hello parent zone toocomplete hello delegation. hello record set name in hello parent zone matches hello child zone name, in this case "partners".
$parent_ns_recordset = New-AzureRmDnsRecordSet -Zone $parent -Name "partners" -RecordType NS -Ttl 3600
$parent_ns_recordset.Records = $child_ns_recordset.Records
Set-AzureRmDnsRecordSet -RecordSet $parent_ns_recordset
```

Gebruik `nslookup` tooverify dat alles juist is ingesteld door het opzoeken van Hallo SOA-record van Hallo onderliggende zone.

```
nslookup -type=SOA partners.contoso.com
```

```
Server: ns1-08.azure-dns.com
Address: 208.76.47.8

partners.contoso.com
    primary name server = ns1-08.azure-dns.com
    responsible mail addr = msnhst.microsoft.com
    serial = 1
    refresh = 900 (15 mins)
    retry = 300 (5 mins)
    expire = 604800 (7 days)
    default TTL = 300 (5 mins)
```

#### <a name="azure-cli"></a>Azure CLI

```azurecli
#!/bin/bash

# Create hello parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
az network dns zone create -g contosoRG -n contoso.net
az network dns zone create -g contosoRG -n partners.contoso.net
```

Ophalen van de naamservers Hallo voor Hallo `partners.contoso.net` zone uit Hallo uitvoer.

```
{
  "etag": "00000003-0000-0000-418f-250de2b2d201",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/contosorg/providers/Microsoft.Network/dnszones/partners.contoso.net",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "partners.contoso.net",
  "nameServers": [
    "ns1-09.azure-dns.com.",
    "ns2-09.azure-dns.net.",
    "ns3-09.azure-dns.org.",
    "ns4-09.azure-dns.info."
  ],
  "numberOfRecordSets": 2,
  "resourceGroup": "contosorg",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

Hallo-Recordset en NS-records voor elke naamserver maken.

```azurecli
#!/bin/bash

# Create hello record set
az network dns record-set ns create --resource-group contosorg --zone-name contoso.net --name partners

# Create a ns record for each name server.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns1-09.azure-dns.com.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns2-09.azure-dns.net.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns3-09.azure-dns.org.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns4-09.azure-dns.info.
```

## <a name="delete-all-resources"></a>Alle resources verwijderen

toodelete alle resources die worden gemaakt in dit artikel wordt voltooid Hallo stappen te volgen:

1. In de Azure-portal Hallo **Favorieten** deelvenster, klikt u op **alle resources**. Klik op Hallo **contosorg** resourcegroep in Hallo alle resources blade. Als u hebt geselecteerd al Hallo-abonnement verschillende resources heeft, kunt u **contosorg** in Hallo **filteren op naam...** vak tooeasily toegang Hallo resourcegroep.
1. In Hallo **contosorg** blade, klikt u op Hallo **verwijderen** knop.
1. Hallo portal, moet u tootype Hallo-naam van Hallo resource groep tooconfirm dat u wilt dat toodelete deze. Type *contosorg* hello Resourcegroepnaam, vervolgens klikt u op **verwijderen**. Een resourcegroep verwijdert, worden alle bronnen binnen de resourcegroep hello, dus altijd zeker tooconfirm Hallo inhoud van een resourcegroep voordat u het verwijdert. Hallo portal Hiermee verwijdert u alle resources binnen de resourcegroep Hallo vervolgens Hallo resourcegroep zelf verwijdert. Dit proces duurt enkele minuten.

## <a name="next-steps"></a>Volgende stappen

[DNS-zones beheren](dns-operations-dnszones.md)

[DNS-records beheren](dns-operations-recordsets.md)
