---
title: een virtuele machine van Windows hello klassieke implementatiemodel - Azure aaaResize | Microsoft Docs
description: Het formaat van een virtuele Windows-machine in Hallo klassieke implementatiemodel, met Azure Powershell hebt gemaakt.
services: virtual-machines-windows
documentationcenter: 
author: Drewm3
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: e3038215-001c-406e-904d-e0f4e326a4c7
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 10/19/2016
ms.author: drewm
ms.openlocfilehash: 39fab14431e2351c9515b0611e850eccfec7a798
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-windows-vm-created-in-hello-classic-deployment-model"></a>Een Windows-VM gemaakt in het klassieke implementatiemodel Hallo vergroten of verkleinen
Dit artikel laat zien hoe tooresize een Windows-VM gemaakt in het klassieke implementatiemodel Hallo met Azure Powershell.

Als u overweegt Hallo mogelijkheid tooresize een virtuele machine, zijn er twee concepten waarmee de Hallo bereik van grootten beschikbaar tooresize Hallo virtuele machine. Hallo eerste concept is Hallo-regio waarin uw virtuele machine wordt geïmplementeerd. Hallo-lijst met VM-grootten die beschikbaar zijn in de regio is Hallo Services tabblad van hello Azure-gebieden webpagina. tweede concept Hallo is Hallo fysieke hardware momenteel als host optreedt van de VM. Hallo fysieke servers die als host fungeert voor VM's zijn gegroepeerd in clusters van algemene fysieke hardware. Hallo-methode van het wijzigen van een VM-grootte verschilt afhankelijk van of hello wordt gewenste nieuwe VM-grootte ondersteund door Hallo hardware cluster momenteel host Hallo VM.

> [!IMPORTANT] 
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken. U kunt ook [vergroten of verkleinen van een virtuele machine gemaakt in Hallo Resource Manager-implementatiemodel](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="add-your-account"></a>Uw account toevoegen
U moet Azure PowerShell toowork configureren met de klassieke Azure-resources. Hallo stappen hieronder tooconfigure Azure PowerShell toomanage klassieke resources.

1. Typ achter de PowerShell-prompt Hallo `Add-AzureAccount` en klik op **Enter**. 
2. Typ Hallo e-mailadres gekoppeld aan uw Azure-abonnement en klik op **doorgaan**. 
3. Typ in het Hallo-wachtwoord voor je account. 
4. Klik op **aanmelden**. 

## <a name="resize-in-hello-same-hardware-cluster"></a>Vergroten of verkleinen in Hallo dezelfde hardware-cluster
tooresize grootte van de VM-tooa beschikbaar in Hallo hardware cluster die als host fungeert voor Hallo VM, uitvoeren Hallo stappen te volgen.

1. Hallo volgende PowerShell-opdracht is beschikbaar in Hallo hardware cluster hostingservice Hallo cloud waarin toolist Hallo VM-grootten Hallo VM worden uitgevoerd.
   
    ```powershell
    Get-AzureService | where {$_.ServiceName -eq "<cloudServiceName>"}
    ```
2. Hallo na opdrachten tooresize Hallo VM worden uitgevoerd.
   
    ```powershell
    Get-AzureVM -ServiceName <cloudServiceName> -Name <vmName> | Set-AzureVMSize -InstanceSize <newVMSize> | Update-AzureVM
    ```

## <a name="resize-on-a-new-hardware-cluster"></a>Op een nieuwe hardware cluster vergroten of verkleinen
grootte van de VM-tooa niet beschikbaar in het Hallo hardware cluster host tooresize Hallo VM, hello cloudservice en alle virtuele machines in de cloudservice Hallo moeten opnieuw worden gemaakt. Elke cloudservice wordt gehost op een cluster met één hardware, zodat alle VM's in de cloudservice Hallo moet een grootte die wordt ondersteund op een hardware-cluster. Hallo volgende stappen wordt beschreven hoe een virtuele machine verwijderd en vervolgens opnieuw te maken van tooresize Hallo cloud service.

1. Hallo volgende PowerShell-opdracht toolist Hallo VM-grootten beschikbaar in Hallo regio worden uitgevoerd. 
   
    ```powershell
    Get-AzureLocation | where {$_.Name -eq "<locationName>"}
    ```
2. Noteer alle configuratie-instellingen voor elke virtuele machine in Hallo cloudservice waarin Hallo VM toobe is gewijzigd. 
3. Verwijder alle VM's in de cloudservice Hallo Hallo optie tooretain Hallo schijven selecteren voor elke virtuele machine.
4. Maak deze opnieuw Hallo VM toobe gewijzigd met behulp van Hallo gewenste VM-grootte.
5. Alle andere virtuele machines die zich in de Hallo cloudservice met behulp van een VM-grootte beschikbaar zijn in Hallo hardware cluster service in de cloud Hallo nu de host opnieuw.

Een voorbeeld van een script voor het verwijderen en opnieuw maken van een cloudservice met behulp van een nieuwe VM-grootte vindt [hier](https://github.com/Azure/azure-vm-scripts). 

## <a name="next-steps"></a>Volgende stappen
* [Formaat van een virtuele machine gemaakt in Hallo Resource Manager-implementatiemodel](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

