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
# <a name="azure-active-directory-version-2-cmdlets-for-group-management"></a><span data-ttu-id="2460e-104">Azure Active Directory-cmdlets van versie 2 voor groepsbeheer</span><span class="sxs-lookup"><span data-stu-id="2460e-104">Azure Active Directory version 2 cmdlets for group management</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2460e-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="2460e-105">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="2460e-106">Klassieke Azure Portal</span><span class="sxs-lookup"><span data-stu-id="2460e-106">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="2460e-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2460e-107">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="2460e-108">Dit artikel bevat voorbeelden van hoe toouse PowerShell toomanage uw groepen in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2460e-108">This article contains examples of how toouse PowerShell toomanage your groups in Azure Active Directory (Azure AD).</span></span>  <span data-ttu-id="2460e-109">Deze ook ziet u hoe de tooget instellen met hello Azure AD PowerShell-module.</span><span class="sxs-lookup"><span data-stu-id="2460e-109">It also tells you how tooget set up with hello Azure AD PowerShell module.</span></span> <span data-ttu-id="2460e-110">Eerst moet u [hello Azure AD PowerShell-module downloaden](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="2460e-110">First, you must [download hello Azure AD PowerShell module](https://www.powershellgallery.com/packages/AzureAD/).</span></span>

## <a name="installing-hello-azure-ad-powershell-module"></a><span data-ttu-id="2460e-111">Hello Azure AD PowerShell-module installeren</span><span class="sxs-lookup"><span data-stu-id="2460e-111">Installing hello Azure AD PowerShell module</span></span>
<span data-ttu-id="2460e-112">tooinstall hello Azure AD PowerShell-module, gebruikt u Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="2460e-112">tooinstall hello Azure AD PowerShell module, use hello following commands:</span></span>

    PS C:\Windows\system32> install-module azuread

<span data-ttu-id="2460e-113">tooverify die Hallo module is geïnstalleerd, Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="2460e-113">tooverify that hello module was installed, use hello following command:</span></span>

    PS C:\Windows\system32> get-module azuread

    ModuleType Version      Name                                ExportedCommands
    ---------- ---------    ----                                ----------------
    Binary     2.0.0.115    azuread                      {Add-AzureADAdministrati...}

<span data-ttu-id="2460e-114">U kunt nu starten met Hallo-cmdlets in Hallo-module.</span><span class="sxs-lookup"><span data-stu-id="2460e-114">Now you can start using hello cmdlets in hello module.</span></span> <span data-ttu-id="2460e-115">Raadpleeg voor een volledige beschrijving van de cmdlets Hallo in hello Azure AD-module toohello online naslagdocumentatie voor [Azure Active Directory PowerShell versie 2](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="2460e-115">For a full description of hello cmdlets in hello Azure AD module, please refer toohello online reference documentation for [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

## <a name="connecting-toohello-directory"></a><span data-ttu-id="2460e-116">Verbinding maken met toohello directory</span><span class="sxs-lookup"><span data-stu-id="2460e-116">Connecting toohello directory</span></span>
<span data-ttu-id="2460e-117">Voordat u kunt het beheer van groepen met behulp van Azure AD PowerShell-cmdlets, moet u uw directory PowerShell-sessie toohello u toomanage wilt verbinden.</span><span class="sxs-lookup"><span data-stu-id="2460e-117">Before you can start managing groups using Azure AD PowerShell cmdlets, you must connect your PowerShell session toohello directory you want toomanage.</span></span> <span data-ttu-id="2460e-118">Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="2460e-118">Use hello following command:</span></span>

    PS C:\Windows\system32> Connect-AzureAD

<span data-ttu-id="2460e-119">Hallo cmdlet vraagt naar Hallo referenties die u wilt dat toouse tooaccess uw directory.</span><span class="sxs-lookup"><span data-stu-id="2460e-119">hello cmdlet prompts you for hello credentials you want toouse tooaccess your directory.</span></span> <span data-ttu-id="2460e-120">In dit voorbeeld gebruiken we karen@drumkit.onmicrosoft.com tooaccess Hallo demonstratie directory.</span><span class="sxs-lookup"><span data-stu-id="2460e-120">In this example, we are using karen@drumkit.onmicrosoft.com tooaccess hello demonstration directory.</span></span> <span data-ttu-id="2460e-121">Hallo cmdlet retourneert een bevestiging tooshow Hallo-sessie met succes was verbonden tooyour directory:</span><span class="sxs-lookup"><span data-stu-id="2460e-121">hello cmdlet returns a confirmation tooshow hello session was connected successfully tooyour directory:</span></span>

    Account                       Environment Tenant
    -------                       ----------- ------
    Karen@drumkit.onmicrosoft.com AzureCloud  85b5ff1e-0402-400c-9e3c-0f…

<span data-ttu-id="2460e-122">U kunt nu starten met Hallo AzureAD cmdlets toomanage groepen in uw directory.</span><span class="sxs-lookup"><span data-stu-id="2460e-122">Now you can start using hello AzureAD cmdlets toomanage groups in your directory.</span></span>

## <a name="retrieving-groups"></a><span data-ttu-id="2460e-123">Bij het ophalen van groepen</span><span class="sxs-lookup"><span data-stu-id="2460e-123">Retrieving groups</span></span>
<span data-ttu-id="2460e-124">de bestaande groepen tooretrieve van uw directory die kunt u Hallo de cmdlet Get-AzureADGroups.</span><span class="sxs-lookup"><span data-stu-id="2460e-124">tooretrieve existing groups from your directory you can use hello Get-AzureADGroups cmdlet.</span></span> <span data-ttu-id="2460e-125">tooretrieve alle groepen in de directory hello, gebruik de cmdlet Hallo zonder parameters:</span><span class="sxs-lookup"><span data-stu-id="2460e-125">tooretrieve all groups in hello directory, use hello cmdlet without parameters:</span></span>

    PS C:\Windows\system32> get-azureadgroup

<span data-ttu-id="2460e-126">Hallo cmdlet retourneert alle groepen in gekoppelde Hallo-adreslijst.</span><span class="sxs-lookup"><span data-stu-id="2460e-126">hello cmdlet returns all groups in hello connected directory.</span></span>

<span data-ttu-id="2460e-127">Hallo - object-id-parameter tooretrieve kunt u een specifieke groep waarvoor u een van de groep Hallo objectID opgeven:</span><span class="sxs-lookup"><span data-stu-id="2460e-127">You can use hello -objectID parameter tooretrieve a specific group for which you specify hello group’s objectID:</span></span>

    PS C:\Windows\system32> get-azureadgroup -ObjectId e29bae11-4ac0-450c-bc37-6dae8f3da61b

<span data-ttu-id="2460e-128">Hallo cmdlet retourneert nu Hallo-groep waarvan objectID overeenkomt met de waarde Hallo van Hallo-parameter die u hebt ingevoerd:</span><span class="sxs-lookup"><span data-stu-id="2460e-128">hello cmdlet now returns hello group whose objectID matches hello value of hello parameter you entered:</span></span>

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

<span data-ttu-id="2460e-129">U kunt zoeken naar een specifieke groep met Hallo - filter-parameter.</span><span class="sxs-lookup"><span data-stu-id="2460e-129">You can search for a specific group using hello -filter parameter.</span></span> <span data-ttu-id="2460e-130">Deze parameter heeft een ODATA-filter-component en resulteert in alle groepen die overeenkomen met de Hallo-filter, zoals in het volgende voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="2460e-130">This parameter takes an ODATA filter clause and returns all groups that match hello filter, as in hello following example:</span></span>

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
> <span data-ttu-id="2460e-131">Hallo AzureAD PowerShell-cmdlets Hallo OData-query die standaard worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="2460e-131">hello AzureAD PowerShell cmdlets implement hello OData query standard.</span></span> <span data-ttu-id="2460e-132">Zie voor meer informatie **$filter** in [OData-query systeemopties Hallo OData-eindpunt met](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter).</span><span class="sxs-lookup"><span data-stu-id="2460e-132">For more information, see **$filter** in [OData system query options using hello OData endpoint](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter).</span></span>

## <a name="creating-groups"></a><span data-ttu-id="2460e-133">Groepen maken</span><span class="sxs-lookup"><span data-stu-id="2460e-133">Creating groups</span></span>
<span data-ttu-id="2460e-134">een nieuwe groep in uw directory, gebruik de cmdlet New-AzureADGroup hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="2460e-134">toocreate a new group in your directory, use hello New-AzureADGroup cmdlet.</span></span> <span data-ttu-id="2460e-135">Deze cmdlet maakt een nieuwe beveiligingsgroep met de naam 'Marketing':</span><span class="sxs-lookup"><span data-stu-id="2460e-135">This cmdlet creates a new security group called “Marketing":</span></span>

    PS C:\Windows\system32> New-AzureADGroup -Description "Marketing" -DisplayName "Marketing" -MailEnabled $false -SecurityEnabled $true -MailNickName "Marketing"

## <a name="updating-groups"></a><span data-ttu-id="2460e-136">Bijwerken van groepen</span><span class="sxs-lookup"><span data-stu-id="2460e-136">Updating groups</span></span>
<span data-ttu-id="2460e-137">een bestaande groep tooupdate Hallo Set AzureADGroup cmdlet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2460e-137">tooupdate an existing group, use hello Set-AzureADGroup cmdlet.</span></span> <span data-ttu-id="2460e-138">In dit voorbeeld wijzigt we Hallo eigenschap DisplayName van Hallo groep 'Intune-beheerders'.</span><span class="sxs-lookup"><span data-stu-id="2460e-138">In this example, we’re changing hello DisplayName property of hello group “Intune Administrators.”</span></span> <span data-ttu-id="2460e-139">We je eerst Hallo-groep met behulp van Hallo Get AzureADGroup cmdlet en filteren met Hallo DisplayName kenmerk zoeken:</span><span class="sxs-lookup"><span data-stu-id="2460e-139">First, we’re finding hello group using hello Get-AzureADGroup cmdlet and filter using hello DisplayName attribute:</span></span>

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

<span data-ttu-id="2460e-140">Vervolgens wijzigt we Hallo beschrijving toohello nieuwe waarde van de eigenschap 'Intune apparaat Administrators':</span><span class="sxs-lookup"><span data-stu-id="2460e-140">Next, we’re changing hello Description property toohello new value “Intune Device Administrators”:</span></span>

    PS C:\Windows\system32> Set-AzureADGroup -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -Description "Intune Device Administrators"

<span data-ttu-id="2460e-141">Is bijgewerkt tooreflect nieuwe waarde in Media Player Hallo nu als we Hallo groep opnieuw vinden, ziet u de eigenschap Description Hallo:</span><span class="sxs-lookup"><span data-stu-id="2460e-141">Now if we find hello group again, we see hello Description property is updated tooreflect hello new value:</span></span>

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

## <a name="deleting-groups"></a><span data-ttu-id="2460e-142">Groepen verwijderen</span><span class="sxs-lookup"><span data-stu-id="2460e-142">Deleting groups</span></span>
<span data-ttu-id="2460e-143">groepen van uw directory toodelete Hallo verwijderen AzureADGroup cmdlet als volgt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="2460e-143">toodelete groups from your directory, use hello Remove-AzureADGroup cmdlet as follows:</span></span>

    PS C:\Windows\system32> Remove-AzureADGroup -ObjectId b11ca53e-07cc-455d-9a89-1fe3ab24566b

## <a name="managing-members-of-groups"></a><span data-ttu-id="2460e-144">Leden van groepen beheren</span><span class="sxs-lookup"><span data-stu-id="2460e-144">Managing members of groups</span></span>
<span data-ttu-id="2460e-145">Als u moet de nieuwe groep van leden tooa tooadd, Hallo toevoegen AzureADGroupMember cmdlet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2460e-145">If you need tooadd new members tooa group, use hello Add-AzureADGroupMember cmdlet.</span></span> <span data-ttu-id="2460e-146">Met deze opdracht wordt een lid toohello Intune-beheerders groep die wordt gebruikt in het vorige voorbeeld Hallo toegevoegd:</span><span class="sxs-lookup"><span data-stu-id="2460e-146">This command adds a member toohello Intune Administrators group we used in hello previous example:</span></span>

    PS C:\Windows\system32> Add-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="2460e-147">Hallo - object-id-parameter is Hallo ObjectID van Hallo groep toowhich willen we tooadd lid en Hallo - RefObjectId is Hallo object-id van gebruiker Hallo willen we tooadd als een lid toohello-groep.</span><span class="sxs-lookup"><span data-stu-id="2460e-147">hello -ObjectId parameter is hello ObjectID of hello group toowhich we want tooadd a member, and hello -RefObjectId is hello ObjectID of hello user we want tooadd as a member toohello group.</span></span>

<span data-ttu-id="2460e-148">tooget hello bestaande leden van een groep gebruikt de cmdlet Get-AzureADGroupMember hello, zoals in dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2460e-148">tooget hello existing members of a group, use hello Get-AzureADGroupMember cmdlet, as in this example:</span></span>

    PS C:\Windows\system32> Get-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          72cd4bbd-2594-40a2-935c-016f3cfeeeea User
                          8120cc36-64b4-4080-a9e8-23aa98e8b34f User

<span data-ttu-id="2460e-149">tooremove hello lid we toegevoegd eerder toohello groep gebruik Hallo verwijderen AzureADGroupMember cmdlet, zoals hier wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="2460e-149">tooremove hello member we previously added toohello group, use hello Remove-AzureADGroupMember cmdlet, as is shown here:</span></span>

    PS C:\Windows\system32> Remove-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -MemberId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="2460e-150">tooverify hello groep lidmaatschappen van een gebruiker Hallo Selecteer AzureADGroupIdsUserIsMemberOf cmdlet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2460e-150">tooverify hello group membership(s) of a user, use hello Select-AzureADGroupIdsUserIsMemberOf cmdlet.</span></span> <span data-ttu-id="2460e-151">Deze cmdlet wordt als de parameters Hallo object-id van de gebruiker Hallo voor welke toocheck Hallo-groepslidmaatschappen en een lijst met groepen voor welke toocheck Hallo lidmaatschappen.</span><span class="sxs-lookup"><span data-stu-id="2460e-151">This cmdlet takes as its parameters hello ObjectId of hello user for which toocheck hello group memberships, and a list of groups for which toocheck hello memberships.</span></span> <span data-ttu-id="2460e-152">Hallo-lijst met groepen moet zijn opgegeven in Hallo vorm van een complex variabele van type 'Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck', dus we eerst moet een variabele met dit type maken:</span><span class="sxs-lookup"><span data-stu-id="2460e-152">hello list of groups must be provided in hello form of a complex variable of type “Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck”, so we first must create a variable with that type:</span></span>

    PS C:\Windows\system32> $g = new-object Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck

<span data-ttu-id="2460e-153">We vervolgens opgeven waarden voor Hallo groupIds toocheck in Hallo kenmerk 'GroupIds' van deze variabele complex:</span><span class="sxs-lookup"><span data-stu-id="2460e-153">Next, we provide values for hello groupIds toocheck in hello attribute “GroupIds” of this complex variable:</span></span>

    PS C:\Windows\system32> $g.GroupIds = "b11ca53e-07cc-455d-9a89-1fe3ab24566b", "31f1ff6c-d48c-4f8a-b2e1-abca7fd399df"

<span data-ttu-id="2460e-154">Nu we toocheck Hallo groepslidmaatschappen van een gebruiker met ObjectID 72cd4bbd-2594-40a2-935c-016f3cfeeeea tegen Hallo groepen in $g kunt dat we moeten gebruiken:</span><span class="sxs-lookup"><span data-stu-id="2460e-154">Now, if we want toocheck hello group memberships of a user with ObjectID 72cd4bbd-2594-40a2-935c-016f3cfeeeea against hello groups in $g, we should use:</span></span>

    PS C:\Windows\system32> Select-AzureADGroupIdsUserIsMemberOf -ObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea -GroupIdsForMembershipCheck $g

    OdataMetadata                                                                                                 Value
    -------------                                                                                                  -----
    https://graph.windows.net/85b5ff1e-0402-400c-9e3c-0f9e965325d1/$metadata#Collection(Edm.String)             {31f1ff6c-d48c-4f8a-b2e1-abca7fd399df}


<span data-ttu-id="2460e-155">Hallo-waarde die het resultaat is een lijst met groepen waarvan deze gebruiker lid is.</span><span class="sxs-lookup"><span data-stu-id="2460e-155">hello value returned is a list of groups of which this user is a member.</span></span> <span data-ttu-id="2460e-156">U kunt deze methode toocheck contactpersonen, groepen of Service-Principals lidmaatschap voor een opgegeven lijst met groepen met behulp van de Select-AzureADGroupIdsContactIsMemberOf, selecteer AzureADGroupIdsGroupIsMemberOf ook toepassen of Selecteer AzureADGroupIdsServicePrincipalIsMemberOf</span><span class="sxs-lookup"><span data-stu-id="2460e-156">You can also apply this method toocheck Contacts, Groups or Service Principals membership for a given list of groups, using Select-AzureADGroupIdsContactIsMemberOf, Select-AzureADGroupIdsGroupIsMemberOf or Select-AzureADGroupIdsServicePrincipalIsMemberOf</span></span>

## <a name="managing-owners-of-groups"></a><span data-ttu-id="2460e-157">Eigenaren van groepen beheren</span><span class="sxs-lookup"><span data-stu-id="2460e-157">Managing owners of groups</span></span>
<span data-ttu-id="2460e-158">tooadd eigenaars tooa groep, gebruik de cmdlet Add-AzureADGroupOwner Hallo:</span><span class="sxs-lookup"><span data-stu-id="2460e-158">tooadd owners tooa group, use hello Add-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> Add-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="2460e-159">Hallo - object-id-parameter is Hallo ObjectID van Hallo groep toowhich willen we tooadd een eigenaar en Hallo - RefObjectId is Hallo object-id van gebruiker Hallo willen we tooadd als een eigenaar van het Hallo-groep.</span><span class="sxs-lookup"><span data-stu-id="2460e-159">hello -ObjectId parameter is hello ObjectID of hello group toowhich we want tooadd an owner, and hello -RefObjectId is hello ObjectID of hello user we want tooadd as an owner of hello group.</span></span>

<span data-ttu-id="2460e-160">tooretrieve hello eigenaren van een groep, gebruikt u Hallo Get AzureADGroupOwner cmdlet:</span><span class="sxs-lookup"><span data-stu-id="2460e-160">tooretrieve hello owners of a group, use hello Get-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> Get-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

<span data-ttu-id="2460e-161">Hallo cmdlet retourneert Hallo lijst met eigenaren voor de opgegeven groep Hallo:</span><span class="sxs-lookup"><span data-stu-id="2460e-161">hello cmdlet returns hello list of owners for hello specified group:</span></span>

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          e831b3fd-77c9-49c7-9fca-de43e109ef67 User

<span data-ttu-id="2460e-162">Als u een eigenaar van een groep tooremove wilt, gebruikt u Hallo verwijderen AzureADGroupOwner cmdlet:</span><span class="sxs-lookup"><span data-stu-id="2460e-162">If you want tooremove an owner from a group, use hello Remove-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> remove-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -OwnerId e831b3fd-77c9-49c7-9fca-de43e109ef67

## <a name="reserved-aliases"></a><span data-ttu-id="2460e-163">Gereserveerde aliassen</span><span class="sxs-lookup"><span data-stu-id="2460e-163">Reserved aliases</span></span> 
<span data-ttu-id="2460e-164">Wanneer een groep is gemaakt, kunnen bepaalde eindpunten Hallo eindgebruiker toospecify een mailNickname of alias toobe gebruikt als onderdeel van het e-mailadres van de groep Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="2460e-164">When a group is created, certain endpoints allow hello end user toospecify a mailNickname or alias toobe used as part of hello email address of hello group.</span></span> <span data-ttu-id="2460e-165">Groepen met bijzondere rechten e-aliassen te volgen hello kunnen alleen worden gemaakt door een globale beheerder van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2460e-165">Groups with hello following highly privileged email aliases can only be created by an Azure AD global administrator.</span></span> 
  
* <span data-ttu-id="2460e-166">misbruik</span><span class="sxs-lookup"><span data-stu-id="2460e-166">abuse</span></span> 
* <span data-ttu-id="2460e-167">Beheerder</span><span class="sxs-lookup"><span data-stu-id="2460e-167">admin</span></span> 
* <span data-ttu-id="2460e-168">Beheerder</span><span class="sxs-lookup"><span data-stu-id="2460e-168">administrator</span></span> 
* <span data-ttu-id="2460e-169">hostmaster</span><span class="sxs-lookup"><span data-stu-id="2460e-169">hostmaster</span></span> 
* <span data-ttu-id="2460e-170">majordomo</span><span class="sxs-lookup"><span data-stu-id="2460e-170">majordomo</span></span> 
* <span data-ttu-id="2460e-171">postbeheerder</span><span class="sxs-lookup"><span data-stu-id="2460e-171">postmaster</span></span> 
* <span data-ttu-id="2460e-172">hoofdmap</span><span class="sxs-lookup"><span data-stu-id="2460e-172">root</span></span> 
* <span data-ttu-id="2460e-173">Beveiligen</span><span class="sxs-lookup"><span data-stu-id="2460e-173">secure</span></span> 
* <span data-ttu-id="2460e-174">Beveiliging</span><span class="sxs-lookup"><span data-stu-id="2460e-174">security</span></span> 
* <span data-ttu-id="2460e-175">SSL-beheerder</span><span class="sxs-lookup"><span data-stu-id="2460e-175">ssl-admin</span></span> 
* <span data-ttu-id="2460e-176">beheerder</span><span class="sxs-lookup"><span data-stu-id="2460e-176">webmaster</span></span> 

## <a name="next-steps"></a><span data-ttu-id="2460e-177">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2460e-177">Next steps</span></span>
<span data-ttu-id="2460e-178">U vindt meer Azure Active Directory PowerShell-documentatie op [Azure Active Directory-Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="2460e-178">You can find more Azure Active Directory PowerShell documentation at [Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

* [<span data-ttu-id="2460e-179">Tooresources toegang beheren met Azure Active Directory-groepen</span><span class="sxs-lookup"><span data-stu-id="2460e-179">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="2460e-180">Uw on-premises identiteiten integreren met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2460e-180">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
