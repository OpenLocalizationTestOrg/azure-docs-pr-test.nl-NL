---
title: Toepassing systeemupdates in Azure Security Center | Microsoft Docs
description: Dit document ziet u hoe de Azure Security Center aanbevelingen implementeren ** toepassen system updates ** en ** na system updates ** opnieuw opgestart.
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
ms.openlocfilehash: 50cdea437db5387813c6a3905d14b6904d2aba34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="apply-system-updates-in-azure-security-center"></a><span data-ttu-id="72195-103">Systeemupdates in Azure Security Center toepassen</span><span class="sxs-lookup"><span data-stu-id="72195-103">Apply system updates in Azure Security Center</span></span>
<span data-ttu-id="72195-104">Azure Security Center bewaakt dagelijks Windows en Linux virtuele machines (VM's) voor besturingssysteemupdates ontbreken.</span><span class="sxs-lookup"><span data-stu-id="72195-104">Azure Security Center monitors daily Windows and  Linux virtual machines (VMs) for missing operating system updates.</span></span> <span data-ttu-id="72195-105">Security Center haalt een lijst met beschikbare beveiligingsupdates en essentiële updates via Windows Update of Windows Server Update Services (WSUS), afhankelijk van welke service is geconfigureerd op een virtuele machine van Windows.</span><span class="sxs-lookup"><span data-stu-id="72195-105">Security Center retrieves a list of available security and critical updates from Windows Update or Windows Server Update Services (WSUS), depending on which service is configured on a Windows VM.</span></span>  <span data-ttu-id="72195-106">Security Center controleert ook of de meest recente updates in de Linux-systemen.</span><span class="sxs-lookup"><span data-stu-id="72195-106">Security Center also checks for the latest updates in Linux systems.</span></span> <span data-ttu-id="72195-107">Als uw VM een systeemupdate ontbreekt is, wordt Security Center aangeraden systeemupdates</span><span class="sxs-lookup"><span data-stu-id="72195-107">If your VM is missing a system update, Security Center will recommend that you apply system updates</span></span>

> [!NOTE]
> <span data-ttu-id="72195-108">In dit document wordt de service geïntroduceerd aan de hand van een voorbeeldimplementatie.</span><span class="sxs-lookup"><span data-stu-id="72195-108">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="72195-109">Dit is geen stapsgewijze handleiding.</span><span class="sxs-lookup"><span data-stu-id="72195-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="72195-110">De aanbeveling implementeren</span><span class="sxs-lookup"><span data-stu-id="72195-110">Implement the recommendation</span></span>
1. <span data-ttu-id="72195-111">In de **aanbevelingen** blade Selecteer **toepassen systeemupdates**.</span><span class="sxs-lookup"><span data-stu-id="72195-111">In the **Recommendations** blade, select **Apply system updates**.</span></span>

   ![Systeemupdates toepassen][1]
2. <span data-ttu-id="72195-113">De **toepassen systeemupdates** blade wordt geopend met een lijst van ontbrekende systeemupdates virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="72195-113">The **Apply system updates** blade opens displaying a list of VMs missing system updates.</span></span> <span data-ttu-id="72195-114">Selecteer een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="72195-114">Select a VM.</span></span>

   ![Selecteer een virtuele machine][2]
3. <span data-ttu-id="72195-116">Er wordt een blade geopend met een lijst van ontbrekende updates voor die VM.</span><span class="sxs-lookup"><span data-stu-id="72195-116">A blade opens displaying a list of missing updates for that VM.</span></span> <span data-ttu-id="72195-117">Selecteer een systeemupdate.</span><span class="sxs-lookup"><span data-stu-id="72195-117">Select a system update.</span></span> <span data-ttu-id="72195-118">In dit voorbeeld gaan we KB3156016 selecteren.</span><span class="sxs-lookup"><span data-stu-id="72195-118">In this example, let’s select KB3156016.</span></span>

   ![Ontbrekende beveiligingsupdates][3]

4. <span data-ttu-id="72195-120">Volg de stappen in de **beveiligingsupdate** blade de ontbrekende update toe te passen.</span><span class="sxs-lookup"><span data-stu-id="72195-120">Follow the steps in the **Security Update** blade to apply the missing update.</span></span>

   ![Beveiligingsupdate][4]

## <a name="reboot-after-system-updates"></a><span data-ttu-id="72195-122">Opnieuw opstarten na systeemupdates</span><span class="sxs-lookup"><span data-stu-id="72195-122">Reboot after system updates</span></span>
1. <span data-ttu-id="72195-123">Ga terug naar de **aanbevelingen** blade.</span><span class="sxs-lookup"><span data-stu-id="72195-123">Return to the **Recommendations** blade.</span></span> <span data-ttu-id="72195-124">Een nieuwe vermelding is gegenereerd nadat u systeemupdates, aangeroepen toegepast **opnieuw opgestart na systeemupdates**.</span><span class="sxs-lookup"><span data-stu-id="72195-124">A new entry was generated after you applied system updates, called **Reboot after system updates**.</span></span> <span data-ttu-id="72195-125">Deze vermelding laat u weten dat u de virtuele machine moet voor het voltooien van het proces van het toepassen van systeemupdates opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="72195-125">This entry lets you know that you need to reboot the VM to complete the process of applying system updates.</span></span>

   ![Opnieuw opstarten na systeemupdates][5]
2. <span data-ttu-id="72195-127">Selecteer **opnieuw opgestart na systeemupdates**.</span><span class="sxs-lookup"><span data-stu-id="72195-127">Select **Reboot after system updates**.</span></span> <span data-ttu-id="72195-128">Hiermee opent u **opnieuw worden opgestart om te voltooien systeemupdates** blade met een lijst van virtuele machines die u nodig hebt om opnieuw te starten voor het voltooien van het systeem toepassen updates proces.</span><span class="sxs-lookup"><span data-stu-id="72195-128">This opens **A restart is pending to complete system updates** blade displaying a list of VMs that you need to restart to complete the apply system updates process.</span></span>

   ![Opnieuw opstarten in behandeling][6]

<span data-ttu-id="72195-130">Start opnieuw op de virtuele machine van Azure om het proces te voltooien.</span><span class="sxs-lookup"><span data-stu-id="72195-130">Restart the VM from Azure to complete the process.</span></span>

## <a name="see-also"></a><span data-ttu-id="72195-131">Zie ook</span><span class="sxs-lookup"><span data-stu-id="72195-131">See also</span></span>
<span data-ttu-id="72195-132">Zie de volgende onderwerpen voor meer informatie over het Beveiligingscentrum:</span><span class="sxs-lookup"><span data-stu-id="72195-132">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="72195-133">[Setting security policies in Azure Security Center](security-center-policies.md) (Beveiligingsbeleid instellen in Azure Security Center): leer hoe u beveiligingsbeleid voor uw Azure-abonnementen en -resourcegroepen configureert.</span><span class="sxs-lookup"><span data-stu-id="72195-133">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="72195-134">[Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md) --Leer hoe aanbevelingen u uw Azure-resources te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="72195-134">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="72195-135">[Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md) --informatie over het bewaken van de status van uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="72195-135">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="72195-136">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) (Beveiligingswaarschuwingen beheren en erop reageren in Azure Security Center): ontdek hoe u beveiligingswaarschuwingen kunt beheren en erop kunt reageren.</span><span class="sxs-lookup"><span data-stu-id="72195-136">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="72195-137">[Partneroplossingen bewaken met Azure Security Center](security-center-partner-solutions.md): leer hoe u de integriteitsstatus van uw partneroplossingen kunt bewaken.</span><span class="sxs-lookup"><span data-stu-id="72195-137">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="72195-138">[Azure Security Center FAQ](security-center-faq.md) (Veelgestelde vragen over Azure Security Center): raadpleeg veelgestelde vragen over het gebruik van de service.</span><span class="sxs-lookup"><span data-stu-id="72195-138">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="72195-139">[Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/) --Lees blogberichten over Azure-beveiliging en naleving.</span><span class="sxs-lookup"><span data-stu-id="72195-139">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-apply-system-updates/recommendation.png
[2]:./media/security-center-apply-system-updates/select-vm.png
[3]: ./media/security-center-apply-system-updates/missing-security-updates.png
[4]: ./media/security-center-apply-system-updates/security-update.png
[5]: ./media/security-center-apply-system-updates/reboot-after-system-updates.png
[6]: ./media/security-center-apply-system-updates/restart-pending.png
