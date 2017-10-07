---
title: aaaCommon PowerShell-opdrachten voor Azure Virtual Machines | Microsoft Docs
description: Algemene PowerShell-opdrachten tooget u gestart maken en beheren van uw Windows-machines in Azure.
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ba3839a2-f3d5-4e19-a5de-95bfb1c0e61e
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: 3de9bd4d20259ced2c0aa8ef7a3f7d9520a071d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="common-powershell-commands-for-creating-and-managing-azure-virtual-machines"></a>Algemene PowerShell-opdrachten voor het maken en beheren van Azure Virtual Machines

In dit artikel bevat informatie over sommige hello die Azure PowerShell-opdrachten toocreate gebruiken en beheren van virtuele machines in uw Azure-abonnement.  Voor meer hulp bij specifieke opdrachtregelopties en opties, kunt u **Get-Help** *opdracht*.

Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) voor meer informatie over Hallo meest recente versie van Azure PowerShell installeren, uw abonnement te selecteren en tooyour account aanmelden.

Deze variabelen kunnen nuttig zijn voor u als meer dan één Hallo opdrachten in dit artikel wordt uitgevoerd:

- $location - Hallo-locatie van Hallo virtuele machine. U kunt [Get-AzureRmLocation](https://docs.microsoft.com/powershell/module/azurerm.resources/get-azurermlocation) toofind een [geografische regio](https://azure.microsoft.com/regions/) die voor u geschikt.
- $myResourceGroup - Hallo-naam van resourcegroep Hallo die Hallo virtuele machine bevat.
- $myVM - Hallo-naam van Hallo virtuele machine.

## <a name="create-a-vm"></a>Een virtuele machine maken

| Taak | Opdracht |
| ---- | ------- |
| Maak een VM-configuratie |$vm = [nieuw AzureRmVMConfig](https://docs.microsoft.com/powershell/module/azurerm.compute/new-azurermvmconfig) - VMName $myVM - VMSize 'Standard_D1_v1'<BR></BR><BR></BR>Hallo VM-configuratie is gebruikte toodefine of update-instellingen voor Hallo VM. Hallo-configuratie met de naam van de Hallo Hallo VM is geïnitialiseerd en de bijbehorende [grootte](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). |
| Configuratie-instellingen toevoegen |$vm = [set AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) - VM $vm-Windows - ComputerName $myVM-$cred - ProvisionVMAgent referentie - EnableAutoUpdate<BR></BR><BR></BR>Instellingen van besturingssystemen met inbegrip van [referenties](https://technet.microsoft.com/library/hh849815.aspx) toohello configuration-object dat u eerder hebt gemaakt met behulp van New-AzureRmVMConfig worden toegevoegd. |
| Toevoegen van een netwerkinterface |$vm = [toevoegen AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.5.0/Add-AzureRmVMNetworkInterface) - VM $vm-Id $nic. ID<BR></BR><BR></BR>Een virtuele machine moet hebben een [netwerkinterface](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toocommunicate in een virtueel netwerk. U kunt ook [Get-AzureRmNetworkInterface](https://docs.microsoft.com/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) tooretrieve een bestaande netwerkinterface-object. |
| Geef een platforminstallatiekopie |$vm = [set AzureRmVMSourceImage](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmsourceimage) - VM $vm - PublisherName 'publisher_name'-'publisher_offer' bieden - SKU's 'product_sku'-'nieuwste' versie<BR></BR><BR></BR>[Afbeelding van informatie](cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello configuration-object dat u eerder hebt gemaakt met behulp van New-AzureRmVMConfig wordt toegevoegd. Hallo-object geretourneerd door deze opdracht wordt alleen gebruikt wanneer u een platforminstallatiekopie Hallo OS schijf toouse instellen. |
| OS-schijf toouse een platforminstallatiekopie instellen |$vm = [set AzureRmVMOSDisk](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmosdisk) - VM $vm-http://mystore1.blob.core.windows.net/vhds/myOSDisk.vhd' Name 'myOSDisk' - VhdUri' - CreateOption FromImage<BR></BR><BR></BR>Hallo-naam van de besturingssysteemschijf hello en de locatie in [opslag](../../storage/common/storage-powershell-guide-full.md) toohello configuration-object dat u eerder hebt gemaakt wordt toegevoegd. |
| Een algemene installatiekopie voor OS schijf toouse instellen |$vm = $vm set AzureRmVMOSDisk - VM-naam 'myOSDisk' - SourceImageUri 'https://mystore1.blob.core.windows.net/system/Microsoft.Compute/Images/myimages/myprefix-osDisk. {guid} .vhd"- VhdUri 'https://mystore1.blob.core.windows.net/vhds/disk_name.vhd' - CreateOption FromImage-Windows<BR></BR><BR></BR>Hallo-naam van besturingssysteemschijf hello, Hallo-locatie van de broninstallatiekopie Hallo en de locatie van de schijf Hallo in [opslag](../../storage/common/storage-powershell-guide-full.md) toohello configuration-object is toegevoegd. |
| OS-schijf toouse een gespecialiseerde installatiekopie instellen |$vm = $vm set AzureRmVMOSDisk - VM-naam 'myOSDisk' - VhdUri 'http://mystore1.blob.core.windows.net/vhds/' - CreateOption koppelen - Windows |
| Een virtuele machine maken |[Nieuwe AzureRmVM]() - ResourceGroupName $myResourceGroup-locatie $location - VM $vm<BR></BR><BR></BR>Alle resources worden gemaakt in een [resourcegroep](../../azure-resource-manager/powershell-azure-resource-manager.md). Voordat u deze opdracht uitvoert, nieuw AzureRmVMConfig, Set AzureRmVMOperatingSystem, Set AzureRmVMSourceImage, toevoegen AzureRmVMNetworkInterface en Set-AzureRmVMOSDisk uitvoeren. |

## <a name="get-information-about-vms"></a>Informatie ophalen over virtuele machines

| Taak | Opdracht |
| ---- | ------- |
| Lijst met virtuele machines in een abonnement |[Get-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvm) |
| Lijst met virtuele machines in een resourcegroep |Get-AzureRmVM - ResourceGroupName $myResourceGroup<BR></BR><BR></BR>tooget een lijst met resource groepen in uw abonnement, gebruikt u [Get-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/get-azurermresourcegroup). |
| Informatie over een VM ophalen |Get-AzureRmVM - ResourceGroupName $myResourceGroup-$myVM naam |

## <a name="manage-vms"></a>Virtuele machines beheren
| Taak | Opdracht |
| --- | --- |
| Een VM starten |[Start-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/start-azurermvm) - ResourceGroupName $myResourceGroup-$myVM naam |
| Een VM stoppen |[Stop-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/stop-azurermvm) - ResourceGroupName $myResourceGroup-$myVM naam |
| Een actieve virtuele machine starten |[Start-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/restart-azurermvm) - ResourceGroupName $myResourceGroup-$myVM naam |
| Een VM verwijderen |[Remove-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/remove-azurermvm) - ResourceGroupName $myResourceGroup-$myVM naam |
| Een virtuele machine generalize |[Set-AzureRmVm](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvm) - ResourceGroupName $myResourceGroup-naam $myVM-gegeneraliseerd<BR></BR><BR></BR>Deze opdracht uitvoeren voordat u opslaan AzureRmVMImage uitvoert. |
| Een virtuele machine vastleggen |[Opslaan AzureRmVMImage](https://docs.microsoft.com/powershell/module/azurerm.compute/save-azurermvmimage) myImagePrefix' - ResourceGroupName $myResourceGroup - VMName $myVM - DestinationContainerName 'myImageContainer' - VHDNamePrefix'-'C:\filepath\filename.json' pad<BR></BR><BR></BR>Een virtuele machine moet worden [voorbereid, afgesloten en gegeneraliseerd](prepare-for-upload-vhd-image.md) toocreate toobe gebruikt een afbeelding. Voordat u deze opdracht uitvoert, voert u Set-AzureRmVm. |
| Een virtuele machine bijwerken |[Update-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/update-azurermvm) - ResourceGroupName $myResourceGroup - VM $vm<BR></BR><BR></BR>Hallo huidige VM-configuratie met behulp van Get-AzureRmVM ophalen, configuratie-instellingen op VM-object op Hallo wijzigen en voer deze opdracht. |
| Toevoegen van een data schijf tooa VM |[Voeg AzureRmVMDataDisk](https://docs.microsoft.com/powershell/module/azurerm.compute/add-azurermvmdatadisk) - VM $vm-https://mystore1.blob.core.windows.net/vhds/myDataDisk.vhd' Name 'myDataDisk' - VhdUri' - LUN #-Caching ReadWrite - DiskSizeinGB # - CreateOption leeg<BR></BR><BR></BR>Gebruik Get-AzureRmVM tooget Hallo VM-object. Hallo LUN aantal en de grootte van de Hallo van Hallo schijf opgeven. Update-AzureRmVM tooapply Hallo configuratie wijzigingen toohello VM worden uitgevoerd. Hallo-schijf die u toevoegt, is niet geïnitialiseerd. |
| Een gegevensschijf verwijderen van een VM |[Verwijder AzureRmVMDataDisk](https://docs.microsoft.com/powershell/module/azurerm.compute/remove-azurermvmdatadisk) - VM $vm-naam 'myDataDisk'<BR></BR><BR></BR>Gebruik Get-AzureRmVM tooget Hallo VM-object. Update-AzureRmVM tooapply Hallo configuratie wijzigingen toohello VM worden uitgevoerd. |
| Toevoegen van een extensie tooa VM |[Set-AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) - ResourceGroupName $myResourceGroup-locatie $location - VMName $myVM-naam 'Extensienaam'-Publisher 'publisherName'-Type 'extensionType' - TypeHandlerVersion ' #. # '-Instellingen $Settings - ProtectedSettings $ProtectedSettings<BR></BR><BR></BR>Deze opdracht uitvoert met de juiste Hallo [configuratiegegevens](template-description.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#extensions) voor Hallo-extensie die u tooinstall wilt. |
| Een VM-extensie verwijderen |[Verwijder AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/remove-azurermvmextension) - ResourceGroupName $myResourceGroup-naam 'Extensienaam' - VMName $myVM |

## <a name="next-steps"></a>Volgende stappen
* Zie Hallo basisstappen voor het maken van een virtuele machine in [maken van een Windows-VM met Resource Manager en PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

