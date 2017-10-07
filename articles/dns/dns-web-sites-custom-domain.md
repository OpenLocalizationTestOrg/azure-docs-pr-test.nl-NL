---
title: aaaCreate aangepaste DNS-records voor een web-app | Microsoft Docs
description: Hoe toocreate aangepast domein-DNS-records voor web-app met Azure DNS.
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 6c16608c-4819-44e7-ab88-306cf4d6efe5
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: 070c808a55bab922eb624d99ae5c275d8eaa5aaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-dns-records-for-a-web-app-in-a-custom-domain"></a>DNS-records voor een web-app maken in een aangepast domein

U kunt Azure DNS toohost een aangepast domein voor uw web-apps gebruiken. Bijvoorbeeld, u een Azure-web-app maakt en u wilt dat uw gebruikers tooaccess deze door een van beide contoso.com of www.contoso.com als een FQDN-naam gebruiken.

toodo, hebt u twee records toocreate:

* Een record aan wijzen toocontoso.com voor hoofdmap "A"
* Een 'CNAME'-record voor Hallo www-naam die toohello verwijst een record

Houd er rekening mee dat als u een A-record voor een web-app in Azure maakt, Hallo Hallo die een record moet handmatig worden bijgewerkt als onderliggende IP-adres voor Hallo web appwijzigingen.

## <a name="before-you-begin"></a>Voordat u begint

Voordat u begint, moet u eerst een DNS-zone maken in Azure DNS en Hallo zone delegeren in uw registrar tooAzure DNS.

1. een DNS-zone toocreate Hallo stappen in [maken van een DNS-zone](dns-getstarted-create-dnszone.md).
2. toodelegate uw DNS-tooAzure DNS, stappen Hallo in [DNS-domeindelegering](dns-domain-delegation.md).

Na het maken van een zone en het overdragen van tooAzure DNS, kunt u vervolgens records maken voor uw aangepaste domein.

## <a name="1-create-an-a-record-for-your-custom-domain"></a>1. Maak een A-record voor uw aangepaste domein

Een A-record is gebruikte toomap een naam tooits IP-adres. In het volgende voorbeeld Hallo wordt we @ toewijzen als een A-record tooan IPv4-adres:

### <a name="step-1"></a>Stap 1

Een A-record maken en toewijzen tooa variabele $rs

```powershell
$rs= New-AzureRMDnsRecordSet -Name "@" -RecordType "A" -ZoneName "contoso.com" -ResourceGroupName "MyAzureResourceGroup" -Ttl 600
```

### <a name="step-2"></a>Stap 2

Toevoegen Hallo IPv4 waarde toohello eerder gemaakte recordset ' @ ' hello $rs variabele toegewezen. Hallo IPv4-waarde die is toegewezen worden Hallo IP-adres voor uw web-app.

toofind hello IP-adres voor een web-app Hallo stappen in [een aangepaste domeinnaam configureren in Azure App Service](../app-service-web/app-service-web-tutorial-custom-domain.md).

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Ipv4Address "<your web app IP address>"
```

### <a name="step-3"></a>Stap 3

Hallo toohello Recordset-wijzigingen worden doorgevoerd. Gebruik `Set-AzureRMDnsRecordSet` tooupload hello toohello Recordset tooAzure DNS-wijzigingen:

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="2-create-a-cname-record-for-your-custom-domain"></a>2. Maak een CNAME-record voor uw aangepaste domein

Als uw domein wordt al beheerd door Azure DNS (Zie [DNS-domeindelegering](dns-domain-delegation.md), kunt u Hallo Hallo voorbeeld toocreate een CNAME-record voor contoso.azurewebsites.net te volgen.

### <a name="step-1"></a>Stap 1

Open PowerShell en een nieuwe CNAME-recordset maken en toewijzen tooa variabele $rs. In dit voorbeeld maakt u een Recordset type CNAME met een 'uitvoeringstijd toolive' 600 seconden in DNS-zone met de naam 'contoso.com'.

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName contoso.com -ResourceGroupName myresourcegroup -Name "www" -RecordType "CNAME" -Ttl 600
```

Hallo volgende voorbeeld is Hallo antwoord.

```
Name              : www
ZoneName          : contoso.com
ResourceGroupName : myresourcegroup
Ttl               : 600
Etag              : 8baceeb9-4c2c-4608-a22c-229923ee1856
RecordType        : CNAME
Records           : {}
Tags              : {}
```

### <a name="step-2"></a>Stap 2

Zodra Hallo CNAME-recordset is gemaakt, moet u toocreate een aliaswaarde die verwijst toohello web-app.

U kunt met behulp van de eerder toegewezen variabele '$rs' Hallo Hallo PowerShell-opdracht hieronder toocreate Hallo alias gebruiken voor Hallo web app contoso.azurewebsites.net.

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "contoso.azurewebsites.net"
```

Hallo volgende voorbeeld is Hallo antwoord.

```
    Name              : www
    ZoneName          : contoso.com
    ResourceGroupName : myresourcegroup
    Ttl               : 600
    Etag              : 8baceeb9-4c2c-4608-a22c-229923ee185
    RecordType        : CNAME
    Records           : {contoso.azurewebsites.net}
    Tags              : {}
```

### <a name="step-3"></a>Stap 3

Hallo wijzigingen met behulp van Hallo `Set-AzureRMDnsRecordSet` cmdlet:

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

U kunt valideren Hallo record correct is gemaakt door het uitvoeren van query's Hallo 'www.contoso.com' met nslookup, zoals hieronder wordt weergegeven:

```
PS C:\> nslookup
Default Server:  Default
Address:  192.168.0.1

> www.contoso.com
Server:  default server
Address:  192.168.0.1

Non-authoritative answer:
Name:    <instance of web app service>.cloudapp.net
Address:  <ip of web app service>
Aliases:  www.contoso.com
contoso.azurewebsites.net
<instance of web app service>.vip.azurewebsites.windows.net
```

## <a name="create-an-awverify-record-for-web-apps"></a>Maak een 'awverify'-record voor web-apps

Als u toouse een A-record voor uw web-app besluit, moet u gaan via een proces verificatie tooensure u eigen Hallo aangepast domein. Deze verificatiestap wordt gedaan door het maken van een speciale CNAME-record met de naam 'awverify'. Deze sectie geldt alleen voor tooA records.

### <a name="step-1"></a>Stap 1

Hallo 'awverify'-record maken. We gaan Hallo 'aweverify'-record voor contoso.com tooverify eigendom van het aangepaste domein Hallo maken in Hallo onderstaande voorbeeld.

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "myresourcegroup" -Name "awverify" -RecordType "CNAME" -Ttl 600
```

Hallo volgende voorbeeld is Hallo antwoord.

```
Name              : awverify
ZoneName          : contoso.com
ResourceGroupName : myresourcegroup
Ttl               : 600
Etag              : 8baceeb9-4c2c-4608-a22c-229923ee1856
RecordType        : CNAME
Records           : {}
Tags              : {}
```

### <a name="step-2"></a>Stap 2

Zodra de recordset 'awverify' hello is gemaakt, wijs Hallo CNAME-Recordset alias. In onderstaande Hallo voorbeeld, wijst Hallo CNAME-Recordset alias tooawverify.contoso.azurewebsites.net toe.

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "awverify.contoso.azurewebsites.net"
```

Hallo volgende voorbeeld is Hallo antwoord.

```
    Name              : awverify
    ZoneName          : contoso.com
    ResourceGroupName : myresourcegroup
    Ttl               : 600
    Etag              : 8baceeb9-4c2c-4608-a22c-229923ee185
    RecordType        : CNAME
    Records           : {awverify.contoso.azurewebsites.net}
    Tags              : {}
```

### <a name="step-3"></a>Stap 3

Hallo wijzigingen met behulp van Hallo `Set-AzureRMDnsRecordSet cmdlet`, zoals weergegeven in onderstaande Hallo-opdracht.

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="next-steps"></a>Volgende stappen

Volg de stappen Hallo in [configureren van een aangepaste domeinnaam voor App Service](../app-service-web/web-sites-custom-domain-name.md) tooconfigure uw web-app toouse een aangepast domein.
