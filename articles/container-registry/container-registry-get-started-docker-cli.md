---
title: "Een Docker-installatiekopie pushen naar uw privé-Azure-register | Microsoft Docs"
description: "Docker-installatiekopieën pushen naar en ophalen van een privécontainerregister in Azure met de Docker-CLI"
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
ms.openlocfilehash: 07d4d72e94eda02e8594dfddb0e911eb0e63012d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="push-your-first-image-to-a-private-docker-container-registry-using-the-docker-cli"></a><span data-ttu-id="0c816-103">Uw eerste installatiekopie naar een Docker-containerregister pushen met de Docker-CLI</span><span class="sxs-lookup"><span data-stu-id="0c816-103">Push your first image to a private Docker container registry using the Docker CLI</span></span>
<span data-ttu-id="0c816-104">Een Azure-containerregister slaat persoonlijke [Docker](http://hub.docker.com)-containerinstallatiekopieën op en beheert ze, vergelijkbaar met de manier waarop [Docker Hub](https://hub.docker.com/) openbare Docker-installatiekopieën opslaat.</span><span class="sxs-lookup"><span data-stu-id="0c816-104">An Azure container registry stores and manages private [Docker](http://hub.docker.com) container images, similar to the way [Docker Hub](https://hub.docker.com/) stores public Docker images.</span></span> <span data-ttu-id="0c816-105">U gebruikt de [Docker-Command-Line Interface](https://docs.docker.com/engine/reference/commandline/cli/) (Docker-CLI) voor [aanmelden](https://docs.docker.com/engine/reference/commandline/login/), [pushen](https://docs.docker.com/engine/reference/commandline/push/), [ophalen](https://docs.docker.com/engine/reference/commandline/pull/) en andere bewerkingen voor uw containerregister.</span><span class="sxs-lookup"><span data-stu-id="0c816-105">You use the [Docker Command-Line Interface](https://docs.docker.com/engine/reference/commandline/cli/) (Docker CLI) for [login](https://docs.docker.com/engine/reference/commandline/login/), [push](https://docs.docker.com/engine/reference/commandline/push/), [pull](https://docs.docker.com/engine/reference/commandline/pull/), and other operations on your container registry.</span></span>

<span data-ttu-id="0c816-106">Zie [het overzicht](container-registry-intro.md) voor meer achtergrondinformatie en concepten</span><span class="sxs-lookup"><span data-stu-id="0c816-106">For more background and concepts, see [the overview](container-registry-intro.md)</span></span>



## <a name="prerequisites"></a><span data-ttu-id="0c816-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="0c816-107">Prerequisites</span></span>
* <span data-ttu-id="0c816-108">**Azure-containerregister**: maak een containerregister in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="0c816-108">**Azure container registry** - Create a container registry in your Azure subscription.</span></span> <span data-ttu-id="0c816-109">Gebruik bijvoorbeeld [Azure Portal](container-registry-get-started-portal.md) of de [Azure-CLI 2.0](container-registry-get-started-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="0c816-109">For example, use the [Azure portal](container-registry-get-started-portal.md) or the [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span></span>
* <span data-ttu-id="0c816-110">**Docker-CLI**: installeer de [Docker-engine](https://docs.docker.com/engine/installation/) om uw lokale computer als een Docker-host in te stellen en de Docker-CLI-opdrachten te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0c816-110">**Docker CLI** - To set up your local computer as a Docker host and access the Docker CLI commands, install [Docker Engine](https://docs.docker.com/engine/installation/).</span></span>

## <a name="log-in-to-a-registry"></a><span data-ttu-id="0c816-111">Aanmelden bij een register</span><span class="sxs-lookup"><span data-stu-id="0c816-111">Log in to a registry</span></span>
<span data-ttu-id="0c816-112">Voer `docker login` uit om u bij uw containerregister aan te melden met uw [registerreferenties](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="0c816-112">Run `docker login` to log in to your container registry with your [registry credentials](container-registry-authentication.md).</span></span>

<span data-ttu-id="0c816-113">In het volgende voorbeeld worden de id en het wachtwoord van een [service-principal](../active-directory/active-directory-application-objects.md) van Azure Active Directory doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="0c816-113">The following example passes the ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="0c816-114">U hebt bijvoorbeeld een service-principal aan uw register toegewezen voor een automatiseringsscenario.</span><span class="sxs-lookup"><span data-stu-id="0c816-114">For example, you might have assigned a service principal to your registry for an automation scenario.</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

> [!TIP]
> <span data-ttu-id="0c816-115">Geef de registernaam op die aan alle vereisten voldoet (zonder hoofdletters).</span><span class="sxs-lookup"><span data-stu-id="0c816-115">Make sure to specify the fully qualified registry name (all lowercase).</span></span> <span data-ttu-id="0c816-116">In dit voorbeeld is het `myregistry.azurecr.io`.</span><span class="sxs-lookup"><span data-stu-id="0c816-116">In this example, it is `myregistry.azurecr.io`.</span></span>

## <a name="steps-to-pull-and-push-an-image"></a><span data-ttu-id="0c816-117">Stappen voor ophalen en pushen van een installatiekopie</span><span class="sxs-lookup"><span data-stu-id="0c816-117">Steps to pull and push an image</span></span>
<span data-ttu-id="0c816-118">In het volgende voorbeeld wordt de Nginx-installatiekopie gedownload uit het openbare Docker Hub-register, getagd voor uw persoonlijke Azure-containerregister, gepusht naar uw register en vervolgens weer opgehaald.</span><span class="sxs-lookup"><span data-stu-id="0c816-118">The follow example downloads the Nginx image from the public Docker Hub registry, tags it for your private Azure container registry, pushes it to your registry, then pulls it again.</span></span>

<span data-ttu-id="0c816-119">**1. De officiële Docker-installatiekopie ophalen voor Nginx**</span><span class="sxs-lookup"><span data-stu-id="0c816-119">**1. Pull the Docker official image for Nginx**</span></span>

<span data-ttu-id="0c816-120">Haal eerst de openbare Nginx-installatiekopie op naar uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="0c816-120">First pull the public Nginx image to your local computer.</span></span>

```
docker pull nginx
```
<span data-ttu-id="0c816-121">**2. De Nginx-container starten**</span><span class="sxs-lookup"><span data-stu-id="0c816-121">**2. Start the Nginx container**</span></span>

<span data-ttu-id="0c816-122">Met de volgende opdracht wordt de lokale Nginx-container interactief gestart via poort 8080, zodat u uitvoer van Nginx kunt zien.</span><span class="sxs-lookup"><span data-stu-id="0c816-122">The following command starts the local Nginx container interactively on port 8080, allowing you to see output from Nginx.</span></span> <span data-ttu-id="0c816-123">De container die wordt uitgevoerd, wordt verwijderd zodra deze is gestopt.</span><span class="sxs-lookup"><span data-stu-id="0c816-123">It removes the running container once stopped.</span></span>

```
docker run -it --rm -p 8080:80 nginx
```

<span data-ttu-id="0c816-124">Ga naar [http://localhost:8080](http://localhost:8080) om de container die wordt uitgevoerd, weer te geven.</span><span class="sxs-lookup"><span data-stu-id="0c816-124">Browse to [http://localhost:8080](http://localhost:8080) to view the running container.</span></span> <span data-ttu-id="0c816-125">Er wordt een venster zoals het volgende weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0c816-125">You see a screen similar to the following one.</span></span>

![Nginx op lokale computer](./media/container-registry-get-started-docker-cli/nginx.png)

<span data-ttu-id="0c816-127">Druk op [CTRL]+[C] om de container die wordt uitgevoerd, te stoppen.</span><span class="sxs-lookup"><span data-stu-id="0c816-127">To stop the running container, press [CTRL]+[C].</span></span>

<span data-ttu-id="0c816-128">**3. Een alias van de installatiekopie in uw register maken**</span><span class="sxs-lookup"><span data-stu-id="0c816-128">**3. Create an alias of the image in your registry**</span></span>

<span data-ttu-id="0c816-129">Met de volgende opdracht maakt u een alias van de installatiekopie met een volledig gekwalificeerd pad naar uw register.</span><span class="sxs-lookup"><span data-stu-id="0c816-129">The following command creates an alias of the image, with a fully qualified path to your registry.</span></span> <span data-ttu-id="0c816-130">In dit voorbeeld wordt de naamruimte `samples` gespecificeerd om overbodige items in de hoofdmap van het register te voorkomen.</span><span class="sxs-lookup"><span data-stu-id="0c816-130">This example specifies the `samples` namespace to avoid clutter in the root of the registry.</span></span>

```
docker tag nginx myregistry.azurecr.io/samples/nginx
```  

<span data-ttu-id="0c816-131">**4. De installatiekopie naar uw register pushen**</span><span class="sxs-lookup"><span data-stu-id="0c816-131">**4. Push the image to your registry**</span></span>

```
docker push myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="0c816-132">**5. De installatiekopie vanuit uw register ophalen**</span><span class="sxs-lookup"><span data-stu-id="0c816-132">**5. Pull the image from your registry**</span></span>

```
docker pull myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="0c816-133">**6. De Nginx-container vanuit uw register starten**</span><span class="sxs-lookup"><span data-stu-id="0c816-133">**6. Start the Nginx container from your registry**</span></span>

```
docker run -it --rm -p 8080:80 myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="0c816-134">Ga naar [http://localhost:8080](http://localhost:8080) om de container die wordt uitgevoerd, weer te geven.</span><span class="sxs-lookup"><span data-stu-id="0c816-134">Browse to [http://localhost:8080](http://localhost:8080) to view the running container.</span></span>

<span data-ttu-id="0c816-135">Druk op [CTRL]+[C] om de container die wordt uitgevoerd, te stoppen.</span><span class="sxs-lookup"><span data-stu-id="0c816-135">To stop the running container, press [CTRL]+[C].</span></span>

<span data-ttu-id="0c816-136">**7. (optioneel) De installatiekopie verwijderen**</span><span class="sxs-lookup"><span data-stu-id="0c816-136">**7. (Optional) Remove the image**</span></span>

```
docker rmi myregistry.azurecr.io/samples/nginx
```

##<a name="concurrent-limits"></a><span data-ttu-id="0c816-137">Gelijktijdige limieten</span><span class="sxs-lookup"><span data-stu-id="0c816-137">Concurrent Limits</span></span>
<span data-ttu-id="0c816-138">In sommige gevallen kan het gelijktijdig uitvoeren van aanroepen leiden tot fouten.</span><span class="sxs-lookup"><span data-stu-id="0c816-138">In some scenarios, executing calls concurrently might result in errors.</span></span> <span data-ttu-id="0c816-139">De volgende tabel bevat de limieten voor gelijktijdige aanroepen met Push- en Pull-bewerkingen in Azure Container Registry:</span><span class="sxs-lookup"><span data-stu-id="0c816-139">The following table contains the limits of concurrent calls with "Push" and "Pull" operations on Azure container registry:</span></span>

| <span data-ttu-id="0c816-140">Bewerking</span><span class="sxs-lookup"><span data-stu-id="0c816-140">Operation</span></span>  | <span data-ttu-id="0c816-141">Limiet</span><span class="sxs-lookup"><span data-stu-id="0c816-141">Limit</span></span>                                  |
| ---------- | -------------------------------------- |
| <span data-ttu-id="0c816-142">PULL</span><span class="sxs-lookup"><span data-stu-id="0c816-142">PULL</span></span>       | <span data-ttu-id="0c816-143">Maximaal 10 gelijktijdige bewerkingen per register</span><span class="sxs-lookup"><span data-stu-id="0c816-143">Up to 10 concurrent pulls per registry</span></span> |
| <span data-ttu-id="0c816-144">PUSH</span><span class="sxs-lookup"><span data-stu-id="0c816-144">PUSH</span></span>       | <span data-ttu-id="0c816-145">Maximaal 5 gelijktijdige bewerkingen per register</span><span class="sxs-lookup"><span data-stu-id="0c816-145">Up to 5 concurrent pushes per registry</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0c816-146">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0c816-146">Next steps</span></span>
<span data-ttu-id="0c816-147">Nu u de basisprincipes kent, kunt u uw register gaan gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0c816-147">Now that you know the basics, you are ready to start using your registry!</span></span> <span data-ttu-id="0c816-148">Begin bijvoorbeeld met het implementeren van containerinstallatiekopieën op een [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/)-cluster.</span><span class="sxs-lookup"><span data-stu-id="0c816-148">For example, start deploying container images to an [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span></span>
