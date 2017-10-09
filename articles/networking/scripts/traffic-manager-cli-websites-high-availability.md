---
title: aaaAzure voorbeeldscript CLI - routeverkeer voor hoge beschikbaarheid van toepassingen | Microsoft Docs
description: Azure CLI-voorbeeldscript - routeverkeer voor hoge beschikbaarheid van toepassingen
services: traffic-manager
documentationcenter: traffic-manager
author: KumudD
manager: timlt
editor: tysonn
tags: azure-infrastructure
ms.assetid: 
ms.service: traffic-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: traffic-manager
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 2142c8bbec1dffc2f12b5500df142a429393a145
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a><span data-ttu-id="2a8cf-103">Verkeer leiden voor hoge beschikbaarheid van toepassingen</span><span class="sxs-lookup"><span data-stu-id="2a8cf-103">Route traffic for high availability of applications</span></span>

<span data-ttu-id="2a8cf-104">Dit script maakt een resourcegroep, twee app-serviceabonnementen, twee web-apps, een traffic manager-profiel en twee traffic manager-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="2a8cf-104">This script creates a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="2a8cf-105">Traffic Manager stuurt verkeer toohello toepassing in één regio bevinden als de primaire regio Hallo en de secundaire regio toohello wanneer Hallo-toepassing in Hallo primaire regio niet beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="2a8cf-105">Traffic Manager directs traffic toohello application in one region as hello primary region, and toohello secondary region when hello application in hello primary region is unavailable.</span></span> <span data-ttu-id="2a8cf-106">Voordat u Hallo script wordt uitgevoerd, moet u Hallo MyWebApp, MyWebAppL1 en MyWebAppL2 waarden toounique waarden in Azure.</span><span class="sxs-lookup"><span data-stu-id="2a8cf-106">Before executing hello script, you must change hello MyWebApp, MyWebAppL1 and MyWebAppL2 values toounique values across Azure.</span></span> <span data-ttu-id="2a8cf-107">Na het uitvoeren van script hello, kunt u in de primaire regio Hallo met Hallo URL mywebapp.trafficmanager.net Hallo app openen.</span><span class="sxs-lookup"><span data-stu-id="2a8cf-107">After running hello script, you can access hello app in hello primary region with hello URL mywebapp.trafficmanager.net.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="2a8cf-108">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="2a8cf-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.sh "Route traffic for high availability")]


## <a name="clean-up-deployment"></a><span data-ttu-id="2a8cf-109">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="2a8cf-109">Clean up deployment</span></span> 

<span data-ttu-id="2a8cf-110">Na het uitvoeren van het voorbeeldscript Hallo is Hallo Volg opdracht gebruikte tooremove Hallo-resourcegroep, App Service-app en alle gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="2a8cf-110">After hello script sample has been run, hello follow command can be used tooremove hello resource group, App Service app, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup1 --yes
az group delete --name myResourceGroup2 --yes
```

## <a name="script-explanation"></a><span data-ttu-id="2a8cf-111">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="2a8cf-111">Script explanation</span></span>

<span data-ttu-id="2a8cf-112">Dit script gebruikt Hallo opdrachten toocreate een resourcegroep, web-app, traffic manager-profiel te volgen en alle bijbehorende resources.</span><span class="sxs-lookup"><span data-stu-id="2a8cf-112">This script uses hello following commands toocreate a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="2a8cf-113">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="2a8cf-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="2a8cf-114">Opdracht</span><span class="sxs-lookup"><span data-stu-id="2a8cf-114">Command</span></span> | <span data-ttu-id="2a8cf-115">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="2a8cf-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2a8cf-116">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="2a8cf-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="2a8cf-117">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="2a8cf-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2a8cf-118">AZ appservice-abonnement maken</span><span class="sxs-lookup"><span data-stu-id="2a8cf-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="2a8cf-119">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="2a8cf-119">Creates an App Service plan.</span></span> <span data-ttu-id="2a8cf-120">Dit is vergelijkbaar met een serverfarm voor uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="2a8cf-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="2a8cf-121">AZ appservice web maken</span><span class="sxs-lookup"><span data-stu-id="2a8cf-121">az appservice web create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#create) | <span data-ttu-id="2a8cf-122">Hiermee maakt u een Azure-web-app in het Hallo-App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="2a8cf-122">Creates an Azure web app within hello App Service plan.</span></span> |
| [<span data-ttu-id="2a8cf-123">AZ netwerk traffic manager-profiel maken</span><span class="sxs-lookup"><span data-stu-id="2a8cf-123">az network traffic-manager profile create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | <span data-ttu-id="2a8cf-124">Een Azure Traffic Manager-profiel maakt.</span><span class="sxs-lookup"><span data-stu-id="2a8cf-124">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="2a8cf-125">netwerkeindpunt voor het traffic manager AZ maken</span><span class="sxs-lookup"><span data-stu-id="2a8cf-125">az network traffic-manager endpoint create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | <span data-ttu-id="2a8cf-126">Voegt een eindpunt tooan Azure Traffic Manager-profiel.</span><span class="sxs-lookup"><span data-stu-id="2a8cf-126">Adds a endpoint tooan Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2a8cf-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2a8cf-127">Next steps</span></span>

<span data-ttu-id="2a8cf-128">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2a8cf-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="2a8cf-129">Extra-App Service CLI scriptvoorbeelden kunnen u vinden in Hallo [documentatie Azure Networking](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="2a8cf-129">Additional App Service CLI script samples can be found in hello [Azure Networking documentation](../cli-samples.md).</span></span>
