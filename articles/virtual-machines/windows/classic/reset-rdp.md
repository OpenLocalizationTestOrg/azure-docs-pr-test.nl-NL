---
title: aaaReset Hallo wachtwoord of de configuratie van extern bureaublad op een Windows-virtuele machine in Azure | Microsoft Docs
description: Meer informatie over hoe een wachtwoord of extern bureaublad-services op een virtuele machine van Windows die worden gemaakt met behulp van Hallo Classic deployment model met behulp van tooreset hello Azure-portal of Azure PowerShell.
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: iainfou
ms.openlocfilehash: 1721a91fc6c89b46df74e76dfcf918b1c4c77a4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-hello-remote-desktop-service-or-its-login-password-in-a-windows-vm-created-using-hello-classic-deployment-model"></a><span data-ttu-id="5b41e-103">Hoe tooreset Hallo extern bureaublad-service of het aanmeldingswachtwoord op een Windows-VM gemaakt met behulp van Hallo klassieke implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="5b41e-103">How tooreset hello Remote Desktop service or its login password in a Windows VM created using hello Classic deployment model</span></span>
> [!IMPORTANT]
> <span data-ttu-id="5b41e-104">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="5b41e-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="5b41e-105">In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="5b41e-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="5b41e-106">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5b41e-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="5b41e-107">U kunt ook [deze stappen uitvoert voor virtuele machines die zijn gemaakt met Resource Manager-implementatiemodel Hallo](../reset-rdp.md).</span><span class="sxs-lookup"><span data-stu-id="5b41e-107">You can also [perform these steps for VMs created with hello Resource Manager deployment model](../reset-rdp.md).</span></span>

<span data-ttu-id="5b41e-108">Als u geen verbinding maken tooa Windows virtuele machine (VM), kunt u Hallo lokale administrator-wachtwoord opnieuw instellen of opnieuw instellen van Hallo extern bureaublad-serviceconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="5b41e-108">If you can't connect tooa Windows virtual machine (VM), you can reset hello local administrator password or reset hello Remote Desktop service configuration.</span></span> <span data-ttu-id="5b41e-109">U kunt beide hello Azure portal of Hallo toegang van de VM-extensie in Azure PowerShell tooreset Hallo wachtwoord gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5b41e-109">You can use either hello Azure portal or hello VM Access extension in Azure PowerShell tooreset hello password.</span></span>

## <a name="ways-tooreset-configuration-or-credentials"></a><span data-ttu-id="5b41e-110">Manieren tooreset configuratie of referenties</span><span class="sxs-lookup"><span data-stu-id="5b41e-110">Ways tooreset configuration or credentials</span></span>
<span data-ttu-id="5b41e-111">U kunt Extern bureaublad-services en referenties herstellen op verschillende manieren, afhankelijk van uw behoeften:</span><span class="sxs-lookup"><span data-stu-id="5b41e-111">You can reset Remote Desktop services and credentials in a few different ways, depending on your needs:</span></span>

- [<span data-ttu-id="5b41e-112">Opnieuw instellen met hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="5b41e-112">Reset using hello Azure portal</span></span>](#azure-portal)
- [<span data-ttu-id="5b41e-113">Opnieuw instellen met Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b41e-113">Reset using Azure PowerShell</span></span>](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a><span data-ttu-id="5b41e-114">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5b41e-114">Azure portal</span></span>
<span data-ttu-id="5b41e-115">U kunt Hallo [Azure-portal](https://portal.azure.com) tooreset Hallo extern bureaublad-service.</span><span class="sxs-lookup"><span data-stu-id="5b41e-115">You can use hello [Azure portal](https://portal.azure.com) tooreset hello Remote Desktop service.</span></span> <span data-ttu-id="5b41e-116">de voor- en klik op Hallo drie balken in de linkerbovenhoek Hallo tooexpand Hallo portal menu **virtuele machines (klassiek)**:</span><span class="sxs-lookup"><span data-stu-id="5b41e-116">tooexpand hello portal menu, click hello three bars in hello upper left corner and then click **Virtual machines (classic)**:</span></span>

![Blader naar uw Azure VM](./media/reset-rdp/Portal-Select-Classic-VM.png)

<span data-ttu-id="5b41e-118">Selecteer uw Windows-machine en klik op **extern opnieuw instellen...** . hello volgende dialoogvenster wordt weergegeven tooreset Hallo extern bureaublad-configuratie:</span><span class="sxs-lookup"><span data-stu-id="5b41e-118">Select your Windows virtual machine and then click **Reset Remote...**. hello following dialog appears tooreset hello Remote Desktop configuration:</span></span>

![Pagina RDP-configuratie opnieuw instellen](./media/reset-rdp/Portal-RDP-Reset-Windows.png)

<span data-ttu-id="5b41e-120">U kunt ook Hallo gebruikersnaam en wachtwoord van de lokale beheerdersaccount Hallo herstellen.</span><span class="sxs-lookup"><span data-stu-id="5b41e-120">You can also reset hello username and password of hello local administrator account.</span></span> <span data-ttu-id="5b41e-121">Van uw virtuele machine, klikt u op **ondersteuning + probleemoplossing** > **wachtwoord opnieuw instellen**.</span><span class="sxs-lookup"><span data-stu-id="5b41e-121">From your VM, click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="5b41e-122">Hallo wachtwoord opnieuw instellen van blade wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="5b41e-122">hello password reset blade is displayed:</span></span>

![Pagina voor wachtwoordherstel](./media/reset-rdp/Portal-PW-Reset-Windows.png)

<span data-ttu-id="5b41e-124">Nadat u Hallo nieuwe gebruikersnaam en wachtwoord opgeven, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="5b41e-124">After you enter hello new user name and password, click **Save**.</span></span>

## <a name="vmaccess-extension-and-powershell"></a><span data-ttu-id="5b41e-125">VMAccess-extensie en PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b41e-125">VMAccess extension and PowerShell</span></span>
<span data-ttu-id="5b41e-126">Zorg ervoor dat Hallo die VM-Agent is geïnstalleerd op Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="5b41e-126">Make sure hello VM Agent is installed on hello virtual machine.</span></span> <span data-ttu-id="5b41e-127">Hallo VMAccess-extensie nodig niet voor toobe geïnstalleerd voordat u gebruiken kunt, zolang Hallo VM-Agent beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="5b41e-127">hello VMAccess extension doesn't need toobe installed before you can use it, as long as hello VM Agent is available.</span></span> <span data-ttu-id="5b41e-128">Controleer of deze VM-Agent al is geïnstalleerd met behulp van de volgende opdracht Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="5b41e-128">Verify that hello VM Agent is already installed by using hello following command.</span></span> <span data-ttu-id="5b41e-129">(Vervang 'myCloudService' en 'myVM' op Hallo namen van uw cloudservice en de virtuele machine, respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="5b41e-129">(Replace "myCloudService" and "myVM" by hello names of your cloud service and your VM, respectively.</span></span> <span data-ttu-id="5b41e-130">U kunt meer informatie over deze namen door het uitvoeren van `Get-AzureVM` zonder parameters.)</span><span class="sxs-lookup"><span data-stu-id="5b41e-130">You can learn these names by running `Get-AzureVM` without any parameters.)</span></span>

```powershell
$vm = Get-AzureVM -ServiceName "myCloudService" -Name "myVM"
write-host $vm.VM.ProvisionGuestAgent
```

<span data-ttu-id="5b41e-131">Als hello **write-host** opdracht geeft **True**, Hallo VM-Agent is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="5b41e-131">If hello **write-host** command displays **True**, hello VM Agent is installed.</span></span> <span data-ttu-id="5b41e-132">Als deze wordt weergegeven in **False**, Zie Hallo-instructies en een koppeling toohello downloaden in Hallo [VM-Agent en -extensies: Part 2](http://go.microsoft.com/fwlink/p/?linkid=403947&clcid=0x409) Azure blogbericht.</span><span class="sxs-lookup"><span data-stu-id="5b41e-132">If it displays **False**, see hello instructions and a link toohello download in hello [VM Agent and Extensions - Part 2](http://go.microsoft.com/fwlink/p/?linkid=403947&clcid=0x409) Azure blog post.</span></span>

<span data-ttu-id="5b41e-133">Als u met behulp van de portal Hallo Hallo virtuele machine hebt gemaakt, controleert u of `$vm.GetInstance().ProvisionGuestAgent` retourneert **True**.</span><span class="sxs-lookup"><span data-stu-id="5b41e-133">If you created hello virtual machine by using hello portal, check whether `$vm.GetInstance().ProvisionGuestAgent` returns **True**.</span></span> <span data-ttu-id="5b41e-134">Als dat niet het geval is, kunt u dit instellen met behulp van deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="5b41e-134">If not, you can set it by using this command:</span></span>

```powershell
$vm.GetInstance().ProvisionGuestAgent = $true
```

<span data-ttu-id="5b41e-135">Deze opdracht zorgt ervoor dat de volgende fout wanneer u Hallo uitvoert Hallo **Set AzureVMExtension** opdracht in de volgende stappen Hallo: "Inrichten Guest-Agent moet zijn ingeschakeld op Hallo VM-object voordat u de uitbreiding voor IaaS VM-toegang."</span><span class="sxs-lookup"><span data-stu-id="5b41e-135">This command prevents hello following error when you're running hello **Set-AzureVMExtension** command in hello next steps: “Provision Guest Agent must be enabled on hello VM object before setting IaaS VM Access Extension.”</span></span>

### <a name="reset-hello-local-administrator-account-password"></a><span data-ttu-id="5b41e-136">**Hallo beheerderswachtwoord opnieuw instellen**</span><span class="sxs-lookup"><span data-stu-id="5b41e-136">**Reset hello local administrator account password**</span></span>
<span data-ttu-id="5b41e-137">Een referentie aanmelden met huidige lokale beheerder Hallo-accountnaam en een nieuw wachtwoord maken en voer vervolgens Hallo `Set-AzureVMAccessExtension` als volgt.</span><span class="sxs-lookup"><span data-stu-id="5b41e-137">Create a sign-in credential with hello current local administrator account name and a new password, and then run hello `Set-AzureVMAccessExtension` as follows.</span></span>

```powershell
$cred=Get-Credential
Set-AzureVMAccessExtension –vm $vm -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password  | Update-AzureVM
```

<span data-ttu-id="5b41e-138">Als u een andere naam dan de huidige account gebruiken Hallo typt, Hallo VMAccess-extensie wijzigt de naam van de lokale beheerdersaccount Hallo Hallo wachtwoord toothat account wordt toegewezen en problemen met een extern bureaublad afmelding plaatsvindt. Als Hallo lokale administrator-account is uitgeschakeld, schakelt u Hallo VMAccess-extensie deze.</span><span class="sxs-lookup"><span data-stu-id="5b41e-138">If you type a different name than hello current account, hello VMAccess extension renames hello local administrator account, assigns hello password toothat account, and issues a Remote Desktop sign-out. If hello local administrator account is disabled, hello VMAccess extension enables it.</span></span>

<span data-ttu-id="5b41e-139">Deze opdrachten opnieuw ook Hallo extern bureaublad-service configureren.</span><span class="sxs-lookup"><span data-stu-id="5b41e-139">These commands also reset hello Remote Desktop service configuration.</span></span>

### <a name="reset-hello-remote-desktop-service-configuration"></a><span data-ttu-id="5b41e-140">**Hallo extern bureaublad-service-configuratie opnieuw instellen**</span><span class="sxs-lookup"><span data-stu-id="5b41e-140">**Reset hello Remote Desktop service configuration**</span></span>
<span data-ttu-id="5b41e-141">tooreset hello serviceconfiguratie van extern bureaublad, Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="5b41e-141">tooreset hello Remote Desktop service configuration, run hello following command:</span></span>

```powershell
Set-AzureVMAccessExtension –vm $vm | Update-AzureVM
```

<span data-ttu-id="5b41e-142">Hallo VMAccess-extensie twee opdrachten op Hallo virtuele machine wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="5b41e-142">hello VMAccess extension runs two commands on hello virtual machine:</span></span>

```powershell
netsh advfirewall firewall set rule group="Remote Desktop" new enable=Yes
```

<span data-ttu-id="5b41e-143">Met deze opdracht wordt het ingebouwde Windows Firewall groep hello, waarmee binnenkomend verkeer voor extern bureaublad, die gebruikmaakt van TCP-poort 3389.</span><span class="sxs-lookup"><span data-stu-id="5b41e-143">This command enables hello built-in Windows Firewall group that allows incoming Remote Desktop traffic, which uses TCP port 3389.</span></span>

```powershell
Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server' -name "fDenyTSConnections" -Value 0
```

<span data-ttu-id="5b41e-144">Hallo fDenyTSConnections register waarde too0, het inschakelen van extern bureaublad-verbindingen met deze opdracht ingesteld.</span><span class="sxs-lookup"><span data-stu-id="5b41e-144">This command sets hello fDenyTSConnections registry value too0, enabling Remote Desktop connections.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b41e-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5b41e-145">Next steps</span></span>
<span data-ttu-id="5b41e-146">Als uitbreiding van virtuele machine van Azure toegang Hallo niet reageert en u niet kan tooreset Hallo wachtwoord, kunt u [reset Hallo lokale Windows-wachtwoord offline](../reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5b41e-146">If hello Azure VM access extension does not respond and you are unable tooreset hello password, you can [reset hello local Windows password offline](../reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="5b41e-147">Deze methode is een meer geavanceerde proces en moet u tooconnect Hallo virtuele harde schijf van Hallo problematisch VM tooanother VM.</span><span class="sxs-lookup"><span data-stu-id="5b41e-147">This method is a more advanced process and requires you tooconnect hello virtual hard disk of hello problematic VM tooanother VM.</span></span> <span data-ttu-id="5b41e-148">Hallo stappen beschreven in dit artikel eerst en proberen enkel Hallo offline wachtwoord opnieuw instellen van de methode een laatste toevlucht.</span><span class="sxs-lookup"><span data-stu-id="5b41e-148">Follow hello steps documented in this article first, and only attempt hello offline password reset method as a last resort.</span></span>

[<span data-ttu-id="5b41e-149">Azure VM-extensies en functies</span><span class="sxs-lookup"><span data-stu-id="5b41e-149">Azure VM extensions and features</span></span>](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="5b41e-150">Verbinding maken met virtuele machine van Azure tooan met RDP of SSH</span><span class="sxs-lookup"><span data-stu-id="5b41e-150">Connect tooan Azure virtual machine with RDP or SSH</span></span>](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[<span data-ttu-id="5b41e-151">Problemen met extern bureaublad-verbindingen tooa op basis van Windows Azure virtuele machine</span><span class="sxs-lookup"><span data-stu-id="5b41e-151">Troubleshoot Remote Desktop connections tooa Windows-based Azure virtual machine</span></span>](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

