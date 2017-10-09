---
title: aaaUse Azure DevTest Labs voor ontwikkelaars | Microsoft Docs
description: Meer informatie over hoe Azure DevTest Labs toouse voor scenario's voor ontwikkelaars.
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
ms.openlocfilehash: 16a3ef47c9fcbca3050dd50db5b472a9a1e3c62c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-devtest-labs-for-developers"></a><span data-ttu-id="874e9-103">Gebruik Azure DevTest Labs voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="874e9-103">Use Azure DevTest Labs for developers</span></span>
<span data-ttu-id="874e9-104">Azure DevTest Labs kunnen worden gebruikt tooimplement veel belangrijke scenario's, maar een van de primaire Hallo-scenario's omvat het gebruik van DevTest Labs toohost ontwikkeling machines voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="874e9-104">Azure DevTest Labs can be used tooimplement many key scenarios, but one of hello primary scenarios involves using DevTest Labs toohost development machines for developers.</span></span> <span data-ttu-id="874e9-105">In dit scenario biedt DevTest Labs de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="874e9-105">In this scenario, DevTest Labs provides these benefits:</span></span>

- <span data-ttu-id="874e9-106">Ontwikkelaars kunnen hun computers ontwikkeling op aanvraag snel inrichten.</span><span class="sxs-lookup"><span data-stu-id="874e9-106">Developers can quickly provision their development machines on demand.</span></span>
- <span data-ttu-id="874e9-107">Ontwikkelaars kunnen hun computers ontwikkeling als dat nodig is gemakkelijk aanpassen.</span><span class="sxs-lookup"><span data-stu-id="874e9-107">Developers can easily customize their development machines whenever needed.</span></span>
- <span data-ttu-id="874e9-108">Beheerders kunnen kosten beheren door ervoor te zorgen dat:</span><span class="sxs-lookup"><span data-stu-id="874e9-108">Administrators can control costs by ensuring that:</span></span>
  - <span data-ttu-id="874e9-109">Ontwikkelaars kunnen niet meer virtuele machines dan ze nodig hebben voor de ontwikkeling van ophalen.</span><span class="sxs-lookup"><span data-stu-id="874e9-109">Developers cannot get more VMs than they need for development.</span></span>
  - <span data-ttu-id="874e9-110">Virtuele machines worden afgesloten wanneer deze niet in gebruik.</span><span class="sxs-lookup"><span data-stu-id="874e9-110">VMs are shut down when not in use.</span></span> 

![DevTest Labs gebruiken voor training](./media/devtest-lab-developer-lab/devtest-lab-developer-lab.png)

<span data-ttu-id="874e9-112">In dit artikel leert u verschillende functies van Azure DevTest Labs die kunnen worden gebruikt toomeet developer-vereisten en Hallo gedetailleerde stappen dat u tooset van een testomgeving kunt volgen.</span><span class="sxs-lookup"><span data-stu-id="874e9-112">In this article, you learn about various Azure DevTest Labs features that can be used toomeet developer requirements and hello detailed steps that you can follow tooset up a lab.</span></span>

## <a name="implementing-developer-environments-with-azure-devtest-labs"></a><span data-ttu-id="874e9-113">Implementatie van ontwikkelaars omgevingen met Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="874e9-113">Implementing developer environments with Azure DevTest Labs</span></span>
1. <span data-ttu-id="874e9-114">**Hallo lab maken**</span><span class="sxs-lookup"><span data-stu-id="874e9-114">**Create hello lab**</span></span> 
   
    <span data-ttu-id="874e9-115">Labs zijn Hallo beginpunt in Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="874e9-115">Labs are hello starting point in Azure DevTest Labs.</span></span> <span data-ttu-id="874e9-116">Wanneer u een testomgeving maakt, kunt u taken zoals het toevoegen van gebruikers (ontwikkelaars) toohello lab, instelling beleid toocontrol kosten, het definiëren van de VM-installatiekopieën die snel kunnen maken en meer uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="874e9-116">Once you create a lab, you can perform tasks such as adding users (developers) toohello lab, setting policies toocontrol costs, defining VM images that can create quickly, and more.</span></span>  
   
    <span data-ttu-id="874e9-117">Meer informatie door te klikken op koppelingen in de volgende tabel Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="874e9-117">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="874e9-118">Taak</span><span class="sxs-lookup"><span data-stu-id="874e9-118">Task</span></span> | <span data-ttu-id="874e9-119">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="874e9-119">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="874e9-120">Een lab maken in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="874e9-120">Create a lab in Azure DevTest Labs</span></span>](devtest-lab-create-lab.md) |<span data-ttu-id="874e9-121">Meer informatie over hoe toocreate een lab in Azure DevTest Labs in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="874e9-121">Learn how toocreate a lab in Azure DevTest Labs in hello Azure portal.</span></span> |
2. <span data-ttu-id="874e9-122">**Virtuele machines in minuten met behulp van vooraf gedefinieerde marketplace-installatiekopieën en aangepaste installatiekopieën maken**</span><span class="sxs-lookup"><span data-stu-id="874e9-122">**Create VMs in minutes using ready-made marketplace images and custom images**</span></span> 
   
    <span data-ttu-id="874e9-123">U kunt vooraf gedefinieerde installatiekopieën van een groot aantal afbeeldingen kiezen in hello Azure Marketplace en zodat ze beschikbaar zijn in de testomgeving Hallo.</span><span class="sxs-lookup"><span data-stu-id="874e9-123">You can pick ready-made images from a wide variety of images in hello Azure Marketplace and make them available in hello lab.</span></span> <span data-ttu-id="874e9-124">Als Hallo kant-en-afbeeldingen niet aan uw vereisten voldoet, kunt u een aangepaste installatiekopie maken door het maken van een testomgeving met de installatiekopie van een vooraf gedefinieerde vanuit Azure Marketplace, alle Hallo software installeren die u nodig hebt, en opslaan Hallo VM als een aangepaste installatiekopie in de testomgeving Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="874e9-124">If hello ready-made images don't meet your requirements, you can create a custom image by creating a lab VM using a ready-made image from Azure Marketplace, installing all hello software that you need, and saving hello VM as a custom image in hello lab.</span></span>

    <span data-ttu-id="874e9-125">Als u aangepaste installatiekopieën gebruikt, overweeg het gebruik van een installatiekopie factory toocreate en distribueren van uw afbeeldingen.</span><span class="sxs-lookup"><span data-stu-id="874e9-125">If you will be using custom images, consider using an image factory toocreate and distribute your images.</span></span> <span data-ttu-id="874e9-126">De fabrieksinstellingen van een installatiekopie is een configuratie als code-oplossing die regelmatig bouwt en uw geconfigureerde installatiekopieën automatisch distribueert.</span><span class="sxs-lookup"><span data-stu-id="874e9-126">An image factory is a configuration-as-code solution that regularly builds and distributes your configured images automatically.</span></span> <span data-ttu-id="874e9-127">Dit bespaart Hallo tijd die nodig is toomanually Hallo system configureren nadat een virtuele machine is gemaakt met de Hallo OS baseren.</span><span class="sxs-lookup"><span data-stu-id="874e9-127">This saves hello time required toomanually configure hello system after a VM has been created with hello base OS.</span></span>
  
    <span data-ttu-id="874e9-128">Meer informatie door te klikken op koppelingen in de volgende tabel Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="874e9-128">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="874e9-129">Taak</span><span class="sxs-lookup"><span data-stu-id="874e9-129">Task</span></span> | <span data-ttu-id="874e9-130">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="874e9-130">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="874e9-131">Azure Marketplace-installatiekopieën configureren</span><span class="sxs-lookup"><span data-stu-id="874e9-131">Configure Azure Marketplace images</span></span>](devtest-lab-configure-marketplace-images.md) |<span data-ttu-id="874e9-132">Meer informatie over hoe u kunt geaccepteerde Azure Marketplace-installatiekopieën, beschikbaar voor selectie alleen Hallo afbeeldingen die u voor Hallo ontwikkelaars maken.</span><span class="sxs-lookup"><span data-stu-id="874e9-132">Learn how you can whitelist Azure Marketplace images, making available for selection only hello images you want for hello developers.</span></span>|
   | [<span data-ttu-id="874e9-133">Een aangepaste installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="874e9-133">Create a custom image</span></span>](devtest-lab-create-template.md) |<span data-ttu-id="874e9-134">Maak een aangepaste installatiekopie vooraf Hallo door software te installeren u moet zodat ontwikkelaars snel een virtuele machine met behulp van de aangepaste installatiekopie Hallo kunnen maken.</span><span class="sxs-lookup"><span data-stu-id="874e9-134">Create a custom image by pre-installing hello software you need so that developers can quickly create a VM using hello custom image.</span></span>|
   | [<span data-ttu-id="874e9-135">Meer informatie over de installatiekopie-factory</span><span class="sxs-lookup"><span data-stu-id="874e9-135">Learn about image factory</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2017/04/17/video-custom-image-factory-with-azure-devtest-labs/) |<span data-ttu-id="874e9-136">Bekijk een video waarin wordt beschreven hoe tooset boven en een installatiekopie factory gebruiken.</span><span class="sxs-lookup"><span data-stu-id="874e9-136">Watch a video that describes how tooset up and use an image factory.</span></span>|

3. <span data-ttu-id="874e9-137">**Herbruikbare sjablonen maken voor ontwikkelaars machines**</span><span class="sxs-lookup"><span data-stu-id="874e9-137">**Create reusable templates for developer machines**</span></span> 
   
    <span data-ttu-id="874e9-138">Een formule in Azure DevTest Labs is dat een lijst met standaardwaarden voor de eigenschap toocreate een virtuele machine gebruikt.</span><span class="sxs-lookup"><span data-stu-id="874e9-138">A formula in Azure DevTest Labs is a list of default property values used toocreate a VM.</span></span> <span data-ttu-id="874e9-139">U kunt een formule in Hallo lab maken door het verzamelen van een installatiekopie van een VM-grootte (een combinatie van CPU en RAM) en een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="874e9-139">You can create a formula in hello lab by picking an image, a VM size (a combination of CPU and RAM), and a virtual network.</span></span> <span data-ttu-id="874e9-140">Elke ontwikkelaar kan zien Hallo formule in Hallo lab en toocreate een virtuele machine worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="874e9-140">Each developer can see hello formula in hello lab and use it toocreate a VM.</span></span> 
   
    <span data-ttu-id="874e9-141">Meer informatie door te klikken op koppelingen in de volgende tabel Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="874e9-141">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="874e9-142">Taak</span><span class="sxs-lookup"><span data-stu-id="874e9-142">Task</span></span> | <span data-ttu-id="874e9-143">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="874e9-143">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="874e9-144">DevTest Labs formules toocreate VM's beheren</span><span class="sxs-lookup"><span data-stu-id="874e9-144">Manage DevTest Labs formulas toocreate VMs</span></span>](devtest-lab-manage-formulas.md) |<span data-ttu-id="874e9-145">Meer informatie over hoe u een formule kunt maken met een installatiekopie van een VM-grootte (combinatie van CPU en RAM) en een virtueel netwerk ophalen.</span><span class="sxs-lookup"><span data-stu-id="874e9-145">Learn how you can create a formula by picking up an image, VM size (combination of CPU and RAM), and a virtual network.</span></span>|

4. <span data-ttu-id="874e9-146">**Artefacten tooenable flexibele VM aanpassing maken**</span><span class="sxs-lookup"><span data-stu-id="874e9-146">**Create artifacts tooenable flexible VM customization**</span></span>

   <span data-ttu-id="874e9-147">Artefacten zijn gebruikte toodeploy en uw toepassing configureren nadat een virtuele machine is ingericht.</span><span class="sxs-lookup"><span data-stu-id="874e9-147">Artifacts are used toodeploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="874e9-148">Artefacten kunnen het volgende zijn:</span><span class="sxs-lookup"><span data-stu-id="874e9-148">Artifacts can be:</span></span>

   - <span data-ttu-id="874e9-149">Hulpprogramma's die u tooinstall op Hallo VM, zoals agents, Fiddler en Visual Studio wilt.</span><span class="sxs-lookup"><span data-stu-id="874e9-149">Tools that you want tooinstall on hello VM - such as agents, Fiddler, and Visual Studio.</span></span>
   - <span data-ttu-id="874e9-150">Acties die u wilt de toorun op Hallo VM, zoals het klonen van een opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="874e9-150">Actions that you want toorun on hello VM - such as cloning a repo.</span></span>
   - <span data-ttu-id="874e9-151">Toepassingen die u tootest wilt.</span><span class="sxs-lookup"><span data-stu-id="874e9-151">Applications that you want tootest.</span></span>

   <span data-ttu-id="874e9-152">Veel artefacten zijn al beschikbaar out-of-the-box.</span><span class="sxs-lookup"><span data-stu-id="874e9-152">Many artifacts are already available out-of-the-box.</span></span> <span data-ttu-id="874e9-153">U kunt uw eigen aangepaste artefacten maken als u wilt dat meer aanpassen voor uw specifieke behoeften.</span><span class="sxs-lookup"><span data-stu-id="874e9-153">You can create your own custom artifacts if you want more customization for your specific needs.</span></span>

   <span data-ttu-id="874e9-154">Meer informatie door te klikken op koppelingen in de volgende tabel Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="874e9-154">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="874e9-155">Taak</span><span class="sxs-lookup"><span data-stu-id="874e9-155">Task</span></span> | <span data-ttu-id="874e9-156">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="874e9-156">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="874e9-157">Aangepaste artefacten maken voor uw DevTest Labs VM</span><span class="sxs-lookup"><span data-stu-id="874e9-157">Create custom artifacts for your DevTest Labs VM</span></span>](devtest-lab-artifact-author.md) |<span data-ttu-id="874e9-158">Maak uw eigen aangepaste artefacten voor Hallo virtuele machines in uw testomgeving.</span><span class="sxs-lookup"><span data-stu-id="874e9-158">Create your own custom artifacts for hello virtual machines in your lab.</span></span>|
   | [<span data-ttu-id="874e9-159">Voeg een Git-opslagplaats toostore aangepaste artefacten en Azure Resource Manager-sjablonen voor gebruik in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="874e9-159">Add a Git repository toostore custom artifacts and Azure Resource Manager templates for use in Azure DevTest Labs</span></span>](devtest-lab-add-artifact-repo.md) |<span data-ttu-id="874e9-160">Meer informatie over hoe toostore uw aangepaste artefacten in uw eigen persoonlijke Git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="874e9-160">Learn how toostore your custom artifacts in your own private Git repo.</span></span>|

5. <span data-ttu-id="874e9-161">**Beheer van kosten**</span><span class="sxs-lookup"><span data-stu-id="874e9-161">**Control costs**</span></span>
   
    <span data-ttu-id="874e9-162">Azure DevTest Labs kunt u tooset een beleid Hallo lab toospecify Hallo maximum aantal VM's die kunnen worden gemaakt door een ontwikkelaar in Hallo-testomgeving.</span><span class="sxs-lookup"><span data-stu-id="874e9-162">Azure DevTest Labs allows you tooset a policy in hello lab toospecify hello maximum number of VMs that can be created by a developer in hello lab.</span></span> 
   
    <span data-ttu-id="874e9-163">Als uw developer-team heeft een set werkschema en u wilt dat toostop alle Hallo virtuele machines op een bepaald tijdstip Hallo en vervolgens automatisch opnieuw opgestart ze Hallo na dag, kunt u die gemakkelijk door instelling automatisch afsluiten en automatisch starten van beleid in Hallo lab uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="874e9-163">If your developer team has a set work schedule and you want toostop all hello VMs at a particular time of hello day and then automatically restart them hello following day, you can easily accomplish that by setting auto-shutdown and auto-start policies in hello lab.</span></span> 
   
    <span data-ttu-id="874e9-164">Ten slotte, als ontwikkeling van apps voltooid is, kunt u verwijderen alle Hallo VM's in één keer een één PowerShell-script uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="874e9-164">Finally, when app development is complete, you can delete all hello VMs at once by running a single PowerShell script.</span></span> 
   
    <span data-ttu-id="874e9-165">Meer informatie door te klikken op koppelingen in de volgende tabel Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="874e9-165">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="874e9-166">Taak</span><span class="sxs-lookup"><span data-stu-id="874e9-166">Task</span></span> | <span data-ttu-id="874e9-167">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="874e9-167">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="874e9-168">Beleid voor lab maken</span><span class="sxs-lookup"><span data-stu-id="874e9-168">Define lab policies</span></span>](devtest-lab-set-lab-policy.md) |<span data-ttu-id="874e9-169">Kosten door het instellen van beleidsregels in Hallo lab te controleren.</span><span class="sxs-lookup"><span data-stu-id="874e9-169">Control costs by setting policies in hello lab.</span></span> |
   | [<span data-ttu-id="874e9-170">Verwijder alle Hallo lab virtuele machines met een PowerShell-script</span><span class="sxs-lookup"><span data-stu-id="874e9-170">Delete all hello lab VMs using a PowerShell script</span></span>](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |<span data-ttu-id="874e9-171">Verwijder alle Hallo labs in één bewerking als ontwikkeling voltooid is.</span><span class="sxs-lookup"><span data-stu-id="874e9-171">Delete all hello labs in one operation when development is complete.</span></span>|

1. <span data-ttu-id="874e9-172">**Toevoegen van een virtueel netwerk tooa VM**</span><span class="sxs-lookup"><span data-stu-id="874e9-172">**Add a virtual network tooa VM**</span></span> 
   
    <span data-ttu-id="874e9-173">DevTest Labs maakt een nieuw virtueel netwerk (VNET) als een lab is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="874e9-173">DevTest Labs creates a new virtual network (VNET) whenever a lab is created.</span></span> <span data-ttu-id="874e9-174">Als u uw eigen VNET hebt geconfigureerd: bijvoorbeeld via ExpressRoute of site-naar-site VPN-kunt u instellingen voor dit VNET tooyour lab virtuele netwerk kunt toevoegen, zodat deze beschikbaar is bij het maken van virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="874e9-174">If you have configured your own VNET – for example, by using ExpressRoute or site-to-site VPN – you can add this VNET tooyour lab's virtual network settings so that it is available when creating VMs.</span></span>

    <span data-ttu-id="874e9-175">Daarnaast is er een beschikbaar die wordt lid van een VM tooa domein wanneer Hallo VM wordt gemaakt van Azure Active Directory domain join artefact.</span><span class="sxs-lookup"><span data-stu-id="874e9-175">In addition, there is an Azure Active Directory domain join artifact available that will join a VM tooa domain when hello VM is being created.</span></span> 
   
    <span data-ttu-id="874e9-176">Meer informatie door te klikken op koppelingen in de volgende tabel Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="874e9-176">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="874e9-177">Taak</span><span class="sxs-lookup"><span data-stu-id="874e9-177">Task</span></span> | <span data-ttu-id="874e9-178">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="874e9-178">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="874e9-179">Een virtueel netwerk configureren in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="874e9-179">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md) |<span data-ttu-id="874e9-180">Meer informatie over hoe een virtueel netwerk in Azure DevTest Labs met behulp van tooconfigure hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="874e9-180">Learn how tooconfigure a virtual network in Azure DevTest Labs using hello Azure portal.</span></span>|

6. <span data-ttu-id="874e9-181">**Hallo lab delen met elke ontwikkelaar**</span><span class="sxs-lookup"><span data-stu-id="874e9-181">**Share hello lab with each developer**</span></span>
   
    <span data-ttu-id="874e9-182">Labs zijn rechtstreeks toegankelijk via een koppeling die u met uw ontwikkelaars deelt.</span><span class="sxs-lookup"><span data-stu-id="874e9-182">Labs can be directly accessed using a link that you share with your developers.</span></span> <span data-ttu-id="874e9-183">Ze niet zelfs toohave Azure-account hebt, zolang ze beschikken over een [Microsoft-account](devtest-lab-faq.md#what-is-a-microsoft-account).</span><span class="sxs-lookup"><span data-stu-id="874e9-183">They don't even have toohave an Azure account, as long as they have a [Microsoft account](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span> <span data-ttu-id="874e9-184">Ontwikkelaars zichtbaar niet voor virtuele machines die zijn gemaakt door andere ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="874e9-184">Developers cannot see VMs created by other developers.</span></span>  
   
    <span data-ttu-id="874e9-185">Meer informatie door te klikken op koppelingen in de volgende tabel Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="874e9-185">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="874e9-186">Taak</span><span class="sxs-lookup"><span data-stu-id="874e9-186">Task</span></span> | <span data-ttu-id="874e9-187">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="874e9-187">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="874e9-188">Een ontwikkelaar tooa lab toevoegen in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="874e9-188">Add a developer tooa lab in Azure DevTest Labs</span></span>](devtest-lab-add-devtest-user.md) |<span data-ttu-id="874e9-189">Gebruik hello Azure portal tooadd ontwikkelaars tooyour lab.</span><span class="sxs-lookup"><span data-stu-id="874e9-189">Use hello Azure portal tooadd developers tooyour lab.</span></span>|
   | [<span data-ttu-id="874e9-190">Ontwikkelaars toohello testomgeving met een PowerShell-script toevoegen</span><span class="sxs-lookup"><span data-stu-id="874e9-190">Add developers toohello lab using a PowerShell script</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |<span data-ttu-id="874e9-191">Gebruik PowerShell tooautomate ontwikkelaars tooyour lab toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="874e9-191">Use PowerShell tooautomate adding developers tooyour lab.</span></span> |
   | [<span data-ttu-id="874e9-192">Een koppeling toohello lab ophalen</span><span class="sxs-lookup"><span data-stu-id="874e9-192">Get a link toohello lab</span></span>](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |<span data-ttu-id="874e9-193">Meer informatie over hoe ontwikkelaars rechtstreeks toegang tot een lab via een hyperlink.</span><span class="sxs-lookup"><span data-stu-id="874e9-193">Learn how developers can directly access a lab via a hyperlink.</span></span>|

7. <span data-ttu-id="874e9-194">**Lab maken voor meer teams automatiseren**</span><span class="sxs-lookup"><span data-stu-id="874e9-194">**Automate lab creation for more teams**</span></span> 
   
    <span data-ttu-id="874e9-195">U kunt maken van de testomgeving, met inbegrip van aangepaste instellingen door te maken van een Resource Manager-sjabloon en het toocreate identiek labs opnieuw kunt automatiseren.</span><span class="sxs-lookup"><span data-stu-id="874e9-195">You can automate lab creation, including custom settings, by creating a Resource Manager template and using it toocreate identical labs again and again.</span></span> 
   
    <span data-ttu-id="874e9-196">Meer informatie door te klikken op koppelingen in de volgende tabel Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="874e9-196">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="874e9-197">Taak</span><span class="sxs-lookup"><span data-stu-id="874e9-197">Task</span></span> | <span data-ttu-id="874e9-198">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="874e9-198">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="874e9-199">Een lab met een Resource Manager-sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="874e9-199">Create a lab using a Resource Manager template</span></span>](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |<span data-ttu-id="874e9-200">Labs in Azure DevTest Labs met Resource Manager-sjablonen maken.</span><span class="sxs-lookup"><span data-stu-id="874e9-200">Create labs in Azure DevTest Labs using Resource Manager templates.</span></span> |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

