---
title: aaaGuidelines voor implementatie van Windows Server Active Directory op Azure Virtual Machines | Microsoft Docs
description: Als u weet hoe toodeploy AD Domain Services en AD Federation Services on-premises, meer informatie over hoe deze werken op virtuele machines in Azure.
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
ms.assetid: 04df4c46-e6b6-4754-960a-57b823d617fa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/26/2017
ms.author: femila
ms.openlocfilehash: 9ad5a5f138a6402cbb656d9160545846051207b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="guidelines-for-deploying-windows-server-active-directory-on-azure-virtual-machines"></a>Richtlijnen voor het implementeren van Windows Server Active Directory op virtuele machines in Azure
Dit artikel wordt uitgelegd Hallo belangrijke verschillen tussen implementatie Windows Server Active Directory Domain Services (AD DS) en Active Directory Federation Services (AD FS) lokale versus implementeren op Microsoft Azure virtuele machines.

## <a name="scope-and-audience"></a>Bereik en doelgroep
Hallo artikel is bedoeld voor die al bij de implementatie van Active Directory lokaal heeft ondergaan. Er wordt aangegeven Hallo verschillen tussen Active Directory implementeren op Microsoft Azure virtuele machines/Azure virtual networks en traditionele on-premises Active Directory-implementaties. Azure virtuele machines en virtuele netwerken van Azure uitmaken deel van een infrastructuur-as-a-Service (IaaS) bieden voor organisaties tooleverage computerbronnen in Hallo cloud.

Zie die u niet bekend met de implementatie van AD bent, Hallo [Implementatiehandleiding voor AD DS](https://technet.microsoft.com/library/cc753963) of [uw AD FS-implementatie plannen](https://technet.microsoft.com/library/dn151324.aspx) zo nodig.

In dit artikel wordt ervan uitgegaan dat Hallo lezer bekend bent met de volgende concepten Hallo:

* Windows Server AD DS-implementatie en beheer
* Implementatie en configuratie van DNS-toosupport een Windows Server AD DS-infrastructuur
* Windows Server AD FS-implementatie en beheer
* Implementeren, configureren en beheren van relying party-toepassingen (websites en web services) die Windows Server AD FS-tokens kunnen worden gebruikt.
* Concepten van algemene virtuele machine, zoals hoe tooconfigure een virtuele machine, virtuele schijven en virtuele netwerken

In dit artikel licht Hallo-vereisten voor een hybride implementatiescenario waarin Windows Server AD DS of AD FS gedeeltelijk geïmplementeerde on-premises en gedeeltelijk geïmplementeerd op virtuele machines in Azure. Hallo-document bevat eerst Hallo kritieke verschillen tussen het uitvoeren van Windows Server AD DS en AD FS op Azure virtuele machines versus on-premises en belangrijke beslispunten die invloed hebben op het ontwerp en implementatie. Hallo rest Hallo papier wordt richtlijnen voor elk Hallo beslispunten in meer detail en hoe tooapply Hallo richtlijnen toovarious implementatiescenario's.

In dit artikel wordt niet beschreven configuratie Hallo van [Azure Active Directory](http://azure.microsoft.com/services/active-directory/), dit is een op REST gebaseerde service die mogelijkheden voor beheer en toegang beheren voor cloud-toepassingen biedt. Azure Active Directory (Azure AD) en Windows Server AD DS zijn echter ontworpen toowork samen tooprovide een oplossing voor identiteits- en toegangsbeheer voor vandaag hybride IT-omgevingen en moderne toepassingen. toohelp begrijpen Hallo verschillen en relaties tussen Windows Server AD DS en Azure AD, houd rekening met de volgende Hallo:

1. U kunt tegenkomen Windows Server AD DS in Hallo cloud op Azure virtuele machines wanneer u Azure tooextend met uw on-premises datacentrum Hallo cloud.
2. U kunt Azure AD-toogive gebruiken uw gebruikers eenmalige aanmelding tooSoftware-as-a-Service (SaaS)-toepassingen. Microsoft Office 365 maakt gebruik van deze technologie bijvoorbeeld en toepassingen die worden uitgevoerd op Azure of andere cloudplatforms kunnen ook worden gebruikt.
3. U kunt Azure AD (de Access Control Service) toolet gebruikers aanmelden via identiteiten van Facebook, Google, Microsoft en andere id-providers tooapplications die worden gehost in Hallo cloud of on-premises gebruiken.

Zie voor meer informatie over deze verschillen, [Azure Identity](fundamentals-identity.md).

## <a name="related-resources"></a>Gerelateerde resources
U kunt downloaden en uitvoeren Hallo [Azure virtuele Machine Readiness Assessment](https://www.microsoft.com/download/details.aspx?id=40898). Hallo assessment automatisch inspecteren van uw on-premises omgeving en genereren van een aangepast rapport op basis van Hallo richtlijnen gevonden in dit onderwerp toohelp u Hallo omgeving tooAzure migreren.

We raden u ook eerst Hallo zelfstudies en handleidingen video's die betrekking hebben op Hallo volgende onderwerpen:

* [Een virtueel netwerk Cloud-Only in hello Azure-Portal configureren](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)
* [Een Site-naar-Site-VPN configureren in hello Azure Portal](../vpn-gateway/vpn-gateway-site-to-site-create.md)
* [Een nieuw Active Directory-forest installeren op een virtuele Azure-netwerk](active-directory-new-forest-virtual-machine.md)
* [Een replica Active Directory-domeincontroller installeren in Azure](active-directory-install-replica-active-directory-domain-controller.md)
* [Microsoft Azure IT Pro IaaS: grondbeginselen (01) virtuele Machine](https://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/01)
* [Microsoft Azure IT Pro IaaS: (05) maken van virtuele netwerken en Cross-Premises connectiviteit](https://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/05)

## <a name="introduction"></a>Inleiding
Hallo fundamentele vereisten voor het implementeren van Windows Server Active Directory op Azure virtuele machines verschillen weinig van deze is geïmplementeerd in on-premises virtuele machines (en toosome mate, fysieke machines). Bijvoorbeeld in Hallo geval van Windows Server AD DS, als Hallo domeincontrollers (DC's) die u op virtuele machines in Azure implementeert replica's in een bestaand zijn lokaal zakelijke domein/forest, en vervolgens hello Azure-implementatie kan grotendeels worden behandeld in Hallo dezelfde manier als u mogelijk moet u een andere aanvullende Windows Server Active Directory-site behandelen. Dat wil zeggen, subnetten moeten worden gedefinieerd in Windows Server AD DS, een site die is gemaakt, Hallo subnetten toothat site gekoppeld en verbonden met de juiste sitekoppelingen tooother-sites. Er zijn echter enkele verschillen die algemene tooall Azure-implementaties en sommige die variëren volgens specifieke toohello implementatiescenario. Twee fundamentele verschillen worden hieronder beschreven:

### <a name="azure-virtual-machines-may-need-connectivity-toohello-on-premises-corporate-network"></a>Virtuele machines in Azure moet connectiviteit toohello on-premises zakelijke netwerk mogelijk.
Verbinding maken met virtuele machines in Azure back tooan lokale bedrijfsnetwerk virtuele Azure-netwerk, waaronder een site-naar-site of site-naar-punt virtueel particulier netwerk (VPN) vereist onderdeel kunnen tooseamlessly verbinding virtuele machines in Azure en een on-premises machines. Dit VPN-onderdeel kan ook inschakelen op het lokale domein lid computers tooaccess een Windows Server Active Directory-domein waarvan domeincontrollers uitsluitend op virtuele machines in Azure worden gehost. Het echter belangrijk toonote is, dat als hello VPN mislukt, verificatie en andere bewerkingen die afhankelijk van Windows Server Active Directory zijn ook mislukt. Terwijl gebruikers mogelijk kunnen toosign bij het gebruik van bestaande referenties in in de cache, alle peer-to-peer of client-naar-server verificatiepogingen voor welke tickets nog toobe uitgegeven of verouderd zijn mislukt.

Zie [virtueel netwerk](http://azure.microsoft.com/documentation/services/virtual-network/) voor een demonstratie van video- en een lijst met zelfstudies met stapsgewijze instructies, inclusief [een Site-naar-Site-VPN configureren in Azure-portal Hallo](../vpn-gateway/vpn-gateway-site-to-site-create.md).

> [!NOTE]
> U kunt ook Windows Server Active Directory implementeren op een Azure-netwerk dat geen verbinding maken met een on-premises netwerk. Hallo richtlijnen in dit onderwerp wordt echter ervan uitgegaan dat een virtuele Azure-netwerk wordt gebruikt, omdat dit IP-adressen van de mogelijkheden die essentieel tooWindows Server zijn biedt.
> 
> 

### <a name="static-ip-addresses-must-be-configured-with-azure-powershell"></a>Statische IP-adressen moeten worden geconfigureerd met Azure PowerShell.
Dynamische adressen worden standaard toegewezen, maar in plaats daarvan Hallo Set AzureStaticVNetIP cmdlet tooassign een statisch IP-adres gebruiken. Die Hiermee stelt u een statisch IP-adres dat via de service herstel- en uitschakelen/opnieuw opstarten van de virtuele machine actief blijft. Zie voor meer informatie [statische interne IP-adres voor virtuele machines](http://azure.microsoft.com/blog/static-internal-ip-address-for-virtual-machines/).

## <a name="BKMK_Glossary"></a>Termen en definities
Hallo volgende is een niet-uitputtende lijst met voorwaarden voor verschillende Azure-technologieën die in dit artikel wordt verwezen.

* **Virtuele machines in Azure**: Hallo IaaS-aanbod in Azure die klanten kan toodeploy virtuele machines met vrijwel elke oudsher lokale serverwerkbelasting.
* **Virtuele Azure-netwerk**: Hallo networking-service in Azure waarmee klanten maken en beheren van virtuele netwerken in Azure en koppel deze veilig tootheir eigen on-premises netwerken infrastructuur met behulp van een virtueel particulier netwerk (VPN).
* **Virtueel IP-adres**: een internetgerichte IP-adres is niet gebonden tooa specifieke computer of het netwerk netwerkinterfacekaart. Cloud-services zijn een virtueel IP-adres voor het ontvangen netwerkverkeer dat omgeleide tooan Azure VM is toegewezen. Een virtueel IP-adres is een eigenschap van een cloudservice die een of meer virtuele machines van Azure kan bevatten. Let ook op dat een virtuele Azure-netwerk een of meer cloud-services kan bevatten. Virtuele IP-adressen bieden mogelijkheden voor native-taakverdeling.
* **Dynamische IP-adres**: dit is Hallo IP-adres dat is alleen voor intern gebruik. Deze moet worden geconfigureerd als een statisch IP-adres (via de cmdlet Set-AzureStaticVNetIP Hallo) voor virtuele machines die Hallo domeincontroller en DNS-serverfuncties hosten.
* **Service herstel**: waarin Azure automatisch een tooa service actief status opnieuw retourneert na het detecteren van die service Hallo Hallo-proces is mislukt. Herstel-service is een van de aspecten Hallo van Azure die ondersteuning biedt voor beschikbaarheid en robuustheid van. Tijdens het onwaarschijnlijk, Hallo resultaat na een service incident herstel voor een domeincontroller die wordt uitgevoerd op een virtuele machine is vergelijkbaar tooan niet-geplande opnieuw wordt opgestart, maar heeft enkele bijwerkingen:
  
  * Hallo virtuele netwerkadapter in Hallo VM wordt gewijzigd.
  * Hallo MAC-adres van de virtuele netwerkadapter hello wordt gewijzigd.
  * Hallo Processor/CPU-ID van Hallo VM wordt gewijzigd.
  * Hallo wordt-IP-configuratie van de virtuele netwerkadapter Hallo niet gewijzigd zolang Hallo VM aangesloten tooa virtueel netwerk is en hello van de virtuele machine IP-adres statisch is.
  
  Geen van deze problemen van invloed zijn op Windows Server Active Directory omdat er geen afhankelijkheid van Hallo MAC-adres of de Processor/CPU-ID en alle Windows Server Active Directory-implementaties in Azure worden aanbevolen toobe uitvoeren op een virtuele Azure-netwerk, zoals hierboven wordt beschreven .

## <a name="is-it-safe-toovirtualize-windows-server-active-directory-domain-controllers"></a>Is het veilig toovirtualize Windows Server Active Directory-domeincontrollers?
Implementatie van Windows Server Active Directory-DC's op virtuele machines in Azure is onderwerp toohello dezelfde richtlijnen DC's lokaal uitgevoerd op een virtuele machine. Gevirtualiseerde DC's wordt uitgevoerd, is een veilige procedure als richtlijnen gegeven voor een back-up en herstellen van DC's worden gevolgd. Zie voor meer informatie over de beperkingen en richtlijnen voor het uitvoeren van gevirtualiseerde DC's, [Running Domain Controllers in Hyper-V](https://technet.microsoft.com/library/dd363553).

Geef op hypervisors of trivialize technologieën die kunnen problemen veroorzaken voor veel gedistribueerde systemen, met inbegrip van Windows Server Active Directory. Bijvoorbeeld, op een fysieke server, kunt u een schijf klonen of niet-ondersteunde methoden tooroll back Hallo status van een server, inclusief het gebruik van SAN's, enzovoort, maar dat op een fysieke server doet is veel moeilijker dan het terugzetten van een momentopname van de virtuele machine in een hypervisor. Azure biedt functionaliteit die tot Hallo dezelfde leiden kan ongewenste voorwaarde. Bijvoorbeeld, moet u VHD-bestanden van DC's niet kopiëren in plaats van het uitvoeren van regelmatige back-ups, omdat deze terug te zetten in een dergelijke situatie toousing momentopname terugzetten onderdelen resulteren kan.

Dergelijke Rollback introduceren USN-bellen die toopermanently uiteenlopende statussen tussen DC's kunnen leiden. Die de oorzaak van problemen, zoals:

* Achtergebleven objecten
* Inconsistente wachtwoorden
* Inconsistente kenmerkwaarden
* Schema komt niet overeen met als Hallo schema-master wordt teruggedraaid

Zie voor meer informatie over hoe de DC's worden beïnvloed, [USN and USN Rollback](https://technet.microsoft.com/library/virtual_active_directory_domain_controller_virtualization_hyperv.aspx#usn_and_usn_rollback).

Vanaf Windows Server 2012 [extra beveiliging zijn ingebouwd in tooAD DS](https://technet.microsoft.com/library/hh831734.aspx). Met deze beveiligingen te helpen beveiligen van gevirtualiseerde domeincontrollers op basis van de hiervoor genoemde problemen hello, zolang het onderliggende hypervisorplatform Hallo VM-GenerationID ondersteunt. Azure ondersteunt VM-GenerationID, wat betekent dat domeincontrollers met Windows Server 2012 of later op Azure virtual machines Hallo extra beveiliging.

> [!NOTE]
> U moet afsluiten en opnieuw opstarten van een virtuele machine die rol domeincontroller Hallo in Azure wordt uitgevoerd binnen het gastbesturingssysteem in plaats van Hallo Hallo **afsluiten** optie in hello Azure Portal. Met behulp van de portal tooshut Hallo omlaag een virtuele machine wordt vandaag de dag Hallo VM toobe toewijzing ongedaan gemaakt. Een toewijzing ongedaan is gemaakt VM heeft Hallo voordeel niet steeds kosten, maar ook worden opnieuw ingesteld Hallo VM-GenerationID die ongewenste voor een domeincontroller is. Wanneer Hallo generatie-id opnieuw wordt ingesteld, Hallo invocationID van Hallo AD DS-database ook opnieuw ingesteld, Hallo RID-groep is verwijderd en SYSVOL is gemarkeerd als niet-bindende. Zie voor meer informatie [inleiding tooActive Directory Domain Services (AD DS) Virtualization](https://technet.microsoft.com/library/hh831734.aspx) en [Safely Virtualizing DFSR](http://blogs.technet.com/b/filecab/archive/2013/04/05/safely-virtualizing-dfsr.aspx).
> 
> 

## <a name="why-deploy-windows-server-ad-ds-on-azure-virtual-machines"></a>Waarom Windows Server AD DS op Azure Virtual Machines implementeren?
Er zijn veel scenario's voor Windows Server AD DS-implementatie geschikt zijn voor de implementatie als virtuele machines in Azure. Stel dat u hebt een bedrijf in Europa die tooauthenticate gebruikers in een externe locatie in Azië behoeften. Hallo bedrijf heeft niet eerder hebt geïmplementeerd Windows Server Active Directory-DC's in Azië vanwege toohello kosten toodeploy ze en beperkte expertise toomanage Hallo servers na de implementatie. Hierdoor kunnen worden verificatieaanvragen van Azië afgehandeld door de DC's in Europa met suboptimale resultaten. In dit geval kunt u een domeincontroller op een virtuele machine die u hebt opgegeven moet worden uitgevoerd binnen hello Azure-datacenter in Azië implementeren. Koppelen van die DC tooan Azure-netwerk dat is verbonden, direct toohello externe locatie, worden de verificatieprestaties.

Azure is ook geschikt als een vervangende toootherwise kostbare disaster recovery (DR) sites. Hallo relatief lage kosten voor het hosten van een klein aantal domeincontrollers en één virtueel netwerk in Azure vertegenwoordigt een aantrekkelijk alternatief.

Ten slotte kunt u toodeploy een netwerktoepassing in Azure, zoals SharePoint, die Windows Server Active Directory is vereist, maar heeft geen afhankelijkheid op Hallo on-premises netwerk of Hallo zakelijke Windows Server Active Directory. In dit geval implementatie van een geïsoleerd forest op Azure toomeet Hallo SharePoint vereisten van de server is optimaal. Opnieuw wordt implementeren van netwerktoepassingen die vereisen connectiviteit toohello on-premises netwerk en Hallo zakelijk Active Directory ook ondersteund.

> [!NOTE]
> Aangezien een layer 3-verbinding biedt, Hallo VPN-onderdeel waarmee de verbinding tussen een Azure-netwerk en een on-premises netwerk kunt lidservers met lokale tooleverage DC's die worden uitgevoerd als Azure virtuele machines in Azure ook inschakelen virtueel netwerk. Maar als Hallo VPN niet beschikbaar is, communicatie tussen on-premises computers en domeincontrollers op basis van Azure werkt niet, wat leidt tot verificatie en verschillende andere fouten.  
> 
> 

## <a name="contrasts-between-deploying-windows-server-active-directory-domain-controllers-on-azure-virtual-machines-versus-on-premises"></a>Anders dan tussen het implementeren van Windows Server Active Directory-domeincontrollers op Azure Virtual Machines tegenover on-premises
* Voor elk scenario Windows Server Active Directory dat meer dan één VM bevat, is het nodig toouse virtueel netwerk van Azure consistentie van IP-adres. Houd er rekening mee dat deze handleiding wordt aangenomen dat de DC's worden uitgevoerd op een virtuele Azure-netwerk.
* Net als bij lokale DC's, worden statische IP-adressen aanbevolen. Een statisch IP-adres kan alleen worden geconfigureerd met behulp van Azure PowerShell. Zie [statische interne IP-adres voor virtuele machines](http://azure.microsoft.com/blog/static-internal-ip-address-for-virtual-machines/) voor meer informatie. Als u het bewaken van systemen of andere oplossingen die voor statische IP-adresconfiguratie in het gastbesturingssysteem Hallo controleren hebt, kunt u hetzelfde statische IP-adres toohello eigenschappen van netwerkadapter Hallo VM Hallo toewijzen. Maar houd er rekening mee dat Hallo-netwerkadapter worden genegeerd als hello VM ondergaat herstel van de service of wordt afgesloten in Hallo-portal en heeft het adres de toewijzing ongedaan gemaakt. In dat geval moet statisch IP-adres in de Gast Hallo Hallo toobe opnieuw instellen.
* Implementeren van virtuele machines op een virtueel netwerk niet impliceren (of vereisen) connectiviteit back tooan on-premises netwerk; Hallo virtueel netwerk kunt alleen deze mogelijkheid. U moet een virtueel netwerk voor persoonlijke communicatie tussen Azure en uw on-premises netwerk maken. U moet toodeploy een VPN-eindpunt op Hallo on-premises netwerk. Hallo VPN wordt geopend vanuit Azure toohello on-premises netwerk. Zie voor meer informatie [Virtual Network-overzicht](../virtual-network/virtual-networks-overview.md) en [een Site-naar-Site-VPN configureren in Azure Portal Hallo](../vpn-gateway/vpn-gateway-site-to-site-create.md).

> [!NOTE]
> Een optie te[maken van een punt-naar-site VPN](../vpn-gateway/vpn-gateway-point-to-site-create.md) is beschikbaar tooconnect afzonderlijke op Windows gebaseerde computers rechtstreeks tooan virtuele Azure-netwerk.
> 
> 

* Ongeacht of u een virtueel netwerk of niet, Azure kosten voor uitgaande verkeer, maar niet inkomend. Verschillende ontwerpkeuzen van Windows Server Active Directory kunnen invloed hebben op hoeveel uitgaande verkeer wordt gegenereerd door een implementatie. Bijvoorbeeld, beperkt het implementeren van een alleen-lezen domeincontroller (RODC) uitgaande verkeer omdat deze wordt niet gerepliceerd uitgaand. Maar Hallo besluit toodeploy een RODC moet toobe afgewogen tegen Hallo nodig tooperform schrijfbewerkingen tegen Hallo DC en Hallo [compatibiliteit](https://technet.microsoft.com/library/cc755190) toepassingen en services op Hallo site met de RODC's hebben. Zie voor meer informatie over kosten voor verkeer [Azure prijzen op overzichtelijke](http://azure.microsoft.com/pricing/).
* Terwijl u volledige controle over welke toouse server bronnen voor virtuele machines on-premises, zoals het RAM-geheugen, schijfruimte, enzovoort, zijn op Azure moet u uit een lijst met vooraf geconfigureerde server grootten. Voor een domeincontroller wordt een gegevensschijf nodig in toevoeging toohello besturingssysteemschijf in volgorde toostore Hallo Windows Server Active Directory-database.

## <a name="can-you-deploy-windows-server-ad-fs-on-azure-virtual-machines"></a>Kunt u Windows Server AD FS op virtuele machines in Azure implementeren?
Ja, u kunt Windows Server AD FS op virtuele machines in Azure implementeren en Hallo [best practices voor AD FS-implementatie](https://technet.microsoft.com/library/dn151324.aspx) lokale gelden voor zowel tooAD FS-implementatie in Azure. Maar Hallo best practices, zoals taakverdeling en hoge beschikbaarheid technologieën afgezien van wat AD FS biedt zelf nodig hebt. Ze moeten door de onderliggende infrastructuur Hallo worden geleverd. Laten we Bekijk deze best practices en hoe ze met behulp van Azure VM's en een Azure-netwerk kunnen worden bereikt.

1. **Nooit beschikbaar security token service (STS) servers rechtstreeks toohello Internet.**
   
    Dit is belangrijk omdat Hallo STS beveiligingstokens verstrekt. Als gevolg hiervan STS-servers, zoals AD FS-servers moeten worden behandeld met Hallo hetzelfde niveau van bescherming als een domeincontroller. Als een STS is geknoeid, hebben kwaadwillende gebruikers Hallo mogelijkheid tooissue toegangstokens mogelijk met claims van hun kiezen toorelying of toepassingen van derden en andere servers STS in vertrouwende organisaties.
2. **Active Directory-domeincontrollers voor alle gebruikersdomeinen in Hallo netwerk als Hallo AD FS-servers implementeren.**
   
    AD FS-servers gebruiken tooauthenticate gebruikers van Active Directory Domain Services. Het verdient aanbeveling toodeploy domeincontrollers op Hallo netwerk als Hallo AD FS-servers. Dit biedt bedrijfscontinuïteit geval Hallo koppeling tussen hello Azure-netwerk en uw on-premises netwerk is verbroken en lagere latentie en verbeterde prestaties voor aanmeldingen maakt.
3. **Meerdere AD FS-knooppunten voor hoge beschikbaarheid en taakverdeling Hallo implementeren.**
   
    In de meeste gevallen is Hallo falen van een toepassing waarmee AD FS onaanvaardbaar omdat Hallo-toepassingen waarvoor beveiligingstokens zijn vaak bedrijfskritieke. Als gevolg hiervan en omdat AD FS bevindt zich nu in Hallo kritieke pad tooaccessing bedrijfskritieke toepassingen, Hallo AD FS-service moet maximaal beschikbaar is via meerdere AD FS-proxy's en AD FS-servers. tooachieve distributie van aanvragen, netwerktaakverdelers worden doorgaans geïmplementeerd voor zowel Hallo AD FS-proxy's en Hallo AD FS-servers.
4. **Implementeer een of meer Web Application Proxy knooppunten voor toegang tot internet.**
   
    Wanneer gebruikers moeten tooaccess toepassingen die zijn beveiligd door Hallo AD FS-service, Hallo Hallo AD FS-service moet toobe beschikbaar is via internet. Dit wordt bereikt door het implementeren van Hallo Web Application Proxy-service. Het is raadzaam toodeploy meer dan één knooppunt voor de toepassing hello van hoge beschikbaarheid en taakverdeling.
5. **De toegang beperken Hallo Web Application Proxy knooppunten toointernal-netwerkbronnen.**
   
    tooallow externe gebruikers tooaccess AD FS van Hallo internet, moet u toodeploy Web Application Proxy knooppunten (of AD FS-Proxy in eerdere versies van Windows Server). Hallo Web Application proxy knooppunten rechtstreeks zijn blootgesteld toohello Internet. Ze zijn niet vereist toobe domein en ze alleen moeten toegang hebben tot toohello AD FS-servers via TCP-poorten 443 en 80. Het is raadzaam dat communicatie tooall andere computers (met name domeincontrollers) is geblokkeerd.
   
    Dit is doorgaans bereikte lokale middels een DMZ genoemd. Firewalls gebruikt een goedgekeurde bewerking toorestrict verkeer van Hallo DMZ toohello on-premises netwerk (dat wil zeggen, alleen het verkeer van Hallo IP-adressen opgegeven en via poorten is toegestaan en alle andere verkeer wordt geblokkeerd).

Hallo volgende diagram toont een traditionele lokale AD FS-implementatie.

![Diagram van een implementatie van traditionele on-premises Active Directory Federation Services](media/active-directory-deploying-ws-ad-guidelines/ADFS_onprem.png)

Omdat Azure geen native, uitgebreide firewall mogelijkheid biedt, moeten andere opties gebruikt toobe toorestrict verkeer. Hallo volgende tabel ziet u elke optie en voordelen en nadelen.

| Optie | Gebruik | Nadeel |
| --- | --- | --- |
| [Azure-netwerk-ACL 's](../virtual-network/virtual-networks-acl.md) |Minder dure en eenvoudigere beginconfiguratie |Extra netwerk ACL-configuratie vereist als er nieuwe VM's toohello implementatie worden toegevoegd |
| [Barracuda NG firewall](https://www.barracuda.com/products/ngfirewall) |Geaccepteerde modus van bewerking en vereist geen ACL-netwerkconfiguratie |Hogere kosten en complexiteit voor de eerste installatie |

Hallo stappen op hoog niveau toodeploy AD FS zijn in dit geval als volgt:

1. Maak een virtueel netwerk met cross-premises-connectiviteit met behulp van een VPN of [ExpressRoute](http://azure.microsoft.com/services/expressroute/).
2. Implementeer domeincontrollers op Hallo virtueel netwerk. Deze stap is optioneel maar aanbevolen.
3. AD FS-servers op het virtuele netwerk Hallo domein implementeren.
4. Maak een [interne load set met gelijke taakverdeling](http://azure.microsoft.com/blog/internal-load-balancing/) bevat Hallo AD FS-servers en maakt gebruik van een nieuwe persoonlijke IP-adres binnen Hallo virtueel netwerk (dynamische IP-adres).
   
   1. Toocreate hello FQDN toopoint toohello persoonlijke (dynamische) IP-adres van DNS-Hallo interne set met gelijke taakverdeling bijwerken.
5. Maak een cloudservice (of een afzonderlijke virtueel netwerk) voor Hallo Web Application Proxy-knooppunten.
6. Hallo Web Application Proxy knooppunten in de cloudservice hello of een virtueel netwerk implementeren
   
   1. Maak een externe set met gelijke taakverdeling met Hallo Web Application Proxy knooppunten.
   2. Werk Hallo externe DNS-naam (Fully Qualified Domain Name) toopoint toohello cloud service openbare IP-adres (Hallo virtueel IP-adres).
   3. AD FS-proxy's toouse Hallo FQDN-naam die overeenkomt met toohello interne set met gelijke taakverdeling voor Hallo AD FS-servers configureren.
   4. Bijwerken van websites op basis van claims toouse hello externe FQDN-naam voor de claimprovider.
7. Beperk de toegang tussen Web Application Proxy tooany machine in het virtuele netwerk van Hallo AD FS.

toorestrict verkeer, Hallo taakverdeling set voor hello Azure interne load balancer moet toobe geconfigureerd voor alleen verkeer tooTCP poorten 80 en 443 en alle andere verkeer toohello interne dynamische IP-adres van Hallo set met gelijke taakverdeling is verwijderd.

![Diagram van AD FS-netwerk-ACL's met TCP 443 en 80 wordt toegestaan.](media/active-directory-deploying-ws-ad-guidelines/ADFS_ACLs.png)

Verkeer toohello AD FS-servers zou mag alleen door de volgende bronnen Hallo:

* Hello Azure interne load balancer.
* Hallo IP-adres van een beheerder op Hallo on-premises netwerk.

> [!WARNING]
> Hallo ontwerp moet voorkomen dat Web Application Proxy knooppunten eventuele andere virtuele machines in Hallo virtuele Azure-netwerk of locaties op Hallo on-premises netwerk bereikt. Dat kan worden gedaan door firewallregels in Hallo lokale toestel voor Express Route-verbindingen of Hallo VPN-apparaat voor site-naar-site VPN-verbindingen configureren.
> 
> 

Een nadeel toothis-optie is Hallo nodig tooconfigure Hallo netwerk ACL's voor meerdere apparaten, waaronder interne load balancer, Hallo AD FS-servers en andere servers die zijn toegevoegd toohello virtueel netwerk. Als een apparaat wordt toohello implementatie toegevoegd zonder het configureren van netwerk-ACL's toorestrict verkeer tooit, te de volledige implementatie Hallo lopen risico worden. Als Hallo IP-adressen van Hallo Web Application Proxy knooppunten ooit wijzigt, Hallo netwerk ACL's moet opnieuw worden ingesteld (wat betekent dat Hallo proxy's moet geconfigureerde toouse [statische dynamische IP-adressen](http://azure.microsoft.com/blog/static-internal-ip-address-for-virtual-machines/)).

![AD FS in Azure met de netwerk-ACL's.](media/active-directory-deploying-ws-ad-guidelines/ADFS_Azure.png)

Een andere optie is toouse hello [Barracuda NG Firewall](https://www.barracuda.com/products/ngfirewall) toestel toocontrol verkeer tussen AD FS-proxyservers en Hallo AD FS-servers. Deze optie voldoet aan best practices voor beveiliging en hoge beschikbaarheid en vereist minder beheer na de initiële installatie Hallo omdat Hallo Barracuda NG firewallapparaat een lijst met geaccepteerde-modus van beheer van de firewall biedt en kan worden geïnstalleerd rechtstreeks op een virtuele Azure-netwerk. Die elimineert Hallo nodig tooconfigure netwerk ACL's elk gewenst moment die een nieuwe server toohello implementatie wordt toegevoegd. Maar deze optie verhoogt de initiële implementatiecomplexiteit en kosten.

In dit geval worden twee virtuele netwerken geïmplementeerd in plaats van een. We bellen u ze VNet1 en VNet2. VNet1 hello proxy's bevat en VNet2 bevat Hallo STSs en Hallo netwerk verbinding back toohello bedrijfsnetwerk. VNet1 daarom is het fysiek (die mogelijk vrijwel) geïsoleerd van VNet2 en op zijn beurt uit Hallo bedrijfsnetwerk. VNet1 wordt vervolgens tooVNet2 verbonden via een speciale tunneling-technologie bekend als Transport onafhankelijk netwerk architectuur (TINA). Hallo TINA tunnel is aangesloten tooeach van Hallo virtuele netwerken met behulp van een firewall Barracuda NG: één Barracuda op elk van de virtuele netwerken Hallo.  Voor hoge beschikbaarheid, wordt aanbevolen dat u twee barracuda's op elke virtuele netwerk implementeert. een actieve Hallo andere passief. Ze bieden zeer uitgebreide mogelijkheden gebruik waarmee ons toomimic Hallo werking van een DMZ traditionele on-premises in Azure.

![AD FS in Azure met firewall.](media/active-directory-deploying-ws-ad-guidelines/ADFS_Azure_firewall.png)

Zie voor meer informatie [AD FS: uitbreiden van een claimbewuste lokale front-toohello Internet](#BKMK_CloudOnlyFed).

### <a name="an-alternative-tooad-fs-deployment-if-hello-goal-is-office-365-sso-alone"></a>De implementatie van een alternatieve tooAD FS als Hallo doel alleen van Office 365 SSO is
Er is een andere alternatieve toodeploying AD FS helemaal als het doel alleen tooenable aanmeldingspagina voor Office 365 is. In dat geval u kunt gewoon implementeren DirSync met wachtwoord sync on-premises en bereiken dezelfde eindresultaat Hallo met minimale implementatiecomplexiteit, omdat deze benadering geen AD FS of Azure vereist.

Hallo vergelijkt volgende tabel hoe Hallo aanmelden processen werken met en zonder de AD FS implementeren.

| Office 365 eenmalige aanmelding met AD FS en DirSync | Office 365 dezelfde aanmelding met DirSync + Wachtwoordsynchronisatie |
| --- | --- |
| 1. Hallo gebruiker tooa bedrijfsnetwerk aanmeldt en geverifieerde tooWindows Server Active Directory is. |1. Hallo gebruiker tooa bedrijfsnetwerk aanmeldt en geverifieerde tooWindows Server Active Directory is. |
| 2. Hallo gebruiker probeert tooaccess Office 365 (ik ben @contoso.com). |2. Hallo gebruiker probeert tooaccess Office 365 (ik ben @contoso.com). |
| 3. Office 365 wordt omgeleid Hallo gebruiker tooAzure AD. |3. Office 365 wordt omgeleid Hallo gebruiker tooAzure AD. |
| 4. Aangezien Azure AD Hallo-gebruiker kan niet worden geverifieerd en er is een vertrouwensrelatie met AD FS on-premises begrijpt, wordt hij omgeleid Hallo gebruiker tooAD FS. |4. Azure AD kan geen Kerberos-tickets rechtstreeks accepteren en geen vertrouwensrelatie bestaat, dus vraagt deze die gebruiker Hallo referenties invoeren. |
| 5. Hallo gebruiker verzendt een Kerberos-ticket toohello AD FS-STS. |5. Hallo gebruiker invoert Hallo dezelfde on-premises wachtwoord, en Azure AD valideert ze tegen het Hallo-gebruikersnaam en wachtwoord die is gesynchroniseed met DirSync. |
| 6. AD FS transformeert Hallo Kerberos-ticket toohello vereist token indeling/claims en Hallo gebruiker tooAzure AD wordt omgeleid. |6. Azure AD wordt omgeleid Hallo gebruiker tooOffice 365. |
| 7. Hallo gebruiker wordt geverifieerd tooAzure AD (een andere transformatie optreedt). |7. Hallo gebruiker kan zich aanmelden tooOffice 365 en OWA met hello Azure AD-token. |
| 8. Azure AD wordt omgeleid Hallo gebruiker tooOffice 365. | |
| 9. Hallo gebruiker is achtergrond op tooOffice 365 ondertekend. | |

In Office 365 met DirSync Hallo met wachtwoordsynchronisatiescenario (geen AD FS), wordt eenmalige aanmelding vervangen door "dezelfde aanmelding' waar 'dezelfde' betekent dat gebruikers moeten hun referenties opnieuw invoeren dezelfde on-premises bij het openen van Office 365. Opmerking dat deze gegevens kan worden onthouden door van Hallo gebruiker browser toohelp Verminder de verdere aanwijzingen.

### <a name="additional-food-for-thought"></a>Aanvullende voeding for gedachte
* Als u AD FS-proxy op een virtuele machine van Azure implementeert, is de connectiviteit toohello AD FS-servers nodig. Als ze zich on-premises, is het raadzaam dat u gebruikmaken van Hallo site-naar-site VPN-verbindingen geleverd door Hallo virtueel netwerk tooallow Hallo Web Application Proxy knooppunten toocommunicate met hun AD FS-servers.
* Als u een AD FS-server op een virtuele Azure implementeert machine, connectiviteit tooWindows Server Active Directory-domeincontrollers, Kenmerkarchieven, en configuratiedatabases nodig en kan ook een ExpressRoute- of een site-naar-site VPN-verbinding vereist tussen hello Azure virtuele netwerk en Hallo on-premises netwerk.
* Kosten worden toegepast tooall verkeer van virtuele machines in Azure (uitgaande verkeer). Als kosten aangedreven factor hello is, is het raadzaam toodeploy Hallo Web Application Proxy knooppunten op Azure, verlaten Hallo AD FS-servers op de lokale. Als Hallo AD FS-servers zijn geïmplementeerd op virtuele machines in Azure ook, worden extra kosten gemaakte tooauthenticate on-premises gebruikers. Uitgaande verkeer maakt een kosten ongeacht of het doorlopen van Hallo ExpressRoute of Hallo VPN-site-naar-site-verbinding.
* Als u toouse Azure systeemeigen taakverdeling van servers mogelijkheden voor hoge beschikbaarheid van de AD FS-servers besluit, houd er rekening mee dat de taakverdeling biedt voor de tests die status van de gebruikte toodetermine Hallo van Hallo virtuele machines binnen het Hallo-cloudservice zijn. In geval van hello Azure virtual machines (als tegengestelde tooweb of worker-functies), moet een aangepaste test worden gebruikt omdat het Hallo-agent die toohello standaard tests reageert is niet aanwezig op de virtuele machines in Azure. Voor het gemak, kunt u een aangepaste TCP-test: dit is vereist alleen dat een TCP-verbinding (een segment TCP SYN verzonden en gereageerd toowith een segment TCP SYN ACK) status van de virtuele machine is tot stand gebrachte toodetermine. U kunt Hallo aangepaste test toouse alle TCP-poort toowhich die uw virtuele machines actief zijn luistert configureren.

> [!NOTE]
> Virtuele machines die nodig tooexpose Hallo die dezelfde van poorten set direct toohello Internet (zoals poort 80 en 443) niet delen Hallo dezelfde service in de cloud. Het is daarom raadzaam dat u een toegewijde cloud-service maken voor uw Windows Server AD FS-servers in de volgorde tooavoid potentiële overlapt tussen Poortvereisten voor een toepassing en Windows Server AD FS.
> 
> 

## <a name="deployment-scenarios"></a>Implementatiescenario's
Hallo volgende sectie bevat een overzicht van heel gebruikelijk scenario's toodraw aandacht tooimportant overwegingen voor de implementatie die moeten worden gehouden. Elk scenario heeft koppelingen toomore details over Hallo beslissingen en tooconsider factoren.

1. [AD DS: Een AD DS-compatibele toepassing implementeren met geen vereiste voor verbinding met zakelijke netwerken](#BKMK_CloudOnly)
   
    Bijvoorbeeld, wordt een internetgerichte SharePoint-service geïmplementeerd op een virtuele machine van Azure. Hallo-toepassing heeft geen afhankelijkheden op zakelijke netwerkbronnen. Hallo toepassing vereist dat Windows Server AD DS, maar geen vereist Hallo zakelijke Windows Server AD DS.
2. [AD FS: Een claimbewuste lokale front-toohello Internet uitbreiden](#BKMK_CloudOnlyFed)
   
    Bijvoorbeeld, moet een claimbewuste toepassing die is geïmplementeerd op lokale is en die wordt gebruikt door zakelijke gebruikers toobecome toegankelijk is vanaf Internet Hallo. Hallo-toepassing moet toobe toegankelijk is rechtstreeks via Internet Hallo zowel door zakelijke partners gebruik van hun eigen bedrijf identiteiten en bestaande zakelijke gebruikers.
3. [AD DS: Windows Server AD DS-bewuste toepassingen waarvoor verbinding toohello bedrijfsnetwerk distribueren](#BKMK_HybridExt)
   
    Bijvoorbeeld, is een LDAP-bewuste toepassingen die ondersteuning biedt voor geïntegreerde Windows-verificatie en maakt gebruik van Windows Server AD DS als een opslagplaats voor configuratie en gebruikersprofiel gegevens op een virtuele machine van Azure geïmplementeerd. Het is handig voor Hallo toepassing tooleverage Hallo bestaande zakelijke Windows Server AD DS en eenmalige aanmelding bieden. Hallo-toepassing is niet claimbewuste.

### <a name="BKMK_CloudOnly"></a>1. AD DS: Een AD DS-compatibele toepassing implementeren met geen vereiste voor verbinding met zakelijke netwerken
![AD DS-implementatie alleen in de cloud](media/active-directory-deploying-ws-ad-guidelines/ADDS_cloud.png)
**afbeelding 1**

#### <a name="description"></a>Beschrijving
SharePoint is geïmplementeerd op een virtuele machine van Azure en Hallo-toepassing heeft geen afhankelijkheden op zakelijke netwerkbronnen. Hallo toepassing vereist Windows Server AD DS maar *niet* vereisen Hallo zakelijke Windows Server AD DS. Er is geen Kerberos of Federatieve vertrouwensrelaties zijn vereist, omdat gebruikers zelf via de toepassing hello in Hallo Windows Server AD DS-domein dat ook wordt gehost in de cloud Hallo op virtuele machines van Azure ingericht.

#### <a name="scenario-considerations-and-how-technology-areas-apply-toohello-scenario"></a>Scenario overwegingen en hoe technologiegebieden toohello scenario toepassen
* [Netwerktopologie](#BKMK_NetworkTopology): maken van een Azure-netwerk zonder cross-premises-connectiviteit (ook wel bekend als site-naar-site-connectiviteit).
* [DC-implementatieconfiguratie](#BKMK_DeploymentConfig): implementeert een nieuwe domeincontroller in een nieuwe, één domein, Windows Server Active Directory-forest. Dit moet samen met de Hallo Windows DNS-server worden geïmplementeerd.
* [Windows Server Active Directory-site-topologie](#BKMK_ADSiteTopology): gebruik Hallo standaard Windows Server Active Directory-site (alle computers zich in een Default-First-Site-Name).
* [De IP-adressen en DNS-](#BKMK_IPAddressDNS):
  
  * Een statisch IP-adres voor Hallo DC instellen met behulp van Hallo Set AzureStaticVNetIP Azure PowerShell-cmdlet.
  * Installeren en configureren van Windows Server DNS op Hallo domeincontroller (s) in Azure.
  * Eigenschappen van het virtuele netwerk Hallo met Hallo naam en IP-adres van de virtuele machine die als host fungeert voor Hallo DC- en DNS-serverfuncties Hallo configureren.
* [Globale catalogus](#BKMK_GC): hello eerste domeincontroller in het Hallo-forest moet een globale-catalogusserver. Aanvullende DC's moeten ook worden geconfigureerd als GC omdat in een forest één domein Hallo globale catalogus geen extra werk van Hallo DC vereist.
* [Plaatsing van Hallo Windows Server AD DS-database en SYSVOL](#BKMK_PlaceDB): Voeg een gegevens-schijf tooDCs uitgevoerd als Azure virtuele machines in de volgorde toostore Hallo Windows Server Active Directory-database, logboekbestanden en SYSVOL.
* [Back-up en herstel](#BKMK_BUR): bepalen waar u toostore systeemstatusback-ups. Voeg desgewenst een andere gegevens toohello DC VM toostore back-ups schijf toe.

### <a name="BKMK_CloudOnlyFed"></a>2 AD FS: een claimbewuste lokale front-toohello Internet uitbreiden
![Federatie met cross-premises connectiviteit](media/active-directory-deploying-ws-ad-guidelines/Federation_xprem.png)
**afbeelding 2**

#### <a name="description"></a>Beschrijving
Een claimbewuste toepassing die is geïmplementeerd op lokale is en die wordt gebruikt door zakelijke gebruikers behoeften toobecome direct toegankelijk vanaf Internet Hallo. Hallo toepassing fungeert als een web frontend tooa SQL-database waarin gegevens worden opgeslagen. Hallo SQL-servers die worden gebruikt door de toepassing hello staan ook op Hallo bedrijfsnetwerk bevinden. Twee Windows Server AD FS STSs en een load balancer is geïmplementeerde on-premises tooprovide toegang toohello zakelijke gebruikers. Hallo toepassing nu moet toobe bovendien toegankelijk is rechtstreeks via Internet Hallo zowel door zakelijke partners gebruik van hun eigen bedrijf identiteiten en bestaande zakelijke gebruikers.

In een toosimplify inspanning en de implementatie en configuratie moet voldoen aan Hallo van deze nieuwe vereiste, wordt besloten dat twee extra web frontends en twee Windows Server AD FS-proxyservers worden geïnstalleerd op virtuele machines in Azure. Alle vier virtuele machines worden blootgesteld rechtstreeks toohello Internet en de connectiviteit toohello on-premises netwerk met behulp van Azure Virtual Network site-naar-site VPN-functionaliteit worden geleverd.

#### <a name="scenario-considerations-and-how-technology-areas-apply-toohello-scenario"></a>Scenario overwegingen en hoe technologiegebieden toohello scenario toepassen
* [Netwerktopologie](#BKMK_NetworkTopology): maken van een virtuele Azure-netwerk en [cross-premises connectiviteit configureren](../vpn-gateway/vpn-gateway-site-to-site-create.md).
  
  > [!NOTE]
  > Zorg dat hello URL gedefinieerd binnen Hallo certificaatsjabloon en Hallo resulterende certificaten kunnen worden bereikt door Hallo Windows Server AD FS-exemplaren die zijn uitgevoerd op Azure voor elke Hallo Windows Server AD FS-certificaten. Hiervoor moet mogelijk cross-premises connectiviteit tooparts van uw PKI-infrastructuur. Voor bijvoorbeeld als de Hallo CRL-eindpunt is on-premises LDAP en gehoste uitsluitend en cross-premises connectiviteit wordt vereist. Als dit niet het wenselijk is, kan het benodigde toouse certificaten worden uitgegeven door een CA waarvan CRL toegankelijk vanaf Internet Hallo is zijn.
  > 
  > 
* [Configuratie voor cloud-services](#BKMK_CloudSvcConfig): Controleer of u hebt twee cloudservices in volgorde bieden twee taakverdeling virtuele IP-adressen. Hallo eerste service in de cloud van virtuele IP-adres worden gerichte toohello twee Windows Server AD FS-proxy VM's op de poorten 80 en 443. Hallo Windows Server AD FS-proxy die VMS zijn geconfigureerd toopoint toohello IP-adres van Hallo lokale load balancer dat voorzijde's Windows Server AD FS STSs Hallo. Hallo tweede cloudservice van virtuele IP-adres worden gerichte toohello twee virtuele machines opnieuw uit te voeren Hallo web frontend op poort 80 en 443. Configureren van een aangepaste test tooensure Hallo load balancer alleen verkeer toofunctioning Windows Server AD FS proxy- en web frontend virtuele machines wordt verwezen.
* [Configuratie van de Federation-server](#BKMK_FedSrvConfig): configureren van Windows Server AD FS federation-server (STS) toogenerate beveiliging voor Windows Server Active Directory-forest Hallo gemaakt in de cloud Hallo tokens. Federatieve claims provider-vertrouwensrelaties met Hallo verschillende partners die u wenst dat tooaccept identiteiten van ingesteld en relying party-vertrouwensrelaties met Hallo verschillende toepassingen die u wilt dat toogenerate tokens te configureren.
  
    Windows Server AD FS proxy-servers zijn geïmplementeerd in een internetgerichte capaciteit om veiligheidsredenen in de meeste gevallen terwijl de oorspronkelijke Windows Server AD FS federation bestanden geïsoleerd van directe verbinding met Internet blijven. Ongeacht het implementatiescenario, moet u uw cloudservice configureren met een virtueel IP-adres waarmee een openbaar blootgestelde IP-adres en poort die op uw twee exemplaren van Windows Server AD FS-STS of proxy-exemplaren kunnen tooload-saldo.
* [Windows Server AD FS-configuratie voor hoge beschikbaarheid](#BKMK_ADFSHighAvail): het is raadzaam toodeploy een Windows Server AD FS-farm met ten minste twee servers voor failover en taakverdeling. U mogelijk wilt tooconsider Hallo Windows Internal Database (WID) voor Windows Server AD FS-configuratiegegevens met en gebruik van Hallo interne taakverdeling mogelijkheden van Azure toodistribute inkomende aanvragen op Hallo-servers in Hallo-farm.

Zie voor meer informatie, Hallo [Implementatiehandleiding voor AD DS](https://technet.microsoft.com/library/cc753963).

### <a name="BKMK_HybridExt"></a>3. AD DS: Windows Server AD DS-bewuste toepassingen waarvoor verbinding toohello bedrijfsnetwerk distribueren
![Cross-premises AD DS-implementatie](media/active-directory-deploying-ws-ad-guidelines/ADDS_xprem.png)
**afbeelding 3**

#### <a name="description"></a>Beschrijving
Een LDAP-compatibele toepassing wordt geïmplementeerd op een virtuele machine van Azure. Deze ondersteuning biedt voor geïntegreerde Windows-verificatie en Windows Server AD DS gebruikt als een opslagplaats voor configuratie- en gebruikersbestanden profielgegevens. Hallo doel Hallo toepassing tooleverage Hallo bestaande zakelijke Windows Server AD DS en eenmalige aanmelding. Hallo-toepassing is niet claimbewuste. Gebruikers moeten ook tooaccess Hallo toepassing rechtstreeks vanuit Hallo Internet. toooptimize voor prestaties en kosten, wordt besloten dat twee extra domeincontrollers die deel uitmaken van het bedrijfsdomein Hallo naast Hallo-toepassing in Azure worden geïmplementeerd.

#### <a name="scenario-considerations-and-how-technology-areas-apply-toohello-scenario"></a>Scenario overwegingen en hoe technologiegebieden toohello scenario toepassen
* [Netwerktopologie](#BKMK_NetworkTopology): maken van een Azure-netwerk met [cross-premises connectiviteit](../vpn-gateway/vpn-gateway-site-to-site-create.md).
* [Installatiemethode](#BKMK_InstallMethod): replica DC van Hallo bedrijfsdomein Windows Server Active Directory implementeren. Voor een replica van een DC, kunt u Windows Server AD DS installeren op Hallo VM en eventueel gebruik Hallo installeren vanaf medium (IFM) functie tooreduce Hallo hoeveelheid gegevens die moeten worden toobe toohello gerepliceerd nieuwe domeincontroller tijdens de installatie. Zie voor een zelfstudie [een replica Active Directory-domeincontroller installeren in Azure](active-directory-install-replica-active-directory-domain-controller.md). Zelfs als u IFM hebt gebruikt, kan het zijn efficiënter toobuild Hallo virtuele DC on-premises en verplaatsen Hallo volledige virtuele hardeschijf (VHD) toohello in de cloud in plaats van Windows Server AD DS tijdens de installatie te repliceren. Voor de veiligheid, wordt het aanbevolen Hallo VHD uit Hallo on-premises netwerk te verwijderen nadat het gekopieerde tooAzure is.
* [Windows Server Active Directory-site-topologie](#BKMK_ADSiteTopology): Maak een nieuwe Azure site in Active Directory: Sites en Services. Maak een Windows Server Active Directory-subnet-object toorepresent Hallo virtuele Azure-netwerk en Hallo subnet toohello site toe te voegen. Maak een nieuwe sitekoppeling die Hallo nieuwe Azure-site en in welke Hallo VPN-eindpunt virtuele Azure-netwerk bevindt zich in de volgorde toocontrol Hallo-site bevat en optimaliseren van Windows Server Active Directory-verkeer tooand van Azure.
* [De IP-adressen en DNS-](#BKMK_IPAddressDNS):
  
  * Een statisch IP-adres voor Hallo DC instellen met behulp van Hallo Set AzureStaticVNetIP Azure PowerShell-cmdlet.
  * Installeren en configureren van Windows Server DNS op Hallo domeincontroller (s) in Azure.
  * Eigenschappen van het virtuele netwerk Hallo met Hallo naam en IP-adres van de virtuele machine die als host fungeert voor Hallo DC- en DNS-serverfuncties Hallo configureren.
* [Geografisch verspreide DC's](#BKMK_DistributedDCs): indien nodig aanvullende virtuele netwerken configureren. Als uw Active Directory-site-topologie DC's in de locaties die overeenkomen met toodifferent Azure vereist regio's dan u wenst toocreate Active Directory-sites dienovereenkomstig.
* [Alleen-lezen domeincontrollers](#BKMK_RODC): U mogelijk een RODC in hello Azure site implementeert, afhankelijk van uw vereisten voor het uitvoeren van schrijfbewerkingen tegen Hallo DC en Hallo compatibiliteit van toepassingen en services op Hallo-locatie met RODC's. Zie voor meer informatie over toepassingscompatibiliteit Hallo [compatibiliteit gebruikershandleiding voor de toepassing van de domeincontrollers van de alleen-lezen domeincontroller](https://technet.microsoft.com/library/cc755190).
* [Globale catalogus](#BKMK_GC): aangegeven benodigde tooservice aanmeldingsaanvragen in forests met meerdere domeinen zijn. Als u een GC-exemplaar in hello Azure site geen implementeren, kunt u kosten voor uitgaand verkeer, worden als verificatieaanvragen query's aangegeven in andere sites veroorzaken. toominimize die verkeer, kunt u universeel groepslidmaatschap in cache opslaan voor hello Azure site in Active Directory: Sites en Services inschakelen.
  
    Als u een GC-exemplaar implementeert, configureert u sitekoppelingen en sitekoppelingen kosten zodat Hallo GC in hello Azure site wordt niet aanbevolen als een bron-DC door andere aangegeven die tooreplicate moeten dezelfde gedeeltelijke domeinpartities Hallo.
* [Plaatsing van Hallo Windows Server AD DS-database en SYSVOL](#BKMK_PlaceDB): Voeg een gegevens-schijf tooDCs uitgevoerd op Azure VM's in volgorde toostore Hallo Windows Server Active Directory-database, logboekbestanden en SYSVOL.
* [Back-up en herstel](#BKMK_BUR): bepalen waar u toostore systeemstatusback-ups. Voeg desgewenst een andere gegevens toohello DC VM toostore back-ups schijf toe.

## <a name="deployment-decisions-and-factors"></a>Beslissingen voor de implementatie en factoren
Deze tabel bevat een overzicht van Hallo Windows Server Active Directory-technologiegebieden die worden beïnvloed in Hallo voorafgaand aan scenario's en Hallo bijbehorende beslissingen tooconsider, met koppelingen toomore hieronder beschreven. Sommige technologiegebieden mogelijk niet van toepassing tooevery implementatiescenario en sommige technologiegebieden mogelijk meer kritieke tooa implementatiescenario dan andere technologiegebieden.

Bijvoorbeeld, als u een replica van een DC op een virtueel netwerk implementeren en uw forest één domein heeft, kan Kies toodeploy globale-catalogusserver in dat geval niet worden kritieke toohello implementatiescenario omdat eventuele aanvullende replicatie wordt niet gemaakt vereisten. Op Hallo daarentegen als Hallo forest verschillende domeinen heeft en Hallo besluit toodeploy een globale catalogus op een virtueel netwerk kan invloed hebben op de beschikbare bandbreedte, prestaties, verificatie, directory zoekacties, enzovoort.

| Windows Server Active Directory-technologiegebied | Beslissingen | Factoren |
| --- | --- | --- |
| [Netwerktopologie](#BKMK_NetworkTopology) |Een virtueel netwerk maken? |<li>Vereisten tooaccess Corp resources</li> <li>Authentication</li> <li>Accountbeheer</li> |
| [Configuratie van DC-implementatie](#BKMK_DeploymentConfig) |<li>Een afzonderlijk forest zonder eventuele vertrouwensrelaties implementeren?</li> <li>Een nieuw forest met Federatie implementeren?</li> <li>Een nieuw forest met Windows Server Active Directory-forest vertrouwen of Kerberos implementeren?</li> <li>Corp-forest uitbreiden door het implementeren van een replica van een DC?</li> <li>Corp-forest uitbreiden door het implementeren van een nieuw onderliggend domein of een domeinstructuur?</li> |<li>Beveiliging</li> <li>Naleving</li> <li>Kosten</li> <li>Tolerantie en fouttolerantie</li> <li>Toepassingscompatibiliteit</li> |
| [Windows Server Active Directory-site-topologie](#BKMK_ADSiteTopology) |Hoe u subnetten, sites en site-koppelingen configureren met Azure Virtual Network toooptimize verkeer en kosten beperken? |<li>Definities van subnet en een site</li> <li>Site-eigenschappen van koppeling en wijzig melding</li> <li>Compressie van replicatie</li> |
| [IP-adressen en DNS](#BKMK_IPAddressDNS) |Hoe tooconfigure IP-adressen en naamomzetting? |<li>Hallo gebruik Hallo Set AzureStaticVNetIP cmdlet tooassign een statisch IP-adres gebruiken</li> <li>Windows Server DNS-server installeren en configureren van eigenschappen van het virtuele netwerk Hallo met Hallo naam en IP-adres van de virtuele machine die als host fungeert voor Hallo DC- en DNS-serverfuncties Hallo</li> |
| [Geografisch verspreide DC 's](#BKMK_DistributedDCs) |Hoe afzonderlijk tooreplicate tooDCs op virtuele netwerken. |Als uw Active Directory-site-topologie DC's in de locaties die overeenkomt met toodifferent Azure vereist regio's dan u wenst toocreate Active Directory-sites dienovereenkomstig. [Configureren van virtueel netwerk toovirtual network Connectivity](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md) tooreplicate tussen domeincontrollers op afzonderlijke virtuele netwerken. |
| [Alleen-lezen domeincontrollers](#BKMK_RODC) |Alleen-lezen of beschrijfbare domeincontrollers gebruiken? |<li>HBI/PII filterkenmerken</li> <li>Filter geheimen</li> <li>Limiet voor uitgaand verkeer</li> |
| [Globale catalogus](#BKMK_GC) |Globale catalogus installeren? |<li>Voor forest met één domein, moet u alle DC's aangegeven</li> <li>Voor de forest met meerdere domeinen zijn GC vereist voor verificatie</li> |
| [Installatiemethode](#BKMK_InstallMethod) |Hoe tooinstall DC in Azure? |Beide: <li>Installatie van AD DS met Windows PowerShell of Dcpromo</li> <li>Verplaats de VHD van een lokale virtuele domeincontroller</li> |
| [Plaatsing van Hallo Windows Server AD DS-database en SYSVOL](#BKMK_PlaceDB) |Indien toostore Windows Server AD DS-database zich aanmeldt, en SYSVOL? |Dcpromo.exe standaardwaarden wijzigen. Deze kritieke Active Directory-bestanden *moet* in plaats van de schijven van het besturingssysteem die schrijfcache implementeren op Azure gegevensschijven worden geplaatst. |
| [Back-up en herstel](#BKMK_BUR) |Hoe gegevens toosafeguard en herstellen? |Systeem voor systeemstatusback-ups maken |
| [Configuratie van de Federation-server](#BKMK_FedSrvConfig) |<li>Een nieuw forest met Federatie in Hallo cloud implementeren?</li> <li>AD FS on-premises implementeren en een proxy in Hallo cloud beschikbaar?</li> |<li>Beveiliging</li> <li>Naleving</li> <li>Kosten</li> <li>Toegang tooapplications door zakelijke partners</li> |
| [Configuratie voor cloud-services](#BKMK_CloudSvcConfig) |De implementatie van een cloudservice wordt impliciet Hallo van de eerste keer dat u een virtuele machine maken. Moet u de aanvullende cloudservices toodeploy? |<li>Een virtuele machine of virtuele machines vereist rechtstreekse blootstelling toohello Internet?</li> <li> Hallo-service vereist taakverdeling?</li> |
| [Federatieve server-vereisten voor openbare en particuliere IP-adressering (dynamische IP versus virtuele IP)](#BKMK_FedReqVIPDIP) |<li>Heeft Hallo Windows Server AD FS-exemplaar toobe bereikt rechtstreeks vanuit Hallo Internet nodig?</li> <li>Vereist Hallo-toepassing wordt geïmplementeerd in de cloud Hallo eigen internetgerichte IP-adres en poort?</li> |Maak een cloudservice voor elke virtuele IP-adres dat is vereist voor uw implementatie |
| [Windows Server AD FS-configuratie voor hoge beschikbaarheid](#BKMK_ADFSHighAvail) |<li>Het aantal knooppunten in mijn Windows Server AD FS serverfarm?</li> <li>Het aantal knooppunten toodeploy in mijn Windows Server AD FS-farm proxy?</li> |Tolerantie en fouttolerantie |

### <a name="BKMK_NetworkTopology"></a>Netwerktopologie
In de volgorde toomeet Hallo IP-adres consistentie en DNS-vereisten voor Windows Server AD DS, is het nodig toofirst maken een [virtuele Azure-netwerk](../virtual-network/virtual-networks-overview.md) en koppelt u uw virtuele machines tooit. Tijdens het maken, moet u beslissen of toooptionally uitbreiden connectiviteit tooyour lokale zakelijke netwerk, waardoor transparant verbindt Azure virtual machines tooon-premises machines, dit wordt bereikt met traditionele VPN-technologieën en vereist dat een VPN-eindpunt op Hallo rand van het bedrijfsnetwerk Hallo worden blootgesteld. Dat wil zeggen, wordt Hallo VPN gestart van Azure toohello bedrijfsnetwerk, niet andersom.

Houd er rekening mee dat extra kosten worden toegepast wanneer u een virtueel netwerk tooyour on-premises netwerk buiten Hallo standaard kosten die van toepassing zijn tooeach VM uitbreidt. Er zijn in het bijzonder kosten voor CPU-tijd van hello Azure Virtual Network gateway en Hallo uitgaande verkeer dat wordt gegenereerd door elke virtuele machine die met lokale virtuele machines via Hallo VPN communiceert. Zie voor meer informatie over het netwerkverkeer kosten [Azure prijzen op overzichtelijke](http://azure.microsoft.com/pricing/).

### <a name="BKMK_DeploymentConfig"></a>Configuratie van DC-implementatie
Hallo manier configureren van Hallo DC afhankelijk Hallo vereisten voor het Hallo-service dat u wilt toorun op Azure. Bijvoorbeeld, u een nieuw forest is geïsoleerd van uw eigen zakelijke forest kunt implementeren, voor het testen van een bewijs van concept, een nieuwe toepassing of enige andere project voor de korte termijn die directoryservices, maar niet specifiek toegang toointernal bedrijfsbronnen vereist.

Als een voordeel een geïsoleerd forest die DC wordt niet gerepliceerd met lokale DC's, wat resulteert in minder uitgaand netwerkverkeer gegenereerd door Hallo systeem zelf, rechtstreeks de kosten te verlagen. Zie voor meer informatie over het netwerkverkeer kosten [Azure prijzen op overzichtelijke](http://azure.microsoft.com/pricing/).

Stel een ander voorbeeld: u privacy-vereisten voor een service, maar Hallo-service is afhankelijk van toegang tooyour interne Windows Server Active Directory. Als u gegevens voor Hallo-service in de cloud Hallo toohost zijn toegestaan, kunt u een nieuw onderliggend domein kunt implementeren voor de interne forest in Azure. In dit geval kunt u een domeincontroller voor het nieuwe onderliggende domein hello (zonder Hallo globale catalogus in volgorde toohelp adres privacyproblemen) implementeren. Dit scenario, samen met een replica DC-implementatie vereist een virtueel netwerk voor verbinding met uw lokale DC's.

Als u een nieuw forest maakt, kiest u of toouse [Active Directory vertrouwt](https://technet.microsoft.com/library/cc771397) of [Federation-vertrouwensrelaties](https://technet.microsoft.com/library/dd807036). Hallo vereisten bepaald door de compatibiliteit, beveiliging, naleving, kosten en tolerantie kan worden verdeeld. Bijvoorbeeld: tootake profiteren van [selectieve verificatie](https://technet.microsoft.com/library/cc755844) u bijvoorbeeld toodeploy kiest u een nieuw forest in Azure, maakt u een Windows Server Active Directory-vertrouwensrelatie tussen Hallo lokale forest en Hallo cloud forest. Als de toepassing hello claimbewuste, u echter mogelijk implementeren federation-vertrouwensrelaties in plaats van Active Directory-forest-vertrouwensrelaties. Een andere factor worden Hallo kostengegevens tooeither repliceren meer door uw on-premises Windows Server Active Directory toohello cloud uitbreiden of meer uitgaande netwerkverkeer als gevolg van verificatie en querybelasting genereren.

Vereisten voor de beschikbaarheid en fouttolerantie zijn ook van invloed op uw keuze. Bijvoorbeeld, als Hallo koppeling wordt onderbroken, worden toepassingen gebruik te maken van een Kerberos-vertrouwensrelatie of een federatieve vertrouwensrelatie alle waarschijnlijk geheel onderverdeeld tenzij u voldoende infrastructuur in Azure hebt geïmplementeerd. Alternatieve implementatieconfiguraties zoals replica DC's (beschrijfbare of RODC's) niet kunnen tootolerate koppeling uitval Hallo ongewenst verhogen.

### <a name="BKMK_ADSiteTopology"></a>Windows Server Active Directory-site-topologie
U moet definiëren toocorrectly sites en site-koppelingen in de volgorde toooptimize verkeer en kosten te minimaliseren. Sites, sitekoppelingen en subnetten invloed hebben op Hallo-replicatietopologie tussen domeincontrollers en Hallo verkeersstroom verificatie. Overweeg het volgende verkeer kosten Hallo implementeren en configureren van DC's volgens de vereisten van uw implementatiescenario toohello:

* Er is een nominaal kosten per uur voor Hallo gateway zelf:
  
  * Worden kan gestart en gestopt wens naar
  * Als gestopt, zijn Azure VM's geïsoleerd van Hallo-bedrijfsnetwerk
* Binnenkomend verkeer is gratis
* Uitgaand verkeer wordt in rekening gebracht, te volgens[Azure prijzen op overzichtelijke](http://azure.microsoft.com/pricing/). Eigenschappen van de site-koppeling tussen lokale sites en Hallo cloud sites kunt u als volgt optimaliseren:
  
  * Als u meerdere virtuele netwerken gebruikt, configureert u Hallo sitekoppelingen en hun kosten op de juiste wijze tooprevent Windows Server AD DS van de prioriteit te geven hello Azure site via een die Hallo kosteloos dezelfde serviceniveaus kan bieden. U kunt ook overwegen uitschakelen Hallo Bridge alle-(BASL)-koppelingsoptie site (die standaard is ingeschakeld). Dit zorgt ervoor dat alleen rechtstreeks verbonden sites gerepliceerd met elkaar. DC's in transitief verbonden sites niet langer kunnen tooreplicate direct met elkaar zijn, maar moeten worden gerepliceerd via een gemeenschappelijke site of sites. Hallo tussenliggende sites niet beschikbaar zijn voor een bepaalde reden, wordt replicatie tussen de DC's in transitief verbonden sites niet uitgevoerd als zelfs als connectiviteit tussen sites Hallo beschikbaar is. Ten slotte waar secties transitieve replicatie gedrag wenselijk blijven, sitekoppelingsbruggen maken die Hallo juiste sitekoppelingen en sites, zoals het on-premises sites bedrijfsnetwerk bevatten.
  * [Configureren van de kosten van sitekoppelingen](https://technet.microsoft.com/library/cc794882) op de juiste wijze tooavoid onbedoeld verkeer. Bijvoorbeeld, als **probeer dichtstbijzijnde Site** instelling is ingeschakeld, ervoor Hallo virtueel netwerk sites worden niet op de volgende Hallo dichtstbijzijnde doordat Hallo kosten die is gekoppeld van Hallo sitekoppeling object die verbinding hello Azure site back toohello maakt bedrijfsnetwerk.
  * Site-koppeling configureren [intervallen](https://technet.microsoft.com/library/cc794878) en [planningen](https://technet.microsoft.com/library/cc816906) volgens de vereisten voor tooconsistency en frequentie van object wordt gewijzigd. Replicatieschema uitgelijnd met de tolerantie latentie. DC's repliceren alleen Hallo laatste status van een waarde, zodat afnemende Hallo replicatie-interval kosten kunt opslaan als er een snelheid voldoende object wijzigen.
* Als kosten te minimaliseren, een prioriteit wordt, zorg er dan replicatie is gepland en wijzigingsbericht niet is ingeschakeld. Dit is de standaardconfiguratie Hallo bij replicatie tussen sites. Dit is niet belangrijk als u een alleen-lezen domeincontroller op een virtueel netwerk implementeert omdat Hallo RODC uitgaande wijzigingen niet gerepliceerd. Maar als u een beschrijfbare domeincontroller implementeert, moet u ervoor zorgen dat Hallo site-koppeling is niet geconfigureerd tooreplicate updates met onnodige frequentie. Als u een globale catalogusserver (GC) implementeert, zorg ervoor dat elke site met een GC repliceert domeinpartities van een bron-DC in een site die is verbonden met een site-koppeling of sitekoppelingen die een lagere kosten dan Hallo GC in hello Azure site.
* Het is mogelijk toofurther nog steeds netwerkverkeer gegenereerd door de replicatie tussen sites door te wijzigen Hallo replicatie compressiealgoritme verminderen. Hallo-compressiealgoritme wordt bepaald door Hallo REG_DWORD register vermelding HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\Parameters\Replicator compressiealgoritme. Hallo standaardwaarde is 3, die toohello Xpress Compress-algoritme correleert. U kunt Hallo waarde too2, welke wijzigingen Hallo algoritme tooMSZip wijzigen. In de meeste gevallen Hierdoor neemt Hallo compressie, maar dit gebeurt op Hallo kosten CPU-gebruik. Zie voor meer informatie [werkt hoe Active Directory-replicatie-topologie](https://technet.microsoft.com/library/cc755994).

### <a name="BKMK_IPAddressDNS"></a>IP-adressen en DNS
Virtuele machines in Azure zijn "DHCP-lease adressen" Standaard zijn toegewezen. Omdat dynamische adressen voor virtuele Azure-netwerk met een virtuele machine zich blijven voor Hallo levensduur van Hallo virtuele machine voordoen, wordt Hallo vereisten van Windows Server AD DS voldaan.

Als gevolg hiervan wanneer u een dynamisch adres in Azure, bent u van kracht met behulp van een statisch IP-adres omdat het routeerbaar gedurende Hallo Hallo lease, en Hallo periode Hallo lease gelijk toohello levensduur van Hallo-cloudservice is.

Echter, Hallo dynamisch adres toewijzing ongedaan wordt gemaakt als Hallo VM afgesloten wordt. tooprevent hello IP-adres van de toewijzing ongedaan wordt gemaakt, kunt u [Set AzureStaticVNetIP tooassign een statisch IP-adres gebruiken](http://social.technet.microsoft.com/wiki/contents/articles/23447.how-to-assign-a-private-static-ip-to-an-azure-vm.aspx).

Naamomzetting implementeren om uw eigen (of gebruikmaken van uw bestaande) DNS-serverinfrastructuur; Azure DNS-voldoet niet aan Hallo geavanceerde name resolution behoeften van Windows Server AD DS. Bijvoorbeeld deze geen ondersteuning voor dynamische SRV-records, enzovoort. Naamomzetting is een essentiële configuratie-item voor domein-clients en DC's. DC's moet kunnen worden bronrecords registreert en het oplossen van andere DC-bronrecords.
Voor fouttolerantie en tolerantie prestatieredenen is optimale tooinstall Hallo Windows Server DNS-service op Hallo DC's uitgevoerd op Azure. Vervolgens Hallo virtuele Azure-netwerkeigenschappen configureren met de Hallo naam en IP-adres van Hallo DNS-server. Wanneer andere virtuele machines op het virtuele netwerk Hallo start, wordt de DNS-omzetter clientinstellingen geconfigureerd met DNS-server als onderdeel van de dynamische toewijzing van IP-adres Hallo.

> [!NOTE]
> U kunt op lokale computers tooa Windows Server AD DS Active Directory-domein dat wordt gehost op Azure rechtstreeks via Internet Hallo niet koppelen. Hallo Poortvereisten voor Active Directory en de domein-join-bewerking Hallo het niet praktisch toodirectly zichtbaar Hallo nodig poorten geven en in feite een hele DC toohello Internet.
> 
> 

Virtuele machines registreren hun DNS-naam automatisch bij het opstarten of wanneer er een wijziging.

Zie voor meer informatie over het volgende voorbeeld en een ander voorbeeld ziet u hoe tooprovision eerste VM Hallo en installeren van AD DS op deze [een nieuw Active Directory-forest installeren in Microsoft Azure](active-directory-new-forest-virtual-machine.md). Zie voor meer informatie over het gebruik van Windows PowerShell [Azure PowerShell installeren](/powershell/azureps-cmdlets-docs) en [Azure Management-Cmdlets](/powershell/module/azurerm.compute/#virtual_machines).

### <a name="BKMK_DistributedDCs"></a>Geografisch verspreide DC 's
Azure biedt voordelen bij het hosten van meerdere domeincontrollers op verschillende virtuele netwerken:

* Fouttolerantie voor meerdere locaties
* Fysieke nabijheid toobranch kantoren (lagere latentie)

Zie voor meer informatie over het configureren van rechtstreekse communicatie tussen virtuele netwerken [virtueel netwerk toovirtual netwerkconnectiviteit configureren](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).

### <a name="BKMK_RODC"></a>Alleen-lezen domeincontrollers
U moet toochoose of toodeploy lezen-alleen of beschrijfbare domeincontrollers. Geneigd toodeploy RODC's mogelijk op omdat u geen fysieke besturingselement beweegt, maar RODC's zijn ontworpen toobe geïmplementeerd in de locaties waar hun fysieke beveiliging risico, zoals filialen.

Azure biedt geen gevaar Hallo fysieke beveiliging voor een filiaal, maar RODC's mogelijk nog steeds bewijzen toobe rendabeler omdat Hallo-functies die ze bieden geschikt toothese omgevingen zij voor zeer verschillende redenen zijn. Bijvoorbeeld, RODC's hebben geen uitgaande replicatie en zijn kunnen tooselectively vullen geheimen (wachtwoorden). Hallo gebrek aan deze geheime gegevens mogelijk op Hallo-neerwaartse uitgaand verkeer op aanvraag toovalidate ze als een gebruiker of computer verifieert. Maar geheimen kunnen selectief worden vooraf ingevuld en worden opgeslagen in de cache.

RODC's bieden een extra voordeel in en rond HBI en PII problemen omdat u de kenmerken die gevoelige gegevens toohello RODC bevatten gefilterde kenmerkset (VA) kunt toevoegen. Hallo door is een aanpasbare set kenmerken die niet-gerepliceerde tooRODCs. Als u niet zijn toegestaan of niet dat toostore PII of HBI op Azure wilt, kunt u Hallo door als beveiliging. Zie voor meer informatie [gefilterde kenmerk alleen-lezen domeincontroller [(https://technet.microsoft.com/library/cc753459)] ingesteld.

Zorg ervoor dat toepassingen compatibel zijn met de RODC's zijn u van plan bent toouse. Veel Windows Server Active Directory-toepassingen met RODC's werken, maar sommige toepassingen kunnen uitvoeren, inefficiënt of mislukken als ze geen toegang tot tooa beschrijfbare domeincontroller. Zie voor meer informatie [handleiding voor compatibiliteit met alleen-lezen domeincontrollers](https://technet.microsoft.com/library/cc755190).

### <a name="BKMK_GC"></a>Globale catalogus
Moet u toochoose of tooinstall een globale catalogus (GC). In een forest één domein, moet u alle DC's configureren als GC-servers. Kosten wordt niet verhoogd omdat er geen extra replicatieverkeer zullen zijn.

In een forest zijn aangegeven nodig tooexpand Universal groepslidmaatschappen tijdens het verificatieproces Hallo. Als u geen een GC-exemplaar implementeert, genereren werkbelastingen op Hallo virtueel netwerk die worden geverifieerd bij een domeincontroller op Azure uitgaande verificatie verkeer tooquery aangegeven lokale indirect tijdens elke authenticatiepoging.

Hallo kosten in verband met iedere GC zijn minder voorspelbare omdat het hosten van elk domein (in onderdeel). Als Hallo werkbelasting fungeert als host voor een service internetgerichte en gebruikers op basis van Windows Server AD DS verifieert, kunnen de Hallo kosten volledig onvoorspelbaar zijn. toohelp GC-query's buiten Hallo cloud site verminderen tijdens de verificatie, kunt u [universeel groepslidmaatschap in cache opslaan inschakelen](https://technet.microsoft.com/library/cc816928).

### <a name="BKMK_InstallMethod"></a>Installatiemethode
Moet u toochoose hoe tooinstall Hallo DC's in het virtuele netwerk Hallo:

* Promoveren nieuwe DC's. Zie voor meer informatie [een nieuw Active Directory-forest installeren op een virtuele Azure-netwerk](active-directory-new-forest-virtual-machine.md).
* Hallo VHD van een lokale virtuele domeincontroller toohello cloud verplaatsen. In dit geval moet u ervoor zorgen dat Hallo lokale virtuele DC wordt 'verplaatst,' geen 'gekopieerde' of "gekloonde."

Gebruik alleen Azure virtuele machines voor DC's (als tegengestelde tooAzure 'web' of 'worker'-rol virtuele machines). Ze zijn duurzame en duurzaamheid van de status voor een domeincontroller is vereist. Virtuele machines in Azure zijn ontworpen voor werkbelastingen zoals DC's.

Geen gebruik van SYSPREP toodeploy of klonen van domeincontrollers. Hallo mogelijkheid tooclone DC's is alleen beschikbaar vanaf Windows Server 2012. functie voor het klonen Hallo vereist ondersteuning voor VMGenerationID in Hallo onderliggende hypervisor. Hyper-V in Windows Server 2012 en Azure virtuele netwerken beide VMGenerationID, ondersteunen evenals softwareleveranciers virtualisatie van derden.

### <a name="BKMK_PlaceDB"></a>Plaatsing van Hallo Windows Server AD DS-database en SYSVOL
Selecteer waar toolocate Hallo Windows Server AD DS-database, logboekbestanden en SYSVOL. Ze moeten worden geïmplementeerd op Azure gegevensschijven.

> [!NOTE]
> Azure gegevensschijven zijn beperkte too1 TB.
> 
> 

Schijfstations voor gegevens niet cache schrijfbewerkingen standaard gebeurt. Schijfstations voor gegevens die aangesloten tooa VM zijn gebruik write-through cachebewerkingen. Write-through caching zorgt ervoor dat zeker Hallo schrijven is doorgevoerd toodurable Azure storage voordat Hallo transactie voltooid vanuit het perspectief van het besturingssysteem van de VM Hallo Hallo van is. Het biedt duurzaamheid op Hallo kosten van iets langer schrijfbewerkingen.

Dit is belangrijk voor Windows Server AD DS veronderstellingen van Hallo DC write-behind schijfcache ongeldig. Windows Server AD DS probeert toodisable schrijfcache maar het is toohello schijf-IO-systeem toohonor deze. Fout toodisable schrijfcache kan, onder bepaalde omstandigheden, leiden tot USN-terugdraaiacties waardoor achtergebleven objecten en andere problemen.

Als een best practice voor virtuele DC's Hallo te volgen:

* Hallo Host Cache voorkeursinstelling op Hallo Azure-gegevensschijf voor geen instellen. Hiermee voorkomt u problemen met schrijfcache voor AD DS-bewerkingen.
* Hallo-database, logboekbestanden en SYSVOL opslaan op Hallo van dezelfde gegevens schijf of verschillende gegevensschijven. Dit is meestal een andere schijf da Hallo schijf gebruikt voor het besturingssysteem Hallo zelf. Hallo sleutel takeaway is die Hallo Windows Server AD DS-database en SYSVOL moet niet worden opgeslagen op een type besturingssysteem van de Azure-schijf. Standaard installeert hello AD DS-installatieproces deze onderdelen in map % systemroot %, wat niet wordt aanbevolen voor Azure.

### <a name="BKMK_BUR"></a>Back-up en herstel
Zich bewust zijn van wat is en wordt niet ondersteund voor back-up en herstel van een domeincontroller in het algemeen en meer specifiek, die worden uitgevoerd in een virtuele machine. Zie [back-up en herstellen van de overwegingen voor gevirtualiseerde DC's](https://technet.microsoft.com/library/virtual_active_directory_domain_controller_virtualization_hyperv#backup_and_restore_considerations_for_virtualized_domain_controllers).

Systeem systeemstatusback-ups met alleen back-upsoftware die specifiek bewust zijn van de back-eisen voor Windows Server AD DS, zoals Windows Server back-up maken.

Kopieer of klonen VHD-bestanden van DC's in plaats van het uitvoeren van regelmatige back-ups niet. Een terugzetbewerking moet ooit zijn vereist, doet, met behulp van de gekloonde of gekopieerde virtuele harde schijven zonder Windows Server 2012 en een ondersteunde hypervisor leidt tot USN-bellen.

### <a name="BKMK_FedSrvConfig"></a>Configuratie van de Federation-server
Hallo-configuratie van Windows Server AD FS-federatieservers (STSs), hangt gedeeltelijk of hello toepassingen die u wilt dat toodeploy in Azure nodig tooaccess bronnen op uw on-premises netwerk.

Als Hallo toepassingen aan Hallo volgende criteria voldoen, kan u Hallo toepassingen in isolatie implementeren vanuit uw on-premises netwerk.

* Ze accepteren SAML beveiligingstokens
* Ze zijn exposable toohello Internet
* Ze geen toegang krijgen tot lokale bronnen

In dit geval wordt de Windows Server AD FS STSs als volgt configureren:

1. Een geïsoleerde forest met één domein configureren in Azure.
2. Bieden federatieve toegang krijgen tot toohello forest met het configureren van een Windows Server AD FS-federatieserverfarm.
3. Windows Server AD FS (federatieserverfarm en federatieve serverproxyfarm) in Hallo lokale forest configureren.
4. Een federatieve vertrouwensrelatie opzetten tussen Hallo on-premises en Azure-exemplaren van Windows Server AD FS.

Op Hallo anderzijds, als Hallo toepassingen toegang tooon lokale bronnen vereisen, kan u Windows Server AD FS configureren met de toepassing hello op Azure als volgt:

1. Connectiviteit tussen on-premises netwerken en Azure configureren.
2. Een Windows Server AD FS-federatieserverfarm in Hallo lokale forest configureren.
3. Een Windows Server AD FS federatieve serverproxyfarm configureren in Azure.

Deze configuratie heeft Hallo voordeel Hallo blootstelling van lokale bronnen vergelijkbare tooconfiguring Windows Server AD FS met toepassingen in een perimeternetwerk te verminderen.

Houd er rekening mee dat in beide scenario's, u vertrouwensrelaties relaties met meer id-providers instellen kunt als business-to-business samenwerking nodig is.

### <a name="BKMK_CloudSvcConfig"></a>Configuratie voor cloud-services
Cloudservices zijn nodig als u wilt dat tooexpose een virtuele machine rechtstreeks toohello Internet of een internetgerichte tooexpose taakverdeling toepassing. Dit is mogelijk omdat elke cloudservice één configureerbare virtuele IP-adres biedt.

### <a name="BKMK_FedReqVIPDIP"></a>Federatieve server-vereisten voor openbare en particuliere IP-adressering (dynamische IP versus virtuele IP)
Elke virtuele machine van Azure ontvangt een dynamische IP-adres. Een dynamische IP-adres is een persoonlijk adres toegankelijk zijn alleen binnen Azure. In de meeste gevallen wordt het echter noodzakelijk tooconfigure een virtueel IP-adres voor uw Windows Server AD FS-implementaties zijn. Hallo virtueel IP-adres nodig tooexpose Windows Server AD FS-eindpunten toohello Internet is, en door federatieve partners en -clients wordt gebruikt voor verificatie en het doorlopende beheer. Een virtueel IP-adres is een eigenschap van een cloudservice waarin een of meer virtuele machines in Azure. Als de claimbewuste toepassing hello geïmplementeerd op Azure en Windows Server AD FS internetgerichte en -share algemene poorten, elk een virtueel IP-adres van de eigen is vereist en zal deze daarom nodig toocreate een cloudservice voor de toepassing hello en een tweede voor Windows Server AD FS.

Zie voor definities van Hallo voorwaarden virtueel IP-adres en dynamische IP-adres, [termen en definities](#BKMK_Glossary).

### <a name="BKMK_ADFSHighAvail"></a>Windows Server AD FS-configuratie voor hoge beschikbaarheid
Het is mogelijk toodeploy zelfstandige Windows Server AD FS federatieservices, maar het is aanbevolen toodeploy een farm met ten minste twee knooppunten voor AD FS-STS- en proxy's voor productieomgevingen.

Zie [aandachtspunten voor AD FS 2.0 implementatie topologie](https://technet.microsoft.com/library/gg982489) in Hallo [AD FS 2.0-ontwerphandleiding](https://technet.microsoft.com/library/dd807036) toodecide Distributieconfiguratie die opties beste aanpassen aan uw specifieke behoeften.

> [!NOTE]
> Volgorde tooget load balancing voor Windows Server AD FS-eindpunten op Azure, configureert u alle leden van Hallo Windows Server AD FS-farm in Hallo dezelfde cloudservice en gebruik Hallo load balancing-mogelijkheden van Azure voor HTTP (standaard 80) en HTTPS-poorten (standaard 443). Zie voor meer informatie [Azure load balancer-test](https://msdn.microsoft.com/library/azure/jj151530).
> Windows Server Network Load Balancing (NLB) wordt niet ondersteund in Azure.
> 
> 

