---
title: aaaDesigning uw netwerkinfrastructuur voor herstel na noodgevallen | Microsoft Docs
description: Dit artikel worden de overwegingen bij het ontwerpen van netwerk voor Azure Site Recovery
services: site-recovery
documentationcenter: 
author: prateek9us
manager: jwhit
editor: 
ms.assetid: ce787731-d930-4f00-a309-e2fbc2e1f53b
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/20/2017
ms.author: pratshar
ms.openlocfilehash: 18bafa1b8b334192bfaf2f4aeba9f090011041ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="designing-your-network-for-disaster-recovery"></a>Ontwerpen van uw netwerk voor herstel na noodgevallen

Dit artikel is gerichte tooIT-professionals die verantwoordelijk zijn voor veranderd, implementeren en ondersteunen van zakelijke continuïteit en disaster recovery (BCDR)-infrastructuur en willen tooleverage Microsoft Azure Site Recovery (ASR) toosupport en om hun BCDR-services te verbeteren. Dit artikel wordt beschreven praktische overwegingen in het netwerk op disaster recovery site structureren, worden deze Azure of een andere on-premises site. 

## <a name="overview"></a>Overzicht
[Azure Site Recovery (ASR)](https://azure.microsoft.com/services/site-recovery/) is een Microsoft Azure-service die ingedeeld Hallo beveiligings- en hersteltaken van uw gevirtualiseerde toepassingen voor zakelijke continuïteit (BCDR) noodherstel. Dit document is bedoeld tooguide de lezer Hallo door Hallo proces van het ontwerpen van Hallo-netwerken te focussen op IP-adresbereiken en -subnetten op Hallo disaster recovery site veranderd bij het repliceren van virtuele machines (VM's) met Site Recovery.

Bovendien in dit artikel laat zien hoe Site Recovery kunt uitbreidt en een meerdere locaties virtuele datacenter toosupport BCDR-services implementeren op moment van de test- of na noodgevallen.

In een situatie waarin iedereen 24/7 connectiviteit verwacht, is het belangrijker dan ooit tookeep uw infrastructuur en toepassingen zetten. Hallo doel van zakelijke continuïteit en herstel na noodgevallen (BCDR) is toorestore is mislukt-onderdelen zodat Hallo organisatie opnieuw kan snel normale bewerkingen. Ontwikkelen disaster recovery strategieën toodeal met onwaarschijnlijk, vernietigende gebeurtenissen is erg lastig. Dit is vanwege toohello inherente moeite van het voorspellen van toekomstige hello, met name omdat deze zich verhoudt tooimprobable gebeurtenissen en Hallo hoge kosten tooprovide passende maatregelen ter bescherming tegen groot catastrophes.

Essentieel voor BCDR planning, herstel tijd Objective (RTO) en herstel Herstelpuntdoel (RPO) moeten worden gedefinieerd als onderdeel van een noodherstelplan. Wanneer een noodgeval van de klant Hallo datacentrum met Azure Site Recovery, kunnen klanten snel (laag RTO) biedt online brengt de gerepliceerde virtuele machines zich in de secundaire Datacenter Hallo of Microsoft Azure met minimaal gegevensverlies (lage RPO).

Failover wordt mogelijk gemaakt door ASR die in eerste instantie aangewezen virtuele machines opgehaald uit Hallo primaire data center toohello secundaire Datacenter of tooAzure (afhankelijk van het scenario voor Hallo) en vervolgens worden regelmatig vernieuwd Hallo replica's. Bij het plannen van de infrastructuur moet netwerkontwerp worden beschouwd als mogelijke knelpunt kan worden voorkomen dat u van vergadering bedrijf RTO en RPO doelstellingen.  

Wanneer beheerders een noodherstel toodeploy plant, is een belangrijke vragen Hallo in een hoe Hallo virtuele machine bereikbaar zou zijn als Hallo failover is voltooid. ASR kan Hallo beheerder toochoose Hallo netwerk toowhich een virtuele machine zijn verbonden tooafter failover. Als de primaire site hello Azure of een lokale site en vervolgens dit wordt bereikt is door middel van netwerktoewijzing worden beheerd door een VMM-server. Meer informatie over [netwerktoewijzing in Azure tooAzure DR](site-recovery-network-mapping-azure-to-azure.md) en [netwerktoewijzing uit VMM](site-recovery-network-mapping.md)


Hallo beheerder heeft tijdens het ontwerpen van Hallo netwerk voor Hallo herstelsite twee mogelijkheden:

* Gebruik een ander IP-adresbereik voor Hallo-netwerk op de site recovery. In dit scenario Hallo virtuele machine na een failover wordt een nieuw IP-adres verkrijgen en Hallo beheerder toodo zou hebben een DNS-update. 
* Gebruik hetzelfde IP-adresbereik voor Hallo-netwerk op Hallo herstelsite. In bepaalde scenario's liever beheerders tooretain Hallo IP-adressen die ze op de primaire site Hallo zelfs na het Hallo-failover hebben. In een normale scenario zou een beheerder tooupdate Hallo routes tooindicate Hallo nieuwe locatie van Hallo IP-adressen hebben. Maar in Hallo scenario waarop een gespreide subnet tussen primaire Hallo en Hallo herstel sites wordt geïmplementeerd, bewaren Hallo IP-adressen voor virtuele machines die Hallo wordt een aantrekkelijke optie. Uitrekken van een subnet van een lokaal netwerk tooan Azure-netwerk of tussen twee netwerken in Azure is niet mogelijk.  

Wanneer beheerders een noodherstel toodeploy plant, is een belangrijke vragen Hallo hun rekening hoe Hallo toepassingen bereikbaar nadat Hallo failover is voltooid. Moderne toepassingen zijn bijna altijd afhankelijk van de mate van toosome, dus fysiek verplaatsen van een service van één site tooanother vertegenwoordigt een netwerken uitdaging netwerken. Er zijn twee manieren die dit probleem wordt behandeld in oplossingen voor herstel na noodgevallen. Hallo eerste benadering bestaat toomaintain vaste IP-adressen. Ondanks Hallo services verplaatsen en Hallo die als host fungeert voor servers in verschillende fysieke locaties, nemen toepassingen Hallo IP-adresconfiguratie met hen toohello nieuwe locatie. Hallo tweede oplossing omvat volledig Hallo IP-adres wijzigen tijdens het Hallo overstappen naar Hallo herstelde site. Elke methode biedt verschillende implementatie afwijkingen die hieronder worden samengevat.

Hallo beheerder heeft tijdens het ontwerpen van Hallo netwerk voor Hallo herstelsite twee mogelijkheden:

## <a name="option-1-retain-ip-addresses"></a>Optie 1: IP-adressen behouden
Disaster recovery proces vanuit het oogpunt van, toobe Hallo eenvoudigste methode tooimplement met vaste IP-adressen weergegeven, maar heeft een aantal potentiële uitdagingen die in de praktijk het maken Hallo minst populaire benadering. Azure Site Recovery biedt de mogelijkheid van Hallo tooretain Hallo IP-adressen in alle scenario's. Voordat u een IP tooretain beslist, moet de juiste manier toohello beperkingen opgelegd Hallo failoverfuncties worden genomen. Laat het ons bekijkt hello factoren waarmee u kunnen toomake die een beslissing tooretain IP-, of niet adressen. Dit kan op twee manieren worden gerealiseerd, met behulp van een gespreide subnet of u een volledige subnet failover uitvoert.

### <a name="stretched-subnet"></a>Gespreide subnet
Hier worden Hallo subnet beschikbaar gesteld gelijktijdig in zowel primaire als de DR-locaties. Eenvoudige voorwaarden betekent dit dat u kunt een server verplaatsen en de IP-(laag 3) configuratie toohello tweede site- en Hallo netwerk routeert Hallo verkeer toohello nieuwe locatie automatisch. Dit is essentieel toodeal met vanuit het perspectief van een server, maar heeft een aantal uitdagingen:

* Vanuit een Layer 2 (data link-laag)-perspectief moet worden netwerkapparatuur die een gespreide VLAN kunt beheren, maar dit minder, van een probleem als het is nu algemeen beschikbaar is geworden. Hallo tweede en moeilijker probleem is dat door het uitrekken Hallo VLAN Hallo potentiële foutdomein is uitgebreid tooboth sites, wordt in wezen een potentieel risico. Dit is waarschijnlijk niet voorkomt, is het een broadcast-storm gestart, maar kan niet worden geïsoleerd opgetreden. We hebben gemengde mening over dit laatste probleem gevonden en veel geslaagde implementaties evenals 'we zullen nooit implementeren van deze technologie hier' hebt gezien.
* Gespreide subnet is niet mogelijk als u Microsoft Azure als Hallo DR-site.

### <a name="subnet-failover"></a>Subnet failover
Het is mogelijk tooimplement subnet failover tooobtain Hallo voordelen van Hallo uitgerekt subnet oplossing die hierboven worden beschreven zonder uitrekken Hallo-subnet op meerdere sites. Hier een bepaald subnet moeten aanwezig zijn op de Site 1 of 2, maar niet op beide sites tegelijkertijd. In de volgorde toomaintain Hallo IP-adresruimte in Hallo gebeurtenis van een failover, is het mogelijk tooprogrammatically voor Hallo router infrastructuur toomove Hallo subnetten van één site tooanother rangschikken. In een failover-scenario Hallo subnetten zou gekoppeld verplaatsen Hello beveiligde virtuele machines. Hallo grootste nadeel toothis aanpak is in geval van een storing Hallo u toomove Hallo hele subnet, waardoor mogelijk OK hebt, maar kan invloed hebben op Hallo granulatie overwegingen.

We onderzoeken hoe een fictieve onderneming met de naam Contoso kunnen tooreplicate is de locatie van virtuele machines tooa herstel bij storing worden overgenomen Hallo gehele subnet. Eerst kijken we hoe Contoso kunnen toomanage wordt hun subnetten terwijl virtuele machines repliceren tussen twee on-premises locaties en vervolgens bespreken we hoe subnet failover werkt wanneer [Azure wordt gebruikt als Hallo disaster recovery site](#failover-to-azure).

#### <a name="failover-from-on-premises-tooazure"></a>Failover van de lokale tooAzure 
Azure Site Recovery (ASR) kunt Azure toobe gebruikt als een site van het herstel na noodgevallen voor uw virtuele machines.  

We onderzoeken een scenario waarbij een fictief bedrijf met de naam Woodgrove Bank on-premises infrastructuur die als host fungeert voor de line-of-business-toepassingen en ze hun mobiele toepassingen in Azure worden gehost. Connectiviteit tussen de Woodgrove Bank virtuele machines in Azure en on-premises servers wordt verstrekt door een site-naar-site (S2S) virtuele particuliere netwerk (VPN) of ExpressRoute. S2S-VPN kunt van Woodgrove Bank virtueel netwerk in Azure toobe gezien als een uitbreiding van de Woodgrove Bank op lokale netwerk. Deze communicatie wordt ingeschakeld door S2S VPN tussen Woodgrove Bank rand en virtuele Azure-netwerk. Nu wil Woodgrove toouse ASR tooreplicate de werkbelastingen primaire Azure-regio tooanother Azure-regio. Deze optie voldoet aan de behoeften van Hallo van Woodgrove, dat wil een voordelige DR-optie en kunnen toostore gegevens in openbare cloudomgevingen wordt. Woodgrove toodeal met toepassingen en configuraties die afhankelijk van de vastgelegde IP-adressen zijn heeft, daarom ze een vereiste tooretain IP-adressen voor hun toepassingen hebben nadat ze zijn mislukt via tooanother regio in Azure.

Woodgrove heeft besloten tooassign IP-adressen van IP-bereik (172.16.1.0/24, 172.16.2.0/24) tooits adresbronnen in Azure wordt uitgevoerd.

Voor de Woodgrove toobe kunnen tooreplicate de virtuele machines tooAzure behoud Hallo IP-adressen, een Azure-netwerk moet toobe gemaakt. Een uitbreiding van Hallo on-premises netwerk moet zijn dat toepassingen failover van Hallo lokale site tooAzure naadloos kunnen. Azure kunt u tooadd site-naar-site, evenals een punt-naar-site VPN-verbinding toohello virtuele netwerken in Azure gemaakt. Bij het instellen van uw site-naar-site-verbinding, kunt Azure-netwerk u tooroute verkeer toohello on-premises locatie (Azure-aanroepen het lokale netwerk) alleen als Hallo IP-adresbereik anders dan Hallo lokale IP-adresbereik, is omdat Azure niet ondersteuning voor uitrekken subnetten.  Dit betekent dat als er een subnet 192.168.1.0/24 lokale, u kunt geen een lokaal netwerk 192.168.1.0/24 toevoegen in hello Azure-netwerk. Dit is de verwachting omdat Azure kan niet worden vastgesteld of er geen actieve VM's in Hallo subnet zijn en alleen ter informatie DR dat Hallo-subnet wordt gemaakt. toobe kunnen toocorrectly netwerkverkeer buiten een Azure-netwerk Hallo subnetten in Hallo netwerk- en LAN Hallo mogen geen conflicten opleveren.

![Vóór de Subnet-Failover](./media/site-recovery-network-design/network-design7.png)

Vóór de failover

toohelp Woodgrove hun zakelijke vereisten voldoen, moeten we tooimplement Hallo werkstromen te volgen:

* Een extra netwerk maakt, roepen laat het ons herstel netwerk, waarbij Hallo failover virtuele machines moet worden gemaakt.
* tooensure hello IP voor een virtuele machine blijft na een failover, gaat u toohello configureren tabblad onder VM-eigenschappen, Hallo dezelfde IP die Hallo VM een on-premises en klik op opslaan opgeven. Wanneer Hallo VM failover wordt uitgevoerd, wordt de Azure Site Recovery Hallo opgegeven IP-toohello virtuele machine toewijzen.

![Eigenschappen van het netwerk](./media/site-recovery-network-design/network-design8.png)

Zodra de Hallo failover wordt geactiveerd en Hallo virtuele machines worden gemaakt in Hallo herstel netwerk met Hallo gewenst IP-adres, connectiviteit toothis netwerk kan worden gemaakt met behulp van een [Vnet tooVnet verbinding](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md). Indien nodig met deze actie kan scripts worden gebruikt.  Zoals besproken in de vorige sectie Hallo over subnet failover, zelfs in geval van failover-tooAzure Hallo routes zou hebt toobe op de juiste wijze gewijzigd tooreflect is die 192.168.1.0/24 tooAzure nu verplaatst.

![Na een Failover van Subnet](./media/site-recovery-network-design/network-design9.png)

Na een failover

Als u geen een netwerk van het Azure hebt, zoals wordt weergegeven in de vorige Hallo-afbeelding. Na een failover Hallo kunt u een site toosite VPN-verbinding tussen uw 'Primaire Site' en de herstel-netwerk.  


#### <a name="failover-tooa-secondary-on-premises-site"></a>Failover tooa secundaire lokale site
Laat het ons kijken naar een scenario waar we willen Hallo IP-adres van elk van de VM Hallo behouden en failover-Hallo subnet samen te voltooien. Hallo primaire site heeft toepassingen in een subnet 192.168.1.0/24. Wanneer failover Hallo gebeurt, wordt alle Hallo virtuele machines die deel van dit subnet uitmaken toohello herstelsite wordt failover en hun IP-adressen behouden. Routes hebben toobe gewijzigd op de juiste wijze tooreflect Hallo feit dat alle Hallo virtuele machines die horen toosubnet 192.168.1.0/24 toohello herstelsite zijn nu verplaatst.

In Hallo volgende illustratie Hallo van routes tussen primaire site en de site recovery, derde en primaire site en derde en de site recovery heeft toobe op de juiste wijze zijn gewijzigd.

Hallo volgende afbeeldingen ziet Hallo subnetten voordat Hallo failover wordt uitgevoerd. Subnet 192.168.0.1/24 actief is op Hallo primaire Site voordat Hallo failover wordt uitgevoerd en wordt na failover Hallo actief Hallo Herstelsite

![Vóór de Failover](./media/site-recovery-network-design/network-design2.png)

Vóór de failover

Hallo in de volgende afbeelding toont de netwerken en subnetten na een failover.

![Na een Failover](./media/site-recovery-network-design/network-design3.png)

Na een failover

Lokaal op de secundaire site hebt en u gebruikt een VMM server toomanage vervolgens wanneer inschakelen van de beveiliging voor een specifieke virtuele machine, ASR netwerkresources volgens de volgende werkstroom toohello worden toegewezen:

* ASR wijst een IP-adres voor elke netwerkinterface op Hallo virtuele machine uit Hallo statische IP-adresgroep gedefinieerd op de relevante Hallo-netwerk voor elk exemplaar van System Center VMM.
* Hallo dezelfde als Hallo beheerder Hallo hetzelfde IP-adresgroep voor Hallo-netwerk op de herstelsite Hallo als definieert dat van Hallo IP-adresgroep Hallo-netwerk op de primaire site Hallo bij het toewijzen van Hallo IP-adres toohello replica virtuele machine ASR zou toewijzen IP-adres als die van Hallo primaire virtuele machine.  Hallo IP-adres is gereserveerd in VMM, maar niet ingesteld als de failover-IP op Hallo Hyper-v-host. Failover-IP op een Hyper-v-host is net vóór Hallo failover ingesteld.


Als hello dezelfde IP niet beschikbaar is, zou ASR sommige andere beschikbaar IP-adres toewijzen uit Hallo gedefinieerd IP-adresgroep.

Na het Hallo die VM is ingeschakeld voor beveiliging kunt u na sample script tooverify Hallo IP die toohello virtuele machine is toegewezen. Hallo dezelfde IP zou worden ingesteld als Failover IP en toohello VM op moment van failover Hallo toegewezen:

        $vm = Get-SCVirtualMachine -Name <VM_NAME>
        $na = $vm[0].VirtualNetworkAdapters>
        $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
        $ip.address  

> [!NOTE]
> In Hallo scenario waar de virtuele machines DHCP gebruikt, is het Hallo-beheer van IP-adressen volledig buiten Hallo-controle van ASR. Een beheerder heeft tooensure dat Hallo DHCP-server voor Hallo IP-adressen op de herstelsite Hallo van Hallo voorzien kunnen hetzelfde bereik als die van de primaire site Hallo.
>
>



## <a name="option-2-changing-ip-addresses"></a>Optie 2: IP-adressen wijzigen
Deze aanpak lijkt toobe Hallo meest voorkomende op basis van wat wij hebben. Het duurt Hallo vorm van Hallo IP-adres van elke VM die bij Hallo failover betrokken is. Een nadeel van deze benadering vereist Hallo binnenkomende netwerk too'learn' hello toepassing die op IPx was bevindt zich nu op IPy. Zelfs als IPx en IPy logische namen, DNS-vermeldingen hebben doorgaans toobe gewijzigd of leeggemaakte in Hallo-netwerk en vermeldingen in cache in netwerk tabellen toobe bijgewerkt of verwijderd, dus een uitvaltijd kan worden gezien, al naar gelang hoe Hallo DNS-infrastructuur heeft is geïnstalleerd. Deze problemen kunnen worden verminderd door lage TTL-waarden in geval van intranettoepassingen hello gebruiken en [Azure Traffic Manager met ASR](http://azure.microsoft.com/blog/2015/03/03/reduce-rto-by-using-azure-traffic-manager-with-azure-site-recovery/) voor op internet gebaseerde toepassingen

### <a name="changing-hello-ip-addresses---illustration"></a>Hallo IP-adressen - afbeelding wijzigen
Laat het ons bekijkt hello scenario waar u van plan bent toouse verschillende IP-adressen op Hallo van primaire en Hallo herstel sites. In het volgende voorbeeld Hallo hebben we ook een derde site uit waarbij Hallo toepassingen die worden gehost op de primaire of herstel site toegankelijk zijn.

![Verschillende IP - vóór de Failover](./media/site-recovery-network-design/network-design10.png)


In bovenstaande Hallo-afbeelding zijn sommige toepassingen die worden gehost in een subnet 192.168.1.0/24 subnet op Hallo primaire site en ze zijn geconfigureerd toocome up op de herstelsite Hallo in subnet 172.16.1.0/24 na een failover. VPN-verbindingen/netwerkroutes zijn op de juiste wijze geconfigureerd zodat alle drie sites toegang elkaar tot hebben.

Als Hallo afbeelding hieronder bevat nadat ze zijn mislukt op een of meer toepassingen, wordt deze hersteld in Hallo herstel subnet. In dit geval zijn we niet beperkte toofailover Hallo gehele subnet op Hallo hetzelfde moment. Er zijn geen wijzigingen vereist tooreconfigure VPN- of netwerkbeheerder routes. Een failover en een aantal DNS-updates zorgt ervoor dat toepassingen toegankelijk blijven. Als Hallo DNS geconfigureerde tooallow dynamische updates wordt wilt vervolgens Hallo virtuele machines registreren zelf via de nieuwe IP Hallo zodra ze na een failover starten.

![Verschillende IP - na een Failover](./media/site-recovery-network-design/network-design11.png)


Nadat u wellicht niet goed werkende over Hallo replica virtuele machine een IP-adres dat niet dezelfde als Hallo IP-adres van de primaire virtuele machine Hallo Hallo. Virtuele machines Hallo DNS-server die ze gebruiken wordt bijgewerkt nadat ze zijn gestart. DNS-vermeldingen hebben doorgaans toobe gewijzigd of leeggemaakte in Hallo netwerk en vermeldingen in cache in netwerk tabellen hebben toobe bijgewerkt of leeggemaakt, zodat het niet ongewoon toobe geconfronteerd met uitvaltijd terwijl deze statuswijzigingen plaatsvinden. Dit probleem kan worden verholpen door:

* Met behulp van laag TTL-waarden voor intranettoepassingen.
* Toepassingen op basis van het gebruik van Azure Traffic Manager met ASR voor internet.
* Gebruik de volgende Hallo script binnen het herstel van uw plan tooupdate Hallo DNS-Server tooensure een tijdige update (Hallo-script is niet vereist als Hallo dynamische DNS-registratie is geconfigureerd)

        param(
        string]$Zone,
        [string]$name,
        [string]$IP
        )
        $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
        $newrecord = $record.clone()
        $newrecord.RecordData[0].IPv4Address  =  $IP
        Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord

### <a name="changing-hello-ip-addresses--dr-tooazure"></a>Veranderende Hallo IP-adressen: DR tooAzure
Hallo [Networking infrastructuur Setup voor Microsoft Azure als een herstel na noodgevallen Site](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) blogbericht wordt uitgelegd hoe toosetup Hallo vereist Azure VPN-infrastructuur bij het behouden van IP-adressen is geen vereiste. Deze begint met het Hallo-toepassing en zoekt u op hoe toosetup netwerken op lokale en beschrijven op Azure en vervolgens met het sluiten van toodo een testfailover en een geplande failover.

## <a name="next-steps"></a>Volgende stappen
[Meer informatie over](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) hoe Site Recovery bron en doel netwerken toegewezen wanneer een VMM-server gebruikt toomanage Hallo primaire site wordt.
