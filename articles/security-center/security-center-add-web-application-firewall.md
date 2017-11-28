---
title: Web application firewall toevoegen in Azure Security Center | Microsoft Docs
description: Dit document ziet u hoe de Azure Security Center aanbevelingen implementeren ** toevoegen van een web application firewall ** en ** voltooien toepassing beveiliging **.
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
ms.openlocfilehash: d04a07237029953d8a9b20704d85e852ce45d867
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="add-a-web-application-firewall-in-azure-security-center"></a><span data-ttu-id="871d6-103">Web application firewall toevoegen in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="871d6-103">Add a web application firewall in Azure Security Center</span></span>
<span data-ttu-id="871d6-104">Azure Security Center kan aanbevelen web application firewall (WAF) toe te voegen uit een Microsoft-partner voor het beveiligen van uw webtoepassingen.</span><span class="sxs-lookup"><span data-stu-id="871d6-104">Azure Security Center may recommend that you add a web application firewall (WAF) from a Microsoft partner to secure your web applications.</span></span> <span data-ttu-id="871d6-105">Dit document vindt u via een voorbeeld van het toepassen van deze aanbeveling.</span><span class="sxs-lookup"><span data-stu-id="871d6-105">This document walks you through an example of how to apply this recommendation.</span></span>

<span data-ttu-id="871d6-106">Een WAF aanbeveling wordt voor een openbare internetgerichte IP (exemplaar niveau IP- of Load Balanced IP) met een gekoppelde netwerkbeveiligingsgroep met poorten voor inkomend web openen (80,443) weergegeven.</span><span class="sxs-lookup"><span data-stu-id="871d6-106">A WAF recommendation is shown for any public facing IP (either Instance Level IP or Load Balanced IP) that has an associated network security group with open inbound web ports (80,443).</span></span>

<span data-ttu-id="871d6-107">Security Center raadt aan dat u een WAF om te helpen beschermen tegen aanvallen die gericht is op uw webtoepassingen op virtuele machines en op App Service-omgeving inrichten.</span><span class="sxs-lookup"><span data-stu-id="871d6-107">Security Center recommends that you provision a WAF to help defend against attacks targeting your web applications on virtual machines and on App Service Environment.</span></span> <span data-ttu-id="871d6-108">Een as-omgeving (App Service omgeving) is een [Premium](https://azure.microsoft.com/pricing/details/app-service/) service-plan optie van Azure App Service die een volledig geïsoleerde en toegewezen omgeving biedt voor het veilig uitvoeren van Azure App Service-apps.</span><span class="sxs-lookup"><span data-stu-id="871d6-108">An App Service Environment (ASE) is a [Premium](https://azure.microsoft.com/pricing/details/app-service/) service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps.</span></span> <span data-ttu-id="871d6-109">Zie voor meer informatie over het as-omgeving, de [documentatie van App Service-omgeving](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="871d6-109">To learn more about ASE, see the [App Service Environment Documentation](../app-service/app-service-app-service-environments-readme.md).</span></span>

> [!NOTE]
> <span data-ttu-id="871d6-110">In dit document wordt de service geïntroduceerd aan de hand van een voorbeeldimplementatie.</span><span class="sxs-lookup"><span data-stu-id="871d6-110">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="871d6-111">Dit document is niet een stapsgewijze handleiding.</span><span class="sxs-lookup"><span data-stu-id="871d6-111">This document is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="871d6-112">De aanbeveling implementeren</span><span class="sxs-lookup"><span data-stu-id="871d6-112">Implement the recommendation</span></span>
1. <span data-ttu-id="871d6-113">In de **aanbevelingen** blade Selecteer **-webtoepassing met web application firewall Secure**.</span><span class="sxs-lookup"><span data-stu-id="871d6-113">In the **Recommendations** blade, select **Secure web application using web application firewall**.</span></span>
   <span data-ttu-id="871d6-114">![Web Application beveiligen][1]</span><span class="sxs-lookup"><span data-stu-id="871d6-114">![Secure web Application][1]</span></span>
2. <span data-ttu-id="871d6-115">In de **beveiligen van uw webtoepassingen met web application firewall** blade, selecteert u een webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="871d6-115">In the **Secure your web applications using web application firewall** blade, select a web application.</span></span> <span data-ttu-id="871d6-116">De **Web Application Firewall toevoegen** blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="871d6-116">The **Add a Web Application Firewall** blade opens.</span></span>
   <span data-ttu-id="871d6-117">![Een firewall voor webtoepassingen toevoegen][2]</span><span class="sxs-lookup"><span data-stu-id="871d6-117">![Add a web application firewall][2]</span></span>
3. <span data-ttu-id="871d6-118">U kunt kiezen om een bestaande web application firewall als beschikbaar of u kunt een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="871d6-118">You can choose to use an existing web application firewall if available or you can create a new one.</span></span> <span data-ttu-id="871d6-119">In dit voorbeeld zijn er geen bestaande WAFs beschikbaar, dus we een WAF maken.</span><span class="sxs-lookup"><span data-stu-id="871d6-119">In this example, there are no existing WAFs available so we create a WAF.</span></span>
4. <span data-ttu-id="871d6-120">Selecteer voor het maken van een WAF, een oplossing uit de lijst met geïntegreerde partners.</span><span class="sxs-lookup"><span data-stu-id="871d6-120">To create a WAF, select a solution from the list of integrated partners.</span></span> <span data-ttu-id="871d6-121">In dit voorbeeld selecteren we **Barracuda Web Application Firewall**.</span><span class="sxs-lookup"><span data-stu-id="871d6-121">In this example, we select **Barracuda Web Application Firewall**.</span></span>
5. <span data-ttu-id="871d6-122">De **Barracuda Web Application Firewall** blade wordt geopend zodat u informatie over de partneroplossing.</span><span class="sxs-lookup"><span data-stu-id="871d6-122">The **Barracuda Web Application Firewall** blade opens providing you information about the partner solution.</span></span> <span data-ttu-id="871d6-123">Selecteer **maken** in de blade informatie.</span><span class="sxs-lookup"><span data-stu-id="871d6-123">Select **Create** in the information blade.</span></span>

   ![Firewall-informatie-blade][3]

6. <span data-ttu-id="871d6-125">De **nieuwe Web Application Firewall** blade wordt geopend, waar u kunt uitvoeren **VM-configuratie** stappen en geef **WAF informatie**.</span><span class="sxs-lookup"><span data-stu-id="871d6-125">The **New Web Application Firewall** blade opens, where you can perform **VM Configuration** steps and provide **WAF Information**.</span></span> <span data-ttu-id="871d6-126">Selecteer **VM-configuratie**.</span><span class="sxs-lookup"><span data-stu-id="871d6-126">Select **VM Configuration**.</span></span>
7. <span data-ttu-id="871d6-127">In de **VM-configuratie** blade, voert u gegevens die zijn vereist voor de virtuele machine die wordt uitgevoerd de WAF draaien.</span><span class="sxs-lookup"><span data-stu-id="871d6-127">In the **VM Configuration** blade, you enter information required to spin up the virtual machine that runs the WAF.</span></span>
   <span data-ttu-id="871d6-128">![VM-configuratie][4]</span><span class="sxs-lookup"><span data-stu-id="871d6-128">![VM configuration][4]</span></span>
8. <span data-ttu-id="871d6-129">Ga terug naar de **nieuwe Web Application Firewall** blade en selecteer **WAF informatie**.</span><span class="sxs-lookup"><span data-stu-id="871d6-129">Return to the **New Web Application Firewall** blade and select **WAF Information**.</span></span> <span data-ttu-id="871d6-130">In de **WAF informatie** blade u de WAF zelf configureren.</span><span class="sxs-lookup"><span data-stu-id="871d6-130">In the **WAF Information** blade, you configure the WAF itself.</span></span> <span data-ttu-id="871d6-131">Stap 7 kunt u voor het configureren van de virtuele machine waarop de WAF wordt uitgevoerd en stap 8 kunt u voor het inrichten van de WAF zelf.</span><span class="sxs-lookup"><span data-stu-id="871d6-131">Step 7 allows you to configure the virtual machine on which the WAF runs and step 8 enables you to provision the WAF itself.</span></span>

## <a name="finalize-application-protection"></a><span data-ttu-id="871d6-132">Toepassingsbeveiliging voltooien</span><span class="sxs-lookup"><span data-stu-id="871d6-132">Finalize application protection</span></span>
1. <span data-ttu-id="871d6-133">Ga terug naar de **aanbevelingen** blade.</span><span class="sxs-lookup"><span data-stu-id="871d6-133">Return to the **Recommendations** blade.</span></span> <span data-ttu-id="871d6-134">Een nieuwe vermelding is gegenereerd nadat u de WAF, aangeroepen gemaakt **Toepassingsbeveiliging voltooien**.</span><span class="sxs-lookup"><span data-stu-id="871d6-134">A new entry was generated after you created the WAF, called **Finalize application protection**.</span></span> <span data-ttu-id="871d6-135">Deze vermelding laat u weten dat u voltooien van het proces moet van het daadwerkelijk bekabeling van de WAF binnen het virtuele netwerk van Azure, zodat deze de toepassing kunt beveiligen.</span><span class="sxs-lookup"><span data-stu-id="871d6-135">This entry lets you know that you need to complete the process of actually wiring up the WAF within the Azure Virtual Network so that it can protect the application.</span></span>

   ![Toepassingsbeveiliging voltooien][5]

2. <span data-ttu-id="871d6-137">Selecteer **Toepassingsbeveiliging voltooien**.</span><span class="sxs-lookup"><span data-stu-id="871d6-137">Select **Finalize application protection**.</span></span> <span data-ttu-id="871d6-138">Er wordt een nieuwe blade geopend.</span><span class="sxs-lookup"><span data-stu-id="871d6-138">A new blade opens.</span></span> <span data-ttu-id="871d6-139">U ziet dat er een webtoepassing die u moet beschikken over de verkeer gerouteerd.</span><span class="sxs-lookup"><span data-stu-id="871d6-139">You can see that there is a web application that needs to have its traffic rerouted.</span></span>
3. <span data-ttu-id="871d6-140">Selecteer de webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="871d6-140">Select the web application.</span></span> <span data-ttu-id="871d6-141">Er wordt een blade geopend waarmee u stappen voor het voltooien van de web application firewall-instellingen.</span><span class="sxs-lookup"><span data-stu-id="871d6-141">A blade opens that gives you steps for finalizing the web application firewall setup.</span></span> <span data-ttu-id="871d6-142">Voer de stappen uit en selecteer vervolgens **verkeer te beperken**.</span><span class="sxs-lookup"><span data-stu-id="871d6-142">Complete the steps, and then select **Restrict traffic**.</span></span> <span data-ttu-id="871d6-143">Security Center doet vervolgens de bedrading-up voor u.</span><span class="sxs-lookup"><span data-stu-id="871d6-143">Security Center then does the wiring-up for you.</span></span>

   ![Verkeer te beperken][6]

> [!NOTE]
> <span data-ttu-id="871d6-145">U kunt meerdere webtoepassingen in Security Center beveiligen door deze toepassingen toevoegen aan uw bestaande WAF-implementaties.</span><span class="sxs-lookup"><span data-stu-id="871d6-145">You can protect multiple web applications in Security Center by adding these applications to your existing WAF deployments.</span></span>
>
>

<span data-ttu-id="871d6-146">De logboeken van die WAF zijn nu volledig geïntegreerd.</span><span class="sxs-lookup"><span data-stu-id="871d6-146">The logs from that WAF are now fully integrated.</span></span> <span data-ttu-id="871d6-147">Security Center kunt starten automatisch verzamelen en analyseren in de logboeken zodat dit kan belangrijk beveiligingswaarschuwingen surface voor u.</span><span class="sxs-lookup"><span data-stu-id="871d6-147">Security Center can start automatically gathering and analyzing the logs so that it can surface important security alerts to you.</span></span>

## <a name="next-steps"></a><span data-ttu-id="871d6-148">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="871d6-148">Next steps</span></span>
<span data-ttu-id="871d6-149">Dit document hebt u geleerd hoe u implementeert de aanbeveling Security Center "Een webtoepassing toevoegen".</span><span class="sxs-lookup"><span data-stu-id="871d6-149">This document showed you how to implement the Security Center recommendation "Add a web application."</span></span> <span data-ttu-id="871d6-150">Zie de volgende onderwerpen voor meer informatie over het configureren van een web application firewall:</span><span class="sxs-lookup"><span data-stu-id="871d6-150">To learn more about configuring a web application firewall, see the following:</span></span>

* [<span data-ttu-id="871d6-151">Web Application Firewall (WAF) configureren voor App Service-omgeving</span><span class="sxs-lookup"><span data-stu-id="871d6-151">Configuring a Web Application Firewall (WAF) for App Service Environment</span></span>](../app-service-web/app-service-app-service-environment-web-application-firewall.md)

<span data-ttu-id="871d6-152">Zie de volgende onderwerpen voor meer informatie over het Beveiligingscentrum:</span><span class="sxs-lookup"><span data-stu-id="871d6-152">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="871d6-153">[Setting security policies in Azure Security Center](security-center-policies.md) (Beveiligingsbeleid instellen in Azure Security Center): leer hoe u beveiligingsbeleid voor uw Azure-abonnementen en -resourcegroepen configureert.</span><span class="sxs-lookup"><span data-stu-id="871d6-153">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="871d6-154">[Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md) --informatie over het bewaken van de status van uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="871d6-154">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="871d6-155">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) (Beveiligingswaarschuwingen beheren en erop reageren in Azure Security Center): ontdek hoe u beveiligingswaarschuwingen kunt beheren en erop kunt reageren.</span><span class="sxs-lookup"><span data-stu-id="871d6-155">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="871d6-156">[Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md) --Leer hoe aanbevelingen u uw Azure-resources te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="871d6-156">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="871d6-157">[Azure Security Center FAQ](security-center-faq.md) (Veelgestelde vragen over Azure Security Center): raadpleeg veelgestelde vragen over het gebruik van de service.</span><span class="sxs-lookup"><span data-stu-id="871d6-157">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="871d6-158">[Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/) --Lees blogberichten over Azure-beveiliging en naleving.</span><span class="sxs-lookup"><span data-stu-id="871d6-158">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-add-web-application-firewall/secure-web-application.png
[2]:./media/security-center-add-web-application-firewall/add-a-waf.png
[3]: ./media/security-center-add-web-application-firewall/info-blade.png
[4]: ./media/security-center-add-web-application-firewall/select-vm-config.png
[5]: ./media/security-center-add-web-application-firewall/finalize-waf.png
[6]: ./media/security-center-add-web-application-firewall/restrict-traffic.png
