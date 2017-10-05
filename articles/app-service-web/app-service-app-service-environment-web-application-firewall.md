---
title: Web Application Firewall (WAF) configureren voor App Service-omgeving
description: Informatie over het configureren van een web application firewall voor uw App Service-omgeving.
services: app-service\web
documentationcenter: 
author: naziml
manager: erikre
editor: jimbe
ms.assetid: a2101291-83ba-4169-98a2-2c0ed9a65e8d
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: naziml
ms.openlocfilehash: 3e9e9fa4ddab60a467e8aa793ec0ca269b0bc4e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-a-web-application-firewall-waf-for-app-service-environment"></a><span data-ttu-id="983c0-103">Web Application Firewall (WAF) configureren voor App Service-omgeving</span><span class="sxs-lookup"><span data-stu-id="983c0-103">Configuring a Web Application Firewall (WAF) for App Service Environment</span></span>
## <a name="overview"></a><span data-ttu-id="983c0-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="983c0-104">Overview</span></span>
<span data-ttu-id="983c0-105">Web application firewalls, zoals de [Barracuda WAF voor Azure](https://www.barracuda.com/programs/azure) die beschikbaar is op de [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) helpt bij het beveiligen van uw webtoepassingen door te inspecteren inkomend webverkeer blokkeren SQL-injectie, Cross-Site Scripting, malware uploads & DDoS-toepassing en andere aanvallen.</span><span class="sxs-lookup"><span data-stu-id="983c0-105">Web application firewalls like the [Barracuda WAF for Azure](https://www.barracuda.com/programs/azure) that is available on the [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) helps secure your web applications by inspecting inbound web traffic to block SQL injections, Cross-Site Scripting, malware uploads & application DDoS and other attacks.</span></span> <span data-ttu-id="983c0-106">Deze ook inspecteert de antwoorden van de back-end-webservers gegevens gegevensverlies te voorkomen (DLP).</span><span class="sxs-lookup"><span data-stu-id="983c0-106">It also inspects the responses from the back-end web servers for Data Loss Prevention (DLP).</span></span> <span data-ttu-id="983c0-107">In combinatie met de isolatie en aanvullende schalen geleverd door App Service-omgevingen, biedt dit een ideale omgeving naar host business kritieke webtoepassingen die bestand zijn tegen schadelijke aanvragen en grote hoeveelheden verkeer wilt.</span><span class="sxs-lookup"><span data-stu-id="983c0-107">Combined with the isolation and additional scaling provided by App Service Environments, this provides an ideal environment to host business critical web applications that need to withstand malicious requests and high volume traffic.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)] 

## <a name="setup"></a><span data-ttu-id="983c0-108">Instellen</span><span class="sxs-lookup"><span data-stu-id="983c0-108">Setup</span></span>
<span data-ttu-id="983c0-109">Onze App Service-omgeving achter meerdere load balanced exemplaren van Barracuda WAF voor dit document die we configureert zodat alleen verkeer van de WAF App Service-omgeving bereiken kan en zal deze niet toegankelijk is vanaf het Perimeternetwerk.</span><span class="sxs-lookup"><span data-stu-id="983c0-109">For this document we will configure our App Service Environment behind multiple load balanced instances of Barracuda WAF so that only traffic from the WAF can reach the App Service Environment and it will not be accessible from the DMZ.</span></span> <span data-ttu-id="983c0-110">We hebben ook Azure Traffic Manager voor onze Barracuda WAF exemplaren te verdelen over Azure-datacenters en regio's.</span><span class="sxs-lookup"><span data-stu-id="983c0-110">We will also have Azure Traffic Manager in front of our Barracuda WAF instances to load balance across Azure data centers and regions.</span></span> <span data-ttu-id="983c0-111">Een hoog niveau diagram van de installatie eruit zou wat wordt hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="983c0-111">A high level diagram of the setup would look like what is shown below.</span></span>

![Architectuur][Architecture] 

> <span data-ttu-id="983c0-113">Opmerking: door de introductie van [ILB ondersteuning voor App Service-omgeving](app-service-environment-with-internal-load-balancer.md), kunt u het as-omgeving om te worden niet toegankelijk vanaf het Perimeternetwerk en alleen beschikbaar voor het particuliere netwerk configureren.</span><span class="sxs-lookup"><span data-stu-id="983c0-113">Note: With the introduction of [ILB support for App Service Environment](app-service-environment-with-internal-load-balancer.md), you can configure the ASE to be inaccessible from the DMZ and only be available to the private network.</span></span> 
> 
> 

## <a name="configuring-your-app-service-environment"></a><span data-ttu-id="983c0-114">Uw App-serviceomgeving configureren</span><span class="sxs-lookup"><span data-stu-id="983c0-114">Configuring your App Service Environment</span></span>
<span data-ttu-id="983c0-115">Voor het configureren van een App-serviceomgeving verwijzen naar [onze documentatie](app-service-web-how-to-create-an-app-service-environment.md) over dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="983c0-115">To configure an App Service Environment refer to [our documentation](app-service-web-how-to-create-an-app-service-environment.md) on the subject.</span></span> <span data-ttu-id="983c0-116">Zodra u een App-serviceomgeving is gemaakt hebt, kunt u [Web-Apps](app-service-web-overview.md), [API Apps](../app-service-api/app-service-api-apps-why-best-platform.md) en [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) in deze omgeving die al worden beveiligd achter de WAF we in de volgende sectie configureren.</span><span class="sxs-lookup"><span data-stu-id="983c0-116">Once you have an App Service Environment created, you can create [Web Apps](app-service-web-overview.md), [API Apps](../app-service-api/app-service-api-apps-why-best-platform.md) and [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) in this environment that will all be protected behind the WAF we configure in the next section.</span></span>

## <a name="configuring-your-barracuda-waf-cloud-service"></a><span data-ttu-id="983c0-117">Uw Barracuda WAF Cloud Service configureren</span><span class="sxs-lookup"><span data-stu-id="983c0-117">Configuring your Barracuda WAF Cloud Service</span></span>
<span data-ttu-id="983c0-118">Barracuda heeft een [gedetailleerde artikel](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) over het implementeren van de WAF op een virtuele machine in Azure.</span><span class="sxs-lookup"><span data-stu-id="983c0-118">Barracuda has a [detailed article](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) on deploying its WAF on a virtual machine in Azure.</span></span> <span data-ttu-id="983c0-119">Maar omdat we redundantie wilt en geen een potentieel risico introduceren, u wilt implementeren ten minste 2 WAF exemplaar virtuele machines in dezelfde Cloud-Service wanneer deze instructies te volgen.</span><span class="sxs-lookup"><span data-stu-id="983c0-119">But because we want redundancy and not introduce a single point of failure, you want to deploy at least 2 WAF instance VMs into the same Cloud Service when following these instructions.</span></span>

### <a name="adding-endpoints-to-cloud-service"></a><span data-ttu-id="983c0-120">Toevoegen van eindpunten in de Cloud Service</span><span class="sxs-lookup"><span data-stu-id="983c0-120">Adding Endpoints to Cloud Service</span></span>
<span data-ttu-id="983c0-121">Nadat u 2 hebt of meer WAF VM-in uw Cloud-Service exemplaren kunt u de [Azure-portal](https://portal.azure.com/) HTTP en HTTPS-eindpunten die worden gebruikt door uw toepassing, zoals wordt weergegeven in de onderstaande afbeelding toevoegen.</span><span class="sxs-lookup"><span data-stu-id="983c0-121">Once you have 2 or more WAF VM instances in your Cloud Service you can use the [Azure portal](https://portal.azure.com/) to add HTTP and HTTPS endpoints that are used by your application as shown in the image below.</span></span>

![-Eindpunt configureren][ConfigureEndpoint]

<span data-ttu-id="983c0-123">Als uw toepassingen met andere eindpunten, zorg er dan voor dat deze toevoegen aan deze lijst ook.</span><span class="sxs-lookup"><span data-stu-id="983c0-123">If your applications use other endpoints, make sure to add those to this list as well.</span></span> 

### <a name="configuring-barracuda-waf-through-its-management-portal"></a><span data-ttu-id="983c0-124">Barracuda WAF via de beheerportal configureren</span><span class="sxs-lookup"><span data-stu-id="983c0-124">Configuring Barracuda WAF through its Management Portal</span></span>
<span data-ttu-id="983c0-125">Barracuda WAF maakt gebruik van TCP-poort 8000 voor configuratie via de beheerportal.</span><span class="sxs-lookup"><span data-stu-id="983c0-125">Barracuda WAF uses TCP Port 8000 for configuration through its management portal.</span></span> <span data-ttu-id="983c0-126">Aangezien we er meerdere exemplaren van de WAF virtuele machines moet u hier de stappen herhalen voor elke VM-instantie.</span><span class="sxs-lookup"><span data-stu-id="983c0-126">Since we have multiple instances of the WAF VMs you will need to repeat the steps here for each VM instance.</span></span> 

> <span data-ttu-id="983c0-127">Opmerking: Wanneer u klaar bent met WAF configuratie, verwijdert het TCP/8000-eindpunt van uw WAF VMs uw WAF om veilig te houden.</span><span class="sxs-lookup"><span data-stu-id="983c0-127">Note: Once you are done with WAF configuration, remove the TCP/8000 endpoint from all your WAF VMs to keep your WAF secure.</span></span>
> 
> 

<span data-ttu-id="983c0-128">Het eindpunt management zoals weergegeven in de onderstaande afbeelding voor het configureren van uw Barracuda WAF toevoegen</span><span class="sxs-lookup"><span data-stu-id="983c0-128">Add the management endpoint as shown in the image below to configure your Barracuda WAF.</span></span>

![Management-eindpunt toevoegen][AddManagementEndpoint]

<span data-ttu-id="983c0-130">Een browser gebruiken om te bladeren naar het eindpunt van het beheer op uw Cloud-Service.</span><span class="sxs-lookup"><span data-stu-id="983c0-130">Use a browser to browse to the management endpoint on your Cloud Service.</span></span> <span data-ttu-id="983c0-131">Als uw Cloudservice test.cloudapp.net aangeroepen wordt, zou u dit eindpunt openen door te bladeren naar http://test.cloudapp.net:8000.</span><span class="sxs-lookup"><span data-stu-id="983c0-131">If your Cloud Service is called test.cloudapp.net, you would access this endpoint by browsing to http://test.cloudapp.net:8000.</span></span> <span data-ttu-id="983c0-132">U ziet een aanmeldingspagina zoals hieronder dat u zich kunt aanmelden met referenties die u hebt opgegeven in de installatiefase WAF VM.</span><span class="sxs-lookup"><span data-stu-id="983c0-132">You should see a login page like below that you can login using credentials you specified in the WAF VM setup phase.</span></span>

![Aanmeldingspagina voor beheer][ManagementLoginPage]

<span data-ttu-id="983c0-134">Eenmaal u aanmelding ziet u een dashboard als het nummer in de onderstaande afbeelding elementaire statistieken over de beveiliging WAF biedt.</span><span class="sxs-lookup"><span data-stu-id="983c0-134">Once you login you should see a dashboard as the one in the image below that will present basic statistics about the WAF protection.</span></span>

![Management Dashboard][ManagementDashboard]

<span data-ttu-id="983c0-136">Klik op het tabblad Services kunt u configureren dat uw WAF voor services die deze beveiligt.</span><span class="sxs-lookup"><span data-stu-id="983c0-136">Clicking on the Services tab will let you configure your WAF for services it is protecting.</span></span> <span data-ttu-id="983c0-137">U kunt raadplegen voor meer informatie over het configureren van uw WAF Barracuda [hun documentatie](https://techlib.barracuda.com/waf/getstarted1).</span><span class="sxs-lookup"><span data-stu-id="983c0-137">For more details on configuring your Barracuda WAF you can consult [their documentation](https://techlib.barracuda.com/waf/getstarted1).</span></span> <span data-ttu-id="983c0-138">In het voorbeeld hieronder een Azure-Web-App is voor verkeer op HTTP- en HTTPS geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="983c0-138">In the example below an Azure Web App serving traffic on HTTP and HTTPS has been configured.</span></span>

![Management-Services toevoegen][ManagementAddServices]

> <span data-ttu-id="983c0-140">Opmerking: Afhankelijk van hoe uw toepassingen worden geconfigureerd en welke functies in uw App Service-omgeving worden gebruikt, u moet voor het doorsturen van verkeer voor TCP-poorten dan 80 en 443, bijvoorbeeld als u setup voor IP-SSL voor een Web-App.</span><span class="sxs-lookup"><span data-stu-id="983c0-140">Note: Depending on how your applications are configured and what features are being used in your App Service Environment, you will need to forward traffic for TCP ports other than 80 and 443, e.g. if you have IP SSL setup for a Web App.</span></span> <span data-ttu-id="983c0-141">Voor een lijst met netwerkpoorten die in App Service-omgevingen worden gebruikt, raadpleegt u [inkomend verkeer voor beheer-documentatie](app-service-app-service-environment-control-inbound-traffic.md) netwerkpoorten sectie.</span><span class="sxs-lookup"><span data-stu-id="983c0-141">For a list of network ports used in App Service Environments, please refer to [Control Inbound Traffic documentation's](app-service-app-service-environment-control-inbound-traffic.md) Network Ports section.</span></span>
> 
> 

## <a name="configuring-microsoft-azure-traffic-manager-optional"></a><span data-ttu-id="983c0-142">Configureren van Microsoft Azure Traffic Manager (optioneel)</span><span class="sxs-lookup"><span data-stu-id="983c0-142">Configuring Microsoft Azure Traffic Manager (OPTIONAL)</span></span>
<span data-ttu-id="983c0-143">Als uw toepassing beschikbaar in meerdere regio's, is wordt u wilt laden saldo achter [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="983c0-143">If your application is available in multiple regions, then you would want to load balance them behind [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md).</span></span> <span data-ttu-id="983c0-144">Hiervoor kunt u een eindpunt in toevoegen de [klassieke Azure-portal](https://manage.azure.com) met de naam van de Cloudservice voor uw WAF in Traffic Manager-profiel, zoals wordt weergegeven in de onderstaande afbeelding.</span><span class="sxs-lookup"><span data-stu-id="983c0-144">To do so you can add an endpoint in the [Azure classic portal](https://manage.azure.com) using the Cloud Service name for your WAF in the Traffic Manager profile as shown in the image below.</span></span> 

![Traffic Manager-eindpunt][TrafficManagerEndpoint]

<span data-ttu-id="983c0-146">Als uw toepassing verificatie vereist, zorg ervoor dat u hebt een resource die geen verificatie voor Traffic Manager te pingen niet vereist voor de beschikbaarheid van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="983c0-146">If your application requires authentication, ensure you have some resource that doesn't require any authentication for Traffic Manager to ping for the availability of your application.</span></span> <span data-ttu-id="983c0-147">U kunt de URL in de sectie Configure configureren op de [klassieke Azure-portal](https://manage.azure.com) zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="983c0-147">You can configure the URL under the Configure section on the [Azure classic portal](https://manage.azure.com) as shown below.</span></span>

![Traffic Manager configureren][ConfigureTrafficManager]

<span data-ttu-id="983c0-149">Het Traffic Manager-pings verder vanaf uw WAF voor uw toepassing, moet u setup vertalingen van de Website op uw WAF Barracuda voor het doorsturen van verkeer naar uw toepassing, zoals wordt weergegeven in het onderstaande voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="983c0-149">To forward the Traffic Manager pings from your WAF to your application, you need to setup Website Translations on your Barracuda WAF to forward traffic to your application as shown in the example below.</span></span>

![Vertalingen van de website][WebsiteTranslations]

## <a name="securing-traffic-to-app-service-environment-using-network-security-groups-nsg"></a><span data-ttu-id="983c0-151">Beveiligen van verkeer naar App Service-omgeving met behulp van Netwerkbeveiligingsgroepen (NSG)</span><span class="sxs-lookup"><span data-stu-id="983c0-151">Securing Traffic to App Service Environment Using Network Security Groups (NSG)</span></span>
<span data-ttu-id="983c0-152">Ga als volgt de [besturingselement binnenkomend verkeer documentatie](app-service-app-service-environment-control-inbound-traffic.md) voor meer informatie over het verkeer beperkt tot uw App Service-omgeving van de WAF alleen met behulp van de VIP-adres van uw Cloud-Service.</span><span class="sxs-lookup"><span data-stu-id="983c0-152">Follow the [Control Inbound Traffic documentation](app-service-app-service-environment-control-inbound-traffic.md) for details on restricting traffic to your App Service Environment from the WAF only by using the VIP address of your Cloud Service.</span></span> <span data-ttu-id="983c0-153">Hier volgt een voorbeeld-Powershell-opdracht voor het uitvoeren van deze taak voor TCP-poort 80.</span><span class="sxs-lookup"><span data-stu-id="983c0-153">Here's a sample Powershell command for performing this task for TCP port 80.</span></span>

    Get-AzureNetworkSecurityGroup -Name "RestrictWestUSAppAccess" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP Barracuda" -Type Inbound -Priority 201 -Action Allow -SourceAddressPrefix '191.0.0.1'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP

<span data-ttu-id="983c0-154">De SourceAddressPrefix vervangen door het virtuele IP-adres (VIP) van uw WAF-Cloudservice.</span><span class="sxs-lookup"><span data-stu-id="983c0-154">Replace the SourceAddressPrefix with the Virtual IP Address (VIP) of your WAF's Cloud Service.</span></span>

> <span data-ttu-id="983c0-155">Opmerking: Het VIP van uw Cloud-Service wordt gewijzigd wanneer u verwijderen en opnieuw maken van de Cloudservice.</span><span class="sxs-lookup"><span data-stu-id="983c0-155">Note: The VIP of your Cloud Service will change when you delete and re-create the Cloud Service.</span></span> <span data-ttu-id="983c0-156">Zorg ervoor dat het IP-adres in de resourcegroep netwerk bijwerken nadat u doet dit.</span><span class="sxs-lookup"><span data-stu-id="983c0-156">Make sure to update the IP address in the Network Resource group once you do so.</span></span> 
> 
> 

<!-- IMAGES -->
[Architecture]: ./media/app-service-app-service-environment-web-application-firewall/Architecture.png
[ConfigureEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/ConfigureEndpoint.png
[AddManagementEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/AddManagementEndpoint.png
[ManagementAddServices]: ./media/app-service-app-service-environment-web-application-firewall/ManagementAddServices.png
[ManagementDashboard]: ./media/app-service-app-service-environment-web-application-firewall/ManagementDashboard.png
[ManagementLoginPage]: ./media/app-service-app-service-environment-web-application-firewall/ManagementLoginPage.png
[TrafficManagerEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/TrafficManagerEndpoint.png
[ConfigureTrafficManager]: ./media/app-service-app-service-environment-web-application-firewall/ConfigureTrafficManager.png
[WebsiteTranslations]: ./media/app-service-app-service-environment-web-application-firewall/WebsiteTranslations.png
