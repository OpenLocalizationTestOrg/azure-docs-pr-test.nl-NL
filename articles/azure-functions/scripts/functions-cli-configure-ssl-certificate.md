---
title: aaaAzure voorbeeldscript CLI - Bind een aangepaste SSL-certificaat tooa functie-app | Microsoft Docs
description: Azure CLI-voorbeeldscript - Bind een aangepaste SSL-certificaat tooa functie-app in Azure
services: functions
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: eb95d350-81ea-4145-a1e2-6eea3b7469b2
ms.service: functions
ms.workload: na
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 04/10/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 692dbc03583f2978131823083f1bfd257882664c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="bind-a-custom-ssl-certificate-tooa-function-app"></a><span data-ttu-id="12646-103">Binden van een aangepaste SSL-certificaat tooa functie-app</span><span class="sxs-lookup"><span data-stu-id="12646-103">Bind a custom SSL certificate tooa function app</span></span>

<span data-ttu-id="12646-104">Dit voorbeeldscript wordt gemaakt van een functie-app in App Service met de bijbehorende resources en vervolgens Hallo SSL-certificaat van een aangepast domein naam tooit wordt gebonden.</span><span class="sxs-lookup"><span data-stu-id="12646-104">This sample script creates a function app in App Service with its related resources, then binds hello SSL certificate of a custom domain name tooit.</span></span> <span data-ttu-id="12646-105">Voor dit voorbeeld hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="12646-105">For this sample, you need:</span></span>

* <span data-ttu-id="12646-106">Toegang tot pagina tooyour-domeinregistrar van DNS-configuratie.</span><span class="sxs-lookup"><span data-stu-id="12646-106">Access tooyour domain registrar's DNS configuration page.</span></span>
* <span data-ttu-id="12646-107">Een geldig. PFX-bestand en het bijbehorende wachtwoord voor Hallo SSL-certificaat u wilt dat tooupload en een binding.</span><span class="sxs-lookup"><span data-stu-id="12646-107">A valid .PFX file and its password for hello SSL certificate you want tooupload and bind.</span></span>

<span data-ttu-id="12646-108">toobind een SSL-certificaat, de functie-app moet worden gemaakt in een App Service-plan en niet in een plan verbruik.</span><span class="sxs-lookup"><span data-stu-id="12646-108">toobind an SSL certificate, your function app must be created in an App Service plan and not in a consumption plan.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="12646-109">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="12646-109">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="12646-110">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="12646-110">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="12646-111">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="12646-111">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="12646-112">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="12646-112">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate tooa web app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="12646-113">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="12646-113">Script explanation</span></span>

<span data-ttu-id="12646-114">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="12646-114">This script uses hello following commands.</span></span> <span data-ttu-id="12646-115">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="12646-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="12646-116">Opdracht</span><span class="sxs-lookup"><span data-stu-id="12646-116">Command</span></span> | <span data-ttu-id="12646-117">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="12646-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="12646-118">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="12646-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="12646-119">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="12646-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="12646-120">AZ appservice-abonnement maken</span><span class="sxs-lookup"><span data-stu-id="12646-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="12646-121">Hiermee maakt u een App Service-abonnement vereist toobind SSL-certificaten.</span><span class="sxs-lookup"><span data-stu-id="12646-121">Creates an App Service plan required toobind SSL certificates.</span></span> |
| [<span data-ttu-id="12646-122">AZ functionapp maken</span><span class="sxs-lookup"><span data-stu-id="12646-122">az functionapp create</span></span>]() | <span data-ttu-id="12646-123">Hiermee maakt u een functie-app.</span><span class="sxs-lookup"><span data-stu-id="12646-123">Creates a function app.</span></span> |
| [<span data-ttu-id="12646-124">AZ appservice web config hostnaam toevoegen</span><span class="sxs-lookup"><span data-stu-id="12646-124">az appservice web config hostname add</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | <span data-ttu-id="12646-125">Een aangepast domein toohello functie-app wordt toegewezen.</span><span class="sxs-lookup"><span data-stu-id="12646-125">Maps a custom domain toohello function app.</span></span> |
| [<span data-ttu-id="12646-126">AZ appservice web config ssl uploaden</span><span class="sxs-lookup"><span data-stu-id="12646-126">az appservice web config ssl upload</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/ssl#upload) | <span data-ttu-id="12646-127">Een SSL-certificaat tooa functie-app geüpload.</span><span class="sxs-lookup"><span data-stu-id="12646-127">Uploads an SSL certificate tooa function app.</span></span> |
| [<span data-ttu-id="12646-128">AZ appservice web config ssl-binding</span><span class="sxs-lookup"><span data-stu-id="12646-128">az appservice web config ssl bind</span></span>](https://docs.microsoft.com/en-us/cli/azure/appservice/web/config/ssl#bind) | <span data-ttu-id="12646-129">Een geüploade SSL-certificaat tooa functie-app, wordt gebonden.</span><span class="sxs-lookup"><span data-stu-id="12646-129">Binds an uploaded SSL certificate tooa function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="12646-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="12646-130">Next steps</span></span>

<span data-ttu-id="12646-131">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="12646-131">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="12646-132">Extra-App Service CLI scriptvoorbeelden kunnen u vinden in Hallo [Azure App Service-documentatie]().</span><span class="sxs-lookup"><span data-stu-id="12646-132">Additional App Service CLI script samples can be found in hello [Azure App Service documentation]().</span></span>
