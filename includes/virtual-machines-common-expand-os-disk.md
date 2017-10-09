## <a name="overview"></a>Overzicht
Wanneer u een nieuwe virtuele machine (VM) maakt in een resourcegroep met de implementatie van een installatiekopie van [Azure Marketplace](https://azure.microsoft.com/marketplace/), Hallo standaard OS station is 127 GB. Hoewel het mogelijk tooadd gegevens schijven toohello VM (hoeveel, al naar gelang Hallo SKU u hebt gekozen) is en bovendien is het aanbevolen tooinstall toepassingen en werkbelastingen met een intensieve CPU op deze schijven addendum, moeten vaak ook klanten tooexpand Hallo OS station toosupport bepaalde scenario's zoals het volgende:

1. Ondersteuning voor oudere toepassingen die onderdelen op de besturingssysteemschijf installeren.
2. Een fysieke computer of virtuele machine migreren van on-premises met een grotere besturingssysteemschijf.

> [!IMPORTANT]
> In Azure zijn twee verschillende implementatiemodellen beschikbaar voor het maken van en werken met resources: Resource Manager en het klassieke model. In dit artikel bevat informatie over met behulp van Hallo Resource Manager-model. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.
> 
> 

## <a name="resize-hello-os-drive"></a>Hallo OS station vergroten of verkleinen
In dit artikel hebt we uitvoeren van de taak Hallo Hallo OS-station met resource manager-modules van formaat wijzigen van [Azure Powershell](/powershell/azureps-cmdlets-docs). Open de Powershell ISE of de Powershell-venster in de beheerdersmodus en volg onderstaande stappen voor Hallo:

1. Aanmelden tooyour Microsoft Azure-account op de resource management-modus en selecteer uw abonnement als volgt:
   
   ```Powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription –SubscriptionName 'my-subscription-name'
   ```
2. Stel de naam van de resourcegroep en de VM als volgt in:
   
   ```Powershell
   $rgName = 'my-resource-group-name'
   $vmName = 'my-vm-name'
   ```
3. Een verwijzing tooyour VM als volgt verkrijgen:
   
   ```Powershell
   $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```
4. Hallo VM stoppen voordat het vergroten of verkleinen Hallo schijf als volgt:
   
    ```Powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    ```
5. En komen Hallo momenteel die we hebt gewacht! Hallo-grootte van de waarde voor toohello gewenst Hallo OS-schijf instellen en Hallo VM als volgt bijwerken:
   
   ```Powershell
   $vm.StorageProfile.OSDisk.DiskSizeGB = 1023
   Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
   ```
   
   > [!WARNING]
   > Hallo nieuwe grootte moet groter zijn dan de bestaande schijfgrootte Hallo zijn. maximale toegestane Hallo is 1023 GB.
   > 
   > 
6. Bijwerken Hallo VM kan een paar seconden duren. Zodra het Hallo-opdracht is uitgevoerd, start u Hallo VM als volgt opnieuw:
   
   ```Powershell
   Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```

Dat is alles. Nu RDP in Hallo VM, open Computerbeheer (of Schijfbeheer) en vouw Hallo-station met Hallo zojuist toegewezen ruimte.

## <a name="summary"></a>Samenvatting
In dit artikel hebben we Azure Resource Manager-modules van Powershell tooexpand Hallo OS-schijf van de virtuele machine voor IaaS gebruikt. Hieronder wordt Hallo volledige script ter referentie:

```Powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName 'my-subscription-name'
$rgName = 'my-resource-group-name'
$vmName = 'my-vm-name'
$vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
$vm.StorageProfile.OSDisk.DiskSizeGB = 1023
Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
```

## <a name="next-steps"></a>Volgende stappen
Hoewel in dit artikel wordt primair gericht op het uitbreiden van de schijf Hallo OS Hallo VM, kan hello ontwikkelde script ook worden gebruikt voor het uitbreiden van Hallo gegevens schijven gekoppelde toohello VM door één regel code wijzigen. Bijvoorbeeld tooexpand Hallo eerste gegevens gekoppelde toohello VM schijf, vervang Hallo ```OSDisk``` object van het ```StorageProfile``` met ```DataDisks``` matrix en het gebruik van een numerieke index tooobtain een schijf verwijzing toofirst bijgesloten gegevens, zoals hieronder wordt weergegeven:

```Powershell
$vm.StorageProfile.DataDisks[0].DiskSizeGB = 1023
```
U kunt ook verwijzen naar andere schijven gekoppelde toohello VM, met behulp van een index, zoals hierboven van gegevens of Hallo ```Name``` van Hallo schijf zoals hieronder weergegeven:

```Powershell
($vm.StorageProfile.DataDisks | Where {$_.Name -eq 'my-second-data-disk'})[0].DiskSizeGB = 1023
```

Als u toofind wilt uit hoe tooattach tooan Azure Resource Manager VM schijven, dit selectievakje inschakelt [artikel](../articles/virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

