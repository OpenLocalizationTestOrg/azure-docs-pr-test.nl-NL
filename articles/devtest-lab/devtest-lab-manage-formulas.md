---
title: aaaManage formules in Azure DevTest Labs toocreate VMs | Microsoft Docs
description: Meer informatie over hoe Azure DevTest Labs formules voor tooupdate en verwijderen
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 841dd95a-657f-4d80-ba26-59a9b5104fe4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: tarcher
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 855debe46f3b70cc45ea5d55869663b64e225124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-devtest-labs-formulas"></a>Azure DevTest Labs formules beheren

[!INCLUDE [devtest-lab-formula-definition](../../includes/devtest-lab-formula-definition.md)]

Dit artikel wordt beschreven hoe toocreate een formule van een base (aangepaste installatiekopie, Marketplace-installatiekopie of een andere formule) of een bestaande virtuele machine. In dit artikel helpt u ook bij het beheren van bestaande formules.

## <a name="create-a-formula"></a>Maak een formule
Iedereen met DevTest Labs *gebruikers* machtigingen kunnen toocreate virtuele machines met een formule als basis is. Er zijn twee manieren toocreate formules: 

* Gebruik van een basis - als u alle Hallo kenmerken van Hallo formule toodefine wilt.
* Van een bestaande lab VM - gebruiken als u wilt dat toocreate een formule op basis van Hallo-instellingen van een bestaande virtuele machine.

Zie voor meer informatie over het toevoegen van gebruikers en machtigingen [eigenaars en gebruikers toevoegen in Azure DevTest Labs](./devtest-lab-add-devtest-user.md).

### <a name="create-a-formula-from-a-base"></a>Maak een formule van een basis
Hallo stappen volgen helpt u bij het Hallo-proces voor het maken van een formule van een aangepaste installatiekopie, Marketplace-installatiekopie of een andere formule.

1. Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).

2. Selecteer **meer Services**, en selecteer vervolgens **DevTest Labs** uit Hallo-lijst.

3. Selecteer de gewenste lab Hallo in lijst Hallo van labs.  

4. Selecteer op Hallo van labblade, **formules (herbruikbare bases)**.
   
    ![Menu formule](./media/devtest-lab-create-formulas/lab-settings-formulas.png)

5. Op Hallo **formules** blade Selecteer **+ toevoegen**.
   
    ![Een formule toevoegen](./media/devtest-lab-create-formulas/add-formula.png)

6. Op Hallo **kiezen een base** blade Selecteer Hallo base (aangepaste installatiekopie, Marketplace-installatiekopie of formule) waaruit de toocreate Hallo formule.
   
    ![Base lijst](./media/devtest-lab-create-formulas/base-list.png)

7. Op Hallo **formule maken** blade Hallo volgende waarden opgeven:
   
    * **Formulenaam** -Voer een naam voor de formule. Deze waarde wordt weergegeven in de lijst Hallo met basisinstallatiekopieën bij het maken van een virtuele machine. Hallo-naam wordt al gevalideerd als u deze typen, en als dat niet geldig, er wordt gemeld Hallo-vereisten voor een geldige naam.
    * **Beschrijving** -Voer een duidelijke beschrijving voor de formule. Deze waarde is beschikbaar in het contextmenu van de formule Hallo bij het maken van een virtuele machine.
    * **Gebruikersnaam** -Voer een gebruikersnaam die wordt verleend administrator-bevoegdheden.
    * **Wachtwoord** : Geef - of Selecteer in de vervolgkeuzelijst Hallo - u op een waarde die is gekoppeld aan het Hallo-geheim (wachtwoord) wilt u toouse voor Hallo opgegeven gebruiker. Zie voor meer informatie over Hallo geheimen [Azure DevTest Labs: persoonlijke archief van de geheime](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/).
    * **Virtuele machine schijftype** – Geef de harde schijf (harde schijf) of SSD (solid-state drive) tooindicate welke opslagschijf type is toegestaan voor Hallo virtuele machines zijn ingericht met behulp van deze basisinstallatiekopie.
    * ** Virtuele machine grootte ** - Selecteer een van de vooraf gedefinieerde Hallo-items die Hallo processorcores, RAM-geheugen en grootte van de vaste schijf Hallo van Hallo VM toocreate opgeven. 
    * **Artefacten** -Selecteer tooopen hello **artefacten toevoegen** blade die u selecteert en Hallo artefacten die u tooadd toohello basisinstallatiekopie wilt configureren. Zie voor meer informatie over artefacten [beheren VM artefacten in Azure DevTest Labs](./devtest-lab-add-vm-with-artifacts.md).
    * **Geavanceerde instellingen** -Selecteer tooopen hello **Geavanceerd** blade waar u Hallo volgende instellingen configureren:
        * **Virtueel netwerk** -Hallo gewenst virtueel netwerk opgeven.
        * **Subnet** -Hallo gewenst subnet opgeven.    
        * **IP-adresconfiguratie** -opgeven of u wilt dat Hallo Public, Private of gedeelde IP-adressen. Zie voor meer informatie over gedeelde IP-adressen [Understand gedeelde IP-adressen in Azure DevTest Labs](./devtest-lab-shared-ip.md).
        * **Zorg dat deze machine claimable** -maken van een machine 'claimable' betekent dat deze wordt niet worden toegewezen eigendom op Hallo moment gemaakt. In plaats daarvan lab kunnen gebruikers zich kunnen tootake eigendom ("claim") Hallo machine in Hallo labblade.     
    * **Afbeelding** -dit veld bevat de naam van Hallo basisinstallatiekopie u hebt geselecteerd op de vorige blade Hallo. 
     
       ![Formule maken](./media/devtest-lab-create-formulas/create-formula.png)

8. Selecteer **maken** toocreate Hallo formule.

9. Wanneer het Hallo-formule is gemaakt, wordt weergegeven in de lijst Hallo op Hallo **formules** blade.

### <a name="create-a-formula-from-a-vm"></a>Maak een formule van een virtuele machine
Hallo volgende stappen begeleiden u bij Hallo-proces voor het maken van een formule op basis van een bestaande virtuele machine. 

> [!NOTE]
> toocreate een formule van een virtuele machine, Hallo VM moet zijn gemaakt na 30 maart 2016. 
> 
> 

1. Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Selecteer **meer Services**, en selecteer vervolgens **DevTest Labs** uit Hallo-lijst.
3. Selecteer de gewenste lab Hallo in lijst Hallo van labs.  
4. Op de Hallo lab **overzicht** blade Selecteer Hallo VM van waaruit u wilt dat toocreate Hallo formule.
   
    ![Virtuele machines Labs](./media/devtest-lab-create-formulas/my-vms.png)
5. Selecteer op de blade Hallo van de virtuele machine **formule (op basis van herbruikbare) maken**.
   
    ![Formule maken](./media/devtest-lab-create-formulas/create-formula-menu.png)
6. Op Hallo **formule maken** blade, voer een **naam** en **beschrijving** voor uw nieuwe formule.
   
    ![Formule blade maken](./media/devtest-lab-create-formulas/create-formula-blade.png)
7. Selecteer **OK** toocreate Hallo formule.

## <a name="modify-a-formula"></a>Een formule wijzigen
een formule toomodify als volgt te werk:

1. Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Selecteer **meer Services**, en selecteer vervolgens **DevTest Labs** uit Hallo-lijst.
3. Selecteer de gewenste lab Hallo in lijst Hallo van labs.  
4. Selecteer op Hallo van labblade, **formules (herbruikbare bases)**.
   
    ![Menu formule](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. Op Hallo **Lab formules** blade, selecteer Hallo-formule die u wenst dat toomodify.
6. Op Hallo **formule bijwerken** blade Hallo gewenst bewerkingen en selecteer **Update**.

## <a name="delete-a-formula"></a>Verwijderen van een formule
een formule toodelete als volgt te werk:

1. Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Selecteer **meer Services**, en selecteer vervolgens **DevTest Labs** uit Hallo-lijst.
3. Selecteer de gewenste lab Hallo in lijst Hallo van labs.  
4. Op Hallo lab **instellingen** blade Selecteer **formules**.
   
    ![Menu formule](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. Op Hallo **Lab formules** blade, selecteer Hallo weglatingsteken toohello rechts van de formule Hallo gewenste toodelete.
   
    ![Menu formule](./media/devtest-lab-manage-formulas/lab-formulas-blade.png)
6. Selecteer in het contextmenu van de formule hello, **verwijderen**.
   
    ![Formule contextmenu](./media/devtest-lab-manage-formulas/formula-delete-context-menu.png)
7. Selecteer **Ja** toohello verwijdering bevestigen.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>Verwante blogberichten
* [Aangepaste installatiekopieën of formules?](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a>Volgende stappen
Nadat u een formule voor gebruik gemaakt hebt bij het maken van een virtuele machine, Hallo volgende stap is te[toevoegen van een VM tooyour lab](devtest-lab-add-vm-with-artifacts.md).

