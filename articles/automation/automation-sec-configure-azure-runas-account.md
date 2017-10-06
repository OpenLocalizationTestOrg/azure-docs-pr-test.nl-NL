---
title: een Azure uitvoeren als-Account aaaConfigure | Microsoft Docs
description: Deze zelfstudie wordt u begeleid Hallo maken, testen en voorbeeld-gebruik van verificatie van de beveiligingsprincipal in Azure Automation.
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
keywords: naam van service-principal, setspn, azure-verificatie
ms.assetid: 2f783441-15c7-4ea0-ba27-d7daa39b1dd3
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/06/2017
ms.author: magoedte
ROBOTS: NOINDEX
redirect_url: /azure/automation/
redirect_document_id: True
ms.openlocfilehash: 06675d2f6b9d8e7260ffaead4f2b2f61c2b98d13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-runbooks-with-an-azure-run-as-account"></a>Runbooks verifiëren met een Azure Uitvoeren als-account
Dit artikel laat zien hoe tooconfigure een Azure Automation-account in hello Azure-portal. toodo dus u Hallo Run As-account functie tooauthenticate runbooks gebruiken voor het beheren van resources in Azure Resource Manager of Azure Service Management.

Wanneer u een Automation-account in hello Azure-portal maakt, maakt u automatisch twee accounts:

* Een Uitvoeren als-account. Door dit account worden een service-principal in Azure Active Directory (Azure AD) en een certificaat gemaakt. Hallo Inzender op rollen gebaseerde toegangsbeheer (RBAC), die Resource Manager-resources met behulp van runbooks beheert wijst ook toe.
* Een klassiek Uitvoeren als-account. Dit account een beheercertificaat dat is geüpload gebruikt toomanage Service Management of klassieke resources met behulp van runbooks.

Maken van een account Hallo eenvoudiger voor u en helpt die u snel starten maken en implementeren van runbooks toosupport Automation uw automation moet.

Met een Uitvoeren als- en een klassiek Uitvoeren als-account kunt u:

* Bieden een gestandaardiseerde manier tooauthenticate Azure bij het beheren van Resource Manager of de Service Management-resources van runbooks in hello Azure-portal.
* Hallo-gebruik van globale runbooks die u in Azure waarschuwingen configureren kunt automatiseren.

> [!NOTE]
> Hallo [Azure waarschuwing integratiefunctie](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) met Automation globale runbooks vereist een Automation-account dat geconfigureerd met Run As-account en een klassieke Run As-account. U kunt een automatiseringsaccount dat al is gedefinieerd uitvoeren als en klassieke Run As-accounts kunt selecteren, of u kunt toocreate een nieuw automatiseringsaccount.
>  

Dit artikel laat zien hoe toocreate een Automation-account van hello Azure-portal een Automation-account bijwerken met behulp van Azure PowerShell, Hallo-accountconfiguratie beheren en verifiëren in uw runbooks.

Voordat u begint met het maken van een Automation-account, is een goed idee toounderstand en houd rekening met de volgende Hallo:

* Een automatiseringsaccount maakt, heeft dit geen invloed op de Automation-accounts die kunt u al hebt gemaakt in de klassieke Hallo of Resource Manager-implementatiemodel.
* Hallo-proces werkt alleen voor Automation-accounts die u in hello Azure-portal maakt. Poging een account van de klassieke Azure-portal Hallo toocreate repliceert niet Hallo configuratie Run As-account.
* Als u al runbooks en activa (zoals planningen of variabelen) in plaats toomanage klassieke resources hebt en u wilt dat runbooks tooauthenticate met Hallo nieuwe klassieke Run As-account, gaat u een van de volgende Hallo:

  * toocreate klassieke Run As-account, volg Hallo-instructies in 'Uw Run As-account beheren' Hallo-sectie. 
  * tooupdate uw bestaande account, gebruik Hallo PowerShell script in 'Uw Automation-account bijwerken met behulp van PowerShell' Hallo-sectie.
* tooauthenticate met behulp van Hallo nieuwe Run As-account en klassieke uitvoeren als Automation-account, moet u uw bestaande runbooks met voorbeeldcode in de sectie Hallo Hallo toomodify [voorbeelden van verificatiecode](#authentication-code-examples).

    >[!NOTE]
    >Hallo Run As-account is voor verificatie met een Resource Manager-resources met Hallo op basis van certificaten service-principal. Hallo klassieke Run As-account is voor verificatie ten opzichte van de Service Management-resources met een beheercertificaat.

## <a name="create-an-automation-account-from-hello-azure-portal"></a>Een Automation-account maken vanuit hello Azure-portal
In deze sectie maakt u een Azure Automation-account van hello Azure portal, dat op zijn beurt zowel een Run As-account en een klassieke Run As-account maakt.

>[!NOTE]
>toocreate een Automation-account, moet u lid zijn van Hallo serviceadministrators rol of medebeheerder van Hallo-abonnement dat is toohello-abonnement toegang verleent. U moet ook worden toegevoegd als een gebruiker toothat abonnement standaard Active Directory-exemplaar. Hallo account hoeft niet toobe een bevoorrechte rol toegewezen.
>
>Als u niet lid zijn van de Active Directory-exemplaar van Hallo abonnement voordat u toohello mede beheerdersrol van Hallo abonnement worden toegevoegd, wordt u tooActive Directory toegevoegd als gast. In dit geval ontvangt u een "u hebt geen machtigingen toocreate..." Waarschuwing voor Hallo **Automation-Account toevoegen** blade.
>
>Gebruikers die zijn toegevoegd toohello medebeheerder rol kan worden verwijderd uit Active Directory-exemplaar van het abonnement Hallo eerst en opnieuw toegevoegd toomake ze een volledige gebruiker in Active Directory. tooverify deze situatie Hallo **Azure Active Directory** deelvenster in hello Azure-portal door te selecteren **gebruikers en groepen**, selecteren **alle gebruikers** en, nadat u hebt geselecteerd specifieke gebruiker Hello, selecteren **profiel**. waarde van Hallo Hallo **gebruikerstype** kenmerk onder Hallo gebruikersprofiel moet niet gelijk aan **Gast**.
>

1. Meld u aan toohello Azure-portal met een account dat lid is van Hallo abonnement beheerders rol en medebeheerder van Hallo-abonnement.

2. Selecteer **Automation-accounts**.

3. Op Hallo **Automation-Accounts** blade, klikt u op **toevoegen**.
Hallo **Automation-Account toevoegen** blade wordt geopend.

 ![Hallo 'Automation-Account toevoegen' blade](media/automation-sec-configure-azure-runas-account/create-automation-account-properties-b.png)

   > [!NOTE]
   > Als uw account geen lid is van Hallo abonnement beheerders rol en medebeheerder van Hallo abonnement is, Hallo volgende waarschuwing wordt weergegeven op Hallo **Automation-Account toevoegen** blade:
   >
   >![Waarschuwing bij Automation-account toevoegen](media/automation-sec-configure-azure-runas-account/create-account-without-perms.png)
   >
   >

4. Op Hallo **Automation-Account toevoegen** blade in Hallo **naam** typt u een naam voor uw nieuwe Automation-account.

5. Als u meer dan één abonnement hebt, Hallo te volgen:

    a. Onder **abonnement**, één voor de nieuwe account Hallo opgeven.

    b. Klik onder **Resourcegroep** op **Nieuwe maken** of **Bestaande gebruiken**.

    c. Geef onder **Locatie** een Azure-datacenter op.

6. Selecteer onder **Een Uitvoeren als-account voor Azure maken** de optie **Ja** en klik vervolgens op **Maken**.

   > [!NOTE]
   > Als u ervoor geen toocreate Hallo Run As-account door te selecteren kiest **Nee**, een waarschuwingsbericht weergegeven Hallo **Automation-Account toevoegen** blade. Hoewel het Hallo-account is gemaakt in hello Azure-portal, heeft deze geen overeenkomstige verificatie-id in de klassieke of Resource Manager abonnement directoryservice. Hallo-account heeft dus geen tooresources toegang in uw abonnement. Met dit scenario wordt voorkomen dat runbooks die naar dit account verwijzen, taken verifiëren en uitvoeren met resources in die implementatiemodellen.
   >
   > ![Waarschuwingsbericht op Hallo 'Automation-Account toevoegen' blade](media/automation-sec-configure-azure-runas-account/create-account-decline-create-runas-msg.png)
   >
   > Bovendien Hallo service-principal is niet gemaakt, omdat de is rol van Inzender Hallo niet toegewezen.
   >

7. Terwijl Azure Hallo Automation-account maakt, kunt u de voortgang Hallo onder bijhouden **meldingen** in Hallo-menu.

### <a name="resources"></a>Resources
Als Hallo Automation-account is gemaakt, worden automatisch verschillende resources voor u gemaakt. Hallo resources worden samengevat in de volgende twee tabellen Hallo:

#### <a name="run-as-account-resources"></a>Resources voor Uitvoeren als-account

| Resource | Beschrijving |
| --- | --- |
| AzureAutomationTutorial Runbook | Een grafische voorbeeldrunbook dat laat zien hoe tooauthenticate met behulp van Hallo Run As-account en alle Hallo Resource Manager-resources opgehaald. |
| AzureAutomationTutorialScript Runbook | Een voorbeeldrunbook PowerShell die laat zien hoe tooauthenticate met behulp van Hallo Run As-account en alle Hallo Resource Manager-resources opgehaald. |
| AzureRunAsCertificate | Hallo-certificaatasset dat automatisch wordt gemaakt wanneer u een Automation-account maken of Hallo volgende PowerShell-script voor een bestaand account gebruiken. Hallo certificaat kunt u tooauthenticate met Azure zodat u Azure Resource Manager-resources van runbooks beheren kunt. Hallo-certificaat heeft een één jaar geldig. |
| AzureRunAsConnection | Hallo-verbindingsasset dat automatisch wordt gemaakt wanneer u een Automation-account maken of Hallo PowerShell-script voor een bestaande account gebruiken. |

#### <a name="classic-run-as-account-resources"></a>Resources voor klassiek Uitvoeren als-account

| Resource | Beschrijving |
| --- | --- |
| AzureClassicAutomationTutorial Runbook | Een grafische voorbeeldrunbook waarin alle Hallo VM's die zijn gemaakt met behulp van het klassieke implementatiemodel Hallo in een abonnement met behulp van Hallo klassieke Run As-account (certificaat), en vervolgens schrijft Hallo VM-naam en status worden opgehaald. |
| AzureClassicAutomationTutorial Script Runbook | Een voorbeeld van de PowerShell-runbook die alle opgehaald Hallo klassieke virtuele machines in een abonnement met behulp van Hallo klassieke Run As-account (certificaat) en vervolgens schrijfbewerkingen Hallo VM-naam en de status. |
| AzureClassicRunAsCertificate | Hallo automatisch gemaakt certificaatasset tooauthenticate te gebruiken met Azure zodat u de klassieke Azure-resources van runbooks beheren kunt. Hallo-certificaat heeft een één jaar geldig. |
| AzureClassicRunAsConnection | Hallo automatisch gemaakte verbindingsasset tooauthenticate te gebruiken met Azure zodat u de klassieke Azure-resources van runbooks beheren kunt. |

## <a name="verify-run-as-authentication"></a>Uitvoeren als-verificatie verifiëren
Voer een kleine test tooconfirm die u verifiëren kunt met behulp van Hallo nieuwe Run As-account.

1. Open in hello Azure-portal, Hallo Automation-account dat u eerder hebt gemaakt.

2. Klik op Hallo **Runbooks** tegel tooopen Hallo lijst van runbooks.

3. Selecteer Hallo **AzureAutomationTutorialScript** runbook, en klik vervolgens op **Start** toostart hello runbook. Hallo volgende gebeurtenissen zich voordoen:
 * Een [runbooktaak](automation-runbook-execution.md) is gemaakt, hello **taak** blade wordt weergegeven en Hallo taakstatus wordt weergegeven in Hallo **taakoverzicht** tegel.
 * Hallo taakstatus begint als **in de wachtrij geplaatst**, die aangeeft dat er wordt gewacht tot een runbook worker in Hallo cloud toobecome beschikbaar.
 * Hallo-status wordt **starten** wanneer een werknemer Hallo taak claims.
 * Hallo-status wordt **met** wanneer Hallo runbook wordt gestart.
 * Wanneer het Hallo-runbooktaak is voltooid, ziet u de status van **voltooid**.

       ![Security Principal Runbook Test](media/automation-sec-configure-azure-runas-account/job-summary-automationtutorialscript.png)
4. toosee Hallo gedetailleerde resultaten van Hallo runbook, klikt u op Hallo **uitvoer** tegel.  
Hallo **uitvoer** blade wordt weergegeven, met dat runbook Hallo heeft geverifieerd en een lijst met alle beschikbare resources in Hallo resourcegroep geretourneerd.

5. Sluit Hallo **uitvoer** blade tooreturn toohello **taakoverzicht** blade.

6. Sluit Hallo **taakoverzicht** blade en de bijbehorende van Hallo **AzureAutomationTutorialScript** runbookblade.

## <a name="verify-classic-run-as-authentication"></a>Klassieke Uitvoeren als-verificatie verifiëren
Uitvoeren van een vergelijkbare kleine tooconfirm die u verifiëren kunt met behulp van Hallo nieuwe klassieke Run As-account te testen.

1. Open in hello Azure-portal, Hallo Automation-account dat u eerder hebt gemaakt.

2. Klik op Hallo **Runbooks** tegel tooopen Hallo lijst van runbooks.

3. Selecteer Hallo **AzureClassicAutomationTutorialScript** runbook, en klik vervolgens op **Start** Hallo-runbook te starten. Hallo volgende gebeurtenissen zich voordoen:

 * Een [runbooktaak](automation-runbook-execution.md) is gemaakt, hello **taak** blade wordt weergegeven en Hallo taakstatus wordt weergegeven in Hallo **taakoverzicht** tegel.
 * Hallo taakstatus begint als **in de wachtrij geplaatst**, die aangeeft dat er wordt gewacht tot een runbook worker in Hallo cloud toobecome beschikbaar.
 * Hallo-status wordt **starten** wanneer een werknemer Hallo taak claims.
 * Hallo-status wordt **met** wanneer Hallo runbook wordt gestart.
 * Wanneer het Hallo-runbooktaak is voltooid, ziet u de status van **voltooid**.

    ![Runbooktest beveiligingsprincipal](media/automation-sec-configure-azure-runas-account/job-summary-automationclassictutorialscript.png)<br>
4. toosee Hallo gedetailleerde resultaten van Hallo runbook, klikt u op Hallo **uitvoer** tegel.  
Hallo **uitvoer** blade wordt weergegeven, met dat runbook Hallo heeft geverifieerd en een lijst met alle klassieke VM's in Hallo abonnement geretourneerd.

5. Sluit Hallo **uitvoer** blade tooreturn toohello **taakoverzicht** blade.

6. Sluit Hallo **taakoverzicht** blade en de bijbehorende van Hallo **AzureAutomationTutorialScript** runbookblade.

## <a name="managing-your-run-as-account"></a>Uw Uitvoeren als-account beheren
Op een bepaald moment voordat uw Automation-account is verlopen, moet u toorenew Hallo certificaat. Als u dat Hallo Run As-account er inbreuk is gemaakt denkt, kunt u deze kunt verwijderen en opnieuw maken. Deze sectie wordt beschreven hoe tooperform deze bewerkingen.

### <a name="self-signed-certificate-renewal"></a>Zelfondertekend certificaat vernieuwen
Hallo zelfondertekend certificaat dat u hebt gemaakt voor Hallo Run As-account verloopt een jaar na de datum Hallo van maken. U kunt het certificaat op elk gewenst moment vernieuwen voordat het verloopt. Als u deze vernieuwt, wordt Hallo huidige geldig certificaat terugkerende tooensure dat alle runbooks die in de wachtrij staan actief of actief actief, en die zich verifiëren met Hallo Run As-account, niet nadelig worden beïnvloed. Hallo-certificaat is geldig tot de vervaldatum.

> [!NOTE]
> Als u uw Automation Run As-account toouse een certificaat dat is uitgegeven door de certificeringsinstantie van uw onderneming hebt geconfigureerd en u deze optie gebruikt, wordt de Hallo enterprise-certificaat worden vervangen door een zelfondertekend certificaat.

Hallo toorenew certificaat, Hallo te volgen:

1. Open in hello Azure-portal, Hallo Automation-account.

2. Op Hallo **Automation-Account** blade in Hallo **eigenschappen van Account** deelvenster onder **Accountinstellingen**, selecteer **Run As-Accounts**.

    ![Eigenschappendeelvenster voor Automation-account](media/automation-sec-configure-azure-runas-account/automation-account-properties-pane.png)
3. Op Hallo **Run As-Accounts** eigenschappenblade, selecteer de Hallo Run As-account of Hallo klassieke Run As-account die u wilt dat toorenew Hallo certificaat voor.

4. Op Hallo **eigenschappen** blade voor Hallo account hebt geselecteerd, klikt u op **certificaat vernieuwen**.

    ![Certificaat vernieuwen voor Uitvoeren als-account](media/automation-sec-configure-azure-runas-account/automation-account-renew-runas-certificate.png)

5. Tijdens het Hallo-certificaat wordt vernieuwd, kunt u de voortgang Hallo onder bijhouden **meldingen** in Hallo-menu.

### <a name="delete-a-run-as-or-classic-run-as-account"></a>Een Uitvoeren als- of klassiek Uitvoeren als-account verwijderen
Deze sectie wordt beschreven hoe toodelete en opnieuw maken van een Run As- of klassieke Run As-account. Wanneer u deze actie uitvoert, wordt Hallo Automation-account bewaard. Nadat u een Run As- of klassieke Run As-account verwijdert, kunt u het opnieuw maken in hello Azure-portal.

1. Open in hello Azure-portal, Hallo Automation-account.

2. Op Hallo **Automation-account** blade in Hallo account eigenschappendeelvenster selecteert **Run As-Accounts**.

3. Op Hallo **Run As-Accounts** eigenschappenblade, selecteer de Hallo Run As-account of klassieke Run As-account dat u wilt dat toodelete. Klik vervolgens op Hallo **eigenschappen** blade voor Hallo account hebt geselecteerd, klikt u op **verwijderen**.

 ![Uitvoeren als-account verwijderen](media/automation-sec-configure-azure-runas-account/automation-account-delete-runas.png)

4. Tijdens het Hallo-account wordt verwijderd, u kunt de voortgang Hallo onder volgen **meldingen** in Hallo-menu.

5. Nadat het Hallo-account is verwijderd, kunt u opnieuw dit maken op Hallo **Run As-Accounts** eigenschappenblade door het selecteren van Hallo maken de optie **Azure uitvoeren als-Account**.

 ![Hallo Automation Run As-account opnieuw maken](media/automation-sec-configure-azure-runas-account/automation-account-create-runas.png)

### <a name="misconfiguration"></a>Onjuiste configuratie
Bepaalde configuratie-items die nodig zijn voor Hallo Run As- of klassieke Run As-account toofunction goed mogelijk is verwijderd of niet goed worden gemaakt tijdens de eerste configuratie. Hallo-items omvatten:

* Certificaatasset
* Verbindingsasset
* Run As-account is verwijderd uit de rol Inzender Hallo
* Service-principal of toepassing in Azure AD

In de voorgaande Hallo en andere exemplaren van onjuiste configuratie, detecteert Hallo Automation-account Hallo wijzigingen en een status weer van *onvolledig* op Hallo **Run As-Accounts** eigenschappenblade voor Hallo account.

![Onvolledige Uitvoeren als-configuratiestatus](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config.png)

Wanneer u Hallo Run As-account selecteert, Hallo account **eigenschappen** deelvenster Hallo volgende foutbericht weergegeven:

![Waarschuwingsbericht Onvolledige Uitvoeren als-configuratie](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config-msg.png).

Deze problemen Run As-account kunt u snel oplossen door te verwijderen en opnieuw Hallo-account te maken.

## <a name="update-your-automation-account-by-using-powershell"></a>Uw Automation-account bijwerken met behulp van PowerShell
U kunt PowerShell tooupdate uw bestaande Automation-account gebruiken als:

* U maakt een Automation-account maar weigeren toocreate Hallo Run As-account.
* U al een Automation-account toomanage Resource Manager-resources gebruikt en gewenste tooupdate Hallo account tooinclude Hallo Run As-account voor de runbook-verificatie.
* U al een Automation-account toomanage klassieke resources gebruikt en u wilt tooupdate het toouse Hallo klassieke Run As-account in plaats van een nieuw account maken en uw runbooks en activa tooit migreren.   
* Toocreate wilt u een Run As- en klassieke Run As-account met behulp van een certificaat zijn uitgegeven door uw enterprise-certificeringsinstantie (CA).

Hallo-script heeft Hallo volgende vereisten:

* Hallo-script kan alleen op Windows 10 en Windows Server 2016 met Azure Resource Manager-modules 2.01 en hoger worden uitgevoerd. Uitvoeren wordt niet ondersteund in eerdere versies van Windows.
* Azure PowerShell 1.0 en hoger. Zie voor meer informatie over Hallo PowerShell 1.0 release [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).
* Een Automation-account waarnaar wordt verwezen als waarde voor Hallo Hallo *-AutomationAccountName* en *- ApplicationDisplayName* parameters in de volgende PowerShell-script Hallo.

Hallo tooget waarden voor *SubscriptionID*, *ResourceGroup*, en *AutomationAccountName*, die de vereiste parameters voor Hallo scripts zijn, Hallo te volgen:
1. In Hallo Azure-portal, selecteert u uw Automation-account op Hallo **Automation-account** blade en selecteer vervolgens **alle instellingen**. 
2. Op Hallo **alle instellingen** blade onder **Accountinstellingen**, selecteer **eigenschappen**. 
3. Houd er rekening mee Hallo waarden op Hallo **eigenschappen** blade.

![blade 'Eigenschappen' Hello Automation-account](media/automation-sec-configure-azure-runas-account/automation-account-properties.png)  

### <a name="create-a-run-as-account-powershell-script"></a>Een PowerShell-script voor Uitvoeren als-account maken
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

tooexecute Hallo script en Hallo-certificaat uploaden, Hallo te volgen:

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

2. Klik op uw computer op **Start** en start vervolgens **Windows PowerShell** met verhoogde gebruikersrechten.

3. Verhoogde van Hallo PowerShell opdrachtregel-shell Ga toohello map die u hebt gemaakt in stap 1 Hallo-script bevat.

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
* Gebruik dit certificaat als u een klassiek Uitvoeren als-account hebt gemaakt met een openbaar certificaat (.cer-bestand). Volg de instructies Hallo voor [uploaden van een API management-certificaat toohello klassieke Azure-portal](../azure-api-management-certs.md), en vervolgens Hallo verwijzingsconfiguratie met Service Management-resources te valideren met behulp van Hallo [voorbeeldcode tooauthenticate met Service Management-Resources](#sample-code-to-authenticate-with-service-management-resources). 
* Als u dit hebt gedaan *niet* klassieke Run As-account maken en verifiëren met Resource Manager-resources Hallo verwijzingsconfiguratie valideren met behulp van Hallo [voorbeeldcode voor verificatie met Service Management resources](#sample-code-to-authenticate-with-resource-manager-resources).

## <a name="sample-code-tooauthenticate-with-resource-manager-resources"></a>Voorbeeld code tooauthenticate met Resource Manager-resources
Kunt u Hallo volgende bijgewerkt voorbeeldcode die afkomstig zijn uit Hallo *AzureAutomationTutorialScript* voorbeeldrunbook, tooauthenticate met behulp van Hallo Run As-account toomanage Resource Manager-resources met uw runbooks.

    $connectionName = "AzureRunAsConnection"
    $SubId = Get-AutomationVariable -Name 'SubscriptionId'
    try
    {
       # Get hello connection "AzureRunAsConnection "
       $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

       "Signing in tooAzure..."
       Add-AzureRmAccount `
         -ServicePrincipal `
         -TenantId $servicePrincipalConnection.TenantId `
         -ApplicationId $servicePrincipalConnection.ApplicationId `
         -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
       "Setting context tooa specific subscription"     
       Set-AzureRmContext -SubscriptionId $SubId              
    }
    catch {
        if (!$servicePrincipalConnection)
        {
           $ErrorMessage = "Connection $connectionName not found."
           throw $ErrorMessage
         } else{
            Write-Error -Message $_.Exception
            throw $_.Exception
         }
    }

toohelp u tooeasily tussen meerdere abonnementen werkt, Hallo script bevat twee extra regels met code die ondersteuning bieden voor die verwijzen naar de context van een abonnement. Een variabel asset met de naam *SubscriptionId* Hallo Hallo abonnement-ID bevat. Na het Hallo `Add-AzureRmAccount` instructie van de cmdlet Hallo [ `Set-AzureRmContext` ](/powershell/module/azurerm.profile/set-azurermcontext) cmdlet vermeld met de parameterset Hallo *- SubscriptionId*. Als de naam van variabele Hallo te algemeen is, kunt u herzien tooinclude een voorvoegsel of een andere naming convention toomake deze eenvoudiger tooidentify. U kunt ook kunt u de parameterset Hallo *- SubscriptionName* in plaats van *- SubscriptionId* met een bijbehorende variabeleasset.

Hallo cmdlet die u kunt gebruiken voor verificatie in Hallo-runbook `Add-AzureRmAccount`, gebruikt Hallo *ServicePrincipalCertificate* parameterset. Hiermee verifieert met behulp van Hallo service principal certificaat niet Hallo gebruikersreferenties.

## <a name="sample-code-tooauthenticate-with-service-management-resources"></a>Voorbeeld code tooauthenticate met Service Management-resources
U kunt na de bijgewerkte voorbeeldcode die is genomen van Hallo Hallo *AzureClassicAutomationTutorialScript* voorbeeldrunbook, tooauthenticate met behulp van Hallo klassieke Run As-account toomanage klassieke resources met uw runbooks.

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get hello connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate tooAzure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in hello Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting hello certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in hello Automation account."
    }

    Write-Verbose "Authenticating tooAzure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID

## <a name="next-steps"></a>Volgende stappen
* [Toepassings- en service-principalobjecten in Azure AD](../active-directory/active-directory-application-objects.md)
* [Op rollen gebaseerd toegangsbeheer in Azure Automation](automation-role-based-access-control.md)
* [Overzicht van certificaten voor Azure Cloud Services](../cloud-services/cloud-services-certs-create.md)
