---
title: aaaAzure container register opslagplaatsen | Microsoft Docs
description: "Hoe toouse Azure Container register opslagplaatsen voor Docker-installatiekopieën"
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
ms.openlocfilehash: 108622c565e41777fbb1fc9da9a01168abc7a7fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-registry-repositories"></a><span data-ttu-id="96acc-103">Register-opslagplaatsen voor Azure-container</span><span class="sxs-lookup"><span data-stu-id="96acc-103">Azure container registry repositories</span></span>

<span data-ttu-id="96acc-104">Azure-container register kunt u toostore container afbeeldingen in de opslagplaatsen.</span><span class="sxs-lookup"><span data-stu-id="96acc-104">Azure container registry allows you toostore container images in repositories.</span></span> <span data-ttu-id="96acc-105">Afbeeldingen in de opslagplaatsen opslaat, kunt u groepen van installatiekopieën (of de versie van afbeeldingen) in een geïsoleerde omgeving hebben.</span><span class="sxs-lookup"><span data-stu-id="96acc-105">By storing images in repositories, you can have groups of images (or version of images) in isolated environments.</span></span> <span data-ttu-id="96acc-106">U kunt deze opslagplaatsen opgeven wanneer u push-installatiekopieën tooyour register.</span><span class="sxs-lookup"><span data-stu-id="96acc-106">You can specify these repositories when you push images tooyour registry.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="96acc-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="96acc-107">Prerequisites</span></span>
* <span data-ttu-id="96acc-108">**Azure-containerregister**: maak een containerregister in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="96acc-108">**Azure container registry** - Create a container registry in your Azure subscription.</span></span> <span data-ttu-id="96acc-109">Gebruik bijvoorbeeld Hallo [Azure-portal](container-registry-get-started-portal.md) of Hallo [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="96acc-109">For example, use hello [Azure portal](container-registry-get-started-portal.md) or hello [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span></span>
* <span data-ttu-id="96acc-110">**Docker CLI** -tooset van uw lokale computer als een Docker-host en toegang Hallo Docker CLI-opdrachten, installeren [Docker-Engine](https://docs.docker.com/engine/installation/).</span><span class="sxs-lookup"><span data-stu-id="96acc-110">**Docker CLI** - tooset up your local computer as a Docker host and access hello Docker CLI commands, install [Docker Engine](https://docs.docker.com/engine/installation/).</span></span>
* <span data-ttu-id="96acc-111">**Pull-installatiekopie van een** - Pull-een afbeelding uit het register van Hallo openbare Docker-Hub, het labelen en dit tooyour register doorgeven.</span><span class="sxs-lookup"><span data-stu-id="96acc-111">**Pull an image** - Pull an image from hello public Docker Hub registry, tag it, and push it tooyour registry.</span></span> <span data-ttu-id="96acc-112">Voor instructies voor het pushen en installatiekopieën pull, Zie [Push Docker installatiekopie tooAzure persoonlijke register](container-registry-get-started-docker-cli.md).</span><span class="sxs-lookup"><span data-stu-id="96acc-112">For guidance on how push and pull images, see [Push Docker image tooAzure private registry](container-registry-get-started-docker-cli.md).</span></span>


## <a name="viewing-repositories-in-hello-portal"></a><span data-ttu-id="96acc-113">Opslagplaatsen in Hallo Portal weergeven</span><span class="sxs-lookup"><span data-stu-id="96acc-113">Viewing repositories in hello Portal</span></span>

<span data-ttu-id="96acc-114">Als u installatiekopieën tooyour container register hebt gedrukt, kunt u een overzicht van Hallo-opslagplaatsen Hallo afbeeldingen in hello Azure-portal te hosten.</span><span class="sxs-lookup"><span data-stu-id="96acc-114">Once you have pushed images tooyour container registry, you can see a list of hello repositories hosting hello images in hello Azure portal.</span></span>

<span data-ttu-id="96acc-115">Als u de stappen Hallo in Hallo gevolgd [Docker Push installatiekopie tooAzure persoonlijke register](container-registry-get-started-docker-cli.md) artikel, u hebt nu een Nginx-installatiekopie in het register van de container.</span><span class="sxs-lookup"><span data-stu-id="96acc-115">If you followed hello steps in hello [Push Docker image tooAzure private registry](container-registry-get-started-docker-cli.md) article, you should now have a Nginx image in your container registry.</span></span> <span data-ttu-id="96acc-116">Als onderdeel van het Hallo-instructies, moet u een naamruimte voor de installatiekopie van het Hallo hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="96acc-116">As part of hello instructions, you should have specified a namespace for hello image.</span></span> <span data-ttu-id="96acc-117">In onderstaande Hallo voorbeeld pushes Hallo opdracht Hallo NGinx toohello 'voorbeelden' installatiekopieopslagplaats:</span><span class="sxs-lookup"><span data-stu-id="96acc-117">In hello example below, hello command pushes hello NGinx image toohello "samples" repository:</span></span>

```
docker push myregistry.azurecr.io/samples/nginx
```
 <span data-ttu-id="96acc-118">Azure Container Registry ondersteunt naamruimten voor opslagplaatsen op meerdere niveaus.</span><span class="sxs-lookup"><span data-stu-id="96acc-118">Azure Container Registry supports multilevel repository namespaces.</span></span> <span data-ttu-id="96acc-119">Deze functie kunt u toogroup verzamelingen van installatiekopieën gerelateerde tooa specifieke app of een verzameling van apps toospecific ontwikkeling of operationele teams.</span><span class="sxs-lookup"><span data-stu-id="96acc-119">This feature enables you toogroup collections of images related tooa specific app, or a collection of apps toospecific development or operational teams.</span></span> <span data-ttu-id="96acc-120">Zie tooread meer informatie over opslagplaatsen in container-registers [registers voor persoonlijke Docker-container in Azure](container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="96acc-120">tooread more about repositories in container registries, see [Private Docker container registries in Azure](container-registry-intro.md).</span></span>

<span data-ttu-id="96acc-121">register-opslagplaatsen voor tooview Hallo container</span><span class="sxs-lookup"><span data-stu-id="96acc-121">tooview hello container registry repositories:</span></span>

1. <span data-ttu-id="96acc-122">Meld u bij toohello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="96acc-122">Log in toohello Azure portal</span></span>
2. <span data-ttu-id="96acc-123">Op Hallo **Azure Container register** blade, selecteer Hallo register gewenst tooinspect</span><span class="sxs-lookup"><span data-stu-id="96acc-123">On hello **Azure Container Registry** blade, select hello registry you wish tooinspect</span></span>
3. <span data-ttu-id="96acc-124">Klik op Hallo register blade **opslagplaatsen** toosee een lijst met alle Hallo-opslagplaatsen en hun installatiekopieën</span><span class="sxs-lookup"><span data-stu-id="96acc-124">In hello registry blade, click **Repositories** toosee a list of all hello repositories and their images</span></span>
4. <span data-ttu-id="96acc-125">(Optioneel) Selecteer een specifieke installatiekopie toosee labels</span><span class="sxs-lookup"><span data-stu-id="96acc-125">(Optional) Select a specific image toosee tags</span></span>

![Opslagplaatsen in Hallo-portal](./media/container-registry-repositories/container-registry-repositories.png)


## <a name="next-steps"></a><span data-ttu-id="96acc-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="96acc-127">Next steps</span></span>
<span data-ttu-id="96acc-128">Nu u weet Hallo basisbeginselen, bent u klaar toostart met behulp van het register!</span><span class="sxs-lookup"><span data-stu-id="96acc-128">Now that you know hello basics, you are ready toostart using your registry!</span></span> <span data-ttu-id="96acc-129">Bijvoorbeeld, beginnen met het implementeren van de container installatiekopieën tooan [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span><span class="sxs-lookup"><span data-stu-id="96acc-129">For example, start deploying container images tooan [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span></span>
