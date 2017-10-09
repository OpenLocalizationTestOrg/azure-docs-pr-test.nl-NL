---
title: aaaPush Docker installatiekopie tooprivate Azure register | Microsoft Docs
description: "Push als pull Docker installatiekopieën tooa privé-container register in Azure met behulp van Docker CLI Hallo"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 64fbe43f-fdde-4c17-a39a-d04f2d6d90a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a81a6f4bfcb23642a89ac7631348d40e2f4911a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="push-your-first-image-tooa-private-docker-container-registry-using-hello-docker-cli"></a><span data-ttu-id="4ee62-103">Uw eerste afbeelding tooa persoonlijke Docker-container register met Hallo Docker CLI push</span><span class="sxs-lookup"><span data-stu-id="4ee62-103">Push your first image tooa private Docker container registry using hello Docker CLI</span></span>
<span data-ttu-id="4ee62-104">Een Azure container-register worden opgeslagen en beheerd persoonlijke [Docker](http://hub.docker.com) container afbeeldingen, vergelijkbare toohello manier [Docker Hub](https://hub.docker.com/) openbare Docker-installatiekopieën worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="4ee62-104">An Azure container registry stores and manages private [Docker](http://hub.docker.com) container images, similar toohello way [Docker Hub](https://hub.docker.com/) stores public Docker images.</span></span> <span data-ttu-id="4ee62-105">Gebruik van Hallo [Docker-opdrachtregelinterface](https://docs.docker.com/engine/reference/commandline/cli/) (Docker CLI) voor [aanmelding](https://docs.docker.com/engine/reference/commandline/login/), [push](https://docs.docker.com/engine/reference/commandline/push/), [pull](https://docs.docker.com/engine/reference/commandline/pull/), en andere bewerkingen op de container het register.</span><span class="sxs-lookup"><span data-stu-id="4ee62-105">You use hello [Docker Command-Line Interface](https://docs.docker.com/engine/reference/commandline/cli/) (Docker CLI) for [login](https://docs.docker.com/engine/reference/commandline/login/), [push](https://docs.docker.com/engine/reference/commandline/push/), [pull](https://docs.docker.com/engine/reference/commandline/pull/), and other operations on your container registry.</span></span>

<span data-ttu-id="4ee62-106">Zie voor meer informatie over de achtergrond en concepten [Hallo overzicht](container-registry-intro.md)</span><span class="sxs-lookup"><span data-stu-id="4ee62-106">For more background and concepts, see [hello overview](container-registry-intro.md)</span></span>



## <a name="prerequisites"></a><span data-ttu-id="4ee62-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="4ee62-107">Prerequisites</span></span>
* <span data-ttu-id="4ee62-108">**Azure-containerregister**: maak een containerregister in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="4ee62-108">**Azure container registry** - Create a container registry in your Azure subscription.</span></span> <span data-ttu-id="4ee62-109">Gebruik bijvoorbeeld Hallo [Azure-portal](container-registry-get-started-portal.md) of Hallo [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="4ee62-109">For example, use hello [Azure portal](container-registry-get-started-portal.md) or hello [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span></span>
* <span data-ttu-id="4ee62-110">**Docker CLI** -tooset van uw lokale computer als een Docker-host en toegang Hallo Docker CLI-opdrachten, installeren [Docker-Engine](https://docs.docker.com/engine/installation/).</span><span class="sxs-lookup"><span data-stu-id="4ee62-110">**Docker CLI** - tooset up your local computer as a Docker host and access hello Docker CLI commands, install [Docker Engine](https://docs.docker.com/engine/installation/).</span></span>

## <a name="log-in-tooa-registry"></a><span data-ttu-id="4ee62-111">Meld u bij tooa register</span><span class="sxs-lookup"><span data-stu-id="4ee62-111">Log in tooa registry</span></span>
<span data-ttu-id="4ee62-112">Voer `docker login` toolog in tooyour container register met uw [register referenties](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="4ee62-112">Run `docker login` toolog in tooyour container registry with your [registry credentials](container-registry-authentication.md).</span></span>

<span data-ttu-id="4ee62-113">Hallo volgende voorbeeld wordt doorgegeven Hallo-ID en wachtwoord van een Azure Active Directory [service-principal](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="4ee62-113">hello following example passes hello ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="4ee62-114">Bijvoorbeeld, u mogelijk hebt toegewezen een register van de service principal tooyour voor een scenario voor automatisering.</span><span class="sxs-lookup"><span data-stu-id="4ee62-114">For example, you might have assigned a service principal tooyour registry for an automation scenario.</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

> [!TIP]
> <span data-ttu-id="4ee62-115">Zorg ervoor dat toospecify Hallo register volledig gekwalificeerde naam (alle kleine letters).</span><span class="sxs-lookup"><span data-stu-id="4ee62-115">Make sure toospecify hello fully qualified registry name (all lowercase).</span></span> <span data-ttu-id="4ee62-116">In dit voorbeeld is het `myregistry.azurecr.io`.</span><span class="sxs-lookup"><span data-stu-id="4ee62-116">In this example, it is `myregistry.azurecr.io`.</span></span>

## <a name="steps-toopull-and-push-an-image"></a><span data-ttu-id="4ee62-117">Stappen toopull en een installatiekopie van een push</span><span class="sxs-lookup"><span data-stu-id="4ee62-117">Steps toopull and push an image</span></span>
<span data-ttu-id="4ee62-118">Hallo volgen downloads Hallo Nginx-installatiekopie uit Hallo openbare Docker Hub register, tags voor uw register persoonlijke Azure-container duwt deze tooyour register vervolgens opnieuw ophaalt.</span><span class="sxs-lookup"><span data-stu-id="4ee62-118">hello follow example downloads hello Nginx image from hello public Docker Hub registry, tags it for your private Azure container registry, pushes it tooyour registry, then pulls it again.</span></span>

<span data-ttu-id="4ee62-119">**1. Pull-hallo Docker officiële installatiekopie voor Nginx**</span><span class="sxs-lookup"><span data-stu-id="4ee62-119">**1. Pull hello Docker official image for Nginx**</span></span>

<span data-ttu-id="4ee62-120">Eerste pull hallo openbare Nginx-image tooyour lokale computer.</span><span class="sxs-lookup"><span data-stu-id="4ee62-120">First pull hello public Nginx image tooyour local computer.</span></span>

```
docker pull nginx
```
<span data-ttu-id="4ee62-121">**2. Hallo Nginx-container starten**</span><span class="sxs-lookup"><span data-stu-id="4ee62-121">**2. Start hello Nginx container**</span></span>

<span data-ttu-id="4ee62-122">Hallo volgende opdracht start Hallo lokale Nginx-container interactief op poort 8080, zodat u toosee uitvoer van Nginx.</span><span class="sxs-lookup"><span data-stu-id="4ee62-122">hello following command starts hello local Nginx container interactively on port 8080, allowing you toosee output from Nginx.</span></span> <span data-ttu-id="4ee62-123">Verwijdert deze container één keer gestopt met Hallo.</span><span class="sxs-lookup"><span data-stu-id="4ee62-123">It removes hello running container once stopped.</span></span>

```
docker run -it --rm -p 8080:80 nginx
```

<span data-ttu-id="4ee62-124">Te bladeren[http://localhost: 8080](http://localhost:8080) tooview Hallo container uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4ee62-124">Browse too[http://localhost:8080](http://localhost:8080) tooview hello running container.</span></span> <span data-ttu-id="4ee62-125">U ziet een scherm vergelijkbare toohello volgt.</span><span class="sxs-lookup"><span data-stu-id="4ee62-125">You see a screen similar toohello following one.</span></span>

![Nginx op lokale computer](./media/container-registry-get-started-docker-cli/nginx.png)

<span data-ttu-id="4ee62-127">toostop Hallo actieve container, drukt u op [CTRL] + [C].</span><span class="sxs-lookup"><span data-stu-id="4ee62-127">toostop hello running container, press [CTRL]+[C].</span></span>

<span data-ttu-id="4ee62-128">**3. Een alias van Hallo afbeelding maken in het register**</span><span class="sxs-lookup"><span data-stu-id="4ee62-128">**3. Create an alias of hello image in your registry**</span></span>

<span data-ttu-id="4ee62-129">Hallo volgende opdracht maakt u een alias van de afbeelding hello, met een volledig gekwalificeerde pad tooyour-register.</span><span class="sxs-lookup"><span data-stu-id="4ee62-129">hello following command creates an alias of hello image, with a fully qualified path tooyour registry.</span></span> <span data-ttu-id="4ee62-130">In dit voorbeeld geeft Hallo `samples` naamruimte tooavoid vol in de hoofdmap Hallo van Hallo-register.</span><span class="sxs-lookup"><span data-stu-id="4ee62-130">This example specifies hello `samples` namespace tooavoid clutter in hello root of hello registry.</span></span>

```
docker tag nginx myregistry.azurecr.io/samples/nginx
```  

<span data-ttu-id="4ee62-131">**4. Push Hallo installatiekopie tooyour register**</span><span class="sxs-lookup"><span data-stu-id="4ee62-131">**4. Push hello image tooyour registry**</span></span>

```
docker push myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="4ee62-132">**5. Pull-hallo-installatiekopie uit het register**</span><span class="sxs-lookup"><span data-stu-id="4ee62-132">**5. Pull hello image from your registry**</span></span>

```
docker pull myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="4ee62-133">**6. Hallo Nginx-container starten vanuit het register**</span><span class="sxs-lookup"><span data-stu-id="4ee62-133">**6. Start hello Nginx container from your registry**</span></span>

```
docker run -it --rm -p 8080:80 myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="4ee62-134">Te bladeren[http://localhost: 8080](http://localhost:8080) tooview Hallo container uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4ee62-134">Browse too[http://localhost:8080](http://localhost:8080) tooview hello running container.</span></span>

<span data-ttu-id="4ee62-135">toostop Hallo actieve container, drukt u op [CTRL] + [C].</span><span class="sxs-lookup"><span data-stu-id="4ee62-135">toostop hello running container, press [CTRL]+[C].</span></span>

<span data-ttu-id="4ee62-136">**7. (Optioneel) Hallo afbeelding verwijderen**</span><span class="sxs-lookup"><span data-stu-id="4ee62-136">**7. (Optional) Remove hello image**</span></span>

```
docker rmi myregistry.azurecr.io/samples/nginx
```

##<a name="concurrent-limits"></a><span data-ttu-id="4ee62-137">Gelijktijdige limieten</span><span class="sxs-lookup"><span data-stu-id="4ee62-137">Concurrent Limits</span></span>
<span data-ttu-id="4ee62-138">In sommige gevallen kan het gelijktijdig uitvoeren van aanroepen leiden tot fouten.</span><span class="sxs-lookup"><span data-stu-id="4ee62-138">In some scenarios, executing calls concurrently might result in errors.</span></span> <span data-ttu-id="4ee62-139">Hallo volgende tabel bevat Hallo limieten van gelijktijdige aanroepen met 'Push' en 'Pull' bewerkingen op Azure-container registersleutel:</span><span class="sxs-lookup"><span data-stu-id="4ee62-139">hello following table contains hello limits of concurrent calls with "Push" and "Pull" operations on Azure container registry:</span></span>

| <span data-ttu-id="4ee62-140">Bewerking</span><span class="sxs-lookup"><span data-stu-id="4ee62-140">Operation</span></span>  | <span data-ttu-id="4ee62-141">Limiet</span><span class="sxs-lookup"><span data-stu-id="4ee62-141">Limit</span></span>                                  |
| ---------- | -------------------------------------- |
| <span data-ttu-id="4ee62-142">PULL</span><span class="sxs-lookup"><span data-stu-id="4ee62-142">PULL</span></span>       | <span data-ttu-id="4ee62-143">Haalt up too10 gelijktijdige per register</span><span class="sxs-lookup"><span data-stu-id="4ee62-143">Up too10 concurrent pulls per registry</span></span> |
| <span data-ttu-id="4ee62-144">PUSH</span><span class="sxs-lookup"><span data-stu-id="4ee62-144">PUSH</span></span>       | <span data-ttu-id="4ee62-145">Up too5 gelijktijdige pushes per register</span><span class="sxs-lookup"><span data-stu-id="4ee62-145">Up too5 concurrent pushes per registry</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4ee62-146">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4ee62-146">Next steps</span></span>
<span data-ttu-id="4ee62-147">Nu u weet Hallo basisbeginselen, bent u klaar toostart met behulp van het register!</span><span class="sxs-lookup"><span data-stu-id="4ee62-147">Now that you know hello basics, you are ready toostart using your registry!</span></span> <span data-ttu-id="4ee62-148">Bijvoorbeeld, beginnen met het implementeren van de container installatiekopieën tooan [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span><span class="sxs-lookup"><span data-stu-id="4ee62-148">For example, start deploying container images tooan [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span></span>
