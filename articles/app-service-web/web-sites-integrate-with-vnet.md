---
title: aaaIntegrate een app met een Azure Virtual Network
description: Laat u zien hoe tooconnect een app in Azure App Service tooa nieuwe of bestaande virtuele Azure-netwerk
services: app-service
documentationcenter: 
author: ccompy
manager: erikre
editor: cephalin
ms.assetid: 90bc6ec6-133d-4d87-a867-fcf77da75f5a
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: ccompy
ms.openlocfilehash: a93c504481400245b02220b541a008a7c874d10a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-your-app-with-an-azure-virtual-network"></a>Uw app integreren met een Azure-netwerk
Dit document beschrijft hello Azure App Service virtueel netwerk-integratiefunctie en ziet u hoe tooset het met apps in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714). Als u niet bekend bent met Azure Virtual Networks (vnet's), is dit een functie waarmee u veel van uw Azure-resources in een internet-routeable netwerk dat u beheert de toegang tot tooplace. Deze netwerken kunnen vervolgens worden verbonden tooyour on-premises netwerken met een aantal VPN-technologieën. meer informatie over Azure Virtual Networks, toolearn beginnen met Hallo informatie hier: [Azure Virtual Network-overzicht][VNETOverview]. 

Hello Azure App Service heeft twee vormen. 

1. Hallo multitenant systemen die ondersteuning bieden voor Hallo talrijke prijsstelling
2. Hallo as-omgeving (App Service omgeving) premium functie in uw VNet implementeert. 

Dit document doorloopt VNet-integratie en geen App Service-omgeving. Als u wilt dat toolearn meer over de functie Hallo as-omgeving, beginnen met een Hallo informatie hier: [App Service-omgeving inleiding][ASEintro].

Integratie met VNet resulteert in uw web-app toegang tooresources in het virtuele netwerk maar verleent geen persoonlijke toegang tooyour web-app van Hallo virtuele netwerk. Toegang tot persoonlijke site verwijst toomaking uw app alleen toegankelijk vanaf een particulier netwerk zoals van binnen een virtuele Azure-netwerk. Toegang tot persoonlijke site is alleen beschikbaar als er een as-omgeving met een interne Load Balancer (ILB) geconfigureerd. Start met Hallo artikel hier voor meer informatie over het gebruik van een as ILB-omgeving: [maken en gebruiken van een as-omgeving voor de ILB][ILBASE]. 

Een veelvoorkomend scenario waar u de VNet-integratie wilt gebruiken met het inschakelen van de toegang van uw web-app tooa database of een webservice die wordt uitgevoerd op een virtuele machine in uw Azure virtual network. VNet integratie, u hoeft niet tooexpose een openbaar eindpunt voor toepassingen op de virtuele machine maar Hallo persoonlijke niet internet routeerbare adressen in plaats daarvan kunt gebruiken. 

Hallo VNet-integratiefunctie:

* vereist een standaard, Premium of geïsoleerd prijzen plannen 
* werkt met de klassieke weergave of Resource Manager VNet 
* biedt ondersteuning voor TCP en UDP
* werkt met mobiele, Web en API apps
* Hiermee kunt u een app tooconnect tooonly 1 VNet tegelijk
* Hiermee up toofive VNets toobe geïntegreerd met in een App Service-Plan 
* Hiermee kunt Hallo hetzelfde VNet toobe die wordt gebruikt door meerdere apps in een App Service-Plan
* ondersteunt een SLA met 99,9% vanwege toohello SLA op Hallo VNet-Gateway

Er zijn een aantal zaken die VNet integratie biedt geen ondersteuning voor met inbegrip van:

* koppelen van een station
* AD-integratie 
* NetBios
* toegang tot persoonlijke site

### <a name="getting-started"></a>Aan de slag
Hier volgen enkele dingen tookeep rekening voordat het verbinden van uw web-app tooa virtueel netwerk:

* VNet-integratie werkt alleen met apps in een **standaard**, **Premium**, of **geïsoleerd** plan prijzen. Als u Hallo-functie inschakelen en vervolgens uw App Service-abonnement tooan niet-ondersteunde te schalen verliezen prijzen plan uw apps hun verbindingen toohello VNets die ze gebruiken. 
* Als het virtuele doelnetwerk al bestaat, moet de punt-naar-site VPN is ingeschakeld met een gateway voor dynamische routering kan pas verbonden tooan app worden hebben. Als uw gateway is geconfigureerd met statische routering, kunt u de punt-naar-site virtueel particulier netwerk (VPN) niet inschakelen.
* Hallo VNet moet Hallo hetzelfde abonnement als uw App Service-Plan(ASP). 
* Hallo-apps die zijn geïntegreerd met een VNet gebruiken Hallo DNS die is opgegeven voor dit VNet.
* Standaard routeren uw integreren apps alleen verkeer in uw VNet op basis van Hallo routes die zijn gedefinieerd in uw VNet. 

## <a name="enabling-vnet-integration"></a>VNet-integratie inschakelen
Dit document richt zich voornamelijk over het gebruik van hello Azure-portal voor VNet-integratie. tooenable VNet integratie met uw app met behulp van PowerShell, volgt u Hallo aanwijzingen hier: [verbinding maken met uw app tooyour virtueel netwerk met behulp van PowerShell][IntPowershell].

U hebt uw app tooa nieuwe of bestaande virtuele netwerk Hallo optie tooconnect. Als u een nieuw netwerk als onderdeel van uw integratie maakt, vervolgens bovendien toojust maken Hallo VNet, een gateway voor dynamische routering is vooraf geconfigureerd voor u en punt tooSite VPN is ingeschakeld. 

> [!NOTE]
> Configureren van een nieuwe virtuele netwerkintegratie kan enkele minuten duren. 
> 
> 

tooenable VNet integratie, opent u de instellingen van uw app en selecteer vervolgens de netwerken. Hallo gebruikersinterface die wordt geopend biedt drie netwerken opties. Deze handleiding zal in VNet integratie echter hybride verbindingen en App Service-omgevingen worden verderop in dit document besproken. 

Als uw app zich niet in de juiste prijzen plan hello, kunt Hallo UI u tooscale uw plan tooa prijzen hoger plan van uw keuze.

![][1]

### <a name="enabling-vnet-integration-with-a-pre-existing-vnet"></a>VNet-integratie met een bestaande VNet inschakelen
Hallo gebruikersinterface van de VNet-integratie kunt u tooselect uit een lijst met uw vnet's. Hallo klassieke vnet's geven aan dat ze zoals met Hallo woord 'Klassiek' in de volgende toohello VNet-naam haakjes. Hallo is lijst gesorteerd zodat hello Resource Manager VNets worden eerst weergegeven. In Hallo kunt u onderstaande afbeelding zien dat er slechts één VNet kan worden geselecteerd. Er zijn meerdere redenen dat een VNet worden lichter gekleurd weergegeven met inbegrip van kan:

* Hallo VNet bevindt zich in een ander abonnement dat uw account toegang tot heeft
* Hallo VNet heeft geen punt tooSite ingeschakeld
* Hallo VNet heeft geen gateway voor dynamische routering

![][2]

integratie van tooenable Klik gewoon op Hallo toointegrate met gewenst VNet. Nadat u Hallo VNet hebt geselecteerd, wordt uw app automatisch opnieuw opgestart om Hallo wijzigingen tootake effect. 

##### <a name="enable-point-toosite-in-a-classic-vnet"></a>Punt tooSite in een klassiek VNet inschakelen
Als uw VNet geen een gateway heeft noch punt tooSite heeft, hebt u tooset dat bij de eerste. toodo dit voor een klassiek VNet gaat toohello [Azure-portal] [ AzurePortal] en online zetten van het Hallo-lijst met virtuele Networks(classic). Klik op Hallo netwerk u toointegrate met wilt en klikt u op Hallo big vak onder Essentials aangeroepen VPN-verbindingen vanaf deze locatie. Hier kunt u uw VPN-punt toosite maken en zelfs laten maken van een gateway. Nadat u Hallo punt toosite gateway maken ervaring doorloopt is ongeveer 30 minuten voordat deze gereed is. 

![][8]

##### <a name="enabling-point-toosite-in-a-resource-manager-vnet"></a>Punt tooSite in een Resource Manager VNet inschakelen
een Resource Manager VNet met een gateway en punt tooSite tooconfigure, kunt u beide PowerShell zoals beschreven hier [een punt-naar-Site-verbinding tooa virtueel netwerk configureren met behulp van PowerShell] [ V2VNETP2S] of hello Azure-portal zoals beschreven hier gebruiken [configureren een punt-naar-Site verbinding tooa VNet met behulp van Azure-portal Hallo][V2VNETPortal]. Hallo UI tooperform deze mogelijkheid is nog niet beschikbaar. Houd er rekening mee dat u toocreate certificaten nodig voor Hallo punt tooSite configuratie. Dit wordt automatisch geconfigureerd wanneer u verbinding maakt met uw WebApp toohello VNet. 

### <a name="creating-a-pre-configured-vnet"></a>Maken van een vooraf geconfigureerde VNet
Als u toocreate een nieuw VNet dat is geconfigureerd met een gateway en punt-naar-Site wilt heeft hello networking UI-App Service Hallo mogelijkheid toodo die maar alleen voor een Resource Manager VNet. Als u toocreate een klassiek VNet met een gateway en punt-naar-Site wenst, moet u toodo dit handmatig via de gebruikersinterface van Hallo netwerken. 

selecteert u een Resource Manager VNet via Hallo VNet integratie-gebruikersinterface toocreate **nieuw virtueel netwerk maken** en geef de:

* Virtuele-netwerknaam
* Virtueel netwerkadresblok
* De subnetnaam van het
* Adresblok van gatewaysubnet
* Gateway-Adresblok
* Punt-naar-Site-Adresblok

Als u dit VNet tooconnect tooany op andere netwerken wilt, moet u vervolgens niet verzamelen van IP-adresruimte met deze netwerken overlapt. 

> [!NOTE]
> Maken van een Resource Manager VNet met een gateway duurt ongeveer 30 minuten en momenteel is niet geïntegreerd Hallo VNet met uw app. Nadat uw VNet is gemaakt met de gateway Hallo u toocome back tooyour app VNet integratie gebruikersinterface nodig hebt en uw nieuwe VNet te selecteren.
> 
> 

![][3]

Azure VNets worden gewoonlijk gemaakt binnen een particulier netwerkadressen. Functie routeert door standaard Hallo VNet integratie verkeer dat is bestemd voor deze IP-adresbereiken in uw VNet. Hallo privé IP-adresbereiken zijn:

* -Dit is dezelfde Hallo als 10.0.0.0 - 10.0.0.0/8 10.255.255.255
* -Dit is dezelfde Hallo als 172.16.0.0 - 172.16.0.0/12 172.31.255.255 
* -Dit is dezelfde Hallo als 192.168.0.0 - 192.168.0.0/16 192.168.255.255

Hallo VNet-adresruimte moet toobe opgegeven in CIDR-notatie. Als u niet bekend met CIDR-notatie bent, is dit een methode voor het opgeven van adresblokken met een IP-adres en een geheel getal dat Hallo netwerkmasker vertegenwoordigt. Als een snelle verwijzing rekening mee dat 10.1.0.0/24 zou 256 adressen en 10.1.0.0/25 128 adressen zou zijn. Een IPv4-adres met een /32 zou slechts 1 adres zijn. 

Als u Hallo DNS-serverinformatie hier instelt, wordt die is ingesteld voor uw VNet. U kunt deze informatie Hallo VNet gebruikerservaringen bewerken na het maken van een VNet. Als u Hallo Hallo VNet DNS wijzigt, moet u een synchronisatie netwerkbewerking tooperform.

Bij het maken van een klassiek VNet hello VNet integratie gebruikersinterface met een VNet wordt gemaakt in Hallo dezelfde resourcegroep als uw app. 

## <a name="how-hello-system-works"></a>De werking van Hallo-systeem
Onder Hallo dekt dit onderdeel is gebaseerd boven op het punt-naar-Site VPN-technologie tooconnect uw app tooyour VNet. Apps in Azure App Service beschikken over een multitenant-systeemarchitectuur, die inrichten van een app rechtstreeks in een VNet verhindert, zoals met virtuele machines wordt uitgevoerd. We beperken netwerk toegang toojust Hallo virtuele machine die als host fungeert voor de app Hallo door voort te bouwen op punt-naar-site-technologie. Toegang tot het netwerk toohello wordt verder beperkt op deze hosts app zodat uw apps alleen toegang Hallo-netwerken tot die u deze tooaccess configureert. 

![][4]

Als u nog een DNS-server geconfigureerd met het virtuele netwerk, moet uw app toouse IP-adressen tooreach resource in Hallo VNet. Tijdens het gebruik van IP-adressen, houd er rekening mee dat Hallo groot voordeel van deze functie is dat Hiermee u toouse Hallo particuliere adressen binnen uw particuliere netwerk kunt. Als u uw app up toouse openbare IP-adressen voor een van uw virtuele machines, u Hallo VNet-integratiefunctie niet gebruikt en communiceren via Hallo internet.

## <a name="managing-hello-vnet-integrations"></a>Hallo VNet integraties beheren
Hallo mogelijkheid tooconnect en tooa die vnet op het niveau van een app is verbreken. Bewerkingen die invloed kunnen zijn op Hallo VNet-integratie voor meerdere apps zich op een ASP-niveau. Van de gebruikersinterface die wordt weergegeven op het niveau app Hallo Hallo, krijgt u informatie op uw VNet. De meeste Hallo dezelfde informatie ook op Hallo ASP niveau weergegeven wordt. 

![][5]

Hallo netwerkstatus van de functie pagina ziet u als uw app verbonden tooyour VNet is. Als uw VNet-gateway is niet actief om welke reden is, zou dit wordt weergegeven als niet-verbonden. 

Hallo informatie u hebt nu beschikbaar tooyou in niveau VNet integratie UI is dezelfde als Hallo gedetailleerde informatie over u krijgen via Hallo ASP Hallo Hallo-app. Hier volgen die items:

* VNet - naam van deze koppeling opent Hallo UI virtuele Azure-netwerk
* Locatie - dit duidt op Hallo-locatie van uw VNet. Het is mogelijk toointegrate met een VNet in een andere locatie.
* Certificaatstatus - er zijn certificaten gebruikt toosecure Hallo VPN-verbinding tussen Hallo-app en Hallo VNet. Dit duidt op een test tooensure ze zijn gesynchroniseerd.
* Status van de gateway - uw gateways moet omlaag om welke reden vervolgens uw app geen toegang tot bronnen in Hallo VNet. 
* VNet-adresruimte - dit Hallo IP-adresruimte voor uw VNet is. 
* Punt tooSite adresruimte - dit Hallo punt toosite IP-adresruimte voor uw VNet is. Uw app bevat communicatie afkomstig is van een van de Hallo IP-adressen in deze adresruimte. 
* Site toosite adresruimte - kunt u Site tooSite VPN-verbindingen tooconnect uw VNet tooyour lokale bronnen of tooother VNet. Hebt u die vervolgens Hallo IP-adresbereiken die worden gedefinieerd met behulp van de VPN-verbinding wordt hier geconfigureerd.
* DNS-Servers - als u DNS-Servers geconfigureerd met uw VNet hebt en vervolgens worden deze hier weergegeven.
* IP-adressen gerouteerd toohello VNet - er zijn een lijst met IP-adressen die uw VNet gedefinieerd is voor Routering en de adressen die hier worden weergegeven. 

Hallo bewerkingen die van Hallo app weergave van uw VNet-integratie kunt u uw is toodisconnect uw app uit Hallo momenteel is verbonden met VNet. toodo deze klikt u boven Hallo verbreken. Deze actie wordt niet gewijzigd voor uw VNet. Hallo VNet en inclusief Hallo gateways configuratie blijft ongewijzigd. Als u vervolgens toodelete uw VNet wilt, moet u toofirst verwijderen Hallo resources daarin inclusief Hallo gateways. 

Hallo weergave App Service-Plan heeft een aantal aanvullende bewerkingen. Het is ook vanuit anders dan Hallo-app. tooreach hello ASP Networking UI open gewoon uw ASP-UI en schuif omlaag. Er is een UI-element netwerkstatus van de functie wordt aangeroepen. Dit biedt de details van sommige secundaire rond de integratie van uw VNet. Hallo netwerk functie Status gebruikersinterface te klikken op deze gebruikersinterface worden geopend. Als u vervolgens op Hallo op 'Klik hier toomanage', gebruikersinterface met een lijst met Hallo VNet integraties in deze ASP wordt geopend.

![][6]

Hallo-locatie van Hallo ASP is goed tooremember wanneer bekijkt hello locaties Hallo VNets die u integreert. Wanneer Hallo VNet in een andere locatie zijn veel meer waarschijnlijke toosee latentieproblemen. 

Hallo VNets die zijn geïntegreerd met is een herinnering op hoeveel VNets dat uw apps in deze ASP en hoeveel er zijn geïntegreerd met. 

details toosee toegevoegd op elke VNet, klik op Hallo u geïnteresseerd bent in VNet. Bovendien toohello details die eerder werden vermeld, u kunt ook een overzicht van Hallo-apps in deze ASP die van dit VNet gebruikmaken. 

Ten opzichte van zijn tooactions er twee primaire acties. Hallo is eerst Hallo mogelijkheid tooadd routes die uw app in uw VNet uitgaand verkeer van station. de tweede actie Hallo is Hallo mogelijkheid toosync certificaten en informatie over het netwerk.

![][7]

**Routering** zoals eerder opgemerkt Hallo-routes die zijn gedefinieerd in uw VNet zijn wat wordt gebruikt voor het routeren van verkeer naar uw VNet vanaf uw app. Er zijn enkele toepassingen al klanten waar toosend extra uitgaand verkeer van een app in Hallo VNet en ze deze mogelijkheid is opgegeven. Wat gebeurt er toohello verkeer daarna up toohow Hallo klant Hiermee configureert u het VNet. 

**Certificaten** Hallo certificaatstatus duidt op een controle uitgevoerd door Hallo App Service-toovalidate dat Hallo-certificaten die we voor Hallo VPN-verbinding nog steeds goed zijn. Wanneer VNet-integratie is ingeschakeld, klikt u vervolgens is als dit Hallo eerste integratie-toothat VNet uit alle apps in deze ASP een vereiste uitwisseling van certificaten tooensure Hallo beveiliging van Hallo-verbinding. Samen met de Hallo certificaten krijgen we Hallo DNS-configuratie, routes en andere vergelijkbare dingen die Hallo-netwerk beschrijven.
Als deze certificaten of informatie over het netwerk is gewijzigd, moet u tooclick 'Sync netwerk'. **Opmerking**: wanneer u klikt op 'Sync netwerk' en zorgt u ervoor een korte uitval in de verbinding tussen uw app en uw VNet dat. Terwijl u uw app niet opnieuw wordt opgestart, Hallo verlies van verbinding kan ervoor zorgen dat uw site toonot functie goed. 

## <a name="accessing-on-premises-resources"></a>Toegang tot lokale bronnen
Een van de voordelen Hallo van Hallo VNet-integratiefunctie is dat zo is verbonden met uw VNet tooyour on-premises netwerk met een Site tooSite VPN-en vervolgens uw apps toegang tot tooyour lokale bronnen van uw app hebben kunnen. Voor deze toowork Hoewel u tooupdate wellicht uw lokale VPN-gateway met Hallo van routes voor uw punt tooSite IP-adresbereik. Wanneer Hallo Site tooSite VPN eerst is ingesteld en vervolgens het Hallo-scripts gebruiken tooconfigure moet deze routes, met inbegrip van uw VPN-punt tooSite instellen. Als u Hallo punt tooSite VPN toevoegen nadat u uw Site tooSite VPN hebt gemaakt, moet u tooupdate Hallo routes handmatig. Informatie over hoe toodo die verschillen per gateway en niet in de hier beschreven. 

> [!NOTE]
> Hallo-integratiefunctie VNet is niet geïntegreerd met een app met een VNet met een ExpressRoute-Gateway. Zelfs als Hallo ExpressRoute-Gateway is geconfigureerd in [co-existentie modus] [ VPNERCoex] hello VNet integratie niet werkt. Als u tooaccess resources via een ExpressRoute-verbinding nodig, dan kunt u een [App Service-omgeving][ASE], die wordt uitgevoerd in uw VNet.
> 
> 

## <a name="pricing-details"></a>Prijsdetails
Er zijn slechts enkele nuances waarmee u houden moet rekening bij het gebruik van de VNet-integratiefunctie Hallo prijzen. Er zijn 3 gerelateerde kosten toohello gebruik van deze functie:

* ASP prijzen laag vereisten
* Kosten voor de gegevensoverdracht
* Kosten van de VPN-Gateway.

Voor uw apps toobe kunnen toouse deze functie moeten toobe in een Standard of Premium App Service-Plan. Op deze kosten hier kunt u meer informatie bekijken: [prijzen van App Service][ASPricing]. 

Vervaldatum toohello manier punt tooSite VPN-verbindingen worden verwerkt, hebt u altijd kosten met zich mee voor uitgaande gegevens via de integratie van de VNet-verbinding zelfs als Hallo VNet in Hallo hetzelfde Datacenter. toosee wat deze kosten zijn, kijkt u hier: [gegevens overbrengen Pricing Details][DataPricing]. 

laatste item Hallo is Hallo kosten van het Hallo-VNet-gateways. Als u geen Hallo gateways voor iets anders zoals tooSite Site-VPN-verbindingen, klikt betaalt u voor gateways toosupport hello VNet-integratiefunctie. Er zijn meer informatie op deze kosten hier: [prijzen voor VPN-Gateway][VNETPricing]. 

## <a name="troubleshooting"></a>Problemen oplossen
Tijdens het Hallo-functie is eenvoudig tooset, niet dat betekent dat dat uw ervaring probleem beschikbaar zal zijn. Moet u tegenkomt zijn problemen bij toegang tot het gewenste eindpunt er een aantal hulpprogramma's kunt u verbinding hebben met tootest Hallo app-console. Er zijn twee ervaringen van de console die kunt u. Een van de Hallo Kudu-console en Hallo andere is Hallo-console die u kunt op Hallo Azure-portal bereiken. tooget toohello Kudu-console van uw app gaat tooTools Kudu ->. Dit is dezelfde als te gaan Hallo [sitename]. scm.azurewebsites.net. Zodra dat wordt geopend gewoon Ga toohello foutopsporing console tabblad tooget toohello Azure portal gehoste-console klikt u vervolgens vanuit uw app gaat-tooTools >-Console. 

#### <a name="tools"></a>Hulpprogramma's
ping Hallo-hulpprogramma's, nslookup en tracert werken via de console vanwege beperkingen toosecurity Hallo niet. toofill hello void er zijn twee afzonderlijke hulpprogramma's toegevoegd. In de volgorde tootest DNS-functionaliteit hebben we een hulpprogramma met de naam nameresolver.exe toegevoegd. Hallo-syntaxis is:

    nameresolver.exe hostname [optional: DNS Server]

U kunt nameresolver toocheck Hallo hostnamen afhankelijk van uw app kunt gebruiken. Op deze manier kunt u als u iets verkeerd geconfigureerd met uw DNS of mogelijk heb toegang tooyour DNS-server testen.

de volgende hulpprogramma Hallo kunt u tootest voor TCP-verbinding tooa host en poort combinatie. Dit programma heet tcpping.exe en Hallo syntaxis is:

    tcpping.exe hostname [optional: port]

Hallo tcpping hulpprogramma kunt u zien als u een specifieke host en poort kan bereiken. Alleen succes kan tonen als: Er is een toepassing die luistert op de combinatie van de host en poort van de Hallo en er is toegang tot het netwerk van uw app toohello opgegeven host en poort.

#### <a name="debugging-access-toovnet-hosted-resources"></a>Foutopsporing tooVNet toegang tot gehoste bronnen
Er zijn een aantal dingen die u kunt voorkomen dat uw app in een specifieke host en poort bereikt. Hallo meestal is een van drie dingen:

* **Er is een firewall in Hallo manier** als er een firewall op Hallo manier, bereikt u Hallo TCP-time. Dat is 21 seconden in dit geval. Hallo tcpping hulpprogramma tootest verbinding gebruiken. TCP-outs kunnen worden vanwege toomany dingen voorbij firewalls, maar er starten. 
* **DNS is niet toegankelijk** Hallo DNS time is drie seconden per DNS-server. Als u twee DNS-servers hebt, is Hallo time-out 6 seconden. Gebruik nameresolver toosee als DNS werkt. Houd er rekening mee dat u niet nslookup gebruiken zoals die geen Hallo uw VNet is geconfigureerd gebruikt met DNS.
* **Ongeldige P2S-IP-adresbereik** Hallo punt toosite IP-adresbereik moet toobe in RFC 1918 Hallo persoonlijke IP-adresbereiken (10.0.0.0-10.255.255.255 / 172.16.0.0-172.31.255.255 / 192.168.0.0-192.168.255.255). Als Hallo bereik IP-adressen buiten die gebruikt, vervolgens werkt dingen niet. 

Als deze items niet beantwoord uw probleem, er eerst voor eenvoudige zaken Hallo: 

* Wordt Hallo Gateway weergegeven alsof ze Hallo portal?
* Kunnen certificaten dat deze synchroon weergeven?
* Iedereen Hallo netwerkconfiguratie wijzigen zonder een 'Sync netwerk' in Hallo van invloed op een ASP? 

Als uw gateway actief is, brengt u het back-up. Als uw certificaten niet gesynchroniseerd zijn, gaat u toohello ASP weergave van uw VNet-integratie en 'Sync netwerk' bereikt. Als u vermoedt dat er van een wijziging aangebracht tooyour VNet-configuratie is sprake en het is geen synchronisatie zou met uw ASP vervolgens gaat u toohello ASP weergave van uw VNet-integratie en klik op 'Sync netwerk' net zoals een herinnering, dit zorgt ervoor dat een korte stroomstoring met uw VNet-verbinding en uw apps . 

Als dat goed is, moet u toodig in een dieper bits:

* Zijn er geen andere apps met behulp van VNet integratie tooreach bronnen in Hallo hetzelfde VNet? 
* Kunt u gaan toohello app-console en tcpping tooreach van andere bronnen in uw VNet gebruiken? 

Als een van bovenstaande hello voldaan wordt, wordt uw VNet-integratie fijn en Hallo probleem ergens anders is. Dit is waar het ophalen van toobe meer een uitdaging omdat er geen eenvoudige manier toosee waarom u een hostnaam: poort niet bereiken. Sommige Hallo oorzaken zijn:

* u hebt een firewall up op de host toegang toohello toepassing poort van uw IP-adresbereik punt toosite voorkomen. Vaak overschrijden van subnetten vereist openbare toegang.
* de doelhost is niet actief
* uw toepassing is niet beschikbaar
* moest u Hallo verkeerde IP- of hostnaam
* uw toepassing luistert op een andere poort dan wat u verwacht. U kunt dit controleren door te gaan op die host en 'netstat - aon' met behulp van Hallo-opdrachtprompt. Hiermee geeft u welk proces ID luistert op poort. 
* de netwerkbeveiligingsgroepen zijn zodanig dat toegang tooyour toepassingshost en de poort van uw IP-adresbereik punt toosite geconfigureerd

Houd er rekening mee dat u niet welk IP-in uw punt tooSite IP-adresbereik die door uw app wordt gebruikt weet, dus u tooallow toegang vanaf Hallo hele bereik moet. 

Extra stappen omvatten:

* aanmelden bij een andere virtuele machine in uw VNet en poging tooreach uw resource hostnaam: poort daar. Er zijn een aantal TCP-ping-hulpprogramma's kunt gebruiken voor dit doel uit te voeren of zelfs telnet kunt gebruiken als moeten worden. Hallo is doel hier alleen toodetermine als de verbinding er van deze andere virtuele machine is. 
* Zorg ervoor dat een toepassing op een andere virtuele machine en toegang toothat host en de poort van de console Hallo van uw app testen

#### <a name="on-premises-resources"></a>Lokale bronnen ####
Als uw app niet kan lokale bereiken, is Hallo eerste wat die u moet controleren als u een resource in uw VNet kan bereiken. Als dat werkt, probeert u tooreach Hallo on-premises toepassing van een virtuele machine in Hallo VNet. U kunt telnet of een TCP-ping-hulpprogramma gebruiken. Als uw virtuele machine kan niet bereiken van uw lokale resource vervolgens controleren of dat uw Site tooSite VPN-verbinding werkt. Als u werkt, moet u Hallo dezelfde mogelijkheden eerder hebt genoteerd evenals Hallo on-premises gateway-configuratie en status te controleren. 

Nu zijn als uw VNet gehost VM toegang heeft tot uw on-premises systeem, maar uw app niet dan Hallo reden is waarschijnlijk een van de volgende Hallo:

* de routes zijn niet geconfigureerd met uw punt toosite IP-adresbereiken in uw on-premises gateway
* de netwerkbeveiligingsgroepen blokkeren toegang voor uw IP-adresbereik punt tooSite
* de firewalls op het lokale blokkeren verkeer van uw IP-adresbereik punt tooSite
* hebt u een gebruiker gedefinieerde Route(UDR) in uw VNet waarmee wordt voorkomen uw verkeer punt tooSite op basis van dat uw on-premises netwerk bereikt

## <a name="hybrid-connections-and-app-service-environments"></a>Hybride verbindingen en App Service-omgevingen
Er zijn drie functies waarmee u toegang tot tooVNet gehoste bronnen. Ze zijn:

* VNet-integratie
* Hybride verbindingen
* App Service-omgevingen

Hybride verbindingen, moet u tooinstall een relay-agent Hallo hybride verbinding Manager(HCM) in uw netwerk genoemd. Hallo HCM moet toobe kunnen tooconnect tooAzure en ook tooyour toepassing. Deze oplossing is met name geweldige van een extern netwerk zoals uw on-premises netwerk of zelfs een andere cloud gehost netwerk omdat het geen een internet toegankelijk eindpunt vereist. Hallo HCM kan alleen worden uitgevoerd op Windows en u kunt up toofive instanties die actief zijn tooprovide hoge beschikbaarheid. Hybride verbindingen biedt alleen ondersteuning voor TCP via en elk eindpunt CH toomatch tooa specifieke hostnaam: poort combinatie heeft. 

Hallo App Service-omgeving functie kunt u een exemplaar van Azure App Service Hallo toorun in uw VNet. Hiermee kunt uw apps toegang tot bronnen in uw VNet zonder eventuele extra stappen. Sommige Hallo andere voordelen van een App Service-omgeving zijn waarmee u Dv2 op basis van werknemers met up too14 GB RAM-geheugen kunt. Een ander voordeel is dat u Hallo system toomeet uw behoeften schalen kunt. In tegenstelling tot Hallo multitenant omgevingen waarin de ASP beperkt too20 exemplaren is in een as-omgeving kunt u opschalen too100 ASP-exemplaren. Hallo-bewerkingen dat u met een as-omgeving die u niet met VNet-integratie is dat een App Service-omgeving met een ExpressRoute-VPN kunt werken. 

Hoewel er dat enkele case overlapping gebruiken, kunt geen van deze functie vervangen Hallo anderen. Weten welke functie toouse is gebonden tooyour behoeften. Bijvoorbeeld:

* Als u een ontwikkelaar en alleen wilt toorun een site in Azure en hebben toegang Hallo-database op Hallo werkstation onder uw helpdesk dan is het eenvoudigste ding toouse Hallo hybride verbindingen. 
* Als u een grote organisatie die tooput wil een groot aantal eigenschappen in de openbare cloud Hallo web en deze op uw eigen netwerk beheren, wilt u toogo Hello App Service-omgeving. 
* Als u een aantal App Service hebt gehost apps en gewoon wilt tooaccess resources in uw VNet, dan VNet integratie Hallo manier toogo is. 

Afgezien van gebruiksvoorbeelden hello, zijn sommige eenvoud gerelateerde aspecten. Als uw VNet is al verbonden tooyour on-premises netwerk, met behulp van VNet-integratie of een App Service-omgeving is een eenvoudige manier tooconsume lokale resources. Als uw VNet is niet verbonden op Hallo tooyour on-premises netwerk veel die meer overhead tooset van een site toosite VPN met uw VNet vergeleken met de installatie van Hallo HCM is. 

Voorbij Hallo functionele verschillen, er zijn ook prijzen verschillen. Hallo-App Service-omgeving-functie is een Premium serviceaanbieding maar aanbiedingen Hallo configuratie van de meeste netwerkmogelijkheden bovendien tooother handige functies. VNet-integratie met Standard of Premium ASP's kunnen worden gebruikt en is ideaal voor het veilig verbruik van bronnen in uw VNet vanaf Hallo-multitenant-App Service. Hybride verbindingen is momenteel afhankelijk van een account, wat heeft niveaus die gratis start en vervolgens geleidelijk duurdere op basis van Hallo bedrag u moet BizTalk. Wanneer er tooworking via netwerken met veel echter, kan niet worden andere zoals hybride verbindingen die middelen in afzonderlijke netwerken ook meer dan 100 tooaccess kunt inschakelen. 

<!--Image references-->
[1]: ./media/web-sites-integrate-with-vnet/vnetint-upgradeplan.png
[2]: ./media/web-sites-integrate-with-vnet/vnetint-existingvnet.png
[3]: ./media/web-sites-integrate-with-vnet/vnetint-createvnet.png
[4]: ./media/web-sites-integrate-with-vnet/vnetint-howitworks.png
[5]: ./media/web-sites-integrate-with-vnet/vnetint-appmanage.png
[6]: ./media/web-sites-integrate-with-vnet/vnetint-aspmanage.png
[7]: ./media/web-sites-integrate-with-vnet/vnetint-aspmanagedetail.png
[8]: ./media/web-sites-integrate-with-vnet/vnetint-vnetp2s.png

<!--Links-->
[VNETOverview]: http://azure.microsoft.com/documentation/articles/virtual-networks-overview/ 
[AzurePortal]: http://portal.azure.com/
[ASPricing]: http://azure.microsoft.com/pricing/details/app-service/
[VNETPricing]: http://azure.microsoft.com/pricing/details/vpn-gateway/
[DataPricing]: http://azure.microsoft.com/pricing/details/data-transfers/
[V2VNETP2S]: http://azure.microsoft.com/documentation/articles/vpn-gateway-howto-point-to-site-rm-ps/
[IntPowershell]: http://azure.microsoft.com/documentation/articles/app-service-vnet-integration-powershell/
[ASEintro]: http://docs.microsoft.com/azure/app-service/app-service-environment/intro
[ILBASE]: http://docs.microsoft.com/azure/app-service/app-service-environment/create-ilb-ase
[V2VNETPortal]: https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal
[VPNERCoex]: http://docs.microsoft.com/en-us/azure/expressroute/expressroute-howto-coexist-resource-manager
[ASE]: http://docs.microsoft.com/azure/app-service/app-service-environment/intro
