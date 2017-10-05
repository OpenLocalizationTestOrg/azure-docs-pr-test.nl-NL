---
title: Het herstellen van een Server in Azure-Database voor MySQL | Microsoft Docs
description: Dit artikel wordt beschreven hoe u een server in Azure-Database herstelt voor MySQL met de Azure portal.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 8c06dce534b628a602127fd02b152c8e04e02cc4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-backup-and-restore-a-server-in-azure-database-for-mysql-using-the-azure-portal"></a><span data-ttu-id="01626-103">Het back-up en herstellen van een server in Azure-Database voor MySQL met de Azure portal</span><span class="sxs-lookup"><span data-stu-id="01626-103">How To Backup and Restore a server in Azure Database for MySQL using the Azure portal</span></span>

## <a name="backup-happens-automatically"></a><span data-ttu-id="01626-104">Back-up automatisch wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="01626-104">Backup happens Automatically</span></span>
<span data-ttu-id="01626-105">Wanneer u Azure-Database voor MySQL, wordt de database-service automatisch een back-up van de service om de 5 minuten.</span><span class="sxs-lookup"><span data-stu-id="01626-105">When using Azure Database for MySQL, the database service automatically makes a backup of the service every 5 minutes.</span></span> 

<span data-ttu-id="01626-106">De back-ups zijn beschikbaar voor de zeven dagen bij gebruik van Basisstaffel en 35 dagen bij gebruik van de Standard-laag.</span><span class="sxs-lookup"><span data-stu-id="01626-106">The backups are available for 7 days when using Basic Tier, and 35 days when using Standard Tier.</span></span> <span data-ttu-id="01626-107">Zie voor meer informatie [Azure Database voor de Servicelagen MySQL](concepts-service-tiers.md)</span><span class="sxs-lookup"><span data-stu-id="01626-107">For more information, see [Azure Database for MySQL service tiers](concepts-service-tiers.md)</span></span>

<span data-ttu-id="01626-108">Met deze functie voor automatische back-up kan u de server en alle bijbehorende databases herstellen naar een nieuwe server aan een eerder punt in tijd.</span><span class="sxs-lookup"><span data-stu-id="01626-108">Using this automatic backup feature you may restore the server and all its databases into a new server to an earlier point-in-time.</span></span>

## <a name="restore-in-the-azure-portal"></a><span data-ttu-id="01626-109">Herstellen in de Azure portal</span><span class="sxs-lookup"><span data-stu-id="01626-109">Restore in the Azure portal</span></span>
<span data-ttu-id="01626-110">Azure MySQL-Database kunt u de server weer terugzetten naar een punt in tijd en in op een nieuwe kopie van de server.</span><span class="sxs-lookup"><span data-stu-id="01626-110">Azure Database for MySQL allows you to restore the server back to a point in time and into to a new copy of the server.</span></span> <span data-ttu-id="01626-111">U kunt deze nieuwe server gebruiken om uw gegevens te herstellen.</span><span class="sxs-lookup"><span data-stu-id="01626-111">You can use this new server to recover your data.</span></span> 

<span data-ttu-id="01626-112">Bijvoorbeeld, als een tabel per ongeluk is kan verwijderd op twaalf uur 's middags vandaag de dag u herstellen en de tijd net vóór twaalf uur 's middags en ophalen van de ontbrekende tabel en de gegevens van die nieuwe kopie van de server.</span><span class="sxs-lookup"><span data-stu-id="01626-112">For example, if a table was accidentally dropped at noon today, you could restore to the time just before noon and retrieve the missing table and data from that new copy of the server.</span></span>

<span data-ttu-id="01626-113">De volgende stappen uit voor het herstellen van de voorbeeldserver naar een punt in tijd:</span><span class="sxs-lookup"><span data-stu-id="01626-113">The following steps restore the sample server to a point in time:</span></span>

1. <span data-ttu-id="01626-114">Meld u aan bij de [Azure-portal](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="01626-114">Sign into the [Azure portal](https://portal.azure.com/)</span></span>

2. <span data-ttu-id="01626-115">Ga naar uw Azure-Database voor de MySQL-server.</span><span class="sxs-lookup"><span data-stu-id="01626-115">Locate your Azure Database for MySQL server.</span></span> <span data-ttu-id="01626-116">Selecteer in het linkerdeelvenster **alle resources**, selecteer uw server uit de lijst.</span><span class="sxs-lookup"><span data-stu-id="01626-116">In the left pane, select **All resources**, then select your server from the list.</span></span>

3.  <span data-ttu-id="01626-117">Klik boven aan de overzichtsblade van server **herstellen** op de werkbalk.</span><span class="sxs-lookup"><span data-stu-id="01626-117">On the top of the server overview blade, click **Restore** on the toolbar.</span></span> <span data-ttu-id="01626-118">De Restore-blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="01626-118">The Restore blade opens.</span></span>
<span data-ttu-id="01626-119">![Klik op de knop herstellen](./media/howto-restore-server-portal/click-restore-button.png)</span><span class="sxs-lookup"><span data-stu-id="01626-119">![click restore button](./media/howto-restore-server-portal/click-restore-button.png)</span></span>

4. <span data-ttu-id="01626-120">Vul het formulier terugzetten met de vereiste informatie in:</span><span class="sxs-lookup"><span data-stu-id="01626-120">Fill out the Restore form with the required information:</span></span>

- <span data-ttu-id="01626-121">**Herstelpunt (UTC)**: Selecteer een point-in-time om naar te herstellen met de objectkiezer datum en tijd kiezen.</span><span class="sxs-lookup"><span data-stu-id="01626-121">**Restore point (UTC)**: Using the Date picker and time picker, select a point-in-time to restore to.</span></span> <span data-ttu-id="01626-122">De opgegeven tijd is in UTC-notatie, dus u waarschijnlijk moet worden de lokale tijd geconverteerd naar UTC.</span><span class="sxs-lookup"><span data-stu-id="01626-122">The time specified is in UTC format, so you likely need to convert the local time into UTC.</span></span>
- <span data-ttu-id="01626-123">**Herstellen naar de nieuwe server**: Geef een nieuwe naam van de server om de bestaande server naar te herstellen.</span><span class="sxs-lookup"><span data-stu-id="01626-123">**Restore to new server**: Provide a new server name to restore the existing server into.</span></span>
- <span data-ttu-id="01626-124">**Locatie**: de keuze regio automatisch gevuld met de server bron regio en kan niet worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="01626-124">**Location**: The region choice automatically populates with the source server region, and cannot be changed.</span></span>
- <span data-ttu-id="01626-125">**Prijscategorie**: de prijscategorie laag keuze automatisch gevuld met de dezelfde prijscategorie als de bronserver en kan hier niet worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="01626-125">**Pricing tier**: The pricing tier choice automatically populates with the same pricing tier as the source server, and cannot be changed here.</span></span> 
<span data-ttu-id="01626-126">![PITR terugzetten](./media/howto-restore-server-portal/pitr-restore.png)</span><span class="sxs-lookup"><span data-stu-id="01626-126">![PITR Restore](./media/howto-restore-server-portal/pitr-restore.png)</span></span>

5. <span data-ttu-id="01626-127">Klik op **OK** om de server te herstellen naar een punt in tijd te herstellen.</span><span class="sxs-lookup"><span data-stu-id="01626-127">Click **OK** to restore the server to restore to a point in time.</span></span> 

6. <span data-ttu-id="01626-128">Nadat het herstel is voltooid, zoekt u de nieuwe server die is gemaakt om te controleren of dat de databases zijn teruggezet zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="01626-128">After the restore finishes, locate the new server that was created to verify the databases were restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="01626-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="01626-129">Next steps</span></span>
- [<span data-ttu-id="01626-130">Verbindingsbibliotheken voor Azure-Database voor MySQL</span><span class="sxs-lookup"><span data-stu-id="01626-130">Connection libraries for Azure Database for MySQL</span></span>](concepts-connection-libraries.md)