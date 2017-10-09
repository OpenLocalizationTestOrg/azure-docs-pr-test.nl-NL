---
title: aaaGetting de slag met Microsoft Azure-beveiliging | Microsoft Docs
description: Dit artikel bevat een overzicht van Microsoft Azure-beveiligingsmogelijkheden en algemene overwegingen voor organisaties die hun activa tooa cloudprovider wilt migreren.
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: 8d8a0088-c85a-48e7-bd04-2bc7b78b0691
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/09/2017
ms.author: yurid
ms.openlocfilehash: c61dd99ffd0143bc7b165367dadadc977ffcf47b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-microsoft-azure-security"></a>Aan de slag met de beveiliging in Microsoft Azure
Wanneer u bouwen of migreren van IT activa tooa cloudprovider, zijn u afhankelijk te zijn van die organisatie mogelijkheden tooprotect uw toepassingen en gegevens met Hallo services en ze toomanage Hallo beveiliging van uw cloud-gebaseerde activa bieden Hallo-besturingselementen.

Azure infrastructuur is speciaal ontworpen van Hallo faciliteit tooapplications voor het hosten van miljoenen klanten tegelijkertijd en biedt een betrouwbare basis waarop bedrijven hun beveiliging behoeften kunnen. Bovendien Azure biedt u een breed scala aan configureerbare beveiliging opties en Hallo mogelijkheid toocontrol ze zodat u beveiliging toomeet Hallo unieke vereisten van uw implementaties kunt aanpassen.

In dit overzichtsartikel over de beveiliging in Azure komen de volgende onderwerpen aan de orde:

* Azure-services en functies kunt u toohelp Beveilig uw services en -gegevens in Azure.
* Hoe Microsoft hello Azure-infrastructuur toohelp beveiligt uw gegevens en toepassingen beveiligen.

## <a name="identity-and-access-management"></a>Identiteits- en toegangsbeheer
Het is essentieel tooIT-infrastructuur, gegevens en toepassingen te beheren. Microsoft Azure biedt deze mogelijkheden door services zoals Azure Active Directory (Azure AD), Azure Storage en biedt ondersteuning voor meerdere standaarden en API's.

[Azure AD](../active-directory/active-directory-whatis.md) is een identiteitsopslagplaats en de engine voor verificatie, autorisatie en toegangsbeheer voorziet in een organisatie gebruikers, groepen en objecten. Azure AD biedt ontwikkelaars ook een effectieve manier toointegrate identiteitsbeheer in hun toepassingen. Industriestandaard-protocollen, zoals [SAML 2.0](https://en.wikipedia.org/wiki/SAML_2.0), [WS-Federation](https://msdn.microsoft.com/library/bb498017.aspx), en [OpenID Connect](http://openid.net/connect/) aanmelden mogelijk maken op platformen, zoals .NET, Java, Node.js en PHP.

Hallo REST gebaseerde Graph API kan ontwikkelaars tooread en write toohello map uit een willekeurig platform. Dankzij de ondersteuning van [OAuth 2.0](http://oauth.net/2/), kunnen ontwikkelaars mobiele en webtoepassingen die zijn geïntegreerd met Microsoft en derden web-API's en bouwen van hun eigen beveiligde web-API's. Er zijn open source-clientbibliotheken beschikbaar voor .Net, Windows Store, iOS en Android, en er worden meer bibliotheken ontwikkeld.

### <a name="how-azure-enables-identity-and-access-management"></a>Identiteits- en toegangsbeheer in Azure
Azure AD kan worden gebruikt als een zelfstandige clouddirectory voor uw organisatie of als een geïntegreerde oplossing met uw bestaande on-premises Active Directory. Sommige integratiefuncties omvatten directory-synchronisatie en eenmalige aanmelding (SSO). Deze Hallo bereik van uw bestaande on-premises identiteiten in Hallo cloud uitbreiden en Hallo beheerder en gebruiker ervaring te verbeteren.

Azure biedt daarnaast onder andere de volgende mogelijkheden voor identiteits- en toegangsbeheer:

* Azure AD kunt [SSO](https://azure.microsoft.com/documentation/videos/overview-of-single-sign-on/) tooSaaS toepassingen, ongeacht waar ze worden gehost. Voor sommige toepassingen kan federatieve aanmelding worden gebruikt via Azure AD en voor andere toepassingen kan eenmalige aanmelding (SSO) met een wachtwoord worden gebruikt. Federatieve toepassingen kunnen ook ondersteuning bieden voor het inrichten van gebruikers en het bewaren van wachtwoorden in een wachtwoordkluis.
* Toegang toodata in [Azure Storage](https://azure.microsoft.com/services/storage/) wordt beheerd via verificatie. Elk opslagaccount is een primaire sleutel ([opslagaccountsleutel](https://msdn.microsoft.com/library/azure/ee460785.aspx), of SAK) en een secundaire geheime sleutel (shared access signature voor Hallo of SAS).
* Azure AD levert de identiteit als via de federation Service met behulp van [Active Directory Federation Services](../active-directory/fundamentals-identity.md), synchronisatie en replicatie met on-premises adreslijsten.
* [Azure multi-factor Authentication](../multi-factor-authentication/multi-factor-authentication.md) hello multi-factor authentication-service waarvoor gebruikers tooverify aanmeldingen met een mobiele app, telefonische oproep of SMS-bericht is. Worden kan gebruikt met Azure AD-toohelp veilige on-premises resources met hello Azure multi-factor Authentication-server en aangepaste toepassingen en mappen met Hallo SDK.
* [Azure AD Domain Services](https://azure.microsoft.com/services/active-directory-ds/) kunt u virtuele Azure-machines tooa domein toevoegen zonder het implementeren van domeincontrollers. U kunt toothese virtuele machines zich aanmelden met uw bedrijfsreferenties in Active Directory en domein virtuele machines beheren met behulp van Groepsbeleid tooenforce beveiligingsbasislijnen op uw Azure virtuele machines.
* [Azure Active Directory B2C](https://azure.microsoft.com/services/active-directory-b2c/) biedt een maximaal beschikbare globale-identity management-service voor consumententoepassingen die schaalbaar toohundreds miljoenen identiteiten. De service kan worden geïntegreerd in zowel mobiele als webplatforms. Uw consumenten kunnen aanmelden tooall uw toepassingen via aanpasbare ervaringen met behulp van hun bestaande sociale accounts of maken van nieuwe referenties.

## <a name="data-access-control-and-encryption"></a>Gegevenstoegangsbeheer en versleuteling
Microsoft maakt gebruik van Hallo principes van scheiding van taken en [minimale bevoegdheden](https://en.wikipedia.org/wiki/Principle_of_least_privilege) in Azure-bewerkingen. Toegang toodata door medewerkers van de ondersteuning van Azure de expliciete toestemming vereist en wordt verleend op een basis van het type 'just-in-time' die is geregistreerd en gecontroleerd, klikt u vervolgens ingetrokken na voltooiing van Hallo engagement.

Azure biedt ook meerdere mogelijkheden voor het beveiligen van gegevens in rust en onderweg. Dit omvat de versleuteling van gegevens, bestanden, toepassingen, services, communicatie en stations. U kunt versleutelen voordat deze in Azure plaatst en sleutels ook opslaan in uw lokale datacenters.

![Microsoft Antimalware in Azure](./media/azure-security-getting-started/sec-azgsfig1.PNG)

### <a name="azure-encryption-technologies"></a>Versleutelingstechnologieën van Azure
U kunt meer informatie over beheerderstoegang tooyour abonnementomgeving verzamelen met behulp van [Azure AD-rapportage](../active-directory/active-directory-reporting-audit-events.md). U kunt configureren [BitLocker-stationsversleuteling](https://technet.microsoft.com/library/cc732774.aspx) op VHD's met gevoelige gegevens in Azure.

Andere functies in Azure die u helpt uw gegevens veilig tookeep zijn onder andere:

* Ontwikkelaars kunnen bouwen versleuteling in Hallo-toepassingen die ze in Azure implementeren met behulp van Windows hello [CryptoAPI](https://msdn.microsoft.com/library/ms867086.aspx) en .NET Framework.
* Volledig beheer Hallo sleutels met versleuteling aan clientzijde voor Azure Blob-opslag. Hallo opslagservice nooit ziet Hallo sleutels en geen Hallo gegevens kan decoderen.
* [Azure Rights Management (Azure RMS)](https://technet.microsoft.com/library/jj585026.aspx) (Hello [RMS SDK](https://msdn.microsoft.com/library/dn758244.aspx)) biedt bestands- en gegevensniveau codering en gegevenslek preventie tot toegangsbeheer op basis van beleid.
* Azure ondersteunt [op tabelniveau en op kolomniveau codering (TDE/wissen)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/12/recommendations-for-using-cell-level-encryption-in-azure-sql-database.aspx) in virtuele machines van SQL Server en het derde ondersteunt lokale Sleutelbeheer servers in datacentra.
* Toegangscodes voor opslag, handtekeningen voor gedeelde toegang, certificaten en andere sleutels zijn uniek tooeach Azure-tenant.
* Azure [StorSimple](http://www.microsoft.com/server-cloud/products/storsimple/overview.aspx) hybride opslag versleutelt gegevens via een 128-bits openbaar/persoonlijk sleutelpaar voordat u dit tooAzure Storage uploadt.
* Azure ondersteunt en talrijke versleuteling mechanismen, met inbegrip van SSL/TLS, IPsec en AES, afhankelijk van het Hallo-gegevenstypen, containers en -transporten gebruikt.

## <a name="virtualization"></a>Virtualisatie
Hello Azure-platform maakt gebruik van een gevirtualiseerde omgeving. Gebruikersexemplaren werken als zelfstandige virtuele machines die geen toegang tot tooa fysieke host-server en deze isolatie wordt afgedwongen met behulp van fysieke [processor (ring-0-en ring 3) bevoegdheidsniveaus](https://en.wikipedia.org/wiki/Protection_ring).

Ring 0 is Hallo meest privileged en 3 Hallo minste. Hallo gastbesturingssysteem wordt uitgevoerd in een minder bevoegdheden Ring 1 en toepassingen worden uitgevoerd Hallo laagst Ring 3. Deze virtualisatie van fysieke resources leidt tooa duidelijke scheiding tussen het gastbesturingssysteem en hypervisor, wat leidt tot extra beveiliging scheiding tussen twee Hallo.

Hello Azure hypervisor fungeert als een micro-kernel en worden alle hardware toegangsaanvragen van de Gast virtuele machines toohello host voor de verwerking met behulp van een gedeeld geheugen interface VMBus aangeroepen. Dit voorkomt dat gebruikers het verkrijgen van toegang voor onbewerkte lezen, schrijven/uitvoeren toohello system en verkleint Hallo risico van het delen van systeembronnen.

![Microsoft Antimalware in Azure](./media/azure-security-getting-started/sec-azgsfig2.PNG)

### <a name="how-azure-implements-virtualization"></a>De implementatie van virtualisatie in Azure
Azure maakt gebruik van een firewall hypervisor (pakketfilter) die is geïmplementeerd in Hallo hypervisor en geconfigureerd door een agent fabric-controller. Hiermee worden tenants beter beveiligd tegen onbevoegde toegang. Standaard al het verkeer wordt geblokkeerd als een virtuele machine wordt gemaakt en Hallo fabric controller agent vervolgens Hallo pakket filter tooadd configureert *regels en uitzonderingen* tooallow verkeer toegestaan.

Er zijn twee categorieën regels die hier worden geprogrammeerd:

* **Configuratie of infrastructuur regels machine**: standaard alle communicatie is geblokkeerd. Er zijn uitzonderingen tooallow een virtuele machine toosend en DHCP en DNS-verkeer ontvangen. Virtuele machines kunnen ook verkeer verzenden toohello 'openbare' internet en verzenden verkeer tooother virtuele machines binnen Hallo-cluster en Hallo OS activeringsserver. lijst van toegestane uitgaande bestemmingen Hallo virtuele machines bevat geen Azure-router subnetten, Azure management back-end en andere eigenschappen van Microsoft.
* **Configuratiebestand van de rol**: Hiermee definieert u Hallo inkomende toegangsbeheerlijsten (ACL's) op basis van het servicemodel Hallo-tenant. Bijvoorbeeld, als een tenant een webfront-end op poort 80 op een bepaalde virtuele machine heeft, Azure opent vervolgens TCP-poort 80 tooall IP-adressen als u een eindpunt in Hallo configureren kunt [Azure klassieke implementatiemodel](../azure-resource-manager/resource-manager-deployment-model.md). Als Hallo virtuele machine een back-end- of worker-rol die zijn uitgevoerd heeft, wordt geopend Hallo worker-rol toohello virtuele machine die alleen binnen het Hallo-dezelfde tenant.

## <a name="isolation"></a>Isolatie
Een ander belangrijk cloud beveiligingsvereiste is scheiding tooprevent onbevoegde en onbedoelde overdracht van gegevens tussen implementaties in een gedeelde architectuur met meerdere tenants.

Azure implementeert [toegangsbeheer netwerk](https://azure.microsoft.com/blog/network-isolation-options-for-machines-in-windows-azure-virtual-networks/) en scheiding via VLAN-isolatie, ACL's, load balancers en IP-filters. Het externe verkeer beperkt inkomende tooports en protocollen op uw virtuele machines die u definieert. Azure implementeert filteren tooprevent vervalst netwerkverkeer en beperken van binnenkomende en uitgaande verkeer tootrusted platform-onderdelen. Er zijn verkeersstroombeleidsregels geïmplementeerd voor grensbeveiligingsapparaten die het verkeer standaard weigeren.

![Microsoft Antimalware in Azure](./media/azure-security-getting-started/sec-azgsfig3.PNG)

NAT (Network Address Translation) wordt gebruikt tooseparate interne netwerkverkeer van het externe verkeer. Intern verkeer is niet extern routeerbaar. [Virtuele IP-adressen](http://blogs.msdn.com/b/cloud_solution_architect/archive/2014/11/08/vips-dips-and-pips-in-microsoft-azure.aspx) die extern routeerbaar zijn, worden omgezet in [interne dynamische IP](http://blogs.msdn.com/b/cloud_solution_architect/archive/2014/11/08/vips-dips-and-pips-in-microsoft-azure.aspx)-adressen die alleen routeerbaar zijn binnen Azure.

Externe verkeer tooAzure virtuele machines is met firewall via de ACL's op routers, load balancers en Layer 3-switches. Alleen specifieke bekende protocollen zijn toegestaan. ACL's bestaan in place toolimit verkeer van virtuele machines voor gasten tooother VLAN's gebruikt voor beheer. Bovendien wordt verkeer gefilterd via IP-filters op Hallo OS verdere limieten Hallo hostverkeer op beide lagen van koppelings- en gegevens.

### <a name="how-azure-implements-isolation"></a>De implementatie van isolatie in Azure
Hello Azure-Infrastructuurcontroller is verantwoordelijk voor het toewijzen van infrastructuurresources tootenant werkbelastingen en het Unidirectioneel communicatie van Hallo toovirtual hostmachines beheert. Hello Azure hypervisor afgedwongen geheugen en proces scheiding tussen virtuele machines en netwerkverkeer tooguest OS tenants veilig van routes. Azure implementeert ook isolatie voor tenants, opslag en virtuele netwerken.

* Elke Azure AD-tenant is logisch geïsoleerd met behulp van beveiligingsgrenzen.
* Azure storage-accounts zijn unieke tooeach abonnement en toegang moet worden geverifieerd met behulp van de sleutel van een opslagaccount.
* Virtuele netwerken zijn logisch is geïsoleerd door een combinatie van unieke privé IP-adressen, firewalls en IP-ACL's. Netwerktaakverdelers verkeer toohello juiste tenants op basis van de eindpuntdefinities worden gerouteerd.

## <a name="virtual-networks-and-firewalls"></a>Virtuele netwerken en firewalls
Hallo [gedistribueerde en virtuele netwerken](http://download.microsoft.com/download/4/3/9/43902EC9-410E-4875-8800-0788BE146A3D/Windows%20Azure%20Network%20Security%20Whitepaper%20-%20FINAL.docx) in de help van Azure ervoor dat uw particuliere netwerkverkeer logisch is geïsoleerd van verkeer op andere virtuele netwerken in Azure.

![Microsoft Antimalware in Azure](./media/azure-security-getting-started/sec-azgsfig4.PNG)

Uw abonnement kunt bevatten meerdere geïsoleerde particuliere netwerken (en zijn de firewall, taakverdeling en netwerkadresomzetting).

Azure biedt drie primaire niveaus van netwerk scheiding in elke Azure cluster toologically segregate verkeer. [Virtual local area network](https://azure.microsoft.com/services/virtual-network/) (VLAN's) worden gebruikt tooseparate klantverkeer van de rest Hallo van hello Azure-netwerk. Toegang toohello Azure-netwerk van buitenaf Hallo-cluster is beperkt tot en met load balancers.

Netwerkverkeer tooand van virtuele machines moet doorgeven aan Hallo hypervisor virtuele switch. Hallo IP-filter-component in Hallo hoofdmap OS Hallo hoofdmap virtuele machine van de virtuele gastmachines Hallo en Hallo virtuele gastmachines van elkaar geïsoleerd. Hiermee worden uitgevoerd voor het filteren van verkeer toorestrict communicatie tussen de knooppunten van een tenant en de Hallo openbare Internet (op basis van de serviceconfiguratie van de klant Hallo), ze te scheiden van andere tenants.

Hallo IP-filter helpt voorkomen dat virtuele machines voor gasten van:

* Vervalste verkeer wordt gegenereerd.
* Geen verkeer ontvangt verholpen toothem.
* Het routeren van verkeer tooprotected infrastructuur eindpunten.
* Verzenden of ontvangen van ongeschikte broadcast-verkeer.

U kunt uw virtuele machines naar plaatsen [virtuele netwerken van Azure](https://azure.microsoft.com/documentation/services/virtual-network/). Deze virtuele netwerken zijn vergelijkbaar toohello netwerken die u in on-premises omgevingen configureert waarin ze worden doorgaans gekoppeld aan een virtuele switch. Virtuele machines verbonden toohello hetzelfde virtuele netwerk kan communiceren met elkaar zonder aanvullende configuratie. U kunt ook verschillende subnetten configureren in uw virtuele netwerk.

U kunt Azure Virtual Network-technologieën toohelp beveiligde communicatie te volgen in het virtuele netwerk hello gebruiken:

* [**Netwerkbeveiligingsgroepen (nsg's)**](../virtual-network/virtual-networks-nsg.md). U kunt een NSG toocontrol verkeer tooone of meer exemplaren van de virtuele machine gebruiken in uw virtuele netwerk. Een netwerkbeveiligingsgroep bevat toegangsbeheerregels waarmee verkeer wordt toegestaan of geweigerd op basis van verkeersrichting, protocol, bronadres en poort en doeladres en poort.
* [**Gebruiker gedefinieerde routering**](../virtual-network/virtual-networks-udr-overview.md). U kunt beheren Hallo routering van pakketten via een virtueel apparaat door te maken van de gebruiker gedefinieerde routes die Hallo volgende hop voor pakketten tooa specifiek subnet toogo tooa virtuele beveiliging netwerkapparaat opgeven.
* [**Doorsturen via IP**](../virtual-network/virtual-networks-udr-overview.md). Beveiliging van een virtueel netwerkapparaat moet kunnen tooreceive binnenkomend verkeer dat niet geadresseerd tooitself. een virtuele machine tooreceive verkeer tooallow geadresseerd tooother bestemmingen, u doorsturen via IP voor Hallo virtuele machine inschakelen.
* [**Geforceerde tunneling**](../vpn-gateway/vpn-gateway-about-forced-tunneling.md). Geforceerde tunneling, kunt u het omleiden of 'force' alle internetverkeer gegenereerd door uw virtuele machines in een virtueel netwerk back tooyour on-premises locatie via een site-naar-site VPN-tunnel voor inspectie en controle
* [**Eindpunt-ACL's**](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). U kunt bepalen welke computers binnenkomende verbindingen van Hallo Internet tooa virtuele machine zijn toegestaan in het virtuele netwerk met het eindpunt-ACL's definiëren.
* [**Beveiligingsoplossingen voor partnernetwerken**](https://azure.microsoft.com/marketplace/). Er zijn een aantal beveiligingsoplossingen van partners netwerk die u vanaf hello Azure Marketplace openen kunt.

### <a name="how-azure-implements-virtual-networks-and-firewalls"></a>Hoe Azure implementeert virtuele netwerken en firewalls
Azure implementeert filteren van netwerkpakketten firewalls op alle host- en gastverkeer virtuele machines standaard. Installatiekopieën van het Windows-besturingssysteem van hello Azure Marketplace hebben ook Windows Firewall standaard ingeschakeld. Load balancers op Hallo perimeter van communicatie van netwerken in openbare Azure-beheer op basis van IP-ACL's worden beheerd door beheerders van de klant.

Als in Azure als onderdeel van normale bewerkingen of tijdens een noodgeval gegevens van de klant worden verplaatst, gebeurt dat via private, versleutelde communicatiekanalen. Andere werkzaam bij Azure toouse in virtuele netwerken en firewalls mogelijkheden zijn:

* **Systeemeigen hostfirewall**: Azure Service Fabric en Azure Storage worden uitgevoerd op een eigen besturingssysteem dat geen hypervisor heeft. Daarom is Hallo windows firewall geconfigureerd met Hallo vorige twee sets met regels. Opslag wordt systeemeigen toooptimize prestaties uitgevoerd.
* **Hostfirewall**: Hallo hostfirewall is tooprotect Hallo hostbesturingssysteem dat wordt uitgevoerd Hallo hypervisor. Hallo-regels zijn geprogrammeerde tooallow alleen Hallo Service Fabric-controller en vakken tootalk toohello host OS gaan op een specifieke poort. Hallo andere uitzonderingen zijn tooallow DHCP-antwoord en DNS-antwoorden. Azure maakt gebruik van een machine-configuratiebestand met de sjabloon Hallo firewallregels voor Hallo gastbesturingssysteem. Hallo-host zelf wordt aanvallen van buitenaf beveiligd door een Windows firewall geconfigureerd toopermit alleen communicatie van bekende, geverifieerde bronnen.
* **Gast firewall**: Hallo regels in Hallo virtuele machine Switch pakketfilters maar geprogrammeerde in verschillende software (zoals Hallo Windows Firewall stukje Hallo gastbesturingssysteem) worden gerepliceerd. Hallo Gast virtuele machine firewall kunt geconfigureerde toorestrict communicatie tooor van Hallo Gast virtuele machine zijn, zelfs als Hallo communicatie wordt toegestaan door de configuraties op Hallo host IP-Filter. Bijvoorbeeld, u kunt toouse Hallo Gast virtuele machine firewall toorestrict communicatie tussen twee van de VNets die zijn geconfigureerd tooconnect tooone een andere.
* **Opslag-firewall (FW)**: Hallo-firewall op Hallo opslag front-end filtert verkeer toobe alleen op de poorten 80/443 en andere benodigde hulpprogramma-poorten. Hallo-firewall op Hallo opslag back-end voorkomt dat communicatie toocome alleen opslag-front-endservers.
* **Virtuele netwerkgateway**: Hallo [Azure virtuele netwerkgateway](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md) fungeert als Hallo cross-premises gateway verbinding maken met uw workloads in Azure Virtual Network tooyour lokale sites. Het vereiste tooconnect is tooon-premises-sites via [IPSec-site-naar-site VPN-tunnels](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md), of via [ExpressRoute](../expressroute/expressroute-introduction.md) circuits. Voor IPsec/IKE-VPN-tunnels Hallo gateways IKE handshakes uitvoeren en Hallo IPsec S2S VPN-tunnels tussen virtuele netwerken Hallo en lokale sites tot stand brengen. Virtuele netwerkgateways ook beëindigen [punt-naar-site VPN-verbindingen](../vpn-gateway/vpn-gateway-point-to-site-create.md).

## <a name="secure-remote-access"></a>Veilige externe toegang
Gegevens die zijn opgeslagen in de cloud Hallo moet voldoende beveiligingen ingeschakeld tooprevent exploits hebben en vertrouwelijkheid en integriteit tijdens in transit. Hiertoe behoren ook netwerkbeheervoorzieningen die aansluiten bij de op beleid gebaseerde, controleerbare identiteits- en toegangsbeheermechanismen van een organisatie.

Ingebouwde cryptografische technologie kunt u tooencrypt communicatie binnen en tussen implementaties, tussen Azure-regio's en vanaf Azure tooon-premises datacenters. Beheerder toegang toovirtual machines via [extern bureaublad-sessies](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json), [externe Windows PowerShell](http://blogs.technet.com/b/heyscriptingguy/archive/2013/09/07/weekend-scripter-remoting-the-cloud-with-windows-azure-and-powershell.aspx), en hello Azure-portal wordt altijd versleuteld.

toosecurely uit te breiden uw on-premises datacenter toohello cloud, biedt Azure [site-naar-site VPN](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md) en [punt-naar-site VPN](../vpn-gateway/vpn-gateway-point-to-site-create.md), plus specifieke verbindingen met [ExpressRoute](../expressroute/expressroute-introduction.md)(tooAzure verbindingen zijn versleuteld met virtuele netwerken via VPN).

### <a name="how-azure-implements-secure-remote-access"></a>De implementatie van veilige externe toegang in Azure
Verbindingen toohello Azure-portal moet altijd worden geverifieerd en ze SSL/TLS nodig hebben. U kunt management certificaten tooenable beveiligde management configureren. Beveiliging van industriestandaard-protocollen, zoals [SSTP](https://technet.microsoft.com/magazine/2007.06.cableguy.aspx) en [IPsec](https://en.wikipedia.org/wiki/IPsec) worden volledig ondersteund.

Met [Azure ExpressRoute](../expressroute/expressroute-introduction.md) kunt u particuliere verbindingen maken tussen Azure-datacenters en -infrastructuur binnen uw onderneming of in een co-locatie-omgeving. ExpressRoute-verbindingen gaan niet via Hallo openbare Internet. Ze bieden meer betrouwbaarheid, sneller en hebben ze lagere latenties en betere beveiliging dan typische op Internet gebaseerde koppelingen. In sommige gevallen overbrengen van gegevens tussen on-premises locaties en Azure met behulp van ExpressRoute-verbindingen kan ook aanzienlijke kostenvoordelen opleveren.

## <a name="logging-and-monitoring"></a>Logboekregistratie en bewaking
Azure biedt geverifieerde logboekregistratie van beveiliging relevante gebeurtenissen die een audittrail genereren en engineering toobe tegen tootampering is. Dit omvat systeeminformatie, zoals het beveiligingslogboek in virtuele machines van Azure-infrastructuur en Azure AD. Gebeurtenis beveiligingsbewaking omvat het verzamelen van gebeurtenissen, zoals wijzigingen in de DHCP- of DNS-server IP-adressen; poging tot toegang tooports, protocollen of IP-adressen die zijn geblokkeerd door ontwerp; wijzigingen in beleids- of firewall beveiligingsinstellingen; maken van het account of groep; en onverwachte processen of stuurprogramma-installatiebestand.

![Microsoft Antimalware in Azure](./media/azure-security-getting-started/sec-azgsfig5.PNG)

Controlelogboeken waarin activiteiten van bevoegde gebruikers, geautoriseerde en niet-geautoriseerde pogingen om toegang te krijgen, systeemuitzonderingen en informatiebeveiligingsgebeurtenissen worden geregistreerd, worden slechts een bepaalde tijd bewaard. Hallo retentie van uw logboeken is naar eigen inzicht omdat u logboekgegevens verzameld en eigen vereisten voor de bewaarperiode tooyour configureren.

### <a name="how-azure-implements-logging-and-monitoring"></a>De implementatie van logboekregistratie en bewaking in Azure
Azure implementeert Management Agents (MA) en Azure Security Monitor (ASM) agents tooeach compute-, opslag- of fabric-knooppunt onder beheer, ongeacht of deze systeemeigen of virtual. Elke Management Agent is geconfigureerde tooauthenticate tooa service team storage-account met een certificaat verkregen uit Azure Hallo-certificaatarchief en voorwaarts vooraf geconfigureerde diagnostische en event gegevens toohello storage-account. Deze agenten zijn niet geïmplementeerd toocustomers virtuele machines.

Beheerders van Azure toegang tot logboeken via een webportal voor geverifieerde en beheerde toegang toohello Logboeken. Een beheerder kan logboeken parseren, filteren, vergelijken en analyseren. Hello Azure service team storage-accounts voor logboeken zijn beveiligd tegen direct beheerder toegang toohelp voorkomen dat tegen knoeien logboek.

Microsoft verzamelt logboeken van netwerkapparaten met Hallo Syslog-protocol en van de host-servers met behulp van Microsoft Audit Collection Services (ACS). Deze logboeken worden geplaatst in een logboekdatabase waarin waarschuwingen naar verdachte gebeurtenissen worden gegenereerd. Hallo beheerder kan bekijken en analyseren van deze logboeken.

[Azure Diagnostics](https://msdn.microsoft.com/library/azure/gg433048.aspx) is een functie van Azure waarmee u toocollect diagnostische gegevens van een toepassing in Azure wordt uitgevoerd. Dit zijn diagnostische gegevens voor foutopsporing en het oplossen van problemen, meten van de prestaties, Resourcegebruik, analyse van het netwerkverkeer, capaciteitsplanning bewaking en controle. Nadat het Hallo diagnostische gegevens worden verzameld, kan het zijn overgedragen tooan Azure storage-account voor persistentie. Overdrachten kunnen ofwel worden gepland of op aanvraag.

## <a name="threat-mitigation"></a>Threat risicobeperking
Azure maakt gebruik van een aantal threat risicobeperking mechanismen en processen tooprotect infrastructuur en services in toevoeging tooisolation, versleuteling en filteren. Deze interne controles en technologieën toodetect en geavanceerde bedreigingen zoals DDoS, uitbreiding van bevoegdheden en Hallo herstellen [OWASP Top 10](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project).

Microsoft heeft in place toosecure verminderen van de cloudinfrastructuur Hallo beveiligingsmechanismen en risicobeheer Hallo risico op beveiligingsincidenten. In Hallo voordoet gebeurtenis een incident, Hallo Security Incident Management (SIM) team in het Microsoft-Services voor Online beveiliging en naleving (OSSC) team Hallo is gereed toorespond op elk gewenst moment.

### <a name="how-azure-implements-threat-mitigation"></a>De implementatie van risicobeperking in Azure
Azure heeft beveiligingsmechanismen in place tooimplement threat risicobeperking en ook toohelp klanten potentiële bedreigingen in hun omgeving te verhelpen. Hallo volgt een overzicht Hallo threat risicobeperking mogelijkheden die worden aangeboden door Azure:

* [Azure Antimalware](azure-security-antimalware.md) is standaard ingeschakeld op alle infrastructuurservers. U kunt deze desgewenst inschakelen in uw eigen virtuele machines.
* Microsoft onderhoudt doorlopende bewaking tussen servers, netwerken en toepassingen toodetect bedreigingen en aanvallen te voorkomen. Geautomatiseerde waarschuwingen melden beheerders van afwijkend gedrag, zodat ze tootake corrigerende maatregelen op interne en externe bedreigingen.
* U kunt oplossingen van derden implementeren binnen uw abonnementen, zoals web application firewalls van [Barracuda](https://techlib.barracuda.com/ng54/deployonazure).
* Microsoft benadering toopenetration test '[rood teams](http://download.microsoft.com/download/C/1/9/C1990DBA-502F-4C2A-848D-392B93D9B9C3/Microsoft_Enterprise_Cloud_Red_Teaming.pdf), ' die betrekking heeft op de medewerkers van Microsoft security is een aanval op (niet-klant) live productiesystemen van Azure tootest beveiliging tegen echte, geavanceerde , permanente bedreigingen.
* Geïntegreerde implementatie systemen beheren Hallo distributie en de installatie van beveiligingspatches in hello Azure-platform.

## <a name="next-steps"></a>Volgende stappen
[Vertrouwenscentrum van Azure](https://azure.microsoft.com/support/trust-center/)

[Blog van het Azure-beveiligingsteam](http://blogs.msdn.com/b/azuresecurity/)

[Microsoft Security Response Center](https://technet.microsoft.com/library/dn440717.aspx)

[Active Directory-blog](http://blogs.technet.com/b/ad/)
