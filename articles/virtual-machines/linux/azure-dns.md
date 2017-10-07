---
title: aaaDNS opties voor naamomzetting voor Linux virtuele machines in Azure
description: Naam resolutie scenario's voor virtuele Linux-machines in Azure IaaS, met inbegrip van opgegeven DNS-services, hybride externe DNS- en Bring Your Own DNS-server.
services: virtual-machines
documentationcenter: na
author: RicksterCDN
manager: timlt
editor: tysonn
ms.assetid: 787a1e04-cebf-4122-a1b4-1fcf0a2bbf5f
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/19/2016
ms.author: rclaus
ms.openlocfilehash: 7df2320b6f6b42b479bf4070ea60fe5770a78a41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="dns-name-resolution-options-for-linux-virtual-machines-in-azure"></a>Opties voor Linux virtuele machines in Azure DNS-naamomzetting
Azure biedt DNS-naamomzetting standaard voor alle virtuele machines die zich in één virtueel netwerk. U kunt uw eigen DNS-naam resolutie oplossing implementeren door uw eigen DNS-services op uw virtuele machines te configureren die Azure als host fungeert. Hallo moeten volgende scenario's u helpen kiezen Hallo een die geschikt is voor uw situatie.

* [Naamomzetting door Azure worden geboden](#azure-provided-name-resolution)
* [Naamomzetting met uw eigen DNS-server](#name-resolution-using-your-own-dns-server)

Hallo type naamomzetting die u gebruikt, is afhankelijk van hoe uw virtuele machines en rolinstanties toocommunicate met elkaar moeten.

Hallo volgende tabel ziet u scenario's en bijbehorende name resolution-oplossingen:

| **Scenario** | **Oplossing** | **Achtervoegsel** |
| --- | --- | --- |
| De naamomzetting tussen de rolinstanties of virtuele machines in Hallo hetzelfde virtuele netwerk |[Naamomzetting door Azure worden geboden](#azure-provided-name-resolution) |hostnaam of FQDN-naam (fully qualified domain name) |
| Naamomzetting tussen de rolinstanties of virtuele machines in verschillende virtuele netwerken |Door de klant beheerde DNS-servers doorsturen van query's tussen virtuele netwerken voor de omzetting van Azure (DNS-proxy). Zie [naamomzetting met uw eigen DNS-server](#name-resolution-using-your-own-dns-server). |Alleen FQDN |
| De resolutie van lokale computers en -namen van rolexemplaren te controleren of de virtuele machines in Azure |Door de klant beheerde DNS-servers (bijvoorbeeld op de lokale domeincontroller, lokale alleen-lezen domeincontroller of een secundaire DNS gesynchroniseerd met behulp van zoneoverdrachten). Zie [naamomzetting met uw eigen DNS-server](#name-resolution-using-your-own-dns-server). |Alleen FQDN |
| De resolutie van Azure hostnamen van lokale computers |Query's tooa door de klant beheerde DNS-proxyserver in de bijbehorende virtuele netwerk Hallo doorsturen. Hallo proxy-server stuurt tooAzure query's voor naamomzetting. Zie [naamomzetting met uw eigen DNS-server](#name-resolution-using-your-own-dns-server). |Alleen FQDN |
| Omgekeerde DNS voor interne IP-adressen |[Naamomzetting met uw eigen DNS-server](#name-resolution-using-your-own-dns-server) |N.v.t. |

## <a name="name-resolution-that-azure-provides"></a>Naamomzetting door Azure worden geboden
Azure biedt interne naamomzetting voor virtuele machines en rolexemplaren die zich in hetzelfde virtuele netwerk Hallo samen met de omzetting van openbare DNS-namen. In virtuele netwerken die zijn gebaseerd op Azure Resource Manager is Hallo DNS-achtervoegsel consistent op het virtuele netwerk Hallo; Hallo FQDN-naam is niet nodig. DNS-namen kunnen worden toegewezen tooboth netwerkinterfacekaarten (NIC's) en virtuele machines. Hoewel het Hallo-naamomzetting die Azure biedt geen configuratie vereist, is het niet de juiste keuze Hallo voor alle implementatiescenario's weergegeven op de voorgaande tabel Hallo.

### <a name="features-and-considerations"></a>Functies en overwegingen
**Functies:**

* Er is geen configuratie vereist toouse naamomzetting die Azure biedt.
* Hallo name resolution-service die Azure biedt is maximaal beschikbaar. U geen toocreate nodig hebt en clusters van uw eigen DNS-servers beheren.
* Hallo name resolution-service die Azure biedt kan worden gebruikt samen met uw eigen DNS-servers tooresolve zowel on-premises en Azure hostnamen.
* Naamomzetting is tussen virtuele machines in virtuele netwerken zonder dat nodig is voor Hallo FQDN-naam opgegeven.
* U kunt hostnamen die het beste uw implementaties te beschrijven in plaats van het werken met de automatisch gegenereerde naam.

**Overwegingen:**

* Hallo DNS-achtervoegsel dat Azure maakt, kan niet worden gewijzigd.
* U kunt uw eigen records kan niet handmatig registreren.
* WINS- en NetBIOS worden niet ondersteund.
* Hostnamen moet DNS-compatibele.
    Namen moeten alleen 0-9, a-z, gebruiken en '-', en ze mag niet beginnen of eindigen met een '-'. Zie RFC 3696 sectie 2.
* DNS-query-verkeer is voor elke virtuele machine beperkt. Beperking mag niet van invloed op de meeste toepassingen.  Indien aanvraag beperking is waargenomen, zorg ervoor dat caching aan clientzijde is ingeschakeld.  Zie voor meer informatie [ophalen Hallo van naamomzetting die Azure biedt de meeste](#getting-the-most-from-name-resolution-that-azure-provides).

### <a name="getting-hello-most-from-name-resolution-that-azure-provides"></a>Hallo van naamomzetting die Azure biedt de meeste ophalen
**Caching aan clientzijde:**

Sommige DNS-query's worden niet via Hallo-netwerk verzonden. Caching aan clientzijde helpt de latentie te verminderen en de herstelmogelijkheden toonetwork inconsistenties verbeteren door terugkerende DNS-query's uit de lokale cache op te lossen. DNS-records bevatten een Time-To-Live (TTL), waardoor Hallo toostore hello cacherecord voor zo lang mogelijk zonder enige impact op record versheid. Als gevolg hiervan is het geschikt is voor de meeste situaties caching aan clientzijde.

Sommige Linux-distributies omvatten geen cache standaard. Het is raadzaam dat u een cache tooeach Linux virtuele machine toevoegen nadat u hebt gecontroleerd dat nog niet een lokale cache is.

Enkele andere DNS-cache van pakketten, zoals dnsmasq, zijn beschikbaar. Hier volgen Hallo stappen tooinstall dnsmasq op de meest voorkomende distributies Hallo:

**Ubuntu (maakt gebruik van resolvconf)**
  * Het installatiepakket Hallo dnsmasq ('sudo apt get-installatie dnsmasq').

**SUSE (maakt gebruik van netconf)**:
1. Het installatiepakket Hallo dnsmasq ('sudo zypper installeren dnsmasq').
2. Hallo dnsmasq-service ('systemctl inschakelen dnsmasq.service') inschakelen.
3. Start Hallo dnsmasq-service ('systemctl start dnsmasq.service').
4. Bewerken '/ etc/sysconfig/netwerk/config' en wijzigt u NETCONFIG_DNS_FORWARDER = "" te 'dnsmasq'.
5. Resolv.conf ('netconfig-update') tooset Hallo cache als lokale DNS-resolver Hallo niet bijwerken.

**CentOS door Rogue Wave-Software (voorheen OpenLogic; maakt gebruik van NetworkManager)**
1. Het installatiepakket Hallo dnsmasq ('sudo yum installeren dnsmasq').
2. Hallo dnsmasq-service ('systemctl inschakelen dnsmasq.service') inschakelen.
3. Start Hallo dnsmasq-service ('systemctl start dnsmasq.service').
4. Voeg toe 'toevoegen domain name servers 127.0.0.1;' too"/etc/dhclient-eth0.conf '.
5. Hallo netwerk-service ('service netwerk opnieuw starten') tooset Hallo-cache opnieuw opstarten als de lokale DNS-resolver Hallo

> [!NOTE]
> : Hallo 'dnsmasq' pakket is slechts één Hallo veel DNS in de cache opgeslagen die beschikbaar zijn voor Linux. Voordat u deze kunt gebruiken, Controleer de geschiktheid voor uw behoeften en die geen andere cache is geïnstalleerd.
>
>

**Nieuwe pogingen voor clientzijde**

DNS is voornamelijk een UDP-protocol. Omdat Hallo UDP-protocol niet levering van berichten garanderen, verwerkt Hallo DNS-protocol zelf Pogingslogica. Elke DNS-client (besturingssysteem) kan zich voordoen verschillende Pogingslogica afhankelijk van de maker van de Hallo voorkeur van:

* Windows-besturingssystemen opnieuw proberen na een tweede en nog een keer na de andere twee, vier en andere vier seconden.
* Hallo standaard Linux setup pogingen na vijf seconden.  U moet deze tooretry vijf keer met een interval van één seconde.  

toocheck Hallo huidige instellingen op een virtuele Linux-machine, 'cat /etc/resolv.conf', en bekijkt hello 'options' regel, bijvoorbeeld:

    options timeout:1 attempts:5

Hallo resolv.conf bestand automatisch wordt gegenereerd en mag niet worden bewerkt. Hallo specifieke stappen die Hallo 'opties' regel verschillen per distributiepunt toevoegen:

**Ubuntu** (maakt gebruik van resolvconf)
1. Hallo opties regel too'/etc/resolveconf/resolv.conf.d/head toevoegen '.
2. Resolvconf -u tooupdate worden uitgevoerd.

**SUSE** (maakt gebruik van netconf)
1. Voeg 'timeout:1 pogingen: 5' toohello NETCONFIG_DNS_RESOLVER_OPTIONS = "" parameter in '/ etc/sysconfig/netwerk/config'.
2. Tooupdate netconfig-update worden uitgevoerd.

**CentOS door Rogue Wave-Software (voorheen OpenLogic)** (maakt gebruik van NetworkManager)
1. Toevoegen van too'/etc/NetworkManager/dispatcher.d/11-dhclient 'echo ' opties timeout:1 pogingen: 5', '.
2. 'Service netwerk restart' tooupdate worden uitgevoerd.

## <a name="name-resolution-using-your-own-dns-server"></a>Naamomzetting met uw eigen DNS-server
De behoeften van uw name resolution mogelijk verder dan Hallo-functies die Azure biedt. U kunt bijvoorbeeld vereisen dat DNS-omzetting tussen virtuele netwerken. toocover dit scenario kunt u uw eigen DNS-servers.  

DNS-servers binnen een virtueel netwerk kan forward DNS-query toorecursive resolvers van hostnamen Azure tooresolve die zich in hetzelfde virtuele netwerk Hallo. Een DNS-server die wordt uitgevoerd in Azure reageren bijvoorbeeld tooDNS query's voor de eigen DNS-zone van bestanden en alle andere query's tooAzure door te sturen. Deze functionaliteit kunnen virtuele machines toosee beide de vermeldingen in de zonebestanden en hostnamen die Azure (via Hallo-doorstuurserver biedt). Toegang toohello recursieve resolvers van Azure wordt opgegeven via Hallo virtueel IP-adres 168.63.129.16.

DNS-doorsturen DNS-omzetting tussen virtuele netwerken kan ook en kunt uw lokale machines tooresolve hostnamen die Azure biedt. tooresolve hostnaam van de virtuele machines, virtuele machine van Hallo DNS-server moet zich bevinden in hetzelfde virtuele netwerk Hallo en worden de geconfigureerde tooforward hostnaam query's tooAzure. Aangezien Hallo DNS-achtervoegsel in elk virtueel netwerk verschilt, kunt u voorwaardelijk doorsturen regels toosend DNS-query toohello corrigeren virtueel netwerk voor naamomzetting. Hallo volgende afbeelding ziet u twee virtuele netwerken en een on-premises netwerk tijdens het doorzoeken van DNS-omzetting tussen virtuele netwerken met deze methode:

![DNS-omzetting tussen virtuele netwerken](./media/azure-dns/inter-vnet-dns.png)

Wanneer u naamomzetting die Azure biedt, krijgt Hallo interne DNS-achtervoegsel tooeach virtuele machine met behulp van DHCP. Wanneer u uw eigen name resolution-oplossing, is dit achtervoegsel niet opgegeven toovirtual machines omdat Hallo achtervoegsel andere DNS-architecturen verstoort. toorefer toomachines door de FQDN-naam of tooconfigure Hallo-achtervoegsel op uw virtuele machines, kunt u PowerShell of Hallo API toodetermine Hallo achtervoegsel:

* Voor virtuele netwerken die worden beheerd met Azure Resource Manager, Hallo-achtervoegsel is beschikbaar via Hallo [netwerkinterfacekaart](https://msdn.microsoft.com/library/azure/mt163668.aspx) resource. U kunt ook uitvoeren Hallo `azure network public-ip show <resource group> <pip name>` opdracht toodisplay Hallo details van uw openbare IP-adres, waaronder Hallo FQDN-naam van Hallo NIC.

Als het doorsturen van tooAzure niet behoeften van uw query's, moet u tooprovide uw eigen DNS-oplossing.  Uw DNS-oplossing moet:

* Geef juiste hostnaamomzetting, bijvoorbeeld [DDNS](../../virtual-network/virtual-networks-name-resolution-ddns.md). Als u DDNS gebruikt, moet u mogelijk toodisable opruiming van DNS-record. DHCP-leases van Azure erg lang zijn en opruiming kan DNS-records verwijderen voortijdig.
* Bieden de juiste oplossing tooallow naamomzetting van externe domeinnamen.
* Toegankelijk (TCP en UDP op poort 53) van het fungeert Hallo-clients en kunnen tooaccess Hallo Internet.
* Beveiligd is tegen toegang vanaf Hallo Internet toomitigate dreigingen van externe agents.

> [!NOTE]
> Voor de beste prestaties wanneer u virtuele machines in Azure DNS-servers, IPv6 uitschakelen en wijs een [openbare IP op exemplaarniveau](../../virtual-network/virtual-networks-instance-level-public-ip.md) tooeach DNS-server virtuele machine.  
>
>
