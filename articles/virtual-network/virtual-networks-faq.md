---
title: Veelgestelde vragen over het virtuele netwerk aaaAzure | Microsoft Docs
description: Antwoorden toohello veelgestelde meest vragen over Microsoft Azure virtuele netwerken.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 54bee086-a8a5-4312-9866-19a1fba913d0
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/18/2017
ms.author: jdial
ms.openlocfilehash: c2f9faee41b9c45e8bb196c58282d597ae732e54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-network-frequently-asked-questions-faq"></a>Veelgestelde vragen (FAQ) virtuele Azure-netwerk

## <a name="virtual-network-basics"></a>Basisbeginselen van het virtuele netwerk

### <a name="what-is-an-azure-virtual-network-vnet"></a>Wat is een Azure-netwerk (VNet)?
Een Azure-netwerk (VNet) is een weergave van uw eigen netwerk in Hallo cloud. Het is een logische isolatie van hello Azure cloud toegewezen tooyour-abonnement. U kunt gebruiken VNets tooprovision en beheren van virtuele particuliere netwerken (VPN's) in Azure en, desgewenst, koppeling Hallo VNets met andere vnet's in Azure of met uw on-premises IT-infrastructuur toocreate hybride of cross-premises-oplossingen. Elke VNet die u maakt een eigen CIDR-blok heeft, en kan worden gekoppelde tooother VNets en on-premises netwerken zolang Hallo CIDR-blokken niet overlappen. U hebt ook controle van DNS-serverinstellingen voor VNets en segmentering Hallo VNet in subnetten.

Gebruik de VNets aan:

* Een speciale persoonlijke cloudconfiguratie VNet soms u geen configuratie van een cross-premises nodig hebt voor uw oplossing maken. Wanneer u een VNet maakt, uw services en virtuele machines binnen uw VNet kunnen rechtstreeks en veilig communiceren met elkaar in Hallo cloud. Dit verkeer veilig binnen Hallo VNet houdt, maar kunt u nog steeds tooconfigure eindpunt verbindingen voor Hallo VM's en services waarvoor internetcommunicatie als onderdeel van uw oplossing.
* Veilig uitbreiden van uw datacenter met vnet's, kunt u traditionele toosecurely schaal van de site-naar-site (S2S) VPN's de capaciteit van uw datacenter. S2S-VPN's gebruiken IPSEC tooprovide een beveiligde verbinding tussen uw zakelijke VPN-gateway en Azure.
* Schakel hybride cloud scenario's bieden u een vnet's Hallo flexibiliteit toosupport tal van hybride cloud-scenario's. Veilig kunt u cloud-gebaseerde toepassingen tooany type on-premises systeem zoals mainframes en Unix-systemen.

### <a name="how-do-i-know-if-i-need-a-vnet"></a>Hoe weet als ik een VNet nodig?
Hallo [Virtual network-overzicht](virtual-networks-overview.md) artikel vindt u een Beslissingstabel waarmee u besluit Hallo beste netwerk ontwerpoptie voor u.

### <a name="how-do-i-get-started"></a>Hoe ga ik aan de slag?
Ga naar Hallo [documentatie van uw virtuele netwerk](https://docs.microsoft.com/azure/virtual-network/) tooget gestart. Deze inhoud biedt een overzicht en implementatie-informatie voor alle functies van Hallo VNet.

### <a name="can-i-use-vnets-without-cross-premises-connectivity"></a>Kan ik VNets zonder cross-premises connectiviteit gebruiken?
Ja. U kunt een VNet zonder gebruik van hybride verbindingen gebruiken. Dit is vooral handig als u toorun Microsoft Windows Server Active Directory-domeincontrollers en SharePoint-farms in Azure wilt.

### <a name="can-i-perform-wan-optimization-between-vnets-or-a-vnet-and-my-on-premises-data-center"></a>Kan ik WAN-optimalisatie tussen VNets of een VNet en mijn on-premises Datacenter uitvoeren?

Ja. U kunt een [virtueel netwerkapparaat WAN-optimalisatie](https://azure.microsoft.com/marketplace/?term=wan+optimization) van verschillende leveranciers via hello Azure Marketplace.

## <a name="configuration"></a>Configuratie

### <a name="what-tools-do-i-use-toocreate-a-vnet"></a>Wat extra doen ik toocreate een VNet gebruiken?
U kunt Hallo na toocreate in hulpprogramma's gebruiken of een VNet configureren:

* Azure-Portal (voor klassieke en VNets met Resource Manager).
* Een netwerk-configuratiebestand (netcfg - voor klassieke vnet's). Zie Hallo [configureren van een VNet met een netwerk configuratiebestand](virtual-networks-using-network-configuration-file.md) artikel.
* PowerShell (voor klassieke en VNets met Resource Manager).
* Azure CLI (voor klassieke en VNets met Resource Manager).

### <a name="what-address-ranges-can-i-use-in-my-vnets"></a>Welke adresbereiken kan ik gebruiken in mijn vnet's?
Alle IP-adresbereik is gedefinieerd in [RFC 1918](http://tools.ietf.org/html/rfc1918). Bijvoorbeeld: 10.0.0.0/16.

### <a name="can-i-have-public-ip-addresses-in-my-vnets"></a>Kan ik openbare IP-adressen in mijn vnet's hebben?
Ja. Zie voor meer informatie over openbare IP-adresbereiken Hallo [openbare IP-adresruimte in een virtueel netwerk](virtual-networks-public-ip-within-vnet.md) artikel. Uw openbare IP-adressen worden niet rechtstreeks toegankelijk vanaf Internet Hallo.

### <a name="is-there-a-limit-toohello-number-of-subnets-in-my-vnet"></a>Is er een aantal van de toohello beperken met subnetten in mijn VNet?
Ja. Lees Hallo [Azure beperkt](../azure-subscription-service-limits.md#networking-limits) artikel voor meer informatie. Subnet adresruimten elkaar niet overlappen elkaar.

### <a name="are-there-any-restrictions-on-using-ip-addresses-within-these-subnets"></a>Zijn er beperkingen voor het gebruik van IP-adressen binnen deze subnetten?
Ja. Azure bepaalde IP-adressen binnen elk subnet gereserveerd. Hallo zijn eerste en laatste IP-adressen van Hallo subnetten gereserveerd voor protocol overeenstemming, samen met 3 meer adressen voor Azure-services gebruikt.

### <a name="how-small-and-how-large-can-vnets-and-subnets-be"></a>Hoe klein en hoe groot kunnen worden vnet's en subnetten?
de kleinste subnet Hello die wordt ondersteund is een/29 en Hallo grootste is een/8 die (met behulp van de CIDR-subnetdefinities).

### <a name="can-i-bring-my-vlans-tooazure-using-vnets"></a>Kan ik mijn VLAN's tooAzure VNets met brengen?
Nee. Vnet's zijn Layer 3-overlays. Azure biedt geen ondersteuning voor een Layer 2-semantiek.

### <a name="can-i-specify-custom-routing-policies-on-my-vnets-and-subnets"></a>Kan ik aangepaste routeringsbeleid opgeven op mijn vnet's en subnetten?
Ja. U kunt de gebruiker gedefinieerde routering (UDR) gebruiken. Voor meer informatie over UDR, gaat u naar [gebruiker gedefinieerde Routes en doorsturen via IP](virtual-networks-udr-overview.md).

### <a name="do-vnets-support-multicast-or-broadcast"></a>Ondersteunen VNets multicast- of broadcastnetwerkverkeer?
Nee. Wij ondersteunen geen multicast- of broadcast.

### <a name="what-protocols-can-i-use-within-vnets"></a>Welke protocollen kan ik gebruiken binnen VNets?
U kunt TCP, UDP en TCP/IP ICMP-protocollen binnen VNets gebruiken. Multicast, broadcast, IP-in-IP-encapsulated pakketten en Generic Routing Encapsulation (GRE) pakketten worden binnen VNets geblokkeerd. 

### <a name="can-i-ping-my-default-routers-within-a-vnet"></a>Kan ik mijn routers standaard binnen een VNet pingen?
Nee.

### <a name="can-i-use-tracert-toodiagnose-connectivity"></a>Kan ik tracert toodiagnose verbinding gebruiken?
Nee.

### <a name="can-i-add-subnets-after-hello-vnet-is-created"></a>Kan ik subnetten toevoegen nadat Hallo die vnet wordt gemaakt?
Ja. Subnetten kunnen worden toegevoegd tooVNets op elk gewenst moment zolang Hallo subnetadres geen deel uit van een ander subnet in Hallo VNet maakt.

### <a name="can-i-modify-hello-size-of-my-subnet-after-i-create-it"></a>Kan ik Hallo grootte van mijn subnet wijzigen nadat ik deze maken?
Ja. U kunt toevoegen, verwijderen, uitbreiden of verkleinen van een subnet als er zijn geen virtuele machines of services die zijn geïmplementeerd in het.

### <a name="can-i-modify-subnets-after-i-created-them"></a>Kan ik subnetten wijzigen nadat ik ze zijn gemaakt?
Ja. U kunt toevoegen, verwijderen en aanpassen van Hallo CIDR-blokken die worden gebruikt door een VNet.

### <a name="can-i-connect-toohello-internet-if-i-am-running-my-services-in-a-vnet"></a>Kan ik toohello verbinden internet als ik mijn services in een VNet?
Ja. Alle services die zijn geïmplementeerd in een VNet verbinding kunnen maken van toohello internet. Elke cloudservice die is geïmplementeerd in Azure heeft een openbaar adresseerbare VIP tooit toegewezen. Hebt u toodefine invoereindpunten voor PaaS-rollen en -eindpunten voor virtuele machines tooenable deze services tooaccept verbindingen van Hallo internet.

### <a name="do-vnets-support-ipv6"></a>Vnet's bieden ondersteuning voor IPv6?
Nee. U kunt IPv6 niet gebruiken met Vnetten op dit moment.

### <a name="can-a-vnet-span-regions"></a>Kan een VNet regio's omspannen?
Nee. Een VNet is beperkt tooa één regio.

### <a name="can-i-connect-a-vnet-tooanother-vnet-in-azure"></a>Kan ik een VNet tooanother VNet in Azure verbinden?
Ja. U kunt verbinding maken met een VNet tooanother VNet gebruiken:
- Een Azure VPN-Gateway. Lees Hallo [een VNet-naar-VNet-verbinding configureren](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) artikel voor meer informatie. 
- VNet-peering. Lees Hallo [VNet-peering overzicht](virtual-network-peering-overview.md) artikel voor meer informatie.

## <a name="name-resolution-dns"></a>Naamomzetting (DNS)

### <a name="what-are-my-dns-options-for-vnets"></a>Wat zijn de DNS-opties voor VNets?
Gebruik Hallo Beslissingstabel op Hallo [naamomzetting voor VM's en Rolexemplaren](virtual-networks-name-resolution-for-vms-and-role-instances.md) pagina tooguide u door alle Hallo DNS-opties beschikbaar.

### <a name="can-i-specify-dns-servers-for-a-vnet"></a>Kan ik DNS-servers opgeven voor een VNet?
Ja. U kunt DNS-server IP-adressen in Hallo VNet-instellingen opgeven. Dit wordt toegepast als Hallo standaard DNS-server (s) voor alle virtuele machines in Hallo VNet.

### <a name="how-many-dns-servers-can-i-specify"></a>Hoeveel DNS-servers kan ik opgeven?
Verwijzing Hallo [Azure beperkt](../azure-subscription-service-limits.md#networking-limits) artikel voor meer informatie.

### <a name="can-i-modify-my-dns-servers-after-i-have-created-hello-network"></a>Kan ik mijn DNS-servers niet wijzigen nadat ik Hallo netwerk hebt gemaakt?
Ja. U kunt Hallo lijst met DNS-server voor uw VNet op elk gewenst moment wijzigen. Als u uw lijst met DNS-server wijzigt, moet u toorestart Hallo VM's in uw VNet zodat ze toopick up Hallo nieuwe DNS-server.

### <a name="what-is-azure-provided-dns-and-does-it-work-with-vnets"></a>Wat is Azure DNS- en werkt het met VNets?
Azure DNS-is een multitenant-DNS-service die worden aangeboden door Microsoft. Azure registreert alle virtuele machines en cloud service-rolexemplaren in deze service. Deze service biedt naamomzetting door hostnaam voor VM's en rolexemplaren die zich in Hallo dezelfde cloudservice en Hallo met FQDN-naam voor de VM's en rolinstanties in hetzelfde VNet. Lees Hallo [naamomzetting voor VM's en Rolexemplaren](virtual-networks-name-resolution-for-vms-and-role-instances.md) artikel toolearn meer over DNS.

> [!NOTE]
> Er is een beperking op dit moment toohello eerst 100 cloudservices in een VNet voor de naamomzetting van cross-tenant met behulp van Azure verschafte DNS. Als u uw eigen DNS-server gebruikt, is deze beperking niet van toepassing.
> 
> 

### <a name="can-i-override-my-dns-settings-on-a-per-vm--service-basis"></a>Kan ik mijn DNS-instellingen van een VM per negeren / service basis?
Ja. U kunt DNS-servers instellen voor een per cloud service basis toooverride Hallo netwerk standaardinstellingen. We raden echter aan dat u het hele netwerk DNS zo veel mogelijk.

### <a name="can-i-bring-my-own-dns-suffix"></a>Kan ik mijn eigen DNS-achtervoegsel brengen?
Nee. U kunt een aangepaste DNS-achtervoegsel opgeven voor uw vnet's.

## <a name="connecting-virtual-machines"></a>Verbinding maken met virtuele machines

### <a name="can-i-deploy-vms-tooa-vnet"></a>Kan ik virtuele machines tooa VNet implementeren?
Ja. Alle network interfaces (NIC) gekoppeld tooa VM is geïmplementeerd via Hallo Resource Manager-implementatiemodel moet verbonden tooa VNet. Virtuele machines die worden geïmplementeerd via de klassieke implementatiemodel Hallo kunnen eventueel worden verbonden tooa VNet.

### <a name="what-are-hello-different-types-of-ip-addresses-i-can-assign-toovms"></a>Wat zijn de verschillende typen Hallo van IP-adressen ik tooVMs kunt toewijzen?
* **Persoonlijk:** tooeach NIC binnen elke virtuele machine wordt toegewezen. Hallo-adres wordt toegewezen via een Hallo statische of dynamische methoden. Privé IP-adressen worden toegewezen uit Hallo-bereik dat u hebt opgegeven in de subnetinstellingen Hallo van uw VNet. Resources die zijn geïmplementeerd via de klassieke implementatiemodel Hallo privé IP-adressen zijn toegewezen, zelfs als ze niet verbonden bent tooa VNet. Een persoonlijke IP-adres toegewezen door Hallo dynamische methode blijft tooa resource toegewezen tot Hallo resource wordt verwijderd (virtuele machines of Cloud Service implementatiesites). Een persoonlijke IP-adres toegewezen met dynamische methode Hallo kan veranderen wanneer u een virtuele machine opnieuw wordt opgestart nadat in het Hallo (toewijzing ongedaan gemaakt) staat gestopt. Een persoonlijke IP-adres is toegewezen aan Hallo statische methode blijft toegewezen tooa resource tot Hallo resource wordt verwijderd. Als u moet tooensure dat Hallo persoonlijke IP-adres voor een resource nooit worden gewijzigd totdat Hallo resource wordt verwijderd, een particulier IP-adres met de statische methode Hallo toewijzen.
* **Openbaar:** eventueel toegewezen tooNICs gekoppeld tooVMs geïmplementeerd via hello Azure Resource Manager-implementatiemodel. Hallo-adres kan worden toegewezen met een statische of dynamische toewijzingsmethode Hallo. Alle virtuele machines en Cloud Services-rolexemplaren die worden geïmplementeerd via de klassieke implementatiemodel Hallo bestaan binnen een cloudservice die is toegewezen een *dynamische*, openbare virtuele IP-adres (VIP)-adres. Een openbare *statische* IP-adres, aangeroepen een [gereserveerd IP-adres](virtual-networks-reserved-public-ip.md), eventueel kunnen worden toegewezen als een VIP-adres. U kunt de openbare IP-adressen tooindividual exemplaren van virtuele machines of Cloud Services-rol is geïmplementeerd via de klassieke implementatiemodel Hallo toewijzen. Deze adressen heten [niveau openbare IP-instantie (ILPIP](virtual-networks-instance-level-public-ip.md) lost en dynamisch kunnen worden toegewezen.

### <a name="can-i-reserve-a-private-ip-address-for-a-vm-that-i-will-create-at-a-later-time"></a>Kan ik een particulier IP-adres reserveren voor een virtuele machine die ik op een later tijdstip wilt maken?
Nee. Een persoonlijke IP-adres kan niet worden gereserveerd. Als een persoonlijk IP-adres beschikbaar is zal het exemplaar worden toegewezen tooa VM of rol door Hallo DHCP-server. Worden Hallo die u wilt dat Hallo persoonlijke IP-adres toobe toegewezen aan dat de virtuele machine mogelijk of is niet toegestaan. U kunt echter Hallo privé IP-adres van een bestaande VM tooany beschikbaar privé IP-adres wijzigen.

### <a name="do-private-ip-addresses-change-for-vms-in-a-vnet"></a>Persoonlijke IP-adressen wijzigen voor virtuele machines in een VNet doen?
Dat hangt ervan af. Dynamische particuliere IP-adressen met een VM blijven totdat de gestopt (toewijzing opgeheven) of is verwijderd. Statische privé IP-adressen worden niet vrijgegeven van een virtuele machine totdat deze wordt verwijderd.

### <a name="can-i-manually-assign-ip-addresses-toonics-within-hello-vm-operating-system"></a>Kan ik handmatig IP-adressen tooNICs binnen Hallo VM besturingssysteem toewijzen?
Ja, maar dit wordt niet aanbevolen. Hallo IP-adres handmatig wijzigen voor een NIC in het besturingssysteem van een virtuele machine kan leiden toolosing connectiviteit toohello VM als Hallo IP-adres toegewezen tooa NIC binnen hello Azure VM toochange zijn.

### <a name="what-happens-toomy-ip-addresses-if-i-stop-a-cloud-service-deployment-slot-or-shutdown-a-vm-from-within-hello-operating-system"></a>Wat gebeurt er toomy IP-adressen als ik een Cloudservice implementatiesleuf of het afsluiten een virtuele machine uit in het besturingssysteem Hallo stoppen?
Er zijn geen. Hallo IP-adressen (openbare VIP, openbare en persoonlijke) blijven toegewezen toohello cloud service implementatiesleuf of virtuele machine. Dynamische adressen zijn alleen beschikbaar als een virtuele machine is gestopt (toewijzing ongedaan gemaakt) of verwijderd, of een cloud service-implementatiesleuf wordt verwijderd. Te klikken op Hallo **stoppen** knop voor een virtuele machine binnen hello Azure-portal de status tooStopped stelt (toewijzing opgeheven). Hallo VM verliest in dit geval zijn IP-adressen.

### <a name="can-i-move-vms-from-one-subnet-tooanother-subnet-in-a-vnet-without-re-deploying"></a>Kan ik virtuele machines verplaatsen van één subnet tooanother subnet in een VNet zonder opnieuw implementeren?
Ja. U vindt meer informatie in Hallo [hoe toomove een VM of de rol tooa ander subnet exemplaar](virtual-networks-move-vm-role-to-subnet.md) artikel.

### <a name="can-i-configure-a-static-mac-address-for-my-vm"></a>Kan ik een statische MAC-adres configureren voor mijn VM
Nee. Een MAC-adres kan niet statisch worden geconfigureerd.

### <a name="will-hello-mac-address-remain-hello-same-for-my-vm-once-it-has-been-created"></a>Hallo MAC-adres blijft dezelfde Hallo voor mijn virtuele machine nadat deze is gemaakt?
Ja, blijft Hallo MAC-adres Hallo die identiek zijn voor een virtuele machine via Hallo Resource Manager en klassieke implementatiemodel hebt geïmplementeerd, totdat deze wordt verwijderd. Hallo MAC-adres is eerder uitgebracht als hello VM is gestopt (toewijzing ongedaan gemaakt), maar nu Hallo MAC-adres worden bewaard, zelfs als Hallo VM in Hallo staat de toewijzing ongedaan gemaakt.

### <a name="can-i-connect-toohello-internet-from-a-vm-in-a-vnet"></a>Kan ik toohello verbinden internet vanaf een virtuele machine in een VNet?
Ja. Alle virtuele machines en Cloud Services-rolexemplaren die binnen een VNet zijn geïmplementeerd kunnen toohello Internet verbinden.

## <a name="azure-services-that-connect-toovnets"></a>Azure-services die verbinding maken met tooVNets

### <a name="can-i-use-azure-app-service-web-apps-with-a-vnet"></a>Kan ik Azure App Service Web Apps met een VNet gebruiken?
Ja. U kunt de Web-Apps binnen een VNet met een as-omgeving (App Service-omgeving) implementeren. Alle Web-Apps kunnen veilig verbinding maken en toegang tot bronnen in uw Azure VNet hebt u een punt-naar-site-verbinding geconfigureerd voor uw VNet. Zie voor meer informatie Hallo artikelen te volgen:

* [Web-Apps maken in App Service-omgeving](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [Uw app integreren met een Azure-netwerk](../app-service-web/web-sites-integrate-with-vnet.md)
* [VNet-integratie en hybride verbindingen gebruiken met WebApps](../app-service-web/web-sites-integrate-with-vnet.md#hybrid-connections-and-app-service-environments)

### <a name="can-i-deploy-cloud-services-with-web-and-worker-roles-paas-in-a-vnet"></a>Kan ik Cloud Services implementeren met web- en werkrollen rollen (PaaS) in een VNet?
Ja. (Optioneel) kunt u Cloud Services-rolexemplaren binnen VNets implementeren. toodo dus u Hallo VNet-naam en Hallo rol-en subnet toewijzingen opgeven in het netwerk-configuratiesectie Hallo van uw serviceconfiguratie. U hoeft niet tooupdate een van de binaire bestanden.

### <a name="can-i-connect-a-virtual-machine-scale-set-vmss-tooa-vnet"></a>Kan ik een virtuele Machine schaal instellen (VMSS) tooa VNet verbinden?
Ja. U moet een VMSS tooa VNet verbinding.

### <a name="can-i-move-my-services-in-and-out-of-vnets"></a>Kan ik mijn services in en uit de VNets verplaatsen?
Nee. U kunt services in en uit de VNets niet verplaatsen. U hebt toodelete en opnieuw implementeren Hallo service toomove het tooanother VNet.

## <a name="security"></a>Beveiliging

### <a name="what-is-hello-security-model-for-vnets"></a>Wat is de beveiligingsmodel Hallo voor VNets?
Vnet's zijn volledig geïsoleerd van elkaar en andere services die worden gehost in hello Azure-infrastructuur. Een VNet is grens van een vertrouwensrelatie.

### <a name="can-i-restrict-inbound-or-outbound-traffic-flow-toovnet-connected-resources"></a>Kan ik binnenkomend of uitgaand verkeer stroom tooVNet verbonden bronnen beperken?
Ja. U kunt toepassen [Netwerkbeveiligingsgroepen](virtual-networks-nsg.md) tooindividual subnetten binnen een VNet NIC's gekoppeld tooa VNet of beide.

### <a name="can-i-implement-a-firewall-between-vnet-connected-resources"></a>Kan ik een firewall tussen het VNet verbonden resources implementeren?
Ja. U kunt een [virtueel netwerkapparaat firewall](https://azure.microsoft.com/en-us/marketplace/?term=firewall) van verschillende leveranciers via hello Azure Marketplace.

### <a name="is-there-information-available-about-securing-vnets"></a>Is er informatie beschikbaar over het beveiligen van VNets?
Ja. Zie Hallo [Azure Network Security Overview](../security/security-network-overview.md) artikel voor meer informatie.

## <a name="apis-schemas-and-tools"></a>API's, schema's en hulpprogramma 's

### <a name="can-i-manage-vnets-from-code"></a>Kan ik VNets beheren vanuit code?
Ja. U kunt REST-API's gebruiken voor VNets in Hallo [Azure Resource Manager](https://msdn.microsoft.com/library/mt163658.aspx) en [klassieke (Service Management)](http://go.microsoft.com/fwlink/?LinkId=296833)) implementatiemodellen.

### <a name="is-there-tooling-support-for-vnets"></a>Is er tooling ondersteuning voor VNets?
Ja. Meer informatie over het gebruik van:
- Azure portal toodeploy VNets via Hallo Hallo [Azure Resource Manager](virtual-networks-create-vnet-arm-pportal.md) en [klassieke](virtual-networks-create-vnet-classic-pportal.md) implementatiemodellen.
- PowerShell toomanage VNets die zijn geïmplementeerd via Hallo [Resource Manager](/powershell/resourcemanager/azurerm.network/v3.1.0/azurerm.network.md) en [klassieke](/powershell/module/azure/?view=azuresmps-3.7.0) implementatiemodellen.
- Hallo [Azure-opdrachtregelinterface (CLI)](../virtual-machines/azure-cli-arm-commands.md#azure-network-commands-to-manage-network-resources) toomanage VNets die zijn geïmplementeerd via beide implementatiemodellen.  
