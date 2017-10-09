---
title: aaaAdd een claimable VM tooa lab in Azure DevTest Labs | Microsoft Docs
description: Meer informatie over hoe tooadd een lab dat is tooa claimable virtuele machine in Azure DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: f671e66e-9630-4e30-a131-a6bad9ed9c11
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: tarcher
ms.openlocfilehash: fe6385ae2e59b9636b82aec250dc3a1f8a40ba5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-claimable-vm-tooa-lab-in-azure-devtest-labs"></a>Toevoegen van een claimable tooa lab voor virtuele machine in Azure DevTest Labs
U een claimable VM tooa lab toevoegen in een vergelijkbare manier toohow u [toevoegen van een standaard virtuele machine](devtest-lab-add-vm.md) – Selecteer in een *base* dat ofwel een [aangepaste installatiekopie](devtest-lab-create-template.md), [formule](devtest-lab-manage-formulas.md), of [Marketplace-installatiekopie](devtest-lab-configure-marketplace-images.md). In deze zelfstudie wordt u begeleid bij gebruik van Azure portal tooadd Hallo een claimable VM tooa lab in DevTest Labs en ziet u Hallo proces dat een gebruiker via tooclaim Hallo VM.

> [!NOTE]
> Als u virtuele machines lab via implementeert [Azure Resource Manager-sjablonen](devtest-lab-create-environment-from-arm.md), kunt u claimable virtuele machines maken met de instelling Hallo **allowClaim** eigenschap tootrue in de sectie eigenschappen Hallo.
>
>

## <a name="steps-tooadd-a-claimable-vm-tooa-lab-in-azure-devtest-labs"></a>Stappen tooadd een claimable VM tooa lab in Azure DevTest Labs
1. Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Selecteer **meer Services**, en selecteer vervolgens **DevTest Labs** uit Hallo-lijst.
1. Selecteer in lijst Hallo van labs Hallo lab in die u wilt dat Hallo toocreate claimable VM.  
1. Op de Hallo lab **overzicht** blade Selecteer **+ toevoegen**.  

    ![VM-knop toevoegen](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. Op Hallo **kiezen een base** blade, selecteert u een basis voor Hallo VM.
1. Op Hallo **virtuele machine** blade, voer een naam voor de nieuwe virtuele machine Hallo in Hallo **virtuele-machinenaam** in het tekstvak.

    ![VM-labblade](./media/devtest-lab-add-vm/devtestlab-lab-vm-blade.png)

1. Voer een **gebruikersnaam** die administrator-bevoegdheden op Hallo virtuele machine wordt verleend.  
1. Als u wilt dat toouse een wachtwoord opgeslagen in uw [geheime store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store), selecteer **een opgeslagen geheim**, en geef de waarde van een sleutel die overeenkomt met tooyour geheim (wachtwoord). Anders een wachtwoord opgeven in Hallo tekstveld met het label **typt u een waarde**.
1. Hallo **virtuele machine schijftype** wordt bepaald welk type opslagschijf is toegestaan voor Hallo virtuele machines in Hallo lab.
1. Selecteer **grootte van virtuele machine** en selecteer een van de Hallo vooraf gedefinieerde items die Hallo processorcores, RAM-geheugen en grootte van de vaste schijf Hallo van Hallo VM toocreate opgeven.
1. Selecteer **artefacten** in lijst Hallo van artefacten en selecteer Hallo artefacten die u tooadd toohello basisinstallatiekopie wilt configureren. Als u nieuwe tooDevTest Labs of configureren van artefacten, Raadpleeg toohello [toevoegen van een bestaande artefact tooa VM](devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) sectie en ga vervolgens terug hier na voltooiing.
1. Selecteer **geavanceerde instellingen** opties opties en verlopen een tooconfigure Hallo VM-netwerk. Onder **opties Claim**, kies **Ja** claimable toomake Hallo-machine.

  ![Kies toomake hello claimable VM.](./media/devtest-lab-add-vm/devtestlab-claim-VM-option.png)

1. Als u wilt dat tooview of hello Azure Resource Manager-sjabloon kopieert, raadpleeg dan toohello [opslaan Azure Resource Manager-sjabloon](devtest-lab-add-vm.md#save-azure-resource-manager-template) sectie en hier terug wanneer voltooid.
1. Selecteer **maken** tooadd Hallo VM toohello lab opgegeven.
1. Hallo-status van Hallo van de virtuele machine maken: Hallo labblade eerst weergegeven als **maken**, klikt u vervolgens als **met** na Hallo VM is gestart.


## <a name="using-a-claimable-vm"></a>Met behulp van een claimable VM

Een gebruiker kan VM van de lijst van 'Claimable virtuele machines' Hallo claim op een van de volgende stappen uit:

* Met de rechtermuisknop op een van de Hallo virtuele machines in de lijst Hallo vanuit Hallo lijst met 'Claimable virtuele machines' Hallo onderaan de blade overzicht van het lab Hallo in, en kies **Claim machine**.

 ![Aanvragen van een specifieke claimable virtuele machine.](./media/devtest-lab-add-vm/devtestlab-claim-VM.png)


* Hallo boven aan het Hallo **overzicht** blade kiezen **een Claim**. Een willekeurige virtuele machine wordt toegewezen uit Hallo lijst met claimable VM's.

 ![Aanvraag geen claimable VM.](./media/devtest-lab-add-vm/devtestlab-claim-any.png)


Nadat een gebruiker claims van een virtuele machine, omhoog verplaatst naar hun lijst met 'Mijn virtuele machines' en is niet langer claimable door een andere gebruiker.

## <a name="next-steps"></a>Volgende stappen
* Eenmaal Hallo VM is gemaakt, kunt u toohello VM door te selecteren **Connect** op Hallo van de virtuele machine-blade.
* Hallo verkennen [sjablonengalerie DevTest Labs Azure Resource Manager QuickStart](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)
