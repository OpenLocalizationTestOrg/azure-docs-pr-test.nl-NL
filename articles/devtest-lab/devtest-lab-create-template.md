---
title: de aangepaste installatiekopie van een Azure DevTest Labs vanaf een VHD-bestand aaaCreate | Microsoft Docs
description: Meer informatie over hoe een aangepaste installatiekopie in Azure DevTest Labs vanaf een VHD-bestand met toocreate hello Azure-portal
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: b795bc61-7c28-40e6-82fc-96d629ee0568
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 80af8ea1cb72380f868df0a76c4a0dcd92e63cf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vhd-file"></a>Een aangepaste installatiekopie van een VHD-bestand maken

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a>Stapsgewijze instructies

Hallo volgende stappen maakt u een aangepaste installatiekopie maken van een VHD-bestand met behulp van hello Azure-portal:

1. Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Selecteer **meer services**, en selecteer vervolgens **DevTest Labs** uit Hallo-lijst.

1. Selecteer de gewenste lab Hallo in lijst Hallo van labs.  

1. Selecteer op Hallo van labblade, **configuratie**. 

1. Op Hallo lab **configuratie** blade Selecteer **aangepaste installatiekopieën (VHD's)**.

1. Op Hallo **aangepaste installatiekopieën** blade Selecteer **+ toevoegen**.

    ![Aangepaste installatiekopie toe te voegen](./media/devtest-lab-create-template/add-custom-image.png)

1. Hallo-naam van de aangepaste installatiekopie Hallo invoeren. Deze naam wordt weergegeven in de lijst Hallo met basisinstallatiekopieën bij het maken van een virtuele machine.

1. Hallo-omschrijving van de aangepaste installatiekopie Hallo invoeren. Deze beschrijving wordt weergegeven in de lijst van basisinstallatiekopieën Hallo bij het maken van een virtuele machine.

1. Selecteer **VHD**.

1. Van Hallo **VHD** blade, selecteer Hallo gewenst VHD-bestand.

1. Selecteer **OK** tooclose hello **VHD** blade.

1. Selecteer **configuratie van het besturingssysteem**.

1. Op Hallo **configuratie van het besturingssysteem** tabblad, selecteert u **Windows** of **Linux**.

1. Als **Windows** is geselecteerd, geeft u via Hallo selectievakje of *Sysprep* op Hallo machine is uitgevoerd. 

1. Selecteer **OK** tooclose hello **configuratie van het besturingssysteem** blade.

1. Selecteer **OK** toocreate Hallo aangepaste installatiekopie.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>Verwante blogberichten

- [Aangepaste installatiekopieën of formules?](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [Kopiëren van aangepaste installatiekopieën tussen Azure DevTest Labs](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a>Volgende stappen

- [Een VM tooyour lab toevoegen](./devtest-lab-add-vm-with-artifacts.md)
