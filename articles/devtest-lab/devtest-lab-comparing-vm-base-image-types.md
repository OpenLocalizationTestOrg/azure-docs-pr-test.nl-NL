---
title: "Vergelijking van aangepaste installatiekopieën en formules in DevTest Labs | Microsoft Docs"
description: "Meer informatie over de verschillen tussen aangepaste installatiekopieën en formules als VM baseert zodat u kunt beslissen welke beste past bij uw omgeving."
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
ms.openlocfilehash: ff771abc26c08f0adb977c29739d2f5c91924b21
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="comparing-custom-images-and-formulas-in-devtest-labs"></a><span data-ttu-id="525cb-103">Vergelijking van aangepaste installatiekopieën en formules in DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="525cb-103">Comparing custom images and formulas in DevTest Labs</span></span>
<span data-ttu-id="525cb-104">Beide [aangepaste installatiekopieën](devtest-lab-create-template.md) en [formules](devtest-lab-manage-formulas.md) kan worden gebruikt als basis voor [gemaakt van de nieuwe virtuele machines](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="525cb-104">Both [custom images](devtest-lab-create-template.md) and [formulas](devtest-lab-manage-formulas.md) can be used as bases for [created new VMs](devtest-lab-add-vm-with-artifacts.md).</span></span> <span data-ttu-id="525cb-105">Het belangrijkste verschil tussen aangepaste installatiekopieën en formules is echter dat een aangepaste installatiekopie is gewoon een op basis van een VHD, terwijl een formule een installatiekopie op basis van een VHD is *naast* vooraf geconfigureerde instellingen - zoals VM-grootte, virtueel netwerk subnet en artefacten.</span><span class="sxs-lookup"><span data-stu-id="525cb-105">However, the key distinction between custom images and formulas is that a custom image is simply an image based on a VHD, while a formula is an image based on a VHD *in addition to* preconfigured settings - such as VM Size, virtual network, subnet, and artifacts.</span></span> <span data-ttu-id="525cb-106">Deze vooraf geconfigureerde instellingen zijn ingesteld met de standaardwaarden die kunnen worden genegeerd op het moment van de virtuele machine maken.</span><span class="sxs-lookup"><span data-stu-id="525cb-106">These preconfigured settings are set up with default values that can be overridden at the time of VM creation.</span></span> <span data-ttu-id="525cb-107">In dit artikel worden enkele van de (professionals) voordelen en nadelen (nadelen) voor het gebruik van aangepaste installatiekopieën ten opzichte van formules.</span><span class="sxs-lookup"><span data-stu-id="525cb-107">This article explains some of the advantages (pros) and disadvantages (cons) to using custom images versus using formulas.</span></span>

## <a name="custom-image-pros-and-cons"></a><span data-ttu-id="525cb-108">Aangepaste installatiekopie voor- en nadelen</span><span class="sxs-lookup"><span data-stu-id="525cb-108">Custom image pros and cons</span></span>
<span data-ttu-id="525cb-109">Aangepaste installatiekopieën bieden een statische, niet-wijzigbaar manier om virtuele machines maken vanuit een gewenste-omgeving.</span><span class="sxs-lookup"><span data-stu-id="525cb-109">Custom images provide a static, immutable way to create VMs from a desired environment.</span></span> 

<span data-ttu-id="525cb-110">**Professionals**</span><span class="sxs-lookup"><span data-stu-id="525cb-110">**Pros**</span></span>

* <span data-ttu-id="525cb-111">VM-inrichting van een aangepaste installatiekopie is snelle als er niets wordt gewijzigd nadat de virtuele machine uit de afbeelding wordt ingezet.</span><span class="sxs-lookup"><span data-stu-id="525cb-111">VM provisioning from a custom image is fast as nothing changes after the VM is spun up from the image.</span></span> <span data-ttu-id="525cb-112">Met andere woorden, zijn er geen instellingen tijdens de aangepaste installatiekopie alleen maar een afbeelding zonder de instellingen is toegepast.</span><span class="sxs-lookup"><span data-stu-id="525cb-112">In other words, there are no settings to apply as the custom image is just an image without settings.</span></span> 
* <span data-ttu-id="525cb-113">Virtuele machines die zijn gemaakt op basis van één aangepaste installatiekopie zijn identiek.</span><span class="sxs-lookup"><span data-stu-id="525cb-113">VMs created from a single custom image are identical.</span></span>

<span data-ttu-id="525cb-114">**Nadelen**</span><span class="sxs-lookup"><span data-stu-id="525cb-114">**Cons**</span></span>

* <span data-ttu-id="525cb-115">Als u bijwerken van een bepaald aspect van de aangepaste installatiekopie wilt, de installatiekopie moet opnieuw worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="525cb-115">If you need to update some aspect of the custom image, the image must be recreated.</span></span>  

## <a name="formula-pros-and-cons"></a><span data-ttu-id="525cb-116">Formule voor- en nadelen</span><span class="sxs-lookup"><span data-stu-id="525cb-116">Formula pros and cons</span></span>
<span data-ttu-id="525cb-117">Formules bieden een dynamische manier om te maken van virtuele machines van de gewenste instellingen.</span><span class="sxs-lookup"><span data-stu-id="525cb-117">Formulas provide a dynamic way to create VMs from the desired configuration/settings.</span></span>

<span data-ttu-id="525cb-118">**Professionals**</span><span class="sxs-lookup"><span data-stu-id="525cb-118">**Pros**</span></span>

* <span data-ttu-id="525cb-119">Wijzigingen in de omgeving kunnen worden vastgelegd op elk gewenst moment via artefacten.</span><span class="sxs-lookup"><span data-stu-id="525cb-119">Changes in the environment can be captured on the fly via artifacts.</span></span> <span data-ttu-id="525cb-120">Bijvoorbeeld, als u een virtuele machine is geïnstalleerd met de meest recente bits vanuit de pipeline release of de meest recente code van uw opslagplaats aanmelden, kunt u gewoon opgeven een artefact die zich aanmeldt de meest recente code in de formule samen met een base doel of de meest recente bits geïmplementeerd afbeelding.</span><span class="sxs-lookup"><span data-stu-id="525cb-120">For example, if you want a VM installed with the latest bits from your release pipeline or enlist the latest code from your repository, you can simply specify an artifact that deploys the latest bits or enlists the latest code in the formula together with a target base image.</span></span> <span data-ttu-id="525cb-121">Wanneer deze formule wordt gebruikt voor het maken van virtuele machines, zijn de meest recente bits/code geïmplementeerd/aangemeld met de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="525cb-121">Whenever this formula is used to create VMs, the latest bits/code are deployed/enlisted to the VM.</span></span> 
* <span data-ttu-id="525cb-122">Formules kunnen standaardinstellingen die aangepaste installatiekopieën niet - zoals instellingen voor virtuele netwerken en VM-grootten biedt definiëren.</span><span class="sxs-lookup"><span data-stu-id="525cb-122">Formulas can define default settings that custom images cannot provide - such as VM sizes and virtual network settings.</span></span> 
* <span data-ttu-id="525cb-123">De instellingen die zijn opgeslagen in een formule als standaardwaarden worden weergegeven, maar kunnen worden gewijzigd wanneer de virtuele machine wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="525cb-123">The settings saved in a formula are shown as default values, but can be modified when the VM is created.</span></span> 

<span data-ttu-id="525cb-124">**Nadelen**</span><span class="sxs-lookup"><span data-stu-id="525cb-124">**Cons**</span></span>

* <span data-ttu-id="525cb-125">Een VM maken van een formule kan langer duren dan het maken van een virtuele machine van een aangepaste installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="525cb-125">Creating a VM from a formula can take more time than creating a VM from a custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="525cb-126">Verwante blogberichten</span><span class="sxs-lookup"><span data-stu-id="525cb-126">Related blog posts</span></span>
* [<span data-ttu-id="525cb-127">Aangepaste installatiekopieën of formules?</span><span class="sxs-lookup"><span data-stu-id="525cb-127">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a><span data-ttu-id="525cb-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="525cb-128">Next steps</span></span>
- [<span data-ttu-id="525cb-129">DevTest Labs Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="525cb-129">DevTest Labs FAQ</span></span>](devtest-lab-faq.md)