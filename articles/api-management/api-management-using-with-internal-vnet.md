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
# <a name="using-azure-api-management-service-with-internal-virtual-network"></a><span data-ttu-id="a2384-103">Met behulp van Azure API Management-service met een intern virtueel netwerk</span><span class="sxs-lookup"><span data-stu-id="a2384-103">Using Azure API Management service with Internal Virtual Network</span></span>
<span data-ttu-id="a2384-104">Met virtuele netwerken van Azure (vnet's) beheren API Management API's die niet toegankelijk op Hallo Internet.</span><span class="sxs-lookup"><span data-stu-id="a2384-104">With Azure Virtual Networks (VNETs), API Management can manage APIs not accessible on hello Internet.</span></span> <span data-ttu-id="a2384-105">Een aantal VPN-technologieën zijn beschikbaar toomake Hallo verbinding en API Management kan worden geïmplementeerd in twee belangrijke modi binnen Hallo VNET:</span><span class="sxs-lookup"><span data-stu-id="a2384-105">A number of VPN technologies are available toomake hello connection and API Management can be deployed in two main modes inside hello VNET:</span></span>
* <span data-ttu-id="a2384-106">Extern</span><span class="sxs-lookup"><span data-stu-id="a2384-106">External</span></span>
* <span data-ttu-id="a2384-107">interne</span><span class="sxs-lookup"><span data-stu-id="a2384-107">Internal</span></span>

## <span data-ttu-id="a2384-108"><a name="overview"> </a>Overzicht</span><span class="sxs-lookup"><span data-stu-id="a2384-108"><a name="overview"> </a>Overview</span></span>
<span data-ttu-id="a2384-109">Wanneer API Management wordt geïmplementeerd in een modus voor interne virtuele netwerk, zijn alle Hallo service-eindpunten (gateway, developer-portal, publicatieportal, direct beheer en Git) alleen zichtbaar zijn in een virtueel netwerk dat u toegang tot.</span><span class="sxs-lookup"><span data-stu-id="a2384-109">When API Management is deployed in an Internal Virtual network mode, all hello service endpoints (gateway, developer portal, publisher portal, direct management and Git) are only visible inside a Virtual network that you control access to.</span></span> <span data-ttu-id="a2384-110">Geen van de service-eindpunten Hallo zijn geregistreerd op Hallo openbare DNS-Server.</span><span class="sxs-lookup"><span data-stu-id="a2384-110">None of hello service endpoints are registered on hello Public DNS Server.</span></span>

<span data-ttu-id="a2384-111">Met API Management in interne modus en kunt u bereiken Hallo volgen scenario 's</span><span class="sxs-lookup"><span data-stu-id="a2384-111">Using API Management in Internal mode, you can achieve hello following scenarios</span></span>
* <span data-ttu-id="a2384-112">Veilig aanbrengen in uw persoonlijke datacenter toegankelijk door 3e partijen buiten de Site-naar-Site of ExpressRoute-VPN-verbindingen met gehoste API's.</span><span class="sxs-lookup"><span data-stu-id="a2384-112">Securely make APIs hosted in your private datacenter accessible by 3rd parties outside of it using Site-to-Site or ExpressRoute VPN connections.</span></span>
* <span data-ttu-id="a2384-113">Hybride cloud-scenario's mogelijk bij het blootstellen van uw cloud-gebaseerde API's en on-premises-API's via een gemeenschappelijke gateway.</span><span class="sxs-lookup"><span data-stu-id="a2384-113">Enable hybrid cloud scenarios by exposing your cloud-based APIs and on-prem APIs through a common gateway.</span></span>
* <span data-ttu-id="a2384-114">Beheren van uw API's die worden gehost in meerdere geografische locaties met behulp van één Gateway-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="a2384-114">Manage your APIs hosted in multiple geographic locations using a single Gateway endpoint.</span></span> 

## <span data-ttu-id="a2384-115"><a name="enable-vpn"></a>Een API Management in interne virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="a2384-115"><a name="enable-vpn"> </a>Creating an API Management in Internal Virtual network</span></span>
<span data-ttu-id="a2384-116">Hallo API Management-service in het interne virtuele netwerk wordt achter een interne Load Balancer(ILB) gehost.</span><span class="sxs-lookup"><span data-stu-id="a2384-116">hello API Management service in Internal Virtual network is hosted behind an Internal Load Balancer(ILB).</span></span> <span data-ttu-id="a2384-117">Hallo IP-adres van Hallo ILB is in Hallo [RFC1918](http://www.faqs.org/rfcs/rfc1918.html) bereik.</span><span class="sxs-lookup"><span data-stu-id="a2384-117">hello IP Address of hello ILB is in hello [RFC1918](http://www.faqs.org/rfcs/rfc1918.html) range.</span></span>  

### <a name="enable-vnet-connection-using-azure-portal"></a><span data-ttu-id="a2384-118">VNET-verbinding met Azure portal inschakelen</span><span class="sxs-lookup"><span data-stu-id="a2384-118">Enable VNET connection using Azure portal</span></span>
<span data-ttu-id="a2384-119">Hallo API Management-service eerst te maken door Hallo stappen te volgen [maken API Management-service][Create API Management service].</span><span class="sxs-lookup"><span data-stu-id="a2384-119">First create hello API Management service by following hello steps [Create API Management service][Create API Management service].</span></span> <span data-ttu-id="a2384-120">Vervolgens set-up API Management toobe binnen een virtueel netwerk is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="a2384-120">Then set-up API Management toobe deployed inside a Virtual network.</span></span>

![Menu voor het instellen van APIM in een intern virtueel netwerk][api-management-using-internal-vnet-menu]

<span data-ttu-id="a2384-122">Nadat het Hallo-implementatie is geslaagd, ziet u Hallo interne virtuele IP-adres van uw service op Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="a2384-122">After hello deployment succeeds, you should see hello Internal Virtual IP Address of your service on hello dashboard.</span></span>

![API Management Dashboard met interne VNET geconfigureerd][api-management-internal-vnet-dashboard]

### <a name="enable-vnet-connection-using-powershell-cmdlets"></a><span data-ttu-id="a2384-124">VNET-verbinding met Powershell-cmdlets inschakelen</span><span class="sxs-lookup"><span data-stu-id="a2384-124">Enable VNET connection using Powershell cmdlets</span></span>
<span data-ttu-id="a2384-125">U kunt ook de VNET-connectiviteit met de PowerShell-cmdlets Hallo inschakelen.</span><span class="sxs-lookup"><span data-stu-id="a2384-125">You can also enable VNET connectivity using hello PowerShell cmdlets.</span></span>

* <span data-ttu-id="a2384-126">**Maak een API Management-service binnen een VNET**: Gebruik de cmdlet Hallo [nieuw AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) toocreate een Azure API Management service binnen een VNET en configureer deze toouse Hallo interne VNET type.</span><span class="sxs-lookup"><span data-stu-id="a2384-126">**Create an API Management service inside a VNET**: Use hello cmdlet [New-AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) toocreate an Azure API Management service inside a VNET and configure it toouse hello Internal VNET type.</span></span>

* <span data-ttu-id="a2384-127">**Implementeren van een bestaande API Management-service binnen een VNET**: Gebruik de cmdlet Hallo [Update AzureRmApiManagementDeployment](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) toomove een bestaande Azure API Management service binnen een virtueel netwerk en configureer deze toouse Interne VNET-type.</span><span class="sxs-lookup"><span data-stu-id="a2384-127">**Deploy an existing API Management service inside a VNET**: Use hello cmdlet [Update-AzureRmApiManagementDeployment](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) toomove an existing Azure API Management service inside a Virtual network and configure it toouse Internal VNET type.</span></span>

## <span data-ttu-id="a2384-128"><a name="apim-dns-configuration"></a>DNS-configuratie</span><span class="sxs-lookup"><span data-stu-id="a2384-128"><a name="apim-dns-configuration"></a>DNS configuration</span></span>
<span data-ttu-id="a2384-129">Wanneer u API Management in de externe virtuele netwerkmodus gebruikt, wordt door Azure DNS beheerd.</span><span class="sxs-lookup"><span data-stu-id="a2384-129">When using API Management in External Virtual network mode, DNS is managed by Azure.</span></span> <span data-ttu-id="a2384-130">Voor interne virtuele netwerk-modus hebt u toomanage uw eigen DNS.</span><span class="sxs-lookup"><span data-stu-id="a2384-130">For Internal Virtual network mode, you have toomanage your own DNS.</span></span>

> [!NOTE]
> <span data-ttu-id="a2384-131">API Management-service luistert op IP-adressen afkomstig toorequests niet.</span><span class="sxs-lookup"><span data-stu-id="a2384-131">API Management service does not listen toorequests coming on IP addresses.</span></span> <span data-ttu-id="a2384-132">Reageert alleen toorequests toohello hostnaam geconfigureerd op de service-eindpunten (waaronder gateway, developer-portal, publisher Portal, direct beheer eindpunt en git).</span><span class="sxs-lookup"><span data-stu-id="a2384-132">It only responds toorequests toohello Hostname configured on its service endpoints (which includes gateway, developer portal, publisher Portal, direct management endpoint, and git).</span></span>

### <a name="access-on-default-host-names"></a><span data-ttu-id="a2384-133">Toegang van standaard hostnamen:</span><span class="sxs-lookup"><span data-stu-id="a2384-133">Access on default host names:</span></span>
<span data-ttu-id="a2384-134">Wanneer u een API Management-service maakt in openbare Azure-cloud, met bijvoorbeeld de naam 'contoso', zijn hello volgende service-eindpunten standaard geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="a2384-134">When you create an API Management service in public Azure cloud, named "contoso" for example, hello following service endpoints are configured by default.</span></span>

>   <span data-ttu-id="a2384-135">Gateway / Proxy - contoso.azure api.net</span><span class="sxs-lookup"><span data-stu-id="a2384-135">Gateway / Proxy - contoso.azure-api.net</span></span>

> <span data-ttu-id="a2384-136">Publicatieportal en -Portal voor ontwikkelaars - contoso.portal.azure api.net</span><span class="sxs-lookup"><span data-stu-id="a2384-136">Publisher Portal and Developer Portal - contoso.portal.azure-api.net</span></span>

> <span data-ttu-id="a2384-137">Direct beheer Endpoint - contoso.management.azure api.net</span><span class="sxs-lookup"><span data-stu-id="a2384-137">Direct Management Endpoint - contoso.management.azure-api.net</span></span>

>   <span data-ttu-id="a2384-138">GIT - contoso.scm.azure api.net</span><span class="sxs-lookup"><span data-stu-id="a2384-138">GIT - contoso.scm.azure-api.net</span></span>

<span data-ttu-id="a2384-139">tooaccess deze API Management-service-eindpunten, u kunt een virtuele Machine maken in een subnet verbonden toohello virtuele netwerk waarin API Management wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="a2384-139">tooaccess these API Management service endpoints, you can create a Virtual Machine in a subnet connected toohello Virtual network in which API Management is deployed.</span></span> <span data-ttu-id="a2384-140">Ervan uitgaande dat Hallo interne virtuele IP-adres voor uw service 10.0.0.5 is, kunt u doen Hallo bestandstoewijzing hosts (% SystemDrive%\drivers\etc\hosts) als volgt:</span><span class="sxs-lookup"><span data-stu-id="a2384-140">Assuming hello Internal Virtual IP Address for your service is 10.0.0.5, you can do hello hosts file mapping (%SystemDrive%\drivers\etc\hosts) as follows:</span></span>

> <span data-ttu-id="a2384-141">10.0.0.5 contoso.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="a2384-141">10.0.0.5    contoso.azure-api.net</span></span>

> <span data-ttu-id="a2384-142">10.0.0.5 contoso.portal.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="a2384-142">10.0.0.5    contoso.portal.azure-api.net</span></span>

> <span data-ttu-id="a2384-143">10.0.0.5 contoso.management.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="a2384-143">10.0.0.5    contoso.management.azure-api.net</span></span>

> <span data-ttu-id="a2384-144">10.0.0.5 contoso.scm.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="a2384-144">10.0.0.5    contoso.scm.azure-api.net</span></span>

<span data-ttu-id="a2384-145">U kunt vervolgens alle Hallo service-eindpunten openen vanaf Hallo virtuele Machine die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a2384-145">You can then access all hello service endpoints from hello Virtual Machine you created.</span></span> <span data-ttu-id="a2384-146">Als u een aangepaste DNS-server in een virtueel netwerk gebruikt, u kunt ook een DNS-records maken en toegang tot deze eindpunten vanaf elke locatie in het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="a2384-146">If using a Custom DNS server in a Virtual network, you can also create A DNS records and access these endpoints from anywhere in your Virtual network.</span></span> 

### <a name="access-on-custom-domain-names"></a><span data-ttu-id="a2384-147">Toegang van aangepaste domeinnamen:</span><span class="sxs-lookup"><span data-stu-id="a2384-147">Access on custom domain names:</span></span>
<span data-ttu-id="a2384-148">Als u niet tooaccess Hallo API Management-service met Hallo standaard hostnamen wilt, kunt u aangepaste domeinnamen voor alle uw service-eindpunten zoals hieronder instellen</span><span class="sxs-lookup"><span data-stu-id="a2384-148">If you don’t want tooaccess hello API Management service with hello default host names, you can setup custom domain names for all your service endpoints like below</span></span>

![Instellen van het aangepaste domein voor API Management][api-management-custom-domain-name]

<span data-ttu-id="a2384-150">Vervolgens kunt u A-records in uw DNS-Server tooaccess deze eindpunten die alleen toegankelijk vanuit uw virtuele netwerk zijn.</span><span class="sxs-lookup"><span data-stu-id="a2384-150">Then you can create A records in your DNS Server tooaccess these endpoints which are only accessible from within your Virtual network.</span></span>

## <span data-ttu-id="a2384-151"><a name="related-content"></a>Verwante inhoud</span><span class="sxs-lookup"><span data-stu-id="a2384-151"><a name="related-content"> </a>Related content</span></span>
* <span data-ttu-id="a2384-152">[Configuratie van algemene netwerkproblemen tijdens het instellen van APIM in VNET][Common Network Configuration Issues]</span><span class="sxs-lookup"><span data-stu-id="a2384-152">[Common Network configuration issues while setting up APIM in VNET][Common Network Configuration Issues]</span></span>
* [<span data-ttu-id="a2384-153">Virtueel netwerk Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="a2384-153">Virtual Network faqs</span></span>](../virtual-network/virtual-networks-faq.md)
* [<span data-ttu-id="a2384-154">Maken van A-record in DNS</span><span class="sxs-lookup"><span data-stu-id="a2384-154">Creating A record in DNS</span></span>](https://msdn.microsoft.com/en-us/library/bb727018.aspx)

[api-management-using-internal-vnet-menu]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-menu.png
[api-management-internal-vnet-dashboard]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-dashboard.png
[api-management-custom-domain-name]: ./media/api-management-using-with-internal-vnet/api-management-custom-domain-name.png

[Create API Management service]: api-management-get-started.md#create-service-instance
[Common Network Configuration Issues]: api-management-using-with-vnet.md#network-configuration-issues
