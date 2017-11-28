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
# <a name="azure-active-directory-cmdlets-for-configuring-group-settings"></a><span data-ttu-id="adbb1-103">Azure Active Directory cmdlets voor het configureren van groepsinstellingen</span><span class="sxs-lookup"><span data-stu-id="adbb1-103">Azure Active Directory cmdlets for configuring group settings</span></span>

> [!IMPORTANT]
> <span data-ttu-id="adbb1-104">Deze inhoud is van toepassing alleen tooOffice 365-groepen.</span><span class="sxs-lookup"><span data-stu-id="adbb1-104">This content applies only tooOffice 365 groups.</span></span> <span data-ttu-id="adbb1-105">Voor meer informatie over het tooallow gebruikers toocreate beveiligingsgroepen ingesteld `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True` zoals beschreven in [Set-MSOLCompanySettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).</span><span class="sxs-lookup"><span data-stu-id="adbb1-105">For more information on how tooallow users toocreate Security groups, set `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True` as described in [Set-MSOLCompanySettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).</span></span> 

<span data-ttu-id="adbb1-106">Instellingen voor Office 365-groepen zijn geconfigureerd met een object-instellingen en een SettingsTemplate-object.</span><span class="sxs-lookup"><span data-stu-id="adbb1-106">Office 365 Groups settings are configured using a Settings object and a SettingsTemplate object.</span></span> <span data-ttu-id="adbb1-107">In eerste instantie is er geen voor instellingenobjecten in uw directory omdat uw directory is geconfigureerd met de standaardinstellingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="adbb1-107">Initially, you don't see any Settings objects in your directory, because your directory is configured with hello default settings.</span></span> <span data-ttu-id="adbb1-108">standaardinstellingen voor toochange hello, moet u een nieuw object voor instellingen met een sjabloon instellingen maken.</span><span class="sxs-lookup"><span data-stu-id="adbb1-108">toochange hello default settings, you must create a new settings object using a settings template.</span></span> <span data-ttu-id="adbb1-109">Instellingen voor sjablonen zijn gedefinieerd door Microsoft.</span><span class="sxs-lookup"><span data-stu-id="adbb1-109">Settings templates are defined by Microsoft.</span></span> <span data-ttu-id="adbb1-110">Er zijn verschillende sjablonen met verschillende instellingen.</span><span class="sxs-lookup"><span data-stu-id="adbb1-110">There are several different settings templates.</span></span> <span data-ttu-id="adbb1-111">Groepsinstellingen tooconfigure Office 365 voor uw directory, dat u met de naam 'Group.Unified' Hallo-sjabloon gebruiken.</span><span class="sxs-lookup"><span data-stu-id="adbb1-111">tooconfigure Office 365 group settings for your directory, you use hello template named "Group.Unified".</span></span> <span data-ttu-id="adbb1-112">de instellingen voor Office 365 tooconfigure op één groep Hallo-sjabloon met de naam 'Group.Unified.Guest' gebruiken.</span><span class="sxs-lookup"><span data-stu-id="adbb1-112">tooconfigure Office 365 group settings on a single group, use hello template named "Group.Unified.Guest".</span></span> <span data-ttu-id="adbb1-113">Deze sjabloon is gebruikte toomanage Gast toegangsgroep tooan Office 365.</span><span class="sxs-lookup"><span data-stu-id="adbb1-113">This template is used toomanage guest access tooan Office 365 group.</span></span> 

<span data-ttu-id="adbb1-114">Hallo cmdlets maken deel uit van hello Azure Active Directory PowerShell V2-module.</span><span class="sxs-lookup"><span data-stu-id="adbb1-114">hello cmdlets are part of hello Azure Active Directory PowerShell V2 module.</span></span> <span data-ttu-id="adbb1-115">Zie voor instructies hoe toodownload en Hallo-module installeren op uw computer Hallo artikel [Azure Active Directory PowerShell versie 2](https://docs.microsoft.com/powershell/azuread/).</span><span class="sxs-lookup"><span data-stu-id="adbb1-115">For instructions how toodownload and install hello module on your computer, see hello article [Azure Active Directory PowerShell Version 2](https://docs.microsoft.com/powershell/azuread/).</span></span> <span data-ttu-id="adbb1-116">U kunt installeren Hallo versie 2-release van Hallo module op basis van [Hallo PowerShell gallery](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="adbb1-116">You can install hello version 2 release of hello module from [hello PowerShell gallery](https://www.powershellgallery.com/packages/AzureAD/).</span></span>

## <a name="retrieve-a-specific-settings-value"></a><span data-ttu-id="adbb1-117">De waarde van een specifieke instellingen ophalen</span><span class="sxs-lookup"><span data-stu-id="adbb1-117">Retrieve a specific settings value</span></span>
<span data-ttu-id="adbb1-118">Als u Hallo naam weet van Hallo instelling die u wilt dat tooretrieve, kunt u Hallo hieronder cmdlet tooretrieve Hallo huidige waarde van de instellingen.</span><span class="sxs-lookup"><span data-stu-id="adbb1-118">If you know hello name of hello setting you want tooretrieve, you can use hello below cmdlet tooretrieve hello current settings value.</span></span> <span data-ttu-id="adbb1-119">In dit voorbeeld ophaalt we Hallo-waarde voor een instelling met de naam 'UsageGuidelinesUrl'.</span><span class="sxs-lookup"><span data-stu-id="adbb1-119">In this example, we're retrieving hello value for a setting named "UsageGuidelinesUrl."</span></span> <span data-ttu-id="adbb1-120">U vindt dat meer informatie over instellingen voor directory en hun namen verder omlaag in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="adbb1-120">You can read more about directory settings and their names further down in this article.</span></span>

```powershell
(Get-AzureADDirectorySetting).Values | Where-Object -Property Name -Value UsageGuidelinesUrl -EQ
```

## <a name="create-settings-at-hello-directory-level"></a><span data-ttu-id="adbb1-121">Instellingen op Hallo directory niveau maken</span><span class="sxs-lookup"><span data-stu-id="adbb1-121">Create settings at hello directory level</span></span>
<span data-ttu-id="adbb1-122">Deze stappen maken instellingen op het niveau van de directory die tooall Office 365-groepen (Unified groepen) in de map Hallo toepassen.</span><span class="sxs-lookup"><span data-stu-id="adbb1-122">These steps create settings at directory level, which apply tooall Office 365 groups (Unified groups) in hello directory.</span></span>

1. <span data-ttu-id="adbb1-123">Hallo DirectorySettings cmdlets, moet u Hallo-ID van Hallo SettingsTemplate u toouse wilt opgeven.</span><span class="sxs-lookup"><span data-stu-id="adbb1-123">In hello DirectorySettings cmdlets, you must specify hello ID of hello SettingsTemplate you want toouse.</span></span> <span data-ttu-id="adbb1-124">Als u deze ID niet weet, retourneert deze cmdlet Hallo lijst met alle instellingen sjablonen:</span><span class="sxs-lookup"><span data-stu-id="adbb1-124">If you do not know this ID, this cmdlet returns hello list of all settings templates:</span></span>
  
  ```
  PS C:> Get-AzureADDirectorySettingTemplate
  ```
  <span data-ttu-id="adbb1-125">De aanroep van deze cmdlet retourneert alle sjablonen die beschikbaar zijn:</span><span class="sxs-lookup"><span data-stu-id="adbb1-125">This cmdlet call returns all templates that are available:</span></span>
  
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
2. <span data-ttu-id="adbb1-126">een URL van de richtlijn gebruik tooadd, moet u eerst tooget hello SettingsTemplate-object dat Hallo gebruik richtlijn URL-waarde bepaalt; dat wil zeggen, Hallo Group.Unified sjabloon:</span><span class="sxs-lookup"><span data-stu-id="adbb1-126">tooadd a usage guideline URL, first you need tooget hello SettingsTemplate object that defines hello usage guideline URL value; that is, hello Group.Unified template:</span></span>
  
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 62375ab9-6b52-47ed-826b-58e47e0e304b
  ```
3. <span data-ttu-id="adbb1-127">Maak vervolgens een nieuw object van instellingen op basis van die sjabloon:</span><span class="sxs-lookup"><span data-stu-id="adbb1-127">Next, create a new settings object based on that template:</span></span>
  
  ```
  $Setting = $template.CreateDirectorySetting()
  ```  
4. <span data-ttu-id="adbb1-128">Werk vervolgens de richtlijn gebruikswaarde Hallo:</span><span class="sxs-lookup"><span data-stu-id="adbb1-128">Then update hello usage guideline value:</span></span>
  
  ```
  $setting["UsageGuidelinesUrl"] = "<https://guideline.com>"
  ```  
5. <span data-ttu-id="adbb1-129">Ten slotte Hallo-instellingen toepassen:</span><span class="sxs-lookup"><span data-stu-id="adbb1-129">Finally, apply hello settings:</span></span>
  
  ```
  New-AzureADDirectorySetting -DirectorySetting $setting
  ```

<span data-ttu-id="adbb1-130">Na geslaagde voltooiing retourneert Hallo cmdlet Hallo-ID van nieuwe instellingenobject Hallo:</span><span class="sxs-lookup"><span data-stu-id="adbb1-130">Upon successful completion, hello cmdlet returns hello ID of hello new settings object:</span></span>
  ```
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323             62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```
<span data-ttu-id="adbb1-131">Hier zijn gedefinieerd in Hallo Group.Unified SettingsTemplate Hallo-instellingen.</span><span class="sxs-lookup"><span data-stu-id="adbb1-131">Here are hello settings defined in hello Group.Unified SettingsTemplate.</span></span>

| <span data-ttu-id="adbb1-132">**Instelling**</span><span class="sxs-lookup"><span data-stu-id="adbb1-132">**Setting**</span></span> | <span data-ttu-id="adbb1-133">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="adbb1-133">**Description**</span></span> |
| --- | --- |
|  <ul><li><span data-ttu-id="adbb1-134">EnableGroupCreation</span><span class="sxs-lookup"><span data-stu-id="adbb1-134">EnableGroupCreation</span></span><li><span data-ttu-id="adbb1-135">Type: Booleaanse</span><span class="sxs-lookup"><span data-stu-id="adbb1-135">Type: Boolean</span></span><li><span data-ttu-id="adbb1-136">Standaard: True</span><span class="sxs-lookup"><span data-stu-id="adbb1-136">Default: True</span></span> |<span data-ttu-id="adbb1-137">Hallo-vlag die aangeeft of het maken van Unified in Hallo directory is toegestaan.</span><span class="sxs-lookup"><span data-stu-id="adbb1-137">hello flag indicating whether Unified Group creation is allowed in hello directory.</span></span> |
|  <ul><li><span data-ttu-id="adbb1-138">GroupCreationAllowedGroupId</span><span class="sxs-lookup"><span data-stu-id="adbb1-138">GroupCreationAllowedGroupId</span></span><li><span data-ttu-id="adbb1-139">Type: String</span><span class="sxs-lookup"><span data-stu-id="adbb1-139">Type: String</span></span><li><span data-ttu-id="adbb1-140">Standaardwaarde: ' "</span><span class="sxs-lookup"><span data-stu-id="adbb1-140">Default: “”</span></span> |<span data-ttu-id="adbb1-141">GUID van de beveiligingsgroep Hallo voor welke Hallo leden toocreate Unified groepen zijn toegestaan, zelfs wanneer EnableGroupCreation == false.</span><span class="sxs-lookup"><span data-stu-id="adbb1-141">GUID of hello security group for which hello members are allowed toocreate Unified Groups even when EnableGroupCreation == false.</span></span> |
|  <ul><li><span data-ttu-id="adbb1-142">UsageGuidelinesUrl</span><span class="sxs-lookup"><span data-stu-id="adbb1-142">UsageGuidelinesUrl</span></span><li><span data-ttu-id="adbb1-143">Type: String</span><span class="sxs-lookup"><span data-stu-id="adbb1-143">Type: String</span></span><li><span data-ttu-id="adbb1-144">Standaardwaarde: ' "</span><span class="sxs-lookup"><span data-stu-id="adbb1-144">Default: “”</span></span> |<span data-ttu-id="adbb1-145">Een koppeling toohello richtlijnen voor het gebruik van groep.</span><span class="sxs-lookup"><span data-stu-id="adbb1-145">A link toohello Group Usage Guidelines.</span></span> |
|  <ul><li><span data-ttu-id="adbb1-146">ClassificationDescriptions</span><span class="sxs-lookup"><span data-stu-id="adbb1-146">ClassificationDescriptions</span></span><li><span data-ttu-id="adbb1-147">Type: String</span><span class="sxs-lookup"><span data-stu-id="adbb1-147">Type: String</span></span><li><span data-ttu-id="adbb1-148">Standaardwaarde: ' "</span><span class="sxs-lookup"><span data-stu-id="adbb1-148">Default: “”</span></span> | <span data-ttu-id="adbb1-149">Een door komma's gescheiden lijst met beschrijvingen van de classificatie.</span><span class="sxs-lookup"><span data-stu-id="adbb1-149">A comma-delimited list of classification descriptions.</span></span> |
|  <ul><li><span data-ttu-id="adbb1-150">DefaultClassification</span><span class="sxs-lookup"><span data-stu-id="adbb1-150">DefaultClassification</span></span><li><span data-ttu-id="adbb1-151">Type: String</span><span class="sxs-lookup"><span data-stu-id="adbb1-151">Type: String</span></span><li><span data-ttu-id="adbb1-152">Standaardwaarde: ' "</span><span class="sxs-lookup"><span data-stu-id="adbb1-152">Default: “”</span></span> | <span data-ttu-id="adbb1-153">Hallo-classificatie die toobe gebruikt als Hallo Standaardclassificatie voor een groep als deze is niet opgegeven.</span><span class="sxs-lookup"><span data-stu-id="adbb1-153">hello classification that is toobe used as hello default classification for a group if none was specified.</span></span>|
|  <ul><li><span data-ttu-id="adbb1-154">PrefixSuffixNamingRequirement</span><span class="sxs-lookup"><span data-stu-id="adbb1-154">PrefixSuffixNamingRequirement</span></span><li><span data-ttu-id="adbb1-155">Type: String</span><span class="sxs-lookup"><span data-stu-id="adbb1-155">Type: String</span></span><li><span data-ttu-id="adbb1-156">Standaardwaarde: ' "</span><span class="sxs-lookup"><span data-stu-id="adbb1-156">Default: “”</span></span> |<span data-ttu-id="adbb1-157">Nog niet geïmplementeerd</span><span class="sxs-lookup"><span data-stu-id="adbb1-157">Not implemented yet</span></span>
|  <ul><li><span data-ttu-id="adbb1-158">AllowGuestsToBeGroupOwner</span><span class="sxs-lookup"><span data-stu-id="adbb1-158">AllowGuestsToBeGroupOwner</span></span><li><span data-ttu-id="adbb1-159">Type: Booleaanse</span><span class="sxs-lookup"><span data-stu-id="adbb1-159">Type: Boolean</span></span><li><span data-ttu-id="adbb1-160">Standaard: False</span><span class="sxs-lookup"><span data-stu-id="adbb1-160">Default: False</span></span> | <span data-ttu-id="adbb1-161">Een Boolean die aangeeft of een gastgebruiker moet een eigenaar van de groepen kan worden.</span><span class="sxs-lookup"><span data-stu-id="adbb1-161">Boolean indicating whether or not a guest user can be an owner of groups.</span></span> |
|  <ul><li><span data-ttu-id="adbb1-162">AllowGuestsToAccessGroups</span><span class="sxs-lookup"><span data-stu-id="adbb1-162">AllowGuestsToAccessGroups</span></span><li><span data-ttu-id="adbb1-163">Type: Booleaanse</span><span class="sxs-lookup"><span data-stu-id="adbb1-163">Type: Boolean</span></span><li><span data-ttu-id="adbb1-164">Standaard: True</span><span class="sxs-lookup"><span data-stu-id="adbb1-164">Default: True</span></span> | <span data-ttu-id="adbb1-165">Een Boolean die aangeeft of een gastgebruiker toegangsgroepen van tooUnified inhoud kan hebben.</span><span class="sxs-lookup"><span data-stu-id="adbb1-165">Boolean indicating whether or not a guest user can have access tooUnified groups' content.</span></span> |
|  <ul><li><span data-ttu-id="adbb1-166">GuestUsageGuidelinesUrl</span><span class="sxs-lookup"><span data-stu-id="adbb1-166">GuestUsageGuidelinesUrl</span></span><li><span data-ttu-id="adbb1-167">Type: String</span><span class="sxs-lookup"><span data-stu-id="adbb1-167">Type: String</span></span><li><span data-ttu-id="adbb1-168">Standaardwaarde: ' "</span><span class="sxs-lookup"><span data-stu-id="adbb1-168">Default: “”</span></span> | <span data-ttu-id="adbb1-169">Hallo-url van een koppeling toohello Gast richtlijnen.</span><span class="sxs-lookup"><span data-stu-id="adbb1-169">hello url of a link toohello guest usage guidelines.</span></span> |
|  <ul><li><span data-ttu-id="adbb1-170">AllowToAddGuests</span><span class="sxs-lookup"><span data-stu-id="adbb1-170">AllowToAddGuests</span></span><li><span data-ttu-id="adbb1-171">Type: Booleaanse</span><span class="sxs-lookup"><span data-stu-id="adbb1-171">Type: Boolean</span></span><li><span data-ttu-id="adbb1-172">Standaard: True</span><span class="sxs-lookup"><span data-stu-id="adbb1-172">Default: True</span></span> | <span data-ttu-id="adbb1-173">Een boolean die aangeeft of of niet is toegestaan tooadd gasten toothis directory.</span><span class="sxs-lookup"><span data-stu-id="adbb1-173">A boolean indicating whether or not is allowed tooadd guests toothis directory.</span></span>|
|  <ul><li><span data-ttu-id="adbb1-174">ClassificationList</span><span class="sxs-lookup"><span data-stu-id="adbb1-174">ClassificationList</span></span><li><span data-ttu-id="adbb1-175">Type: String</span><span class="sxs-lookup"><span data-stu-id="adbb1-175">Type: String</span></span><li><span data-ttu-id="adbb1-176">Standaardwaarde: ' "</span><span class="sxs-lookup"><span data-stu-id="adbb1-176">Default: “”</span></span> |<span data-ttu-id="adbb1-177">Een door komma's gescheiden lijst met geldige classificatiewaarden die toegepast tooUnified groepen worden kunnen.</span><span class="sxs-lookup"><span data-stu-id="adbb1-177">A comma-delimited list of valid classification values that can be applied tooUnified Groups.</span></span> |
|  <ul><li><span data-ttu-id="adbb1-178">EnableGroupCreation</span><span class="sxs-lookup"><span data-stu-id="adbb1-178">EnableGroupCreation</span></span><li><span data-ttu-id="adbb1-179">Type: Booleaanse</span><span class="sxs-lookup"><span data-stu-id="adbb1-179">Type: Boolean</span></span><li><span data-ttu-id="adbb1-180">Standaard: True</span><span class="sxs-lookup"><span data-stu-id="adbb1-180">Default: True</span></span> | <span data-ttu-id="adbb1-181">Een boolean die aangeeft of niet-beheerders van nieuwe maken kunnen geïntegreerde groepen.</span><span class="sxs-lookup"><span data-stu-id="adbb1-181">A boolean indicating whether or not non-admin users can create new Unified groups.</span></span> |


## <a name="read-settings-at-hello-directory-level"></a><span data-ttu-id="adbb1-182">Instellingen lezen op Hallo directory niveau</span><span class="sxs-lookup"><span data-stu-id="adbb1-182">Read settings at hello directory level</span></span>
<span data-ttu-id="adbb1-183">Volgende stappen uit op het niveau van de directory-instellingen die van toepassing zijn tooall Office-groepen in de map Hallo gelezen.</span><span class="sxs-lookup"><span data-stu-id="adbb1-183">These steps read settings at directory level, which apply tooall Office groups in hello directory.</span></span>

1. <span data-ttu-id="adbb1-184">Lees alle bestaande directoryinstellingen:</span><span class="sxs-lookup"><span data-stu-id="adbb1-184">Read all existing directory settings:</span></span>
  ```
  Get-AzureADDirectorySetting -All $True
  ```
  <span data-ttu-id="adbb1-185">Deze cmdlet retourneert een lijst met alle directoryinstellingen:</span><span class="sxs-lookup"><span data-stu-id="adbb1-185">This cmdlet returns a list of all directory settings:</span></span>
  ```
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```

2. <span data-ttu-id="adbb1-186">Lees alle instellingen voor een specifieke groep:</span><span class="sxs-lookup"><span data-stu-id="adbb1-186">Read all settings for a specific group:</span></span>
  ```
  Get-AzureADObjectSetting -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -TargetType Groups
  ```

3. <span data-ttu-id="adbb1-187">Lezen van alle waarden in de directory instellingen van een specifieke map instellingen-object met Id-GUID-instellingen:</span><span class="sxs-lookup"><span data-stu-id="adbb1-187">Read all directory settings values of a specific directory settings object, using Settings Id GUID:</span></span>
  ```
  (Get-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323).values
  ```
  <span data-ttu-id="adbb1-188">Deze cmdlet retourneert Hallo namen en waarden in deze object-instellingen voor deze specifieke groep:</span><span class="sxs-lookup"><span data-stu-id="adbb1-188">This cmdlet returns hello names and values in this settings object for this specific group:</span></span>
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

## <a name="update-settings-for-a-specific-group"></a><span data-ttu-id="adbb1-189">Instellingen voor een specifieke groep bijwerken</span><span class="sxs-lookup"><span data-stu-id="adbb1-189">Update settings for a specific group</span></span>

1. <span data-ttu-id="adbb1-190">Zoeken naar Hallo instellingen sjabloon met de naam 'Groups.Unified.Guest'</span><span class="sxs-lookup"><span data-stu-id="adbb1-190">Search for hello settings template named "Groups.Unified.Guest"</span></span>
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
2. <span data-ttu-id="adbb1-191">Hallo sjabloonobject voor Hallo Groups.Unified.Guest sjabloon ophalen:</span><span class="sxs-lookup"><span data-stu-id="adbb1-191">Retrieve hello template object for hello Groups.Unified.Guest template:</span></span>
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 08d542b9-071f-4e16-94b0-74abb372e3d9
  ```
3. <span data-ttu-id="adbb1-192">Maak een nieuw instellingenobject van Hallo sjabloon:</span><span class="sxs-lookup"><span data-stu-id="adbb1-192">Create a new settings object from hello template:</span></span>
  ```
  $Setting = $Template.CreateDirectorySetting()
  ```

4. <span data-ttu-id="adbb1-193">Hallo toohello vereist instellingswaarde instellen:</span><span class="sxs-lookup"><span data-stu-id="adbb1-193">Set hello setting toohello required value:</span></span>
  ```
  $Setting["AllowToAddGuests"]=$False
  ```
5. <span data-ttu-id="adbb1-194">Nieuwe instelling voor de vereiste groep Hallo Hallo op Hallo directory maken:</span><span class="sxs-lookup"><span data-stu-id="adbb1-194">Create hello new setting for hello required group in hello directory:</span></span>
  ```
  New-AzureADObjectSetting -TargetType Groups -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -DirectorySetting $Setting
  
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  25651479-a26e-4181-afce-ce24111b2cb5             08d542b9-071f-4e16-94b0-74abb372e3d9 {class SettingValue {...
  ```

## <a name="update-settings-at-hello-directory-level"></a><span data-ttu-id="adbb1-195">Update-instellingen op Hallo directory niveau</span><span class="sxs-lookup"><span data-stu-id="adbb1-195">Update settings at hello directory level</span></span>

<span data-ttu-id="adbb1-196">Volgende stappen uit bijwerken op het niveau van de directory-instellingen die van toepassing zijn tooall Unified groepen in Hallo directory.</span><span class="sxs-lookup"><span data-stu-id="adbb1-196">These steps update settings at directory level, which apply tooall Unified groups in hello directory.</span></span> <span data-ttu-id="adbb1-197">Deze voorbeelden wordt ervan uitgegaan dat er is al een object-instellingen in uw directory.</span><span class="sxs-lookup"><span data-stu-id="adbb1-197">These examples assume there is already a Settings object in your directory.</span></span>

1. <span data-ttu-id="adbb1-198">Bestaand instellingenobject Hallo vinden:</span><span class="sxs-lookup"><span data-stu-id="adbb1-198">Find hello existing Settings object:</span></span>
  ```
  Get-AzureADDirectorySetting | Where-object -Property Displayname -Value "Group.Unified" -EQ
  
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  
  $setting = Get-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323
  ```
2. <span data-ttu-id="adbb1-199">Hallo waarde bijwerken:</span><span class="sxs-lookup"><span data-stu-id="adbb1-199">Update hello value:</span></span>
  
  ```
  $Setting["AllowToAddGuests"] = "false"
  ```
3. <span data-ttu-id="adbb1-200">Hallo-instelling bijwerken:</span><span class="sxs-lookup"><span data-stu-id="adbb1-200">Update hello setting:</span></span>
  
  ```
  Set-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323 -DirectorySetting $Setting
  ```

## <a name="remove-settings-at-hello-directory-level"></a><span data-ttu-id="adbb1-201">Verwijder de instellingen op Hallo directory niveau</span><span class="sxs-lookup"><span data-stu-id="adbb1-201">Remove settings at hello directory level</span></span>
<span data-ttu-id="adbb1-202">Deze stap verwijdert-instellingen op het niveau van de directory die van toepassing zijn tooall Office-groepen in Hallo-directory.</span><span class="sxs-lookup"><span data-stu-id="adbb1-202">This step removes settings at directory level, which apply tooall Office groups in hello directory.</span></span>
  ```
  Remove-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323c
  ```

## <a name="cmdlet-syntax-reference"></a><span data-ttu-id="adbb1-203">Verwijzing naar de cmdlet</span><span class="sxs-lookup"><span data-stu-id="adbb1-203">Cmdlet syntax reference</span></span>
<span data-ttu-id="adbb1-204">U vindt meer Azure Active Directory PowerShell-documentatie op [Azure Active Directory-Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="adbb1-204">You can find more Azure Active Directory PowerShell documentation at [Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

## <a name="additional-reading"></a><span data-ttu-id="adbb1-205">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="adbb1-205">Additional reading</span></span>

* [<span data-ttu-id="adbb1-206">Tooresources toegang beheren met Azure Active Directory-groepen</span><span class="sxs-lookup"><span data-stu-id="adbb1-206">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="adbb1-207">Uw on-premises identiteiten integreren met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="adbb1-207">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
