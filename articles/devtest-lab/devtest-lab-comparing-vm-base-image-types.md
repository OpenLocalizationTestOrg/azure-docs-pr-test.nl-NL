---
title: "aaaComparing aangepaste installatiekopieën en formules in DevTest Labs | Microsoft Docs"
description: "Meer informatie over Hallo verschillen tussen aangepaste installatiekopieën en formules als VM baseert zodat u kunt beslissen welke beste past bij uw omgeving."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: a3cb259a-7d80-40ec-8ee8-45105704d589
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: tarcher
ms.openlocfilehash: 3c1d88dfe0ff94b8e825bb7a0b4aca3341c9330d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="comparing-custom-images-and-formulas-in-devtest-labs"></a><span data-ttu-id="e8284-103">Vergelijking van aangepaste installatiekopieën en formules in DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="e8284-103">Comparing custom images and formulas in DevTest Labs</span></span>
<span data-ttu-id="e8284-104">Beide [aangepaste installatiekopieën](devtest-lab-create-template.md) en [formules](devtest-lab-manage-formulas.md) kan worden gebruikt als basis voor [gemaakt van de nieuwe virtuele machines](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="e8284-104">Both [custom images](devtest-lab-create-template.md) and [formulas](devtest-lab-manage-formulas.md) can be used as bases for [created new VMs](devtest-lab-add-vm-with-artifacts.md).</span></span> <span data-ttu-id="e8284-105">Hallo belangrijkste onderscheid tussen aangepaste installatiekopieën en formules is echter dat een aangepaste installatiekopie is gewoon een op basis van een VHD, terwijl een formule een installatiekopie op basis van een VHD is *naast* vooraf geconfigureerde instellingen - zoals VM-grootte, virtueel netwerk subnet en artefacten.</span><span class="sxs-lookup"><span data-stu-id="e8284-105">However, hello key distinction between custom images and formulas is that a custom image is simply an image based on a VHD, while a formula is an image based on a VHD *in addition to* preconfigured settings - such as VM Size, virtual network, subnet, and artifacts.</span></span> <span data-ttu-id="e8284-106">Deze vooraf geconfigureerde instellingen zijn ingesteld met de standaardwaarden die gelijktijdig Hallo met maken van VM's kunnen worden genegeerd.</span><span class="sxs-lookup"><span data-stu-id="e8284-106">These preconfigured settings are set up with default values that can be overridden at hello time of VM creation.</span></span> <span data-ttu-id="e8284-107">Dit artikel worden enkele voordelen hello (professionals) en nadelen (nadelen) toousing aangepaste installatiekopieën ten opzichte van formules.</span><span class="sxs-lookup"><span data-stu-id="e8284-107">This article explains some of hello advantages (pros) and disadvantages (cons) toousing custom images versus using formulas.</span></span>

## <a name="custom-image-pros-and-cons"></a><span data-ttu-id="e8284-108">Aangepaste installatiekopie voor- en nadelen</span><span class="sxs-lookup"><span data-stu-id="e8284-108">Custom image pros and cons</span></span>
<span data-ttu-id="e8284-109">Aangepaste installatiekopieën bieden een statische, niet-wijzigbaar manier toocreate VM's van een gewenste-omgeving.</span><span class="sxs-lookup"><span data-stu-id="e8284-109">Custom images provide a static, immutable way toocreate VMs from a desired environment.</span></span> 

<span data-ttu-id="e8284-110">**Professionals**</span><span class="sxs-lookup"><span data-stu-id="e8284-110">**Pros**</span></span>

* <span data-ttu-id="e8284-111">VM-inrichting van een aangepaste installatiekopie is snelle als niets na Hallo die VM wordt ingezet wordt gewijzigd van Hallo-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="e8284-111">VM provisioning from a custom image is fast as nothing changes after hello VM is spun up from hello image.</span></span> <span data-ttu-id="e8284-112">Met andere woorden, zijn er geen instellingen tooapply Hallo aangepaste installatiekopie wordt alleen maar een afbeelding zonder de instellingen.</span><span class="sxs-lookup"><span data-stu-id="e8284-112">In other words, there are no settings tooapply as hello custom image is just an image without settings.</span></span> 
* <span data-ttu-id="e8284-113">Virtuele machines die zijn gemaakt op basis van één aangepaste installatiekopie zijn identiek.</span><span class="sxs-lookup"><span data-stu-id="e8284-113">VMs created from a single custom image are identical.</span></span>

<span data-ttu-id="e8284-114">**Nadelen**</span><span class="sxs-lookup"><span data-stu-id="e8284-114">**Cons**</span></span>

* <span data-ttu-id="e8284-115">Als u een bepaald aspect van de aangepaste installatiekopie Hallo tooupdate moet, Hallo installatiekopie moet opnieuw worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e8284-115">If you need tooupdate some aspect of hello custom image, hello image must be recreated.</span></span>  

## <a name="formula-pros-and-cons"></a><span data-ttu-id="e8284-116">Formule voor- en nadelen</span><span class="sxs-lookup"><span data-stu-id="e8284-116">Formula pros and cons</span></span>
<span data-ttu-id="e8284-117">Formules bieden een dynamische manier toocreate VM's van Hallo gewenste instellingen.</span><span class="sxs-lookup"><span data-stu-id="e8284-117">Formulas provide a dynamic way toocreate VMs from hello desired configuration/settings.</span></span>

<span data-ttu-id="e8284-118">**Professionals**</span><span class="sxs-lookup"><span data-stu-id="e8284-118">**Pros**</span></span>

* <span data-ttu-id="e8284-119">Wijzigingen in Hallo-omgeving kunnen worden vastgelegd op Hallo snel via artefacten.</span><span class="sxs-lookup"><span data-stu-id="e8284-119">Changes in hello environment can be captured on hello fly via artifacts.</span></span> <span data-ttu-id="e8284-120">Bijvoorbeeld, als u een virtuele machine is geïnstalleerd met de meest recente bits Hallo vanuit de pipeline release of meest recente code op Hallo van uw opslagplaats bijschrijven, kunt u gewoon opgeven een artefact die de meest recente bits Hallo implementeert of zich aanmeldt Hallo meest recente code in Hallo formule samen met een doel basisinstallatiekopie.</span><span class="sxs-lookup"><span data-stu-id="e8284-120">For example, if you want a VM installed with hello latest bits from your release pipeline or enlist hello latest code from your repository, you can simply specify an artifact that deploys hello latest bits or enlists hello latest code in hello formula together with a target base image.</span></span> <span data-ttu-id="e8284-121">Telkens wanneer deze formule gebruikte toocreate VM's en zijn Hallo nieuwste bits/code geïmplementeerd/aangemeld toohello VM.</span><span class="sxs-lookup"><span data-stu-id="e8284-121">Whenever this formula is used toocreate VMs, hello latest bits/code are deployed/enlisted toohello VM.</span></span> 
* <span data-ttu-id="e8284-122">Formules kunnen standaardinstellingen die aangepaste installatiekopieën niet - zoals instellingen voor virtuele netwerken en VM-grootten biedt definiëren.</span><span class="sxs-lookup"><span data-stu-id="e8284-122">Formulas can define default settings that custom images cannot provide - such as VM sizes and virtual network settings.</span></span> 
* <span data-ttu-id="e8284-123">Hallo-instellingen opgeslagen in een formule als standaardwaarden worden weergegeven, maar kunnen worden gewijzigd wanneer Hallo VM wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e8284-123">hello settings saved in a formula are shown as default values, but can be modified when hello VM is created.</span></span> 

<span data-ttu-id="e8284-124">**Nadelen**</span><span class="sxs-lookup"><span data-stu-id="e8284-124">**Cons**</span></span>

* <span data-ttu-id="e8284-125">Een VM maken van een formule kan langer duren dan het maken van een virtuele machine van een aangepaste installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="e8284-125">Creating a VM from a formula can take more time than creating a VM from a custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="e8284-126">Verwante blogberichten</span><span class="sxs-lookup"><span data-stu-id="e8284-126">Related blog posts</span></span>
* [<span data-ttu-id="e8284-127">Aangepaste installatiekopieën of formules?</span><span class="sxs-lookup"><span data-stu-id="e8284-127">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a><span data-ttu-id="e8284-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e8284-128">Next steps</span></span>
- [<span data-ttu-id="e8284-129">DevTest Labs Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="e8284-129">DevTest Labs FAQ</span></span>](devtest-lab-faq.md)