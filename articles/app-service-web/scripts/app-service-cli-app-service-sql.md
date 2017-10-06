---
title: aaaAzure voorbeeldscript CLI - verbinding maken met een web-app tooa SQL-database | Microsoft Docs
description: Azure CLI-Script steekproef - verbinding maken met een web-app tooa SQL-database
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 7c2efdd0-f553-4038-a77a-e953021b3f77
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: adee42cd659d977b49e71d974d240324f68f67f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-tooa-sql-database"></a><span data-ttu-id="2e753-103">Verbinding maken met een web-app tooa SQL-database</span><span class="sxs-lookup"><span data-stu-id="2e753-103">Connect a web app tooa SQL database</span></span>

<span data-ttu-id="2e753-104">In dit scenario leert u hoe toocreate een Azure SQL database en een Azure web-app.</span><span class="sxs-lookup"><span data-stu-id="2e753-104">In this scenario you will learn how toocreate an Azure SQL database and an Azure web app.</span></span> <span data-ttu-id="2e753-105">Vervolgens koppelt u Hallo SQL database toohello web-app met app-instellingen.</span><span class="sxs-lookup"><span data-stu-id="2e753-105">Then you will link hello SQL database toohello web app using app settings.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="2e753-106">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2e753-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="2e753-107">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="2e753-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="2e753-108">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2e753-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="2e753-109">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="2e753-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-sql/connect-to-sql.sh?highlight=9-10 "SQL Database")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="2e753-110">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="2e753-110">Script explanation</span></span>

<span data-ttu-id="2e753-111">Dit script maakt gebruik van Hallo opdrachten toocreate een resourcegroep, web-app, SQL-database en alle gerelateerde resources te volgen.</span><span class="sxs-lookup"><span data-stu-id="2e753-111">This script uses hello following commands toocreate a resource group, web app, SQL database and all related resources.</span></span> <span data-ttu-id="2e753-112">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="2e753-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="2e753-113">Opdracht</span><span class="sxs-lookup"><span data-stu-id="2e753-113">Command</span></span> | <span data-ttu-id="2e753-114">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="2e753-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2e753-115">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="2e753-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="2e753-116">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="2e753-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2e753-117">AZ appservice-abonnement maken</span><span class="sxs-lookup"><span data-stu-id="2e753-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="2e753-118">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="2e753-118">Creates an App Service plan.</span></span> <span data-ttu-id="2e753-119">Dit is vergelijkbaar met een serverfarm voor uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="2e753-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="2e753-120">AZ webapp maken</span><span class="sxs-lookup"><span data-stu-id="2e753-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="2e753-121">Hiermee maakt u een Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="2e753-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="2e753-122">AZ sql server maken</span><span class="sxs-lookup"><span data-stu-id="2e753-122">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="2e753-123">Hiermee maakt u een SQL Database-Server.</span><span class="sxs-lookup"><span data-stu-id="2e753-123">Creates a SQL Database Server.</span></span>  |
| [<span data-ttu-id="2e753-124">AZ sql-database maken</span><span class="sxs-lookup"><span data-stu-id="2e753-124">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="2e753-125">Maakt een nieuwe database met Hallo SQL Database-Server.</span><span class="sxs-lookup"><span data-stu-id="2e753-125">Creates a new database with hello SQL Database Server.</span></span> |
| [<span data-ttu-id="2e753-126">AZ webapp config appsettings instellen</span><span class="sxs-lookup"><span data-stu-id="2e753-126">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="2e753-127">Maken of bijwerken van een app-instelling voor een Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="2e753-127">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="2e753-128">App-instellingen worden weergegeven als omgevingsvariabelen voor uw app.</span><span class="sxs-lookup"><span data-stu-id="2e753-128">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2e753-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2e753-129">Next steps</span></span>

<span data-ttu-id="2e753-130">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2e753-130">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="2e753-131">Extra-App Service CLI scriptvoorbeelden kunnen u vinden in Hallo [Azure App Service-documentatie](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="2e753-131">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
