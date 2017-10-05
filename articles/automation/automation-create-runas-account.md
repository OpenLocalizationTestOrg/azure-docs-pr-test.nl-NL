---
title: Azure Automation Uitvoeren als-accounts maken | Microsoft Docs
description: In dit artikel wordt beschreven hoe u uw Automation-account bijwerkt en Uitvoeren als-accounts maakt met PowerShell of vanuit de portal.
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
ms.openlocfilehash: eaf6eb49bbfe4572827fcc101d1f552b48ab91e6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="update-your-automation-account-authentication-with-run-as-accounts"></a><span data-ttu-id="38a81-103">Uw Automation-account bijwerken met Uitvoeren als-accounts</span><span class="sxs-lookup"><span data-stu-id="38a81-103">Update your Automation account authentication with Run As accounts</span></span> 
<span data-ttu-id="38a81-104">In de volgende gevallen kunt u een bestaand Automation-account bijwerken vanuit de portal of met PowerShell:</span><span class="sxs-lookup"><span data-stu-id="38a81-104">You can update your existing Automation account from the portal or use PowerShell if:</span></span>

* <span data-ttu-id="38a81-105">U maakt wel een Automation-account, maar geen Uitvoeren als-account.</span><span class="sxs-lookup"><span data-stu-id="38a81-105">You create an Automation account but decline to create the Run As account.</span></span>
* <span data-ttu-id="38a81-106">U gebruikt al een Automation-account voor het beheer van Resource Manager-resources en u wilt het account bijwerken met het Uitvoeren als-account voor runbookverificatie.</span><span class="sxs-lookup"><span data-stu-id="38a81-106">You already use an Automation account to manage Resource Manager resources and you want to update the account to include the Run As account for runbook authentication.</span></span>
* <span data-ttu-id="38a81-107">U gebruikt al een Automation-account voor het beheer van klassieke resources en u wilt dit bijwerken, zodat u het klassieke Uitvoeren als-account kunt gebruiken in plaats van een nieuw account te maken, en uw runbooks en activa daarnaartoe te migreren.</span><span class="sxs-lookup"><span data-stu-id="38a81-107">You already use an Automation account to manage classic resources and you want to update it to use the Classic Run As account instead of creating a new account and migrating your runbooks and assets to it.</span></span>   
* <span data-ttu-id="38a81-108">U wilt een Uitvoeren als-account maken en een klassiek Uitvoeren als-account via een certificaat dat is uitgegeven door de certificeringsinstantie van uw bedrijf.</span><span class="sxs-lookup"><span data-stu-id="38a81-108">You want to create a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="38a81-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="38a81-109">Prerequisites</span></span>

* <span data-ttu-id="38a81-110">Het script kan alleen worden uitgevoerd in Windows 10 en Windows Server 2016 met Azure Resource Manager-modules 3.0.0 en hoger.</span><span class="sxs-lookup"><span data-stu-id="38a81-110">The script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 3.0.0 and later.</span></span> <span data-ttu-id="38a81-111">Uitvoeren wordt niet ondersteund in eerdere versies van Windows.</span><span class="sxs-lookup"><span data-stu-id="38a81-111">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="38a81-112">Azure PowerShell 1.0 en hoger.</span><span class="sxs-lookup"><span data-stu-id="38a81-112">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="38a81-113">Zie [Azure PowerShell installeren en configureren](/powershell/azureps-cmdlets-docs) voor meer informatie over de PowerShell 1.0-release.</span><span class="sxs-lookup"><span data-stu-id="38a81-113">For information about the PowerShell 1.0 release, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>
* <span data-ttu-id="38a81-114">Een Automation-account waarnaar wordt verwezen als de waarde voor de parameter *– AutomationAccountName* en *- ApplicationDisplayName* in het volgende PowerShell-script.</span><span class="sxs-lookup"><span data-stu-id="38a81-114">An Automation account, which is referenced as the value for the *–AutomationAccountName* and *-ApplicationDisplayName* parameters in the following PowerShell script.</span></span>

<span data-ttu-id="38a81-115">Ga als volgt te werk om de waarden op te halen voor *SubscriptionID*, *ResourceGroup* en *AutomationAccountName*; dit zijn vereiste parameters voor de scripts:</span><span class="sxs-lookup"><span data-stu-id="38a81-115">To get the values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for the script, do the following:</span></span>

1. <span data-ttu-id="38a81-116">Selecteer in Azure Portal uw Automation-account op de blade **Automation-account** en selecteer **Alle instellingen**.</span><span class="sxs-lookup"><span data-stu-id="38a81-116">In the Azure portal, select your Automation account on the **Automation account** blade, and then select **All settings**.</span></span>  
2. <span data-ttu-id="38a81-117">Selecteer op de blade **Alle instellingen** onder **Accountinstellingen** de optie **Eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="38a81-117">On the **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="38a81-118">Let op de waarden op de blade **Eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="38a81-118">Note the values on the **Properties** blade.</span></span><br><br> <span data-ttu-id="38a81-119">![De blade Eigenschappen voor het Automation-account](media/automation-create-runas-account/automation-account-properties.png)</span><span class="sxs-lookup"><span data-stu-id="38a81-119">![The Automation account "Properties" blade](media/automation-create-runas-account/automation-account-properties.png)</span></span>  

### <a name="required-permissions-to-update-your-automation-account"></a><span data-ttu-id="38a81-120">Machtigingen die zijn vereist om een Automation-account bij te werken</span><span class="sxs-lookup"><span data-stu-id="38a81-120">Required permissions to update your Automation account</span></span>
<span data-ttu-id="38a81-121">Als u een Automation-account wilt bijwerken, moet u de volgende specifieke machtigingen en bevoegdheden hebben om dit onderwerp te voltooien.</span><span class="sxs-lookup"><span data-stu-id="38a81-121">To update an Automation account, you must have the following specific privileges and permissions required to complete this topic.</span></span>   
 
* <span data-ttu-id="38a81-122">Uw AD-gebruikersaccount moet worden toegevoegd aan een rol die machtigingen heeft die equivalent zijn aan de rol Inzender voor Microsoft.Automation-resources. Dit is beschreven in het artikel [Op rollen gebaseerd toegangsbeheer in Azure Automation](automation-role-based-access-control.md#contributor-role-permissions).</span><span class="sxs-lookup"><span data-stu-id="38a81-122">Your AD user account needs to be added to a role with permissions equivalent to the Contributor role for Microsoft.Automation resources as outlined in article [Role-based access control in Azure Automation](automation-role-based-access-control.md#contributor-role-permissions).</span></span>  
* <span data-ttu-id="38a81-123">Gebruikers zonder beheerdersrechten in uw Azure AD-tenant kunnen [AD-toepassingen registreren](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions) als de instelling App-registraties is ingesteld op **Ja**.</span><span class="sxs-lookup"><span data-stu-id="38a81-123">Non-admin users in your Azure AD tenant can [register AD applications](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions) if the App registrations setting is set to **Yes**.</span></span>  <span data-ttu-id="38a81-124">Als de app-registratie-instelling is ingesteld op **Nee**, moet de gebruiker die deze actie uitvoert een globale beheerder zijn in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="38a81-124">If the app registrations setting is set to **No**, the user performing this action must be a global administrator in Azure AD.</span></span> 

<span data-ttu-id="38a81-125">Als u geen lid bent van het Active Directory-exemplaar van het abonnement voordat u wordt toegevoegd aan de rol van globale beheerder/medebeheerder van het abonnement, wordt u als gast toegevoegd aan Active Directory.</span><span class="sxs-lookup"><span data-stu-id="38a81-125">If you are not a member of the subscription’s Active Directory instance before you are added to the global administrator/co-administrator role of the subscription, you are added to Active Directory as a guest.</span></span> <span data-ttu-id="38a81-126">In dat geval wordt de waarschuwing 'U bent niet gemachtigd om…'</span><span class="sxs-lookup"><span data-stu-id="38a81-126">In this situation, you receive a “You do not have permissions to create…”</span></span> <span data-ttu-id="38a81-127">weergegeven op de blade **Automation-account toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="38a81-127">warning on the **Add Automation Account** blade.</span></span> <span data-ttu-id="38a81-128">Gebruikers die zijn toegevoegd aan de rol van globale beheerder/medebeheerder, kunnen worden verwijderd uit het Active Directory-exemplaar van het abonnement en opnieuw worden toegevoegd, zodat ze een volledige gebruiker worden in Active Directory.</span><span class="sxs-lookup"><span data-stu-id="38a81-128">Users who were added to the global administrator/co-administrator role first can be removed from the subscription's Active Directory instance and re-added to make them a full User in Active Directory.</span></span> <span data-ttu-id="38a81-129">U kunt deze situatie controleren door in het deelvenster **Azure Active Directory** van Azure Portal **Gebruikers en groepen** te selecteren. Selecteer vervolgens **Alle gebruikers**, de specifieke gebruiker en **Profiel**.</span><span class="sxs-lookup"><span data-stu-id="38a81-129">To verify this situation, from the **Azure Active Directory** pane in the Azure portal, select **Users and groups**, select **All users** and, after you select the specific user, select **Profile**.</span></span> <span data-ttu-id="38a81-130">De waarde van het kenmerk **Gebruikerstype** onder het gebruikersprofiel mag niet gelijk zijn aan **Gast**.</span><span class="sxs-lookup"><span data-stu-id="38a81-130">The value of the **User type** attribute under the users profile should not equal **Guest**.</span></span>

## <a name="create-run-as-account-from-the-portal"></a><span data-ttu-id="38a81-131">Uitvoeren als-account maken vanuit de portal</span><span class="sxs-lookup"><span data-stu-id="38a81-131">Create Run As account from the portal</span></span>
<span data-ttu-id="38a81-132">In deze sectie voert u de volgende stappen uit om een Azure Automation-account bij te werken vanuit Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="38a81-132">In this section, perform the following steps to update your Azure Automation account from  the Azure portal.</span></span>  <span data-ttu-id="38a81-133">U maakt de Uitvoeren als- en klassieke Uitvoeren als-accounts afzonderlijk, en als u geen resources in de klassieke Azure-portal hoeft te beheren, hoeft u alleen een Azure Uitvoeren als-account te maken.</span><span class="sxs-lookup"><span data-stu-id="38a81-133">You create the Run As and Classic Run As accounts individually, and if you don't need to manage resources in the classic Azure portal, you can just create the Azure Run As account.</span></span>  

<span data-ttu-id="38a81-134">Tijdens dit proces worden de volgende items in uw Automation-account gemaakt.</span><span class="sxs-lookup"><span data-stu-id="38a81-134">The process creates the following items in your Automation account.</span></span>

<span data-ttu-id="38a81-135">**Voor Uitvoeren als-accounts:**</span><span class="sxs-lookup"><span data-stu-id="38a81-135">**For Run As accounts:**</span></span>

* <span data-ttu-id="38a81-136">Er wordt een Azure AD-toepassing met een zelf-ondertekend certificaat gemaakt. Daarnaast wordt er voor de toepassing in Azure AD een service-principalaccount gemaakt en wordt aan dit account de rol Inzender toegewezen in uw huidige abonnement.</span><span class="sxs-lookup"><span data-stu-id="38a81-136">Creates an Azure AD application with a self-signed certificate, creates a service principal account for the application in Azure AD, and assigns the Contributor role for the account in your current subscription.</span></span> <span data-ttu-id="38a81-137">U kunt deze instelling wijzigen in Eigenaar of een andere rol.</span><span class="sxs-lookup"><span data-stu-id="38a81-137">You can change this setting to Owner or any other role.</span></span> <span data-ttu-id="38a81-138">Zie [Op rollen gebaseerd toegangsbeheer in Azure Automation](automation-role-based-access-control.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="38a81-138">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="38a81-139">Er wordt een Automation-certificaatasset gemaakt met de naam *AzureRunAsCertificate* in het opgegeven Automation-account.</span><span class="sxs-lookup"><span data-stu-id="38a81-139">Creates an Automation certificate asset named *AzureRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="38a81-140">Het certificaatasset bevat de persoonlijke sleutel van het certificaat die wordt gebruikt door de Azure AD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="38a81-140">The certificate asset holds the certificate private key that's used by the Azure AD application.</span></span>
* <span data-ttu-id="38a81-141">Er wordt een Automation-verbindingsasset gemaakt met de naam *AzureRunAsConnection* in het opgegeven Automation-account.</span><span class="sxs-lookup"><span data-stu-id="38a81-141">Creates an Automation connection asset named *AzureRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="38a81-142">Het verbindingsasset bevat de toepassing-id, tenant-id, abonnement-id en certificaatvingerafdruk.</span><span class="sxs-lookup"><span data-stu-id="38a81-142">The connection asset holds the applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="38a81-143">**Voor klassieke uitvoeren als-accounts:**</span><span class="sxs-lookup"><span data-stu-id="38a81-143">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="38a81-144">Er wordt een Automation-certificaatasset gemaakt met de naam *AzureClassicRunAsCertificate* in het opgegeven Automation-account.</span><span class="sxs-lookup"><span data-stu-id="38a81-144">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="38a81-145">Het certificaatasset bevat de persoonlijke sleutel van het certificaat die wordt gebruikt door het beheercertificaat.</span><span class="sxs-lookup"><span data-stu-id="38a81-145">The certificate asset holds the certificate private key used by the management certificate.</span></span>
* <span data-ttu-id="38a81-146">Er wordt een Automation-verbindingsasset gemaakt met de naam *AzureClassicRunAsConnection* in het opgegeven Automation-account.</span><span class="sxs-lookup"><span data-stu-id="38a81-146">Creates an Automation connection asset named *AzureClassicRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="38a81-147">Het verbindingsasset bevat de naam van het abonnement, de abonnements-id en de certificaatassetnaam.</span><span class="sxs-lookup"><span data-stu-id="38a81-147">The connection asset holds the subscription name, subscriptionId, and certificate asset name.</span></span>

1. <span data-ttu-id="38a81-148">Meld u aan bij Azure Portal met een account dat lid is van de rol Abonnementsbeheerders en dat medebeheerder is van het abonnement.</span><span class="sxs-lookup"><span data-stu-id="38a81-148">Sign in to the Azure portal with an account that is a member of the Subscription Admins role and co-administrator of the subscription.</span></span>
2. <span data-ttu-id="38a81-149">Selecteer op de blade Automation-account de optie **Uitvoeren als-accounts** in de sectie **Accountinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="38a81-149">From the Automation account blade, select **Run As Accounts** under the section **Account Settings**.</span></span>  
3. <span data-ttu-id="38a81-150">Afhankelijk van welk account u nodig hebt, selecteert u **Uitvoeren als-account van Azure**  of **Klassiek Uitvoeren als-account van Azure**.</span><span class="sxs-lookup"><span data-stu-id="38a81-150">Depending on which account you require, select either **Azure Run As Account** or **Azure Classic Run As Account**.</span></span>  <span data-ttu-id="38a81-151">Na deze selectie wordt de blade **Uitvoeren als-account toevoegen** of **Klassiek Uitvoeren als-account toevoegen** weergegeven. Controleer de overzichtsgegevens en klik op **Maken** om verder te gaan met het maken van een Uitvoeren als-account.</span><span class="sxs-lookup"><span data-stu-id="38a81-151">After selecting either the **Add Azure Run As** or **Add Azure Classic Run As Account** blade appears and after reviewing the overview information, click **Create** to proceed with Run As account creation.</span></span>  
4. <span data-ttu-id="38a81-152">Terwijl Azure het Uitvoeren als-account maakt, kunt u de voortgang volgen onder **Meldingen** in het menu en een banner waarin wordt vermeld dat het account wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="38a81-152">While Azure creates the Run As account, you can track the progress under **Notifications** from the menu and a banner is displayed stating the account is being created.</span></span>  <span data-ttu-id="38a81-153">Dit proces kan enkele minuten duren.</span><span class="sxs-lookup"><span data-stu-id="38a81-153">This process can take a few minutes to complete.</span></span>  

## <a name="create-run-as-account-using-powershell-script"></a><span data-ttu-id="38a81-154">Uitvoeren als-account maken met een PowerShell-script</span><span class="sxs-lookup"><span data-stu-id="38a81-154">Create Run As account using PowerShell script</span></span>
<span data-ttu-id="38a81-155">Dit PowerShell-script biedt ondersteuning voor de volgende configuraties:</span><span class="sxs-lookup"><span data-stu-id="38a81-155">This PowerShell script includes support for the following configurations:</span></span>

* <span data-ttu-id="38a81-156">Een Uitvoeren als-account maken met een zelfondertekend certificaat.</span><span class="sxs-lookup"><span data-stu-id="38a81-156">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="38a81-157">Een Uitvoeren als-account en een klassiek Uitvoeren als-account maken met een zelfondertekend certificaat.</span><span class="sxs-lookup"><span data-stu-id="38a81-157">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="38a81-158">Een Uitvoeren als-account en een klassiek Uitvoeren als-account maken met een bedrijfscertificaat.</span><span class="sxs-lookup"><span data-stu-id="38a81-158">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="38a81-159">Een Uitvoeren als-account en een klassiek Uitvoeren als-account maken met een zelfondertekend certificaat in de cloud van Azure Government.</span><span class="sxs-lookup"><span data-stu-id="38a81-159">Create a Run As account and a Classic Run As account by using a self-signed certificate in the Azure Government cloud.</span></span>

<span data-ttu-id="38a81-160">Afhankelijk van de configuratieoptie die u selecteert, maakt het script de volgende items.</span><span class="sxs-lookup"><span data-stu-id="38a81-160">Depending on the configuration option you select, the script creates the following items.</span></span>

<span data-ttu-id="38a81-161">**Voor Uitvoeren als-accounts:**</span><span class="sxs-lookup"><span data-stu-id="38a81-161">**For Run As accounts:**</span></span>

* <span data-ttu-id="38a81-162">Er wordt een Azure AD-toepassing gemaakt die wordt geëxporteerd met het zelfondertekende certificaat of de openbare sleutel van het bedrijfscertificaat en een service-principalaccount voor deze toepassing in Azure AD. Daarnaast wordt voor dit account de rol Inzender toegewezen in uw huidige abonnement.</span><span class="sxs-lookup"><span data-stu-id="38a81-162">Creates an Azure AD application to be exported with either the self-signed or enterprise certificate public key, creates a service principal account for the application in Azure AD, and assigns the Contributor role for the account in your current subscription.</span></span> <span data-ttu-id="38a81-163">U kunt deze instelling wijzigen in Eigenaar of een andere rol.</span><span class="sxs-lookup"><span data-stu-id="38a81-163">You can change this setting to Owner or any other role.</span></span> <span data-ttu-id="38a81-164">Zie [Op rollen gebaseerd toegangsbeheer in Azure Automation](automation-role-based-access-control.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="38a81-164">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="38a81-165">Er wordt een Automation-certificaatasset gemaakt met de naam *AzureRunAsCertificate* in het opgegeven Automation-account.</span><span class="sxs-lookup"><span data-stu-id="38a81-165">Creates an Automation certificate asset named *AzureRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="38a81-166">Het certificaatasset bevat de persoonlijke sleutel van het certificaat die wordt gebruikt door de Azure AD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="38a81-166">The certificate asset holds the certificate private key that's used by the Azure AD application.</span></span>
* <span data-ttu-id="38a81-167">Er wordt een Automation-verbindingsasset gemaakt met de naam *AzureRunAsConnection* in het opgegeven Automation-account.</span><span class="sxs-lookup"><span data-stu-id="38a81-167">Creates an Automation connection asset named *AzureRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="38a81-168">Het verbindingsasset bevat de toepassing-id, tenant-id, abonnement-id en certificaatvingerafdruk.</span><span class="sxs-lookup"><span data-stu-id="38a81-168">The connection asset holds the applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="38a81-169">**Voor klassieke uitvoeren als-accounts:**</span><span class="sxs-lookup"><span data-stu-id="38a81-169">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="38a81-170">Er wordt een Automation-certificaatasset gemaakt met de naam *AzureClassicRunAsCertificate* in het opgegeven Automation-account.</span><span class="sxs-lookup"><span data-stu-id="38a81-170">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="38a81-171">Het certificaatasset bevat de persoonlijke sleutel van het certificaat die wordt gebruikt door het beheercertificaat.</span><span class="sxs-lookup"><span data-stu-id="38a81-171">The certificate asset holds the certificate private key used by the management certificate.</span></span>
* <span data-ttu-id="38a81-172">Er wordt een Automation-verbindingsasset gemaakt met de naam *AzureClassicRunAsConnection* in het opgegeven Automation-account.</span><span class="sxs-lookup"><span data-stu-id="38a81-172">Creates an Automation connection asset named *AzureClassicRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="38a81-173">Het verbindingsasset bevat de naam van het abonnement, de abonnements-id en de certificaatassetnaam.</span><span class="sxs-lookup"><span data-stu-id="38a81-173">The connection asset holds the subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="38a81-174">Als u ervoor kiest om een klassiek Uitvoeren als-account te maken, moet u na het uitvoeren van het script het openbare certificaat (bestandsnaamextensie .cer) uploaden naar het beheerarchief voor het abonnement waarin het Automation-account is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="38a81-174">If you select either option for creating a Classic Run As account, after the script is executed, upload the public certificate (.cer file name extension) to the management store for the subscription that the Automation account was created in.</span></span>
> 

1. <span data-ttu-id="38a81-175">Sla het volgende script op uw computer op.</span><span class="sxs-lookup"><span data-stu-id="38a81-175">Save the following script on your computer.</span></span> <span data-ttu-id="38a81-176">Sla het bestand in dit voorbeeld op met de bestandsnaam *New-RunAsAccount.ps1*.</span><span class="sxs-lookup"><span data-stu-id="38a81-176">In this example, save it with the filename *New-RunAsAccount.ps1*.</span></span>

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

        # Sleep here for a few seconds to allow the service principal application to become active (ordinarily takes a few seconds)
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
            Write-Error -Message "Please install the latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
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

        # Create the Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $CertifcateAssetName $PfxCertPathForRunAsAccount $PfxCertPlainPasswordForRunAsAccount $true

        # Populate the ConnectionFieldValues
        $SubscriptionInfo = Get-AzureRmSubscription -SubscriptionId $SubscriptionId
        $TenantID = $SubscriptionInfo | Select TenantId -First 1
        $Thumbprint = $PfxCert.Thumbprint
        $ConnectionFieldValues = @{"ApplicationId" = $ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Thumbprint; "SubscriptionId" = $SubscriptionId}

        # Create an Automation connection asset named AzureRunAsConnection in the Automation account. This connection uses the service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ConnectionAssetName $ConnectionTypeName $ConnectionFieldValues

        if ($CreateClassicRunAsAccount) {
             # Create a Run As account by using a service principal
             $ClassicRunAsAccountCertifcateAssetName = "AzureClassicRunAsCertificate"
             $ClassicRunAsAccountConnectionAssetName = "AzureClassicRunAsConnection"
             $ClassicRunAsAccountConnectionTypeName = "AzureClassicCertificate "
             $UploadMessage = "Please upload the .cer format of #CERT# to the Management store by following the steps below." + [Environment]::NewLine +
                     "Log in to the Microsoft Azure Management portal (https://manage.windowsazure.com) and select Settings -> Management Certificates." + [Environment]::NewLine +
                     "Then click Upload and upload the .cer format of #CERT#"

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

        # Create the Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountCertifcateAssetName $PfxCertPathForClassicRunAsAccount $PfxCertPlainPasswordForClassicRunAsAccount $false

        # Populate the ConnectionFieldValues
        $SubscriptionName = $subscription.Subscription.Name
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in the Automation account. This connection uses the service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. <span data-ttu-id="38a81-177">Start op uw computer **Windows PowerShell** op vanaf het **Start**scherm met verhoogde gebruikersrechten.</span><span class="sxs-lookup"><span data-stu-id="38a81-177">On your computer, start **Windows PowerShell** from the **Start** screen with elevated user rights.</span></span>
3. <span data-ttu-id="38a81-178">Ga vanuit de opdrachtregel-shell met verhoogde bevoegdheden naar de map die het script bevat dat u in stap 1 hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="38a81-178">From the elevated command-line shell, go to the folder that contains the script you created in step 1.</span></span>  
4. <span data-ttu-id="38a81-179">Voer het script uit met de parameterwaarden voor de configuratie die u nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="38a81-179">Execute the script by using the parameter values for the configuration you require.</span></span>

    <span data-ttu-id="38a81-180">**Een Uitvoeren als-account maken met een zelfondertekend certificaat**</span><span class="sxs-lookup"><span data-stu-id="38a81-180">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="38a81-181">**Een Uitvoeren als-account en een klassiek Uitvoeren als-account maken met een zelfondertekend certificaat**</span><span class="sxs-lookup"><span data-stu-id="38a81-181">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="38a81-182">**Een Uitvoeren als-account en een klassiek Uitvoeren als-account maken met een bedrijfscertificaat**</span><span class="sxs-lookup"><span data-stu-id="38a81-182">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="38a81-183">**Een Uitvoeren als-account en een klassiek Uitvoeren als-account maken met een zelfondertekend certificaat in de cloud van Azure Government**</span><span class="sxs-lookup"><span data-stu-id="38a81-183">**Create a Run As account and a Classic Run As account by using a self-signed certificate in the Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="38a81-184">Nadat het script is uitgevoerd, wordt u gevraagd zich te verifiëren met Azure.</span><span class="sxs-lookup"><span data-stu-id="38a81-184">After the script has executed, you will be prompted to authenticate with Azure.</span></span> <span data-ttu-id="38a81-185">Meld u aan met een account dat lid is van de rol Abonnementsbeheerders en dat medebeheerder is van het abonnement.</span><span class="sxs-lookup"><span data-stu-id="38a81-185">Sign in with an account that is a member of the subscription administrators role and co-administrator of the subscription.</span></span>
    >
    >

<span data-ttu-id="38a81-186">Let op het volgende nadat het script is uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="38a81-186">After the script has executed successfully, note the following:</span></span>
* <span data-ttu-id="38a81-187">Als u een klassiek Uitvoeren als-account hebt gemaakt met een zelfondertekend openbaar certificaat (.cer-bestand), wordt het door het script gemaakt en opgeslagen in de map met tijdelijke bestanden op uw computer, onder het gebruikersprofiel *%USERPROFILE%\AppData\Local\Temp*, dat u hebt gebruikt voor het uitvoeren van de PowerShell-sessie.</span><span class="sxs-lookup"><span data-stu-id="38a81-187">If you created a Classic Run As account with a self-signed public certificate (.cer file), the script creates and saves it to the temporary files folder on your computer under the user profile *%USERPROFILE%\AppData\Local\Temp*, which you used to execute the PowerShell session.</span></span>
* <span data-ttu-id="38a81-188">Gebruik dit certificaat als u een klassiek Uitvoeren als-account hebt gemaakt met een openbaar certificaat (.cer-bestand).</span><span class="sxs-lookup"><span data-stu-id="38a81-188">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="38a81-189">Volg de instructies voor het [uploaden van een API-beheercertificaat naar de klassieke Azure-portal](../azure-api-management-certs.md) en valideer de configuratie van de referenties met klassieke implementatieresources met behulp van de [Voorbeeldcode voor verificatie bij Resource Manager-resources](automation-verify-runas-authentication.md#classic-run-as-authentication).</span><span class="sxs-lookup"><span data-stu-id="38a81-189">Follow the instructions for [uploading a management API certificate to the Azure classic portal](../azure-api-management-certs.md), and then validate the credential configuration with classic deployment resources by using the [sample code to authenticate with Azure Classic Deployment Resources](automation-verify-runas-authentication.md#classic-run-as-authentication).</span></span> 
* <span data-ttu-id="38a81-190">Als u *geen* klassiek Uitvoeren als-account hebt gemaakt, verifieert u met Resource Manager-resources en valideert u de configuratie van de referenties met behulp van de [voorbeeldcode om verificatie met Service Management-resources uit te voeren](automation-verify-runas-authentication.md#automation-run-as-authentication).</span><span class="sxs-lookup"><span data-stu-id="38a81-190">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate the credential configuration by using the [sample code for authenticating with Service Management resources](automation-verify-runas-authentication.md#automation-run-as-authentication).</span></span>

## <a name="next-steps"></a><span data-ttu-id="38a81-191">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="38a81-191">Next steps</span></span>
* <span data-ttu-id="38a81-192">Zie [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md) (Toepassingsobjecten en service-principalobjecten) voor meer informatie over service-principals.</span><span class="sxs-lookup"><span data-stu-id="38a81-192">For more information about Service Principals, refer to [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="38a81-193">Voor meer informatie over certificaten en Azure-services raadpleegt u [Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md) (Overzicht van certificaten voor Azure Cloud Services).</span><span class="sxs-lookup"><span data-stu-id="38a81-193">For more information about certificates and Azure services, refer to [Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>