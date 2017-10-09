---
title: systeemupdates aaaApply in Azure Security Center | Microsoft Docs
description: Dit document leest u hoe tooimplement hello Azure Security Center aanbevelingen ** toepassen system updates ** en ** na system updates ** opnieuw opgestart.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: e5bd7f55-38fd-4ebb-84ab-32bd60e9fa7a
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2017
ms.author: terrylan
ms.openlocfilehash: 02024f1558b4758c09141fe1934c2e1a9845cc96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="apply-system-updates-in-azure-security-center"></a><span data-ttu-id="c1cd3-103">Systeemupdates in Azure Security Center toepassen</span><span class="sxs-lookup"><span data-stu-id="c1cd3-103">Apply system updates in Azure Security Center</span></span>
<span data-ttu-id="c1cd3-104">Azure Security Center bewaakt dagelijks Windows en Linux virtuele machines (VM's) voor besturingssysteemupdates ontbreken.</span><span class="sxs-lookup"><span data-stu-id="c1cd3-104">Azure Security Center monitors daily Windows and  Linux virtual machines (VMs) for missing operating system updates.</span></span> <span data-ttu-id="c1cd3-105">Security Center haalt een lijst met beschikbare beveiligingsupdates en essentiële updates via Windows Update of Windows Server Update Services (WSUS), afhankelijk van welke service is geconfigureerd op een virtuele machine van Windows.</span><span class="sxs-lookup"><span data-stu-id="c1cd3-105">Security Center retrieves a list of available security and critical updates from Windows Update or Windows Server Update Services (WSUS), depending on which service is configured on a Windows VM.</span></span>  <span data-ttu-id="c1cd3-106">Security Center controleert ook of de meest recente updates Hallo in Linux-systemen.</span><span class="sxs-lookup"><span data-stu-id="c1cd3-106">Security Center also checks for hello latest updates in Linux systems.</span></span> <span data-ttu-id="c1cd3-107">Als uw VM een systeemupdate ontbreekt is, wordt Security Center aangeraden systeemupdates</span><span class="sxs-lookup"><span data-stu-id="c1cd3-107">If your VM is missing a system update, Security Center will recommend that you apply system updates</span></span>

> [!NOTE]
> <span data-ttu-id="c1cd3-108">Dit document bevat Hallo service met behulp van een voorbeeldimplementatie.</span><span class="sxs-lookup"><span data-stu-id="c1cd3-108">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="c1cd3-109">Dit is geen stapsgewijze handleiding.</span><span class="sxs-lookup"><span data-stu-id="c1cd3-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="c1cd3-110">Hallo aanbeveling implementeren</span><span class="sxs-lookup"><span data-stu-id="c1cd3-110">Implement hello recommendation</span></span>
1. <span data-ttu-id="c1cd3-111">In Hallo **aanbevelingen** blade Selecteer **toepassen systeemupdates**.</span><span class="sxs-lookup"><span data-stu-id="c1cd3-111">In hello **Recommendations** blade, select **Apply system updates**.</span></span>

   ![Systeemupdates toepassen][1]
2. <span data-ttu-id="c1cd3-113">Hallo **toepassen systeemupdates** blade wordt geopend met een lijst van ontbrekende systeemupdates virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="c1cd3-113">hello **Apply system updates** blade opens displaying a list of VMs missing system updates.</span></span> <span data-ttu-id="c1cd3-114">Selecteer een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c1cd3-114">Select a VM.</span></span>

   ![Selecteer een virtuele machine][2]
3. <span data-ttu-id="c1cd3-116">Er wordt een blade geopend met een lijst van ontbrekende updates voor die VM.</span><span class="sxs-lookup"><span data-stu-id="c1cd3-116">A blade opens displaying a list of missing updates for that VM.</span></span> <span data-ttu-id="c1cd3-117">Selecteer een systeemupdate.</span><span class="sxs-lookup"><span data-stu-id="c1cd3-117">Select a system update.</span></span> <span data-ttu-id="c1cd3-118">In dit voorbeeld gaan we KB3156016 selecteren.</span><span class="sxs-lookup"><span data-stu-id="c1cd3-118">In this example, let’s select KB3156016.</span></span>

   ![Ontbrekende beveiligingsupdates][3]

4. <span data-ttu-id="c1cd3-120">Volg de stappen Hallo in Hallo **beveiligingsupdate** blade tooapply Hallo update ontbreekt.</span><span class="sxs-lookup"><span data-stu-id="c1cd3-120">Follow hello steps in hello **Security Update** blade tooapply hello missing update.</span></span>

   ![Beveiligingsupdate][4]

## <a name="reboot-after-system-updates"></a><span data-ttu-id="c1cd3-122">Opnieuw opstarten na systeemupdates</span><span class="sxs-lookup"><span data-stu-id="c1cd3-122">Reboot after system updates</span></span>
1. <span data-ttu-id="c1cd3-123">Retourneren van toohello **aanbevelingen** blade.</span><span class="sxs-lookup"><span data-stu-id="c1cd3-123">Return toohello **Recommendations** blade.</span></span> <span data-ttu-id="c1cd3-124">Een nieuwe vermelding is gegenereerd nadat u systeemupdates, aangeroepen toegepast **opnieuw opgestart na systeemupdates**.</span><span class="sxs-lookup"><span data-stu-id="c1cd3-124">A new entry was generated after you applied system updates, called **Reboot after system updates**.</span></span> <span data-ttu-id="c1cd3-125">Deze vermelding laat u weten dat u nodig hebt tooreboot Hallo VM toocomplete Hallo proces van het toepassen van systeemupdates.</span><span class="sxs-lookup"><span data-stu-id="c1cd3-125">This entry lets you know that you need tooreboot hello VM toocomplete hello process of applying system updates.</span></span>

   ![Opnieuw opstarten na systeemupdates][5]
2. <span data-ttu-id="c1cd3-127">Selecteer **opnieuw opgestart na systeemupdates**.</span><span class="sxs-lookup"><span data-stu-id="c1cd3-127">Select **Reboot after system updates**.</span></span> <span data-ttu-id="c1cd3-128">Hiermee opent u **opnieuw opstarten is in behandeling toocomplete systeemupdates** blade met een lijst van virtuele machines dat u nodig hebt toorestart toocomplete Hallo systeemproces-updates toepassen.</span><span class="sxs-lookup"><span data-stu-id="c1cd3-128">This opens **A restart is pending toocomplete system updates** blade displaying a list of VMs that you need toorestart toocomplete hello apply system updates process.</span></span>

   ![Opnieuw opstarten in behandeling][6]

<span data-ttu-id="c1cd3-130">Opnieuw opstarten Hallo VM van Azure toocomplete Hallo proces.</span><span class="sxs-lookup"><span data-stu-id="c1cd3-130">Restart hello VM from Azure toocomplete hello process.</span></span>

## <a name="see-also"></a><span data-ttu-id="c1cd3-131">Zie ook</span><span class="sxs-lookup"><span data-stu-id="c1cd3-131">See also</span></span>
<span data-ttu-id="c1cd3-132">toolearn meer informatie over Security Center Hallo ziet:</span><span class="sxs-lookup"><span data-stu-id="c1cd3-132">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="c1cd3-133">[Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md) --meer informatie over hoe tooconfigure beveiligingsbeleid voor uw Azure-abonnementen en resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="c1cd3-133">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="c1cd3-134">[Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md) --Leer hoe aanbevelingen u uw Azure-resources te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="c1cd3-134">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="c1cd3-135">[Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md) --meer informatie over hoe toomonitor Hallo status van uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="c1cd3-135">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="c1cd3-136">[Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md) --meer informatie over hoe toomanage en gereageerd had toosecurity waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="c1cd3-136">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="c1cd3-137">[Partneroplossingen bewaken met Azure Security Center](security-center-partner-solutions.md) --meer informatie over hoe toomonitor gezondheidsstatus van uw partneroplossingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="c1cd3-137">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="c1cd3-138">[Veelgestelde vragen over Azure Security Center](security-center-faq.md) --Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="c1cd3-138">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="c1cd3-139">[Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/) --Lees blogberichten over Azure-beveiliging en naleving.</span><span class="sxs-lookup"><span data-stu-id="c1cd3-139">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-apply-system-updates/recommendation.png
[2]:./media/security-center-apply-system-updates/select-vm.png
[3]: ./media/security-center-apply-system-updates/missing-security-updates.png
[4]: ./media/security-center-apply-system-updates/security-update.png
[5]: ./media/security-center-apply-system-updates/reboot-after-system-updates.png
[6]: ./media/security-center-apply-system-updates/restart-pending.png
