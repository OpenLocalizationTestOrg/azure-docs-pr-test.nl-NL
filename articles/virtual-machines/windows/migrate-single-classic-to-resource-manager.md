---
title: een klassieke VM tooan ARM beheerd schijf VM aaaMigrate | Microsoft Docs
description: "Migreren van één Azure VM van Hallo-classic deployment model tooManaged schijven Hallo Resource Manager-implementatiemodel."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: d8c4b9431f5dd8a071fcbc2ee36581a33f76ba62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manually-migrate-a-classic-vm-tooa-new-arm-managed-disk-vm-from-hello-vhd"></a>Handmatig migreren van een klassieke VM tooa nieuwe ARM beheerd schijf VM van Hallo VHD 


Deze sectie helpt u toomigrate uw bestaande Azure VM's vanuit het klassieke implementatiemodel hello te[schijven beheerd](managed-disks-overview.md) Hallo Resource Manager-implementatiemodel.


## <a name="plan-for-hello-migration-toomanaged-disks"></a>Hallo-migratie plannen tooManaged schijven

Deze sectie helpt u bij toomake Hallo beste beslissing op schijf en VM-typen.


### <a name="location"></a>Locatie

Kies een locatie waar Azure beheerd schijven beschikbaar zijn. Als u tooPremium beheerd schijven migreert, zorg er ook voor Premium-opslag is beschikbaar in Hallo regio waar u van plan bent toomigrate aan. Zie [Azure Services byRegion](https://azure.microsoft.com/regions/#services) voor actuele informatie over beschikbare locaties.

### <a name="vm-sizes"></a>Formaten van virtuele machines

Als u tooPremium beheerd schijven migreert, hebt u tooupdate Hallo grootte van Hallo VM tooPremium kan grootte van de opslagruimte beschikbaar is in Hallo regio waar de VM zich bevindt. Bekijk Hallo VM-grootten die Premium-opslag die geschikt zijn. Hello Azure VM-grootte specificaties worden vermeld in [grootten voor virtuele machines](sizes.md).
Bekijk de prestatiekenmerken Hallo van virtuele machines die geschikt is voor Premium-opslag en kies Hallo meest geschikte VM-grootte die het beste past bij uw werkbelasting. Zorg ervoor dat er voldoende bandbreedte beschikbaar op uw VM toodrive Hallo schijf verkeer is.

### <a name="disk-sizes"></a>Schijfformaten

**Premium beheerde schijven**

Er zijn zeven typen premium-beheerde schijven die kunnen worden gebruikt met uw virtuele machine en elke principal heeft bepaalde IOPs en doorvoerlimieten limieten. Houd rekening met deze limieten bij het kiezen van Hallo Premium schijftype voor uw virtuele machine op basis van Hallo behoeften van uw toepassing in termen van capaciteit, prestaties, schaalbaarheid en piek worden geladen.

| Premium-schijven Type  | P4    | P6    | P10   | P20   | P30   | P40   | P50   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| Schijfgrootte           | 128 GB| 512 GB| 128 GB| 512 GB            | 1024 GB (1 TB)    | 2048 GB (2 TB)    | 4095 GB (4 TB)    | 
| IOP's per schijf       | 120   | 240   | 500   | 2300              | 5000              | 7500              | 7500              | 
| Doorvoer per schijf | 25 MB per seconde  | 50 MB per seconde  | 100 MB per seconde | 150 MB per seconde | 200 MB per seconde | 250 MB per seconde | 250 MB per seconde | 

**Beheerde standaardschijven**

Er zijn zeven soorten Standard-beheerde schijven die kunnen worden gebruikt met uw virtuele machine. Elk van deze andere capaciteit hebben maar dezelfde IOPS en doorvoerlimieten hebben. Standard-beheerde schijven op basis van de capaciteitsbehoeften Hallo van uw toepassing hello type kiezen.

| Standard-schijftype  | S4               | S6               | S10              | S20              | S30              | S40              | S50              | 
|---------------------|---------------------|---------------------|------------------|------------------|------------------|------------------|------------------| 
| Schijfgrootte           | 30 GB            | 64 GB            | 128 GB           | 512 GB           | 1024 GB (1 TB)   | 2048 GB (2TB)    | 4095 GB (4 TB)   | 
| IOP's per schijf       | 500              | 500              | 500              | 500              | 500              | 500             | 500              | 
| Doorvoer per schijf | 60 MB per seconde | 60 MB per seconde | 60 MB per seconde | 60 MB per seconde | 60 MB per seconde | 60 MB per seconde | 60 MB per seconde | 


### <a name="disk-caching-policy"></a>Het beleid voor schijf 

**Premium beheerde schijven**

Beleid voor de schijfcache is standaard *alleen-lezen* voor alle gegevensschijven Premium, Hallo en *lezen-schrijven* voor Hallo Premium besturingssysteemschijf gekoppeld toohello VM. Deze configuratieinstelling wordt aanbevolen tooachieve Hallo optimale prestaties voor uw toepassing IOs. Voor schijven schrijven zware of alleen-schrijven gegevens (zoals SQL Server-logboekbestanden), uitschakelen schijfcache, zodat u kunt betere prestaties bereiken.

### <a name="pricing"></a>Prijzen

Bekijk Hallo [prijzen voor schijven beheerd](https://azure.microsoft.com/en-us/pricing/details/managed-disks/). Prijzen van beheerde Premium-schijven is hetzelfde als Hallo onbeheerde Premium-schijven. Maar prijzen voor beheerde standaardschijven is anders dan standaardschijven zonder begeleiding.


## <a name="checklist"></a>Controlelijst

1.  Als u tooPremium beheerd schijven migreert, zorg er dan voor dat deze beschikbaar is in Hallo regio die u naar migreert.

2.  Bepaal Hallo nieuwe VM-reeks die u gaat gebruiken. Deze moet een Premium-opslag geschikt als u tooPremium beheerd schijven migreert.

3.  Bepaal Hallo exacte VM-grootte u wilt gebruiken die beschikbaar zijn in Hallo regio die u migreert naar. VM-grootte moet toobe groot genoeg toosupport Hallo aantal gegevensschijven dat u hebt. Als u vier gegevensschijven hebt, moet Hallo VM twee of meer kernen hebben. Houd ook rekening met verwerkingskracht, geheugen en netwerkbandbreedte moet.

4.  Informatie over een Hallo huidige VM handige, inclusief Hallo-lijst van schijven en de bijbehorende VHD-blobs.

Bereid uw toepassing uitvaltijd. toodo een schone migratie, hebt u toostop Hallo verwerking in de huidige systeem Hallo. Alleen dan kunt u dit downloaden tooconsistent staat die u kunt migreren toohello nieuwe platform. Duur van uitvaltijd is afhankelijk van Hallo hoeveelheid gegevens in Hallo schijven toomigrate.


## <a name="migrate-hello-vm"></a>Hallo VM migreren

Bereid uw toepassing uitvaltijd. toodo een schone migratie, hebt u toostop Hallo verwerking in de huidige systeem Hallo. Alleen dan kunt u dit downloaden tooconsistent staat die u kunt migreren toohello nieuwe platform. Duur van uitvaltijd is afhankelijk van de hoeveelheid gegevens in Hallo schijven toomigrate Hallo.


1.  Stel eerst Hallo algemene parameters:

    ```powershell
    $resourceGroupName = 'yourResourceGroupName'
    
    $location = 'your location' 
    
    $virtualNetworkName = 'yourExistingVirtualNetworkName'
    
    $virtualMachineName = 'yourVMName'
    
    $virtualMachineSize = 'Standard_DS3'
    
    $adminUserName = "youradminusername"
    
    $adminPassword = "yourpassword" | ConvertTo-SecureString -AsPlainText -Force
    
    $imageName = 'yourImageName'
    
    $osVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd'
    
    $dataVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk1.vhd'
    
    $dataDiskName = 'dataDisk1'
    ```

2.  Maak een beheerde OS-schijf met Hallo VHD van Hallo klassieke VM.

    Zorg ervoor dat u hebt opgegeven Hallo URI Hallo OS VHD toohello $osVhdUri parameter voltooien. Typ ook **- AccountType** als **PremiumLRS** of **StandardLRS** op basis van het type schijven (Premium of Standard) u migreert naar.

    ```powershell
    $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $osVhdUri) '
    -ResourceGroupName $resourceGroupName
    ```

3.  Hallo OS schijf toohello koppelen nieuwe virtuele machine.

    ```powershell
    $VirtualMachine = New-AzureRmVMConfig -VMName $virtualMachineName -VMSize $virtualMachineSize
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -ManagedDiskId $osDisk.Id '
    -StorageAccountType PremiumLRS -DiskSizeInGB 128 -CreateOption Attach -Windows
    ```

4.  Een beheerde gegevensschijf van Hallo gegevens VHD-bestand maken en toe te voegen toohello nieuwe virtuele machine.

    ```powershell
    $dataDisk1 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreationDataCreateOption Import '
    -SourceUri $dataVhdUri ) -ResourceGroupName $resourceGroupName
    
    $VirtualMachine = Add-AzureRmVMDataDisk -VM $VirtualMachine -Name $dataDiskName '
    -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1
    ```

5.  Maken van nieuwe virtuele machine Hallo door in te stellen van openbare IP-, virtueel netwerk en NIC.

    ```powershell
    $publicIp = New-AzureRmPublicIpAddress -Name ($VirtualMachineName.ToLower()+'_ip') '
    -ResourceGroupName $resourceGroupName -Location $location -AllocationMethod Dynamic
    
    $vnet = Get-AzureRmVirtualNetwork -Name $virtualNetworkName -ResourceGroupName $resourceGroupName
    
    $nic = New-AzureRmNetworkInterface -Name ($VirtualMachineName.ToLower()+'_nic') '
    -ResourceGroupName $resourceGroupName -Location $location -SubnetId $vnet.Subnets[0].Id '
    -PublicIpAddressId $publicIp.Id
    
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $nic.Id
    
    New-AzureRmVM -VM $VirtualMachine -ResourceGroupName $resourceGroupName -Location $location
    ```

> [!NOTE]
>Mogelijk zijn er extra stappen nodig toosupport uw toepassing die niet worden gedekt door deze handleiding.
>
>

## <a name="next-steps"></a>Volgende stappen

- Verbinding maken met toohello virtuele machine. Zie voor instructies [hoe tooconnect en aanmelden tooan Azure virtuele machine met Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

