---
title: "aaaAbout installatiekopieën voor virtuele machines van Windows | Microsoft Docs"
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
ms.openlocfilehash: c7cfa1d018a5e99d5b68f559ec9ae1f14e4dec8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="about-images-for-windows-virtual-machines"></a><span data-ttu-id="0e649-103">Over de installatiekopieën voor virtuele machines van Windows</span><span class="sxs-lookup"><span data-stu-id="0e649-103">About images for Windows virtual machines</span></span>
> [!IMPORTANT]
> <span data-ttu-id="0e649-104">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="0e649-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="0e649-105">In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="0e649-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="0e649-106">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0e649-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="0e649-107">Zie voor meer informatie over het vinden en gebruiken van afbeeldingen in het Resource Manager-model Hallo [hier](../../virtual-machines-windows-cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0e649-107">For information about finding and using images in hello Resource Manager model, see [here](../../virtual-machines-windows-cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-about-images](../../../../includes/virtual-machines-common-classic-about-images.md)]

## <a name="working-with-images"></a><span data-ttu-id="0e649-108">Werken met installatiekopieën</span><span class="sxs-lookup"><span data-stu-id="0e649-108">Working with images</span></span>

<span data-ttu-id="0e649-109">U kunt hello Azure PowerShell-module en hello Azure portal toomanage Hallo installatiekopieën beschikbaar tooyour Azure-abonnement gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0e649-109">You can use hello Azure PowerShell module and hello Azure portal toomanage hello images available tooyour Azure subscription.</span></span> <span data-ttu-id="0e649-110">Hello Azure PowerShell-module biedt meer opdrachtopties, zodat u precies wat kan leiden of wilt u toosee doen.</span><span class="sxs-lookup"><span data-stu-id="0e649-110">hello Azure PowerShell module provides more command options, so you can pinpoint exactly what you want toosee or do.</span></span> <span data-ttu-id="0e649-111">Hello Azure-portal biedt een grafische gebruikersinterface voor veel van de dagelijkse beheertaken Hallo.</span><span class="sxs-lookup"><span data-stu-id="0e649-111">hello Azure portal provides a GUI for many of hello everyday administrative tasks.</span></span>

<span data-ttu-id="0e649-112">Hier volgen enkele voorbeelden die gebruikmaken van hello Azure PowerShell-module.</span><span class="sxs-lookup"><span data-stu-id="0e649-112">Here are some examples that use hello Azure PowerShell module.</span></span>

* <span data-ttu-id="0e649-113">**Ophalen van alle installatiekopieën**:`Get-AzureVMImage`retourneert een lijst met alle Hallo installatiekopieën beschikbaar zijn in uw huidige abonnement: uw afbeeldingen en die worden verstrekt door Azure of partners.</span><span class="sxs-lookup"><span data-stu-id="0e649-113">**Get all images**:`Get-AzureVMImage`returns a list of all hello images available in your current subscription: your images and those provided by Azure or partners.</span></span> <span data-ttu-id="0e649-114">de resulterende lijst Hallo kan oplopen.</span><span class="sxs-lookup"><span data-stu-id="0e649-114">hello resulting list could be large.</span></span> <span data-ttu-id="0e649-115">volgende voorbeelden kunt u zien hoe Hallo tooget een kortere lijst.</span><span class="sxs-lookup"><span data-stu-id="0e649-115">hello next examples show how tooget a shorter list.</span></span>
* <span data-ttu-id="0e649-116">**Opvragen van families van de afbeelding**:`Get-AzureVMImage | select ImageFamily` opgehaald van een lijst van families van de installatiekopie door te geven tekenreeksen **ImageFamily** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="0e649-116">**Get image families**:`Get-AzureVMImage | select ImageFamily` gets a list of image families by showing strings **ImageFamily** property.</span></span>
* <span data-ttu-id="0e649-117">**Ophalen van alle afbeeldingen in een specifieke productfamilie**:`Get-AzureVMImage | Where-Object {$_.ImageFamily -eq $family}`</span><span class="sxs-lookup"><span data-stu-id="0e649-117">**Get all images in a specific family**: `Get-AzureVMImage | Where-Object {$_.ImageFamily -eq $family}`</span></span>
* <span data-ttu-id="0e649-118">**VM-installatiekopieën vinden**: `Get-AzureVMImage | where {(gm –InputObject $_ -Name DataDiskConfigurations) -ne $null} | Select -Property Label, ImageName` deze cmdlet werkt met een filter Hallo DataDiskConfiguration eigenschap, die afbeeldingen tooVM is alleen van toepassing.</span><span class="sxs-lookup"><span data-stu-id="0e649-118">**Find VM Images**: `Get-AzureVMImage | where {(gm –InputObject $_ -Name DataDiskConfigurations) -ne $null} | Select -Property Label, ImageName` This cmdlet works by filtering hello DataDiskConfiguration property, which only applies tooVM Images.</span></span> <span data-ttu-id="0e649-119">In dit voorbeeld wordt ook Hallo tooonly Hallo label en image uitvoernaam filtert.</span><span class="sxs-lookup"><span data-stu-id="0e649-119">This example also filters hello output tooonly hello label and image name.</span></span>
* <span data-ttu-id="0e649-120">**Opslaan van een algemene installatiekopie**:`Save-AzureVMImage –ServiceName "myServiceName" –Name "MyVMtoCapture" –OSState "Generalized" –ImageName "MyVmImage" –ImageLabel "This is my generalized image"`</span><span class="sxs-lookup"><span data-stu-id="0e649-120">**Save a generalized image**: `Save-AzureVMImage –ServiceName "myServiceName" –Name "MyVMtoCapture" –OSState "Generalized" –ImageName "MyVmImage" –ImageLabel "This is my generalized image"`</span></span>
* <span data-ttu-id="0e649-121">**Opslaan van de installatiekopie van een gespecialiseerde**:`Save-AzureVMImage –ServiceName "mySvc2" –Name "MyVMToCapture2" –ImageName "myFirstVMImageSP" –OSState "Specialized" -Verbose`</span><span class="sxs-lookup"><span data-stu-id="0e649-121">**Save a specialized image**: `Save-AzureVMImage –ServiceName "mySvc2" –Name "MyVMToCapture2" –ImageName "myFirstVMImageSP" –OSState "Specialized" -Verbose`</span></span>

  > [!TIP]
  > <span data-ttu-id="0e649-122">Hallo OSState parameter is vereist toocreate een VM-installatiekopie die omvat Hallo besturingssysteemschijf en gegevensschijven gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="0e649-122">hello OSState parameter is required toocreate a VM image, which includes hello operating system disk and attached data disks.</span></span> <span data-ttu-id="0e649-123">Als u Hallo-parameter niet gebruikt, maakt het Hallo-cmdlet een installatiekopie van het besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="0e649-123">If you don’t use hello parameter, hello cmdlet creates an OS image.</span></span> <span data-ttu-id="0e649-124">Hallo-waarde van parameter Hallo aangeeft of Hallo-installatiekopie is gegeneraliseerd of speciale, gebaseerd op of de besturingssysteemschijf Hallo is voorbereid voor hergebruik.</span><span class="sxs-lookup"><span data-stu-id="0e649-124">hello value of hello parameter indicates whether hello image is generalized or specialized, based on whether hello operating system disk has been prepared for reuse.</span></span>

* <span data-ttu-id="0e649-125">**Verwijderen van een installatiekopie van een**:`Remove-AzureVMImage –ImageName "MyOldVmImage"`</span><span class="sxs-lookup"><span data-stu-id="0e649-125">**Delete an image**: `Remove-AzureVMImage –ImageName "MyOldVmImage"`</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e649-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0e649-126">Next Steps</span></span>
<span data-ttu-id="0e649-127">U kunt ook [maken van een Windows-machine met behulp van Azure-portal Hallo](tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="0e649-127">You can also [create a Windows machine using hello Azure portal](tutorial.md).</span></span>
