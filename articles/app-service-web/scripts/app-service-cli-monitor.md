---
title: Azure CLI-voorbeeldscript - Monitor voor een web-app met web server-Logboeken | Microsoft Docs
description: Azure CLI-voorbeeldscript - Monitor voor een web-app met web server-Logboeken
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0887656f-611c-4627-8247-b5cded7cef60
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: df4ca5b1270ada849e231ad9608a5b1d2edda8be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-a-web-app-with-web-server-logs"></a><span data-ttu-id="afb3d-103">Een web-app met web server-logboeken bewaken</span><span class="sxs-lookup"><span data-stu-id="afb3d-103">Monitor a web app with web server logs</span></span>

<span data-ttu-id="afb3d-104">In dit scenario wordt u een resourcegroep, de app service-abonnement, de web-app maken en configureren van de web-app zodat web server-Logboeken.</span><span class="sxs-lookup"><span data-stu-id="afb3d-104">In this scenario you will create a resource group, app service plan, web app and configure the web app to enable web server logs.</span></span> <span data-ttu-id="afb3d-105">Vervolgens downloadt u de logboekbestanden voor revisie.</span><span class="sxs-lookup"><span data-stu-id="afb3d-105">You will then download the log files for review.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="afb3d-106">Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor dit onderwerp gebruikmaken van Azure CLI versie 2.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="afb3d-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="afb3d-107">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="afb3d-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="afb3d-108">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="afb3d-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="afb3d-109">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="afb3d-109">Sample script</span></span>

<span data-ttu-id="afb3d-110">[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/app-service/monitor-with-logs/monitor-with-logs.sh "logboeken van de Monitor")]</span><span class="sxs-lookup"><span data-stu-id="afb3d-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/monitor-with-logs/monitor-with-logs.sh "Monitor Logs")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="afb3d-111">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="afb3d-111">Script explanation</span></span>

<span data-ttu-id="afb3d-112">Dit script maakt gebruik van de volgende opdrachten voor het maken van een resourcegroep, web-app en alle gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="afb3d-112">This script uses the following commands to create a resource group, web app, and all related resources.</span></span> <span data-ttu-id="afb3d-113">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="afb3d-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="afb3d-114">Opdracht</span><span class="sxs-lookup"><span data-stu-id="afb3d-114">Command</span></span> | <span data-ttu-id="afb3d-115">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="afb3d-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="afb3d-116">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="afb3d-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="afb3d-117">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="afb3d-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="afb3d-118">AZ appservice-abonnement maken</span><span class="sxs-lookup"><span data-stu-id="afb3d-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="afb3d-119">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="afb3d-119">Creates an App Service plan.</span></span> <span data-ttu-id="afb3d-120">Dit is vergelijkbaar met een serverfarm voor uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="afb3d-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="afb3d-121">AZ webapp maken</span><span class="sxs-lookup"><span data-stu-id="afb3d-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="afb3d-122">Hiermee maakt u een Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="afb3d-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="afb3d-123">AZ webapp logboek config</span><span class="sxs-lookup"><span data-stu-id="afb3d-123">az webapp log config</span></span>](https://docs.microsoft.com/cli/azure/webapp/log#config) | <span data-ttu-id="afb3d-124">Hiermee configureert u welke logboeken van toepassing zijn op een Azure-web-app blijft.</span><span class="sxs-lookup"><span data-stu-id="afb3d-124">Configures which logs an Azure web app will persist.</span></span> |
| [<span data-ttu-id="afb3d-125">Meld u AZ webapp downloaden</span><span class="sxs-lookup"><span data-stu-id="afb3d-125">az webapp log download</span></span>](https://docs.microsoft.com/cli/azure/webapp/log#download) | <span data-ttu-id="afb3d-126">Downloadt de logboeken van de een Azure-web-app op uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="afb3d-126">Downloads the logs of the an Azure web app to your local machine.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="afb3d-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="afb3d-127">Next steps</span></span>

<span data-ttu-id="afb3d-128">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="afb3d-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="afb3d-129">Extra-App Service CLI scriptvoorbeelden vindt u in de [Azure App Service-documentatie](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="afb3d-129">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
