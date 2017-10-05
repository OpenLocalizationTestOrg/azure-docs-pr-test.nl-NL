---
title: Het herstellen van een Server in Azure-Database voor PostgreSQL | Microsoft Docs
description: Dit artikel wordt beschreven hoe u een server in Azure-Database herstelt voor PostgreSQL met de Azure portal.
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 07/20/2017
ms.openlocfilehash: 3fbdb7741481bd3620466c3489d3609f9ea6961f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-backup-and-restore-a-server-in-azure-database-for-postgresql-using-the-azure-portal"></a><span data-ttu-id="01af0-103">Het back-up en herstellen van een server in Azure-Database voor PostgreSQL met de Azure portal</span><span class="sxs-lookup"><span data-stu-id="01af0-103">How To Backup and Restore a server in Azure Database for PostgreSQL using the Azure portal</span></span>

## <a name="backup-happens-automatically"></a><span data-ttu-id="01af0-104">Back-up automatisch wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="01af0-104">Backup happens Automatically</span></span>
<span data-ttu-id="01af0-105">Wanneer u Azure-Database voor PostgreSQL, wordt de database-service automatisch een back-up van de service om de 5 minuten.</span><span class="sxs-lookup"><span data-stu-id="01af0-105">When using Azure Database for PostgreSQL, the database service automatically makes a backup of the service every 5 minutes.</span></span> 

<span data-ttu-id="01af0-106">De back-ups zijn beschikbaar voor de zeven dagen bij gebruik van Basisstaffel en 35 dagen bij gebruik van de Standard-laag.</span><span class="sxs-lookup"><span data-stu-id="01af0-106">The backups are available for 7 days when using Basic Tier, and 35 days when using Standard Tier.</span></span> <span data-ttu-id="01af0-107">Zie voor meer informatie [Azure Database voor de Servicelagen PostgreSQL](concepts-service-tiers.md)</span><span class="sxs-lookup"><span data-stu-id="01af0-107">For more information, see [Azure Database for PostgreSQL service tiers](concepts-service-tiers.md)</span></span>

<span data-ttu-id="01af0-108">Met deze functie voor automatische back-up kan u de server en alle bijbehorende databases herstellen naar een nieuwe server aan een eerder punt in tijd.</span><span class="sxs-lookup"><span data-stu-id="01af0-108">Using this automatic backup feature you may restore the server and all its databases into a new server to an earlier point-in-time.</span></span>

## <a name="restore-in-the-azure-portal"></a><span data-ttu-id="01af0-109">Herstellen in de Azure portal</span><span class="sxs-lookup"><span data-stu-id="01af0-109">Restore in the Azure portal</span></span>
<span data-ttu-id="01af0-110">Azure PostgreSQL-Database kunt u de server weer terugzetten naar een punt in tijd en in op een nieuwe kopie van de server.</span><span class="sxs-lookup"><span data-stu-id="01af0-110">Azure Database for PostgreSQL allows you to restore the server back to a point in time and into to a new copy of the server.</span></span> <span data-ttu-id="01af0-111">U kunt deze nieuwe server gebruiken om uw gegevens te herstellen.</span><span class="sxs-lookup"><span data-stu-id="01af0-111">You can use this new server to recover your data.</span></span> 

<span data-ttu-id="01af0-112">Bijvoorbeeld, als een tabel per ongeluk is kan verwijderd op twaalf uur 's middags vandaag de dag u herstellen en de tijd net vóór twaalf uur 's middags en ophalen van de ontbrekende tabel en de gegevens van die nieuwe kopie van de server.</span><span class="sxs-lookup"><span data-stu-id="01af0-112">For example, if a table was accidentally dropped at noon today, you could restore to the time just before noon and retrieve the missing table and data from that new copy of the server.</span></span>

<span data-ttu-id="01af0-113">De volgende stappen uit voor het herstellen van de voorbeeldserver naar een punt in tijd:</span><span class="sxs-lookup"><span data-stu-id="01af0-113">The following steps restore the sample server to a point in time:</span></span>
1. <span data-ttu-id="01af0-114">Meld u aan bij de [Azure-portal](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="01af0-114">Sign into the [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="01af0-115">Ga naar uw Azure-Database voor PostgreSQL-server.</span><span class="sxs-lookup"><span data-stu-id="01af0-115">Locate your Azure Database for PostgreSQL server.</span></span> <span data-ttu-id="01af0-116">Klik in de Azure-portal op **alle Resources** uit het menu links en typ de naam zoals **mypgserver 20170401**, om te zoeken naar de bestaande server.</span><span class="sxs-lookup"><span data-stu-id="01af0-116">In the Azure portal, click **All Resources** from the left-hand menu and type in the name, such as **mypgserver-20170401**, to search for your existing server.</span></span> <span data-ttu-id="01af0-117">Klik op de servernaam in de zoekresultaten.</span><span class="sxs-lookup"><span data-stu-id="01af0-117">Click the server name listed in the search result.</span></span> <span data-ttu-id="01af0-118">De pagina **Overzicht** wordt geopend voor uw server en biedt opties voor verdere configuratie.</span><span class="sxs-lookup"><span data-stu-id="01af0-118">The **Overview** page for your server opens and provides options for further configuration.</span></span>

   ![Azure portal - zoekt u naar de server](media/postgresql-howto-restore-server-portal/1-locate.png)

3. <span data-ttu-id="01af0-120">Klik boven aan de overzichtsblade van server **herstellen** op de werkbalk.</span><span class="sxs-lookup"><span data-stu-id="01af0-120">On the top of the server overview blade, click **Restore** on the toolbar.</span></span> <span data-ttu-id="01af0-121">De Restore-blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="01af0-121">The Restore blade opens.</span></span>

   ![Azure-Database voor herstel PostgreSQL - overzicht - knop](./media/postgresql-howto-restore-server-portal/2_server.png)

4. <span data-ttu-id="01af0-123">Vul het formulier terugzetten met de vereiste informatie in:</span><span class="sxs-lookup"><span data-stu-id="01af0-123">Fill out the Restore form with the required information:</span></span>

   ![<span data-ttu-id="01af0-124">Azure-Database voor PostgreSQL - informatie terugzetten</span><span class="sxs-lookup"><span data-stu-id="01af0-124">Azure Database for PostgreSQL - Restore information</span></span> ](./media/postgresql-howto-restore-server-portal/3_restore.png)
  - <span data-ttu-id="01af0-125">**Herstelpunt**: Selecteer een point-in-time die deze gebeurtenis treedt op voordat de server is gewijzigd</span><span class="sxs-lookup"><span data-stu-id="01af0-125">**Restore point**: Select a point-in-time that occurs before the server was changed</span></span>
  - <span data-ttu-id="01af0-126">**Doelserver**: Geef een nieuwe servernaam die u terugzetten wilt naar</span><span class="sxs-lookup"><span data-stu-id="01af0-126">**Target server**: Provide a new server name you want to restore to</span></span>
  - <span data-ttu-id="01af0-127">**Locatie**: U kunt de regio niet selecteren, standaard is dit hetzelfde als de bronserver</span><span class="sxs-lookup"><span data-stu-id="01af0-127">**Location**: You cannot select the region, by default it is same as the source server</span></span>
  - <span data-ttu-id="01af0-128">**Prijscategorie**: U kunt deze waarde niet wijzigen bij het herstellen van een server.</span><span class="sxs-lookup"><span data-stu-id="01af0-128">**Pricing tier**: You cannot change this value when restoring a server.</span></span> <span data-ttu-id="01af0-129">Dit is hetzelfde als de bronserver.</span><span class="sxs-lookup"><span data-stu-id="01af0-129">It is same as the source server.</span></span> 

5. <span data-ttu-id="01af0-130">Klik op **OK** om de server te herstellen naar een punt in tijd te herstellen.</span><span class="sxs-lookup"><span data-stu-id="01af0-130">Click **OK** to restore the server to restore to a point in time.</span></span> 

6. <span data-ttu-id="01af0-131">Nadat het herstel is voltooid, zoek de nieuwe server die wordt gemaakt om te controleren of dat de gegevens is hersteld, zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="01af0-131">Once the restore finishes, locate the new server that is created to verify the data was restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="01af0-132">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="01af0-132">Next steps</span></span>
- [<span data-ttu-id="01af0-133">Verbindingsbibliotheken voor Azure-Database voor PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="01af0-133">Connection libraries for Azure Database for PostgreSQL</span></span>](concepts-connection-libraries.md)
