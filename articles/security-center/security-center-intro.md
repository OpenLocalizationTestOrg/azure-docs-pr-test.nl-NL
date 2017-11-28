---
title: Inleiding tot Azure Security Center | Microsoft Docs
description: Meer informatie over Azure Security Center, de belangrijkste mogelijkheden van Azure Security Center en hoe Azure Security Center werkt.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 45b9756b-6449-49ec-950b-5ed1e7c56daa
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 8951167213da6ab5341c1ca420353ec625ef5424
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-azure-security-center"></a><span data-ttu-id="3f967-103">Inleiding tot Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="3f967-103">Introduction to Azure Security Center</span></span>
<span data-ttu-id="3f967-104">Meer informatie over Azure Security Center, de belangrijkste mogelijkheden van Azure Security Center en hoe Azure Security Center werkt.</span><span class="sxs-lookup"><span data-stu-id="3f967-104">Learn about Azure Security Center, its key capabilities, and how it works.</span></span>

> [!NOTE]
> <span data-ttu-id="3f967-105">Vanaf begin juni 2017 zal Security Center de Microsoft Monitoring Agent gebruiken voor het verzamelen en opslaan van gegevens.</span><span class="sxs-lookup"><span data-stu-id="3f967-105">Beginning in early June 2017, Security Center will use the Microsoft Monitoring Agent to collect and store data.</span></span> <span data-ttu-id="3f967-106">Zie [Migratie van Azure Security Center-platform](security-center-platform-migration.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3f967-106">See [Azure Security Center Platform Migration](security-center-platform-migration.md) to learn more.</span></span> <span data-ttu-id="3f967-107">De informatie in dit artikel beschrijft functionaliteit van Security Center na de overstap naar de Microsoft Monitoring Agent.</span><span class="sxs-lookup"><span data-stu-id="3f967-107">The information in this article represents Security Center functionality after transition to the Microsoft Monitoring Agent.</span></span>
>
>

## <a name="what-is-azure-security-center"></a><span data-ttu-id="3f967-108">Wat is Azure Security Center?</span><span class="sxs-lookup"><span data-stu-id="3f967-108">What is Azure Security Center?</span></span>
 <span data-ttu-id="3f967-109">Azure Security Center helpt u bij het detecteren, voorkomen van en reageren op bedreigingen dankzij een verhoogde zichtbaarheid van en controle over de beveiliging van uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="3f967-109">Security Center helps you prevent, detect, and respond to threats with increased visibility into and control over the security of your Azure resources.</span></span> <span data-ttu-id="3f967-110">Het biedt geïntegreerde beveiligingsbewaking en beleidsbeheer voor uw Azure-abonnementen, helpt bedreigingen te detecteren die anders onopgemerkt zouden blijven, en werkt met een uitgebreid ecosysteem van beveiligingsoplossingen.</span><span class="sxs-lookup"><span data-stu-id="3f967-110">It provides integrated security monitoring and policy management across your Azure subscriptions, helps detect threats that might otherwise go unnoticed, and works with a broad ecosystem of security solutions.</span></span>

## <a name="key-capabilities"></a><span data-ttu-id="3f967-111">Belangrijkste mogelijkheden</span><span class="sxs-lookup"><span data-stu-id="3f967-111">Key capabilities</span></span>
 <span data-ttu-id="3f967-112">Security Center biedt eenvoudige en effectieve preventie en detectie van bedreigingen en reactiemogelijkheden die zijn ingebouwd in Azure.</span><span class="sxs-lookup"><span data-stu-id="3f967-112">Security Center delivers easy-to-use and effective threat prevention, detection, and response capabilities that are built in to Azure.</span></span> <span data-ttu-id="3f967-113">De belangrijkste mogelijkheden zijn:</span><span class="sxs-lookup"><span data-stu-id="3f967-113">Key capabilities are:</span></span>

| <span data-ttu-id="3f967-114">Fase</span><span class="sxs-lookup"><span data-stu-id="3f967-114">Stage</span></span> | <span data-ttu-id="3f967-115">Mogelijkheid</span><span class="sxs-lookup"><span data-stu-id="3f967-115">Capability</span></span> |
| --- | --- |
| <span data-ttu-id="3f967-116">Voorkomen</span><span class="sxs-lookup"><span data-stu-id="3f967-116">Prevent</span></span> |<span data-ttu-id="3f967-117">De beveiligingsstatus van uw Azure-resources wordt gecontroleerd</span><span class="sxs-lookup"><span data-stu-id="3f967-117">Monitors the security state of your Azure resources</span></span> |
| <span data-ttu-id="3f967-118">Voorkomen</span><span class="sxs-lookup"><span data-stu-id="3f967-118">Prevent</span></span> | <span data-ttu-id="3f967-119">Wordt beleid gedefinieerd voor uw Azure-abonnementen op basis van beveiligingsvereisten van uw bedrijf, de typen toepassingen die u hebt gebruikt, en de vertrouwelijkheid van uw gegevens</span><span class="sxs-lookup"><span data-stu-id="3f967-119">Defines policies for your Azure subscriptions based on your company’s security requirements, the types of applications that you use, and the sensitivity of your data</span></span> |
| <span data-ttu-id="3f967-120">Voorkomen</span><span class="sxs-lookup"><span data-stu-id="3f967-120">Prevent</span></span> | <span data-ttu-id="3f967-121">Er wordt gebruikgemaakt van beveiligingsaanbevelingen van het beleid om service-eigenaren te begeleiden bij de implementatie van benodigde besturingselementen</span><span class="sxs-lookup"><span data-stu-id="3f967-121">Uses policy-driven security recommendations to guide service owners through the process of implementing needed controls</span></span> |
| <span data-ttu-id="3f967-122">Voorkomen</span><span class="sxs-lookup"><span data-stu-id="3f967-122">Prevent</span></span> | <span data-ttu-id="3f967-123">Beveiligingsservices en -toepassingen van Microsoft en partners worden snel geïmplementeerd</span><span class="sxs-lookup"><span data-stu-id="3f967-123">Rapidly deploys security services and appliances from Microsoft and partners</span></span> |
| <span data-ttu-id="3f967-124">Detecteren</span><span class="sxs-lookup"><span data-stu-id="3f967-124">Detect</span></span> |<span data-ttu-id="3f967-125">Beveiligingsgegevens van uw Azure-resources, het netwerk en partneroplossingen zoals antimalwareprogramma's en firewalls worden automatisch verzameld en geanalyseerd</span><span class="sxs-lookup"><span data-stu-id="3f967-125">Automatically collects and analyzes security data from your Azure resources, the network, and partner solutions like antimalware programs and firewalls</span></span> |
| <span data-ttu-id="3f967-126">Detecteren</span><span class="sxs-lookup"><span data-stu-id="3f967-126">Detect</span></span> | <span data-ttu-id="3f967-127">Maakt gebruik van globale dreiging intelligence van Microsoft-producten en services, de Microsoft Digital Crimes Unit (DCU), de Microsoft Security Response Center (MSRC) en externe feeds</span><span class="sxs-lookup"><span data-stu-id="3f967-127">Uses global threat intelligence from Microsoft products and services, the Microsoft Digital Crimes Unit (DCU), the Microsoft Security Response Center (MSRC), and external feeds</span></span> |
| <span data-ttu-id="3f967-128">Detecteren</span><span class="sxs-lookup"><span data-stu-id="3f967-128">Detect</span></span> | <span data-ttu-id="3f967-129">Er worden geavanceerde analyses toegepast, waaronder machine learning en gedragsanalyse</span><span class="sxs-lookup"><span data-stu-id="3f967-129">Applies advanced analytics, including machine learning and behavioral analysis</span></span> |
| <span data-ttu-id="3f967-130">Reageren</span><span class="sxs-lookup"><span data-stu-id="3f967-130">Respond</span></span> |<span data-ttu-id="3f967-131">Beveiligingsincidenten/-waarschuwingen worden met prioriteit geleverd</span><span class="sxs-lookup"><span data-stu-id="3f967-131">Provides prioritized security incidents/alerts</span></span> |
| <span data-ttu-id="3f967-132">Reageren</span><span class="sxs-lookup"><span data-stu-id="3f967-132">Respond</span></span> | <span data-ttu-id="3f967-133">Er wordt inzicht geboden in de bron van de aanval en betrokken resources</span><span class="sxs-lookup"><span data-stu-id="3f967-133">Offers insights into the source of the attack and impacted resources</span></span> |
| <span data-ttu-id="3f967-134">Reageren</span><span class="sxs-lookup"><span data-stu-id="3f967-134">Respond</span></span> | <span data-ttu-id="3f967-135">Er worden manieren voorgesteld om de huidige aanval te stoppen en toekomstige aanvallen te voorkomen</span><span class="sxs-lookup"><span data-stu-id="3f967-135">Suggests ways to stop the current attack and help prevent future attacks</span></span> |

## <a name="introductory-walkthrough"></a><span data-ttu-id="3f967-136">Introductie</span><span class="sxs-lookup"><span data-stu-id="3f967-136">Introductory walkthrough</span></span>

> [!NOTE]
> <span data-ttu-id="3f967-137">In dit document wordt de service geïntroduceerd aan de hand van een voorbeeldimplementatie.</span><span class="sxs-lookup"><span data-stu-id="3f967-137">This document introduces the service by using an example deployment.</span></span> <span data-ttu-id="3f967-138">Dit document is niet een stapsgewijze handleiding.</span><span class="sxs-lookup"><span data-stu-id="3f967-138">This document is not a step-by-step guide.</span></span>
>
>

 <span data-ttu-id="3f967-139">Security Center is toegankelijk via [Azure Portal](https://azure.microsoft.com/features/azure-portal/).</span><span class="sxs-lookup"><span data-stu-id="3f967-139">You access Security Center from the [Azure portal](https://azure.microsoft.com/features/azure-portal/).</span></span> <span data-ttu-id="3f967-140">[Aanmelden bij de portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3f967-140">[Sign in to the portal](https://portal.azure.com).</span></span> <span data-ttu-id="3f967-141">Schuif onder het portal hoofdmenu naar de **Security Center** optie of Selecteer de **Security Center** tegel die u eerder aan het portaldashboard hebt vastgemaakt.</span><span class="sxs-lookup"><span data-stu-id="3f967-141">Under the main portal menu, scroll to the **Security Center** option or select the **Security Center** tile that you previously pinned to the portal dashboard.</span></span>

![Beveiligingstegel in Azure Portal][1]

<span data-ttu-id="3f967-143">Vanuit Security Center kunt u beveiligingsbeleid instellen, beveiligingsconfiguraties bewaken en beveiligingswaarschuwingen weergeven.</span><span class="sxs-lookup"><span data-stu-id="3f967-143">From Security Center, you can set security policies, monitor security configurations, and view security alerts.</span></span>

### <a name="security-policies"></a><span data-ttu-id="3f967-144">Beveiligingsbeleid</span><span class="sxs-lookup"><span data-stu-id="3f967-144">Security policies</span></span>
<span data-ttu-id="3f967-145">U kunt beleid definiëren voor uw Azure-abonnementen volgens de vereisten van de beveiliging van uw bedrijf.</span><span class="sxs-lookup"><span data-stu-id="3f967-145">You can define policies for your Azure subscriptions according to your company's security requirements.</span></span> <span data-ttu-id="3f967-146">Vervolgens kunt u het beleid aanpassen aan de typen toepassingen die u gebruikt, of de vertrouwelijkheid van de gegevens in elk abonnement.</span><span class="sxs-lookup"><span data-stu-id="3f967-146">You can also tailor them to the types of applications you're using or to the sensitivity of the data in each subscription.</span></span> <span data-ttu-id="3f967-147">Zo kunnen er voor resources die worden gebruikt voor ontwikkeling of tests, andere beveiligingsvereisten zijn dan voor resources die worden gebruikt voor productietoepassingen.</span><span class="sxs-lookup"><span data-stu-id="3f967-147">For example, resources used for development or testing may have different security requirements than those used for production applications.</span></span> <span data-ttu-id="3f967-148">Ook kan voor toepassingen met gereglementeerde gegevens, zoals PII, een hoger beveiligingsniveau vereist zijn.</span><span class="sxs-lookup"><span data-stu-id="3f967-148">Likewise, applications with regulated data like PII may require a higher level of security.</span></span>

> [!NOTE]
> <span data-ttu-id="3f967-149">Als u wilt een beveiligingsbeleid wijzigen, moet u een beveiligingsbeheerder of eigenaar of bijdrager van het abonnement.</span><span class="sxs-lookup"><span data-stu-id="3f967-149">To modify a security policy, you must be a Security Administrator or the subscription's Owner or Contributor.</span></span> <span data-ttu-id="3f967-150">Voor meer informatie over rollen en toegestane acties in Security Center, Zie [machtigingen in Azure Security Center](security-center-permissions.md).</span><span class="sxs-lookup"><span data-stu-id="3f967-150">To learn more about roles and allowed actions in Security Center, see [Permissions in Azure Security Center](security-center-permissions.md).</span></span>
>
>

<span data-ttu-id="3f967-151">Selecteer op de blade **Security Center** de tegel **Beleid** voor een lijst met uw abonnementen en resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="3f967-151">On the **Security Center** blade, select the **Policy** tile for a list of your subscriptions and resource groups.</span></span>   

![Blade Security Center][2]

<span data-ttu-id="3f967-153">Op de **beveiligingsbeleid** blade, selecteert u een abonnement om details van het beleid weer te geven.</span><span class="sxs-lookup"><span data-stu-id="3f967-153">On the **Security policy** blade, select a subscription to view the policy details.</span></span>

<span data-ttu-id="3f967-154">**Gegevensverzameling** schakelt u gegevensverzameling voor een beveiligingsbeleid.</span><span class="sxs-lookup"><span data-stu-id="3f967-154">**Data collection** enables data collection for a security policy.</span></span> <span data-ttu-id="3f967-155">Het inschakelen biedt:</span><span class="sxs-lookup"><span data-stu-id="3f967-155">Enabling provides:</span></span>

* <span data-ttu-id="3f967-156">Dagelijks scannen van alle virtuele machines (VM's) ondersteund voor het bewaken van de beveiliging en aanbevelingen.</span><span class="sxs-lookup"><span data-stu-id="3f967-156">Daily scanning of all supported virtual machines (VMs) for security monitoring and recommendations.</span></span>
* <span data-ttu-id="3f967-157">Verzameling van beveiligingsgebeurtenissen voor analyse en detectie van bedreigingen.</span><span class="sxs-lookup"><span data-stu-id="3f967-157">Collection of security events for analysis and threat detection.</span></span>

> [!NOTE]
> <span data-ttu-id="3f967-158">Gegevensverzameling is geconfigureerd op het abonnementsniveau.</span><span class="sxs-lookup"><span data-stu-id="3f967-158">Data collection is configured at the subscription level.</span></span>
>
>

<span data-ttu-id="3f967-159">Selecteer **preventiebeleid** openen de **preventiebeleid** blade.</span><span class="sxs-lookup"><span data-stu-id="3f967-159">Select **Prevention policy** to open the **Prevention policy** blade.</span></span> <span data-ttu-id="3f967-160">**Aanbevelingen weergeven voor** kunt u ervoor kiest de beveiligingsmechanismen die u wilt bewaken en de aanbevelingen die u wilt weergeven op basis van de beveiligingsvereisten van de resources in het abonnement.</span><span class="sxs-lookup"><span data-stu-id="3f967-160">**Show recommendations for** lets you choose the security controls that you want to monitor and the recommendations that you want to see based on the security needs of the resources within the subscription.</span></span>

### <a name="security-recommendations"></a><span data-ttu-id="3f967-161">Aanbevelingen voor beveiliging</span><span class="sxs-lookup"><span data-stu-id="3f967-161">Security recommendations</span></span>
 <span data-ttu-id="3f967-162">Security Center analyseert de beveiligingsstatus van uw Azure-resources om mogelijke beveiligingsproblemen op te sporen.</span><span class="sxs-lookup"><span data-stu-id="3f967-162">Security Center analyzes the security state of your Azure resources to identify potential security vulnerabilities.</span></span> <span data-ttu-id="3f967-163">Een lijst met aanbevelingen begeleidt u bij het configureren van benodigde besturingselementen.</span><span class="sxs-lookup"><span data-stu-id="3f967-163">A list of recommendations guides you through the process of configuring needed controls.</span></span> <span data-ttu-id="3f967-164">Voorbeelden zijn:</span><span class="sxs-lookup"><span data-stu-id="3f967-164">Examples include:</span></span>

* <span data-ttu-id="3f967-165">Inrichting van antimalware om schadelijke software te identificeren en te verwijderen</span><span class="sxs-lookup"><span data-stu-id="3f967-165">Provisioning antimalware to help identify and remove malicious software</span></span>
* <span data-ttu-id="3f967-166">Netwerkbeveiligingsgroepen en regels voor het verkeer voor beheer voor virtuele machines configureren</span><span class="sxs-lookup"><span data-stu-id="3f967-166">Configuring network security groups and rules to control traffic to VMs</span></span>
* <span data-ttu-id="3f967-167">Inrichten van Web Application Firewalls om te beschermen tegen aanvallen die zijn gericht op uw webtoepassingen</span><span class="sxs-lookup"><span data-stu-id="3f967-167">Provisioning of web application firewalls to help defend against attacks that target your web applications</span></span>
* <span data-ttu-id="3f967-168">Implementatie van ontbrekende systeemupdates</span><span class="sxs-lookup"><span data-stu-id="3f967-168">Deploying missing system updates</span></span>
* <span data-ttu-id="3f967-169">Aanpassing van besturingssysteemconfiguraties die niet overeenkomen met de aanbevolen basislijnen</span><span class="sxs-lookup"><span data-stu-id="3f967-169">Addressing OS configurations that do not match the recommended baselines</span></span>

<span data-ttu-id="3f967-170">Klik op de tegel **Aanbevelingen** voor een lijst met aanbevelingen.</span><span class="sxs-lookup"><span data-stu-id="3f967-170">Click the **Recommendations** tile for a list of recommendations.</span></span> <span data-ttu-id="3f967-171">Klik op elke aanbeveling om extra informatie weer te geven of te doen om het probleem te verhelpen.</span><span class="sxs-lookup"><span data-stu-id="3f967-171">Click each recommendation to view additional information or to take action to resolve the issue.</span></span>

![Aanbevelingen voor beveiliging in Azure Security Center][5]

### <a name="security-state-of-azure-resources"></a><span data-ttu-id="3f967-173">Beveiligingsstatus van de Azure-resources</span><span class="sxs-lookup"><span data-stu-id="3f967-173">Security state of Azure resources</span></span>
<span data-ttu-id="3f967-174">De **preventie** gedeelte van het dashboard ziet u de algehele beveiligingsstatus van de omgeving per resourcetype, met inbegrip van virtuele machines, webtoepassingen en andere bronnen.</span><span class="sxs-lookup"><span data-stu-id="3f967-174">The **Prevention** section of the dashboard shows the overall security posture of the environment by resource type, including VMs, web applications, and other resources.</span></span>   

<span data-ttu-id="3f967-175">Selecteer een resourcetype onder **preventie** voor meer informatie, waaronder een lijst met alle mogelijke beveiligingsproblemen die zijn geïdentificeerd.</span><span class="sxs-lookup"><span data-stu-id="3f967-175">Select a resource type under **Prevention** to view more information, including a list of any potential security vulnerabilities that have been identified.</span></span> <span data-ttu-id="3f967-176">(**Compute** is geselecteerd in het onderstaande voorbeeld.)</span><span class="sxs-lookup"><span data-stu-id="3f967-176">(**Compute** is selected in the example below.)</span></span>

![Tegel Status van resources][6]

### <a name="security-alerts"></a><span data-ttu-id="3f967-178">Beveiligingswaarschuwingen</span><span class="sxs-lookup"><span data-stu-id="3f967-178">Security alerts</span></span>
 <span data-ttu-id="3f967-179">Security Center verzamelt, analyseert en integreert automatisch logboekgegevens van uw Azure-resources, het netwerk en partneroplossingen zoals antimalwareprogramma's en firewalls.</span><span class="sxs-lookup"><span data-stu-id="3f967-179">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, the network, and partner solutions like antimalware programs and firewalls.</span></span> <span data-ttu-id="3f967-180">Wanneer er dreigingen worden gedetecteerd, wordt een beveiligingswaarschuwing gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3f967-180">When threats are detected, a security alert is created.</span></span> <span data-ttu-id="3f967-181">Voorbeelden zijn detectie van:</span><span class="sxs-lookup"><span data-stu-id="3f967-181">Examples include detection of:</span></span>

* <span data-ttu-id="3f967-182">Verdachte VM's die communiceren met bekende schadelijke IP-adressen</span><span class="sxs-lookup"><span data-stu-id="3f967-182">Compromised VMs communicating with known malicious IP addresses</span></span>
* <span data-ttu-id="3f967-183">Geavanceerde malware die is gedetecteerd met Windows Foutrapportage</span><span class="sxs-lookup"><span data-stu-id="3f967-183">Advanced malware detected by using Windows error reporting</span></span>
* <span data-ttu-id="3f967-184">Beveiligingsaanvallen op virtuele machines</span><span class="sxs-lookup"><span data-stu-id="3f967-184">Brute force attacks against VMs</span></span>
* <span data-ttu-id="3f967-185">Beveiligingswaarschuwingen van geïntegreerde antimalwareprogramma's en firewalls</span><span class="sxs-lookup"><span data-stu-id="3f967-185">Security alerts from integrated antimalware programs and firewalls</span></span>

<span data-ttu-id="3f967-186">Als u op de tegel **Beveiligingswaarschuwingen** klikt, wordt een lijst waarschuwingen met prioriteit weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3f967-186">Clicking the **Security alerts** tile displays a list of prioritized alerts.</span></span>

![Beveiligingswaarschuwingen][7]

<span data-ttu-id="3f967-188">Als u een waarschuwing selecteert, ziet u meer informatie over de aanval en suggesties voor herstel.</span><span class="sxs-lookup"><span data-stu-id="3f967-188">Selecting an alert shows more information about the attack and suggestions for how to remediate it.</span></span>

![Details van beveiligingswaarschuwing][8]

### <a name="partner-solutions"></a><span data-ttu-id="3f967-190">Partneroplossingen</span><span class="sxs-lookup"><span data-stu-id="3f967-190">Partner solutions</span></span>
<span data-ttu-id="3f967-191">De **partneroplossingen** tegel kunt u controleren in één oogopslag de beveiligingsstatus van uw partneroplossingen die zijn geïntegreerd met uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="3f967-191">The **Partner solutions** tile lets you monitor at a glance the security state of your partner solutions integrated with your Azure subscription.</span></span> <span data-ttu-id="3f967-192">Security Center bevat waarschuwingen die van de oplossingen afkomstig zijn.</span><span class="sxs-lookup"><span data-stu-id="3f967-192">Security Center displays alerts coming from the solutions.</span></span>

<span data-ttu-id="3f967-193">Selecteer de tegel **Partneroplossingen**.</span><span class="sxs-lookup"><span data-stu-id="3f967-193">Select the **Partner solutions** tile.</span></span> <span data-ttu-id="3f967-194">Er wordt een blade met een lijst van alle verbonden partneroplossingen geopend.</span><span class="sxs-lookup"><span data-stu-id="3f967-194">A blade opens displaying a list of all connected partner solutions.</span></span>

![Partneroplossingen][9]

## <a name="get-started"></a><span data-ttu-id="3f967-196">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="3f967-196">Get started</span></span>
<span data-ttu-id="3f967-197">Om te beginnen met Security Center, moet u een abonnement op Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="3f967-197">To get started with Security Center, you need a subscription to Microsoft Azure.</span></span> <span data-ttu-id="3f967-198">Security Center wordt met uw Azure-abonnement ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="3f967-198">Security Center is enabled with your Azure subscription.</span></span> <span data-ttu-id="3f967-199">Als u geen abonnement hebt, kunt u zich aanmelden voor een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3f967-199">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

 <span data-ttu-id="3f967-200">Security Center is toegankelijk via [Azure Portal](https://azure.microsoft.com/features/azure-portal/).</span><span class="sxs-lookup"><span data-stu-id="3f967-200">You access Security Center from the [Azure portal](https://azure.microsoft.com/features/azure-portal/).</span></span> <span data-ttu-id="3f967-201">Zie de [portaldocumentatie](https://azure.microsoft.com/documentation/services/azure-portal/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3f967-201">See the [portal documentation](https://azure.microsoft.com/documentation/services/azure-portal/) to learn more.</span></span>

<span data-ttu-id="3f967-202">In [Aan de slag met Azure Security Center](security-center-get-started.md) leert u snel de onderdelen van Security Center voor de bewaking van de beveiliging en het beheer van het beleid kennen.</span><span class="sxs-lookup"><span data-stu-id="3f967-202">[Getting started with Azure Security Center](security-center-get-started.md) quickly guides you through the security-monitoring and policy-management components of Security Center.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f967-203">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3f967-203">Next steps</span></span>
<span data-ttu-id="3f967-204">Dit document is een inleiding tot Security Center, de belangrijkste mogelijkheden hiervan en hoe u met Security Center aan de slag gaat.</span><span class="sxs-lookup"><span data-stu-id="3f967-204">In this document, you were introduced to Security Center, its key capabilities, and how to get started.</span></span> <span data-ttu-id="3f967-205">Zie de volgende bronnen voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="3f967-205">To learn more, see the following resources:</span></span>

* <span data-ttu-id="3f967-206">[Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md) : informatie over het beveiligingsbeleid voor uw Azure-abonnementen en resourcegroepen configureren.</span><span class="sxs-lookup"><span data-stu-id="3f967-206">[Setting security policies in Azure Security Center](security-center-policies.md) — Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="3f967-207">[Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md) : Leer hoe aanbevelingen u uw Azure-resources te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="3f967-207">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="3f967-208">[Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md): meer informatie over het bewaken van de status van uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="3f967-208">[Security health monitoring in Azure Security Center](security-center-monitoring.md) — Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="3f967-209">[Het beheren van en reageren op beveiligingswaarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md) : informatie over het beheren van en reageren op beveiligingswaarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="3f967-209">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) — Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="3f967-210">[Partneroplossingen controleren met Azure Security Center](security-center-partner-solutions.md): leer hoe u de integriteitsstatus van uw partneroplossingen kunt controleren.</span><span class="sxs-lookup"><span data-stu-id="3f967-210">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) — Learn how to monitor the health status of your partner solutions.</span></span>
- <span data-ttu-id="3f967-211">[Beveiliging van gegevens van Azure Security Center](security-center-data-security.md) -informatie over hoe gegevens worden beheerd en beveiligd in Security Center.</span><span class="sxs-lookup"><span data-stu-id="3f967-211">[Azure Security Center data security](security-center-data-security.md) - Learn how data is managed and safeguarded in Security Center.</span></span>
* <span data-ttu-id="3f967-212">[Azure Security Center FAQ](security-center-faq.md): raadpleeg veelgestelde vragen over het gebruik van de service.</span><span class="sxs-lookup"><span data-stu-id="3f967-212">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="3f967-213">[Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/) — Lees het laatste nieuws van de Azure-beveiliging en de informatie.</span><span class="sxs-lookup"><span data-stu-id="3f967-213">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-intro/security-tile.png
[2]: ./media/security-center-intro/security-center.png
[3]: ./media/security-center-intro/security-policy.png
[4]: ./media/security-center-intro/security-policy-blade.png
[5]: ./media/security-center-intro/recommendations.png
[6]: ./media/security-center-intro/resources-health.png
[7]: ./media/security-center-intro/security-alert.png
[8]: ./media/security-center-intro/security-alert-detail.png
[9]: ./media/security-center-intro/partner-solutions.png
