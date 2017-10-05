---
title: Groepsinstellingen configureren via Azure Active Directory-cmdlets | Microsoft Docs
description: Hoe beheert u de instellingen voor groepen met behulp van Azure Active Directory-cmdlets
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
ms.openlocfilehash: 0d89f12955b90c7e1a8301b7c3a1a92e7f62d085
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-cmdlets-for-configuring-group-settings"></a><span data-ttu-id="6b3af-103">Azure Active Directory cmdlets voor het configureren van groepsinstellingen</span><span class="sxs-lookup"><span data-stu-id="6b3af-103">Azure Active Directory cmdlets for configuring group settings</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6b3af-104">Deze inhoud geldt alleen voor Office 365-groepen.</span><span class="sxs-lookup"><span data-stu-id="6b3af-104">This content applies only to Office 365 groups.</span></span> <span data-ttu-id="6b3af-105">Voor meer informatie over het zodat gebruikers kunnen beveiligingsgroepen maken, stelt `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True` zoals beschreven in [Set-MSOLCompanySettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).</span><span class="sxs-lookup"><span data-stu-id="6b3af-105">For more information on how to allow users to create Security groups, set `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True` as described in [Set-MSOLCompanySettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).</span></span> 

<span data-ttu-id="6b3af-106">Instellingen voor Office 365-groepen zijn geconfigureerd met een object-instellingen en een SettingsTemplate-object.</span><span class="sxs-lookup"><span data-stu-id="6b3af-106">Office 365 Groups settings are configured using a Settings object and a SettingsTemplate object.</span></span> <span data-ttu-id="6b3af-107">In eerste instantie is er geen voor instellingenobjecten in uw directory omdat uw directory is geconfigureerd met de standaardinstellingen.</span><span class="sxs-lookup"><span data-stu-id="6b3af-107">Initially, you don't see any Settings objects in your directory, because your directory is configured with the default settings.</span></span> <span data-ttu-id="6b3af-108">Als u wilt de standaardinstellingen wilt wijzigen, moet u een nieuw object voor instellingen met een sjabloon voor instellingen.</span><span class="sxs-lookup"><span data-stu-id="6b3af-108">To change the default settings, you must create a new settings object using a settings template.</span></span> <span data-ttu-id="6b3af-109">Instellingen voor sjablonen zijn gedefinieerd door Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6b3af-109">Settings templates are defined by Microsoft.</span></span> <span data-ttu-id="6b3af-110">Er zijn verschillende sjablonen met verschillende instellingen.</span><span class="sxs-lookup"><span data-stu-id="6b3af-110">There are several different settings templates.</span></span> <span data-ttu-id="6b3af-111">Instellingen voor Office 365-groep voor uw directory configureren, moet u de sjabloon met de naam 'Group.Unified' gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6b3af-111">To configure Office 365 group settings for your directory, you use the template named "Group.Unified".</span></span> <span data-ttu-id="6b3af-112">Gebruik de sjabloon met de naam "Group.Unified.Guest" voor informatie over het configureren van instellingen voor Office 365-groep op één groep.</span><span class="sxs-lookup"><span data-stu-id="6b3af-112">To configure Office 365 group settings on a single group, use the template named "Group.Unified.Guest".</span></span> <span data-ttu-id="6b3af-113">Deze sjabloon wordt gebruikt voor het beheren van gasttoegang tot een Office 365-groep.</span><span class="sxs-lookup"><span data-stu-id="6b3af-113">This template is used to manage guest access to an Office 365 group.</span></span> 

<span data-ttu-id="6b3af-114">De cmdlets maken deel uit van de Azure Active Directory PowerShell V2-module.</span><span class="sxs-lookup"><span data-stu-id="6b3af-114">The cmdlets are part of the Azure Active Directory PowerShell V2 module.</span></span> <span data-ttu-id="6b3af-115">Voor instructies het downloaden en installeren van de module op uw computer, Zie het artikel [Azure Active Directory PowerShell versie 2](https://docs.microsoft.com/powershell/azuread/).</span><span class="sxs-lookup"><span data-stu-id="6b3af-115">For instructions how to download and install the module on your computer, see the article [Azure Active Directory PowerShell Version 2](https://docs.microsoft.com/powershell/azuread/).</span></span> <span data-ttu-id="6b3af-116">U kunt installeren de release versie 2 van de module op basis van [de PowerShell-galerie](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="6b3af-116">You can install the version 2 release of the module from [the PowerShell gallery](https://www.powershellgallery.com/packages/AzureAD/).</span></span>

## <a name="retrieve-a-specific-settings-value"></a><span data-ttu-id="6b3af-117">De waarde van een specifieke instellingen ophalen</span><span class="sxs-lookup"><span data-stu-id="6b3af-117">Retrieve a specific settings value</span></span>
<span data-ttu-id="6b3af-118">Als u de naam van de instelling die u wilt ophalen, kunt u de onderstaande cmdlet voor het ophalen van de huidige waarde van de instellingen.</span><span class="sxs-lookup"><span data-stu-id="6b3af-118">If you know the name of the setting you want to retrieve, you can use the below cmdlet to retrieve the current settings value.</span></span> <span data-ttu-id="6b3af-119">In dit voorbeeld ophaalt we de waarde voor een instelling met de naam 'UsageGuidelinesUrl'.</span><span class="sxs-lookup"><span data-stu-id="6b3af-119">In this example, we're retrieving the value for a setting named "UsageGuidelinesUrl."</span></span> <span data-ttu-id="6b3af-120">U vindt dat meer informatie over instellingen voor directory en hun namen verder omlaag in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="6b3af-120">You can read more about directory settings and their names further down in this article.</span></span>

```powershell
(Get-AzureADDirectorySetting).Values | Where-Object -Property Name -Value UsageGuidelinesUrl -EQ
```

## <a name="create-settings-at-the-directory-level"></a><span data-ttu-id="6b3af-121">Instellingen op het niveau van de directory maken</span><span class="sxs-lookup"><span data-stu-id="6b3af-121">Create settings at the directory level</span></span>
<span data-ttu-id="6b3af-122">Deze stappen maken instellingen op het niveau van de directory die van toepassing op alle Office 365-groepen (Unified groepen) in de map.</span><span class="sxs-lookup"><span data-stu-id="6b3af-122">These steps create settings at directory level, which apply to all Office 365 groups (Unified groups) in the directory.</span></span>

1. <span data-ttu-id="6b3af-123">In de cmdlets DirectorySettings, moet u de ID van de SettingsTemplate die u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6b3af-123">In the DirectorySettings cmdlets, you must specify the ID of the SettingsTemplate you want to use.</span></span> <span data-ttu-id="6b3af-124">Als u deze ID niet weet, retourneert deze cmdlet de lijst met alle instellingen sjablonen:</span><span class="sxs-lookup"><span data-stu-id="6b3af-124">If you do not know this ID, this cmdlet returns the list of all settings templates:</span></span>
  
  ```
  PS C:> Get-AzureADDirectorySettingTemplate
  ```
  <span data-ttu-id="6b3af-125">De aanroep van deze cmdlet retourneert alle sjablonen die beschikbaar zijn:</span><span class="sxs-lookup"><span data-stu-id="6b3af-125">This cmdlet call returns all templates that are available:</span></span>
  
  ```
  Id                                   DisplayName         Description
  --                                   -----------         -----------
  62375ab9-6b52-47ed-826b-58e47e0e304b Group.Unified       ...
  08d542b9-071f-4e16-94b0-74abb372e3d9 Group.Unified.Guest Settings for a specific Unified Group
  16933506-8a8d-4f0d-ad58-e1db05a5b929 Company.BuiltIn     Setting templates define the different settings that can be used for the associ...
  4bc7f740-180e-4586-adb6-38b2e9024e6b Application...
  898f1161-d651-43d1-805c-3b0b388a9fc2 Custom Policy       Settings ...
  5cf42378-d67d-4f36-ba46-e8b86229381d Password Rule       Settings ...
  ```
2. <span data-ttu-id="6b3af-126">Als u wilt een richtlijn gebruik URL kunt toevoegen, moet u eerst het SettingsTemplate-object dat de waarde van de URL in de gebruik richtlijn; definieert ophalen dat wil zeggen, de sjabloon Group.Unified:</span><span class="sxs-lookup"><span data-stu-id="6b3af-126">To add a usage guideline URL, first you need to get the SettingsTemplate object that defines the usage guideline URL value; that is, the Group.Unified template:</span></span>
  
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 62375ab9-6b52-47ed-826b-58e47e0e304b
  ```
3. <span data-ttu-id="6b3af-127">Maak vervolgens een nieuw object van instellingen op basis van die sjabloon:</span><span class="sxs-lookup"><span data-stu-id="6b3af-127">Next, create a new settings object based on that template:</span></span>
  
  ```
  $Setting = $template.CreateDirectorySetting()
  ```  
4. <span data-ttu-id="6b3af-128">Werk vervolgens de waarde van de richtlijn gebruik:</span><span class="sxs-lookup"><span data-stu-id="6b3af-128">Then update the usage guideline value:</span></span>
  
  ```
  $setting["UsageGuidelinesUrl"] = "<https://guideline.com>"
  ```  
5. <span data-ttu-id="6b3af-129">Ten slotte de instellingen toepassen:</span><span class="sxs-lookup"><span data-stu-id="6b3af-129">Finally, apply the settings:</span></span>
  
  ```
  New-AzureADDirectorySetting -DirectorySetting $setting
  ```

<span data-ttu-id="6b3af-130">Heeft voltooid wordt de cmdlet de ID van de nieuwe voor instellingenobject:</span><span class="sxs-lookup"><span data-stu-id="6b3af-130">Upon successful completion, the cmdlet returns the ID of the new settings object:</span></span>
  ```
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323             62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```
<span data-ttu-id="6b3af-131">Hier vindt u de instellingen die zijn gedefinieerd in de Group.Unified SettingsTemplate.</span><span class="sxs-lookup"><span data-stu-id="6b3af-131">Here are the settings defined in the Group.Unified SettingsTemplate.</span></span>

| <span data-ttu-id="6b3af-132">**Instelling**</span><span class="sxs-lookup"><span data-stu-id="6b3af-132">**Setting**</span></span> | <span data-ttu-id="6b3af-133">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="6b3af-133">**Description**</span></span> |
| --- | --- |
|  <ul><li><span data-ttu-id="6b3af-134">EnableGroupCreation</span><span class="sxs-lookup"><span data-stu-id="6b3af-134">EnableGroupCreation</span></span><li><span data-ttu-id="6b3af-135">Type: Booleaanse</span><span class="sxs-lookup"><span data-stu-id="6b3af-135">Type: Boolean</span></span><li><span data-ttu-id="6b3af-136">Standaard: True</span><span class="sxs-lookup"><span data-stu-id="6b3af-136">Default: True</span></span> |<span data-ttu-id="6b3af-137">De vlag die aangeeft of het maken van Unified groep is toegestaan in de map.</span><span class="sxs-lookup"><span data-stu-id="6b3af-137">The flag indicating whether Unified Group creation is allowed in the directory.</span></span> |
|  <ul><li><span data-ttu-id="6b3af-138">GroupCreationAllowedGroupId</span><span class="sxs-lookup"><span data-stu-id="6b3af-138">GroupCreationAllowedGroupId</span></span><li><span data-ttu-id="6b3af-139">Type: String</span><span class="sxs-lookup"><span data-stu-id="6b3af-139">Type: String</span></span><li><span data-ttu-id="6b3af-140">Standaardwaarde: ' "</span><span class="sxs-lookup"><span data-stu-id="6b3af-140">Default: “”</span></span> |<span data-ttu-id="6b3af-141">GUID van de beveiligingsgroep waarvan de leden mogen Unified groepen maken, zelfs wanneer EnableGroupCreation == false.</span><span class="sxs-lookup"><span data-stu-id="6b3af-141">GUID of the security group for which the members are allowed to create Unified Groups even when EnableGroupCreation == false.</span></span> |
|  <ul><li><span data-ttu-id="6b3af-142">UsageGuidelinesUrl</span><span class="sxs-lookup"><span data-stu-id="6b3af-142">UsageGuidelinesUrl</span></span><li><span data-ttu-id="6b3af-143">Type: String</span><span class="sxs-lookup"><span data-stu-id="6b3af-143">Type: String</span></span><li><span data-ttu-id="6b3af-144">Standaardwaarde: ' "</span><span class="sxs-lookup"><span data-stu-id="6b3af-144">Default: “”</span></span> |<span data-ttu-id="6b3af-145">Een koppeling naar de richtlijnen voor het gebruik van groep.</span><span class="sxs-lookup"><span data-stu-id="6b3af-145">A link to the Group Usage Guidelines.</span></span> |
|  <ul><li><span data-ttu-id="6b3af-146">ClassificationDescriptions</span><span class="sxs-lookup"><span data-stu-id="6b3af-146">ClassificationDescriptions</span></span><li><span data-ttu-id="6b3af-147">Type: String</span><span class="sxs-lookup"><span data-stu-id="6b3af-147">Type: String</span></span><li><span data-ttu-id="6b3af-148">Standaardwaarde: ' "</span><span class="sxs-lookup"><span data-stu-id="6b3af-148">Default: “”</span></span> | <span data-ttu-id="6b3af-149">Een door komma's gescheiden lijst met beschrijvingen van de classificatie.</span><span class="sxs-lookup"><span data-stu-id="6b3af-149">A comma-delimited list of classification descriptions.</span></span> |
|  <ul><li><span data-ttu-id="6b3af-150">DefaultClassification</span><span class="sxs-lookup"><span data-stu-id="6b3af-150">DefaultClassification</span></span><li><span data-ttu-id="6b3af-151">Type: String</span><span class="sxs-lookup"><span data-stu-id="6b3af-151">Type: String</span></span><li><span data-ttu-id="6b3af-152">Standaardwaarde: ' "</span><span class="sxs-lookup"><span data-stu-id="6b3af-152">Default: “”</span></span> | <span data-ttu-id="6b3af-153">De classificatie die moet worden gebruikt als de Standaardclassificatie voor een groep als deze is niet opgegeven.</span><span class="sxs-lookup"><span data-stu-id="6b3af-153">The classification that is to be used as the default classification for a group if none was specified.</span></span>|
|  <ul><li><span data-ttu-id="6b3af-154">PrefixSuffixNamingRequirement</span><span class="sxs-lookup"><span data-stu-id="6b3af-154">PrefixSuffixNamingRequirement</span></span><li><span data-ttu-id="6b3af-155">Type: String</span><span class="sxs-lookup"><span data-stu-id="6b3af-155">Type: String</span></span><li><span data-ttu-id="6b3af-156">Standaardwaarde: ' "</span><span class="sxs-lookup"><span data-stu-id="6b3af-156">Default: “”</span></span> |<span data-ttu-id="6b3af-157">Nog niet geïmplementeerd</span><span class="sxs-lookup"><span data-stu-id="6b3af-157">Not implemented yet</span></span>
|  <ul><li><span data-ttu-id="6b3af-158">AllowGuestsToBeGroupOwner</span><span class="sxs-lookup"><span data-stu-id="6b3af-158">AllowGuestsToBeGroupOwner</span></span><li><span data-ttu-id="6b3af-159">Type: Booleaanse</span><span class="sxs-lookup"><span data-stu-id="6b3af-159">Type: Boolean</span></span><li><span data-ttu-id="6b3af-160">Standaard: False</span><span class="sxs-lookup"><span data-stu-id="6b3af-160">Default: False</span></span> | <span data-ttu-id="6b3af-161">Een Boolean die aangeeft of een gastgebruiker moet een eigenaar van de groepen kan worden.</span><span class="sxs-lookup"><span data-stu-id="6b3af-161">Boolean indicating whether or not a guest user can be an owner of groups.</span></span> |
|  <ul><li><span data-ttu-id="6b3af-162">AllowGuestsToAccessGroups</span><span class="sxs-lookup"><span data-stu-id="6b3af-162">AllowGuestsToAccessGroups</span></span><li><span data-ttu-id="6b3af-163">Type: Booleaanse</span><span class="sxs-lookup"><span data-stu-id="6b3af-163">Type: Boolean</span></span><li><span data-ttu-id="6b3af-164">Standaard: True</span><span class="sxs-lookup"><span data-stu-id="6b3af-164">Default: True</span></span> | <span data-ttu-id="6b3af-165">Een Boolean die aangeeft of een gastgebruiker toegang tot inhoud Unified-groepen krijgen kan.</span><span class="sxs-lookup"><span data-stu-id="6b3af-165">Boolean indicating whether or not a guest user can have access to Unified groups' content.</span></span> |
|  <ul><li><span data-ttu-id="6b3af-166">GuestUsageGuidelinesUrl</span><span class="sxs-lookup"><span data-stu-id="6b3af-166">GuestUsageGuidelinesUrl</span></span><li><span data-ttu-id="6b3af-167">Type: String</span><span class="sxs-lookup"><span data-stu-id="6b3af-167">Type: String</span></span><li><span data-ttu-id="6b3af-168">Standaardwaarde: ' "</span><span class="sxs-lookup"><span data-stu-id="6b3af-168">Default: “”</span></span> | <span data-ttu-id="6b3af-169">De url van een koppeling naar de richtlijnen voor het gebruik van Gast.</span><span class="sxs-lookup"><span data-stu-id="6b3af-169">The url of a link to the guest usage guidelines.</span></span> |
|  <ul><li><span data-ttu-id="6b3af-170">AllowToAddGuests</span><span class="sxs-lookup"><span data-stu-id="6b3af-170">AllowToAddGuests</span></span><li><span data-ttu-id="6b3af-171">Type: Booleaanse</span><span class="sxs-lookup"><span data-stu-id="6b3af-171">Type: Boolean</span></span><li><span data-ttu-id="6b3af-172">Standaard: True</span><span class="sxs-lookup"><span data-stu-id="6b3af-172">Default: True</span></span> | <span data-ttu-id="6b3af-173">Een boolean die aangeeft of of niet is toegestaan gasten toevoegen aan deze map.</span><span class="sxs-lookup"><span data-stu-id="6b3af-173">A boolean indicating whether or not is allowed to add guests to this directory.</span></span>|
|  <ul><li><span data-ttu-id="6b3af-174">ClassificationList</span><span class="sxs-lookup"><span data-stu-id="6b3af-174">ClassificationList</span></span><li><span data-ttu-id="6b3af-175">Type: String</span><span class="sxs-lookup"><span data-stu-id="6b3af-175">Type: String</span></span><li><span data-ttu-id="6b3af-176">Standaardwaarde: ' "</span><span class="sxs-lookup"><span data-stu-id="6b3af-176">Default: “”</span></span> |<span data-ttu-id="6b3af-177">Een door komma's gescheiden lijst met geldige classificatiewaarden die kunnen worden toegepast op groepen Unified.</span><span class="sxs-lookup"><span data-stu-id="6b3af-177">A comma-delimited list of valid classification values that can be applied to Unified Groups.</span></span> |
|  <ul><li><span data-ttu-id="6b3af-178">EnableGroupCreation</span><span class="sxs-lookup"><span data-stu-id="6b3af-178">EnableGroupCreation</span></span><li><span data-ttu-id="6b3af-179">Type: Booleaanse</span><span class="sxs-lookup"><span data-stu-id="6b3af-179">Type: Boolean</span></span><li><span data-ttu-id="6b3af-180">Standaard: True</span><span class="sxs-lookup"><span data-stu-id="6b3af-180">Default: True</span></span> | <span data-ttu-id="6b3af-181">Een boolean die aangeeft of niet-beheerders van nieuwe maken kunnen geïntegreerde groepen.</span><span class="sxs-lookup"><span data-stu-id="6b3af-181">A boolean indicating whether or not non-admin users can create new Unified groups.</span></span> |


## <a name="read-settings-at-the-directory-level"></a><span data-ttu-id="6b3af-182">Instellingen op het mapniveau van de lezen</span><span class="sxs-lookup"><span data-stu-id="6b3af-182">Read settings at the directory level</span></span>
<span data-ttu-id="6b3af-183">Volgende stappen uit op het niveau van de directory-instellingen die van toepassing op alle Office-groepen in de map gelezen.</span><span class="sxs-lookup"><span data-stu-id="6b3af-183">These steps read settings at directory level, which apply to all Office groups in the directory.</span></span>

1. <span data-ttu-id="6b3af-184">Lees alle bestaande directoryinstellingen:</span><span class="sxs-lookup"><span data-stu-id="6b3af-184">Read all existing directory settings:</span></span>
  ```
  Get-AzureADDirectorySetting -All $True
  ```
  <span data-ttu-id="6b3af-185">Deze cmdlet retourneert een lijst met alle directoryinstellingen:</span><span class="sxs-lookup"><span data-stu-id="6b3af-185">This cmdlet returns a list of all directory settings:</span></span>
  ```
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```

2. <span data-ttu-id="6b3af-186">Lees alle instellingen voor een specifieke groep:</span><span class="sxs-lookup"><span data-stu-id="6b3af-186">Read all settings for a specific group:</span></span>
  ```
  Get-AzureADObjectSetting -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -TargetType Groups
  ```

3. <span data-ttu-id="6b3af-187">Lezen van alle waarden in de directory instellingen van een specifieke map instellingen-object met Id-GUID-instellingen:</span><span class="sxs-lookup"><span data-stu-id="6b3af-187">Read all directory settings values of a specific directory settings object, using Settings Id GUID:</span></span>
  ```
  (Get-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323).values
  ```
  <span data-ttu-id="6b3af-188">Deze cmdlet retourneert de namen en waarden in deze object-instellingen voor deze specifieke groep:</span><span class="sxs-lookup"><span data-stu-id="6b3af-188">This cmdlet returns the names and values in this settings object for this specific group:</span></span>
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

## <a name="update-settings-for-a-specific-group"></a><span data-ttu-id="6b3af-189">Instellingen voor een specifieke groep bijwerken</span><span class="sxs-lookup"><span data-stu-id="6b3af-189">Update settings for a specific group</span></span>

1. <span data-ttu-id="6b3af-190">Zoeken naar de instellingen sjabloon met de naam 'Groups.Unified.Guest'</span><span class="sxs-lookup"><span data-stu-id="6b3af-190">Search for the settings template named "Groups.Unified.Guest"</span></span>
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
2. <span data-ttu-id="6b3af-191">Het ophalen van de sjabloonobject voor de sjabloon Groups.Unified.Guest:</span><span class="sxs-lookup"><span data-stu-id="6b3af-191">Retrieve the template object for the Groups.Unified.Guest template:</span></span>
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 08d542b9-071f-4e16-94b0-74abb372e3d9
  ```
3. <span data-ttu-id="6b3af-192">Maak een nieuw object van de instellingen van de sjabloon:</span><span class="sxs-lookup"><span data-stu-id="6b3af-192">Create a new settings object from the template:</span></span>
  ```
  $Setting = $Template.CreateDirectorySetting()
  ```

4. <span data-ttu-id="6b3af-193">Stel de instelling op de vereiste waarde:</span><span class="sxs-lookup"><span data-stu-id="6b3af-193">Set the setting to the required value:</span></span>
  ```
  $Setting["AllowToAddGuests"]=$False
  ```
5. <span data-ttu-id="6b3af-194">De nieuwe instelling maken voor de vereiste groep in de map:</span><span class="sxs-lookup"><span data-stu-id="6b3af-194">Create the new setting for the required group in the directory:</span></span>
  ```
  New-AzureADObjectSetting -TargetType Groups -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -DirectorySetting $Setting
  
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  25651479-a26e-4181-afce-ce24111b2cb5             08d542b9-071f-4e16-94b0-74abb372e3d9 {class SettingValue {...
  ```

## <a name="update-settings-at-the-directory-level"></a><span data-ttu-id="6b3af-195">Update-instellingen op het niveau van de directory</span><span class="sxs-lookup"><span data-stu-id="6b3af-195">Update settings at the directory level</span></span>

<span data-ttu-id="6b3af-196">Deze stappen bijwerken op het niveau van de directory-instellingen die van toepassing op alle Unified groepen in Active directory.</span><span class="sxs-lookup"><span data-stu-id="6b3af-196">These steps update settings at directory level, which apply to all Unified groups in the directory.</span></span> <span data-ttu-id="6b3af-197">Deze voorbeelden wordt ervan uitgegaan dat er is al een object-instellingen in uw directory.</span><span class="sxs-lookup"><span data-stu-id="6b3af-197">These examples assume there is already a Settings object in your directory.</span></span>

1. <span data-ttu-id="6b3af-198">Zoek het bestaande object-instellingen:</span><span class="sxs-lookup"><span data-stu-id="6b3af-198">Find the existing Settings object:</span></span>
  ```
  Get-AzureADDirectorySetting | Where-object -Property Displayname -Value "Group.Unified" -EQ
  
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  
  $setting = Get-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323
  ```
2. <span data-ttu-id="6b3af-199">Werk de waarde:</span><span class="sxs-lookup"><span data-stu-id="6b3af-199">Update the value:</span></span>
  
  ```
  $Setting["AllowToAddGuests"] = "false"
  ```
3. <span data-ttu-id="6b3af-200">Werk de instelling:</span><span class="sxs-lookup"><span data-stu-id="6b3af-200">Update the setting:</span></span>
  
  ```
  Set-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323 -DirectorySetting $Setting
  ```

## <a name="remove-settings-at-the-directory-level"></a><span data-ttu-id="6b3af-201">Verwijder de instellingen op het niveau van de directory</span><span class="sxs-lookup"><span data-stu-id="6b3af-201">Remove settings at the directory level</span></span>
<span data-ttu-id="6b3af-202">Deze stap verwijdert instellingen op het niveau van de directory die van toepassing op alle Office-groepen in de map.</span><span class="sxs-lookup"><span data-stu-id="6b3af-202">This step removes settings at directory level, which apply to all Office groups in the directory.</span></span>
  ```
  Remove-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323c
  ```

## <a name="cmdlet-syntax-reference"></a><span data-ttu-id="6b3af-203">Verwijzing naar de cmdlet</span><span class="sxs-lookup"><span data-stu-id="6b3af-203">Cmdlet syntax reference</span></span>
<span data-ttu-id="6b3af-204">U vindt meer Azure Active Directory PowerShell-documentatie op [Azure Active Directory-Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="6b3af-204">You can find more Azure Active Directory PowerShell documentation at [Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

## <a name="additional-reading"></a><span data-ttu-id="6b3af-205">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="6b3af-205">Additional reading</span></span>

* <span data-ttu-id="6b3af-206">[Managing access to resources with Azure Active Directory groups](active-directory-manage-groups.md) (Toegang tot resources beheren met Azure Active Directory-groepen)</span><span class="sxs-lookup"><span data-stu-id="6b3af-206">[Managing access to resources with Azure Active Directory groups](active-directory-manage-groups.md)</span></span>
* [<span data-ttu-id="6b3af-207">Uw on-premises identiteiten integreren met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6b3af-207">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
