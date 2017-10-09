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
# <a name="create-a-custom-image-from-a-vhd-file-using-powershell"></a>Een aangepaste installatiekopie maken van een VHD-bestand met behulp van PowerShell

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a>Stapsgewijze instructies

Hallo volgende stappen maakt u een aangepaste installatiekopie van een VHD-bestand met behulp van PowerShell maken:

1. Bij een PowerShell-prompt aanmelden tooyour Azure-account met de volgende aanroep toohello Hallo **Login-AzureRmAccount** cmdlet.  
    
    ```PowerShell
    Login-AzureRmAccount
    ```

1.  Selecteer hello Azure-abonnement door de aanroepende Hallo gewenst **Select-AzureRmSubscription** cmdlet. Vervangen van de volgende tijdelijke aanduiding voor Hallo Hallo **$subscriptionId** variabele met een geldige Azure-abonnement-ID. 

    ```PowerShell
    $subscriptionId = '<Specify your subscription ID here>'
    Select-AzureRmSubscription -SubscriptionId $subscriptionId
    ```

1.  Hallo lab object ophalen door de aanroepende Hallo **Get-AzureRmResource** cmdlet. Vervangen van de volgende tijdelijke aanduidingen voor Hallo Hallo **$labRg** en **$labName** variabelen met Hallo waarden voor uw omgeving nodig. 

    ```PowerShell
    $labRg = '<Specify your lab resource group name here>'
    $labName = '<Specify your lab name here>'
    $lab = Get-AzureRmResource -ResourceId ('/subscriptions/' + $subscriptionId + '/resourceGroups/' + $labRg + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    ```
 
1.  Ophalen Hallo lab-opslagaccount en lab-opslagaccount sleutelwaarden van Hallo lab-object. 

    ```PowerShell
    $labStorageAccount = Get-AzureRmResource -ResourceId $lab.Properties.defaultStorageAccount 
    $labStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $labStorageAccount.ResourceGroupName -Name $labStorageAccount.ResourceName)[0].Value
    ```

1.  Vervangen van de volgende tijdelijke aanduiding voor Hallo Hallo **$vhdUri** variabele Hello URI tooyour geüpload VHD-bestand. Hallo VHD-bestand van URI kunt u krijgen via Hallo storage-account van blob-blade in hello Azure-portal.

    ```PowerShell
    $vhdUri = '<Specify hello VHD URI here>'
    ```

1.  Hallo aangepaste installatiekopie met behulp van Hallo maken **New-AzureRmResourceGroupDeployment** cmdlet. Vervangen van de volgende tijdelijke aanduidingen voor Hallo Hallo **$customImageName** en **$customImageDescription** variabelen toomeaningful namen voor uw omgeving.

    ```PowerShell
    $customImageName = '<Specify hello custom image name>'
    $customImageDescription = '<Specify hello custom image description>'

    $parameters = @{existingLabName="$($lab.Name)"; existingVhdUri=$vhdUri; imageOsType='windows'; isVhdSysPrepped=$false; imageName=$customImageName; imageDescription=$customImageDescription}

    New-AzureRmResourceGroupDeployment -ResourceGroupName $lab.ResourceGroupName -Name CreateCustomImage -TemplateUri 'https://raw.githubusercontent.com/Azure/azure-devtestlab/master/Samples/201-dtl-create-customimage-from-vhd/azuredeploy.json' -TemplateParameterObject $parameters
    ```

## <a name="powershell-script-toocreate-a-custom-image-from-a-vhd-file"></a>PowerShell-script toocreate een aangepaste installatiekopie van een VHD-bestand

Hallo volgende PowerShell-script kan worden gebruikt toocreate een aangepaste installatiekopie van een VHD-bestand. Hallo tijdelijke aanduidingen (vanaf en eindigend met punthaken) vervangen door de juiste waarden Hallo voor uw behoeften. 

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

## <a name="related-blog-posts"></a>Verwante blogberichten

- [Aangepaste installatiekopieën of formules?](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [Kopiëren van aangepaste installatiekopieën tussen Azure DevTest Labs](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a>Volgende stappen

- [Een VM tooyour lab toevoegen](./devtest-lab-add-vm-with-artifacts.md)
