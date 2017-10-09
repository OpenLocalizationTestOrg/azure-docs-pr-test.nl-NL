---
title: aaaUpload VHD-bestand met behulp van Microsoft Azure Storage Explorer van tooAzure DevTest Labs | Microsoft Docs
description: VHD-bestand toolab storage-account met behulp van Microsoft Azure Storage Explorer uploaden
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
ms.openlocfilehash: 686691e3676cea4b2d7cd8bf045bc43a792c667e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-microsoft-azure-storage-explorer"></a>VHD-bestand toolab storage-account met behulp van Microsoft Azure Storage Explorer uploaden

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

VHD-bestanden kunnen gebruikte toocreate aangepaste installatiekopieën die gebruikt tooprovision virtuele machines zijn worden in Azure DevTest Labs. Dit artikel wordt beschreven hoe toouse [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooupload een VHD-bestand van tooa lab-opslagaccount. Nadat u uw VHD-bestand hebt geüpload, Hallo [Vervolgstappen sectie](#next-steps) bevat enkele artikelen die aangeven hoe een aangepaste installatiekopie van Hallo toocreate VHD-bestand geüpload. Zie voor meer informatie over schijven en VHD's in Azure [over schijven en virtuele harde schijven voor virtuele machines](../virtual-machines/linux/about-disks-and-vhds.md)

## <a name="step-by-step-instructions"></a>Stapsgewijze instructies

volgende stappen walk u via een VHD uploaden bestand tooDevTest Labs met Hallo [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).

1. [Download en installeer de meest recente versie van Microsoft Azure Storage Explorer Hallo Hallo](http://www.storageexplorer.com).

1. Hallo-naam van de storage-account van het lab Hallo hello Azure-portal met opvragen:

    1. Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
    
    1. Selecteer **meer services**, en selecteer vervolgens **DevTest Labs** uit Hallo-lijst.
    
    1. Selecteer de gewenste lab Hallo in lijst Hallo van labs.  
    
    1. Selecteer op Hallo van labblade, **configuratie**. 
    
    1. Op Hallo lab **configuratie** blade Selecteer **aangepaste installatiekopieën (VHD's)**.
    
    1. Op Hallo **aangepaste installatiekopieën** blade Selecteer **+ toevoegen**. 
    
    1. Op Hallo **aangepaste installatiekopie** blade Selecteer **VHD**.
    
    1. Op Hallo **VHD** blade Selecteer **een VHD uploaden met PowerShell**.
    
        ![Virtuele harde schijf met behulp van PowerShell geüpload][0]
    
    1. Hallo **een installatiekopie uploaden met PowerShell** blade wordt een aanroep van toohello **Add-AzureVhd** cmdlet. de eerste parameter Hallo (*bestemming*) opslagaccountnaam voor Hallo lab in de volgende indeling Hallo Hallo bevat:
    
        https://<STORAGE-account-name>.BLOB.Core.Windows.NET/uploads/... 

    1. Noteer de opslagaccountnaam Hallo omdat deze wordt gebruikt in latere stappen.
    
1. Verbinding maken met Azure-abonnementsrekening met Opslagverkenner tooan.

    > [!TIP] 
    > 
    > Opslagverkenner ondersteunt verschillende verbindingsopties. Deze sectie ziet u verbindende tooa storage-account die is gekoppeld aan uw Azure-abonnement. toosee andere verbindingsopties ondersteund door Opslagverkenner hello, raadpleeg dan toohello artikel [aan de slag met Opslagverkenner](../vs-azure-tools-storage-manage-with-storage-explorer.md).
 
    1. Open Opslagverkenner.
    
    1. Selecteer in Opslagverkenner **Azure Accountinstellingen**. 
    
        ![Azure-accountinstellingen][1]
    
    1. Hallo linkerdeelvenster geeft Hallo hebt aangemeld bij Microsoft-accounts. tooconnect tooanother account, selecteer **account toevoegen**, en volgt u Hallo dialoogvensters toosign met een Microsoft-account dat is gekoppeld aan ten minste één actief Azure-abonnement.
    
        ![Een account toevoegen][2]
    
    1. Zodra u zich hebt aangemeld met een Microsoft-account, het linkerdeelvenster Hallo gevuld met hello Azure-abonnementen die zijn gekoppeld aan dat account. Selecteer hello Azure-abonnementen die u wilt toowork en selecteer vervolgens **toepassen**. (Selecteren **alle abonnementen** Schakelknoppen Hallo selectie van alle of geen van hello Azure-abonnementen vermeld.)
    
        ![Selecteer Azure-abonnementen][3]
    
    1. Hallo linkerdeelvenster geeft Hallo storage-accounts die zijn gekoppeld aan Azure-abonnementen Hallo geselecteerd.
    
        ![Geselecteerde Azure-abonnementen][4]

1. Zoek de Hallo lab-opslagaccount:

    1. In Hallo Opslagverkenner linkerdeelvenster vinden en Hallo knooppunt voor hello Azure-abonnement dat eigenaar is van Hallo lab.
    
    1. Vouw onder het knooppunt van het abonnement hello, **Opslagaccounts**.

    1. Vouw Hallo van storage account knooppunt tooreveal knooppunten van het testlab voor **Blob-Containers**, **bestandsshares**, **wachtrijen**, en **tabellen**.
    
    1. Vouw Hallo **Blob-Containers** knooppunt.
    
    1. Hallo uploads blob-container toodisplay van de inhoud in het rechterdeelvenster Hallo selecteren.
        
        ![Directory uploaden][5]

1. Hallo VHD-bestand met Opslagverkenner uploaden:

    1. In Hallo Opslagverkenner rechterdeelvenster, ziet u een overzicht van de blobs in Hallo Hallo **uploadt** blob-container van het Hallo lab-opslagaccount. Selecteer op de werkbalk van Hallo blob editor **uploaden** 
        
        ![Knop uploaden][6]
    
    1. Van Hallo **uploaden** vervolgkeuzelijst, selecteer **bestanden uploaden...** .
    
    1. Op Hallo **bestanden uploaden** dialoogvenster, selecteer Hallo weglatingsteken.
        
        ![Bestand selecteren][8]  

    1. Op Hallo **Selecteer bestanden tooupload** dialoogvenster Bladeren toohello gewenst VHD-bestand en selecteer vervolgens selecteert u het **Open**.
    
    1. Wanneer geretourneerd toohello **bestanden uploaden** dialoogvenster wijziging **type Blob** te**pagina-Blob**.
    
    1. Selecteer **Uploaden**.

        ![Bestand selecteren][9]  
    
    1. Hallo Opslagverkenner **activiteitenlogboek** deelvenster Hallo downloadstatus (samen met het uploaden van koppelingen toocancel Hallo) bevat. Hallo-proces van het uploaden van een VHD-bestand kan worden langdurige, afhankelijk van de grootte van de Hallo van Hallo VHD-bestand en de verbindingssnelheid. 

        ![Uploadbestand status][10]  

## <a name="next-steps"></a>Volgende stappen

- [Een aangepaste installatiekopie maken in Azure DevTest Labs van een VHD-bestand met behulp van hello Azure-portal](devtest-lab-create-template.md)
- [Een aangepaste installatiekopie maken in Azure DevTest Labs van een VHD-bestand met behulp van PowerShell](devtest-lab-create-custom-image-from-vhd-using-powershell.md)

[0]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-image-using-psh.png
[1]: ./media/devtest-lab-upload-vhd-using-storage-explorer/settings-icon.png
[2]: ./media/devtest-lab-upload-vhd-using-storage-explorer/add-account-link.png
[3]: ./media/devtest-lab-upload-vhd-using-storage-explorer/subscriptions-list.png
[4]: ./media/devtest-lab-upload-vhd-using-storage-explorer/storage-accounts-list.png
[5]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-dir.png
[6]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-button.png
[7]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-files.png
[8]: ./media/devtest-lab-upload-vhd-using-storage-explorer/select-file.png
[9]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-file.png
[10]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-status.png
