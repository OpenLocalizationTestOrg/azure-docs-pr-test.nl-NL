---
title: aaaCreate Automation Azure die Run As-account met PowerShell | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooupgrade uw Automation-account met PowerShell toocreate Hallo Run As-accounts als u deze stap geen hebben uitgevoerd tijdens het maken van de eerste van Hallo-portal.
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
ms.date: 04/14/2017
ms.author: magoedte
ms.openlocfilehash: 1049601321d2bc1e5f9d982f622788f8e4e4d797
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="update-automation-run-as-account-using-powershell"></a><span data-ttu-id="25fc9-103">Automation Uitvoeren als-account bijwerken met PowerShell</span><span class="sxs-lookup"><span data-stu-id="25fc9-103">Update Automation Run As account using PowerShell</span></span>
<span data-ttu-id="25fc9-104">U kunt PowerShell tooupdate uw bestaande Automation-account gebruiken als:</span><span class="sxs-lookup"><span data-stu-id="25fc9-104">You can use PowerShell tooupdate your existing Automation account if:</span></span>

* <span data-ttu-id="25fc9-105">U maakt een Automation-account maar weigeren toocreate Hallo Run As-account.</span><span class="sxs-lookup"><span data-stu-id="25fc9-105">You create an Automation account but decline toocreate hello Run As account.</span></span>
* <span data-ttu-id="25fc9-106">U al een Automation-account toomanage Resource Manager-resources gebruikt en gewenste tooupdate Hallo account tooinclude Hallo Run As-account voor de runbook-verificatie.</span><span class="sxs-lookup"><span data-stu-id="25fc9-106">You already use an Automation account toomanage Resource Manager resources and you want tooupdate hello account tooinclude hello Run As account for runbook authentication.</span></span>
* <span data-ttu-id="25fc9-107">U al een Automation-account toomanage klassieke resources gebruikt en u wilt tooupdate het toouse Hallo klassieke Run As-account in plaats van een nieuw account maken en uw runbooks en activa tooit migreren.</span><span class="sxs-lookup"><span data-stu-id="25fc9-107">You already use an Automation account toomanage classic resources and you want tooupdate it toouse hello Classic Run As account instead of creating a new account and migrating your runbooks and assets tooit.</span></span>   
* <span data-ttu-id="25fc9-108">Toocreate wilt u een Run As- en klassieke Run As-account met behulp van een certificaat zijn uitgegeven door uw enterprise-certificeringsinstantie (CA).</span><span class="sxs-lookup"><span data-stu-id="25fc9-108">You want toocreate a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="25fc9-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="25fc9-109">Prerequisites</span></span>

* <span data-ttu-id="25fc9-110">Hallo-script kan alleen op Windows 10 en Windows Server 2016 met Azure Resource Manager-modules 2.01 en hoger worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="25fc9-110">hello script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 2.01 and later.</span></span> <span data-ttu-id="25fc9-111">Uitvoeren wordt niet ondersteund in eerdere versies van Windows.</span><span class="sxs-lookup"><span data-stu-id="25fc9-111">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="25fc9-112">Azure PowerShell 1.0 en hoger.</span><span class="sxs-lookup"><span data-stu-id="25fc9-112">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="25fc9-113">Zie voor meer informatie over Hallo PowerShell 1.0 release [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="25fc9-113">For information about hello PowerShell 1.0 release, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="25fc9-114">Een Automation-account waarnaar wordt verwezen als waarde voor Hallo Hallo *-AutomationAccountName* en *- ApplicationDisplayName* parameters in de volgende PowerShell-script Hallo.</span><span class="sxs-lookup"><span data-stu-id="25fc9-114">An Automation account, which is referenced as hello value for hello *–AutomationAccountName* and *-ApplicationDisplayName* parameters in hello following PowerShell script.</span></span>

<span data-ttu-id="25fc9-115">Hallo tooget waarden voor *SubscriptionID*, *ResourceGroup*, en *AutomationAccountName*, die de vereiste parameters voor Hallo scripts zijn, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="25fc9-115">tooget hello values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for hello scripts, do hello following:</span></span>
1. <span data-ttu-id="25fc9-116">In Hallo Azure-portal, selecteert u uw Automation-account op Hallo **Automation-account** blade en selecteer vervolgens **alle instellingen**.</span><span class="sxs-lookup"><span data-stu-id="25fc9-116">In hello Azure portal, select your Automation account on hello **Automation account** blade, and then select **All settings**.</span></span> 
2. <span data-ttu-id="25fc9-117">Op Hallo **alle instellingen** blade onder **Accountinstellingen**, selecteer **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="25fc9-117">On hello **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="25fc9-118">Houd er rekening mee Hallo waarden op Hallo **eigenschappen** blade.</span><span class="sxs-lookup"><span data-stu-id="25fc9-118">Note hello values on hello **Properties** blade.</span></span>

![blade 'Eigenschappen' Hello Automation-account](media/automation-sec-configure-azure-runas-account/automation-account-properties.png)  

## <a name="create-run-as-account-powershell-script"></a><span data-ttu-id="25fc9-120">PowerShell-script voor Uitvoeren als-account maken</span><span class="sxs-lookup"><span data-stu-id="25fc9-120">Create Run As Account PowerShell script</span></span>
<span data-ttu-id="25fc9-121">Deze PowerShell-script biedt ondersteuning voor Hallo volgende configuraties:</span><span class="sxs-lookup"><span data-stu-id="25fc9-121">This PowerShell script includes support for hello following configurations:</span></span>

* <span data-ttu-id="25fc9-122">Een Uitvoeren als-account maken met een zelfondertekend certificaat.</span><span class="sxs-lookup"><span data-stu-id="25fc9-122">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="25fc9-123">Een Uitvoeren als-account en een klassiek Uitvoeren als-account maken met een zelfondertekend certificaat.</span><span class="sxs-lookup"><span data-stu-id="25fc9-123">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="25fc9-124">Een Uitvoeren als-account en een klassiek Uitvoeren als-account maken met een bedrijfscertificaat.</span><span class="sxs-lookup"><span data-stu-id="25fc9-124">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="25fc9-125">Een Run As-account en een klassieke Run As-account maken met behulp van een zelfondertekend certificaat in hello Azure Government cloud.</span><span class="sxs-lookup"><span data-stu-id="25fc9-125">Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud.</span></span>

<span data-ttu-id="25fc9-126">Afhankelijk van Hallo configuratieoptie die u selecteert, maakt Hallo script Hallo volgende items.</span><span class="sxs-lookup"><span data-stu-id="25fc9-126">Depending on hello configuration option you select, hello script creates hello following items.</span></span>

<span data-ttu-id="25fc9-127">**Voor Uitvoeren als-accounts:**</span><span class="sxs-lookup"><span data-stu-id="25fc9-127">**For Run As accounts:**</span></span>

* <span data-ttu-id="25fc9-128">Hiermee maakt u een Azure AD-toepassing toobe geëxporteerd met een zelf-ondertekend Hallo of openbare sleutel voor de enterprise-certificaat, maakt u een account voor de service-principal voor de toepassing hello in Azure AD en wijst de rol van inzender voor Hallo-account in uw huidige Hallo abonnement.</span><span class="sxs-lookup"><span data-stu-id="25fc9-128">Creates an Azure AD application toobe exported with either hello self-signed or enterprise certificate public key, creates a service principal account for hello application in Azure AD, and assigns hello Contributor role for hello account in your current subscription.</span></span> <span data-ttu-id="25fc9-129">U kunt deze instelling tooOwner of een andere rol wijzigen.</span><span class="sxs-lookup"><span data-stu-id="25fc9-129">You can change this setting tooOwner or any other role.</span></span> <span data-ttu-id="25fc9-130">Zie [Op rollen gebaseerd toegangsbeheer in Azure Automation](automation-role-based-access-control.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="25fc9-130">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="25fc9-131">Hiermee maakt u een Automation-certificaatasset met de naam *AzureRunAsCertificate* in Hallo opgegeven Automation-account.</span><span class="sxs-lookup"><span data-stu-id="25fc9-131">Creates an Automation certificate asset named *AzureRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="25fc9-132">Hallo-certificaatasset bevat Hallo privésleutel voor certificaten die wordt gebruikt door de toepassing hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="25fc9-132">hello certificate asset holds hello certificate private key that's used by hello Azure AD application.</span></span>
* <span data-ttu-id="25fc9-133">Hiermee maakt u een Automation-verbindingsasset genaamd *AzureRunAsConnection* in Hallo opgegeven Automation-account.</span><span class="sxs-lookup"><span data-stu-id="25fc9-133">Creates an Automation connection asset named *AzureRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="25fc9-134">Hallo-verbindingsasset bevat Hallo applicationId, tenantId, subscriptionId en de vingerafdruk van certificaat.</span><span class="sxs-lookup"><span data-stu-id="25fc9-134">hello connection asset holds hello applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="25fc9-135">**Voor klassieke uitvoeren als-accounts:**</span><span class="sxs-lookup"><span data-stu-id="25fc9-135">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="25fc9-136">Hiermee maakt u een Automation-certificaatasset met de naam *AzureClassicRunAsCertificate* in Hallo opgegeven Automation-account.</span><span class="sxs-lookup"><span data-stu-id="25fc9-136">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="25fc9-137">Hallo-certificaatasset bevat Hallo privésleutel voor certificaten die door het Hallo-beheercertificaat gebruikt.</span><span class="sxs-lookup"><span data-stu-id="25fc9-137">hello certificate asset holds hello certificate private key used by hello management certificate.</span></span>
* <span data-ttu-id="25fc9-138">Hiermee maakt u een Automation-verbindingsasset genaamd *AzureClassicRunAsConnection* in Hallo opgegeven Automation-account.</span><span class="sxs-lookup"><span data-stu-id="25fc9-138">Creates an Automation connection asset named *AzureClassicRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="25fc9-139">Hallo-verbindingsasset bevat Hallo abonnementsnaam, abonnements-id en naam van certificaat asset.</span><span class="sxs-lookup"><span data-stu-id="25fc9-139">hello connection asset holds hello subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="25fc9-140">Als u de optie voor het maken van een klassieke Run As-account nadat Hallo-script is uitgevoerd is uploaden Hallo openbaar certificaat (.cer bestandsnaamextensie) toohello management opslaan voor Hallo-abonnement dat Hallo Automation-account gemaakt in.</span><span class="sxs-lookup"><span data-stu-id="25fc9-140">If you select either option for creating a Classic Run As account, after hello script is executed, upload hello public certificate (.cer file name extension) toohello management store for hello subscription that hello Automation account was created in.</span></span>
> 

1. <span data-ttu-id="25fc9-141">Hallo script volgen op uw computer opslaan.</span><span class="sxs-lookup"><span data-stu-id="25fc9-141">Save hello following script on your computer.</span></span> <span data-ttu-id="25fc9-142">Sla het bestand in dit voorbeeld met Hallo filename *nieuw RunAsAccount.ps1*.</span><span class="sxs-lookup"><span data-stu-id="25fc9-142">In this example, save it with hello filename *New-RunAsAccount.ps1*.</span></span>

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
        $KeyCredential.EndDate= [DateTime]$PfxCert.GetExpirationDateString()
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
        if (!(($AzureRMProfileVersion.Major -ge 2 -and $AzureRMProfileVersion.Minor -ge 1) -or ($AzureRMProfileVersion.Major -gt 2)))
        {
           Write-Error -Message "Please install hello latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
           return
        }

        Login-AzureRmAccount -EnvironmentName $EnvironmentName
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
        $SubscriptionName = $subscription.Subscription.SubscriptionName
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. <span data-ttu-id="25fc9-143">Start op uw computer **Windows PowerShell** van Hallo **Start** scherm met verhoogde gebruikersrechten.</span><span class="sxs-lookup"><span data-stu-id="25fc9-143">On your computer, start **Windows PowerShell** from hello **Start** screen with elevated user rights.</span></span>
3. <span data-ttu-id="25fc9-144">Van Hallo verhoogde opdrachtregel-shell, Ga toohello map die u hebt gemaakt in stap 1 Hallo-script bevat.</span><span class="sxs-lookup"><span data-stu-id="25fc9-144">From hello elevated command-line shell, go toohello folder that contains hello script you created in step 1.</span></span>  
4. <span data-ttu-id="25fc9-145">Hallo-script uitvoeren met behulp van de parameterwaarden Hallo voor Hallo-configuratie die u nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="25fc9-145">Execute hello script by using hello parameter values for hello configuration you require.</span></span>

    <span data-ttu-id="25fc9-146">**Een Uitvoeren als-account maken met een zelfondertekend certificaat**</span><span class="sxs-lookup"><span data-stu-id="25fc9-146">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="25fc9-147">**Een Uitvoeren als-account en een klassiek Uitvoeren als-account maken met een zelfondertekend certificaat**</span><span class="sxs-lookup"><span data-stu-id="25fc9-147">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="25fc9-148">**Een Uitvoeren als-account en een klassiek Uitvoeren als-account maken met een bedrijfscertificaat**</span><span class="sxs-lookup"><span data-stu-id="25fc9-148">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="25fc9-149">**Een Run As-account en een klassieke Run As-account maken met behulp van een zelfondertekend certificaat in hello Azure Government cloud**</span><span class="sxs-lookup"><span data-stu-id="25fc9-149">**Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="25fc9-150">Nadat het Hallo-script is uitgevoerd, kunt u zich na vragen aan gebruiker tooauthenticate met Azure.</span><span class="sxs-lookup"><span data-stu-id="25fc9-150">After hello script has executed, you will be prompted tooauthenticate with Azure.</span></span> <span data-ttu-id="25fc9-151">Aanmelden met een account dat lid is van Hallo abonnement beheerders rol en medebeheerder van Hallo-abonnement.</span><span class="sxs-lookup"><span data-stu-id="25fc9-151">Sign in with an account that is a member of hello subscription administrators role and co-administrator of hello subscription.</span></span>
    >
    >

<span data-ttu-id="25fc9-152">Nadat het Hallo-script met succes is uitgevoerd, let u op Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="25fc9-152">After hello script has executed successfully, note hello following:</span></span>
* <span data-ttu-id="25fc9-153">Als u een klassieke Run As-account hebt gemaakt met een zelf-ondertekend openbaar certificaat (.cer-bestand), Hallo script wordt gemaakt en slaat deze toohello map met tijdelijke bestanden op uw computer onder Hallo gebruikersprofiel *%USERPROFILE%\AppData\Local\Temp*, die u gebruikt tooexecute Hallo PowerShell-sessie.</span><span class="sxs-lookup"><span data-stu-id="25fc9-153">If you created a Classic Run As account with a self-signed public certificate (.cer file), hello script creates and saves it toohello temporary files folder on your computer under hello user profile *%USERPROFILE%\AppData\Local\Temp*, which you used tooexecute hello PowerShell session.</span></span>
* <span data-ttu-id="25fc9-154">Gebruik dit certificaat als u een klassiek Uitvoeren als-account hebt gemaakt met een openbaar certificaat (.cer-bestand).</span><span class="sxs-lookup"><span data-stu-id="25fc9-154">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="25fc9-155">Hallo-instructies voor [een beheer-API certificaat toohello klassieke Azure-portal uploaden](../azure-api-management-certs.md), en vervolgens Hallo verwijzingsconfiguratie met resources van klassieke implementatie te valideren met behulp van Hallo [voorbeeldcode tooauthenticate met Azure Classic Deployment Resources](automation-verify-runas-authentication.md#classic-run-as-authentication).</span><span class="sxs-lookup"><span data-stu-id="25fc9-155">Follow hello instructions for [uploading a management API certificate toohello Azure classic portal](../azure-api-management-certs.md), and then validate hello credential configuration with classic deployment resources by using hello [sample code tooauthenticate with Azure Classic Deployment Resources](automation-verify-runas-authentication.md#classic-run-as-authentication).</span></span> 
* <span data-ttu-id="25fc9-156">Als u dit hebt gedaan *niet* klassieke Run As-account maken en verifiëren met Resource Manager-resources Hallo verwijzingsconfiguratie valideren met behulp van Hallo [voorbeeldcode voor verificatie met Service Management resources](automation-verify-runas-authentication.md#automation-run-as-authentication).</span><span class="sxs-lookup"><span data-stu-id="25fc9-156">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate hello credential configuration by using hello [sample code for authenticating with Service Management resources](automation-verify-runas-authentication.md#automation-run-as-authentication).</span></span>

## <a name="next-steps"></a><span data-ttu-id="25fc9-157">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="25fc9-157">Next steps</span></span>
* <span data-ttu-id="25fc9-158">Voor meer informatie over Service-Principals te verwijzen[toepassingsobjecten en Service-Principal objecten](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="25fc9-158">For more information about Service Principals, refer too[Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="25fc9-159">Voor meer informatie over certificaten en Azure-services te verwijzen[certificaten voor Azure Cloud Services-overzicht](../cloud-services/cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="25fc9-159">For more information about certificates and Azure services, refer too[Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>
