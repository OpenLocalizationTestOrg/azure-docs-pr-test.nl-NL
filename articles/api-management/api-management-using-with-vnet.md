---
title: aaaHow toouse Azure API Management met virtuele netwerken
description: Meer informatie over hoe toosetup verbinding tooa virtueel netwerk in Azure API Management en toegang tot web-services via het.
services: api-management
documentationcenter: 
author: antonba
manager: erikre
editor: 
ms.assetid: 64b58f7b-ca22-47dc-89c0-f6bb0af27a48
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 426b3974e4fed7daffdb0c3f02381edbc326dc28
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-api-management-with-virtual-networks"></a>Hoe toouse Azure API Management met virtuele netwerken
Virtuele netwerken van Azure (vnet's) kunt u een van uw Azure-resources in een internet-routeable netwerk dat u beheert de toegang tot tooplace. Deze netwerken kunnen vervolgens worden verbonden tooyour on-premises netwerken met behulp van verschillende VPN-technologieën. meer informatie over Azure Virtual Networks met Hallo informatie hier beginnen toolearn: [Azure Virtual Network-overzicht](../virtual-network/virtual-networks-overview.md).

Azure API Management kunnen worden geïmplementeerd in Hallo virtuele netwerk (VNET), zodat deze toegang heeft tot back-end-services binnen Hallo-netwerk. Hallo developer-portal en API-gateway, geconfigureerde toobe toegankelijk is vanaf Internet Hallo of alleen binnen het virtuele netwerk Hallo kan zijn.

> [!NOTE]
> Azure API Management biedt ondersteuning voor classic en Azure Resource Manager-vnet's.
>
>

## <a name="enable-vpn"></a>Inschakelen VNET-verbinding
> [!NOTE]
> VNET-connectiviteit is beschikbaar in Hallo **Premium** en **Developer** lagen. tooswitch tussen lagen hello, opent u uw API Management-service in hello Azure-portal en open vervolgens Hallo **schaal en prijzen** tabblad. Onder Hallo **prijscategorie** sectie, selecteer de laag Premium of ontwikkelaar Hallo en klik op opslaan.
>

tooenable VNET-connectiviteit, open uw API Management-service in hello Azure-portal en Hallo **virtueel netwerk** pagina.

![Virtueel netwerk menu van API Management][api-management-using-vnet-menu]

Hallo gewenste toegangstype selecteren:

* **Externe**: Hallo API Management-gateway en developer portal toegankelijk zijn vanaf Hallo openbare internet via een externe load balancer. Hallo-gateway toegang tot bronnen in het virtuele netwerk Hallo.

![Openbare peering][api-management-vnet-public]

* **Interne**: Hallo API Management-gateway en developer-portal zijn alleen toegankelijk vanuit Hallo virtueel netwerk via een interne load balancer. Hallo-gateway toegang tot bronnen in het virtuele netwerk Hallo.

![Persoonlijke peering][api-management-vnet-private]

U ziet nu een lijst met alle regio's waar uw API Management-service is ingericht. Selecteer een VNET en een subnet voor elke regio. Hallo-lijst is gevuld met zowel klassieke als Resource Manager virtuele netwerken die beschikbaar zijn in uw Azure-abonnementen die zijn ingesteld in Hallo regio die u configureert.

> [!NOTE]
> **Service-eindpunt** in Hallo hierboven diagram bevat Gateway of Proxy, Publicatieportal, Developer-Portal, GIT en Hallo Direct eindpunt.
> **Eindpunt** in Hallo bovenstaande diagram wordt gehost op Hallo serviceconfiguratie toomanage via Azure portal en Powershell Hallo-eindpunt.
> Ook, houd er rekening mee dat, hoewel Hallo diagram ziet u IP-adressen voor de verschillende API Management-service-eindpunten **alleen** reageert op de geconfigureerde hostnamen.

> [!IMPORTANT]
> Bij het implementeren van een Azure API Management-exemplaar tooa Resource Manager VNET moet Hallo-service een toegewezen subnet dat geen andere resources, met uitzondering van exemplaren van Azure API Management bevat. Als wordt geprobeerd toodeploy mislukt een Azure API Management-exemplaar tooa Resource Manager VNET subnet met andere resources, het Hallo-implementatie.
>
>

![Selecteer VPN][api-management-setup-vpn-select]

Klik op **opslaan** Hallo boven aan het welkomstscherm.

> [!NOTE]
> Hallo VIP-adres van het exemplaar van API Management Hallo wordt gewijzigd wanneer VNET is ingeschakeld of uitgeschakeld.  
> Hallo VIP-adres, wijzigt u ook wanneer API Management wordt verplaatst van **externe** te**intern** of omgekeerd
>


> [!IMPORTANT]
> Als u API Management uit een VNET verwijderen of Hallo een die machine is geïmplementeerd in wijzigt, vergrendeld Hallo eerder gebruikte VNET kan blijven voor too4 uur. Tijdens deze periode wordt het niet mogelijk toodelete hello VNET of een nieuwe resource tooit implementeren.

## <a name="enable-vnet-powershell"></a>Inschakelen VNET-verbinding met PowerShell-cmdlets
U kunt ook de VNET-connectiviteit met de PowerShell-cmdlets Hallo inschakelen

* **Maak een API Management-service binnen een VNET**: Gebruik de cmdlet Hallo [nieuw AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) toocreate binnen een VNET een Azure API Management-service.

* **Implementeren van een bestaande API Management-service binnen een VNET**: Gebruik de cmdlet Hallo [Update AzureRmApiManagementDeployment](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) toomove een bestaande Azure API Management-service in een virtueel netwerk.

## <a name="connect-vnet"></a>Tooa webservice die wordt gehost binnen een virtueel netwerk verbinding maken
Nadat uw API Management-service verbonden toohello VNET is, gaat toegang tot services in het back-end niet anders zijn dan de toegang tot openbare services zijn. Typ in het Hallo lokale IP-adres of Hallo van hostnaam (als een DNS-server is geconfigureerd voor Hallo VNET) van uw web-service in Hallo **webservice-URL** veld bij het maken van een nieuwe API of een bestaande bewerkt.

![API via VPN-netwerk toevoegen][api-management-setup-vpn-add-api]

## <a name="network-configuration-issues"></a>Algemene configuratie netwerkproblemen
Hier volgt een lijst met veelvoorkomende configuratiefouten die optreden kunnen tijdens het implementeren van API Management-service in een virtueel netwerk.

* **Aangepaste DNS-server setup**: Hallo API Management-service is afhankelijk van verschillende Azure-services. Wanneer u API Management wordt gehost in een VNET met een aangepaste DNS-server, moet deze tooresolve Hallo hostnamen van deze Azure-services. Volg [dit](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) hulp bij het aangepaste DNS-instellingen. Zie Hallo poorten in de volgende tabel en andere netwerkvereisten ter referentie.

> [!IMPORTANT]
> Het verdient aanbeveling dat, als u van een aangepaste DNS-server (s) voor Hallo VNET gebruikmaakt, u dat instellen **voordat** een API Management-service implementeren in de App. Anders u nodig hebt te bijwerken Hallo API Management-service telkens wanneer u Hallo DNS-Servers (s wijzigt) door het uitvoeren van Hallo [netwerkbewerking configuratie toepassen](https://docs.microsoft.com/en-us/rest/api/apimanagement/apimanagementservice#ApiManagementService_ApplyNetworkConfigurationUpdates)

* **Vereiste poorten voor API Management**: binnenkomend en uitgaand verkeer naar Hallo Subnet waarin API Management wordt geïmplementeerd, kan worden beheerd met behulp van [Netwerkbeveiligingsgroep][Network Security Group]. Als een van deze poorten niet beschikbaar zijn, wordt API Management werkt mogelijk niet correct en kan ontoegankelijk worden. Met een of meer van deze poorten geblokkeerd is een andere veelvoorkomende onjuiste configuratie probleem wanneer u API Management met een VNET.

Wanneer een exemplaar van API Management-service wordt gehost in een VNET, worden Hallo-poorten in de volgende tabel hello gebruikt.

| Bron / bestemming poort(en) | Richting | Protocol-transport | Doel | Bron / doel | Toegangstype |
| --- | --- | --- | --- | --- | --- |
| * / 80, 443 |Inkomend |TCP |Client communicatie tooAPI Management |INTERNET / VIRTUAL_NETWORK |Extern |
| * / 3443 |Inkomend |TCP |Eindpunt voor Azure-portal en Powershell |INTERNET / VIRTUAL_NETWORK |Externe & interne |
| * / 80, 443 |Uitgaand |TCP |Afhankelijkheid van Azure Storage en Azure Servicebus |VIRTUAL_NETWORK / INTERNET |Externe & interne |
| * / 1433 |Uitgaand |TCP |Afhankelijkheid van Azure SQL |VIRTUAL_NETWORK / INTERNET |Externe & interne |
| * / 11000 - 11999 |Uitgaand |TCP |Afhankelijkheid van V12 Azure SQL |VIRTUAL_NETWORK / INTERNET |Externe & interne |
| * / 14000 - 14999 |Uitgaand |TCP |Afhankelijkheid van V12 Azure SQL |VIRTUAL_NETWORK / INTERNET |Externe & interne |
| * / 5671 |Uitgaand |AMQP |Afhankelijkheid van logboek tooEvent Hub beleid en bewakingsagent |VIRTUAL_NETWORK / INTERNET |Externe & interne |
| 6381 - 6383 / 6381 - 6383 |Binnenkomend en uitgaand |UDP |Afhankelijkheid van Redis-Cache |VIRTUAL_NETWORK / VIRTUAL_NETWORK |Externe & interne |-
| * / 445 |Uitgaand |TCP |Afhankelijkheid van Azure-bestandsshare voor GIT |VIRTUAL_NETWORK / INTERNET |Externe & interne |
| * / * | Inkomend |TCP |Azure-infrastructuur Load Balancer | AZURE_LOAD_BALANCER / VIRTUAL_NETWORK |Externe & interne |

* **SSL-functionaliteit**: tooenable keten gebouw en validatie Hallo API Management-service moet uitgaande network connectivity tooocsp.msocsp.com, mscrl.microsoft.com en crl.microsoft.com SSL-certificaat. Deze afhankelijkheid is niet vereist, als een certificaat dat u uploadt tooAPI Management Hallo volledige keten toohello CA hoofdmap bevatten.

* **DNS-toegang**: uitgaand verkeer op poort 53 is vereist voor communicatie met de DNS-servers. Als u een aangepaste DNS-server bestaat op Hallo van andere einde van een VPN-gateway, Hallo DNS-server moet bereikbaar zijn vanaf Hallo subnet die als host fungeert voor API Management.

* **Metrische gegevens en statuscontrole**: uitgaande netwerk connectiviteit tooAzure controle-eindpunten die onder de volgende domeinen Hallo oplossen: global.metrics.nsatc.net, shoebox2.metrics.nsatc.net, prod3.metrics.nsatc.net.

* **Express Route-instelling**: een algemene configuratie van de klant toodefine hun eigen standaardroute (0.0.0.0/0), waardoor uitgaande Internet verkeer tooinstead stroom lokaal is. Dit netwerkverkeer altijd verbinding met Azure API Management wordt verbroken omdat er Hallo uitgaand verkeer wordt geblokkeerd on-premises of NAT'd tooan onherkenbare set adressen die niet langer met verschillende Azure-eindpunten werken. Hallo-oplossing is de gebruiker gedefinieerde routes toodefine er (of meer) ([udr's][UDRs]) op Hallo subnet met hello Azure API Management. Een UDR definieert subnet-specifieke routes die in plaats van de standaardroute Hallo gehonoreerd.
  Indien mogelijk, wordt aangeraden toouse Hallo volgende configuratie:
 * Hallo ExpressRoute configuratie kondigt 0.0.0.0/0 en standaard force alle uitgaande verkeer lokale tunnels.
 * Hallo UDR toegepast toohello subnet met hello Azure API Management definieert 0.0.0.0/0 met een volgend hoptype van Internet.
 Hallo is gecombineerde effect van deze stappen dat Hallo subnetniveau UDR voorrang hebben op Hallo ExpressRoute geforceerde tunneling, zodat uitgaande toegang tot Internet vanaf hello Azure API Management.

>[!WARNING]  
>Azure API Management wordt niet ondersteund met ExpressRoute-configuraties die **onjuist cross-adverteert routes van Hallo pad toohello persoonlijke peering pad voor openbare peering**. ExpressRoute-configuraties waarvoor openbare peering is geconfigureerd, ontvangen route-advertisements van Microsoft voor een groot aantal Microsoft Azure-IP-adresbereiken. Als deze adresbereiken onjuist cross aangekondigd op Hallo-pad voor persoonlijke peering, is Hallo eindresultaat dat alle uitgaande pakketten van subnet hello Azure API Management exemplaar van de klant ten onrechte force via een tunnel tooa on-premises netwerk infrastructuur. Deze stroom van het netwerk verbreekt Azure API Management. Hallo oplossing toothis probleem is toostop cross-adverteert routes van Hallo pad toohello persoonlijke peering pad voor openbare peering.


## <a name="troubleshooting"></a>Probleemoplossing
Bij het doorvoeren van wijzigingen tooyour netwerk te verwijzen[NetworkStatus API](https://docs.microsoft.com/en-us/rest/api/apimanagement/networkstatus), toovalidate als Hallo API Management-service niet verloren gegaan toegang tooany Hallo kritieke bronnen die dit is afhankelijk van. de verbindingsstatus Hallo moet worden bijgewerkt om de 15 minuten.

## <a name="limitations"></a>Beperkingen
* Een subnet met exemplaren van API Management kan geen andere Azure-brontypen bevatten.
* Hallo-subnet en Hallo API Management-service moet zijn in Hallo hetzelfde abonnement.
* Een subnet met exemplaren van API Management kan niet worden verplaatst tussen abonnementen.
* Wanneer u een intern virtueel netwerk alleen een interne IP-adres beschikbaar is via Hallo bereik vermeld in de [RFC 1918](https://tools.ietf.org/html/rfc1918), een openbare IP-adres kan niet worden opgegeven.
* Voor meerdere landen/regio API Management-implementaties zijn met interne virtuele netwerken die zijn geconfigureerd, gebruikers verantwoordelijk voor het beheren van hun eigen taakverdeling als eigenaar van Hallo DNS.


## <a name="related-content"></a>Verwante inhoud
* [Verbinding maken met een virtueel netwerk toobackend met behulp van VPN-Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md#s2smulti)
* [Verbinding maken met een virtueel netwerk vanuit verschillende implementatiemodellen](../vpn-gateway/vpn-gateway-connect-different-deployment-models-powershell.md)
* [Hoe toouse Hallo API Inspector tootrace aanroept in Azure API Management](api-management-howto-api-inspector.md)

[api-management-using-vnet-menu]: ./media/api-management-using-with-vnet/api-management-menu-vnet.png
[api-management-setup-vpn-select]: ./media/api-management-using-with-vnet/api-management-using-vnet-type.png
[api-management-setup-vpn-select]: ./media/api-management-using-with-vnet/api-management-using-vnet-select.png
[api-management-setup-vpn-add-api]: ./media/api-management-using-with-vnet/api-management-using-vnet-add-api.png
[api-management-vnet-private]: ./media/api-management-using-with-vnet/api-management-vnet-private.png
[api-management-vnet-public]: ./media/api-management-using-with-vnet/api-management-vnet-public.png

[Enable VPN connections]: #enable-vpn
[Connect tooa web service behind VPN]: #connect-vpn
[Related content]: #related-content

[UDRs]: ../virtual-network/virtual-networks-udr-overview.md
[Network Security Group]: ../virtual-network/virtual-networks-nsg.md
