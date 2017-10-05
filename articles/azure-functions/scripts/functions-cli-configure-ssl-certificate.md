---
title: Azure CLI-voorbeeldscript - Bind een aangepaste SSL-certificaat voor een functie-app | Microsoft Docs
description: Azure CLI-voorbeeldscript - Bind een aangepaste SSL-certificaat voor een functie-app in Azure
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
ms.openlocfilehash: ddabb701d7d5615232d1f6163aa6fb166efe5cb0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="bind-a-custom-ssl-certificate-to-a-function-app"></a><span data-ttu-id="6968f-103">Een aangepaste SSL-certificaat binden aan een functie-app</span><span class="sxs-lookup"><span data-stu-id="6968f-103">Bind a custom SSL certificate to a function app</span></span>

<span data-ttu-id="6968f-104">Dit voorbeeldscript wordt een functie-app in App Service gemaakt met de bijbehorende resources en vervolgens koppelt het SSL-certificaat van een aangepaste domeinnaam aan deze.</span><span class="sxs-lookup"><span data-stu-id="6968f-104">This sample script creates a function app in App Service with its related resources, then binds the SSL certificate of a custom domain name to it.</span></span> <span data-ttu-id="6968f-105">Voor dit voorbeeld hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="6968f-105">For this sample, you need:</span></span>

* <span data-ttu-id="6968f-106">Toegang tot de pagina voor DNS-configuratie van uw domeinregistrar.</span><span class="sxs-lookup"><span data-stu-id="6968f-106">Access to your domain registrar's DNS configuration page.</span></span>
* <span data-ttu-id="6968f-107">Een geldig. PFX-bestand en het bijbehorende wachtwoord voor het SSL-certificaat dat u wilt uploaden en binden.</span><span class="sxs-lookup"><span data-stu-id="6968f-107">A valid .PFX file and its password for the SSL certificate you want to upload and bind.</span></span>

<span data-ttu-id="6968f-108">Als u wilt een SSL-certificaat bindt, moet uw app in de functie worden gemaakt in een App Service-plan en niet in een plan verbruik.</span><span class="sxs-lookup"><span data-stu-id="6968f-108">To bind an SSL certificate, your function app must be created in an App Service plan and not in a consumption plan.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6968f-109">Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor dit onderwerp gebruikmaken van Azure CLI versie 2.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="6968f-109">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="6968f-110">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="6968f-110">Run `az --version` to find the version.</span></span> <span data-ttu-id="6968f-111">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6968f-111">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="6968f-112">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="6968f-112">Sample script</span></span>

<span data-ttu-id="6968f-113">[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/azure-functions/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "een aangepaste SSL-certificaat binden aan een web-app")]</span><span class="sxs-lookup"><span data-stu-id="6968f-113">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="6968f-114">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="6968f-114">Script explanation</span></span>

<span data-ttu-id="6968f-115">Dit script maakt gebruik van de volgende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="6968f-115">This script uses the following commands.</span></span> <span data-ttu-id="6968f-116">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="6968f-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="6968f-117">Opdracht</span><span class="sxs-lookup"><span data-stu-id="6968f-117">Command</span></span> | <span data-ttu-id="6968f-118">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="6968f-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6968f-119">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="6968f-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="6968f-120">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="6968f-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6968f-121">AZ appservice-abonnement maken</span><span class="sxs-lookup"><span data-stu-id="6968f-121">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="6968f-122">Hiermee maakt u een App Service-abonnement vereist voor het binden van SSL-certificaten.</span><span class="sxs-lookup"><span data-stu-id="6968f-122">Creates an App Service plan required to bind SSL certificates.</span></span> |
| [<span data-ttu-id="6968f-123">AZ functionapp maken</span><span class="sxs-lookup"><span data-stu-id="6968f-123">az functionapp create</span></span>]() | <span data-ttu-id="6968f-124">Hiermee maakt u een functie-app.</span><span class="sxs-lookup"><span data-stu-id="6968f-124">Creates a function app.</span></span> |
| [<span data-ttu-id="6968f-125">AZ appservice web config hostnaam toevoegen</span><span class="sxs-lookup"><span data-stu-id="6968f-125">az appservice web config hostname add</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | <span data-ttu-id="6968f-126">Een aangepast domein wordt toegewezen aan de functie-app.</span><span class="sxs-lookup"><span data-stu-id="6968f-126">Maps a custom domain to the function app.</span></span> |
| [<span data-ttu-id="6968f-127">AZ appservice web config ssl uploaden</span><span class="sxs-lookup"><span data-stu-id="6968f-127">az appservice web config ssl upload</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/ssl#upload) | <span data-ttu-id="6968f-128">Een SSL-certificaat naar een functie-app geüpload.</span><span class="sxs-lookup"><span data-stu-id="6968f-128">Uploads an SSL certificate to a function app.</span></span> |
| [<span data-ttu-id="6968f-129">AZ appservice web config ssl-binding</span><span class="sxs-lookup"><span data-stu-id="6968f-129">az appservice web config ssl bind</span></span>](https://docs.microsoft.com/en-us/cli/azure/appservice/web/config/ssl#bind) | <span data-ttu-id="6968f-130">Een geüploade SSL-certificaat koppelt aan een functie-app.</span><span class="sxs-lookup"><span data-stu-id="6968f-130">Binds an uploaded SSL certificate to a function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6968f-131">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6968f-131">Next steps</span></span>

<span data-ttu-id="6968f-132">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6968f-132">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6968f-133">Extra-App Service CLI scriptvoorbeelden vindt u in de [Azure App Service-documentatie]().</span><span class="sxs-lookup"><span data-stu-id="6968f-133">Additional App Service CLI script samples can be found in the [Azure App Service documentation]().</span></span>
