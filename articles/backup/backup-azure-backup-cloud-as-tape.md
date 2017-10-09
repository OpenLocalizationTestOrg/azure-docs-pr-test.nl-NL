---
title: Azure Backup-tooreplace aaaUse uw tape-infrastructuur | Microsoft Docs
description: Informatie over hoe Azure Backup biedt tape-achtige-semantiek waardoor u toobackup en het herstellen van gegevens in Azure
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
ms.openlocfilehash: 4c5b095d95d39267c54b1eed9427bda09658bb94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-your-long-term-storage-from-tape-toohello-azure-cloud"></a><span data-ttu-id="b5a52-103">Uw langdurige opslag verplaatsen van tape toohello Azure-cloud</span><span class="sxs-lookup"><span data-stu-id="b5a52-103">Move your long-term storage from tape toohello Azure cloud</span></span>
<span data-ttu-id="b5a52-104">Azure back-up- en System Center Data Protection Manager-klanten kunnen:</span><span class="sxs-lookup"><span data-stu-id="b5a52-104">Azure Backup and System Center Data Protection Manager customers can:</span></span>

* <span data-ttu-id="b5a52-105">Maak een back-up van gegevens in de schema's die het best past bij Hallo organisatorische behoeften.</span><span class="sxs-lookup"><span data-stu-id="b5a52-105">Back up data in schedules which best suit hello organizational needs.</span></span>
* <span data-ttu-id="b5a52-106">Back-upgegevens Hallo behouden voor langere tijd</span><span class="sxs-lookup"><span data-stu-id="b5a52-106">Retain hello backup data for longer periods</span></span>
* <span data-ttu-id="b5a52-107">Controleer Azure een deel van hun lange bewaartermijn (in plaats van tape moet).</span><span class="sxs-lookup"><span data-stu-id="b5a52-107">Make Azure a part of their long-term retention needs (instead of tape).</span></span>

<span data-ttu-id="b5a52-108">Dit artikel wordt uitgelegd hoe klanten back-up en retentie beleidsregels kunnen inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b5a52-108">This article explains how customers can enable backup and retention policies.</span></span> <span data-ttu-id="b5a52-109">Klanten die gebruikmaken van tapes tooaddress hun lange-termijn-bewaren moet beschikt nu over een krachtige en levensvatbaar alternatief Hallo en de beschikbaarheid van deze functie.</span><span class="sxs-lookup"><span data-stu-id="b5a52-109">Customers who use tapes tooaddress their long-term-retention needs now have a powerful and viable alternative with hello availability of this feature.</span></span> <span data-ttu-id="b5a52-110">Hallo functie is ingeschakeld in de meest recente release Hallo van hello Azure Backup (die beschikbaar is [hier](http://aka.ms/azurebackup_agent)).</span><span class="sxs-lookup"><span data-stu-id="b5a52-110">hello feature is enabled in hello latest release of hello Azure Backup (which is available [here](http://aka.ms/azurebackup_agent)).</span></span> <span data-ttu-id="b5a52-111">System Center DPM klanten moeten bijwerken naar, ten minste DPM 2012 R2 UR5 voordat u DPM met hello Azure Backup-service.</span><span class="sxs-lookup"><span data-stu-id="b5a52-111">System Center DPM customers must update to, at least, DPM 2012 R2 UR5 before using DPM with hello Azure Backup service.</span></span>

## <a name="what-is-hello-backup-schedule"></a><span data-ttu-id="b5a52-112">Wat is Hallo back-upschema?</span><span class="sxs-lookup"><span data-stu-id="b5a52-112">What is hello Backup Schedule?</span></span>
<span data-ttu-id="b5a52-113">Hallo back-upschema Hallo frequentie van back-upbewerking Hallo aangeeft.</span><span class="sxs-lookup"><span data-stu-id="b5a52-113">hello backup schedule indicates hello frequency of hello backup operation.</span></span> <span data-ttu-id="b5a52-114">Hallo-instellingen in het volgende scherm Hallo bijvoorbeeld aangeven dat de back-ups dagelijks om 18: 00 uur en om middernacht worden genomen.</span><span class="sxs-lookup"><span data-stu-id="b5a52-114">For example, hello settings in hello following screen indicate that backups are taken daily at 6pm and at midnight.</span></span>

![Dagelijks schema](./media/backup-azure-backup-cloud-as-tape/dailybackupschedule.png)

<span data-ttu-id="b5a52-116">Klanten kunnen ook een wekelijkse back-up plannen.</span><span class="sxs-lookup"><span data-stu-id="b5a52-116">Customers can also schedule a weekly backup.</span></span> <span data-ttu-id="b5a52-117">Bijvoorbeeld hello instellingen in het volgende scherm Hallo aangeven dat de back-ups elke alternatieve zondag & woensdag op 9:30:00 uur en 1:00 uur worden genomen.</span><span class="sxs-lookup"><span data-stu-id="b5a52-117">For example, hello settings in hello following screen indicate that backups are taken every alternate Sunday & Wednesday at 9:30AM and 1:00AM.</span></span>

![Wekelijkse planning](./media/backup-azure-backup-cloud-as-tape/weeklybackupschedule.png)

## <a name="what-is-hello-retention-policy"></a><span data-ttu-id="b5a52-119">Wat is Hallo bewaarbeleid?</span><span class="sxs-lookup"><span data-stu-id="b5a52-119">What is hello Retention Policy?</span></span>
<span data-ttu-id="b5a52-120">Hallo bewaarbeleid geeft Hallo duur waarvoor Hallo back-up moet worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="b5a52-120">hello retention policy specifies hello duration for which hello backup must be stored.</span></span> <span data-ttu-id="b5a52-121">In plaats van alleen 'plat beleid' voor alle back-uppunten opgeeft, kunnen klanten opgeven verschillende Bewaarbeleidsregels op basis van wanneer Hallo back-up is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b5a52-121">Rather than just specifying a “flat policy” for all backup points, customers can specify different retention policies based on when hello backup is taken.</span></span> <span data-ttu-id="b5a52-122">Bijvoorbeeld, blijft Hallo back-uppunt dagelijks, genomen die als een operationele herstelpunt maakt fungeert, behouden gedurende 90 dagen.</span><span class="sxs-lookup"><span data-stu-id="b5a52-122">For example, hello backup point taken daily, which serves as an operational recovery point, is preserved for 90 days.</span></span> <span data-ttu-id="b5a52-123">Hallo back-uppunt die is genomen op Hallo einde van elk kwartaal voor auditdoeleinden blijft behouden gedurende een langere periode.</span><span class="sxs-lookup"><span data-stu-id="b5a52-123">hello backup point taken at hello end of each quarter for audit purposes is preserved for a longer duration.</span></span>

![Bewaarbeleid](./media/backup-azure-backup-cloud-as-tape/retentionpolicy.png)

<span data-ttu-id="b5a52-125">Hallo totaal aantal 'bewaarpunten' opgegeven in dit beleid is 90 (punten per dag) + 40 (elk kwartaal tien jaar) = 130.</span><span class="sxs-lookup"><span data-stu-id="b5a52-125">hello total number of “retention points” specified in this policy is 90 (daily points) + 40 (one each quarter for 10 years) = 130.</span></span>

## <a name="example--putting-both-together"></a><span data-ttu-id="b5a52-126">Voorbeeld: het samenstellen van beide</span><span class="sxs-lookup"><span data-stu-id="b5a52-126">Example – Putting both together</span></span>
![Voorbeeldscherm](./media/backup-azure-backup-cloud-as-tape/samplescreen.png)

1. <span data-ttu-id="b5a52-128">**Dagelijkse bewaarbeleid**: back-ups dagelijks die zijn opgeslagen voor de zeven dagen.</span><span class="sxs-lookup"><span data-stu-id="b5a52-128">**Daily retention policy**: Backups taken daily are stored for seven days.</span></span>
2. <span data-ttu-id="b5a52-129">**Wekelijkse bewaarbeleid**: back-ups die elke dag om middernacht en 18: 00 uur zaterdag bewaard voor vier weken</span><span class="sxs-lookup"><span data-stu-id="b5a52-129">**Weekly retention policy**: Backups taken every day at midnight and 6PM Saturday are preserved for four weeks</span></span>
3. <span data-ttu-id="b5a52-130">**Maandelijkse bewaarbeleid**: back-ups die op middernacht en 18: 00 uur op Hallo Laatste zaterdag van elke maand worden bewaard gedurende 12 maanden</span><span class="sxs-lookup"><span data-stu-id="b5a52-130">**Monthly retention policy**: Backups taken at midnight and 6pm on hello last Saturday of each month are preserved for 12 months</span></span>
4. <span data-ttu-id="b5a52-131">**Jaarlijks bewaarbeleid**: back-ups die op Hallo om middernacht Laatste zaterdag van elke maart tien jaar worden bewaard</span><span class="sxs-lookup"><span data-stu-id="b5a52-131">**Yearly retention policy**: Backups taken at midnight on hello last Saturday of every March are preserved for 10 years</span></span>

<span data-ttu-id="b5a52-132">Totaal aantal 'bewaarpunten' hello (punten waaruit een klant kunt gegevens herstellen) in Hallo voorgaande diagram als volgt berekend:</span><span class="sxs-lookup"><span data-stu-id="b5a52-132">hello total number of “retention points” (points from which a customer can restore data) in hello preceding diagram is computed as follows:</span></span>

* <span data-ttu-id="b5a52-133">twee beheerpunten herstelpunten per dag voor de zeven dagen = 14</span><span class="sxs-lookup"><span data-stu-id="b5a52-133">two points per day for seven days = 14 recovery points</span></span>
* <span data-ttu-id="b5a52-134">twee beheerpunten per week voor vier weken = 8 herstelpunten</span><span class="sxs-lookup"><span data-stu-id="b5a52-134">two points per week for four weeks = 8 recovery points</span></span>
* <span data-ttu-id="b5a52-135">twee beheerpunten per maand gedurende 12 maanden = 24 herstelpunten</span><span class="sxs-lookup"><span data-stu-id="b5a52-135">two points per month for 12 months = 24 recovery points</span></span>
* <span data-ttu-id="b5a52-136">één punt per jaar per 10 jaar = 10 herstel verwijst</span><span class="sxs-lookup"><span data-stu-id="b5a52-136">one point per year per 10 years = 10 recovery points</span></span>

<span data-ttu-id="b5a52-137">Totaal aantal herstelpunten Hallo is 56.</span><span class="sxs-lookup"><span data-stu-id="b5a52-137">hello total number of recovery points is 56.</span></span>

> [!NOTE]
> <span data-ttu-id="b5a52-138">Azure backup heeft geen beperking op het aantal herstelpunten.</span><span class="sxs-lookup"><span data-stu-id="b5a52-138">Azure backup doesn't have a restriction on number of recovery points.</span></span>
>
>

## <a name="advanced-configuration"></a><span data-ttu-id="b5a52-139">Geavanceerde configuratie</span><span class="sxs-lookup"><span data-stu-id="b5a52-139">Advanced configuration</span></span>
<span data-ttu-id="b5a52-140">Door te klikken op **wijzigen** in Hallo voorgaande scherm, klanten hebben meer flexibiliteit bij het bewaarschema opgeven.</span><span class="sxs-lookup"><span data-stu-id="b5a52-140">By clicking **Modify** in hello preceding screen, customers have further flexibility in specifying retention schedules.</span></span>

![Wijzigen](./media/backup-azure-backup-cloud-as-tape/modify.png)

## <a name="next-steps"></a><span data-ttu-id="b5a52-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b5a52-142">Next Steps</span></span>
<span data-ttu-id="b5a52-143">Zie voor meer informatie over Azure Backup:</span><span class="sxs-lookup"><span data-stu-id="b5a52-143">For more information about Azure Backup, see:</span></span>

* [<span data-ttu-id="b5a52-144">Inleiding tooAzure back-up</span><span class="sxs-lookup"><span data-stu-id="b5a52-144">Introduction tooAzure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="b5a52-145">Azure Backup proberen</span><span class="sxs-lookup"><span data-stu-id="b5a52-145">Try Azure Backup</span></span>](backup-try-azure-backup-in-10-mins.md)
