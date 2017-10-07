---
title: aaaAzure voorbeeldscript CLI - een web-app met web server-logboeken bewaken | Microsoft Docs
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
ms.openlocfilehash: 012b800c03af77387bed3d098fae3c96d82aee29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-web-app-with-web-server-logs"></a><span data-ttu-id="fb461-103">Een web-app met web server-logboeken bewaken</span><span class="sxs-lookup"><span data-stu-id="fb461-103">Monitor a web app with web server logs</span></span>

<span data-ttu-id="fb461-104">In dit scenario wordt u een resourcegroep, de app service-abonnement, de web-app maken en configureren van Hallo web app tooenable web server-Logboeken.</span><span class="sxs-lookup"><span data-stu-id="fb461-104">In this scenario you will create a resource group, app service plan, web app and configure hello web app tooenable web server logs.</span></span> <span data-ttu-id="fb461-105">Hallo-logboekbestanden voor revisie wordt vervolgens gedownload.</span><span class="sxs-lookup"><span data-stu-id="fb461-105">You will then download hello log files for review.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="fb461-106">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="fb461-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="fb461-107">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="fb461-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="fb461-108">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="fb461-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="fb461-109">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="fb461-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/monitor-with-logs/monitor-with-logs.sh "Monitor Logs")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="fb461-110">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="fb461-110">Script explanation</span></span>

<span data-ttu-id="fb461-111">Dit script maakt gebruik van Hallo opdrachten toocreate een resourcegroep, web-app en alle gerelateerde resources te volgen.</span><span class="sxs-lookup"><span data-stu-id="fb461-111">This script uses hello following commands toocreate a resource group, web app, and all related resources.</span></span> <span data-ttu-id="fb461-112">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="fb461-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="fb461-113">Opdracht</span><span class="sxs-lookup"><span data-stu-id="fb461-113">Command</span></span> | <span data-ttu-id="fb461-114">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="fb461-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fb461-115">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="fb461-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="fb461-116">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="fb461-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="fb461-117">AZ appservice-abonnement maken</span><span class="sxs-lookup"><span data-stu-id="fb461-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="fb461-118">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="fb461-118">Creates an App Service plan.</span></span> <span data-ttu-id="fb461-119">Dit is vergelijkbaar met een serverfarm voor uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="fb461-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="fb461-120">AZ webapp maken</span><span class="sxs-lookup"><span data-stu-id="fb461-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="fb461-121">Hiermee maakt u een Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="fb461-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="fb461-122">AZ webapp logboek config</span><span class="sxs-lookup"><span data-stu-id="fb461-122">az webapp log config</span></span>](https://docs.microsoft.com/cli/azure/webapp/log#config) | <span data-ttu-id="fb461-123">Hiermee configureert u welke logboeken van toepassing zijn op een Azure-web-app blijft.</span><span class="sxs-lookup"><span data-stu-id="fb461-123">Configures which logs an Azure web app will persist.</span></span> |
| [<span data-ttu-id="fb461-124">Meld u AZ webapp downloaden</span><span class="sxs-lookup"><span data-stu-id="fb461-124">az webapp log download</span></span>](https://docs.microsoft.com/cli/azure/webapp/log#download) | <span data-ttu-id="fb461-125">Downloads Hallo logboeken Hallo een Azure-web-app tooyour lokale machine.</span><span class="sxs-lookup"><span data-stu-id="fb461-125">Downloads hello logs of hello an Azure web app tooyour local machine.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fb461-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fb461-126">Next steps</span></span>

<span data-ttu-id="fb461-127">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fb461-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="fb461-128">Extra-App Service CLI scriptvoorbeelden kunnen u vinden in Hallo [Azure App Service-documentatie](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="fb461-128">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
