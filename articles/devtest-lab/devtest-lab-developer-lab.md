---
title: Gebruik Azure DevTest Labs voor ontwikkelaars | Microsoft Docs
description: Informatie over het gebruik van Azure DevTest Labs voor scenario's voor ontwikkelaars.
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 22e070e5-3d1a-49fe-9d4c-5e07cb0b7fe2
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: tarcher
ms.openlocfilehash: c187819e9392908c8979556f80e8c94739eb14d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-devtest-labs-for-developers"></a><span data-ttu-id="1e4b3-103">Gebruik Azure DevTest Labs voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="1e4b3-103">Use Azure DevTest Labs for developers</span></span>
<span data-ttu-id="1e4b3-104">Azure DevTest Labs kunnen worden gebruikt voor het implementeren van veel van belangrijke scenario's, maar een van de primaire scenario's wordt DevTest Labs voor ontwikkeling hostmachines voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="1e4b3-104">Azure DevTest Labs can be used to implement many key scenarios, but one of the primary scenarios involves using DevTest Labs to host development machines for developers.</span></span> <span data-ttu-id="1e4b3-105">In dit scenario biedt DevTest Labs de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="1e4b3-105">In this scenario, DevTest Labs provides these benefits:</span></span>

- <span data-ttu-id="1e4b3-106">Ontwikkelaars kunnen hun computers ontwikkeling op aanvraag snel inrichten.</span><span class="sxs-lookup"><span data-stu-id="1e4b3-106">Developers can quickly provision their development machines on demand.</span></span>
- <span data-ttu-id="1e4b3-107">Ontwikkelaars kunnen hun computers ontwikkeling als dat nodig is gemakkelijk aanpassen.</span><span class="sxs-lookup"><span data-stu-id="1e4b3-107">Developers can easily customize their development machines whenever needed.</span></span>
- <span data-ttu-id="1e4b3-108">Beheerders kunnen kosten beheren door ervoor te zorgen dat:</span><span class="sxs-lookup"><span data-stu-id="1e4b3-108">Administrators can control costs by ensuring that:</span></span>
  - <span data-ttu-id="1e4b3-109">Ontwikkelaars kunnen niet meer virtuele machines dan ze nodig hebben voor de ontwikkeling van ophalen.</span><span class="sxs-lookup"><span data-stu-id="1e4b3-109">Developers cannot get more VMs than they need for development.</span></span>
  - <span data-ttu-id="1e4b3-110">Virtuele machines worden afgesloten wanneer deze niet in gebruik.</span><span class="sxs-lookup"><span data-stu-id="1e4b3-110">VMs are shut down when not in use.</span></span> 

![DevTest Labs gebruiken voor training](./media/devtest-lab-developer-lab/devtest-lab-developer-lab.png)

<span data-ttu-id="1e4b3-112">In dit artikel leert u over verschillende Azure DevTest Labs-functies die kunnen worden gebruikt om te voldoen aan vereisten voor ontwikkelaars en de gedetailleerde stappen die u volgen kunt om een testomgeving instellen.</span><span class="sxs-lookup"><span data-stu-id="1e4b3-112">In this article, you learn about various Azure DevTest Labs features that can be used to meet developer requirements and the detailed steps that you can follow to set up a lab.</span></span>

## <a name="implementing-developer-environments-with-azure-devtest-labs"></a><span data-ttu-id="1e4b3-113">Implementatie van ontwikkelaars omgevingen met Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="1e4b3-113">Implementing developer environments with Azure DevTest Labs</span></span>
1. <span data-ttu-id="1e4b3-114">**De testomgeving maken**</span><span class="sxs-lookup"><span data-stu-id="1e4b3-114">**Create the lab**</span></span> 
   
    <span data-ttu-id="1e4b3-115">Labs vormen het beginpunt in Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="1e4b3-115">Labs are the starting point in Azure DevTest Labs.</span></span> <span data-ttu-id="1e4b3-116">Wanneer u een testomgeving maakt, kunt u taken uitvoert zoals gebruikers (ontwikkelaars) toevoegen aan het lab, beleid instellen voor het beheren van kosten, het definiëren van de VM-installatiekopieën die snel kunnen maken en meer.</span><span class="sxs-lookup"><span data-stu-id="1e4b3-116">Once you create a lab, you can perform tasks such as adding users (developers) to the lab, setting policies to control costs, defining VM images that can create quickly, and more.</span></span>  
   
    <span data-ttu-id="1e4b3-117">Meer leren door te klikken op de koppelingen in de volgende tabel:</span><span class="sxs-lookup"><span data-stu-id="1e4b3-117">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="1e4b3-118">Taak</span><span class="sxs-lookup"><span data-stu-id="1e4b3-118">Task</span></span> | <span data-ttu-id="1e4b3-119">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="1e4b3-119">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="1e4b3-120">Een lab maken in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="1e4b3-120">Create a lab in Azure DevTest Labs</span></span>](devtest-lab-create-lab.md) |<span data-ttu-id="1e4b3-121">Informatie over het maken van een testomgeving in Azure DevTest Labs in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1e4b3-121">Learn how to create a lab in Azure DevTest Labs in the Azure portal.</span></span> |
2. <span data-ttu-id="1e4b3-122">**Virtuele machines in minuten met behulp van vooraf gedefinieerde marketplace-installatiekopieën en aangepaste installatiekopieën maken**</span><span class="sxs-lookup"><span data-stu-id="1e4b3-122">**Create VMs in minutes using ready-made marketplace images and custom images**</span></span> 
   
    <span data-ttu-id="1e4b3-123">U kunt vooraf gedefinieerde installatiekopieën van een groot aantal afbeeldingen kiezen in Azure Marketplace en zodat ze beschikbaar zijn in de testomgeving.</span><span class="sxs-lookup"><span data-stu-id="1e4b3-123">You can pick ready-made images from a wide variety of images in the Azure Marketplace and make them available in the lab.</span></span> <span data-ttu-id="1e4b3-124">Als de kant-en-afbeeldingen niet aan uw vereisten voldoet, kunt u een aangepaste installatiekopie maken door het maken van een testomgeving VM die gebruikmaakt van een installatiekopie van een vooraf gedefinieerde uit Azure Marketplace, installatie van de software die u nodig hebt, en het opslaan van de virtuele machine als een aangepaste installatiekopie in de testomgeving.</span><span class="sxs-lookup"><span data-stu-id="1e4b3-124">If the ready-made images don't meet your requirements, you can create a custom image by creating a lab VM using a ready-made image from Azure Marketplace, installing all the software that you need, and saving the VM as a custom image in the lab.</span></span>

    <span data-ttu-id="1e4b3-125">Als u aangepaste installatiekopieën gebruikt, kunt u overwegen de fabrieksinstellingen van een installatiekopie te maken en distribueren van uw afbeeldingen.</span><span class="sxs-lookup"><span data-stu-id="1e4b3-125">If you will be using custom images, consider using an image factory to create and distribute your images.</span></span> <span data-ttu-id="1e4b3-126">De fabrieksinstellingen van een installatiekopie is een configuratie als code-oplossing die regelmatig bouwt en uw geconfigureerde installatiekopieën automatisch distribueert.</span><span class="sxs-lookup"><span data-stu-id="1e4b3-126">An image factory is a configuration-as-code solution that regularly builds and distributes your configured images automatically.</span></span> <span data-ttu-id="1e4b3-127">Hierdoor wordt de tijd die nodig zijn om het systeem handmatig configureren nadat een virtuele machine is gemaakt met het Basisbesturingssysteem opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="1e4b3-127">This saves the time required to manually configure the system after a VM has been created with the base OS.</span></span>
  
    <span data-ttu-id="1e4b3-128">Meer leren door te klikken op de koppelingen in de volgende tabel:</span><span class="sxs-lookup"><span data-stu-id="1e4b3-128">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="1e4b3-129">Taak</span><span class="sxs-lookup"><span data-stu-id="1e4b3-129">Task</span></span> | <span data-ttu-id="1e4b3-130">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="1e4b3-130">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="1e4b3-131">Azure Marketplace-installatiekopieën configureren</span><span class="sxs-lookup"><span data-stu-id="1e4b3-131">Configure Azure Marketplace images</span></span>](devtest-lab-configure-marketplace-images.md) |<span data-ttu-id="1e4b3-132">Meer informatie over hoe u kunt geaccepteerde Azure Marketplace-installatiekopieën, beschikbaar voor selectie alleen de installatiekopieën die u voor de ontwikkelaars wilt maken.</span><span class="sxs-lookup"><span data-stu-id="1e4b3-132">Learn how you can whitelist Azure Marketplace images, making available for selection only the images you want for the developers.</span></span>|
   | [<span data-ttu-id="1e4b3-133">Een aangepaste installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="1e4b3-133">Create a custom image</span></span>](devtest-lab-create-template.md) |<span data-ttu-id="1e4b3-134">Een aangepaste installatiekopie maken door het vooraf installeren van de software die u nodig hebt, zodat ontwikkelaars snel een virtuele machine met behulp van de aangepaste installatiekopie kunnen maken.</span><span class="sxs-lookup"><span data-stu-id="1e4b3-134">Create a custom image by pre-installing the software you need so that developers can quickly create a VM using the custom image.</span></span>|
   | [<span data-ttu-id="1e4b3-135">Meer informatie over de installatiekopie-factory</span><span class="sxs-lookup"><span data-stu-id="1e4b3-135">Learn about image factory</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2017/04/17/video-custom-image-factory-with-azure-devtest-labs/) |<span data-ttu-id="1e4b3-136">Bekijk een video waarin wordt beschreven hoe instellen en gebruiken van een installatiekopie-factory.</span><span class="sxs-lookup"><span data-stu-id="1e4b3-136">Watch a video that describes how to set up and use an image factory.</span></span>|

3. <span data-ttu-id="1e4b3-137">**Herbruikbare sjablonen maken voor ontwikkelaars machines**</span><span class="sxs-lookup"><span data-stu-id="1e4b3-137">**Create reusable templates for developer machines**</span></span> 
   
    <span data-ttu-id="1e4b3-138">Een formule in Azure DevTest Labs is een lijst van de eigenschap standaardwaarden gebruikt voor het maken van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="1e4b3-138">A formula in Azure DevTest Labs is a list of default property values used to create a VM.</span></span> <span data-ttu-id="1e4b3-139">U kunt een formule in de testomgeving door het verzamelen van een installatiekopie van een VM-grootte (een combinatie van CPU en RAM) en een virtueel netwerk maken.</span><span class="sxs-lookup"><span data-stu-id="1e4b3-139">You can create a formula in the lab by picking an image, a VM size (a combination of CPU and RAM), and a virtual network.</span></span> <span data-ttu-id="1e4b3-140">Elke ontwikkelaar kan de formule zien in de testomgeving en deze gebruiken voor het maken van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="1e4b3-140">Each developer can see the formula in the lab and use it to create a VM.</span></span> 
   
    <span data-ttu-id="1e4b3-141">Meer leren door te klikken op de koppelingen in de volgende tabel:</span><span class="sxs-lookup"><span data-stu-id="1e4b3-141">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="1e4b3-142">Taak</span><span class="sxs-lookup"><span data-stu-id="1e4b3-142">Task</span></span> | <span data-ttu-id="1e4b3-143">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="1e4b3-143">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="1e4b3-144">DevTest Labs formules voor het maken van virtuele machines beheren</span><span class="sxs-lookup"><span data-stu-id="1e4b3-144">Manage DevTest Labs formulas to create VMs</span></span>](devtest-lab-manage-formulas.md) |<span data-ttu-id="1e4b3-145">Meer informatie over hoe u een formule kunt maken met een installatiekopie van een VM-grootte (combinatie van CPU en RAM) en een virtueel netwerk ophalen.</span><span class="sxs-lookup"><span data-stu-id="1e4b3-145">Learn how you can create a formula by picking up an image, VM size (combination of CPU and RAM), and a virtual network.</span></span>|

4. <span data-ttu-id="1e4b3-146">**Artefacten zodat flexibele aanpassing van de virtuele machine maken**</span><span class="sxs-lookup"><span data-stu-id="1e4b3-146">**Create artifacts to enable flexible VM customization**</span></span>

   <span data-ttu-id="1e4b3-147">Artefacten worden gebruikt voor het implementeren en configureren van uw toepassing nadat een virtuele machine is ingericht.</span><span class="sxs-lookup"><span data-stu-id="1e4b3-147">Artifacts are used to deploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="1e4b3-148">Artefacten kunnen het volgende zijn:</span><span class="sxs-lookup"><span data-stu-id="1e4b3-148">Artifacts can be:</span></span>

   - <span data-ttu-id="1e4b3-149">Hulpprogramma's die u wilt installeren op de virtuele machine - zoals agents, Fiddler en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1e4b3-149">Tools that you want to install on the VM - such as agents, Fiddler, and Visual Studio.</span></span>
   - <span data-ttu-id="1e4b3-150">Acties die u uitvoeren op de VM wilt, zoals het klonen van een opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="1e4b3-150">Actions that you want to run on the VM - such as cloning a repo.</span></span>
   - <span data-ttu-id="1e4b3-151">Programma's die u wilt testen.</span><span class="sxs-lookup"><span data-stu-id="1e4b3-151">Applications that you want to test.</span></span>

   <span data-ttu-id="1e4b3-152">Veel artefacten zijn al beschikbaar out-of-the-box.</span><span class="sxs-lookup"><span data-stu-id="1e4b3-152">Many artifacts are already available out-of-the-box.</span></span> <span data-ttu-id="1e4b3-153">U kunt uw eigen aangepaste artefacten maken als u wilt dat meer aanpassen voor uw specifieke behoeften.</span><span class="sxs-lookup"><span data-stu-id="1e4b3-153">You can create your own custom artifacts if you want more customization for your specific needs.</span></span>

   <span data-ttu-id="1e4b3-154">Meer leren door te klikken op de koppelingen in de volgende tabel:</span><span class="sxs-lookup"><span data-stu-id="1e4b3-154">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="1e4b3-155">Taak</span><span class="sxs-lookup"><span data-stu-id="1e4b3-155">Task</span></span> | <span data-ttu-id="1e4b3-156">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="1e4b3-156">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="1e4b3-157">Aangepaste artefacten maken voor uw DevTest Labs VM</span><span class="sxs-lookup"><span data-stu-id="1e4b3-157">Create custom artifacts for your DevTest Labs VM</span></span>](devtest-lab-artifact-author.md) |<span data-ttu-id="1e4b3-158">Maak uw eigen aangepaste artefacten voor de virtuele machines in uw testomgeving.</span><span class="sxs-lookup"><span data-stu-id="1e4b3-158">Create your own custom artifacts for the virtual machines in your lab.</span></span>|
   | [<span data-ttu-id="1e4b3-159">Voeg een Git-opslagplaats voor het opslaan van aangepaste artefacten en Azure Resource Manager-sjablonen voor gebruik in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="1e4b3-159">Add a Git repository to store custom artifacts and Azure Resource Manager templates for use in Azure DevTest Labs</span></span>](devtest-lab-add-artifact-repo.md) |<span data-ttu-id="1e4b3-160">Informatie over het opslaan van uw aangepaste artefacten in uw eigen persoonlijke Git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="1e4b3-160">Learn how to store your custom artifacts in your own private Git repo.</span></span>|

5. <span data-ttu-id="1e4b3-161">**Beheer van kosten**</span><span class="sxs-lookup"><span data-stu-id="1e4b3-161">**Control costs**</span></span>
   
    <span data-ttu-id="1e4b3-162">Azure DevTest Labs kunt u een beleid in een testomgeving om Geef het maximum aantal VM's die kunnen worden gemaakt door een ontwikkelaar in de testomgeving instellen.</span><span class="sxs-lookup"><span data-stu-id="1e4b3-162">Azure DevTest Labs allows you to set a policy in the lab to specify the maximum number of VMs that can be created by a developer in the lab.</span></span> 
   
    <span data-ttu-id="1e4b3-163">Als uw developer-team heeft een set werken planning en u wilt stoppen van de virtuele machines op een bepaald tijdstip van de dag en vervolgens automatisch opnieuw opgestart ze de volgende dag, kunt u die eenvoudig uitvoeren door het instellen van beleidsregels voor automatisch afsluiten en automatisch starten in de testomgeving.</span><span class="sxs-lookup"><span data-stu-id="1e4b3-163">If your developer team has a set work schedule and you want to stop all the VMs at a particular time of the day and then automatically restart them the following day, you can easily accomplish that by setting auto-shutdown and auto-start policies in the lab.</span></span> 
   
    <span data-ttu-id="1e4b3-164">Ten slotte, als ontwikkeling van apps voltooid is, kunt u verwijderen de virtuele machines in één keer een één PowerShell-script uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="1e4b3-164">Finally, when app development is complete, you can delete all the VMs at once by running a single PowerShell script.</span></span> 
   
    <span data-ttu-id="1e4b3-165">Meer leren door te klikken op de koppelingen in de volgende tabel:</span><span class="sxs-lookup"><span data-stu-id="1e4b3-165">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="1e4b3-166">Taak</span><span class="sxs-lookup"><span data-stu-id="1e4b3-166">Task</span></span> | <span data-ttu-id="1e4b3-167">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="1e4b3-167">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="1e4b3-168">Beleid voor lab maken</span><span class="sxs-lookup"><span data-stu-id="1e4b3-168">Define lab policies</span></span>](devtest-lab-set-lab-policy.md) |<span data-ttu-id="1e4b3-169">Kosten beheren door het instellen van beleidsregels in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="1e4b3-169">Control costs by setting policies in the lab.</span></span> |
   | [<span data-ttu-id="1e4b3-170">Verwijder alle lab virtuele machines met een PowerShell-script</span><span class="sxs-lookup"><span data-stu-id="1e4b3-170">Delete all the lab VMs using a PowerShell script</span></span>](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |<span data-ttu-id="1e4b3-171">Verwijder alle labs in één bewerking als ontwikkeling voltooid is.</span><span class="sxs-lookup"><span data-stu-id="1e4b3-171">Delete all the labs in one operation when development is complete.</span></span>|

1. <span data-ttu-id="1e4b3-172">**Een virtueel netwerk toevoegen aan een virtuele machine**</span><span class="sxs-lookup"><span data-stu-id="1e4b3-172">**Add a virtual network to a VM**</span></span> 
   
    <span data-ttu-id="1e4b3-173">DevTest Labs maakt een nieuw virtueel netwerk (VNET) als een lab is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1e4b3-173">DevTest Labs creates a new virtual network (VNET) whenever a lab is created.</span></span> <span data-ttu-id="1e4b3-174">Als u uw eigen VNET hebt geconfigureerd: bijvoorbeeld via ExpressRoute of site-naar-site VPN-kunt u dit VNET toevoegen aan de instellingen van het virtuele netwerk van uw lab zodat deze beschikbaar is bij het maken van virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="1e4b3-174">If you have configured your own VNET – for example, by using ExpressRoute or site-to-site VPN – you can add this VNET to your lab's virtual network settings so that it is available when creating VMs.</span></span>

    <span data-ttu-id="1e4b3-175">Daarnaast is er een beschikbaar die wordt een virtuele machine toevoegen aan een domein, wanneer de virtuele machine wordt gemaakt van Azure Active Directory domain join artefact.</span><span class="sxs-lookup"><span data-stu-id="1e4b3-175">In addition, there is an Azure Active Directory domain join artifact available that will join a VM to a domain when the VM is being created.</span></span> 
   
    <span data-ttu-id="1e4b3-176">Meer leren door te klikken op de koppelingen in de volgende tabel:</span><span class="sxs-lookup"><span data-stu-id="1e4b3-176">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="1e4b3-177">Taak</span><span class="sxs-lookup"><span data-stu-id="1e4b3-177">Task</span></span> | <span data-ttu-id="1e4b3-178">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="1e4b3-178">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="1e4b3-179">Een virtueel netwerk configureren in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="1e4b3-179">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md) |<span data-ttu-id="1e4b3-180">Informatie over het configureren van een virtueel netwerk in Azure DevTest Labs met de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1e4b3-180">Learn how to configure a virtual network in Azure DevTest Labs using the Azure portal.</span></span>|

6. <span data-ttu-id="1e4b3-181">**De testomgeving delen met elke ontwikkelaar**</span><span class="sxs-lookup"><span data-stu-id="1e4b3-181">**Share the lab with each developer**</span></span>
   
    <span data-ttu-id="1e4b3-182">Labs zijn rechtstreeks toegankelijk via een koppeling die u met uw ontwikkelaars deelt.</span><span class="sxs-lookup"><span data-stu-id="1e4b3-182">Labs can be directly accessed using a link that you share with your developers.</span></span> <span data-ttu-id="1e4b3-183">Ze hoeft te hebben van een Azure-account, zolang ze beschikken over een [Microsoft-account](devtest-lab-faq.md#what-is-a-microsoft-account).</span><span class="sxs-lookup"><span data-stu-id="1e4b3-183">They don't even have to have an Azure account, as long as they have a [Microsoft account](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span> <span data-ttu-id="1e4b3-184">Ontwikkelaars zichtbaar niet voor virtuele machines die zijn gemaakt door andere ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="1e4b3-184">Developers cannot see VMs created by other developers.</span></span>  
   
    <span data-ttu-id="1e4b3-185">Meer leren door te klikken op de koppelingen in de volgende tabel:</span><span class="sxs-lookup"><span data-stu-id="1e4b3-185">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="1e4b3-186">Taak</span><span class="sxs-lookup"><span data-stu-id="1e4b3-186">Task</span></span> | <span data-ttu-id="1e4b3-187">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="1e4b3-187">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="1e4b3-188">Een ontwikkelaar toevoegen aan een lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="1e4b3-188">Add a developer to a lab in Azure DevTest Labs</span></span>](devtest-lab-add-devtest-user.md) |<span data-ttu-id="1e4b3-189">De Azure portal gebruiken voor ontwikkelaars toevoegen aan uw testomgeving.</span><span class="sxs-lookup"><span data-stu-id="1e4b3-189">Use the Azure portal to add developers to your lab.</span></span>|
   | [<span data-ttu-id="1e4b3-190">Ontwikkelaars toevoegen aan de testomgeving met een PowerShell-script</span><span class="sxs-lookup"><span data-stu-id="1e4b3-190">Add developers to the lab using a PowerShell script</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |<span data-ttu-id="1e4b3-191">PowerShell gebruiken voor het automatiseren van ontwikkelaars van toe te voegen aan uw testomgeving.</span><span class="sxs-lookup"><span data-stu-id="1e4b3-191">Use PowerShell to automate adding developers to your lab.</span></span> |
   | [<span data-ttu-id="1e4b3-192">Een koppeling naar het lab</span><span class="sxs-lookup"><span data-stu-id="1e4b3-192">Get a link to the lab</span></span>](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |<span data-ttu-id="1e4b3-193">Meer informatie over hoe ontwikkelaars rechtstreeks toegang tot een lab via een hyperlink.</span><span class="sxs-lookup"><span data-stu-id="1e4b3-193">Learn how developers can directly access a lab via a hyperlink.</span></span>|

7. <span data-ttu-id="1e4b3-194">**Lab maken voor meer teams automatiseren**</span><span class="sxs-lookup"><span data-stu-id="1e4b3-194">**Automate lab creation for more teams**</span></span> 
   
    <span data-ttu-id="1e4b3-195">U kunt maken van de testomgeving, met inbegrip van aangepaste instellingen door Resource Manager-sjabloon maken en deze opnieuw maken van identieke labs automatiseren.</span><span class="sxs-lookup"><span data-stu-id="1e4b3-195">You can automate lab creation, including custom settings, by creating a Resource Manager template and using it to create identical labs again and again.</span></span> 
   
    <span data-ttu-id="1e4b3-196">Meer leren door te klikken op de koppelingen in de volgende tabel:</span><span class="sxs-lookup"><span data-stu-id="1e4b3-196">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="1e4b3-197">Taak</span><span class="sxs-lookup"><span data-stu-id="1e4b3-197">Task</span></span> | <span data-ttu-id="1e4b3-198">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="1e4b3-198">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="1e4b3-199">Een lab met een Resource Manager-sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="1e4b3-199">Create a lab using a Resource Manager template</span></span>](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |<span data-ttu-id="1e4b3-200">Labs in Azure DevTest Labs met Resource Manager-sjablonen maken.</span><span class="sxs-lookup"><span data-stu-id="1e4b3-200">Create labs in Azure DevTest Labs using Resource Manager templates.</span></span> |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

