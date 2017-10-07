---
title: Hoe tooback ups en het terugzetten van een server in Azure-Database voor PostgreSQL | Microsoft Docs
description: Meer informatie over hoe Hallo tooback up en herstel van een server in Azure-Database voor PostgreSQL met behulp van Azure CLI.
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 0b9ed25e3e3a88dd5c7ffe2ae7c27f8eef9be710
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooback-up-and-restore-a-server-in-azure-database-for-postgresql-by-using-hello-azure-cli"></a><span data-ttu-id="922a1-103">Hoe Hallo tooback up en herstel van een server in Azure-Database voor PostgreSQL met behulp van Azure CLI</span><span class="sxs-lookup"><span data-stu-id="922a1-103">How tooback up and restore a server in Azure Database for PostgreSQL by using hello Azure CLI</span></span>

<span data-ttu-id="922a1-104">Azure-Database gebruiken voor PostgreSQL toorestore een server-database tooan eerdere datum die van 7 too35 dagen omvat.</span><span class="sxs-lookup"><span data-stu-id="922a1-104">Use Azure Database for PostgreSQL toorestore a server database tooan earlier date that spans from 7 too35 days.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="922a1-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="922a1-105">Prerequisites</span></span>
<span data-ttu-id="922a1-106">toocomplete hoe-tooguide die u nodig:</span><span class="sxs-lookup"><span data-stu-id="922a1-106">toocomplete this how-tooguide, you need:</span></span>
- <span data-ttu-id="922a1-107">Een [Azure Database voor PostgreSQL-server en database](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="922a1-107">An [Azure Database for PostgreSQL server and database](quickstart-create-server-database-azure-cli.md)</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

 

> [!IMPORTANT]
> <span data-ttu-id="922a1-108">Als u installeert en lokaal hello Azure CLI gebruiken, wordt deze hoe-tooguide vereist dat u Azure CLI versie 2.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="922a1-108">If you install and use hello Azure CLI locally, this how-tooguide requires that you use Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="922a1-109">Voer tooconfirm Hallo versie bij hello Azure CLI-opdrachtprompt `az --version`.</span><span class="sxs-lookup"><span data-stu-id="922a1-109">tooconfirm hello version, at hello Azure CLI command prompt, enter `az --version`.</span></span> <span data-ttu-id="922a1-110">tooinstall upgraden, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="922a1-110">tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="back-up-happens-automatically"></a><span data-ttu-id="922a1-111">Wordt automatisch een back-up.</span><span class="sxs-lookup"><span data-stu-id="922a1-111">Back up happens automatically</span></span>
<span data-ttu-id="922a1-112">Wanneer u Azure-Database voor PostgreSQL, wordt Hallo database-service automatisch een back-up van Hallo-service om de 5 minuten.</span><span class="sxs-lookup"><span data-stu-id="922a1-112">When you use Azure Database for PostgreSQL, hello database service automatically makes a backup of hello service every 5 minutes.</span></span> 

<span data-ttu-id="922a1-113">Basic-laag zijn Hallo back-ups beschikbaar voor 7 dagen.</span><span class="sxs-lookup"><span data-stu-id="922a1-113">For Basic Tier, hello backups are available for 7 days.</span></span> <span data-ttu-id="922a1-114">Standard-laag zijn Hallo back-ups beschikbaar voor 35 dagen.</span><span class="sxs-lookup"><span data-stu-id="922a1-114">For Standard Tier, hello backups are available for 35 days.</span></span> <span data-ttu-id="922a1-115">Zie voor meer informatie [Azure Database voor PostgreSQL Prijscategorieën](concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="922a1-115">For more information, see [Azure Database for PostgreSQL pricing tiers](concepts-service-tiers.md).</span></span>

<span data-ttu-id="922a1-116">U kunt met deze functie voor automatische back-up herstellen Hallo-server en de databases tooan eerdere datum of tijdstip voor herstel.</span><span class="sxs-lookup"><span data-stu-id="922a1-116">With this automatic backup feature, you can restore hello server and its databases tooan earlier date, or point in time.</span></span>

## <a name="restore-a-database-tooa-previous-point-in-time-by-using-hello-azure-cli"></a><span data-ttu-id="922a1-117">Een database tooa eerder punt in tijd herstellen met behulp van hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="922a1-117">Restore a database tooa previous point in time by using hello Azure CLI</span></span>
<span data-ttu-id="922a1-118">Azure-Database gebruiken voor PostgreSQL toorestore Hallo server tooa vorige punt in tijd.</span><span class="sxs-lookup"><span data-stu-id="922a1-118">Use Azure Database for PostgreSQL toorestore hello server tooa previous point in time.</span></span> <span data-ttu-id="922a1-119">Hallo hersteld gegevens wordt de nieuwe server gekopieerde tooa en bestaande Hallo-server is ongewijzigd worden gelaten.</span><span class="sxs-lookup"><span data-stu-id="922a1-119">hello restored data is copied tooa new server, and hello existing server is left as is.</span></span> <span data-ttu-id="922a1-120">Als een tabel wordt per ongeluk verwijderd op twaalf uur 's middags vandaag de dag, kunt u bijvoorbeeld toohello tijd net vóór twaalf uur 's middags herstellen.</span><span class="sxs-lookup"><span data-stu-id="922a1-120">For example, if a table is accidentally dropped at noon today, you can restore toohello time just before noon.</span></span> <span data-ttu-id="922a1-121">U kunt vervolgens Hallo ontbrekende tabel en gegevens uit de Hallo hersteld kopieën van Hallo server ophalen.</span><span class="sxs-lookup"><span data-stu-id="922a1-121">Then, you can retrieve hello missing table and data from hello restored copy of hello server.</span></span> 

<span data-ttu-id="922a1-122">Gebruik hello Azure CLI-server Hallo toorestore [az postgres server terugzetten](/cli/azure/postgres/server#restore) opdracht.</span><span class="sxs-lookup"><span data-stu-id="922a1-122">toorestore hello server, use hello Azure CLI [az postgres server restore](/cli/azure/postgres/server#restore) command.</span></span>

### <a name="run-hello-restore-command"></a><span data-ttu-id="922a1-123">Hallo restore-opdracht uitvoeren</span><span class="sxs-lookup"><span data-stu-id="922a1-123">Run hello restore command</span></span>

<span data-ttu-id="922a1-124">toorestore hello server op Hallo Azure CLI-opdrachtregel invoeren Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="922a1-124">toorestore hello server, at hello Azure CLI command prompt, enter hello following command:</span></span>

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

<span data-ttu-id="922a1-125">Hallo `az postgres server restore` opdracht vereist Hallo volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="922a1-125">hello `az postgres server restore` command requires hello following parameters:</span></span>
| <span data-ttu-id="922a1-126">Instelling</span><span class="sxs-lookup"><span data-stu-id="922a1-126">Setting</span></span> | <span data-ttu-id="922a1-127">Voorgestelde waarde</span><span class="sxs-lookup"><span data-stu-id="922a1-127">Suggested value</span></span> | <span data-ttu-id="922a1-128">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="922a1-128">Description</span></span>  |
| --- | --- | --- |
| <span data-ttu-id="922a1-129">resourcegroep</span><span class="sxs-lookup"><span data-stu-id="922a1-129">resource-group</span></span> |  <span data-ttu-id="922a1-130">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="922a1-130">myResourceGroup</span></span> |  <span data-ttu-id="922a1-131">De resourcegroep waar Hallo bronserver bestaat.</span><span class="sxs-lookup"><span data-stu-id="922a1-131">The resource group where hello source server exists.</span></span>  |
| <span data-ttu-id="922a1-132">naam</span><span class="sxs-lookup"><span data-stu-id="922a1-132">name</span></span> | <span data-ttu-id="922a1-133">mypgserver hersteld</span><span class="sxs-lookup"><span data-stu-id="922a1-133">mypgserver-restored</span></span> | <span data-ttu-id="922a1-134">Hallo-naam van de nieuwe Hallo-server die is gemaakt door de opdracht restore Hallo.</span><span class="sxs-lookup"><span data-stu-id="922a1-134">hello name of hello new server that is created by hello restore command.</span></span> |
| <span data-ttu-id="922a1-135">herstel punt in tijd</span><span class="sxs-lookup"><span data-stu-id="922a1-135">restore-point-in-time</span></span> | <span data-ttu-id="922a1-136">2017-04-13T13:59:00Z</span><span class="sxs-lookup"><span data-stu-id="922a1-136">2017-04-13T13:59:00Z</span></span> | <span data-ttu-id="922a1-137">Selecteer een punt in tijd toorestore aan.</span><span class="sxs-lookup"><span data-stu-id="922a1-137">Select a point in time toorestore to.</span></span> <span data-ttu-id="922a1-138">Deze datum en tijd moet binnen Hallo van bronserver maakt u een back-up van de bewaarperiode.</span><span class="sxs-lookup"><span data-stu-id="922a1-138">This date and time must be within hello source server's back up retention period.</span></span> <span data-ttu-id="922a1-139">Gebruik Hallo ISO8601-indeling voor datum en tijd.</span><span class="sxs-lookup"><span data-stu-id="922a1-139">Use hello ISO8601 date and time format.</span></span> <span data-ttu-id="922a1-140">Bijvoorbeeld, kunt u uw eigen lokale tijdzone, zoals `2017-04-13T05:59:00-08:00`.</span><span class="sxs-lookup"><span data-stu-id="922a1-140">For example, you can use your own local time zone, such as `2017-04-13T05:59:00-08:00`.</span></span> <span data-ttu-id="922a1-141">U kunt ook Hallo Zulu UTC-indeling, bijvoorbeeld `2017-04-13T13:59:00Z`.</span><span class="sxs-lookup"><span data-stu-id="922a1-141">You can also use hello UTC Zulu format, for example, `2017-04-13T13:59:00Z`.</span></span> |
| <span data-ttu-id="922a1-142">bron-server</span><span class="sxs-lookup"><span data-stu-id="922a1-142">source-server</span></span> | <span data-ttu-id="922a1-143">mypgserver 20170401</span><span class="sxs-lookup"><span data-stu-id="922a1-143">mypgserver-20170401</span></span> | <span data-ttu-id="922a1-144">Hallo-naam of ID van Hallo bron server toorestore uit.</span><span class="sxs-lookup"><span data-stu-id="922a1-144">hello name or ID of hello source server toorestore from.</span></span> |

<span data-ttu-id="922a1-145">Wanneer u een tooan server herstelt eerdere punt in tijd, een nieuwe server is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="922a1-145">When you restore a server tooan earlier point in time, a new server is created.</span></span> <span data-ttu-id="922a1-146">Hallo oorspronkelijke server en de databases van Hallo opgegeven tijdstip zijn gekopieerde toohello nieuwe server.</span><span class="sxs-lookup"><span data-stu-id="922a1-146">hello original server and its databases from hello specified point in time are copied toohello new server.</span></span>

<span data-ttu-id="922a1-147">Hallo locatie en prijzen laag waarden Hallo voor blijven hersteld Hallo server dezelfde als de oorspronkelijke server Hallo.</span><span class="sxs-lookup"><span data-stu-id="922a1-147">hello location and pricing tier values for hello restored server remain hello same as hello original server.</span></span> 

<span data-ttu-id="922a1-148">Hallo `az postgres server restore` opdracht synchroon is.</span><span class="sxs-lookup"><span data-stu-id="922a1-148">hello `az postgres server restore` command is synchronous.</span></span> <span data-ttu-id="922a1-149">Nadat het Hallo-server is hersteld, kunt u deze opnieuw toorepeat Hallo proces voor een ander punt in tijd.</span><span class="sxs-lookup"><span data-stu-id="922a1-149">After hello server is restored, you can use it again toorepeat hello process for a different point in time.</span></span> 

<span data-ttu-id="922a1-150">Na het Hallo herstellen proces is voltooid, zoek de nieuwe server Hallo en controleer of dat Hallo gegevens is hersteld, zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="922a1-150">After hello restore process finishes, locate hello new server and verify that hello data is restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="922a1-151">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="922a1-151">Next steps</span></span>
[<span data-ttu-id="922a1-152">Verbindingsbibliotheken voor Azure-Database voor PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="922a1-152">Connection libraries for Azure Database for PostgreSQL</span></span>](concepts-connection-libraries.md)
