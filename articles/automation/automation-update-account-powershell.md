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
# <a name="update-automation-run-as-account-using-powershell"></a>Automation Uitvoeren als-account bijwerken met PowerShell
U kunt PowerShell tooupdate uw bestaande Automation-account gebruiken als:

* U maakt een Automation-account maar weigeren toocreate Hallo Run As-account.
* U al een Automation-account toomanage Resource Manager-resources gebruikt en gewenste tooupdate Hallo account tooinclude Hallo Run As-account voor de runbook-verificatie.
* U al een Automation-account toomanage klassieke resources gebruikt en u wilt tooupdate het toouse Hallo klassieke Run As-account in plaats van een nieuw account maken en uw runbooks en activa tooit migreren.   
* Toocreate wilt u een Run As- en klassieke Run As-account met behulp van een certificaat zijn uitgegeven door uw enterprise-certificeringsinstantie (CA).

## <a name="prerequisites"></a>Vereisten

* Hallo-script kan alleen op Windows 10 en Windows Server 2016 met Azure Resource Manager-modules 2.01 en hoger worden uitgevoerd. Uitvoeren wordt niet ondersteund in eerdere versies van Windows.
* Azure PowerShell 1.0 en hoger. Zie voor meer informatie over Hallo PowerShell 1.0 release [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).
* Een Automation-account waarnaar wordt verwezen als waarde voor Hallo Hallo *-AutomationAccountName* en *- ApplicationDisplayName* parameters in de volgende PowerShell-script Hallo.

Hallo tooget waarden voor *SubscriptionID*, *ResourceGroup*, en *AutomationAccountName*, die de vereiste parameters voor Hallo scripts zijn, Hallo te volgen:
1. In Hallo Azure-portal, selecteert u uw Automation-account op Hallo **Automation-account** blade en selecteer vervolgens **alle instellingen**. 
2. Op Hallo **alle instellingen** blade onder **Accountinstellingen**, selecteer **eigenschappen**. 
3. Houd er rekening mee Hallo waarden op Hallo **eigenschappen** blade.

![blade 'Eigenschappen' Hello Automation-account](media/automation-sec-configure-azure-runas-account/automation-account-properties.png)  

## <a name="create-run-as-account-powershell-script"></a>PowerShell-script voor Uitvoeren als-account maken
Deze PowerShell-script biedt ondersteuning voor Hallo volgende configuraties:

* Een Uitvoeren als-account maken met een zelfondertekend certificaat.
* Een Uitvoeren als-account en een klassiek Uitvoeren als-account maken met een zelfondertekend certificaat.
* Een Uitvoeren als-account en een klassiek Uitvoeren als-account maken met een bedrijfscertificaat.
* Een Run As-account en een klassieke Run As-account maken met behulp van een zelfondertekend certificaat in hello Azure Government cloud.

Afhankelijk van Hallo configuratieoptie die u selecteert, maakt Hallo script Hallo volgende items.

**Voor Uitvoeren als-accounts:**

* Hiermee maakt u een Azure AD-toepassing toobe geëxporteerd met een zelf-ondertekend Hallo of openbare sleutel voor de enterprise-certificaat, maakt u een account voor de service-principal voor de toepassing hello in Azure AD en wijst de rol van inzender voor Hallo-account in uw huidige Hallo abonnement. U kunt deze instelling tooOwner of een andere rol wijzigen. Zie [Op rollen gebaseerd toegangsbeheer in Azure Automation](automation-role-based-access-control.md) voor meer informatie.
* Hiermee maakt u een Automation-certificaatasset met de naam *AzureRunAsCertificate* in Hallo opgegeven Automation-account. Hallo-certificaatasset bevat Hallo privésleutel voor certificaten die wordt gebruikt door de toepassing hello Azure AD.
* Hiermee maakt u een Automation-verbindingsasset genaamd *AzureRunAsConnection* in Hallo opgegeven Automation-account. Hallo-verbindingsasset bevat Hallo applicationId, tenantId, subscriptionId en de vingerafdruk van certificaat.

**Voor klassieke uitvoeren als-accounts:**

* Hiermee maakt u een Automation-certificaatasset met de naam *AzureClassicRunAsCertificate* in Hallo opgegeven Automation-account. Hallo-certificaatasset bevat Hallo privésleutel voor certificaten die door het Hallo-beheercertificaat gebruikt.
* Hiermee maakt u een Automation-verbindingsasset genaamd *AzureClassicRunAsConnection* in Hallo opgegeven Automation-account. Hallo-verbindingsasset bevat Hallo abonnementsnaam, abonnements-id en naam van certificaat asset.

>[!NOTE]
> Als u de optie voor het maken van een klassieke Run As-account nadat Hallo-script is uitgevoerd is uploaden Hallo openbaar certificaat (.cer bestandsnaamextensie) toohello management opslaan voor Hallo-abonnement dat Hallo Automation-account gemaakt in.
> 

1. Hallo script volgen op uw computer opslaan. Sla het bestand in dit voorbeeld met Hallo filename *nieuw RunAsAccount.ps1*.

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

2. Start op uw computer **Windows PowerShell** van Hallo **Start** scherm met verhoogde gebruikersrechten.
3. Van Hallo verhoogde opdrachtregel-shell, Ga toohello map die u hebt gemaakt in stap 1 Hallo-script bevat.  
4. Hallo-script uitvoeren met behulp van de parameterwaarden Hallo voor Hallo-configuratie die u nodig hebt.

    **Een Uitvoeren als-account maken met een zelfondertekend certificaat**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    **Een Uitvoeren als-account en een klassiek Uitvoeren als-account maken met een zelfondertekend certificaat**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    **Een Uitvoeren als-account en een klassiek Uitvoeren als-account maken met een bedrijfscertificaat**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    **Een Run As-account en een klassieke Run As-account maken met behulp van een zelfondertekend certificaat in hello Azure Government cloud**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > Nadat het Hallo-script is uitgevoerd, kunt u zich na vragen aan gebruiker tooauthenticate met Azure. Aanmelden met een account dat lid is van Hallo abonnement beheerders rol en medebeheerder van Hallo-abonnement.
    >
    >

Nadat het Hallo-script met succes is uitgevoerd, let u op Hallo volgende:
* Als u een klassieke Run As-account hebt gemaakt met een zelf-ondertekend openbaar certificaat (.cer-bestand), Hallo script wordt gemaakt en slaat deze toohello map met tijdelijke bestanden op uw computer onder Hallo gebruikersprofiel *%USERPROFILE%\AppData\Local\Temp*, die u gebruikt tooexecute Hallo PowerShell-sessie.
* Gebruik dit certificaat als u een klassiek Uitvoeren als-account hebt gemaakt met een openbaar certificaat (.cer-bestand). Hallo-instructies voor [een beheer-API certificaat toohello klassieke Azure-portal uploaden](../azure-api-management-certs.md), en vervolgens Hallo verwijzingsconfiguratie met resources van klassieke implementatie te valideren met behulp van Hallo [voorbeeldcode tooauthenticate met Azure Classic Deployment Resources](automation-verify-runas-authentication.md#classic-run-as-authentication). 
* Als u dit hebt gedaan *niet* klassieke Run As-account maken en verifiëren met Resource Manager-resources Hallo verwijzingsconfiguratie valideren met behulp van Hallo [voorbeeldcode voor verificatie met Service Management resources](automation-verify-runas-authentication.md#automation-run-as-authentication).

## <a name="next-steps"></a>Volgende stappen
* Voor meer informatie over Service-Principals te verwijzen[toepassingsobjecten en Service-Principal objecten](../active-directory/active-directory-application-objects.md).
* Voor meer informatie over certificaten en Azure-services te verwijzen[certificaten voor Azure Cloud Services-overzicht](../cloud-services/cloud-services-certs-create.md).
