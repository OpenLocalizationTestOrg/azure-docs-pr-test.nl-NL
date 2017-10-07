---
title: "toepassingen met een Firewall en nsg's van een DMZ tooprotect bouwen aaaDMZ voorbeeld – | Microsoft Docs"
description: Maken van een DMZ met een Firewall en Netwerkbeveiligingsgroepen (NSG)
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: c78491c7-54ac-4469-851c-b35bfed0f528
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: jonor;sivae
ms.openlocfilehash: 18f116dc3897567bff14a509ae8c13f449182bfb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="example-2--build-a-dmz-tooprotect-applications-with-a-firewall-and-nsgs"></a>Voorbeeld 2: een DMZ tooprotect bouwen toepassingen met een Firewall en nsg 's
[Best Practices beveiligingspagina-grens toohello retourneren][HOME]

In dit voorbeeld wordt een DMZ maken met een firewall, vier windows-servers en Netwerkbeveiligingsgroepen. Deze ook begeleidt bij elk Hallo relevante opdrachten tooprovide een beter begrip van elke stap. Er is ook een verkeer Scenario sectie tooprovide een gedetailleerd stapsgewijs hoe verkeer wordt voortgezet via Hallo lagen verdediging in Hallo DMZ. Ten slotte is in de sectie Verwijzingen Hallo de volledige code Hallo en instructie toobuild deze omgeving tootest en het experiment met verschillende scenario's. 

![Inkomende DMZ met NVA en NSG][1]

## <a name="environment-description"></a>Beschrijving van de omgeving
In dit voorbeeld is er een abonnement dat Hallo volgende bevat:

* Twee cloudservices: 'FrontEnd001' en 'BackEnd001'
* Een virtueel netwerk 'CorpNetwork' met twee subnetten: 'FrontEnd' en back-end'
* Een enkele Netwerkbeveiligingsgroep die toegepaste tooboth subnetten
* Een virtueel netwerkapparaat, in dit voorbeeld een Barracuda NextGen Firewall, verbonden toohello Frontend subnet
* Een Windows-Server waarmee een toepassing webserver ('IIS01')
* Twee windows-servers die toepassing terug vertegenwoordigen end servers ('AppVM01', 'AppVM02')
* Een Windows-server met een DNS-server ('DNS01')

> [!NOTE]
> Hoewel dit voorbeeld een Barracuda NextGen Firewall veel Hallo die verschillende virtuele netwerkapparaten kan worden gebruikt voor dit voorbeeld wordt.
> 
> 

In onderstaande Hallo verwijzingen gedeelte is er een PowerShell-script dat de meeste Hallo-omgeving die hierboven worden beschreven bouwt. Gebouw Hallo VM's en virtuele netwerken worden Hoewel worden uitgevoerd door Hallo voorbeeldscript wordt niet in dit document uitvoeriger beschreven.

toobuild hello omgeving:

1. Hallo netwerk config XML-bestand is opgenomen in de sectie Verwijzingen hello (bijgewerkt met de naam, locatie en IP-adressen toomatch Hallo gegeven scenario) opslaan
2. Update Hallo Gebruikersvariabelen in Hallo script toomatch Hallo omgeving Hallo script is toobe uitgevoerd (abonnementen, servicenamen, enzovoort)
3. Hallo-script uitvoeren in PowerShell

**Opmerking**: Hallo regio aangegeven in Hallo PowerShell-script moet overeenkomen met de Hallo regio in xml-configuratiebestand met Hallo netwerk aangegeven.

Zodra het Hallo-script wordt uitgevoerd kan Hallo na script stappen kan worden genomen:

1. Hallo-firewallregels instellen, deze procedure wordt besproken in Hallo onderstaande sectie met de titel: Firewall-regels.
2. Optioneel zijn in de sectie Verwijzingen Hallo twee scripts tooset up Hallo-webserver en appserver met een eenvoudige web application tooallow testen met deze configuratie DMZ.

Hallo volgende sectie wordt uitgelegd meeste Hallo scripts instructies relatieve tooNetwork beveiligingsgroepen.

## <a name="network-security-groups-nsg"></a>Netwerkbeveiligingsgroepen (NSG's)
In dit voorbeeld is een groep NSG gebouwd en vervolgens geladen met zes regels. 

> [!TIP]
> In het algemeen moet u eerst uw specifieke regels voor 'Toestaan' maken en vervolgens laatste Hallo algemene "Deny" regels. Hallo toegewezen prioriteit bepaalt welke regels eerst worden geëvalueerd. Als verkeer tooapply tooa specifieke regel gevonden wordt, wordt er geen verdere regels worden geëvalueerd. NSG-regels kunnen toepassen in op Hallo binnenkomende of uitgaande richting (vanuit het perspectief van de Hallo van Hallo subnet).
> 
> 

Declaratief, worden Hallo volgens de regels voor binnenkomend verkeer gebouwd:

1. Interne DNS-verkeer (poort 53) is toegestaan
2. RDP-verkeer (poort 3389) van Hallo Internet tooany VM is toegestaan
3. HTTP-verkeer (poort 80) van Hallo Internet toohello NVA (firewall) is toegestaan
4. Verkeer (alle poorten) van IIS01 tooAppVM1 is toegestaan
5. Verkeer (alle poorten) van Hallo Internet toohello hele VNet (beide subnetten) is geweigerd.
6. Verkeer (alle poorten) van Hallo Frontend subnet toohello back-end-subnet is geweigerd

Met deze regels gebonden tooeach-subnet als een HTTP-aanvraag was binnenkomend van Hallo Internet toohello webserver beide regels 3 (toestaan) en 5 (weigeren) toepassing zou zijn, maar omdat de regel 3 heeft een hogere prioriteit alleen zou worden toegepast en regel 5 niet in de play zou komen. Hallo HTTP-aanvraag zou dus toohello firewall toegestaan. Als dat dezelfde verkeer tooreach hello DNS01 server probeerde, zou regel 5 (weigeren) zijn de eerste tooapply en Hallo verkeer Hallo zou niet toegestaan toopass toohello server. Regel 6 (weigeren) blokken Hallo subnet Frontend in gesprekken toohello back-end-subnet (met uitzondering van toegestane regels 1 en 4-verkeer), dit beschermt Hallo back-end-netwerk als een aanvaller inbreuk Hallo webtoepassing op Hallo Frontend, Hallo aanvaller moet beperkte toegang toohello back-end '-beveiliging gebruiken' netwerk (alleen tooresources blootgesteld op Hallo AppVM01 server).

Er is een uitgaande standaardregel waarmee verkeer van toohello internet. Voor dit voorbeeld bent we uitgaand verkeer toestaat en alle regels voor uitgaande verbindingen niet wijzigen. toolock omlaag verkeer in beide richtingen gebruiker gedefinieerde routering is vereist, dit in een ander voorbeeld die u in Hallo vinden kunt is verkend [belangrijkste beveiliging grens document][HOME].

Hallo hierboven besproken NSG-regels zijn vergelijkbaar toohello NSG-regels in [voorbeeld 1: een eenvoudige DMZ met nsg's bouwen][Example1]. Controleer Hallo NSG beschrijving in dat document voor een gedetailleerde blik op elke regel van het NSG en de kenmerken.

## <a name="firewall-rules"></a>Firewallregels
Een Beheerclient toobe geïnstalleerd op een PC toomanage Hallo firewall nodig hebt en Hallo configuraties nodig maken. Zie de leverancier van de documentatie van uw firewall (of andere NVA) Hallo over hoe toomanage apparaat Hallo. Hallo rest van deze sectie wordt beschreven Hallo configuratie van Hallo firewall zelf, via Hallo leveranciers management-client (d.w.z. niet hello Azure-portal of PowerShell).

Instructies voor het downloaden van de client en verbindende toohello Barracuda gebruikt in dit voorbeeld vindt u hier: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)

Regels voor doorsturen moet toobe gemaakt op Hallo-firewall. Omdat in dit voorbeeld wordt alleen routes in gebonden toohello firewall voor internet-verkeer en vervolgens toohello webserver, wordt slechts één doorsturen NAT-regel vereist. Regel zou op Hallo Barracuda NextGen Firewall gebruikt in dit voorbeeld Hallo zijn een doel-NAT-regel ('zomertijd NAT') toopass dit verkeer.

toocreate hello volgende regel (of Controleer of de bestaande standaardregels), vanaf Hallo Barracuda NG Admin client dashboard, navigeer toohello configuratie tabblad, in Hallo operationele configuratie sectie Ruleset klikt u op. Een raster aangeroepen, wordt 'Main regels' hello bestaande actieve en gedeactiveerd regels op Hallo firewall weergegeven. Hallo rechterbovenhoek van dit raster is een klein, groene '+' knop, klikt u op deze toocreate een nieuwe regel (Opmerking: uw firewall mogelijk 'vergrendeld' om wijzigingen, als er een knop gemarkeerd als 'Vergrendelen' en kan niet toocreate zijn of regels bewerken, klikt u op deze knop te 'ontgrendelen' Hallo ruleSet en bewerken). Als u een bestaande regel tooedit wilt, selecteert u deze regel, met de rechtermuisknop op en selecteer regel bewerken.

Maak een nieuwe regel en geef een naam op, zoals 'WebTraffic'. 

Hallo bestemming NAT-regel pictogram uitziet: ![bestemming NAT-pictogram][2]

Hallo-regel zelf zou als volgt uitzien:

![Firewallregel][3]

Hier een inkomende adres dat treffers Hallo Firewall probeert tooreach HTTP (poort 80 of 443 voor HTTPS) wordt verzonden van Firewall 'DHCP1 lokale-IP-interface en omgeleide toohello Web Server met IP-adres van 10.0.1.5 Hallo Hallo. Omdat Hallo-verkeer op poort 80 en gaat toohello webserver op poort 80 in afkomstig is geen poortwijziging is vereist. Echter Hallo Hallo doellijst kan zijn 10.0.1.5:8080 als uw webserver worden geluisterd op poort 8080 dus vertalen van de binnenkomende poort 80 op Hallo firewall tooinbound poort 8080 op Hallo-webserver.

Een verbindingsmethode moet ook worden aangegeven, voor Hallo bestemming regel vanaf Internet, Hallo 'Dynamische snat omzetten' is het meest geschikt. 

Hoewel u slechts één regel is gemaakt is het belangrijk dat de prioriteit correct is ingesteld. Als in raster Hallo van alle regels op Hallo firewall voor dat deze nieuwe regel wordt aan de onderkant hello (onder Hallo 'BLOCKALL' regel) dit wordt nooit een rol spelen. Zorg ervoor dat Hallo nieuwe regel voor internetverkeer hierboven Hallo BLOCKALL regel.

Zodra het Hallo-regel is gemaakt, moet deze zijn gedistribueerd toohello firewall en wordt geactiveerd, als dit niet gebeurt Hallo regel wijziging wordt pas van kracht. Hallo push en activering proces wordt beschreven in de volgende sectie Hallo.

## <a name="rule-activation"></a>Activering van de regel
Hello ruleset gewijzigd tooadd met deze regel, Hallo ruleset moet worden geüpload toohello firewall en geactiveerd.

![Activering van de firewall-regel][4]

In Hallo rechtsboven van Hallo Beheerclient zijn een cluster van knoppen. Hallo 'verzenden wijzigingen' knop toosend Hallo gewijzigd regels toohello firewall, klik op de knop 'Activeren' Hallo.

Deze versie van de omgeving voorbeeld is bij activering via Hallo Hallo firewall ruleSet voltooid. Eventueel Hallo post build scripts in Hallo verwijzingen sectie kan worden uitgevoerd tooadd een toepassing toothis omgeving tootest Hallo onderstaande verkeer scenario's.

> [!IMPORTANT]
> Kritieke toorealize dat niet u Hallo webserver rechtstreeks bereikt is. Wanneer een browser een HTTP-pagina van FrontEnd001.CloudApp.Net aanvraagt, webserver Hallo HTTP-eindpunt (poort 80) geeft dit verkeer toohello firewall niet Hallo. Hallo firewall vervolgens hierboven NAT's die toohello webserver aanvragen volgens regel toohello gemaakt.
> 
> 

## <a name="traffic-scenarios"></a>Verkeer scenario 's
#### <a name="allowed-web-tooweb-server-through-firewall"></a>(Toegestaan) TooWeb Web Server via de Firewall
1. Internet aanvragen HTTP-gebruikerspagina van FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)
2. Cloud-service geeft verkeer via open eindpunten op poort 80 toofirewall lokale interface op 10.0.1.4:80
3. Subnet frontend begint verwerking van inkomende regel:
   1. NSG regel 1 (DNS) niet van toepassing, toonext regel verplaatsen
   2. NSG regel 2 (RDP) niet van toepassing, toonext regel verplaatsen
   3. NSG regel 3 (Internet tooFirewall) is van toepassing, -verkeer is toegestaan, zelfs niet meer regelverwerking
4. Verkeer komt binnen via interne IP-adres van Hallo firewall (10.0.1.4)
5. Regel voor doorsturen van de firewall Zie dit netwerkverkeer via de poort 80 is, stuurt het webserver toohello IIS01
6. IIS01 luistert voor internetverkeer, ontvangt deze aanvraag en begint met de verwerking van Hallo-aanvraag
7. IIS01 vraagt Hallo SQL Server op AppVM01 voor meer informatie
8. Er is geen uitgaande regels op subnet Frontend verkeer wordt toegestaan.
9. Hallo back-end subnet begint verwerking van inkomende regel:
   1. NSG regel 1 (DNS) niet van toepassing, toonext regel verplaatsen
   2. NSG regel 2 (RDP) niet van toepassing, toonext regel verplaatsen
   3. NSG regel 3 (Internet tooFirewall) niet van toepassing, toonext regel verplaatsen
   4. NSG regel 4 (IIS01 tooAppVM01) is van toepassing, -verkeer is toegestaan, zelfs niet meer regelverwerking
10. AppVM01 ontvangen Hallo SQL-Query en beantwoord
11. Omdat er geen uitgaande regels op Hallo antwoord Hallo van back-end-subnet is toegestaan
12. Subnet frontend begint verwerking van inkomende regel:
    1. Er is geen NSG-regel die van toepassing tooInbound verkeer van Hallo back-end subnet toohello Frontend subnet, is zodat geen van Hallo NSG-regels toepassen
    2. Hallo system standaardregel verkeer tussen subnetten zou dit verkeer toestaan zodat Hallo verkeer is toegestaan.
13. Hallo SQL antwoord wordt ontvangen en Hallo HTTP-antwoord is voltooid en toohello aanvrager verzendt Hallo IIS-server
14. Aangezien dit een NAT-sessie van de firewall hello, is Hallo antwoord bestemming (in eerste instantie) voor Hallo Firewall
15. Hallo firewall antwoord Hallo ontvangt van Hallo webserver en stuurt back toohello Internet-gebruiker
16. Omdat er geen uitgaande regels op Hallo Frontend subnet Hallo antwoord is toegestaan en Hallo Internet-gebruiker ontvangt Hallo webpagina aangevraagd.

#### <a name="allowed-rdp-toobackend"></a>(Toegestaan) RDP-tooBackend
1. RDP-sessie tooAppVM01 op BackEnd001.CloudApp.Net:xxxxx waarbij xxxxx Hallo willekeurig toegewezen poort voor RDP tooAppVM01 is serverbeheerder op internet-aanvragen (Hallo toegewezen poort kan worden gevonden op Hallo Azure Portal of via PowerShell)
2. Sinds Hallo die Hallo FrontEnd001.CloudApp.Net adres alleen Firewall luistert, is niet verbonden met dit netwerkverkeer
3. Subnet backend begint verwerking van inkomende regel:
   1. NSG regel 1 (DNS) niet van toepassing, toonext regel verplaatsen
   2. NSG regel 2 (RDP) is van toepassing, -verkeer is toegestaan, zelfs niet meer regelverwerking
4. Er is geen uitgaande regels standaardregels toepassen en terugkerend verkeer is toegestaan
5. RDP-sessie is ingeschakeld
6. AppVM01 gebruikersnaam wachtwoord gevraagd

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a>(Toegestaan) Web Server DNS-lookup op DNS-server
1. Web-Server, IIS01, moeten een gegevensfeed op www.data.gov, maar moet tooresolve Hallo adres.
2. Hallo netwerkconfiguratie voor Hallo VNet lijsten DNS01 (10.0.2.4 op Hallo back-end subnet) als het primaire DNS-server hello, IIS01 verzendt Hallo DNS-aanvraag tooDNS01
3. Er is geen uitgaande regels op subnet Frontend verkeer wordt toegestaan.
4. Subnet backend begint verwerking van inkomende regel:
   1. NSG regel 1 (DNS) is van toepassing, -verkeer is toegestaan, zelfs niet meer regelverwerking
5. DNS-server ontvangt Hallo aanvraag
6. DNS-server heeft geen Hallo-adres in de cache opgeslagen en wordt u gevraagd een basis-DNS-server op Hallo internet
7. Er is geen uitgaande regels op subnet Backend verkeer wordt toegestaan.
8. Internet-DNS-server reageert, omdat deze sessie is gestart, intern, is antwoord Hallo toegestaan
9. DNS-server in de cache opgeslagen antwoord Hallo en toohello eerste aanvraag back tooIIS01 reageert
10. Er is geen uitgaande regels op subnet Backend verkeer wordt toegestaan.
11. Subnet frontend begint verwerking van inkomende regel:
    1. Er is geen NSG-regel die van toepassing tooInbound verkeer van Hallo back-end subnet toohello Frontend subnet, is zodat geen van Hallo NSG-regels toepassen
    2. Hallo system standaardregel verkeer tussen subnetten zou dit verkeer toestaan dus Hallo verkeer is toegestaan
12. IIS01 ontvangt antwoord Hallo van DNS01

#### <a name="allowed-web-server-access-file-on-appvm01"></a>(Toegestaan) Web Server toegang tot bestand op AppVM01
1. IIS01 vraagt om een bestand op AppVM01
2. Er is geen uitgaande regels op subnet Frontend verkeer wordt toegestaan.
3. Hallo back-end subnet begint verwerking van inkomende regel:
   1. NSG regel 1 (DNS) niet van toepassing, toonext regel verplaatsen
   2. NSG regel 2 (RDP) niet van toepassing, toonext regel verplaatsen
   3. NSG regel 3 (Internet tooFirewall) niet van toepassing, toonext regel verplaatsen
   4. NSG regel 4 (IIS01 tooAppVM01) is van toepassing, -verkeer is toegestaan, zelfs niet meer regelverwerking
4. AppVM01 hello aanvraag ontvangt en reageert met bestand (ervan uitgaande dat toegang wordt geverifieerd)
5. Omdat er geen uitgaande regels op Hallo antwoord Hallo van back-end-subnet is toegestaan
6. Subnet frontend begint verwerking van inkomende regel:
   1. Er is geen NSG-regel die van toepassing tooInbound verkeer van Hallo back-end subnet toohello Frontend subnet, is zodat geen van Hallo NSG-regels toepassen
   2. Hallo system standaardregel verkeer tussen subnetten zou dit verkeer toestaan zodat Hallo verkeer is toegestaan.
7. Hallo IIS server ontvangt Hallo-bestand

#### <a name="denied-web-direct-tooweb-server"></a>(Geweigerd) Web direct tooWeb Server
Sinds Hallo webserver, IIS01 en Hallo Firewall zijn in Hallo dezelfde Cloudservice ze delen Hallo dezelfde openbare internetgerichte IP-adres. Dus HTTP-verkeer zou worden omgeleid toohello firewall. Tijdens het Hallo-aanvraag zou met succes worden geleverd, deze kan niet gaat u rechtstreeks toohello webserver, die wordt doorgegeven, die is ontworpen, via Hallo Firewall eerst. Zie Hallo eerste Scenario in dit gedeelte voor het Hallo-netwerkverkeer.

#### <a name="denied-web-toobackend-server"></a>(Geweigerd) TooBackend Web Server
1. Internet-gebruiker probeert een bestand op AppVM01 via Hallo BackEnd001.CloudApp.Net service tooaccess
2. Aangezien er geen eindpunten voor de bestandsshare is geopend zijn, dit zou niet Hallo Cloudservice doorgeven en wouldn't Hallo-server niet bereiken
3. Als het Hallo-eindpunten zijn geopend voor een bepaalde reden, wordt NSG regel 5 (Internet tooVNet) dit verkeer geblokkeerd

#### <a name="denied-web-dns-lookup-on-dns-server"></a>(Geweigerd) Web DNS-zoekopdracht op DNS-server
1. Internet-gebruiker probeert een interne DNS-record op DNS01 via Hallo BackEnd001.CloudApp.Net service toolookup
2. Aangezien er geen eindpunten voor DNS is geopend zijn, dit zou niet Hallo Cloudservice doorgeven en wouldn't Hallo-server niet bereiken
3. Als het Hallo-eindpunten zijn geopend voor een bepaalde reden, NSG regel 5 (Internet tooVNet) dit verkeer wordt geblokkeerd (Opmerking: deze regel 1 (DNS) is niet van toepassing om twee redenen, eerste Hallo-bronadres is internet Hallo, deze regel is alleen van toepassing toohello lokale VNet als Hallo bron ook Dit is een regel voor toestaan, zodat deze zou nooit verkeer weigeren)

#### <a name="denied-web-toosql-access-through-firewall"></a>(Geweigerd) TooSQL webtoegang via Firewall
1. Internet-gebruiker opvraagt SQL-gegevens uit FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)
2. Aangezien er geen eindpunten geopend voor SQL zijn, dit zou Hallo Cloudservice niet doorgeven en Hallo firewall wouldn't bereiken
3. Als eindpunten geopend voor een bepaalde reden zijn, begint Hallo Frontend subnet verwerking van inkomende regel:
   1. NSG regel 1 (DNS) niet van toepassing, toonext regel verplaatsen
   2. NSG regel 2 (RDP) niet van toepassing, toonext regel verplaatsen
   3. NSG-regel 2 (Internet tooFirewall) is van toepassing, -verkeer is toegestaan, zelfs niet meer regelverwerking
4. Verkeer komt binnen via interne IP-adres van Hallo firewall (10.0.1.4)
5. Firewall heeft geen regels doorsturen voor SQL en verwijdert Hallo verkeer

## <a name="conclusion"></a>Conclusie
Dit is een relatief eenvoudig en duidelijk van het beveiligen van uw toepassing met een firewall en Hallo back-end subnet uit binnenkomend verkeer isoleren.

Meer voorbeelden en een overzicht van het netwerk beveiligingsgrenzen vindt [hier][HOME].

## <a name="references"></a>Verwijzingen
### <a name="main-script-and-network-config"></a>Belangrijkste Script en netwerkconfiguratie
Hallo volledige Script opslaat in een PowerShell-scriptbestand. Sla Hallo netwerkconfiguratie naar een bestand met de naam 'NetworkConf2.xml'.
Hallo door de gebruiker gedefinieerde variabelen zo nodig wijzigen. Hallo-script uitvoeren en volg Hallo Firewall regel setup instructies hierboven.

#### <a name="full-script"></a>Volledige Script
Dit script wordt, op basis van Hallo door de gebruiker gedefinieerde variabelen:

1. Verbinding maken met tooan Azure-abonnement
2. Een nieuw opslagaccount maken
3. Maak een nieuw VNet en twee subnets zoals gedefinieerd in het configuratiebestand voor Hallo netwerk
4. 4 windows server-VM's maken
5. Configureer het NSG inclusief:
   * Maken van een NSG
   * Met regels in te vullen
   * Binding Hallo NSG toohello juiste subnetten

Deze PowerShell-script moet lokaal op worden uitgevoerd dat een internet verbonden PC of de server.

> [!IMPORTANT]
> Wanneer dit script wordt uitgevoerd, kunnen er waarschuwingen of andere informatieve berichten die pop in PowerShell. Alleen foutberichten in rood zijn aanleiding.
> 
> 

    <# 
     .SYNOPSIS
      Example of DMZ and Network Security Groups in an isolated network (Azure only, no hybrid connections)

     .DESCRIPTION
      This script will build out a sample DMZ setup containing:
       - A default storage account for VM disks
       - Two new cloud services
       - Two Subnets (FrontEnd and BackEnd subnets)
       - A Network Virtual Appliance (NVA), in this case a Barracuda NextGen Firewall
       - One server on hello FrontEnd Subnet (plus hello NVA on hello FrontEnd subnet)
       - Three Servers on hello BackEnd Subnet
       - Network Security Groups tooallow/deny traffic patterns as declared

      Before running script, ensure hello network configuration file is created in
      hello directory referenced by $NetworkConfigFile variable (or update the
      variable tooreflect hello path and file name of hello config file being used).

     .Notes
      Security requirements are different for each use case and can be addressed in a
      myriad of ways. Please be sure that any sensitive data or applications are behind
      hello appropriate layer(s) of protection. This script serves as an example of some
      of hello techniques that can be used, but should not be used for all scenarios. You
      are responsible tooassess your security needs and hello appropriate protections
      needed, and then effectively implement those protections.

      FrontEnd Service (FrontEnd subnet 10.0.1.0/24)
       myFirewall - 10.0.1.4
       IIS01      - 10.0.1.5

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
        $FrontEndService = "FrontEnd001"
        $BackEndService = "BackEnd001"

      # Network Details
        $VNetName = "CorpNetwork"
        $FESubnet = "FrontEnd"
        $FEPrefix = "10.0.1.0/24"
        $BESubnet = "BackEnd"
        $BEPrefix = "10.0.2.0/24"
        $NetworkConfigFile = "C:\Scripts\NetworkConf2.xml"

      # VM Base Disk Image Details
        $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}
        $FWImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Barracuda NextGen Firewall'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

      # NSG Details
        $NSGName = "MyVNetSG"

    # User Defined VM Specific Config
        # Note: tooensure proper NSG Rule creation later in this script:
        #       - hello Web Server must be VM 1
        #       - hello AppVM1 Server must be VM 2
        #       - hello DNS server must be VM 4
        #
        #       Otherwise hello NSG rules in hello last section of this
        #       script will need toobe changed toomatch hello modified
        #       VM array numbers ($i) so hello NSG Rule IP addresses
        #       are aligned toohello associated VM IP addresses.

        # VM 0 - hello Network Virtual Appliance (NVA)
          $VMName += "myFirewall"
          $ServiceName += $FrontEndService
          $VMFamily += "Firewall"
          $img += $FWImg
          $size += "Small"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.4"

        # VM 1 - hello Web Server
          $VMName += "IIS01"
          $ServiceName += $FrontEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.5"

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

    If (Test-AzureName -Service -Name $FrontEndService) { 
        Write-Host "hello FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello FrontEndService service name is valid for use." -ForegroundColor Green}

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
                # Note: Web traffic goes through hello firewall, so we'll need tooset up a HTTP endpoint.
                #       Also, hello firewall will be redirecting web traffic tooa new IP and Port in a
                #       forwarding rule, so hello HTTP endpoint here will have hello same public and local
                #       port and hello firewall will do hello NATing and redirection as declared in the
                #       firewall rule.
                Add-AzureEndpoint -Name "MgmtPort1" -Protocol tcp -PublicPort 801  -LocalPort 801  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "MgmtPort2" -Protocol tcp -PublicPort 807  -LocalPort 807  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "HTTP"      -Protocol tcp -PublicPort 80   -LocalPort 80   -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                # Note: A SSH endpoint is automatically created on port 22 when hello appliance is created.
                }
            Else
                {
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
                    Remove-AzureEndpoint -Name "PowerShell" | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                    # Note: A Remote Desktop endpoint is automatically created when each VM is created.
                }
            $i++
        }

    # Configure NSG
        Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

      # Build hello NSG
        Write-Host "Building hello NSG" -ForegroundColor Cyan
        New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

      # Add NSG Rules
        Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
            -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[4] -DestinationPortRange '53' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet too$($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
            -SourceAddressPrefix Internet -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[1]) too$($VMName[2])" -Type Inbound -Priority 130 -Action Allow `
            -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[2] -DestinationPortRange '*' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet from hello Internet" -Type Inbound -Priority 140 -Action Deny `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $FESubnet subnet from hello $BESubnet subnet" -Type Inbound -Priority 150 -Action Deny `
            -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
            -DestinationAddressPrefix $BEPrefix -DestinationPortRange '*' `
            -Protocol *

        # Assign hello NSG toohello Subnets
            Write-Host "Binding hello NSG tooboth subnets" -ForegroundColor Cyan
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
[1]: ./media/virtual-networks-dmz-nsg-fw-asm/example2design.png "Inkomende DMZ met NSG"
[2]: ./media/virtual-networks-dmz-nsg-fw-asm/dstnaticon.png "Bestemming NAT-pictogram"
[3]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallrule.png "Firewallregel"
[4]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallruleactivate.png "Activering van de firewall-regel"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md
[Example1]: ./virtual-networks-dmz-nsg-asm.md
