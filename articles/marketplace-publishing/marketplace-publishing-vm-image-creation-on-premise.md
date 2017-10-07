---
title: een installatiekopie van een lokale virtuele machine voor hello Azure Marketplace aaaCreating | Microsoft Docs
description: Begrijpen en Hallo stappen toocreate een installatiekopie van een lokale virtuele machine uitvoeren en implementeren van toohello Azure Marketplace voor anderen toopurchase.
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 26dfbd5a-8685-4b19-987e-c20ca60540ec
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 04/29/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: c7a265330f1e494db8d0e981a38ee00d85746bb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-an-on-premises-virtual-machine-image-for-hello-azure-marketplace"></a>Ontwikkelen van een installatiekopie van een lokale virtuele machine voor hello Azure Marketplace
Het is raadzaam dat u Azure virtuele harde schijven (VHD's) rechtstreeks in de cloud Hallo ontwikkelen met behulp van Remote Desktop Protocol. Als u moet het is echter mogelijk toodownload een VHD en het ontwikkelen met behulp van on-premises infrastructuur.  

Voor lokale ontwikkeling, moet u Hallo besturingssysteem VHD Hallo gemaakt downloaden VM. Deze stappen zou worden uitgevoerd als onderdeel van de stap 3.3, hierboven.  

## <a name="download-a-vhd-image"></a>Een VHD-installatiekopie te downloaden
### <a name="locate-a-blob-url"></a>Ga naar een blob-URL
In de volgorde toodownload Hallo VHD, moet u eerst Hallo blob-URL voor de besturingssysteemschijf Hallo vinden.

Zoek Hallo blob URL uit Hallo nieuwe [Microsoft Azure-portal](https://portal.azure.com):

1. Ga te**Bladeren** > **VMs**, en selecteer vervolgens Hallo VM geïmplementeerd.
2. Onder **configureren**, selecteer Hallo **schijven** tegel, die Hallo schijven blade wordt geopend.
   
   ![tekenen](media/marketplace-publishing-vm-image-creation-on-premise/img01.png)
3. Selecteer Hallo **Besturingssysteemschijf**, waarmee u een andere blade die wordt weergegeven van de eigenschappen van de schijf, met inbegrip van de locatie van de VHD Hallo opent.
4. Kopieer deze blob-URL.
   
   ![tekenen](media/marketplace-publishing-vm-image-creation-on-premise/img02.png)
5. Verwijder nu Hallo VM geïmplementeerd zonder Hallo back-ups maken schijven te verwijderen. U kunt ook Hallo VM stoppen in plaats van te verwijderen. Besturingssysteem-VHD Hallo niet downloaden wanneer Hallo VM wordt uitgevoerd.
   
   ![tekenen](media/marketplace-publishing-vm-image-creation-on-premise/img03.png)

### <a name="download-a-vhd"></a>Een VHD downloaden
Nadat u Hallo blob URL weet, kunt u Hallo VHD downloaden met behulp van Hallo [Azure-portal](http://manage.windowsazure.com/) of PowerShell.  

> [!NOTE]
> Gelijktijdig Hallo met het maken van deze handleiding is Hallo functionaliteit toodownload een VHD nog niet aanwezig in Hallo nieuwe Microsoft Azure-portal.  
> 
> 

**Hallo besturingssysteem-VHD via Hallo huidige downloaden [Azure-portal](http://manage.windowsazure.com/)**

1. Meld u toohello Azure-portal als u dit nog niet hebt gedaan.
2. Klik op Hallo **opslag** tabblad.
3. Selecteer Hallo storage-account in welke Hallo VHD wordt opgeslagen.
   
   ![tekenen](media/marketplace-publishing-vm-image-creation-on-premise/img04.png)
4. U ziet nu eigenschappen van het opslagaccount. Selecteer Hallo **Containers** tabblad.
   
   ![tekenen](media/marketplace-publishing-vm-image-creation-on-premise/img05.png)
5. Selecteer Hallo-container in welke Hallo VHD wordt opgeslagen. Standaard wanneer gemaakt vanuit de portal Hallo Hallo VHD opgeslagen in een VHD-container.
   
   ![tekenen](media/marketplace-publishing-vm-image-creation-on-premise/img06.png)
6. Selecteer Hallo juiste besturingssysteem-VHD door te vergelijken Hallo URL toohello een die u opgeslagen.
7. Klik op **Downloaden**.
   
   ![tekenen](media/marketplace-publishing-vm-image-creation-on-premise/img07.png)

### <a name="download-a-vhd-by-using-powershell"></a>Een VHD te downloaden met behulp van PowerShell
Bovendien toousing hello Azure-portal, kunt u Hallo [opslaan AzureVhd](http://msdn.microsoft.com/library/dn495297.aspx) besturingssysteem-cmdlet toodownload Hallo VHD.

        Save-AzureVhd –Source <storageURIOfVhd> `
        -LocalFilePath <diskLocationOnWorkstation> `
        -StorageKey <keyForStorageAccount>
Bijvoorbeeld opslaan-AzureVhd-bron "https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd" - LocalFilePath 'C:\Users\Administrator\Desktop\baseimagevm.vhd' - StorageKey<String>

> [!NOTE]
> **Opslaan AzureVhd** heeft ook een **NumberOfThreads** optie die kan worden gebruikt tooincrease parallelle uitvoering toomake Hallo optimaal gebruik van de beschikbare bandbreedte voor Hallo downloaden.
> 
> 

## <a name="upload-vhds-tooan-azure-storage-account"></a>VHD's tooan Azure storage-account uploaden
Als u uw VHD's on-premises voorbereid, moet u deze in een opslag in Azure-account tooupload. Deze stap vindt plaats nadat het maken van uw VHD lokale maar voordat het verkrijgen van de certificeringsinstantie voor uw VM-installatiekopie.

### <a name="create-a-storage-account-and-container"></a>Een opslagaccount en container maken
We raden aan dat de VHD's worden geüpload naar een opslagaccount in een regio in Hallo Verenigde Staten. Alle VHD's voor een enkele SKU worden geplaatst in een enkele container binnen een enkele opslagaccount.

toocreate storage-account, kunt u Hallo [Microsoft Azure-portal](https://portal.azure.com/), PowerShell of Hallo Linux opdrachtregelhulpprogramma.  

**Een opslagaccount maken vanuit Hallo Microsoft Azure portal**

1. Klik op **Nieuw**.
2. Selecteer **opslag**.
3. Vul Hallo opslagaccountnaam en selecteer vervolgens een locatie.
   
   ![tekenen](media/marketplace-publishing-vm-image-creation-on-premise/img08.png)
4. Klik op **Create**.
5. Hallo-blade voor Hallo storage-account gemaakt is geopend. Zo niet, selecteer **Bladeren** > **Opslagaccounts**. Blade op Hallo Storage-account, selecteert u Hallo storage-account is gemaakt.
6. Selecteer **Containers**.
   
   ![tekenen](media/marketplace-publishing-vm-image-creation-on-premise/img09.png) 
7. Selecteer op de blade Containers Hallo **toevoegen**, en voer een naam en het Hallo-container machtigingen voor de computercontainer. Selecteer **persoonlijke** voor machtigingen van de container.

> [!TIP]
> U wordt aangeraden dat u een container per SKU dat u van plan bent toopublish maken.
> 
> 

  ![tekenen](media/marketplace-publishing-vm-image-creation-on-premise/img10.png)

### <a name="create-a-storage-account-by-using-powershell"></a>Een opslagaccount maken met behulp van PowerShell
Met behulp van PowerShell, een opslagaccount maken met behulp van Hallo [nieuw AzureStorageAccount](http://msdn.microsoft.com/library/dn495115.aspx) cmdlet.

        New-AzureStorageAccount -StorageAccountName “mystorageaccount” -Location “West US”

Vervolgens u een container in dat storage-account maken kunt met behulp van Hallo [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) cmdlet.

        New-AzureStorageContainer -Name “containername” -Permission “Off”

> [!NOTE]
> Deze opdrachten wordt ervan uitgegaan dat Hallo huidige storage account context is al ingesteld in PowerShell.   Raadpleeg te[instellen van Azure PowerShell](marketplace-publishing-powershell-setup.md) voor meer informatie over de installatie van PowerShell.  
> 
> ### <a name="create-a-storage-account-by-using-hello-command-line-tool-for-mac-and-linux"></a>Een opslagaccount maken met behulp van Hallo-opdrachtregelprogramma voor Mac en Linux
> Van [Linux opdrachtregelprogramma](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), als volgt een opslagaccount maken.
> 
> 

        azure storage account create mystorageaccount --location "West US"

Als volgt te werk om een container te maken.

        azure storage container create containername --account-name mystorageaccount --accountkey <accountKey>

## <a name="upload-a-vhd"></a>Een VHD uploaden
Nadat het Hallo-opslagaccount en container worden gemaakt, kunt u uw voorbereide VHD's uploaden. U kunt PowerShell, Hallo Linux opdrachtregelprogramma of andere Azure Storage management-hulpprogramma's gebruiken.

### <a name="upload-a-vhd-via-powershell"></a>Een VHD via PowerShell uploaden
Gebruik Hallo [Add-AzureVhd](http://msdn.microsoft.com/library/dn495173.aspx) cmdlet.

        Add-AzureVhd –Destination “http://mystorageaccount.blob.core.windows.net/containername/vmsku.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\vmsku.vhd”

### <a name="upload-a-vhd-by-using-hello-command-line-tool-for-mac-and-linux"></a>Een VHD uploaden met Hallo-opdrachtregelprogramma voor Mac en Linux
Hello [Linux opdrachtregelprogramma](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2), gebruikt u de volgende Hallo: azure vm-installatiekopie maken <image name> --locatie <Location of hello data center> --OS Linux<LocationOfLocalVHD>

## <a name="see-also"></a>Zie ook
* [Maken van de installatiekopie van een virtuele machine voor Hallo Marketplace](marketplace-publishing-vm-image-creation.md)
* [Instellen van Azure PowerShell](marketplace-publishing-powershell-setup.md)

