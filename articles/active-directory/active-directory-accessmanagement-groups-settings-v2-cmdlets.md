---
title: PowerShell-voorbeelden voor het beheren van groepen in Azure Active Directory | Microsoft Docs
description: Deze pagina vindt u voorbeelden van PowerShell om u te helpen bij het beheren van uw groepen in Azure Active Directory
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
ms.openlocfilehash: a81820bc778c26f6e8051e2817ebd2b9c24b697a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-version-2-cmdlets-for-group-management"></a><span data-ttu-id="fb0dd-104">Azure Active Directory-cmdlets van versie 2 voor groepsbeheer</span><span class="sxs-lookup"><span data-stu-id="fb0dd-104">Azure Active Directory version 2 cmdlets for group management</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fb0dd-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="fb0dd-105">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="fb0dd-106">Klassieke Azure Portal</span><span class="sxs-lookup"><span data-stu-id="fb0dd-106">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="fb0dd-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fb0dd-107">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="fb0dd-108">Dit artikel bevat voorbeelden van hoe u PowerShell gebruikt voor het beheren van uw groepen in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fb0dd-108">This article contains examples of how to use PowerShell to manage your groups in Azure Active Directory (Azure AD).</span></span>  <span data-ttu-id="fb0dd-109">Deze ook wordt uitgelegd hoe u met de Azure AD PowerShell-module ophalen instellen.</span><span class="sxs-lookup"><span data-stu-id="fb0dd-109">It also tells you how to get set up with the Azure AD PowerShell module.</span></span> <span data-ttu-id="fb0dd-110">Eerst moet u [downloaden van de Azure AD PowerShell-module](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="fb0dd-110">First, you must [download the Azure AD PowerShell module](https://www.powershellgallery.com/packages/AzureAD/).</span></span>

## <a name="installing-the-azure-ad-powershell-module"></a><span data-ttu-id="fb0dd-111">De Azure AD PowerShell-module installeren</span><span class="sxs-lookup"><span data-stu-id="fb0dd-111">Installing the Azure AD PowerShell module</span></span>
<span data-ttu-id="fb0dd-112">Gebruik de volgende opdrachten voor het installeren van de Azure AD PowerShell-module:</span><span class="sxs-lookup"><span data-stu-id="fb0dd-112">To install the Azure AD PowerShell module, use the following commands:</span></span>

    PS C:\Windows\system32> install-module azuread

<span data-ttu-id="fb0dd-113">Controleer of de module is geïnstalleerd, moet u de volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="fb0dd-113">To verify that the module was installed, use the following command:</span></span>

    PS C:\Windows\system32> get-module azuread

    ModuleType Version      Name                                ExportedCommands
    ---------- ---------    ----                                ----------------
    Binary     2.0.0.115    azuread                      {Add-AzureADAdministrati...}

<span data-ttu-id="fb0dd-114">U kunt nu starten met de cmdlets in de module.</span><span class="sxs-lookup"><span data-stu-id="fb0dd-114">Now you can start using the cmdlets in the module.</span></span> <span data-ttu-id="fb0dd-115">Voor een volledige beschrijving van de cmdlets in de Azure AD-module raadpleegt u de online documentatie bij [Azure Active Directory PowerShell versie 2](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="fb0dd-115">For a full description of the cmdlets in the Azure AD module, please refer to the online reference documentation for [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

## <a name="connecting-to-the-directory"></a><span data-ttu-id="fb0dd-116">Verbinding maken met de map</span><span class="sxs-lookup"><span data-stu-id="fb0dd-116">Connecting to the directory</span></span>
<span data-ttu-id="fb0dd-117">Voordat u kunt het beheer van groepen met behulp van Azure AD PowerShell-cmdlets, moet u de PowerShell-sessie verbinding maken met de map die u wilt beheren.</span><span class="sxs-lookup"><span data-stu-id="fb0dd-117">Before you can start managing groups using Azure AD PowerShell cmdlets, you must connect your PowerShell session to the directory you want to manage.</span></span> <span data-ttu-id="fb0dd-118">Gebruik de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="fb0dd-118">Use the following command:</span></span>

    PS C:\Windows\system32> Connect-AzureAD

<span data-ttu-id="fb0dd-119">De cmdlet wordt u gevraagd om de referenties die u gebruiken wilt voor toegang tot uw directory.</span><span class="sxs-lookup"><span data-stu-id="fb0dd-119">The cmdlet prompts you for the credentials you want to use to access your directory.</span></span> <span data-ttu-id="fb0dd-120">In dit voorbeeld gebruiken we karen@drumkit.onmicrosoft.com voor toegang tot de map demonstratie.</span><span class="sxs-lookup"><span data-stu-id="fb0dd-120">In this example, we are using karen@drumkit.onmicrosoft.com to access the demonstration directory.</span></span> <span data-ttu-id="fb0dd-121">De cmdlet retourneert een bevestiging voor het weergeven van dat de sessie met succes is verbonden met uw directory:</span><span class="sxs-lookup"><span data-stu-id="fb0dd-121">The cmdlet returns a confirmation to show the session was connected successfully to your directory:</span></span>

    Account                       Environment Tenant
    -------                       ----------- ------
    Karen@drumkit.onmicrosoft.com AzureCloud  85b5ff1e-0402-400c-9e3c-0f…

<span data-ttu-id="fb0dd-122">U kunt nu starten met de AzureAD-cmdlets voor het beheren van groepen in uw directory.</span><span class="sxs-lookup"><span data-stu-id="fb0dd-122">Now you can start using the AzureAD cmdlets to manage groups in your directory.</span></span>

## <a name="retrieving-groups"></a><span data-ttu-id="fb0dd-123">Bij het ophalen van groepen</span><span class="sxs-lookup"><span data-stu-id="fb0dd-123">Retrieving groups</span></span>
<span data-ttu-id="fb0dd-124">U kunt de cmdlet Get-AzureADGroups gebruiken voor het ophalen van de bestaande groepen in uw directory.</span><span class="sxs-lookup"><span data-stu-id="fb0dd-124">To retrieve existing groups from your directory you can use the Get-AzureADGroups cmdlet.</span></span> <span data-ttu-id="fb0dd-125">Gebruik de cmdlet zonder parameters voor het ophalen van alle groepen in de map:</span><span class="sxs-lookup"><span data-stu-id="fb0dd-125">To retrieve all groups in the directory, use the cmdlet without parameters:</span></span>

    PS C:\Windows\system32> get-azureadgroup

<span data-ttu-id="fb0dd-126">De cmdlet retourneert alle groepen in de gekoppelde map.</span><span class="sxs-lookup"><span data-stu-id="fb0dd-126">The cmdlet returns all groups in the connected directory.</span></span>

<span data-ttu-id="fb0dd-127">U kunt de parameter - object-id gebruiken voor het ophalen van een specifieke groep waarvoor u de groep objectID opgeven:</span><span class="sxs-lookup"><span data-stu-id="fb0dd-127">You can use the -objectID parameter to retrieve a specific group for which you specify the group’s objectID:</span></span>

    PS C:\Windows\system32> get-azureadgroup -ObjectId e29bae11-4ac0-450c-bc37-6dae8f3da61b

<span data-ttu-id="fb0dd-128">De cmdlet retourneert nu de groep waarvan objectID overeenkomt met de waarde van de parameter die u hebt ingevoerd:</span><span class="sxs-lookup"><span data-stu-id="fb0dd-128">The cmdlet now returns the group whose objectID matches the value of the parameter you entered:</span></span>

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

<span data-ttu-id="fb0dd-129">U kunt zoeken naar een specifieke groep met de - filterparameter.</span><span class="sxs-lookup"><span data-stu-id="fb0dd-129">You can search for a specific group using the -filter parameter.</span></span> <span data-ttu-id="fb0dd-130">Deze parameter heeft een ODATA-filter-component en resulteert in alle groepen die overeenkomen met het filter, zoals in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="fb0dd-130">This parameter takes an ODATA filter clause and returns all groups that match the filter, as in the following example:</span></span>

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
> <span data-ttu-id="fb0dd-131">De AzureAD PowerShell-cmdlets implementeren de OData-query-norm.</span><span class="sxs-lookup"><span data-stu-id="fb0dd-131">The AzureAD PowerShell cmdlets implement the OData query standard.</span></span> <span data-ttu-id="fb0dd-132">Zie voor meer informatie **$filter** in [OData-query-opties voor systeem met behulp van de OData-eindpunt](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter).</span><span class="sxs-lookup"><span data-stu-id="fb0dd-132">For more information, see **$filter** in [OData system query options using the OData endpoint](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter).</span></span>

## <a name="creating-groups"></a><span data-ttu-id="fb0dd-133">Groepen maken</span><span class="sxs-lookup"><span data-stu-id="fb0dd-133">Creating groups</span></span>
<span data-ttu-id="fb0dd-134">Voor het maken van een nieuwe groep in uw directory, gebruikt u de cmdlet New-AzureADGroup.</span><span class="sxs-lookup"><span data-stu-id="fb0dd-134">To create a new group in your directory, use the New-AzureADGroup cmdlet.</span></span> <span data-ttu-id="fb0dd-135">Deze cmdlet maakt een nieuwe beveiligingsgroep met de naam 'Marketing':</span><span class="sxs-lookup"><span data-stu-id="fb0dd-135">This cmdlet creates a new security group called “Marketing":</span></span>

    PS C:\Windows\system32> New-AzureADGroup -Description "Marketing" -DisplayName "Marketing" -MailEnabled $false -SecurityEnabled $true -MailNickName "Marketing"

## <a name="updating-groups"></a><span data-ttu-id="fb0dd-136">Bijwerken van groepen</span><span class="sxs-lookup"><span data-stu-id="fb0dd-136">Updating groups</span></span>
<span data-ttu-id="fb0dd-137">Gebruik de cmdlet Set-AzureADGroup voor het bijwerken van een bestaande groep.</span><span class="sxs-lookup"><span data-stu-id="fb0dd-137">To update an existing group, use the Set-AzureADGroup cmdlet.</span></span> <span data-ttu-id="fb0dd-138">In dit voorbeeld wilt wordt de eigenschap DisplayName van de groep 'Intune-beheerders.' wijzigen</span><span class="sxs-lookup"><span data-stu-id="fb0dd-138">In this example, we’re changing the DisplayName property of the group “Intune Administrators.”</span></span> <span data-ttu-id="fb0dd-139">Eerst we de groep met de cmdlet Get-AzureADGroup bent zoeken en filteren met het kenmerk DisplayName:</span><span class="sxs-lookup"><span data-stu-id="fb0dd-139">First, we’re finding the group using the Get-AzureADGroup cmdlet and filter using the DisplayName attribute:</span></span>

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

<span data-ttu-id="fb0dd-140">Vervolgens wordt de eigenschap Description wijzigt op de nieuwe waarde 'Intune apparaat Administrators':</span><span class="sxs-lookup"><span data-stu-id="fb0dd-140">Next, we’re changing the Description property to the new value “Intune Device Administrators”:</span></span>

    PS C:\Windows\system32> Set-AzureADGroup -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -Description "Intune Device Administrators"

<span data-ttu-id="fb0dd-141">Nu als we de groep opnieuw vinden, ziet u dat de eigenschap Description is bijgewerkt, zodat de nieuwe waarde:</span><span class="sxs-lookup"><span data-stu-id="fb0dd-141">Now if we find the group again, we see the Description property is updated to reflect the new value:</span></span>

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

## <a name="deleting-groups"></a><span data-ttu-id="fb0dd-142">Groepen verwijderen</span><span class="sxs-lookup"><span data-stu-id="fb0dd-142">Deleting groups</span></span>
<span data-ttu-id="fb0dd-143">Als u wilt verwijderen van groepen van uw directory, gebruikt u de cmdlet Remove-AzureADGroup als volgt:</span><span class="sxs-lookup"><span data-stu-id="fb0dd-143">To delete groups from your directory, use the Remove-AzureADGroup cmdlet as follows:</span></span>

    PS C:\Windows\system32> Remove-AzureADGroup -ObjectId b11ca53e-07cc-455d-9a89-1fe3ab24566b

## <a name="managing-members-of-groups"></a><span data-ttu-id="fb0dd-144">Leden van groepen beheren</span><span class="sxs-lookup"><span data-stu-id="fb0dd-144">Managing members of groups</span></span>
<span data-ttu-id="fb0dd-145">Als u moet nieuwe leden toevoegen aan een groep, gebruikt u de cmdlet Add-AzureADGroupMember.</span><span class="sxs-lookup"><span data-stu-id="fb0dd-145">If you need to add new members to a group, use the Add-AzureADGroupMember cmdlet.</span></span> <span data-ttu-id="fb0dd-146">Een lid met deze opdracht toegevoegd aan de groep van de Intune-beheerders die hebben we in het vorige voorbeeld gebruikt:</span><span class="sxs-lookup"><span data-stu-id="fb0dd-146">This command adds a member to the Intune Administrators group we used in the previous example:</span></span>

    PS C:\Windows\system32> Add-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="fb0dd-147">De parameter - object-id is de object-id van de groep waarop we willen geen lid toevoegen en de RefObjectId - id van de gebruiker wilt toevoegen als lid aan de groep is.</span><span class="sxs-lookup"><span data-stu-id="fb0dd-147">The -ObjectId parameter is the ObjectID of the group to which we want to add a member, and the -RefObjectId is the ObjectID of the user we want to add as a member to the group.</span></span>

<span data-ttu-id="fb0dd-148">Als u de bestaande leden van een groep, gebruikt u de cmdlet Get-AzureADGroupMember, zoals in dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="fb0dd-148">To get the existing members of a group, use the Get-AzureADGroupMember cmdlet, as in this example:</span></span>

    PS C:\Windows\system32> Get-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          72cd4bbd-2594-40a2-935c-016f3cfeeeea User
                          8120cc36-64b4-4080-a9e8-23aa98e8b34f User

<span data-ttu-id="fb0dd-149">U kunt het lid dat we eerder zijn toegevoegd aan de groep verwijderen met de cmdlet Remove-AzureADGroupMember, zoals hier wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="fb0dd-149">To remove the member we previously added to the group, use the Remove-AzureADGroupMember cmdlet, as is shown here:</span></span>

    PS C:\Windows\system32> Remove-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -MemberId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="fb0dd-150">Om te controleren of de lidmaatschappen van de groep van een gebruiker, selecteer AzureADGroupIdsUserIsMemberOf cmdlet te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fb0dd-150">To verify the group membership(s) of a user, use the Select-AzureADGroupIdsUserIsMemberOf cmdlet.</span></span> <span data-ttu-id="fb0dd-151">Deze cmdlet heeft als de parameters de object-id van de gebruiker waarvoor u wilt controleren van de groepslidmaatschappen en een lijst met groepen waarvoor u de lidmaatschappen controleren.</span><span class="sxs-lookup"><span data-stu-id="fb0dd-151">This cmdlet takes as its parameters the ObjectId of the user for which to check the group memberships, and a list of groups for which to check the memberships.</span></span> <span data-ttu-id="fb0dd-152">De lijst met groepen moet zijn opgegeven in de vorm van een complex variabele van type 'Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck', zodat we eerst moet een variabele met dit type maken:</span><span class="sxs-lookup"><span data-stu-id="fb0dd-152">The list of groups must be provided in the form of a complex variable of type “Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck”, so we first must create a variable with that type:</span></span>

    PS C:\Windows\system32> $g = new-object Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck

<span data-ttu-id="fb0dd-153">We bieden vervolgens waarden voor de groupIds om te controleren in het kenmerk 'GroupIds' van deze variabele complex:</span><span class="sxs-lookup"><span data-stu-id="fb0dd-153">Next, we provide values for the groupIds to check in the attribute “GroupIds” of this complex variable:</span></span>

    PS C:\Windows\system32> $g.GroupIds = "b11ca53e-07cc-455d-9a89-1fe3ab24566b", "31f1ff6c-d48c-4f8a-b2e1-abca7fd399df"

<span data-ttu-id="fb0dd-154">Nu als we het groepslidmaatschap van een gebruiker met ObjectID 72cd4bbd-2594-40a2-935c-016f3cfeeeea tegen de groepen in $g controleren willen, dat we moeten gebruiken:</span><span class="sxs-lookup"><span data-stu-id="fb0dd-154">Now, if we want to check the group memberships of a user with ObjectID 72cd4bbd-2594-40a2-935c-016f3cfeeeea against the groups in $g, we should use:</span></span>

    PS C:\Windows\system32> Select-AzureADGroupIdsUserIsMemberOf -ObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea -GroupIdsForMembershipCheck $g

    OdataMetadata                                                                                                 Value
    -------------                                                                                                  -----
    https://graph.windows.net/85b5ff1e-0402-400c-9e3c-0f9e965325d1/$metadata#Collection(Edm.String)             {31f1ff6c-d48c-4f8a-b2e1-abca7fd399df}


<span data-ttu-id="fb0dd-155">De geretourneerde waarde is een lijst met groepen waarvan deze gebruiker lid is.</span><span class="sxs-lookup"><span data-stu-id="fb0dd-155">The value returned is a list of groups of which this user is a member.</span></span> <span data-ttu-id="fb0dd-156">U kunt deze methode om te controleren, contactpersonen, groepen of Service-Principals lidmaatschap voor een opgegeven lijst met groepen met behulp van de Select-AzureADGroupIdsContactIsMemberOf, selecteer AzureADGroupIdsGroupIsMemberOf ook toepassen of Selecteer AzureADGroupIdsServicePrincipalIsMemberOf</span><span class="sxs-lookup"><span data-stu-id="fb0dd-156">You can also apply this method to check Contacts, Groups or Service Principals membership for a given list of groups, using Select-AzureADGroupIdsContactIsMemberOf, Select-AzureADGroupIdsGroupIsMemberOf or Select-AzureADGroupIdsServicePrincipalIsMemberOf</span></span>

## <a name="managing-owners-of-groups"></a><span data-ttu-id="fb0dd-157">Eigenaren van groepen beheren</span><span class="sxs-lookup"><span data-stu-id="fb0dd-157">Managing owners of groups</span></span>
<span data-ttu-id="fb0dd-158">Als eigenaars toevoegen aan een groep, kunt u de cmdlet Add-AzureADGroupOwner:</span><span class="sxs-lookup"><span data-stu-id="fb0dd-158">To add owners to a group, use the Add-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> Add-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="fb0dd-159">De parameter - object-id is de object-id van de groep die we wilt toevoegen van een eigenaar en de RefObjectId - id van de gebruiker wilt toevoegen als een eigenaar van de groep is.</span><span class="sxs-lookup"><span data-stu-id="fb0dd-159">The -ObjectId parameter is the ObjectID of the group to which we want to add an owner, and the -RefObjectId is the ObjectID of the user we want to add as an owner of the group.</span></span>

<span data-ttu-id="fb0dd-160">Gebruik de cmdlet Get-AzureADGroupOwner voor het ophalen van de eigenaren van een groep:</span><span class="sxs-lookup"><span data-stu-id="fb0dd-160">To retrieve the owners of a group, use the Get-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> Get-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

<span data-ttu-id="fb0dd-161">De cmdlet retourneert de lijst met eigenaren voor de opgegeven groep:</span><span class="sxs-lookup"><span data-stu-id="fb0dd-161">The cmdlet returns the list of owners for the specified group:</span></span>

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          e831b3fd-77c9-49c7-9fca-de43e109ef67 User

<span data-ttu-id="fb0dd-162">Als u een eigenaar verwijderen uit een groep wilt, gebruikt u de cmdlet Remove-AzureADGroupOwner:</span><span class="sxs-lookup"><span data-stu-id="fb0dd-162">If you want to remove an owner from a group, use the Remove-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> remove-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -OwnerId e831b3fd-77c9-49c7-9fca-de43e109ef67

## <a name="reserved-aliases"></a><span data-ttu-id="fb0dd-163">Gereserveerde aliassen</span><span class="sxs-lookup"><span data-stu-id="fb0dd-163">Reserved aliases</span></span> 
<span data-ttu-id="fb0dd-164">Wanneer een groep is gemaakt, bepaalde eindpunten toestaan dat de eindgebruiker een mailNickname of alias moet worden gebruikt als onderdeel van het e-mailadres van de groep opgeven.</span><span class="sxs-lookup"><span data-stu-id="fb0dd-164">When a group is created, certain endpoints allow the end user to specify a mailNickname or alias to be used as part of the email address of the group.</span></span> <span data-ttu-id="fb0dd-165">Groepen met de volgende bijzondere rechten e-aliassen kunnen alleen worden gemaakt door een globale beheerder van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fb0dd-165">Groups with the following highly privileged email aliases can only be created by an Azure AD global administrator.</span></span> 
  
* <span data-ttu-id="fb0dd-166">misbruik</span><span class="sxs-lookup"><span data-stu-id="fb0dd-166">abuse</span></span> 
* <span data-ttu-id="fb0dd-167">Beheerder</span><span class="sxs-lookup"><span data-stu-id="fb0dd-167">admin</span></span> 
* <span data-ttu-id="fb0dd-168">Beheerder</span><span class="sxs-lookup"><span data-stu-id="fb0dd-168">administrator</span></span> 
* <span data-ttu-id="fb0dd-169">hostmaster</span><span class="sxs-lookup"><span data-stu-id="fb0dd-169">hostmaster</span></span> 
* <span data-ttu-id="fb0dd-170">majordomo</span><span class="sxs-lookup"><span data-stu-id="fb0dd-170">majordomo</span></span> 
* <span data-ttu-id="fb0dd-171">postbeheerder</span><span class="sxs-lookup"><span data-stu-id="fb0dd-171">postmaster</span></span> 
* <span data-ttu-id="fb0dd-172">hoofdmap</span><span class="sxs-lookup"><span data-stu-id="fb0dd-172">root</span></span> 
* <span data-ttu-id="fb0dd-173">Beveiligen</span><span class="sxs-lookup"><span data-stu-id="fb0dd-173">secure</span></span> 
* <span data-ttu-id="fb0dd-174">Beveiliging</span><span class="sxs-lookup"><span data-stu-id="fb0dd-174">security</span></span> 
* <span data-ttu-id="fb0dd-175">SSL-beheerder</span><span class="sxs-lookup"><span data-stu-id="fb0dd-175">ssl-admin</span></span> 
* <span data-ttu-id="fb0dd-176">beheerder</span><span class="sxs-lookup"><span data-stu-id="fb0dd-176">webmaster</span></span> 

## <a name="next-steps"></a><span data-ttu-id="fb0dd-177">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fb0dd-177">Next steps</span></span>
<span data-ttu-id="fb0dd-178">U vindt meer Azure Active Directory PowerShell-documentatie op [Azure Active Directory-Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="fb0dd-178">You can find more Azure Active Directory PowerShell documentation at [Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

* <span data-ttu-id="fb0dd-179">[Managing access to resources with Azure Active Directory groups](active-directory-manage-groups.md) (Toegang tot resources beheren met Azure Active Directory-groepen)</span><span class="sxs-lookup"><span data-stu-id="fb0dd-179">[Managing access to resources with Azure Active Directory groups](active-directory-manage-groups.md)</span></span>
* [<span data-ttu-id="fb0dd-180">Uw on-premises identiteiten integreren met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fb0dd-180">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
