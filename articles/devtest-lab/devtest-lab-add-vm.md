---
title: aaaAdd een lab VM tooa in Azure DevTest Labs | Microsoft Docs
description: Meer informatie over hoe tooadd een virtuele machine tooa lab in Azure DevTest Labs
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
ms.date: 02/24/2017
ms.author: tarcher
ms.openlocfilehash: 82838e4349550db56de311264c188140b9556b24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-vm-tooa-lab-in-azure-devtest-labs"></a>Een VM tooa lab toevoegen in Azure DevTest Labs
Als u al hebt [gemaakt van uw eerste VM](devtest-lab-create-first-vm.md), waarschijnlijk werd ook een vooraf geladen [marketplace-installatiekopie](devtest-lab-configure-marketplace-images.md). Nu, als u tooadd latere virtuele machines tooyour lab wilt, u kunt ook een *base* dat ofwel een [aangepaste installatiekopie](devtest-lab-create-template.md) of een [formule](devtest-lab-manage-formulas.md). Deze zelfstudie leert u met behulp van Azure portal tooadd een VM tooa lab Hallo in DevTest Labs.

Dit artikel leest u hoe toomanage artefacten Hallo voor een virtuele machine in uw testomgeving.

## <a name="steps-tooadd-a-vm-tooa-lab-in-azure-devtest-labs"></a>Stappen tooadd een lab VM tooa in Azure DevTest Labs
1. Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Selecteer **meer Services**, en selecteer vervolgens **DevTest Labs** uit Hallo-lijst.
1. Selecteer in lijst Hallo van labs Hallo lab waarin wordt gezocht toocreate Hallo VM.  
1. Op de Hallo lab **overzicht** blade Selecteer **+ toevoegen**.  

    ![VM-knop toevoegen](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. Op Hallo **kiezen een base** blade, selecteert u een basis voor Hallo VM.
1. Op Hallo **virtuele machine** blade, voer een naam voor de nieuwe virtuele machine Hallo in Hallo **virtuele-machinenaam** in het tekstvak.

    ![VM-labblade](./media/devtest-lab-add-vm/devtestlab-lab-vm-blade.png)

1. Voer een **gebruikersnaam** die administrator-bevoegdheden op Hallo virtuele machine wordt verleend.  
1. Als u wilt dat toouse een wachtwoord opgeslagen in uw [geheime store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store), selecteer **een opgeslagen geheim**, en geef de waarde van een sleutel die overeenkomt met tooyour geheim (wachtwoord). Anders een wachtwoord opgeven in Hallo tekstveld met het label **typt u een waarde**.
1. Hallo **virtuele machine schijftype** wordt bepaald welk type opslagschijf is toegestaan voor Hallo virtuele machines in Hallo lab.
1. Selecteer **grootte van virtuele machine** en selecteer een van de Hallo vooraf gedefinieerde items die Hallo processorcores, RAM-geheugen en grootte van de vaste schijf Hallo van Hallo VM toocreate opgeven.
1. Selecteer **artefacten** - in de lijst Hallo van artefacten - en selecteer Hallo artefacten die u tooadd toohello basisinstallatiekopie wilt configureren.
    **Opmerking:** als u nieuwe tooDevTest Labs of configureren van artefacten, Raadpleeg toohello [toevoegen van een bestaande artefact tooa VM](#add-an-existing-artifact-to-a-vm) sectie en ga vervolgens terug hier na voltooiing.
1. Selecteer **geavanceerde instellingen** opties opties en verlopen een tooconfigure Hallo VM-netwerk. 

   een optie verlopen tooset kiezen Hallo kalender pictogram toospecify een datum waarop Hallo VM automatisch worden verwijderd.  Standaard Hallo VM nooit verloopt. 
1. Als u wilt dat tooview of hello Azure Resource Manager-sjabloon kopieert, raadpleeg dan toohello [opslaan Azure Resource Manager-sjabloon](#save-azure-resource-manager-template) sectie en hier terug wanneer voltooid.
1. Selecteer **maken** tooadd Hallo VM toohello lab opgegeven.
1. Hallo-status van Hallo van de virtuele machine maken: Hallo labblade eerst weergegeven als **maken**, klikt u vervolgens als **met** na Hallo VM is gestart.

> [!NOTE]
> [Toevoegen van een claimable VM](devtest-lab-add-claimable-vm.md) ziet u hoe toomake VM claimable Hallo zodat deze beschikbaar voor gebruik door elke gebruiker in Hallo lab.
>
>

## <a name="add-an-existing-artifact-tooa-vm"></a>Toevoegen van een bestaande artefact tooa VM
U kunt bestaande artefacten toevoegen tijdens het maken van een virtuele machine. Elke lab bevat artefacten uit Hallo openbare DevTest Labs-Artefactopslagplaats evenals artefacten dat u hebt gemaakt en toegevoegd tooyour eigenaar Artefactopslagplaats.

* Azure DevTest Labs *artefacten* kunt u opgeven *acties* die worden uitgevoerd wanneer Hallo VM is ingericht, zoals Windows PowerShell-scripts uitvoeren, Bash opdrachten uit te voeren en het installeren van software.
* Artefacten *parameters* kunt u Hallo artefact voor uw specifieke scenario aanpassen

hoe toocreate artefacten, Zie toodiscover Hallo artikel [informatie over hoe tooauthor uw eigen artefacten voor gebruik met DevTest Labs](devtest-lab-artifact-author.md).

1. Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Selecteer **meer Services**, en selecteer vervolgens **DevTest Labs** uit Hallo-lijst.
1. Selecteer in de lijst van de Hallo van labs, Hallo lab die Hallo VM die u wilt dat toowork bevat.  
1. Selecteer **mijn virtuele machines**.
1. Selecteer Hallo gewenste VM.
1. Selecteer **artefacten**. 
1. Selecteer **toepassen artefacten**.
1. Op Hallo **toepassen artefacten** blade, selecteer Hallo artefacten die u wenst dat tooadd toohello VM.
1. Op Hallo **toevoegen artefact** blade invoeren van parameterwaarden Hallo vereist en eventuele optionele parameters die u nodig hebt.  
1. Selecteer **toevoegen** tooadd Hallo artefacten en keer terug toohello **toepassen artefacten** blade.
1. Doorgaan met het toevoegen van artefacten nodig zijn voor uw virtuele machine.
1. Nadat u uw artefacten hebt toegevoegd, kunt u [Hallo in volgorde welke Hallo artefacten zijn uitgevoerd wijzigen](#change-the-order-in-which-artifacts-are-run). U kunt ook teruggaan te[weergeven of wijzigen van een artefact](#view-or-modify-an-artifact).
1. Wanneer u klaar bent met het toevoegen van artefacten selecteren **toepassen**

## <a name="change-hello-order-in-which-artifacts-are-run"></a>Hallo-volgorde wijzigen waarin artefacten worden uitgevoerd
Hallo acties van Hallo artefacten worden standaard uitgevoerd in Hallo volgorde waarin ze toohello VM worden toegevoegd. Hallo volgende stappen laten zien hoe toochange Hallo in volgorde welke Hallo artefacten zijn uitgevoerd.

1. Hallo boven aan het Hallo **toepassen artefacten** blade, selecteer Hallo-koppeling die het aantal artefacten die zijn toegevoegd aan de toohello VM Hallo aangeeft.
   
    ![Aantal artefacten tooVM toegevoegd](./media/devtest-lab-add-vm-with-artifacts/devtestlab-add-artifacts-blade-selected-artifacts.png)
1. Op Hallo **geselecteerd artefacten** blade, slepen en neerzetten Hallo artefacten in Hallo gewenste volgorde. **Opmerking:** als u problemen ondervindt bij het Hallo-artefacten te slepen, zorgt u ervoor dat u vanaf de linkerkant Hallo artefact Hallo sleept. 
1. Selecteer **OK** wanneer u gereed bent.  

## <a name="view-or-modify-an-artifact"></a>Weergeven of wijzigen van een artefact
Hallo volgende stappen laten zien hoe tooview of Hallo parameters van een artefact wijzigen:

1. Hallo boven aan het Hallo **toepassen artefacten** blade, selecteer Hallo-koppeling die het aantal artefacten die zijn toegevoegd aan de toohello VM Hallo aangeeft.
   
    ![Aantal artefacten tooVM toegevoegd](./media/devtest-lab-add-vm-with-artifacts/devtestlab-add-artifacts-blade-selected-artifacts.png)
1. Op Hallo **geselecteerd artefacten** blade, selecteer Hallo artefact dat u wilt dat tooview of bewerkt.  
1. Op Hallo **toevoegen artefact** blade, controleert alle wijzigingen die nodig zijn en selecteer **OK** tooclose hello **toevoegen artefact** blade.
1. Selecteer **OK** tooclose hello **geselecteerd artefacten** blade.

## <a name="save-azure-resource-manager-template"></a>Azure Resource Manager-sjabloon opslaan
Een Azure Resource Manager-sjabloon biedt een declaratieve manier toodefine een herhaalbare implementatie. Hallo stappen wordt uitgelegd hoe toosave hello Azure Resource Manager-sjabloon voor Hallo VM wordt gemaakt.
Wanneer opgeslagen, kunt u hello Azure Resource Manager-sjabloon te[implementeren van nieuwe virtuele machines met Azure PowerShell](../azure-resource-manager/resource-group-overview.md#template-deployment).

1. Op Hallo **virtuele machine** blade Selecteer **ARM-sjabloon weergeven**.
2. Op Hallo **weergave Azure Resource Manager-sjabloon** blade, selecteer Hallo sjabloontekst.
3. Hallo geselecteerde tekst toohello Klembord kopiëren.
4. Selecteer **OK** tooclose hello **weergave Azure Resource Manager-sjabloon blade**.
5. Open een teksteditor.
6. In Hallo sjabloontekst van Hallo Klembord te plakken.
7. Hallo opslaan voor later gebruik.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a>Volgende stappen
* Eenmaal Hallo VM is gemaakt, kunt u toohello VM door te selecteren **Connect** op Hallo van de virtuele machine-blade.
* Meer informatie over hoe te[aangepaste artefacten maken voor uw DevTest Labs VM](devtest-lab-artifact-author.md).
* Hallo verkennen [DevTest Labs Azure Resource Manager QuickStart sjablonengalerie](https://github.com/Azure/azure-devtestlab/tree/master/Samples).
