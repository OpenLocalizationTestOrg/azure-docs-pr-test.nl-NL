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
# <a name="passing-credentials-toohello-azure-dsc-extension-handler"></a><span data-ttu-id="327cf-103">Het doorgeven van referenties toohello Azure DSC-uitbreiding handler</span><span class="sxs-lookup"><span data-stu-id="327cf-103">Passing credentials toohello Azure DSC extension handler</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="327cf-104">In dit artikel bevat informatie over Hallo Desired State Configuration-extensie voor Azure.</span><span class="sxs-lookup"><span data-stu-id="327cf-104">This article covers hello Desired State Configuration extension for Azure.</span></span> <span data-ttu-id="327cf-105">Een overzicht van Hallo DSC-uitbreiding handler kan worden gevonden op [inleiding toohello Azure Desired State Configuration extensie handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="327cf-105">An overview of hello DSC extension handler can be found at [Introduction toohello Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

## <a name="passing-in-credentials"></a><span data-ttu-id="327cf-106">Doorgeven van referenties</span><span class="sxs-lookup"><span data-stu-id="327cf-106">Passing in credentials</span></span>
<span data-ttu-id="327cf-107">Als onderdeel van het configuratieproces hello, moet u mogelijk tooset van gebruikersaccounts, toegang tot de services of een programma installeert in een gebruikerscontext.</span><span class="sxs-lookup"><span data-stu-id="327cf-107">As a part of hello configuration process, you may need tooset up user accounts, access services, or install a program in a user context.</span></span> <span data-ttu-id="327cf-108">toodo deze dingen, moet u referenties tooprovide.</span><span class="sxs-lookup"><span data-stu-id="327cf-108">toodo these things, you need tooprovide credentials.</span></span> 

<span data-ttu-id="327cf-109">DSC kunt u met parameters configuraties waarin de referenties zijn doorgegeven in de configuratie van Hallo en veilig opgeslagen in het MOF-bestanden.</span><span class="sxs-lookup"><span data-stu-id="327cf-109">DSC allows for parameterized configurations in which credentials are passed into hello configuration and securely stored in MOF files.</span></span> <span data-ttu-id="327cf-110">Referentiebeheer vereenvoudigt Hello Azure extensie Handler door automatisch beheer van certificaten.</span><span class="sxs-lookup"><span data-stu-id="327cf-110">hello Azure Extension Handler simplifies credential management by providing automatic management of certificates.</span></span> 

<span data-ttu-id="327cf-111">Overweeg de volgende DSC-configuratiescript dat een lokale gebruikersaccount met het opgegeven wachtwoord Hallo maakt Hallo:</span><span class="sxs-lookup"><span data-stu-id="327cf-111">Consider hello following DSC configuration script that creates a local user account with hello specified password:</span></span>

<span data-ttu-id="327cf-112">*user_configuration.ps1*</span><span class="sxs-lookup"><span data-stu-id="327cf-112">*user_configuration.ps1*</span></span>

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

<span data-ttu-id="327cf-113">Het is belangrijk tooinclude *knooppunt localhost* als onderdeel van Hallo-configuratie.</span><span class="sxs-lookup"><span data-stu-id="327cf-113">It is important tooinclude *node localhost* as part of hello configuration.</span></span> <span data-ttu-id="327cf-114">Als deze instructie ontbreekt, werken hello volgende stappen niet als Hallo knooppunt localhost instructie Hallo extensie handler specifiek zoekt.</span><span class="sxs-lookup"><span data-stu-id="327cf-114">If this statement is missing, hello following steps do not work as hello extension handler specifically looks for hello node localhost statement.</span></span> <span data-ttu-id="327cf-115">Het is ook belangrijk tooinclude hello typecast *[PsCredential]*, zoals dit specifieke type Hallo extensie tooencrypt Hallo referentie activeert.</span><span class="sxs-lookup"><span data-stu-id="327cf-115">It is also important tooinclude hello typecast *[PsCredential]*, as this specific type triggers hello extension tooencrypt hello credential.</span></span> 

<span data-ttu-id="327cf-116">Dit script tooblob opslag publiceren:</span><span class="sxs-lookup"><span data-stu-id="327cf-116">Publish this script tooblob storage:</span></span>

`Publish-AzureVMDscConfiguration -ConfigurationPath .\user_configuration.ps1`

<span data-ttu-id="327cf-117">Hello Azure DSC-uitbreiding instellen en Hallo referenties opgeeft:</span><span class="sxs-lookup"><span data-stu-id="327cf-117">Set hello Azure DSC extension and provide hello credential:</span></span>

```
$configurationName = "Main"
$configurationArguments = @{ Credential = Get-Credential }
$configurationArchive = "user_configuration.ps1.zip"
$vm = Get-AzureVM "example-1"

$vm = Set-AzureVMDSCExtension -VM $vm -ConfigurationArchive $configurationArchive 
-ConfigurationName $configurationName -ConfigurationArgument @configurationArguments

$vm | Update-AzureVM
```
## <a name="how-credentials-are-secured"></a><span data-ttu-id="327cf-118">Hoe referenties worden beveiligd</span><span class="sxs-lookup"><span data-stu-id="327cf-118">How credentials are secured</span></span>
<span data-ttu-id="327cf-119">Vraagt u deze code uitvoert om een referentie.</span><span class="sxs-lookup"><span data-stu-id="327cf-119">Running this code prompts for a credential.</span></span> <span data-ttu-id="327cf-120">Zodra deze is opgegeven, wordt opgeslagen in het geheugen kort.</span><span class="sxs-lookup"><span data-stu-id="327cf-120">Once it is provided, it is stored in memory briefly.</span></span> <span data-ttu-id="327cf-121">Wanneer deze wordt gepubliceerd met `Set-AzureVmDscExtension` cmdlet, op het via HTTPS toohello VM wordt verzonden, waarbij Azure opgeslagen op schijf, met Hallo lokale VM certificaat is versleuteld.</span><span class="sxs-lookup"><span data-stu-id="327cf-121">When it is published with `Set-AzureVmDscExtension` cmdlet, it is transmitted over HTTPS toohello VM, where Azure stores it encrypted on disk, using hello local VM certificate.</span></span> <span data-ttu-id="327cf-122">Kort ontsleutelde van geheugen en de opnieuw versleutelde toopass is het tooDSC.</span><span class="sxs-lookup"><span data-stu-id="327cf-122">Then it is briefly decrypted in memory and re-encrypted toopass it tooDSC.</span></span>

<span data-ttu-id="327cf-123">Dit gedrag is anders dan [met behulp van veilige configuraties zonder Hallo extensie handler](https://msdn.microsoft.com/powershell/dsc/securemof).</span><span class="sxs-lookup"><span data-stu-id="327cf-123">This behavior is different than [using secure configurations without hello extension handler](https://msdn.microsoft.com/powershell/dsc/securemof).</span></span> <span data-ttu-id="327cf-124">Hello Azure-omgeving biedt een manier tootransmit configuratiegegevens veilig via certificaten.</span><span class="sxs-lookup"><span data-stu-id="327cf-124">hello Azure environment gives a way tootransmit configuration data securely via certificates.</span></span> <span data-ttu-id="327cf-125">Wanneer u de handler voor Hallo DSC-uitbreiding, er is geen noodzaak tooprovide $CertificatePath of een $CertificateID / $Thumbprint vermelding in ConfigurationData.</span><span class="sxs-lookup"><span data-stu-id="327cf-125">When using hello DSC extension handler, there is no need tooprovide $CertificatePath or a $CertificateID / $Thumbprint entry in ConfigurationData.</span></span>

## <a name="next-steps"></a><span data-ttu-id="327cf-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="327cf-126">Next steps</span></span>
<span data-ttu-id="327cf-127">Zie voor meer informatie over hello Azure DSC-uitbreiding handler [inleiding toohello Azure Desired State Configuration extensie handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="327cf-127">For more information on hello Azure DSC extension handler, see [Introduction toohello Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="327cf-128">Hallo onderzoeken [Azure Resource Manager-sjabloon voor Hallo DSC-uitbreiding](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="327cf-128">Examine hello [Azure Resource Manager template for hello DSC extension](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="327cf-129">Voor meer informatie over PowerShell DSC [gaat u naar de PowerShell-documentatiecentrum hello](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="327cf-129">For more information about PowerShell DSC, [visit hello PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

<span data-ttu-id="327cf-130">toofind aanvullende functionaliteit die u met PowerShell DSC beheren kunt [bladeren Hallo PowerShell gallery](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) voor meer DSC-resources.</span><span class="sxs-lookup"><span data-stu-id="327cf-130">toofind additional functionality you can manage with PowerShell DSC, [browse hello PowerShell gallery](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) for more DSC resources.</span></span>

