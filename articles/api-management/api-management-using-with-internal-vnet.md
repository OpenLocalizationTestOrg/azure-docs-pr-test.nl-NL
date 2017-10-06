---
title: aaaHow toouse Azure API Management met een intern virtueel netwerk | Microsoft Docs
description: Meer informatie over hoe toosetup en configureren van Azure API Management in intern virtueel netwerk.
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
ms.openlocfilehash: 8d25de14e0c0bebe7ba7b47ca432ea4e45dde312
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-api-management-service-with-internal-virtual-network"></a>Met behulp van Azure API Management-service met een intern virtueel netwerk
Met virtuele netwerken van Azure (vnet's) beheren API Management API's die niet toegankelijk op Hallo Internet. Een aantal VPN-technologieën zijn beschikbaar toomake Hallo verbinding en API Management kan worden geïmplementeerd in twee belangrijke modi binnen Hallo VNET:
* Extern
* interne

## <a name="overview"> </a>Overzicht
Wanneer API Management wordt geïmplementeerd in een modus voor interne virtuele netwerk, zijn alle Hallo service-eindpunten (gateway, developer-portal, publicatieportal, direct beheer en Git) alleen zichtbaar zijn in een virtueel netwerk dat u toegang tot. Geen van de service-eindpunten Hallo zijn geregistreerd op Hallo openbare DNS-Server.

Met API Management in interne modus en kunt u bereiken Hallo volgen scenario 's
* Veilig aanbrengen in uw persoonlijke datacenter toegankelijk door 3e partijen buiten de Site-naar-Site of ExpressRoute-VPN-verbindingen met gehoste API's.
* Hybride cloud-scenario's mogelijk bij het blootstellen van uw cloud-gebaseerde API's en on-premises-API's via een gemeenschappelijke gateway.
* Beheren van uw API's die worden gehost in meerdere geografische locaties met behulp van één Gateway-eindpunt. 

## <a name="enable-vpn"></a>Een API Management in interne virtueel netwerk maken
Hallo API Management-service in het interne virtuele netwerk wordt achter een interne Load Balancer(ILB) gehost. Hallo IP-adres van Hallo ILB is in Hallo [RFC1918](http://www.faqs.org/rfcs/rfc1918.html) bereik.  

### <a name="enable-vnet-connection-using-azure-portal"></a>VNET-verbinding met Azure portal inschakelen
Hallo API Management-service eerst te maken door Hallo stappen te volgen [maken API Management-service][Create API Management service]. Vervolgens set-up API Management toobe binnen een virtueel netwerk is geïmplementeerd.

![Menu voor het instellen van APIM in een intern virtueel netwerk][api-management-using-internal-vnet-menu]

Nadat het Hallo-implementatie is geslaagd, ziet u Hallo interne virtuele IP-adres van uw service op Hallo-dashboard.

![API Management Dashboard met interne VNET geconfigureerd][api-management-internal-vnet-dashboard]

### <a name="enable-vnet-connection-using-powershell-cmdlets"></a>VNET-verbinding met Powershell-cmdlets inschakelen
U kunt ook de VNET-connectiviteit met de PowerShell-cmdlets Hallo inschakelen.

* **Maak een API Management-service binnen een VNET**: Gebruik de cmdlet Hallo [nieuw AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) toocreate een Azure API Management service binnen een VNET en configureer deze toouse Hallo interne VNET type.

* **Implementeren van een bestaande API Management-service binnen een VNET**: Gebruik de cmdlet Hallo [Update AzureRmApiManagementDeployment](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) toomove een bestaande Azure API Management service binnen een virtueel netwerk en configureer deze toouse Interne VNET-type.

## <a name="apim-dns-configuration"></a>DNS-configuratie
Wanneer u API Management in de externe virtuele netwerkmodus gebruikt, wordt door Azure DNS beheerd. Voor interne virtuele netwerk-modus hebt u toomanage uw eigen DNS.

> [!NOTE]
> API Management-service luistert op IP-adressen afkomstig toorequests niet. Reageert alleen toorequests toohello hostnaam geconfigureerd op de service-eindpunten (waaronder gateway, developer-portal, publisher Portal, direct beheer eindpunt en git).

### <a name="access-on-default-host-names"></a>Toegang van standaard hostnamen:
Wanneer u een API Management-service maakt in openbare Azure-cloud, met bijvoorbeeld de naam 'contoso', zijn hello volgende service-eindpunten standaard geconfigureerd.

>   Gateway / Proxy - contoso.azure api.net

> Publicatieportal en -Portal voor ontwikkelaars - contoso.portal.azure api.net

> Direct beheer Endpoint - contoso.management.azure api.net

>   GIT - contoso.scm.azure api.net

tooaccess deze API Management-service-eindpunten, u kunt een virtuele Machine maken in een subnet verbonden toohello virtuele netwerk waarin API Management wordt geïmplementeerd. Ervan uitgaande dat Hallo interne virtuele IP-adres voor uw service 10.0.0.5 is, kunt u doen Hallo bestandstoewijzing hosts (% SystemDrive%\drivers\etc\hosts) als volgt:

> 10.0.0.5 contoso.azure-api.net

> 10.0.0.5 contoso.portal.azure-api.net

> 10.0.0.5 contoso.management.azure-api.net

> 10.0.0.5 contoso.scm.azure-api.net

U kunt vervolgens alle Hallo service-eindpunten openen vanaf Hallo virtuele Machine die u hebt gemaakt. Als u een aangepaste DNS-server in een virtueel netwerk gebruikt, u kunt ook een DNS-records maken en toegang tot deze eindpunten vanaf elke locatie in het virtuele netwerk. 

### <a name="access-on-custom-domain-names"></a>Toegang van aangepaste domeinnamen:
Als u niet tooaccess Hallo API Management-service met Hallo standaard hostnamen wilt, kunt u aangepaste domeinnamen voor alle uw service-eindpunten zoals hieronder instellen

![Instellen van het aangepaste domein voor API Management][api-management-custom-domain-name]

Vervolgens kunt u A-records in uw DNS-Server tooaccess deze eindpunten die alleen toegankelijk vanuit uw virtuele netwerk zijn.

## <a name="related-content"></a>Verwante inhoud
* [Configuratie van algemene netwerkproblemen tijdens het instellen van APIM in VNET][Common Network Configuration Issues]
* [Virtueel netwerk Veelgestelde vragen](../virtual-network/virtual-networks-faq.md)
* [Maken van A-record in DNS](https://msdn.microsoft.com/en-us/library/bb727018.aspx)

[api-management-using-internal-vnet-menu]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-menu.png
[api-management-internal-vnet-dashboard]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-dashboard.png
[api-management-custom-domain-name]: ./media/api-management-using-with-internal-vnet/api-management-custom-domain-name.png

[Create API Management service]: api-management-get-started.md#create-service-instance
[Common Network Configuration Issues]: api-management-using-with-vnet.md#network-configuration-issues
