---
title: Azure AD-gebruikersaccount aaaCreate | Microsoft Docs
description: Dit artikel wordt beschreven hoe een Azure AD-gebruikersaccount toocreate referentie voor runbooks in Azure Automation tooauthenticate in Azure en de klassieke Azure.
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
keywords: Azure Active Directory-gebruiker, Azure Service Management, Azure AD-gebruikersaccount
ms.assetid: fcfe266d-b22e-4dfb-8272-adcab09fc0cf
ms.service: automation
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/13/2017
ms.author: magoedte
ms.openlocfilehash: 7c6ed4182dbab074d0bc5da7057f74ad321d8884
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-runbooks-with-azure-classic-deployment-and-resource-manager"></a>Runbooks met klassieke Azure-implementatie en Resource Manager verifiëren
Dit artikel wordt beschreven Hallo stappen die u moet een Azure AD-gebruikersaccount tooconfigure uitvoeren voor Azure Automation-runbooks uitvoeren in Azure klassieke implementatiemodel of Azure Resource Manager-resources.  Terwijl dit nog steeds toobe een ondersteunde verificatie-identiteit voor uw Azure Resource Manager gebaseerde runbooks, Hallo aanbevolen methode maakt gebruik van een Azure uitvoeren als-account.       

## <a name="create-a-new-azure-active-directory-user"></a>Een nieuwe Azure Active Directory-gebruiker maken
1. Toohello klassieke Azure-portal als servicebeheerder voor hello Azure-abonnement u toomanage wilt aanmelden.
2. Selecteer **Active Directory**, en selecteer vervolgens Hallo-naam van de organisatiedirectory.
3. Selecteer Hallo **gebruikers** tabblad en selecteer vervolgens in het opdrachtgebied hello **gebruiker toevoegen**.
4. Op Hallo **Vertel ons meer over deze gebruiker** pagina onder **Type gebruiker**, selecteer **nieuwe gebruiker in uw organisatie**.
5. Voer een gebruikersnaam in.  
6. Selecteer de mapnaam Hallo die is gekoppeld aan uw Azure-abonnement op de pagina Active Directory Hallo.
7. Op Hallo **gebruikersprofiel** pagina, voorzien van een eerste en laatste naam, een gebruiksvriendelijke naam en gebruiker vanaf Hallo **rollen** lijst.  Schakel **Multi-Factor Authentication** niet in.
8. Houd er rekening mee Hallo volledige naam en het tijdelijke wachtwoord.
9. Selecteer **Instellingen > Beheerders > Toevoegen**.
10. Typ de volledige gebruikersnaam Hallo van Hallo-gebruiker die u hebt gemaakt.
11. Hallo-abonnement dat u wilt dat gebruikers toomanage Hallo selecteren.
12. Meld u af bij Azure en meld u opnieuw aan met de Hallo-account die u zojuist hebt gemaakt. U zult na vragen aan gebruiker toochange Hallo het wachtwoord van gebruiker.

## <a name="create-an-automation-account-in-azure-classic-portal"></a>Een Automation-account maken in de klassieke Azure-portal
In deze sectie maakt uitvoeren u Hallo volgende stappen toocreate een Azure Automation-account in hello Azure-portal voor gebruik met uw runbooks voor het beheren van bronnen in de klassieke Azure-implementatie.  

> [!NOTE]
> Automation-accounts die zijn gemaakt met de klassieke Azure-portal Hallo kunnen worden beheerd door zowel Hallo klassieke Azure-Portal en Azure-portal en een set cmdlets. Zodra het Hallo-account is gemaakt, is het maakt niet uit hoe u maken en beheren van resources binnen het Hallo-account. Als u van plan bent toocontinue toouse Hallo klassieke Azure-portal, gebruikt u deze in plaats van hello Azure portal toocreate Automation-accounts.
> 
> 

1. Toohello klassieke Azure-portal als servicebeheerder voor hello Azure-abonnement u toomanage wilt aanmelden.
2. Selecteer **Automation**.
3. Op Hallo **Automation** pagina **een Automation-Account maken**.
4. In Hallo **een Automation-Account maken** , typ een naam voor uw nieuwe Automation-account en kiest u een **regio** uit de vervolgkeuzelijst Hallo.  
5. Klik op **OK** tooaccept uw instellingen en maak Hallo-account.
6. Nadat deze is gemaakt wordt het weergegeven op Hallo **Automation** pagina.
7. Klik op het Hallo-account en het ervoor zorgt dat toohello dashboardpagina.  
8. Selecteer op de pagina Dashboard van Automation Hallo **activa**.
9. Op Hallo **activa** pagina **instellingen toevoegen** zich onderaan Hallo Hallo pagina.
10. Op Hallo **instellingen toevoegen** pagina **referentie toevoegen**.
11. Op Hallo **referentie definiëren** pagina **Windows PowerShell-referentie** van Hallo **referentietype** vervolgkeuzelijst en geef een naam voor Hallo referentie.
12. Op de volgende Hallo **referentie definiëren** pagina type Hallo gebruikersnaam Hallo AD-gebruikersaccount gemaakt eerder in Hallo **gebruikersnaam** veld en Hallo wachtwoord in Hallo **wachtwoord**en **wachtwoord bevestigen** velden. Klik op **OK** toosave uw wijzigingen.

## <a name="create-an-automation-account-in-hello-azure-portal"></a>Een automatiseringsaccount maken in hello Azure-portal
In deze sectie uitvoeren Hallo volgende stappen toocreate een Azure Automation-account in hello Azure-portal voor gebruik met uw runbooks voor het beheren van bronnen in de modus Azure Resource Manager.  

1. Aanmelden toohello Azure-portal als servicebeheerder voor hello Azure-abonnement u wilt dat toomanage.
2. Selecteer **Automation-accounts**.
3. Klik in de blade Automation-Accounts Hallo op **toevoegen**.<br><br>![Automation-account toevoegen](media/automation-create-aduser-account/add-automation-acct-properties.png)
4. In Hallo **Automation-Account toevoegen** blade in Hallo **naam** vak Typ een naam voor uw nieuwe Automation-account.
5. Als u meer dan één abonnement hebt, geeft u Hallo voor het nieuwe account hello, evenals een nieuwe of bestaande **resourcegroep** en een Azure-datacenter **locatie**.
6. Selecteer Hallo waarde **Ja** voor Hallo **Azure uitvoeren als-account maken** optie en klik op Hallo **maken** knop.  
   
    > [!NOTE]
    > Als u kiest toonot Hallo Run As-account maken met de optie Hallo **Nee**, er verschijnt een waarschuwing weergegeven in Hallo **Automation-Account toevoegen** blade.  Tijdens het Hallo-account is gemaakt en toegewezen toohello **Inzender** rol in het Hallo-abonnement, heeft deze geen overeenkomstige verificatie-id in de adreslijstservice van uw abonnementen en daarom geen toegang resources in uw abonnement.  Dit wordt voorkomen dat alle runbooks die verwijzen naar dit account kunnen tooauthenticate worden en uitvoeren op basis van Azure Resource Manager-bronnen.
    > 
    >

    <br>![Waarschuwing bij Automation-account toevoegen](media/automation-create-aduser-account/add-automation-acct-properties-error.png)<br>  
7. Terwijl Azure Hallo Automation-account maakt, kunt u de voortgang Hallo onder bijhouden **meldingen** in Hallo-menu.

Bij het maken van de referentie Hallo Hallo is voltooid, moet u toocreate eerder een Referentieasset tooassociate Hallo Automation-Account met Hallo AD-gebruikersaccount hebt gemaakt.  Denk eraan dat we alleen Hallo Automation-account hebt gemaakt en is niet gekoppeld aan een verificatie-identiteit.  Voer Hallo stappen uit die worden beschreven in Hallo [Referentieassets in Azure Automation-artikel](automation-credentials.md#creating-a-new-credential-asset) en Voer Hallo-waarde voor **gebruikersnaam** Hallo indeling **domein\gebruiker**.

## <a name="use-hello-credential-in-a-runbook"></a>Hallo-referentie gebruiken in een runbook
U kunt ophalen Hallo referentie in een runbook met behulp van Hallo [Get-AutomationPSCredential](http://msdn.microsoft.com/library/dn940015.aspx) activiteit en vervolgens worden gebruikt met [Add-AzureAccount](http://msdn.microsoft.com/library/azure/dn722528.aspx) tooconnect tooyour Azure-abonnement. Als Hallo referentie een beheerder van meerdere Azure-abonnementen, wordt ook moet u gebruiken [Select-AzureSubscription](http://msdn.microsoft.com/library/dn495203.aspx) toospecify Hallo juiste is. Dit wordt weergegeven in Hallo voorbeeld Windows PowerShell onderstaande die doorgaans wordt weergegeven boven Hallo aan de meeste Azure Automation-runbooks.

    $cred = Get-AutomationPSCredential –Name "myuseraccount.onmicrosoft.com"
    Add-AzureAccount –Credential $cred
    Select-AzureSubscription –SubscriptionName "My Subscription"

U moet deze regels na [controlepunten](http://technet.microsoft.com/library/dn469257.aspx#bk_Checkpoints) in uw runbook herhalen. Als Hallo runbook wordt onderbroken en op een andere werknemer hervat, moet deze opnieuw tooperform Hallo-verificatie.

## <a name="next-steps"></a>Volgende stappen
* Bekijk Hallo verschillende runbooktypen en stappen voor het maken van uw eigen runbooks van Hallo volgende artikel [Azure Automation-runbooktypen](automation-runbook-types.md)

