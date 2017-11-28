---
title: Azure CLI-voorbeeldscript - Bind een aangepaste SSL-certificaat voor een web-app | Microsoft Docs
description: Azure CLI-voorbeeldscript - Bind een aangepaste SSL-certificaat voor een web-app
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
ms.openlocfilehash: d4fab3fb2c297bf5f498b63bee46692febb9180b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="bind-a-custom-ssl-certificate-to-a-web-app"></a><span data-ttu-id="80866-103">Een aangepaste SSL-certificaat binden aan een web-app</span><span class="sxs-lookup"><span data-stu-id="80866-103">Bind a custom SSL certificate to a web app</span></span>

<span data-ttu-id="80866-104">Dit voorbeeldscript wordt een web-app in App Service gemaakt met de bijbehorende resources en vervolgens koppelt het SSL-certificaat van een aangepaste domeinnaam aan deze.</span><span class="sxs-lookup"><span data-stu-id="80866-104">This sample script creates a web app in App Service with its related resources, then binds the SSL certificate of a custom domain name to it.</span></span> <span data-ttu-id="80866-105">Voor dit voorbeeld hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="80866-105">For this sample, you will need:</span></span>

* <span data-ttu-id="80866-106">Toegang tot de pagina voor DNS-configuratie van uw domeinregistrar.</span><span class="sxs-lookup"><span data-stu-id="80866-106">Access to your domain registrar's DNS configuration page.</span></span>
* <span data-ttu-id="80866-107">Een geldig. PFX-bestand en het bijbehorende wachtwoord voor het SSL-certificaat dat u wilt uploaden en binden.</span><span class="sxs-lookup"><span data-stu-id="80866-107">A valid .PFX file and its password for the SSL certificate you want to upload and bind.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="80866-108">Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor dit onderwerp gebruikmaken van Azure CLI versie 2.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="80866-108">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="80866-109">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="80866-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="80866-110">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="80866-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="80866-111">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="80866-111">Sample script</span></span>

<span data-ttu-id="80866-112">[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "een aangepaste SSL-certificaat binden aan een web-app")]</span><span class="sxs-lookup"><span data-stu-id="80866-112">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="80866-113">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="80866-113">Script explanation</span></span>

<span data-ttu-id="80866-114">Dit script maakt gebruik van de volgende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="80866-114">This script uses the following commands.</span></span> <span data-ttu-id="80866-115">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="80866-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="80866-116">Opdracht</span><span class="sxs-lookup"><span data-stu-id="80866-116">Command</span></span> | <span data-ttu-id="80866-117">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="80866-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="80866-118">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="80866-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="80866-119">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="80866-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="80866-120">AZ appservice-abonnement maken</span><span class="sxs-lookup"><span data-stu-id="80866-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="80866-121">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="80866-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="80866-122">AZ webapp maken</span><span class="sxs-lookup"><span data-stu-id="80866-122">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="80866-123">Hiermee maakt u een Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="80866-123">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="80866-124">AZ webapp config hostnaam toevoegen</span><span class="sxs-lookup"><span data-stu-id="80866-124">az webapp config hostname add</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/hostname#add) | <span data-ttu-id="80866-125">Een aangepast domein wordt toegewezen aan een web-app.</span><span class="sxs-lookup"><span data-stu-id="80866-125">Maps a custom domain to a web app.</span></span> |
| [<span data-ttu-id="80866-126">AZ webapp config ssl uploaden</span><span class="sxs-lookup"><span data-stu-id="80866-126">az webapp config ssl upload</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/ssl#upload) | <span data-ttu-id="80866-127">Een SSL-certificaat naar een web-app geüpload.</span><span class="sxs-lookup"><span data-stu-id="80866-127">Uploads an SSL certificate to a web app.</span></span> |
| [<span data-ttu-id="80866-128">AZ webapp config ssl-binding</span><span class="sxs-lookup"><span data-stu-id="80866-128">az webapp config ssl bind</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/ssl#bind) | <span data-ttu-id="80866-129">Een geüploade SSL-certificaat koppelt aan een web-app.</span><span class="sxs-lookup"><span data-stu-id="80866-129">Binds an uploaded SSL certificate to a web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="80866-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="80866-130">Next steps</span></span>

<span data-ttu-id="80866-131">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="80866-131">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="80866-132">Extra-App Service CLI scriptvoorbeelden vindt u in de [Azure App Service-documentatie](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="80866-132">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
