---
title: aaaConfiguring een Web Application Firewall (WAF) voor App Service-omgeving
description: Meer informatie over hoe een webtoepassing tooconfigure firewall voor uw App Service-omgeving.
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
ms.openlocfilehash: 0fcf62aea871751c9d4f294d2d24df2186fc0e7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-web-application-firewall-waf-for-app-service-environment"></a><span data-ttu-id="55901-103">Web Application Firewall (WAF) configureren voor App Service-omgeving</span><span class="sxs-lookup"><span data-stu-id="55901-103">Configuring a Web Application Firewall (WAF) for App Service Environment</span></span>
## <a name="overview"></a><span data-ttu-id="55901-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="55901-104">Overview</span></span>
<span data-ttu-id="55901-105">Web application firewalls zoals Hallo [Barracuda WAF voor Azure](https://www.barracuda.com/programs/azure) die beschikbaar is op Hallo [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) helpt uw webtoepassingen beveiligen door web binnenkomend verkeer tooblock SQL te bekijken injectie, Cross-Site Scripting, malware uploads & DDoS-toepassing en andere aanvallen.</span><span class="sxs-lookup"><span data-stu-id="55901-105">Web application firewalls like hello [Barracuda WAF for Azure](https://www.barracuda.com/programs/azure) that is available on hello [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) helps secure your web applications by inspecting inbound web traffic tooblock SQL injections, Cross-Site Scripting, malware uploads & application DDoS and other attacks.</span></span> <span data-ttu-id="55901-106">Deze ook inspecteert Hallo-antwoorden van back-end-webservers Hallo gegevens gegevensverlies te voorkomen (DLP).</span><span class="sxs-lookup"><span data-stu-id="55901-106">It also inspects hello responses from hello back-end web servers for Data Loss Prevention (DLP).</span></span> <span data-ttu-id="55901-107">In combinatie met de Hallo isolatie en aanvullende schalen geleverd door App Service-omgevingen, biedt dit een ideale omgeving toohost business kritieke webtoepassingen die toowithstand schadelijke aanvragen en grote hoeveelheden verkeer nodig.</span><span class="sxs-lookup"><span data-stu-id="55901-107">Combined with hello isolation and additional scaling provided by App Service Environments, this provides an ideal environment toohost business critical web applications that need toowithstand malicious requests and high volume traffic.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)] 

## <a name="setup"></a><span data-ttu-id="55901-108">Instellen</span><span class="sxs-lookup"><span data-stu-id="55901-108">Setup</span></span>
<span data-ttu-id="55901-109">Onze App Service-omgeving achter meerdere load balanced exemplaren van Barracuda WAF voor dit document die we configureert zodat alleen verkeer van Hallo WAF Hallo App Service-omgeving bereiken kan en zal deze niet toegankelijk is vanaf Hallo DMZ.</span><span class="sxs-lookup"><span data-stu-id="55901-109">For this document we will configure our App Service Environment behind multiple load balanced instances of Barracuda WAF so that only traffic from hello WAF can reach hello App Service Environment and it will not be accessible from hello DMZ.</span></span> <span data-ttu-id="55901-110">We ook hebt Azure Traffic Manager voor onze Barracuda WAF exemplaren tooload saldo in Azure-datacenters en regio's.</span><span class="sxs-lookup"><span data-stu-id="55901-110">We will also have Azure Traffic Manager in front of our Barracuda WAF instances tooload balance across Azure data centers and regions.</span></span> <span data-ttu-id="55901-111">Een hoog niveau diagram van Hallo setup eruit zou wat wordt hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="55901-111">A high level diagram of hello setup would look like what is shown below.</span></span>

![Architectuur][Architecture] 

> <span data-ttu-id="55901-113">Opmerking: met de introductie van Hallo [ILB ondersteuning voor App Service-omgeving](app-service-environment-with-internal-load-balancer.md), kunt u configureren Hallo as-omgeving toobe niet toegankelijk vanuit Hallo DMZ en worden alleen beschikbaar toohello particuliere netwerk.</span><span class="sxs-lookup"><span data-stu-id="55901-113">Note: With hello introduction of [ILB support for App Service Environment](app-service-environment-with-internal-load-balancer.md), you can configure hello ASE toobe inaccessible from hello DMZ and only be available toohello private network.</span></span> 
> 
> 

## <a name="configuring-your-app-service-environment"></a><span data-ttu-id="55901-114">Uw App-serviceomgeving configureren</span><span class="sxs-lookup"><span data-stu-id="55901-114">Configuring your App Service Environment</span></span>
<span data-ttu-id="55901-115">een App-serviceomgeving tooconfigure te verwijzen[onze documentatie](app-service-web-how-to-create-an-app-service-environment.md) op Hallo onderwerp.</span><span class="sxs-lookup"><span data-stu-id="55901-115">tooconfigure an App Service Environment refer too[our documentation](app-service-web-how-to-create-an-app-service-environment.md) on hello subject.</span></span> <span data-ttu-id="55901-116">Zodra u een App-serviceomgeving is gemaakt hebt, kunt u [Web-Apps](app-service-web-overview.md), [API Apps](../app-service-api/app-service-api-apps-why-best-platform.md) en [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) in deze omgeving die al worden beveiligd achter Hallo WAF we in de volgende sectie Hallo configureren.</span><span class="sxs-lookup"><span data-stu-id="55901-116">Once you have an App Service Environment created, you can create [Web Apps](app-service-web-overview.md), [API Apps](../app-service-api/app-service-api-apps-why-best-platform.md) and [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) in this environment that will all be protected behind hello WAF we configure in hello next section.</span></span>

## <a name="configuring-your-barracuda-waf-cloud-service"></a><span data-ttu-id="55901-117">Uw Barracuda WAF Cloud Service configureren</span><span class="sxs-lookup"><span data-stu-id="55901-117">Configuring your Barracuda WAF Cloud Service</span></span>
<span data-ttu-id="55901-118">Barracuda heeft een [gedetailleerde artikel](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) over het implementeren van de WAF op een virtuele machine in Azure.</span><span class="sxs-lookup"><span data-stu-id="55901-118">Barracuda has a [detailed article](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) on deploying its WAF on a virtual machine in Azure.</span></span> <span data-ttu-id="55901-119">Maar omdat we redundantie wilt en geen een potentieel risico introduceren, u ten minste 2 toodeploy WAF exemplaar virtuele machines in Hallo dezelfde Cloud-Service wanneer deze instructies te volgen.</span><span class="sxs-lookup"><span data-stu-id="55901-119">But because we want redundancy and not introduce a single point of failure, you want toodeploy at least 2 WAF instance VMs into hello same Cloud Service when following these instructions.</span></span>

### <a name="adding-endpoints-toocloud-service"></a><span data-ttu-id="55901-120">Toevoegen van eindpunten tooCloud Service</span><span class="sxs-lookup"><span data-stu-id="55901-120">Adding Endpoints tooCloud Service</span></span>
<span data-ttu-id="55901-121">Nadat u 2 hebt of meer WAF VM-in uw Cloud-Service exemplaren kunt u Hallo [Azure-portal](https://portal.azure.com/) tooadd HTTP en HTTPS-eindpunten die worden gebruikt door uw toepassing, zoals wordt weergegeven in onderstaande afbeelding voor Hallo.</span><span class="sxs-lookup"><span data-stu-id="55901-121">Once you have 2 or more WAF VM instances in your Cloud Service you can use hello [Azure portal](https://portal.azure.com/) tooadd HTTP and HTTPS endpoints that are used by your application as shown in hello image below.</span></span>

![-Eindpunt configureren][ConfigureEndpoint]

<span data-ttu-id="55901-123">Als uw toepassingen met andere eindpunten, moet u ervoor dat tooadd die toothis lijst met.</span><span class="sxs-lookup"><span data-stu-id="55901-123">If your applications use other endpoints, make sure tooadd those toothis list as well.</span></span> 

### <a name="configuring-barracuda-waf-through-its-management-portal"></a><span data-ttu-id="55901-124">Barracuda WAF via de beheerportal configureren</span><span class="sxs-lookup"><span data-stu-id="55901-124">Configuring Barracuda WAF through its Management Portal</span></span>
<span data-ttu-id="55901-125">Barracuda WAF maakt gebruik van TCP-poort 8000 voor configuratie via de beheerportal.</span><span class="sxs-lookup"><span data-stu-id="55901-125">Barracuda WAF uses TCP Port 8000 for configuration through its management portal.</span></span> <span data-ttu-id="55901-126">Omdat er meerdere exemplaren van virtuele machines Hallo-WAF moet u hier toorepeat Hallo stappen voor elke VM-instantie.</span><span class="sxs-lookup"><span data-stu-id="55901-126">Since we have multiple instances of hello WAF VMs you will need toorepeat hello steps here for each VM instance.</span></span> 

> <span data-ttu-id="55901-127">Opmerking: Wanneer u klaar bent met WAF configuratie verwijderd Hallo TCP/8000 endpoint van alle virtuele machines WAF-tookeep uw beveiligde WAF.</span><span class="sxs-lookup"><span data-stu-id="55901-127">Note: Once you are done with WAF configuration, remove hello TCP/8000 endpoint from all your WAF VMs tookeep your WAF secure.</span></span>
> 
> 

<span data-ttu-id="55901-128">Hallo management eindpunt zoals weergegeven in de afbeelding hieronder tooconfigure Hallo uw Barracuda WAF toevoegen.</span><span class="sxs-lookup"><span data-stu-id="55901-128">Add hello management endpoint as shown in hello image below tooconfigure your Barracuda WAF.</span></span>

![Management-eindpunt toevoegen][AddManagementEndpoint]

<span data-ttu-id="55901-130">Gebruik een browser toobrowse toohello management-eindpunt op uw Cloud-Service.</span><span class="sxs-lookup"><span data-stu-id="55901-130">Use a browser toobrowse toohello management endpoint on your Cloud Service.</span></span> <span data-ttu-id="55901-131">Als uw Cloudservice test.cloudapp.net aangeroepen wordt, zou u dit eindpunt openen door te bladeren toohttp://test.cloudapp.net:8000.</span><span class="sxs-lookup"><span data-stu-id="55901-131">If your Cloud Service is called test.cloudapp.net, you would access this endpoint by browsing toohttp://test.cloudapp.net:8000.</span></span> <span data-ttu-id="55901-132">U ziet een aanmeldingspagina zoals hieronder dat u zich kunt aanmelden met referenties die u hebt opgegeven in VM-installatiefase Hallo WAF.</span><span class="sxs-lookup"><span data-stu-id="55901-132">You should see a login page like below that you can login using credentials you specified in hello WAF VM setup phase.</span></span>

![Aanmeldingspagina voor beheer][ManagementLoginPage]

<span data-ttu-id="55901-134">Eenmaal u aanmelding ziet u een dashboard als Hallo in de afbeelding hieronder die Hallo biedt elementaire statistieken over Hallo WAF beveiliging.</span><span class="sxs-lookup"><span data-stu-id="55901-134">Once you login you should see a dashboard as hello one in hello image below that will present basic statistics about hello WAF protection.</span></span>

![Management Dashboard][ManagementDashboard]

<span data-ttu-id="55901-136">Te klikken op het tabblad Hallo-Services kunt u uw WAF voor services die deze beveiligt configureren.</span><span class="sxs-lookup"><span data-stu-id="55901-136">Clicking on hello Services tab will let you configure your WAF for services it is protecting.</span></span> <span data-ttu-id="55901-137">U kunt raadplegen voor meer informatie over het configureren van uw WAF Barracuda [hun documentatie](https://techlib.barracuda.com/waf/getstarted1).</span><span class="sxs-lookup"><span data-stu-id="55901-137">For more details on configuring your Barracuda WAF you can consult [their documentation](https://techlib.barracuda.com/waf/getstarted1).</span></span> <span data-ttu-id="55901-138">In voorbeeld Hallo hieronder een Azure-Web-App is voor verkeer op HTTP- en HTTPS geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="55901-138">In hello example below an Azure Web App serving traffic on HTTP and HTTPS has been configured.</span></span>

![Management-Services toevoegen][ManagementAddServices]

> <span data-ttu-id="55901-140">Opmerking: Afhankelijk van hoe uw toepassingen worden geconfigureerd en welke functies worden gebruikt in uw App Service-omgeving, moet u tooforward verkeer voor TCP-poorten dan 80 en 443, bijvoorbeeld als u setup voor IP-SSL voor een Web-App.</span><span class="sxs-lookup"><span data-stu-id="55901-140">Note: Depending on how your applications are configured and what features are being used in your App Service Environment, you will need tooforward traffic for TCP ports other than 80 and 443, e.g. if you have IP SSL setup for a Web App.</span></span> <span data-ttu-id="55901-141">Voor een lijst met netwerkpoorten die in App Service-omgevingen worden gebruikt, raadpleegt u te[inkomend verkeer voor beheer-documentatie](app-service-app-service-environment-control-inbound-traffic.md) netwerkpoorten sectie.</span><span class="sxs-lookup"><span data-stu-id="55901-141">For a list of network ports used in App Service Environments, please refer too[Control Inbound Traffic documentation's](app-service-app-service-environment-control-inbound-traffic.md) Network Ports section.</span></span>
> 
> 

## <a name="configuring-microsoft-azure-traffic-manager-optional"></a><span data-ttu-id="55901-142">Configureren van Microsoft Azure Traffic Manager (optioneel)</span><span class="sxs-lookup"><span data-stu-id="55901-142">Configuring Microsoft Azure Traffic Manager (OPTIONAL)</span></span>
<span data-ttu-id="55901-143">Als uw toepassing beschikbaar in meerdere regio's is, moet u tooload saldo zou willen ze achter [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="55901-143">If your application is available in multiple regions, then you would want tooload balance them behind [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md).</span></span> <span data-ttu-id="55901-144">toodo zodat u een eindpunt in Hallo toevoegen kunt [klassieke Azure-portal](https://manage.azure.com) Hallo Cloud Service-naam voor uw WAF in Hallo Traffic Manager-profiel gebruiken, zoals in Hallo in onderstaande afbeelding.</span><span class="sxs-lookup"><span data-stu-id="55901-144">toodo so you can add an endpoint in hello [Azure classic portal](https://manage.azure.com) using hello Cloud Service name for your WAF in hello Traffic Manager profile as shown in hello image below.</span></span> 

![Traffic Manager-eindpunt][TrafficManagerEndpoint]

<span data-ttu-id="55901-146">Als uw toepassing verificatie vereist, zorg ervoor dat u hebt een resource die geen verificatie voor het Traffic Manager tooping voor beschikbaarheid van uw toepassing hello vereist.</span><span class="sxs-lookup"><span data-stu-id="55901-146">If your application requires authentication, ensure you have some resource that doesn't require any authentication for Traffic Manager tooping for hello availability of your application.</span></span> <span data-ttu-id="55901-147">U kunt URL onder sectie configureren Hallo Hallo configureren op Hallo [klassieke Azure-portal](https://manage.azure.com) zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="55901-147">You can configure hello URL under hello Configure section on hello [Azure classic portal](https://manage.azure.com) as shown below.</span></span>

![Traffic Manager configureren][ConfigureTrafficManager]

<span data-ttu-id="55901-149">tooforward hello Traffic Manager-pings van uw WAF tooyour toepassing, moet u vertalingen toosetup Website op uw Barracuda WAF tooforward verkeer tooyour toepassing zoals weergegeven in Hallo voorbeeld hieronder.</span><span class="sxs-lookup"><span data-stu-id="55901-149">tooforward hello Traffic Manager pings from your WAF tooyour application, you need toosetup Website Translations on your Barracuda WAF tooforward traffic tooyour application as shown in hello example below.</span></span>

![Vertalingen van de website][WebsiteTranslations]

## <a name="securing-traffic-tooapp-service-environment-using-network-security-groups-nsg"></a><span data-ttu-id="55901-151">Beveiliging van verkeer tooApp Service omgeving met behulp van Netwerkbeveiligingsgroep groepen (NSG)</span><span class="sxs-lookup"><span data-stu-id="55901-151">Securing Traffic tooApp Service Environment Using Network Security Groups (NSG)</span></span>
<span data-ttu-id="55901-152">Ga als volgt Hallo [besturingselement binnenkomend verkeer documentatie](app-service-app-service-environment-control-inbound-traffic.md) voor meer informatie over het beperken van verkeer tooyour App Service-omgeving van Hallo WAF alleen met behulp van Hallo VIP-adres van uw Cloud-Service.</span><span class="sxs-lookup"><span data-stu-id="55901-152">Follow hello [Control Inbound Traffic documentation](app-service-app-service-environment-control-inbound-traffic.md) for details on restricting traffic tooyour App Service Environment from hello WAF only by using hello VIP address of your Cloud Service.</span></span> <span data-ttu-id="55901-153">Hier volgt een voorbeeld-Powershell-opdracht voor het uitvoeren van deze taak voor TCP-poort 80.</span><span class="sxs-lookup"><span data-stu-id="55901-153">Here's a sample Powershell command for performing this task for TCP port 80.</span></span>

    Get-AzureNetworkSecurityGroup -Name "RestrictWestUSAppAccess" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP Barracuda" -Type Inbound -Priority 201 -Action Allow -SourceAddressPrefix '191.0.0.1'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP

<span data-ttu-id="55901-154">Hallo SourceAddressPrefix vervangen door Hallo virtueel IP-adres (VIP) van uw WAF-Cloudservice.</span><span class="sxs-lookup"><span data-stu-id="55901-154">Replace hello SourceAddressPrefix with hello Virtual IP Address (VIP) of your WAF's Cloud Service.</span></span>

> <span data-ttu-id="55901-155">Opmerking: Hallo VIP van uw Cloud-Service wordt gewijzigd wanneer u verwijderen en opnieuw Hallo Service in de Cloud maken.</span><span class="sxs-lookup"><span data-stu-id="55901-155">Note: hello VIP of your Cloud Service will change when you delete and re-create hello Cloud Service.</span></span> <span data-ttu-id="55901-156">Zorg ervoor dat tooupdate Hallo IP-adres in Hallo netwerk resourcegroep zodra u doet dit.</span><span class="sxs-lookup"><span data-stu-id="55901-156">Make sure tooupdate hello IP address in hello Network Resource group once you do so.</span></span> 
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
