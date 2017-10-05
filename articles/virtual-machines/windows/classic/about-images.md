---
title: "Over de installatiekopieën voor virtuele machines van Windows | Microsoft Docs"
description: Meer informatie over hoe afbeeldingen worden gebruikt met Windows virtuele machines in Azure.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 66ff3fab-8e7f-4dff-b8da-ab1c9c9c9af8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: cynthn
ms.openlocfilehash: d421cee0becabdf81d865036d0c98b12b077152b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="about-images-for-windows-virtual-machines"></a><span data-ttu-id="55a3e-103">Over de installatiekopieën voor virtuele machines van Windows</span><span class="sxs-lookup"><span data-stu-id="55a3e-103">About images for Windows virtual machines</span></span>
> [!IMPORTANT]
> <span data-ttu-id="55a3e-104">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="55a3e-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="55a3e-105">In dit artikel bevat informatie over met behulp van het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="55a3e-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="55a3e-106">U doet er verstandig aan voor de meeste nieuwe implementaties het Resource Manager-model te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="55a3e-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="55a3e-107">Zie voor meer informatie over het vinden en gebruiken van afbeeldingen in het Resource Manager-model [hier](../../virtual-machines-windows-cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="55a3e-107">For information about finding and using images in the Resource Manager model, see [here](../../virtual-machines-windows-cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-about-images](../../../../includes/virtual-machines-common-classic-about-images.md)]

## <a name="working-with-images"></a><span data-ttu-id="55a3e-108">Werken met installatiekopieën</span><span class="sxs-lookup"><span data-stu-id="55a3e-108">Working with images</span></span>

<span data-ttu-id="55a3e-109">U kunt de Azure PowerShell-module en de Azure portal gebruiken voor het beheren van de beschikbare installatiekopieën naar uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="55a3e-109">You can use the Azure PowerShell module and the Azure portal to manage the images available to your Azure subscription.</span></span> <span data-ttu-id="55a3e-110">De Azure PowerShell-module biedt meer opdrachtopties, zodat u kunt achterhalen precies wat u wilt bekijken of te doen.</span><span class="sxs-lookup"><span data-stu-id="55a3e-110">The Azure PowerShell module provides more command options, so you can pinpoint exactly what you want to see or do.</span></span> <span data-ttu-id="55a3e-111">De Azure portal biedt een grafische gebruikersinterface voor veel van de dagelijkse beheertaken.</span><span class="sxs-lookup"><span data-stu-id="55a3e-111">The Azure portal provides a GUI for many of the everyday administrative tasks.</span></span>

<span data-ttu-id="55a3e-112">Hier volgen enkele voorbeelden die gebruikmaken van de Azure PowerShell-module.</span><span class="sxs-lookup"><span data-stu-id="55a3e-112">Here are some examples that use the Azure PowerShell module.</span></span>

* <span data-ttu-id="55a3e-113">**Ophalen van alle installatiekopieën**:`Get-AzureVMImage`retourneert een lijst met alle installatiekopieën die beschikbaar zijn in uw huidige abonnement: uw afbeeldingen en die worden verstrekt door Azure of partners.</span><span class="sxs-lookup"><span data-stu-id="55a3e-113">**Get all images**:`Get-AzureVMImage`returns a list of all the images available in your current subscription: your images and those provided by Azure or partners.</span></span> <span data-ttu-id="55a3e-114">De resulterende lijst kan worden grote.</span><span class="sxs-lookup"><span data-stu-id="55a3e-114">The resulting list could be large.</span></span> <span data-ttu-id="55a3e-115">De volgende voorbeelden laten zien hoe een kortere lijst.</span><span class="sxs-lookup"><span data-stu-id="55a3e-115">The next examples show how to get a shorter list.</span></span>
* <span data-ttu-id="55a3e-116">**Opvragen van families van de afbeelding**:`Get-AzureVMImage | select ImageFamily` opgehaald van een lijst van families van de installatiekopie door te geven tekenreeksen **ImageFamily** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="55a3e-116">**Get image families**:`Get-AzureVMImage | select ImageFamily` gets a list of image families by showing strings **ImageFamily** property.</span></span>
* <span data-ttu-id="55a3e-117">**Ophalen van alle afbeeldingen in een specifieke productfamilie**:`Get-AzureVMImage | Where-Object {$_.ImageFamily -eq $family}`</span><span class="sxs-lookup"><span data-stu-id="55a3e-117">**Get all images in a specific family**: `Get-AzureVMImage | Where-Object {$_.ImageFamily -eq $family}`</span></span>
* <span data-ttu-id="55a3e-118">**VM-installatiekopieën vinden**: `Get-AzureVMImage | where {(gm –InputObject $_ -Name DataDiskConfigurations) -ne $null} | Select -Property Label, ImageName` deze cmdlet werkt door het filteren van de eigenschap DataDiskConfiguration, die alleen van toepassing op de VM-installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="55a3e-118">**Find VM Images**: `Get-AzureVMImage | where {(gm –InputObject $_ -Name DataDiskConfigurations) -ne $null} | Select -Property Label, ImageName` This cmdlet works by filtering the DataDiskConfiguration property, which only applies to VM Images.</span></span> <span data-ttu-id="55a3e-119">In dit voorbeeld wordt ook de uitvoer naar alleen de naam label en image filtert.</span><span class="sxs-lookup"><span data-stu-id="55a3e-119">This example also filters the output to only the label and image name.</span></span>
* <span data-ttu-id="55a3e-120">**Opslaan van een algemene installatiekopie**:`Save-AzureVMImage –ServiceName "myServiceName" –Name "MyVMtoCapture" –OSState "Generalized" –ImageName "MyVmImage" –ImageLabel "This is my generalized image"`</span><span class="sxs-lookup"><span data-stu-id="55a3e-120">**Save a generalized image**: `Save-AzureVMImage –ServiceName "myServiceName" –Name "MyVMtoCapture" –OSState "Generalized" –ImageName "MyVmImage" –ImageLabel "This is my generalized image"`</span></span>
* <span data-ttu-id="55a3e-121">**Opslaan van de installatiekopie van een gespecialiseerde**:`Save-AzureVMImage –ServiceName "mySvc2" –Name "MyVMToCapture2" –ImageName "myFirstVMImageSP" –OSState "Specialized" -Verbose`</span><span class="sxs-lookup"><span data-stu-id="55a3e-121">**Save a specialized image**: `Save-AzureVMImage –ServiceName "mySvc2" –Name "MyVMToCapture2" –ImageName "myFirstVMImageSP" –OSState "Specialized" -Verbose`</span></span>

  > [!TIP]
  > <span data-ttu-id="55a3e-122">De parameter OSState is vereist voor het maken van een VM-installatiekopie, dat bestaat uit de besturingssysteemschijf en gegevensschijven gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="55a3e-122">The OSState parameter is required to create a VM image, which includes the operating system disk and attached data disks.</span></span> <span data-ttu-id="55a3e-123">Als u de parameter niet gebruikt, maakt de cmdlet een installatiekopie van het besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="55a3e-123">If you don’t use the parameter, the cmdlet creates an OS image.</span></span> <span data-ttu-id="55a3e-124">De waarde van de parameter aangeeft of de afbeelding is gegeneraliseerd of speciale, gebaseerd op of de schijf van het besturingssysteem is voorbereid voor hergebruik.</span><span class="sxs-lookup"><span data-stu-id="55a3e-124">The value of the parameter indicates whether the image is generalized or specialized, based on whether the operating system disk has been prepared for reuse.</span></span>

* <span data-ttu-id="55a3e-125">**Verwijderen van een installatiekopie van een**:`Remove-AzureVMImage –ImageName "MyOldVmImage"`</span><span class="sxs-lookup"><span data-stu-id="55a3e-125">**Delete an image**: `Remove-AzureVMImage –ImageName "MyOldVmImage"`</span></span>

## <a name="next-steps"></a><span data-ttu-id="55a3e-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="55a3e-126">Next Steps</span></span>
<span data-ttu-id="55a3e-127">U kunt ook [maken van een Windows-machine met de Azure portal](tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="55a3e-127">You can also [create a Windows machine using the Azure portal](tutorial.md).</span></span>
