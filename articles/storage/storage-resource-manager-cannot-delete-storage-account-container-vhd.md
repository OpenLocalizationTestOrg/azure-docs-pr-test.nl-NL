---
title: aaaTroubleshoot fouten wanneer u Azure storage-accounts, containers of VHD's verwijderen | Microsoft Docs
description: Fouten oplossen wanneer u Azure storage-accounts, containers of VHD's verwijderen
services: storage
documentationcenter: 
author: genlin
manager: cshepard
editor: na
tags: storage
ms.assetid: 17403aa1-fe8d-45ec-bc33-2c0b61126286
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 77361593e2c924d39aba853e0807dc3188f50e60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-errors-when-you-delete-azure-storage-accounts-containers-or-vhds"></a>Fouten oplossen wanneer u Azure storage-accounts, containers of VHD's verwijderen

U bijvoorbeeld fouten ontvangt wanneer u toodelete een Azure storage-account, container of virtuele harde schijf (VHD probeert) in Hallo [Azure-portal](https://portal.azure.com). Dit artikel bevat richtlijnen toohelp los Hallo probleem in een Azure Resource Manager-implementatie op te lossen.

Als u dit artikel niet van toepassing uw Azure probleem, gaat u naar Azure-forums op Hallo [MSDN en Stack Overflow](https://azure.microsoft.com/support/forums/). U kunt het probleem op deze forums boeken of too@AzureSupport op Twitter. U kunt ook een ondersteuning van Azure-aanvraag indienen door te selecteren **ondersteuning krijgen** op Hallo [ondersteuning van Azure](https://azure.microsoft.com/support/options/) site.

## <a name="symptoms"></a>Symptomen
### <a name="scenario-1"></a>Scenario 1
Wanneer u een VHD in een opslagaccount in de implementatie van een Resource Manager toodelete, ontvangen Hallo volgende foutbericht weergegeven:

**Kan geen toodelete blob 'vhds/BlobName.vhd'. Fout: Er is momenteel een lease op Hallo blob en geen lease-ID is opgegeven in Hallo-aanvraag.**

Dit probleem kan optreden omdat een virtuele machine (VM) een lease op Hallo heeft dat u toodelete probeert VHD.

### <a name="scenario-2"></a>Scenario 2
Wanneer u een container in een opslagaccount in de implementatie van een Resource Manager toodelete probeert, ontvangen Hallo volgende foutbericht weergegeven:

**Kan geen VHD-container 'toodelete opslag's '. Fout: Er is momenteel een lease op Hallo-container en geen lease-ID is opgegeven in Hallo-aanvraag.**

Dit probleem kan optreden omdat het Hallo-container is een VHD die is vergrendeld in Hallo lease staat.

### <a name="scenario-3"></a>Scenario 3
Wanneer u een opslagaccount in de implementatie van een Resource Manager toodelete, ontvangen Hallo volgende foutbericht weergegeven:

**Kan geen toodelete storage-account 'StorageAccountName'. Fout: Hallo storage-account kan niet worden verwijderd vanwege tooits artefacten die in gebruik.**

Dit probleem kan optreden omdat het Hallo-opslagaccount bevat een VHD die Hallo lease status heeft.

## <a name="solution"></a>Oplossing 
tooresolve deze problemen, moet u vaststellen Hallo VHD die Hallo fout veroorzaakt en Hallo VM gekoppeld. Vervolgens loskoppelen Hallo VHD van Hallo VM (voor gegevensschijven) of verwijderen Hallo VM die van Hallo VHD (voor OS-schijven gebruikmaakt). Dit Hallo lease verwijdert uit Hallo VHD en toestaat dat deze toobe verwijderd. 

toodo dit, gebruik een van de volgende methoden Hallo:

### <a name="method-1---use-azure-storage-explorer"></a>Methode 1 - gebruik Azure Opslagverkenner

### <a name="step-1-identify-hello-vhd-that-prevent-deletion-of-hello-storage-account"></a>Stap 1 identificeren Hallo VHD die voorkomen dat Hallo storage-account wordt verwijderd

1. Wanneer u Hallo storage-account verwijdert, ontvangt u een dialoogvenster weergegeven zoals Hallo volgende: 

    ![bericht wanneer het Hallo-storage-account verwijderen](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. Controleer de Hallo **schijf URL** tooidentify Hallo storage-account en Hallo VHD waardoor het Hallo-opslagaccount verwijderen. Hallo in Hallo voorbeeld te volgen, tekenreeks vóór '. blob.core.windows.net ' hello opslagaccountnaam is en 'SCCM2012-2015-08-28.vhd' hello VHD-naam.  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

### <a name="step-2-delete-hello-vhd-by-using-azure-storage-explorer"></a>Stap 2 Hallo VHD verwijderen met behulp van Azure Storage Explorer

1. Download en installeer Hallo meest recente versie van [Azure Opslagverkenner](http://storageexplorer.com/). Dit hulpprogramma is een zelfstandige app van Microsoft waarmee u tooeasily werken met Azure Storage-gegevens op Windows, Mac OS- en Linux.
2. Open Azure Storage Explorer, selecteer ![pictogram](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/account.png) Selecteer uw Azure-omgeving op Hallo linkerbalk en vervolgens weer aanmelden.

3. Selecteer alle abonnementen of Hallo-abonnement dat Hallo storage-account dat u wilt dat toodelete bevat.

    ![Abonnement toevoegen](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/addsub.png)

4. Ga toohello storage-account die wordt verkregen door Hallo schijf URL eerdere, selecteer Hallo **Blob-Containers** > **VHD's** en zoek naar Hallo VHD die u niet kunt verwijderen Hallo storage-account.
5. Als Hallo VHD wordt gevonden, controleert u Hallo **VM-naam** kolom toofind Hallo VM die van deze VHD gebruikmaakt.

    ![Controleer de virtuele machine](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/check-vm.png)

6. Hallo lease van Hallo VHD verwijderen met behulp van Azure-portal. Zie voor meer informatie [verwijderen Hallo lease van Hallo VHD](#remove-the-lease-from-the-vhd). 

7. Ga toohello Azure Storage Explorer, met de rechtermuisknop op Hallo VHD en selecteer verwijderen.

8. Hallo storage-account verwijderen.

### <a name="method-2---use-azure-portal"></a>Methode 2: gebruik Azure-portal 

#### <a name="step-1-identify-hello-vhd-that-prevent-deletion-of-hello-storage-account"></a>Stap 1: Identificeren Hallo VHD die voorkomen dat Hallo storage-account wordt verwijderd

1. Wanneer u Hallo storage-account verwijdert, ontvangt u een dialoogvenster weergegeven zoals Hallo volgende: 

    ![bericht wanneer het Hallo-storage-account verwijderen](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. Controleer de Hallo **schijf URL** tooidentify Hallo storage-account en Hallo VHD waardoor het Hallo-opslagaccount verwijderen. Hallo in Hallo voorbeeld te volgen, tekenreeks vóór '. blob.core.windows.net ' hello opslagaccountnaam is en 'SCCM2012-2015-08-28.vhd' hello VHD-naam.  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

2. Meld u aan toohello [Azure-portal](https://portal.azure.com).
3. Selecteer op de Hub-menu Hallo **alle resources**. Ga toohello storage-account en selecteer vervolgens **Blobs** > **VHD's**.

    ![Schermopname van het Hallo-portal, met het Hallo-opslagaccount en Hallo "VHD" container gemarkeerd](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/opencontainer.png)

4. Zoek Hallo VHD die we eerder van Hallo schijf URL hebt verkregen. Vervolgens bepalen welke VM maakt gebruik van Hallo VHD. Meestal kunt u bepalen welk VM Hallo VHD door het controleren van de naam van de VHD Hallo bevat:

Virtuele machine in een model voor Resource Manager-ontwikkeling

   * OS-schijven in het algemeen volgt u deze naamconventie: VMName-jjjj-MM-DD-HHMMSS.vhd
   * Gegevensschijven in het algemeen volgt u deze naamconventie: VMName-jjjj-MM-DD-HHMMSS.vhd

Virtuele machine in het model van de ontwikkeling klassiek

   * OS-schijven in het algemeen volgt u deze naamconventie: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd
   * Gegevensschijven in het algemeen volgt u deze naamconventie: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd

#### <a name="step-2-remove-hello-lease-from-hello-vhd"></a>Stap 2: Hallo lease uit Hallo VHD verwijderen

[Hallo lease verwijderen uit Hallo VHD](#remove-the-lease-from-the-vhd), en verwijder vervolgens Hallo storage-account.

## <a name="what-is-a-lease"></a>Wat is een lease?
Een lease is een vergrendeling die gebruikt toocontrol toegang tooa-blob (bijvoorbeeld een VHD worden kan). Als de lease van een blob toegang alleen Hallo eigenaars van de lease Hallo Hallo blob. Een lease is belangrijk voor Hallo volgende redenen:

* Deze voorkomt dat gegevensbeschadiging als meerdere eigenaren toowrite toohello probeert hetzelfde deel van de Hallo blob op Hallo hetzelfde moment.
* Dit voorkomt dat Hallo blob wordt verwijderd als er iets actief gebruikt wordt (bijvoorbeeld een VM).
* Dit voorkomt dat Hallo storage-account wordt verwijderd als er iets actief gebruikt wordt (bijvoorbeeld een VM).

### <a name="remove-hello-lease-from-hello-vhd"></a>Hallo lease uit Hallo VHD verwijderen
Als een besturingssysteemschijf is Hallo VHD, moet u Hallo VM tooremove Hallo lease verwijderen:

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Op Hallo **Hub** selecteert u **virtuele Machines**.
3. Hallo VM waarin een lease op Hallo VHD selecteren.
4. Zorg ervoor dat er niets is actief Hallo virtuele machine, en dat u niet langer nodig Hallo virtuele machine.
5. Hallo boven aan het Hallo **VM details** blade Selecteer **verwijderen**, en klik vervolgens op **Ja** tooconfirm.
6. Hallo VM moet worden verwijderd, maar Hallo VHD kan worden bewaard. Hallo VHD mag niet langer een lease hebben erop. Het kan enkele minuten duren voordat Hallo lease toobe uitgebracht. tooverify die lease Hallo wordt uitgebracht, gaat u te**alle resources** > **Opslagaccountnaam** > **Blobs**  >  **VHD's**. In Hallo **Blob-eigenschappen** deelvenster, Hallo **Lease Status** waarde moet **ontgrendeld**.

Ontkoppel de Hallo VHD van Hallo VM tooremove Hallo lease als een gegevensschijf Hallo VHD is:

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Op Hallo **Hub** selecteert u **virtuele Machines**.
3. Hallo VM waarin een lease op Hallo VHD selecteren.
4. Selecteer **schijven** op Hallo **VM details** blade.
5. Hallo-gegevensschijf waarin een lease op Hallo VHD selecteren. Kunt u bepalen welk VHD is gekoppeld Hallo schijf door te controleren URL Hallo Hallo VHD.
6. Bepalen met zekerheid dat niets Hallo gegevensschijf actief wordt gebruikt.
7. Klik op **Detach** op Hallo **schijf details** blade.
8. Hallo-schijf moet nu worden ontkoppeld van Hallo VM en Hallo VHD moet niet langer een lease erop. Het kan enkele minuten duren voordat Hallo lease toobe uitgebracht. tooverify die lease Hallo is vrijgegeven, gaat u te**alle resources** > **Opslagaccountnaam** > **Blobs**  >  **VHD's**. In Hallo **Blob-eigenschappen** deelvenster, Hallo **Lease Status** waarde moet **ontgrendeld**.

## <a name="next-steps"></a>Volgende stappen
* [Een opslagaccount verwijderen](storage-create-storage-account.md#delete-a-storage-account)
* [Hoe toobreak Hallo lease van blob storage vergrendeld in Microsoft Azure (PowerShell)](https://gallery.technet.microsoft.com/scriptcenter/How-to-break-the-locked-c2cd6492)
