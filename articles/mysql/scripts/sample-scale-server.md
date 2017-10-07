---
title: aaaAzure CLI voorbeelden tooscale een Azure-Database voor de MySQL-server | Microsoft Docs
description: Dit voorbeeldscript CLI schaalt Azure Database voor MySQL server tooa verschillende prestatieniveau na het uitvoeren van query's Hallo metrische gegevens.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: sample
ms.custom: mvc
ms.date: 05/31/2017
ms.openlocfilehash: 721ef9db35a5f3be7a38438c1abb724187b18b75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-scale-an-azure-database-for-mysql-server-using-azure-cli"></a><span data-ttu-id="101b5-103">Bewaken en schalen van een Azure-Database voor de MySQL-server met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="101b5-103">Monitor and scale an Azure Database for MySQL server using Azure CLI</span></span>
<span data-ttu-id="101b5-104">Dit voorbeeldscript CLI schaalt één Azure-Database voor MySQL server tooa verschillende prestatieniveau na het uitvoeren van query's Hallo metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="101b5-104">This sample CLI script scales a single Azure Database for MySQL server tooa different performance level after querying hello metrics.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="101b5-105">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="101b5-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="101b5-106">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="101b5-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="101b5-107">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="101b5-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="101b5-108">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="101b5-108">Sample script</span></span>
<span data-ttu-id="101b5-109">In dit voorbeeldscript Hallo gemarkeerde regels toocustomize Hallo beheerdersgebruikersnaam en wachtwoord te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="101b5-109">In this sample script, change hello highlighted lines toocustomize hello admin username and password.</span></span> <span data-ttu-id="101b5-110">Vervang Hallo abonnements-id in Hallo az monitor opdrachten met uw eigen abonnements-id gebruikt.[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/scale-mysql-server.sh?highlight=15-16 "Create and scale Azure Database for MySQL.")]</span><span class="sxs-lookup"><span data-stu-id="101b5-110">Replace hello subscription id used in hello az monitor commands with your own subscription id. [!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/scale-mysql-server.sh?highlight=15-16 "Create and scale Azure Database for MySQL.")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="101b5-111">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="101b5-111">Clean up deployment</span></span>
<span data-ttu-id="101b5-112">Na het uitvoeren van het voorbeeldscript Hallo mag na de opdracht Hallo gebruikte tooremove Hallo-resourcegroep en alle resources die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="101b5-112">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/delete-mysql.sh  "Delete hello resource group.")]

## <a name="script-explanation"></a><span data-ttu-id="101b5-113">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="101b5-113">Script explanation</span></span>
<span data-ttu-id="101b5-114">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="101b5-114">This script uses hello following commands.</span></span> <span data-ttu-id="101b5-115">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="101b5-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="101b5-116">**Opdracht**</span><span class="sxs-lookup"><span data-stu-id="101b5-116">**Command**</span></span> | <span data-ttu-id="101b5-117">**Opmerkingen bij de**</span><span class="sxs-lookup"><span data-stu-id="101b5-117">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="101b5-118">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="101b5-118">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="101b5-119">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="101b5-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="101b5-120">AZ mysql-server maken</span><span class="sxs-lookup"><span data-stu-id="101b5-120">az mysql server create</span></span>](/cli/azure/mysql/server#create) | <span data-ttu-id="101b5-121">Hiermee maakt u een MySQL-server die als host fungeert voor Hallo-databases.</span><span class="sxs-lookup"><span data-stu-id="101b5-121">Creates a MySQL server that hosts hello databases.</span></span> |
| [<span data-ttu-id="101b5-122">lijst met AZ monitor metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="101b5-122">az monitor metrics list</span></span>](/cli/azure/monitor/metrics#list) | <span data-ttu-id="101b5-123">Hallo metrische waarde voor Hallo resources weergeven.</span><span class="sxs-lookup"><span data-stu-id="101b5-123">List hello metric value for hello resources.</span></span> |
| [<span data-ttu-id="101b5-124">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="101b5-124">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="101b5-125">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="101b5-125">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="101b5-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="101b5-126">Next steps</span></span>
- <span data-ttu-id="101b5-127">Meer informatie over hello Azure CLI: [documentatie van Azure CLI](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="101b5-127">Read more information on hello Azure CLI: [Azure CLI documentation](/cli/azure/overview).</span></span>
- <span data-ttu-id="101b5-128">Probeer extra scripts: [voorbeelden van Azure CLI voor Azure-Database voor MySQL](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="101b5-128">Try additional scripts: [Azure CLI samples for Azure Database for MySQL](../sample-scripts-azure-cli.md)</span></span>
- <span data-ttu-id="101b5-129">Zie voor meer informatie over het schalen [Servicelagen](../concepts-service-tiers.md) en [Compute-eenheden en opslageenheden](../concepts-compute-unit-and-storage.md).</span><span class="sxs-lookup"><span data-stu-id="101b5-129">For more information on scaling, see [Service Tiers](../concepts-service-tiers.md) and [Compute Units and Storage Units](../concepts-compute-unit-and-storage.md).</span></span>
