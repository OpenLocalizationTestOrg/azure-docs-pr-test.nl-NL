---
title: Het gebruik van Azure API Management met intern virtueel netwerk | Microsoft Docs
description: Informatie over het installeren en configureren van Azure API Management in een intern virtueel netwerk.
services: api-management
documentationcenter: 
author: solankisamir
manager: kjoshi
editor: 
ms.assetid: dac28ccf-2550-45a5-89cf-192d87369bc3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 55248387c7e78d05c1cf1afd615b7b921e9669d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-api-management-service-with-internal-virtual-network"></a>Met behulp van Azure API Management-service met een intern virtueel netwerk
Met virtuele netwerken van Azure (vnet's) beheren API Management API's die niet toegankelijk op het Internet. Een aantal VPN-technologieën zijn beschikbaar voor het maken van de verbinding en API Management kan worden geïmplementeerd in twee belangrijke modi binnen het VNET:
* Extern
* interne

## <a name="overview"> </a>Overzicht
Wanneer API Management wordt geïmplementeerd in een modus voor interne virtuele netwerk, alle de service-eindpunten (gateway, developer-portal, publicatieportal, direct beheer en Git) zijn alleen zichtbaar binnen een virtueel netwerk dat u beheert de toegang tot. Geen van de service-eindpunten zijn geregistreerd op de openbare DNS-Server.

Met behulp van API Management in de interne modus, kunt u de volgende scenario's bereiken
* Veilig aanbrengen in uw persoonlijke datacenter toegankelijk door 3e partijen buiten de Site-naar-Site of ExpressRoute-VPN-verbindingen met gehoste API's.
* Hybride cloud-scenario's mogelijk bij het blootstellen van uw cloud-gebaseerde API's en on-premises-API's via een gemeenschappelijke gateway.
* Beheren van uw API's die worden gehost in meerdere geografische locaties met behulp van één Gateway-eindpunt. 

## <a name="enable-vpn"></a>Een API Management in interne virtueel netwerk maken
De API Management-service in het interne virtuele netwerk wordt achter een interne Load Balancer(ILB) gehost. Het IP-adres van de ILB is in de [RFC1918](http://www.faqs.org/rfcs/rfc1918.html) bereik.  

### <a name="enable-vnet-connection-using-azure-portal"></a>VNET-verbinding met Azure portal inschakelen
De API Management-service eerst te maken door de stappen te volgen [maken API Management-service][Create API Management service]. Vervolgens set-up API Management binnen een virtueel netwerk worden geïmplementeerd.

![Menu voor het instellen van APIM in een intern virtueel netwerk][api-management-using-internal-vnet-menu]

Nadat de implementatie is geslaagd, ziet u de interne virtuele IP-adres van uw service op het dashboard.

![API Management Dashboard met interne VNET geconfigureerd][api-management-internal-vnet-dashboard]

### <a name="enable-vnet-connection-using-powershell-cmdlets"></a>VNET-verbinding met Powershell-cmdlets inschakelen
U kunt ook inschakelen met behulp van de PowerShell-cmdlets voor VNET-connectiviteit.

* **Maak een API Management-service binnen een VNET**: Gebruik de cmdlet [nieuw AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) een Azure API Management-service binnen een VNET maken en configureren voor het gebruik van het type interne VNET.

* **Implementeren van een bestaande API Management-service binnen een VNET**: Gebruik de cmdlet [Update AzureRmApiManagementDeployment](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) verplaatsen van een bestaande Azure API Management-service binnen een virtueel netwerk en configureren voor gebruik Interne VNET-type.

## <a name="apim-dns-configuration"></a>DNS-configuratie
Wanneer u API Management in de externe virtuele netwerkmodus gebruikt, wordt door Azure DNS beheerd. U hebt voor het beheren van uw eigen DNS voor de interne virtuele netwerk-modus.

> [!NOTE]
> API Management-service luistert niet op aanvragen die afkomstig zijn van IP-adressen. Alleen reageert op aanvragen voor de hostnaam geconfigureerd op de service-eindpunten (waaronder gateway, developer-portal, publisher Portal, direct beheer eindpunt en git).

### <a name="access-on-default-host-names"></a>Toegang van standaard hostnamen:
Wanneer u een API Management-service maakt in openbare Azure-cloud, met bijvoorbeeld de naam 'contoso', worden de volgende service-eindpunten standaard geconfigureerd.

>   Gateway / Proxy - contoso.azure api.net

> Publicatieportal en -Portal voor ontwikkelaars - contoso.portal.azure api.net

> Direct beheer Endpoint - contoso.management.azure api.net

>   GIT - contoso.scm.azure api.net

Voor toegang tot deze API Management-service-eindpunten, kunt u een virtuele Machine in een subnet is verbonden met het virtuele netwerk waarin API Management wordt geïmplementeerd. Ervan uitgaande dat de interne virtuele IP-adres voor uw service 10.0.0.5 is, kunt u de hosts doen bestand toewijzing (% SystemDrive%\drivers\etc\hosts) als volgt:

> 10.0.0.5 contoso.azure-api.net

> 10.0.0.5 contoso.portal.azure-api.net

> 10.0.0.5 contoso.management.azure-api.net

> 10.0.0.5 contoso.scm.azure-api.net

U kunt vervolgens toegang tot alle service-eindpunten van de virtuele Machine die u hebt gemaakt. Als u een aangepaste DNS-server in een virtueel netwerk gebruikt, u kunt ook een DNS-records maken en toegang tot deze eindpunten vanaf elke locatie in het virtuele netwerk. 

### <a name="access-on-custom-domain-names"></a>Toegang van aangepaste domeinnamen:
Als u toegang tot de API Management-service met de standaard hostnamen niet wilt, kunt u aangepaste domeinnamen voor alle uw service-eindpunten zoals hieronder instellen

![Instellen van het aangepaste domein voor API Management][api-management-custom-domain-name]

Vervolgens kunt u A-records maken in uw DNS-Server voor toegang tot deze eindpunten die alleen toegankelijk vanuit uw virtuele netwerk zijn.

## <a name="related-content"></a>Verwante inhoud
* [Configuratie van algemene netwerkproblemen tijdens het instellen van APIM in VNET][Common Network Configuration Issues]
* [Virtueel netwerk Veelgestelde vragen](../virtual-network/virtual-networks-faq.md)
* [Maken van A-record in DNS](https://msdn.microsoft.com/en-us/library/bb727018.aspx)

[api-management-using-internal-vnet-menu]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-menu.png
[api-management-internal-vnet-dashboard]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-dashboard.png
[api-management-custom-domain-name]: ./media/api-management-using-with-internal-vnet/api-management-custom-domain-name.png

[Create API Management service]: api-management-get-started.md#create-service-instance
[Common Network Configuration Issues]: api-management-using-with-vnet.md#network-configuration-issues
