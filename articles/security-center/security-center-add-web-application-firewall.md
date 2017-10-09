---
title: aaaAdd web application firewall in Azure Security Center | Microsoft Docs
description: Dit document leest u hoe tooimplement hello Azure Security Center aanbevelingen ** toevoegen van een web application firewall ** en ** voltooien toepassing beveiliging **.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 8f56139a-4466-48ac-90fb-86d002cf8242
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: terrylan
ms.openlocfilehash: bff0aa2a5c6e0dde23396f93de52abe295053581
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-web-application-firewall-in-azure-security-center"></a><span data-ttu-id="f3595-103">Web application firewall toevoegen in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="f3595-103">Add a web application firewall in Azure Security Center</span></span>
<span data-ttu-id="f3595-104">Azure Security Center kan aanbevelen dat u, web application firewall (WAF) van een Microsoft-partner toosecure uw webtoepassingen toevoegt.</span><span class="sxs-lookup"><span data-stu-id="f3595-104">Azure Security Center may recommend that you add a web application firewall (WAF) from a Microsoft partner toosecure your web applications.</span></span> <span data-ttu-id="f3595-105">Dit document vindt u via een voorbeeld van hoe tooapply deze aanbeveling.</span><span class="sxs-lookup"><span data-stu-id="f3595-105">This document walks you through an example of how tooapply this recommendation.</span></span>

<span data-ttu-id="f3595-106">Een WAF aanbeveling wordt voor een openbare internetgerichte IP (exemplaar niveau IP- of Load Balanced IP) met een gekoppelde netwerkbeveiligingsgroep met poorten voor inkomend web openen (80,443) weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f3595-106">A WAF recommendation is shown for any public facing IP (either Instance Level IP or Load Balanced IP) that has an associated network security group with open inbound web ports (80,443).</span></span>

<span data-ttu-id="f3595-107">Security Center raadt aan dat u een WAF toohelp inrichten bescherming tegen aanvallen die gericht is op uw webtoepassingen op virtuele machines en op App Service-omgeving.</span><span class="sxs-lookup"><span data-stu-id="f3595-107">Security Center recommends that you provision a WAF toohelp defend against attacks targeting your web applications on virtual machines and on App Service Environment.</span></span> <span data-ttu-id="f3595-108">Een as-omgeving (App Service omgeving) is een [Premium](https://azure.microsoft.com/pricing/details/app-service/) service-plan optie van Azure App Service die een volledig geïsoleerde en toegewezen omgeving biedt voor het veilig uitvoeren van Azure App Service-apps.</span><span class="sxs-lookup"><span data-stu-id="f3595-108">An App Service Environment (ASE) is a [Premium](https://azure.microsoft.com/pricing/details/app-service/) service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps.</span></span> <span data-ttu-id="f3595-109">toolearn meer informatie over het as-omgeving, Zie Hallo [documentatie van App Service-omgeving](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="f3595-109">toolearn more about ASE, see hello [App Service Environment Documentation](../app-service/app-service-app-service-environments-readme.md).</span></span>

> [!NOTE]
> <span data-ttu-id="f3595-110">Dit document bevat Hallo service met behulp van een voorbeeldimplementatie.</span><span class="sxs-lookup"><span data-stu-id="f3595-110">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="f3595-111">Dit document is niet een stapsgewijze handleiding.</span><span class="sxs-lookup"><span data-stu-id="f3595-111">This document is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="f3595-112">Hallo aanbeveling implementeren</span><span class="sxs-lookup"><span data-stu-id="f3595-112">Implement hello recommendation</span></span>
1. <span data-ttu-id="f3595-113">In Hallo **aanbevelingen** blade Selecteer **-webtoepassing met web application firewall Secure**.</span><span class="sxs-lookup"><span data-stu-id="f3595-113">In hello **Recommendations** blade, select **Secure web application using web application firewall**.</span></span>
   <span data-ttu-id="f3595-114">![Web Application beveiligen][1]</span><span class="sxs-lookup"><span data-stu-id="f3595-114">![Secure web Application][1]</span></span>
2. <span data-ttu-id="f3595-115">In Hallo **beveiligen van uw webtoepassingen met web application firewall** blade, selecteert u een webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="f3595-115">In hello **Secure your web applications using web application firewall** blade, select a web application.</span></span> <span data-ttu-id="f3595-116">Hallo **Web Application Firewall toevoegen** blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="f3595-116">hello **Add a Web Application Firewall** blade opens.</span></span>
   <span data-ttu-id="f3595-117">![Een firewall voor webtoepassingen toevoegen][2]</span><span class="sxs-lookup"><span data-stu-id="f3595-117">![Add a web application firewall][2]</span></span>
3. <span data-ttu-id="f3595-118">U kunt toouse een bestaande web application firewall indien beschikbaar of u kunt een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="f3595-118">You can choose toouse an existing web application firewall if available or you can create a new one.</span></span> <span data-ttu-id="f3595-119">In dit voorbeeld zijn er geen bestaande WAFs beschikbaar, dus we een WAF maken.</span><span class="sxs-lookup"><span data-stu-id="f3595-119">In this example, there are no existing WAFs available so we create a WAF.</span></span>
4. <span data-ttu-id="f3595-120">een WAF toocreate Selecteer een oplossing uit de lijst Hallo van geïntegreerde partners.</span><span class="sxs-lookup"><span data-stu-id="f3595-120">toocreate a WAF, select a solution from hello list of integrated partners.</span></span> <span data-ttu-id="f3595-121">In dit voorbeeld selecteren we **Barracuda Web Application Firewall**.</span><span class="sxs-lookup"><span data-stu-id="f3595-121">In this example, we select **Barracuda Web Application Firewall**.</span></span>
5. <span data-ttu-id="f3595-122">Hallo **Barracuda Web Application Firewall** blade wordt geopend zodat u informatie over Hallo partneroplossing.</span><span class="sxs-lookup"><span data-stu-id="f3595-122">hello **Barracuda Web Application Firewall** blade opens providing you information about hello partner solution.</span></span> <span data-ttu-id="f3595-123">Selecteer **maken** Hallo informatie blade.</span><span class="sxs-lookup"><span data-stu-id="f3595-123">Select **Create** in hello information blade.</span></span>

   ![Firewall-informatie-blade][3]

6. <span data-ttu-id="f3595-125">Hallo **nieuwe Web Application Firewall** blade wordt geopend, waar u kunt uitvoeren **VM-configuratie** stappen en geef **WAF informatie**.</span><span class="sxs-lookup"><span data-stu-id="f3595-125">hello **New Web Application Firewall** blade opens, where you can perform **VM Configuration** steps and provide **WAF Information**.</span></span> <span data-ttu-id="f3595-126">Selecteer **VM-configuratie**.</span><span class="sxs-lookup"><span data-stu-id="f3595-126">Select **VM Configuration**.</span></span>
7. <span data-ttu-id="f3595-127">In Hallo **VM-configuratie** blade, voert u gegevens vereist toospin Hallo virtuele machine die wordt uitgevoerd Hallo WAF.</span><span class="sxs-lookup"><span data-stu-id="f3595-127">In hello **VM Configuration** blade, you enter information required toospin up hello virtual machine that runs hello WAF.</span></span>
   <span data-ttu-id="f3595-128">![VM-configuratie][4]</span><span class="sxs-lookup"><span data-stu-id="f3595-128">![VM configuration][4]</span></span>
8. <span data-ttu-id="f3595-129">Retourneren van toohello **nieuwe Web Application Firewall** blade en selecteer **WAF informatie**.</span><span class="sxs-lookup"><span data-stu-id="f3595-129">Return toohello **New Web Application Firewall** blade and select **WAF Information**.</span></span> <span data-ttu-id="f3595-130">In Hallo **WAF informatie** blade u Hallo WAF zelf configureren.</span><span class="sxs-lookup"><span data-stu-id="f3595-130">In hello **WAF Information** blade, you configure hello WAF itself.</span></span> <span data-ttu-id="f3595-131">Stap 7 kunt u tooconfigure Hallo virtuele machine op welke Hallo WAF wordt uitgevoerd en stap 8 kunt u tooprovision hello WAF zelf.</span><span class="sxs-lookup"><span data-stu-id="f3595-131">Step 7 allows you tooconfigure hello virtual machine on which hello WAF runs and step 8 enables you tooprovision hello WAF itself.</span></span>

## <a name="finalize-application-protection"></a><span data-ttu-id="f3595-132">Toepassingsbeveiliging voltooien</span><span class="sxs-lookup"><span data-stu-id="f3595-132">Finalize application protection</span></span>
1. <span data-ttu-id="f3595-133">Retourneren van toohello **aanbevelingen** blade.</span><span class="sxs-lookup"><span data-stu-id="f3595-133">Return toohello **Recommendations** blade.</span></span> <span data-ttu-id="f3595-134">Een nieuwe vermelding is gegenereerd nadat u hebt gemaakt Hallo WAF, aangeroepen **Toepassingsbeveiliging voltooien**.</span><span class="sxs-lookup"><span data-stu-id="f3595-134">A new entry was generated after you created hello WAF, called **Finalize application protection**.</span></span> <span data-ttu-id="f3595-135">Deze vermelding laat u weten dat u nodig hebt toocomplete Hallo proces daadwerkelijk voorbereiden Hallo WAF binnen hello Azure Virtual Network zodat het Hallo-toepassing kunt beveiligen.</span><span class="sxs-lookup"><span data-stu-id="f3595-135">This entry lets you know that you need toocomplete hello process of actually wiring up hello WAF within hello Azure Virtual Network so that it can protect hello application.</span></span>

   ![Toepassingsbeveiliging voltooien][5]

2. <span data-ttu-id="f3595-137">Selecteer **Toepassingsbeveiliging voltooien**.</span><span class="sxs-lookup"><span data-stu-id="f3595-137">Select **Finalize application protection**.</span></span> <span data-ttu-id="f3595-138">Er wordt een nieuwe blade geopend.</span><span class="sxs-lookup"><span data-stu-id="f3595-138">A new blade opens.</span></span> <span data-ttu-id="f3595-139">U ziet dat er een webtoepassing die toohave de verkeer gerouteerd moet.</span><span class="sxs-lookup"><span data-stu-id="f3595-139">You can see that there is a web application that needs toohave its traffic rerouted.</span></span>
3. <span data-ttu-id="f3595-140">Selecteer Hallo-webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="f3595-140">Select hello web application.</span></span> <span data-ttu-id="f3595-141">Er wordt een blade geopend waarmee u stappen voor het Hallo web application firewall setup te voltooien.</span><span class="sxs-lookup"><span data-stu-id="f3595-141">A blade opens that gives you steps for finalizing hello web application firewall setup.</span></span> <span data-ttu-id="f3595-142">Hallo stappen hebt uitgevoerd en selecteer vervolgens **verkeer te beperken**.</span><span class="sxs-lookup"><span data-stu-id="f3595-142">Complete hello steps, and then select **Restrict traffic**.</span></span> <span data-ttu-id="f3595-143">Security Center vervolgens Hallo bedrading-up voor u.</span><span class="sxs-lookup"><span data-stu-id="f3595-143">Security Center then does hello wiring-up for you.</span></span>

   ![Verkeer te beperken][6]

> [!NOTE]
> <span data-ttu-id="f3595-145">U kunt meerdere webtoepassingen in Security Center beveiligen door deze toepassingen tooyour bestaande WAF implementaties toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="f3595-145">You can protect multiple web applications in Security Center by adding these applications tooyour existing WAF deployments.</span></span>
>
>

<span data-ttu-id="f3595-146">Hallo-logboeken van die WAF zijn nu volledig geïntegreerd.</span><span class="sxs-lookup"><span data-stu-id="f3595-146">hello logs from that WAF are now fully integrated.</span></span> <span data-ttu-id="f3595-147">Security Center kunt starten automatisch verzamelen en analyseren van Hallo Logboeken zodat deze kan belangrijke waarschuwingen tooyou surface.</span><span class="sxs-lookup"><span data-stu-id="f3595-147">Security Center can start automatically gathering and analyzing hello logs so that it can surface important security alerts tooyou.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f3595-148">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f3595-148">Next steps</span></span>
<span data-ttu-id="f3595-149">Dit document hebt u geleerd hoe tooimplement Hallo Security Center aanbeveling "Een webtoepassing toevoegen".</span><span class="sxs-lookup"><span data-stu-id="f3595-149">This document showed you how tooimplement hello Security Center recommendation "Add a web application."</span></span> <span data-ttu-id="f3595-150">toolearn meer informatie over het configureren van een web application firewall Hallo ziet:</span><span class="sxs-lookup"><span data-stu-id="f3595-150">toolearn more about configuring a web application firewall, see hello following:</span></span>

* [<span data-ttu-id="f3595-151">Web Application Firewall (WAF) configureren voor App Service-omgeving</span><span class="sxs-lookup"><span data-stu-id="f3595-151">Configuring a Web Application Firewall (WAF) for App Service Environment</span></span>](../app-service-web/app-service-app-service-environment-web-application-firewall.md)

<span data-ttu-id="f3595-152">toolearn meer informatie over Security Center Hallo ziet:</span><span class="sxs-lookup"><span data-stu-id="f3595-152">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="f3595-153">[Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md) --meer informatie over hoe tooconfigure beveiligingsbeleid voor uw Azure-abonnementen en resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="f3595-153">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="f3595-154">[Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md) --meer informatie over hoe toomonitor Hallo status van uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="f3595-154">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="f3595-155">[Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md) --meer informatie over hoe toomanage en gereageerd had toosecurity waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="f3595-155">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="f3595-156">[Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md) --Leer hoe aanbevelingen u uw Azure-resources te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="f3595-156">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="f3595-157">[Veelgestelde vragen over Azure Security Center](security-center-faq.md) --Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="f3595-157">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="f3595-158">[Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/) --Lees blogberichten over Azure-beveiliging en naleving.</span><span class="sxs-lookup"><span data-stu-id="f3595-158">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-add-web-application-firewall/secure-web-application.png
[2]:./media/security-center-add-web-application-firewall/add-a-waf.png
[3]: ./media/security-center-add-web-application-firewall/info-blade.png
[4]: ./media/security-center-add-web-application-firewall/select-vm-config.png
[5]: ./media/security-center-add-web-application-firewall/finalize-waf.png
[6]: ./media/security-center-add-web-application-firewall/restrict-traffic.png
