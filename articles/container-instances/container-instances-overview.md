---
title: Overzicht van de Container exemplaren aaaAzure | Azure Docs
description: Inzicht krijgen in Azure Container Instances
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/20/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: c0662ede1260b15d9841bfc2c3c4cec4c30338d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-instances"></a><span data-ttu-id="c9204-103">Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="c9204-103">Azure Container Instances</span></span>

<span data-ttu-id="c9204-104">Containers worden snel Hallo voorkeur manier toopackage steeds, implementeren en beheren van cloudtoepassingen.</span><span class="sxs-lookup"><span data-stu-id="c9204-104">Containers are quickly becoming hello preferred way toopackage, deploy, and manage cloud applications.</span></span> <span data-ttu-id="c9204-105">Azure Containerexemplaren biedt Hallo snelste en eenvoudigste manier toorun een container in Azure, zonder tooprovision virtuele machines en zonder tooadopt een service op een hoger niveau.</span><span class="sxs-lookup"><span data-stu-id="c9204-105">Azure Container Instances offers hello fastest and simplest way toorun a container in Azure, without having tooprovision any virtual machines and without having tooadopt a higher-level service.</span></span> 

<span data-ttu-id="c9204-106">Azure Container Instances is een ideale oplossing voor elk scenario dat kan werken in geïsoleerde containers, met inbegrip van eenvoudige toepassingen, taakautomatisering en het bouwen van taken.</span><span class="sxs-lookup"><span data-stu-id="c9204-106">Azure Container Instances is a great solution for any scenario that can operate in isolated containers, including simple applications, task automation, and build jobs.</span></span> <span data-ttu-id="c9204-107">Voor scenario's waarin u hebt volledige container orchestration, met inbegrip van servicedetectie op meerdere containers, automatisch schalen en gecoördineerde toepassingsupgrades, raden wij aan Hallo [Azure Container Service](https://docs.microsoft.com/azure/container-service/).</span><span class="sxs-lookup"><span data-stu-id="c9204-107">For scenarios where you need full container orchestration, including service discovery across multiple containers, automatic scaling, and coordinated application upgrades, we recommend hello [Azure Container Service](https://docs.microsoft.com/azure/container-service/).</span></span>

## <a name="fast-startup-times"></a><span data-ttu-id="c9204-108">Snel opstarten</span><span class="sxs-lookup"><span data-stu-id="c9204-108">Fast startup times</span></span>

<span data-ttu-id="c9204-109">Containers bieden aanzienlijke opstartvoordelen ten opzichte van virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="c9204-109">Containers offer significant startup benefits over virtual machines.</span></span> <span data-ttu-id="c9204-110">Met exemplaren van Azure-Container, kunt u een container in Azure te starten in seconden zonder Hallo nodig tooprovision en beheren van virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="c9204-110">With Azure Container Instances, you can start a container in Azure in seconds without hello need tooprovision and manage VMs.</span></span>

## <a name="hypervisor-level-security"></a><span data-ttu-id="c9204-111">Beveiliging op hypervisorniveau</span><span class="sxs-lookup"><span data-stu-id="c9204-111">Hypervisor-level security</span></span>

<span data-ttu-id="c9204-112">In het verleden boden containers toepassingsafhankelijke isolatie en resourcebesturing, maar werden ze niet voldoende veilig beschouwd voor onveilig multitenant gebruik.</span><span class="sxs-lookup"><span data-stu-id="c9204-112">Historically, containers have offered application dependency isolation and resource governance but have not been considered sufficiently hardened for hostile multi-tenant usage.</span></span> <span data-ttu-id="c9204-113">Met Azure Container Instances is uw toepassing even geïsoleerd in een container als deze op een virtuele machine zou zijn.</span><span class="sxs-lookup"><span data-stu-id="c9204-113">With Azure Container Instances, your application is as isolated in a container as it would be in a VM.</span></span>

## <a name="custom-sizes"></a><span data-ttu-id="c9204-114">Aangepaste grootten</span><span class="sxs-lookup"><span data-stu-id="c9204-114">Custom sizes</span></span>

<span data-ttu-id="c9204-115">Containers zijn doorgaans geoptimaliseerde toorun slechts één toepassing, maar de exacte behoeften Hallo van deze toepassingen kunnen aanzienlijk verschillen.</span><span class="sxs-lookup"><span data-stu-id="c9204-115">Containers are typically optimized toorun just a single application, but hello exact needs of those applications can differ greatly.</span></span> <span data-ttu-id="c9204-116">Met Azure Container Instances kunt u vragen om precies wat u zoekt in termen van CPU-kernen en het geheugen.</span><span class="sxs-lookup"><span data-stu-id="c9204-116">With Azure Container Instances, you can request exactly what you need in terms of CPU cores and memory.</span></span> <span data-ttu-id="c9204-117">U betaalt op basis van aanvragen, gefactureerd door Hallo tweede, zodat u uw uitgaven op basis van de behoeften van uw fijn kunt optimaliseren.</span><span class="sxs-lookup"><span data-stu-id="c9204-117">You pay based on what you request, billed by hello second, so you can finely optimize your spending based on your needs.</span></span>

## <a name="public-ip-connectivity"></a><span data-ttu-id="c9204-118">Openbare IP-verbinding</span><span class="sxs-lookup"><span data-stu-id="c9204-118">Public IP connectivity</span></span>

<span data-ttu-id="c9204-119">Met Azure Containerexemplaren, kan uw containers worden blootgesteld rechtstreeks toohello internet met een openbaar IP-adres.</span><span class="sxs-lookup"><span data-stu-id="c9204-119">With Azure Container Instances, you can expose your containers directly toohello internet with a public IP address.</span></span> <span data-ttu-id="c9204-120">In toekomstige Hallo, wordt er Vouw onze netwerken mogelijkheden tooinclude integratie met virtuele netwerken, load balancers en andere basisonderdelen van hello Azure netwerkinfrastructuur.</span><span class="sxs-lookup"><span data-stu-id="c9204-120">In hello future, we will expand our networking capabilities tooinclude integration with virtual networks, load balancers, and other core parts of hello Azure networking infrastructure.</span></span>

## <a name="persistent-storage"></a><span data-ttu-id="c9204-121">Permanente opslag</span><span class="sxs-lookup"><span data-stu-id="c9204-121">Persistent storage</span></span>

<span data-ttu-id="c9204-122">tooretrieve en persist-status met exemplaren van Azure-Container, bieden we direct koppelen van Azure bestanden shares.</span><span class="sxs-lookup"><span data-stu-id="c9204-122">tooretrieve and persist state with Azure Container Instances, we offer direct mounting of Azure files shares.</span></span>

## <a name="linux-and-windows-containers"></a><span data-ttu-id="c9204-123">Linux- en Windows-containers</span><span class="sxs-lookup"><span data-stu-id="c9204-123">Linux and Windows containers</span></span>

<span data-ttu-id="c9204-124">Met exemplaren van Azure-Container, kunt u plannen van zowel Windows en Linux-containers met Hallo dezelfde API.</span><span class="sxs-lookup"><span data-stu-id="c9204-124">With Azure Container Instances, you can schedule both Windows and Linux containers with hello same API.</span></span> <span data-ttu-id="c9204-125">Gewoon geven Hallo basistype besturingssysteem en alle andere identiek is.</span><span class="sxs-lookup"><span data-stu-id="c9204-125">Simply indicate hello base OS type and everything else is identical.</span></span>

## <a name="co-scheduled-groups"></a><span data-ttu-id="c9204-126">Samen geplande groepen</span><span class="sxs-lookup"><span data-stu-id="c9204-126">Co-scheduled groups</span></span>

<span data-ttu-id="c9204-127">Azure Container Instances biedt ondersteuning voor planning van meerdere containergroepen die een hostmachine, lokaal netwerk, opslag en levenscyclus delen.</span><span class="sxs-lookup"><span data-stu-id="c9204-127">Azure Container Instances supports scheduling of multi-container groups that share a host machine, local network, storage, and lifecycle.</span></span> <span data-ttu-id="c9204-128">Hierdoor kunnen u toocombine uw hoofdtoepassing met anderen in een ondersteunende rol, zoals logboekregistratie fungeert.</span><span class="sxs-lookup"><span data-stu-id="c9204-128">This enables you toocombine your main application with others acting in a supporting role, such as logging.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9204-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c9204-129">Next steps</span></span>

<span data-ttu-id="c9204-130">Probeer het implementeren van een container tooAzure met een afzonderlijke opdracht met onze [Quick Start guide](container-instances-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="c9204-130">Try deploying a container tooAzure with a single command using our [quickstart guide](container-instances-quickstart.md).</span></span>
