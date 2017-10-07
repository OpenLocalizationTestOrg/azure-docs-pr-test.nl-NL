---
title: aaaLayered beveiligingsarchitectuur met App Service-omgevingen
description: Het implementeren van een gelaagd beveiligingsarchitectuur met App Service-omgevingen.
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 73ce0213-bd3e-4876-b1ed-5ecad4ad5601
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/30/2016
ms.author: stefsch
ms.openlocfilehash: 0627ba6fa849908506fe62c451c888c147cabc03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="implementing-a-layered-security-architecture-with-app-service-environments"></a>Implementatie van een gelaagd beveiligingsarchitectuur met App Service-omgevingen
## <a name="overview"></a>Overzicht
Omdat App Service-omgevingen een geïsoleerde runtime-omgeving in een virtueel netwerk geïmplementeerd bieden, kunnen ontwikkelaars een gelaagd beveiligingsarchitectuur bieden verschillende niveaus van toegang tot het netwerk voor elke toepassingslaag fysieke maken.

Een algemene streven toohide API-back-ends van algemene toegang tot het Internet is en dat alleen API's toobe aangeroepen door de upstream-web-apps.  [Netwerkbeveiligingsgroepen (nsg's)] [ NetworkSecurityGroups] op subnetten met App Service-omgevingen toorestrict openbare toegang tooAPI toepassingen kunnen worden gebruikt.

Hallo diagram hieronder toont een voorbeeld-architectuur met een WebAPI op basis van app geïmplementeerd op een App Service-omgeving.  Drie afzonderlijke web app-exemplaren, geïmplementeerd op drie aparte App Service-omgevingen, Controleer back-end-aanroepen toohello dezelfde WebAPI-app.

![Conceptionele architectuur][ConceptualArchitecture] 

Hallo groen plusteken aangeven dat Hallo netwerkbeveiligingsgroep op Hallo subnet met 'apiase' kunt binnenkomende oproepen van Hallo upstream web-apps, als ook aanroepen van zichzelf.  Maar Hallo dezelfde netwerkbeveiligingsgroep expliciet geweigerd toegang toogeneral binnenkomend verkeer van Hallo Internet. 

netwerkbeveiligingsgroep van Hallo stappen nodig tooconfigure Hallo Hallo rest van dit onderwerp wordt uitgelegd op Hallo subnet met 'apiase'.

## <a name="determining-hello-network-behavior"></a>Hallo netwerkverkeer bepalen
In de volgorde tooknow moet welke netwerkbeveiliging regels nodig zijn, u toodetermine welke netwerkclients krijgt tooreach Hallo App Service-omgeving met Hallo API-app en welke clients worden geblokkeerd.

Aangezien [netwerkbeveiligingsgroepen (nsg's)] [ NetworkSecurityGroups] zijn toegepaste toosubnets en App Service-omgevingen zijn geïmplementeerd in subnetten, toepassing hello regels in een NSG te**alle** Apps die worden uitgevoerd op een App Service-omgeving.  Hallo voorbeeldarchitectuur voor dit artikel met zodra een netwerkbeveiligingsgroep toegepaste toohello subnet 'apiase' alle apps die worden uitgevoerd op Hallo 'apiase is' App Service-omgeving worden beveiligd door Hallo met set dezelfde beveiligingsregels voor verbindingen. 

* **Hallo uitgaande IP-adres van de upstream-aanroepfuncties bepalen:** wat is er of Hallo IP-adressen van Hallo upstream aanroepfuncties?  Deze adressen moet expliciet toegang is toegestaan in Hallo NSG toobe.  Omdat aanroepen tussen App Service-omgevingen worden beschouwd als 'Internet' aanroepen, betekent dit Hallo uitgaande IP-adres toegewezen tooeach van Hallo drie upstream-App Service-omgevingen behoeften toobe toegang is toegestaan in Hallo NSG voor subnet van Hallo 'apiase'.   Voor meer informatie over het Hallo uitgaande IP-adres bepalen voor apps die worden uitgevoerd in een App-serviceomgeving Zie Hallo [netwerkarchitectuur] [ NetworkArchitecture] overzichtsartikel.
* **Moet Hallo back-end-API-app toocall zelf?**  Een punt soms onderbelicht en subtiele is Hallo-scenario waarin het back-endtoepassing Hallo toocall zelf moet.  Als een back-end-API-toepassing op een App-serviceomgeving toocall zelf moet, is dit ook behandeld als een aanroep van 'Internet'.  Hiervoor moet de toegang te verlenen vanaf Hallo uitgaande IP-adres van Hallo 'apiase' App Service-omgeving ook uit te voeren in Hallo voorbeeldarchitectuur.

## <a name="setting-up-hello-network-security-group"></a>Hallo Netwerkbeveiligingsgroep instellen
Zodra Hallo ingesteld van uitgaande IP-adressen bekend zijn, de volgende stap Hallo is tooconstruct een netwerkbeveiligingsgroep.  Netwerkbeveiligingsgroepen kunnen worden gemaakt voor beide Resource Manager virtuele netwerken, evenals klassieke virtuele netwerken gebaseerde.  Hallo voorbeelden hieronder ziet u maken en configureren van een NSG op een klassiek virtueel netwerk met behulp van Powershell.

Hallo-omgevingen bevinden zich in Zuid-centraal VS, voor voorbeeldarchitectuur hello, zodat een lege NSG wordt gemaakt in deze regio:

    New-AzureNetworkSecurityGroup -Name "RestrictBackendApi" -Location "South Central US" -Label "Only allow web frontend and loopback traffic"

Eerst een expliciete toestaan regel wordt toegevoegd voor hello Azure management infrastructuur zoals beschreven in artikel Hallo op [binnenkomend verkeer] [ InboundTraffic] voor App Service-omgevingen.

    #Open ports for access by Azure management infrastructure
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW AzureMngmt" -Type Inbound -Priority 100 -Action Allow -SourceAddressPrefix 'INTERNET' -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '454-455' -Protocol TCP

Vervolgens twee regels worden toegevoegd tooallow HTTP en HTTPS-aanroepen vanuit Hallo eerste upstream-App Service-omgeving ('fe1ase').

    #Grant access toorequests from hello first upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe1ase" -Type Inbound -Priority 200 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe1ase" -Type Inbound -Priority 300 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

Spoelen en Herhaal dit voor Hallo tweede en derde upstream-App Service-omgevingen ('fe2ase' en 'fe3ase').

    #Grant access toorequests from hello second upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe2ase" -Type Inbound -Priority 400 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe2ase" -Type Inbound -Priority 500 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

    #Grant access toorequests from hello third upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe3ase" -Type Inbound -Priority 600 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe3ase" -Type Inbound -Priority 700 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

Ten slotte verlenen toegang toohello uitgaande IP-adres van Hallo back-end-API-App Service-omgeving zodat terug naar zichzelf kan worden aangeroepen.

    #Allow apps on hello apiase environment toocall back into itself
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP apiase" -Type Inbound -Priority 800 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS apiase" -Type Inbound -Priority 900 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

Er zijn geen andere netwerkbeveiligingsregels moeten toobe omdat elke NSG bevat een set met standaardregels die inkomende toegang tot Internet Hallo geblokkeerd standaard geconfigureerd.

Hallo volledige lijst met regels in Hallo netwerkbeveiligingsgroep worden hieronder weergegeven.  Houd er rekening mee hoe de laatste regel hello, die is gemarkeerd, blokkeert binnenkomende toegang vanaf alle aanroepfuncties dan degene die expliciet toegang hebben gekregen.

![NSG-configuratie][NSGConfiguration] 

de laatste stap Hallo is tooapply hello NSG toohello subnet met Hallo 'apiase' App Service-omgeving.  

     #Apply hello NSG toohello backend API subnet
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'yourvnetnamehere' -SubnetName 'API-ASE-Subnet'

Met Hallo NSG toegepast toohello subnet zijn alleen hello drie upstream-App Service-omgevingen en Hallo App Service-omgeving met Hallo API-back-end, toegestaan toocall naar Hallo 'apiase'-omgeving.

## <a name="additional-links-and-information"></a>Aanvullende koppelingen en informatie
Alle artikelen en hoe-aan de voor App Service-omgevingen beschikbaar in Hallo zijn [Leesmij-bestand voor Toepassingsserviceomgevingen](../app-service/app-service-app-service-environments-readme.md).

Informatie over [netwerkbeveiligingsgroepen](../virtual-network/virtual-networks-nsg.md). 

Informatie over [uitgaande IP-adressen] [ NetworkArchitecture] en App Service-omgevingen.

[Netwerkpoorten] [ InboundTraffic] die wordt gebruikt door App Service-omgevingen.

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[NetworkArchitecture]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-architecture-overview/
[InboundTraffic]:  https://azure.microsoft.com/en-us/documentation/articles/app-service-app-service-environment-control-inbound-traffic/

<!-- IMAGES -->
[ConceptualArchitecture]: ./media/app-service-app-service-environment-layered-security/ConceptualArchitecture-1.png
[NSGConfiguration]:  ./media/app-service-app-service-environment-layered-security/NSGConfiguration-1.png
