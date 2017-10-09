---
title: aaaWhat is Azure Scheduler? | Microsoft Docs
description: Azure Scheduler kunt u toodeclaratively beschrijven acties toorun in Hallo cloud. En vervolgens worden deze acties automatisch gepland en uitgevoerd.
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 52aa6ae1-4c3d-43fb-81b0-6792c84bcfae
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 062e25ae473510264dc0038198c05e7ac1e86210
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-scheduler"></a><span data-ttu-id="27a4c-105">Wat is Azure Scheduler?</span><span class="sxs-lookup"><span data-stu-id="27a4c-105">What is Azure Scheduler?</span></span>
<span data-ttu-id="27a4c-106">Azure Scheduler kunt u toodeclaratively beschrijven acties toorun in Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="27a4c-106">Azure Scheduler allows you toodeclaratively describe actions toorun in hello cloud.</span></span> <span data-ttu-id="27a4c-107">En vervolgens worden deze acties automatisch gepland en uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="27a4c-107">It then schedules and runs those actions automatically.</span></span>  <span data-ttu-id="27a4c-108">Scheduler wordt dit met behulp van [hello Azure-portal](scheduler-get-started-portal.md), code, [REST-API](https://msdn.microsoft.com/library/mt629143.aspx), of Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="27a4c-108">Scheduler does this by using [hello Azure portal](scheduler-get-started-portal.md), code, [REST API](https://msdn.microsoft.com/library/mt629143.aspx), or Azure PowerShell.</span></span>

<span data-ttu-id="27a4c-109">Scheduler maakt, onderhoudt en roept gepland werk aan.</span><span class="sxs-lookup"><span data-stu-id="27a4c-109">Scheduler creates, maintains, and invokes scheduled work.</span></span>  <span data-ttu-id="27a4c-110">Scheduler host geen workloads en voert geen programmacode uit.</span><span class="sxs-lookup"><span data-stu-id="27a4c-110">Scheduler does not host any workloads or run any code.</span></span> <span data-ttu-id="27a4c-111">Scheduler *roept* programmacode aan die elders wordt gehost, in Azure, on-premises of bij een andere provider.</span><span class="sxs-lookup"><span data-stu-id="27a4c-111">It only *invokes* code hosted elsewhere—in Azure, on-premises, or with another provider.</span></span> <span data-ttu-id="27a4c-112">Dit aanroepen gebeurt via HTTP, HTTPS, een opslagwachtrij, een Service Bus-wachtrij of een Service Bus-onderwerp.</span><span class="sxs-lookup"><span data-stu-id="27a4c-112">It invokes via HTTP, HTTPS, a storage queue, a service bus queue, or a service bus topic.</span></span>

<span data-ttu-id="27a4c-113">Scheduler planningen [taken](scheduler-concepts-terms.md), resultaten van taken in het verleden bijgehouden dat een bekijken kunt en deterministisch en betrouwbaar planningen werkbelastingen toobe uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="27a4c-113">Scheduler schedules [jobs](scheduler-concepts-terms.md), keeps a history of job execution results that one can review, and deterministically and reliably schedules workloads toobe run.</span></span> <span data-ttu-id="27a4c-114">Azure WebJobs (onderdeel van de functie van de Hallo Web Apps in Azure App Service) en andere mogelijkheden van Azure Scheduler gebruik van Scheduler op Hallo achtergrond.</span><span class="sxs-lookup"><span data-stu-id="27a4c-114">Azure WebJobs (part of hello Web Apps feature in Azure App Service) and other Azure scheduling capabilities use Scheduler in hello background.</span></span> <span data-ttu-id="27a4c-115">Hallo [Scheduler REST API](https://msdn.microsoft.com/library/mt629143.aspx) helpt bij het beheer Hallo communicatie voor deze acties.</span><span class="sxs-lookup"><span data-stu-id="27a4c-115">hello [Scheduler REST API](https://msdn.microsoft.com/library/mt629143.aspx) helps manage hello communication for these actions.</span></span> <span data-ttu-id="27a4c-116">Als zodanig ondersteunt Scheduler met gemak [complexe schema's en geavanceerde terugkeerpatronen](scheduler-advanced-complexity.md).</span><span class="sxs-lookup"><span data-stu-id="27a4c-116">As such, Scheduler supports [complex schedules and advanced recurrence](scheduler-advanced-complexity.md) easily.</span></span>

<span data-ttu-id="27a4c-117">Er zijn verschillende scenario's die zich goed toohello gebruik van Scheduler lenen.</span><span class="sxs-lookup"><span data-stu-id="27a4c-117">There are several scenarios that lend themselves toohello usage of Scheduler.</span></span> <span data-ttu-id="27a4c-118">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="27a4c-118">For example:</span></span>

* <span data-ttu-id="27a4c-119">*Terugkerende acties van toepassingen*: periodiek verzamelen van gegevens van Twitter in een feed.</span><span class="sxs-lookup"><span data-stu-id="27a4c-119">*Recurring application actions:* Periodically gathering data from Twitter into a feed.</span></span>
* <span data-ttu-id="27a4c-120">*Dagelijks onderhoud*: het dagelijks verwijderen van logboeken, het uitvoeren van back-ups en overige onderhoudstaken.</span><span class="sxs-lookup"><span data-stu-id="27a4c-120">*Daily maintenance:* Daily pruning of logs, performing backups, and other maintenance tasks.</span></span> <span data-ttu-id="27a4c-121">Een beheerder kan bijvoorbeeld tooback Hallo updatabase kiezen om 1:00 uur</span><span class="sxs-lookup"><span data-stu-id="27a4c-121">For example, an administrator may choose tooback up hello database at 1:00 A.M.</span></span> <span data-ttu-id="27a4c-122">dagelijks op Hallo volgende negen maanden.</span><span class="sxs-lookup"><span data-stu-id="27a4c-122">every day for hello next nine months.</span></span>

<span data-ttu-id="27a4c-123">Scheduler kunt u toocreate, bijwerken, verwijderen, weergeven en beheren van taken en [taakverzamelingen](scheduler-concepts-terms.md) programmatisch met behulp van scripts en in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="27a4c-123">Scheduler allows you toocreate, update, delete, view, and manage jobs and [job collections](scheduler-concepts-terms.md) programmatically, by using scripts, and in hello portal.</span></span>

## <a name="see-also"></a><span data-ttu-id="27a4c-124">Zie ook</span><span class="sxs-lookup"><span data-stu-id="27a4c-124">See also</span></span>
 [<span data-ttu-id="27a4c-125">Azure Scheduler-concepten, -terminologie en -entiteitenhiërarchie</span><span class="sxs-lookup"><span data-stu-id="27a4c-125">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="27a4c-126">Aan de slag met behulp van Scheduler in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="27a4c-126">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="27a4c-127">Plannen en facturering in Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="27a4c-127">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="27a4c-128">Hoe plant u toobuild complexe en geavanceerde terugkeerpatronen met Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="27a4c-128">How toobuild complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="27a4c-129">Naslaginformatie over REST API van Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="27a4c-129">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="27a4c-130">Naslaginformatie over Azure Scheduler PowerShell-cmdlets</span><span class="sxs-lookup"><span data-stu-id="27a4c-130">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="27a4c-131">Hoge beschikbaarheid en betrouwbaarheid van Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="27a4c-131">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="27a4c-132">Azure Scheduler-limieten, standaardwaarden en foutcodes</span><span class="sxs-lookup"><span data-stu-id="27a4c-132">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="27a4c-133">Azure Scheduler uitgaande verificatie</span><span class="sxs-lookup"><span data-stu-id="27a4c-133">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

