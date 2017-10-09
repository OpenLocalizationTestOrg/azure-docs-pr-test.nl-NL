---
title: aaaAzure voorbeeldscript CLI - Bind een aangepaste SSL-certificaat tooa web-app | Microsoft Docs
description: Azure CLI-voorbeeldscript - Bind een aangepaste SSL-certificaat tooa web-app
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: eb95d350-81ea-4145-a1e2-6eea3b7469b2
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 2fec2db84a2007fa6b005776c84d4f8cba392b46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="bind-a-custom-ssl-certificate-tooa-web-app"></a><span data-ttu-id="16606-103">Binden van een aangepaste SSL-certificaat tooa web-app</span><span class="sxs-lookup"><span data-stu-id="16606-103">Bind a custom SSL certificate tooa web app</span></span>

<span data-ttu-id="16606-104">Dit voorbeeldscript wordt gemaakt van een web-app in App Service met de bijbehorende resources en vervolgens Hallo SSL-certificaat van een aangepast domein naam tooit wordt gebonden.</span><span class="sxs-lookup"><span data-stu-id="16606-104">This sample script creates a web app in App Service with its related resources, then binds hello SSL certificate of a custom domain name tooit.</span></span> <span data-ttu-id="16606-105">Voor dit voorbeeld hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="16606-105">For this sample, you will need:</span></span>

* <span data-ttu-id="16606-106">Toegang tot pagina tooyour-domeinregistrar van DNS-configuratie.</span><span class="sxs-lookup"><span data-stu-id="16606-106">Access tooyour domain registrar's DNS configuration page.</span></span>
* <span data-ttu-id="16606-107">Een geldig. PFX-bestand en het bijbehorende wachtwoord voor Hallo SSL-certificaat u wilt dat tooupload en een binding.</span><span class="sxs-lookup"><span data-stu-id="16606-107">A valid .PFX file and its password for hello SSL certificate you want tooupload and bind.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="16606-108">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="16606-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="16606-109">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="16606-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="16606-110">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="16606-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="16606-111">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="16606-111">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate tooa web app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="16606-112">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="16606-112">Script explanation</span></span>

<span data-ttu-id="16606-113">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="16606-113">This script uses hello following commands.</span></span> <span data-ttu-id="16606-114">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="16606-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="16606-115">Opdracht</span><span class="sxs-lookup"><span data-stu-id="16606-115">Command</span></span> | <span data-ttu-id="16606-116">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="16606-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="16606-117">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="16606-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="16606-118">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="16606-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="16606-119">AZ appservice-abonnement maken</span><span class="sxs-lookup"><span data-stu-id="16606-119">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="16606-120">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="16606-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="16606-121">AZ webapp maken</span><span class="sxs-lookup"><span data-stu-id="16606-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="16606-122">Hiermee maakt u een Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="16606-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="16606-123">AZ webapp config hostnaam toevoegen</span><span class="sxs-lookup"><span data-stu-id="16606-123">az webapp config hostname add</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/hostname#add) | <span data-ttu-id="16606-124">Een aangepast domein tooa web-app wordt toegewezen.</span><span class="sxs-lookup"><span data-stu-id="16606-124">Maps a custom domain tooa web app.</span></span> |
| [<span data-ttu-id="16606-125">AZ webapp config ssl uploaden</span><span class="sxs-lookup"><span data-stu-id="16606-125">az webapp config ssl upload</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/ssl#upload) | <span data-ttu-id="16606-126">Een SSL-certificaat tooa web-app geüpload.</span><span class="sxs-lookup"><span data-stu-id="16606-126">Uploads an SSL certificate tooa web app.</span></span> |
| [<span data-ttu-id="16606-127">AZ webapp config ssl-binding</span><span class="sxs-lookup"><span data-stu-id="16606-127">az webapp config ssl bind</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/ssl#bind) | <span data-ttu-id="16606-128">Een geüploade SSL-certificaat tooa web-app, wordt gebonden.</span><span class="sxs-lookup"><span data-stu-id="16606-128">Binds an uploaded SSL certificate tooa web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="16606-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="16606-129">Next steps</span></span>

<span data-ttu-id="16606-130">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="16606-130">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="16606-131">Extra-App Service CLI scriptvoorbeelden kunnen u vinden in Hallo [Azure App Service-documentatie](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="16606-131">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
