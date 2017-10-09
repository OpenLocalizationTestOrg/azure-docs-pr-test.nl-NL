---
title: aaaCreate uw eerste virtuele machine in een testomgeving in Azure DevTest Labs | Microsoft Docs
description: Meer informatie over hoe toocreate uw eerste virtuele machine in een testomgeving in Azure DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: fbc5a438-6e02-4952-b654-b8fa7322ae5f
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/24/2017
ms.author: tarcher
ms.openlocfilehash: 4c3257efca9be6fdd190eaac1db731464e07fcfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-vm-in-a-lab-in-azure-devtest-labs"></a>Uw eerste virtuele machine maken in een testomgeving in Azure DevTest Labs

Wanneer u in eerste instantie DevTest Labs toegang en toocreate uw eerste virtuele machine, wordt waarschijnlijk hiervoor met behulp van een vooraf geladen [base marketplace-installatiekopie](devtest-lab-configure-marketplace-images.md). Later ook, moet u kunnen toochoose van een [aangepaste installatiekopie en een formule](devtest-lab-add-vm.md) bij het maken van meer virtuele machines. 

Deze zelfstudie leert u met behulp van Azure portal tooadd Hallo uw eerste VM tooa lab in DevTest Labs.

## <a name="steps-tooadd-your-first-vm-tooa-lab-in-azure-devtest-labs"></a>Stappen tooadd uw eerste VM tooa lab in Azure DevTest Labs
1. Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Selecteer **meer Services**, en selecteer vervolgens **DevTest Labs** uit Hallo-lijst.
1. Selecteer in lijst Hallo van labs Hallo lab waarin wordt gezocht toocreate Hallo VM.  
1. Op de Hallo lab **overzicht** blade Selecteer **+ toevoegen**.  

    ![VM-knop toevoegen](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. Op Hallo **kiezen een base** blade, selecteer een marketplace-installatiekopie voor Hallo VM.
1. Op Hallo **virtuele machine** blade, voer een naam voor de nieuwe virtuele machine Hallo in Hallo **virtuele-machinenaam** in het tekstvak.

    ![VM-labblade](./media/devtest-lab-add-vm/devtestlab-lab-add-first-vm.png)

1. Voer een **gebruikersnaam** die administrator-bevoegdheden op Hallo virtuele machine wordt verleend.  
1. Voer een wachtwoord in Hallo tekstveld met het label **typt u een waarde**.
1. Hallo **virtuele machine schijftype** wordt bepaald welk type opslagschijf is toegestaan voor Hallo virtuele machines in Hallo lab.
1. Selecteer **grootte van virtuele machine** en selecteer een van de Hallo vooraf gedefinieerde items die Hallo processorcores, RAM-geheugen en grootte van de vaste schijf Hallo van Hallo VM toocreate opgeven.
1. Selecteer **artefacten** - in de lijst Hallo van artefacten - en selecteer Hallo artefacten die u tooadd toohello basisinstallatiekopie wilt configureren.
    **Opmerking:** als u nieuwe tooDevTest Labs of configureren van artefacten, Raadpleeg toohello [toevoegen van een bestaande artefact tooa VM](./devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) sectie en ga vervolgens terug hier na voltooiing.
1. Selecteer **maken** tooadd Hallo VM toohello lab opgegeven.

   Hallo-status van Hallo van de virtuele machine maken: Hallo labblade eerst weergegeven als **maken**, klikt u vervolgens als **met** na Hallo VM is gestart.

## <a name="next-steps"></a>Volgende stappen
* Eenmaal Hallo VM is gemaakt, kunt u toohello VM door te selecteren **Connect** op Hallo van de virtuele machine-blade.
* Bekijk [toevoegen van een VM tooa lab](devtest-lab-add-vm.md) voor gedetailleerde informatie over het toevoegen van de volgende virtuele machines in uw testomgeving.
* Hallo verkennen [DevTest Labs Azure Resource Manager QuickStart sjablonengalerie](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates).
