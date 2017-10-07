---
title: Hoe een Server in Azure-Database voor PostgreSQL tooRestore | Microsoft Docs
description: Dit artikel wordt beschreven hoe een server in Azure-Database voor het gebruik van PostgreSQL toorestore hello Azure-portal.
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 07/20/2017
ms.openlocfilehash: bc7351f384607397806d837afd3e1d7a26575e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobackup-and-restore-a-server-in-azure-database-for-postgresql-using-hello-azure-portal"></a><span data-ttu-id="c6af8-103">Hoe tooBackup en terugzetten van een server in Azure-Database voor het gebruik van PostgreSQL hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="c6af8-103">How tooBackup and Restore a server in Azure Database for PostgreSQL using hello Azure portal</span></span>

## <a name="backup-happens-automatically"></a><span data-ttu-id="c6af8-104">Back-up automatisch wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="c6af8-104">Backup happens Automatically</span></span>
<span data-ttu-id="c6af8-105">Wanneer u Azure-Database voor PostgreSQL, wordt Hallo database-service automatisch een back-up van Hallo-service om de 5 minuten.</span><span class="sxs-lookup"><span data-stu-id="c6af8-105">When using Azure Database for PostgreSQL, hello database service automatically makes a backup of hello service every 5 minutes.</span></span> 

<span data-ttu-id="c6af8-106">Hallo back-ups zijn beschikbaar voor de zeven dagen bij gebruik van Basisstaffel en 35 dagen bij gebruik van de Standard-laag.</span><span class="sxs-lookup"><span data-stu-id="c6af8-106">hello backups are available for 7 days when using Basic Tier, and 35 days when using Standard Tier.</span></span> <span data-ttu-id="c6af8-107">Zie voor meer informatie [Azure Database voor de Servicelagen PostgreSQL](concepts-service-tiers.md)</span><span class="sxs-lookup"><span data-stu-id="c6af8-107">For more information, see [Azure Database for PostgreSQL service tiers](concepts-service-tiers.md)</span></span>

<span data-ttu-id="c6af8-108">Met deze functie voor automatische back-up kan u Hallo-server en alle bijbehorende databases herstellen naar een nieuwe server tooan eerder punt in tijd.</span><span class="sxs-lookup"><span data-stu-id="c6af8-108">Using this automatic backup feature you may restore hello server and all its databases into a new server tooan earlier point-in-time.</span></span>

## <a name="restore-in-hello-azure-portal"></a><span data-ttu-id="c6af8-109">Herstellen in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="c6af8-109">Restore in hello Azure portal</span></span>
<span data-ttu-id="c6af8-110">Azure PostgreSQL-Database kunt u toorestore Hallo server back-tooa punt in tijd en in nieuwe versie van de tooa van Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="c6af8-110">Azure Database for PostgreSQL allows you toorestore hello server back tooa point in time and into tooa new copy of hello server.</span></span> <span data-ttu-id="c6af8-111">U kunt deze nieuwe server toorecover uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="c6af8-111">You can use this new server toorecover your data.</span></span> 

<span data-ttu-id="c6af8-112">Bijvoorbeeld, als een tabel per ongeluk is kan verwijderd op twaalf uur 's middags vandaag de dag u herstellen toohello tijd net vóór twaalf uur 's middags en Hallo ontbrekende tabel en gegevens van die nieuwe versie van Hallo server ophalen.</span><span class="sxs-lookup"><span data-stu-id="c6af8-112">For example, if a table was accidentally dropped at noon today, you could restore toohello time just before noon and retrieve hello missing table and data from that new copy of hello server.</span></span>

<span data-ttu-id="c6af8-113">Hallo herstelpunt volgt Hallo voorbeeld server tooa in tijd:</span><span class="sxs-lookup"><span data-stu-id="c6af8-113">hello following steps restore hello sample server tooa point in time:</span></span>
1. <span data-ttu-id="c6af8-114">Meld u aan bij Hallo [Azure-portal](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="c6af8-114">Sign into hello [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="c6af8-115">Ga naar uw Azure-Database voor PostgreSQL-server.</span><span class="sxs-lookup"><span data-stu-id="c6af8-115">Locate your Azure Database for PostgreSQL server.</span></span> <span data-ttu-id="c6af8-116">In hello Azure-portal, klikt u op **alle Resources** van links menu Hallo en typt u de naam van de Hallo, zoals **mypgserver 20170401**, toosearch voor uw bestaande server.</span><span class="sxs-lookup"><span data-stu-id="c6af8-116">In hello Azure portal, click **All Resources** from hello left-hand menu and type in hello name, such as **mypgserver-20170401**, toosearch for your existing server.</span></span> <span data-ttu-id="c6af8-117">Klik op Hallo servernaam weergegeven in zoekresultaten Hallo.</span><span class="sxs-lookup"><span data-stu-id="c6af8-117">Click hello server name listed in hello search result.</span></span> <span data-ttu-id="c6af8-118">Hallo **overzicht** pagina voor de server wordt geopend en opties voor verdere configuratie biedt.</span><span class="sxs-lookup"><span data-stu-id="c6af8-118">hello **Overview** page for your server opens and provides options for further configuration.</span></span>

   ![Azure-portal - toolocate uw server zoeken](media/postgresql-howto-restore-server-portal/1-locate.png)

3. <span data-ttu-id="c6af8-120">Klik op Hallo bovenaan Hallo server overzichtsblade **herstellen** op Hallo-werkbalk.</span><span class="sxs-lookup"><span data-stu-id="c6af8-120">On hello top of hello server overview blade, click **Restore** on hello toolbar.</span></span> <span data-ttu-id="c6af8-121">Hallo terugzetten blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="c6af8-121">hello Restore blade opens.</span></span>

   ![Azure-Database voor herstel PostgreSQL - overzicht - knop](./media/postgresql-howto-restore-server-portal/2_server.png)

4. <span data-ttu-id="c6af8-123">Hallo terugzetten formulier met Hallo vereiste informatie invullen:</span><span class="sxs-lookup"><span data-stu-id="c6af8-123">Fill out hello Restore form with hello required information:</span></span>

   ![<span data-ttu-id="c6af8-124">Azure-Database voor PostgreSQL - informatie terugzetten</span><span class="sxs-lookup"><span data-stu-id="c6af8-124">Azure Database for PostgreSQL - Restore information</span></span> ](./media/postgresql-howto-restore-server-portal/3_restore.png)
  - <span data-ttu-id="c6af8-125">**Herstelpunt**: Selecteer een point-in-time die deze gebeurtenis treedt op voordat het Hallo-server is gewijzigd</span><span class="sxs-lookup"><span data-stu-id="c6af8-125">**Restore point**: Select a point-in-time that occurs before hello server was changed</span></span>
  - <span data-ttu-id="c6af8-126">**Doelserver**: Geef een nieuwe naam van een server toorestore naar gewenste</span><span class="sxs-lookup"><span data-stu-id="c6af8-126">**Target server**: Provide a new server name you want toorestore to</span></span>
  - <span data-ttu-id="c6af8-127">**Locatie**: U kunt geen Hallo regio selecteren, standaard is dit hetzelfde als de bronserver Hallo</span><span class="sxs-lookup"><span data-stu-id="c6af8-127">**Location**: You cannot select hello region, by default it is same as hello source server</span></span>
  - <span data-ttu-id="c6af8-128">**Prijscategorie**: U kunt deze waarde niet wijzigen bij het herstellen van een server.</span><span class="sxs-lookup"><span data-stu-id="c6af8-128">**Pricing tier**: You cannot change this value when restoring a server.</span></span> <span data-ttu-id="c6af8-129">Dit is hetzelfde als de bronserver Hallo.</span><span class="sxs-lookup"><span data-stu-id="c6af8-129">It is same as hello source server.</span></span> 

5. <span data-ttu-id="c6af8-130">Klik op **OK** toorestore Hallo server toorestore tooa punt in tijd.</span><span class="sxs-lookup"><span data-stu-id="c6af8-130">Click **OK** toorestore hello server toorestore tooa point in time.</span></span> 

6. <span data-ttu-id="c6af8-131">Zodra het Hallo terugzetten is voltooid, zoek Hallo nieuwe server die wordt gemaakt tooverify Hallo gegevens is hersteld, zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="c6af8-131">Once hello restore finishes, locate hello new server that is created tooverify hello data was restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6af8-132">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c6af8-132">Next steps</span></span>
- [<span data-ttu-id="c6af8-133">Verbindingsbibliotheken voor Azure-Database voor PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="c6af8-133">Connection libraries for Azure Database for PostgreSQL</span></span>](concepts-connection-libraries.md)
