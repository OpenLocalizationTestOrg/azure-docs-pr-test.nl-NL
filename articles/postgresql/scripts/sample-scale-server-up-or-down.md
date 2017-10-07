---
title: aaa "Azure CLI Script Scale Azure voor PostgreSQL-Database | Microsoft Docs'
description: 'Azure CLI - voorbeeldscript: de schaal Azure-Database voor PostgreSQL tooa verschillende prestatieniveau van de server na het uitvoeren van query''s Hallo metrische gegevens.'
services: postgresql
author: salonisonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.custom: mvc
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: 678b28941dbb4334cb374d4888991a00b44966b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-scale-a-single-postgresql-server-using-azure-cli"></a><span data-ttu-id="d9fa9-103">Bewaken en schalen van één PostgreSQL-server met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d9fa9-103">Monitor and scale a single PostgreSQL server using Azure CLI</span></span>
<span data-ttu-id="d9fa9-104">Dit voorbeeldscript CLI schaalt één Azure-Database voor PostgreSQL server tooa verschillende prestatieniveau na het uitvoeren van query's Hallo metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="d9fa9-104">This sample CLI script scales a single Azure Database for PostgreSQL server tooa different performance level after querying hello metrics.</span></span> 

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d9fa9-105">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d9fa9-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="d9fa9-106">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="d9fa9-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="d9fa9-107">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d9fa9-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="d9fa9-108">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="d9fa9-108">Sample script</span></span>
<span data-ttu-id="d9fa9-109">In dit voorbeeldscript Hallo gemarkeerde regels toocustomize Hallo beheerdersgebruikersnaam en wachtwoord te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="d9fa9-109">In this sample script, change hello highlighted lines toocustomize hello admin username and password.</span></span> <span data-ttu-id="d9fa9-110">Vervang Hallo abonnements-id in Hallo az monitor opdrachten met uw eigen abonnements-id gebruikt.[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/scale-postgresql-server.sh?highlight=15-16 "Create and scale Azure Database for PostgreSQL.")]</span><span class="sxs-lookup"><span data-stu-id="d9fa9-110">Replace hello subscription id used in hello az monitor commands with your own subscription id. [!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/scale-postgresql-server.sh?highlight=15-16 "Create and scale Azure Database for PostgreSQL.")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="d9fa9-111">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="d9fa9-111">Clean up deployment</span></span>
<span data-ttu-id="d9fa9-112">Na het uitvoeren van het voorbeeldscript Hallo mag na de opdracht Hallo gebruikte tooremove Hallo-resourcegroep en alle resources die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="d9fa9-112">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/delete-postgresql.sh "Delete hello resource group.")]

## <a name="script-explanation"></a><span data-ttu-id="d9fa9-113">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="d9fa9-113">Script explanation</span></span>
<span data-ttu-id="d9fa9-114">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="d9fa9-114">This script uses hello following commands.</span></span> <span data-ttu-id="d9fa9-115">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="d9fa9-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="d9fa9-116">**Opdracht**</span><span class="sxs-lookup"><span data-stu-id="d9fa9-116">**Command**</span></span> | <span data-ttu-id="d9fa9-117">**Opmerkingen bij de**</span><span class="sxs-lookup"><span data-stu-id="d9fa9-117">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="d9fa9-118">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="d9fa9-118">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="d9fa9-119">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="d9fa9-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d9fa9-120">AZ postgres server maken</span><span class="sxs-lookup"><span data-stu-id="d9fa9-120">az postgres server create</span></span>](/cli/azure/postgres/server#create) | <span data-ttu-id="d9fa9-121">Maakt een PostgreSQL-server die als host fungeert voor Hallo-databases.</span><span class="sxs-lookup"><span data-stu-id="d9fa9-121">Creates a PostgreSQL server that hosts hello databases.</span></span> |
| [<span data-ttu-id="d9fa9-122">lijst met AZ monitor metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="d9fa9-122">az monitor metrics list</span></span>](/cli/azure/monitor/metrics#list) | <span data-ttu-id="d9fa9-123">Hallo metrische waarde voor Hallo resources weergeven.</span><span class="sxs-lookup"><span data-stu-id="d9fa9-123">List hello metric value for hello resources.</span></span> |
| [<span data-ttu-id="d9fa9-124">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="d9fa9-124">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="d9fa9-125">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="d9fa9-125">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d9fa9-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d9fa9-126">Next steps</span></span>
- <span data-ttu-id="d9fa9-127">Meer informatie over hello Azure CLI: [Azure CLI-documentatie](/cli/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="d9fa9-127">Read more information on hello Azure CLI: [Azure CLI documentation](/cli/azure/overview)</span></span>
- <span data-ttu-id="d9fa9-128">Probeer extra scripts: [voorbeelden van Azure CLI voor Azure-Database voor PostgreSQL](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="d9fa9-128">Try additional scripts: [Azure CLI samples for Azure Database for PostgreSQL](../sample-scripts-azure-cli.md)</span></span>
- <span data-ttu-id="d9fa9-129">Meer informatie over het schalen: [Servicelagen](../concepts-service-tiers.md) en [Compute-eenheden en de eenheden voor opslag](../concepts-compute-unit-and-storage.md)</span><span class="sxs-lookup"><span data-stu-id="d9fa9-129">Read more information on scaling: [Service Tiers](../concepts-service-tiers.md) and [Compute Units and Storage Units](../concepts-compute-unit-and-storage.md)</span></span>
