---
title: aaaVirtual machine extensies en functies voor Windows in Azure | Microsoft Docs
description: Meer informatie over welke extensies beschikbaar zijn voor virtuele machines in Azure, gegroepeerd op wat ze bieden of verbeteren.
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 999d63ee-890e-432e-9391-25b3fc6cde28
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/06/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 61ccfd696b38e9be1026d836d5796c2346fd650f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machine-extensions-and-features-for-windows"></a>Virtuele machine-extensies en functies voor Windows

Virtuele machine van Azure-extensies zijn kleine toepassingen waarmee de configuratie en automatisering taken na de implementatie op virtuele machines in Azure. Als een virtuele machine vereist een software-installatie, beveiliging tegen virussen of Docker-configuratie, een VM-extensie kan bijvoorbeeld worden gebruikt toocomplete deze taken. Azure VM-extensies kunnen worden uitgevoerd met behulp van hello Azure CLI, Azure Resource Manager-sjablonen, PowerShell en hello Azure-portal. Uitbreidingen worden gebundeld met een nieuwe implementatie van de virtuele machine of eventuele bestaande systeem uitgevoerd.

Dit document bevat een overzicht van de virtuele machine-extensies vereisten voor het gebruik van uitbreidingen van de virtuele machine en richtlijnen over hoe toodetect, beheren en uitbreidingen van de virtuele machine verwijderen. Dit document vindt u algemene informatie omdat veel VM-extensies beschikbaar zijn, elk met een potentieel unieke configuratie. Extensie-specifieke informatie vindt u in elke afzonderlijke document specifieke toohello-extensie.

## <a name="use-cases-and-samples"></a>Gebruiksvoorbeelden en voorbeelden

Er zijn veel verschillende Azure VM-extensies beschikbaar, elk met een specifieke aanvraag gebruikt. Er zijn enkele gebruiksvoorbeelden:

- Virtuele machine met PowerShell gewenst status configuraties tooa toepassen door middel van Hallo DSC-uitbreiding voor Windows. Zie voor meer informatie [Azure gewenst State configuration-uitbreiding](extensions-dsc-overview.md).
- Virtuele machine met behulp van Microsoft Monitoring Agent VM-extensie Hallo controle configureren Zie voor meer informatie [verbinding maken met Azure virtuele machines tooLog Analytics](../../log-analytics/log-analytics-azure-vm-extension.md).
- Bewaking van uw Azure-infrastructuur met Hallo Datadog-uitbreiding configureren. Zie voor meer informatie, Hallo [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).
- Een virtuele machine van Azure met behulp van Chef configureren. Zie voor meer informatie [Azure automatisering van de implementatie van de virtuele machine met Chef](chef-automation.md).

Bovendien tooprocess-specifieke uitbreidingen, een extensie voor aangepaste scripts is beschikbaar voor Windows- en Linux virtuele machines. Hallo-extensie voor aangepaste scripts voor Windows kunt een PowerShell-script toobe uitvoeren op een virtuele machine. Dit is handig bij het ontwerpen van Azure-implementaties die moeten worden geconfigureerd afgezien van wat systeemeigen Azure tooling kan bieden. Zie voor meer informatie [Windows VM aangepaste scriptextensie](extensions-customscript.md).


## <a name="prerequisites"></a>Vereisten

De extensie van elke virtuele machine mogelijk een eigen set vereisten. Hallo Docker VM-extensie heeft bijvoorbeeld een vereiste van een ondersteunde Linux-distributie. Vereisten van afzonderlijke uitbreidingen zijn aangegeven in het Hallo-extensie-specifieke documentatie.

### <a name="azure-vm-agent"></a>Azure VM-agent
Hello Azure VM-agent beheert interactie tussen een virtuele machine van Azure en hello Azure-infrastructuurcontroller. Hallo VM-agent is verantwoordelijk voor veel functionele aspecten van het implementeren en beheren van virtuele machines in Azure, waaronder het uitvoeren van de VM-extensies. Hello Azure VM-agent is geïnstalleerd op Azure Marketplace-installatiekopieën en kan worden geïnstalleerd op ondersteunde besturingssystemen.

Zie voor informatie over ondersteunde besturingssystemen en installatie-instructies, [virtuele machine van Azure-agent](agent-user-guide.md).

## <a name="discover-vm-extensions"></a>VM-extensies detecteren
Veel andere VM-extensies zijn beschikbaar voor gebruik met virtuele machines in Azure. toosee een volledige lijst Hallo volgende opdracht met hello Azure Resource Manager PowerShell-module worden uitgevoerd. Zorg ervoor dat toospecify Hallo gewenste locatie wanneer u deze opdracht uitvoert.

```powershell
Get-AzureRmVmImagePublisher -Location WestUS | `
Get-AzureRmVMExtensionImageType | `
Get-AzureRmVMExtensionImage | Select Type, Version
```

## <a name="run-vm-extensions"></a>VM-extensies worden uitgevoerd

Uitbreidingen van de virtuele machine van Azure kunnen worden uitgevoerd op een bestaande virtuele machines die is handig als u de verbinding op een reeds geïmplementeerde virtuele machine herstellen of toomake configuratiewijzigingen nodig. VM-extensies kunnen ook worden gebundeld met implementaties van Azure Resource Manager-sjabloon. Via uitbreidingen met Resource Manager-sjablonen kunt u virtuele machines in Azure toobe geïmplementeerd en geconfigureerd zonder dat tussenkomst van de na de implementatie Hallo inschakelen.

Hallo volgende methoden kan worden gebruikt toorun een uitbreiding op basis van een bestaande virtuele machine.

### <a name="powershell"></a>PowerShell

Er bestaan verschillende PowerShell-opdrachten voor het uitvoeren van afzonderlijke uitbreidingen. toosee een lijst Hallo volgende PowerShell-opdrachten uitvoeren.

```powershell
get-command Set-AzureRM*Extension* -Module AzureRM.Compute
```

Dit biedt soortgelijke toohello-volgende uitvoer:

```powershell
CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Set-AzureRmVMAccessExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMADDomainExtension                     2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMAEMExtension                          2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMBackupExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMBginfoExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMChefExtension                         2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMCustomScriptExtension                 2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDiagnosticsExtension                  2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDiskEncryptionExtension               2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDscExtension                          2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMExtension                             2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMSqlServerExtension                    2.2.0      AzureRM.Compute
```

Hallo volgende voorbeeld wordt Hallo aangepast Script extensie toodownload een script van een GitHub-opslagplaats op Hallo doel-virtuele machine en vervolgens Hallo-script uitvoeren. Zie voor meer informatie over Hallo extensie voor aangepaste scripts [extensieoverzicht aangepast Script](extensions-customscript.md).

```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" -Name "myCustomScript" `
    -FileUri "https://raw.githubusercontent.com/neilpeterson/nepeters-azure-templates/master/windows-custom-script-simple/support-scripts/Create-File.ps1" `
    -Run "Create-File.ps1" -Location "West US"
```

In dit voorbeeld is Hallo uitbreiding voor toegang tot VM gebruikte tooreset Hallo beheerderswachtwoord van een virtuele machine van Windows. Zie voor meer informatie over Hallo uitbreiding voor toegang tot VM [opnieuw instellen van extern bureaublad-service in een Windows-VM](reset-rdp.md).

```powershell
$cred=Get-Credential

Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" -Name "myVMAccess" `
    -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

Hallo `Set-AzureRmVMExtension` opdracht gebruikte toostart elke VM-extensie kan zijn. Zie voor meer informatie, Hallo [Set AzureRmVMExtension verwijzing](https://msdn.microsoft.com/en-us/library/mt603745.aspx).


### <a name="azure-portal"></a>Azure Portal

Een VM-extensie kan worden toegepast tooan bestaande virtuele machine via hello Azure-portal. toodo dus Hallo virtuele machine selecteert u toouse wilt, kiest u **extensies**, en klik op **toevoegen**. Dit biedt een lijst met beschikbare uitbreidingen. Selecteer Hallo een u wilt en volg de stappen Hallo in Hallo-wizard.

Hallo toont volgende afbeelding Hallo-installatie van Hallo Microsoft Antimalware-extensie van hello Azure-portal.

![Antimalware-uitbreiding installeren](./media/extensions-features/installantimalwareextension.png)

### <a name="azure-resource-manager-templates"></a>Azure Resource Manager-sjablonen

VM-extensies kunnen toegevoegde tooan Azure Resource Manager-sjabloon en uitgevoerd met de implementatie van de sjabloon Hallo Hallo. Uitbreidingen met een sjabloon implementeren is handig voor het volledig geconfigureerde Azure-implementaties maken. Bijvoorbeeld: hello die volgende JSON is genomen van de Resource Manager-sjabloon die u implementeert een set van netwerktaakverdeling virtuele machines en een Azure SQL database en installeert een toepassing .NET Core op elke virtuele machine. Hallo VM-extensie zorgt voor Hallo software-installatie.

Zie voor meer informatie, Hallo [volledige Resource Manager-sjabloon](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

Zie voor meer informatie [Azure Resource Manager-sjablonen samenstellen met Windows VM-extensies](template-description.md#extensions).

## <a name="secure-vm-extension-data"></a>Beveiligde gegevens van de VM-extensie

Wanneer u een VM-extensie uitvoert, kan het benodigde tooinclude gevoelige informatie zoals referenties, namen van opslagaccounts en toegang tot de opslagaccountsleutels zijn. Veel VM-extensies bevatten een beveiligde configuratie die gegevens versleutelt en ontsleutelt deze alleen in de virtuele doelmachine Hallo. Elke uitbreiding heeft een specifieke beveiligde configuratieschema die worden uiteengezet in de documentatie van de extensie-specifieke.

Hallo volgende voorbeeld ziet u een exemplaar van Hallo extensie voor aangepaste scripts voor Windows. U ziet dat tooexecute Hallo-opdracht bevat een set referenties. In dit voorbeeld Hallo opdracht tooexecute niet versleuteld.


```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ],
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

Hallo uitvoering tekenreeks beveiligen door Hallo verplaatsen **opdracht tooexecute** eigenschap toohello **beveiligd** configuratie.

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

## <a name="troubleshoot-vm-extensions"></a>VM-extensies oplossen

Elk VM-extensie wellicht specifieke stappen voor probleemoplossing. Bijvoorbeeld, wanneer u Hallo aangepaste scriptextensie, script uitvoering details zijn te vinden lokaal op Hallo virtuele machine waarop Hallo-extensie is uitgevoerd. Probleemoplossing-extensie-specifieke worden beschreven in de documentatie van de extensie-specifieke.

Hallo volgende stappen voor probleemoplossing toepassing tooall-extensies voor virtuele machine.

### <a name="view-extension-status"></a>Status van de extensie weergeven

Nadat de extensie van een virtuele machine is uitgevoerd voor een virtuele machine, gebruikt u Hallo status van de PowerShell-opdracht tooreturn-extensie te volgen. Parameternamen voorbeeld vervangen door uw eigen waarden. Hallo `Name` parameter toohello extensie opgegeven tijdens het uitvoeren van Hallo-naam heeft.

```PowerShell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

Hallo-uitvoer ziet er Hallo volgende:

```json
ResourceGroupName       : myResourceGroup
VMName                  : myVM
Name                    : myExtensionName
Location                : westus
Etag                    : null
Publisher               : Microsoft.Azure.Extensions
ExtensionType           : DockerExtension
TypeHandlerVersion      : 1.0
Id                      : /subscriptions/mySubscriptionIS/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM/extensions/myExtensionName
PublicSettings          :
ProtectedSettings       :
ProvisioningState       : Succeeded
Statuses                :
SubStatuses             :
AutoUpgradeMinorVersion : False
ForceUpdateTag          :
```

Status van extensie-uitvoering kan worden gevonden in hello Azure-portal. tooview hello status van een extensie, selecteer Hallo virtuele machine kiezen **extensies**, en selecteer de gewenste extensie Hallo.

### <a name="rerun-vm-extensions"></a>VM-extensies opnieuw uitvoeren

Mogelijk zijn er gevallen waarin de extensie van een virtuele machine toobe moet opnieuw uit. U kunt dit doen door Hallo extensie verwijderen en vervolgens opnieuw uit te voeren Hallo-extensie met een methode van de uitvoering van uw keuze. tooremove een uitbreiding Hallo volgende opdracht met hello Azure PowerShell-module worden uitgevoerd. Parameternamen voorbeeld vervangen door uw eigen waarden.

```powershell
Remove-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

Een uitbreiding kan ook worden verwijderd via hello Azure-portal. toodo zodat:

1. Selecteer een virtuele machine.
2. Selecteer **extensies**.
3. Kies Hallo gewenste extensie.
4. Selecteer **verwijderen**.

## <a name="common-vm-extensions-reference"></a>Algemene referentie voor VM-extensies
| Naam van de uitbreiding | Beschrijving | Meer informatie |
| --- | --- | --- |
| Extensie voor aangepaste scripts voor Windows |Scripts uitvoeren op een virtuele machine van Azure |[Extensie voor aangepaste scripts voor Windows](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| DSC-extensie voor Windows |PowerShell DSC (Desired State Configuration)-extensie |[DSC-extensie voor Windows](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| Azure Diagnostics-extensie |Azure Diagnostics beheren |[Azure Diagnostics-extensie](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| Uitbreiding van de toegang tot Azure VM |Gebruikers en referenties beheren |[Uitbreiding van de VM-toegang voor Linux](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
