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
# <a name="how-tooreset-hello-remote-desktop-service-or-its-login-password-in-a-windows-vm-created-using-hello-classic-deployment-model"></a>Hoe tooreset Hallo extern bureaublad-service of het aanmeldingswachtwoord op een Windows-VM gemaakt met behulp van Hallo klassieke implementatiemodel
> [!IMPORTANT]
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en classic](../../../resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken. U kunt ook [deze stappen uitvoert voor virtuele machines die zijn gemaakt met Resource Manager-implementatiemodel Hallo](../reset-rdp.md).

Als u geen verbinding maken tooa Windows virtuele machine (VM), kunt u Hallo lokale administrator-wachtwoord opnieuw instellen of opnieuw instellen van Hallo extern bureaublad-serviceconfiguratie. U kunt beide hello Azure portal of Hallo toegang van de VM-extensie in Azure PowerShell tooreset Hallo wachtwoord gebruiken.

## <a name="ways-tooreset-configuration-or-credentials"></a>Manieren tooreset configuratie of referenties
U kunt Extern bureaublad-services en referenties herstellen op verschillende manieren, afhankelijk van uw behoeften:

- [Opnieuw instellen met hello Azure-portal](#azure-portal)
- [Opnieuw instellen met Azure PowerShell](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a>Azure Portal
U kunt Hallo [Azure-portal](https://portal.azure.com) tooreset Hallo extern bureaublad-service. de voor- en klik op Hallo drie balken in de linkerbovenhoek Hallo tooexpand Hallo portal menu **virtuele machines (klassiek)**:

![Blader naar uw Azure VM](./media/reset-rdp/Portal-Select-Classic-VM.png)

Selecteer uw Windows-machine en klik op **extern opnieuw instellen...** . hello volgende dialoogvenster wordt weergegeven tooreset Hallo extern bureaublad-configuratie:

![Pagina RDP-configuratie opnieuw instellen](./media/reset-rdp/Portal-RDP-Reset-Windows.png)

U kunt ook Hallo gebruikersnaam en wachtwoord van de lokale beheerdersaccount Hallo herstellen. Van uw virtuele machine, klikt u op **ondersteuning + probleemoplossing** > **wachtwoord opnieuw instellen**. Hallo wachtwoord opnieuw instellen van blade wordt weergegeven:

![Pagina voor wachtwoordherstel](./media/reset-rdp/Portal-PW-Reset-Windows.png)

Nadat u Hallo nieuwe gebruikersnaam en wachtwoord opgeven, klikt u op **opslaan**.

## <a name="vmaccess-extension-and-powershell"></a>VMAccess-extensie en PowerShell
Zorg ervoor dat Hallo die VM-Agent is geïnstalleerd op Hallo virtuele machine. Hallo VMAccess-extensie nodig niet voor toobe geïnstalleerd voordat u gebruiken kunt, zolang Hallo VM-Agent beschikbaar is. Controleer of deze VM-Agent al is geïnstalleerd met behulp van de volgende opdracht Hallo Hallo. (Vervang 'myCloudService' en 'myVM' op Hallo namen van uw cloudservice en de virtuele machine, respectievelijk. U kunt meer informatie over deze namen door het uitvoeren van `Get-AzureVM` zonder parameters.)

```powershell
$vm = Get-AzureVM -ServiceName "myCloudService" -Name "myVM"
write-host $vm.VM.ProvisionGuestAgent
```

Als hello **write-host** opdracht geeft **True**, Hallo VM-Agent is geïnstalleerd. Als deze wordt weergegeven in **False**, Zie Hallo-instructies en een koppeling toohello downloaden in Hallo [VM-Agent en -extensies: Part 2](http://go.microsoft.com/fwlink/p/?linkid=403947&clcid=0x409) Azure blogbericht.

Als u met behulp van de portal Hallo Hallo virtuele machine hebt gemaakt, controleert u of `$vm.GetInstance().ProvisionGuestAgent` retourneert **True**. Als dat niet het geval is, kunt u dit instellen met behulp van deze opdracht:

```powershell
$vm.GetInstance().ProvisionGuestAgent = $true
```

Deze opdracht zorgt ervoor dat de volgende fout wanneer u Hallo uitvoert Hallo **Set AzureVMExtension** opdracht in de volgende stappen Hallo: "Inrichten Guest-Agent moet zijn ingeschakeld op Hallo VM-object voordat u de uitbreiding voor IaaS VM-toegang."

### <a name="reset-hello-local-administrator-account-password"></a>**Hallo beheerderswachtwoord opnieuw instellen**
Een referentie aanmelden met huidige lokale beheerder Hallo-accountnaam en een nieuw wachtwoord maken en voer vervolgens Hallo `Set-AzureVMAccessExtension` als volgt.

```powershell
$cred=Get-Credential
Set-AzureVMAccessExtension –vm $vm -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password  | Update-AzureVM
```

Als u een andere naam dan de huidige account gebruiken Hallo typt, Hallo VMAccess-extensie wijzigt de naam van de lokale beheerdersaccount Hallo Hallo wachtwoord toothat account wordt toegewezen en problemen met een extern bureaublad afmelding plaatsvindt. Als Hallo lokale administrator-account is uitgeschakeld, schakelt u Hallo VMAccess-extensie deze.

Deze opdrachten opnieuw ook Hallo extern bureaublad-service configureren.

### <a name="reset-hello-remote-desktop-service-configuration"></a>**Hallo extern bureaublad-service-configuratie opnieuw instellen**
tooreset hello serviceconfiguratie van extern bureaublad, Hallo volgende opdracht uitvoeren:

```powershell
Set-AzureVMAccessExtension –vm $vm | Update-AzureVM
```

Hallo VMAccess-extensie twee opdrachten op Hallo virtuele machine wordt uitgevoerd:

```powershell
netsh advfirewall firewall set rule group="Remote Desktop" new enable=Yes
```

Met deze opdracht wordt het ingebouwde Windows Firewall groep hello, waarmee binnenkomend verkeer voor extern bureaublad, die gebruikmaakt van TCP-poort 3389.

```powershell
Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server' -name "fDenyTSConnections" -Value 0
```

Hallo fDenyTSConnections register waarde too0, het inschakelen van extern bureaublad-verbindingen met deze opdracht ingesteld.

## <a name="next-steps"></a>Volgende stappen
Als uitbreiding van virtuele machine van Azure toegang Hallo niet reageert en u niet kan tooreset Hallo wachtwoord, kunt u [reset Hallo lokale Windows-wachtwoord offline](../reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Deze methode is een meer geavanceerde proces en moet u tooconnect Hallo virtuele harde schijf van Hallo problematisch VM tooanother VM. Hallo stappen beschreven in dit artikel eerst en proberen enkel Hallo offline wachtwoord opnieuw instellen van de methode een laatste toevlucht.

[Azure VM-extensies en functies](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[Verbinding maken met virtuele machine van Azure tooan met RDP of SSH](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[Problemen met extern bureaublad-verbindingen tooa op basis van Windows Azure virtuele machine](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

