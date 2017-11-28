---
title: Virtuele-Machineschaalset met Visual Studio aaaDeploy | Microsoft Docs
description: Virtuele-Machineschaalsets met Visual Studio en het Resource Manager-sjabloon implementeren
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ed0786b8-34b2-49a8-85b5-2a628128ead6
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: guybo
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c89a9f2478ccc3d22989aea604a4273bcc46df82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-virtual-machine-scale-set-with-visual-studio"></a><span data-ttu-id="08f23-103">Hoe toocreate een virtuele-Machineschaalset met Visual Studio</span><span class="sxs-lookup"><span data-stu-id="08f23-103">How toocreate a Virtual Machine Scale Set with Visual Studio</span></span>
<span data-ttu-id="08f23-104">Dit artikel laat zien hoe toodeploy een Azure virtuele-Machineschaalset instelt met behulp van een Visual Studio Resource Group-implementatie.</span><span class="sxs-lookup"><span data-stu-id="08f23-104">This article shows you how toodeploy an Azure Virtual Machine Scale Set using a Visual Studio Resource Group Deployment.</span></span>

<span data-ttu-id="08f23-105">[Azure virtuele-Machineschaalsets](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/) is een resource Azure Compute toodeploy en beheren van een verzameling van soortgelijke virtuele machines met automatisch schalen en taakverdeling.</span><span class="sxs-lookup"><span data-stu-id="08f23-105">[Azure Virtual Machine Scale Sets](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/) is an Azure Compute resource toodeploy and manage a collection of similar virtual machines with auto-scale and load balancing.</span></span> <span data-ttu-id="08f23-106">U kunt inrichten en implementeren van virtuele-Machineschaalsets met [Azure Resource Manager-sjablonen](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="08f23-106">You can provision and deploy Virtual Machine Scale Sets using [Azure Resource Manager Templates](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="08f23-107">Azure Resource Manager-sjablonen kunnen worden geïmplementeerd met behulp van de REST van de Azure CLI, PowerShell, en ook rechtstreeks vanuit Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="08f23-107">Azure Resource Manager Templates can be deployed using Azure CLI, PowerShell, REST and also directly from Visual Studio.</span></span> <span data-ttu-id="08f23-108">Visual Studio biedt een set van voorbeeld-sjablonen die kunnen worden geïmplementeerd als onderdeel van een implementatie van Azure Resource Group-project.</span><span class="sxs-lookup"><span data-stu-id="08f23-108">Visual Studio provides a set of example templates, which can be deployed as part of an Azure Resource Group Deployment project.</span></span>

<span data-ttu-id="08f23-109">Azure Resource Group-implementaties zijn een manier toogroup en publiceren van een verzameling Azure gerelateerde resources in een met één implementatiebewerking.</span><span class="sxs-lookup"><span data-stu-id="08f23-109">Azure Resource Group deployments are a way toogroup and publish a set of related Azure resources in a single deployment operation.</span></span> <span data-ttu-id="08f23-110">Voor meer informatie over deze hier: [maken en implementeren van Azure-resourcegroepen met Visual Studio](../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="08f23-110">You can learn more about them here: [Creating and deploying Azure resource groups through Visual Studio](../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="08f23-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="08f23-111">Pre-requisites</span></span>
<span data-ttu-id="08f23-112">tooget gestart met het implementeren van virtuele-Machineschaalsets in Visual Studio, moet u de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="08f23-112">tooget started deploying Virtual Machine Scale Sets in Visual Studio, you need hello following:</span></span>

* <span data-ttu-id="08f23-113">Visual Studio 2013 of hoger</span><span class="sxs-lookup"><span data-stu-id="08f23-113">Visual Studio 2013 or later</span></span>
* <span data-ttu-id="08f23-114">Azure SDK 2.7, 2.8 of 2.9</span><span class="sxs-lookup"><span data-stu-id="08f23-114">Azure SDK 2.7, 2.8 or 2.9</span></span>

>[!NOTE]
><span data-ttu-id="08f23-115">Deze instructies wordt ervan uitgegaan dat u met behulp van Visual Studio met [Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).</span><span class="sxs-lookup"><span data-stu-id="08f23-115">These instructions assume you are using Visual Studio with [Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).</span></span>

## <a name="creating-a-project"></a><span data-ttu-id="08f23-116">Een Project maken</span><span class="sxs-lookup"><span data-stu-id="08f23-116">Creating a Project</span></span>
1. <span data-ttu-id="08f23-117">Maak een nieuw project in Visual Studio door te kiezen **bestand | Nieuwe | Project**.</span><span class="sxs-lookup"><span data-stu-id="08f23-117">Create a new project in Visual Studio by choosing **File | New | Project**.</span></span>
   
    ![Nieuw bestand][file_new]

2. <span data-ttu-id="08f23-119">Onder **Visual C# | Cloud**, kies **Azure Resource Manager** toocreate een project voor het implementeren van een Azure Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="08f23-119">Under **Visual C# | Cloud**, choose **Azure Resource Manager** toocreate a project for deploying an Azure Resource Manager Template.</span></span>
   
    ![Project maken][create_project]

3. <span data-ttu-id="08f23-121">Selecteer Hallo Linux of Windows Scale ingesteld Virtuelemachinesjabloon in Hallo lijst met sjablonen.</span><span class="sxs-lookup"><span data-stu-id="08f23-121">From hello list of Templates, select either hello Linux or Windows Virtual Machine Scale Set Template.</span></span>
   
   ![Sjabloon selecteren][select_Template]

4. <span data-ttu-id="08f23-123">U ziet PowerShell-scripts voor implementatie, een Azure Resource Manager-sjabloon en een parameterbestand voor virtuele-Machineschaalset Hallo wanneer het project is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="08f23-123">Once your project is created you see PowerShell deployment scripts, an Azure Resource Manager Template, and a parameter file for hello Virtual Machine Scale Set.</span></span>
   
    ![Solution Explorer][solution_explorer]

## <a name="customize-your-project"></a><span data-ttu-id="08f23-125">Aanpassen van uw project</span><span class="sxs-lookup"><span data-stu-id="08f23-125">Customize your project</span></span>
<span data-ttu-id="08f23-126">Nu kunt u Hallo sjabloon toocustomize laden voor de behoeften van uw toepassing, zoals VM-extensie-eigenschappen toevoegen of bewerken van regels voor taakverdeling.</span><span class="sxs-lookup"><span data-stu-id="08f23-126">Now you can edit hello Template toocustomize it for your application's needs, such as adding VM extension properties or editing load balancing rules.</span></span> <span data-ttu-id="08f23-127">Hallo Scale ingesteld Virtuelemachinesjablonen zijn standaard geconfigureerde toodeploy hello AzureDiagnostics uitbreiding, waardoor het eenvoudig tooadd automatisch schalen regels.</span><span class="sxs-lookup"><span data-stu-id="08f23-127">By default hello Virtual Machine Scale Set Templates are configured toodeploy hello AzureDiagnostics extension, which makes it easy tooadd autoscale rules.</span></span> <span data-ttu-id="08f23-128">Ook implementeert u een load balancer met een openbaar IP-adres geconfigureerd met binnenkomende NAT-regels.</span><span class="sxs-lookup"><span data-stu-id="08f23-128">It also deploys a load balancer with a public IP address, configured with inbound NAT rules.</span></span> 

<span data-ttu-id="08f23-129">Hallo load balancer kunt u verbinding maken met de VM-instanties toohello met SSH (Linux) of RDP (Windows).</span><span class="sxs-lookup"><span data-stu-id="08f23-129">hello load balancer lets you connect toohello VM instances with SSH (Linux) or RDP (Windows).</span></span> <span data-ttu-id="08f23-130">Hallo front-endpoort bereik begint met 50000.</span><span class="sxs-lookup"><span data-stu-id="08f23-130">hello front-end port range starts at 50000.</span></span> <span data-ttu-id="08f23-131">Voor linux dit betekent dat wanneer u SSH tooport 50000, bent u gerouteerde tooport 22 van Hallo eerste VM in het Hallo-Schaalset.</span><span class="sxs-lookup"><span data-stu-id="08f23-131">For linux this means that if you SSH tooport 50000, you are routed tooport 22 of hello first VM in hello Scale Set.</span></span> <span data-ttu-id="08f23-132">Verbinding maken met tooport 50001 is gerouteerde tooport 22 Hallo tweede VM enzovoort.</span><span class="sxs-lookup"><span data-stu-id="08f23-132">Connecting tooport 50001 is routed tooport 22 of hello second VM and so on.</span></span>

 <span data-ttu-id="08f23-133">Een goede manier tooedit uw sjablonen met Visual Studio is toouse Hallo JSON-overzicht tooorganize Hallo parameters, variabelen en bronnen.</span><span class="sxs-lookup"><span data-stu-id="08f23-133">A good way tooedit your Templates with Visual Studio is toouse hello JSON Outline tooorganize hello parameters, variables, and resources.</span></span> <span data-ttu-id="08f23-134">Met kennis over Hallo kan schema Visual Studio wijzen fouten in uw sjabloon voordat u deze implementeert.</span><span class="sxs-lookup"><span data-stu-id="08f23-134">With an understanding of hello schema Visual Studio can point out errors in your Template before you deploy it.</span></span>

![JSON Explorer][json_explorer]

## <a name="deploy-hello-project"></a><span data-ttu-id="08f23-136">Hallo-project implementeert</span><span class="sxs-lookup"><span data-stu-id="08f23-136">Deploy hello project</span></span>
1. <span data-ttu-id="08f23-137">Implementeer hello Azure Resource Manager-sjabloon toocreate Hallo virtuele-Machineschaalset resource.</span><span class="sxs-lookup"><span data-stu-id="08f23-137">Deploy hello Azure Resource Manager Template toocreate hello Virtual Machine Scale Set resource.</span></span> <span data-ttu-id="08f23-138">Met de rechtermuisknop op het projectknooppunt Hallo en kies **implementeren | Nieuwe implementatie**.</span><span class="sxs-lookup"><span data-stu-id="08f23-138">Right-click on hello project node and choose **Deploy | New Deployment**.</span></span>
   
    ![Sjabloon implementeren][5deploy_Template]
    
2. <span data-ttu-id="08f23-140">Selecteer uw abonnement in Hallo 'Implementeren tooResource groep' dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="08f23-140">Select your subscription in hello “Deploy tooResource Group” dialog.</span></span>
   
    ![Sjabloon implementeren][6deploy_Template]

3. <span data-ttu-id="08f23-142">Hier kunt u een Azure-resourcegroep toodeploy de sjabloon wilt maken.</span><span class="sxs-lookup"><span data-stu-id="08f23-142">From here, you can create an Azure Resource Group toodeploy your Template to.</span></span>
   
    ![Nieuwe resourcegroep][new_resource]

4. <span data-ttu-id="08f23-144">Klik vervolgens op **Parameters bewerken** tooenter-parameters die zijn doorgegeven tooyour sjabloon.</span><span class="sxs-lookup"><span data-stu-id="08f23-144">Next, click **Edit Parameters** tooenter parameters that are passed tooyour Template.</span></span> <span data-ttu-id="08f23-145">Geef Hallo gebruikersnaam en wachtwoord voor Hallo besturingssysteem, die vereist toocreate Hallo-implementatie is.</span><span class="sxs-lookup"><span data-stu-id="08f23-145">Provide hello username and password for hello OS, which is required toocreate hello deployment.</span></span> <span data-ttu-id="08f23-146">Als er geen PowerShell-hulpprogramma's voor Visual Studio is geïnstalleerd, is het raadzaam toocheck **wachtwoorden opslaan** tooavoid een verborgen PowerShell opdrachtregel vragen of gebruik [keyvault ondersteuning](https://azure.microsoft.com/blog/keyvault-support-for-arm-templates/).</span><span class="sxs-lookup"><span data-stu-id="08f23-146">If you don't have PowerShell Tools for Visual Studio installed, it is recommended toocheck **Save passwords** tooavoid a hidden PowerShell command-line prompt, or use [keyvault support](https://azure.microsoft.com/blog/keyvault-support-for-arm-templates/).</span></span>
   
    ![Parameters bewerken][edit_parameters]

5. <span data-ttu-id="08f23-148">Klik nu op **implementeren**.</span><span class="sxs-lookup"><span data-stu-id="08f23-148">Now click **Deploy**.</span></span> <span data-ttu-id="08f23-149">Hallo **uitvoer** venster bevat Hallo implementatie uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="08f23-149">hello **Output** window shows hello deployment progress.</span></span> <span data-ttu-id="08f23-150">Opmerking Hallo actie uitvoeren van Hallo **implementeren AzureResourceGroup.ps1** script.</span><span class="sxs-lookup"><span data-stu-id="08f23-150">Note that hello action is executing hello **Deploy-AzureResourceGroup.ps1** script.</span></span>
   
   ![Venster Output][output_window]

## <a name="exploring-your-virtual-machine-scale-set"></a><span data-ttu-id="08f23-152">De virtuele-Machineschaalset verkennen</span><span class="sxs-lookup"><span data-stu-id="08f23-152">Exploring your Virtual Machine Scale Set</span></span>
<span data-ttu-id="08f23-153">Als het Hallo-implementatie is voltooid, kunt u bekijken Hallo nieuwe virtuele-Machineschaalset in Visual Studio Hallo **Cloud Explorer** (vernieuwen Hallo lijst).</span><span class="sxs-lookup"><span data-stu-id="08f23-153">Once hello deployment completes, you can view hello new Virtual Machine Scale Set in hello Visual Studio **Cloud Explorer** (refresh hello list).</span></span> <span data-ttu-id="08f23-154">Cloud Explorer kunt u Azure-resources in Visual Studio tijdens het ontwikkelen van toepassingen beheren.</span><span class="sxs-lookup"><span data-stu-id="08f23-154">Cloud Explorer lets you manage Azure resources in Visual Studio while developing applications.</span></span> <span data-ttu-id="08f23-155">U kunt ook bekijken uw virtuele-Machineschaalset in Hallo [Azure-portal](https://portal.azure.com) en [Azure Resource Explorer](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="08f23-155">You can also view your Virtual Machine Scale Set in hello [Azure portal](https://portal.azure.com) and [Azure Resource Explorer](https://resources.azure.com/).</span></span>

![Cloud Explorer][cloud_explorer]

 <span data-ttu-id="08f23-157">Hallo-portal biedt de beste manier Hallo toovisually beheren van uw Azure-infrastructuur met een webbrowser, terwijl Azure Resource Explorer biedt een eenvoudige manier tooexplore en fouten opsporen in Azure-resources, geeft een venster in Hallo 'exemplaar weergeven' en ook weer met PowerShell opdrachten voor u bekijkt hello-bronnen.</span><span class="sxs-lookup"><span data-stu-id="08f23-157">hello portal provides hello best way toovisually manage your Azure infrastructure with a web browser, while Azure Resource Explorer provides an easy way tooexplore and debug Azure resources, giving a window into hello "instance view" and also showing PowerShell commands for hello resources you are looking at.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08f23-158">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="08f23-158">Next steps</span></span>
<span data-ttu-id="08f23-159">Als u virtuele-Machineschaalsets met Visual Studio hebt geïmplementeerd, kunt u verder aanpassen uw project toosuit de toepassingsvereisten van uw.</span><span class="sxs-lookup"><span data-stu-id="08f23-159">Once you’ve successfully deployed Virtual Machine Scale Sets through Visual Studio, you can further customize your project toosuit your application requirements.</span></span> <span data-ttu-id="08f23-160">Bijvoorbeeld automatisch schalen configureren door het toevoegen van een **Insights** resource, infrastructuur tooyour sjabloon (zoals zelfstandige virtuele machines) toevoegen of implementeren van toepassingen met behulp van de aangepaste scriptextensie Hallo.</span><span class="sxs-lookup"><span data-stu-id="08f23-160">For example, configure auto-scale by adding an **Insights** resource, adding infrastructure tooyour Template (like standalone VMs), or deploying applications using hello custom script extension.</span></span> <span data-ttu-id="08f23-161">Goed voorbeeld sjablonen kunnen u vinden in Hallo [Azure-Snelstartsjablonen](https://github.com/Azure/azure-quickstart-templates) GitHub-opslagplaats (zoek 'vmss').</span><span class="sxs-lookup"><span data-stu-id="08f23-161">Good example templates can be found in hello [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates) GitHub repository (search for "vmss").</span></span>

[file_new]: ./media/virtual-machine-scale-sets-vs-create/1-FileNew.png
[create_project]: ./media/virtual-machine-scale-sets-vs-create/2-CreateProject.png
[select_Template]: ./media/virtual-machine-scale-sets-vs-create/3b-SelectTemplateLin.png
[solution_explorer]: ./media/virtual-machine-scale-sets-vs-create/4-SolutionExplorer.png
[json_explorer]: ./media/virtual-machine-scale-sets-vs-create/10-JsonExplorer.png
[5deploy_Template]: ./media/virtual-machine-scale-sets-vs-create/5-DeployTemplate.png
[6deploy_Template]: ./media/virtual-machine-scale-sets-vs-create/6-DeployTemplate.png
[new_resource]: ./media/virtual-machine-scale-sets-vs-create/7-NewResourceGroup.png
[edit_parameters]: ./media/virtual-machine-scale-sets-vs-create/8-EditParameter.png
[output_window]: ./media/virtual-machine-scale-sets-vs-create/9-Output.png
[cloud_explorer]: ./media/virtual-machine-scale-sets-vs-create/12-CloudExplorer.png
