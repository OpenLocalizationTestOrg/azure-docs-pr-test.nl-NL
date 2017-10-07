---
title: "aaaAzure DMZ voorbeeld – een eenvoudige DMZ met nsg's bouwen | Microsoft Docs"
description: Maken van een DMZ met Netwerkbeveiligingsgroepen (NSG)
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: 11c5c6026da30fbc9c5e585f5c16e2d411d6fd80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-an-azure-resource-manager-template"></a>Voorbeeld 1: een eenvoudige DMZ met nsg's met een Azure Resource Manager-sjabloon maken
[Best Practices beveiligingspagina-grens toohello retourneren][HOME]

> [!div class="op_single_selector"]
> * [Resource Manager-sjabloon](virtual-networks-dmz-nsg.md)
> * [Klassieke - PowerShell](virtual-networks-dmz-nsg-asm.md)
> 
>

In dit voorbeeld maakt een primitieve DMZ met vier Windows-servers en Netwerkbeveiligingsgroepen. In dit voorbeeld worden alle Hallo gewenste sjabloon secties tooprovide een beter begrip van elke stap beschreven. Er is ook een sectie verkeer Scenario tooprovide een diepgaande stapsgewijze blik op hoe verkeer Hallo lagen verdediging in Hallo DMZ doorlopen. Ten slotte is in de sectie Verwijzingen Hallo het Hallo volledige sjabloon code en instructies toobuild deze omgeving tootest en experiment met verschillende scenario's. 

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)] 

![Inkomende DMZ met NSG][1]

## <a name="environment-description"></a>Beschrijving van de omgeving
In dit voorbeeld bevat een abonnement Hallo resources te volgen:

* Één resourcegroep
* Een virtueel netwerk met twee subnetten; 'FrontEnd' en back-end'
* Een Netwerkbeveiligingsgroep die toegepaste tooboth subnetten
* Een Windows-Server waarmee een toepassing webserver ('IIS01')
* Twee windows-servers die vertegenwoordigen toepassingsservers van back-end ('AppVM01', 'AppVM02')
* Een Windows-server met een DNS-server ('DNS01')
* Een openbaar IP-adres die zijn gekoppeld aan de webserver Hallo-toepassing

In de sectie Verwijzingen hello is er een koppeling tooan Azure Resource Manager-sjabloon die Hallo-omgeving beschreven in dit voorbeeld voortbouwt. Gebouw Hallo VM's en virtuele netwerken worden Hoewel uitgevoerd door Hallo voorbeeldsjabloon, niet in dit document uitvoeriger beschreven. 

**toobuild deze omgeving** (gedetailleerde instructies vindt u in Hallo verwijzingen sectie van dit document);

1. Implementatie van Azure Resource Manager-sjabloon op Hallo: [Azure Quick Start-sjablonen][Template]
2. Installeren van de voorbeeldtoepassing Hallo op: [voorbeeldscript toepassing][SampleApp]

>[!NOTE]
>tooRDP tooany back-end-servers in dit geval wordt Hallo IIS-server wordt gebruikt als een 'jump vak'. Eerste RDP toohello IIS-server en vervolgens naar Hallo IIS Server RDP toohello back-end-server. Een openbaar IP-adres kan ook worden gekoppeld aan elke server NIC voor RDP eenvoudiger.
> 
>

Hallo bevatten volgende secties een gedetailleerde beschrijving van Hallo Netwerkbeveiligingsgroep en hoe werkt dit voorbeeld door de stap voor stap regels Hallo Azure Resource Manager-sjabloon.

## <a name="network-security-groups-nsg"></a>Netwerkbeveiligingsgroepen (NSG's)
In dit voorbeeld is een groep NSG gebouwd en vervolgens geladen met zes regels. 

>[!TIP]
>In het algemeen moet u eerst uw specifieke regels voor 'Toestaan' maken en vervolgens laatste Hallo algemene "Deny" regels. Hallo toegewezen prioriteit bepaalt welke regels eerst worden geëvalueerd. Als verkeer tooapply tooa specifieke regel gevonden wordt, wordt er geen verdere regels worden geëvalueerd. NSG-regels kunnen toepassen in op Hallo binnenkomende of uitgaande richting (vanuit het perspectief van de Hallo van Hallo subnet).
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

Er is een uitgaande standaardregel waarmee verkeer van toohello internet. Voor dit voorbeeld bent we uitgaand verkeer toestaat en alle regels voor uitgaande verbindingen niet wijzigen. tooapply beveiliging beleid tootraffic in beide richtingen, de gebruiker gedefinieerde routering is vereist en in 'Voorbeeld 3' is verkend op Hallo [Best Practices beveiligingspagina-grens][HOME].

Elke regel is als volgt in meer detail besproken:

1. De bron van een Netwerkbeveiligingsgroep moet geïnstantieerd toohold Hallo regels:

    ```JSON
    "resources": [
      {
        "apiVersion": "2015-05-01-preview",
        "type": "Microsoft.Network/networkSecurityGroups",
        "name": "[variables('NSGName')]",
        "location": "[resourceGroup().location]",
        "properties": { }
      }
    ]
    ``` 

2. de eerste regel Hallo in dit voorbeeld kunt DNS-verkeer tussen alle interne netwerken toohello DNS-server op Hallo back-end-subnet. Hallo regel heeft enkele belangrijke parameters:
  * 'destinationAddressPrefix' - regels kunnen gebruiken een speciaal type adresvoorvoegsel een "standaard code' genoemd, deze tags zijn systeem-id's die een grotere categorie van adresvoorvoegsels voor een eenvoudige manier tooaddress toestaan. Deze regel gebruikt standaard Tag 'Internet' Hallo toosignify een adres buiten Hallo VNet. Andere labels voorvoegsel zijn VirtualNetwork en AzureLoadBalancer.
  * 'Richting' geeft aan in welke richting van verkeer met deze regel wordt van kracht. Hallo richting is vanuit Hallo perspectief van Hallo subnet of een virtuele Machine (afhankelijk van waar deze NSG is gekoppeld). Dus als richting is 'Inkomend' en verkeer is Hallo subnet invoeren, Hallo regel van toepassing en Hallo subnet uitgaand verkeer niet wordt beïnvloed door deze regel.
  * 'Prioriteit' stelt Hallo volgorde waarin netwerkverkeer wordt geëvalueerd. Hallo lagere Hallo nummer Hallo hogere Hallo prioriteit. Wanneer een regel van toepassing tooa specifieke netwerkverkeer is, kan er geen verdere regels worden verwerkt. Dus als een regel met prioriteit 1 gegevensverkeer, en een regel met prioriteit 2 verkeer weigert, en beide regels zijn van toepassing tootraffic vervolgens Hallo verkeer tooflow mogen (omdat de regel 1 een hogere prioriteit heeft geduurd effect en geen verdere regels zijn toegepast).
  * 'Toegang' geeft aan of verkeer dat is beïnvloed door deze regel is geblokkeerd ("Deny") of toegestane ('toestaan').

    ```JSON
    "properties": {
    "securityRules": [
      {
        "name": "enable_dns_rule",
        "properties": {
          "description": "Enable Internal DNS",
          "protocol": "*",
          "sourcePortRange": "*",
          "destinationPortRange": "53",
          "sourceAddressPrefix": "VirtualNetwork",
          "destinationAddressPrefix": "10.0.2.4",
          "access": "Allow",
          "priority": 100,
          "direction": "Inbound"
        }
      },
    ```

3. Deze regel kunnen de RDP-verkeer tooflow vanaf internet toohello RDP-poort op elke server op Hallo Hallo gebonden subnet. 

    ```JSON
    {
      "name": "enable_rdp_rule",
      "properties": {
        "description": "Allow RDP",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "3389",
        "sourceAddressPrefix": "*",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 110,
        "direction": "Inbound"
      }
    },
    ```

4. Deze regel kunnen binnenkomende internet verkeer toohit Hallo webserver. Deze regel wordt het routeringsgedrag Hallo niet gewijzigd. Hallo regel kunnen alleen verkeer dat is bestemd voor IIS01 toopass. Dus als verkeer van Internet Hallo Hallo webserver als de bestemming voor deze regel zou toe te staan en stoppen met het verwerken van verdere regels had. (In de regel Hallo met prioriteit 140 alle andere Binnenkomend internetverkeer wordt geblokkeerd). Als u alleen HTTP-verkeer wordt verwerkt, met deze regel kan worden verder beperkt tooonly toestaan bestemming poort 80.

    ```JSON
    {
      "name": "enable_web_rule",
      "properties": {
        "description": "Enable Internet too[variables('VM01Name')]",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "80",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "10.0.1.5",
        "access": "Allow",
        "priority": 120,
        "direction": "Inbound"
        }
      },
    ```

5. Deze regel kan verkeer toopass van Hallo IIS01 server toohello AppVM01 server, een hoger regel blokkeert al het andere Frontend tooBackend verkeer. tooimprove deze regel als Hallo poort bekend is dat moet worden toegevoegd. Bijvoorbeeld, als Hallo IIS-server alleen SQL Server op AppVM01 roept is, Hallo Doelpoortbereik moet worden gewijzigd van ' * ' (Any) too1433 (hello SQL-poort) waardoor een kleinere inkomende kwetsbaarheid voor aanvallen op AppVM01 of webtoepassing Hallo ooit verdacht.

    ```JSON
    {
      "name": "enable_app_rule",
      "properties": {
        "description": "Enable [variables('VM01Name')] too[variables('VM02Name')]",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "10.0.1.5",
        "destinationAddressPrefix": "10.0.2.5",
        "access": "Allow",
        "priority": 130,
        "direction": "Inbound"
      }
    },
     ```

6. Deze regel weigert verkeer van Hallo internet tooany servers op Hallo-netwerk. Met regels met prioriteit 110 en 120 Hallo Hallo effect is tooallow alleen inkomend verkeer toohello firewall voor internet- en RDP-poorten op servers en blokkeert al het andere. Deze regel is een 'veiligheidsmaatregel' regel tooblock alle onverwachte stromen.

    ```JSON
    {
      "name": "deny_internet_rule",
      "properties": {
        "description": "Isolate hello [variables('VNetName')] VNet from hello Internet",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "VirtualNetwork",
        "access": "Deny",
        "priority": 140,
        "direction": "Inbound"
      }
    },
     ```

7. de laatste regel Hallo weigert verkeer van Hallo Frontend subnet toohello back-end-subnet. Aangezien deze regel een inkomende regel alleen is, is (van Hallo back-end toohello Frontend) omgekeerde verkeer toegestaan.

    ```JSON
    {
      "name": "deny_frontend_rule",
      "properties": {
        "description": "Isolate hello [variables('Subnet1Name')] subnet from hello [variables('Subnet2Name')] subnet",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "[variables('Subnet1Prefix')]",
        "destinationAddressPrefix": "[variables('Subnet2Prefix')]",
        "access": "Deny",
        "priority": 150,
        "direction": "Inbound"
      }
    }
    ```

## <a name="traffic-scenarios"></a>Verkeer scenario 's
#### <a name="allowed-internet-tooweb-server"></a>(*Toegestane*) tooweb internetserver
1. Een internet-gebruiker aanvragen een pagina http-van het openbare IP-adres Hallo Hallo NIC die is gekoppeld aan Hallo IIS01 NIC
2. Hallo openbare IP-adres wordt doorgegeven verkeer toohello VNet naar IIS01 (Hallo webserver)
3. Subnet frontend begint verwerking van inkomende regel:
  1. NSG regel 1 (DNS) niet van toepassing, toonext regel verplaatsen
  2. NSG regel 2 (RDP) niet van toepassing, toonext regel verplaatsen
  3. NSG regel 3 (Internet tooIIS01) is van toepassing, -verkeer is toegestaan, zelfs niet meer regelverwerking
4. Verkeer komt binnen via interne IP-adres van de webserver Hallo IIS01 (10.0.1.5)
5. IIS01 luistert voor internetverkeer, ontvangt deze aanvraag en begint met de verwerking van Hallo-aanvraag
6. IIS01 vraagt Hallo SQL Server op AppVM01 voor meer informatie
7. Er is geen uitgaande regels op subnet Frontend verkeer wordt toegestaan.
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
13. Aangezien er geen uitgaande regels op Hallo Frontend subnet zijn, antwoord Hallo is toegestaan en Hallo Internet-gebruiker ontvangt Hallo webpagina aangevraagd.

#### <a name="allowed-rdp-tooiis-server"></a>(*Toegestane*) RDP tooIIS server
1. Een serverbeheerder op internet vraagt een tooIIS01 RDP-sessie op het openbare IP-adres Hallo Hallo NIC die is gekoppeld aan Hallo IIS01 NIC (dit openbare IP-adres kan worden gevonden via Hallo Portal of PowerShell)
2. Hallo openbare IP-adres wordt doorgegeven verkeer toohello VNet naar IIS01 (Hallo webserver)
3. Subnet frontend begint verwerking van inkomende regel:
  1. NSG regel 1 (DNS) niet van toepassing, toonext regel verplaatsen
  2. NSG regel 2 (RDP) is van toepassing, -verkeer is toegestaan, zelfs niet meer regelverwerking
4. Er is geen uitgaande regels standaardregels toepassen en terugkerend verkeer is toegestaan
5. RDP-sessie is ingeschakeld
6. IIS01 wordt u gevraagd om het Hallo-gebruikersnaam en wachtwoord

>[!NOTE]
>tooRDP tooany back-end-servers in dit geval wordt Hallo IIS-server wordt gebruikt als een 'jump vak'. Eerste RDP toohello IIS-server en vervolgens naar Hallo IIS Server RDP toohello back-end-server.
>
>

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

#### <a name="denied-rdp-toobackend"></a>(*Geweigerd*) RDP toobackend
1. Een internet-gebruiker probeert tooRDP tooserver AppVM01
2. Aangezien er geen openbare IP-adressen die zijn gekoppeld aan deze servers NIC zijn, dit verkeer voert nooit Hallo VNet en wouldn't Hallo-server niet bereiken
3. Maar als een openbaar IP-adres is ingeschakeld voor een bepaalde reden, NSG-regel 2 (RDP) zou dit verkeer toestaan

>[!NOTE]
>tooRDP tooany back-end-servers in dit geval wordt Hallo IIS-server wordt gebruikt als een 'jump vak'. Eerste RDP toohello IIS-server en vervolgens naar Hallo IIS Server RDP toohello back-end-server.
>
>

#### <a name="denied-web-toobackend-server"></a>(*Geweigerd*) toobackend webserver
1. Een internet-gebruiker probeert een bestand op AppVM01 tooaccess
2. Aangezien er geen openbare IP-adressen die zijn gekoppeld aan deze servers NIC zijn, dit verkeer voert nooit Hallo VNet en wouldn't Hallo-server niet bereiken
3. Als een openbaar IP-adres is ingeschakeld voor een bepaalde reden, wordt NSG regel 5 (Internet tooVNet) dit verkeer geblokkeerd

#### <a name="denied-web-dns-look-up-on-dns-server"></a>(*Geweigerd*) opzoeken in Web DNS op DNS-server
1. Een internet-gebruiker probeert toolook van een interne DNS-record op DNS01
2. Aangezien er geen openbare IP-adressen die zijn gekoppeld aan deze servers NIC zijn, dit verkeer voert nooit Hallo VNet en wouldn't Hallo-server niet bereiken
3. Als een openbaar IP-adres is ingeschakeld voor een bepaalde reden, NSG regel 5 (Internet tooVNet) dit verkeer wordt geblokkeerd (Opmerking: of regel 1 (DNS) niet van toepassing hello verzoeken bronadres is internet Hallo en regel 1 zijn alleen van toepassing toohello lokale VNet als Hallo bron)

#### <a name="denied-sql-access-on-hello-web-server"></a>(*Geweigerd*) toegang tot SQL op Hallo-webserver
1. Een internetgebruiker opvraagt SQL-gegevens uit IIS01
2. Aangezien er geen openbare IP-adressen die zijn gekoppeld aan deze servers NIC zijn, dit verkeer voert nooit Hallo VNet en wouldn't Hallo-server niet bereiken
3. Als een openbaar IP-adres is ingeschakeld voor een bepaalde reden, begint Hallo Frontend subnet verwerking van inkomende regel:
  1. NSG regel 1 (DNS) niet van toepassing, toonext regel verplaatsen
  2. NSG regel 2 (RDP) niet van toepassing, toonext regel verplaatsen
  3. NSG regel 3 (Internet tooIIS01) is van toepassing, -verkeer is toegestaan, zelfs niet meer regelverwerking
4. Verkeer komt binnen via interne IP-adres van Hallo IIS01 (10.0.1.5)
5. IIS01 wordt niet geluisterd op poort 1433, zodat er geen reactie toohello aanvraag

## <a name="conclusion"></a>Conclusie
In dit voorbeeld is een relatief eenvoudige en meteen verder manier Hallo back-end subnet uit binnenkomend verkeer isoleren.

Meer voorbeelden en een overzicht van het netwerk beveiligingsgrenzen vindt [hier][HOME].

## <a name="references"></a>Verwijzingen
### <a name="azure-resource-manager-template"></a>Azure Resource Manager-sjabloon
In dit voorbeeld wordt een vooraf gedefinieerde Azure Resource Manager-sjabloon gebruikt in een door Microsoft beheerde GitHub-opslagplaats en open toohello community. Deze sjabloon kan worden geïmplementeerd rechtstreeks uit de GitHub of gedownload en gewijzigd toofit uw behoeften. 

Hallo belangrijkste sjabloon is in het Hallo-bestand met de naam 'azuredeploy.json'. Deze sjabloon kan worden verzonden via PowerShell of CLI (met Hallo gekoppeld 'azuredeploy.parameters.json'-bestand) toodeploy deze sjabloon. Ik vinden Hallo eenvoudigste manier is toouse Hallo 'TooAzure implementeren' knop op Hallo README.md pagina op GitHub.

toodeploy hello sjabloon die in dit voorbeeld voortbouwt GitHub en hello Azure-portal, als volgt te werk:

1. Navigeer via een browser toohello [sjabloon][Template]
2. Klik op Hallo 'TooAzure implementeren' knop (of Hallo 'Visualiseren' knop toosee een grafische weergave van deze sjabloon)
3. Hallo Storage-Account, gebruikersnaam en wachtwoord invoeren in de blade Parameters Hallo en klik vervolgens op **OK**
5. Maak een resourcegroep voor deze implementatie (u kunt een bestaande, maar ik het beste een nieuw wachtwoord voor de beste resultaten)
6. Wijzig indien nodig, Hallo abonnement en de locatie-instellingen voor uw VNet.
7. Klik op **juridische voorwaarden bekijken**, Hallo voorwaarden lezen en klikt u op **aankoop** tooagree.
8. Klik op **maken** toobegin Hallo implementatie van deze sjabloon.
9. Nadat de Hallo-implementatie wordt voltooid, gaat u toohello die resourcegroep voor deze implementatie toosee Hallo bronnen gemaakt binnen geconfigureerd.

>[!NOTE]
>Deze sjabloon kunt RDP toohello IIS01 alleen server (zoeken hello openbare IP-adres voor IIS01 op Hallo Portal). tooRDP tooany back-end-servers in dit geval wordt Hallo IIS-server wordt gebruikt als een 'jump vak'. Eerste RDP toohello IIS-server en vervolgens naar Hallo IIS Server RDP toohello back-end-server.
>
>

tooremove voor deze implementatie, delete Hallo resourcegroep en alle onderliggende resources worden eveneens verwijderd.

#### <a name="sample-application-scripts"></a>Voorbeeldscripts toepassing
Als Hallo sjabloon uitgevoerd is, kunt u met een eenvoudige web application tooallow testen met deze configuratie DMZ up Hallo-webserver en appserver instellen. een voorbeeldtoepassing voor deze en andere voorbeelden DMZ tooinstall, een is opgegeven op de koppeling Hallo: [voorbeeldscript toepassing][SampleApp]

## <a name="next-steps"></a>Volgende stappen

* In dit voorbeeld implementeren
* Hallo-voorbeeldtoepassing bouwen
* Ander verkeer stroomt via deze DMZ testen

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-arm/example1design.png "Inkomende DMZ met NSG"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[Template]: https://github.com/Azure/azure-quickstart-templates/tree/master/301-dmz-nsg
[SampleApp]: ./virtual-networks-sample-app.md