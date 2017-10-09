---
title: aaaUse Azure DevTest Labs voor virtuele machine en PaaS-testomgeving | Microsoft Docs
description: Meer informatie over hoe toouse Azure DevTest Labs voor virtuele machine en PaaS test omgeving scenario's.
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: d4e2c334-643a-40c9-9051-625b8f39fc86
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: tarcher
ms.openlocfilehash: 9285090da768491e1275942318b094fae89e3273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-devtest-labs-for-vm-and-paas-test-environments"></a><span data-ttu-id="4455a-103">Gebruik Azure DevTest Labs voor virtuele machine en PaaS-testomgeving</span><span class="sxs-lookup"><span data-stu-id="4455a-103">Use Azure DevTest Labs for VM and PaaS test environments</span></span>

<span data-ttu-id="4455a-104">U kunt Azure DevTest Labs tooimplement veel belangrijke scenario's, maar een primaire scenario omvat het gebruik van DevTest Labs toohost machines testers.</span><span class="sxs-lookup"><span data-stu-id="4455a-104">You can use Azure DevTest Labs tooimplement many key scenarios, but a primary scenario involves using DevTest Labs toohost machines for testers.</span></span> 

<span data-ttu-id="4455a-105">In dit scenario biedt DevTest Labs de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="4455a-105">In this scenario, DevTest Labs provides these benefits:</span></span>

- <span data-ttu-id="4455a-106">Testers kunnen Hallo meest recente versie van de toepassing testen door snel inrichten van Windows en Linux-omgevingen met herbruikbare sjablonen en artefacten.</span><span class="sxs-lookup"><span data-stu-id="4455a-106">Testers can test hello latest version of their application by quickly provisioning Windows and Linux environments using reusable templates and artifacts.</span></span>
- <span data-ttu-id="4455a-107">Testers kunnen opschalen van hun load testen door meerdere agents van de test wordt ingericht.</span><span class="sxs-lookup"><span data-stu-id="4455a-107">Testers can scale up their load testing by provisioning multiple test agents.</span></span>
- <span data-ttu-id="4455a-108">Beheerders kunnen kosten beheren door ervoor te zorgen dat:</span><span class="sxs-lookup"><span data-stu-id="4455a-108">Administrators can control costs by ensuring that:</span></span>
  - <span data-ttu-id="4455a-109">Testers kunnen meer virtuele machines dan ze nodig hebben niet ophalen.</span><span class="sxs-lookup"><span data-stu-id="4455a-109">Testers cannot get more VMs than they need.</span></span>
  - <span data-ttu-id="4455a-110">Virtuele machines worden afgesloten wanneer deze niet in gebruik.</span><span class="sxs-lookup"><span data-stu-id="4455a-110">VMs are shut down when not in use.</span></span>

![DevTest Labs gebruiken voor training](./media/devtest-lab-developer-lab/devtest-lab-developer-lab.png)

<span data-ttu-id="4455a-112">In dit artikel leert u informatie over de vereisten toomeet-tester voor verschillende Azure DevTest Labs functies die worden gebruikt en Hallo gedetailleerde stappen toofollow tooset van een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="4455a-112">In this article, you learn about various Azure DevTest Labs features used toomeet tester requirements and hello detailed steps toofollow tooset up a lab.</span></span>

## <a name="implementing-test-environments-with-azure-devtest-labs"></a><span data-ttu-id="4455a-113">Implementatie van testomgevingen met Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="4455a-113">Implementing test environments with Azure DevTest Labs</span></span>
1. <span data-ttu-id="4455a-114">**Hallo lab maken**</span><span class="sxs-lookup"><span data-stu-id="4455a-114">**Create hello lab**</span></span> 
   
    <span data-ttu-id="4455a-115">Labs zijn Hallo beginpunt in Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="4455a-115">Labs are hello starting point in Azure DevTest Labs.</span></span> <span data-ttu-id="4455a-116">Wanneer u een testomgeving maakt, kunt u taken zoals het toevoegen van gebruikers (testers) toohello lab, instelling beleid toocontrol kosten, het definiëren van de VM-installatiekopieën die snel kunnen maken en meer uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="4455a-116">Once you create a lab, you can perform tasks such as adding users (testers) toohello lab, setting policies toocontrol costs, defining VM images that can create quickly, and more.</span></span>  
   
    <span data-ttu-id="4455a-117">Meer informatie door te klikken op koppelingen in de volgende tabel Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="4455a-117">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="4455a-118">Taak</span><span class="sxs-lookup"><span data-stu-id="4455a-118">Task</span></span> | <span data-ttu-id="4455a-119">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="4455a-119">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="4455a-120">Een lab maken in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="4455a-120">Create a lab in Azure DevTest Labs</span></span>](devtest-lab-create-lab.md) |<span data-ttu-id="4455a-121">Meer informatie over hoe toocreate een lab in Azure DevTest Labs in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="4455a-121">Learn how toocreate a lab in Azure DevTest Labs in hello Azure portal.</span></span> |
2. <span data-ttu-id="4455a-122">**Virtuele machines in minuten met behulp van vooraf gedefinieerde marketplace-installatiekopieën en aangepaste installatiekopieën maken**</span><span class="sxs-lookup"><span data-stu-id="4455a-122">**Create VMs in minutes using ready-made marketplace images and custom images**</span></span> 
   
    <span data-ttu-id="4455a-123">U kunt vooraf gedefinieerde installatiekopieën van een groot aantal afbeeldingen kiezen in hello Azure Marketplace en zodat ze beschikbaar zijn in de testomgeving Hallo.</span><span class="sxs-lookup"><span data-stu-id="4455a-123">You can pick ready-made images from a wide variety of images in hello Azure Marketplace and make them available in hello lab.</span></span> <span data-ttu-id="4455a-124">Als Hallo kant-en-afbeeldingen niet aan uw vereisten voldoet, kunt u een aangepaste installatiekopie maken door het maken van een testomgeving met de installatiekopie van een vooraf gedefinieerde vanuit Azure Marketplace, alle Hallo software installeren die u nodig hebt, en opslaan Hallo VM als een aangepaste installatiekopie in de testomgeving Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="4455a-124">If hello ready-made images don't meet your requirements, you can create a custom image by creating a lab VM using a ready-made image from Azure Marketplace, installing all hello software that you need, and saving hello VM as a custom image in hello lab.</span></span>

    <span data-ttu-id="4455a-125">Als u aangepaste installatiekopieën gebruikt, overweeg het gebruik van een installatiekopie factory toocreate en distribueren van uw afbeeldingen.</span><span class="sxs-lookup"><span data-stu-id="4455a-125">If you will be using custom images, consider using an image factory toocreate and distribute your images.</span></span> <span data-ttu-id="4455a-126">De fabrieksinstellingen van een installatiekopie is een configuratie als code-oplossing die regelmatig bouwt en uw geconfigureerde installatiekopieën automatisch distribueert.</span><span class="sxs-lookup"><span data-stu-id="4455a-126">An image factory is a configuration-as-code solution that regularly builds and distributes your configured images automatically.</span></span> <span data-ttu-id="4455a-127">Dit bespaart Hallo tijd die nodig is toomanually Hallo system configureren nadat een virtuele machine is gemaakt met de Hallo OS baseren.</span><span class="sxs-lookup"><span data-stu-id="4455a-127">This saves hello time required toomanually configure hello system after a VM has been created with hello base OS.</span></span>
  
    <span data-ttu-id="4455a-128">Meer informatie door te klikken op koppelingen in de volgende tabel Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="4455a-128">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="4455a-129">Taak</span><span class="sxs-lookup"><span data-stu-id="4455a-129">Task</span></span> | <span data-ttu-id="4455a-130">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="4455a-130">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="4455a-131">Azure Marketplace-installatiekopieën configureren</span><span class="sxs-lookup"><span data-stu-id="4455a-131">Configure Azure Marketplace images</span></span>](devtest-lab-configure-marketplace-images.md) |<span data-ttu-id="4455a-132">Meer informatie over hoe u kunt geaccepteerde Azure Marketplace-installatiekopieën, beschikbaar voor selectie alleen Hallo afbeeldingen die u voor Hallo testers maken.</span><span class="sxs-lookup"><span data-stu-id="4455a-132">Learn how you can whitelist Azure Marketplace images, making available for selection only hello images you want for hello testers.</span></span>|
   | [<span data-ttu-id="4455a-133">Een aangepaste installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="4455a-133">Create a custom image</span></span>](devtest-lab-create-template.md) |<span data-ttu-id="4455a-134">Maak een aangepaste installatiekopie vooraf Hallo door software te installeren u moet zodat testers snel een virtuele machine met behulp van de aangepaste installatiekopie Hallo kunnen maken.</span><span class="sxs-lookup"><span data-stu-id="4455a-134">Create a custom image by pre-installing hello software you need so that testers can quickly create a VM using hello custom image.</span></span>|
   | [<span data-ttu-id="4455a-135">Meer informatie over de installatiekopie-factory</span><span class="sxs-lookup"><span data-stu-id="4455a-135">Learn about image factory</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2017/04/17/video-custom-image-factory-with-azure-devtest-labs/) |<span data-ttu-id="4455a-136">Bekijk een video waarin wordt beschreven hoe tooset boven en een installatiekopie factory gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4455a-136">Watch a video that describes how tooset up and use an image factory.</span></span>|

3. <span data-ttu-id="4455a-137">**Herbruikbare sjablonen maken voor test-machines**</span><span class="sxs-lookup"><span data-stu-id="4455a-137">**Create reusable templates for test machines**</span></span> 
   
    <span data-ttu-id="4455a-138">Een formule in Azure DevTest Labs is dat een lijst met standaardwaarden voor de eigenschap toocreate een virtuele machine gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4455a-138">A formula in Azure DevTest Labs is a list of default property values used toocreate a VM.</span></span> <span data-ttu-id="4455a-139">U kunt een formule in Hallo lab maken door het verzamelen van een installatiekopie van een VM-grootte (een combinatie van CPU en RAM) en een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="4455a-139">You can create a formula in hello lab by picking an image, a VM size (a combination of CPU and RAM), and a virtual network.</span></span> <span data-ttu-id="4455a-140">Elke tester kunt zien Hallo formule in Hallo lab en toocreate een virtuele machine worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4455a-140">Each tester can see hello formula in hello lab and use it toocreate a VM.</span></span> 
   
    <span data-ttu-id="4455a-141">Meer informatie door te klikken op koppelingen in de volgende tabel Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="4455a-141">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="4455a-142">Taak</span><span class="sxs-lookup"><span data-stu-id="4455a-142">Task</span></span> | <span data-ttu-id="4455a-143">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="4455a-143">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="4455a-144">DevTest Labs formules toocreate VM's beheren</span><span class="sxs-lookup"><span data-stu-id="4455a-144">Manage DevTest Labs formulas toocreate VMs</span></span>](devtest-lab-manage-formulas.md) |<span data-ttu-id="4455a-145">Meer informatie over hoe u een formule kunt maken met een installatiekopie van een VM-grootte (combinatie van CPU en RAM) en een virtueel netwerk ophalen.</span><span class="sxs-lookup"><span data-stu-id="4455a-145">Learn how you can create a formula by picking up an image, VM size (combination of CPU and RAM), and a virtual network.</span></span>|

3. <span data-ttu-id="4455a-146">**Multi-VM testomgevingen maken**</span><span class="sxs-lookup"><span data-stu-id="4455a-146">**Create multi-VM test environments**</span></span> 
   
    <span data-ttu-id="4455a-147">U kunt gebruiken van Azure Resource Manager-sjablonen toodefine Hallo-infrastructuur en configuratie van uw Azure-oplossing en herhaaldelijk implementeren die meerdere test-virtuele machines in een consistente status.</span><span class="sxs-lookup"><span data-stu-id="4455a-147">You can use Azure Resource Manager templates toodefine hello infrastructure and configuration of your Azure solution and repeatedly deploy multiple test VMs in a consistent state.</span></span>

    <span data-ttu-id="4455a-148">Azure PaaS-resources in een omgeving met een Resource Manager-sjabloon kunnen worden ingericht en weergegeven in het bijhouden van kosten.</span><span class="sxs-lookup"><span data-stu-id="4455a-148">Azure PaaS resources can be provisioned in an environment from a Resource Manager template and appear in cost tracking.</span></span> <span data-ttu-id="4455a-149">Virtuele machine automatisch afsluiten geldt echter niet tooPaaS resources.</span><span class="sxs-lookup"><span data-stu-id="4455a-149">However, VM auto shutdown does not apply tooPaaS resources.</span></span>

    <span data-ttu-id="4455a-150">Meer informatie door te klikken op koppelingen in de volgende tabel Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="4455a-150">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="4455a-151">Taak</span><span class="sxs-lookup"><span data-stu-id="4455a-151">Task</span></span> | <span data-ttu-id="4455a-152">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="4455a-152">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="4455a-153">Multi-VM-omgevingen en PaaS-resources maken met Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="4455a-153">Create multi-VM environments and PaaS resources with Azure Resource Manager templates</span></span>](devtest-lab-create-environment-from-arm.md) |<span data-ttu-id="4455a-154">Meer informatie over hoe u meerdere virtuele machines in een consistente status kunt implementeren voor uw testomgeving.</span><span class="sxs-lookup"><span data-stu-id="4455a-154">Learn how you can deploy multiple VMs in a consistent state for your test environment.</span></span>|

4. <span data-ttu-id="4455a-155">**Artefacten tooenable flexibele VM aanpassing maken**</span><span class="sxs-lookup"><span data-stu-id="4455a-155">**Create artifacts tooenable flexible VM customization**</span></span>

   <span data-ttu-id="4455a-156">Artefacten zijn gebruikte toodeploy en uw toepassing configureren nadat een virtuele machine is ingericht.</span><span class="sxs-lookup"><span data-stu-id="4455a-156">Artifacts are used toodeploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="4455a-157">Artefacten kunnen het volgende zijn:</span><span class="sxs-lookup"><span data-stu-id="4455a-157">Artifacts can be:</span></span>

   - <span data-ttu-id="4455a-158">Hulpprogramma's die u tooinstall op Hallo VM, zoals agents, Fiddler en Visual Studio wilt.</span><span class="sxs-lookup"><span data-stu-id="4455a-158">Tools that you want tooinstall on hello VM - such as agents, Fiddler, and Visual Studio.</span></span>
   - <span data-ttu-id="4455a-159">Acties die u wilt de toorun op Hallo VM, zoals het klonen van een opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="4455a-159">Actions that you want toorun on hello VM - such as cloning a repo.</span></span>
   - <span data-ttu-id="4455a-160">Toepassingen die u tootest wilt.</span><span class="sxs-lookup"><span data-stu-id="4455a-160">Applications that you want tootest.</span></span>

   <span data-ttu-id="4455a-161">Veel artefacten zijn al beschikbaar out-of-the-box.</span><span class="sxs-lookup"><span data-stu-id="4455a-161">Many artifacts are already available out-of-the-box.</span></span> <span data-ttu-id="4455a-162">Maar als u meer aanpassing voor uw specifieke behoeften wilt, kunt u uw eigen aangepaste artefacten maken.</span><span class="sxs-lookup"><span data-stu-id="4455a-162">But if you want more customization for your specific needs, you can create your own custom artifacts.</span></span>

   <span data-ttu-id="4455a-163">Meer informatie door te klikken op koppelingen in de volgende tabel Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="4455a-163">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="4455a-164">Taak</span><span class="sxs-lookup"><span data-stu-id="4455a-164">Task</span></span> | <span data-ttu-id="4455a-165">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="4455a-165">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="4455a-166">Aangepaste artefacten maken voor uw DevTest Labs VM</span><span class="sxs-lookup"><span data-stu-id="4455a-166">Create custom artifacts for your DevTest Labs VM</span></span>](devtest-lab-artifact-author.md) |<span data-ttu-id="4455a-167">Maak uw eigen aangepaste artefacten voor Hallo virtuele machines in uw testomgeving.</span><span class="sxs-lookup"><span data-stu-id="4455a-167">Create your own custom artifacts for hello virtual machines in your lab.</span></span>|
   | [<span data-ttu-id="4455a-168">Voeg een Git-opslagplaats toostore aangepaste artefacten en Azure Resource Manager-sjablonen voor gebruik in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="4455a-168">Add a Git repository toostore custom artifacts and Azure Resource Manager templates for use in Azure DevTest Labs</span></span>](devtest-lab-add-artifact-repo.md) |<span data-ttu-id="4455a-169">Meer informatie over hoe toostore uw aangepaste artefacten in uw eigen persoonlijke Git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="4455a-169">Learn how toostore your custom artifacts in your own private Git repo.</span></span>|

5. <span data-ttu-id="4455a-170">**Beheer van kosten**</span><span class="sxs-lookup"><span data-stu-id="4455a-170">**Control costs**</span></span>
   
    <span data-ttu-id="4455a-171">Azure DevTest Labs kunt u tooset een beleid Hallo lab toospecify Hallo maximum aantal VM's die kunnen worden gemaakt door een testprogramma in Hallo-testomgeving.</span><span class="sxs-lookup"><span data-stu-id="4455a-171">Azure DevTest Labs allows you tooset a policy in hello lab toospecify hello maximum number of VMs that can be created by a tester in hello lab.</span></span> 
   
    <span data-ttu-id="4455a-172">Als uw testteam heeft een set werkschema en u wilt dat toostop alle Hallo virtuele machines op een bepaald tijdstip Hallo en vervolgens automatisch opnieuw opgestart ze Hallo na dag, kunt u die gemakkelijk door instelling automatisch afsluiten en automatisch starten van beleid in Hallo lab uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="4455a-172">If your test team has a set work schedule and you want toostop all hello VMs at a particular time of hello day and then automatically restart them hello following day, you can easily accomplish that by setting auto-shutdown and auto-start policies in hello lab.</span></span> 
   
    <span data-ttu-id="4455a-173">Ten slotte, als ontwikkeling van apps voltooid is, kunt u verwijderen alle Hallo VM's in één keer een één PowerShell-script uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="4455a-173">Finally, when app development is complete, you can delete all hello VMs at once by running a single PowerShell script.</span></span> 
   
    <span data-ttu-id="4455a-174">Meer informatie door te klikken op koppelingen in de volgende tabel Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="4455a-174">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="4455a-175">Taak</span><span class="sxs-lookup"><span data-stu-id="4455a-175">Task</span></span> | <span data-ttu-id="4455a-176">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="4455a-176">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="4455a-177">Beleid voor lab maken</span><span class="sxs-lookup"><span data-stu-id="4455a-177">Define lab policies</span></span>](devtest-lab-set-lab-policy.md) |<span data-ttu-id="4455a-178">Kosten door het instellen van beleidsregels in Hallo lab te controleren.</span><span class="sxs-lookup"><span data-stu-id="4455a-178">Control costs by setting policies in hello lab.</span></span> |
   | [<span data-ttu-id="4455a-179">Verwijder alle Hallo lab virtuele machines met een PowerShell-script</span><span class="sxs-lookup"><span data-stu-id="4455a-179">Delete all hello lab VMs using a PowerShell script</span></span>](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |<span data-ttu-id="4455a-180">Verwijder alle Hallo labs in één bewerking wanneer de test is voltooid.</span><span class="sxs-lookup"><span data-stu-id="4455a-180">Delete all hello labs in one operation when testing is complete.</span></span>|

1. <span data-ttu-id="4455a-181">**Een virtueel netwerk tooa Lab toevoegen**</span><span class="sxs-lookup"><span data-stu-id="4455a-181">**Add a virtual network tooa Lab**</span></span> 
   
    <span data-ttu-id="4455a-182">DevTest Labs maakt een nieuw virtueel netwerk (VNET) als een lab is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4455a-182">DevTest Labs creates a new virtual network (VNET) whenever a lab is created.</span></span> <span data-ttu-id="4455a-183">Als u uw eigen VNET hebt geconfigureerd: bijvoorbeeld via ExpressRoute of site-naar-site VPN-kunt u instellingen voor dit VNET tooyour lab virtuele netwerk kunt toevoegen, zodat deze beschikbaar is bij het maken van virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="4455a-183">If you have configured your own VNET – for example, by using ExpressRoute or site-to-site VPN – you can add this VNET tooyour lab's virtual network settings so that it is available when creating VMs.</span></span>

    <span data-ttu-id="4455a-184">Er is bovendien een Azure Active Directory domain join artefact beschikbaar die lid van een domein van de tooa VM wanneer Hallo VM wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4455a-184">In addition, there is an Azure Active Directory domain join artifact available that joins a VM tooa domain when hello VM is being created.</span></span> 
   
    <span data-ttu-id="4455a-185">Meer informatie door te klikken op koppelingen in de volgende tabel Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="4455a-185">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="4455a-186">Taak</span><span class="sxs-lookup"><span data-stu-id="4455a-186">Task</span></span> | <span data-ttu-id="4455a-187">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="4455a-187">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="4455a-188">Een virtueel netwerk configureren in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="4455a-188">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md) |<span data-ttu-id="4455a-189">Meer informatie over hoe een virtueel netwerk in Azure DevTest Labs met behulp van tooconfigure hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="4455a-189">Learn how tooconfigure a virtual network in Azure DevTest Labs using hello Azure portal.</span></span>|

6. <span data-ttu-id="4455a-190">**Hallo lab delen met elke tester**</span><span class="sxs-lookup"><span data-stu-id="4455a-190">**Share hello lab with each tester**</span></span>
   
    <span data-ttu-id="4455a-191">Labs zijn rechtstreeks toegankelijk via een koppeling die u met uw testers deelt.</span><span class="sxs-lookup"><span data-stu-id="4455a-191">Labs can be directly accessed using a link that you share with your testers.</span></span> <span data-ttu-id="4455a-192">Ze niet zelfs toohave Azure-account hebt, zolang ze beschikken over een [Microsoft-account](devtest-lab-faq.md#what-is-a-microsoft-account).</span><span class="sxs-lookup"><span data-stu-id="4455a-192">They don't even have toohave an Azure account, as long as they have a [Microsoft account](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span> <span data-ttu-id="4455a-193">Testers zichtbaar niet voor virtuele machines die zijn gemaakt door andere testers.</span><span class="sxs-lookup"><span data-stu-id="4455a-193">Testers cannot see VMs created by other testers.</span></span>  
   
    <span data-ttu-id="4455a-194">Meer informatie door te klikken op koppelingen in de volgende tabel Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="4455a-194">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="4455a-195">Taak</span><span class="sxs-lookup"><span data-stu-id="4455a-195">Task</span></span> | <span data-ttu-id="4455a-196">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="4455a-196">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="4455a-197">Een testprogramma tooa lab toevoegen in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="4455a-197">Add a tester tooa lab in Azure DevTest Labs</span></span>](devtest-lab-add-devtest-user.md) |<span data-ttu-id="4455a-198">Gebruik hello Azure portal tooadd testers tooyour lab.</span><span class="sxs-lookup"><span data-stu-id="4455a-198">Use hello Azure portal tooadd testers tooyour lab.</span></span>|
   | [<span data-ttu-id="4455a-199">Testers toohello testomgeving met een PowerShell-script toevoegen</span><span class="sxs-lookup"><span data-stu-id="4455a-199">Add testers toohello lab using a PowerShell script</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |<span data-ttu-id="4455a-200">Gebruik PowerShell tooautomate testers tooyour lab toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="4455a-200">Use PowerShell tooautomate adding testers tooyour lab.</span></span> |
   | [<span data-ttu-id="4455a-201">Een koppeling toohello lab ophalen</span><span class="sxs-lookup"><span data-stu-id="4455a-201">Get a link toohello lab</span></span>](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |<span data-ttu-id="4455a-202">Meer informatie over hoe testers rechtstreeks toegang tot een lab via een hyperlink.</span><span class="sxs-lookup"><span data-stu-id="4455a-202">Learn how testers can directly access a lab via a hyperlink.</span></span>|

7. <span data-ttu-id="4455a-203">**Lab maken voor meer teams automatiseren**</span><span class="sxs-lookup"><span data-stu-id="4455a-203">**Automate lab creation for more teams**</span></span> 
   
    <span data-ttu-id="4455a-204">U kunt maken van de testomgeving, met inbegrip van aangepaste instellingen door te maken van een Resource Manager-sjabloon en het toocreate identiek labs opnieuw kunt automatiseren.</span><span class="sxs-lookup"><span data-stu-id="4455a-204">You can automate lab creation, including custom settings, by creating a Resource Manager template and using it toocreate identical labs again and again.</span></span> 
   
    <span data-ttu-id="4455a-205">Meer informatie door te klikken op koppelingen in de volgende tabel Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="4455a-205">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="4455a-206">Taak</span><span class="sxs-lookup"><span data-stu-id="4455a-206">Task</span></span> | <span data-ttu-id="4455a-207">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="4455a-207">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="4455a-208">Een lab met een Resource Manager-sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="4455a-208">Create a lab using a Resource Manager template</span></span>](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |<span data-ttu-id="4455a-209">Labs in Azure DevTest Labs met Resource Manager-sjablonen maken.</span><span class="sxs-lookup"><span data-stu-id="4455a-209">Create labs in Azure DevTest Labs using Resource Manager templates.</span></span> |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

