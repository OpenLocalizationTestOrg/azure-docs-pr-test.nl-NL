---
title: aaaSQL Database Noodhersteloefeningen | Microsoft Docs
description: Informatie over richtlijnen en aanbevolen procedures voor het gebruik van Azure SQL Database tooperform disaster recovery zoomt toohelp Houd uw missie bedrijfskritieke toepassingen robuuste toofailures en storingen.
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
ms.openlocfilehash: bf17857a19fdebddf0d4f55e4db3a1b33efb4e8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="performing-disaster-recovery-drill"></a><span data-ttu-id="d1ba2-103">Disaster Recovery inzoomen uitvoeren</span><span class="sxs-lookup"><span data-stu-id="d1ba2-103">Performing Disaster Recovery Drill</span></span>
<span data-ttu-id="d1ba2-104">Het is raadzaam dat validatie van de gereedheid van de toepassing voor herstelwerkstroom regelmatig wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d1ba2-104">It is recommended that validation of application readiness for recovery workflow is performed periodically.</span></span> <span data-ttu-id="d1ba2-105">Gedrag van de toepassing controleren Hallo en implicaties van gegevens verloren gaan en/of Hallo onderbreking moet u dat de failover is een goede gewoonte engineering.</span><span class="sxs-lookup"><span data-stu-id="d1ba2-105">Verifying hello application behavior and implications of data loss and/or hello disruption that failover involves is a good engineering practice.</span></span> <span data-ttu-id="d1ba2-106">Het is ook een vereiste door de meeste industrienormen als onderdeel van zakelijke continuïteit-certificering.</span><span class="sxs-lookup"><span data-stu-id="d1ba2-106">It is also a requirement by most industry standards as part of business continuity certification.</span></span>

<span data-ttu-id="d1ba2-107">Uitvoeren van een herstel na noodgevallen detailanalyse bestaat uit:</span><span class="sxs-lookup"><span data-stu-id="d1ba2-107">Performing a disaster recovery drill consists of:</span></span>

* <span data-ttu-id="d1ba2-108">Onderbreking van de laag Simulating gegevens</span><span class="sxs-lookup"><span data-stu-id="d1ba2-108">Simulating data tier outage</span></span>
* <span data-ttu-id="d1ba2-109">Herstellen</span><span class="sxs-lookup"><span data-stu-id="d1ba2-109">Recovering</span></span>
* <span data-ttu-id="d1ba2-110">Toepassingsherstel integriteit post valideren</span><span class="sxs-lookup"><span data-stu-id="d1ba2-110">Validate application integrity post recovery</span></span>

<span data-ttu-id="d1ba2-111">Afhankelijk van hoe u [ontworpen van uw toepassing voor bedrijfscontinuïteit](sql-database-business-continuity.md), Hallo werkstroom tooexecute Hallo inzoomen kan variëren.</span><span class="sxs-lookup"><span data-stu-id="d1ba2-111">Depending on how you [designed your application for business continuity](sql-database-business-continuity.md), hello workflow tooexecute hello drill can vary.</span></span> <span data-ttu-id="d1ba2-112">Hieronder worden beschreven Hallo aanbevolen procedures voor het uitvoeren van een detailanalyse van het herstel na noodgevallen in de context Hallo van Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="d1ba2-112">Below we describe hello best practices conducting a disaster recovery drill in hello context of Azure SQL Database.</span></span>

## <a name="geo-restore"></a><span data-ttu-id="d1ba2-113">Geo-herstel</span><span class="sxs-lookup"><span data-stu-id="d1ba2-113">Geo-restore</span></span>
<span data-ttu-id="d1ba2-114">tooprevent Hallo mogelijk gegevensverlies bij het uitvoeren van een herstel na noodgevallen detailanalyse, wordt aangeraden uitvoeren Hallo inzoomen met behulp van een testomgeving door een kopie van de productieomgeving Hallo maken en deze werkstroom tooverify Hallo van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="d1ba2-114">tooprevent hello potential data loss when conducting a disaster recovery drill, we recommend performing hello drill using a test environment by creating a copy of hello production environment and using it tooverify hello application’s failover workflow.</span></span>

#### <a name="outage-simulation"></a><span data-ttu-id="d1ba2-115">Storing simulatie</span><span class="sxs-lookup"><span data-stu-id="d1ba2-115">Outage simulation</span></span>
<span data-ttu-id="d1ba2-116">toosimulate Hallo onderbreking, kunt u verwijderen of wijzig de naam van de brondatabase Hallo.</span><span class="sxs-lookup"><span data-stu-id="d1ba2-116">toosimulate hello outage, you can delete or rename hello source database.</span></span> <span data-ttu-id="d1ba2-117">Dit zorgt ervoor dat de problemen met de toepassingen.</span><span class="sxs-lookup"><span data-stu-id="d1ba2-117">This causes application connectivity failures.</span></span>

#### <a name="recovery"></a><span data-ttu-id="d1ba2-118">Herstel</span><span class="sxs-lookup"><span data-stu-id="d1ba2-118">Recovery</span></span>
* <span data-ttu-id="d1ba2-119">Hallo geo-herstel van database Hallo uitvoeren in een andere server, zoals wordt beschreven [hier](sql-database-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="d1ba2-119">Perform hello geo-restore of hello database into a different server as described [here](sql-database-disaster-recovery.md).</span></span>
* <span data-ttu-id="d1ba2-120">Wijziging Hallo toepassing configuratie tooconnect toohello herstelde database en volg Hallo [na het herstel van een database te configureren](sql-database-disaster-recovery.md) toocomplete Hallo herstel leiden.</span><span class="sxs-lookup"><span data-stu-id="d1ba2-120">Change hello application configuration tooconnect toohello recovered database and follow hello [Configure a database after recovery](sql-database-disaster-recovery.md) guide toocomplete hello recovery.</span></span>

#### <a name="validation"></a><span data-ttu-id="d1ba2-121">Validatie</span><span class="sxs-lookup"><span data-stu-id="d1ba2-121">Validation</span></span>
* <span data-ttu-id="d1ba2-122">Volledige Hallo inzoomen door Hallo integriteit post toepassingsherstel (inclusief verbindingsreeksen, aanmeldingen, testen van de basisfunctionaliteit of andere onderdeel validaties van standaardtoepassing ondertekeningen procedures) te verifiëren.</span><span class="sxs-lookup"><span data-stu-id="d1ba2-122">Complete hello drill by verifying hello application integrity post recovery (including connection strings, logins, basic functionality testing or other validations part of standard application signoffs procedures).</span></span>

## <a name="geo-replication"></a><span data-ttu-id="d1ba2-123">Geo-replicatie</span><span class="sxs-lookup"><span data-stu-id="d1ba2-123">Geo-replication</span></span>
<span data-ttu-id="d1ba2-124">Voor een database die is beveiligd met geo-replicatie Hallo inzoomen omvat oefening geplande failover toohello secundaire database.</span><span class="sxs-lookup"><span data-stu-id="d1ba2-124">For a database that is protected using geo-replication hello drill exercise involves planned failover toohello secondary database.</span></span> <span data-ttu-id="d1ba2-125">Hallo geplande failover zorgt ervoor dat Hallo primaire en secundaire databases Hallo synchroon blijven wanneer Hallo rollen worden omgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="d1ba2-125">hello planned failover ensures that hello primary and hello secondary databases remain in sync when hello roles are switched.</span></span> <span data-ttu-id="d1ba2-126">In tegenstelling tot Hallo van niet-geplande failover, deze bewerking niet resulteren in verlies van gegevens, zodat Hallo inzoomen kan worden uitgevoerd in de productieomgeving Hallo.</span><span class="sxs-lookup"><span data-stu-id="d1ba2-126">Unlike hello unplanned failover, this operation does not result in data loss, so hello drill can be performed in hello production environment.</span></span>

#### <a name="outage-simulation"></a><span data-ttu-id="d1ba2-127">Storing simulatie</span><span class="sxs-lookup"><span data-stu-id="d1ba2-127">Outage simulation</span></span>
<span data-ttu-id="d1ba2-128">toosimulate hello onderbreking, kunt u Hallo-webtoepassing of virtuele machine verbonden toohello database uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="d1ba2-128">toosimulate hello outage, you can disable hello web application or virtual machine connected toohello database.</span></span> <span data-ttu-id="d1ba2-129">Dit resulteert in Hallo verbindingsfouten voor Hallo webserver en webclients.</span><span class="sxs-lookup"><span data-stu-id="d1ba2-129">This results in hello connectivity failures for hello web clients.</span></span>

#### <a name="recovery"></a><span data-ttu-id="d1ba2-130">Herstel</span><span class="sxs-lookup"><span data-stu-id="d1ba2-130">Recovery</span></span>
* <span data-ttu-id="d1ba2-131">Configuratie van de toepassing of Hallo maken in Hallo DR regio punten toohello voormalige secundaire hello wordt volledig toegankelijk nieuwe primaire.</span><span class="sxs-lookup"><span data-stu-id="d1ba2-131">Make sure hello application configuration in hello DR region points toohello former secondary which becomes hello fully accessible new primary.</span></span>
* <span data-ttu-id="d1ba2-132">Voer [geplande failover](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) toomake Hallo secundaire database een nieuwe primaire</span><span class="sxs-lookup"><span data-stu-id="d1ba2-132">Perform [planned failover](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) toomake hello secondary database a new primary</span></span>
* <span data-ttu-id="d1ba2-133">Ga als volgt Hallo [na het herstel van een database te configureren](sql-database-disaster-recovery.md) toocomplete Hallo herstel leiden.</span><span class="sxs-lookup"><span data-stu-id="d1ba2-133">Follow hello [Configure a database after recovery](sql-database-disaster-recovery.md) guide toocomplete hello recovery.</span></span>

#### <a name="validation"></a><span data-ttu-id="d1ba2-134">Validatie</span><span class="sxs-lookup"><span data-stu-id="d1ba2-134">Validation</span></span>
* <span data-ttu-id="d1ba2-135">Volledige Hallo inzoomen door Hallo integriteit post toepassingsherstel (inclusief verbindingsreeksen, aanmeldingen, testen van de basisfunctionaliteit of andere onderdeel validaties van standaardtoepassing ondertekeningen procedures) te verifiëren.</span><span class="sxs-lookup"><span data-stu-id="d1ba2-135">Complete hello drill by verifying hello application integrity post recovery (including connection strings, logins, basic functionality testing or other validations part of standard application signoffs procedures).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1ba2-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d1ba2-136">Next steps</span></span>
* <span data-ttu-id="d1ba2-137">toolearn over zakelijke continuïteit scenario's, Zie [continuïteit scenario's](sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="d1ba2-137">toolearn about business continuity scenarios, see [Continuity scenarios](sql-database-business-continuity.md)</span></span>
* <span data-ttu-id="d1ba2-138">toolearn over Azure SQL Database automatische back-ups, Zie [geautomatiseerde back-ups van SQL-Database](sql-database-automated-backups.md)</span><span class="sxs-lookup"><span data-stu-id="d1ba2-138">toolearn about Azure SQL Database automated backups, see [SQL Database automated backups](sql-database-automated-backups.md)</span></span>
* <span data-ttu-id="d1ba2-139">toolearn over het gebruik van automatische back-ups voor herstel, Zie [een database terugzetten vanuit Hallo service geïnitieerde back-ups](sql-database-recovery-using-backups.md)</span><span class="sxs-lookup"><span data-stu-id="d1ba2-139">toolearn about using automated backups for recovery, see [restore a database from hello service-initiated backups](sql-database-recovery-using-backups.md)</span></span>
* <span data-ttu-id="d1ba2-140">Zie toolearn over opties voor sneller herstel [actieve geo-replicatie](sql-database-geo-replication-overview.md)</span><span class="sxs-lookup"><span data-stu-id="d1ba2-140">toolearn about faster recovery options, see [active geo-replication](sql-database-geo-replication-overview.md)</span></span>  
