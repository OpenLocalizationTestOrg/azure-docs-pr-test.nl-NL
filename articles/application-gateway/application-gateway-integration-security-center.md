---
title: Gateway-integratie van toepassingen met Azure Security Center | Microsoft Docs
description: "Deze pagina bevat informatie over hoe Application Gateway is geïntegreerd in Azure Security Center."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: 
ms.assetid: e5ea5cf9-3b41-4b85-a12c-e758bff7f3ec
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: 
ms.workload: infrastructure-services
ms.date: 06/07/2017
ms.author: gwallace
ms.openlocfilehash: 737cdff3140be68cf9d6d396b470dd09c65c52f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="overview-of-integration-between-application-gateway-and-azure-security-center"></a><span data-ttu-id="181f6-103">Overzicht van de integratie tussen Application Gateway en Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="181f6-103">Overview of integration between Application Gateway and Azure Security Center</span></span>

<span data-ttu-id="181f6-104">Meer informatie over hoe Application Gateway en Security Center beter beveiligen van uw webtoepassingsbronnen.</span><span class="sxs-lookup"><span data-stu-id="181f6-104">Learn how Application Gateway and Security Center help protect your web application resources.</span></span> <span data-ttu-id="181f6-105">Application gateway web application firewall (WAF) kan worden geïntegreerd met [Security Center](../security-center/security-center-intro.md) voor een naadloze weergeven om te voorkomen, detecteren en reageren op bedreigingen voor de niet-beveiligde webtoepassingen in uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="181f6-105">Application gateway web application firewall (WAF) integrates with [Security Center](../security-center/security-center-intro.md) to provide a seamless view to prevent, detect and respond to threats to unprotected web applications in your environment.</span></span>

## <a name="overview"></a><span data-ttu-id="181f6-106">Overzicht</span><span class="sxs-lookup"><span data-stu-id="181f6-106">Overview</span></span>

<span data-ttu-id="181f6-107">Application Gateway WAF wordt aanbevolen in Security Center voor het beveiligen van webtoepassingen van aanvallen en beveiligingsproblemen.</span><span class="sxs-lookup"><span data-stu-id="181f6-107">Application Gateway WAF is a recommendation in Security Center for protecting web applications from exploits and vulnerabilities.</span></span> <span data-ttu-id="181f6-108">Ingeschakeld webbronnen die niet zijn beveiligd door WAF weergegeven in het Beveiligingscentrum als hoog dreigingsniveau aanbevelingen.</span><span class="sxs-lookup"><span data-stu-id="181f6-108">Web enabled resources that are not protected by WAF show in the security center as high severity recommendations.</span></span> <span data-ttu-id="181f6-109">Aanbevelingen voor web application firewalls worden weergegeven op de **overzicht** pagina onder **toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="181f6-109">Recommendations for web application firewalls are shown on the **Overview** page, under **Applications**.</span></span>

![integratie met security center][1]

<span data-ttu-id="181f6-111">Als u geen aanbevelingen over web application firewall Hiermee opent u een nieuwe blade worden de details van de aanbeveling op.</span><span class="sxs-lookup"><span data-stu-id="181f6-111">Clicking any recommendations regarding web application firewall opens a new blade showing the details of the recommendation.</span></span>

## <a name="add-a-web-application-firewall-to-an-existing-resource"></a><span data-ttu-id="181f6-112">Web application firewall toevoegen aan een bestaande resource</span><span class="sxs-lookup"><span data-stu-id="181f6-112">Add a web application firewall to an existing resource</span></span>

<span data-ttu-id="181f6-113">Navigeer naar **meer Services** > **beveiliging en identiteit** > **Security Center** en klik op de **Security Center - overzicht** blade, klikt u op **toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="181f6-113">Navigate to **More Services** > **Security + Identity** > **Security Center** and on the **Security Center - Overview** blade, click **Applications**.</span></span> <span data-ttu-id="181f6-114">Op de **Security Center - toepassingen** blade in de tabel bevat een lijst met toepassingen die Security Center gedetecteerd in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="181f6-114">On the **Security Center - Applications** blade, the table contains a list of applications that Security Center detected in your subscription.</span></span>

![webtoepassingen][3]

<span data-ttu-id="181f6-116">Door te klikken op een webtoepassing met een kritiek probleem, u krijgt de **beveiligingsstatus van de toepassing** blade.</span><span class="sxs-lookup"><span data-stu-id="181f6-116">By clicking on a web application with a critical issue, you get the **Application security health** blade.</span></span> <span data-ttu-id="181f6-117">In de onderstaande afbeelding, de webtoepassing die niet wordt beveiligd door een web application firewall.</span><span class="sxs-lookup"><span data-stu-id="181f6-117">In the image below, the web application that is not protected by a web application firewall.</span></span> 

![webbronnen niet beveiligd][2]

<span data-ttu-id="181f6-119">Klik op **web application firewall toevoegen** onder **aanbevelingen** openen de **Web Application Firewall toevoegen** blade.</span><span class="sxs-lookup"><span data-stu-id="181f6-119">Click **Add a web application firewall** under **Recommendations** to open the **Add a Web Application Firewall** blade.</span></span>

<span data-ttu-id="181f6-120">Als u geen hebben van een bestaande toepassingsgateway of wilt maken van een nieuwe, klikt u op **nieuw** en klik op de **maken van een nieuwe Web Application Firewall** blade en klik op **Microsoft - Application Gateway**.</span><span class="sxs-lookup"><span data-stu-id="181f6-120">If you do not have an existing Application Gateway, or want to create a new one, click **Create New** and on the **Create a new Web Application Firewall** blade, and click **Microsoft - Application Gateway**.</span></span> <span data-ttu-id="181f6-121">Hiermee gaat u door de stappen om een toepassingsgateway te maken.</span><span class="sxs-lookup"><span data-stu-id="181f6-121">This takes you through the steps to create an application gateway.</span></span> <span data-ttu-id="181f6-122">Uw webtoepassing is op dit punt wordt toegevoegd als een beveiligde bron, nu Security Center, houdt dat deze bron wordt beveiligd door een web application firewall.</span><span class="sxs-lookup"><span data-stu-id="181f6-122">At this point, your web application is added as a protected resource, Security Center now tracks that this resource is protected by a web application firewall.</span></span> <span data-ttu-id="181f6-123">Hiermee wordt het niet als een lid van de groep back-end toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="181f6-123">This does not add it as a backend pool member.</span></span>

<span data-ttu-id="181f6-124">Als u een bestaande toepassingsgateway hebt, kunt u deze onder **bestaande oplossing gebruiken**</span><span class="sxs-lookup"><span data-stu-id="181f6-124">If you have an existing application gateway, you can choose it under **Use existing solution**</span></span>

![blade Web application firewall toevoegen][4]

<span data-ttu-id="181f6-126">Toevoegen van dat een webtoepassing om een toepassingsgateway door Security Center te heeft de resource niet toevoegen als een lid van de groep back-end, moet u dit doen op de toepassingsgatewayresource rechtstreeks.</span><span class="sxs-lookup"><span data-stu-id="181f6-126">Adding a web application to an application gateway through Security Center does not add the resource as a backend pool member, this must be done on the application gateway resource directly.</span></span>

## <a name="add-a-resource-to-an-existing-web-application-firewall"></a><span data-ttu-id="181f6-127">Een resource toevoegen aan een bestaande web application firewall</span><span class="sxs-lookup"><span data-stu-id="181f6-127">Add a resource to an existing web application firewall</span></span>

<span data-ttu-id="181f6-128">Navigeer naar **meer Services** > **beveiliging en identiteit** > **Security Center** en klik op de **Security Center - overzicht** blade, klikt u op **partneroplossingen**.</span><span class="sxs-lookup"><span data-stu-id="181f6-128">Navigate to **More Services** > **Security + Identity** > **Security Center** and on the **Security Center - Overview** blade, click **Partner solutions**.</span></span> <span data-ttu-id="181f6-129">Bestaande Security Center op de hoogte Toepassingsgateways weergeven in de **partneroplossingen** blade.</span><span class="sxs-lookup"><span data-stu-id="181f6-129">Existing Security Center aware application gateways show in the **Partner Solutions** blade.</span></span>

![partneroplossingen][7]

<span data-ttu-id="181f6-131">Klik op **app koppelen** openen de **toepassingen koppelen** blade Hier krijgt u de opties voor het selecteren van bestaande toepassingen.</span><span class="sxs-lookup"><span data-stu-id="181f6-131">Click **Link app** to open the **Link Applications** blade, here you are given the options to select existing applications.</span></span> <span data-ttu-id="181f6-132">Kies de toepassingen te beschermen en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="181f6-132">Choose the applications to protect and click **OK**.</span></span> <span data-ttu-id="181f6-133">Hiermee wordt de webtoepassing naar de back-endpool van de toepassingsgateway niet toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="181f6-133">This does not add the web application to the backend pool of the application gateway.</span></span> <span data-ttu-id="181f6-134">Hiermee stelt u de resources als een beveiligde bron zodat Security Center kunnen worden bijgehouden.</span><span class="sxs-lookup"><span data-stu-id="181f6-134">This sets the resources as a protected resource so Security Center can track it.</span></span> <span data-ttu-id="181f6-135">Als u wilt de bron toevoegen als een lid van de groep back-end, moet u dit doen in de toepassingsgateway, uit de huidige blade kunt u **oplossingenconsole** om te worden uitgevoerd om de toepassingsgatewayresource waarin u de webtoepassing aan de endadresgroep back-kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="181f6-135">To add the resource as a backend pool member, this must be done on the application gateway, from the current blade you can click **Solution console** to be taken to the application gateway resource where you can add the web application to the backend pool.</span></span>

![toepassingen van partners oplossingen][6]

## <a name="finalize-configuration"></a><span data-ttu-id="181f6-137">Configuratie voltooien</span><span class="sxs-lookup"><span data-stu-id="181f6-137">Finalize configuration</span></span>

<span data-ttu-id="181f6-138">Security Center houdt toepassingen toegevoegd aan een application gateway als een beveiligde bron.</span><span class="sxs-lookup"><span data-stu-id="181f6-138">Security Center tracks applications added to an application gateway as a protected resource.</span></span>  <span data-ttu-id="181f6-139">Het controleert de status van deze resource en zorgt ervoor dat deze wordt beveiligd door een toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="181f6-139">It monitors the health of this resource and ensures that it is protected by an application gateway.</span></span> <span data-ttu-id="181f6-140">De volgende stap is het toevoegen van de privé-IP, openbare IP-adres of NIC van uw virtuele machine naar de back-endpool van de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="181f6-140">The next step is to add the private IP, public IP, or NIC of your virtual machine to the backend pool of the application gateway.</span></span> <span data-ttu-id="181f6-141">Totdat een extra aanbeveling van dit is **Toepassingsbeveiliging voltooien** wordt weergegeven totdat de bron is toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="181f6-141">Until this is done an additional recommendation of **Finalize application protection** is shown until the resource is added.</span></span>

![blade Web application firewall toevoegen][5]

## <a name="security-alerts"></a><span data-ttu-id="181f6-143">Beveiligingswaarschuwingen</span><span class="sxs-lookup"><span data-stu-id="181f6-143">Security Alerts</span></span>

<span data-ttu-id="181f6-144">In Security Center navigeren naar **detectie** > **beveiligingswaarschuwingen**.</span><span class="sxs-lookup"><span data-stu-id="181f6-144">Within Security Center navigate to **DETECTION** > **Security Alerts**.</span></span>  <span data-ttu-id="181f6-145">Hier vindt u WAF waarschuwingen voor uw Toepassingsgateways.</span><span class="sxs-lookup"><span data-stu-id="181f6-145">Here you find WAF alerts for your application gateways.</span></span> <span data-ttu-id="181f6-146">Waarschuwingen worden opgesplitst op WAF regel.</span><span class="sxs-lookup"><span data-stu-id="181f6-146">Alerts are broken down by WAF rule.</span></span>

![beveiligingswaarschuwingen][8]

<span data-ttu-id="181f6-148">Te klikken op een regel om een lijst met waarschuwingen voor die specifieke WAF regel te bieden.</span><span class="sxs-lookup"><span data-stu-id="181f6-148">Clicking an rule will provide a list of alerts for that specific WAF rule.</span></span> <span data-ttu-id="181f6-149">Elke waarschuwing worden aanvullende details over het zoeken.</span><span class="sxs-lookup"><span data-stu-id="181f6-149">Each alert shows additional details on the finding.</span></span> <span data-ttu-id="181f6-150">De gegevens bevatten een koppeling naar de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="181f6-150">The details provide a link to the application gateway.</span></span>
 
![Waarschuwingsdetails][9]

## <a name="next-steps"></a><span data-ttu-id="181f6-152">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="181f6-152">Next steps</span></span>

<span data-ttu-id="181f6-153">Als u wilt weten hoe web application firewall inschakelen in een bestaande toepassingsgateway, gaat u naar [maken of bijwerken van een Azure-toepassingsgateway met web application firewall](application-gateway-web-application-firewall-portal.md#add-web-application-firewall-to-an-existing-application-gateway)</span><span class="sxs-lookup"><span data-stu-id="181f6-153">To learn how to enable web application firewall on an existing application gateway, visit [Create or update an Azure Application Gateway with web application firewall](application-gateway-web-application-firewall-portal.md#add-web-application-firewall-to-an-existing-application-gateway)</span></span>

[1]: ./media/application-gateway-integration-security-center/figure1.png
[2]: ./media/application-gateway-integration-security-center/figure2.png
[3]: ./media/application-gateway-integration-security-center/figure3.png
[4]: ./media/application-gateway-integration-security-center/figure4.png
[5]: ./media/application-gateway-integration-security-center/figure5.png
[6]: ./media/application-gateway-integration-security-center/figure6.png
[7]: ./media/application-gateway-integration-security-center/figure7.png
[8]: ./media/application-gateway-integration-security-center/securitycenter.png
[9]: ./media/application-gateway-integration-security-center/figure9.png