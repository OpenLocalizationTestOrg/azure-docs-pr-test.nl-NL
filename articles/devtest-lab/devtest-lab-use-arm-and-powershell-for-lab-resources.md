---
title: Maken of wijzigen van automatisch in PowerShell met Azure Resource Manager-sjablonen labs | Microsoft Docs
description: Informatie over het gebruik van Azure Resource Manager-sjablonen met PowerShell maken of wijzigen van labs automatisch in een DevTest lab
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: dad9944c-0b20-48be-ba80-8f4aa0950903
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/21/2017
ms.author: tarcher
ms.openlocfilehash: cea4531175df2cc39790497dc049d27e23ffa0c6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-or-modify-labs-automatically-using-azure-resource-manager-templates-and-powershell"></a><span data-ttu-id="b3fd1-103">Maken of wijzigen van labs automatisch met Azure Resource Manager-sjablonen en PowerShell</span><span class="sxs-lookup"><span data-stu-id="b3fd1-103">Create or modify labs automatically using Azure Resource Manager templates and PowerShell</span></span>

<span data-ttu-id="b3fd1-104">DevTest Labs biedt tal van sjablonen voor Azure Resource Manager en PowerShell-scripts die kunnen helpen u snel en automatisch maken van nieuwe labs of wijzig bestaande labs en vervolgens implementeert deze resources.</span><span class="sxs-lookup"><span data-stu-id="b3fd1-104">DevTest Labs provides many Azure Resource Manager templates and PowerShell scripts that can help you quickly and automatically create new labs or modify existing labs and then deploy these resources.</span></span>

<span data-ttu-id="b3fd1-105">In dit artikel begeleidt u bij het proces van het gebruik van deze sjablonen en scripts voor het maken, wijzigen en implementeren van uw labs automatiseren.</span><span class="sxs-lookup"><span data-stu-id="b3fd1-105">This article helps guide you through the process of using these templates and scripts to automate the creation, modification, and deployment of your labs.</span></span> <span data-ttu-id="b3fd1-106">In dit artikel ziet u ook waar u meer informatie over het gebruik van PowerShell enkele veelvoorkomende taken uitvoeren in DevTest Labs kan vinden.</span><span class="sxs-lookup"><span data-stu-id="b3fd1-106">This article also shows you where you can find more information about how to use PowerShell to perform some common tasks in DevTest Labs.</span></span>

## <a name="step-1-gather-your-templates-and-scripts"></a><span data-ttu-id="b3fd1-107">Stap 1: Uw sjablonen en scripts verzamelen</span><span class="sxs-lookup"><span data-stu-id="b3fd1-107">Step 1: Gather your templates and scripts</span></span>
<span data-ttu-id="b3fd1-108">U kunt vinden en-klare [Azure Resource Manager-sjablonen](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates) en [PowerShell-scripts](https://github.com/Azure/azure-devtestlab/tree/master/Scripts) op onze openbare [Github-opslagplaats](https://github.com/Azure/azure-devtestlab).</span><span class="sxs-lookup"><span data-stu-id="b3fd1-108">You can find pre-made [Azure Resource Manager templates](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates) and [PowerShell scripts](https://github.com/Azure/azure-devtestlab/tree/master/Scripts) at our public [Github repository](https://github.com/Azure/azure-devtestlab).</span></span> <span data-ttu-id="b3fd1-109">Gebruik deze als-is, of pas ze aan uw behoeften en op te slaan in uw eigen [persoonlijke Git-opslagplaats](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="b3fd1-109">Use them as-is, or customize them for your needs and store them in your own [private Git repo](devtest-lab-add-artifact-repo.md).</span></span> 

## <a name="step-2-modify-your-azure-resource-manager-template"></a><span data-ttu-id="b3fd1-110">Stap 2: Uw Azure Resource Manager-sjabloon wijzigen</span><span class="sxs-lookup"><span data-stu-id="b3fd1-110">Step 2: Modify your Azure Resource Manager template</span></span>
<span data-ttu-id="b3fd1-111">U kunt de stappen op [maken van uw eerste Azure Resource Manager-sjabloon](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-create-first-template) als u een sjabloon voordat nooit hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b3fd1-111">You can follow the steps at [Create your first Azure Resource Manager template](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-create-first-template) if you have never created a template before.</span></span>

<span data-ttu-id="b3fd1-112">Bovendien [aanbevolen procedures voor het maken van Azure Resource Manager-sjablonen](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices) biedt veel richtlijnen en suggesties voor het maken van Azure Resource Manager-sjablonen die zijn betrouwbaar en eenvoudig te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b3fd1-112">In addition, [Best practices for creating Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices) offers many guidelines and suggestions to help you create Azure Resource Manager templates that are reliable and easy to use.</span></span> <span data-ttu-id="b3fd1-113">U wordt normaal gesproken gebruik een variant van een van de wijze van aanpak of voorbeelden en wijzigen van de sjabloon voor uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="b3fd1-113">Typically, you will use a variation of one of the approaches or examples provided and modify your template for your needs.</span></span>

## <a name="step-3-deploy-resources-with-powershell"></a><span data-ttu-id="b3fd1-114">Stap 3: Implementatie van resources met PowerShell</span><span class="sxs-lookup"><span data-stu-id="b3fd1-114">Step 3: Deploy resources with PowerShell</span></span>
<span data-ttu-id="b3fd1-115">Nadat u uw sjablonen en scripts hebt aangepast, volg de stappen die nodig zijn voor [implementeren van resources met Resource Manager-sjablonen en Azure PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span><span class="sxs-lookup"><span data-stu-id="b3fd1-115">After you have customized your templates and scripts, follow the steps necessary to [deploy resources with Resource Manager templates and Azure PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span></span> <span data-ttu-id="b3fd1-116">Het artikel bevat algemene informatie over het implementeren van uw resources in Azure met Azure PowerShell met Azure Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="b3fd1-116">The article provides general information about using Azure PowerShell with Azure Resource Manager templates to deploy your resources to Azure.</span></span>


## <a name="common-tasks-you-can-perform-in-devtest-labs-using-powershell"></a><span data-ttu-id="b3fd1-117">Algemene taken die u kunt uitvoeren in DevTest labs met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="b3fd1-117">Common tasks you can perform in DevTest labs using PowerShell</span></span>
<span data-ttu-id="b3fd1-118">Er zijn veel andere veelvoorkomende taken die u automatiseren kunt met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b3fd1-118">There are many other common tasks that you can automate by using PowerShell.</span></span> <span data-ttu-id="b3fd1-119">De volgende secties van de documentatie worden de stappen die nodig zijn om uit te voeren deze taken.</span><span class="sxs-lookup"><span data-stu-id="b3fd1-119">The following sections of the documentation outline the steps required to perform these tasks.</span></span>

* [<span data-ttu-id="b3fd1-120">Een aangepaste installatiekopie maken van een VHD-bestand met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="b3fd1-120">Create a custom image from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)
* [<span data-ttu-id="b3fd1-121">VHD-bestand uploaden naar het lab-opslagaccount met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="b3fd1-121">Upload VHD file to lab's storage account using PowerShell</span></span>](devtest-lab-upload-vhd-using-powershell.md)
* [<span data-ttu-id="b3fd1-122">Een externe gebruiker toevoegen aan een testomgeving met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="b3fd1-122">Add an external user to a lab using PowerShell</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell)
* [<span data-ttu-id="b3fd1-123">Maakt een lab aangepaste rol met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="b3fd1-123">Create a lab custom role using PowerShell</span></span>](devtest-lab-grant-user-permissions-to-specific-lab-policies.md#creating-a-lab-custom-role-using-powershell)

### <a name="next-steps"></a><span data-ttu-id="b3fd1-124">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b3fd1-124">Next steps</span></span>
* <span data-ttu-id="b3fd1-125">Meer informatie over het maken van een [persoonlijke Git-opslagplaats](devtest-lab-add-artifact-repo.md) waar u uw aangepaste sjablonen of scripts wilt opslaan.</span><span class="sxs-lookup"><span data-stu-id="b3fd1-125">Learn how to create a [private Git repository](devtest-lab-add-artifact-repo.md) where you will store your customized templates or scripts.</span></span>
* <span data-ttu-id="b3fd1-126">Verken de [Azure Resource Manager-sjablonen uit Azure sjabloon snelstartgalerie](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="b3fd1-126">Explore the [Azure Resource Manager templates from Azure Quickstart template gallery](https://github.com/Azure/azure-quickstart-templates).</span></span>
