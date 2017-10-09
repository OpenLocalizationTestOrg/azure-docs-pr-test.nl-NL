---
title: aaaUpload VHD-bestand met behulp van AzCopy van tooAzure DevTest Labs | Microsoft Docs
description: Uploaden van de VHD-bestand toolab storage-account met behulp van AzCopy
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 14f9e933b0bd27451f6bcb94841ecc381213e578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-azcopy"></a>Uploaden van de VHD-bestand toolab storage-account met behulp van AzCopy

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

VHD-bestanden kunnen gebruikte toocreate aangepaste installatiekopieën die gebruikt tooprovision virtuele machines zijn worden in Azure DevTest Labs. Hallo stappen doorlopen met behulp van Hallo AzCopy-opdrachtregelprogramma tooupload een VHD-bestand tooa lab-opslagaccount. Nadat u uw VHD-bestand hebt geüpload, Hallo [Vervolgstappen sectie](#next-steps) bevat enkele artikelen die aangeven hoe een aangepaste installatiekopie van Hallo toocreate VHD-bestand geüpload. Zie voor meer informatie over schijven en VHD's in Azure [over schijven en virtuele harde schijven voor virtuele machines](../virtual-machines/linux/about-disks-and-vhds.md)

> [!NOTE] 
>  
> AzCopy is een alleen-Windows-opdrachtregelprogramma.

## <a name="step-by-step-instructions"></a>Stapsgewijze instructies

volgende stappen walk u via een VHD uploaden bestand tooAzure DevTest Labs met Hallo [AzCopy](http://aka.ms/downloadazcopy). 

1. Hallo-naam van de storage-account van het lab Hallo hello Azure-portal met opvragen:

1. Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Selecteer **meer services**, en selecteer vervolgens **DevTest Labs** uit Hallo-lijst.

1. Selecteer de gewenste lab Hallo in lijst Hallo van labs.  

1. Selecteer op Hallo van labblade, **configuratie**. 

1. Op Hallo lab **configuratie** blade Selecteer **aangepaste installatiekopieën (VHD's)**.

1. Op Hallo **aangepaste installatiekopieën** blade Selecteer **+ toevoegen**. 

1. Op Hallo **aangepaste installatiekopie** blade Selecteer **VHD**.

1. Op Hallo **VHD** blade Selecteer **een VHD uploaden met PowerShell**.

    ![Virtuele harde schijf met behulp van PowerShell geüpload](./media/devtest-lab-upload-vhd-using-azcopy/upload-image-using-psh.png)

1. Hallo **een installatiekopie uploaden met PowerShell** blade wordt een aanroep van toohello **Add-AzureVhd** cmdlet. de eerste parameter Hallo (*bestemming*) bevat Hallo URI voor een blob-container (*uploadt*) in de volgende indeling Hallo:

    ```
    https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...
    ``` 

1. Noteer Hallo volledige URI omdat deze wordt gebruikt in latere stappen.

1. Hallo VHD-bestand met behulp van AzCopy uploaden:
 
1. [Download en installeer de meest recente versie van AzCopy hello](http://aka.ms/downloadazcopy).

1. Open een opdrachtvenster en navigeer toohello AzCopy-installatiemap. U kunt eventueel Hallo AzCopy locatie tooyour system installatiepad toevoegen. AzCopy is standaard geïnstalleerd toohello directory te volgen:

    ```command-line
    %ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy
    ```

1. Hallo volgende opdracht achter de opdrachtprompt Hallo Hallo storage account sleutel en de blob-container URI gebruikt, worden uitgevoerd. Hallo *vhdFileName* waarde moet toobe tussen aanhalingstekens. Hallo-proces van het uploaden van een VHD-bestand kan worden langdurige, afhankelijk van de grootte van de Hallo van Hallo VHD-bestand en de verbindingssnelheid.   

    ```command-line
    AzCopy /Source:<sourceDirectory> /Dest:<blobContainerUri> /DestKey:<storageAccountKey> /Pattern:"<vhdFileName>" /BlobType:page
    ```

## <a name="next-steps"></a>Volgende stappen

- [Een aangepaste installatiekopie maken in Azure DevTest Labs van een VHD-bestand met behulp van hello Azure-portal](devtest-lab-create-template.md)
- [Een aangepaste installatiekopie maken in Azure DevTest Labs van een VHD-bestand met behulp van PowerShell](devtest-lab-create-custom-image-from-vhd-using-powershell.md)