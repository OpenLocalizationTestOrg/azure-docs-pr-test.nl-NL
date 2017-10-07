---
title: "aaaAzure DMZ voorbeeld – een eenvoudige DMZ met nsg's bouwen | Microsoft Docs"
description: Maken van een DMZ met Netwerkbeveiligingsgroepen (NSG)
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: f8622b1d-c07d-4ea6-b41c-4ae98d998fff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: 32a40a8dc7539c4c7293988e6c36e5e32ef11045
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-classic-powershell"></a>Voorbeeld 1: een eenvoudige DMZ met nsg's met klassieke PowerShell bouwen
[Best Practices beveiligingspagina-grens toohello retourneren][HOME]

> [!div class="op_single_selector"]
> * [Resource Manager-sjabloon](virtual-networks-dmz-nsg.md)
> * [Klassieke - PowerShell](virtual-networks-dmz-nsg-asm.md)
> 
>

In dit voorbeeld maakt een primitieve DMZ met vier Windows-servers en Netwerkbeveiligingsgroepen. In dit voorbeeld worden alle Hallo relevante PowerShell-opdrachten tooprovide een beter begrip van elke stap beschreven. Er is ook een verkeer Scenario sectie tooprovide een gedetailleerd stapsgewijs hoe verkeer wordt voortgezet via Hallo lagen verdediging in Hallo DMZ. Ten slotte is in de sectie Verwijzingen Hallo de volledige code Hallo en instructie toobuild deze omgeving tootest en het experiment met verschillende scenario's. 

![Inkomende DMZ met NSG][1]

## <a name="environment-description"></a>Beschrijving van de omgeving
In dit voorbeeld bevat een abonnement Hallo resources te volgen:

* Twee cloudservices: 'FrontEnd001' en 'BackEnd001'
* Een virtueel netwerk, 'CorpNetwork' met twee subnetten; 'FrontEnd' en back-end'
* Een Netwerkbeveiligingsgroep die toegepaste tooboth subnetten
* Een Windows-Server waarmee een toepassing webserver ('IIS01')
* Twee windows-servers die vertegenwoordigen toepassingsservers van back-end ('AppVM01', 'AppVM02')
* Een Windows-server met een DNS-server ('DNS01')

In de sectie Verwijzingen hello is er een PowerShell-script dat de meeste Hallo-omgeving beschreven in dit voorbeeld is gebaseerd. Gebouw Hallo VM's en virtuele netwerken worden Hoewel worden uitgevoerd door Hallo voorbeeldscript wordt niet in dit document uitvoeriger beschreven. 

toobuild Hallo-omgeving.

1. Hallo netwerk config XML-bestand is opgenomen in de sectie Verwijzingen hello (bijgewerkt met de naam, locatie en IP-adressen toomatch Hallo gegeven scenario) opslaan
2. Update Hallo Gebruikersvariabelen in Hallo script toomatch Hallo omgeving Hallo script is toobe uitgevoerd (abonnementen, servicenamen, enz.)
3. Hallo-script uitvoeren in PowerShell

>[!Note]
>Hallo regio aangegeven in Hallo PowerShell-script moet overeenkomen met de Hallo regio in xml-configuratiebestand met Hallo netwerk aangegeven.
>
>

Zodra het Hallo-script wordt uitgevoerd is aanvullende optionele stappen kunnen worden genomen, zijn in de sectie Verwijzingen Hallo twee scripts tooset up Hallo-webserver en appserver met een eenvoudige web application tooallow testen met deze configuratie DMZ.

Hallo bevatten volgende secties een gedetailleerde beschrijving van Netwerkbeveiligingsgroepen en hoe ze werken in dit voorbeeld door de regels van de PowerShell-script Hallo doorlopen.

## <a name="network-security-groups-nsg"></a>Netwerkbeveiligingsgroepen (NSG's)
In dit voorbeeld is een groep NSG gebouwd en vervolgens geladen met zes regels. 

> [!TIP]
> In het algemeen moet u eerst uw specifieke regels voor 'Toestaan' maken en vervolgens laatste Hallo algemene "Deny" regels. Hallo toegewezen prioriteit bepaalt welke regels eerst worden geëvalueerd. Als verkeer tooapply tooa specifieke regel gevonden wordt, wordt er geen verdere regels worden geëvalueerd. NSG-regels kunnen toepassen in op Hallo binnenkomende of uitgaande richting (vanuit het perspectief van de Hallo van Hallo subnet).
> 
> 

Declaratief, worden Hallo volgens de regels voor binnenkomend verkeer gebouwd:

1. Interne DNS-verkeer (poort 53) is toegestaan
2. RDP-verkeer (poort 3389) van Hallo Internet tooany VM is toegestaan
3. HTTP-verkeer (poort 80) van Hallo tooweb internetserver (IIS01) is toegestaan
4. Verkeer (alle poorten) van IIS01 tooAppVM1 is toegestaan
5. Verkeer (alle poorten) van Hallo Internet toohello hele VNet (beide subnetten) is geweigerd.
6. Verkeer (alle poorten) van Hallo Frontend subnet toohello back-end-subnet is geweigerd

Met deze regels gebonden tooeach-subnet als een HTTP-aanvraag was binnenkomend van Hallo Internet toohello webserver beide regels 3 (toestaan) en 5 (weigeren) toepassing zou zijn, maar omdat de regel 3 heeft een hogere prioriteit alleen zou worden toegepast en regel 5 niet in de play zou komen. Hallo HTTP-aanvraag zou dus toohello webserver toegestaan. Als dat dezelfde verkeer tooreach hello DNS01 server probeerde, zou regel 5 (weigeren) zijn de eerste tooapply en Hallo verkeer Hallo zou niet toegestaan toopass toohello server. Regel 6 (weigeren) blokkeert Hallo Frontend subnet uit praten toohello back-end-subnet (met uitzondering van toegestane regels 1 en 4-verkeer), deze regelset beschermt Hallo back-end-netwerk als een aanvaller inbreuk Hallo webtoepassing op Hallo Frontend, Hallo aanvaller zou beperkte toegang toohello back-end '-beveiliging gebruiken' netwerk (alleen tooresources blootgesteld op Hallo AppVM01 server).

Er is een uitgaande standaardregel waarmee verkeer van toohello internet. Voor dit voorbeeld bent we uitgaand verkeer toestaat en alle regels voor uitgaande verbindingen niet wijzigen. toolock omlaag verkeer in beide richtingen, de gebruiker gedefinieerde routering is vereist en in 'Voorbeeld 3' is verkend op Hallo [Best Practices beveiligingspagina-grens][HOME].

Elke regel als volgt in detail beschreven (**Opmerking**: een item in de volgende lijst, te beginnen met een dollarteken Hallo (bijvoorbeeld: $NSGName) is een gebruiker gedefinieerde variabele uit het Hallo-script in Hallo verwijzing sectie van dit document):

1. Een Netwerkbeveiligingsgroep moet eerst toohold Hallo regels gebaseerd:

    ```PowerShell
    New-AzureNetworkSecurityGroup -Name $NSGName `
        -Location $DeploymentLocation `
        -Label "Security group for $VNetName subnets in $DeploymentLocation"
    ```

2. de eerste regel Hallo in dit voorbeeld kunt DNS-verkeer tussen alle interne netwerken toohello DNS-server op Hallo back-end-subnet. Hallo regel heeft enkele belangrijke parameters:
   
   * 'Typ' geeft aan in welke richting van verkeer met deze regel wordt van kracht. Hallo richting is vanuit Hallo perspectief van Hallo subnet of een virtuele Machine (afhankelijk van waar deze NSG is gekoppeld). Dus als Type is 'Inkomend' en verkeer is Hallo subnet invoeren, Hallo regel van toepassing en Hallo subnet uitgaand verkeer niet wordt beïnvloed door deze regel.
   * 'Prioriteit' stelt Hallo volgorde waarin netwerkverkeer wordt geëvalueerd. Hallo lagere Hallo nummer Hallo hogere Hallo prioriteit. Wanneer een regel van toepassing tooa specifieke netwerkverkeer is, kan er geen verdere regels worden verwerkt. Dus als een regel met prioriteit 1 gegevensverkeer, en een regel met prioriteit 2 verkeer weigert, en beide regels zijn van toepassing tootraffic vervolgens Hallo verkeer tooflow mogen (omdat de regel 1 een hogere prioriteit heeft geduurd effect en geen verdere regels zijn toegepast).
   * "Action" betekent dat verkeer dat is beïnvloed door deze regel is geblokkeerd of toegestaan.

    ```PowerShell    
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" `
        -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[4] `
        -DestinationPortRange '53' `
        -Protocol *
    ```

3. Deze regel kunnen de RDP-verkeer tooflow vanaf internet toohello RDP-poort op elke server op Hallo Hallo gebonden subnet. Deze regel maakt gebruik van twee speciale soorten adresvoorvoegsels; 'VIRTUAL_NETWORK' en 'INTERNET'. Deze tags zijn een eenvoudige manier tooaddress een grotere categorie van adresvoorvoegsels.

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" `
         -Type Inbound -Priority 110 -Action Allow `
         -SourceAddressPrefix INTERNET -SourcePortRange '*' `
         -DestinationAddressPrefix VIRTUAL_NETWORK `
         -DestinationPortRange '3389' `
         -Protocol *
    ```

4. Deze regel kunnen binnenkomende internet verkeer toohit Hallo webserver. Deze regel wordt het routeringsgedrag Hallo niet gewijzigd. Hallo regel kunnen alleen verkeer dat is bestemd voor IIS01 toopass. Dus als verkeer van Internet Hallo Hallo webserver als de bestemming voor deze regel zou toe te staan en stoppen met het verwerken van verdere regels had. (In de regel Hallo met prioriteit 140 alle andere Binnenkomend internetverkeer wordt geblokkeerd). Als u alleen HTTP-verkeer wordt verwerkt, met deze regel kan worden verder beperkt tooonly toestaan bestemming poort 80.

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable Internet too$VMName[0]" `
         -Type Inbound -Priority 120 -Action Allow `
         -SourceAddressPrefix Internet -SourcePortRange '*' `
         -DestinationAddressPrefix $VMIP[0] `
         -DestinationPortRange '*' `
         -Protocol *
    ```

5. Deze regel kan verkeer toopass van Hallo IIS01 server toohello AppVM01 server, een hoger regel blokkeert al het andere Frontend tooBackend verkeer. tooimprove deze regel als Hallo poort bekend is dat moet worden toegevoegd. Bijvoorbeeld, als Hallo IIS-server alleen SQL Server op AppVM01 roept is, Hallo Doelpoortbereik moet worden gewijzigd van ' * ' (Any) too1433 (hello SQL-poort) waardoor een kleinere inkomende kwetsbaarheid voor aanvallen op AppVM01 of webtoepassing Hallo ooit verdacht.

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable $VMName[1] too$VMName[2]" `
        -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[2] `
        -DestinationPortRange '*' `
        -Protocol *
    ```

6. Deze regel weigert verkeer van Hallo internet tooany servers op Hallo-netwerk. Met regels met prioriteit 110 en 120 Hallo Hallo effect is tooallow alleen inkomend verkeer toohello firewall voor internet- en RDP-poorten op servers en blokkeert al het andere. Deze regel is een 'veiligheidsmaatregel' regel tooblock alle onverwachte stromen.
    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate hello $VNetName VNet from hello Internet" `
        -Type Inbound -Priority 140 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *
    ```
7. de laatste regel Hallo weigert verkeer van Hallo Frontend subnet toohello back-end-subnet. Aangezien deze regel een inkomende regel alleen is, is (van Hallo back-end toohello Frontend) omgekeerde verkeer toegestaan.

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate hello $FESubnet subnet from hello $BESubnet subnet" `
        -Type Inbound -Priority 150 -Action Deny `
        -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
        -DestinationAddressPrefix $BEPrefix `
        -DestinationPortRange '*' `
        -Protocol * 
    ```

## <a name="traffic-scenarios"></a>Verkeer scenario 's
#### <a name="allowed-internet-tooweb-server"></a>(*Toegestane*) tooweb internetserver
1. Een internet-gebruiker aanvragen een pagina http-van FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)
2. Cloud service geeft verkeer via open eindpunten op poort 80 voor IIS01 (Hallo webserver)
3. Subnet frontend begint verwerking van inkomende regel:
   1. NSG regel 1 (DNS) niet van toepassing, toonext regel verplaatsen
   2. NSG regel 2 (RDP) niet van toepassing, toonext regel verplaatsen
   3. NSG regel 3 (Internet tooIIS01) is van toepassing, -verkeer is toegestaan, zelfs niet meer regelverwerking
4. Verkeer komt binnen via interne IP-adres van de webserver Hallo IIS01 (10.0.1.5)
5. IIS01 luistert voor internetverkeer, ontvangt deze aanvraag en begint met de verwerking van Hallo-aanvraag
6. IIS01 vraagt Hallo SQL Server op AppVM01 voor meer informatie
7. Aangezien er geen uitgaande regels op subnet Frontend zijn, is verkeer toegestaan
8. Hallo back-end subnet begint verwerking van inkomende regel:
   1. NSG regel 1 (DNS) niet van toepassing, toonext regel verplaatsen
   2. NSG regel 2 (RDP) niet van toepassing, toonext regel verplaatsen
   3. NSG regel 3 (Internet tooFirewall) niet van toepassing, toonext regel verplaatsen
   4. NSG regel 4 (IIS01 tooAppVM01) is van toepassing, -verkeer is toegestaan, zelfs niet meer regelverwerking
9. AppVM01 ontvangen Hallo SQL-Query en beantwoord
10. Aangezien er geen uitgaande regels op Hallo back-end-subnet zijn, is antwoord Hallo toegestaan
11. Subnet frontend begint verwerking van inkomende regel:
    1. Er is geen NSG-regel die van toepassing tooInbound verkeer van Hallo back-end subnet toohello Frontend subnet, is zodat geen van Hallo NSG-regels toepassen
    2. Hallo system standaardregel verkeer tussen subnetten zou dit verkeer toestaan zodat Hallo verkeer is toegestaan.
12. Hallo SQL antwoord wordt ontvangen en Hallo HTTP-antwoord is voltooid en toohello aanvrager verzendt Hallo IIS-server
13. Aangezien er geen uitgaande regels op Hallo Frontend subnet zijn hello antwoord is toegestaan en hello internet ontvangt Hallo webpagina aangevraagd.

#### <a name="allowed-rdp-toobackend"></a>(*Toegestane*) RDP toobackend
1. RDP-sessie tooAppVM01 op BackEnd001.CloudApp.Net:xxxxx waarbij xxxxx Hallo willekeurig toegewezen poort voor RDP tooAppVM01 is serverbeheerder op internet-aanvragen (Hallo toegewezen poort kan worden gevonden op Hallo Azure-portal of via PowerShell)
2. Subnet backend begint verwerking van inkomende regel:
   1. NSG regel 1 (DNS) niet van toepassing, toonext regel verplaatsen
   2. NSG regel 2 (RDP) is van toepassing, -verkeer is toegestaan, zelfs niet meer regelverwerking
3. Er is geen uitgaande regels standaardregels toepassen en terugkerend verkeer is toegestaan
4. RDP-sessie is ingeschakeld
5. AppVM01 wordt u gevraagd om het Hallo-gebruikersnaam en wachtwoord

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a>(*Toegestane*) Web server opzoeken in DNS op DNS-server
1. Web-Server, IIS01, moeten een gegevensfeed op www.data.gov, maar moet tooresolve Hallo adres.
2. Hallo netwerkconfiguratie voor Hallo VNet lijsten DNS01 (10.0.2.4 op Hallo back-end subnet) als het primaire DNS-server hello, IIS01 verzendt Hallo DNS-aanvraag tooDNS01
3. Er is geen uitgaande regels op subnet Frontend verkeer wordt toegestaan.
4. Subnet backend begint verwerking van inkomende regel:
   * NSG regel 1 (DNS) is van toepassing, -verkeer is toegestaan, zelfs niet meer regelverwerking
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

#### <a name="allowed-web-server-access-file-on-appvm01"></a>(*Toegestane*) Web server toegang tot bestand op AppVM01
1. IIS01 vraagt om een bestand op AppVM01
2. Er is geen uitgaande regels op subnet Frontend verkeer wordt toegestaan.
3. Hallo back-end subnet begint verwerking van inkomende regel:
   1. NSG regel 1 (DNS) niet van toepassing, toonext regel verplaatsen
   2. NSG regel 2 (RDP) niet van toepassing, toonext regel verplaatsen
   3. NSG regel 3 (Internet tooIIS01) niet van toepassing, toonext regel verplaatsen
   4. NSG regel 4 (IIS01 tooAppVM01) is van toepassing, -verkeer is toegestaan, zelfs niet meer regelverwerking
4. AppVM01 hello aanvraag ontvangt en reageert met bestand (ervan uitgaande dat toegang wordt geverifieerd)
5. Aangezien er geen uitgaande regels op Hallo back-end-subnet zijn, is antwoord Hallo toegestaan
6. Subnet frontend begint verwerking van inkomende regel:
   1. Er is geen NSG-regel die van toepassing tooInbound verkeer van Hallo back-end subnet toohello Frontend subnet, is zodat geen van Hallo NSG-regels toepassen
   2. Hallo system standaardregel verkeer tussen subnetten zou dit verkeer toestaan zodat Hallo verkeer is toegestaan.
7. Hallo IIS server ontvangt Hallo-bestand

#### <a name="denied-web-toobackend-server"></a>(*Geweigerd*) toobackend webserver
1. Een internet-gebruiker probeert een bestand op AppVM01 via Hallo BackEnd001.CloudApp.Net service tooaccess
2. Aangezien er geen eindpunten voor de bestandsshare is geopend zijn, dit verkeer zou Hallo Cloudservice niet doorgeven en wouldn't Hallo-server niet bereiken
3. Als het Hallo-eindpunten zijn geopend voor een bepaalde reden, wordt NSG regel 5 (Internet tooVNet) dit verkeer geblokkeerd

#### <a name="denied-web-dns-look-up-on-dns-server"></a>(*Geweigerd*) opzoeken in Web DNS op DNS-server
1. Een internet-gebruiker probeert toolook van een interne DNS-record op DNS01 via Hallo BackEnd001.CloudApp.Net service
2. Aangezien er geen eindpunten voor DNS is geopend zijn, dit verkeer zou Hallo Cloudservice niet doorgeven en wouldn't Hallo-server niet bereiken
3. Als het Hallo-eindpunten zijn geopend voor een bepaalde reden, NSG regel 5 (Internet tooVNet) dit verkeer wordt geblokkeerd (Opmerking: deze regel 1 (DNS) is niet van toepassing om twee redenen, eerste Hallo-bronadres is internet Hallo, deze regel is alleen van toepassing toohello lokale VNet als Hallo bron ook Deze regel wordt een regel voor toestaan, zodat deze zou nooit verkeer weigeren)

#### <a name="denied-web-toosql-access-through-firewall"></a>(*Geweigerd*) tooSQL webtoegang via firewall
1. Een internetgebruiker opvraagt SQL-gegevens uit FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)
2. Aangezien er geen eindpunten geopend voor SQL zijn, dit verkeer zou Hallo Cloudservice niet doorgeven en Hallo firewall wouldn't bereiken
3. Als eindpunten geopend voor een bepaalde reden zijn, begint Hallo Frontend subnet verwerking van inkomende regel:
   1. NSG regel 1 (DNS) niet van toepassing, toonext regel verplaatsen
   2. NSG regel 2 (RDP) niet van toepassing, toonext regel verplaatsen
   3. NSG regel 3 (Internet tooIIS01) is van toepassing, -verkeer is toegestaan, zelfs niet meer regelverwerking
4. Verkeer komt binnen via interne IP-adres van Hallo IIS01 (10.0.1.5)
5. IIS01 wordt niet geluisterd op poort 1433, zodat er geen reactie toohello aanvraag

## <a name="conclusion"></a>Conclusie
In dit voorbeeld is een relatief eenvoudige en meteen verder manier Hallo back-end subnet uit binnenkomend verkeer isoleren.

Meer voorbeelden en een overzicht van het netwerk beveiligingsgrenzen vindt [hier][HOME].

## <a name="references"></a>Verwijzingen
### <a name="main-script-and-network-config"></a>Belangrijkste script en netwerk-configuratie
Hallo volledige Script opslaat in een PowerShell-scriptbestand. Sla Hallo netwerkconfiguratie naar een bestand met de naam 'NetworkConf1.xml'.
De gebruiker gedefinieerde variabelen Hallo als nodig en Voer Hallo script wijzigen.

#### <a name="full-script"></a>Volledige script
Dit script wordt, op basis van Hallo door gebruiker gedefinieerde variabelen.

1. Verbinding maken met tooan Azure-abonnement
2. Een opslagaccount maken
3. Een VNet en twee subnetten zoals gedefinieerd in het configuratiebestand voor Hallo netwerk maken
4. Vier windows server-VM's maken
5. Configureer het NSG inclusief:
   * Maken van een NSG
   * Met regels in te vullen
   * Binding Hallo NSG toohello juiste subnetten

Deze PowerShell-script moet lokaal op worden uitgevoerd dat een internet verbonden PC of de server.

> [!IMPORTANT]
> Wanneer dit script wordt uitgevoerd, kunnen er waarschuwingen of andere informatieve berichten die pop in PowerShell. Alleen foutberichten in rood zijn aanleiding.
> 
>

```PowerShell
<# 
 .SYNOPSIS
  Example of Network Security Groups in an isolated network (Azure only, no hybrid connections)

 .DESCRIPTION
  This script will build out a sample DMZ setup containing:
   - A default storage account for VM disks
   - Two new cloud services
   - Two Subnets (FrontEnd and BackEnd subnets)
   - One server on hello FrontEnd Subnet
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

# User-Defined Global Variables
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
    $NetworkConfigFile = "C:\Scripts\NetworkConf1.xml"

  # VM Base Disk Image Details
    $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

  # NSG Details
    $NSGName = "MyVNetSG"

# User-Defined VM Specific Configuration
    # Note: tooensure proper NSG Rule creation later in this script:
    #       - hello Web Server must be VM 0
    #       - hello AppVM1 Server must be VM 1
    #       - hello DNS server must be VM 3
    #
    #       Otherwise hello NSG rules in hello last section of this
    #       script will need toobe changed toomatch hello modified
    #       VM array numbers ($i) so hello NSG Rule IP addresses
    #       are aligned toohello associated VM IP addresses.

    # VM 0 - hello Web Server
      $VMName += "IIS01"
      $ServiceName += $FrontEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $FESubnet
      $VMIP += "10.0.1.5"

    # VM 1 - hello First Application Server
      $VMName += "AppVM01"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.5"

    # VM 2 - hello Second Application Server
      $VMName += "AppVM02"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.6"

    # VM 3 - hello DNS Server
      $VMName += "DNS01"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.4"

# ----------------------------- #
# No User-Defined Variables or  #
# Configuration past this point #
# ----------------------------- #    

  # Get your Azure accounts
    Add-AzureAccount
    Set-AzureSubscription –SubscriptionId $subID -ErrorAction Stop
    Select-AzureSubscription -SubscriptionId $subID -Current -ErrorAction Stop

  # Create Storage Account
    If (Test-AzureName -Storage -Name $StorageAccountName) { 
        Write-Host "Fatal Error: This storage account name is already in use, please pick a different name." -ForegroundColor Red
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
Else { Write-Host "hello network configuration file was found" -ForegroundColor Green
        If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
            Write-Host 'hello deployment location was not found in hello network config file, please check hello network config file tooensure hello $DeploymentLocation variable is correct and hello network config file matches.' -ForegroundColor Yellow
            $FatalError = $true}
        Else { Write-Host "hello deployment location was found in hello network config file." -ForegroundColor Green}}

If ($FatalError) {
    Write-Host "A fatal error has occurred, please see hello above messages for more information." -ForegroundColor Red
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
        New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
            Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
            Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
            Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
            Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
            Remove-AzureEndpoint -Name "PowerShell" | `
            New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
            # Note: A Remote Desktop endpoint is automatically created when each VM is created.
        $i++
    }
    # Add HTTP Endpoint for IIS01
    Get-AzureVM -ServiceName $ServiceName[0] -Name $VMName[0] | Add-AzureEndpoint -Name HTTP -Protocol tcp -LocalPort 80 -PublicPort 80 | Update-AzureVM

# Configure NSG
    Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

  # Build hello NSG
    Write-Host "Building hello NSG" -ForegroundColor Cyan
    New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

  # Add NSG Rules
    Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[3] -DestinationPortRange '53' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet too$($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
        -SourceAddressPrefix Internet -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[0]) too$($VMName[1])" -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[0] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[1] -DestinationPortRange '*' `
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
  # Install Test Web App (Run Post-Build Script on hello IIS Server)
  # Install Backend resource (Run Post-Build Script on hello AppVM01)
  Write-Host
  Write-Host "Build Complete!" -ForegroundColor Green
  Write-Host
  Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
  Write-Host " - Install Test Web App (Run Post-Build Script on hello IIS Server)" -ForegroundColor Gray
  Write-Host " - Install Backend resource (Run Post-Build Script on hello AppVM01)" -ForegroundColor Gray
  Write-Host
```

#### <a name="network-config-file"></a>Netwerk-configuratiebestand
Dit xml-bestand opslaan met bijgewerkte locatie en Hallo koppeling toothis bestand toohello $NetworkConfigFile variabele toevoegen in Hallo vóór het script.

```XML
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
```

#### <a name="sample-application-scripts"></a>Voorbeeldscripts toepassing
Als u een voorbeeldtoepassing tooinstall voor deze en andere voorbeelden van het Perimeternetwerk wilt, een is opgegeven op de koppeling Hallo: [voorbeeldscript toepassing][SampleApp]

## <a name="next-steps"></a>Volgende stappen
* Bijwerken en XML-bestand opslaan
* Hallo PowerShell script toobuild Hallo-omgeving uitvoeren
* Hallo-voorbeeldtoepassing installeren
* Ander verkeer stroomt via deze DMZ testen

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-asm/example1design.png "Inkomende DMZ met NSG"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md

