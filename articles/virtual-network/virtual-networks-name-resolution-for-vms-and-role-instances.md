---
title: aaaResolution voor VM's en Rolinstanties
description: 'Naam van oplossing scenario''s voor Azure IaaS, oplossingen voor hybride, tussen verschillende cloud-services, Active Directory en met uw eigen DNS-server '
services: virtual-network
documentationcenter: na
author: GarethBradshawMSFT
manager: carmonm
editor: tysonn
ms.assetid: 5d73edde-979a-470a-b28c-e103fcf07e3e
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/06/2016
ms.author: telmos
ms.openlocfilehash: 0ec7903cf200c1d04d75601a5b0cefe4268f3dcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="name-resolution-for-vms-and-role-instances"></a>Name Resolution for VMs and Role Instances (Naamomzetting voor virtuele machines en rolinstanties)
Afhankelijk van hoe u Azure toohost IaaS en PaaS hybride oplossingen gebruiken, moet u mogelijk tooallow Hallo VM's en rolinstanties toocommunicate met elkaar maken. Deze communicatie kan worden gedaan met behulp van IP-adressen, is maar het veel eenvoudiger toouse-namen die gemakkelijk kunnen worden onthouden en niet wijzigen. 

Wanneer tooresolve domein namen toointernal IP-adressen rolinstanties en virtuele machines die worden gehost in Azure moeten, kunnen ze een van twee methoden gebruiken:

* [Azure verschafte naamomzetting](#azure-provided-name-resolution)
* [Naamomzetting met uw eigen DNS-server](#name-resolution-using-your-own-dns-server) (die mogelijk naar voren query's toohello Azure DNS-servers) 

Hallo type naamomzetting die u gebruikt, is afhankelijk van hoe uw VM's en rolexemplaren toocommunicate met elkaar moeten.

**Hallo volgende tabel ziet u scenario's en bijbehorende name resolution-oplossingen:**

| **Scenario** | **Oplossing** | **Achtervoegsel** |
| --- | --- | --- |
| Naamomzetting tussen de rolinstanties of virtuele machines zich bevinden in Hallo dezelfde cloud service of een virtueel netwerk |[Azure verschafte naamomzetting](#azure-provided-name-resolution) |de hostnaam of FQDN-naam |
| Naamomzetting tussen de rolinstanties of virtuele machines zich in verschillende virtuele netwerken |Door de klant beheerde DNS-servers doorsturen van query's tussen vnets voor de omzetting van Azure (DNS-proxy).  Zie [naamomzetting met uw eigen DNS-server](#name-resolution-using-your-own-dns-server) |Alleen FQDN |
| Omzetting van lokale computer en de service namen van rolexemplaren te controleren of de virtuele machines in Azure |Door de klant beheerde DNS-servers (bijvoorbeeld op de lokale domeincontroller, lokale alleen-lezen domeincontroller of een secundaire DNS gesynchroniseerd met zoneoverdrachten).  Zie [naamomzetting met uw eigen DNS-server](#name-resolution-using-your-own-dns-server) |Alleen FQDN |
| De resolutie van Azure hostnamen van lokale computers |Doorsturen van query's tooa door de klant beheerde DNS-proxyserver in de bijbehorende vnet hello, Hallo proxy-server stuurt tooAzure voor de omzetting van query's. Zie [naamomzetting met uw eigen DNS-server](#name-resolution-using-your-own-dns-server) |Alleen FQDN |
| Omgekeerde DNS voor interne IP-adressen |[Naamomzetting met uw eigen DNS-server](#name-resolution-using-your-own-dns-server) |N.v.t. |
| Naamomzetting tussen VM's of rolexemplaren die zich in verschillende cloud-services, niet in een virtueel netwerk |Niet van toepassing. Connectiviteit tussen VM's en rolexemplaren in een andere cloud-services wordt niet ondersteund buiten een virtueel netwerk. |N.v.t. |

## <a name="azure-provided-name-resolution"></a>Azure verschafte naamomzetting
Azure biedt interne naamomzetting voor VM's en rolexemplaren die zich bevinden in hetzelfde virtuele netwerk of cloud service Hallo samen met de omzetting van openbare DNS-namen.  Virtuele machines/exemplaren in een cloudservice delen Hallo dezelfde DNS achtervoegsel (zodat alleen Hallo-hostnaam voldoende is), maar in verschillende cloudservices voor klassieke virtuele netwerken hebben verschillende DNS-achtervoegsels dus Hallo FQDN namen van de benodigde tooresolve tussen verschillende cloud-services is.  Hallo DNS-achtervoegsel consistent is op het virtuele netwerk hello (zodat Hallo FQDN-naam is niet nodig) en DNS-namen kunnen worden toegewezen tooboth NIC's en virtuele machines in virtuele netwerken in Hallo Resource Manager-implementatiemodel. Hoewel Azure verschafte naamomzetting geen configuratie vereist is, is het niet de juiste keuze Hallo voor alle implementatiescenario's zoals gezien in Hallo bovenstaande tabel.

> [!NOTE]
> U kunt ook Hallo interne IP-adressen rolinstanties op basis van Hallo rol en het exemplaar nummer met hello Azure Service Management REST API in geval van web-en werkrollen Hallo openen. Zie voor meer informatie [Service Management REST API-verwijzing](https://msdn.microsoft.com/library/azure/ee460799.aspx).
> 
> 

### <a name="features-and-considerations"></a>Functies en overwegingen
**Functies:**

* Gebruiksgemak: geen configuratie is vereist in de volgorde toouse Azure verschafte naamomzetting.
* Hello Azure verschafte name resolution-service is maximaal beschikbaar, opslaan Hallo u moet toocreate en clusters van uw eigen DNS-servers beheren.
* Kan worden gebruikt in combinatie met uw eigen DNS-servers tooresolve zowel on-premises en Azure hostnamen.
* Naamomzetting is opgegeven tussen rol exemplaren/virtuele machines binnen Hallo dezelfde cloudservice zonder dat nodig is voor een FQDN-naam.
* Naamomzetting is tussen virtuele machines in virtuele netwerken die gebruikmaken van Hallo Resource Manager-implementatiemodel, zonder dat nodig is voor Hallo FQDN-naam opgegeven. Virtuele netwerken in het klassieke implementatiemodel Hallo vereisen Hallo FQDN bij het omzetten van namen in andere cloudservices. 
* U kunt hostnamen die het beste uw implementaties te beschrijven in plaats van het werken met de automatisch gegenereerde naam.

**Overwegingen:**

* Hallo gemaakt met een Azure DNS-achtervoegsel kan niet worden gewijzigd.
* U kunt uw eigen records kan niet handmatig registreren.
* WINS- en NetBIOS worden niet ondersteund. (U kunt uw virtuele machines in Windows Verkenner niet zien.)
* Hostnamen moet DNS-compatibele (ze moeten gebruiken alleen 0-9, a-z en '-', en mag niet beginnen of eindigen met een '-'. Zie RFC 3696 sectie 2.)
* DNS-query-verkeer is voor elke virtuele machine beperkt. Dit mag niet van invloed op de meeste toepassingen.  Indien aanvraag beperking is waargenomen, zorg ervoor dat caching aan clientzijde is ingeschakeld.  Zie voor meer informatie [Hallo ophalen van de meeste van Azure verschafte naamomzetting](#Getting-the-most-from-Azure-provided-name-resolution).
* Alleen virtuele machines in Hallo eerste 180 cloud-services zijn geregistreerd voor elke virtuele netwerk in een klassieke implementatiemodel. Dit geldt niet toovirtual netwerken in het Resource Manager-implementatiemodel.

### <a name="getting-hello-most-from-azure-provided-name-resolution"></a>Hallo ophalen van de meeste van Azure verschafte naamomzetting
**Caching aan clientzijde:**

Niet elke DNS-query moet toobe via Hallo netwerk verzonden.  Caching aan clientzijde helpt de latentie te verminderen en de herstelmogelijkheden toonetwork blips verbeteren door terugkerende DNS-query's uit de lokale cache op te lossen.  DNS-records bevatten een Time-To-Live (TTL) waarmee Hallo toostore hello cacherecord voor zo lang mogelijk zonder enige impact op record nieuwheid zodat caching aan clientzijde geschikt voor de meeste situaties is.

Hallo standaard Windows-DNS-Client heeft een ingebouwde DNS-cache.  Sommige Linux distributies omvatten geen cache standaard, wordt aangeraden dat een tooeach Linux VM (na controleren dat nog niet is een lokale cache) worden toegevoegd.

Er zijn een aantal verschillende DNS-cache in pakketten beschikbaar zijn, bijvoorbeeld dnsmasq, zijn hier Hallo stappen tooinstall dnsmasq op de meest voorkomende distributies Hallo:

* **Ubuntu (maakt gebruik van resolvconf)**:
  * alleen het installatiepakket Hallo dnsmasq ('sudo apt get-installatie dnsmasq').
* **SUSE (maakt gebruik van netconf)**:
  * het installatiepakket Hallo dnsmasq ('sudo zypper installeren dnsmasq') 
  * Hallo dnsmasq service ('systemctl inschakelen dnsmasq.service') inschakelen 
  * Start Hallo dnsmasq-service ('systemctl start dnsmasq.service") 
  * bewerken '/ etc/sysconfig/netwerk/config' en wijzigt u NETCONFIG_DNS_FORWARDER = "" te 'dnsmasq'
  * resolv.conf ('netconfig-update') tooset Hallo cache als lokale DNS-resolver Hallo bijwerken
* **OpenLogic (maakt gebruik van NetworkManager)**:
  * het installatiepakket Hallo dnsmasq ('sudo yum installeren dnsmasq')
  * Hallo dnsmasq service ('systemctl inschakelen dnsmasq.service') inschakelen
  * Start Hallo dnsmasq-service ('systemctl start dnsmasq.service")
  * Voeg toe 'toevoegen domain name servers 127.0.0.1;' too"/etc/dhclient-eth0.conf '
  * Hallo netwerk-service ('service netwerk opnieuw starten') tooset Hallo-cache opnieuw opstarten als de lokale DNS-resolver Hallo

> [!NOTE]
> Hallo 'dnsmasq' pakket is slechts één Hallo veel DNS-caches beschikbaar voor Linux.  Controleer voordat u deze gebruikt geschikt is voor uw specifieke behoeften en die geen andere cache is geïnstalleerd.
> 
> 

**Client-side nieuwe pogingen:**

DNS is voornamelijk een UDP-protocol.  Als UDP-protocol Hallo niet levering van berichten garandeert, wordt Pogingslogica op Hallo DNS-protocol zelf behandeld.  Elke DNS-client (besturingssysteem) kan zich voordoen verschillende Pogingslogica, afhankelijk van Hallo auteurs voorkeur:

* Windows besturingssystemen opnieuw proberen na 1 seconde en vervolgens na een andere 2, 4 en een andere 4 seconden. 
* Hallo standaard Linux setup pogingen na 5 seconden.  Het is aanbevolen toochange deze tooretry 5 maal op 1 tweede intervallen.  

toocheck huidige instellingen op een Linux-VM 'cat /etc/resolv.conf' Hallo en bekijkt hello 'options' regel, bijvoorbeeld:

    options timeout:1 attempts:5

Hallo resolv.conf bestand is doorgaans automatisch gegenereerd en mag niet worden bewerkt.  Hallo specifieke stappen voor het toevoegen van Hallo 'options' regel verschillen per distro:

* **Ubuntu** (maakt gebruik van resolvconf):
  * Hallo opties regel too'/etc/resolveconf/resolv.conf.d/head toevoegen ' 
  * resolvconf -u tooupdate uitvoeren
* **SUSE** (maakt gebruik van netconf):
  * Voeg 'timeout:1 pogingen: 5' toohello NETCONFIG_DNS_RESOLVER_OPTIONS = "" parameter in '/ etc/sysconfig/netwerk/config' 
  * tooupdate netconfig-update uitvoeren
* **OpenLogic** (maakt gebruik van NetworkManager):
  * toevoegen van too'/etc/NetworkManager/dispatcher.d/11-dhclient 'echo ' opties timeout:1 pogingen: 5' ' 
  * 'service netwerk restart' tooupdate uitvoeren

## <a name="name-resolution-using-your-own-dns-server"></a>Naamomzetting met uw eigen DNS-server
Er zijn een aantal situaties waarbij de behoeften van uw name resolution mogelijk gaat voorbij Hallo functies van Azure, bijvoorbeeld wanneer met behulp van Active Directory-domeinen of wanneer u de DNS-omzetting tussen virtuele netwerken (vnet's) vereist.  toocover deze scenario's, Azure biedt Hallo mogelijkheid voor toouse u uw eigen DNS-servers.  

DNS-servers binnen een virtueel netwerk kunnen doorsturen van DNS-query's tooAzure recursieve resolvers tooresolve hostnamen binnen dit virtuele netwerk.  Bijvoorbeeld, een domeincontroller (DC) uitgevoerd in Azure reageren tooDNS query's voor de domeinen en alle andere query's tooAzure doorsturen.  Hierdoor kunnen virtuele machines toosee uw lokale bronnen (via Hallo DC) en de Azure verschafte hostnamen (via Hallo-doorstuurserver).  Toegang tooAzure van recursieve resolvers wordt opgegeven via Hallo virtueel IP-adres 168.63.129.16.

DNS-doorsturen inter vnet DNS-omzetting kan ook en kunt uw lokale machines tooresolve Azure verschafte hostnamen.  In volgorde tooresolve hostnaam van een virtuele machine, Hallo DNS-server VM moet zich bevinden op Hallo van hetzelfde virtuele netwerk en geconfigureerde tooforward hostnaam query's tooAzure worden.  Als Hallo DNS-achtervoegsel in elke vnet anders is, kunt u voorwaardelijk doorsturen regels toosend DNS-query toohello Corrigeer dan vnet voor de omzetting.  Hallo volgende afbeelding ziet u twee vnets en een on-premises netwerk tijdens het doorzoeken van inter vnet DNS-omzetting met deze methode.  Een voorbeeld van de DNS-doorstuurserver is beschikbaar in Hallo [galerie van Azure-Snelstartsjablonen](https://azure.microsoft.com/documentation/templates/301-dns-forwarder/) en [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/301-dns-forwarder).

![Inter vnet DNS](./media/virtual-networks-name-resolution-for-vms-and-role-instances/inter-vnet-dns.png)

Wanneer u Azure verschafte naamomzetting, een interne DNS-achtervoegsel (*. internal.cloudapp.net) opgegeven tooeach VM DHCP gebruikt.  Hierdoor hostnaamomzetting als Hallo hostnaam records in Hallo internal.cloudapp.net zone zijn.  Wanneer u uw eigen name resolution-oplossing, Hallo IDN-achtervoegsel niet is opgegeven tooVMs, omdat deze andere DNS-architecturen (zoals scenario's voor het domein verstoort).  In plaats daarvan bieden we een niet-functionerende tijdelijke aanduiding (reddog.microsoft.com).  

Indien nodig, kan Hallo interne DNS-achtervoegsel worden bepaald met behulp van PowerShell of Hallo API:

* Voor virtuele netwerken in het Resource Manager-implementatiemodel Hallo-achtervoegsel is beschikbaar via Hallo [netwerkinterfacekaart](https://msdn.microsoft.com/library/azure/mt163668.aspx) resource of via Hallo [Get-AzureRmNetworkInterface](https://msdn.microsoft.com/library/mt619434.aspx) cmdlet.    
* In de klassieke implementatiemodellen Hallo-achtervoegsel is beschikbaar via Hallo [ophalen implementatie API](https://msdn.microsoft.com/library/azure/ee460804.aspx) aanroepen of via Hallo [Get-AzureVM-Debug](https://msdn.microsoft.com/library/azure/dn495236.aspx) cmdlet.

Als doorstuurt tooAzure niet behoeften van uw query's, moet u tooprovide uw eigen DNS-oplossing.  Uw DNS-oplossing moet:

* Geef juiste hostnaamomzetting, bijvoorbeeld [DDNS](virtual-networks-name-resolution-ddns.md).  Houd er rekening mee, met behulp van DDNS mogelijk moet u toodisable record opruiming van DNS-als Azure DHCP-leases erg lang zijn en opruiming van DNS verwijderen voortijdig registreert. 
* Bieden de juiste oplossing tooallow naamomzetting van externe domeinnamen.
* Worden Hallo toegankelijk (TCP en UDP op poort 53) van Hallo clients deze fungeert en kunnen tooaccess worden internet.
* Beveiligd is tegen toegang vanaf Hallo internet, toomitigate dreigingen van externe agents.

> [!NOTE]
> Voor de beste prestaties bij gebruik van Azure Virtual machines als DNS-servers, IPv6 moet zijn uitgeschakeld en een [openbare IP op exemplaarniveau](virtual-networks-instance-level-public-ip.md) tooeach DNS-server VM moet worden toegewezen.  Als u ervoor toouse Windows Server als uw DNS-server kiest [in dit artikel](http://blogs.technet.com/b/networking/archive/2015/08/19/name-resolution-performance-of-a-recursive-windows-dns-server-2012-r2.aspx) biedt extra prestatieanalyse en optimalisatie.
> 
> 

### <a name="specifying-dns-servers"></a>DNS-servers opgeven
Wanneer u uw eigen DNS-servers, Azure Hallo mogelijkheid toospecify biedt meerdere DNS-servers per virtueel netwerk of per netwerk interface (Resource Manager)-cloudservice (klassiek).  DNS-servers die zijn opgegeven voor een cloud service/netwerkinterface ophalen voorrang boven die zijn opgegeven voor het virtuele netwerk Hallo.

> [!NOTE]
> Verbindingseigenschappen netwerk, zoals DNS-server IP-adressen, mag niet rechtstreeks vanuit Windows virtuele machines worden bewerkt omdat ze tijdens de service kunnen ophalen gewist retoucheren wanneer de virtuele netwerkadapter Hallo opgehaald vervangen. 
> 
> 

Wanneer u Hallo Resource Manager-implementatiemodel, DNS-servers kunnen worden opgegeven in Hallo Portal API/sjablonen ([vnet](https://msdn.microsoft.com/library/azure/mt163661.aspx), [nic](https://msdn.microsoft.com/library/azure/mt163668.aspx)) of PowerShell ([vnet](https://msdn.microsoft.com/library/mt603657.aspx), [nic](https://msdn.microsoft.com/library/mt619370.aspx)).

Wanneer u het klassieke implementatiemodel hello, DNS-servers voor het virtuele netwerk Hallo kan worden opgegeven in Hallo Portal of [hello *netwerkconfiguratie* bestand](https://msdn.microsoft.com/library/azure/jj157100).  Voor cloud-services, Hallo DNS-servers worden opgegeven via [hello *serviceconfiguratie* bestand](https://msdn.microsoft.com/library/azure/ee758710) of in PowerShell ([New-AzureVM](https://msdn.microsoft.com/library/azure/dn495254.aspx)).

> [!NOTE]
> Als u Hallo DNS-instellingen voor een virtueel netwerk/virtuele machine die al is geïmplementeerd wijzigen, moet u op toorestart elke betrokken VM voor Hallo wijzigingen tootake effect.
> 
> 

## <a name="next-steps"></a>Volgende stappen
Resource Manager-implementatiemodel:

* [Een virtueel netwerk maken of bijwerken](https://msdn.microsoft.com/library/azure/mt163661.aspx)
* [Maken of bijwerken van een netwerkinterfacekaart](https://msdn.microsoft.com/library/azure/mt163668.aspx)
* [Nieuwe-AzureRmVirtualNetwork](https://msdn.microsoft.com/library/mt603657.aspx)
* [Nieuwe AzureRmNetworkInterface](https://msdn.microsoft.com/library/mt619370.aspx)

Klassieke implementatiemodel:

* [Het Schema van Azure-Service](https://msdn.microsoft.com/library/azure/ee758710)
* [Virtual Network-configuratieschema](https://msdn.microsoft.com/library/azure/jj157100)
* [Een virtueel netwerk configureren met behulp van een netwerk-configuratiebestand](virtual-networks-using-network-configuration-file.md) 

