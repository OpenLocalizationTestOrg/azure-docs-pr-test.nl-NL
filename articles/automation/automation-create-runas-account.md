---
title: aaaCreate Automation Azure die Run As-accounts | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooupdate uw Automation-account in en Run As-accounts maken met PowerShell of vanuit het Hallo-portal.
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/27/2017
ms.author: magoedte
ms.openlocfilehash: 94eb54fa0b518056a726d17146c63411e248273b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-automation-account-authentication-with-run-as-accounts"></a><span data-ttu-id="a7189-103">Uw Automation-account bijwerken met Uitvoeren als-accounts</span><span class="sxs-lookup"><span data-stu-id="a7189-103">Update your Automation account authentication with Run As accounts</span></span> 
<span data-ttu-id="a7189-104">U kunt uw bestaande Automation-account via de portal Hallo bijwerken of PowerShell gebruiken als:</span><span class="sxs-lookup"><span data-stu-id="a7189-104">You can update your existing Automation account from hello portal or use PowerShell if:</span></span>

* <span data-ttu-id="a7189-105">U maakt een Automation-account maar weigeren toocreate Hallo Run As-account.</span><span class="sxs-lookup"><span data-stu-id="a7189-105">You create an Automation account but decline toocreate hello Run As account.</span></span>
* <span data-ttu-id="a7189-106">U al een Automation-account toomanage Resource Manager-resources gebruikt en gewenste tooupdate Hallo account tooinclude Hallo Run As-account voor de runbook-verificatie.</span><span class="sxs-lookup"><span data-stu-id="a7189-106">You already use an Automation account toomanage Resource Manager resources and you want tooupdate hello account tooinclude hello Run As account for runbook authentication.</span></span>
* <span data-ttu-id="a7189-107">U al een Automation-account toomanage klassieke resources gebruikt en u wilt tooupdate het toouse Hallo klassieke Run As-account in plaats van een nieuw account maken en uw runbooks en activa tooit migreren.</span><span class="sxs-lookup"><span data-stu-id="a7189-107">You already use an Automation account toomanage classic resources and you want tooupdate it toouse hello Classic Run As account instead of creating a new account and migrating your runbooks and assets tooit.</span></span>   
* <span data-ttu-id="a7189-108">Toocreate wilt u een Run As- en klassieke Run As-account met behulp van een certificaat zijn uitgegeven door uw enterprise-certificeringsinstantie (CA).</span><span class="sxs-lookup"><span data-stu-id="a7189-108">You want toocreate a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a7189-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a7189-109">Prerequisites</span></span>

* <span data-ttu-id="a7189-110">Hallo-script kan worden uitgevoerd alleen op Windows 10 en Windows Server 2016 met Azure Resource Manager-modules 3.0.0 en hoger.</span><span class="sxs-lookup"><span data-stu-id="a7189-110">hello script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 3.0.0 and later.</span></span> <span data-ttu-id="a7189-111">Uitvoeren wordt niet ondersteund in eerdere versies van Windows.</span><span class="sxs-lookup"><span data-stu-id="a7189-111">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="a7189-112">Azure PowerShell 1.0 en hoger.</span><span class="sxs-lookup"><span data-stu-id="a7189-112">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="a7189-113">Zie voor meer informatie over Hallo PowerShell 1.0 release [hoe tooinstall en configureren van Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="a7189-113">For information about hello PowerShell 1.0 release, see [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>
* <span data-ttu-id="a7189-114">Een Automation-account waarnaar wordt verwezen als waarde voor Hallo Hallo *-AutomationAccountName* en *- ApplicationDisplayName* parameters in de volgende PowerShell-script Hallo.</span><span class="sxs-lookup"><span data-stu-id="a7189-114">An Automation account, which is referenced as hello value for hello *–AutomationAccountName* and *-ApplicationDisplayName* parameters in hello following PowerShell script.</span></span>

<span data-ttu-id="a7189-115">Hallo tooget waarden voor *SubscriptionID*, *ResourceGroup*, en *AutomationAccountName*, die de vereiste parameters voor Hallo script zijn, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="a7189-115">tooget hello values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for hello script, do hello following:</span></span>

1. <span data-ttu-id="a7189-116">In Hallo Azure-portal, selecteert u uw Automation-account op Hallo **Automation-account** blade en selecteer vervolgens **alle instellingen**.</span><span class="sxs-lookup"><span data-stu-id="a7189-116">In hello Azure portal, select your Automation account on hello **Automation account** blade, and then select **All settings**.</span></span>  
2. <span data-ttu-id="a7189-117">Op Hallo **alle instellingen** blade onder **Accountinstellingen**, selecteer **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="a7189-117">On hello **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="a7189-118">Houd er rekening mee Hallo waarden op Hallo **eigenschappen** blade.</span><span class="sxs-lookup"><span data-stu-id="a7189-118">Note hello values on hello **Properties** blade.</span></span><br><br> <span data-ttu-id="a7189-119">![blade 'Eigenschappen' Hello Automation-account](media/automation-create-runas-account/automation-account-properties.png)</span><span class="sxs-lookup"><span data-stu-id="a7189-119">![hello Automation account "Properties" blade](media/automation-create-runas-account/automation-account-properties.png)</span></span>  

### <a name="required-permissions-tooupdate-your-automation-account"></a><span data-ttu-id="a7189-120">Vereiste machtigingen tooupdate uw Automation-account</span><span class="sxs-lookup"><span data-stu-id="a7189-120">Required permissions tooupdate your Automation account</span></span>
<span data-ttu-id="a7189-121">tooupdate een Automation-account, hebt u Hallo na specifieke rechten en machtigingen nodig toocomplete in dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="a7189-121">tooupdate an Automation account, you must have hello following specific privileges and permissions required toocomplete this topic.</span></span>   
 
* <span data-ttu-id="a7189-122">Uw AD-gebruikersaccount moet toobe toegevoegde tooa rol met de rol van Inzender gelijkwaardige toohello machtigingen voor Microsoft.Automation bronnen, zoals wordt beschreven in artikel [toegangsbeheer op basis van rollen in Azure Automation](automation-role-based-access-control.md#contributor-role-permissions).</span><span class="sxs-lookup"><span data-stu-id="a7189-122">Your AD user account needs toobe added tooa role with permissions equivalent toohello Contributor role for Microsoft.Automation resources as outlined in article [Role-based access control in Azure Automation](automation-role-based-access-control.md#contributor-role-permissions).</span></span>  
* <span data-ttu-id="a7189-123">Gebruikers zonder beheerdersrechten in uw Azure AD-tenant kunnen [AD-toepassingen registreren](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions) als Hallo App registraties instellen te is ingesteld**Ja**.</span><span class="sxs-lookup"><span data-stu-id="a7189-123">Non-admin users in your Azure AD tenant can [register AD applications](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions) if hello App registrations setting is set too**Yes**.</span></span>  <span data-ttu-id="a7189-124">Als Hallo app registraties instellen te is ingesteld**Nee**, Hallo gebruiker deze bewerking moet een globale beheerder in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a7189-124">If hello app registrations setting is set too**No**, hello user performing this action must be a global administrator in Azure AD.</span></span> 

<span data-ttu-id="a7189-125">Als u niet lid zijn van de Active Directory-exemplaar van Hallo abonnement voordat u toohello globale beheerder/SA-administrator-rol van Hallo abonnement worden toegevoegd, kunt u tooActive Directory wordt toegevoegd als gast.</span><span class="sxs-lookup"><span data-stu-id="a7189-125">If you are not a member of hello subscription’s Active Directory instance before you are added toohello global administrator/co-administrator role of hello subscription, you are added tooActive Directory as a guest.</span></span> <span data-ttu-id="a7189-126">In dit geval ontvangt u een "u hebt geen machtigingen toocreate..."</span><span class="sxs-lookup"><span data-stu-id="a7189-126">In this situation, you receive a “You do not have permissions toocreate…”</span></span> <span data-ttu-id="a7189-127">Waarschuwing voor Hallo **Automation-Account toevoegen** blade.</span><span class="sxs-lookup"><span data-stu-id="a7189-127">warning on hello **Add Automation Account** blade.</span></span> <span data-ttu-id="a7189-128">Gebruikers die zijn toegevoegd toohello globale beheerder/SA-administrator-rol kan worden verwijderd uit Active Directory-exemplaar van het abonnement Hallo eerst en opnieuw toegevoegd toomake ze een volledige gebruiker in Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a7189-128">Users who were added toohello global administrator/co-administrator role first can be removed from hello subscription's Active Directory instance and re-added toomake them a full User in Active Directory.</span></span> <span data-ttu-id="a7189-129">tooverify deze situatie van Hallo **Azure Active Directory** deelvenster in Azure portal, selecteer Hallo **gebruikers en groepen**, selecteer **alle gebruikers** en, nadat u Hallo selecteren specifieke gebruiker, schakelt **profiel**.</span><span class="sxs-lookup"><span data-stu-id="a7189-129">tooverify this situation, from hello **Azure Active Directory** pane in hello Azure portal, select **Users and groups**, select **All users** and, after you select hello specific user, select **Profile**.</span></span> <span data-ttu-id="a7189-130">waarde van Hallo Hallo **gebruikerstype** kenmerk onder Hallo gebruikersprofiel moet niet gelijk aan **Gast**.</span><span class="sxs-lookup"><span data-stu-id="a7189-130">hello value of hello **User type** attribute under hello users profile should not equal **Guest**.</span></span>

## <a name="create-run-as-account-from-hello-portal"></a><span data-ttu-id="a7189-131">Run As-account maken vanuit Hallo-portal</span><span class="sxs-lookup"><span data-stu-id="a7189-131">Create Run As account from hello portal</span></span>
<span data-ttu-id="a7189-132">In deze sectie volgende stappen tooupdate Hallo uw Azure Automation-account van uitvoeren hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a7189-132">In this section, perform hello following steps tooupdate your Azure Automation account from  hello Azure portal.</span></span>  <span data-ttu-id="a7189-133">U maakt Hallo uitvoeren als en klassieke Run As-accounts afzonderlijk, en als u geen bronnen in de klassieke Azure portal Hallo toomanage nodig hebt, kunt u alleen hello Azure uitvoeren als-account maken.</span><span class="sxs-lookup"><span data-stu-id="a7189-133">You create hello Run As and Classic Run As accounts individually, and if you don't need toomanage resources in hello classic Azure portal, you can just create hello Azure Run As account.</span></span>  

<span data-ttu-id="a7189-134">Hallo-proces maakt Hallo volgende items in uw Automation-account.</span><span class="sxs-lookup"><span data-stu-id="a7189-134">hello process creates hello following items in your Automation account.</span></span>

<span data-ttu-id="a7189-135">**Voor Uitvoeren als-accounts:**</span><span class="sxs-lookup"><span data-stu-id="a7189-135">**For Run As accounts:**</span></span>

* <span data-ttu-id="a7189-136">Een Azure AD-toepassing met een zelfondertekend certificaat maakt, maakt een account voor de service-principal voor de toepassing hello in Azure AD en wijst de rol van Inzender Hallo voor Hallo-account in uw huidige abonnement.</span><span class="sxs-lookup"><span data-stu-id="a7189-136">Creates an Azure AD application with a self-signed certificate, creates a service principal account for hello application in Azure AD, and assigns hello Contributor role for hello account in your current subscription.</span></span> <span data-ttu-id="a7189-137">U kunt deze instelling tooOwner of een andere rol wijzigen.</span><span class="sxs-lookup"><span data-stu-id="a7189-137">You can change this setting tooOwner or any other role.</span></span> <span data-ttu-id="a7189-138">Zie [Op rollen gebaseerd toegangsbeheer in Azure Automation](automation-role-based-access-control.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="a7189-138">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="a7189-139">Hiermee maakt u een Automation-certificaatasset met de naam *AzureRunAsCertificate* in Hallo opgegeven Automation-account.</span><span class="sxs-lookup"><span data-stu-id="a7189-139">Creates an Automation certificate asset named *AzureRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="a7189-140">Hallo-certificaatasset bevat Hallo privésleutel voor certificaten die wordt gebruikt door de toepassing hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a7189-140">hello certificate asset holds hello certificate private key that's used by hello Azure AD application.</span></span>
* <span data-ttu-id="a7189-141">Hiermee maakt u een Automation-verbindingsasset genaamd *AzureRunAsConnection* in Hallo opgegeven Automation-account.</span><span class="sxs-lookup"><span data-stu-id="a7189-141">Creates an Automation connection asset named *AzureRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="a7189-142">Hallo-verbindingsasset bevat Hallo applicationId, tenantId, subscriptionId en de vingerafdruk van certificaat.</span><span class="sxs-lookup"><span data-stu-id="a7189-142">hello connection asset holds hello applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="a7189-143">**Voor klassieke uitvoeren als-accounts:**</span><span class="sxs-lookup"><span data-stu-id="a7189-143">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="a7189-144">Hiermee maakt u een Automation-certificaatasset met de naam *AzureClassicRunAsCertificate* in Hallo opgegeven Automation-account.</span><span class="sxs-lookup"><span data-stu-id="a7189-144">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="a7189-145">Hallo-certificaatasset bevat Hallo privésleutel voor certificaten die door het Hallo-beheercertificaat gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a7189-145">hello certificate asset holds hello certificate private key used by hello management certificate.</span></span>
* <span data-ttu-id="a7189-146">Hiermee maakt u een Automation-verbindingsasset genaamd *AzureClassicRunAsConnection* in Hallo opgegeven Automation-account.</span><span class="sxs-lookup"><span data-stu-id="a7189-146">Creates an Automation connection asset named *AzureClassicRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="a7189-147">Hallo-verbindingsasset bevat Hallo abonnementsnaam, abonnements-id en naam van certificaat asset.</span><span class="sxs-lookup"><span data-stu-id="a7189-147">hello connection asset holds hello subscription name, subscriptionId, and certificate asset name.</span></span>

1. <span data-ttu-id="a7189-148">Meld u aan toohello Azure-portal met een account dat lid is van de rol Abonnementsbeheerders hello en medebeheerder van Hallo-abonnement.</span><span class="sxs-lookup"><span data-stu-id="a7189-148">Sign in toohello Azure portal with an account that is a member of hello Subscription Admins role and co-administrator of hello subscription.</span></span>
2. <span data-ttu-id="a7189-149">Selecteer in de blade van Hallo Automation-account, **Run As-Accounts** onder sectie Hallo **Accountinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="a7189-149">From hello Automation account blade, select **Run As Accounts** under hello section **Account Settings**.</span></span>  
3. <span data-ttu-id="a7189-150">Afhankelijk van welk account u nodig hebt, selecteert u **Uitvoeren als-account van Azure**  of **Klassiek Uitvoeren als-account van Azure**.</span><span class="sxs-lookup"><span data-stu-id="a7189-150">Depending on which account you require, select either **Azure Run As Account** or **Azure Classic Run As Account**.</span></span>  <span data-ttu-id="a7189-151">Na het selecteren van beide Hallo **toevoegen Azure uitvoeren als** of **toevoegen Azure Classic Run As-Account** blade wordt weergegeven en bekijk de overzichtsinformatie Hallo op **maken** tooproceed met Run As-account maken.</span><span class="sxs-lookup"><span data-stu-id="a7189-151">After selecting either hello **Add Azure Run As** or **Add Azure Classic Run As Account** blade appears and after reviewing hello overview information, click **Create** tooproceed with Run As account creation.</span></span>  
4. <span data-ttu-id="a7189-152">Terwijl Azure Hallo Run As-account maakt, kunt u de voortgang Hallo onder bijhouden **meldingen** van Hallo menu's en een banner wordt weergegeven waarin staat Hallo-account wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a7189-152">While Azure creates hello Run As account, you can track hello progress under **Notifications** from hello menu and a banner is displayed stating hello account is being created.</span></span>  <span data-ttu-id="a7189-153">Dit kan enkele minuten toocomplete duren.</span><span class="sxs-lookup"><span data-stu-id="a7189-153">This process can take a few minutes toocomplete.</span></span>  

## <a name="create-run-as-account-using-powershell-script"></a><span data-ttu-id="a7189-154">Uitvoeren als-account maken met een PowerShell-script</span><span class="sxs-lookup"><span data-stu-id="a7189-154">Create Run As account using PowerShell script</span></span>
<span data-ttu-id="a7189-155">Deze PowerShell-script biedt ondersteuning voor Hallo volgende configuraties:</span><span class="sxs-lookup"><span data-stu-id="a7189-155">This PowerShell script includes support for hello following configurations:</span></span>

* <span data-ttu-id="a7189-156">Een Uitvoeren als-account maken met een zelfondertekend certificaat.</span><span class="sxs-lookup"><span data-stu-id="a7189-156">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="a7189-157">Een Uitvoeren als-account en een klassiek Uitvoeren als-account maken met een zelfondertekend certificaat.</span><span class="sxs-lookup"><span data-stu-id="a7189-157">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="a7189-158">Een Uitvoeren als-account en een klassiek Uitvoeren als-account maken met een bedrijfscertificaat.</span><span class="sxs-lookup"><span data-stu-id="a7189-158">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="a7189-159">Een Run As-account en een klassieke Run As-account maken met behulp van een zelfondertekend certificaat in hello Azure Government cloud.</span><span class="sxs-lookup"><span data-stu-id="a7189-159">Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud.</span></span>

<span data-ttu-id="a7189-160">Afhankelijk van Hallo configuratieoptie die u selecteert, maakt Hallo script Hallo volgende items.</span><span class="sxs-lookup"><span data-stu-id="a7189-160">Depending on hello configuration option you select, hello script creates hello following items.</span></span>

<span data-ttu-id="a7189-161">**Voor Uitvoeren als-accounts:**</span><span class="sxs-lookup"><span data-stu-id="a7189-161">**For Run As accounts:**</span></span>

* <span data-ttu-id="a7189-162">Hiermee maakt u een Azure AD-toepassing toobe geëxporteerd met een zelf-ondertekend Hallo of openbare sleutel voor de enterprise-certificaat, maakt u een account voor de service-principal voor de toepassing hello in Azure AD en wijst de rol van inzender voor Hallo-account in uw huidige Hallo abonnement.</span><span class="sxs-lookup"><span data-stu-id="a7189-162">Creates an Azure AD application toobe exported with either hello self-signed or enterprise certificate public key, creates a service principal account for hello application in Azure AD, and assigns hello Contributor role for hello account in your current subscription.</span></span> <span data-ttu-id="a7189-163">U kunt deze instelling tooOwner of een andere rol wijzigen.</span><span class="sxs-lookup"><span data-stu-id="a7189-163">You can change this setting tooOwner or any other role.</span></span> <span data-ttu-id="a7189-164">Zie [Op rollen gebaseerd toegangsbeheer in Azure Automation](automation-role-based-access-control.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="a7189-164">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="a7189-165">Hiermee maakt u een Automation-certificaatasset met de naam *AzureRunAsCertificate* in Hallo opgegeven Automation-account.</span><span class="sxs-lookup"><span data-stu-id="a7189-165">Creates an Automation certificate asset named *AzureRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="a7189-166">Hallo-certificaatasset bevat Hallo privésleutel voor certificaten die wordt gebruikt door de toepassing hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a7189-166">hello certificate asset holds hello certificate private key that's used by hello Azure AD application.</span></span>
* <span data-ttu-id="a7189-167">Hiermee maakt u een Automation-verbindingsasset genaamd *AzureRunAsConnection* in Hallo opgegeven Automation-account.</span><span class="sxs-lookup"><span data-stu-id="a7189-167">Creates an Automation connection asset named *AzureRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="a7189-168">Hallo-verbindingsasset bevat Hallo applicationId, tenantId, subscriptionId en de vingerafdruk van certificaat.</span><span class="sxs-lookup"><span data-stu-id="a7189-168">hello connection asset holds hello applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="a7189-169">**Voor klassieke uitvoeren als-accounts:**</span><span class="sxs-lookup"><span data-stu-id="a7189-169">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="a7189-170">Hiermee maakt u een Automation-certificaatasset met de naam *AzureClassicRunAsCertificate* in Hallo opgegeven Automation-account.</span><span class="sxs-lookup"><span data-stu-id="a7189-170">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="a7189-171">Hallo-certificaatasset bevat Hallo privésleutel voor certificaten die door het Hallo-beheercertificaat gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a7189-171">hello certificate asset holds hello certificate private key used by hello management certificate.</span></span>
* <span data-ttu-id="a7189-172">Hiermee maakt u een Automation-verbindingsasset genaamd *AzureClassicRunAsConnection* in Hallo opgegeven Automation-account.</span><span class="sxs-lookup"><span data-stu-id="a7189-172">Creates an Automation connection asset named *AzureClassicRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="a7189-173">Hallo-verbindingsasset bevat Hallo abonnementsnaam, abonnements-id en naam van certificaat asset.</span><span class="sxs-lookup"><span data-stu-id="a7189-173">hello connection asset holds hello subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="a7189-174">Als u de optie voor het maken van een klassieke Run As-account nadat Hallo-script is uitgevoerd is uploaden Hallo openbaar certificaat (.cer bestandsnaamextensie) toohello management opslaan voor Hallo-abonnement dat Hallo Automation-account gemaakt in.</span><span class="sxs-lookup"><span data-stu-id="a7189-174">If you select either option for creating a Classic Run As account, after hello script is executed, upload hello public certificate (.cer file name extension) toohello management store for hello subscription that hello Automation account was created in.</span></span>
> 

1. <span data-ttu-id="a7189-175">Hallo script volgen op uw computer opslaan.</span><span class="sxs-lookup"><span data-stu-id="a7189-175">Save hello following script on your computer.</span></span> <span data-ttu-id="a7189-176">Sla het bestand in dit voorbeeld met Hallo filename *nieuw RunAsAccount.ps1*.</span><span class="sxs-lookup"><span data-stu-id="a7189-176">In this example, save it with hello filename *New-RunAsAccount.ps1*.</span></span>

        #Requires -RunAsAdministrator
        Param (
        [Parameter(Mandatory=$true)]
        [String] $ResourceGroup,

        [Parameter(Mandatory=$true)]
        [String] $AutomationAccountName,

        [Parameter(Mandatory=$true)]
        [String] $ApplicationDisplayName,

        [Parameter(Mandatory=$true)]
        [String] $SubscriptionId,

        [Parameter(Mandatory=$true)]
        [Boolean] $CreateClassicRunAsAccount,

        [Parameter(Mandatory=$true)]
        [String] $SelfSignedCertPlainPassword,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$EnvironmentName="AzureCloud",

        [Parameter(Mandatory=$false)]
        [int] $SelfSignedCertNoOfMonthsUntilExpired = 12
        )

        function CreateSelfSignedCertificate([string] $keyVaultName, [string] $certificateName, [string] $selfSignedCertPlainPassword,
                                       [string] $certPath, [string] $certPathCer, [string] $selfSignedCertNoOfMonthsUntilExpired ) {
        $Cert = New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation cert:\LocalMachine\My `
            -KeyExportPolicy Exportable -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
            -NotAfter (Get-Date).AddMonths($selfSignedCertNoOfMonthsUntilExpired)

        $CertPassword = ConvertTo-SecureString $selfSignedCertPlainPassword -AsPlainText -Force
        Export-PfxCertificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPath -Password $CertPassword -Force | Write-Verbose
        Export-Certificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPathCer -Type CERT | Write-Verbose
        }

        function CreateServicePrincipal([System.Security.Cryptography.X509Certificates.X509Certificate2] $PfxCert, [string] $applicationDisplayName) {  
        $CurrentDate = Get-Date
        $keyValue = [System.Convert]::ToBase64String($PfxCert.GetRawCertData())
        $KeyId = (New-Guid).Guid

        $KeyCredential = New-Object  Microsoft.Azure.Commands.Resources.Models.ActiveDirectory.PSADKeyCredential
        $KeyCredential.StartDate = $CurrentDate
        $KeyCredential.EndDate = Get-Date $PfxCert.GetExpirationDateString()
        $KeyCredential.EndDate = $KeyCredential.EndDate.AddDays(-1)
        $KeyCredential.KeyId = $KeyId
        $KeyCredential.CertValue  = $keyValue

        # Use key credentials and create an Azure AD application
        $Application = New-AzureRmADApplication -DisplayName $ApplicationDisplayName -HomePage ("http://" + $applicationDisplayName) -IdentifierUris ("http://" + $KeyId) -KeyCredentials $KeyCredential
        $ServicePrincipal = New-AzureRMADServicePrincipal -ApplicationId $Application.ApplicationId
        $GetServicePrincipal = Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id

        # Sleep here for a few seconds tooallow hello service principal application toobecome active (ordinarily takes a few seconds)
        Sleep -s 15
        $NewRole = New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
        $Retries = 0;
        While ($NewRole -eq $null -and $Retries -le 6)
        {
            Sleep -s 10
            New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
            $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
            $Retries++;
        }
            return $Application.ApplicationId.ToString();
        }

        function CreateAutomationCertificateAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $certifcateAssetName,[string] $certPath, [string] $certPlainPassword, [Boolean] $Exportable) {
        $CertPassword = ConvertTo-SecureString $certPlainPassword -AsPlainText -Force   
        Remove-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $certifcateAssetName -ErrorAction SilentlyContinue
        New-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Path $certPath -Name $certifcateAssetName -Password $CertPassword -Exportable:$Exportable  | write-verbose
        }

        function CreateAutomationConnectionAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $connectionAssetName, [string] $connectionTypeName, [System.Collections.Hashtable] $connectionFieldValues ) {
        Remove-AzureRmAutomationConnection -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -Force -ErrorAction SilentlyContinue
        New-AzureRmAutomationConnection -ResourceGroupName $ResourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -ConnectionTypeName $connectionTypeName -ConnectionFieldValues $connectionFieldValues
        }

        Import-Module AzureRM.Profile
        Import-Module AzureRM.Resources

        $AzureRMProfileVersion= (Get-Module AzureRM.Profile).Version
        if (!(($AzureRMProfileVersion.Major -ge 3 -and $AzureRMProfileVersion.Minor -ge 0) -or ($AzureRMProfileVersion.Major -gt 3)))
        {
            Write-Error -Message "Please install hello latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
            return
        }

        Login-AzureRmAccount -Environment $EnvironmentName 
        $Subscription = Select-AzureRmSubscription -SubscriptionId $SubscriptionId

        # Create a Run As account by using a service principal
        $CertifcateAssetName = "AzureRunAsCertificate"
        $ConnectionAssetName = "AzureRunAsConnection"
        $ConnectionTypeName = "AzureServicePrincipal"

        if ($EnterpriseCertPathForRunAsAccount -and $EnterpriseCertPlainPasswordForRunAsAccount) {
        $PfxCertPathForRunAsAccount = $EnterpriseCertPathForRunAsAccount
        $PfxCertPlainPasswordForRunAsAccount = $EnterpriseCertPlainPasswordForRunAsAccount
        } else {
           $CertificateName = $AutomationAccountName+$CertifcateAssetName
           $PfxCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".pfx")
           $PfxCertPlainPasswordForRunAsAccount = $SelfSignedCertPlainPassword
           $CerCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".cer")
           CreateSelfSignedCertificate $KeyVaultName $CertificateName $PfxCertPlainPasswordForRunAsAccount $PfxCertPathForRunAsAccount $CerCertPathForRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create a service principal
        $PfxCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($PfxCertPathForRunAsAccount, $PfxCertPlainPasswordForRunAsAccount)
        $ApplicationId=CreateServicePrincipal $PfxCert $ApplicationDisplayName

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $CertifcateAssetName $PfxCertPathForRunAsAccount $PfxCertPlainPasswordForRunAsAccount $true

        # Populate hello ConnectionFieldValues
        $SubscriptionInfo = Get-AzureRmSubscription -SubscriptionId $SubscriptionId
        $TenantID = $SubscriptionInfo | Select TenantId -First 1
        $Thumbprint = $PfxCert.Thumbprint
        $ConnectionFieldValues = @{"ApplicationId" = $ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Thumbprint; "SubscriptionId" = $SubscriptionId}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ConnectionAssetName $ConnectionTypeName $ConnectionFieldValues

        if ($CreateClassicRunAsAccount) {
             # Create a Run As account by using a service principal
             $ClassicRunAsAccountCertifcateAssetName = "AzureClassicRunAsCertificate"
             $ClassicRunAsAccountConnectionAssetName = "AzureClassicRunAsConnection"
             $ClassicRunAsAccountConnectionTypeName = "AzureClassicCertificate "
             $UploadMessage = "Please upload hello .cer format of #CERT# toohello Management store by following hello steps below." + [Environment]::NewLine +
                     "Log in toohello Microsoft Azure Management portal (https://manage.windowsazure.com) and select Settings -> Management Certificates." + [Environment]::NewLine +
                     "Then click Upload and upload hello .cer format of #CERT#"

              if ($EnterpriseCertPathForClassicRunAsAccount -and $EnterpriseCertPlainPasswordForClassicRunAsAccount ) {
              $PfxCertPathForClassicRunAsAccount = $EnterpriseCertPathForClassicRunAsAccount
              $PfxCertPlainPasswordForClassicRunAsAccount = $EnterpriseCertPlainPasswordForClassicRunAsAccount
              $UploadMessage = $UploadMessage.Replace("#CERT#", $PfxCertPathForClassicRunAsAccount)
        } else {
              $ClassicRunAsAccountCertificateName = $AutomationAccountName+$ClassicRunAsAccountCertifcateAssetName
              $PfxCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".pfx")
              $PfxCertPlainPasswordForClassicRunAsAccount = $SelfSignedCertPlainPassword
              $CerCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".cer")
              $UploadMessage = $UploadMessage.Replace("#CERT#", $CerCertPathForClassicRunAsAccount)
              CreateSelfSignedCertificate $KeyVaultName $ClassicRunAsAccountCertificateName $PfxCertPlainPasswordForClassicRunAsAccount $PfxCertPathForClassicRunAsAccount $CerCertPathForClassicRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountCertifcateAssetName $PfxCertPathForClassicRunAsAccount $PfxCertPlainPasswordForClassicRunAsAccount $false

        # Populate hello ConnectionFieldValues
        $SubscriptionName = $subscription.Subscription.Name
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. <span data-ttu-id="a7189-177">Start op uw computer **Windows PowerShell** van Hallo **Start** scherm met verhoogde gebruikersrechten.</span><span class="sxs-lookup"><span data-stu-id="a7189-177">On your computer, start **Windows PowerShell** from hello **Start** screen with elevated user rights.</span></span>
3. <span data-ttu-id="a7189-178">Van Hallo verhoogde opdrachtregel-shell, Ga toohello map die u hebt gemaakt in stap 1 Hallo-script bevat.</span><span class="sxs-lookup"><span data-stu-id="a7189-178">From hello elevated command-line shell, go toohello folder that contains hello script you created in step 1.</span></span>  
4. <span data-ttu-id="a7189-179">Hallo-script uitvoeren met behulp van de parameterwaarden Hallo voor Hallo-configuratie die u nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="a7189-179">Execute hello script by using hello parameter values for hello configuration you require.</span></span>

    <span data-ttu-id="a7189-180">**Een Uitvoeren als-account maken met een zelfondertekend certificaat**</span><span class="sxs-lookup"><span data-stu-id="a7189-180">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="a7189-181">**Een Uitvoeren als-account en een klassiek Uitvoeren als-account maken met een zelfondertekend certificaat**</span><span class="sxs-lookup"><span data-stu-id="a7189-181">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="a7189-182">**Een Uitvoeren als-account en een klassiek Uitvoeren als-account maken met een bedrijfscertificaat**</span><span class="sxs-lookup"><span data-stu-id="a7189-182">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="a7189-183">**Een Run As-account en een klassieke Run As-account maken met behulp van een zelfondertekend certificaat in hello Azure Government cloud**</span><span class="sxs-lookup"><span data-stu-id="a7189-183">**Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="a7189-184">Nadat het Hallo-script is uitgevoerd, kunt u zich na vragen aan gebruiker tooauthenticate met Azure.</span><span class="sxs-lookup"><span data-stu-id="a7189-184">After hello script has executed, you will be prompted tooauthenticate with Azure.</span></span> <span data-ttu-id="a7189-185">Aanmelden met een account dat lid is van Hallo abonnement beheerders rol en medebeheerder van Hallo-abonnement.</span><span class="sxs-lookup"><span data-stu-id="a7189-185">Sign in with an account that is a member of hello subscription administrators role and co-administrator of hello subscription.</span></span>
    >
    >

<span data-ttu-id="a7189-186">Nadat het Hallo-script met succes is uitgevoerd, let u op Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="a7189-186">After hello script has executed successfully, note hello following:</span></span>
* <span data-ttu-id="a7189-187">Als u een klassieke Run As-account hebt gemaakt met een zelf-ondertekend openbaar certificaat (.cer-bestand), Hallo script wordt gemaakt en slaat deze toohello map met tijdelijke bestanden op uw computer onder Hallo gebruikersprofiel *%USERPROFILE%\AppData\Local\Temp*, die u gebruikt tooexecute Hallo PowerShell-sessie.</span><span class="sxs-lookup"><span data-stu-id="a7189-187">If you created a Classic Run As account with a self-signed public certificate (.cer file), hello script creates and saves it toohello temporary files folder on your computer under hello user profile *%USERPROFILE%\AppData\Local\Temp*, which you used tooexecute hello PowerShell session.</span></span>
* <span data-ttu-id="a7189-188">Gebruik dit certificaat als u een klassiek Uitvoeren als-account hebt gemaakt met een openbaar certificaat (.cer-bestand).</span><span class="sxs-lookup"><span data-stu-id="a7189-188">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="a7189-189">Hallo-instructies voor [een beheer-API certificaat toohello klassieke Azure-portal uploaden](../azure-api-management-certs.md), en vervolgens Hallo verwijzingsconfiguratie met resources van klassieke implementatie te valideren met behulp van Hallo [voorbeeldcode tooauthenticate met Azure Classic Deployment Resources](automation-verify-runas-authentication.md#classic-run-as-authentication).</span><span class="sxs-lookup"><span data-stu-id="a7189-189">Follow hello instructions for [uploading a management API certificate toohello Azure classic portal](../azure-api-management-certs.md), and then validate hello credential configuration with classic deployment resources by using hello [sample code tooauthenticate with Azure Classic Deployment Resources](automation-verify-runas-authentication.md#classic-run-as-authentication).</span></span> 
* <span data-ttu-id="a7189-190">Als u dit hebt gedaan *niet* klassieke Run As-account maken en verifiëren met Resource Manager-resources Hallo verwijzingsconfiguratie valideren met behulp van Hallo [voorbeeldcode voor verificatie met Service Management resources](automation-verify-runas-authentication.md#automation-run-as-authentication).</span><span class="sxs-lookup"><span data-stu-id="a7189-190">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate hello credential configuration by using hello [sample code for authenticating with Service Management resources](automation-verify-runas-authentication.md#automation-run-as-authentication).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a7189-191">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a7189-191">Next steps</span></span>
* <span data-ttu-id="a7189-192">Voor meer informatie over Service-Principals te verwijzen[toepassingsobjecten en Service-Principal objecten](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="a7189-192">For more information about Service Principals, refer too[Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="a7189-193">Voor meer informatie over certificaten en Azure-services te verwijzen[certificaten voor Azure Cloud Services-overzicht](../cloud-services/cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="a7189-193">For more information about certificates and Azure services, refer too[Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>
