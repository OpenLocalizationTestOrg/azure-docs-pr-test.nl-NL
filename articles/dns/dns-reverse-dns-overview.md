---
title: aaaOverview van omgekeerde DNS-server in Azure | Microsoft Docs
description: Meer informatie over hoe reverse DNS-werkt en hoe deze kan worden gebruikt in Azure
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
ms.openlocfilehash: 687663fb83469ab8e696bb714649d0856915bad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-reverse-dns-and-support-in-azure"></a>Overzicht van de reverse DNS- en biedt ondersteuning in Azure

In dit artikel biedt een overzicht van hoe reverse DNS-werkt en Hallo omgekeerde DNS-scenario's die worden ondersteund in Azure.

## <a name="what-is-reverse-dns"></a>Wat is omgekeerde DNS?

Conventionele DNS-records van inschakelen een toewijzing van een DNS-naam (zoals 'www.contoso.com') tooan IP-adres (zoals 64.4.6.100).  Omgekeerde DNS kunt Hallo vertaling van een IP-adres (64.4.6.100) back tooa naam (www.contoso.com).

Omgekeerde DNS-records worden gebruikt in verschillende situaties. Omgekeerde DNS-records zijn bijvoorbeeld veel gebruikt in de bestrijding van e-mailbericht door te controleren of de afzender Hallo van een e-mailbericht.  Hallo ontvangende mail-server haalt Hallo omgekeerde DNS-record Hallo van server IP-adres verzenden en controleert of als die host is geautoriseerd toosend e-mailberichten van Hallo die afkomstig zijn domein. 

## <a name="how-reverse-dns-works"></a>Hoe reverse DNS-werkt

Omgekeerde DNS-records worden gehost in speciale DNS-zones, bekend als 'ARPA-zones.  Deze zones vormen een afzonderlijke DNS-hiërarchie in combinatie met normale Hallo-hiërarchie die als host fungeert voor domeinen, zoals 'contoso.com'.

Bijvoorbeeld, wordt DNS-record 'www.contoso.com' hello geïmplementeerd met een "A" DNS-record met de Hallo-naam 'www' hello zone 'contoso.com'.  Deze A-record verwijst toohello bijbehorende IP-adres, in dit geval 64.4.6.100.  Hallo reverse lookup wordt afzonderlijk geïmplementeerd met een 'PTR-record met de naam '100' hello zone '6.4.64.in-addr.arpa' (Let erop dat de IP-adressen in ARPA-zones worden omgekeerd.)  Deze PTR-record verwijst toohello naam 'www.contoso.com' als dit correct is geconfigureerd.

Wanneer een organisatie een IP-Adresblok toegewezen is, aanschaffen ze ook Hallo rechts toomanage Hallo bijbehorende ARPA zone. Hallo ARPA-zones overeenkomt toohello IP-adres blokken die worden gebruikt door Azure worden gehost en beheerd door Microsoft. Uw Internetprovider Hallo ARPA zone voor uw eigen IP-adressen voor u kan hosten of kan tooyou host Hallo ARPA zone in een DNS-service van uw keuze, zoals Azure DNS.

> [!NOTE]
> Forward DNS-zoekacties en reverse DNS-zoekacties worden in afzonderlijke, parallelle DNS-hiërarchieën geïmplementeerd. reverse lookup voor 'www.contoso.com' Hello **niet** gehost in Hallo zone 'contoso.com', in plaats daarvan het wordt gehost in Hallo ARPA zone voor Hallo bijbehorende IP-Adresblok. Afzonderlijke zones worden gebruikt voor IPv4 en IPv6-adresblokken.

### <a name="ipv4"></a>IPv4

Hallo-naam van een IPv4-zone voor reverse lookup moet in de volgende indeling Hallo: `<IPv4 network prefix in reverse order>.in-addr.arpa`.

Bijvoorbeeld bij het maken van een zone voor reverse toohost records voor hosts met IP-adressen die zich in Hallo 192.0.2.0/24 voorvoegsel zouden Hallo zonenaam worden gemaakt met Hallo netwerk voorvoegsel van het Hallo-adres (192.0.2) en vervolgens Hallo volgorde (2.0.192) om te keren en toe te voegen Hallo isoleren achtervoegsel `.in-addr.arpa`.

|Subnet-klasse|Netwerk voorvoegsel  |Omgekeerde netwerk voorvoegsel  |Standaard-achtervoegsel  |Zonenaam van voor reverse |
|-------|----------------|------------|-----------------|---------------------------|
|Klasse A|203.0.0.0/8     | 203        | .in-addr.arpa   | `203.in-addr.arpa`        |
|Klasse B|198.51.0.0/16   | 51.198     | .in-addr.arpa   | `51.198.in-addr.arpa`     |
|Klasse C|192.0.2.0/24    | 2.0.192    | .in-addr.arpa   | `2.0.192.in-addr.arpa`    |

### <a name="classless-ipv4-delegation"></a>Een IPv4-overdracht

In sommige gevallen Hallo IP-adresbereik toegewezen tooan organisatie kleiner is dan een klasse C (/ 24) bereik. Hallo IP-adresbereik valt in dit geval niet op de grens van een zone binnen Hallo `.in-addr.arpa` zone hiërarchie en daarom kan niet worden overgedragen als een onderliggende zone.

In plaats daarvan een ander mechanisme wordt gebruikt tootransfer besturingselement van afzonderlijke reverse lookup (Pointer) registreert tooa specifiek DNS-zone. Dit mechanisme delegeert een onderliggende zone voor elk IP-adresbereik en vervolgens elk IP-adres van Hallo maps bereik afzonderlijk toothat onderliggende zone met behulp van CNAME-records.

Stel bijvoorbeeld dat een organisatie Hallo IP-bereik 192.0.2.128/26 is verleend door de Internetprovider. Dit staat voor 64 IP-adressen uit 192.0.2.128 too192.0.2.191. Omgekeerde DNS voor dit bereik wordt als volgt geïmplementeerd:
- Hallo organisatie maakt aangeroepen 128-26.2.0.192.in-addr.arpa-zone voor reverse lookup. Hallo-voorvoegsel vertegenwoordigt ' 128-26' Hallo netwerk toegewezen segment toohello organisatie binnen Hallo klasse C (/ 24) bereik.
- Hallo ISP maakt tooset van NS-records van DNS-delegering voor Hallo hierboven zone Hallo Hallo klasse C bovenliggende zone. Dit leidt ook tot CNAME-records in hello (klasse C) bovenliggende zone voor reverse lookup toewijzing van elk IP-adres van Hallo IP-bereik toohello nieuwe zone gemaakt door Hallo organisatie:

```
$ORIGIN 2.0.192.in-addr.arpa
; Delegate child zone
128-26    NS       <name server 1 for 128-26.2.0.192.in-addr.arpa>
128-26    NS       <name server 2 for 128-26.2.0.192.in-addr.arpa>
; CNAME records for each IP address
129       CNAME    129.128-26.2.0.192.in-addr.arpa
130       CNAME    130.128-26.2.0.192.in-addr.arpa
131       CNAME    131.128-26.2.0.192.in-addr.arpa
; etc
```
- Hallo organisatie beheert Hallo afzonderlijke PTR-records in de onderliggende zone.

```
$ORIGIN 128-26.2.0.192.in-addr.arpa
; PTR records for each UIP address. Names match CNAME targets in parent zone
129      PTR    www.contoso.com
130      PTR    mail.contoso.com
131      PTR    partners.contoso.com
; etc
```
Een reverse lookup voor Hallo IP-adres '192.0.2.129' query's voor een PTR-record met de naam '129.2.0.192.in-addr.arpa'. Deze query wordt omgezet via Hallo CNAME Hallo bovenliggende zone toohello PTR-record in Hallo onderliggende zone.

### <a name="ipv6"></a>IPv6

Hallo-naam van een IPv6-zone voor reverse lookup moet Hallo formulier te volgen:`<IPv6 network prefix in reverse order>.ip6.arpa`

Bijvoorbeeld:. Bij het maken van een zone voor reverse toohost records voor hosts met IP-adressen die zich in Hallo 2001:db8:1000:abdc:: / 64 voorvoegsel Hallo zonenaam zouden worden gemaakt met de Hallo netwerk voorvoegsel van Hallo adres isoleren (2001:db8:abdc::). Vouw vervolgens Hallo IPv6-netwerk voorvoegsel tooremove [nul compressie](https://technet.microsoft.com/library/cc781672(v=ws.10).aspx), als deze gebruikte tooshorten Hallo IPv6-adresvoorvoegsel (2001:0db8:abdc:0000::). Omgekeerde volgorde hello, gebruik van een punt als scheidingsteken tussen elke hexadecimaal getal in Hallo voorvoegsel Hallo toobuild Hallo omgekeerd netwerk voorvoegsel (`0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2`) en voeg Hallo achtervoegsel `.ip6.arpa`.


|Netwerk voorvoegsel  |Uitgebreide en omgekeerde netwerk voorvoegsel |Standaard-achtervoegsel |Zonenaam van voor reverse  |
|---------|---------|---------|---------|
|2001:db8:abdc:: / 64    | 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2        | . ip6.arpa        | `0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa`       |
|2001:db8:1000:9102:: / 64    | 2.0.1.9.0.0.0.1.8.b.d.0.1.0.0.2        | . ip6.arpa        | `2.0.1.9.0.0.0.1.8.b.d.0.1.0.0.2.ip6.arpa`        |


## <a name="azure-support-for-reverse-dns"></a>Ondersteuning van Azure voor omgekeerde DNS

Azure ondersteunt twee afzonderlijke scenario's met betrekking tooreverse DNS:

**Hallo reverse lookup zone bijbehorende tooyour IP-Adresblok hosten.**
Azure DNS te kunnen worden gebruikt[hosten van uw zones voor reverse lookup en beheren van Hallo PTR-records voor elke reverse DNS-lookup](dns-reverse-dns-hosting.md), voor zowel IPv4 als IPv6.  Hallo proces voor het maken van hello (ARPA) zone voor reverse lookup Hallo delegering instellen en configureren van PTR records is Hallo dezelfde als voor gewone DNS-zones.  Hallo zijn alleen verschillen dat Hallo delegering moet worden geconfigureerd via uw Internetprovider in plaats van uw registrar DNS- en alleen Hallo type PTR-record moet worden gebruikt.

**Configureer Hallo omgekeerde DNS-record voor Hallo IP-adres toegewezen tooyour Azure-service.** Azure kunt u te[Hallo reverse lookup configureren voor Hallo IP-adressen tooyour Azure service toegewezen](dns-reverse-dns-for-azure-services.md).  Deze reverse lookup is geconfigureerd door Azure als een PTR-record in de bijbehorende ARPA zone Hallo.  Deze ARPA-zones overeenkomt tooall Hallo IP-adresbereiken gebruikt door Azure worden gehost door Microsoft

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over omgekeerde DNS [achterwaartse DNS-zoekopdracht op Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).
<br>
Meer informatie over hoe te[host Hallo-zone voor reverse lookup voor uw Internetprovider toegewezen IP-adresbereik in Azure DNS](dns-reverse-dns-for-azure-services.md).
<br>
Meer informatie over hoe te[omgekeerde DNS-records voor uw Azure-services beheren](dns-reverse-dns-for-azure-services.md).

