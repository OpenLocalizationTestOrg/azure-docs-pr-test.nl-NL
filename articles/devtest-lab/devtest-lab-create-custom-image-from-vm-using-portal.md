---
title: de aangepaste installatiekopie van een virtuele machine van een Azure DevTest Labs aaaCreate | Microsoft Docs
description: Meer informatie over hoe een aangepaste installatiekopie in Azure DevTest Labs vanuit een ingericht met VM toocreate hello Azure-portal
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
ms.openlocfilehash: 7dccb79d3db4aae676c7bd2f6b800301210491e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vm"></a>Een aangepaste installatiekopie van een virtuele machine maken

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

## <a name="step-by-step-instructions"></a>Stapsgewijze instructies

U kunt een aangepaste installatiekopie van een ingerichte virtuele machine maken en daarna gebruiken die aangepaste installatiekopie toocreate identieke virtuele machines. Hallo stappen laten zien hoe toocreate een aangepaste installatiekopie van een virtuele machine:

1. Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Selecteer **meer services**, en selecteer vervolgens **DevTest Labs** uit Hallo-lijst.

1. Selecteer de gewenste lab Hallo in lijst Hallo van labs.  

1. Selecteer op Hallo van labblade, **mijn virtuele machines**.
 
1. Op Hallo **mijn virtuele machines** blade Selecteer Hallo VM waaruit de toocreate Hallo aangepaste installatiekopie.

1. Selecteer op de blade Hallo van de virtuele machine **maken aangepaste installatiekopie (VHD)**.

    ![Afbeelding van aangepaste menu-item maken](./media/devtest-lab-create-template/create-custom-image.png)

1. Op Hallo **afbeelding maken** blade een naam en beschrijving voor de aangepaste installatiekopie opgeven. Deze informatie wordt weergegeven in de lijst Hallo van basissen bij het maken van een virtuele machine.

    ![Blade voor aangepaste installatiekopie maken](./media/devtest-lab-create-template/create-custom-image-blade.png)

1. Geef op of sysprep is uitgevoerd op Hallo VM. Als Hallo sysprep is niet uitgevoerd op Hallo VM, kunt u opgeven of u wilt dat sysprep uitgevoerd wanneer een virtuele machine vanuit deze aangepaste installatiekopie wordt gemaakt.

1. Selecteer **OK** wanneer klaar toocreate Hallo aangepaste installatiekopie.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>Verwante blogberichten

- [Aangepaste installatiekopieën of formules?](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [Kopiëren van aangepaste installatiekopieën tussen Azure DevTest Labs](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a>Volgende stappen

- [Een VM tooyour lab toevoegen](./devtest-lab-add-vm-with-artifacts.md)
