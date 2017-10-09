---
title: aaaHow tooRestore een Server in Azure-Database voor MySQL | Microsoft Docs
description: Dit artikel wordt beschreven hoe een server in Azure-Database voor het gebruik van MySQL toorestore hello Azure-portal.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 4b990d5b37c5d4924de9571192b923e3c81094ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobackup-and-restore-a-server-in-azure-database-for-mysql-using-hello-azure-portal"></a><span data-ttu-id="352fa-103">Hoe tooBackup en terugzetten van een server in Azure-Database voor het gebruik van MySQL hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="352fa-103">How tooBackup and Restore a server in Azure Database for MySQL using hello Azure portal</span></span>

## <a name="backup-happens-automatically"></a><span data-ttu-id="352fa-104">Back-up automatisch wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="352fa-104">Backup happens Automatically</span></span>
<span data-ttu-id="352fa-105">Wanneer u Azure-Database voor MySQL, wordt Hallo database-service automatisch een back-up van Hallo-service om de 5 minuten.</span><span class="sxs-lookup"><span data-stu-id="352fa-105">When using Azure Database for MySQL, hello database service automatically makes a backup of hello service every 5 minutes.</span></span> 

<span data-ttu-id="352fa-106">Hallo back-ups zijn beschikbaar voor de zeven dagen bij gebruik van Basisstaffel en 35 dagen bij gebruik van de Standard-laag.</span><span class="sxs-lookup"><span data-stu-id="352fa-106">hello backups are available for 7 days when using Basic Tier, and 35 days when using Standard Tier.</span></span> <span data-ttu-id="352fa-107">Zie voor meer informatie [Azure Database voor de Servicelagen MySQL](concepts-service-tiers.md)</span><span class="sxs-lookup"><span data-stu-id="352fa-107">For more information, see [Azure Database for MySQL service tiers](concepts-service-tiers.md)</span></span>

<span data-ttu-id="352fa-108">Met deze functie voor automatische back-up kan u Hallo-server en alle bijbehorende databases herstellen naar een nieuwe server tooan eerder punt in tijd.</span><span class="sxs-lookup"><span data-stu-id="352fa-108">Using this automatic backup feature you may restore hello server and all its databases into a new server tooan earlier point-in-time.</span></span>

## <a name="restore-in-hello-azure-portal"></a><span data-ttu-id="352fa-109">Herstellen in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="352fa-109">Restore in hello Azure portal</span></span>
<span data-ttu-id="352fa-110">Azure MySQL-Database kunt u toorestore Hallo server back-tooa punt in tijd en in nieuwe versie van de tooa van Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="352fa-110">Azure Database for MySQL allows you toorestore hello server back tooa point in time and into tooa new copy of hello server.</span></span> <span data-ttu-id="352fa-111">U kunt deze nieuwe server toorecover uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="352fa-111">You can use this new server toorecover your data.</span></span> 

<span data-ttu-id="352fa-112">Bijvoorbeeld, als een tabel per ongeluk is kan verwijderd op twaalf uur 's middags vandaag de dag u herstellen toohello tijd net vóór twaalf uur 's middags en Hallo ontbrekende tabel en gegevens van die nieuwe versie van Hallo server ophalen.</span><span class="sxs-lookup"><span data-stu-id="352fa-112">For example, if a table was accidentally dropped at noon today, you could restore toohello time just before noon and retrieve hello missing table and data from that new copy of hello server.</span></span>

<span data-ttu-id="352fa-113">Hallo herstelpunt volgt Hallo voorbeeld server tooa in tijd:</span><span class="sxs-lookup"><span data-stu-id="352fa-113">hello following steps restore hello sample server tooa point in time:</span></span>

1. <span data-ttu-id="352fa-114">Meld u aan bij Hallo [Azure-portal](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="352fa-114">Sign into hello [Azure portal](https://portal.azure.com/)</span></span>

2. <span data-ttu-id="352fa-115">Ga naar uw Azure-Database voor de MySQL-server.</span><span class="sxs-lookup"><span data-stu-id="352fa-115">Locate your Azure Database for MySQL server.</span></span> <span data-ttu-id="352fa-116">Selecteer in het linkerdeelvenster Hallo **alle resources**, selecteer uw server uit de lijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="352fa-116">In hello left pane, select **All resources**, then select your server from hello list.</span></span>

3.  <span data-ttu-id="352fa-117">Klik op Hallo bovenaan Hallo server overzichtsblade **herstellen** op Hallo-werkbalk.</span><span class="sxs-lookup"><span data-stu-id="352fa-117">On hello top of hello server overview blade, click **Restore** on hello toolbar.</span></span> <span data-ttu-id="352fa-118">Hallo terugzetten blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="352fa-118">hello Restore blade opens.</span></span>
<span data-ttu-id="352fa-119">![Klik op de knop herstellen](./media/howto-restore-server-portal/click-restore-button.png)</span><span class="sxs-lookup"><span data-stu-id="352fa-119">![click restore button](./media/howto-restore-server-portal/click-restore-button.png)</span></span>

4. <span data-ttu-id="352fa-120">Hallo terugzetten formulier met Hallo vereiste informatie invullen:</span><span class="sxs-lookup"><span data-stu-id="352fa-120">Fill out hello Restore form with hello required information:</span></span>

- <span data-ttu-id="352fa-121">**Herstelpunt (UTC)**: Selecteer een punt in tijd toorestore aan met picker van Hallo datum en tijd kiezen.</span><span class="sxs-lookup"><span data-stu-id="352fa-121">**Restore point (UTC)**: Using hello Date picker and time picker, select a point-in-time toorestore to.</span></span> <span data-ttu-id="352fa-122">Hallo-tijd die is opgegeven is in UTC-notatie, dus u waarschijnlijk tooconvert Hallo lokale tijd in UTC moet.</span><span class="sxs-lookup"><span data-stu-id="352fa-122">hello time specified is in UTC format, so you likely need tooconvert hello local time into UTC.</span></span>
- <span data-ttu-id="352fa-123">**Herstellen van toonew server**: Geef een nieuwe server name toorestore Hallo bestaande server in.</span><span class="sxs-lookup"><span data-stu-id="352fa-123">**Restore toonew server**: Provide a new server name toorestore hello existing server into.</span></span>
- <span data-ttu-id="352fa-124">**Locatie**: Hallo regio keuze automatisch gevuld met Hallo bron server regio en kan niet worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="352fa-124">**Location**: hello region choice automatically populates with hello source server region, and cannot be changed.</span></span>
- <span data-ttu-id="352fa-125">**Prijscategorie**: Hallo prijzen laag keuze automatisch gevuld met Hallo prijzen voor dezelfde als de bronserver Hallo servicetier en kan hier niet worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="352fa-125">**Pricing tier**: hello pricing tier choice automatically populates with hello same pricing tier as hello source server, and cannot be changed here.</span></span> 
<span data-ttu-id="352fa-126">![PITR terugzetten](./media/howto-restore-server-portal/pitr-restore.png)</span><span class="sxs-lookup"><span data-stu-id="352fa-126">![PITR Restore](./media/howto-restore-server-portal/pitr-restore.png)</span></span>

5. <span data-ttu-id="352fa-127">Klik op **OK** toorestore Hallo server toorestore tooa punt in tijd.</span><span class="sxs-lookup"><span data-stu-id="352fa-127">Click **OK** toorestore hello server toorestore tooa point in time.</span></span> 

6. <span data-ttu-id="352fa-128">Nadat het Hallo terugzetten is voltooid, zoekt u Hallo nieuwe server die is gemaakt tooverify Hallo databases zijn teruggezet zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="352fa-128">After hello restore finishes, locate hello new server that was created tooverify hello databases were restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="352fa-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="352fa-129">Next steps</span></span>
- [<span data-ttu-id="352fa-130">Verbindingsbibliotheken voor Azure-Database voor MySQL</span><span class="sxs-lookup"><span data-stu-id="352fa-130">Connection libraries for Azure Database for MySQL</span></span>](concepts-connection-libraries.md)