---
title: aaaCreate en het uploaden van een virtuele machine een installatiekopie met behulp van Powershell | Microsoft Docs
description: Informatie over toocreate en uploaden van een algemene Windows Server-installatiekopie (VHD) met het klassieke implementatiemodel Hallo en Azure Powershell.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8c4a08fe-7714-4bf0-be87-c728a7806d3f
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: 093b57c9157cea5f348c8ba02b5700c917adbcdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-a-windows-server-vhd-tooazure"></a>Maken en uploaden van een Windows Server-VHD tooAzure
Dit artikel laat zien hoe tooupload uw eigen gegeneraliseerde VM afbeelding als een virtuele harde schijf (VHD) zodat u toocreate virtuele machines kunt gebruiken. Zie voor meer informatie over schijven en VHD's in Microsoft Azure [over schijven en virtuele harde schijven voor virtuele Machines](../about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

> [!IMPORTANT]
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken. U kunt ook [uploaden](../upload-generalized-managed.md) Hallo Resource Manager-model met een virtuele machine.

## <a name="prerequisites"></a>Vereisten
In dit artikel wordt ervan uitgegaan dat u hebt:

* **Een Azure-abonnement** -als u niet hebt, kunt u [gratis een Azure-account openen](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).
* **[Microsoft Azure PowerShell](/powershell/azure/overview)**  -u hebt Hallo Microsoft Azure PowerShell-module geïnstalleerd en geconfigureerd toouse uw abonnement.
* **A. VHD-bestand** - ondersteunde Windows-besturingssysteem die zijn opgeslagen in een VHD-bestand en de gekoppelde tooa virtuele machine. Controleer de toosee als Hallo-serverfuncties op Hallo VHD uitgevoerd worden ondersteund door Sysprep. Zie voor meer informatie [Sysprep-ondersteuning voor serverrollen](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).

    > [!IMPORTANT]
    > Hallo VHDX-indeling wordt niet ondersteund in Microsoft Azure. U kunt converteren Hallo tooVHD schijfindeling met Hyper-V-beheer of Hallo [cmdlet Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx). Zie voor meer informatie dit [blogbericht](http://blogs.msdn.com/b/virtual_pc_guy/archive/2012/10/03/using-powershell-to-convert-a-vhd-to-a-vhdx.aspx).

## <a name="step-1-prep-hello-vhd"></a>Stap 1: Prep Hallo VHD
Voordat u Hallo VHD tooAzure uploadt, moet deze toobe gegeneraliseerd met Sysprep-hulpprogramma Hallo. Hallo VHD toobe gebruikt als een afbeelding wordt voorbereid. Zie voor meer informatie over Sysprep [hoe tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx). Back-up Hallo VM voordat Sysprep wordt uitgevoerd.

Van Hallo virtuele machine die Hallo besturingssysteem is geïnstalleerd voor Hallo na procedure te voltooien:

1. Meld u aan toohello-besturingssysteem.
2. Open een opdrachtpromptvenster als administrator. Hallo directory ook wijzigen**%windir%\system32\sysprep**, en voer vervolgens `sysprep.exe`.

    ![Open een opdrachtpromptvenster](./media/createupload-vhd/sysprep_commandprompt.png)
3. Hallo **hulpprogramma voor systeemvoorbereiding** dialoogvenster wordt weergegeven.

   ![Sysprep starten](./media/createupload-vhd/sysprepgeneral.png)
4. In Hallo **hulpprogramma voor systeemvoorbereiding**, selecteer **Voer System Out of Box Experience (OOBE)** en zorg ervoor dat **Generalize** is ingeschakeld.
5. In **afsluitopties**, selecteer **afsluiten**.
6. Klik op **OK**.

## <a name="step-2-create-a-storage-account-and-a-container"></a>Stap 2: Een opslagaccount en een container maken
U moet een opslagaccount in Azure, zodat u een plaats tooupload Hallo .vhd-bestand hebt. In deze stap ziet u hoe Hallo info toocreate een account of get moet u van een bestaande account. Vervang Hallo variabelen in &lsaquo; haken &rsaquo; met uw eigen gegevens.

1. Aanmelden

    ```powershell
    Add-AzureAccount
    ```

2. Stel uw Azure-abonnement.

    ```powershell
    Select-AzureSubscription -SubscriptionName <SubscriptionName>
    ```

3. Maak een nieuw opslagaccount. Hallo-naam van Hallo storage-account moet uniek zijn, 3 tot 24 tekens. Hallo-naam mag een combinatie van letters en cijfers. U moet ook een locatie zoals 'Oost ons' toospecify

    ```powershell
    New-AzureStorageAccount –StorageAccountName <StorageAccountName> -Location <Location>
    ```

4. Nieuw opslagaccount Hallo als Hallo standaard instellen.

    ```powershell
    Set-AzureSubscription -CurrentStorageAccountName <StorageAccountName> -SubscriptionName <SubscriptionName>
    ```

5. Maak een nieuwe container.

    ```powershell
    New-AzureStorageContainer -Name <ContainerName> -Permission Off
    ```

## <a name="step-3-upload-hello-vhd-file"></a>Stap 3: Hallo .vhd-bestand uploaden
Gebruik Hallo [Add-AzureVhd](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevhd) tooupload Hallo VHD.

Van hello Azure PowerShell-venster u in de vorige stap Hallo gebruikt type Hallo volgende opdracht en vervangt Hallo variabelen in &lsaquo; haken &rsaquo; met uw eigen gegevens.

```powershell
Add-AzureVhd -Destination "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -LocalFilePath <LocalPathtoVHDFile>
```

## <a name="step-4-add-hello-image-tooyour-list-of-custom-images"></a>Stap 4: Hallo afbeeldingenlijst tooyour van aangepaste installatiekopieën toevoegen
Gebruik Hallo [toevoegen AzureVMImage](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevmimage) cmdlet tooadd hello toohello lijst met afbeeldingen van aangepaste installatiekopieën.

```powershell
Add-AzureVMImage -ImageName <ImageName> -MediaLocation "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -OS "Windows"
```

## <a name="next-steps"></a>Volgende stappen
U kunt nu [maken van een aangepaste VM](createportal.md) u geüpload met behulp van Hallo installatiekopie.
