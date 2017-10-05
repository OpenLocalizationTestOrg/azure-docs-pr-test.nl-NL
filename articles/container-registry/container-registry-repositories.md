---
title: Azure-container register opslagplaatsen | Microsoft Docs
description: "Het gebruik van Azure Container register-opslagplaatsen voor Docker-installatiekopieën"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: cristyg
ms.openlocfilehash: 06b809c31cecef1714f60d04657eb74c611be8cb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-container-registry-repositories"></a><span data-ttu-id="7afb4-103">Register-opslagplaatsen voor Azure-container</span><span class="sxs-lookup"><span data-stu-id="7afb4-103">Azure container registry repositories</span></span>

<span data-ttu-id="7afb4-104">Azure container register kunt u installatiekopieën van de container opslaan in de opslagplaatsen.</span><span class="sxs-lookup"><span data-stu-id="7afb4-104">Azure container registry allows you to store container images in repositories.</span></span> <span data-ttu-id="7afb4-105">Afbeeldingen in de opslagplaatsen opslaat, kunt u groepen van installatiekopieën (of de versie van afbeeldingen) in een geïsoleerde omgeving hebben.</span><span class="sxs-lookup"><span data-stu-id="7afb4-105">By storing images in repositories, you can have groups of images (or version of images) in isolated environments.</span></span> <span data-ttu-id="7afb4-106">U kunt deze opslagplaatsen opgeven wanneer u push-installatiekopieën toe aan het register.</span><span class="sxs-lookup"><span data-stu-id="7afb4-106">You can specify these repositories when you push images to your registry.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="7afb4-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7afb4-107">Prerequisites</span></span>
* <span data-ttu-id="7afb4-108">**Azure-containerregister**: maak een containerregister in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="7afb4-108">**Azure container registry** - Create a container registry in your Azure subscription.</span></span> <span data-ttu-id="7afb4-109">Gebruik bijvoorbeeld [Azure Portal](container-registry-get-started-portal.md) of de [Azure-CLI 2.0](container-registry-get-started-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="7afb4-109">For example, use the [Azure portal](container-registry-get-started-portal.md) or the [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span></span>
* <span data-ttu-id="7afb4-110">**Docker-CLI**: installeer de [Docker-engine](https://docs.docker.com/engine/installation/) om uw lokale computer als een Docker-host in te stellen en de Docker-CLI-opdrachten te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7afb4-110">**Docker CLI** - To set up your local computer as a Docker host and access the Docker CLI commands, install [Docker Engine](https://docs.docker.com/engine/installation/).</span></span>
* <span data-ttu-id="7afb4-111">**Pull-installatiekopie van een** - Pull-een afbeelding uit het register met openbare Docker-Hub, het labelen en dit doorgeven aan het register.</span><span class="sxs-lookup"><span data-stu-id="7afb4-111">**Pull an image** - Pull an image from the public Docker Hub registry, tag it, and push it to your registry.</span></span> <span data-ttu-id="7afb4-112">Voor instructies voor het pushen en installatiekopieën pull, Zie [Push Docker-installatiekopie in Azure persoonlijke register](container-registry-get-started-docker-cli.md).</span><span class="sxs-lookup"><span data-stu-id="7afb4-112">For guidance on how push and pull images, see [Push Docker image to Azure private registry](container-registry-get-started-docker-cli.md).</span></span>


## <a name="viewing-repositories-in-the-portal"></a><span data-ttu-id="7afb4-113">Opslagplaatsen weergeven in de Portal</span><span class="sxs-lookup"><span data-stu-id="7afb4-113">Viewing repositories in the Portal</span></span>

<span data-ttu-id="7afb4-114">Zodra u installatiekopieën toe aan het register van de container gepusht hebt, kunt u een overzicht van de opslagplaatsen die als host fungeert voor de afbeeldingen in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="7afb4-114">Once you have pushed images to your container registry, you can see a list of the repositories hosting the images in the Azure portal.</span></span>

<span data-ttu-id="7afb4-115">Als u de stappen in de [Push Docker-installatiekopie in Azure persoonlijke register](container-registry-get-started-docker-cli.md) artikel, u hebt nu een Nginx-installatiekopie in het register van de container.</span><span class="sxs-lookup"><span data-stu-id="7afb4-115">If you followed the steps in the [Push Docker image to Azure private registry](container-registry-get-started-docker-cli.md) article, you should now have a Nginx image in your container registry.</span></span> <span data-ttu-id="7afb4-116">Als onderdeel van de instructies, moet u een naamruimte voor de installatiekopie hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="7afb4-116">As part of the instructions, you should have specified a namespace for the image.</span></span> <span data-ttu-id="7afb4-117">In het onderstaande voorbeeld pushes de opdracht de installatiekopie van het NGinx naar de opslagplaats 'voorbeelden':</span><span class="sxs-lookup"><span data-stu-id="7afb4-117">In the example below, the command pushes the NGinx image to the "samples" repository:</span></span>

```
docker push myregistry.azurecr.io/samples/nginx
```
 <span data-ttu-id="7afb4-118">Azure Container Registry ondersteunt naamruimten voor opslagplaatsen op meerdere niveaus.</span><span class="sxs-lookup"><span data-stu-id="7afb4-118">Azure Container Registry supports multilevel repository namespaces.</span></span> <span data-ttu-id="7afb4-119">Met deze functie kunt u verzamelingen van installatiekopieën maken die gerelateerd zijn aan een specifieke app, of verzamelingen apps die gerelateerd zijn aan specifieke ontwikkelingsteams of operationele teams.</span><span class="sxs-lookup"><span data-stu-id="7afb4-119">This feature enables you to group collections of images related to a specific app, or a collection of apps to specific development or operational teams.</span></span> <span data-ttu-id="7afb4-120">Voor meer informatie over opslagplaatsen in container registers Zie [registers voor persoonlijke Docker-container in Azure](container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="7afb4-120">To read more about repositories in container registries, see [Private Docker container registries in Azure](container-registry-intro.md).</span></span>

<span data-ttu-id="7afb4-121">De container register-opslagplaatsen weergeven:</span><span class="sxs-lookup"><span data-stu-id="7afb4-121">To view the container registry repositories:</span></span>

1. <span data-ttu-id="7afb4-122">Aanmelden bij Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7afb4-122">Log in to the Azure portal</span></span>
2. <span data-ttu-id="7afb4-123">Op de **Azure Container register** blade, selecteert u het register die u wilt onderzoeken</span><span class="sxs-lookup"><span data-stu-id="7afb4-123">On the **Azure Container Registry** blade, select the registry you wish to inspect</span></span>
3. <span data-ttu-id="7afb4-124">Klik op de blade register **opslagplaatsen** om een lijst weer van alle opslagplaatsen en hun afbeeldingen</span><span class="sxs-lookup"><span data-stu-id="7afb4-124">In the registry blade, click **Repositories** to see a list of all the repositories and their images</span></span>
4. <span data-ttu-id="7afb4-125">(Optioneel) Selecteer een specifieke installatiekopie voor een overzicht van tags</span><span class="sxs-lookup"><span data-stu-id="7afb4-125">(Optional) Select a specific image to see tags</span></span>

![Opslagplaatsen in de portal](./media/container-registry-repositories/container-registry-repositories.png)


## <a name="next-steps"></a><span data-ttu-id="7afb4-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7afb4-127">Next steps</span></span>
<span data-ttu-id="7afb4-128">Nu u de basisprincipes kent, kunt u uw register gaan gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7afb4-128">Now that you know the basics, you are ready to start using your registry!</span></span> <span data-ttu-id="7afb4-129">Begin bijvoorbeeld met het implementeren van containerinstallatiekopieën op een [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/)-cluster.</span><span class="sxs-lookup"><span data-stu-id="7afb4-129">For example, start deploying container images to an [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span></span>
