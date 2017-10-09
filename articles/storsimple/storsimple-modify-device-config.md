---
title: configuratie van aaaModify hello StorSimple-apparaat | Microsoft Docs
description: "Hierin wordt beschreven hoe toouse Hallo StorSimple Manager service tooreconfigure een StorSimple-apparaat dat al is geïmplementeerd."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: bb679264-8d46-429c-9ef7-630dc3b4a423
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/19/2017
ms.author: v-sharos
ms.openlocfilehash: 10a54c191260bf1baba58d28cdbfa0ed72217f48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomodify-your-storsimple-device-configuration"></a>Hallo StorSimple Manager-service toomodify de configuratie van uw StorSimple-apparaat gebruiken
## <a name="overview"></a>Overzicht
klassieke Azure-portal Hallo **configureren** pagina bevat alle parameters van de Hallo apparaat die u kunt opnieuw configureren op een StorSimple-apparaat dat wordt beheerd door een StorSimple Manager-service. Deze zelfstudie wordt uitgelegd hoe u kunt Hallo **configureren** pagina tooperform Hallo op apparaatniveau taken te volgen:

* Apparaatinstellingen wijzigen 
* Tijdinstellingen wijzigen 
* DNS-instellingen wijzigen 
* Netwerkinterfaces wijzigen
* Wisselen of opnieuw toewijzen van IP-adressen

## <a name="modify-device-settings"></a>Apparaatinstellingen wijzigen
Hallo-apparaatinstellingen bevatten beschrijvende naam van de Hallo Hallo-apparaat en Hallo apparaatbeschrijving.

> [!NOTE] 
> U kunt Hallo apparaatnaam in de klassieke Azure-portal Hallo niet wijzigen. Hallo hernoemen van het apparaat wordt niet ondersteund.

Een StorSimple-apparaat dat is verbonden toohello StorSimple Manager-service wordt een standaardnaam toegewezen. de standaardnaam Hallo geeft doorgaans serienummer Hallo Hallo-apparaat. Een standaardnaam voor het apparaat dat is 15 tekens lang zijn, zoals 8600-SHX0991003G44HT geeft bijvoorbeeld Hallo volgende aan:

* **8600** – geeft aan dat Hallo-Apparaatmodel.
* **SHX** – geeft aan dat Hallo productie-site.
* **0991003** -geeft aan een specifiek product.
* **G44HT**- hello laatste 5 cijfers worden verhoogd toocreate unieke serienummers. Dit wordt mogelijk niet een sequentiële set.

U kunt een beschrijving van het apparaat opgeven. Een beschrijving van het apparaat kunt meestal Hallo eigenaar en Hallo fysieke locatie van Hallo apparaat identificeren. beschrijvingsveld Hallo moet minder dan 256 tekens bevatten.

## <a name="modify-time-settings"></a>Tijdinstellingen wijzigen
Uw apparaat moet de tijd in volgorde tooauthenticate synchroniseren met uw serviceprovider voor cloud-opslag. Selecteer uw tijdzone in de vervolgkeuzelijst Hallo en geef tootwo Network Time Protocol (NTP)-servers. Hallo primaire NTP-server is vereist en wordt opgegeven wanneer u Windows PowerShell voor StorSimple tooconfigure uw apparaat. U kunt opgeven dat Hallo standaard Windows Server **time.windows.com** als uw NTP-server. U kunt weergeven Hallo primaire NTP-serverconfiguratie via Hallo klassieke Azure-portal, maar moet u Hallo Windows PowerShell-interface toochange deze.

Hallo secundaire NTP-serverconfiguratie is optioneel. U kunt Hallo klassieke portal tooconfigure secundaire NTP-server gebruiken. 

Wanneer u Hallo NTP-server configureert, moet u ervoor zorgen dat uw netwerk Hallo NTP-verkeer toopass van uw datacenter toohello Internet toestaat. Wanneer u een openbare NTP-server opgeeft, moet u ervoor zorgen dat uw netwerkfirewalls en andere beveiligingsapparaten geconfigureerde tooallow NTP-verkeer tootravel tooand van Hallo buiten netwerk zijn. Als bidirectionele NTP-verkeer niet wordt toegestaan, moet u een interne NTP-server (een Windows-domeincontroller biedt deze functie). Als uw apparaat kan geen tijd synchroniseren, mogelijk kunnen toocommunicate met uw cloud-opslag-provider niet meer.

een lijst met openbare NTP-servers, Ga toohello toosee [NTP-Servers Web](http://support.ntp.org/bin/view/Servers/WebHome). 

### <a name="what-happens-if-hello-device-is-deployed-in-a-different-time-zone"></a>Wat gebeurt er als Hallo-apparaat is geïmplementeerd in een andere tijdzone?
Als het Hallo-apparaat is geïmplementeerd in een andere tijdzone, Hallo apparaat tijdzone gewijzigd. Gezien het feit dat alle Hallo back-upbeleid tijdzone Hallo-apparaat gebruikt, wordt de back-upbeleid Hallo automatisch aanpassen in overeenstemming met de nieuwe tijdzone Hallo. Er is geen tussenkomst van de gebruiker is vereist.

## <a name="modify-dns-settings"></a>DNS-instellingen wijzigen
Een DNS-server wordt gebruikt wanneer uw apparaat toocommunicate bij uw serviceprovider voor cloud-opslag probeert. Voor hoge beschikbaarheid, vereist tooconfigure zijn beide Hallo primaire en secundaire DNS-servers tijdens de implementatie van de eerste apparaat Hallo Hallo. tooreconfigure hello primaire DNS-server, moet u toouse Hallo Windows PowerShell-interface op uw StorSimple-apparaat.

toomodify hello secundaire DNS-server, kunt u Hallo klassieke Azure-portal.

## <a name="modify-network-interfaces"></a>Netwerkinterfaces wijzigen
Uw apparaat heeft zes apparaat netwerkinterfaces, waarvan vier 1 GbE zijn en dat de twee 10 GbE zijn. Deze interfaces zijn gelabeld als DATA 0: DATA 5. DATA 0, gegevens-1, gegevens 4 en 5 van de gegevens zijn 1 GbE DATA 2 en DATA 3 10 GbE-netwerkinterfaces zijn.

Configureer **netwerkinterface-instellingen** voor elk Hallo interfaces toobe gebruikt. tooensure hoge beschikbaarheid, raden wij aan dat u ten minste twee interfaces voor iSCSI- en twee interfaces zijn ingeschakeld voor de cloud op uw apparaat. We raden aan maar hoeven niet dat ongebruikte interfaces worden uitgeschakeld.

Wanneer u een van de netwerkinterfaces Hallo configureert, moet u een virtueel IP-adres (VIP) configureren.

DATA 0 is standaard ingeschakeld cloud. Bij het configureren van DATA 0, bent u ook de vereiste tooconfigure twee vaste IP-adressen, één voor elke domeincontroller. Deze vaste IP-adressen kunnen gebruikte tooaccess Hallo apparaatcontrollers rechtstreeks en zijn handig wanneer u updates op Hallo-apparaat of wanneer u toegang krijgen tot Hallo controllers voor Hallo doel installeert van het oplossen van problemen.

In StorSimple 8000 Series Update 1 is Hallo routering meetwaarde van DATA 0 ingesteld toohello laagste; dus als uw apparaat wordt uitgevoerd StorSimple 8000 Series Update 1, wordt alle Hallo cloud-verkeer gerouteerd via DATA 0. Noteer dit als u meer dan één ingeschakeld voor de cloud netwerkinterface op uw StorSimple-apparaat hebt.

> [!NOTE]
> Hallo vaste IP-adressen voor controller hello worden gebruikt voor het onderhoud Hallo updates toohello apparaat. Daarom moet Hallo vaste IP-adressen routeerbaar en kunnen tooconnect toohello Internet.
> 
> 

Voor elke netwerkinterface worden Hallo volgende parameters weergegeven:

* **Snelheid** – geen gebruiker configureerbare parameter. DATA 0, gegevens-1, gegevens 4 en 5 van de gegevens zijn altijd 1 GbE terwijl DATA 2 en DATA 3 10 GbE-interfaces zijn.
  
  > [!NOTE]
  > Snelheid en duplex wordt altijd automatisch-onderhandeld. Jumboframes worden niet ondersteund.
  > 
  > 
* **Interface-status** : een interface kan worden ingeschakeld of uitgeschakeld. Bij inschakeling probeert Hallo apparaat toouse Hallo-interface. We raden aan dat alleen de interfaces die zijn verbonden toohello netwerk en gebruikt worden ingeschakeld. Schakel alle interfaces die u niet gebruikt.
* **Type interface** – deze parameter kunt u tooisolate iSCSI-verkeer van verkeer van de cloud-opslag. Deze parameter is een van de volgende Hallo:
  
  * **Cloud ingeschakeld** – wanneer ingeschakeld, Hallo apparaat deze toocommunicate interface gaat gebruiken met Hallo cloud.
  * **iSCSI ingeschakeld** – wanneer ingeschakeld, Hallo apparaat deze toocommunicate interface gaat gebruiken met Hallo iSCSI-host.
    
    Het is raadzaam dat u iSCSI-verkeer van cloud-opslagverkeer isoleren. Let ook op als de host zich binnen de Hallo hetzelfde subnet als het apparaat, hoeft u geen tooassign een gateway; Als de host zich in een ander subnet dan uw apparaat, moet u echter tooassign een gateway.
* **IP-adres** – dit IPv4 of IPv6- of beide kan zijn. Zowel Hallo IPv4 en IPv6-adresfamilies worden ondersteund voor netwerkinterfaces Hallo-apparaat. Wanneer IPv4 wordt gebruikt, geeft u een 32-bits IP-adres (*xxx.xxx.xxx.xxx*) in punt decimale notatie met punten. Wanneer u IPv6 gebruikt, zijn simpelweg een 4-cijferige voorvoegsel en een 128-bits-adres wordt automatisch gegenereerd voor de netwerkinterface van uw apparaat op basis van het voorvoegsel.
* **Subnet** – dit subnetmasker toohello verwijst en via Hallo Windows PowerShell-interface is geconfigureerd.
* **Gateway** – dit Hallo standaardgateway die door deze interface moet worden gebruikt wanneer er wordt geprobeerd toocommunicate met knooppunten die zich niet binnen de Hallo is dezelfde IP-adresruimte (subnet). Hallo standaardgateway moet in Hallo dezelfde adresruimte (subnet) als Hallo interface IP-adres, zoals wordt bepaald door Hallo subnetmasker op.
* **Vaste IP-adres** – dit veld is alleen beschikbaar als u Hallo DATA 0 configureren interface. Bewerkingen zoals updates of het oplossen van problemen Hallo-apparaat, moet u wellicht tooconnect rechtstreeks toohello apparaat controller. Hallo vaste IP-adres kan worden gebruikt tooaccess zowel Hallo actieve en passieve controller Hallo op uw apparaat.

U kunt opnieuw configureren Controller 0 en Controller 1 tot en met Hallo klassieke Azure-portal.

> [!NOTE]
> * de goede werking tooensure, Controleer of de interfacesnelheid Hallo en duplex op Hallo-switch die de interface van elk apparaat is verbonden met. Switch netwerkinterfaces moet ofwel worden onderhandeld met of worden geconfigureerd voor Gigabit Ethernet (1000 Mbps) en full-duplex. Interfaces besturingssysteem trager of half-duplex leidt tot prestatieproblemen.
> * toominimize onderbrekingen en uitvaltijd, wordt u aangeraden portfast op elk van de poorten die Hallo iSCSI-netwerkinterface van uw apparaat verbinding met maken Hallo-switch in te schakelen. Dit zorgt ervoor dat verbinding met het netwerk kan snel worden opgezet in Hallo-gebeurtenis van een failover.
> 
> 

## <a name="swap-or-reassign-ips"></a>Wisselen of opnieuw toewijzen van IP-adressen
Op dit moment wordt als een netwerkinterface op Hallo-controller wordt toegewezen aan een VIP-adres dat wordt gebruikt (door Hallo hetzelfde apparaat of een ander apparaat in Hallo netwerk), Hallo controller via zullen mislukken. Daarom hebt toofollow Hallo juiste procedure als u bij het wisselen van VIP's voor de netwerkinterface Hallo-apparaat, omdat u een situatie met een dubbele IP-maakt.

Volgende stappen tooswap Hallo uitvoeren of opnieuw toewijzen Hallo VIP's voor alle netwerkinterfaces Hallo:

#### <a name="tooreassign-ips"></a>tooreassign IP-adressen
1. Schakel Hallo IP-adres voor beide interfaces.
2. Nadat Hallo IP-adressen zijn uitgeschakeld, toewijzen Hallo nieuwe IP-adressen toohello respectieve interfaces.

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over hoe te[MPIO configureren voor uw StorSimple-apparaat](storsimple-configure-mpio-windows-server.md).
* Meer informatie over hoe te[gebruik Hallo StorSimple Manager service tooadminister uw StorSimple-apparaat](storsimple-manager-service-administration.md).

