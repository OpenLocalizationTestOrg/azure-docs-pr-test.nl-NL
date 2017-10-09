---
title: verwijderen van Azure storage-accounts, containers of VHD's in een klassieke implementatie aaaTroubleshoot | Microsoft Docs
description: Verwijderen van Azure storage-accounts, containers of VHD's in een klassieke implementatie oplossen
services: storage
documentationcenter: 
author: genlin
manager: felixwu
editor: tysonn
tags: storage
ms.assetid: 0f7a8243-d8dc-432a-9d37-1272a0cb3a5c
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 6bbfa032e1968718c623227bb426d553e2951075
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deleting-azure-storage-accounts-containers-or-vhds-in-a-classic-deployment"></a>Verwijderen van Azure storage-accounts, containers of VHD's in een klassieke implementatie oplossen
[!INCLUDE [storage-selector-cannot-delete-storage-account-container-vhd](../../includes/storage-selector-cannot-delete-storage-account-container-vhd.md)]

Er kunnen fouten optreden wanneer u toodelete hello Azure storage-account, container of VHD in Hallo probeert [Azure-portal](https://portal.azure.com/) of Hallo [klassieke Azure-portal](https://manage.windowsazure.com/). Hallo problemen kunnen zijn veroorzaakt door Hallo volgende omstandigheden:

* Wanneer u een virtuele machine verwijdert, Hallo schijf en de VHD niet automatisch verwijderd. Die mogelijk Hallo reden voor fout van storage-account verwijderen. We kunt Hallo schijf niet verwijderen, zodat u Hallo schijf toomount een andere virtuele machine kunt.
* Er is nog steeds een lease op een schijf of Hallo blob die is gekoppeld aan het Hallo-schijf.
* Er is nog steeds een VM-installatiekopie die een blob-container of storage-account wordt gebruikt.

Als uw Azure probleem niet wordt besproken in dit artikel, gaat u naar Azure-forums op Hallo [MSDN en Hallo Stack Overflow](https://azure.microsoft.com/support/forums/). U kunt het probleem op deze forums boeken of too@AzureSupport op Twitter. U kunt ook een ondersteuning van Azure-aanvraag indienen door te selecteren **ondersteuning krijgen** op Hallo [ondersteuning van Azure](https://azure.microsoft.com/support/options/) site.

## <a name="symptoms"></a>Symptomen
Hallo volgende sectie bevat algemene fouten die wordt weergegeven mogelijk wanneer u toodelete hello Azure storage-accounts, containers of VHD's probeert.

### <a name="scenario-1-unable-toodelete-a-storage-account"></a>Scenario 1: Kan geen toodelete storage-account
Wanneer u toohello klassieke storage-account in Hallo navigeert [Azure-portal](https://portal.azure.com/) en selecteer **verwijderen**, worden weergegeven met een lijst met objecten die verhinderen het verwijderen van opslagaccount Hallo dat:

  ![Afbeelding van de fout als het verwijderen van opslagaccount Hallo](./media/storage-cannot-delete-storage-account-container-vhd/newerror.png)

Wanneer u toohello storage-account in Hallo navigeert [klassieke Azure-portal](https://manage.windowsazure.com/) en selecteer **verwijderen**, ziet u mogelijk een Hallo volgende fouten:

- *Opslagaccount StorageAccountName bevat VM-installatiekopieën. Zorg ervoor dat deze VM-installatiekopieën zijn verwijderd voordat u dit opslagaccount verwijdert.*

- *Kan geen toodelete storage-account < vm-opslag-account-name >. Kan geen toodelete storage-account < vm-opslag-account-name >: "Storage-account < vm-opslag-account-name > heeft een aantal actieve installatiekopieën en/of de schijven. Zorg ervoor dat deze installatiekopieën en/of een of meer schijven zijn verwijderd voordat u dit opslagaccount verwijdert.'.*

- *Storage-account < vm-opslag-account-name > heeft een aantal actieve installatiekopieën en/of schijven, bijvoorbeeld xxxxxxxxx-xxxxxxxxx-O-209490240936090599. Zorg ervoor dat deze installatiekopieën en/of een of meer schijven zijn verwijderd voordat u dit opslagaccount verwijdert.*

- *Storage-account < vm-opslag-account-name > heeft 1 container (s) waarvoor een actieve installatiekopie en/of de schijf artefacten. Zorg ervoor dat deze artefacten zijn verwijderd uit het Hallo-opslagplaats voor installatiekopieën voordat u dit opslagaccount verwijdert*.

- *Verzenden is mislukt Storage-account < vm-opslag-account-name > is 1 container (s) waarvoor een actieve installatiekopie en/of de schijf artefacten. Zorg ervoor dat deze artefacten zijn verwijderd uit het Hallo-opslagplaats voor installatiekopieën voordat u dit opslagaccount verwijdert. Als u een opslagaccount toodelete probeert en er nog steeds actief schijven die zijn gekoppeld zijn, ziet u een bericht dat u er nog actieve schijven die toobe verwijderd moeten*.

### <a name="scenario-2-unable-toodelete-a-container"></a>Scenario 2: Kan geen toodelete een container
Wanneer u toodelete Hallo storage-container, ziet u mogelijk Hallo volgende fout:

*Mislukte toodelete storage-container <container name>. Fout: "Er is momenteel een lease op Hallo-container en geen lease-ID is opgegeven in de aanvraag Hallo*.

of

*Hallo schijven op virtuele machine na blobs in deze container gebruiken, zodat het Hallo-container kan niet worden verwijderd: VirtualMachineDiskName1, VirtualMachineDiskName2,...*

### <a name="scenario-3-unable-toodelete-a-vhd"></a>Scenario 3: Kan geen toodelete een VHD
Nadat u een virtuele machine verwijderen en vervolgens probeert toodelete Hallo blobs voor Hallo VHD's gekoppeld, kan Hallo volgende bericht weergegeven:

*Mislukte toodelete blob ' pad/XXXXXX-XXXXXX-os-1447379084699.vhd'. Fout: "Er is momenteel een lease op Hallo blob en geen lease-ID is opgegeven in Hallo-aanvraag.*

of

*BLOB 'BlobName.vhd' is in gebruik als de schijf van de virtuele machine 'VirtualMachineDiskName' hello blob kan niet worden verwijderd.*

## <a name="solution"></a>Oplossing
meest voorkomende problemen tooresolve hello, proberen Hallo methode te volgen:

### <a name="step-1-delete-any-disks-that-are-preventing-deletion-of-hello-storage-account-container-or-vhd"></a>Stap 1: Geen schijven die verhinderen het verwijderen van opslagaccount hello, container of VHD dat verwijderen
1. Overschakelen van toohello [klassieke Azure-portal](https://manage.windowsazure.com/).
2. Selecteer **virtuele MACHINE** > **schijven**.

    ![Afbeelding van schijven op virtuele machines in de klassieke Azure-portal.](./media/storage-cannot-delete-storage-account-container-vhd/VMUI.png)
3. Hallo-schijven die gekoppeld aan Hallo storage-account, container of VHD zijn die u wilt dat toodelete vinden. Wanneer u de locatie van de schijf Hallo Hallo controleert, vindt u Hallo storage-account-container of VHD die is gekoppeld.

    ![Afbeelding die laat zien van locatiegegevens voor schijven in de klassieke Azure-portal](./media/storage-cannot-delete-storage-account-container-vhd/DiskLocation.png)
4. Hallo schijven verwijderen met behulp van een van de volgende methoden Hallo:

  - Als er geen virtuele machine moet worden weergegeven op Hallo **aangesloten op** veld van Hallo schijf, kunt u rechtstreeks Hallo schijf verwijderen.

  - Als het Hallo-schijf is een gegevensschijf, volg deze stappen:

    1. Controleer de naam van de Hallo Hallo VM die Hallo schijf is gekoppeld aan.
    2. Ga te**virtuele Machines** > **exemplaren**, en ga vervolgens naar Hallo VM.
    3. Zorg ervoor dat er niets is actief Hallo schijf.
    4. Selecteer **schijf loskoppelen** onderaan Hallo Hallo portal toodetach Hallo schijf.
    5. Ga te**virtuele Machines** > **schijven**, en wachten op Hallo **aangesloten op** veld tooturn leeg. Hiermee wordt aangegeven met het Hallo-schijf met succes is losgekoppeld van Hallo VM.
    6. Selecteer **verwijderen** Hallo onderaan in **virtuele Machines** > **schijven** toodelete Hallo schijf.

  - Als de schijf Hallo een besturingssysteemschijf (Hallo **bevat OS** veld heeft een waarde zoals Windows) en gekoppelde tooa VM, als volgt te werk toodelete Hallo VM. Hallo besturingssysteemschijf kan niet worden ontkoppeld zodat we toodelete Hallo VM toorelease Hallo lease hebben.

    1. Controleer de naam van de Hallo Hallo virtuele Machine Hallo die gegevensschijf is gekoppeld aan.  
    2. Ga te**virtuele Machines** > **exemplaren**, en vervolgens selecteert Hallo VM die Hallo schijf is gekoppeld aan.
    3. Zorg ervoor dat er niets is actief Hallo virtuele machine, en dat u niet langer nodig Hallo virtuele machine.
    4. Selecteer Hallo VM Hallo schijf is gekoppeld aan, schakelt u **verwijderen** > **verwijderen Hallo gekoppelde schijven**.
    5. Ga te**virtuele Machines** > **schijven**, en wachten op Hallo schijf toodisappear.  Het kan enkele minuten duren voordat deze toooccur en moet u mogelijk toorefresh Hallo pagina.
    6. Als het Hallo-schijf niet verdwijnt, wacht u totdat Hallo **aangesloten op** veld tooturn leeg. Hiermee wordt aangegeven Hallo schijf volledig is losgekoppeld van Hallo VM.  Vervolgens selecteert u Hallo schijf en selecteer **verwijderen** onderaan Hallo Hallo pagina toodelete Hallo-schijf.


   > [!NOTE]
   > Als een schijf aangesloten tooa VM is, u zich niet kunnen toodelete deze. Schijven zijn asynchroon losgekoppeld van een verwijderde virtuele machine. Het duurt een paar minuten nadat Hallo VM voor deze tooclear veld van wordt verwijderd.
   >
   >


### <a name="step-2-delete-any-vm-images-that-are-preventing-deletion-of-hello-storage-account-or-container"></a>Stap 2: Verwijdert u alle VM-installatiekopieën die verhinderen verwijderen van opslagaccount Hallo of container dat
1. Overschakelen van toohello [klassieke Azure-portal](https://manage.windowsazure.com/).
2. Selecteer **virtuele MACHINE** > **INSTALLATIEKOPIEËN**, en verwijder vervolgens Hallo installatiekopieën die gekoppeld aan Hallo storage-account-container of VHD zijn.

    Daarna opnieuw toodelete Hallo storage-account-container of VHD.

> [!WARNING]
> Ervoor tooback niets worden u toosave voordat u Hallo account verwijdert. Als u een VHD, blob, table, wachtrij of bestand verwijdert, wordt deze permanent verwijderd. Zorg ervoor dat Hallo resource niet in gebruik is.
>
>

## <a name="about-hello-stopped-deallocated-status"></a>Over Hallo status gestopt (toewijzing opgeheven)
Virtuele machines die zijn gemaakt in het klassieke implementatiemodel Hallo en die gehandhaafd blijft heeft Hallo **gestopt (toewijzing opgeheven)** status op beide Hallo [Azure-portal](https://portal.azure.com/) of [klassieke Azure-portal ](https://manage.windowsazure.com/).

**Klassieke Azure-portal**:

![Gestopt (Deallocated) status voor virtuele machines in Azure portal.](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo2.png)

**Azure-portal**:

![Gestopt (toewijzing ongedaan gemaakt) status voor virtuele machines op de klassieke Azure-portal.](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo1.png)

De status 'Gestopt (toewijzing opgeheven)' versies Hallo computerresources, zoals Hallo CPU, geheugen en het netwerk. Hallo-schijven, blijven echter nog steeds behouden zodat u snel opnieuw kunt maken Hallo VM indien nodig. Deze schijven worden gemaakt op de virtuele harde schijven die worden ondersteund door Azure-opslag. Hallo storage-account heeft deze VHD's en Hallo schijven leases hebben op deze virtuele harde schijven.

## <a name="next-steps"></a>Volgende stappen
* [Een opslagaccount verwijderen](storage-create-storage-account.md#delete-a-storage-account)
