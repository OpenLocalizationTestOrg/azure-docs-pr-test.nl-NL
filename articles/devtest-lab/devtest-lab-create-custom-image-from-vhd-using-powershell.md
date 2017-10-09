---
title: de aangepaste installatiekopie van een Azure DevTest Labs vanaf een VHD-bestand met behulp van PowerShell aaaCreate | Microsoft Docs
description: Het maken van een aangepaste installatiekopie in Azure DevTest Labs van een VHD-bestand met behulp van PowerShell automatiseren
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 39b4005fa46cdf86cf0800ca376128134bcfb650
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vhd-file-using-powershell"></a><span data-ttu-id="f33a6-103">Een aangepaste installatiekopie maken van een VHD-bestand met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="f33a6-103">Create a custom image from a VHD file using PowerShell</span></span>

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="f33a6-104">Stapsgewijze instructies</span><span class="sxs-lookup"><span data-stu-id="f33a6-104">Step-by-step instructions</span></span>

<span data-ttu-id="f33a6-105">Hallo volgende stappen maakt u een aangepaste installatiekopie van een VHD-bestand met behulp van PowerShell maken:</span><span class="sxs-lookup"><span data-stu-id="f33a6-105">hello following steps walk you through creating a custom image from a VHD file using PowerShell:</span></span>

1. <span data-ttu-id="f33a6-106">Bij een PowerShell-prompt aanmelden tooyour Azure-account met de volgende aanroep toohello Hallo **Login-AzureRmAccount** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f33a6-106">At a PowerShell prompt, log in tooyour Azure account with hello following call toohello **Login-AzureRmAccount** cmdlet.</span></span>  
    
    ```PowerShell
    Login-AzureRmAccount
    ```

1.  <span data-ttu-id="f33a6-107">Selecteer hello Azure-abonnement door de aanroepende Hallo gewenst **Select-AzureRmSubscription** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f33a6-107">Select hello desired Azure subscription by calling hello **Select-AzureRmSubscription** cmdlet.</span></span> <span data-ttu-id="f33a6-108">Vervangen van de volgende tijdelijke aanduiding voor Hallo Hallo **$subscriptionId** variabele met een geldige Azure-abonnement-ID.</span><span class="sxs-lookup"><span data-stu-id="f33a6-108">Replace hello following placeholder for hello **$subscriptionId** variable with a valid Azure subscription ID.</span></span> 

    ```PowerShell
    $subscriptionId = '<Specify your subscription ID here>'
    Select-AzureRmSubscription -SubscriptionId $subscriptionId
    ```

1.  <span data-ttu-id="f33a6-109">Hallo lab object ophalen door de aanroepende Hallo **Get-AzureRmResource** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f33a6-109">Get hello lab object by calling hello **Get-AzureRmResource** cmdlet.</span></span> <span data-ttu-id="f33a6-110">Vervangen van de volgende tijdelijke aanduidingen voor Hallo Hallo **$labRg** en **$labName** variabelen met Hallo waarden voor uw omgeving nodig.</span><span class="sxs-lookup"><span data-stu-id="f33a6-110">Replace hello following placeholders for hello **$labRg** and **$labName** variables with hello appropriate values for your environment.</span></span> 

    ```PowerShell
    $labRg = '<Specify your lab resource group name here>'
    $labName = '<Specify your lab name here>'
    $lab = Get-AzureRmResource -ResourceId ('/subscriptions/' + $subscriptionId + '/resourceGroups/' + $labRg + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    ```
 
1.  <span data-ttu-id="f33a6-111">Ophalen Hallo lab-opslagaccount en lab-opslagaccount sleutelwaarden van Hallo lab-object.</span><span class="sxs-lookup"><span data-stu-id="f33a6-111">Get hello lab storage account and lab storage account key values from hello lab object.</span></span> 

    ```PowerShell
    $labStorageAccount = Get-AzureRmResource -ResourceId $lab.Properties.defaultStorageAccount 
    $labStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $labStorageAccount.ResourceGroupName -Name $labStorageAccount.ResourceName)[0].Value
    ```

1.  <span data-ttu-id="f33a6-112">Vervangen van de volgende tijdelijke aanduiding voor Hallo Hallo **$vhdUri** variabele Hello URI tooyour geüpload VHD-bestand.</span><span class="sxs-lookup"><span data-stu-id="f33a6-112">Replace hello following placeholder for hello **$vhdUri** variable with hello URI tooyour uploaded VHD file.</span></span> <span data-ttu-id="f33a6-113">Hallo VHD-bestand van URI kunt u krijgen via Hallo storage-account van blob-blade in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f33a6-113">You can get hello VHD file's URI from hello storage account's blob blade in hello Azure portal.</span></span>

    ```PowerShell
    $vhdUri = '<Specify hello VHD URI here>'
    ```

1.  <span data-ttu-id="f33a6-114">Hallo aangepaste installatiekopie met behulp van Hallo maken **New-AzureRmResourceGroupDeployment** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f33a6-114">Create hello custom image using hello **New-AzureRmResourceGroupDeployment** cmdlet.</span></span> <span data-ttu-id="f33a6-115">Vervangen van de volgende tijdelijke aanduidingen voor Hallo Hallo **$customImageName** en **$customImageDescription** variabelen toomeaningful namen voor uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="f33a6-115">Replace hello following placeholders for hello **$customImageName** and **$customImageDescription** variables toomeaningful names for your environment.</span></span>

    ```PowerShell
    $customImageName = '<Specify hello custom image name>'
    $customImageDescription = '<Specify hello custom image description>'

    $parameters = @{existingLabName="$($lab.Name)"; existingVhdUri=$vhdUri; imageOsType='windows'; isVhdSysPrepped=$false; imageName=$customImageName; imageDescription=$customImageDescription}

    New-AzureRmResourceGroupDeployment -ResourceGroupName $lab.ResourceGroupName -Name CreateCustomImage -TemplateUri 'https://raw.githubusercontent.com/Azure/azure-devtestlab/master/Samples/201-dtl-create-customimage-from-vhd/azuredeploy.json' -TemplateParameterObject $parameters
    ```

## <a name="powershell-script-toocreate-a-custom-image-from-a-vhd-file"></a><span data-ttu-id="f33a6-116">PowerShell-script toocreate een aangepaste installatiekopie van een VHD-bestand</span><span class="sxs-lookup"><span data-stu-id="f33a6-116">PowerShell script toocreate a custom image from a VHD file</span></span>

<span data-ttu-id="f33a6-117">Hallo volgende PowerShell-script kan worden gebruikt toocreate een aangepaste installatiekopie van een VHD-bestand.</span><span class="sxs-lookup"><span data-stu-id="f33a6-117">hello following PowerShell script can be used toocreate a custom image from a VHD file.</span></span> <span data-ttu-id="f33a6-118">Hallo tijdelijke aanduidingen (vanaf en eindigend met punthaken) vervangen door de juiste waarden Hallo voor uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="f33a6-118">Replace hello placeholders (starting and ending with angle brackets) with hello appropriate values for your needs.</span></span> 

```PowerShell
# Log in tooyour Azure account.  
Login-AzureRmAccount

# Select hello desired Azure subscription. 
$subscriptionId = '<Specify your subscription ID here>'
Select-AzureRmSubscription -SubscriptionId $subscriptionId

# Get hello lab object.
$labRg = '<Specify your lab resource group name here>'
$labName = '<Specify your lab name here>'
$lab = Get-AzureRmResource -ResourceId ('/subscriptions/' + $subscriptionId + '/resourceGroups/' + $labRg + '/providers/Microsoft.DevTestLab/labs/' + $labName)

# Get hello lab storage account and lab storage account key values.
$labStorageAccount = Get-AzureRmResource -ResourceId $lab.Properties.defaultStorageAccount 
$labStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $labStorageAccount.ResourceGroupName -Name $labStorageAccount.ResourceName)[0].Value

# Set hello URI of hello VHD file.  
$vhdUri = '<Specify hello VHD URI here>'

# Set hello custom image name and description values.
$customImageName = '<Specify hello custom image name>'
$customImageDescription = '<Specify hello custom image description>'

# Set up hello parameters object.
$parameters = @{existingLabName="$($lab.Name)"; existingVhdUri=$vhdUri; imageOsType='windows'; isVhdSysPrepped=$false; imageName=$customImageName; imageDescription=$customImageDescription}

# Create hello custom image. 
New-AzureRmResourceGroupDeployment -ResourceGroupName $lab.ResourceGroupName -Name CreateCustomImage -TemplateUri 'https://raw.githubusercontent.com/Azure/azure-devtestlab/master/Samples/201-dtl-create-customimage-from-vhd/azuredeploy.json' -TemplateParameterObject $parameters
```

## <a name="related-blog-posts"></a><span data-ttu-id="f33a6-119">Verwante blogberichten</span><span class="sxs-lookup"><span data-stu-id="f33a6-119">Related blog posts</span></span>

- [<span data-ttu-id="f33a6-120">Aangepaste installatiekopieën of formules?</span><span class="sxs-lookup"><span data-stu-id="f33a6-120">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="f33a6-121">Kopiëren van aangepaste installatiekopieën tussen Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="f33a6-121">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="f33a6-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f33a6-122">Next steps</span></span>

- [<span data-ttu-id="f33a6-123">Een VM tooyour lab toevoegen</span><span class="sxs-lookup"><span data-stu-id="f33a6-123">Add a VM tooyour lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
