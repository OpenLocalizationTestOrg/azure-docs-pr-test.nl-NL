---
title: Ontkoppelen van Azure Automation-account van logboekanalyse | Microsoft Docs
description: Dit artikel bevat een overzicht van hoe u uw Azure Automation-account van een OMS-werkruimte te ontkoppelen.
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
ms.openlocfilehash: 56b09c2cfc14813b5efcb364c580787fec1bf639
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-unlink-your-automation-account-from-a-log-analytics-workspace"></a><span data-ttu-id="6e835-103">Het ontkoppelen van uw Automation-account van een werkruimte voor logboekanalyse</span><span class="sxs-lookup"><span data-stu-id="6e835-103">How to unlink your Automation account from a Log Analytics workspace</span></span>

<span data-ttu-id="6e835-104">Azure Automation worden geïntegreerd met logboekanalyse voor het niet alleen ondersteuning voor proactieve controle van uw runbooktaken voor alle Automation-accounts, maar is ook vereist als u de volgende oplossingen die afhankelijk van logboekanalyse zijn importeren:</span><span class="sxs-lookup"><span data-stu-id="6e835-104">Azure Automation integrates with Log Analytics to not only support proactive monitoring of your runbook jobs across all of your Automation accounts, but is also required when you import the following solutions that are dependent on Log Analytics:</span></span>

* [<span data-ttu-id="6e835-105">Updatebeheer</span><span class="sxs-lookup"><span data-stu-id="6e835-105">Update Management</span></span>](../operations-management-suite/oms-solution-update-management.md)
* [<span data-ttu-id="6e835-106">Tracering wijzigen</span><span class="sxs-lookup"><span data-stu-id="6e835-106">Change Tracking</span></span>](../log-analytics/log-analytics-change-tracking.md)
* [<span data-ttu-id="6e835-107">Virtuele machines starten/stoppen buiten kantooruren</span><span class="sxs-lookup"><span data-stu-id="6e835-107">Start/Stop VMs during off-hours</span></span>](automation-solution-vm-management.md)
 
<span data-ttu-id="6e835-108">Als u dat u niet langer wilt integreren van uw Automation-account met Log Analytics besluit, kunt u uw account rechtstreeks vanuit de Azure portal kunt ontkoppelen.</span><span class="sxs-lookup"><span data-stu-id="6e835-108">If you decide you no longer wish to integrate your Automation account with Log Analytics, you can unlink your account directly from the Azure portal.</span></span>  <span data-ttu-id="6e835-109">Voordat u doorgaat, moet u eerst te verwijderen van de oplossingen die eerder vermeld, anders dit proces zal worden voorkomen dat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="6e835-109">Before you proceed, you will first need to remove the solutions mentioned earlier, otherwise this process will be prevented from proceeding.</span></span>  <span data-ttu-id="6e835-110">Bekijk het onderwerp voor de specifieke oplossing die u hebt geïmporteerd voor informatie over de stappen die nodig zijn om deze te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="6e835-110">Review the topic for the particular solution you have imported to understand the steps required to remove it.</span></span>  

<span data-ttu-id="6e835-111">U kunt de volgende stappen voor het ontkoppelen van uw Automation-account uitvoeren na het verwijderen van deze oplossingen.</span><span class="sxs-lookup"><span data-stu-id="6e835-111">After you remove these solutions you can perform the following steps to unlink your Automation account.</span></span>

## <a name="unlink-workspace"></a><span data-ttu-id="6e835-112">Ontkoppelen van de werkruimte</span><span class="sxs-lookup"><span data-stu-id="6e835-112">Unlink workspace</span></span>

1. <span data-ttu-id="6e835-113">Open uw Automation-account van de Azure-portal en selecteer in de blade Automation-account in de blade-account **ontkoppelen werkruimte**.</span><span class="sxs-lookup"><span data-stu-id="6e835-113">From the Azure portal, open your Automation account, and in the Automation account blade, in the account blade, select **Unlink workspace**.</span></span><br><br> <span data-ttu-id="6e835-114">![Werkruimte optie ontkoppelen](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)</span><span class="sxs-lookup"><span data-stu-id="6e835-114">![Unlink workspace option](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)</span></span><br><br>  
2. <span data-ttu-id="6e835-115">Klik op de blade van de werkruimte ontkoppelen **worksapce ontkoppelen**.</span><span class="sxs-lookup"><span data-stu-id="6e835-115">On the Unlink workspace blade, click **Unlink worksapce**.</span></span><br><br> <span data-ttu-id="6e835-116">![Ontkoppelen van de werkruimte blade](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).</span><span class="sxs-lookup"><span data-stu-id="6e835-116">![Unlink workspace blade](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).</span></span><br><br>  <span data-ttu-id="6e835-117">U ontvangt een prompt waarin u wordt gevraagd of u wilt doorgaan.</span><span class="sxs-lookup"><span data-stu-id="6e835-117">You will receive a prompt verifying you wish to proceed.</span></span><br><br>
3. <span data-ttu-id="6e835-118">Terwijl Azure Automation probeert te ontkoppelen van het account werkruimte voor logboekanalyse, u kunt de voortgang volgen onder **meldingen** in het menu.</span><span class="sxs-lookup"><span data-stu-id="6e835-118">While Azure Automation attempts to unlink the account your Log Analytics workspace, you can track the progress under **Notifications** from the menu.</span></span>

<span data-ttu-id="6e835-119">Als u de Update-beheeroplossing gebruikt, eventueel u mogelijk wilt verwijderen van de volgende items die niet langer nodig zijn na het verwijderen van de oplossing.</span><span class="sxs-lookup"><span data-stu-id="6e835-119">If you used the Update Management solution, optionally you may want to remove the following items that are no longer needed after you remove the solution.</span></span>

* <span data-ttu-id="6e835-120">Schema's worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="6e835-120">Update schedules.</span></span>  <span data-ttu-id="6e835-121">Elk moeten namen die overeenkomen met de update-implementaties die u hebt gemaakt)</span><span class="sxs-lookup"><span data-stu-id="6e835-121">Each will have names that match the update deployments you created)</span></span>

* <span data-ttu-id="6e835-122">Hybrid worker-groepen is gemaakt voor de oplossing.</span><span class="sxs-lookup"><span data-stu-id="6e835-122">Hybrid worker groups created for the solution.</span></span>  <span data-ttu-id="6e835-123">Elke naam op dezelfde manier naar machine1.contoso.com_9ceb8108 - 26 c 9-4051-b6b3-227600d715c8).</span><span class="sxs-lookup"><span data-stu-id="6e835-123">Each will be named similarly to  machine1.contoso.com_9ceb8108-26c9-4051-b6b3-227600d715c8).</span></span>

<span data-ttu-id="6e835-124">Als u de starten/stoppen virtuele machines tijdens rustige uren oplossing gebruikt, eventueel u mogelijk wilt verwijderen van de volgende items die niet langer nodig zijn na het verwijderen van de oplossing.</span><span class="sxs-lookup"><span data-stu-id="6e835-124">If you used the Start/Stop VMs during off-hours solution, optionally you may want to remove the following items that are no longer needed after you remove the solution.</span></span>

* <span data-ttu-id="6e835-125">Starten en stoppen van runbook-planningen VM</span><span class="sxs-lookup"><span data-stu-id="6e835-125">Start and stop VM runbook schedules</span></span> 
* <span data-ttu-id="6e835-126">VM-runbooks starten en stoppen</span><span class="sxs-lookup"><span data-stu-id="6e835-126">Start and stop VM runbooks</span></span>
* <span data-ttu-id="6e835-127">Variabelen</span><span class="sxs-lookup"><span data-stu-id="6e835-127">Variables</span></span>   

## <a name="next-steps"></a><span data-ttu-id="6e835-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6e835-128">Next steps</span></span>

<span data-ttu-id="6e835-129">Als u wilt uw Automation-account om te integreren met logboekanalyse OMS configureren, Zie [doorsturen taakstatus en taak stromen van Automation voor logboekanalyse (OMS)](automation-manage-send-joblogs-log-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="6e835-129">To reconfigure your Automation account to integrate with OMS Log Analytics, see [Forward job status and job streams from Automation to Log Analytics (OMS)](automation-manage-send-joblogs-log-analytics.md).</span></span> 