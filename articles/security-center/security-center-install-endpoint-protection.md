---
title: aaaInstall Endpoint Protection in Azure Security Center | Microsoft Docs
description: Dit document leest u hoe tooimplement hello Azure Security Center aanbeveling ** installeren Endpoint Protection **.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 1599ad5f-d810-421d-aafc-892e831b403f
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: fea891810e042e4d4f6e55094c0cd4de013ba68a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-endpoint-protection-in-azure-security-center"></a><span data-ttu-id="1624c-103">Endpoint Protection installeren in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="1624c-103">Install Endpoint Protection in Azure Security Center</span></span>
<span data-ttu-id="1624c-104">Azure Security Center raadt endpoint protection op uw virtuele Azure-machines (VM's) te installeren als endpoint protection nog niet is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="1624c-104">Azure Security Center recommends that you install endpoint protection on your Azure virtual machines (VMs) if endpoint protection is not already enabled.</span></span> <span data-ttu-id="1624c-105">Deze aanbeveling is van toepassing tooWindows virtuele machines alleen.</span><span class="sxs-lookup"><span data-stu-id="1624c-105">This recommendation applies tooWindows VMs only.</span></span>

> [!NOTE]
> <span data-ttu-id="1624c-106">Deze voorbeeldimplementatie maakt gebruik van Microsoft Antimalware.</span><span class="sxs-lookup"><span data-stu-id="1624c-106">This example deployment uses Microsoft Antimalware.</span></span> <span data-ttu-id="1624c-107">Zie [Partner-integratie in Azure Security Center](security-center-partner-integration.md#partners-that-integrate-with-security-center) voor een lijst met partners die is geïntegreerd met Security Center.</span><span class="sxs-lookup"><span data-stu-id="1624c-107">See [Partner Integration in Azure Security Center](security-center-partner-integration.md#partners-that-integrate-with-security-center) for a list of partners integrated with Security Center.</span></span>  
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="1624c-108">Hallo aanbeveling implementeren</span><span class="sxs-lookup"><span data-stu-id="1624c-108">Implement hello recommendation</span></span>

> [!NOTE]
> <span data-ttu-id="1624c-109">Dit document bevat Hallo service met behulp van een voorbeeldimplementatie.</span><span class="sxs-lookup"><span data-stu-id="1624c-109">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="1624c-110">Dit document is niet een stapsgewijze handleiding.</span><span class="sxs-lookup"><span data-stu-id="1624c-110">This document is not a step-by-step guide.</span></span>
>
>

1. <span data-ttu-id="1624c-111">In Hallo **aanbevelingen** blade Selecteer **Endpoint Protection installeren**.</span><span class="sxs-lookup"><span data-stu-id="1624c-111">In hello **Recommendations** blade, select **Install Endpoint Protection**.</span></span>
   <span data-ttu-id="1624c-112">![Selecteer de Endpoint Protection installeren][1]</span><span class="sxs-lookup"><span data-stu-id="1624c-112">![Select Install Endpoint Protection][1]</span></span>
2. <span data-ttu-id="1624c-113">Hallo **Endpoint Protection installeren** blade wordt geopend met een lijst van virtuele machines zonder endpoint protection.</span><span class="sxs-lookup"><span data-stu-id="1624c-113">hello **Install Endpoint Protection** blade opens displaying a list of VMs without endpoint protection.</span></span> <span data-ttu-id="1624c-114">Selecteer een van de Hallo lijst Hallo virtuele machines die u wilt tooinstall endpoint protection op en klik op **installeren op virtuele machines**.</span><span class="sxs-lookup"><span data-stu-id="1624c-114">Select from hello list hello VMs that you want tooinstall endpoint protection on and click **Install on VMs**.</span></span>
   <span data-ttu-id="1624c-115">![Selecteer VMs tooinstall Endpoint Protection op][2]</span><span class="sxs-lookup"><span data-stu-id="1624c-115">![Select VMs tooinstall Endpoint Protection on][2]</span></span>
3. <span data-ttu-id="1624c-116">Hallo **Selecteer Endpoint Protection** wordt een blade geopend tooallow u tooselect Hallo oplossing voor eindpuntbeveiliging gewenste toouse.</span><span class="sxs-lookup"><span data-stu-id="1624c-116">hello **Select Endpoint Protection** blade opens tooallow you tooselect hello endpoint protection solution you want toouse.</span></span> <span data-ttu-id="1624c-117">In dit voorbeeld gaan we selecteren **Microsoft Antimalware**.</span><span class="sxs-lookup"><span data-stu-id="1624c-117">In this example, let's select **Microsoft Antimalware**.</span></span>
   <span data-ttu-id="1624c-118">![Selecteer de Endpoint Protection][3]</span><span class="sxs-lookup"><span data-stu-id="1624c-118">![Select Endpoint Protection][3]</span></span>
4. <span data-ttu-id="1624c-119">Meer informatie over de oplossing voor eindpuntbeveiliging hello wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="1624c-119">Additional information about hello endpoint protection solution is displayed.</span></span> <span data-ttu-id="1624c-120">Selecteer **Maken**.</span><span class="sxs-lookup"><span data-stu-id="1624c-120">Select **Create**.</span></span>
   <span data-ttu-id="1624c-121">![Maken van anti-malwareoplossing][4]</span><span class="sxs-lookup"><span data-stu-id="1624c-121">![Create antimalware solution][4]</span></span>
5. <span data-ttu-id="1624c-122">Voer Hallo vereiste configuratie-instellingen op Hallo **Add Extension** blade en selecteer vervolgens **OK**.</span><span class="sxs-lookup"><span data-stu-id="1624c-122">Enter hello required configuration settings on hello **Add Extension** blade, and then select **OK**.</span></span> <span data-ttu-id="1624c-123">toolearn meer informatie over het Hallo-configuratie-instellingen, Zie [standaard en aangepaste Antimalware configuratie](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration).</span><span class="sxs-lookup"><span data-stu-id="1624c-123">toolearn more about hello configuration settings, see [Default and Custom Antimalware Configuration](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration).</span></span>

<span data-ttu-id="1624c-124">[Microsoft Antimalware](../security/azure-security-antimalware.md) is nu actief op Hallo VMs geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="1624c-124">[Microsoft Antimalware](../security/azure-security-antimalware.md) is now active on hello selected VMs.</span></span>

## <a name="see-also"></a><span data-ttu-id="1624c-125">Zie ook</span><span class="sxs-lookup"><span data-stu-id="1624c-125">See also</span></span>
<span data-ttu-id="1624c-126">In dit artikel hebt u geleerd hoe tooimplement Hallo Security Center aanbeveling "Endpoint Protection installeren."</span><span class="sxs-lookup"><span data-stu-id="1624c-126">This article showed you how tooimplement hello Security Center recommendation "Install Endpoint Protection."</span></span> <span data-ttu-id="1624c-127">toolearn meer informatie over het inschakelen van Microsoft Antimalware in Azure, Zie Hallo document te volgen:</span><span class="sxs-lookup"><span data-stu-id="1624c-127">toolearn more about enabling Microsoft Antimalware in Azure, see hello following document:</span></span>

* <span data-ttu-id="1624c-128">[Microsoft Antimalware voor Cloudservices en virtuele Machines](../security/azure-security-antimalware.md) --meer informatie over hoe Microsoft Antimalware toodeploy.</span><span class="sxs-lookup"><span data-stu-id="1624c-128">[Microsoft Antimalware for Cloud Services and Virtual Machines](../security/azure-security-antimalware.md) -- Learn how toodeploy Microsoft Antimalware.</span></span>

<span data-ttu-id="1624c-129">toolearn meer informatie over Security Center, Zie Hallo documenten te volgen:</span><span class="sxs-lookup"><span data-stu-id="1624c-129">toolearn more about Security Center, see hello following documents:</span></span>

* <span data-ttu-id="1624c-130">[Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md) --meer informatie over hoe tooconfigure beveiligingsbeleid.</span><span class="sxs-lookup"><span data-stu-id="1624c-130">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies.</span></span>
* <span data-ttu-id="1624c-131">[Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md) --Leer hoe aanbevelingen u uw Azure-resources te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="1624c-131">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="1624c-132">[Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md) --meer informatie over hoe toomonitor Hallo status van uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="1624c-132">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="1624c-133">[Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md) --meer informatie over hoe toomanage en gereageerd had toosecurity waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="1624c-133">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="1624c-134">[Partneroplossingen bewaken met Azure Security Center](security-center-partner-solutions.md) --meer informatie over hoe toomonitor gezondheidsstatus van uw partneroplossingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="1624c-134">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="1624c-135">[Veelgestelde vragen over Azure Security Center](security-center-faq.md) --Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="1624c-135">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="1624c-136">[Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/) --Lees blogberichten over Azure-beveiliging en naleving.</span><span class="sxs-lookup"><span data-stu-id="1624c-136">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]:./media/security-center-install-endpoint-protection/select-install-endpoint-protection.png
[2]:./media/security-center-install-endpoint-protection/install-endpoint-protection-blade.png
[3]:./media/security-center-install-endpoint-protection/select-endpoint-protection.png
[4]:./media/security-center-install-endpoint-protection/create-antimalware-solution.png
