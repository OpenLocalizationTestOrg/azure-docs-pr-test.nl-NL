---
title: een VHD Linux van Azure aaaDownload | Microsoft Docs
description: Download een Linux-VHD met hello Azure CLI en hello Azure-portal.
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
ms.openlocfilehash: 7e08e985a64a6be581b8f5eedcce60fbd314eaf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="download-a-linux-vhd-from-azure"></a>Downloaden van een VHD Linux van Azure

In dit artikel leert u hoe toodownload een [Linux virtuele harde schijf (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) bestand van het gebruik van Azure hello Azure CLI en Azure-portal. 

Virtuele machines (VM's) in Azure gebruik [schijven](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) als een plaats toostore een besturingssysteem, toepassingen en gegevens. Alle Azure VM's hebben ten minste twee schijven: de schijf van een Windows-besturingssysteem en een tijdelijke schijf. Hallo-besturingssysteemschijf in eerste instantie wordt gemaakt van een installatiekopie en besturingssysteemschijf Hallo zowel Hallo installatiekopie zijn VHD's opgeslagen in Azure storage-account. Virtuele machines hebben ook een of meer gegevensschijven die ook als virtuele harde schijven zijn opgeslagen.

Als u dit nog niet hebt gedaan, installeert u [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).

## <a name="stop-hello-vm"></a>Hallo VM stoppen

Een VHD kan niet worden gedownload van Azure als het wordt aangesloten tooa VM uitgevoerd. U moet toostop Hallo VM toodownload een VHD. Als u een VHD als toouse wilt een [installatiekopie](tutorial-custom-images.md) toocreate andere VM's met nieuwe schijven u moet toodeprovision en generalize Hallo-besturingssysteem die is opgenomen in het Hallo-bestand en Hallo VM stoppen. toouse hello VHD als een schijf voor een nieuw exemplaar van een bestaande virtuele machine of de gegevensschijf u alleen toostop moet en Hallo VM ongedaan gemaakt.

toouse Hallo VHD als een installatiekopie toocreate andere virtuele machines, voert u deze stappen uit:

1. SSH, Hallo-accountnaam en het openbare IP-adres Hallo van Hallo VM tooconnect tooit gebruiken en deze inrichting ervan ongedaan maakt. Hallo + gebruiker parameter Hallo laatste ingerichte gebruikersaccount, worden ook verwijderd. Als u de accountreferenties in toohello VM zijn bakken, laat u uit dit + parameter user. Hallo volgende voorbeeld verwijdert u Hallo laatste ingerichte gebruikersaccount:

    ```bash
    ssh azureuser@40.118.249.235
    sudo waagent -deprovision+user -force
    exit 
    ```

2. Meld u aan tooyour Azure-account met [az aanmelding](https://docs.microsoft.com/cli/azure/#login).
3. Stop en Hallo VM ongedaan gemaakt.

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

4. Hallo VM generalize. 

    ```azurecli
    az vm generalize --resource-group myResourceGroup --name myVM
    ``` 

toouse hello VHD als een schijf voor een nieuw exemplaar van een bestaande virtuele machine of de gegevensschijf, voer deze stappen uit:

1.  Meld u aan toohello [Azure-portal](https://portal.azure.com/).
2.  Klik op het menu Hub Hallo **virtuele Machines**.
3.  Hallo VM in Hallo lijst selecteren.
4.  Klik op de blade voor Hallo VM Hallo **stoppen**.

    ![VM stoppen](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a>Genereren van SAS-URL

toodownload hello VHD-bestand, moet u toogenerate een [shared access signature (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL. Als het Hallo-URL wordt gegenereerd, is een verlooptijd toohello URL toegewezen.

1.  Klik op het menu van Hallo blade voor Hallo VM Hallo **schijven**.
2.  Hallo besturingssysteemschijf voor Hallo VM selecteren en klik vervolgens op **exporteren**.
3.  Klik op **URL genereren**.

    ![URL genereren](./media/download-vhd/export-generate.png)

## <a name="download-vhd"></a>VHD downloaden

1.  Klik op downloaden Hallo VHD-bestand onder Hallo-URL die is gegenereerd.

    ![VHD downloaden](./media/download-vhd/export-download.png)

2.  Mogelijk moet u tooclick **opslaan** in Hallo browser toostart Hallo downloaden. Hallo-standaardnaam voor Hallo VHD-bestand is *abcd*.

    ![Klik op opslaan in de browser Hallo](./media/download-vhd/export-save.png)

## <a name="next-steps"></a>Volgende stappen

- Meer informatie over hoe te[uploaden en Linux-VM te maken van aangepaste schijf Hello Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 
- [Beheren van Azure-schijven hello Azure CLI](tutorial-manage-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

