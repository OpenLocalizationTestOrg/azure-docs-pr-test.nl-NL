---
title: 'Voorbeeld: aaaDMZ bouwen een DMZ tooProtect netwerken met een Firewall, UDR en NSG | Microsoft Docs'
description: Maken van een DMZ met een Firewall, de gebruiker gedefinieerde Routering en Netwerkbeveiligingsgroepen (NSG)
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: dc01ccfb-27b0-4887-8f0b-2792f770ffff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: jonor;sivae
ms.openlocfilehash: cc121f9cd5fe3c3e9ac2c70fbb7d982a80bb345d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="example-3--build-a-dmz-tooprotect-networks-with-a-firewall-udr-and-nsg"></a>Voorbeeld 3: een DMZ tooProtect bouwen netwerken met een Firewall, UDR en NSG
[Best Practices beveiligingspagina-grens toohello retourneren][HOME]

In dit voorbeeld wordt een DMZ gemaakt met een firewall, vier windows-servers, gebruiker gedefinieerde routering, doorsturen via IP en Netwerkbeveiligingsgroepen. Deze ook begeleidt bij elk Hallo relevante opdrachten tooprovide een beter begrip van elke stap. Er is ook een verkeer Scenario sectie tooprovide een gedetailleerd stapsgewijs hoe verkeer wordt voortgezet via Hallo lagen verdediging in Hallo DMZ. Ten slotte is in de sectie Verwijzingen Hallo de volledige code Hallo en instructie toobuild deze omgeving tootest en het experiment met verschillende scenario's. 

![Bidirectionele DMZ met NVA, NSG en UDR][1]

## <a name="environment-setup"></a>Instellen van de omgeving
In dit voorbeeld is er een abonnement dat Hallo volgende bevat:

* Drie cloudservices: 'SecSvc001', 'FrontEnd001' en 'BackEnd001'
* Een virtueel netwerk 'CorpNetwork' met drie subnetten: 'SecNet', 'FrontEnd' en back-end'
* Een virtueel netwerkapparaat, in dit voorbeeld van een firewall, verbonden toohello SecNet subnet
* Een Windows-Server waarmee een toepassing webserver ('IIS01')
* Twee windows-servers die toepassing terug vertegenwoordigen end servers ('AppVM01', 'AppVM02')
* Een Windows-server met een DNS-server ('DNS01')

In onderstaande Hallo verwijzingen gedeelte is er een PowerShell-script dat de meeste Hallo-omgeving die hierboven worden beschreven bouwt. Gebouw Hallo VM's en virtuele netwerken worden Hoewel worden uitgevoerd door Hallo voorbeeldscript wordt niet in dit document uitvoeriger beschreven.

toobuild hello omgeving:

1. Hallo netwerk config XML-bestand is opgenomen in de sectie Verwijzingen hello (bijgewerkt met de naam, locatie en IP-adressen toomatch Hallo gegeven scenario) opslaan
2. Update Hallo Gebruikersvariabelen in Hallo script toomatch Hallo omgeving Hallo script is toobe uitgevoerd (abonnementen, servicenamen, enzovoort)
3. Hallo-script uitvoeren in PowerShell

**Opmerking**: Hallo regio aangegeven in Hallo PowerShell-script moet overeenkomen met de Hallo regio in xml-configuratiebestand met Hallo netwerk aangegeven.

Zodra het Hallo-script wordt uitgevoerd kan Hallo na script stappen kan worden genomen:

1. Hallo-firewallregels instellen, deze procedure wordt besproken in Hallo onderstaande sectie met de titel: Beschrijving van de Firewall-regel.
2. Optioneel zijn in de sectie Verwijzingen Hallo twee scripts tooset up Hallo-webserver en appserver met een eenvoudige web application tooallow testen met deze configuratie DMZ.

Zodra het Hallo-script is uitgevoerd Hallo firewallregels moet toobe voltooid, moet deze procedure wordt besproken in het gedeelte Hallo: Firewall-regels.

## <a name="user-defined-routing-udr"></a>Door de gebruiker gedefinieerde Routering
Standaard worden Hallo na systeemroutes gedefinieerd als:

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.0.0/16}     VNETLocal                            Active   Default    
         {0.0.0.0/0}       Internet                             Active   Default    
         {10.0.0.0/8}      Null                                 Active   Default    
         {100.64.0.0/10}   Null                                 Active   Default    
         {172.16.0.0/12}   Null                                 Active   Default    
         {192.168.0.0/16}  Null                                 Active   Default

Hallo VNETLocal is altijd Hallo gedefinieerd adres prefix(en) Hallo VNet voor die specifieke netwerk (ie wordt gewijzigd van VNet tooVNet, afhankelijk van hoe elke specifieke VNet is gedefinieerd). Hallo resterende systeemroutes zijn statisch en standaard als hierboven.

Als voor de prioriteit, routes worden verwerkt via Hallo langste voorvoegsel overeen (LPM)-methode, dus hello meest specifiek route in de tabel Hallo zou gelden tooa gegeven doeladres.

Verkeer (bijvoorbeeld toohello DNS01 server, 10.0.2.4) bedoeld voor LAN hello (10.0.0.0/16) zouden daarom worden gerouteerd via Hallo VNet tooits bestemming vanwege toohello 10.0.0.0/16 route. Met andere woorden, voor 10.0.2.4 is Hallo 10.0.0.0/16 route het meest specifiek route hello, hoewel Hallo 10.0.0.0/8 en 0.0.0.0/0 ook kunnen toegepast, maar omdat deze minder specifiek zijn ze niet op dit verkeer. Hallo verkeer too10.0.2.4 zou daarom de volgende hop Hallo lokale VNet en gewoon routeren toohello doel hebben.

Als verkeer is bedoeld voor 10.1.1.1 bijvoorbeeld, Hallo 10.0.0.0/16 route toepassen wouldn't, maar Hallo 10.0.0.0/8 Hallo meest specifiek zijn zou en dit verkeer Hallo zou worden verwijderd ('zwart gaan') omdat de volgende hop Hallo Null is. 

Als bestemming Hallo tooany van Hallo Null voorvoegsels of Hallo VNETLocal voorvoegsels niet toepassen en klik vervolgens het minst specifiek Hallo volgt routeren, 0.0.0.0/0 en toohello Internet, zoals de volgende hop Hallo en dus uit de rand van de Azure internet worden doorgestuurd.

Als er twee identieke voorvoegsels in de routetabel hello, volgt Hallo Hallo-volgorde van voorkeur op basis van Hallo routes 'bron'-kenmerk:

1. 'VirtualAppliance' een door de gebruiker gedefinieerde handmatig toegevoegde toohello routetabel =
2. 'VPNGateway' een dynamische Route BGP (gebruikt in combinatie met hybride netwerken), = toegevoegd door een dynamische netwerkprotocol, deze routes kunnen op den duur veranderen als dynamische Hallo-protocol wordt automatisch in het netwerk als peer is ingesteld aangepast
3. 'Standaard' hello Systeemroutes, = Hallo lokale VNet en Hallo statische vermeldingen, zoals wordt weergegeven in de routetabel Hallo hierboven.

> [!NOTE]
> U kunt nu de gebruiker gedefinieerde routering (UDR) gebruiken met ExpressRoute- en VPN-Gateways tooforce uitgaande en binnenkomende cross-premises verkeer toobe gerouteerde tooa netwerk virtueel apparaat (NVA).
> 
> 

#### <a name="creating-hello-local-routes"></a>Hallo maken lokale routes
In dit voorbeeld worden twee routeringstabellen nodig, één voor Hallo front-end- en back-end-subnetten. Elke tabel is geladen met statische routes die geschikt is voor Hallo opgegeven subnet. Voor Hallo doel van dit voorbeeld heeft elke tabel drie routes:

1. Lokaal subnetverkeer geen volgende Hop gedefinieerd tooallow lokale subnet verkeer toobypass Hallo firewall
2. Virtueel netwerkverkeer met een volgende Hop gedefinieerd als een firewall, overschrijft dit Hallo standaardregel waarmee lokale tooroute voor VNet-verkeer rechtstreeks
3. Alle resterende verkeer (0/0) met de volgende Hop gedefinieerd als een firewall Hallo

Ze zijn gebonden tootheir subnetten als Hallo routeringstabellen zijn gemaakt. Voor Hallo Frontend subnet routeringstabel nadat gemaakt en gekoppeld ziet toohello subnet er als volgt:

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.1.0/24}     VNETLocal                            Active 
         {10.0.0.0/16}     VirtualAppliance 10.0.0.4            Active    
         {0.0.0.0/0}       VirtualAppliance 10.0.0.4            Active


Hallo volgende opdrachten in dit voorbeeld gebruikte toobuild Hallo routetabel zijn, een door de gebruiker gedefinieerde route toevoegen en vervolgens binden Hallo route tabel tooa subnet (Opmerking; de items onder die begint met een dollarteken (bijvoorbeeld: $BESubnet) zijn van de gebruiker gedefinieerde variabelen uit het Hallo-script in Hallo verwijzing sectie van dit document):

1. Eerste Hallo base routeringstabel moet worden gemaakt. Dit fragment toont Hallo maken van Hallo tabel voor Hallo back-end-subnet. Hallo-script wordt ook een bijbehorende tabel gemaakt voor Hallo Frontend subnet.
   
     Nieuwe AzureRouteTable-naam $BERouteTableName '
   
         -Location $DeploymentLocation `
         -Label "Route table for $BESubnet subnet"
2. Zodra de routetabel Hallo is gemaakt, kunnen specifieke gebruiker gedefinieerde routes worden toegevoegd. In deze snipped worden al het verkeer (0.0.0.0/0) gerouteerd via Hallo virtueel apparaat (een variabele, $VMIP [0], is de gebruikte toopass Hallo IP-adres is toegewezen als virtueel apparaat Hallo eerder in Hallo-script is gemaakt). In Hallo-script wordt een bijbehorende regel ook in Hallo Frontend tabel gemaakt.
   
     Get-AzureRouteTable $BERouteTableName | `
   
         Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
         -NextHopType VirtualAppliance `
         -NextHopIpAddress $VMIP[0]
3. Hallo boven route item overschrijft de standaardroute '0.0.0.0/0' hello, maar Hallo 10.0.0.0/16 standaardregel nog steeds bestaande zou waarmee verkeer binnen Hallo VNet tooroute rechtstreeks toohello doel en niet toohello virtueel netwerkapparaat. toocorrect die dit gedrag Hallo Volg regel moet worden toegevoegd.
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
4. Er is op dit moment een toobe keuze is gemaakt. Hello hierboven twee routes wordt al het verkeer routeren toohello firewall voor de beoordeling, zelfs verkeer binnen één subnet. Dit kan nodig zijn, maar tooallow verkeer binnen een subnet tooroute lokaal zonder betrokkenheid van Hallo firewall een derde, zeer specifieke regel kan worden toegevoegd. Deze route statussen van een adres voor het lokale subnet Hallo kunt just destine routeren er rechtstreeks (NextHopType = VNETLocal).
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
5. Ten slotte met Hallo routeringstabel gemaakt en gevuld met een gebruiker gedefinieerde routes, moet Hallo tabel nu zijn gebonden tooa subnet. Hallo-front-end-routetabel is in Hallo-script wordt ook afhankelijke toohello subnet Frontend. Hier volgt Hallo binding script voor Hallo back-end-subnet.
   
     Set-AzureSubnetRouteTable - VirtualNetworkName $VNetName '
   
        -SubnetName $BESubnet `
        -RouteTableName $BERouteTableName

## <a name="ip-forwarding"></a>Doorsturen via IP
Een tooUDR companion-functie is doorsturen via IP. Dit is een instelling in een virtueel apparaat waarmee het tooreceive verkeer niet specifiek gericht toohello toestel en vervolgens doorsturen die verkeer tooits uiteindelijke bestemming.

Bijvoorbeeld als een aanvraag toohello DNS01 server, kunt u verkeer van AppVM01 zou UDR routeren deze toohello-firewall. Met doorsturen via IP is ingeschakeld, wordt het verkeer Hallo voor Hallo DNS01 doel (10.0.2.4) worden geaccepteerd door Hallo toestel (10.0.0.4) en vervolgens doorgestuurd tooits uiteindelijke bestemming (10.0.2.4). Zonder doorsturen via IP ingeschakeld op Hallo Firewall, zou verkeer niet geaccepteerd door Hallo toestel Hoewel routetabel Hallo Hallo firewall als Hallo volgende hop is. 

> [!IMPORTANT]
> Het is essentieel tooremember tooenable doorsturen via IP in combinatie met de gebruiker gedefinieerde routering.
> 
> 

Instellen van het doorsturen via IP is één opdracht en kan worden uitgevoerd tijdens de aanmaak van virtuele machine. Voor Hallo stroom van dit voorbeeld Hallo-codefragment aan Hallo einde van het Hallo-script en gegroepeerd met Hallo UDR opdrachten:

1. Bellen Hallo VM-instantie die uw virtuele apparaat, firewall in dit geval Hallo en doorsturen via IP inschakelen (Opmerking; een item in rood die begint met een dollarteken (bijvoorbeeld: $VMName[0]) is een door de gebruiker gedefinieerde variabele uit het Hallo-script in Hallo verwijzing sectie van dit document. Hallo nul vierkante haken, [0], vertegenwoordigt Hallo eerste VM in Hallo-matrix van virtuele machines, voor Hallo voorbeeld script toowork zonder aanpassingen, eerste VM (VM 0) moet Hallo Hallo firewall):
   
     Get-AzureVM-naam $VMName [0] - ServiceName $ServiceName [0] | `
   
        Set-AzureIPForwarding -Enable

## <a name="network-security-groups-nsg"></a>Netwerkbeveiligingsgroepen (NSG's)
In dit voorbeeld is een groep NSG gebouwd en vervolgens geladen met een enkele regel. Deze groep wordt vervolgens gebonden alleen toohello Frontend en Backend subnetten (geen hello SecNet). Declaratief wordt Hallo-regel samengesteld:

1. Verkeer (alle poorten) van Hallo Internet toohello hele VNet (alle subnetten) is geweigerd.

Hoewel het nsg's in dit voorbeeld worden gebruikt, worden de belangrijkste doel is als een laag secundaire beveiliging tegen handmatige onjuiste configuratie. We willen tooblock alle binnenkomend verkeer van Hallo internet tooeither Hallo Frontend of back-end-subnetten, verkeer mag alleen door Hallo SecNet subnet toohello firewall stromen (en vervolgens van toepassing op toohello front-end of back-end subnetten). Bovendien met Hallo UDR regels aanwezig is, zou verkeer om het in Hallo front-end of back-end subnetten worden omgeleid uit toohello firewall (Bedankt tooUDR). Hallo firewall zou dit zien als een asymmetrische stroom en uitgaand verkeer hello wilt verwijderen. Dus zijn er drie lagen beveiliging beschermen Hallo Frontend en Backend subnetten; 1) er is geen open eindpunten op Hallo FrontEnd001 en BackEnd001 cloudservices, 2) nsg's weigeren verkeer vanaf Internet, 3) Hallo firewall neer te zetten asymmetrische verkeer Hallo.

Een interessant punt met betrekking tot Hallo Netwerkbeveiligingsgroep in dit voorbeeld is dat deze slechts één regel, die bevat hieronder worden weergegeven die toodeny internet verkeer toohello gehele virtuele netwerk waaronder Hallo beveiliging subnet. 

    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet `
        from hello Internet" `
        -Type Inbound -Priority 100 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *

Echter, aangezien Hallo NSG alleen wordt gekoppeld toohello Frontend en Backend subnetten, Hallo regel is niet verwerkt op het verkeer inkomend toohello beveiliging subnet. Als gevolg hiervan Hoewel Hallo NSG regel geen adres Internet verkeer tooany op Hallo VNet, staat omdat NSG nooit is Hallo toohello beveiliging subnet gebonden, stromen verkeer toohello beveiliging subnet.

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $FESubnet -VirtualNetworkName $VNetName

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $BESubnet -VirtualNetworkName $VNetName

## <a name="firewall-rules"></a>Firewallregels
Regels voor doorsturen moet toobe gemaakt op Hallo-firewall. Omdat Hallo-firewall geblokkeerd of doorsturen van alle binnenkomende, uitgaande en intra-VNet-verkeer is worden veel firewallregels vereist. Alle binnenkomend verkeer bereikt ook Hallo beveiligingsservice openbaar IP-adres (op verschillende poorten) toobe verwerkt door Hallo firewall. Een aanbevolen procedure is toodiagram Hallo logische stromen voordat u Hallo subnetten en firewall-regels tooavoid dubbel later instelt. Hallo is volgende afbeelding een logische weergave van de firewallregels Hallo voor dit voorbeeld:

![Logische weergave van Hallo Firewall-regels][2]

> [!NOTE]
> Op basis van Hallo die virtueel netwerkapparaat gebruikt, variëren Hallo beheerpoorten. In dit voorbeeld wordt verwezen naar een Barracuda NextGen Firewall gebruikt die poort 22, 801 en 807. Raadpleeg Hallo toestel leverancier documentatie toofind Hallo exacte poorten die worden gebruikt voor het beheer van Hallo-apparaat wordt gebruikt.
> 
> 

### <a name="logical-rule-description"></a>Beschrijving van de logische regel
In Hallo logisch diagram bovenstaande Hallo beveiliging subnet niet weergegeven omdat Hallo firewall Hallo enige resource in dat subnet is, en dit diagram Hallo firewallregels en hoe ze logisch toestaan of verkeersstromen en niet Hallo werkelijke gerouteerde pad weigeren wordt weergegeven. Ook Hallo externe poorten geselecteerd voor Hallo RDP-verkeer hoger varieerde poorten (8014 – 8026) zijn en zijn geselecteerde toosomewhat zijn afgestemd op Hallo van laatste twee octetten van het lokale IP-adres voor een eenvoudiger leesbaarheid Hallo (bijvoorbeeld 10.0.1.4-adres van de lokale server is gekoppeld externe poort 8014), maar een hogere poorten voor niet-conflicterende kunnen worden gebruikt.

Bijvoorbeeld, moeten we 7 typen regels, deze regeltypen worden als volgt beschreven:

* Externe regels (voor inkomend verkeer):
  1. Firewallregel voor beheer: Met deze regel omleidings-App kunt verkeer toopass toohello beheerpoorten van virtueel netwerkapparaat Hallo.
  2. RDP-regels (voor elke WindowsServer): deze vier regels (één voor elke server) wordt toestaan van beheer van Hallo afzonderlijke servers via RDP. Dit kan ook worden gebundeld in één regel, afhankelijk van de mogelijkheden Hallo Hallo virtueel netwerkapparaat wordt gebruikt.
  3. Verkeersregels voor toepassing: Er zijn twee regels voor het netwerkverkeer van toepassing hello eerst voor Hallo-front-end-webverkeer en Hallo tweede voor verkeer van de back-end hello (bijvoorbeeld web server toodata laag). Hallo-configuratie van deze regels, is afhankelijk van Hallo netwerkarchitectuur (waar uw servers worden geplaatst) en verkeersstromen (welke richting Hallo-verkeersstromen en welke poorten worden gebruikt).
     * de eerste regel Hallo kunt Hallo werkelijke toepassing verkeer tooreach Hallo-toepassingsserver. Hallo andere regels toestaan voor de beveiliging, beheer, enz., zijn toepassing regels wat externe gebruikers of services tooaccess Hallo toepassing(en) toestaan. In dit voorbeeld is er één webserver op poort 80, dus één firewallregel toepassing binnenkomend verkeer toohello extern IP-adres, toohello web servers interne IP-adres worden omgeleid. Hallo omgeleid verkeer sessie zou worden NAT gehad toohello interne serverfout.
     * tweede regel voor het netwerkverkeer van toepassing is Hallo Hallo back-end regel tooallow Hallo webserver tootalk toohello AppVM01 server (maar niet AppVM02) via een willekeurige poort.
* Interne regels (voor intra-VNet-verkeer)
  1. Regel voor uitgaande tooInternet: met deze regel kan verkeer van een netwerk toopass toohello geselecteerd netwerken. Deze regel is meestal een standaardregel al op Hallo firewall, maar in een uitgeschakelde status. Deze regel moet worden ingeschakeld voor dit voorbeeld.
  2. DNS-regel: Met deze regel kunnen alleen DNS (poort 53)-verkeer toopass toohello DNS-server. Voor deze omgeving die Hallo Frontend toohello back-end meeste verkeer wordt geblokkeerd, kan deze regel specifiek DNS van een lokale subnet.
  3. Subnet tooSubnet regel: deze regel is tooallow een willekeurige server op Hallo achterkant subnet tooconnect tooany server op Hallo front-end-subnet beëindigen (maar niet Hallo omgekeerde).
* Foutveilige regel (voor verkeer dat niet voldoet aan alle bovenstaande Hallo):
  1. Alle Verkeersregel voor weigeren: Dit moet altijd de laatste regel hello (in termen van prioriteit), en als zodanig als een van de verkeersstromen mislukt toomatch van Hallo voorafgaand aan de regels die het door deze regel wordt verwijderd. Dit is een standaardregel en meestal geactiveerd, worden er zijn geen wijzigingen in het algemeen nodig.

> [!TIP]
> Een willekeurige poort is toegestaan voor dit voorbeeld eenvoudig op Hallo tweede toepassing verkeersregel, in een echte scenario Hallo meest specifiek poort en bereiken gebruikte tooreduce Hallo kwetsbaarheid voor aanvallen van deze regel moeten worden.
> 
> 

<br />

> [!IMPORTANT]
> Zodra alle Hallo hierboven regels zijn gemaakt, is het belangrijk tooreview Hallo prioriteit van elke regel tooensure-verkeer wordt toegestaan of geweigerd desgewenst. In dit voorbeeld zijn Hallo regels in volgorde van prioriteit. Het is gemakkelijk toobe Hallo firewall vanwege toomis besteld regels vergrendeld. Zorg ervoor Hallo beheer voor Hallo firewall zelf is altijd Hallo absolute hoogste prioriteit regel minimaal.
> 
> 

### <a name="rule-prerequisites"></a>Regel voor vereisten
Een vereiste voor Hallo virtuele Machine actief Hallo firewall openbare eindpunten is. Voor Hallo firewall tooprocess verkeer moet de juiste openbare eindpunten Hallo openen. Er zijn drie typen verkeer in dit voorbeeld; 1) management verkeer toocontrol Hallo firewall en firewall-regels, 2) de RDP-verkeer toocontrol Hallo windows-servers en toepassing 3)-verkeer. Dit zijn drie kolommen van de verkeerstypen in het bovenste Hallo Hallo helft van de logische weergave van de firewallregels Hallo hierboven.

> [!IMPORTANT]
> Een sleutel takeway hier is tooremember die **alle** verkeer via de firewall hello wordt geleverd. In dat geval tooremote bureaublad toohello IIS01 server, zelfs als het in Hallo Front-End-Cloudservice en op Hallo front-end-subnet, tooaccess deze server moeten we tooRDP toohello firewall op poort 8014 en laat Hallo firewall tooroute Hallo RDP aanvraag intern toohello IIS01 RDP-poort. Hello Azure portal 'Connect' knop werkt niet omdat er geen directe RDP pad tooIIS01 (zo ver mogelijk Hallo portal kunt zien). Dit betekent dat alle verbindingen op Hallo internet moet worden toohello Security-Service en een poort, bijvoorbeeld secscv001.cloudapp.net:xxxx (verwijzing hello hierboven diagram voor Hallo toewijzing van de externe poort en intern IP-adres en poort).
> 
> 

Een eindpunt kan worden geopend op Hallo-tijd van het maken van VM- of build boekt als is gedaan in Hallo voorbeeldscript en hieronder wordt weergegeven in dit codefragment (Opmerking; een item die begint met een dollarteken (bijvoorbeeld: $VMName[$i]) is een door de gebruiker gedefinieerde variabele uit het script in Hallo referen Hallo CE-sectie van dit document. Hallo '$i' vierkante haken, [$i] Hallo matrix aantal vertegenwoordigt een specifieke virtuele machine in een matrix van virtuele machines):

    Add-AzureEndpoint -Name "HTTP" -Protocol tcp -PublicPort 80 -LocalPort 80 `
        -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | `
        Update-AzureVM

Hoewel het niet duidelijk hier weergegeven vanwege toohello gebruik van variabelen, maar eindpunten zijn **alleen** geopend op Hallo Security Cloud-Service. Dit is dat alle binnenkomend verkeer wordt verwerkt tooensure (gerouteerd, NAT waren, verloren) door Hallo firewall.

Een Beheerclient toobe geïnstalleerd op een PC toomanage Hallo firewall nodig hebt en Hallo configuraties nodig maken. Zie de leverancier van de documentatie van uw firewall (of andere NVA) Hallo over hoe toomanage apparaat Hallo. Hallo rest van deze sectie en de volgende sectie hello, Firewall-regels maken, bevat een beschrijving van Hallo configuratie van Hallo firewall zelf, via Hallo leveranciers management-client (d.w.z. niet hello Azure-portal of PowerShell).

Instructies voor het downloaden van de client en verbindende toohello Barracuda gebruikt in dit voorbeeld vindt u hier: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)

Zodra u aangemeld bent op Hallo firewall, maar voordat u firewallregels maken, zijn er twee vereiste objectklassen waardoor maken Hallo regels gemakkelijker; Netwerk- en Service-objecten.

In dit voorbeeld moet drie benoemde netwerkobjecten gedefinieerd (een voor Hallo Frontend subnet en Hallo-subnet voor back-end, ook een netwerkobject voor Hallo IP-adres van Hallo DNS-server). toocreate een benoemde netwerk. vanaf Hallo Barracuda NG Admin client dashboard, tabblad toohello-configuratie te navigeren, in Hallo operationele configuratiesectie Ruleset, vervolgens klikt u op "Netwerken" onder Hallo Firewallobjecten menu, klik op Nieuw in Hallo bewerken netwerken menu. Hallo-netwerkobject kan nu worden gemaakt, door toe te voegen Hallo naam en het Hallo-voorvoegsel:

![Een Object FrontEnd-netwerk maken][3]

Hiermee maakt u een benoemde netwerk voor Hallo FrontEnd subnet, een vergelijkbaar object Hallo subnet BackEnd ook moet worden gemaakt. Hallo-subnetten kunnen nu gemakkelijker verwezen met de naam in de firewallregels Hallo.

Hallo voor DNS-Server-Object:

![Een DNS-Server-Object maken][4]

Deze één verwijzing naar een IP-adres wordt gebruikt in een DNS-regel verderop in document Hallo.

Hallo tweede vereiste objecten zijn Services objecten. Deze vertegenwoordigt Hallo RDP verbindingspoorten voor elke server. Omdat bestaande RDP-serviceobject Hallo gebonden toohello standaard RDP-poort, kunnen 3389, nieuwe Services worden gemaakt tooallow verkeer van externe Hallo-poorten (8014 8026). de nieuwe poorten Hallo kunnen ook worden toegevoegd toohello bestaande RDP-service, maar voor een eenvoudige demonstratie een afzonderlijke regel voor elke server kan worden gemaakt. toocreate een nieuwe RDP-regel voor een server. tabblad van de configuratie toohello hello Barracuda NG Admin client dashboard vanaf navigeren, Hallo operationele configuratie sectie Ruleset, klikt u op en klik op 'Services' onder Hallo Firewallobjecten menu, schuif omlaag Hallo lijst met services en selecteer Hallo 'RDP' service. Met de rechtermuisknop op en selecteert u kopiëren, en vervolgens met de rechtermuisknop op en selecteer plakken. Er is nu een RDP-Copy1-Object dat kan worden bewerkt. Met de rechtermuisknop op de RDP-Copy1 en selecteer bewerken, Hallo bewerken serviceobject pop-up venster wordt als volgt te werk:

![Kopie van de standaardregel voor RDP][5]

Hallo-waarden kunnen vervolgens worden bewerkte toorepresent Hallo RDP-service voor een specifieke server. RDP-regel moet voor AppVM01 Hallo hierboven standaard gewijzigde tooreflect een nieuwe Service-naam, beschrijving, en externe RDP-poort die worden gebruikt in Hallo afbeelding 8 diagram (Opmerking: Hallo poorten zijn gewijzigd van Hallo RDP 3389 toohello externe poort die wordt gebruikt voor deze standaardwaarde specifieke server, in geval van AppVM01 Hallo externe poort Hallo is 8025) hello gewijzigde service worden hieronder weergegeven:

![AppVM01 regel][6]

Dit proces moet worden herhaald toocreate RDP-Services voor Hallo resterende servers. AppVM02, DNS01 en IIS01. Hallo maken van deze Services maakt Hallo regel maken eenvoudiger en duidelijker in de volgende sectie Hallo.

> [!NOTE]
> Een RDP-service voor Hallo Firewall is niet nodig om twee redenen; 1) de eerste Hallo firewall VM is een installatiekopie op basis van Linux zodat SSH wordt gebruikt op poort 22 voor VM-management in plaats van RDP en 2)-poort 22 en twee andere poorten zijn toegestaan in Hallo eerste management regel hieronder tooallow voor connectiviteit van het beheer beschreven.
> 
> 

### <a name="firewall-rules-creation"></a>Firewall-regels maken
Er zijn drie soorten firewallregels die in dit voorbeeld gebruikt, alle hebben verschillende pictogrammen:

Hallo toepassing omleiden regel: ![toepassing omleidings-pictogram][7]

Hallo bestemming NAT-regel: ![bestemming NAT-pictogram][8]

Hallo Pass regel: ![pictogram doorgeven][9]

U vindt meer informatie over deze regels op Hallo Barracuda-website.

toocreate Hallo regels (of Controleer of de bestaande standaardregels), vanaf Hallo Barracuda NG Admin client dashboard, navigeer toohello configuratie tabblad, in Hallo operationele configuratie sectie Ruleset klikt u op. Een raster aangeroepen, wordt 'Main regels' hello bestaande actieve en gedeactiveerd regels op deze firewall weergegeven. Hallo rechterbovenhoek van dit raster is een klein, groene '+' knop, klikt u op deze toocreate een nieuwe regel (Opmerking: uw firewall mogelijk 'vergrendeld' om wijzigingen, als er een knop 'Vergrendelen' gemarkeerd en kan niet toocreate zijn of regels bewerken, klikt u op deze knop te regel se 'ontgrendelen' Hallo t en bewerken). Als u een bestaande regel tooedit wilt, selecteert u deze regel, met de rechtermuisknop op en selecteer regel bewerken.

Zodra uw regels zijn gemaakt en/of gewijzigd, moeten ze toohello firewall gepusht en vervolgens geactiveerd, als dit niet gebeurt Hallo regel wijzigingen pas van kracht. Hallo push en activering proces wordt hieronder Hallo details regelbeschrijvingen beschreven.

Hallo-details van elke regel vereist toocomplete in dit voorbeeld als volgt worden beschreven:

* **Firewall-regel Management**: deze App omleiden regel staat toe dat verkeer toopass toohello beheerpoorten van Hallo virtueel netwerkapparaat, in dit voorbeeld een Barracuda NextGen Firewall. Hallo management poorten zijn 801, 807 en eventueel 22. Hallo interne en externe poorten zijn Hallo dezelfde (d.w.z. geen poortvertaling). Deze regel, SETUP-MGMT-toegang, is een standaardregel en (in Barracuda NextGen Firewall versie 6.1) standaard ingeschakeld.
  
    ![Firewallregel Management][10]

> [!TIP]
> Hello bron-adresruimte in deze regel is, als hello management IP-adresbereiken bekend zijn, waardoor dit bereik Hallo aanval surface toohello beheerpoorten ook sneller.
> 
> 

* **Regels voor RDP**: deze bestemming NAT-regels kunnen beheer van Hallo afzonderlijke servers via RDP.
  Er zijn vier kritieke velden nodig toocreate met deze regel:
  
  1. Bron: tooallow RDP vanaf elke locatie, Hallo verwijzing 'Any' in veld Hallo-bron gebruikt.
  2. Service – juiste serviceobject eerder hebt gemaakt, in dit geval 'AppVM01 RDP' hello gebruiken, externe poorten Hallo omleiden toohello servers lokale IP-adres en tooport 3386 (Hallo standaard RDP-poort). Deze specifieke regel is voor RDP toegang tooAppVM01.
  3. Doel – moet Hallo *lokale poort op Hallo firewall*, 'DCHP 1 lokale IP-' of eth0 als statische IP-adressen. Hallo rangtelwoord (eth0, eth1, enzovoort) is mogelijk anders als uw netwerkapparaat meerdere lokale interfaces heeft. Dit is de poort Hallo Hallo firewall verstuurt uit (mogelijk dezelfde als de poort ontvangen Hallo Hallo), werkelijke gerouteerde bestemming Hallo Hallo doellijst veld is.
  4. Omleiding – dit gedeelte wordt uitgelegd Hallo virtueel apparaat waar tooultimately dit verkeer worden omgeleid. de eenvoudigste omleiding Hallo is tooplace Hallo IP- en poort (optioneel) in Hallo doellijst veld. Als er geen poort gebruikte Hallo doelpoort op Hallo binnenkomende aanvraag (ie geen vertaling) gebruikt als een poort is aangewezen Hallo poort worden ook NAT zou samen met de Hallo IP adres.
     
     ![RDP-firewallregel][11]
     
     Een totaal van vier RDP-regels nodig toobe gemaakt: 
     
     | Regelnaam | Server | Service | Lijst met doelservers |
     | --- | --- | --- | --- |
     | RDP-naar-IIS01 |IIS01 |IIS01 RDP |10.0.1.4:3389 |
     | RDP-naar-DNS01 |DNS01 |DNS01 RDP |10.0.2.4:3389 |
     | RDP-naar-AppVM01 |AppVM01 |AppVM01 RDP |10.0.2.5:3389 |
     | RDP-naar-AppVM02 |AppVM02 |AppVm02 RDP |10.0.2.6:3389 |

> [!TIP]
> Beperking Hallo bereik van Hallo bron en de velden van de Service beperkt Hallo kwetsbaarheid voor aanvallen. Hallo meest beperkt bereik die zorgen de functionaliteit dat ervoor moet worden gebruikt.
> 
> 

* **Toepassing verkeersregels**: Er zijn twee regels voor het netwerkverkeer van toepassing, Hallo eerst voor Hallo-front-end-webverkeer en Hallo tweede voor verkeer van de back-end hello (bijvoorbeeld web server toodata laag). Deze regels, is afhankelijk van Hallo netwerkarchitectuur (waar uw servers worden geplaatst) en verkeersstromen (welke richting Hallo-verkeersstromen en welke poorten worden gebruikt).
  
    Eerst besproken is Hallo-front-end-regel voor internetverkeer:
  
    ![Web-firewallregel][12]
  
    Deze bestemming NAT-regel staat toe Hallo werkelijke verkeer tooreach Hallo toepassing toepassingsserver. Hallo andere regels toestaan voor de beveiliging, beheer, enz., zijn toepassing regels wat externe gebruikers of services tooaccess Hallo toepassing(en) toestaan. In dit voorbeeld is er één webserver op poort 80, dus één firewallregel toepassing hello binnenkomend verkeer toohello extern IP-adres, toohello web servers interne IP-adres worden omgeleid.
  
    **Opmerking**: dat er is geen poort toegewezen in Hallo doellijst veld, dus hello binnenkomende poort 80 (of 443 voor Hallo Service geselecteerd) wordt gebruikt in Hallo omleiding van Hallo-webserver. Als de webserver Hallo luistert op een andere poort, bijvoorbeeld poort 8080, Hallo doellijst veld bijgewerkte too10.0.1.4:8080 tooallow voor Hallo poort ook omleiding kan worden.
  
    Hallo volgende Verkeersregel van toepassing is Hallo back-end regel tooallow Hallo webserver tootalk toohello AppVM01 server (maar niet AppVM02) via elke service:
  
    ![AppVM01 firewallregel][13]
  
    Deze regel op te geven kunnen IIS-server op Hallo Frontend subnet tooreach hello AppVM01 (IP-adres 10.0.2.5) op een willekeurige poort Protocol tooaccess gegevens die nodig is voor de webtoepassing hello gebruiken.
  
    In deze schermafdruk een '\<expliciete-dest\>' hello bestemming in Hallo bestemming veld toosignify 10.0.2.5 wordt gebruikt. Dit kan zijn expliciete zoals wordt weergegeven of een met de naam netwerkobject (net als bij Hallo-vereisten voor Hallo DNS-server). Dit is van de beheerder van de firewall Hallo toohello toowhich methode wordt gebruikt. tooadd 10.0.2.5 als een Explict Desitnation, dubbelklik op Hallo eerste lege rij onder \<expliciete-dest\> en het Hallo-mailadres invoeren in het Hallo-venster dat wordt weergegeven.
  
    Met deze regel geeft geen NAT is nodig omdat dit is interne verkeer Hallo verbindingsmethode te kan worden ingesteld 'No snat omzetten'.
  
    **Opmerking**: Hallo Bronnetwerk in deze regel wordt een resource in het subnet FrontEnd Hallo als er wordt niet meer dan een of meer specifieke toothose exacte IP-adressen in plaats van is gemaakt toobe een bekende specifiek aantal webservers, een resource kan worden netwerkobject Hallo gehele Frontend-subnet.

> [!TIP]
> Deze regel maakt gebruik van Hallo service '' toomake Hallo voorbeeld toepassing eenvoudiger toosetup en gebruiken, ook hierdoor ICMPv4 (ping) in een enkele regel. Dit is echter niet aanbevolen. Hallo-poorten en protocollen ('Services') moet versmalling toohello minimale mogelijk waarmee de toepassing opnieuw tooreduce Hallo kwetsbaarheid voor aanvallen via deze grens.
> 
> 

<br />

> [!TIP]
> Hoewel met deze regel een verwijzing naar een expliciete-dest wordt gebruikt bevat, moet een consistente werkwijze in de firewallconfiguratie hello worden gebruikt. Het verdient aanbeveling dat met de naam netwerkobject hello worden gebruikt in de gehele voor gemakkelijker leesbaarheid en ondersteuningsmogelijkheden. Hallo expliciete-dest gebruikte hier alleen tooshow is een methode alternatieve verwijzing en wordt over het algemeen niet aanbevolen (met name voor complexe configuraties).
> 
> 

* **Regel voor uitgaande tooInternet**: doorgeven voor deze regel wordt verkeer van elke bron netwerk toopass toohello geselecteerd doelnetwerken toestaan. Deze regel is een standaardregel meestal al op Hallo Barracuda NextGen firewall, maar is uitgeschakeld. Met de rechtermuisknop op deze regel kunt Hallo activeren regel opdracht gebruiken. Hallo regel hier weergegeven is gewijzigde tooadd Hallo twee lokale subnetten die als verwijzingen in de sectie voor vereisten Hallo van dit document toohello bronkenmerk van deze regel zijn gemaakt.
  
    ![Uitgaande firewallregel][14]
* **Een DNS-regel**: deze doorgeven regel staat toe dat alleen DNS (poort 53)-verkeer toopass toohello DNS-server. Deze regel kunnen specifiek DNS voor deze omgeving die de meeste verkeer van Hallo FrontEnd toohello back-end is geblokkeerd.
  
    ![DNS-firewallregel][15]
  
    **Opmerking**: In dit scherm schermopname Hallo verbindingsmethode is opgenomen. Omdat deze regel is voor interne IP-toointernal IP-adres verkeer, geen NATing is vereist, wordt deze Hallo verbindingsmethode ingesteld te 'No snat omzetten' voor deze regel op te geven.
* **Subnet tooSubnet regel**: doorgeven voor deze regel is een standaardregel waarmee is geactiveerd en gewijzigde tooallow elke server op Hallo terug eindigt subnet tooconnect tooany server op Hallo front-end-subnet. Deze regel is alle interne verkeer dus Hallo verbindingsmethode tooNo snat omzetten kan worden ingesteld.
  
    ![Intra-VNet-firewallregel][16]
  
    **Opmerking**: Hallo bidirectionele selectievakje niet is ingeschakeld (noch is ingeschakeld in de meeste regels), dit is van belang voor deze regel maakt deze regel 'eenrichtings', een verbinding kan worden gestart vanaf Hallo back-end subnet toohello front-end-netwerk maar Hallo niet omkeren. Als dit selectievakje is ingeschakeld, zou deze regel in twee richtingen verkeer, wat van onze logisch diagram niet inschakelen.
* **Alle Verkeersregel voor weigeren**: dit moet altijd de laatste regel hello (in termen van prioriteit) en als zodanig als een verkeersstromen mislukt toomatch van Hallo regels voorafgaand aan deze verwijderd door deze regel. Dit is een standaardregel en meestal geactiveerd, worden er zijn geen wijzigingen in het algemeen nodig. 
  
    ![Regel voor weigeren van Firewall][17]

> [!IMPORTANT]
> Zodra alle Hallo hierboven regels zijn gemaakt, is het belangrijk tooreview Hallo prioriteit van elke regel tooensure-verkeer wordt toegestaan of geweigerd desgewenst. In dit voorbeeld hebben Hallo regels Hallo volgorde die in Hallo Main raster van regels in Hallo Barracuda Beheerclient doorsturen dienen te worden opgenomen.
> 
> 

## <a name="rule-activation"></a>Activering van de regel
Met de Hallo ruleset gewijzigd toohello specificatie van Hallo logica diagram Hallo ruleset moet toohello firewall geüpload en wordt geactiveerd.

![Activering van de firewall-regel][18]

In Hallo rechtsboven van Hallo Beheerclient zijn een cluster van knoppen. Hallo 'verzenden wijzigingen' knop toosend Hallo gewijzigd regels toohello firewall, klik op de knop 'Activeren' Hallo.

Deze versie van de omgeving voorbeeld is bij activering via Hallo Hallo firewall ruleSet voltooid.

## <a name="traffic-scenarios"></a>Verkeer scenario 's
> [!IMPORTANT]
> Een sleutel takeway is tooremember die **alle** verkeer via de firewall hello wordt geleverd. In dat geval tooremote bureaublad toohello IIS01 server, zelfs als het in Hallo Front-End-Cloudservice en op Hallo front-end-subnet, tooaccess deze server moeten we tooRDP toohello firewall op poort 8014 en laat Hallo firewall tooroute Hallo RDP aanvraag intern toohello IIS01 RDP-poort. Hello Azure portal 'Connect' knop werkt niet omdat er geen directe RDP pad tooIIS01 (zo ver mogelijk Hallo portal kunt zien). Dit betekent dat alle verbindingen op Hallo internet toohello Security-Service en een poort, bijvoorbeeld secscv001.cloudapp.net:xxxx moet worden.
> 
> 

Voor deze scenario's moet Hallo firewallregels volgende zijn voldaan:

1. Beheer van Firewall
2. RDP-tooIIS01
3. RDP-tooDNS01
4. RDP-tooAppVM01
5. RDP-tooAppVM02
6. App-verkeer toohello Web
7. App-verkeer tooAppVM01
8. Uitgaande toohello Internet
9. Frontend tooDNS01
10. Intra-subnetverkeer (alleen voor back-end toofront end)
11. Alles weigeren

Hallo werkelijke firewall ruleset heeft waarschijnlijk veel andere regels in een toevoeging toothese, Hallo regels op een bepaalde firewall hebben ook andere prioriteitsnummers dan Hallo toepassingsgroepen hier vermeld. Deze lijst en de bijbehorende cijfers zijn tooprovide relevantie tussen alleen deze elf regels en de relatieve prioriteit Hallo onder deze. Met andere woorden; Hallo 'RDP tooIIS01' kan op Hallo werkelijke firewall, regel getal 5, maar als deze onder Hallo 'Firewallbeheer' regel en boven Hallo 'RDP tooDNS01' regel die zou deze afgestemd op Hallo bedoeling van deze lijst is. Hallo lijst helpt ook bij Hallo onderstaande scenario's zodat beknopt alternatief bevat; bijvoorbeeld 'FW regel 9 (DNS)'. Ook als beknopt alternatief bevat, Hallo vier regels voor RDP gezamenlijk worden aangeroepen, "hello RDP regels" wanneer Hallo verkeer scenario niet-verwante tooRDP is.

Ook intrekken dat Netwerkbeveiligingsgroepen in-place voor binnenkomend internetverkeer op Hallo Frontend en Backend subnetten zijn.

#### <a name="allowed-internet-tooweb-server"></a>(Toegestaan) Internet tooWeb Server
1. Internet aanvragen HTTP-gebruikerspagina van SecSvc001.CloudApp.Net (Internet Facing Cloud Service)
2. Cloud-service geeft verkeer via open eindpunten op poort 80 toofirewall interface op 10.0.0.4:80
3. Er is geen NSG toegewezen tooSecurity subnet, zodat het NSG-Systeemregels toofirewall verkeer toestaan
4. Verkeer komt binnen via interne IP-adres van Hallo firewall (10.0.1.4)
5. Firewall begint regelverwerking:
   1. FW regel 1 (FW Mgmt) niet van toepassing, toonext regel verplaatsen
   2. FW regels (regels RDP), 2-5 niet toepassen, toonext regel verplaatsen
   3. FW regel 6 (App: Web) is van toepassing, verkeer wordt toegestaan, firewall NAT's het too10.0.1.4 (IIS01)
6. Hallo Frontend subnet begint verwerking van inkomende regel:
   1. NSG-regel 1 (Internet blokkeren) is niet van toepassing (dit verkeer is NAT zou door Hallo firewall, Hallo bronadres is dus nu Hallo firewall die zich op Hallo beveiliging subnet en zichtbaar zijn voor subnet Frontend voor Hallo NSG toobe "local" verkeer en is dus toegestaan), toonext regel verplaatsen
   2. Standaard NSG-regels toestaat subnet toosubnet verkeer, verkeer is toegestaan, stopt u de verwerking van NSG-regels
7. IIS01 luistert voor internetverkeer, ontvangt deze aanvraag en begint met de verwerking van Hallo-aanvraag
8. IIS01 probeert een FTP-sessie tooAppVM01 tooinitiates op subnet Backend
9. Hallo UDR route voor subnet Frontend maakt Hallo firewall Hallo volgende hop
10. Er is geen uitgaande regels op subnet Frontend verkeer wordt toegestaan.
11. Firewall begint regelverwerking:
    1. FW regel 1 (FW Mgmt) niet van toepassing, toonext regel verplaatsen
    2. FW regel 2-5 (RDP-regels) niet van toepassing, toonext regel verplaatsen
    3. FW regel 6 (App: Web) niet van toepassing, toonext regel verplaatsen
    4. FW regel 7 (App: back-end) is van toepassing, verkeer is toegestaan, firewall stuurt verkeer too10.0.2.5 (AppVM01)
12. Hallo back-end subnet begint verwerking van inkomende regel:
    1. NSG-regel 1 (Internet Block) niet van toepassing, toonext regel verplaatsen
    2. Standaard NSG-regels toestaat subnet toosubnet verkeer, verkeer is toegestaan, stopt u de verwerking van NSG-regels
13. AppVM01 hello aanvraag ontvangt en Hallo-sessie start en reageert
14. Hallo UDR route voor subnet Backend maakt Hallo firewall Hallo volgende hop
15. Omdat er geen uitgaande NSG-regels op Hallo antwoord Hallo van back-end-subnet is toegestaan
16. Omdat dit verkeer op retourneert een vastgestelde sessie Hallo firewall wordt doorgegeven Hallo antwoord back toohello webserver (IIS01)
17. Subnet frontend begint verwerking van inkomende regel:
    1. NSG-regel 1 (Internet Block) niet van toepassing, toonext regel verplaatsen
    2. Standaard NSG-regels toestaat subnet toosubnet verkeer, verkeer is toegestaan, stopt u de verwerking van NSG-regels
18. Hallo IIS-server Hallo antwoord wordt ontvangen, Hallo transactie met AppVM01 en daarna voltooit gebouw Hallo HTTP-antwoord, deze HTTP-antwoord verzonden toohello aanvrager
19. Omdat er geen uitgaande NSG-regels op Hallo Frontend subnet Hallo antwoord is toegestaan
20. HTTP-antwoord treffers Hallo firewall Hallo en omdat dit Hallo antwoord tooan tot stand gebracht NAT-sessie wordt geaccepteerd door de firewall Hallo
21. Hallo firewall stuurt vervolgens door Hallo antwoord back toohello Internet-gebruiker
22. Aangezien er geen uitgaande NSG-regels of UDR hops zijn op Hallo Frontend subnet antwoord Hallo is toegestaan en Hallo Internet-gebruiker ontvangt Hallo webpagina aangevraagd.

#### <a name="allowed-internet-rdp-toobackend"></a>(Toegestaan) Internet RDP tooBackend
1. RDP-sessie tooAppVM01 via SecSvc001.CloudApp.Net:8025, waarbij 8025 Hallo gebruiker toegewezen poortnummer voor de firewallregel voor 'RDP tooAppVM01' hello is serverbeheerder op internet-aanvragen
2. Hallo-cloudservice wordt doorgegeven verkeer via Hallo open eindpunten op poort 8025 toofirewall interface op 10.0.0.4:8025
3. Er is geen NSG toegewezen tooSecurity subnet, zodat het NSG-Systeemregels toofirewall verkeer toestaan
4. Firewall begint regelverwerking:
   1. FW regel 1 (FW Mgmt) niet van toepassing, toonext regel verplaatsen
   2. FW regel 2 (RDP IIS) is niet van toepassing, toonext regel verplaatsen
   3. FW regel 3 (RDP DNS01) niet van toepassing, toonext regel verplaatsen
   4. FW regel 4 (RDP AppVM01) is van toepassing, het verkeer wordt toegestaan, firewall NAT's het too10.0.2.5:3386 (RDP-poort op AppVM01)
5. Hallo back-end subnet begint verwerking van inkomende regel:
   1. NSG-regel 1 (Internet blokkeren) is niet van toepassing (dit verkeer is NAT zou door Hallo firewall, Hallo bronadres is dus nu Hallo firewall die zich op Hallo beveiliging subnet en zichtbaar zijn voor het subnet van de back-end Hallo NSG toobe "local" verkeer en is dus toegestaan), toonext regel verplaatsen
   2. Standaard NSG-regels toestaat subnet toosubnet verkeer, verkeer is toegestaan, stopt u de verwerking van NSG-regels
6. AppVM01 voor RDP-verkeer luistert en antwoordt
7. Standaardregels toepassen met geen uitgaande NSG-regels en terugkerend verkeer is toegestaan
8. UDR routes uitgaand verkeer toohello firewall als de volgende hop Hallo
9. Omdat dit verkeer op retourneert een vastgestelde sessie Hallo firewall wordt doorgegeven Hallo antwoord back toohello internet-gebruiker
10. RDP-sessie is ingeschakeld
11. AppVM01 gebruikersnaam wachtwoord gevraagd

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a>(Toegestaan) Web Server DNS-lookup op DNS-server
1. Web-Server, IIS01, moeten een gegevensfeed op www.data.gov, maar moet tooresolve Hallo adres.
2. Hallo netwerkconfiguratie voor Hallo VNet lijsten DNS01 (10.0.2.4 op Hallo back-end subnet) als het primaire DNS-server hello, IIS01 verzendt Hallo DNS-aanvraag tooDNS01
3. UDR routes uitgaand verkeer toohello firewall als de volgende hop Hallo
4. Er is geen uitgaand NSG-regels zijn gebonden toohello Frontend subnet, is verkeer toegestaan
5. Firewall begint regelverwerking:
   1. FW regel 1 (FW Mgmt) niet van toepassing, toonext regel verplaatsen
   2. FW regel 2-5 (RDP-regels) niet van toepassing, toonext regel verplaatsen
   3. FW regels 6 en 7 (App-regels) niet van toepassing, toonext regel verplaatsen
   4. FW regel 8 (tooInternet) niet van toepassing, toonext regel verplaatsen
   5. FW regel 9 (DNS) is van toepassing, verkeer is toegestaan, firewall stuurt verkeer too10.0.2.4 (DNS01)
6. Hallo back-end subnet begint verwerking van inkomende regel:
   1. NSG-regel 1 (Internet Block) niet van toepassing, toonext regel verplaatsen
   2. Standaard NSG-regels toestaat subnet toosubnet verkeer, verkeer is toegestaan, stopt u de verwerking van NSG-regels
7. DNS-server ontvangt Hallo aanvraag
8. DNS-server heeft geen Hallo-adres in de cache opgeslagen en wordt u gevraagd een basis-DNS-server op Hallo internet
9. UDR routes uitgaand verkeer toohello firewall als de volgende hop Hallo
10. Er is geen uitgaand NSG-regels op subnet Backend, verkeer is toegestaan.
11. Firewall begint regelverwerking:
    1. FW regel 1 (FW Mgmt) niet van toepassing, toonext regel verplaatsen
    2. FW regel 2-5 (RDP-regels) niet van toepassing, toonext regel verplaatsen
    3. FW regels 6 en 7 (App-regels) niet van toepassing, toonext regel verplaatsen
    4. FW regel 8 (tooInternet) is van toepassing, verkeer is toegestaan, sessie snat omzetten uit tooroot DNS-server op Hallo Internet is
12. Internet-DNS-server reageert, omdat deze sessie is gestart vanuit Hallo firewall, antwoord Hallo wordt geaccepteerd door Hallo-firewall
13. Omdat dit een vastgestelde sessie, stuurt Hallo firewall Hallo antwoord toohello initiëren DNS01-server
14. Hallo back-end subnet begint verwerking van inkomende regel:
    1. NSG-regel 1 (Internet Block) niet van toepassing, toonext regel verplaatsen
    2. Standaard NSG-regels toestaat subnet toosubnet verkeer, verkeer is toegestaan, stopt u de verwerking van NSG-regels
15. Hallo DNS-server ontvangt in de cache opgeslagen antwoord Hallo en vervolgens reageert toohello eerste aanvraag back tooIIS01
16. Hallo UDR route voor subnet backend maakt Hallo firewall Hallo volgende hop
17. Er geen uitgaande NSG-regels bestaan op Hallo back-end-subnet, is verkeer toegestaan
18. Dit is een vastgestelde sessie op Hallo firewall, antwoord Hallo wordt doorgestuurd door Hallo firewall back toohello IIS-server
19. Subnet frontend begint verwerking van inkomende regel:
    1. Er is geen NSG-regel die van toepassing tooInbound verkeer van Hallo back-end subnet toohello Frontend subnet, is zodat geen van Hallo NSG-regels toepassen
    2. Hallo system standaardregel verkeer tussen subnetten zou dit verkeer toestaan dus Hallo verkeer is toegestaan
20. IIS01 ontvangt antwoord Hallo van DNS01

#### <a name="allowed-backend-server-toofrontend-server"></a>(Toegestaan) Back-endserver server tooFrontend
1. Een beheerder is aangemeld tooAppVM02 via RDP opvraagt een bestand rechtstreeks vanaf Hallo IIS01 server via windows Verkenner
2. Hallo UDR route voor subnet Backend maakt Hallo firewall Hallo volgende hop
3. Omdat er geen uitgaande NSG-regels op Hallo antwoord Hallo van back-end-subnet is toegestaan
4. Firewall begint regelverwerking:
   1. FW regel 1 (FW Mgmt) niet van toepassing, toonext regel verplaatsen
   2. FW regel 2-5 (RDP-regels) niet van toepassing, toonext regel verplaatsen
   3. FW regels 6 en 7 (App-regels) niet van toepassing, toonext regel verplaatsen
   4. FW regel 8 (tooInternet) niet van toepassing, toonext regel verplaatsen
   5. FW regel 9 (DNS) niet van toepassing, toonext regel verplaatsen
   6. FW regel 10 (Intra-Subnet) is van toepassing, verkeer is toegestaan, firewall verkeer too10.0.1.4 (IIS01) wordt doorgegeven
5. Subnet frontend begint verwerking van inkomende regel:
   1. NSG-regel 1 (Internet Block) niet van toepassing, toonext regel verplaatsen
   2. Standaard NSG-regels toestaat subnet toosubnet verkeer, verkeer is toegestaan, stopt u de verwerking van NSG-regels
6. Als de juiste verificatie en autorisatie, IIS01 Hallo verzoek accepteert en antwoordt
7. Hallo UDR route voor subnet Frontend maakt Hallo firewall Hallo volgende hop
8. Omdat er geen uitgaande NSG-regels op Hallo Frontend subnet Hallo antwoord is toegestaan
9. Omdat dit een bestaande sessie Hallo firewall voor deze reactie is toegestaan en Hallo firewall retourneert Hallo antwoord tooAppVM02
10. Subnet backend begint verwerking van inkomende regel:
    1. NSG-regel 1 (Internet Block) niet van toepassing, toonext regel verplaatsen
    2. Standaard NSG-regels toestaat subnet toosubnet verkeer, verkeer is toegestaan, stopt u de verwerking van NSG-regels
11. AppVM02 Hallo-antwoord wordt ontvangen

#### <a name="denied-internet-direct-tooweb-server"></a>(Geweigerd) Internet direct tooWeb Server
1. Internet-gebruiker probeert tooaccess Hallo webserver IIS01, via Hallo FrontEnd001.CloudApp.Net service
2. Aangezien er geen eindpunten voor HTTP-verkeer is geopend zijn, dit zou niet doorgeven aan Hallo Cloudservice en wouldn't Hallo-server niet bereiken
3. Als het Hallo-eindpunten zijn geopend voor een bepaalde reden, blokkeren Hallo NSG (Internet blokkeren) op Hallo Frontend subnet dit verkeer
4. Ten slotte Hallo Frontend subnet UDR route zou verzenden uitgaand verkeer van IIS01 toohello firewall als de volgende hop Hallo en Hallo firewall zou dit zien als asymmetrische verkeer en uitgaande antwoord Hallo Thus er ten minste drie onafhankelijke lagen zijn verwijderen verdediging tussen Hallo internet en IIS01 via de cloudservice zo wordt voorkomen dat onbevoegde/ongeoorloofde toegang.

#### <a name="denied-internet-toobackend-server"></a>(Geweigerd) Internet tooBackend Server
1. Internet-gebruiker probeert een bestand op AppVM01 via Hallo BackEnd001.CloudApp.Net service tooaccess
2. Aangezien er geen eindpunten voor de bestandsshare is geopend zijn, dit zou niet Hallo Cloudservice doorgeven en wouldn't Hallo-server niet bereiken
3. Als het Hallo-eindpunten zijn geopend voor een bepaalde reden, blokkeren Hallo NSG (Internet blokkeren) dit verkeer
4. Ten slotte Hallo UDR route zou verzenden uitgaand verkeer van AppVM01 toohello firewall als de volgende hop Hallo en Hallo firewall zou dit zien als asymmetrische verkeer en uitgaande antwoord Hallo Thus er ten minste drie onafhankelijke lagen verdediging tussen zijn neerzetten Hallo internet en AppVM01 via de cloudservice zo wordt voorkomen dat onbevoegde/ongeoorloofde toegang.

#### <a name="denied-frontend-server-toobackend-server"></a>(Geweigerd) Frontend server tooBackend Server
1. Stel IIS01 is geknoeid en schadelijke code probeert tooscan Hallo back-endservers voor subnet wordt uitgevoerd.
2. Hallo Frontend subnet UDR route zou uitgaand verkeer van IIS01 toohello firewall als de volgende hop Hallo verzenden. Dit is geen iets dat kan worden gewijzigd door Hallo geknoeid VM.
3. Hallo firewall zou Hallo-verkeer verwerken als Hallo-aanvraag is tooAppVM01 of toohello DNS-server voor DNS-zoekacties die verkeer kan mogelijk worden toegestaan door de firewall hello (vervaldatum tooFW regels 7 en 9). Al het andere verkeer wordt geblokkeerd door FW regel 11 (alle weigeren).
4. Of geavanceerde detectie van dreigingen op Hallo-firewall is ingeschakeld (Zie de documentatie Hallo leverancier voor uw specifieke netwerkapparaat advanced threat mogelijkheden, die niet in dit document wordt besproken), zelfs als het verkeer dat zou worden toegestaan door Hallo basic regels doorsturen beschreven in dit document kan worden voorkomen als Hallo-verkeer bevat handtekeningen van bekende of patronen die een regel voor geavanceerde threat vlag.

#### <a name="denied-internet-dns-lookup-on-dns-server"></a>(Geweigerd) Internet-DNS-lookup op DNS-server
1. Internet-gebruiker probeert een interne DNS-record op DNS01 via BackEnd001.CloudApp.Net service toolookup 
2. Aangezien er geen eindpunten voor DNS-verkeer is geopend zijn, dit zou niet doorgeven aan Hallo Cloudservice en wouldn't Hallo-server niet bereiken
3. Als het Hallo-eindpunten zijn geopend voor een bepaalde reden, wordt Hallo NSG regel (Internet blokkeren) op Hallo Frontend subnet dit verkeer geblokkeerd
4. Ten slotte Hallo back-end subnet UDR route zou verzenden uitgaand verkeer van DNS01 toohello firewall als de volgende hop Hallo en Hallo firewall zou dit zien als asymmetrische verkeer en uitgaande antwoord Hallo Thus er ten minste drie onafhankelijke lagen zijn verwijderen verdediging tussen Hallo internet en DNS01 via de cloudservice zo wordt voorkomen dat onbevoegde/ongeoorloofde toegang.

#### <a name="denied-internet-toosql-access-through-firewall"></a>(Geweigerd) TooSQL internettoegang via Firewall
1. Internet-gebruiker opvraagt SQL-gegevens uit SecSvc001.CloudApp.Net (Internet Facing Cloud Service)
2. Aangezien er geen eindpunten geopend voor SQL zijn, dit zou Hallo Cloudservice niet doorgeven en Hallo firewall wouldn't bereiken
3. Als de SQL-eindpunten zijn geopend voor een bepaalde reden, zouden Hallo firewall regelverwerking beginnen:
   1. FW regel 1 (FW Mgmt) niet van toepassing, toonext regel verplaatsen
   2. FW regels (regels RDP), 2-5 niet toepassen, toonext regel verplaatsen
   3. FW regel 6 en 7 (autorisatieregels) niet van toepassing, toonext regel verplaatsen
   4. FW regel 8 (tooInternet) niet van toepassing, toonext regel verplaatsen
   5. FW regel 9 (DNS) niet van toepassing, toonext regel verplaatsen
   6. FW regel 10 (Intra-Subnet) niet van toepassing, toonext regel verplaatsen
   7. FW regel 11 (alle weigeren) is van toepassing, het verkeer wordt geblokkeerd, stoppen, regelverwerking

## <a name="references"></a>Verwijzingen
### <a name="main-script-and-network-config"></a>Belangrijkste Script en netwerkconfiguratie
Hallo volledige Script opslaat in een PowerShell-scriptbestand. Sla Hallo netwerkconfiguratie naar een bestand met de naam 'NetworkConf2.xml'.
Hallo door de gebruiker gedefinieerde variabelen zo nodig wijzigen. Hallo-script uitvoeren en volg Hallo Firewall regel setup instructies hierboven.

#### <a name="full-script"></a>Volledige Script
Dit script wordt, op basis van Hallo door de gebruiker gedefinieerde variabelen:

1. Verbinding maken met tooan Azure-abonnement
2. Een nieuw opslagaccount maken
3. Maak een nieuw VNet en drie subnetten zoals gedefinieerd in het configuratiebestand voor Hallo netwerk
4. Vijf virtuele machines; opzetten firewall 1 en 4 WindowsServer VM 's
5. Configureer UDR inclusief:
   1. Twee nieuwe routetabellen maken
   2. Routes toohello tabellen toevoegen
   3. Tabellen tooappropriate subnetten binden
6. Doorsturen via IP inschakelen op Hallo NVA
7. Configureer het NSG inclusief:
   1. Maken van een NSG
   2. Een regel toe te voegen
   3. Binding Hallo NSG toohello juiste subnetten

Deze PowerShell-script moet lokaal op worden uitgevoerd dat een internet verbonden PC of de server.

> [!IMPORTANT]
> Wanneer dit script wordt uitgevoerd, kunnen er waarschuwingen of andere informatieve berichten die pop in PowerShell. Alleen foutberichten in rood zijn aanleiding.
> 
> 

    <# 
     .SYNOPSIS
      Example of DMZ and User Defined Routing in an isolated network (Azure only, no hybrid connections)

     .DESCRIPTION
      This script will build out a sample DMZ setup containing:
       - A default storage account for VM disks
       - Three new cloud services
       - Three Subnets (SecNet, FrontEnd, and BackEnd subnets)
       - A Network Virtual Appliance (NVA), in this case a Barracuda NextGen Firewall
       - One server on hello FrontEnd Subnet
       - Three Servers on hello BackEnd Subnet
       - IP Forwading from hello FireWall out toohello internet
       - User Defined Routing FrontEnd and BackEnd Subnets toohello NVA

      Before running script, ensure hello network configuration file is created in
      hello directory referenced by $NetworkConfigFile variable (or update the
      variable tooreflect hello path and file name of hello config file being used).

     .Notes
      Everyone's security requirements are different and can be addressed in a myriad of ways.
      Please be sure that any sensitive data or applications are behind hello appropriate
      layer(s) of protection. This script serves as an example of some of hello techniques
      that can be used, but should not be used for all scenarios. You are responsible to
      assess your security needs and hello appropriate protections needed, and then effectively
      implement those protections.

      Security Service (SecNet subnet 10.0.0.0/24)
       myFirewall - 10.0.0.4

      FrontEnd Service (FrontEnd subnet 10.0.1.0/24)
       IIS01      - 10.0.1.4

      BackEnd Service (BackEnd subnet 10.0.2.0/24)
       DNS01      - 10.0.2.4
       AppVM01    - 10.0.2.5
       AppVM02    - 10.0.2.6

    #>

    # Fixed Variables
        $LocalAdminPwd = Read-Host -Prompt "Enter Local Admin Password toobe used for all VMs"
        $VMName = @()
        $ServiceName = @()
        $VMFamily = @()
        $img = @()
        $size = @()
        $SubnetName = @()
        $VMIP = @()

    # User Defined Global Variables
      # These should be changes tooreflect your subscription and services
      # Invalid options will fail in hello validation section

      # Subscription Access Details
        $subID = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"

      # VM Account, Location, and Storage Details
        $LocalAdmin = "theAdmin"
        $DeploymentLocation = "Central US"
        $StorageAccountName = "vmstore02"

      # Service Details
        $SecureService = "SecSvc001"
        $FrontEndService = "FrontEnd001"
        $BackEndService = "BackEnd001"

      # Network Details
        $VNetName = "CorpNetwork"
        $VNetPrefix = "10.0.0.0/16"
        $SecNet = "SecNet"
        $FESubnet = "FrontEnd"
        $FEPrefix = "10.0.1.0/24"
        $BESubnet = "BackEnd"
        $BEPrefix = "10.0.2.0/24"
        $NetworkConfigFile = "C:\Scripts\NetworkConf3.xml"

      # VM Base Disk Image Details
        $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}
        $FWImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Barracuda NextGen Firewall'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

      # UDR Details
        $FERouteTableName = "FrontEndSubnetRouteTable"
        $BERouteTableName = "BackEndSubnetRouteTable"

      # NSG Details
        $NSGName = "MyVNetSG"

    # User Defined VM Specific Config
        # Note: tooensure UDR and IP forwarding is setup
        # properly this script requires VM 0 be hello NVA.

        # VM 0 - hello Network Virtual Appliance (NVA)
          $VMName += "myFirewall"
          $ServiceName += $SecureService
          $VMFamily += "Firewall"
          $img += $FWImg
          $size += "Small"
          $SubnetName += $SecNet
          $VMIP += "10.0.0.4"

        # VM 1 - hello Web Server
          $VMName += "IIS01"
          $ServiceName += $FrontEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.4"

        # VM 2 - hello First Appliaction Server
          $VMName += "AppVM01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.5"

        # VM 3 - hello Second Appliaction Server
          $VMName += "AppVM02"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.6"

        # VM 4 - hello DNS Server
          $VMName += "DNS01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.4"

    # ----------------------------- #
    # No User Defined Varibles or   #
    # Configuration past this point #
    # ----------------------------- #

      # Get your Azure accounts
        Add-AzureAccount
        Set-AzureSubscription –SubscriptionId $subID -ErrorAction Stop
        Select-AzureSubscription -SubscriptionId $subID -Current -ErrorAction Stop

      # Create Storage Account
        If (Test-AzureName -Storage -Name $StorageAccountName) { 
            Write-Host "Fatal Error: This storage account name is already in use, please pick a diffrent name." -ForegroundColor Red
            Return}
        Else {Write-Host "Creating Storage Account" -ForegroundColor Cyan 
              New-AzureStorageAccount -Location $DeploymentLocation -StorageAccountName $StorageAccountName}

      # Update Subscription Pointer tooNew Storage Account
        Write-Host "Updating Subscription Pointer tooNew Storage Account" -ForegroundColor Cyan 
        Set-AzureSubscription –SubscriptionId $subID -CurrentStorageAccountName $StorageAccountName -ErrorAction Stop

    # Validation
    $FatalError = $false

    If (-Not (Get-AzureLocation | Where {$_.DisplayName -eq $DeploymentLocation})) {
         Write-Host "This Azure Location was not found or available for use" -ForegroundColor Yellow
         $FatalError = $true}

    If (Test-AzureName -Service -Name $SecureService) { 
        Write-Host "hello SecureService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello FrontEndService service name is valid for use." -ForegroundColor Green}

    If (Test-AzureName -Service -Name $FrontEndService) { 
        Write-Host "hello FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello FrontEndService service name is valid for use" -ForegroundColor Green}

    If (Test-AzureName -Service -Name $BackEndService) { 
        Write-Host "hello BackEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello BackEndService service name is valid for use." -ForegroundColor Green}

    If (-Not (Test-Path $NetworkConfigFile)) { 
        Write-Host 'hello network config file was not found, please update hello $NetworkConfigFile variable toopoint toohello network config xml file.' -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello network config file was found" -ForegroundColor Green
            If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
                Write-Host 'hello deployment location was not found in hello network config file, please check hello network config file tooensure hello $DeploymentLocation varible is correct and hello netowrk config file matches.' -ForegroundColor Yellow
                $FatalError = $true}
            Else { Write-Host "hello deployment location was found in hello network config file." -ForegroundColor Green}}

    If ($FatalError) {
        Write-Host "A fatal error has occured, please see hello above messages for more information." -ForegroundColor Red
        Return}
    Else { Write-Host "Validation passed, now building hello environment." -ForegroundColor Green}

    # Create VNET
        Write-Host "Creating VNET" -ForegroundColor Cyan 
        Set-AzureVNetConfig -ConfigurationPath $NetworkConfigFile -ErrorAction Stop

    # Create Services
        Write-Host "Creating Services" -ForegroundColor Cyan
        New-AzureService -Location $DeploymentLocation -ServiceName $SecureService -ErrorAction Stop
        New-AzureService -Location $DeploymentLocation -ServiceName $FrontEndService -ErrorAction Stop
        New-AzureService -Location $DeploymentLocation -ServiceName $BackEndService -ErrorAction Stop

    # Build VMs
        $i=0
        $VMName | Foreach {
            Write-Host "Building $($VMName[$i])" -ForegroundColor Cyan
            If ($VMFamily[$i] -eq "Firewall") 
                { 
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Linux -LinuxUser $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                # Set up all hello EndPoints we'll need once we're up and running
                # Note: All traffic goes through hello firewall, so we'll need tooset up all ports here.
                #       Also, hello firewall will be redirecting traffic tooa new IP and Port in a forwarding
                #       rule, so all of these endpoint have hello same public and local port and hello firewall
                #       will do hello mapping, NATing, and/or redirection as declared in hello firewall rules.
                Add-AzureEndpoint -Name "MgmtPort1" -Protocol tcp -PublicPort 801  -LocalPort 801  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "MgmtPort2" -Protocol tcp -PublicPort 807  -LocalPort 807  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "HTTP"      -Protocol tcp -PublicPort 80   -LocalPort 80   -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPWeb"    -Protocol tcp -PublicPort 8014 -LocalPort 8014 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPApp1"   -Protocol tcp -PublicPort 8025 -LocalPort 8025 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPApp2"   -Protocol tcp -PublicPort 8026 -LocalPort 8026 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPDNS01"  -Protocol tcp -PublicPort 8024 -LocalPort 8024 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                # Note: A SSH endpoint is automatically created on port 22 when hello appliance is created.
                }
            Else
                {
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
                    Remove-AzureEndpoint -Name "RemoteDesktop" | `
                    Remove-AzureEndpoint -Name "PowerShell" | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                }
            $i++
        }

    # Configure UDR and IP Forwarding
        Write-Host "Configuring UDR" -ForegroundColor Cyan

      # Create hello Route Tables
        Write-Host "Creating hello Route Tables" -ForegroundColor Cyan 
        New-AzureRouteTable -Name $BERouteTableName `
            -Location $DeploymentLocation `
            -Label "Route table for $BESubnet subnet"
        New-AzureRouteTable -Name $FERouteTableName `
            -Location $DeploymentLocation `
            -Label "Route table for $FESubnet subnet"

      # Add Routes tooRoute Tables
        Write-Host "Adding Routes toohello Route Tables" -ForegroundColor Cyan 
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $FEPrefix `
            -NextHopType VNETLocal

      # Assoicate hello Route Tables with hello Subnets
        Write-Host "Binding Route Tables toohello Subnets" -ForegroundColor Cyan 
        Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
            -SubnetName $BESubnet `
            -RouteTableName $BERouteTableName
        Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
            -SubnetName $FESubnet `
            -RouteTableName $FERouteTableName

     # Enable IP Forwarding on hello Virtual Appliance
        Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] `
            |Set-AzureIPForwarding -Enable

    # Configure NSG
        Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

      # Build hello NSG
        Write-Host "Building hello NSG" -ForegroundColor Cyan
        New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

      # Add NSG Rule
        Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet from hello Internet" -Type Inbound -Priority 100 -Action Deny `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
            -Protocol *

      # Assign hello NSG tootwo Subnets
        # hello NSG is *not* bound toohello Security Subnet. hello result
        # is that internet traffic flows only toohello Security subnet
        # since hello NSG bound toohello Frontend and Backback subnets
        # will Deny internet traffic toothose subnets.
        Write-Host "Binding hello NSG tootwo subnets" -ForegroundColor Cyan
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $FESubnet -VirtualNetworkName $VNetName
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $BESubnet -VirtualNetworkName $VNetName

    # Optional Post-script Manual Configuration
      # Configure Firewall
      # Install Test Web App (Run Post-Build Script on hello IIS Server)
      # Install Backend resource (Run Post-Build Script on hello AppVM01)
      Write-Host
      Write-Host "Build Complete!" -ForegroundColor Green
      Write-Host
      Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
      Write-Host " - Configure Firewall" -ForegroundColor Gray
      Write-Host " - Install Test Web App (Run Post-Build Script on hello IIS Server)" -ForegroundColor Gray
      Write-Host " - Install Backend resource (Run Post-Build Script on hello AppVM01)" -ForegroundColor Gray
      Write-Host


#### <a name="network-config-file"></a>Netwerk-configuratiebestand
Dit xml-bestand opslaan met bijgewerkte locatie en voeg Hallo koppeling toothis toohello $NetworkConfigFile variabele in bovenstaande Hallo-script bestand.

    <NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
      <VirtualNetworkConfiguration>
        <Dns>
          <DnsServers>
            <DnsServer name="DNS01" IPAddress="10.0.2.4" />
            <DnsServer name="Level3" IPAddress="209.244.0.3" />
          </DnsServers>
        </Dns>
        <VirtualNetworkSites>
          <VirtualNetworkSite name="CorpNetwork" Location="Central US">
            <AddressSpace>
              <AddressPrefix>10.0.0.0/16</AddressPrefix>
            </AddressSpace>
            <Subnets>
              <Subnet name="SecNet">
                <AddressPrefix>10.0.0.0/24</AddressPrefix>
              </Subnet>
              <Subnet name="FrontEnd">
                <AddressPrefix>10.0.1.0/24</AddressPrefix>
              </Subnet>
              <Subnet name="BackEnd">
                <AddressPrefix>10.0.2.0/24</AddressPrefix>
              </Subnet>
            </Subnets>
            <DnsServersRef>
              <DnsServerRef name="DNS01" />
              <DnsServerRef name="Level3" />
            </DnsServersRef>
          </VirtualNetworkSite>
        </VirtualNetworkSites>
      </VirtualNetworkConfiguration>
    </NetworkConfiguration>

#### <a name="sample-application-scripts"></a>Voorbeeldscripts toepassing
Als u een voorbeeldtoepassing tooinstall voor deze en andere voorbeelden van het Perimeternetwerk wilt, een is opgegeven op de koppeling Hallo: [voorbeeldscript toepassing][SampleApp]

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3design.png "Bidirectionele DMZ met NVA, NSG en UDR"
[2]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3firewalllogical.png "Logische weergave van Hallo Firewall-regels"
[3]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectfrontend.png "Een Object FrontEnd-netwerk maken"
[4]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectdns.png "Een DNS-Server-Object maken"
[5]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpa.png "Kopie van de standaardregel voor RDP"
[6]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpb.png "AppVM01 regel"
[7]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconapplicationredirect.png "Pictogram voor toepassing omleiding"
[8]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/icondestinationnat.png "Bestemming NAT-pictogram"
[9]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconpass.png "Pass-pictogram"
[10]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulefirewall.png "Firewallregel Management"
[11]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulerdp.png "RDP-firewallregel"
[12]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleweb.png "Web-firewallregel"
[13]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleappvm01.png "AppVM01 firewallregel"
[14]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleoutbound.png "Uitgaande firewallregel"
[15]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledns.png "DNS-firewallregel"
[16]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleintravnet.png "Intra-VNet-firewallregel"
[17]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledeny.png "Regel voor weigeren van Firewall"
[18]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/firewallruleactivate.png "Activering van de firewall-regel"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md
