---
title: Voorbeelden voor het beheren van groepen in Azure Active Directory aaaPowerShell | Microsoft Docs
description: Op deze pagina toohelp van PowerShell-voorbeelden vindt u uw groepen in Azure Active Directory beheren
keywords: Azure AD, Azure Active Directory PowerShell, groepen, groepsbeheer
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 7a5023dc-2727-4c25-8254-b531fc3244ac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: rodejo
ms.openlocfilehash: ba049babc436e99a290f20899b3a87bcfa811d9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-version-2-cmdlets-for-group-management"></a>Azure Active Directory-cmdlets van versie 2 voor groepsbeheer
> [!div class="op_single_selector"]
> * [Azure Portal](active-directory-groups-create-azure-portal.md)
> * [Klassieke Azure Portal](active-directory-accessmanagement-manage-groups.md)
> * [PowerShell](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

Dit artikel bevat voorbeelden van hoe toouse PowerShell toomanage uw groepen in Azure Active Directory (Azure AD).  Deze ook ziet u hoe de tooget instellen met hello Azure AD PowerShell-module. Eerst moet u [hello Azure AD PowerShell-module downloaden](https://www.powershellgallery.com/packages/AzureAD/).

## <a name="installing-hello-azure-ad-powershell-module"></a>Hello Azure AD PowerShell-module installeren
tooinstall hello Azure AD PowerShell-module, gebruikt u Hallo volgende opdrachten:

    PS C:\Windows\system32> install-module azuread

tooverify die Hallo module is geïnstalleerd, Hallo volgende opdracht gebruiken:

    PS C:\Windows\system32> get-module azuread

    ModuleType Version      Name                                ExportedCommands
    ---------- ---------    ----                                ----------------
    Binary     2.0.0.115    azuread                      {Add-AzureADAdministrati...}

U kunt nu starten met Hallo-cmdlets in Hallo-module. Raadpleeg voor een volledige beschrijving van de cmdlets Hallo in hello Azure AD-module toohello online naslagdocumentatie voor [Azure Active Directory PowerShell versie 2](/powershell/azure/install-adv2?view=azureadps-2.0).

## <a name="connecting-toohello-directory"></a>Verbinding maken met toohello directory
Voordat u kunt het beheer van groepen met behulp van Azure AD PowerShell-cmdlets, moet u uw directory PowerShell-sessie toohello u toomanage wilt verbinden. Hallo volgende opdracht gebruiken:

    PS C:\Windows\system32> Connect-AzureAD

Hallo cmdlet vraagt naar Hallo referenties die u wilt dat toouse tooaccess uw directory. In dit voorbeeld gebruiken we karen@drumkit.onmicrosoft.com tooaccess Hallo demonstratie directory. Hallo cmdlet retourneert een bevestiging tooshow Hallo-sessie met succes was verbonden tooyour directory:

    Account                       Environment Tenant
    -------                       ----------- ------
    Karen@drumkit.onmicrosoft.com AzureCloud  85b5ff1e-0402-400c-9e3c-0f…

U kunt nu starten met Hallo AzureAD cmdlets toomanage groepen in uw directory.

## <a name="retrieving-groups"></a>Bij het ophalen van groepen
de bestaande groepen tooretrieve van uw directory die kunt u Hallo de cmdlet Get-AzureADGroups. tooretrieve alle groepen in de directory hello, gebruik de cmdlet Hallo zonder parameters:

    PS C:\Windows\system32> get-azureadgroup

Hallo cmdlet retourneert alle groepen in gekoppelde Hallo-adreslijst.

Hallo - object-id-parameter tooretrieve kunt u een specifieke groep waarvoor u een van de groep Hallo objectID opgeven:

    PS C:\Windows\system32> get-azureadgroup -ObjectId e29bae11-4ac0-450c-bc37-6dae8f3da61b

Hallo cmdlet retourneert nu Hallo-groep waarvan objectID overeenkomt met de waarde Hallo van Hallo-parameter die u hebt ingevoerd:

    DeletionTimeStamp            :
    ObjectId                     : e29bae11-4ac0-450c-bc37-6dae8f3da61b
    ObjectType                   : Group
    Description                  :
    DirSyncEnabled               :
    DisplayName                  : Pacific NW Support
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 9bb4139b-60a1-434a-8c0d-7c1f8eee2df9
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

U kunt zoeken naar een specifieke groep met Hallo - filter-parameter. Deze parameter heeft een ODATA-filter-component en resulteert in alle groepen die overeenkomen met de Hallo-filter, zoals in het volgende voorbeeld Hallo:

    PS C:\Windows\system32> Get-AzureADGroup -Filter "DisplayName eq 'Intune Administrators'"


    DeletionTimeStamp            :
    ObjectId                     : 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df
    ObjectType                   : Group
    Description                  : Intune Administrators
    DirSyncEnabled               :
    DisplayName                  : Intune Administrators
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 4dd067a0-6515-4f23-968a-cc2ffc2eff5c
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

> [!NOTE] 
> Hallo AzureAD PowerShell-cmdlets Hallo OData-query die standaard worden geïmplementeerd. Zie voor meer informatie **$filter** in [OData-query systeemopties Hallo OData-eindpunt met](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter).

## <a name="creating-groups"></a>Groepen maken
een nieuwe groep in uw directory, gebruik de cmdlet New-AzureADGroup hello toocreate. Deze cmdlet maakt een nieuwe beveiligingsgroep met de naam 'Marketing':

    PS C:\Windows\system32> New-AzureADGroup -Description "Marketing" -DisplayName "Marketing" -MailEnabled $false -SecurityEnabled $true -MailNickName "Marketing"

## <a name="updating-groups"></a>Bijwerken van groepen
een bestaande groep tooupdate Hallo Set AzureADGroup cmdlet gebruiken. In dit voorbeeld wijzigt we Hallo eigenschap DisplayName van Hallo groep 'Intune-beheerders'. We je eerst Hallo-groep met behulp van Hallo Get AzureADGroup cmdlet en filteren met Hallo DisplayName kenmerk zoeken:

    PS C:\Windows\system32> Get-AzureADGroup -Filter "DisplayName eq 'Intune Administrators'"


    DeletionTimeStamp            :
    ObjectId                     : 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df
    ObjectType                   : Group
    Description                  : Intune Administrators
    DirSyncEnabled               :
    DisplayName                  : Intune Administrators
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 4dd067a0-6515-4f23-968a-cc2ffc2eff5c
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

Vervolgens wijzigt we Hallo beschrijving toohello nieuwe waarde van de eigenschap 'Intune apparaat Administrators':

    PS C:\Windows\system32> Set-AzureADGroup -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -Description "Intune Device Administrators"

Is bijgewerkt tooreflect nieuwe waarde in Media Player Hallo nu als we Hallo groep opnieuw vinden, ziet u de eigenschap Description Hallo:

    PS C:\Windows\system32> Get-AzureADGroup -Filter "DisplayName eq 'Intune Administrators'"


    DeletionTimeStamp            :
    ObjectId                     : 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df
    ObjectType                   : Group
    Description                  : Intune Device Administrators
    DirSyncEnabled               :
    DisplayName                  : Intune Administrators
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 4dd067a0-6515-4f23-968a-cc2ffc2eff5c
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

## <a name="deleting-groups"></a>Groepen verwijderen
groepen van uw directory toodelete Hallo verwijderen AzureADGroup cmdlet als volgt gebruiken:

    PS C:\Windows\system32> Remove-AzureADGroup -ObjectId b11ca53e-07cc-455d-9a89-1fe3ab24566b

## <a name="managing-members-of-groups"></a>Leden van groepen beheren
Als u moet de nieuwe groep van leden tooa tooadd, Hallo toevoegen AzureADGroupMember cmdlet gebruiken. Met deze opdracht wordt een lid toohello Intune-beheerders groep die wordt gebruikt in het vorige voorbeeld Hallo toegevoegd:

    PS C:\Windows\system32> Add-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

Hallo - object-id-parameter is Hallo ObjectID van Hallo groep toowhich willen we tooadd lid en Hallo - RefObjectId is Hallo object-id van gebruiker Hallo willen we tooadd als een lid toohello-groep.

tooget hello bestaande leden van een groep gebruikt de cmdlet Get-AzureADGroupMember hello, zoals in dit voorbeeld:

    PS C:\Windows\system32> Get-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          72cd4bbd-2594-40a2-935c-016f3cfeeeea User
                          8120cc36-64b4-4080-a9e8-23aa98e8b34f User

tooremove hello lid we toegevoegd eerder toohello groep gebruik Hallo verwijderen AzureADGroupMember cmdlet, zoals hier wordt weergegeven:

    PS C:\Windows\system32> Remove-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -MemberId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

tooverify hello groep lidmaatschappen van een gebruiker Hallo Selecteer AzureADGroupIdsUserIsMemberOf cmdlet gebruiken. Deze cmdlet wordt als de parameters Hallo object-id van de gebruiker Hallo voor welke toocheck Hallo-groepslidmaatschappen en een lijst met groepen voor welke toocheck Hallo lidmaatschappen. Hallo-lijst met groepen moet zijn opgegeven in Hallo vorm van een complex variabele van type 'Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck', dus we eerst moet een variabele met dit type maken:

    PS C:\Windows\system32> $g = new-object Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck

We vervolgens opgeven waarden voor Hallo groupIds toocheck in Hallo kenmerk 'GroupIds' van deze variabele complex:

    PS C:\Windows\system32> $g.GroupIds = "b11ca53e-07cc-455d-9a89-1fe3ab24566b", "31f1ff6c-d48c-4f8a-b2e1-abca7fd399df"

Nu we toocheck Hallo groepslidmaatschappen van een gebruiker met ObjectID 72cd4bbd-2594-40a2-935c-016f3cfeeeea tegen Hallo groepen in $g kunt dat we moeten gebruiken:

    PS C:\Windows\system32> Select-AzureADGroupIdsUserIsMemberOf -ObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea -GroupIdsForMembershipCheck $g

    OdataMetadata                                                                                                 Value
    -------------                                                                                                  -----
    https://graph.windows.net/85b5ff1e-0402-400c-9e3c-0f9e965325d1/$metadata#Collection(Edm.String)             {31f1ff6c-d48c-4f8a-b2e1-abca7fd399df}


Hallo-waarde die het resultaat is een lijst met groepen waarvan deze gebruiker lid is. U kunt deze methode toocheck contactpersonen, groepen of Service-Principals lidmaatschap voor een opgegeven lijst met groepen met behulp van de Select-AzureADGroupIdsContactIsMemberOf, selecteer AzureADGroupIdsGroupIsMemberOf ook toepassen of Selecteer AzureADGroupIdsServicePrincipalIsMemberOf

## <a name="managing-owners-of-groups"></a>Eigenaren van groepen beheren
tooadd eigenaars tooa groep, gebruik de cmdlet Add-AzureADGroupOwner Hallo:

    PS C:\Windows\system32> Add-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

Hallo - object-id-parameter is Hallo ObjectID van Hallo groep toowhich willen we tooadd een eigenaar en Hallo - RefObjectId is Hallo object-id van gebruiker Hallo willen we tooadd als een eigenaar van het Hallo-groep.

tooretrieve hello eigenaren van een groep, gebruikt u Hallo Get AzureADGroupOwner cmdlet:

    PS C:\Windows\system32> Get-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

Hallo cmdlet retourneert Hallo lijst met eigenaren voor de opgegeven groep Hallo:

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          e831b3fd-77c9-49c7-9fca-de43e109ef67 User

Als u een eigenaar van een groep tooremove wilt, gebruikt u Hallo verwijderen AzureADGroupOwner cmdlet:

    PS C:\Windows\system32> remove-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -OwnerId e831b3fd-77c9-49c7-9fca-de43e109ef67

## <a name="reserved-aliases"></a>Gereserveerde aliassen 
Wanneer een groep is gemaakt, kunnen bepaalde eindpunten Hallo eindgebruiker toospecify een mailNickname of alias toobe gebruikt als onderdeel van het e-mailadres van de groep Hallo Hallo. Groepen met bijzondere rechten e-aliassen te volgen hello kunnen alleen worden gemaakt door een globale beheerder van Azure AD. 
  
* misbruik 
* Beheerder 
* Beheerder 
* hostmaster 
* majordomo 
* postbeheerder 
* hoofdmap 
* Beveiligen 
* Beveiliging 
* SSL-beheerder 
* beheerder 

## <a name="next-steps"></a>Volgende stappen
U vindt meer Azure Active Directory PowerShell-documentatie op [Azure Active Directory-Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0).

* [Tooresources toegang beheren met Azure Active Directory-groepen](active-directory-manage-groups.md)
* [Uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md)
