---
title: Fouten oplossen wanneer u Azure storage-accounts, containers of VHD's verwijderen | Microsoft Docs
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
ms.openlocfilehash: 318d7146ea53a806baf813ff7de2fe91f18becc8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshoot-errors-when-you-delete-azure-storage-accounts-containers-or-vhds"></a>Fouten oplossen wanneer u Azure storage-accounts, containers of VHD's verwijderen

U kunt fouten ontvangt wanneer u probeert te verwijderen van een Azure storage-account, container of virtuele harde schijf (VHD) in de [Azure-portal](https://portal.azure.com). Dit artikel bevat richtlijnen voor probleemoplossing om u te helpen bij het oplossen van het probleem in een Azure Resource Manager-implementatie.

Als dit artikel niet van toepassing uw Azure probleem, gaat u naar de Azure-forums op [MSDN en Stack Overflow](https://azure.microsoft.com/support/forums/). U kunt het probleem op deze forums of boeken @AzureSupport op Twitter. U kunt ook een ondersteuning van Azure-aanvraag indienen door te selecteren **ondersteuning krijgen** op de [ondersteuning van Azure](https://azure.microsoft.com/support/options/) site.

## <a name="symptoms"></a>Symptomen
### <a name="scenario-1"></a>Scenario 1
Wanneer u probeert te verwijderen van een VHD in een opslagaccount in de implementatie van een Resource Manager, wordt het volgende foutbericht weergegeven:

**Verwijderen van blob 'vhds/BlobName.vhd' is mislukt. Fout: Er is momenteel een lease op de blob en geen lease-ID is opgegeven in de aanvraag.**

Dit probleem kan optreden omdat een virtuele machine (VM) een lease op de VHD die u probeert heeft te verwijderen.

### <a name="scenario-2"></a>Scenario 2
Wanneer u probeert te verwijderen van een container in een opslagaccount in de implementatie van een Resource Manager, wordt het volgende foutbericht weergegeven:

**Storage-container 'VHD's ' verwijderen is mislukt. Fout: Er is momenteel een lease voor de container en geen lease-ID is opgegeven in de aanvraag.**

Dit probleem kan optreden omdat de container is een VHD die in de status van de lease is vergrendeld.

### <a name="scenario-3"></a>Scenario 3
Wanneer u probeert te verwijderen van een opslagaccount in de implementatie van een Resource Manager, wordt het volgende foutbericht weergegeven:

**Storage-account 'StorageAccountName' verwijderen is mislukt. Fout: Het storage-account kan niet worden verwijderd omdat de artefacten die in gebruik.**

Dit probleem kan optreden omdat het opslagaccount bevat een VHD met de status van de lease.

## <a name="solution"></a>Oplossing 
Om deze problemen wilt oplossen, moet u de VHD die de fout veroorzaakt en de bijbehorende virtuele machine vaststellen. Vervolgens de VHD van de virtuele machine (voor gegevensschijven) ontkoppelen of verwijderen van de virtuele machine die van de VHD (voor OS-schijven gebruikmaakt). Hiermee verwijdert u de lease van de VHD te kunnen worden verwijderd. 

U doet dit door een van de volgende methoden te gebruiken:

### <a name="method-1---use-azure-storage-explorer"></a>Methode 1 - gebruik Azure Opslagverkenner

### <a name="step-1-identify-the-vhd-that-prevent-deletion-of-the-storage-account"></a>Stap 1 identificeren de VHD die voorkomen dat het storage-account wordt verwijderd

1. Wanneer u het storage-account verwijdert, ontvangt u een dialoogvenster weergegeven zoals het volgende: 

    ![Wanneer het verwijderen van opslagaccount](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. Controleer de **schijf URL** voor het identificeren van de opslag-account en de VHD die voorkomt u dat het opslagaccount verwijderen. In het volgende voorbeeld wordt de tekenreeks voor '. blob.core.windows.net ' is de opslagaccountnaam en 'SCCM2012-2015-08-28.vhd' is de naam van de VHD.  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

### <a name="step-2-delete-the-vhd-by-using-azure-storage-explorer"></a>Stap 2 de VHD verwijderen met behulp van Azure Storage Explorer

1. Download en installeer de nieuwste versie van [Azure Opslagverkenner](http://storageexplorer.com/). Dit hulpprogramma is een zelfstandige app van Microsoft waarmee u eenvoudig werken met Azure Storage-gegevens op Windows, Mac OS- en Linux.
2. Open Azure Storage Explorer, selecteer ![pictogram](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/account.png) Selecteer uw Azure-omgeving in de linkerbalk en vervolgens weer aanmelden.

3. Selecteer alle abonnementen of het abonnement dat u het opslagaccount bevat die u wilt verwijderen.

    ![Abonnement toevoegen](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/addsub.png)

4. Ga naar het opslagaccount dat we van de URL van de schijf eerdere, selecteer verkregen de **Blob-Containers** > **VHD's** en zoekt u de VHD die voorkomt u dat het opslagaccount verwijderen.
5. Als de VHD wordt gevonden, controleert u de **VM-naam** kolom vinden van de virtuele machine die van deze VHD gebruikmaakt.

    ![Controleer de virtuele machine](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/check-vm.png)

6. De lease van de VHD verwijderen met behulp van Azure-portal. Zie voor meer informatie [verwijderen van de lease van de VHD](#remove-the-lease-from-the-vhd). 

7. Ga naar de Azure Storage Explorer, met de rechtermuisknop op de VHD en selecteer verwijderen.

8. Hiermee wordt het opslagaccount verwijderd.

### <a name="method-2---use-azure-portal"></a>Methode 2: gebruik Azure-portal 

#### <a name="step-1-identify-the-vhd-that-prevent-deletion-of-the-storage-account"></a>Stap 1: De VHD die voorkomen dat wordt verwijderd van het opslagaccount identificeren

1. Wanneer u het storage-account verwijdert, ontvangt u een dialoogvenster weergegeven zoals het volgende: 

    ![Wanneer het verwijderen van opslagaccount](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. Controleer de **schijf URL** voor het identificeren van de opslag-account en de VHD die voorkomt u dat het opslagaccount verwijderen. In het volgende voorbeeld wordt de tekenreeks voor '. blob.core.windows.net ' is de opslagaccountnaam en 'SCCM2012-2015-08-28.vhd' is de naam van de VHD.  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

2. Meld u aan bij [Azure Portal](https://portal.azure.com).
3. Selecteer in het menu Hub **alle resources**. Ga naar het storage-account en selecteer vervolgens **Blobs** > **VHD's**.

    ![Schermafbeelding van de portal met de storage-account en de container 'VHD's ' is gemarkeerd](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/opencontainer.png)

4. Zoek de VHD die we eerder van de URL van de schijf hebt verkregen. Vervolgens bepalen welke VM maakt gebruik van de VHD. Meestal kunt u bepalen welk VM bevat de VHD door het controleren van de naam van de VHD:

Virtuele machine in een model voor Resource Manager-ontwikkeling

   * OS-schijven in het algemeen volgt u deze naamconventie: VMName-jjjj-MM-DD-HHMMSS.vhd
   * Gegevensschijven in het algemeen volgt u deze naamconventie: VMName-jjjj-MM-DD-HHMMSS.vhd

Virtuele machine in het model van de ontwikkeling klassiek

   * OS-schijven in het algemeen volgt u deze naamconventie: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd
   * Gegevensschijven in het algemeen volgt u deze naamconventie: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd

#### <a name="step-2-remove-the-lease-from-the-vhd"></a>Stap 2: De lease van de VHD verwijderen

[Verwijderen van de lease van de VHD](#remove-the-lease-from-the-vhd), en verwijder vervolgens het opslagaccount.

## <a name="what-is-a-lease"></a>Wat is een lease?
Een lease is een vergrendeling die kan worden gebruikt voor het toegangsbeheer naar een blob-(bijvoorbeeld een VHD). Wanneer de lease van een blob heeft alleen de eigenaren van de lease toegang tot de blob. Een lease is het belangrijk om de volgende redenen:

* Als meerdere eigenaren probeert te schrijven naar hetzelfde deel van de blob op hetzelfde moment kunnen beschadigde gegevens.
* Dit voorkomt dat de blob wordt verwijderd als er iets actief gebruikt wordt (bijvoorbeeld een VM).
* Dit voorkomt dat het storage-account wordt verwijderd als er iets actief gebruikt wordt (bijvoorbeeld een VM).

### <a name="remove-the-lease-from-the-vhd"></a>Verwijderen van de lease van de VHD
Als de VHD een besturingssysteemschijf is, moet u de virtuele machine als u wilt verwijderen van de lease verwijderen:

1. Meld u aan bij [Azure Portal](https://portal.azure.com).
2. Op de **Hub** selecteert u **virtuele Machines**.
3. Selecteer de virtuele machine die een lease op de VHD bevat.
4. Zorg ervoor dat er niets is actief met behulp van de virtuele machine, en dat u de virtuele machine niet meer nodig hebt.
5. Aan de bovenkant van de **VM details** blade Selecteer **verwijderen**, en klik vervolgens op **Ja** om te bevestigen.
6. De virtuele machine moet worden verwijderd, maar de VHD kan worden bewaard. De VHD moet niet langer een lease hebben erop. Het kan enkele minuten duren voordat de lease worden vrijgegeven. Om te bevestigen dat de lease is uitgebracht, gaat u naar **alle resources** > **Opslagaccountnaam** > **Blobs** > **VHD's**. In de **Blob-eigenschappen** deelvenster de **Lease Status** waarde moet **ontgrendeld**.

Als de VHD een gegevensschijf is, ontkoppel het VHD van de virtuele machine te verwijderen van de lease:

1. Meld u aan bij [Azure Portal](https://portal.azure.com).
2. Op de **Hub** selecteert u **virtuele Machines**.
3. Selecteer de virtuele machine die een lease op de VHD bevat.
4. Selecteer **schijven** op de **VM details** blade.
5. Selecteer de gegevensschijf waarin een lease op de VHD. Kunt u bepalen welk VHD is gekoppeld de schijf door het controleren van de URL van de VHD.
6. Bepalen met zekerheid dat er niets is actief met behulp van de gegevensschijf.
7. Klik op **Detach** op de **schijf details** blade.
8. De schijf moet nu worden ontkoppeld van de virtuele machine en de VHD mag niet langer een lease erop. Het kan enkele minuten duren voordat de lease worden vrijgegeven. Om te bevestigen dat de lease is vrijgegeven, gaat u naar **alle resources** > **Opslagaccountnaam** > **Blobs** > **VHD's**. In de **Blob-eigenschappen** deelvenster de **Lease Status** waarde moet **ontgrendeld**.

## <a name="next-steps"></a>Volgende stappen
* [Een opslagaccount verwijderen](storage-create-storage-account.md#delete-a-storage-account)
* [Hoe u de vergrendelde lease van blob storage in Microsoft Azure (PowerShell)](https://gallery.technet.microsoft.com/scriptcenter/How-to-break-the-locked-c2cd6492)
