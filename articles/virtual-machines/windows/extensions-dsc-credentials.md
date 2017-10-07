---
title: aaaPassing referenties tooAzure gebruik van DSC | Microsoft Docs
description: Overzicht van de veilig doorgeven van referenties tooAzure virtuele machines met behulp van PowerShell Desired State Configuration
services: virtual-machines-windows
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: ea76b7e8-b576-445a-8107-88ea2f3876b9
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 09/15/2016
ms.author: zachal
ms.openlocfilehash: 306ecd3fd481f49a0beca5052fc7531a52999330
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="passing-credentials-toohello-azure-dsc-extension-handler"></a>Het doorgeven van referenties toohello Azure DSC-uitbreiding handler
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

In dit artikel bevat informatie over Hallo Desired State Configuration-extensie voor Azure. Een overzicht van Hallo DSC-uitbreiding handler kan worden gevonden op [inleiding toohello Azure Desired State Configuration extensie handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

## <a name="passing-in-credentials"></a>Doorgeven van referenties
Als onderdeel van het configuratieproces hello, moet u mogelijk tooset van gebruikersaccounts, toegang tot de services of een programma installeert in een gebruikerscontext. toodo deze dingen, moet u referenties tooprovide. 

DSC kunt u met parameters configuraties waarin de referenties zijn doorgegeven in de configuratie van Hallo en veilig opgeslagen in het MOF-bestanden. Referentiebeheer vereenvoudigt Hello Azure extensie Handler door automatisch beheer van certificaten. 

Overweeg de volgende DSC-configuratiescript dat een lokale gebruikersaccount met het opgegeven wachtwoord Hallo maakt Hallo:

*user_configuration.ps1*

```
configuration Main
{
    param(
        [Parameter(Mandatory=$true)]
        [ValidateNotNullorEmpty()]
        [PSCredential]
        $Credential
    )    
    Node localhost {       
        User LocalUserAccount
        {
            Username = $Credential.UserName
            Password = $Credential
            Disabled = $false
            Ensure = "Present"
            FullName = "Local User Account"
            Description = "Local User Account"
            PasswordNeverExpires = $true
        } 
    }  
} 
```

Het is belangrijk tooinclude *knooppunt localhost* als onderdeel van Hallo-configuratie. Als deze instructie ontbreekt, werken hello volgende stappen niet als Hallo knooppunt localhost instructie Hallo extensie handler specifiek zoekt. Het is ook belangrijk tooinclude hello typecast *[PsCredential]*, zoals dit specifieke type Hallo extensie tooencrypt Hallo referentie activeert. 

Dit script tooblob opslag publiceren:

`Publish-AzureVMDscConfiguration -ConfigurationPath .\user_configuration.ps1`

Hello Azure DSC-uitbreiding instellen en Hallo referenties opgeeft:

```
$configurationName = "Main"
$configurationArguments = @{ Credential = Get-Credential }
$configurationArchive = "user_configuration.ps1.zip"
$vm = Get-AzureVM "example-1"

$vm = Set-AzureVMDSCExtension -VM $vm -ConfigurationArchive $configurationArchive 
-ConfigurationName $configurationName -ConfigurationArgument @configurationArguments

$vm | Update-AzureVM
```
## <a name="how-credentials-are-secured"></a>Hoe referenties worden beveiligd
Vraagt u deze code uitvoert om een referentie. Zodra deze is opgegeven, wordt opgeslagen in het geheugen kort. Wanneer deze wordt gepubliceerd met `Set-AzureVmDscExtension` cmdlet, op het via HTTPS toohello VM wordt verzonden, waarbij Azure opgeslagen op schijf, met Hallo lokale VM certificaat is versleuteld. Kort ontsleutelde van geheugen en de opnieuw versleutelde toopass is het tooDSC.

Dit gedrag is anders dan [met behulp van veilige configuraties zonder Hallo extensie handler](https://msdn.microsoft.com/powershell/dsc/securemof). Hello Azure-omgeving biedt een manier tootransmit configuratiegegevens veilig via certificaten. Wanneer u de handler voor Hallo DSC-uitbreiding, er is geen noodzaak tooprovide $CertificatePath of een $CertificateID / $Thumbprint vermelding in ConfigurationData.

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over hello Azure DSC-uitbreiding handler [inleiding toohello Azure Desired State Configuration extensie handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Hallo onderzoeken [Azure Resource Manager-sjabloon voor Hallo DSC-uitbreiding](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Voor meer informatie over PowerShell DSC [gaat u naar de PowerShell-documentatiecentrum hello](https://msdn.microsoft.com/powershell/dsc/overview). 

toofind aanvullende functionaliteit die u met PowerShell DSC beheren kunt [bladeren Hallo PowerShell gallery](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) voor meer DSC-resources.

