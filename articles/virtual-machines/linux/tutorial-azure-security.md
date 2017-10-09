---
title: aaaAzure Security Center- en Linux virtuele machines in Azure | Microsoft Docs
description: Meer informatie over de beveiliging van uw Azure Linux virtuele machine met Azure Security Center.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/07/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 7aa0de35fb311457e769f152c8575ec43e41c39c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-virtual-machine-security-by-using-azure-security-center"></a><span data-ttu-id="f8184-103">Beveiliging van de virtuele machine bewaken met behulp van Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="f8184-103">Monitor virtual machine security by using Azure Security Center</span></span>

<span data-ttu-id="f8184-104">Azure Security Center kunt u meer inzicht verkrijgen in uw Azure-resource procedures voor beveiliging.</span><span class="sxs-lookup"><span data-stu-id="f8184-104">Azure Security Center can help you gain visibility into your Azure resource security practices.</span></span> <span data-ttu-id="f8184-105">Security Center biedt geïntegreerde beveiligingsbewaking.</span><span class="sxs-lookup"><span data-stu-id="f8184-105">Security Center offers integrated security monitoring.</span></span> <span data-ttu-id="f8184-106">Bedreigingen die anders onopgemerkt kunnen worden gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="f8184-106">It can detect threats that otherwise might go unnoticed.</span></span> <span data-ttu-id="f8184-107">In deze zelfstudie hebt u meer informatie over Azure Security Center en hoe:</span><span class="sxs-lookup"><span data-stu-id="f8184-107">In this tutorial, you learn about Azure Security Center, and how to:</span></span>
 
> [!div class="checklist"]
> * <span data-ttu-id="f8184-108">Verzamelen van gegevens instellen</span><span class="sxs-lookup"><span data-stu-id="f8184-108">Set up data collection</span></span>
> * <span data-ttu-id="f8184-109">Een beveiligingsbeleid instellen</span><span class="sxs-lookup"><span data-stu-id="f8184-109">Set up security policies</span></span>
> * <span data-ttu-id="f8184-110">Weergeven en oplossen van problemen met configuratie-status</span><span class="sxs-lookup"><span data-stu-id="f8184-110">View and fix configuration health issues</span></span>
> * <span data-ttu-id="f8184-111">Bekijk de gedetecteerde bedreigingen</span><span class="sxs-lookup"><span data-stu-id="f8184-111">Review detected threats</span></span>  

## <a name="security-center-overview"></a><span data-ttu-id="f8184-112">Security Center-overzicht</span><span class="sxs-lookup"><span data-stu-id="f8184-112">Security Center overview</span></span>

<span data-ttu-id="f8184-113">Beveiligingscentrum identificeert mogelijke configuratieproblemen van de virtuele machine (VM) en gerichte beveiligingsrisico's.</span><span class="sxs-lookup"><span data-stu-id="f8184-113">Security Center identifies potential virtual machine (VM) configuration issues and targeted security threats.</span></span> <span data-ttu-id="f8184-114">Hierbij kunnen virtuele machines met netwerkbeveiligingsgroepen, niet-versleutelde schijven en beveiligingsaanvallen Remote Desktop Protocol (RDP ontbrekende).</span><span class="sxs-lookup"><span data-stu-id="f8184-114">These might include VMs that are missing network security groups, unencrypted disks, and brute-force Remote Desktop Protocol (RDP) attacks.</span></span> <span data-ttu-id="f8184-115">Hallo-informatie wordt weergegeven op Hallo Security Center-dashboard in de grafieken gemakkelijk te lezen.</span><span class="sxs-lookup"><span data-stu-id="f8184-115">hello information is shown on hello Security Center dashboard in easy-to-read graphs.</span></span>

<span data-ttu-id="f8184-116">tooaccess Hallo Security Center-dashboard in hello Azure-portal, selecteer Hallo menu **Security Center**.</span><span class="sxs-lookup"><span data-stu-id="f8184-116">tooaccess hello Security Center dashboard, in hello Azure portal, on hello menu, select  **Security Center**.</span></span> <span data-ttu-id="f8184-117">Op Hallo-dashboard kunt u Zie Hallo beveiligingsstatus van uw Azure-omgeving, een telling van de huidige aanbevelingen vinden en Hallo huidige status van de threat waarschuwingen weergeven.</span><span class="sxs-lookup"><span data-stu-id="f8184-117">On hello dashboard, you can see hello security health of your Azure environment, find a count of current recommendations, and view hello current state of threat alerts.</span></span> <span data-ttu-id="f8184-118">U kunt elke toosee op hoog niveau grafiek uitbreiden meer details.</span><span class="sxs-lookup"><span data-stu-id="f8184-118">You can expand each high-level chart toosee more detail.</span></span>

![Security Center-dashboard](./media/tutorial-azure-security/asc-dash.png)

<span data-ttu-id="f8184-120">Security Center zich verder uitstrekt dan gegevens detectie tooprovide aanbevelingen voor problemen die worden gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="f8184-120">Security Center goes beyond data discovery tooprovide recommendations for issues that it detects.</span></span> <span data-ttu-id="f8184-121">Bijvoorbeeld, als een virtuele machine zonder een gekoppelde netwerkbeveiligingsgroep is geïmplementeerd, Security Center wordt weergegeven een aanbeveling, met herstelstappen die u kunt nemen.</span><span class="sxs-lookup"><span data-stu-id="f8184-121">For example, if a VM was deployed without an attached network security group, Security Center displays a recommendation, with remediation steps you can take.</span></span> <span data-ttu-id="f8184-122">Automatisch doorvoeren krijgt u zonder Hallo context van Security Center.</span><span class="sxs-lookup"><span data-stu-id="f8184-122">You get automated remediation without leaving hello context of Security Center.</span></span>  

![Aanbevelingen](./media/tutorial-azure-security/recommendations.png)

## <a name="set-up-data-collection"></a><span data-ttu-id="f8184-124">Verzamelen van gegevens instellen</span><span class="sxs-lookup"><span data-stu-id="f8184-124">Set up data collection</span></span>

<span data-ttu-id="f8184-125">Voordat u VM-beveiligingsconfiguraties zichtbaarheid krijgen kunt, moet u tooset van gegevensverzameling Security Center.</span><span class="sxs-lookup"><span data-stu-id="f8184-125">Before you can get visibility into VM security configurations, you need tooset up Security Center data collection.</span></span> <span data-ttu-id="f8184-126">Dit omvat het inschakelen van gegevensverzameling en het maken van een Azure storage-account toohold verzamelde gegevens.</span><span class="sxs-lookup"><span data-stu-id="f8184-126">This involves turning on data collection and creating an Azure storage account toohold collected data.</span></span> 

1. <span data-ttu-id="f8184-127">Klik op Hallo Security Center-dashboard, **beveiligingsbeleid**, en selecteer vervolgens uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="f8184-127">On hello Security Center dashboard, click **Security policy**, and then select your subscription.</span></span> 
2. <span data-ttu-id="f8184-128">Voor **gegevensverzameling**, selecteer **op**.</span><span class="sxs-lookup"><span data-stu-id="f8184-128">For **Data collection**, select **On**.</span></span>
3. <span data-ttu-id="f8184-129">selecteert u een opslagaccount toocreate **een opslagaccount kiezen**.</span><span class="sxs-lookup"><span data-stu-id="f8184-129">toocreate a storage account, select **Choose a storage account**.</span></span> <span data-ttu-id="f8184-130">Selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="f8184-130">Then, select **OK**.</span></span>
4. <span data-ttu-id="f8184-131">Op Hallo **beveiligingsbeleid** blade Selecteer **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f8184-131">On hello **Security Policy** blade, select **Save**.</span></span> 

<span data-ttu-id="f8184-132">Hallo Beveiligingscentrum data collection agent geïnstalleerd op alle virtuele machines en begint met het verzamelen van gegevens.</span><span class="sxs-lookup"><span data-stu-id="f8184-132">hello Security Center data collection agent is then installed on all VMs, and data collection begins.</span></span> 

## <a name="set-up-a-security-policy"></a><span data-ttu-id="f8184-133">Een beveiligingsbeleid instellen</span><span class="sxs-lookup"><span data-stu-id="f8184-133">Set up a security policy</span></span>

<span data-ttu-id="f8184-134">Beleidsregels voor veiligheid zijn gebruikte toodefine Hallo items waarvoor Security Center worden gegevens verzameld en worden aanbevelingen gedaan.</span><span class="sxs-lookup"><span data-stu-id="f8184-134">Security policies are used toodefine hello items for which Security Center collects data and makes recommendations.</span></span> <span data-ttu-id="f8184-135">U kunt verschillende beveiligingsvereisten beleid toodifferent sets van Azure-resources kunt toepassen.</span><span class="sxs-lookup"><span data-stu-id="f8184-135">You can apply different security policies toodifferent sets of Azure resources.</span></span> <span data-ttu-id="f8184-136">Hoewel Azure-resources worden standaard geëvalueerd tegen alle beleidsitems, kunt u afzonderlijke beleidsitems voor alle Azure-resources of voor een resourcegroep uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="f8184-136">Although by default Azure resources are evaluated against all policy items, you can turn off individual policy items for all Azure resources or for a resource group.</span></span> <span data-ttu-id="f8184-137">Zie voor gedetailleerde informatie over Security Center-beveiligingsbeleid [beveiligingsbeleid instellen in Azure Security Center](../../security-center/security-center-policies.md).</span><span class="sxs-lookup"><span data-stu-id="f8184-137">For in-depth information about Security Center security policies, see [Set security policies in Azure Security Center](../../security-center/security-center-policies.md).</span></span> 

<span data-ttu-id="f8184-138">tooset van een beveiligingsbeleid voor alle Azure-resources:</span><span class="sxs-lookup"><span data-stu-id="f8184-138">tooset up a security policy for all Azure resources:</span></span>

1. <span data-ttu-id="f8184-139">Selecteer op het Hallo-Security Center-dashboard **beveiligingsbeleid**, en selecteer vervolgens uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="f8184-139">On hello Security Center dashboard, select **Security policy**, and then select your subscription.</span></span>
2. <span data-ttu-id="f8184-140">Selecteer **preventiebeleid**.</span><span class="sxs-lookup"><span data-stu-id="f8184-140">Select **Prevention policy**.</span></span>
3. <span data-ttu-id="f8184-141">Inschakelen of uitschakelen van de beleidsitems die u wilt dat tooapply tooall Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="f8184-141">Turn on or turn off policy items that you want tooapply tooall Azure resources.</span></span>
4. <span data-ttu-id="f8184-142">Wanneer u klaar bent uw instellingen te selecteren, selecteert u **OK**.</span><span class="sxs-lookup"><span data-stu-id="f8184-142">When you're finished selecting your settings, select **OK**.</span></span>
5. <span data-ttu-id="f8184-143">Op Hallo **beveiligingsbeleid** blade Selecteer **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f8184-143">On hello **Security policy** blade, select **Save**.</span></span> 

<span data-ttu-id="f8184-144">tooset om een beleid voor een specifieke resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="f8184-144">tooset up a policy for a specific resource group:</span></span>

1. <span data-ttu-id="f8184-145">Selecteer op het Hallo-Security Center-dashboard **beveiligingsbeleid**, en selecteer vervolgens een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="f8184-145">On hello Security Center dashboard, select **Security policy**, and then select a resource group.</span></span>
2. <span data-ttu-id="f8184-146">Selecteer **preventiebeleid**.</span><span class="sxs-lookup"><span data-stu-id="f8184-146">Select **Prevention policy**.</span></span>
3. <span data-ttu-id="f8184-147">Inschakelen of uitschakelen beleidsitems gewenste tooapply toohello resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="f8184-147">Turn on or turn off policy items that you want tooapply toohello resource group.</span></span>
4. <span data-ttu-id="f8184-148">Onder **overname**, selecteer **unieke**.</span><span class="sxs-lookup"><span data-stu-id="f8184-148">Under **INHERITANCE**, select **Unique**.</span></span>
5. <span data-ttu-id="f8184-149">Wanneer u klaar bent uw instellingen te selecteren, selecteert u **OK**.</span><span class="sxs-lookup"><span data-stu-id="f8184-149">When you're finished selecting your settings, select **OK**.</span></span>
6. <span data-ttu-id="f8184-150">Op Hallo **beveiligingsbeleid** blade Selecteer **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f8184-150">On hello **Security policy** blade, select **Save**.</span></span>  

<span data-ttu-id="f8184-151">Ook kunt u uitschakelen gegevensverzameling voor een specifieke resourcegroep op deze pagina.</span><span class="sxs-lookup"><span data-stu-id="f8184-151">You also can turn off data collection for a specific resource group on this page.</span></span>

<span data-ttu-id="f8184-152">In de Hallo voorbeeld te volgen, een uniek beleid is gemaakt voor een resourcegroep met de naam *myResoureGroup*.</span><span class="sxs-lookup"><span data-stu-id="f8184-152">In hello following example, a unique policy has been created for a resource group named *myResoureGroup*.</span></span> <span data-ttu-id="f8184-153">Schijf versleutelings- en web application firewall aanbevelingen zijn in dit beleid uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="f8184-153">In this policy, disk encryption and web application firewall recommendations are turned off.</span></span>

![Unieke beleidsnaam](./media/tutorial-azure-security/unique-policy.png)

## <a name="view-vm-configuration-health"></a><span data-ttu-id="f8184-155">Configuratiestatus van weergave VM</span><span class="sxs-lookup"><span data-stu-id="f8184-155">View VM configuration health</span></span>

<span data-ttu-id="f8184-156">Nadat u hebt ingeschakeld op het verzamelen van gegevens en een beveiligingsbeleid instellen, begint Security Center tooprovide waarschuwingen en aanbevelingen.</span><span class="sxs-lookup"><span data-stu-id="f8184-156">After you've turned on data collection and set a security policy, Security Center begins tooprovide alerts and recommendations.</span></span> <span data-ttu-id="f8184-157">Als u virtuele machines zijn geïmplementeerd, is Hallo-agent voor het verzamelen van gegevens geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="f8184-157">As VMs are deployed, hello data collection agent is installed.</span></span> <span data-ttu-id="f8184-158">Security Center wordt vervolgens ingevuld met gegevens voor Hallo nieuwe virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="f8184-158">Security Center is then populated with data for hello new VMs.</span></span> <span data-ttu-id="f8184-159">Zie voor gedetailleerde informatie over de configuratiestatus VM [beveiligen van uw virtuele machines in Security Center](../../security-center/security-center-virtual-machine-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="f8184-159">For in-depth information about VM configuration health, see [Protect your VMs in Security Center](../../security-center/security-center-virtual-machine-recommendations.md).</span></span> 

<span data-ttu-id="f8184-160">Als gegevens worden verzameld, wordt de resourcestatus Hallo voor elke virtuele machine en de gerelateerde Azure-resource geaggregeerd.</span><span class="sxs-lookup"><span data-stu-id="f8184-160">As data is collected, hello resource health for each VM and related Azure resource is aggregated.</span></span> <span data-ttu-id="f8184-161">Hallo-informatie wordt weergegeven in het diagram van een gemakkelijk te lezen.</span><span class="sxs-lookup"><span data-stu-id="f8184-161">hello information is shown in an easy-to-read chart.</span></span> 

<span data-ttu-id="f8184-162">de resourcestatus tooview:</span><span class="sxs-lookup"><span data-stu-id="f8184-162">tooview resource health:</span></span>

1.  <span data-ttu-id="f8184-163">Op Hallo Security Center-dashboard, onder **resourcebeveiligingsstatus**, selecteer **Compute**.</span><span class="sxs-lookup"><span data-stu-id="f8184-163">On hello Security Center dashboard, under **Resource security health**, select **Compute**.</span></span> 
2.  <span data-ttu-id="f8184-164">Op Hallo **Compute** blade Selecteer **virtuele machines**.</span><span class="sxs-lookup"><span data-stu-id="f8184-164">On hello **Compute** blade, select **Virtual machines**.</span></span> <span data-ttu-id="f8184-165">Deze weergave bevat een samenvatting van status Hallo-configuratie voor alle virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="f8184-165">This view provides a summary of hello configuration status for all your VMs.</span></span>

![Status berekenen](./media/tutorial-azure-security/compute-health.png)

<span data-ttu-id="f8184-167">toosee alle aanbevelingen voor een VM, selecteer Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="f8184-167">toosee all recommendations for a VM, select hello VM.</span></span> <span data-ttu-id="f8184-168">Aanbevelingen en het doorvoeren worden behandeld in meer detail in de volgende sectie Hallo van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="f8184-168">Recommendations and remediation are covered in more detail in hello next section of this tutorial.</span></span>

## <a name="remediate-configuration-issues"></a><span data-ttu-id="f8184-169">Problemen met de configuratie herstellen</span><span class="sxs-lookup"><span data-stu-id="f8184-169">Remediate configuration issues</span></span>

<span data-ttu-id="f8184-170">Nadat het Beveiligingscentrum gestart toopopulate met configuratiegegevens, zijn aanbevelingen gemaakt op basis van Hallo beveiligingsbeleid voor die u ingesteld.</span><span class="sxs-lookup"><span data-stu-id="f8184-170">After Security Center begins toopopulate with configuration data, recommendations are made based on hello security policy you set up.</span></span> <span data-ttu-id="f8184-171">Als een virtuele machine zonder een gekoppelde netwerkbeveiligingsgroep is ingesteld, wordt een aanbeveling bijvoorbeeld toocreate een gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f8184-171">For instance, if a VM was set up without an associated network security group, a recommendation is made toocreate one.</span></span> 

<span data-ttu-id="f8184-172">een lijst met alle aanbevelingen toosee:</span><span class="sxs-lookup"><span data-stu-id="f8184-172">toosee a list of all recommendations:</span></span> 

1. <span data-ttu-id="f8184-173">Selecteer op het Hallo-Security Center-dashboard **aanbevelingen**.</span><span class="sxs-lookup"><span data-stu-id="f8184-173">On hello Security Center dashboard, select **Recommendations**.</span></span>
2. <span data-ttu-id="f8184-174">Selecteer een specifieke aanbeveling.</span><span class="sxs-lookup"><span data-stu-id="f8184-174">Select a specific recommendation.</span></span> <span data-ttu-id="f8184-175">Er verschijnt een lijst van alle resources waarvoor Hallo aanbeveling van toepassing is.</span><span class="sxs-lookup"><span data-stu-id="f8184-175">A list of all resources for which hello recommendation applies appears.</span></span>
3. <span data-ttu-id="f8184-176">tooapply een aanbeveling, selecteer een specifieke bron.</span><span class="sxs-lookup"><span data-stu-id="f8184-176">tooapply a recommendation, select a specific resource.</span></span> 
4. <span data-ttu-id="f8184-177">Volg de instructies Hallo voor herstelstappen uit.</span><span class="sxs-lookup"><span data-stu-id="f8184-177">Follow hello instructions for remediation steps.</span></span> 

<span data-ttu-id="f8184-178">In veel gevallen Security Center biedt bruikbare stappen u kunt tooaddress een aanbeveling uitvoeren zonder Security Center.</span><span class="sxs-lookup"><span data-stu-id="f8184-178">In many cases, Security Center provides actionable steps you can take tooaddress a recommendation without leaving Security Center.</span></span> <span data-ttu-id="f8184-179">Security Center detecteert in Hallo voorbeeld te volgen, een netwerkbeveiligingsgroep met een onbeperkte inkomende regel.</span><span class="sxs-lookup"><span data-stu-id="f8184-179">In hello following example, Security Center detects a network security group that has an unrestricted inbound rule.</span></span> <span data-ttu-id="f8184-180">Op Hallo aanbeveling pagina kunt u Hallo **binnenkomende regels bewerken** knop.</span><span class="sxs-lookup"><span data-stu-id="f8184-180">On hello recommendation page, you can select hello **Edit inbound rules** button.</span></span> <span data-ttu-id="f8184-181">Hallo gebruikersinterface die benodigde toomodify Hallo regel wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f8184-181">hello UI that is needed toomodify hello rule appears.</span></span> 

![Aanbevelingen](./media/tutorial-azure-security/remediation.png)

<span data-ttu-id="f8184-183">Als de aanbevelingen zijn hersteld, worden ze gemarkeerd als opgelost.</span><span class="sxs-lookup"><span data-stu-id="f8184-183">As recommendations are remediated, they are marked as resolved.</span></span> 

## <a name="view-detected-threats"></a><span data-ttu-id="f8184-184">Weergave van gedetecteerde bedreigingen</span><span class="sxs-lookup"><span data-stu-id="f8184-184">View detected threats</span></span>

<span data-ttu-id="f8184-185">Tooresource configuratieaanbevelingen, Security Center wordt bovendien dagelijks geconstateerde waarschuwingen weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f8184-185">In addition tooresource configuration recommendations, Security Center displays threat detection alerts.</span></span> <span data-ttu-id="f8184-186">Hallo waarschuwingen beveiligingsfunctie aggregeert gegevens verzameld van elke virtuele machine, Azure VPN-logboeken en verbonden partner oplossingen toodetect bedreigingen van Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="f8184-186">hello security alerts feature aggregates data collected from each VM, Azure networking logs, and connected partner solutions toodetect security threats against Azure resources.</span></span> <span data-ttu-id="f8184-187">Zie voor gedetailleerde informatie over Security Center threat detectiemogelijkheden [Azure Security Center detectiemogelijkheden](../../security-center/security-center-detection-capabilities.md).</span><span class="sxs-lookup"><span data-stu-id="f8184-187">For in-depth information about Security Center threat detection capabilities, see [Azure Security Center detection capabilities](../../security-center/security-center-detection-capabilities.md).</span></span>

<span data-ttu-id="f8184-188">Hallo waarschuwingen beveiligingsfunctie vereist Hallo Security Center prijzen laag toobe verhoogd van *vrije* te*standaard*.</span><span class="sxs-lookup"><span data-stu-id="f8184-188">hello security alerts feature requires hello Security Center pricing tier toobe increased from *Free* too*Standard*.</span></span> <span data-ttu-id="f8184-189">Een 30-daagse **gratis proefversie** is beschikbaar wanneer u een hogere prijscategorie toothis verplaatst.</span><span class="sxs-lookup"><span data-stu-id="f8184-189">A 30-day **free trial** is available when you move toothis higher pricing tier.</span></span> 

<span data-ttu-id="f8184-190">toochange hello prijscategorie:</span><span class="sxs-lookup"><span data-stu-id="f8184-190">toochange hello pricing tier:</span></span>  

1. <span data-ttu-id="f8184-191">Klik op Hallo Security Center-dashboard, **beveiligingsbeleid**, en selecteer vervolgens uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="f8184-191">On hello Security Center dashboard, click **Security policy**, and then select your subscription.</span></span>
2. <span data-ttu-id="f8184-192">Selecteer **prijscategorie**.</span><span class="sxs-lookup"><span data-stu-id="f8184-192">Select **Pricing tier**.</span></span>
3. <span data-ttu-id="f8184-193">Selecteer de nieuwe laag hello, en selecteer vervolgens **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="f8184-193">Select hello new tier, and then select **Select**.</span></span>
4. <span data-ttu-id="f8184-194">Op Hallo **beveiligingsbeleid** blade Selecteer **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f8184-194">On hello **Security policy** blade, select **Save**.</span></span> 

<span data-ttu-id="f8184-195">Nadat u Hallo prijscategorie hebt gewijzigd, worden in Hallo beveiliging waarschuwingen grafiek toopopulate begint beveiligingsrisico's worden gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="f8184-195">After you've changed hello pricing tier, hello security alerts graph begins toopopulate as security threats are detected.</span></span>

![Beveiligingswaarschuwingen](./media/tutorial-azure-security/security-alerts.png)

<span data-ttu-id="f8184-197">Selecteer een waarschuwing tooview.</span><span class="sxs-lookup"><span data-stu-id="f8184-197">Select an alert tooview information.</span></span> <span data-ttu-id="f8184-198">U kunt bijvoorbeeld een beschrijving van Hallo threat, detectietijd hello, alle threat pogingen en Hallo aanbevolen herstel.</span><span class="sxs-lookup"><span data-stu-id="f8184-198">For example, you can see a description of hello threat, hello detection time, all threat attempts, and hello recommended remediation.</span></span> <span data-ttu-id="f8184-199">Hallo voorbeeld te volgen, zijn een RDP-brute-force-aanvallen aangetroffen, met 294 mislukte pogingen voor RDP.</span><span class="sxs-lookup"><span data-stu-id="f8184-199">In hello following example, an RDP brute-force attack was detected, with 294 failed RDP attempts.</span></span> <span data-ttu-id="f8184-200">Een aanbevolen oplossing is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="f8184-200">A recommended resolution is provided.</span></span>

![RDP-aanval](./media/tutorial-azure-security/rdp-attack.png)

## <a name="next-steps"></a><span data-ttu-id="f8184-202">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f8184-202">Next steps</span></span>
<span data-ttu-id="f8184-203">In deze zelfstudie kunt u instellen in Azure Security Center en vervolgens geëvalueerd VM's in Security Center.</span><span class="sxs-lookup"><span data-stu-id="f8184-203">In this tutorial, you set up Azure Security Center, and then reviewed VMs in Security Center.</span></span> <span data-ttu-id="f8184-204">U hebt geleerd hoe u:</span><span class="sxs-lookup"><span data-stu-id="f8184-204">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f8184-205">Verzamelen van gegevens instellen</span><span class="sxs-lookup"><span data-stu-id="f8184-205">Set up data collection</span></span>
> * <span data-ttu-id="f8184-206">Een beveiligingsbeleid instellen</span><span class="sxs-lookup"><span data-stu-id="f8184-206">Set up security policies</span></span>
> * <span data-ttu-id="f8184-207">Weergeven en oplossen van problemen met configuratie-status</span><span class="sxs-lookup"><span data-stu-id="f8184-207">View and fix configuration health issues</span></span>
> * <span data-ttu-id="f8184-208">Bekijk de gedetecteerde bedreigingen</span><span class="sxs-lookup"><span data-stu-id="f8184-208">Review detected threats</span></span>

<span data-ttu-id="f8184-209">De volgende zelfstudie toolearn toohello voor vooraf informatie over het maken van een CI/CD-pijplijn met Jenkins, GitHub en Docker.</span><span class="sxs-lookup"><span data-stu-id="f8184-209">Advance toohello next tutorial toolearn more about creating a CI/CD pipeline with Jenkins, GitHub, and Docker.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f8184-210">CI/CD-infrastructuur met Jenkins, GitHub en Docker maken</span><span class="sxs-lookup"><span data-stu-id="f8184-210">Create CI/CD infrastructure with Jenkins, GitHub, and Docker</span></span>](tutorial-jenkins-github-docker-cicd.md)

