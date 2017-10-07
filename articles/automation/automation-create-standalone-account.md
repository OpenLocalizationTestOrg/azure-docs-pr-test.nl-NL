---
title: aaaCreate zelfstandige Azure Automation-Account | Microsoft Docs
description: Zelfstudie die u helpt bij Hallo maken, testen en voorbeeld van beveiliging principal verificatie in Azure Automation.
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 2f783441-15c7-4ea0-ba27-d7daa39b1dd3
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/18/2017
ms.author: magoedte
ms.openlocfilehash: 1500d25d9565d4082768933834303a17c5e84234
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-standalone-azure-automation-account"></a>Een zelfstandig Azure Automation-account maken
Dit onderwerp leest u hoe toocreate een Automation-account van hello Azure-portal als u tooevaluate wilt en meer informatie over Azure Automation zonder op te nemen Hallo aanvullende oplossingen of integratie met OMS Log Analytics tooprovide geavanceerde bewaking van runbooktaken.  U kunt deze oplossingen toevoegen of integreren met logboekanalyse op elk punt in toekomstige Hallo.  Hallo Automation-account bent u kunnen tooauthenticate runbooks beheer van resources in Azure Resource Manager of de klassieke Azure-implementatie.

Als u een Automation-account in hello Azure-portal maakt, wordt automatisch gemaakt:

* Run As-account, die een nieuwe service-principal maakt in Azure Active Directory, een certificaat en wijst Hallo Inzender op rollen gebaseerde toegangsbeheer (RBAC), die is gebruikt toomanage Resource Manager-resources met behulp van runbooks.   
* Klassieke Run As-account door het uploaden van een beheercertificaat dat is gebruikt toomanage klassieke resources met behulp van runbooks.  

Dit vereenvoudigt het Hallo-proces voor u en kunt u snel starten gebouw en behoeften van uw automation runbooks toosupport implementeren.  

## <a name="permissions-required-toocreate-automation-account"></a>Machtigingen vereist toocreate Automation-account
toocreate of update een Automation-account, hebt u Hallo na specifieke rechten en machtigingen nodig toocomplete in dit onderwerp.   
 
* In de volgorde toocreate een Automation-account, uw AD-gebruikersaccount moet toobe toegevoegde tooa rol met de rol van eigenaar gelijkwaardige toohello machtigingen voor Microsoft.Automation bronnen zoals wordt beschreven in artikel [toegangsbeheer op basis van rollen in Azure Automation ](automation-role-based-access-control.md).  
* Als Hallo App registraties instellen te is ingesteld**Ja**, kunnen gebruikers niet-beheerders in uw Azure AD-tenant [AD-toepassingen registreren](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions).  Als Hallo app registraties instellen te is ingesteld**Nee**, Hallo gebruiker deze bewerking moet een globale beheerder in Azure AD. 

Als u niet lid zijn van de Active Directory-exemplaar van Hallo abonnement voordat u toohello globale beheerder/SA-administrator-rol van Hallo abonnement worden toegevoegd, kunt u tooActive Directory wordt toegevoegd als gast. In dit geval ontvangt u een "u hebt geen machtigingen toocreate..." Waarschuwing voor Hallo **Automation-Account toevoegen** blade. Gebruikers die zijn toegevoegd toohello globale beheerder/SA-administrator-rol kan worden verwijderd uit Active Directory-exemplaar van het abonnement Hallo eerst en opnieuw wordt toegevoegd toomake ze een volledige gebruiker in Active Directory. tooverify deze situatie van Hallo **Azure Active Directory** deelvenster in Azure portal, selecteer Hallo **gebruikers en groepen**, selecteer **alle gebruikers** en, nadat u Hallo selecteren specifieke gebruiker, schakelt **profiel**. waarde van Hallo Hallo **gebruikerstype** kenmerk onder Hallo gebruikersprofiel moet niet gelijk aan **Gast**.

## <a name="create-a-new-automation-account-from-hello-azure-portal"></a>Een nieuw Automation-Account maken vanuit hello Azure-portal
In deze sectie uitvoeren Hallo stappen toocreate een Azure Automation-account in hello Azure-portal te volgen.    

1. Meld u aan toohello Azure-portal met een account dat lid is van de rol Abonnementsbeheerders hello en medebeheerder van Hallo-abonnement.
2. Klik op **Nieuw**.<br><br> ![De optie Nieuw selecteren in Azure Portal](media/automation-offering-get-started/automation-portal-martketplacestart.png)<br>  
3. Zoeken naar **Automation** en klik vervolgens in Hallo zoekresultaten Selecteer **Automation en Control***.<br><br> ![Zoek naar en selecteer Automation in Marketplace](media/automation-create-standalone-account/automation-marketplace-select-create-automationacct.png)<br> 
3. Klik in de blade Automation-Accounts Hallo op **toevoegen**.<br><br>![Automation-account toevoegen](media/automation-create-standalone-account/automation-create-automationacct-properties.png)
   
   > [!NOTE]
   > Als u de volgende waarschuwing in Hallo Hallo ziet **Automation-Account toevoegen** blade is omdat uw account geen lid is van de rol Abonnementsbeheerders hello en co-beheerder van het Hallo-abonnement is.<br><br>![Waarschuwing bij Automation-account toevoegen](media/automation-create-standalone-account/create-account-without-perms.png)
   > 
   > 
4. In Hallo **Automation-Account toevoegen** blade in Hallo **naam** vak Typ een naam voor uw nieuwe Automation-account.
5. Als u meer dan één abonnement hebt, één voor de nieuwe account hello, Geef een nieuwe of bestaande **resourcegroep** en een Azure-datacenter **locatie**.
6. Controleer Hallo waarde **Ja** is geselecteerd voor Hallo **Azure uitvoeren als-account maken** optie en klik op Hallo **maken** knop.  
   
   > [!NOTE]
   > Als u kiest toonot Hallo Run As-account maken met de optie Hallo **Nee**, krijgt u een waarschuwing weergegeven op Hallo **Automation-Account toevoegen** blade.  Tijdens het Hallo-account is gemaakt in hello Azure-portal, heeft geen overeenkomstige verificatie-id in de klassieke of Resource Manager abonnement Active Directory en daarom geen tooresources toegang in uw abonnement.  Dit voorkomt dat alle runbooks die naar verwijzen dit account kunnen tooauthenticate en uitvoeren van taken op basis van bronnen in de implementatiemodellen.
   > 
   > ![Waarschuwing bij Automation-account toevoegen](media/automation-create-standalone-account/create-account-decline-create-runas-msg.png)<br>
   > Wanneer het Hallo-service-principal is niet gemaakt is niet de rol Inzender Hallo toegewezen.
   > 

7. Terwijl Azure Hallo Automation-account maakt, kunt u de voortgang Hallo onder bijhouden **meldingen** in Hallo-menu.

### <a name="resources-included"></a>Beschikbare resources
Als Hallo Automation-account is gemaakt, worden automatisch verschillende resources voor u gemaakt.  Hallo volgende tabel geeft een overzicht van resources voor Hallo Run As-account.<br>

| Resource | Beschrijving |
| --- | --- |
| AzureAutomationTutorial Runbook |Een grafische voorbeeldrunbook dat laat zien hoe met behulp van tooauthenticate Hallo Run As-account en alle Hallo Resource Manager-resources opgehaald. |
| AzureAutomationTutorialScript Runbook |Een voorbeeldrunbook PowerShell die laat zien hoe met behulp van tooauthenticate Hallo Run As-account en alle Hallo Resource Manager-resources opgehaald. |
| AzureRunAsCertificate |Certificaatasset automatisch gemaakt tijdens het maken van Automation-account of met behulp van de onderstaande Hallo PowerShell-script voor een bestaande account.  Hiermee kunt u tooauthenticate met Azure zodat u Azure Resource Manager-resources van runbooks beheren kunt.  Dit certificaat is één jaar geldig. |
| AzureRunAsConnection |Verbindingsasset automatisch gemaakt tijdens het maken van Automation-account of met behulp van de onderstaande Hallo PowerShell-script voor een bestaande account. |

Hallo volgende tabel geeft een overzicht van resources voor Hallo klassieke Run As-account.<br>

| Resource | Beschrijving |
| --- | --- |
| AzureClassicAutomationTutorial Runbook |Een voorbeeld grafisch runbook, die alle Hallo klassieke VM's in een abonnement met Hallo klassieke Run As-Account (certificaat) ophalen en vervolgens levert Hallo VM-naam en de status. |
| AzureClassicAutomationTutorial Script Runbook |Een voorbeeld van de PowerShell-runbook dat Hiermee haalt u alle Hallo klassieke VM's in een abonnement met Hallo klassieke Run As-Account (certificaat) en vervolgens levert Hallo VM-naam en de status. |
| AzureClassicRunAsCertificate |Certificaatasset automatisch gemaakt die gebruikt tooauthenticate met Azure zodat u de klassieke Azure-resources van runbooks beheren kunt.  Dit certificaat is één jaar geldig. |
| AzureClassicRunAsConnection |Verbindingsasset automatisch gemaakt die gebruikt tooauthenticate met Azure zodat u de klassieke Azure-resources van runbooks beheren kunt. |


## <a name="next-steps"></a>Volgende stappen
* Zie toolearn meer informatie over grafisch ontwerpen [grafisch ontwerpen in Azure Automation](automation-graphical-authoring-intro.md).
* Zie tooget gestart met PowerShell-runbooks [Mijn eerste PowerShell-runbook](automation-first-runbook-textual-powershell.md).
* tooget gestart met PowerShell workflow-runbooks, Zie [Mijn eerste PowerShell workflow-runbook](automation-first-runbook-textual.md).
