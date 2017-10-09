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
# <a name="how-tooreset-hello-remote-desktop-service-or-its-login-password-in-a-windows-vm"></a>Hoe tooreset Hallo extern bureaublad-service of het aanmeldingswachtwoord op een Windows-VM
Als u geen verbinding maken tooa Windows virtuele machine (VM), kunt u Hallo lokale administrator-wachtwoord opnieuw instellen of opnieuw instellen van Hallo extern bureaublad-serviceconfiguratie. U kunt beide hello Azure portal of Hallo toegang van de VM-extensie in Azure PowerShell tooreset Hallo wachtwoord gebruiken. Als u PowerShell gebruikt, zorg ervoor dat er Hallo [nieuwste PowerShell-module geïnstalleerd en geconfigureerd](/powershell/azure/overview) en tooyour Azure-abonnement bent aangemeld. U kunt ook [deze stappen uitvoert voor virtuele machines die zijn gemaakt met de klassieke implementatiemodel Hallo](reset-rdp.md).

## <a name="ways-tooreset-configuration-or-credentials"></a>Manieren tooreset configuratie of referenties
U kunt Extern bureaublad-services en referenties herstellen op verschillende manieren, afhankelijk van uw behoeften:

- [Opnieuw instellen met hello Azure-portal](#azure-portal)
- [Opnieuw instellen met Azure PowerShell](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a>Azure Portal
de voor- en klik op Hallo drie balken in de linkerbovenhoek Hallo tooexpand Hallo portal menu **virtuele machines**:

![Blader naar uw Azure VM](./media/reset-rdp/Portal-Select-VM.png)

### <a name="reset-hello-local-administrator-account-password"></a>**Hallo beheerderswachtwoord opnieuw instellen**

Selecteer uw Windows-machine en klik vervolgens op **ondersteuning + probleemoplossing** > **wachtwoord opnieuw instellen**. Hallo wachtwoord opnieuw instellen van blade wordt weergegeven:

![Pagina voor wachtwoordherstel](./media/reset-rdp/Portal-RM-PW-Reset-Windows.png)

Hallo-gebruikersnaam en een nieuw wachtwoord invoeren en klik vervolgens op **Update**. Probeer opnieuw verbinding te maken tooyour VM.

### <a name="reset-hello-remote-desktop-service-configuration"></a>**Hallo extern bureaublad-service-configuratie opnieuw instellen**

Selecteer uw Windows-machine en klik vervolgens op **ondersteuning + probleemoplossing** > **wachtwoord opnieuw instellen**. Hallo wachtwoord opnieuw instellen van blade wordt weergegeven. 

![RDP-configuratie opnieuw instellen](./media/reset-rdp/Portal-RM-RDP-Reset.png)

Selecteer **alleen opnieuw instellen van configuratie** uit de vervolgkeuzelijst hello, klik vervolgens op **Update**. Probeer opnieuw verbinding te maken tooyour VM.


## <a name="vmaccess-extension-and-powershell"></a>VMAccess-extensie en PowerShell
Zorg ervoor dat u Hallo hebt [nieuwste PowerShell-module geïnstalleerd en geconfigureerd](/powershell/azure/overview) en zijn ondertekend in Azure-abonnement met Hallo tooyour `Login-AzureRmAccount` cmdlet.

### <a name="reset-hello-local-administrator-account-password"></a>**Hallo beheerderswachtwoord opnieuw instellen**
Opnieuw instellen van Hallo wachtwoord of gebruikersnaam beheerdersnaam Hello [Set AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell-cmdlet. Hiermee maakt u referenties voor uw account als volgt:

```powershell
$cred=Get-Credential
```

> [!NOTE] 
> Als u een andere naam dan de huidige lokale administrator-account Hallo typt op de virtuele machine, Hallo VMAccess-extensie wijzigt de naam van de lokale beheerdersaccount Hallo wijst uw toothat-account opgegeven wachtwoord en problemen met een extern bureaublad-en afmelden-gebeurtenis. Als Hallo lokale beheerdersaccount op de virtuele machine is uitgeschakeld, schakelt u Hallo VMAccess-extensie deze.

Voorbeeld van updates na Hallo Hallo VM met de naam `myVM` in Hallo resourcegroep met de naam `myResourceGroup` toohello referenties die zijn opgegeven.

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

### <a name="reset-hello-remote-desktop-service-configuration"></a>**Hallo extern bureaublad-service-configuratie opnieuw instellen**
Opnieuw instellen van externe toegang tooyour VM Hello [Set AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell-cmdlet. Hallo volgende voorbeeld wordt een extensie van Hallo toegang met de naam `myVMAccess` op Hallo VM met de naam `myVM` in Hallo `myResourceGroup` resourcegroep:

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResoureGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -typeHandlerVersion "2.0" -ForceRerun
```

> [!TIP]
> Een virtuele machine kan slechts één virtuele machine toegang agent hebben op elk gewenst moment. tooset hello VM toegang agent-eigenschappen, Hallo `-ForceRerun` optie kan worden gebruikt. Wanneer u `-ForceRerun`, zorg ervoor dat toouse Hallo dezelfde naam voor Hallo VM toegang agent zoals gebruikt in alle vorige opdrachten.

Als u nog steeds geen verbinding op afstand tooyour virtuele machine maken, raadpleegt u meer stappen tootry op [problemen met extern bureaublad-verbindingen tooa op basis van Windows Azure virtuele machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


## <a name="next-steps"></a>Volgende stappen
Als uitbreiding van virtuele machine van Azure toegang Hallo niet reageert en u niet kan tooreset Hallo wachtwoord, kunt u [reset Hallo lokale Windows-wachtwoord offline](reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Deze methode is een meer geavanceerde proces en moet u tooconnect Hallo virtuele harde schijf van Hallo problematisch VM tooanother VM. Hallo stappen beschreven in dit artikel eerst en proberen enkel Hallo offline wachtwoord opnieuw instellen van de methode een laatste toevlucht.

[Azure VM-extensies en functies](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[Verbinding maken met virtuele machine van Azure tooan met RDP of SSH](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[Problemen met extern bureaublad-verbindingen tooa op basis van Windows Azure virtuele machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

