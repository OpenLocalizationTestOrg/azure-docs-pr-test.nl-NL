---
title: aaaApplication Gateway integratie met Azure Security Center | Microsoft Docs
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
ms.openlocfilehash: 6f6ace105e84c01f525ab02938e81ce040c5c9d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-integration-between-application-gateway-and-azure-security-center"></a><span data-ttu-id="1f457-103">Overzicht van de integratie tussen Application Gateway en Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="1f457-103">Overview of integration between Application Gateway and Azure Security Center</span></span>

<span data-ttu-id="1f457-104">Meer informatie over hoe Application Gateway en Security Center beter beveiligen van uw webtoepassingsbronnen.</span><span class="sxs-lookup"><span data-stu-id="1f457-104">Learn how Application Gateway and Security Center help protect your web application resources.</span></span> <span data-ttu-id="1f457-105">Application gateway web application firewall (WAF) kan worden geïntegreerd met [Security Center](../security-center/security-center-intro.md) tooprovide een tooprevent naadloze weergave detecteren en reageren toothreats toounprotected webtoepassingen in uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="1f457-105">Application gateway web application firewall (WAF) integrates with [Security Center](../security-center/security-center-intro.md) tooprovide a seamless view tooprevent, detect and respond toothreats toounprotected web applications in your environment.</span></span>

## <a name="overview"></a><span data-ttu-id="1f457-106">Overzicht</span><span class="sxs-lookup"><span data-stu-id="1f457-106">Overview</span></span>

<span data-ttu-id="1f457-107">Application Gateway WAF wordt aanbevolen in Security Center voor het beveiligen van webtoepassingen van aanvallen en beveiligingsproblemen.</span><span class="sxs-lookup"><span data-stu-id="1f457-107">Application Gateway WAF is a recommendation in Security Center for protecting web applications from exploits and vulnerabilities.</span></span> <span data-ttu-id="1f457-108">Ingeschakeld webbronnen die niet zijn beveiligd door WAF weergegeven in het Beveiligingscentrum Hallo als hoog dreigingsniveau aanbevelingen.</span><span class="sxs-lookup"><span data-stu-id="1f457-108">Web enabled resources that are not protected by WAF show in hello security center as high severity recommendations.</span></span> <span data-ttu-id="1f457-109">Aanbevelingen voor web application firewalls worden weergegeven op Hallo **overzicht** pagina onder **toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1f457-109">Recommendations for web application firewalls are shown on hello **Overview** page, under **Applications**.</span></span>

![integratie met security center][1]

<span data-ttu-id="1f457-111">Geen aanbevelingen met betrekking tot de web application firewall op, wordt een nieuwe blade met details op Hallo van Hallo aanbeveling geopend.</span><span class="sxs-lookup"><span data-stu-id="1f457-111">Clicking any recommendations regarding web application firewall opens a new blade showing hello details of hello recommendation.</span></span>

## <a name="add-a-web-application-firewall-tooan-existing-resource"></a><span data-ttu-id="1f457-112">Een web application firewall tooan bestaande resource toevoegen</span><span class="sxs-lookup"><span data-stu-id="1f457-112">Add a web application firewall tooan existing resource</span></span>

<span data-ttu-id="1f457-113">Navigeer te**meer Services** > **beveiliging en identiteit** > **Security Center** en op Hallo **Security Center - overzicht**  blade, klikt u op **toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1f457-113">Navigate too**More Services** > **Security + Identity** > **Security Center** and on hello **Security Center - Overview** blade, click **Applications**.</span></span> <span data-ttu-id="1f457-114">Op Hallo **Security Center - toepassingen** blade Hallo tabel bevat een lijst met toepassingen die Security Center gedetecteerd in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="1f457-114">On hello **Security Center - Applications** blade, hello table contains a list of applications that Security Center detected in your subscription.</span></span>

![webtoepassingen][3]

<span data-ttu-id="1f457-116">Door te klikken op een webtoepassing met een kritiek probleem, u Hallo **beveiligingsstatus van de toepassing** blade.</span><span class="sxs-lookup"><span data-stu-id="1f457-116">By clicking on a web application with a critical issue, you get hello **Application security health** blade.</span></span> <span data-ttu-id="1f457-117">Hallo-webtoepassing die niet wordt beveiligd door een web application firewall in Hallo afbeelding hieronder.</span><span class="sxs-lookup"><span data-stu-id="1f457-117">In hello image below, hello web application that is not protected by a web application firewall.</span></span> 

![webbronnen niet beveiligd][2]

<span data-ttu-id="1f457-119">Klik op **web application firewall toevoegen** onder **aanbevelingen** tooopen hello **Web Application Firewall toevoegen** blade.</span><span class="sxs-lookup"><span data-stu-id="1f457-119">Click **Add a web application firewall** under **Recommendations** tooopen hello **Add a Web Application Firewall** blade.</span></span>

<span data-ttu-id="1f457-120">Als u geen hebben van een bestaande toepassingsgateway of toocreate een nieuwe wilt, klikt u op **nieuw** en op Hallo **maken van een nieuwe Web Application Firewall** blade en klik op **Microsoft - Toepassingsgateway**.</span><span class="sxs-lookup"><span data-stu-id="1f457-120">If you do not have an existing Application Gateway, or want toocreate a new one, click **Create New** and on hello **Create a new Web Application Firewall** blade, and click **Microsoft - Application Gateway**.</span></span> <span data-ttu-id="1f457-121">Hiermee gaat u door Hallo stappen toocreate een toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="1f457-121">This takes you through hello steps toocreate an application gateway.</span></span> <span data-ttu-id="1f457-122">Uw webtoepassing is op dit punt wordt toegevoegd als een beveiligde bron, nu Security Center, houdt dat deze bron wordt beveiligd door een web application firewall.</span><span class="sxs-lookup"><span data-stu-id="1f457-122">At this point, your web application is added as a protected resource, Security Center now tracks that this resource is protected by a web application firewall.</span></span> <span data-ttu-id="1f457-123">Hiermee wordt het niet als een lid van de groep back-end toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="1f457-123">This does not add it as a backend pool member.</span></span>

<span data-ttu-id="1f457-124">Als u een bestaande toepassingsgateway hebt, kunt u deze onder **bestaande oplossing gebruiken**</span><span class="sxs-lookup"><span data-stu-id="1f457-124">If you have an existing application gateway, you can choose it under **Use existing solution**</span></span>

![blade Web application firewall toevoegen][4]

<span data-ttu-id="1f457-126">Toevoegen van dat een toepassingsgateway web application tooan door Security Center voegt geen Hallo resource als lid van de groep back-end, moet u dit doen op Hallo toepassingsgatewayresource rechtstreeks.</span><span class="sxs-lookup"><span data-stu-id="1f457-126">Adding a web application tooan application gateway through Security Center does not add hello resource as a backend pool member, this must be done on hello application gateway resource directly.</span></span>

## <a name="add-a-resource-tooan-existing-web-application-firewall"></a><span data-ttu-id="1f457-127">Een resource tooan bestaande web application firewall toevoegen</span><span class="sxs-lookup"><span data-stu-id="1f457-127">Add a resource tooan existing web application firewall</span></span>

<span data-ttu-id="1f457-128">Navigeer te**meer Services** > **beveiliging en identiteit** > **Security Center** en op Hallo **Security Center - overzicht**  blade, klikt u op **partneroplossingen**.</span><span class="sxs-lookup"><span data-stu-id="1f457-128">Navigate too**More Services** > **Security + Identity** > **Security Center** and on hello **Security Center - Overview** blade, click **Partner solutions**.</span></span> <span data-ttu-id="1f457-129">Bestaande Security Center op de hoogte Toepassingsgateways weergeven in Hallo **partneroplossingen** blade.</span><span class="sxs-lookup"><span data-stu-id="1f457-129">Existing Security Center aware application gateways show in hello **Partner Solutions** blade.</span></span>

![partneroplossingen][7]

<span data-ttu-id="1f457-131">Klik op **app koppelen** tooopen hello **toepassingen koppelen** blade Hier krijgt u Hallo opties tooselect bestaande toepassingen.</span><span class="sxs-lookup"><span data-stu-id="1f457-131">Click **Link app** tooopen hello **Link Applications** blade, here you are given hello options tooselect existing applications.</span></span> <span data-ttu-id="1f457-132">Kies Hallo toepassingen tooprotect en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="1f457-132">Choose hello applications tooprotect and click **OK**.</span></span> <span data-ttu-id="1f457-133">Hiermee voegt geen Hallo web application toohello back-endpool van de toepassingsgateway Hallo.</span><span class="sxs-lookup"><span data-stu-id="1f457-133">This does not add hello web application toohello backend pool of hello application gateway.</span></span> <span data-ttu-id="1f457-134">Hiermee stelt u Hallo resources als een beveiligde bron zodat Security Center kunnen worden bijgehouden.</span><span class="sxs-lookup"><span data-stu-id="1f457-134">This sets hello resources as a protected resource so Security Center can track it.</span></span> <span data-ttu-id="1f457-135">tooadd hello resource als lid van de groep back-end, moet u dit doen in de toepassingsgateway hello, huidige Hallo-blade kunt u op **oplossingenconsole** toobe genomen toohello toepassingsgatewayresource waarin u web Hallo kunt toevoegen toepassingsgroep toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="1f457-135">tooadd hello resource as a backend pool member, this must be done on hello application gateway, from hello current blade you can click **Solution console** toobe taken toohello application gateway resource where you can add hello web application toohello backend pool.</span></span>

![toepassingen van partners oplossingen][6]

## <a name="finalize-configuration"></a><span data-ttu-id="1f457-137">Configuratie voltooien</span><span class="sxs-lookup"><span data-stu-id="1f457-137">Finalize configuration</span></span>

<span data-ttu-id="1f457-138">Toepassingsgateway tooan Security Center houdt toepassingen toegevoegd als een beveiligde bron.</span><span class="sxs-lookup"><span data-stu-id="1f457-138">Security Center tracks applications added tooan application gateway as a protected resource.</span></span>  <span data-ttu-id="1f457-139">Hallo-status van deze bron wordt gecontroleerd en zorgt ervoor dat deze wordt beveiligd door een toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="1f457-139">It monitors hello health of this resource and ensures that it is protected by an application gateway.</span></span> <span data-ttu-id="1f457-140">de volgende stap Hallo is tooadd Hallo privé-IP, openbare IP-adres of NIC van uw virtuele machine toohello back-endpool van de toepassingsgateway Hallo.</span><span class="sxs-lookup"><span data-stu-id="1f457-140">hello next step is tooadd hello private IP, public IP, or NIC of your virtual machine toohello backend pool of hello application gateway.</span></span> <span data-ttu-id="1f457-141">Totdat een extra aanbeveling van dit is **Toepassingsbeveiliging voltooien** wordt weergegeven totdat Hallo resource is toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="1f457-141">Until this is done an additional recommendation of **Finalize application protection** is shown until hello resource is added.</span></span>

![blade Web application firewall toevoegen][5]

## <a name="security-alerts"></a><span data-ttu-id="1f457-143">Beveiligingswaarschuwingen</span><span class="sxs-lookup"><span data-stu-id="1f457-143">Security Alerts</span></span>

<span data-ttu-id="1f457-144">In Security Center te navigeren**detectie** > **beveiligingswaarschuwingen**.</span><span class="sxs-lookup"><span data-stu-id="1f457-144">Within Security Center navigate too**DETECTION** > **Security Alerts**.</span></span>  <span data-ttu-id="1f457-145">Hier vindt u WAF waarschuwingen voor uw Toepassingsgateways.</span><span class="sxs-lookup"><span data-stu-id="1f457-145">Here you find WAF alerts for your application gateways.</span></span> <span data-ttu-id="1f457-146">Waarschuwingen worden opgesplitst op WAF regel.</span><span class="sxs-lookup"><span data-stu-id="1f457-146">Alerts are broken down by WAF rule.</span></span>

![beveiligingswaarschuwingen][8]

<span data-ttu-id="1f457-148">Te klikken op een regel om een lijst met waarschuwingen voor die specifieke WAF regel te bieden.</span><span class="sxs-lookup"><span data-stu-id="1f457-148">Clicking an rule will provide a list of alerts for that specific WAF rule.</span></span> <span data-ttu-id="1f457-149">Elke waarschuwing bevat aanvullende informatie op Hallo kan vinden.</span><span class="sxs-lookup"><span data-stu-id="1f457-149">Each alert shows additional details on hello finding.</span></span> <span data-ttu-id="1f457-150">Hallo details bevatten een koppeling toohello application gateway.</span><span class="sxs-lookup"><span data-stu-id="1f457-150">hello details provide a link toohello application gateway.</span></span>
 
![Waarschuwingsdetails][9]

## <a name="next-steps"></a><span data-ttu-id="1f457-152">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1f457-152">Next steps</span></span>

<span data-ttu-id="1f457-153">hoe tooenable web application firewall op een bestaande toepassingsgateway gaat u naar toolearn [maken of bijwerken van een Azure-toepassingsgateway met web application firewall](application-gateway-web-application-firewall-portal.md#add-web-application-firewall-to-an-existing-application-gateway)</span><span class="sxs-lookup"><span data-stu-id="1f457-153">toolearn how tooenable web application firewall on an existing application gateway, visit [Create or update an Azure Application Gateway with web application firewall](application-gateway-web-application-firewall-portal.md#add-web-application-firewall-to-an-existing-application-gateway)</span></span>

[1]: ./media/application-gateway-integration-security-center/figure1.png
[2]: ./media/application-gateway-integration-security-center/figure2.png
[3]: ./media/application-gateway-integration-security-center/figure3.png
[4]: ./media/application-gateway-integration-security-center/figure4.png
[5]: ./media/application-gateway-integration-security-center/figure5.png
[6]: ./media/application-gateway-integration-security-center/figure6.png
[7]: ./media/application-gateway-integration-security-center/figure7.png
[8]: ./media/application-gateway-integration-security-center/securitycenter.png
[9]: ./media/application-gateway-integration-security-center/figure9.png