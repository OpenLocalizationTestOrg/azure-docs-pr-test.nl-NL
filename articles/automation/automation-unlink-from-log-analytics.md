---
title: Azure Automation-account van logboekanalyse aaaUnlink | Microsoft Docs
description: Dit artikel bevat een overzicht van hoe toounlink uw Azure Automation-account van een OMS-werkruimte.
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: how-to-article
ms.date: 02/07/2017
ms.author: magoedte
ms.openlocfilehash: 3ec0745673f6a872538d33023a7a1d2bb1d18ec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toounlink-your-automation-account-from-a-log-analytics-workspace"></a><span data-ttu-id="829d2-103">Hoe toounlink uw Automation-account van een werkruimte voor logboekanalyse</span><span class="sxs-lookup"><span data-stu-id="829d2-103">How toounlink your Automation account from a Log Analytics workspace</span></span>

<span data-ttu-id="829d2-104">Azure Automation worden geïntegreerd met logboekanalyse toonot alleen ondersteuning voor proactieve controle van uw runbooktaken voor alle Automation-accounts, maar is ook vereist bij het importeren van oplossingen die afhankelijk van logboekanalyse zijn na Hallo:</span><span class="sxs-lookup"><span data-stu-id="829d2-104">Azure Automation integrates with Log Analytics toonot only support proactive monitoring of your runbook jobs across all of your Automation accounts, but is also required when you import hello following solutions that are dependent on Log Analytics:</span></span>

* [<span data-ttu-id="829d2-105">Updatebeheer</span><span class="sxs-lookup"><span data-stu-id="829d2-105">Update Management</span></span>](../operations-management-suite/oms-solution-update-management.md)
* [<span data-ttu-id="829d2-106">Tracering wijzigen</span><span class="sxs-lookup"><span data-stu-id="829d2-106">Change Tracking</span></span>](../log-analytics/log-analytics-change-tracking.md)
* [<span data-ttu-id="829d2-107">Virtuele machines starten/stoppen buiten kantooruren</span><span class="sxs-lookup"><span data-stu-id="829d2-107">Start/Stop VMs during off-hours</span></span>](automation-solution-vm-management.md)
 
<span data-ttu-id="829d2-108">Als u dat u niet langer wenst toointegrate uw Automation-account met Log Analytics besluit, kunt u uw account rechtstreeks vanuit hello Azure-portal kunt ontkoppelen.</span><span class="sxs-lookup"><span data-stu-id="829d2-108">If you decide you no longer wish toointegrate your Automation account with Log Analytics, you can unlink your account directly from hello Azure portal.</span></span>  <span data-ttu-id="829d2-109">Voordat u doorgaat, moet u eerst tooremove Hallo oplossingen eerder vermeld, anders dit proces zal worden voorkomen dat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="829d2-109">Before you proceed, you will first need tooremove hello solutions mentioned earlier, otherwise this process will be prevented from proceeding.</span></span>  <span data-ttu-id="829d2-110">Controleer Hallo onderwerp voor een bepaalde oplossing Hallo hebt toounderstand Hallo stappen die nodig is geïmporteerd tooremove deze.</span><span class="sxs-lookup"><span data-stu-id="829d2-110">Review hello topic for hello particular solution you have imported toounderstand hello steps required tooremove it.</span></span>  

<span data-ttu-id="829d2-111">Na het verwijderen van deze oplossingen kunt u uw Automation-account te volgen stappen toounlink Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="829d2-111">After you remove these solutions you can perform hello following steps toounlink your Automation account.</span></span>

## <a name="unlink-workspace"></a><span data-ttu-id="829d2-112">Ontkoppelen van de werkruimte</span><span class="sxs-lookup"><span data-stu-id="829d2-112">Unlink workspace</span></span>

1. <span data-ttu-id="829d2-113">Open uw Automation-account van hello Azure-portal, en selecteer in Hallo Automation-accountblade Hallo account Blade **ontkoppelen werkruimte**.</span><span class="sxs-lookup"><span data-stu-id="829d2-113">From hello Azure portal, open your Automation account, and in hello Automation account blade, in hello account blade, select **Unlink workspace**.</span></span><br><br> <span data-ttu-id="829d2-114">![Werkruimte optie ontkoppelen](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)</span><span class="sxs-lookup"><span data-stu-id="829d2-114">![Unlink workspace option](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)</span></span><br><br>  
2. <span data-ttu-id="829d2-115">Klik op Hallo ontkoppelen werkruimte blade **worksapce ontkoppelen**.</span><span class="sxs-lookup"><span data-stu-id="829d2-115">On hello Unlink workspace blade, click **Unlink worksapce**.</span></span><br><br> <span data-ttu-id="829d2-116">![Ontkoppelen van de werkruimte blade](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).</span><span class="sxs-lookup"><span data-stu-id="829d2-116">![Unlink workspace blade](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).</span></span><br><br>  <span data-ttu-id="829d2-117">U wordt gevraagd u tooproceed wilt controleren.</span><span class="sxs-lookup"><span data-stu-id="829d2-117">You will receive a prompt verifying you wish tooproceed.</span></span><br><br>
3. <span data-ttu-id="829d2-118">Terwijl Azure Automation toounlink Hallo account werkruimte voor logboekanalyse probeert, u kunt de voortgang Hallo onder volgen **meldingen** in Hallo-menu.</span><span class="sxs-lookup"><span data-stu-id="829d2-118">While Azure Automation attempts toounlink hello account your Log Analytics workspace, you can track hello progress under **Notifications** from hello menu.</span></span>

<span data-ttu-id="829d2-119">Als u Hallo updatebeheer oplossing gebruikt, kunt indien gewenst u tooremove Hallo items die niet langer nodig zijn na het verwijderen van Hallo oplossing te volgen.</span><span class="sxs-lookup"><span data-stu-id="829d2-119">If you used hello Update Management solution, optionally you may want tooremove hello following items that are no longer needed after you remove hello solution.</span></span>

* <span data-ttu-id="829d2-120">Schema's worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="829d2-120">Update schedules.</span></span>  <span data-ttu-id="829d2-121">Elk moeten namen die overeenkomen met de Hallo-update-implementaties die u hebt gemaakt)</span><span class="sxs-lookup"><span data-stu-id="829d2-121">Each will have names that match hello update deployments you created)</span></span>

* <span data-ttu-id="829d2-122">Hybrid worker-groepen is gemaakt voor Hallo-oplossing.</span><span class="sxs-lookup"><span data-stu-id="829d2-122">Hybrid worker groups created for hello solution.</span></span>  <span data-ttu-id="829d2-123">Elke naam op dezelfde manier te machine1.contoso.com_9ceb8108 - 26 c 9-4051-b6b3-227600d715c8).</span><span class="sxs-lookup"><span data-stu-id="829d2-123">Each will be named similarly too machine1.contoso.com_9ceb8108-26c9-4051-b6b3-227600d715c8).</span></span>

<span data-ttu-id="829d2-124">Als u virtuele machines starten/stoppen van Hallo tijdens rustige uren oplossing gebruikt, kunt eventueel u tooremove Hallo items die niet langer nodig zijn na het verwijderen van Hallo oplossing te volgen.</span><span class="sxs-lookup"><span data-stu-id="829d2-124">If you used hello Start/Stop VMs during off-hours solution, optionally you may want tooremove hello following items that are no longer needed after you remove hello solution.</span></span>

* <span data-ttu-id="829d2-125">Starten en stoppen van runbook-planningen VM</span><span class="sxs-lookup"><span data-stu-id="829d2-125">Start and stop VM runbook schedules</span></span> 
* <span data-ttu-id="829d2-126">VM-runbooks starten en stoppen</span><span class="sxs-lookup"><span data-stu-id="829d2-126">Start and stop VM runbooks</span></span>
* <span data-ttu-id="829d2-127">Variabelen</span><span class="sxs-lookup"><span data-stu-id="829d2-127">Variables</span></span>   

## <a name="next-steps"></a><span data-ttu-id="829d2-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="829d2-128">Next steps</span></span>

<span data-ttu-id="829d2-129">tooreconfigure uw Automation-account toointegrate met OMS Log Analytics, Zie [taakstatus en taak streams doorsturen van Automation tooLog logboekanalyse (OMS)](automation-manage-send-joblogs-log-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="829d2-129">tooreconfigure your Automation account toointegrate with OMS Log Analytics, see [Forward job status and job streams from Automation tooLog Analytics (OMS)](automation-manage-send-joblogs-log-analytics.md).</span></span> 
