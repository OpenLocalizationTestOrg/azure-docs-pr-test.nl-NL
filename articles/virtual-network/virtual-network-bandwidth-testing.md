---
title: aaaTesting Azure VM netwerkdoorvoer | Microsoft Docs
description: Meer informatie over hoe tootest virtuele machine van Azure-netwerk doorvoer.
services: virtual-network
documentationcenter: na
author: steveesp
manager: Gerald DeGrace
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/21/2017
ms.author: steveesp
ms.openlocfilehash: 2da85c27bc8d16a443b215891f4cd0460f41926f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="bandwidththroughput-testing-ntttcp"></a>Bandbreedte/doorvoer (NTTTCP) testen

Bij het testen van prestaties van de netwerkdoorvoer in Azure, is het beste toouse een hulpprogramma dat gericht is op Hallo netwerk voor het testen en minimaliseert Hallo gebruik van andere bronnen die kan invloed hebben op prestaties. NTTTCP wordt aanbevolen.

Hallo hulpprogramma tootwo Azure Virtual machines Hallo kopiëren dezelfde grootte hebben. Één virtuele machine fungeert als de afzender en Hallo andere als ontvanger.

#### <a name="deploying-vms-for-testing"></a>Implementeren van virtuele machines voor testdoeleinden
Voor Hallo doeleinden van deze test, is Hallo twee virtuele machines moeten zich in dezelfde Cloudservice Hallo of Hallo dezelfde Beschikbaarheidsset zodat we kunnen hun intern IP-adressen gebruiken en Hallo Load Balancers van Hallo test uitsluiten. Het is mogelijk tootest Hello VIP maar dit soort testen valt buiten bereik Hallo van dit document.
 
Noteer Hallo-ontvanger IP-adres. We bellen die IP 'a.b.c.r'

Noteer het aantal kernen Hallo op Hallo VM. Laten we dit noemen '\#num\_kernen '
 
Voer Hallo NTTTCP testen voor 300 seconden (of 5 minuten) op Hallo afzender VM en ontvanger VM.

Tip: Bij het instellen van deze test voor Hallo eerst, u mogelijk probeer een kortere periode tooget feedback voor test sneller. Nadat het hulpprogramma voor Hallo werkt zoals verwacht, uitbreiden Hallo test periode too300 seconden voor de meest nauwkeurige resultaten Hallo.

> [!NOTE]
> Hallo afzender **en** ontvanger moet opgeven **Hallo dezelfde** testen duur van de parameter (-t).

tootest één stream TCP 10 seconden:

Ontvanger parameters: ntttcp - r -t 10 - P 1

Parameters van de afzender: ntttcp-s10.27.33.7 -t 10 - n 1 -P 1

> [!NOTE]
> Hallo voorgaande voorbeeld mogen alleen worden gebruikt tooconfirm uw configuratie. Aantal voorbeelden van testen worden verderop in dit document besproken.

## <a name="testing-vms-running-windows"></a>Testen van virtuele machines waarop WINDOWS wordt uitgevoerd:

#### <a name="get-ntttcp-onto-hello-vms"></a>NTTTCP terechtkomen Hallo virtuele machines.

Download de nieuwste versie Hallo: <https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769>

Of zoekt u het als verplaatst: <https://www.bing.com/search?q=ntttcp+download> \< --moet eerst worden bereikt

Overweeg NTTTCP plaatsen in een afzonderlijke map, zoals c:\\hulpprogramma's

#### <a name="allow-ntttcp-through-hello-windows-firewall"></a>NTTTCP toestaan via Hallo Windows firewall
Maak een regel voor toestaan op Hallo Windows Firewall tooallow de NTTTCP verkeer tooarrive op Hallo ontvanger. Het is eenvoudigste tooallow Hallo volledige NTTTCP programma met de naam in plaats van inkomende tooallow bepaalde TCP-poorten.

Toestaan dat ntttcp via Windows Firewall Hallo als volgt:

Netsh advfirewall firewall regel programma toevoegen =\<pad\>\\ntttcp.exe name = "ntttcp" protocol eventuele dir = in actie = = toestaan inschakelen = yes profile = ANY

Bijvoorbeeld, als u ntttcp.exe toohello gekopieerd ' c:\\extra ' map, zou dit Hallo-opdracht: 

Netsh advfirewall firewall regel programma toevoegen = c:\\hulpprogramma's\\ntttcp.exe naam = 'ntttcp' protocol eventuele dir = in actie = = toestaan inschakelen = yes profile = ANY

#### <a name="running-ntttcp-tests"></a>NTTTCP tests die worden uitgevoerd

Start NTTTCP op Hallo ontvanger (**uitvoeren vanaf CMD**, niet vanuit PowerShell):

ntttcp - r-m [2\*\#num\_kernen],\*, 300 a.b.c.r -t

Als Hallo VM vier kernen en het IP-adres 10.0.0.4 heeft, wordt deze eruit als volgt:

ntttcp - r – m 8,\*, 10.0.0.4 -t 300


Start NTTTCP op Hallo afzender (**uitvoeren vanaf CMD**, niet vanuit PowerShell):

ntttcp -s-m 8,\*, 10.0.0.4 -t 300 

Wachten op Hallo resultaten.


## <a name="testing-vms-running-linux"></a>Testen van virtuele machines waarop LINUX wordt uitgevoerd:

Gebruik nttcp voor linux. Deze beschikbaar is via <https://github.com/Microsoft/ntttcp-for-linux>

Op Hallo virtuele Linux-machines (ZENDER en ontvanger), moet u deze opdrachten om voor te bereiden ntttcp voor linux op uw virtuele machines uitvoeren:

CentOS - Git installeren:
``` bash
  yum install gcc -y  
  yum install git -y
```
Ubuntu - Git installeren:
``` bash
 apt-get -y install build-essential  
 apt-get -y install git
```
Maken en te installeren op beide:
``` bash
 git clone <https://github.com/Microsoft/ntttcp-for-linux>
 cd ntttcp-for-linux/src
 make && make install
```

Als in voorbeeld van de Windows hello Aannemende dat Hallo Linux ontvanger IP-adres is 10.0.0.4

Start NTTTCP voor Linux op Hallo ontvanger:

``` bash
ntttcp -r -t 300
```

En op Hallo afzender, uitvoeren:

``` bash
ntttcp -s10.0.0.4 -t 300
```
 
Test lengte standaardwaarden too60 seconden als er is geen tijdsparameter is gegeven

## <a name="testing-between-vms-running-windows-and-linux"></a>Testen tussen VM's met Windows en LINUX:

Op deze scenario's moeten we Hallo Nee-sync-modus inschakelen zodat Hallo test kunt uitvoeren. Dit wordt gedaan met behulp van Hallo **-N vlag** voor Linux en **-ns vlag** voor Windows.

#### <a name="from-linux-toowindows"></a>Van Linux tooWindows:

Ontvanger <Windows>:

``` bash
ntttcp -r -m <2 x nr cores>,*,<Windows server IP>
```

Afzender <Linux> :

``` bash
ntttcp -s -m <2 x nr cores>,*,<Windows server IP> -N -t 300
```

#### <a name="from-windows-toolinux"></a>Vanaf Windows tooLinux:

Ontvanger <Linux>:

``` bash
ntttcp -r -m <2 x nr cores>,*,<Linux server IP>
```

Afzender <Windows>:

``` bash
ntttcp -s -m <2 x nr cores>,*,<Linux  server IP> -ns -t 300
```

## <a name="next-steps"></a>Volgende stappen
* Afhankelijk van de resultaten, kunnen er ruimte te[netwerk doorvoer machines optimaliseren](virtual-network-optimize-network-bandwidth.md) voor uw scenario.
* Klik hier als u meer wilt weten met [Azure Virtual Network Veelgestelde vragen (FAQ)](virtual-networks-faq.md)
