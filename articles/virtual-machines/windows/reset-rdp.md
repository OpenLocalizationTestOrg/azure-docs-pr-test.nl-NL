---
title: aaaReset wachtwoord of de configuratie van extern bureaublad op een virtuele machine van Windows hello | Microsoft Docs
description: Meer informatie over hoe tooreset wachtwoord van een account of extern bureaublad-services over het gebruik van een virtuele machine van Windows hello Azure-portal of Azure PowerShell.
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 45c69812-d3e4-48de-a98d-39a0f5675777
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 5258df7196621f0adb50debd08dd248922a966de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-hello-remote-desktop-service-or-its-login-password-in-a-windows-vm"></a><span data-ttu-id="f7c73-103">Hoe tooreset Hallo extern bureaublad-service of het aanmeldingswachtwoord op een Windows-VM</span><span class="sxs-lookup"><span data-stu-id="f7c73-103">How tooreset hello Remote Desktop service or its login password in a Windows VM</span></span>
<span data-ttu-id="f7c73-104">Als u geen verbinding maken tooa Windows virtuele machine (VM), kunt u Hallo lokale administrator-wachtwoord opnieuw instellen of opnieuw instellen van Hallo extern bureaublad-serviceconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="f7c73-104">If you can't connect tooa Windows virtual machine (VM), you can reset hello local administrator password or reset hello Remote Desktop service configuration.</span></span> <span data-ttu-id="f7c73-105">U kunt beide hello Azure portal of Hallo toegang van de VM-extensie in Azure PowerShell tooreset Hallo wachtwoord gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f7c73-105">You can use either hello Azure portal or hello VM Access extension in Azure PowerShell tooreset hello password.</span></span> <span data-ttu-id="f7c73-106">Als u PowerShell gebruikt, zorg ervoor dat er Hallo [nieuwste PowerShell-module geïnstalleerd en geconfigureerd](/powershell/azure/overview) en tooyour Azure-abonnement bent aangemeld.</span><span class="sxs-lookup"><span data-stu-id="f7c73-106">If you are using PowerShell, make sure that you have hello [latest PowerShell module installed and configured](/powershell/azure/overview) and are signed in tooyour Azure subscription.</span></span> <span data-ttu-id="f7c73-107">U kunt ook [deze stappen uitvoert voor virtuele machines die zijn gemaakt met de klassieke implementatiemodel Hallo](reset-rdp.md).</span><span class="sxs-lookup"><span data-stu-id="f7c73-107">You can also [perform these steps for VMs created with hello Classic deployment model](reset-rdp.md).</span></span>

## <a name="ways-tooreset-configuration-or-credentials"></a><span data-ttu-id="f7c73-108">Manieren tooreset configuratie of referenties</span><span class="sxs-lookup"><span data-stu-id="f7c73-108">Ways tooreset configuration or credentials</span></span>
<span data-ttu-id="f7c73-109">U kunt Extern bureaublad-services en referenties herstellen op verschillende manieren, afhankelijk van uw behoeften:</span><span class="sxs-lookup"><span data-stu-id="f7c73-109">You can reset Remote Desktop services and credentials in a few different ways, depending on your needs:</span></span>

- [<span data-ttu-id="f7c73-110">Opnieuw instellen met hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="f7c73-110">Reset using hello Azure portal</span></span>](#azure-portal)
- [<span data-ttu-id="f7c73-111">Opnieuw instellen met Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f7c73-111">Reset using Azure PowerShell</span></span>](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a><span data-ttu-id="f7c73-112">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f7c73-112">Azure portal</span></span>
<span data-ttu-id="f7c73-113">de voor- en klik op Hallo drie balken in de linkerbovenhoek Hallo tooexpand Hallo portal menu **virtuele machines**:</span><span class="sxs-lookup"><span data-stu-id="f7c73-113">tooexpand hello portal menu, click hello three bars in hello upper left corner and then click **Virtual machines**:</span></span>

![Blader naar uw Azure VM](./media/reset-rdp/Portal-Select-VM.png)

### <a name="reset-hello-local-administrator-account-password"></a><span data-ttu-id="f7c73-115">**Hallo beheerderswachtwoord opnieuw instellen**</span><span class="sxs-lookup"><span data-stu-id="f7c73-115">**Reset hello local administrator account password**</span></span>

<span data-ttu-id="f7c73-116">Selecteer uw Windows-machine en klik vervolgens op **ondersteuning + probleemoplossing** > **wachtwoord opnieuw instellen**.</span><span class="sxs-lookup"><span data-stu-id="f7c73-116">Select your Windows virtual machine then click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="f7c73-117">Hallo wachtwoord opnieuw instellen van blade wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="f7c73-117">hello password reset blade is displayed:</span></span>

![Pagina voor wachtwoordherstel](./media/reset-rdp/Portal-RM-PW-Reset-Windows.png)

<span data-ttu-id="f7c73-119">Hallo-gebruikersnaam en een nieuw wachtwoord invoeren en klik vervolgens op **Update**.</span><span class="sxs-lookup"><span data-stu-id="f7c73-119">Enter hello username and a new password, then click **Update**.</span></span> <span data-ttu-id="f7c73-120">Probeer opnieuw verbinding te maken tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="f7c73-120">Try connecting tooyour VM again.</span></span>

### <a name="reset-hello-remote-desktop-service-configuration"></a><span data-ttu-id="f7c73-121">**Hallo extern bureaublad-service-configuratie opnieuw instellen**</span><span class="sxs-lookup"><span data-stu-id="f7c73-121">**Reset hello Remote Desktop service configuration**</span></span>

<span data-ttu-id="f7c73-122">Selecteer uw Windows-machine en klik vervolgens op **ondersteuning + probleemoplossing** > **wachtwoord opnieuw instellen**.</span><span class="sxs-lookup"><span data-stu-id="f7c73-122">Select your Windows virtual machine then click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="f7c73-123">Hallo wachtwoord opnieuw instellen van blade wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f7c73-123">hello password reset blade is displayed.</span></span> 

![RDP-configuratie opnieuw instellen](./media/reset-rdp/Portal-RM-RDP-Reset.png)

<span data-ttu-id="f7c73-125">Selecteer **alleen opnieuw instellen van configuratie** uit de vervolgkeuzelijst hello, klik vervolgens op **Update**.</span><span class="sxs-lookup"><span data-stu-id="f7c73-125">Select **Reset configuration only** from hello drop-down menu, then click **Update**.</span></span> <span data-ttu-id="f7c73-126">Probeer opnieuw verbinding te maken tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="f7c73-126">Try connecting tooyour VM again.</span></span>


## <a name="vmaccess-extension-and-powershell"></a><span data-ttu-id="f7c73-127">VMAccess-extensie en PowerShell</span><span class="sxs-lookup"><span data-stu-id="f7c73-127">VMAccess extension and PowerShell</span></span>
<span data-ttu-id="f7c73-128">Zorg ervoor dat u Hallo hebt [nieuwste PowerShell-module geïnstalleerd en geconfigureerd](/powershell/azure/overview) en zijn ondertekend in Azure-abonnement met Hallo tooyour `Login-AzureRmAccount` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f7c73-128">Make sure that you have hello [latest PowerShell module installed and configured](/powershell/azure/overview) and are signed in tooyour Azure subscription with hello `Login-AzureRmAccount` cmdlet.</span></span>

### <a name="reset-hello-local-administrator-account-password"></a><span data-ttu-id="f7c73-129">**Hallo beheerderswachtwoord opnieuw instellen**</span><span class="sxs-lookup"><span data-stu-id="f7c73-129">**Reset hello local administrator account password**</span></span>
<span data-ttu-id="f7c73-130">Opnieuw instellen van Hallo wachtwoord of gebruikersnaam beheerdersnaam Hello [Set AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f7c73-130">Reset hello administrator password or user name with hello [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet.</span></span> <span data-ttu-id="f7c73-131">Hiermee maakt u referenties voor uw account als volgt:</span><span class="sxs-lookup"><span data-stu-id="f7c73-131">Create your account credentials as follows:</span></span>

```powershell
$cred=Get-Credential
```

> [!NOTE] 
> <span data-ttu-id="f7c73-132">Als u een andere naam dan de huidige lokale administrator-account Hallo typt op de virtuele machine, Hallo VMAccess-extensie wijzigt de naam van de lokale beheerdersaccount Hallo wijst uw toothat-account opgegeven wachtwoord en problemen met een extern bureaublad-en afmelden-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="f7c73-132">If you type a different name than hello current local administrator account on your VM, hello VMAccess extension renames hello local administrator account, assigns your specified password toothat account, and issues a Remote Desktop logoff event.</span></span> <span data-ttu-id="f7c73-133">Als Hallo lokale beheerdersaccount op de virtuele machine is uitgeschakeld, schakelt u Hallo VMAccess-extensie deze.</span><span class="sxs-lookup"><span data-stu-id="f7c73-133">If hello local administrator account on your VM is disabled, hello VMAccess extension enables it.</span></span>

<span data-ttu-id="f7c73-134">Voorbeeld van updates na Hallo Hallo VM met de naam `myVM` in Hallo resourcegroep met de naam `myResourceGroup` toohello referenties die zijn opgegeven.</span><span class="sxs-lookup"><span data-stu-id="f7c73-134">hello following example updates hello VM named `myVM` in hello resource group named `myResourceGroup` toohello credentials specified.</span></span>

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

### <a name="reset-hello-remote-desktop-service-configuration"></a><span data-ttu-id="f7c73-135">**Hallo extern bureaublad-service-configuratie opnieuw instellen**</span><span class="sxs-lookup"><span data-stu-id="f7c73-135">**Reset hello Remote Desktop service configuration**</span></span>
<span data-ttu-id="f7c73-136">Opnieuw instellen van externe toegang tooyour VM Hello [Set AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f7c73-136">Reset remote access tooyour VM with hello [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet.</span></span> <span data-ttu-id="f7c73-137">Hallo volgende voorbeeld wordt een extensie van Hallo toegang met de naam `myVMAccess` op Hallo VM met de naam `myVM` in Hallo `myResourceGroup` resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="f7c73-137">hello following example resets hello access extension named `myVMAccess` on hello VM named `myVM` in hello `myResourceGroup` resource group:</span></span>

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResoureGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -typeHandlerVersion "2.0" -ForceRerun
```

> [!TIP]
> <span data-ttu-id="f7c73-138">Een virtuele machine kan slechts één virtuele machine toegang agent hebben op elk gewenst moment.</span><span class="sxs-lookup"><span data-stu-id="f7c73-138">At any point, a VM can have only a single VM access agent.</span></span> <span data-ttu-id="f7c73-139">tooset hello VM toegang agent-eigenschappen, Hallo `-ForceRerun` optie kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f7c73-139">tooset hello VM access agent properties successfully, hello `-ForceRerun` option can be used.</span></span> <span data-ttu-id="f7c73-140">Wanneer u `-ForceRerun`, zorg ervoor dat toouse Hallo dezelfde naam voor Hallo VM toegang agent zoals gebruikt in alle vorige opdrachten.</span><span class="sxs-lookup"><span data-stu-id="f7c73-140">When using `-ForceRerun`, make sure toouse hello same name for hello VM access agent as used in any previous commands.</span></span>

<span data-ttu-id="f7c73-141">Als u nog steeds geen verbinding op afstand tooyour virtuele machine maken, raadpleegt u meer stappen tootry op [problemen met extern bureaublad-verbindingen tooa op basis van Windows Azure virtuele machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f7c73-141">If you still can't connect remotely tooyour virtual machine, see more steps tootry at [Troubleshoot Remote Desktop connections tooa Windows-based Azure virtual machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


## <a name="next-steps"></a><span data-ttu-id="f7c73-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f7c73-142">Next steps</span></span>
<span data-ttu-id="f7c73-143">Als uitbreiding van virtuele machine van Azure toegang Hallo niet reageert en u niet kan tooreset Hallo wachtwoord, kunt u [reset Hallo lokale Windows-wachtwoord offline](reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f7c73-143">If hello Azure VM access extension does not respond and you are unable tooreset hello password, you can [reset hello local Windows password offline](reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="f7c73-144">Deze methode is een meer geavanceerde proces en moet u tooconnect Hallo virtuele harde schijf van Hallo problematisch VM tooanother VM.</span><span class="sxs-lookup"><span data-stu-id="f7c73-144">This method is a more advanced process and requires you tooconnect hello virtual hard disk of hello problematic VM tooanother VM.</span></span> <span data-ttu-id="f7c73-145">Hallo stappen beschreven in dit artikel eerst en proberen enkel Hallo offline wachtwoord opnieuw instellen van de methode een laatste toevlucht.</span><span class="sxs-lookup"><span data-stu-id="f7c73-145">Follow hello steps documented in this article first, and only attempt hello offline password reset method as a last resort.</span></span>

[<span data-ttu-id="f7c73-146">Azure VM-extensies en functies</span><span class="sxs-lookup"><span data-stu-id="f7c73-146">Azure VM extensions and features</span></span>](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="f7c73-147">Verbinding maken met virtuele machine van Azure tooan met RDP of SSH</span><span class="sxs-lookup"><span data-stu-id="f7c73-147">Connect tooan Azure virtual machine with RDP or SSH</span></span>](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[<span data-ttu-id="f7c73-148">Problemen met extern bureaublad-verbindingen tooa op basis van Windows Azure virtuele machine</span><span class="sxs-lookup"><span data-stu-id="f7c73-148">Troubleshoot Remote Desktop connections tooa Windows-based Azure virtual machine</span></span>](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

