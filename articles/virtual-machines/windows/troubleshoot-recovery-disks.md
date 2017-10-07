---
title: aaaUse a Windows VM met Azure PowerShell probleemoplossing | Microsoft Docs
description: Meer informatie over hoe Windows VM tootroubleshoot problemen in Azure door verbinding te maken Hallo OS tooa schijfherstel VM die gebruikmaakt van Azure PowerShell
services: virtual-machines-windows
documentationCenter: 
authors: genlin
manager: timlt
editor: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 7a6a76f64824fe5d06dc4286cb1d87ab8bb794e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-windows-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-azure-powershell"></a>Een virtuele machine van Windows oplossen door het Hallo OS tooa schijfherstel VM die gebruikmaakt van Azure PowerShell koppelen
Als uw Windows-machine (VM) in Azure een opstart- of -fout optreedt, moet u mogelijk tooperform stappen voor probleemoplossing in het virtuele harde schijf hello, zelf. Een veelvoorkomend voorbeeld zou een mislukte toepassingsupdate die verhindert dat Hallo VM kunnen tooboot correct zijn. Dit artikel details hoe toouse Azure PowerShell tooconnect uw virtuele harde schijf tooanother Windows VM toofix eventuele fouten opnieuw maken van de oorspronkelijke VM.


## <a name="recovery-process-overview"></a>Overzicht van het herstelproces
Hallo procedure voor probleemoplossing is als volgt:

1. Verwijder Hallo VM zonder problemen Hallo virtuele harde schijven te houden.
2. Koppelen en koppelen van Hallo virtuele harde schijf tooanother Windows-VM voor het oplossen van problemen.
3. Verbinding maken met toohello VM probleemoplossing. Bestanden bewerken of toofix problemen van alle hulpprogramma's uitvoeren op Hallo oorspronkelijke virtuele harde schijf.
4. Ontkoppel en Hallo virtuele harde schijf van Hallo probleemoplossing VM loskoppelen.
5. Een virtuele machine maken met Hallo oorspronkelijke virtuele harde schijf.

Zorg ervoor dat u hebt [nieuwste Azure PowerShell Hallo](/powershell/azure/overview) geïnstalleerd en geregistreerd in tooyour abonnement:

```powershell
Login-AzureRMAccount
```

In Hallo vervangen volgende voorbeelden parameternamen door uw eigen waarden. De namen van de voorbeeld-parameter `myResourceGroup`, `mystorageaccount`, en `myVM`.


## <a name="determine-boot-issues"></a>Opstartproblemen bepalen
U kunt een schermopname van uw virtuele machine weergeven in Azure toohelp problemen met opstarten. Deze schermafbeelding kunt nagaan waarom een virtuele machine tooboot mislukt. Hallo volgende voorbeeld krijgt Hallo schermafbeelding van virtuele machine met de naam van Windows hello `myVM` in Hallo resourcegroep met de naam `myResourceGroup`:

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup `
    -Name myVM -Windows -LocalPath C:\Users\ops\
```

Bekijk Hallo schermafbeelding toodetermine waarom Hallo VM tooboot is mislukt. Houd er rekening mee specifieke foutberichten of foutcodes die zijn opgegeven.


## <a name="view-existing-virtual-hard-disk-details"></a>Bestaande virtuele harde schijf details weergeven
Voordat u uw virtuele harde schijf tooanother VM koppelen kunt, moet u tooidentify Hallo-naam van Hallo virtuele harde schijf (VHD).

Hallo volgende voorbeeld worden gegevens opgehaald voor virtuele machine met de naam Hallo `myVM` in Hallo resourcegroep met de naam `myResourceGroup`:

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

Zoek naar `Vhd URI` binnen Hallo `StorageProfile` sectie uit Hallo uitvoer van de voorgaande opdracht Hallo. Hallo volgende ingekorte voorbeelduitvoer wordt weergegeven Hallo `Vhd URI` aan einde van het codeblok Hallo Hallo:

```powershell
RequestId                     : 8a134642-2f01-4e08-bb12-d89b5b81a0a0
StatusCode                    : OK
ResourceGroupName             : myResourceGroup
Id                            : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM
Name                          : myVM
Type                          : Microsoft.Compute/virtualMachines
...
StorageProfile                :
  ImageReference              :
    Publisher                 : MicrosoftWindowsServer
    Offer                     : WindowsServer
    Sku                       : 2016-Datacenter
    Version                   : latest
  OsDisk                      :
    OsType                    : Windows
    Name                      : myVM
    Vhd                       :
      Uri                     : https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
    Caching                   : ReadWrite
    CreateOption              : FromImage
```


## <a name="delete-existing-vm"></a>Bestaande virtuele machine verwijderen
Virtuele harde schijven en virtuele machines zijn twee verschillende resources in Azure. Een virtuele harde schijf is waar Hallo besturingssysteem zelf, toepassingen en configuraties worden opgeslagen. Hallo VM zelf zijn gewoon metagegevens die definieert Hallo grootte of de locatie en verwijst naar resources, zoals een virtuele harde schijf of virtuele netwerkinterfacekaart (NIC). Elke virtuele harde schijf heeft een lease toegewezen wanneer gekoppeld tooa VM. Hoewel gegevensschijven kunnen worden gekoppeld en ontkoppeld, zelfs wanneer Hallo VM wordt uitgevoerd, kan de besturingssysteemschijf Hallo kan niet worden losgekoppeld tenzij Hallo VM-resource wordt verwijderd. Hallo lease blijft tooassociate Hallo OS-schijf met een virtuele machine, zelfs wanneer die VM een status gestopt en de toewijzing ongedaan is gemaakt heeft.

eerste stap toorecover Hallo uw VM is toodelete Hallo VM-resource zelf. Verwijderen Hallo VM verlaat Hallo virtuele harde schijven in uw opslagaccount. Na het Hallo die virtuele machine is verwijderd, Hallo virtuele harde schijf tooanother VM tootroubleshoot koppelen en Hallo fouten op te lossen.

Hallo volgende voorbeeld verwijdert met de naam VM Hallo `myVM` van Hallo resourcegroep met de naam `myResourceGroup`:

```powershell
Remove-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

Wacht totdat het Hallo VM verwijderen voordat u Hallo virtuele harde schijf tooanother VM koppelen is voltooid. Hallo-lease op het virtuele harde schijf hello, waarin deze zijn gekoppeld aan VM Hallo moet toobe vrijgegeven voordat u Hallo virtuele harde schijf tooanother VM kunt koppelen.


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a>Bestaande virtuele harde schijf tooanother VM koppelen
Voor Hallo volgende stappen, u een andere virtuele machine gebruiken voor het oplossen van problemen. U koppelt Hallo bestaande virtuele harde schijf toothis VM toobrowse probleemoplossing en inhoud van de schijf Hallo bewerken. Dit proces kunt u toocorrect eventuele fouten in de configuratie of revisie aanvullende toepassings- of logboekbestanden, bijvoorbeeld. Kies of maak een ander VM-toouse voor het oplossen van problemen.

Wanneer u een bestaande virtuele harde schijf van Hallo koppelt, geef Hallo URL toohello schijf verkregen in de voorgaande Hallo `Get-AzureRmVM` opdracht. Hallo volgende voorbeeld wordt een bestaande virtuele harde schijf toohello het oplossen van problemen met de naam VM `myVMRecovery` in Hallo resourcegroep met de naam `myResourceGroup`:

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
Add-AzureRmVMDataDisk -VM $myVM -CreateOption "Attach" -Name "DataDisk" -DiskSizeInGB $null `
    -VhdUri "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

> [!NOTE]
> Een schijf toevoegen, moet u toospecify Hallo grootte van Hallo schijf. Als er een bestaande schijf koppelen, Hallo `-DiskSizeInGB` is opgegeven als `$null`. Deze waarde zorgt Hallo gegevensschijf correct is gekoppeld en zonder Hallo moet toodetermine Hallo true grootte van de gegevensschijf.


## <a name="mount-hello-attached-data-disk"></a>Hallo bijgesloten gegevensschijf koppelen

1. RDP-tooyour het oplossen van problemen met de juiste referenties Hallo VM. Hallo volgende voorbeeld downloadt Hallo RDP-verbindingsbestand voor Hallo VM met de naam `myVMRecovery` in Hallo resourcegroep met de naam `myResourceGroup`, en te downloadt`C:\Users\ops\Documents`'

    ```powershell
    Get-AzureRMRemoteDesktopFile -ResourceGroupName "myResourceGroup" -Name "myVMRecovery" `
        -LocalPath "C:\Users\ops\Documents\myVMRecovery.rdp"
    ```

2. Hallo gegevensschijf wordt automatisch gedetecteerd en gekoppeld. Lijst van de stationsletter van gekoppelde volumes toodetermine Hallo Hallo als volgt bekijken:

    ```powershell
    Get-Disk
    ```

    Hallo volgende voorbeelduitvoer toont Hallo virtuele hardeschijf een schijf verbonden **2**. (U kunt ook `Get-Volume` tooview Hallo stationsletter):

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Online       127 GB MBR
    ```

## <a name="fix-issues-on-original-virtual-hard-disk"></a>Los problemen op de oorspronkelijke virtuele harde schijf
Hallo bestaande virtuele harde schijf gekoppeld, kunt u eventuele onderhoud en probleemoplossing naar behoefte nu uitvoeren. Zodra u Hallo problemen hebt opgelost, kunt u doorgaan met de Hallo stappen te volgen.


## <a name="unmount-and-detach-original-virtual-hard-disk"></a>Ontkoppel en loskoppelen van de oorspronkelijke virtuele harde schijf
Zodra de fouten opgelost zijn, kunt u ontkoppelen en Hallo bestaande virtuele harde schijf los te koppelen van uw VM voor het oplossen van problemen. U kunt de virtuele harde schijf niet gebruiken met een andere VM tot Hallo lease Hallo virtuele harde schijf toohello probleemoplossing VM koppelen is vrijgegeven.

1. Ontkoppel de gegevensschijf Hallo binnen uw RDP-sessie op de herstel-VM. Moet u schijfnummer Hallo van Hallo vorige `Get-Disk` cmdlet. Vervolgens gebruikt u `Set-Disk` tooset Hallo schijf als offline zetten:

    ```powershell
    Set-Disk -Number 2 -IsOffline $True
    ```

    Bevestig het Hallo-schijf is nu ingesteld als het gebruik van offline `Get-Disk` opnieuw. Hallo volgende voorbeelduitvoer wordt weergegeven Hallo schijf nu is ingesteld als offline:

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Offline      127 GB MBR
    ```

2. De RDP-sessie af te sluiten. Hallo probleemoplossing VM opheffen Hallo virtuele hardeschijf van uw Azure PowerShell-sessie.

    ```powershell
    $myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
    Remove-AzureRmVMDataDisk -VM $myVM -Name "DataDisk"
    Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
    ```


## <a name="create-vm-from-original-hard-disk"></a>Virtuele machine van de oorspronkelijke harde schijf maken
toocreate een virtuele machine van de oorspronkelijke virtuele harde schijf gebruiken [deze Azure Resource Manager-sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet). Hallo werkelijke JSON-sjabloon is op Hallo koppeling:

- https://RAW.githubusercontent.com/Azure/Azure-QuickStart-templates/master/201-VM-Specialized-VHD-existing-vnet/azuredeploy.JSON

Hallo sjabloon een virtuele machine implementeert in een bestaand virtueel netwerk met behulp van Hallo VHD URL uit Hallo eerder opdracht. Hallo volgende voorbeeld implementeert Hallo sjabloon toohello resourcegroep met de naam `myResourceGroup`:

```powershell
New-AzureRmResourceGroupDeployment -Name myDeployment -ResourceGroupName myResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json
```

Antwoord Hallo vraagt om de sjabloon Hallo zoals VM-naam, type besturingssysteem en VM-grootte. Hallo `osDiskVhdUri` is dezelfde als eerder is gebruikt bij het toevoegen van Hallo bestaande virtuele harde schijf toohello probleemoplossing VM Hallo.


## <a name="re-enable-boot-diagnostics"></a>Diagnostische gegevens over opstarten weer inschakelen

Wanneer u uw virtuele machine van Hallo bestaande virtuele harde schijf maakt, kan boot diagnostics niet automatisch worden ingeschakeld. Hallo volgende voorbeeld wordt de diagnostische Hallo-extensie op Hallo VM met de naam `myVMDeployed` in Hallo resourcegroep met de naam `myResourceGroup`:

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMDeployed"
Set-AzureRmVMBootDiagnostics -ResourceGroupName myResourceGroup -VM $myVM -enable
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

## <a name="next-steps"></a>Volgende stappen
Als u verbinding maken met tooyour VM problemen ondervindt, raadpleegt u [problemen met RDP-verbindingen tooan Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Zie voor problemen met de toegang tot toepassingen die worden uitgevoerd op de virtuele machine [oplossen verbindingsproblemen van toepassing op een Windows VM](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Zie voor meer informatie over het gebruik van Resource Manager [overzicht van Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
