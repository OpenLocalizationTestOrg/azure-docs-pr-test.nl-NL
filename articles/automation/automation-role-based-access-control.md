---
title: aaaRole gebaseerd toegangsbeheer in Azure Automation | Microsoft Docs
description: Met op rollen gebaseerd toegangsbeheer (RBAC) beschikt u over toegangsbeheer voor Azure-resources. Dit artikel wordt beschreven hoe tooset van RBAC in Azure Automation.
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
keywords: automatisering rbac, rolgebaseerde toegangscontrole, azure rbac
ms.assetid: 04b5625e-0ee8-4b5b-85cd-7734c1b3d4a3
ms.service: automation
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/12/2016
ms.author: magoedte;sngun
ms.openlocfilehash: 051438e44d0c5c514d6dbaac5a312344ee311cdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="role-based-access-control-in-azure-automation"></a>Op rollen gebaseerd toegangsbeheer in Azure Automation
## <a name="role-based-access-control"></a>Op rollen gebaseerd toegangsbeheer
Met op rollen gebaseerd toegangsbeheer (RBAC) beschikt u over toegangsbeheer voor Azure-resources. Met behulp van [RBAC](../active-directory/role-based-access-control-configure.md), kunt u taken scheiden binnen uw team en verleen alleen Hallo hoeveelheid toegang toousers, groepen en toepassingen die zij nodig hebben tooperform hun werk. Op rollen gebaseerde toegang kan worden verleend als toousers met hello Azure-portal, Azure-opdrachtregelprogramma's of Azure Management-API's.

## <a name="rbac-in-automation-accounts"></a>RBAC in Automation-accounts
In Azure Automation wordt toegang verleend door toe te wijzen Hallo juiste RBAC-rol toousers, groepen en toepassingen bij Hallo Automation-accountbereik. Hieronder worden de ingebouwde rollen die worden ondersteund door een Automation-account Hallo:  

| **Rol** | **Beschrijving** |
|:--- |:--- |
| Eigenaar |rol van eigenaar Hallo kan toegang tot tooall bronnen en acties binnen een Automation-account inclusief het bieden van toegang tooother gebruikers, groepen en toepassingen toomanage Hallo Automation-account. |
| Inzender |de rol Inzender Hallo kunt u toomanage alles behalve het wijzigen van andere gebruikers toegang tot machtigingen tooan Automation-account. |
| Lezer |Hallo met de rol lezer kunt u tooview alle Hallo resources in een Automation-account, maar geen wijzigingen kunnen aanbrengen. |
| Automation-operator |de rol Automation-Operator Hallo kunt u tooperform operationele taken zoals het starten, stoppen, onderbreken, hervatten en plannen van taken. Deze rol is handig als u wilt dat tooprotect uw Automation-Account resources zoals referentieassets en runbooks worden weergegeven of gewijzigd, maar wel wilt toestaan dat leden van de tooexecute van uw organisatie deze runbooks. |
| Beheerder van gebruikerstoegang |Hallo beheerder voor gebruikerstoegang rol kunt u toomanage gebruiker toegang tooAzure Automation-accounts. |

> [!NOTE]
> U kunt toegang rechten tooa specifiek runbook of runbooks, alleen toohello resources en acties binnen Hallo Automation-account kan niet verlenen.  
> 
> 

In dit artikel we begeleidt u stapsgewijs door het tooset van RBAC in Azure Automation. Maar eerst laten we nemen een dichter Hallo afzonderlijke machtigingen verleend toohello Inzender, lezer, de Automation-Operator en de beheerder voor gebruikerstoegang kijken zodat krijgen we goed begrijpt voordat u iedereen verleent rechten toohello Automation-account.  Anders kan dit leiden tot onverwachte of ongewenste consequenties.     

## <a name="contributor-role-permissions"></a>Machtigingen voor de rol van Bijdrager
Hallo geeft volgende tabel Hallo specifieke acties die kunnen worden uitgevoerd door de rol van Inzender Hallo in Automation.

| **Resourcetype** | **Lezen** | **Schrijven** | **Verwijderen** | **Andere acties** |
|:--- |:--- |:--- |:--- |:--- |
| Azure Automation Account |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) | |
| Automation Certificate Asset |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) | |
| Automation Connection Asset |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) | |
| Automation Connection Type Asset |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) | |
| Automation Credential Asset |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) | |
| Automation Schedule Asset |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) | |
| Automation Variable Asset |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) | |
| Automation Desired State Configuration | | | |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) |
| Hybrid Runbook Worker Resource Type |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) | |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) | |
| Azure Automation Job |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) | |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) |
| Automation Job Stream |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Automation Job Schedule |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) | |
| Automation Module |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) | |
| Azure Automation Runbook |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) |
| Automation Runbook Draft |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) | | |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) |
| Automation Runbook Draft Test Job |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) | |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) |
| Automation Webhook |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) |

## <a name="reader-role-permissions"></a>Machtigingen voor de rol van Lezer
Hallo geeft volgende tabel Hallo specifieke acties die kunnen worden uitgevoerd door Hallo lezer role in Automation.

| **Resourcetype** | **Lezen** | **Schrijven** | **Verwijderen** | **Andere acties** |
|:--- |:--- |:--- |:--- |:--- |
| Klassiek abonnement beheerder |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Vergrendeling voor beheer |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Machtiging |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Provider-bewerkingen |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Nieuwe roltoewijzing |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Roldefinitie ophalen |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) | | | |

## <a name="automation-operator-role-permissions"></a>Rolmachtigingen Automation-operator
Hallo geeft volgende tabel Hallo specifieke acties die kunnen worden uitgevoerd door Hallo Automation-Operator role in Automation.

| **Resourcetype** | **Lezen** | **Schrijven** | **Verwijderen** | **Andere acties** |
|:--- |:--- |:--- |:--- |:--- |
| Azure Automation Account |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Automation Certificate Asset | | | | |
| Automation Connection Asset | | | | |
| Automation Connection Type Asset | | | | |
| Automation Credential Asset | | | | |
| Automation Schedule Asset |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) | | |
| Automation Variable Asset | | | | |
| Automation Desired State Configuration | | | | |
| Hybrid Runbook Worker Resource Type | | | | |
| Azure Automation Job |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) | |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) |
| Automation Job Stream |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Automation Job Schedule |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) | | |
| Automation Module | | | | |
| Azure Automation Runbook |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Automation Runbook Draft | | | | |
| Automation Runbook Draft Test Job | | | | |
| Automation Webhook | | | | |

Voor meer details, Hallo [Automation-operatoracties](../active-directory/role-based-access-built-in-roles.md#automation-operator) lijsten Hallo acties die worden ondersteund door de rol van Hallo Automation-operator op Hallo Automation-account en de bijbehorende bronnen.

## <a name="user-access-administrator-role-permissions"></a>Machtigingen van de rol Beheerder van de Gebruikerstoegang
Hallo geeft volgende tabel Hallo specifieke acties die kunnen worden uitgevoerd door Hallo beheerder voor gebruikerstoegang role in Automation.

| **Resourcetype** | **Lezen** | **Schrijven** | **Verwijderen** | **Andere acties** |
|:--- |:--- |:--- |:--- |:--- |
| Azure Automation Account |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Automation Certificate Asset |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Automation Connection Asset |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Automation Connection Type Asset |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Automation Credential Asset |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Automation Schedule Asset |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Automation Variable Asset |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Automation Desired State Configuration | | | | |
| Hybrid Runbook Worker Resource Type |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Azure Automation Job |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Automation Job Stream |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Automation Job Schedule |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Automation Module |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Azure Automation Runbook |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Automation Runbook Draft |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Automation Runbook Draft Test Job |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Automation Webhook |![Groene Status](media/automation-role-based-access-control/green-checkmark.png) | | | |

## <a name="configure-rbac-for-your-automation-account-using-azure-portal"></a>RBAC configureren voor uw Automation-account met Azure Portal
1. Meld u bij toohello [Azure Portal](https://portal.azure.com/) en open uw Automation-account van de blade Automation-Accounts Hallo.  
2. Klik op Hallo **toegang** control op Hallo rechterbovenhoek. Hiermee opent u Hallo **gebruikers** blade waarin u nieuwe gebruikers, groepen en toepassingen toomanage uw Automation-account toevoegen kunt en bestaande rollen weergeven die kunnen worden geconfigureerd voor Hallo Automation-Account.  
   
   ![De knop Toegang](media/automation-role-based-access-control/automation-01-access-button.png)  

> [!NOTE]
> **Abonnementsbeheerders** bestaat al als standaardgebruiker Hallo. Hallo abonnement beheerders active directory-groep bevat Hallo-service (s) en medebeheerder voor uw Azure-abonnement. Hallo-servicebeheerder is Hallo eigenaar van uw Azure-abonnement en de bijbehorende bronnen en wordt rol van eigenaar Hallo overgenomen hebben voor Hallo automation-accounts te. Dit betekent dat Hallo toegang **overgenomen** voor **servicebeheerders en medebeheerders** van een abonnement en de **toegewezen** voor alle andere gebruikers Hallo. Klik op **abonnementsbeheerders** tooview om meer details over hun machtigingen.  
> 
> 

### <a name="add-a-new-user-and-assign-a-role"></a>Een nieuwe gebruiker toevoegen en een rol toewijzen
1. Blade gebruikers hello, klik op **toevoegen** tooopen hello **toevoegen toegang blade** kunt u een gebruiker, groep of toepassing toevoegen, en een toothem rol toewijzen.  
   
   ![Gebruiker toevoegen](media/automation-role-based-access-control/automation-02-add-user.png)  
2. Selecteer een rol in de lijst met beschikbare rollen Hallo. We kiezen Hallo **lezer** rol, maar u kunt een van de Hallo beschikbare ingebouwde rol die ondersteuning biedt voor een Automation-Account of elke aangepaste rol die u hebt gedefinieerd.  
   
   ![Rol selecteren](media/automation-role-based-access-control/automation-03-select-role.png)  
3. Klik op **gebruikers toevoegen** tooopen hello **gebruikers toevoegen** blade. Als u alle gebruikers, groepen of toepassingen toomanage hebt toegevoegd en uw abonnement vervolgens die gebruikers worden weergegeven en kunt u deze selecteren tooadd toegang. Als er niet alle gebruikers die worden vermeld of als u geïnteresseerd bent in het toevoegen van Hallo-gebruiker niet wordt vermeld klikt u op **uitnodigen** tooopen hello **een gast uitnodigen** blade waar u een gebruiker met een geldig Microsoft-account kunt uitnodigen e-mailadres zoals Outlook.com, OneDrive of Xbox Live-ID. Wanneer u e-mailadres van de gebruiker Hallo Hallo hebt ingevoerd, klikt u op **Selecteer** tooadd Hallo gebruiker en klik vervolgens op **OK**. 
   
   ![Gebruikers toevoegen](media/automation-role-based-access-control/automation-04-add-users.png)  
   
   Nu u Hallo gebruiker toegevoegd ziet toohello **gebruikers** blade Hello **lezer** rol die is toegewezen.  
   
   ![Gebruikers weergeven](media/automation-role-based-access-control/automation-05-list-users.png)  
   
   U kunt ook een gebruiker, rol toohello vanuit Hallo toewijzen **rollen** blade. 
4. Klik op **rollen** van Hallo gebruikers blade tooopen hello **rollen blade**. U kunt deze blade Hallo-naam van Hallo-rol, Hallo aantal gebruikers en groepen toothat rol is toegewezen bekijken.
   
    ![Rol vanuit blade Gebruikers toewijzen](media/automation-role-based-access-control/automation-06-assign-role-from-users-blade.png)  
   
   > [!NOTE]
   > Op rollen gebaseerde toegangsbeheer kan alleen worden ingesteld op Hallo niveau Automation-Account en niet op een resource onderstaande Hallo Automation-Account.
   > 
   > 
   
    U kunt meer dan één rol tooa gebruiker, groep of toepassing. Bijvoorbeeld, als we Hallo toevoegen **Automation-Operator** functie plus Hallo **rol Lezer** toohello gebruiker en vervolgens zij kunnen alle Hallo Automation-resources bekijken, evenals Hallo runbooktaken uitvoeren. U kunt Hallo dropdown tooview een lijst met rollen toegewezen toohello gebruiker uitbreiden.  
   
    ![Meerdere rollen weergeven](media/automation-role-based-access-control/automation-07-view-multiple-roles.png)  

### <a name="remove-a-user"></a>Een gebruiker verwijderen
Hallo-machtiging voor een gebruiker die Hallo Automation-Account niet beheert of die niet langer voor Hallo organisatie werkt, kunt u verwijderen. Volgende zijn stappen tooremove Hallo een gebruiker: 

1. Van Hallo **gebruikers** blade, selecteer Hallo roltoewijzing gewenste tooremove.
2. Klik op Hallo **verwijderen** knop op Hallo blade toewijzingdetails.
3. Klik op **Ja** tooconfirm verwijderen. 
   
   ![Gebruikers verwijderen](media/automation-role-based-access-control/automation-08-remove-users.png)  

## <a name="role-assigned-user"></a>Gebruiker met toegewezen rol
Wanneer u een gebruikersrol voor toegewezen tooa zich tootheir Automation-account aanmeldt, zien ze nu van de eigenaar van het Hallo-account die worden vermeld in de lijst met Hallo **standaardmappen**. Volgorde tooview Hallo Automation-account dat ze zijn toegevoegd aan, moet deze overschakelen van de standaardmap Hallo standaard directory toohello van de eigenaar.  

![Standaardmap](media/automation-role-based-access-control/automation-09-default-directory-in-role-assigned-user.png)  

### <a name="user-experience-for-automation-operator-role"></a>Gebruikerservaring voor de rol Automation-operator
Wanneer een gebruiker die is toegewezen toohello Automation-Operator rol weergaven Hallo ze worden toegewezen aan Automation-account, kunnen ze alleen Hallo lijst met runbooks, runbooktaken en planningen in Hallo Automation-account hebt gemaakt, maar hun definitie niet weergeven. Ze kunnen starten, stoppen, onderbreken, hervatten of Hallo runbook-taak plannen. Hallo gebruiker geen toegang tot tooother Automation-resources zoals configuraties, hybrid worker-groepen of DSC-knooppunten.  

![Er is geen tooresourcres toegang](media/automation-role-based-access-control/automation-10-no-access-to-resources.png)  

Wanneer Hallo gebruiker op Hallo runbook klikt, zijn hello opdrachten tooview Hallo bron of Hallo runbook bewerken niet beschikbaar omdat rol Automation-operator Hallo toothem toegang niet is toegestaan.  

![Er is geen toegang tot tooedit runbook](media/automation-role-based-access-control/automation-11-no-access-to-edit-runbook.png)  

Hallo tooview en toocreate schema's toegang hebben, maar de gebruiker heeft geen toegang tot tooany andere assettypen.  

![Er is geen tooassets toegang](media/automation-role-based-access-control/automation-12-no-access-to-assets.png)  

Deze gebruiker ook geen toegang tot tooview hello webhooks die zijn gekoppeld aan een runbook

![Er is geen toowebhooks toegang](media/automation-role-based-access-control/automation-13-no-access-to-webhooks.png)  

## <a name="configure-rbac-for-your-automation-account-using-azure-powershell"></a>RBAC configureren voor uw Automation-account met Azure PowerShell
Op rollen gebaseerde toegang kan ook worden geconfigureerd tooan Automation-Account met de volgende Hallo [Azure PowerShell-cmdlets](../active-directory/role-based-access-control-manage-access-powershell.md).

• Met [Get-AzureRmRoleDefinition](https://msdn.microsoft.com/library/mt603792.aspx) wordt een lijst weergegeven van alle RBAC-rollen die beschikbaar zijn in Azure Active Directory. U kunt deze opdracht samen met de Hallo **naam** eigenschap toolist alle acties die kunnen worden uitgevoerd door een specifieke rol Hallo.  
    **Voorbeeld:**  
    ![Roldefinitie ophalen](media/automation-role-based-access-control/automation-14-get-azurerm-role-definition.png)  

• [Get-AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt619413.aspx) een lijst met Azure AD RBAC-roltoewijzingen op Hallo opgegeven bereik. Zonder parameters retourneert deze opdracht alle roltoewijzingen van Hallo die via het Hallo-abonnement. Gebruik Hallo **ExpandPrincipalGroups** parameter toolist toegangstoewijzingen voor Hallo opgegeven gebruiker, evenals Hallo groepen Hallo gebruiker lid is van.  
    **Voorbeeld:** gebruik Hallo volgende opdracht uit toolist alle Hallo-gebruikers en de bijbehorende rollen binnen een automation-account.

    Get-AzureRMRoleAssignment -scope “/subscriptions/<SubscriptionID>/resourcegroups/<Resource Group Name>/Providers/Microsoft.Automation/automationAccounts/<Automation Account Name>” 

![Roltoewijzing ophalen](media/automation-role-based-access-control/automation-15-get-azurerm-role-assignment.png)

• [New AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt603580.aspx) tooassign toegang toousers, groepen en toepassingen tooa bepaald bereik.  
    **Voorbeeld:** gebruik Hallo volgende opdracht tooassign Hallo 'Automation-Operator' rol voor een gebruiker in Hallo Automation-accountbereik.

    New-AzureRmRoleAssignment -SignInName <sign-in Id of a user you wish toogrant access> -RoleDefinitionName "Automation operator" -Scope “/subscriptions/<SubscriptionID>/resourcegroups/<Resource Group Name>/Providers/Microsoft.Automation/automationAccounts/<Automation Account Name>”  

![Nieuwe roltoewijzing](media/automation-role-based-access-control/automation-16-new-azurerm-role-assignment.png)

• Gebruik [Remove-AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt603781.aspx) tooremove toegang van een opgegeven gebruiker, groep of toepassing van een bepaald bereik.  
    **Voorbeeld:** gebruik Hallo volgende opdracht tooremove Hallo gebruiker uit Hallo 'Automation-Operator'-rol in Hallo Automation-accountbereik.

    Remove-AzureRmRoleAssignment -SignInName <sign-in Id of a user you wish tooremove> -RoleDefinitionName "Automation Operator" -Scope “/subscriptions/<SubscriptionID>/resourcegroups/<Resource Group Name>/Providers/Microsoft.Automation/automationAccounts/<Automation Account Name>”

Vervang in Hallo bovenstaande voorbeelden **Id aanmelden**, **abonnements-Id**, **Resourcegroepnaam** en **Automation-accountnaam** met uw accountdetails. Kies **Ja** wanneer tooconfirm gevraagd voordat u doorgaat tooremove gebruiker roltoewijzing.   

## <a name="next-steps"></a>Volgende stappen
* Voor informatie over de verschillende manieren tooconfigure RBAC voor Azure Automation, Raadpleeg te[RBAC met Azure PowerShell beheren](../active-directory/role-based-access-control-manage-access-powershell.md).
* Zie voor meer informatie op verschillende manieren toostart een runbook [een runbook starten](automation-starting-a-runbook.md)
* Voor informatie over de verschillende runbooktypen, Raadpleeg te[Azure Automation-runbooktypen](automation-runbook-types.md)

