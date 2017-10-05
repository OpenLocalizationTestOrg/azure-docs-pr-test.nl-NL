---
title: Azure Backup gebruiken ter vervanging van uw tape-infrastructuur | Microsoft Docs
description: Meer informatie over hoe Azure Backup biedt tape-achtige-semantiek waardoor u back-up en herstellen van gegevens in Azure
services: backup
documentationcenter: 
author: trinadhk
manager: vijayts
editor: 
ms.assetid: 2e1bb67d-986c-4437-8056-3a63169b4214
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 1/10/2017
ms.author: saurse;trinadhk;markgal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f0f3152daf5f91f7c9e540797bf09b21969d2d33
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="move-your-long-term-storage-from-tape-to-the-azure-cloud"></a><span data-ttu-id="be4f3-103">Uw langetermijnopslag van tape verplaatsen naar de Azure-cloud</span><span class="sxs-lookup"><span data-stu-id="be4f3-103">Move your long-term storage from tape to the Azure cloud</span></span>
<span data-ttu-id="be4f3-104">Azure back-up- en System Center Data Protection Manager-klanten kunnen:</span><span class="sxs-lookup"><span data-stu-id="be4f3-104">Azure Backup and System Center Data Protection Manager customers can:</span></span>

* <span data-ttu-id="be4f3-105">Back-up van gegevens in de schema's die het beste behoeften van de organisatie.</span><span class="sxs-lookup"><span data-stu-id="be4f3-105">Back up data in schedules which best suit the organizational needs.</span></span>
* <span data-ttu-id="be4f3-106">De back-upgegevens voor langere tijd behouden</span><span class="sxs-lookup"><span data-stu-id="be4f3-106">Retain the backup data for longer periods</span></span>
* <span data-ttu-id="be4f3-107">Controleer Azure een deel van hun lange bewaartermijn (in plaats van tape moet).</span><span class="sxs-lookup"><span data-stu-id="be4f3-107">Make Azure a part of their long-term retention needs (instead of tape).</span></span>

<span data-ttu-id="be4f3-108">Dit artikel wordt uitgelegd hoe klanten back-up en retentie beleidsregels kunnen inschakelen.</span><span class="sxs-lookup"><span data-stu-id="be4f3-108">This article explains how customers can enable backup and retention policies.</span></span> <span data-ttu-id="be4f3-109">Klanten die tapes gebruiken voor het oplossen van hun lange-termijn-bewaren moeten nu een krachtige en levensvatbaar alternatief met de beschikbaarheid van deze functie hebben.</span><span class="sxs-lookup"><span data-stu-id="be4f3-109">Customers who use tapes to address their long-term-retention needs now have a powerful and viable alternative with the availability of this feature.</span></span> <span data-ttu-id="be4f3-110">De functie is ingeschakeld in de nieuwste versie van de Azure Backup (die beschikbaar is [hier](http://aka.ms/azurebackup_agent)).</span><span class="sxs-lookup"><span data-stu-id="be4f3-110">The feature is enabled in the latest release of the Azure Backup (which is available [here](http://aka.ms/azurebackup_agent)).</span></span> <span data-ttu-id="be4f3-111">Klanten van System Center DPM moeten ten minste bijwerken, DPM 2012 R2 UR5 voordat u DPM met de Azure Backup-service.</span><span class="sxs-lookup"><span data-stu-id="be4f3-111">System Center DPM customers must update to, at least, DPM 2012 R2 UR5 before using DPM with the Azure Backup service.</span></span>

## <a name="what-is-the-backup-schedule"></a><span data-ttu-id="be4f3-112">Wat is de back-upschema?</span><span class="sxs-lookup"><span data-stu-id="be4f3-112">What is the Backup Schedule?</span></span>
<span data-ttu-id="be4f3-113">Het back-upschema geeft de frequentie van de back-upbewerking.</span><span class="sxs-lookup"><span data-stu-id="be4f3-113">The backup schedule indicates the frequency of the backup operation.</span></span> <span data-ttu-id="be4f3-114">De instellingen in het volgende scherm bijvoorbeeld aangeven dat de back-ups dagelijks om 18: 00 uur en om middernacht worden genomen.</span><span class="sxs-lookup"><span data-stu-id="be4f3-114">For example, the settings in the following screen indicate that backups are taken daily at 6pm and at midnight.</span></span>

![Dagelijks schema](./media/backup-azure-backup-cloud-as-tape/dailybackupschedule.png)

<span data-ttu-id="be4f3-116">Klanten kunnen ook een wekelijkse back-up plannen.</span><span class="sxs-lookup"><span data-stu-id="be4f3-116">Customers can also schedule a weekly backup.</span></span> <span data-ttu-id="be4f3-117">De instellingen in het volgende scherm geven bijvoorbeeld back-ups elke alternatieve zondag & woensdag op 9:30:00 uur en 1:00 uur zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="be4f3-117">For example, the settings in the following screen indicate that backups are taken every alternate Sunday & Wednesday at 9:30AM and 1:00AM.</span></span>

![Wekelijkse planning](./media/backup-azure-backup-cloud-as-tape/weeklybackupschedule.png)

## <a name="what-is-the-retention-policy"></a><span data-ttu-id="be4f3-119">Wat is het bewaarbeleid?</span><span class="sxs-lookup"><span data-stu-id="be4f3-119">What is the Retention Policy?</span></span>
<span data-ttu-id="be4f3-120">Het bewaarbeleid geeft de duur waarvoor de back-up moet worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="be4f3-120">The retention policy specifies the duration for which the backup must be stored.</span></span> <span data-ttu-id="be4f3-121">In plaats van alleen 'plat beleid' voor alle back-uppunten opgeeft, kunnen klanten verschillende Bewaarbeleidsregels op basis van wanneer de back-up is gemaakt opgeven.</span><span class="sxs-lookup"><span data-stu-id="be4f3-121">Rather than just specifying a “flat policy” for all backup points, customers can specify different retention policies based on when the backup is taken.</span></span> <span data-ttu-id="be4f3-122">Bijvoorbeeld blijft dagelijks, uitgevoerde back-uppunt die als een operationele herstelpunt maakt fungeert, behouden gedurende 90 dagen.</span><span class="sxs-lookup"><span data-stu-id="be4f3-122">For example, the backup point taken daily, which serves as an operational recovery point, is preserved for 90 days.</span></span> <span data-ttu-id="be4f3-123">Het back-punt aan het einde van elk kwartaal voor auditdoeleinden genomen blijft behouden gedurende een langere periode.</span><span class="sxs-lookup"><span data-stu-id="be4f3-123">The backup point taken at the end of each quarter for audit purposes is preserved for a longer duration.</span></span>

![Bewaarbeleid](./media/backup-azure-backup-cloud-as-tape/retentionpolicy.png)

<span data-ttu-id="be4f3-125">Het totale aantal 'bewaarpunten' opgegeven in dit beleid is 90 (punten per dag) + 40 (elk kwartaal tien jaar) = 130.</span><span class="sxs-lookup"><span data-stu-id="be4f3-125">The total number of “retention points” specified in this policy is 90 (daily points) + 40 (one each quarter for 10 years) = 130.</span></span>

## <a name="example--putting-both-together"></a><span data-ttu-id="be4f3-126">Voorbeeld: het samenstellen van beide</span><span class="sxs-lookup"><span data-stu-id="be4f3-126">Example – Putting both together</span></span>
![Voorbeeldscherm](./media/backup-azure-backup-cloud-as-tape/samplescreen.png)

1. <span data-ttu-id="be4f3-128">**Dagelijkse bewaarbeleid**: back-ups dagelijks die zijn opgeslagen voor de zeven dagen.</span><span class="sxs-lookup"><span data-stu-id="be4f3-128">**Daily retention policy**: Backups taken daily are stored for seven days.</span></span>
2. <span data-ttu-id="be4f3-129">**Wekelijkse bewaarbeleid**: back-ups die elke dag om middernacht en 18: 00 uur zaterdag bewaard voor vier weken</span><span class="sxs-lookup"><span data-stu-id="be4f3-129">**Weekly retention policy**: Backups taken every day at midnight and 6PM Saturday are preserved for four weeks</span></span>
3. <span data-ttu-id="be4f3-130">**Maandelijkse bewaarbeleid**: back-ups die op middernacht en 18: 00 uur op de laatste zaterdag van elke maand worden bewaard gedurende 12 maanden</span><span class="sxs-lookup"><span data-stu-id="be4f3-130">**Monthly retention policy**: Backups taken at midnight and 6pm on the last Saturday of each month are preserved for 12 months</span></span>
4. <span data-ttu-id="be4f3-131">**Jaarlijks bewaarbeleid**: back-ups die op de laatste zaterdag van elke maart om middernacht tien jaar worden bewaard</span><span class="sxs-lookup"><span data-stu-id="be4f3-131">**Yearly retention policy**: Backups taken at midnight on the last Saturday of every March are preserved for 10 years</span></span>

<span data-ttu-id="be4f3-132">Het totale aantal 'bewaarpunten' (punten waaruit een klant kunt gegevens herstellen) in het voorgaande diagram wordt berekend als volgt:</span><span class="sxs-lookup"><span data-stu-id="be4f3-132">The total number of “retention points” (points from which a customer can restore data) in the preceding diagram is computed as follows:</span></span>

* <span data-ttu-id="be4f3-133">twee beheerpunten herstelpunten per dag voor de zeven dagen = 14</span><span class="sxs-lookup"><span data-stu-id="be4f3-133">two points per day for seven days = 14 recovery points</span></span>
* <span data-ttu-id="be4f3-134">twee beheerpunten per week voor vier weken = 8 herstelpunten</span><span class="sxs-lookup"><span data-stu-id="be4f3-134">two points per week for four weeks = 8 recovery points</span></span>
* <span data-ttu-id="be4f3-135">twee beheerpunten per maand gedurende 12 maanden = 24 herstelpunten</span><span class="sxs-lookup"><span data-stu-id="be4f3-135">two points per month for 12 months = 24 recovery points</span></span>
* <span data-ttu-id="be4f3-136">één punt per jaar per 10 jaar = 10 herstel verwijst</span><span class="sxs-lookup"><span data-stu-id="be4f3-136">one point per year per 10 years = 10 recovery points</span></span>

<span data-ttu-id="be4f3-137">Het totale aantal herstelpunten is 56.</span><span class="sxs-lookup"><span data-stu-id="be4f3-137">The total number of recovery points is 56.</span></span>

> [!NOTE]
> <span data-ttu-id="be4f3-138">Azure backup heeft geen beperking op het aantal herstelpunten.</span><span class="sxs-lookup"><span data-stu-id="be4f3-138">Azure backup doesn't have a restriction on number of recovery points.</span></span>
>
>

## <a name="advanced-configuration"></a><span data-ttu-id="be4f3-139">Geavanceerde configuratie</span><span class="sxs-lookup"><span data-stu-id="be4f3-139">Advanced configuration</span></span>
<span data-ttu-id="be4f3-140">Door te klikken op **wijzigen** in het vorige scherm klanten hebben meer flexibiliteit bij het bewaarschema opgeven.</span><span class="sxs-lookup"><span data-stu-id="be4f3-140">By clicking **Modify** in the preceding screen, customers have further flexibility in specifying retention schedules.</span></span>

![Wijzigen](./media/backup-azure-backup-cloud-as-tape/modify.png)

## <a name="next-steps"></a><span data-ttu-id="be4f3-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="be4f3-142">Next Steps</span></span>
<span data-ttu-id="be4f3-143">Zie voor meer informatie over Azure Backup:</span><span class="sxs-lookup"><span data-stu-id="be4f3-143">For more information about Azure Backup, see:</span></span>

* [<span data-ttu-id="be4f3-144">Kennismaking met Azure Backup</span><span class="sxs-lookup"><span data-stu-id="be4f3-144">Introduction to Azure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="be4f3-145">Azure Backup proberen</span><span class="sxs-lookup"><span data-stu-id="be4f3-145">Try Azure Backup</span></span>](backup-try-azure-backup-in-10-mins.md)
