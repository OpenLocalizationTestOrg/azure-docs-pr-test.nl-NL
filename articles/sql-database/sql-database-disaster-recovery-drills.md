---
title: SQL Database-Noodhersteloefeningen | Microsoft Docs
description: Meer informatie over richtlijnen en aanbevolen procedures voor het gebruik van Azure SQL Database om uit te voeren van noodhersteloefeningen om ervoor te zorgen dat uw missie kritieke zakelijke toepassingen robuuste op fouten en storingen.
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: b44a269c-fe2a-404f-b013-290030860bd1
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 07/31/2016
ms.author: sashan
ms.openlocfilehash: 1b1d65a41a794a566287dcffe3581ac58e2a965f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="performing-disaster-recovery-drill"></a><span data-ttu-id="8f5b4-103">Disaster Recovery inzoomen uitvoeren</span><span class="sxs-lookup"><span data-stu-id="8f5b4-103">Performing Disaster Recovery Drill</span></span>
<span data-ttu-id="8f5b4-104">Het is raadzaam dat validatie van de gereedheid van de toepassing voor herstelwerkstroom regelmatig wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-104">It is recommended that validation of application readiness for recovery workflow is performed periodically.</span></span> <span data-ttu-id="8f5b4-105">Verifiëren van de toepassingsgedrag en de gevolgen van het verlies van gegevens en/of de onderbreking moet u dat de failover is een goede gewoonte engineering.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-105">Verifying the application behavior and implications of data loss and/or the disruption that failover involves is a good engineering practice.</span></span> <span data-ttu-id="8f5b4-106">Het is ook een vereiste door de meeste industrienormen als onderdeel van zakelijke continuïteit-certificering.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-106">It is also a requirement by most industry standards as part of business continuity certification.</span></span>

<span data-ttu-id="8f5b4-107">Uitvoeren van een herstel na noodgevallen detailanalyse bestaat uit:</span><span class="sxs-lookup"><span data-stu-id="8f5b4-107">Performing a disaster recovery drill consists of:</span></span>

* <span data-ttu-id="8f5b4-108">Onderbreking van de laag Simulating gegevens</span><span class="sxs-lookup"><span data-stu-id="8f5b4-108">Simulating data tier outage</span></span>
* <span data-ttu-id="8f5b4-109">Herstellen</span><span class="sxs-lookup"><span data-stu-id="8f5b4-109">Recovering</span></span>
* <span data-ttu-id="8f5b4-110">Toepassingsherstel integriteit post valideren</span><span class="sxs-lookup"><span data-stu-id="8f5b4-110">Validate application integrity post recovery</span></span>

<span data-ttu-id="8f5b4-111">Afhankelijk van hoe u [ontworpen van uw toepassing voor bedrijfscontinuïteit](sql-database-business-continuity.md), de werkstroom uit te voeren van de analyse kan variëren.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-111">Depending on how you [designed your application for business continuity](sql-database-business-continuity.md), the workflow to execute the drill can vary.</span></span> <span data-ttu-id="8f5b4-112">Hieronder worden de aanbevolen procedures voor het uitvoeren van een detailanalyse van het herstel na noodgevallen in de context van Azure SQL Database beschreven.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-112">Below we describe the best practices conducting a disaster recovery drill in the context of Azure SQL Database.</span></span>

## <a name="geo-restore"></a><span data-ttu-id="8f5b4-113">Geo-herstel</span><span class="sxs-lookup"><span data-stu-id="8f5b4-113">Geo-restore</span></span>
<span data-ttu-id="8f5b4-114">De mogelijke om gegevensverlies te voorkomen wanneer de uitvoering van een herstel na noodgevallen detailanalyse, wordt u aangeraden uitvoeren met behulp van een testomgeving door een kopie van de productie-omgeving maken en deze om te controleren of de werkstroom van de toepassing van de analyse.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-114">To prevent the potential data loss when conducting a disaster recovery drill, we recommend performing the drill using a test environment by creating a copy of the production environment and using it to verify the application’s failover workflow.</span></span>

#### <a name="outage-simulation"></a><span data-ttu-id="8f5b4-115">Storing simulatie</span><span class="sxs-lookup"><span data-stu-id="8f5b4-115">Outage simulation</span></span>
<span data-ttu-id="8f5b4-116">U kunt om te simuleren de onderbreking, verwijderen of wijzig de naam van de brondatabase.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-116">To simulate the outage, you can delete or rename the source database.</span></span> <span data-ttu-id="8f5b4-117">Dit zorgt ervoor dat de problemen met de toepassingen.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-117">This causes application connectivity failures.</span></span>

#### <a name="recovery"></a><span data-ttu-id="8f5b4-118">Herstel</span><span class="sxs-lookup"><span data-stu-id="8f5b4-118">Recovery</span></span>
* <span data-ttu-id="8f5b4-119">De geo-herstel van de database in een andere server uitvoeren, zoals wordt beschreven [hier](sql-database-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="8f5b4-119">Perform the geo-restore of the database into a different server as described [here](sql-database-disaster-recovery.md).</span></span>
* <span data-ttu-id="8f5b4-120">Wijzig de configuratie van de toepassing verbinding maken met de herstelde database en volg de [configureren van een database na het herstel](sql-database-disaster-recovery.md) handleiding om het herstel te voltooien.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-120">Change the application configuration to connect to the recovered database and follow the [Configure a database after recovery](sql-database-disaster-recovery.md) guide to complete the recovery.</span></span>

#### <a name="validation"></a><span data-ttu-id="8f5b4-121">Validatie</span><span class="sxs-lookup"><span data-stu-id="8f5b4-121">Validation</span></span>
* <span data-ttu-id="8f5b4-122">Voltooien van de analyse door te controleren of de integriteit post toepassingsherstel (inclusief verbindingsreeksen, aanmeldingen, testen van de basisfunctionaliteit of andere onderdeel validaties van standaardtoepassing ondertekeningen procedures).</span><span class="sxs-lookup"><span data-stu-id="8f5b4-122">Complete the drill by verifying the application integrity post recovery (including connection strings, logins, basic functionality testing or other validations part of standard application signoffs procedures).</span></span>

## <a name="geo-replication"></a><span data-ttu-id="8f5b4-123">Geo-replicatie</span><span class="sxs-lookup"><span data-stu-id="8f5b4-123">Geo-replication</span></span>
<span data-ttu-id="8f5b4-124">Voor een database die is beveiligd met geo-replicatie moet de oefening inzoomen geplande failover naar de secundaire database.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-124">For a database that is protected using geo-replication the drill exercise involves planned failover to the secondary database.</span></span> <span data-ttu-id="8f5b4-125">De geplande failover zorgt ervoor dat de primaire en secundaire databases gesynchroniseerd blijven wanneer de rollen worden omgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-125">The planned failover ensures that the primary and the secondary databases remain in sync when the roles are switched.</span></span> <span data-ttu-id="8f5b4-126">In tegenstelling tot de niet-geplande failover resulteren deze bewerking niet in een verlies van gegevens, zodat de analyse kan worden uitgevoerd in de productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-126">Unlike the unplanned failover, this operation does not result in data loss, so the drill can be performed in the production environment.</span></span>

#### <a name="outage-simulation"></a><span data-ttu-id="8f5b4-127">Storing simulatie</span><span class="sxs-lookup"><span data-stu-id="8f5b4-127">Outage simulation</span></span>
<span data-ttu-id="8f5b4-128">Om te simuleren de onderbreking, kunt u de webtoepassing of de virtuele machine verbonden met de database uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-128">To simulate the outage, you can disable the web application or virtual machine connected to the database.</span></span> <span data-ttu-id="8f5b4-129">Dit resulteert in het verbindingsfouten voor de webserver en webclients.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-129">This results in the connectivity failures for the web clients.</span></span>

#### <a name="recovery"></a><span data-ttu-id="8f5b4-130">Herstel</span><span class="sxs-lookup"><span data-stu-id="8f5b4-130">Recovery</span></span>
* <span data-ttu-id="8f5b4-131">Zorg ervoor dat de configuratie van de toepassing in de regio DR verwijst naar de vorige secundaire de nieuwe primaire die volledig toegankelijk zijn wordt.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-131">Make sure the application configuration in the DR region points to the former secondary which becomes the fully accessible new primary.</span></span>
* <span data-ttu-id="8f5b4-132">Voer [geplande failover](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) om te maken van de secundaire database een nieuwe primaire</span><span class="sxs-lookup"><span data-stu-id="8f5b4-132">Perform [planned failover](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) to make the secondary database a new primary</span></span>
* <span data-ttu-id="8f5b4-133">Ga als volgt de [configureren van een database na het herstel](sql-database-disaster-recovery.md) handleiding om het herstel te voltooien.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-133">Follow the [Configure a database after recovery](sql-database-disaster-recovery.md) guide to complete the recovery.</span></span>

#### <a name="validation"></a><span data-ttu-id="8f5b4-134">Validatie</span><span class="sxs-lookup"><span data-stu-id="8f5b4-134">Validation</span></span>
* <span data-ttu-id="8f5b4-135">Voltooien van de analyse door te controleren of de integriteit post toepassingsherstel (inclusief verbindingsreeksen, aanmeldingen, testen van de basisfunctionaliteit of andere onderdeel validaties van standaardtoepassing ondertekeningen procedures).</span><span class="sxs-lookup"><span data-stu-id="8f5b4-135">Complete the drill by verifying the application integrity post recovery (including connection strings, logins, basic functionality testing or other validations part of standard application signoffs procedures).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f5b4-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8f5b4-136">Next steps</span></span>
* <span data-ttu-id="8f5b4-137">Zie voor meer informatie over zakelijke continuïteit-scenario's [continuïteit scenario's](sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="8f5b4-137">To learn about business continuity scenarios, see [Continuity scenarios](sql-database-business-continuity.md)</span></span>
* <span data-ttu-id="8f5b4-138">Voor meer informatie over Azure SQL Database geautomatiseerde back-ups, Zie [geautomatiseerde back-ups van SQL-Database](sql-database-automated-backups.md)</span><span class="sxs-lookup"><span data-stu-id="8f5b4-138">To learn about Azure SQL Database automated backups, see [SQL Database automated backups](sql-database-automated-backups.md)</span></span>
* <span data-ttu-id="8f5b4-139">Zie voor meer informatie over het gebruik van automatische back-ups voor herstel, [een database herstellen vanuit back-ups service is gestart](sql-database-recovery-using-backups.md)</span><span class="sxs-lookup"><span data-stu-id="8f5b4-139">To learn about using automated backups for recovery, see [restore a database from the service-initiated backups](sql-database-recovery-using-backups.md)</span></span>
* <span data-ttu-id="8f5b4-140">Zie voor meer informatie over opties voor sneller herstel, [actieve geo-replicatie](sql-database-geo-replication-overview.md)</span><span class="sxs-lookup"><span data-stu-id="8f5b4-140">To learn about faster recovery options, see [active geo-replication](sql-database-geo-replication-overview.md)</span></span>  
