---
title: aaaAdd eigenaars en gebruikers in Azure DevTest Labs | Microsoft Docs
description: Eigenaars- en gebruikers toevoegen in Azure DevTest Labs met hello Azure-portal of PowerShell
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 4f51d9a5-2702-45f0-a2d5-a3635b58c416
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: 2a98f5fe1efbd7c23e0d97f58f47c37462aed3b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-owners-and-users-in-azure-devtest-labs"></a>Eigenaars- en gebruikers toevoegen in Azure DevTest Labs
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/How-to-set-security-in-your-DevTest-Lab/player]
> 
> 

Toegang in Azure DevTest Labs wordt beheerd door [gebaseerd toegangsbeheer (RBAC)](../active-directory/role-based-access-control-what-is.md). Met RBAC kunt kunt u taken scheiden binnen uw team in *rollen* waarin u alleen Hallo hoeveelheid toegang nodig toousers tooperform hun taken toekennen. Drie van deze RBAC-rollen zijn *eigenaar*, *DevTest Labs gebruiker*, en *Inzender*. In dit artikel leert u welke acties worden uitgevoerd in elk Hallo drie belangrijkste RBAC rollen. Van daaruit leert u hoe tooadd gebruikers tooa lab - die beide via Hallo portal en via een PowerShell-script en hoe gebruikers tooadd op abonnementsniveau Hallo.

## <a name="actions-that-can-be-performed-in-each-role"></a>Acties die kunnen worden uitgevoerd in elke rol
Er zijn drie belangrijkste rollen kunt u een gebruiker toewijzen:

* Eigenaar
* DevTest Labs gebruiker
* Inzender

Hallo volgende tabel ziet u Hallo-acties die kunnen worden uitgevoerd door gebruikers in elk van deze rollen:

| **Gebruikers met deze rol acties kunnen uitvoeren** | **DevTest Labs gebruiker** | **Eigenaar** | **Inzender** |
| --- | --- | --- | --- |
| **Taken voor het testlab** | | | |
| Gebruikers tooa lab toevoegen |Nee |Ja |Nee |
| Update-instellingen |Nee |Ja |Ja |
| **Basis VM-taken** | | | |
| Toevoegen en verwijderen van aangepaste installatiekopieën |Nee |Ja |Ja |
| Toevoegen, bijwerken en verwijderen van formules |Ja |Ja |Ja |
| Geaccepteerde Azure Marketplace-installatiekopieën |Nee |Ja |Ja |
| **VM-taken** | | | |
| Virtuele machines maken |Ja |Ja |Ja |
| Starten, stoppen en verwijderen van virtuele machines |Alleen virtuele machines die zijn gemaakt door gebruiker Hallo |Ja |Ja |
| Beleidsregels voor virtuele machine bijwerken |Nee |Ja |Ja |
| Gegevensschijven van VM's toevoegen of verwijderen |Alleen virtuele machines die zijn gemaakt door gebruiker Hallo |Ja |Ja |
| **Taken van artefacten** | | | |
| Toevoegen en verwijderen van artefacten opslagplaatsen |Nee |Ja |Ja |
| Toepassen van artefacten |Ja |Ja |Ja |

> [!NOTE]
> Wanneer een gebruiker een virtuele machine maakt, wordt deze gebruiker toohello automatisch toegewezen **eigenaar** rol Hallo VM gemaakt.
> 
> 

## <a name="add-an-owner-or-user-at-hello-lab-level"></a>Toevoegen van een eigenaar of gebruiker op Hallo lab niveau
Eigenaars- en gebruikers kunnen worden toegevoegd op Hallo lab niveau via hello Azure-portal. Dit omvat externe gebruikers met een geldig [Microsoft-account (MSA)](devtest-lab-faq.md#what-is-a-microsoft-account).
Hallo stappen volgen helpt u bij Hallo van het toevoegen van een eigenaar of gebruiker tooa lab in Azure DevTest Labs:

1. Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Selecteer **meer services**, en selecteer vervolgens **DevTest Labs** uit Hallo-lijst.
3. Selecteer de gewenste lab Hallo in lijst Hallo van labs.
4. Selecteer op Hallo van labblade, **configuratie**. 
5. Op Hallo **configuratie** blade Selecteer **gebruikers**.
6. Op Hallo **gebruikers** blade Selecteer **+ toevoegen**.
   
    ![Gebruiker toevoegen](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
7. Op Hallo **Selecteer een rol** blade, selecteer Hallo gewenste functie. sectie Hallo [acties die kunnen worden uitgevoerd in elke rol](#actions-that-can-be-performed-in-each-role) lijsten Hallo verschillende acties die kunnen worden uitgevoerd door gebruikers in Hallo eigenaar, DevTest gebruiker en Inzender rollen.
8. Op Hallo **gebruikers toevoegen** blade Voer Hallo e-mailadres of de naam van Hallo gebruiker gewenste tooadd in Hallo-rol die u hebt opgegeven. Als Hallo-gebruiker kan niet worden gevonden, wordt een foutbericht uitgelegd Hallo probleem. Als de gebruiker hello wordt gevonden, wordt die gebruiker weergegeven en geselecteerd. 
9. Selecteer **Selecteer**.
10. Selecteer **OK** tooclose hello **toegang toevoegen** blade.
11. Als u terugkeert toohello **gebruikers** blade Hallo gebruiker is toegevoegd.  

## <a name="add-an-external-user-tooa-lab-using-powershell"></a>Toevoegen van een externe gebruiker tooa lab met behulp van PowerShell
Bovendien tooadding gebruikers in hello Azure-portal, kunt u toevoegen een externe gebruiker tooyour testomgeving met een PowerShell-script. Hallo bijvoorbeeld na gewoon Wijzig in Hallo parameterwaarden onder Hallo **waarden toochange** opmerking.
U kunt ophalen Hallo `subscriptionId`, `labResourceGroup`, en `labName` waarden uit de labblade Hallo in hello Azure-portal.

> [!NOTE]
> Hallo-voorbeeldscript wordt ervan uitgegaan dat Hallo opgegeven gebruiker is toegevoegd als een gast toohello Active Directory en als dat niet Hallo geval mislukken. tooadd een gebruiker niet in Active Directory tooa lab, Hallo hello Azure portal tooassign Hallo-gebruikersrol tooa gebruiken zoals wordt geïllustreerd in de sectie Hallo [toevoegen van een eigenaar of gebruiker op Hallo lab niveau](#add-an-owner-or-user-at-the-lab-level).   
> 
> 

    # Add an external user in DevTest Labs user role tooa lab
    # Ensure that guest users can be added toohello Azure Active directory:
    # https://azure.microsoft.com/en-us/documentation/articles/active-directory-create-users/#set-guest-user-access-policies

    # Values toochange
    $subscriptionId = "<Enter Azure subscription ID here>"
    $labResourceGroup = "<Enter lab's resource name here>"
    $labName = "<Enter lab name here>"
    $userDisplayName = "<Enter user's display name here>"

    # Log into your Azure account
    Login-AzureRmAccount

    # Select hello Azure subscription that contains hello lab. 
    # This step is optional if you have only one subscription.
    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    # Retrieve hello user object
    $adObject = Get-AzureRmADUser -SearchString $userDisplayName

    # Create hello role assignment. 
    $labId = ('subscriptions/' + $subscriptionId + '/resourceGroups/' + $labResourceGroup + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    New-AzureRmRoleAssignment -ObjectId $adObject.Id -RoleDefinitionName 'DevTest Labs User' -Scope $labId

## <a name="add-an-owner-or-user-at-hello-subscription-level"></a>Toevoegen van een eigenaar of gebruiker op het abonnementsniveau Hallo
Azure machtigingen worden overgenomen van bovenliggende bereik toochild bereik in Azure. Eigenaren van een Azure-abonnement met labs worden dus automatisch eigenaren van deze labs. Ze ook eigenaar Hallo VM's en andere resources die zijn gemaakt door Hallo lab van gebruikers en hello Azure DevTest Labs service. 

U kunt aanvullende eigenaars tooa lab via Hallo labblade toevoegen in Hallo [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040). Hallo toegevoegd echter van eigenaar in het bereik van beheer beperken dan Hallo abonnement eigenaar scope zijn. Hallo toegevoegd bijvoorbeeld eigenaars hebben geen volledige toegang toosome Hallo-resources die zijn gemaakt in Hallo abonnement door Hallo DevTest Labs service. 

tooadd een eigenaar tooan Azure-abonnement, als volgt te werk:

1. Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Selecteer **meer Services**, en selecteer vervolgens **abonnementen** uit Hallo-lijst.
3. Hallo gewenste abonnement selecteren.
4. Selecteer **toegang** pictogram. 
   
    ![-Gebruikers](./media/devtest-lab-add-devtest-user/access-users.png)
5. Op Hallo **gebruikers** blade Selecteer **toevoegen**.
   
    ![Gebruiker toevoegen](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
6. Op Hallo **Selecteer een rol** blade Selecteer **eigenaar**.
7. Op Hallo **gebruikers toevoegen** blade Hallo e-mailadres of de naam invoeren van Hallo gebruiker gewenste tooadd als eigenaar. Als het Hallo-gebruiker kan niet worden gevonden, krijgt u een foutbericht weergegeven waarin wordt uitgelegd Hallo probleem. Als de gebruiker hello wordt gevonden, die gebruiker wordt vermeld onder Hallo **gebruiker** in het tekstvak.
8. Selecteer Hallo bevindt gebruikersnaam.
9. Selecteer **Selecteer**.
10. Selecteer **OK** tooclose hello **toegang toevoegen** blade.
11. Als u terugkeert toohello **gebruikers** blade Hallo gebruiker is toegevoegd als een eigenaar. Deze gebruiker is nu eigenaar van een labs gemaakt onder dit abonnement, en dus kunnen tooperform eigenaar taken. 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

