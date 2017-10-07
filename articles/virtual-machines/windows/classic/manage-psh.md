---
title: aaaManage uw virtuele machines met behulp van Azure PowerShell | Microsoft Docs
description: Meer informatie over opdrachten waarmee u tooautomate taken kunt bij het beheren van uw virtuele machines.
services: virtual-machines-windows
documentationcenter: windows
author: singhkays
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 7cdf9bd3-6578-4069-8a95-e8585f04a394
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 10/12/2016
ms.author: kasing
ms.openlocfilehash: e4ca6f098519243a321eac98b6692790fe18c22c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-virtual-machines-by-using-azure-powershell"></a>Virtuele machines beheren met Azure PowerShell
> [!IMPORTANT] 
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken. Raadpleeg voor algemene PowerShell-opdrachten met Resource Manager-model hello, [hier](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Veel taken die u elke dag toomanage uw virtuele machines kunnen worden geautomatiseerd met behulp van Azure PowerShell-cmdlets. In dit artikel krijgt u Voorbeeldopdrachten voor eenvoudigere taken en koppelingen tooarticles die Hallo-opdrachten voor complexere taken weergeven.

> [!NOTE]
> Als u dit nog niet hebt geïnstalleerd en geconfigureerd Azure PowerShell nog, kunt u de instructies op Hallo artikel opvragen [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).
> 
> 

## <a name="how-toouse-hello-example-commands"></a>Hoe toouse Voorbeeldopdrachten Hallo
U moet tooreplace deel van de tekst hello in Hallo opdrachten met de tekst die geschikt is voor uw omgeving. Hallo < en > symbolen geven aan de tekst die u moet tooreplace. Wanneer u de tekst hello vervangt, Hallo symbolen verwijderen, maar blijft de Hallo aanhalingstekens in.

## <a name="get-a-vm"></a>Een virtuele machine ophalen
Dit is een eenvoudige taak die u vaak gebruikt. Gebruik deze tooget informatie over een virtuele machine, taken uitvoeren op een virtuele machine of uitvoer toostore ophalen in een variabele.

tooget informatie over Hallo VM, deze opdracht, vervangt alles in Hallo aanhalingstekens, inclusief Hallo < en > tekens uitvoeren:

     Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

toostore hello uitvoer in een variabele $vm uitvoeren:

    $vm = Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="log-on-tooa-windows-based-vm"></a>Meld u aan tooa VM op basis van Windows
Deze opdrachten uitvoeren:

> [!NOTE]
> U krijgt Hallo virtuele machine en cloudservicenaam uit Hallo-weergave van Hallo **Get-AzureVM** opdracht.
> 
> $svcName = "<cloud service name>" $vmName = '<virtual machine name>' $localPath = "< station en de map locatie toostore Hallo gedownload RDP-bestand, bijvoorbeeld: c:\temp > ' $localFile $localPath = +"\" $vmname + ".rdp' Get-AzureRemoteDesktopFile - ServiceName $svcName-naam $vmName - LocalPath $localFile-starten
> 
> 

## <a name="stop-a-vm"></a>Een VM stoppen
Voer deze opdracht uit:

    Stop-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

> [!IMPORTANT]
> Gebruik deze parameter tookeep Hallo virtuele IP-adres (VIP) van Hallo cloud service mocht dat Hallo laatste VM in deze cloudservice. <br><br> Als u Hallo StayProvisioned parameter gebruikt, hebt u nog steeds worden gefactureerd voor Hallo VM.
> 
> 

## <a name="start-a-vm"></a>Een VM starten
Voer deze opdracht uit:

    Start-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="attach-a-data-disk"></a>Een gegevensschijf koppelen
Deze taak zijn een paar stappen vereist. Gebruik eerst Hallo *** toevoegen-AzureDataDisk *** cmdlet tooadd hello toohello $vm schijfobject. Vervolgens gebruikt u **Update-AzureVM** cmdlet tooupdate Hallo configuratie van Hallo VM.

U moet ook toodecide of tooattach een nieuwe schijf of een die bevat gegevens. Voor een nieuwe schijf Hallo opdracht Hallo .vhd-bestand gemaakt en gekoppeld.

een nieuwe schijf tooattach deze opdracht uitvoeren:

    Add-AzureDataDisk -CreateNew -DiskSizeInGB 128 -DiskLabel "<main>" -LUN <0> -VM $vm | Update-AzureVM

een bestaande gegevensschijf tooattach deze opdracht uitvoeren:

    Add-AzureDataDisk -Import -DiskName "<MyExistingDisk>" -LUN <0> | Update-AzureVM

de gegevensschijven tooattach van een bestaande VHD-bestand in blob storage, wordt deze opdracht uitvoeren:

    Add-AzureDataDisk -ImportFrom -MediaLocation `
              "<https://mystorage.blob.core.windows.net/mycontainer/MyExistingDisk.vhd>" `
              -DiskLabel "<main>" -LUN <0> |
              Update-AzureVM

## <a name="create-a-windows-based-vm"></a>Maak een VM op basis van Windows
een nieuwe Windows gebaseerde virtuele machine in Azure, gebruik Hallo instructies in toocreate [Azure PowerShell gebruiken toocreate en vooraf configureren van virtuele machines op basis van Windows](create-powershell.md). De stappen van dit onderwerp maakt u via Hallo maken van een Azure PowerShell opdracht ingesteld die een VM op basis van Windows die vooraf kan worden geconfigureerd:

* Met het lidmaatschap van de Active Directory-domein.
* Met andere schijven.
* Als een lid van een bestaande Netwerktaakverdeling instellen.
* Met een statisch IP-adres.

