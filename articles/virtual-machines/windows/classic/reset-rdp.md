---
title: Opnieuw instellen van het wachtwoord of de configuratie van extern bureaublad op een Windows-virtuele machine in Azure | Microsoft Docs
description: Informatie over het opnieuw instellen van een wachtwoord of extern bureaublad-services op een Windows-virtuele machine gemaakt met behulp van het klassieke implementatiemodel met de Azure-portal of Azure PowerShell.
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
ms.openlocfilehash: 43e5cf1ab3bc3121d7e3915ea0785998e0ee2fc6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-reset-the-remote-desktop-service-or-its-login-password-in-a-windows-vm-created-using-the-classic-deployment-model"></a><span data-ttu-id="9cc7d-103">Het opnieuw instellen van de extern bureaublad-service of het aanmeldingswachtwoord op een Windows-virtuele machine gemaakt met behulp van het klassieke implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="9cc7d-103">How to reset the Remote Desktop service or its login password in a Windows VM created using the Classic deployment model</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9cc7d-104">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="9cc7d-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="9cc7d-105">In dit artikel bevat informatie over met behulp van het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="9cc7d-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="9cc7d-106">U doet er verstandig aan voor de meeste nieuwe implementaties het Resource Manager-model te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9cc7d-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="9cc7d-107">U kunt ook [deze stappen uitvoert voor virtuele machines die zijn gemaakt met het implementatiemodel van Resource Manager](../reset-rdp.md).</span><span class="sxs-lookup"><span data-stu-id="9cc7d-107">You can also [perform these steps for VMs created with the Resource Manager deployment model](../reset-rdp.md).</span></span>

<span data-ttu-id="9cc7d-108">Als u geen verbinding maken met een Windows virtuele machine (VM), kunt u het lokale administrator-wachtwoord opnieuw instellen of opnieuw instellen van de configuratie van de extern bureaublad-service.</span><span class="sxs-lookup"><span data-stu-id="9cc7d-108">If you can't connect to a Windows virtual machine (VM), you can reset the local administrator password or reset the Remote Desktop service configuration.</span></span> <span data-ttu-id="9cc7d-109">U kunt de Azure portal of de toegang van de VM-extensie in Azure PowerShell om het wachtwoord opnieuw in te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9cc7d-109">You can use either the Azure portal or the VM Access extension in Azure PowerShell to reset the password.</span></span>

## <a name="ways-to-reset-configuration-or-credentials"></a><span data-ttu-id="9cc7d-110">Op de beginwaarden configuratie of referenties</span><span class="sxs-lookup"><span data-stu-id="9cc7d-110">Ways to reset configuration or credentials</span></span>
<span data-ttu-id="9cc7d-111">U kunt Extern bureaublad-services en referenties herstellen op verschillende manieren, afhankelijk van uw behoeften:</span><span class="sxs-lookup"><span data-stu-id="9cc7d-111">You can reset Remote Desktop services and credentials in a few different ways, depending on your needs:</span></span>

- [<span data-ttu-id="9cc7d-112">Opnieuw instellen met de Azure-portal</span><span class="sxs-lookup"><span data-stu-id="9cc7d-112">Reset using the Azure portal</span></span>](#azure-portal)
- [<span data-ttu-id="9cc7d-113">Opnieuw instellen met Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9cc7d-113">Reset using Azure PowerShell</span></span>](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a><span data-ttu-id="9cc7d-114">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="9cc7d-114">Azure portal</span></span>
<span data-ttu-id="9cc7d-115">U kunt de [Azure-portal](https://portal.azure.com) opnieuw instellen van de extern bureaublad-service.</span><span class="sxs-lookup"><span data-stu-id="9cc7d-115">You can use the [Azure portal](https://portal.azure.com) to reset the Remote Desktop service.</span></span> <span data-ttu-id="9cc7d-116">Als het menu van de portal wilt uitbreiden, klikt u op de drie balken in de linkerbovenhoek en klik vervolgens op **virtuele machines (klassiek)**:</span><span class="sxs-lookup"><span data-stu-id="9cc7d-116">To expand the portal menu, click the three bars in the upper left corner and then click **Virtual machines (classic)**:</span></span>

![Blader naar uw Azure VM](./media/reset-rdp/Portal-Select-Classic-VM.png)

<span data-ttu-id="9cc7d-118">Selecteer uw Windows-machine en klik op **extern opnieuw instellen...** .</span><span class="sxs-lookup"><span data-stu-id="9cc7d-118">Select your Windows virtual machine and then click **Reset Remote...**.</span></span> <span data-ttu-id="9cc7d-119">Het volgende dialoogvenster wordt weergegeven voor de extern bureaublad-configuratie opnieuw instellen:</span><span class="sxs-lookup"><span data-stu-id="9cc7d-119">The following dialog appears to reset the Remote Desktop configuration:</span></span>

![Pagina RDP-configuratie opnieuw instellen](./media/reset-rdp/Portal-RDP-Reset-Windows.png)

<span data-ttu-id="9cc7d-121">U kunt ook de gebruikersnaam en het wachtwoord van het lokale administrator-account herstellen.</span><span class="sxs-lookup"><span data-stu-id="9cc7d-121">You can also reset the username and password of the local administrator account.</span></span> <span data-ttu-id="9cc7d-122">Van uw virtuele machine, klikt u op **ondersteuning + probleemoplossing** > **wachtwoord opnieuw instellen**.</span><span class="sxs-lookup"><span data-stu-id="9cc7d-122">From your VM, click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="9cc7d-123">De blade van wachtwoord opnieuw instellen wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="9cc7d-123">The password reset blade is displayed:</span></span>

![Pagina voor wachtwoordherstel](./media/reset-rdp/Portal-PW-Reset-Windows.png)

<span data-ttu-id="9cc7d-125">Nadat u de nieuwe gebruikersnaam en het wachtwoord invoert, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="9cc7d-125">After you enter the new user name and password, click **Save**.</span></span>

## <a name="vmaccess-extension-and-powershell"></a><span data-ttu-id="9cc7d-126">VMAccess-extensie en PowerShell</span><span class="sxs-lookup"><span data-stu-id="9cc7d-126">VMAccess extension and PowerShell</span></span>
<span data-ttu-id="9cc7d-127">Zorg ervoor dat de VM-Agent is geïnstalleerd op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="9cc7d-127">Make sure the VM Agent is installed on the virtual machine.</span></span> <span data-ttu-id="9cc7d-128">De VMAccess-extensie hoeft niet te worden geïnstalleerd voordat u gebruiken kunt, zolang de VM-Agent beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="9cc7d-128">The VMAccess extension doesn't need to be installed before you can use it, as long as the VM Agent is available.</span></span> <span data-ttu-id="9cc7d-129">Controleren of de VM-Agent al is geïnstalleerd met behulp van de volgende opdracht.</span><span class="sxs-lookup"><span data-stu-id="9cc7d-129">Verify that the VM Agent is already installed by using the following command.</span></span> <span data-ttu-id="9cc7d-130">(Vervang 'myCloudService' en 'myVM' door de namen van de cloudservice en de virtuele machine, respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="9cc7d-130">(Replace "myCloudService" and "myVM" by the names of your cloud service and your VM, respectively.</span></span> <span data-ttu-id="9cc7d-131">U kunt meer informatie over deze namen door het uitvoeren van `Get-AzureVM` zonder parameters.)</span><span class="sxs-lookup"><span data-stu-id="9cc7d-131">You can learn these names by running `Get-AzureVM` without any parameters.)</span></span>

```powershell
$vm = Get-AzureVM -ServiceName "myCloudService" -Name "myVM"
write-host $vm.VM.ProvisionGuestAgent
```

<span data-ttu-id="9cc7d-132">Als de **write-host** opdracht geeft **True**, de VM-Agent is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="9cc7d-132">If the **write-host** command displays **True**, the VM Agent is installed.</span></span> <span data-ttu-id="9cc7d-133">Als deze wordt weergegeven in **False**, Zie de instructies en een koppeling naar het downloaden van de [VM-Agent en -extensies: Part 2](http://go.microsoft.com/fwlink/p/?linkid=403947&clcid=0x409) Azure blogbericht.</span><span class="sxs-lookup"><span data-stu-id="9cc7d-133">If it displays **False**, see the instructions and a link to the download in the [VM Agent and Extensions - Part 2](http://go.microsoft.com/fwlink/p/?linkid=403947&clcid=0x409) Azure blog post.</span></span>

<span data-ttu-id="9cc7d-134">Als u de virtuele machine met behulp van de portal hebt gemaakt, controleert u of `$vm.GetInstance().ProvisionGuestAgent` retourneert **True**.</span><span class="sxs-lookup"><span data-stu-id="9cc7d-134">If you created the virtual machine by using the portal, check whether `$vm.GetInstance().ProvisionGuestAgent` returns **True**.</span></span> <span data-ttu-id="9cc7d-135">Als dat niet het geval is, kunt u dit instellen met behulp van deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="9cc7d-135">If not, you can set it by using this command:</span></span>

```powershell
$vm.GetInstance().ProvisionGuestAgent = $true
```

<span data-ttu-id="9cc7d-136">Deze opdracht zorgt ervoor dat de volgende fout wanneer u de **Set AzureVMExtension** opdracht in de volgende stappen: "Inrichten Guest-Agent moet zijn ingeschakeld op het VM-object voordat u de uitbreiding voor IaaS VM-toegang."</span><span class="sxs-lookup"><span data-stu-id="9cc7d-136">This command prevents the following error when you're running the **Set-AzureVMExtension** command in the next steps: “Provision Guest Agent must be enabled on the VM object before setting IaaS VM Access Extension.”</span></span>

### <a name="reset-the-local-administrator-account-password"></a><span data-ttu-id="9cc7d-137">**Het lokale beheerderswachtwoord opnieuw instellen**</span><span class="sxs-lookup"><span data-stu-id="9cc7d-137">**Reset the local administrator account password**</span></span>
<span data-ttu-id="9cc7d-138">Een referentie aanmelden met de naam van de huidige lokale administrator-account en een nieuw wachtwoord maken en voer vervolgens de `Set-AzureVMAccessExtension` als volgt.</span><span class="sxs-lookup"><span data-stu-id="9cc7d-138">Create a sign-in credential with the current local administrator account name and a new password, and then run the `Set-AzureVMAccessExtension` as follows.</span></span>

```powershell
$cred=Get-Credential
Set-AzureVMAccessExtension –vm $vm -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password  | Update-AzureVM
```

<span data-ttu-id="9cc7d-139">Als u een andere naam dan de huidige account typt, de VMAccess-extensie wijzigt de naam van het lokale administrator-account, wordt het wachtwoord wordt toegewezen aan dit account, en problemen met een extern bureaublad afmelding plaatsvindt.</span><span class="sxs-lookup"><span data-stu-id="9cc7d-139">If you type a different name than the current account, the VMAccess extension renames the local administrator account, assigns the password to that account, and issues a Remote Desktop sign-out.</span></span> <span data-ttu-id="9cc7d-140">Als het lokale administrator-account is uitgeschakeld, schakelt u de VMAccess-extensie deze.</span><span class="sxs-lookup"><span data-stu-id="9cc7d-140">If the local administrator account is disabled, the VMAccess extension enables it.</span></span>

<span data-ttu-id="9cc7d-141">Deze opdrachten worden ook de configuratie van de extern bureaublad-service opnieuw.</span><span class="sxs-lookup"><span data-stu-id="9cc7d-141">These commands also reset the Remote Desktop service configuration.</span></span>

### <a name="reset-the-remote-desktop-service-configuration"></a><span data-ttu-id="9cc7d-142">**De configuratie van extern bureaublad-service opnieuw instellen**</span><span class="sxs-lookup"><span data-stu-id="9cc7d-142">**Reset the Remote Desktop service configuration**</span></span>
<span data-ttu-id="9cc7d-143">Als u de configuratie van de extern bureaublad-service herstellen, moet u de volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="9cc7d-143">To reset the Remote Desktop service configuration, run the following command:</span></span>

```powershell
Set-AzureVMAccessExtension –vm $vm | Update-AzureVM
```

<span data-ttu-id="9cc7d-144">De VMAccess-extensie twee opdrachten uitgevoerd op de virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="9cc7d-144">The VMAccess extension runs two commands on the virtual machine:</span></span>

```powershell
netsh advfirewall firewall set rule group="Remote Desktop" new enable=Yes
```

<span data-ttu-id="9cc7d-145">Deze opdracht kunt de ingebouwde Windows Firewall-groep waarmee binnenkomend verkeer voor extern bureaublad, die gebruikmaakt van TCP-poort 3389.</span><span class="sxs-lookup"><span data-stu-id="9cc7d-145">This command enables the built-in Windows Firewall group that allows incoming Remote Desktop traffic, which uses TCP port 3389.</span></span>

```powershell
Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server' -name "fDenyTSConnections" -Value 0
```

<span data-ttu-id="9cc7d-146">Met deze opdracht wordt de fDenyTSConnections registerwaarde ingesteld op 0, het inschakelen van extern bureaublad-verbindingen.</span><span class="sxs-lookup"><span data-stu-id="9cc7d-146">This command sets the fDenyTSConnections registry value to 0, enabling Remote Desktop connections.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9cc7d-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9cc7d-147">Next steps</span></span>
<span data-ttu-id="9cc7d-148">Als u de uitbreiding van de toegang tot Azure VM reageert niet en kan het wachtwoord opnieuw instellen, kunt u [opnieuw instellen van het lokale Windows-wachtwoord offline](../reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9cc7d-148">If the Azure VM access extension does not respond and you are unable to reset the password, you can [reset the local Windows password offline](../reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="9cc7d-149">Deze methode is een meer geavanceerde proces en moet u de virtuele harde schijf van de VM is problematisch verbinding met een andere virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="9cc7d-149">This method is a more advanced process and requires you to connect the virtual hard disk of the problematic VM to another VM.</span></span> <span data-ttu-id="9cc7d-150">Volg de stappen beschreven in dit artikel eerst en probeert u alleen de methode offline wachtwoord opnieuw instellen als een laatste toevlucht.</span><span class="sxs-lookup"><span data-stu-id="9cc7d-150">Follow the steps documented in this article first, and only attempt the offline password reset method as a last resort.</span></span>

[<span data-ttu-id="9cc7d-151">Azure VM-extensies en functies</span><span class="sxs-lookup"><span data-stu-id="9cc7d-151">Azure VM extensions and features</span></span>](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="9cc7d-152">Verbinding maken met een virtuele machine van Azure met RDP of SSH</span><span class="sxs-lookup"><span data-stu-id="9cc7d-152">Connect to an Azure virtual machine with RDP or SSH</span></span>](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[<span data-ttu-id="9cc7d-153">Problemen met extern bureaublad-verbindingen met een op basis van Windows Azure virtuele machine</span><span class="sxs-lookup"><span data-stu-id="9cc7d-153">Troubleshoot Remote Desktop connections to a Windows-based Azure virtual machine</span></span>](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

