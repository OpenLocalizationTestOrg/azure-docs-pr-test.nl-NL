---
title: een Windows-VHD van Azure aaaDownload | Microsoft Docs
description: Download een Windows-VHD met hello Azure-portal.
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: davidmu
ms.openlocfilehash: d0ca8842db98f22751f01648c0ba4e5cde090043
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="download-a-windows-vhd-from-azure"></a>Een Windows-VHD downloaden van Azure

In dit artikel leert u hoe toodownload een [Windows virtuele harde schijf (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) bestand van het gebruik van Azure hello Azure-portal. 

Virtuele machines (VM's) in Azure gebruik [schijven](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) als een plaats toostore een besturingssysteem, toepassingen en gegevens. Alle Azure VM's hebben ten minste twee schijven: de schijf van een Windows-besturingssysteem en een tijdelijke schijf. Hallo-besturingssysteemschijf in eerste instantie wordt gemaakt van een installatiekopie en besturingssysteemschijf Hallo zowel Hallo installatiekopie zijn VHD's opgeslagen in Azure storage-account. Virtuele machines hebben ook een of meer gegevensschijven die ook als virtuele harde schijven zijn opgeslagen.

## <a name="stop-hello-vm"></a>Hallo VM stoppen

Een VHD kan niet worden gedownload van Azure als het wordt aangesloten tooa VM uitgevoerd. U moet toostop Hallo VM toodownload een VHD. Als u wilt dat toouse een VHD als een [installatiekopie](tutorial-custom-images.md) toocreate andere VM's met nieuwe schijven, gebruikt u [Sysprep](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation) toogeneralize Hallo besturingssysteem Hallo-bestand bevat en vervolgens stoppen Hallo VM. toouse hello VHD als een schijf voor een nieuw exemplaar van een bestaande virtuele machine of de gegevensschijf u alleen toostop moet en Hallo VM ongedaan gemaakt.

toouse Hallo VHD als een installatiekopie toocreate andere virtuele machines, voert u deze stappen uit:

1.  Als u dit nog niet hebt gedaan, meld u aan toohello [Azure-portal](https://portal.azure.com/).
2.  [Verbinding maken met toohello VM](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 
3.  Open op Hallo VM, Hallo-opdrachtpromptvenster als administrator.
4.  Hallo directory ook wijzigen*%windir%\system32\sysprep* en sysprep.exe uitvoeren.
5.  Selecteer Hallo hulpprogramma voor systeemvoorbereiding in het dialoogvenster **System Voer Out-of-Box Experience (OOBE)**, en zorg ervoor dat **Generalize** is geselecteerd.
6.  Selecteer in de opties voor afsluiten **afsluiten**, en klik vervolgens op **OK**. 

toouse hello VHD als een schijf voor een nieuw exemplaar van een bestaande virtuele machine of de gegevensschijf, voer deze stappen uit:

1.  Klik op Hallo Hub-menu van hello Azure-portal, **virtuele Machines**.
2.  Hallo VM in Hallo lijst selecteren.
3.  Klik op de blade voor Hallo VM Hallo **stoppen**.

    ![VM stoppen](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a>Genereren van SAS-URL

toodownload hello VHD-bestand, moet u toogenerate een [shared access signature (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL. Als het Hallo-URL wordt gegenereerd, is een verlooptijd toohello URL toegewezen.

1.  Klik op het menu van Hallo blade voor Hallo VM Hallo **schijven**.
2.  Hallo besturingssysteemschijf voor Hallo VM selecteren en klik vervolgens op **exporteren**.
3.  Hallo verlooptijd van Hallo-URL te ingesteld*36000*.
4.  Klik op **URL genereren**.

    ![URL genereren](./media/download-vhd/export-generate.png)

> [!NOTE]
> Hallo verlooptijd is verhoogd van Hallo standaard tooprovide voldoende tijd toodownload Hallo grote VHD-bestand voor een Windows Server-besturingssysteem. U kunt een VHD-bestand met de Hallo Windows Server-besturingssysteem tootake enkele uren toodownload, afhankelijk van uw verbinding verwachten. Als u een VHD voor een gegevensschijf downloadt, is Hallo standaardtijd voldoende. 
> 
> 

## <a name="download-vhd"></a>VHD downloaden

1.  Klik op downloaden Hallo VHD-bestand onder Hallo-URL die is gegenereerd.

    ![VHD downloaden](./media/download-vhd/export-download.png)

2.  Mogelijk moet u tooclick **opslaan** in Hallo browser toostart Hallo downloaden. Hallo-standaardnaam voor Hallo VHD-bestand is *abcd*.

    ![Klik op opslaan in de browser Hallo](./media/download-vhd/export-save.png)

## <a name="next-steps"></a>Volgende stappen

- Meer informatie over hoe te[uploaden van een VHD-bestand tooAzure](upload-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 
- [Beheerde schijven maken van niet-beheerde schijven in een opslagaccount](attach-disk-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
- [Azure-schijven met PowerShell beheren](tutorial-manage-data-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

