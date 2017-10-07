---
title: aaaModify hello StorSimple 8000 series apparaatconfiguratie | Microsoft Docs
description: "Hierin wordt beschreven hoe toouse Hallo tooreconfigure voor Apparaatbeheer van StorSimple-service een StorSimple-apparaat dat al is geïmplementeerd."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/19/2017
ms.author: alkohli
ms.openlocfilehash: 79711b45eafe732c1eed1e562b05e3837fbc9d03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomodify-your-storsimple-device-configuration"></a>Hallo Apparaatbeheer StorSimple-service toomodify de configuratie van uw StorSimple-apparaat gebruiken

## <a name="overview"></a>Overzicht

Azure-portal Hallo **apparaatinstellingen** sectie in Hallo **instellingen** blade bevat alle parameters van de Hallo apparaat die u kunt opnieuw configureren op een StorSimple-apparaat dat wordt beheerd door een StorSimple-Apparaatbeheer de service. Deze zelfstudie wordt uitgelegd hoe u kunt Hallo **instellingen** blade tooperform Hallo op apparaatniveau taken te volgen:

* Beschrijvende naam van apparaat wijzigen
* Apparaatinstellingen tijd wijzigen
* Toewijzen van een secundaire DNS-server
* Netwerkinterfaces wijzigen
* Wisselen of opnieuw toewijzen van IP-adressen

## <a name="modify-device-friendly-name"></a>Beschrijvende naam van apparaat wijzigen

U kunt gebruiken hello Azure portal toochange Hallo apparaatnaam en een unieke beschrijvende naam van uw keuze toewijst. Gebruik Hallo **algemene instellingen** blade op uw apparaat toomodify Hallo beschrijvende apparaatnaam. de beschrijvende naam Hallo kan alle tekens bevatten en mag maximaal 64 tekens lang zijn.

> [!NOTE] 
> U kunt alleen Hallo apparaatnaam in hello Azure-portal wijzigen voordat Hallo apparaat setup voltooid is. Zodra de minimale Apparaatinstelling Hallo voltooid is, kunt u de apparaatnaam Hallo niet wijzigen.

![Apparaatnaam in het algemeen instellingen](./media/storsimple-8000-modify-device-config/modify-general-settings3.png)

Een StorSimple-apparaat dat is verbonden toohello StorSimple-apparaat Manager-service wordt een standaardnaam toegewezen. de standaardnaam Hallo geeft doorgaans serienummer Hallo Hallo-apparaat. Een standaardnaam voor het apparaat dat is 15 tekens lang zijn, zoals 8600-SHX0991003G44HT geeft bijvoorbeeld Hallo volgende aan:

* **8600** – geeft aan dat Hallo-Apparaatmodel.
* **SHX** – geeft aan dat Hallo productie-site.
* **0991003** -geeft aan een specifiek product.
* **G44HT**- hello laatste 5 cijfers worden verhoogd toocreate unieke serienummers. Dit wordt mogelijk niet een sequentiële set.

## <a name="modify-device-description"></a>Beschrijving van het apparaat wijzigen

Gebruik Hallo **algemene instellingen** blade op uw apparaat toomodify Hallo apparaatbeschrijving.

![Apparaatbeschrijving van het in algemene instellingen](./media/storsimple-8000-modify-device-config/modify-general-settings4.png)

Een beschrijving van het apparaat kunt meestal Hallo eigenaar en Hallo fysieke locatie van Hallo apparaat identificeren. beschrijvingsveld Hallo moet minder dan 256 tekens bevatten.

## <a name="modify-time-settings"></a>Tijdinstellingen wijzigen

Uw apparaat moet de tijd in volgorde tooauthenticate synchroniseren met uw serviceprovider voor cloud-opslag. Gebruik Hallo **algemene instellingen** blade op uw apparaat toomodify Hallo-apparaatinstellingen tijd.

![Apparaatbeschrijving van het in algemene instellingen](./media/storsimple-8000-modify-device-config/modify-general-settings2.png)

 Selecteer uw tijdzone in de vervolgkeuzelijst Hallo. U kunt opgeven tootwo Network Time Protocol (NTP)-servers:

 - **Primaire NTP-server** -Hallo-configuratie is vereist en wordt opgegeven wanneer u Windows PowerShell voor StorSimple tooconfigure uw apparaat. U kunt opgeven dat Hallo standaard Windows Server **time.windows.com** als uw NTP-server. U kunt weergeven Hallo primaire NTP-serverconfiguratie via hello Azure-portal, maar moet u Hallo Windows PowerShell-interface toochange deze. Gebruik Hallo `Set-HcsNTPClientServerAddress` cmdlet toomodify Hallo primaire NTP-server van uw apparaat. Ga toosynxtax voor cmdlet [Set-HcsNTPClientServerAddress] (https://technet.microsoft.com/library/dn688138.aspx) voor meer informatie.

- **Secundaire NTP-server** -Hallo-configuratie is optioneel. U kunt Hallo portal tooconfigure secundaire NTP-server gebruiken.

Wanneer u Hallo NTP-server configureert, moet u ervoor zorgen dat uw netwerk Hallo NTP-verkeer toopass van uw datacenter toohello Internet toestaat. Wanneer u een openbare NTP-server opgeeft, moet u ervoor zorgen dat uw netwerkfirewalls en andere beveiligingsapparaten geconfigureerde tooallow NTP-verkeer tootravel tooand van Hallo buiten netwerk zijn. Als bidirectionele NTP-verkeer niet wordt toegestaan, moet u een interne NTP-server (een Windows-domeincontroller biedt deze functie). Als uw apparaat kan geen tijd synchroniseren, mogelijk kunnen toocommunicate met uw cloud-opslag-provider niet meer.

een lijst met openbare NTP-servers, Ga toohello toosee [NTP-Servers Web](http://support.ntp.org/bin/view/Servers/WebHome).

### <a name="what-happens-if-hello-device-is-deployed-in-a-different-time-zone"></a>Wat gebeurt er als Hallo-apparaat is geïmplementeerd in een andere tijdzone?

Als het Hallo-apparaat is geïmplementeerd in een andere tijdzone, Hallo apparaat tijdzone gewijzigd. Gezien het feit dat alle Hallo back-upbeleid tijdzone Hallo-apparaat gebruikt, wordt de back-upbeleid Hallo automatisch aanpassen in overeenstemming met de nieuwe tijdzone Hallo. Er is geen tussenkomst van de gebruiker is vereist.

## <a name="modify-dns-settings"></a>DNS-instellingen wijzigen

Een DNS-server wordt gebruikt wanneer uw apparaat toocommunicate bij uw serviceprovider voor cloud-opslag probeert. Gebruik Hallo **instellingen** blade op uw apparaat tooview en Hallo geconfigureerd DNS-instellingen te wijzigen. 

![DNS-instellingen in netwerkinstellingen](./media/storsimple-8000-modify-device-config/modify-network-settings1.png)

Voor hoge beschikbaarheid, vereist tooconfigure zijn beide Hallo primaire en secundaire DNS-servers tijdens de implementatie van de eerste apparaat Hallo Hallo.

**Primaire DNS-server** -u Hallo Windows PowerShell voor StorSimple toofirst Hallo primaire DNS-server tijdens de eerste configuratie Hallo opgeven. U kunt primaire DNS-server alleen via Windows PowerShell-interface Hallo Hallo opnieuw configureren. Gebruik Hallo `Set-HcsDNSClientServerAddress` cmdlet toomodify Hallo primaire DNS-server van uw apparaat. Ga voor meer informatie, toosynxtax voor [Set HcsDNSClientServerAddress](https://technet.microsoft.com/library/dn688138.aspx) cmdlet.

**Secundaire DNS-server** -toomodify Hallo secundaire DNS-server, gebruik Hallo `Set-HcsDNSClientServerAddress` cmdlet in Windows PowerShell-interface Hallo Hallo-apparaat of **instellingen** blade van uw StorSimple-apparaat in hello Azure Portal.

toomodify hello secundaire DNS-server in Azure portal uitvoeren Hallo stappen te volgen.

1. Ga tooyour Apparaatbeheer StorSimple-service. Selecteer in de lijst van de Hallo van apparaten, en klikt u op uw apparaat.

2. In Hallo **instellingen** blade te gaan**apparaatinstellingen > netwerk**. Hiermee opent u up Hallo **instellingen** blade. Klik op **DNS-instellingen** tegel. Hallo secundaire DNS-server IP-adres wijzigen.

    ![Secundaire DNS-server IP-adderss wijzigen](./media/storsimple-8000-modify-device-config/modify-secondary-dns1.png)

4. Hallo opdrachtbalk en klik op **opslaan** wanneer u om bevestiging gevraagd, klikt u op **OK**.

    ![Opslaan en wijzigingen bevestigen](./media/storsimple-8000-modify-device-config/modify-secondary-dns-2.png)



## <a name="modify-network-interfaces"></a>Netwerkinterfaces wijzigen

Uw apparaat heeft zes apparaat netwerkinterfaces, waarvan vier 1 GbE zijn en dat de twee 10 GbE zijn. Deze interfaces zijn gelabeld als DATA 0: DATA 5. DATA 0, gegevens-1, gegevens 4 en 5 van de gegevens zijn 1 GbE DATA 2 en DATA 3 10 GbE-netwerkinterfaces zijn.

Gebruik Hallo **instellingen** blade tooconfigure, elke Hallo interfaces toobe gebruikt.

![Netwerkinterfaces via netwerkinstellingen configureren](./media/storsimple-8000-modify-device-config/modify-network-settings3.png)

tooensure hoge beschikbaarheid, raden wij aan dat u ten minste twee interfaces voor iSCSI- en twee interfaces zijn ingeschakeld voor de cloud op uw apparaat. We raden aan maar hoeven niet dat ongebruikte interfaces worden uitgeschakeld.

Voor elke netwerkinterface worden Hallo volgende parameters weergegeven:

* **Snelheid** – geen gebruiker configureerbare parameter. DATA 0, gegevens-1, gegevens 4 en 5 van de gegevens zijn altijd 1 GbE terwijl DATA 2 en DATA 3 10 GbE-interfaces zijn.
  
  > [!NOTE]
  > Snelheid en duplex wordt altijd automatisch-onderhandeld. Jumboframes worden niet ondersteund.
  
* **Interface-status** : een interface kan worden ingeschakeld of uitgeschakeld. Bij inschakeling probeert Hallo apparaat toouse Hallo-interface. We raden aan dat alleen de interfaces die zijn verbonden toohello netwerk en gebruikt worden ingeschakeld. Schakel alle interfaces die u niet gebruikt.
* **Type interface** – deze parameter kunt u tooisolate iSCSI-verkeer van verkeer van de cloud-opslag. Deze parameter is een van de volgende Hallo:
  
  * **Cloud ingeschakeld** – wanneer ingeschakeld, Hallo apparaat deze toocommunicate interface gaat gebruiken met Hallo cloud.
  * **iSCSI ingeschakeld** – wanneer ingeschakeld, Hallo apparaat deze toocommunicate interface gaat gebruiken met Hallo iSCSI-host.
    
    Het is raadzaam dat u iSCSI-verkeer van cloud-opslagverkeer isoleren. Let ook op als de host zich binnen de Hallo hetzelfde subnet als het apparaat, hoeft u geen tooassign een gateway; Als de host zich in een ander subnet dan uw apparaat, moet u echter tooassign een gateway.
* **IP-adres** – wanneer u Hallo netwerkinterfaces, configureert u een virtueel IP-adres (VIP) moet configureren. Dit kan zijn IPv4 of IPv6- of beide. Zowel Hallo IPv4 en IPv6-adresfamilies worden ondersteund voor netwerkinterfaces Hallo-apparaat. Wanneer IPv4 wordt gebruikt, geeft u een 32-bits IP-adres (*xxx.xxx.xxx.xxx*) in punt decimale notatie met punten. Wanneer u IPv6 gebruikt, zijn simpelweg een 4-cijferige voorvoegsel en een 128-bits-adres wordt automatisch gegenereerd voor de netwerkinterface van uw apparaat op basis van het voorvoegsel.
* **Subnet** – dit subnetmasker toohello verwijst en via Hallo Windows PowerShell-interface is geconfigureerd.
* **Gateway** – dit Hallo standaardgateway die door deze interface moet worden gebruikt wanneer er wordt geprobeerd toocommunicate met knooppunten die zich niet binnen de Hallo is dezelfde IP-adresruimte (subnet). Hallo standaardgateway moet in Hallo dezelfde adresruimte (subnet) als Hallo interface IP-adres, zoals wordt bepaald door Hallo subnetmasker op.
* **Vaste IP-adres** – dit veld is alleen beschikbaar als u Hallo DATA 0 configureren interface. Bewerkingen zoals updates of het oplossen van problemen Hallo-apparaat, moet u wellicht tooconnect rechtstreeks toohello apparaat controller. Hallo vaste IP-adres kan worden gebruikt tooaccess zowel Hallo actieve en passieve controller Hallo op uw apparaat.

> [!NOTE]
> * de goede werking tooensure, Controleer of de interfacesnelheid Hallo en duplex op Hallo-switch die de interface van elk apparaat is verbonden met. Switch netwerkinterfaces moet ofwel worden onderhandeld met of worden geconfigureerd voor Gigabit Ethernet (1000 Mbps) en full-duplex. Interfaces besturingssysteem trager of half-duplex leidt tot prestatieproblemen.
> * toominimize onderbrekingen en uitvaltijd, wordt u aangeraden portfast op elk van de poorten die Hallo iSCSI-netwerkinterface van uw apparaat verbinding met maken Hallo-switch in te schakelen. Dit zorgt ervoor dat verbinding met het netwerk kan snel worden opgezet in Hallo-gebeurtenis van een failover.

### <a name="configure-data-0"></a>Configureren van de DATA 0

DATA 0 is standaard ingeschakeld cloud. Bij het configureren van DATA 0, bent u ook de vereiste tooconfigure twee vaste IP-adressen, één voor elke domeincontroller. Deze vaste IP-adressen kunnen gebruikte tooaccess Hallo apparaatcontrollers rechtstreeks en zijn handig wanneer u updates op Hallo-apparaat of wanneer u toegang krijgen tot Hallo controllers voor Hallo doel installeert van het oplossen van problemen.

U kunt vaste IP-domeincontrollers via Hallo DATA 0 instellingenblade Hallo opnieuw configureren.

![Netwerkinterface - DATA 0 configureren](./media/storsimple-8000-modify-device-config/modify-network-settings2.png)

> [!NOTE]
> Hallo vaste IP-adressen voor controller hello worden gebruikt voor het onderhoud Hallo updates toohello apparaat. Daarom moet Hallo vaste IP-adressen routeerbaar en kunnen tooconnect toohello Internet.

### <a name="configure-data-1---data-5"></a>GEGEVENS-1 - 5-gegevens configureren

Voor gegevens-1 - 5 netwerkinterfaces van gegevens, kunt u alle Hallo-netwerkinstellingen configureren zoals wordt weergegeven in de volgende schermafbeelding Hallo:

![Netwerkinterfaces DATA 1 - 5-gegevens configureren](./media/storsimple-8000-modify-device-config/modify-network-settings4.png)


## <a name="swap-or-reassign-ips"></a>Wisselen of opnieuw toewijzen van IP-adressen

Op dit moment wordt als een netwerkinterface op Hallo-controller wordt toegewezen aan een VIP-adres dat wordt gebruikt (door Hallo hetzelfde apparaat of een ander apparaat in Hallo netwerk), Hallo controller via zullen mislukken. Als u wisselen of opnieuw toewijzen van VIP's voor een netwerkinterface van het apparaat, moet u een juiste procedure volgen wanneer u een situatie met een dubbele IP kan maakt.

Volgende stappen tooswap Hallo uitvoeren of opnieuw toewijzen Hallo VIP's voor alle netwerkinterfaces Hallo:

#### <a name="tooreassign-ips"></a>tooreassign IP-adressen

1. Schakel Hallo IP-adres voor beide interfaces.
2. Nadat Hallo IP-adressen zijn uitgeschakeld, toewijzen Hallo nieuwe IP-adressen toohello respectieve interfaces.

## <a name="next-steps"></a>Volgende stappen

* Meer informatie over hoe te[MPIO configureren voor uw StorSimple-apparaat](storsimple-8000-configure-mpio-windows-server.md).
* Meer informatie over hoe te[gebruik Hallo StorSimple Apparaatbeheer service tooadminister uw StorSimple-apparaat](storsimple-8000-manager-service-administration.md).

