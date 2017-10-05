---
title: Azure CLI-Script voorbeeld - web-app verbinden met een SQL database | Microsoft Docs
description: 'Azure CLI-Script voorbeeld: een WebApp verbinden met een SQL-database'
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
ms.openlocfilehash: ec5e22bfacc12a89f1fb5882487df4829369777c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="connect-a-web-app-to-a-sql-database"></a><span data-ttu-id="1462b-103">Een WebApp verbinden met een SQL-database</span><span class="sxs-lookup"><span data-stu-id="1462b-103">Connect a web app to a SQL database</span></span>

<span data-ttu-id="1462b-104">In dit scenario leert u hoe u een Azure SQL database en een Azure-web-app maakt.</span><span class="sxs-lookup"><span data-stu-id="1462b-104">In this scenario you will learn how to create an Azure SQL database and an Azure web app.</span></span> <span data-ttu-id="1462b-105">Vervolgens koppelt u de SQL-database aan de web-app met behulp van appinstellingen.</span><span class="sxs-lookup"><span data-stu-id="1462b-105">Then you will link the SQL database to the web app using app settings.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="1462b-106">Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor dit onderwerp gebruikmaken van Azure CLI versie 2.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="1462b-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="1462b-107">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="1462b-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="1462b-108">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="1462b-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="1462b-109">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="1462b-109">Sample script</span></span>

<span data-ttu-id="1462b-110">[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/app-service/connect-to-sql/connect-to-sql.sh?highlight=9-10 "SQL-Database")]</span><span class="sxs-lookup"><span data-stu-id="1462b-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-sql/connect-to-sql.sh?highlight=9-10 "SQL Database")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="1462b-111">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="1462b-111">Script explanation</span></span>

<span data-ttu-id="1462b-112">Dit script maakt gebruik van de volgende opdrachten voor het maken van een resourcegroep, web-app, SQL-database en alle gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="1462b-112">This script uses the following commands to create a resource group, web app, SQL database and all related resources.</span></span> <span data-ttu-id="1462b-113">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="1462b-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="1462b-114">Opdracht</span><span class="sxs-lookup"><span data-stu-id="1462b-114">Command</span></span> | <span data-ttu-id="1462b-115">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="1462b-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1462b-116">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="1462b-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="1462b-117">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="1462b-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1462b-118">AZ appservice-abonnement maken</span><span class="sxs-lookup"><span data-stu-id="1462b-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="1462b-119">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="1462b-119">Creates an App Service plan.</span></span> <span data-ttu-id="1462b-120">Dit is vergelijkbaar met een serverfarm voor uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="1462b-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="1462b-121">AZ webapp maken</span><span class="sxs-lookup"><span data-stu-id="1462b-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="1462b-122">Hiermee maakt u een Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="1462b-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="1462b-123">AZ sql server maken</span><span class="sxs-lookup"><span data-stu-id="1462b-123">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="1462b-124">Hiermee maakt u een SQL Database-Server.</span><span class="sxs-lookup"><span data-stu-id="1462b-124">Creates a SQL Database Server.</span></span>  |
| [<span data-ttu-id="1462b-125">AZ sql-database maken</span><span class="sxs-lookup"><span data-stu-id="1462b-125">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="1462b-126">Maakt een nieuwe database met SQL Database-Server.</span><span class="sxs-lookup"><span data-stu-id="1462b-126">Creates a new database with the SQL Database Server.</span></span> |
| [<span data-ttu-id="1462b-127">AZ webapp config appsettings instellen</span><span class="sxs-lookup"><span data-stu-id="1462b-127">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="1462b-128">Maken of bijwerken van een app-instelling voor een Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="1462b-128">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="1462b-129">App-instellingen worden weergegeven als omgevingsvariabelen voor uw app.</span><span class="sxs-lookup"><span data-stu-id="1462b-129">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1462b-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1462b-130">Next steps</span></span>

<span data-ttu-id="1462b-131">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1462b-131">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="1462b-132">Extra-App Service CLI scriptvoorbeelden vindt u in de [Azure App Service-documentatie](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="1462b-132">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
