---
title: aaaUpload VHD-bestand tooAzure DevTest Labs met behulp van PowerShell | Microsoft Docs
description: Uploaden van de VHD-bestand toolab storage-account met behulp van PowerShell
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
ms.openlocfilehash: 9c3ee96e212457b0ef8203714b419350cb97f895
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-powershell"></a>Uploaden van de VHD-bestand toolab storage-account met behulp van PowerShell

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

VHD-bestanden kunnen gebruikte toocreate aangepaste installatiekopieën die gebruikt tooprovision virtuele machines zijn worden in Azure DevTest Labs. Hallo doorlopen volgende stappen met behulp van PowerShell tooupload een VHD-bestand tooa lab-opslagaccount. Nadat u uw VHD-bestand hebt geüpload, Hallo [Vervolgstappen sectie](#next-steps) bevat enkele artikelen die aangeven hoe een aangepaste installatiekopie van Hallo toocreate VHD-bestand geüpload. Zie voor meer informatie over schijven en VHD's in Azure [over schijven en virtuele harde schijven voor virtuele machines](../virtual-machines/linux/about-disks-and-vhds.md)

## <a name="step-by-step-instructions"></a>Stapsgewijze instructies

Hallo volgende stappen walk u via een VHD uploaden bestand tooAzure DevTest Labs met behulp van PowerShell. 

1. Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Selecteer **meer services**, en selecteer vervolgens **DevTest Labs** uit Hallo-lijst.

1. Selecteer de gewenste lab Hallo in lijst Hallo van labs.  

1. Selecteer op Hallo van labblade, **configuratie**. 

1. Op Hallo lab **configuratie** blade Selecteer **aangepaste installatiekopieën (VHD's)**.

1. Op Hallo **aangepaste installatiekopieën** blade Selecteer **+ toevoegen**. 

1. Op Hallo **aangepaste installatiekopie** blade Selecteer **VHD**.

1. Op Hallo **VHD** blade Selecteer **een VHD uploaden met PowerShell**.

    ![Virtuele harde schijf met behulp van PowerShell geüpload](./media/devtest-lab-upload-vhd-using-powershell/upload-image-using-psh.png)

1. Op Hallo **een installatiekopie uploaden met PowerShell** blade, kopie Hallo gegenereerd PowerShell script tooa teksteditor.

1. Hallo wijzigen **LocalFilePath** parameter Hallo **Add-AzureVhd** cmdlet toopoint toohello locatie Hallo gewenste tooupload VHD-bestand.

1. Uitvoeren op een PowerShell-prompt Hallo **Add-AzureVhd** cmdlet (Hello gewijzigd **LocalFilePath** parameter).

> [!WARNING] 
> 
> Hallo-proces van het uploaden van een VHD-bestand kan worden langdurige, afhankelijk van de grootte van de Hallo van Hallo VHD-bestand en de verbindingssnelheid.

## <a name="next-steps"></a>Volgende stappen

- [Een aangepaste installatiekopie maken in Azure DevTest Labs van een VHD-bestand met behulp van hello Azure-portal](devtest-lab-create-template.md)
- [Een aangepaste installatiekopie maken in Azure DevTest Labs van een VHD-bestand met behulp van PowerShell](devtest-lab-create-custom-image-from-vhd-using-powershell.md)
