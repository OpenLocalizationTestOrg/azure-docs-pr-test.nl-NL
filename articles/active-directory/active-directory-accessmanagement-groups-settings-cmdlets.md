---
title: Groepsinstellingen aaaConfigure met Azure Active Directory-cmdlets | Microsoft Docs
description: Hoe Hallo instellingen beheren voor groepen met behulp van Azure Active Directory-cmdlets
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 9f2090e6-3af4-4f07-bbb2-1d18dae89b73
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: it-pro;
ms.openlocfilehash: 46db49d9dec3eaa41c97ca74c57854189eddc16d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-cmdlets-for-configuring-group-settings"></a>Azure Active Directory cmdlets voor het configureren van groepsinstellingen

> [!IMPORTANT]
> Deze inhoud is van toepassing alleen tooOffice 365-groepen. Voor meer informatie over het tooallow gebruikers toocreate beveiligingsgroepen ingesteld `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True` zoals beschreven in [Set-MSOLCompanySettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0). 

Instellingen voor Office 365-groepen zijn geconfigureerd met een object-instellingen en een SettingsTemplate-object. In eerste instantie is er geen voor instellingenobjecten in uw directory omdat uw directory is geconfigureerd met de standaardinstellingen Hallo. standaardinstellingen voor toochange hello, moet u een nieuw object voor instellingen met een sjabloon instellingen maken. Instellingen voor sjablonen zijn gedefinieerd door Microsoft. Er zijn verschillende sjablonen met verschillende instellingen. Groepsinstellingen tooconfigure Office 365 voor uw directory, dat u met de naam 'Group.Unified' Hallo-sjabloon gebruiken. de instellingen voor Office 365 tooconfigure op één groep Hallo-sjabloon met de naam 'Group.Unified.Guest' gebruiken. Deze sjabloon is gebruikte toomanage Gast toegangsgroep tooan Office 365. 

Hallo cmdlets maken deel uit van hello Azure Active Directory PowerShell V2-module. Zie voor instructies hoe toodownload en Hallo-module installeren op uw computer Hallo artikel [Azure Active Directory PowerShell versie 2](https://docs.microsoft.com/powershell/azuread/). U kunt installeren Hallo versie 2-release van Hallo module op basis van [Hallo PowerShell gallery](https://www.powershellgallery.com/packages/AzureAD/).

## <a name="retrieve-a-specific-settings-value"></a>De waarde van een specifieke instellingen ophalen
Als u Hallo naam weet van Hallo instelling die u wilt dat tooretrieve, kunt u Hallo hieronder cmdlet tooretrieve Hallo huidige waarde van de instellingen. In dit voorbeeld ophaalt we Hallo-waarde voor een instelling met de naam 'UsageGuidelinesUrl'. U vindt dat meer informatie over instellingen voor directory en hun namen verder omlaag in dit artikel.

```powershell
(Get-AzureADDirectorySetting).Values | Where-Object -Property Name -Value UsageGuidelinesUrl -EQ
```

## <a name="create-settings-at-hello-directory-level"></a>Instellingen op Hallo directory niveau maken
Deze stappen maken instellingen op het niveau van de directory die tooall Office 365-groepen (Unified groepen) in de map Hallo toepassen.

1. Hallo DirectorySettings cmdlets, moet u Hallo-ID van Hallo SettingsTemplate u toouse wilt opgeven. Als u deze ID niet weet, retourneert deze cmdlet Hallo lijst met alle instellingen sjablonen:
  
  ```
  PS C:> Get-AzureADDirectorySettingTemplate
  ```
  De aanroep van deze cmdlet retourneert alle sjablonen die beschikbaar zijn:
  
  ```
  Id                                   DisplayName         Description
  --                                   -----------         -----------
  62375ab9-6b52-47ed-826b-58e47e0e304b Group.Unified       ...
  08d542b9-071f-4e16-94b0-74abb372e3d9 Group.Unified.Guest Settings for a specific Unified Group
  16933506-8a8d-4f0d-ad58-e1db05a5b929 Company.BuiltIn     Setting templates define hello different settings that can be used for hello associ...
  4bc7f740-180e-4586-adb6-38b2e9024e6b Application...
  898f1161-d651-43d1-805c-3b0b388a9fc2 Custom Policy       Settings ...
  5cf42378-d67d-4f36-ba46-e8b86229381d Password Rule       Settings ...
  ```
2. een URL van de richtlijn gebruik tooadd, moet u eerst tooget hello SettingsTemplate-object dat Hallo gebruik richtlijn URL-waarde bepaalt; dat wil zeggen, Hallo Group.Unified sjabloon:
  
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 62375ab9-6b52-47ed-826b-58e47e0e304b
  ```
3. Maak vervolgens een nieuw object van instellingen op basis van die sjabloon:
  
  ```
  $Setting = $template.CreateDirectorySetting()
  ```  
4. Werk vervolgens de richtlijn gebruikswaarde Hallo:
  
  ```
  $setting["UsageGuidelinesUrl"] = "<https://guideline.com>"
  ```  
5. Ten slotte Hallo-instellingen toepassen:
  
  ```
  New-AzureADDirectorySetting -DirectorySetting $setting
  ```

Na geslaagde voltooiing retourneert Hallo cmdlet Hallo-ID van nieuwe instellingenobject Hallo:
  ```
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323             62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```
Hier zijn gedefinieerd in Hallo Group.Unified SettingsTemplate Hallo-instellingen.

| **Instelling** | **Beschrijving** |
| --- | --- |
|  <ul><li>EnableGroupCreation<li>Type: Booleaanse<li>Standaard: True |Hallo-vlag die aangeeft of het maken van Unified in Hallo directory is toegestaan. |
|  <ul><li>GroupCreationAllowedGroupId<li>Type: String<li>Standaardwaarde: ' " |GUID van de beveiligingsgroep Hallo voor welke Hallo leden toocreate Unified groepen zijn toegestaan, zelfs wanneer EnableGroupCreation == false. |
|  <ul><li>UsageGuidelinesUrl<li>Type: String<li>Standaardwaarde: ' " |Een koppeling toohello richtlijnen voor het gebruik van groep. |
|  <ul><li>ClassificationDescriptions<li>Type: String<li>Standaardwaarde: ' " | Een door komma's gescheiden lijst met beschrijvingen van de classificatie. |
|  <ul><li>DefaultClassification<li>Type: String<li>Standaardwaarde: ' " | Hallo-classificatie die toobe gebruikt als Hallo Standaardclassificatie voor een groep als deze is niet opgegeven.|
|  <ul><li>PrefixSuffixNamingRequirement<li>Type: String<li>Standaardwaarde: ' " |Nog niet geïmplementeerd
|  <ul><li>AllowGuestsToBeGroupOwner<li>Type: Booleaanse<li>Standaard: False | Een Boolean die aangeeft of een gastgebruiker moet een eigenaar van de groepen kan worden. |
|  <ul><li>AllowGuestsToAccessGroups<li>Type: Booleaanse<li>Standaard: True | Een Boolean die aangeeft of een gastgebruiker toegangsgroepen van tooUnified inhoud kan hebben. |
|  <ul><li>GuestUsageGuidelinesUrl<li>Type: String<li>Standaardwaarde: ' " | Hallo-url van een koppeling toohello Gast richtlijnen. |
|  <ul><li>AllowToAddGuests<li>Type: Booleaanse<li>Standaard: True | Een boolean die aangeeft of of niet is toegestaan tooadd gasten toothis directory.|
|  <ul><li>ClassificationList<li>Type: String<li>Standaardwaarde: ' " |Een door komma's gescheiden lijst met geldige classificatiewaarden die toegepast tooUnified groepen worden kunnen. |
|  <ul><li>EnableGroupCreation<li>Type: Booleaanse<li>Standaard: True | Een boolean die aangeeft of niet-beheerders van nieuwe maken kunnen geïntegreerde groepen. |


## <a name="read-settings-at-hello-directory-level"></a>Instellingen lezen op Hallo directory niveau
Volgende stappen uit op het niveau van de directory-instellingen die van toepassing zijn tooall Office-groepen in de map Hallo gelezen.

1. Lees alle bestaande directoryinstellingen:
  ```
  Get-AzureADDirectorySetting -All $True
  ```
  Deze cmdlet retourneert een lijst met alle directoryinstellingen:
  ```
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```

2. Lees alle instellingen voor een specifieke groep:
  ```
  Get-AzureADObjectSetting -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -TargetType Groups
  ```

3. Lezen van alle waarden in de directory instellingen van een specifieke map instellingen-object met Id-GUID-instellingen:
  ```
  (Get-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323).values
  ```
  Deze cmdlet retourneert Hallo namen en waarden in deze object-instellingen voor deze specifieke groep:
  ```
  Name                          Value
  ----                          -----
  ClassificationDescriptions
  DefaultClassification
  PrefixSuffixNamingRequirement
  AllowGuestsToBeGroupOwner     False 
  AllowGuestsToAccessGroups     True
  GuestUsageGuidelinesUrl
  GroupCreationAllowedGroupId
  AllowToAddGuests              True
  UsageGuidelinesUrl            <https://guideline.com>
  ClassificationList
  EnableGroupCreation           True
  ```

## <a name="update-settings-for-a-specific-group"></a>Instellingen voor een specifieke groep bijwerken

1. Zoeken naar Hallo instellingen sjabloon met de naam 'Groups.Unified.Guest'
  ```
  Get-AzureADDirectorySettingTemplate
  
  Id                                   DisplayName            Description
  --                                   -----------            -----------
  62375ab9-6b52-47ed-826b-58e47e0e304b Group.Unified          ...
  08d542b9-071f-4e16-94b0-74abb372e3d9 Group.Unified.Guest    Settings for a specific Unified Group
  4bc7f740-180e-4586-adb6-38b2e9024e6b Application            ...
  898f1161-d651-43d1-805c-3b0b388a9fc2 Custom Policy Settings ...
  5cf42378-d67d-4f36-ba46-e8b86229381d Password Rule Settings ...
  ```
2. Hallo sjabloonobject voor Hallo Groups.Unified.Guest sjabloon ophalen:
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 08d542b9-071f-4e16-94b0-74abb372e3d9
  ```
3. Maak een nieuw instellingenobject van Hallo sjabloon:
  ```
  $Setting = $Template.CreateDirectorySetting()
  ```

4. Hallo toohello vereist instellingswaarde instellen:
  ```
  $Setting["AllowToAddGuests"]=$False
  ```
5. Nieuwe instelling voor de vereiste groep Hallo Hallo op Hallo directory maken:
  ```
  New-AzureADObjectSetting -TargetType Groups -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -DirectorySetting $Setting
  
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  25651479-a26e-4181-afce-ce24111b2cb5             08d542b9-071f-4e16-94b0-74abb372e3d9 {class SettingValue {...
  ```

## <a name="update-settings-at-hello-directory-level"></a>Update-instellingen op Hallo directory niveau

Volgende stappen uit bijwerken op het niveau van de directory-instellingen die van toepassing zijn tooall Unified groepen in Hallo directory. Deze voorbeelden wordt ervan uitgegaan dat er is al een object-instellingen in uw directory.

1. Bestaand instellingenobject Hallo vinden:
  ```
  Get-AzureADDirectorySetting | Where-object -Property Displayname -Value "Group.Unified" -EQ
  
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  
  $setting = Get-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323
  ```
2. Hallo waarde bijwerken:
  
  ```
  $Setting["AllowToAddGuests"] = "false"
  ```
3. Hallo-instelling bijwerken:
  
  ```
  Set-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323 -DirectorySetting $Setting
  ```

## <a name="remove-settings-at-hello-directory-level"></a>Verwijder de instellingen op Hallo directory niveau
Deze stap verwijdert-instellingen op het niveau van de directory die van toepassing zijn tooall Office-groepen in Hallo-directory.
  ```
  Remove-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323c
  ```

## <a name="cmdlet-syntax-reference"></a>Verwijzing naar de cmdlet
U vindt meer Azure Active Directory PowerShell-documentatie op [Azure Active Directory-Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0).

## <a name="additional-reading"></a>Aanvullende bronnen

* [Tooresources toegang beheren met Azure Active Directory-groepen](active-directory-manage-groups.md)
* [Uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md)
