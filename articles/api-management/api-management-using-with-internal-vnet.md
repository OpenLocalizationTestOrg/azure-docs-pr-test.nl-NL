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
# <a name="using-azure-api-management-service-with-internal-virtual-network"></a><span data-ttu-id="4c1a9-103">Met behulp van Azure API Management-service met een intern virtueel netwerk</span><span class="sxs-lookup"><span data-stu-id="4c1a9-103">Using Azure API Management service with Internal Virtual Network</span></span>
<span data-ttu-id="4c1a9-104">Met virtuele netwerken van Azure (vnet's) beheren API Management API's die niet toegankelijk op het Internet.</span><span class="sxs-lookup"><span data-stu-id="4c1a9-104">With Azure Virtual Networks (VNETs), API Management can manage APIs not accessible on the Internet.</span></span> <span data-ttu-id="4c1a9-105">Een aantal VPN-technologieën zijn beschikbaar voor het maken van de verbinding en API Management kan worden geïmplementeerd in twee belangrijke modi binnen het VNET:</span><span class="sxs-lookup"><span data-stu-id="4c1a9-105">A number of VPN technologies are available to make the connection and API Management can be deployed in two main modes inside the VNET:</span></span>
* <span data-ttu-id="4c1a9-106">Extern</span><span class="sxs-lookup"><span data-stu-id="4c1a9-106">External</span></span>
* <span data-ttu-id="4c1a9-107">interne</span><span class="sxs-lookup"><span data-stu-id="4c1a9-107">Internal</span></span>

## <span data-ttu-id="4c1a9-108"><a name="overview"> </a>Overzicht</span><span class="sxs-lookup"><span data-stu-id="4c1a9-108"><a name="overview"> </a>Overview</span></span>
<span data-ttu-id="4c1a9-109">Wanneer API Management wordt geïmplementeerd in een modus voor interne virtuele netwerk, alle de service-eindpunten (gateway, developer-portal, publicatieportal, direct beheer en Git) zijn alleen zichtbaar binnen een virtueel netwerk dat u beheert de toegang tot.</span><span class="sxs-lookup"><span data-stu-id="4c1a9-109">When API Management is deployed in an Internal Virtual network mode, all the service endpoints (gateway, developer portal, publisher portal, direct management and Git) are only visible inside a Virtual network that you control access to.</span></span> <span data-ttu-id="4c1a9-110">Geen van de service-eindpunten zijn geregistreerd op de openbare DNS-Server.</span><span class="sxs-lookup"><span data-stu-id="4c1a9-110">None of the service endpoints are registered on the Public DNS Server.</span></span>

<span data-ttu-id="4c1a9-111">Met behulp van API Management in de interne modus, kunt u de volgende scenario's bereiken</span><span class="sxs-lookup"><span data-stu-id="4c1a9-111">Using API Management in Internal mode, you can achieve the following scenarios</span></span>
* <span data-ttu-id="4c1a9-112">Veilig aanbrengen in uw persoonlijke datacenter toegankelijk door 3e partijen buiten de Site-naar-Site of ExpressRoute-VPN-verbindingen met gehoste API's.</span><span class="sxs-lookup"><span data-stu-id="4c1a9-112">Securely make APIs hosted in your private datacenter accessible by 3rd parties outside of it using Site-to-Site or ExpressRoute VPN connections.</span></span>
* <span data-ttu-id="4c1a9-113">Hybride cloud-scenario's mogelijk bij het blootstellen van uw cloud-gebaseerde API's en on-premises-API's via een gemeenschappelijke gateway.</span><span class="sxs-lookup"><span data-stu-id="4c1a9-113">Enable hybrid cloud scenarios by exposing your cloud-based APIs and on-prem APIs through a common gateway.</span></span>
* <span data-ttu-id="4c1a9-114">Beheren van uw API's die worden gehost in meerdere geografische locaties met behulp van één Gateway-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="4c1a9-114">Manage your APIs hosted in multiple geographic locations using a single Gateway endpoint.</span></span> 

## <span data-ttu-id="4c1a9-115"><a name="enable-vpn"></a>Een API Management in interne virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="4c1a9-115"><a name="enable-vpn"> </a>Creating an API Management in Internal Virtual network</span></span>
<span data-ttu-id="4c1a9-116">De API Management-service in het interne virtuele netwerk wordt achter een interne Load Balancer(ILB) gehost.</span><span class="sxs-lookup"><span data-stu-id="4c1a9-116">The API Management service in Internal Virtual network is hosted behind an Internal Load Balancer(ILB).</span></span> <span data-ttu-id="4c1a9-117">Het IP-adres van de ILB is in de [RFC1918](http://www.faqs.org/rfcs/rfc1918.html) bereik.</span><span class="sxs-lookup"><span data-stu-id="4c1a9-117">The IP Address of the ILB is in the [RFC1918](http://www.faqs.org/rfcs/rfc1918.html) range.</span></span>  

### <a name="enable-vnet-connection-using-azure-portal"></a><span data-ttu-id="4c1a9-118">VNET-verbinding met Azure portal inschakelen</span><span class="sxs-lookup"><span data-stu-id="4c1a9-118">Enable VNET connection using Azure portal</span></span>
<span data-ttu-id="4c1a9-119">De API Management-service eerst te maken door de stappen te volgen [maken API Management-service][Create API Management service].</span><span class="sxs-lookup"><span data-stu-id="4c1a9-119">First create the API Management service by following the steps [Create API Management service][Create API Management service].</span></span> <span data-ttu-id="4c1a9-120">Vervolgens set-up API Management binnen een virtueel netwerk worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="4c1a9-120">Then set-up API Management to be deployed inside a Virtual network.</span></span>

![Menu voor het instellen van APIM in een intern virtueel netwerk][api-management-using-internal-vnet-menu]

<span data-ttu-id="4c1a9-122">Nadat de implementatie is geslaagd, ziet u de interne virtuele IP-adres van uw service op het dashboard.</span><span class="sxs-lookup"><span data-stu-id="4c1a9-122">After the deployment succeeds, you should see the Internal Virtual IP Address of your service on the dashboard.</span></span>

![API Management Dashboard met interne VNET geconfigureerd][api-management-internal-vnet-dashboard]

### <a name="enable-vnet-connection-using-powershell-cmdlets"></a><span data-ttu-id="4c1a9-124">VNET-verbinding met Powershell-cmdlets inschakelen</span><span class="sxs-lookup"><span data-stu-id="4c1a9-124">Enable VNET connection using Powershell cmdlets</span></span>
<span data-ttu-id="4c1a9-125">U kunt ook inschakelen met behulp van de PowerShell-cmdlets voor VNET-connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="4c1a9-125">You can also enable VNET connectivity using the PowerShell cmdlets.</span></span>

* <span data-ttu-id="4c1a9-126">**Maak een API Management-service binnen een VNET**: Gebruik de cmdlet [nieuw AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) een Azure API Management-service binnen een VNET maken en configureren voor het gebruik van het type interne VNET.</span><span class="sxs-lookup"><span data-stu-id="4c1a9-126">**Create an API Management service inside a VNET**: Use the cmdlet [New-AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) to create an Azure API Management service inside a VNET and configure it to use the Internal VNET type.</span></span>

* <span data-ttu-id="4c1a9-127">**Implementeren van een bestaande API Management-service binnen een VNET**: Gebruik de cmdlet [Update AzureRmApiManagementDeployment](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) verplaatsen van een bestaande Azure API Management-service binnen een virtueel netwerk en configureren voor gebruik Interne VNET-type.</span><span class="sxs-lookup"><span data-stu-id="4c1a9-127">**Deploy an existing API Management service inside a VNET**: Use the cmdlet [Update-AzureRmApiManagementDeployment](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) to move an existing Azure API Management service inside a Virtual network and configure it to use Internal VNET type.</span></span>

## <span data-ttu-id="4c1a9-128"><a name="apim-dns-configuration"></a>DNS-configuratie</span><span class="sxs-lookup"><span data-stu-id="4c1a9-128"><a name="apim-dns-configuration"></a>DNS configuration</span></span>
<span data-ttu-id="4c1a9-129">Wanneer u API Management in de externe virtuele netwerkmodus gebruikt, wordt door Azure DNS beheerd.</span><span class="sxs-lookup"><span data-stu-id="4c1a9-129">When using API Management in External Virtual network mode, DNS is managed by Azure.</span></span> <span data-ttu-id="4c1a9-130">U hebt voor het beheren van uw eigen DNS voor de interne virtuele netwerk-modus.</span><span class="sxs-lookup"><span data-stu-id="4c1a9-130">For Internal Virtual network mode, you have to manage your own DNS.</span></span>

> [!NOTE]
> <span data-ttu-id="4c1a9-131">API Management-service luistert niet op aanvragen die afkomstig zijn van IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="4c1a9-131">API Management service does not listen to requests coming on IP addresses.</span></span> <span data-ttu-id="4c1a9-132">Alleen reageert op aanvragen voor de hostnaam geconfigureerd op de service-eindpunten (waaronder gateway, developer-portal, publisher Portal, direct beheer eindpunt en git).</span><span class="sxs-lookup"><span data-stu-id="4c1a9-132">It only responds to requests to the Hostname configured on its service endpoints (which includes gateway, developer portal, publisher Portal, direct management endpoint, and git).</span></span>

### <a name="access-on-default-host-names"></a><span data-ttu-id="4c1a9-133">Toegang van standaard hostnamen:</span><span class="sxs-lookup"><span data-stu-id="4c1a9-133">Access on default host names:</span></span>
<span data-ttu-id="4c1a9-134">Wanneer u een API Management-service maakt in openbare Azure-cloud, met bijvoorbeeld de naam 'contoso', worden de volgende service-eindpunten standaard geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="4c1a9-134">When you create an API Management service in public Azure cloud, named "contoso" for example, the following service endpoints are configured by default.</span></span>

>   <span data-ttu-id="4c1a9-135">Gateway / Proxy - contoso.azure api.net</span><span class="sxs-lookup"><span data-stu-id="4c1a9-135">Gateway / Proxy - contoso.azure-api.net</span></span>

> <span data-ttu-id="4c1a9-136">Publicatieportal en -Portal voor ontwikkelaars - contoso.portal.azure api.net</span><span class="sxs-lookup"><span data-stu-id="4c1a9-136">Publisher Portal and Developer Portal - contoso.portal.azure-api.net</span></span>

> <span data-ttu-id="4c1a9-137">Direct beheer Endpoint - contoso.management.azure api.net</span><span class="sxs-lookup"><span data-stu-id="4c1a9-137">Direct Management Endpoint - contoso.management.azure-api.net</span></span>

>   <span data-ttu-id="4c1a9-138">GIT - contoso.scm.azure api.net</span><span class="sxs-lookup"><span data-stu-id="4c1a9-138">GIT - contoso.scm.azure-api.net</span></span>

<span data-ttu-id="4c1a9-139">Voor toegang tot deze API Management-service-eindpunten, kunt u een virtuele Machine in een subnet is verbonden met het virtuele netwerk waarin API Management wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="4c1a9-139">To access these API Management service endpoints, you can create a Virtual Machine in a subnet connected to the Virtual network in which API Management is deployed.</span></span> <span data-ttu-id="4c1a9-140">Ervan uitgaande dat de interne virtuele IP-adres voor uw service 10.0.0.5 is, kunt u de hosts doen bestand toewijzing (% SystemDrive%\drivers\etc\hosts) als volgt:</span><span class="sxs-lookup"><span data-stu-id="4c1a9-140">Assuming the Internal Virtual IP Address for your service is 10.0.0.5, you can do the hosts file mapping (%SystemDrive%\drivers\etc\hosts) as follows:</span></span>

> <span data-ttu-id="4c1a9-141">10.0.0.5 contoso.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="4c1a9-141">10.0.0.5    contoso.azure-api.net</span></span>

> <span data-ttu-id="4c1a9-142">10.0.0.5 contoso.portal.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="4c1a9-142">10.0.0.5    contoso.portal.azure-api.net</span></span>

> <span data-ttu-id="4c1a9-143">10.0.0.5 contoso.management.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="4c1a9-143">10.0.0.5    contoso.management.azure-api.net</span></span>

> <span data-ttu-id="4c1a9-144">10.0.0.5 contoso.scm.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="4c1a9-144">10.0.0.5    contoso.scm.azure-api.net</span></span>

<span data-ttu-id="4c1a9-145">U kunt vervolgens toegang tot alle service-eindpunten van de virtuele Machine die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4c1a9-145">You can then access all the service endpoints from the Virtual Machine you created.</span></span> <span data-ttu-id="4c1a9-146">Als u een aangepaste DNS-server in een virtueel netwerk gebruikt, u kunt ook een DNS-records maken en toegang tot deze eindpunten vanaf elke locatie in het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="4c1a9-146">If using a Custom DNS server in a Virtual network, you can also create A DNS records and access these endpoints from anywhere in your Virtual network.</span></span> 

### <a name="access-on-custom-domain-names"></a><span data-ttu-id="4c1a9-147">Toegang van aangepaste domeinnamen:</span><span class="sxs-lookup"><span data-stu-id="4c1a9-147">Access on custom domain names:</span></span>
<span data-ttu-id="4c1a9-148">Als u toegang tot de API Management-service met de standaard hostnamen niet wilt, kunt u aangepaste domeinnamen voor alle uw service-eindpunten zoals hieronder instellen</span><span class="sxs-lookup"><span data-stu-id="4c1a9-148">If you don’t want to access the API Management service with the default host names, you can setup custom domain names for all your service endpoints like below</span></span>

![Instellen van het aangepaste domein voor API Management][api-management-custom-domain-name]

<span data-ttu-id="4c1a9-150">Vervolgens kunt u A-records maken in uw DNS-Server voor toegang tot deze eindpunten die alleen toegankelijk vanuit uw virtuele netwerk zijn.</span><span class="sxs-lookup"><span data-stu-id="4c1a9-150">Then you can create A records in your DNS Server to access these endpoints which are only accessible from within your Virtual network.</span></span>

## <span data-ttu-id="4c1a9-151"><a name="related-content"></a>Verwante inhoud</span><span class="sxs-lookup"><span data-stu-id="4c1a9-151"><a name="related-content"> </a>Related content</span></span>
* <span data-ttu-id="4c1a9-152">[Configuratie van algemene netwerkproblemen tijdens het instellen van APIM in VNET][Common Network Configuration Issues]</span><span class="sxs-lookup"><span data-stu-id="4c1a9-152">[Common Network configuration issues while setting up APIM in VNET][Common Network Configuration Issues]</span></span>
* [<span data-ttu-id="4c1a9-153">Virtueel netwerk Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="4c1a9-153">Virtual Network faqs</span></span>](../virtual-network/virtual-networks-faq.md)
* [<span data-ttu-id="4c1a9-154">Maken van A-record in DNS</span><span class="sxs-lookup"><span data-stu-id="4c1a9-154">Creating A record in DNS</span></span>](https://msdn.microsoft.com/en-us/library/bb727018.aspx)

[api-management-using-internal-vnet-menu]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-menu.png
[api-management-internal-vnet-dashboard]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-dashboard.png
[api-management-custom-domain-name]: ./media/api-management-using-with-internal-vnet/api-management-custom-domain-name.png

[Create API Management service]: api-management-get-started.md#create-service-instance
[Common Network Configuration Issues]: api-management-using-with-vnet.md#network-configuration-issues
