---
title: aaaHow tooconfigure automatische registratie van Windows-domein-apparaten met Azure Active Directory | Microsoft Docs
description: Instellen van uw domein Windows-apparaten tooregister automatisch en zonder tussenkomst met Azure Active Directory.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 6a1aab753f5456ed06ba7979ab05f70f29b4ddee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-automatic-registration-of-windows-domain-joined-devices-with-azure-active-directory"></a>Hoe tooconfigure automatische registratie van Windows-domein apparaten met Azure Active Directory

toouse [voorwaardelijke toegang voor Azure Active Directory op basis van apparaten](active-directory-conditional-access-azure-portal.md), uw computers moeten worden geregistreerd bij Azure Active Directory (Azure AD). U kunt een lijst met geregistreerde apparaten krijgen in uw organisatie met behulp van Hallo [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in Hallo [Azure Active Directory PowerShell-module](/powershell/azure/install-msonlinev1?view=azureadps-2.0). 

Dit artikel bevat Hallo stappen voor het configureren van automatische registratie van Windows-domein apparaten Hallo met Azure AD in uw organisatie.


Voor meer informatie over:

- Voorwaardelijke toegang, Zie [voorwaardelijke toegang voor Azure Active Directory op basis van apparaten](active-directory-conditional-access-azure-portal.md). 
- Windows 10-apparaten in Hallo werkplek en verbeterde Hallo ervaringen wanneer geregistreerd in Azure AD, Zie [Windows 10 voor ondernemingen Hallo: apparaten gebruiken voor het werk](active-directory-azureadjoin-windows10-devices-overview.md).
- Windows 10 Enterprise E3 in CSP, Zie Hallo [Windows 10 Enterprise E3 in het overzicht van de CSP](https://docs.microsoft.com/en-us/windows/deployment/windows-10-enterprise-e3-overview).


## <a name="before-you-begin"></a>Voordat u begint

Voordat u begint met het configureren van Hallo automatische registratie van Windows-domein-apparaten in uw omgeving, moet u dat vertrouwd raken met de Hallo ondersteund scenario's en Hallo beperkingen.  

tooimprove hello leesbaarheid Hallo beschrijvingen van Hallo na termijn maakt gebruik van dit onderwerp: 

- **Huidige Windows-apparaten** -deze term die lid zijn van toodomain apparaten met Windows 10 of Windows Server 2016 verwijst.
- **Apparaten met Windows downlevel-** -deze term verwijst tooall **ondersteund** domein Windows-apparaten die geen actieve Windows 10 of Windows Server 2016.  


### <a name="windows-current-devices"></a>Huidige Windows-apparaten

- Voor apparaten met Hallo Windows desktop-besturingssysteem, wordt u aangeraden speciale Update (versie 1607) voor Windows 10 of hoger. 
- de registratie van de huidige Windows-apparaten Hallo **is** in niet-gefedereerde omgevingen zoals wachtwoord-hash-synchronisatie configuraties ondersteund.  


### <a name="windows-down-level-devices"></a>Eerdere Windows-apparaten

- volgende downlevel-apparaten met Windows Hello worden ondersteund:
    - Windows 8.1
    - Windows 7
    - Windows Server 2012 R2
    - Windows Server 2012
    - Windows Server 2008 R2
- de registratie van een downlevel-apparaten met Windows Hello **is** in niet-gefedereerde omgevingen via naadloze eenmalige aanmelding ondersteund [Azure Active Directory naadloze eenmalige aanmelding](https://aka.ms/hybrid/sso).
- de registratie van een downlevel-apparaten met Windows Hello **is niet** ondersteund voor apparaten met behulp van zwervende profielen. Als u gebruik van zwervende profielen of instellingen, gebruikt u Windows 10.



## <a name="prerequisites"></a>Vereisten

Voordat u begint met het inschakelen van Hallo automatische registratie van apparaten in uw organisatie lid van een domein, moet u ervoor dat u een actuele versie van Azure AD zijn uitgevoerd toomake verbinding maken.

Azure AD Connect:

- Houdt Hallo-koppeling tussen het Hallo-computeraccount in uw lokale Active Directory (AD) en Hallo apparaatobject in Azure AD. 
- Andere apparaat gerelateerde functies, zoals Windows Hello voor bedrijven.



## <a name="configuration-steps"></a>Configuratiestappen

Dit onderwerp bevat stappen voor alle scenario's met standaardconfiguratie Hallo vereist.  
Gebruik Hallo tabel tooget een overzicht van Hallo stappen die nodig voor uw scenario zijn te volgen:  



| Stappen                                      | Windows huidige en het wachtwoord-hash-synchronisatie | De huidige Windows- en Federatie | Windows downlevel- |
| :--                                        | :-:                                    | :-:                            | :-:                |
| Stap 1: Een serviceverbindingspunt configureren | ![Selecteren][1]                            | ![Selecteren][1]                    | ![Selecteren][1]        |
| Stap 2: De uitgifte van claims instellen           |                                        | ![Selecteren][1]                    | ![Selecteren][1]        |
| Stap 3: Windows 10-apparaten inschakelen      |                                        |                                | ![Selecteren][1]        |
| Stap 4: Implementatie van het besturingselement en implementatie     | ![Selecteren][1]                            | ![Selecteren][1]                    | ![Selecteren][1]        |
| Stap 5: Controleren of de geregistreerde apparaten          | ![Selecteren][1]                            | ![Selecteren][1]                    | ![Selecteren][1]        |



## <a name="step-1-configure-service-connection-point"></a>Stap 1: Een serviceverbindingspunt configureren

Hallo service connection point (SCP)-object wordt gebruikt door uw apparaten tijdens Hallo registratie toodiscover informatie over het Azure AD-tenant. Hallo SCP-object voor Hallo automatische registratie van apparaten die lid zijn van een domein moet in uw lokale Active Directory (AD) bestaan op Hallo naming context configuratiepartitie van Hallo computerforest. Er is slechts één configuratienaamgevingscontext per forest. In een configuratie met meerdere forests met Active Directory moet Hallo het service connection point in alle forests met computers domein bestaan.

U kunt Hallo [ **Get-ADRootDSE** ](https://technet.microsoft.com/library/ee617246.aspx) cmdlet tooretrieve Hallo configuratienaamgevingscontext van uw forest.  

Voor een forest met Active Directory-domeinnaam Hallo *fabrikam.com*, configuratienaamgevingscontext Hallo is:

`CN=Configuration,DC=fabrikam,DC=com`

Hallo SCP-object voor Hallo automatische registratie van apparaten die lid zijn van een domein is in uw forest zich op:  

`CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,[Your Configuration Naming Context]`

Afhankelijk van hoe u Azure AD Connect hebt geïmplementeerd, Hallo SCP-object mogelijk al zijn geconfigureerd.
U kunt controleren Hallo Hallo object bestaan en Hallo detectie waarden met behulp van de volgende Windows PowerShell-script Hallo ophalen: 

    $scp = New-Object System.DirectoryServices.DirectoryEntry;

    $scp.Path = "LDAP://CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,CN=Configuration,DC=fabrikam,DC=com";

    $scp.Keywords;

Hallo **$scp. Trefwoorden** uitvoer geeft informatie weer hello Azure AD-tenant, bijvoorbeeld:

    azureADName:microsoft.com
    azureADId:72f988bf-86f1-41af-91ab-2d7cd011db47

Als het serviceverbindingspunt Hallo niet bestaat, kunt u dit maken door het uitvoeren van Hallo `Initialize-ADSyncDomainJoinedComputerSync` cmdlet uit op uw Azure AD Connect-server. Enterprise admin credential is vereist toorun deze cmdlet.  
Hallo-cmdlet:

- Maakt het serviceverbindingspunt Hallo in hello Azure AD Connect is verbonden met Active Directory-forest. 
- Vereist dat u toospecify hello `AdConnectorAccount` parameter. Dit is Hallo-account dat is geconfigureerd als Active Directory connector-account in Azure AD connect. 


Hallo toont volgende script een voorbeeld voor het gebruik van Hallo-cmdlet. In dit script `$aadAdminCred = Get-Credential` moet u een gebruikersnaam tootype. U moet tooprovide Hallo gebruikersnaam Hallo gebruiker UPN (User Principal Name)-indeling (`user@example.com`). 


    Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1";

    $aadAdminCred = Get-Credential;

    Initialize-ADSyncDomainJoinedComputerSync –AdConnectorAccount [connector account name] -AzureADCredentials $aadAdminCred;

Hallo `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:

- Maakt gebruik van de Active Directory PowerShell-module hello, die afhankelijk is van Active Directory Web Services uitgevoerd op een domeincontroller. Active Directory Web Services wordt ondersteund op domeincontrollers met Windows Server 2008 R2 en hoger.
- Wordt alleen ondersteund door Hallo **MSOnline PowerShell moduleversie 1.1.166.0**. toodownload deze module gebruiken deze [koppeling](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).   

Voor domeincontrollers met Windows Server 2008 of eerdere versies, Hallo-script hieronder toocreate Hallo serviceverbindingspunt te gebruiken.

In een configuratie met meerdere forests, moet u Hallo script toocreate Hallo het service connection point in elk forest waar computers bestaan te volgen:
 
    $verifiedDomain = "contoso.com"    # Replace this with any of your verified domain names in Azure AD
    $tenantID = "72f988bf-86f1-41af-91ab-2d7cd011db47"    # Replace this with you tenant ID
    $configNC = "CN=Configuration,DC=corp,DC=contoso,DC=com"    # Replace this with your AD configuration naming context

    $de = New-Object System.DirectoryServices.DirectoryEntry
    $de.Path = "LDAP://CN=Services," + $configNC

    $deDRC = $de.Children.Add("CN=Device Registration Configuration", "container")
    $deDRC.CommitChanges()

    $deSCP = $deDRC.Children.Add("CN=62a0ff2e-97b9-4513-943f-0d221bd30080", "serviceConnectionPoint")
    $deSCP.Properties["keywords"].Add("azureADName:" + $verifiedDomain)
    $deSCP.Properties["keywords"].Add("azureADId:" + $tenantID)

    $deSCP.CommitChanges()


## <a name="step-2-setup-issuance-of-claims"></a>Stap 2: De uitgifte van claims instellen

In een federatieve Azure AD-configuratie apparaten zijn afhankelijk van de Active Directory Federation Services (AD FS) of een 3e party on-premises federation service tooauthenticate tooAzure AD. Apparaten verifiëren tooget een token tooregister toegang tegen hello Azure Active Directory Device Registration Service (DRS Azure).

Windows huidige apparaten met behulp van geïntegreerde Windows-verificatie tooan actieve WS-Trust eindpunt (1.3 of 2005 versies verifiëren) die worden gehost door Hallo lokale federation-service.

> [!NOTE]
> Wanneer u AD FS, ofwel **adfs/services/trust/13/windowstransport** of **adfs/services/trust/2005/windowstransport** moet zijn ingeschakeld. Als u Hallo webproxy verificatie gebruikt, zorg er ook voor dat dit eindpunt is gepubliceerd via Hallo proxy. U kunt zien welke eindpunten worden ingeschakeld via Hallo AD FS-beheerconsole onder **Service > eindpunten**.
>
>Als u geen AD FS als de lokale federation-service, instructies Hallo van uw leverancier toomake zorgen dat ze WS-Trust 1.3 of 2005 eindpunten en deze zijn gepubliceerd via Hallo Metadata Exchange-bestand (MEX) ondersteunen.

Hallo moeten volgende claims bestaan in die door Azure DRS ontvangen voor apparaat registratie toocomplete Hallo-token. Azure DRS maakt een apparaatobject in Azure AD met enkele van deze informatie die vervolgens door Azure AD Connect tooassociate Hallo nieuw apparaatobject met Hallo computer account on-premises gebruikt wordt.

* `http://schemas.microsoft.com/ws/2012/01/accounttype`
* `http://schemas.microsoft.com/identity/claims/onpremobjectguid`
* `http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`

Als u meer dan een geverifieerde domeinnaam hebt, moet u tooprovide Hallo claim voor computers te volgen:

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`

Als u al een claim onveranderbare id genoemd (bijv, alternatieve aanmeldings-ID) moet een overeenkomende claim tooprovide voor computers:

* `http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`

In de Hallo uit te voeren, kunt u informatie vinden over:
 
- Hallo waarden elke claim moet hebben.
- Hoe een definitie eruit als in AD FS

Hallo definitie helpt u bij tooverify of Hallo waarden aanwezig zijn of als u toocreate moet ze.

> [!NOTE]
> Als u AD FS niet voor de lokale federation-server gebruikt, voert u de leverancier van uw instructies toocreate Hallo juiste configuratie tooissue deze claims.

### <a name="issue-account-type-claim"></a>Probleem account type claim

**`http://schemas.microsoft.com/ws/2012/01/accounttype`**-Deze claim moet een waarde van bevatten **DJ**, waarin Hallo-apparaat als een computer lid van een domein. U kunt een regel voor het transformeren van uitgifte die uitziet toevoegen in AD FS:

    @RuleName = "Issue account type for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "DJ"
    );

### <a name="issue-objectguid-of-hello-computer-account-on-premises"></a>Probleem objectGUID van Hallo computer account lokale

**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`**-Deze claim Hallo moet bevatten **objectGUID** waarde Hallo lokale computeraccount. U kunt een regel voor het transformeren van uitgifte die uitziet toevoegen in AD FS:

    @RuleName = "Issue object GUID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/identity/claims/onpremobjectguid"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );
 
### <a name="issue-objectsid-of-hello-computer-account-on-premises"></a>Probleem objectSID van Hallo computer account lokale

**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`**-Deze claim Hallo Hallo moet bevatten **objectSid** waarde Hallo lokale computeraccount. U kunt een regel voor het transformeren van uitgifte die uitziet toevoegen in AD FS:

    @RuleName = "Issue objectSID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(claim = c2);

### <a name="issue-issuerid-for-computer-when-multiple-verified-domain-names-in-azure-ad"></a>IssuerID voor computer uitgeven wanneer meerdere domeinnamen in Azure AD geverifieerd

**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`**-Deze claim moet Hallo id URI (Uniform Resource) van een Hallo geverifieerd domeinnamen die verbinding maken met de Hallo lokale federation-service (AD FS of 3e partij) verlenende Hallo token bevatten. U kunt in AD FS uitgifte transformatieregels die eruitzien zoals toepassingsgroepen onderstaande Hallo in die specifieke volgorde na Hallo toepassingsgroepen bovenstaande toevoegen. Houd er rekening mee dat één regel tooexplicitly probleem Hallo-regel voor gebruikers nodig is. In onderstaande Hallo regels, wordt een eerste regel voor het identificeren van gebruiker versus computerverificatie toegevoegd.

    @RuleName = "Issue account type with hello value User when its not a computer"
    NOT EXISTS(
    [
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "DJ"
    ]
    )
    => add(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "User"
    );
    
    @RuleName = "Capture UPN when AccountType is User and issue hello IssuerID"
    c1:[
        Type == "http://schemas.xmlsoap.org/claims/UPN"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "User"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = regexreplace(
        c1.Value, 
        ".+@(?<domain>.+)", 
        "http://${domain}/adfs/services/trust/"
        )
    );
    
    @RuleName = "Issue issuerID for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = "http://<verified-domain-name>/adfs/services/trust/"
    );


In bovenstaande Hallo-claim

- `$<domain>`Hallo AD FS-service-URL is
- `<verified-domain-name>`is een tijdelijke aanduiding moet u tooreplace met een van uw geverifieerde domeinnamen in Azure AD



Zie voor meer informatie over geverifieerde domeinnamen [toevoegen van een aangepast domein naam tooAzure Active Directory](active-directory-add-domain.md).  
een lijst van uw bedrijf geverifieerde domeinen tooget, kunt u Hallo [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet. 

![Get-MsolDomain](./media/active-directory-conditional-access-automatic-device-registration-setup/01.png)

### <a name="issue-immutableid-for-computer-when-one-for-users-exist-eg-alternate-login-id-is-set"></a>Onveranderbare id genoemd uitgeven voor computer, als een voor gebruikers bestaat (bijvoorbeeld alternatieve aanmeldings-ID is ingesteld)

**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`**-Deze claim moet een geldige waarde voor computers bevatten. In AD FS, kunt u een regel voor het transformeren van uitgifte als volgt:

    @RuleName = "Issue ImmutableID for computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ] 
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );

### <a name="helper-script-toocreate-hello-ad-fs-issuance-transform-rules"></a>Helper toocreate Hallo AD FS uitgifte transformatie scriptregels

Hallo kunt volgende script u met Hallo maken van Hallo uitgifte transformeren regels die hierboven worden beschreven.

    $multipleVerifiedDomainNames = $false
    $immutableIDAlreadyIssuedforUsers = $false
    $oneOfVerifiedDomainNames = 'example.com'   # Replace example.com with one of your verified domains
    
    $rule1 = '@RuleName = "Issue account type for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "DJ"
    );'

    $rule2 = '@RuleName = "Issue object GUID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/identity/claims/onpremobjectguid"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );'

    $rule3 = '@RuleName = "Issue objectSID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(claim = c2);'

    $rule4 = ''
    if ($multipleVerifiedDomainNames -eq $true) {
    $rule4 = '@RuleName = "Issue account type with hello value User when it is not a computer"
    NOT EXISTS(
    [
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "DJ"
    ]
    )
    => add(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "User"
    );
    
    @RuleName = "Capture UPN when AccountType is User and issue hello IssuerID"
    c1:[
        Type == "http://schemas.xmlsoap.org/claims/UPN"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "User"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = regexreplace(
        c1.Value, 
        ".+@(?<domain>.+)", 
        "http://${domain}/adfs/services/trust/"
        )
    );
    
    @RuleName = "Issue issuerID for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = "http://' + $oneOfVerifiedDomainNames + '/adfs/services/trust/"
    );'
    }

    $rule5 = ''
    if ($immutableIDAlreadyIssuedforUsers -eq $true) {
    $rule5 = '@RuleName = "Issue ImmutableID for computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ] 
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );'
    }

    $existingRules = (Get-ADFSRelyingPartyTrust -Identifier urn:federation:MicrosoftOnline).IssuanceTransformRules 

    $updatedRules = $existingRules + $rule1 + $rule2 + $rule3 + $rule4 + $rule5

    $crSet = New-ADFSClaimRuleSet -ClaimRule $updatedRules 

    Set-AdfsRelyingPartyTrust -TargetIdentifier urn:federation:MicrosoftOnline -IssuanceTransformRules $crSet.ClaimRulesString 

### <a name="remarks"></a>Opmerkingen 

- Dit script wordt Hallo regels toohello bestaande regels toegevoegd. Hallo-script worden niet uitgevoerd tweemaal omdat Hallo reeks regels zou twee keer worden toegevoegd. Zorg ervoor dat er geen overeenkomende regels bestaan voor deze claims (onder de bijbehorende voorwaarden Hallo) voordat Hallo script nogmaals uit te voeren.

- Als u meerdere geverifieerde domeinnamen hebben (zoals weergegeven in hello Azure AD-portal of via de cmdlet Get-MsolDomains Hallo), stelt u de waarde Hallo van **$multipleVerifiedDomainNames** in Hallo script te**$true**. Controleer ook of u een bestaande issuerid claim die mogelijk zijn gemaakt met Azure AD Connect of via andere middelen. Hier volgt een voorbeeld voor deze regel:


        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"]
        => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)",  "http://${domain}/adfs/services/trust/")); 

- Als u al uitgegeven een **onveranderbare id genoemd** claim voor gebruikersaccounts, stelt u Hallo-waarde van **$immutableIDAlreadyIssuedforUsers** in Hallo script te**$true**.

## <a name="step-3-enable-windows-down-level-devices"></a>Stap 3: Eerdere Windows-apparaten inschakelen

Als sommige van uw apparaten domein Windows downlevel-apparaten, moet u naar:

- Een beleid in Azure AD-tooenable tooregister apparaten van gebruikers instellen.
 
- Configureren van de lokale federation-service tooissue claims toosupport **geïntegreerde Windows-verificatie (IWA)** voor apparaatregistratie.
 
- Hello Azure AD apparaat verificatie eindpunt toohello lokale intranetzones tooavoid certificaat vraagt bij het verifiëren van Hallo apparaat toevoegen.

### <a name="set-policy-in-azure-ad-tooenable-users-tooregister-devices"></a>Beleid instellen in Azure AD-tooenable tooregister apparaten van gebruikers

tooregister Windows downlevel-apparaten, moet u ervoor dat gebruikers tooallow tooregister apparaten instellen in Azure AD hello wordt ingesteld toomake. In hello Azure-portal, kunt u deze instelling onder vinden:

`Azure Active Directory > Users and groups > Device settings`
    
Hallo volgende beleid moet worden ingesteld te**alle**: **gebruikers hun apparaten kunnen registreren met Azure AD**

![Apparaten registreren](./media/active-directory-conditional-access-automatic-device-registration-setup/23.png)


### <a name="configure-on-premises-federation-service"></a>Configureren van de lokale federation-service 

De lokale federation-service moet ondersteunen verlenende Hallo **authenticationmehod** en **wiaormultiauthn** claims tijdens het ontvangen van een verificatie aanvragen toohello Azure AD relying party die een resouce_params parameter met een gecodeerde waarde zoals hieronder:

    eyJQcm9wZXJ0aWVzIjpbeyJLZXkiOiJhY3IiLCJWYWx1ZSI6IndpYW9ybXVsdGlhdXRobiJ9XX0

    which decoded is {"Properties":[{"Key":"acr","Value":"wiaormultiauthn"}]}

Wanneer een dergelijke aanvraag afkomstig is, Hallo lokale federation-service Hallo-gebruiker met behulp van geïntegreerde Windows-verificatie moet worden geverifieerd en dit lukt, moet het Hallo na twee claims uitgeven:

    http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows
    http://schemas.microsoft.com/claims/wiaormultiauthn

In AD FS, moet u een regel voor het transformeren van uitgifte die verificatiemethode geeft via Hallo toevoegen.  

**tooadd met deze regel:**

1. Ga te in Hallo AD FS-beheerconsole`AD FS > Trust Relationships > Relying Party Trusts`.
2. Hallo Identiteitsplatform van Microsoft Office 365 relying party trust-object met de rechtermuisknop en selecteer vervolgens **Claimregels bewerken**.
3. Op Hallo **uitgifte Transformatieregels** tabblad **regel toevoegen**.
4. In Hallo **claimregel** lijst met sjablonen, selecteer **Claims verzenden met een aangepaste regel**.
5. Selecteer **volgende**.
6. In Hallo **naam Claimregel** in het vak **Auth methode Claimregel**.
7. In Hallo **claimregel** vak, type Hallo-regel:

    `c:[Type == "http://schemas.microsoft.com/claims/authnmethodsreferences"] => issue(claim = c);`

8. Typ op de federatieserver Hallo PowerShell-opdracht hieronder na het vervangen  **\<RPObjectName\>**  met Hallo relying party objectnaam voor uw Azure AD relying party trust-object. Dit object meestal heet **Identiteitsplatform van Microsoft Office 365**.
   
    `Set-AdfsRelyingPartyTrust -TargetName <RPObjectName> -AllowedAuthenticationClassReferences wiaormultiauthn`

### <a name="add-hello-azure-ad-device-authentication-end-point-toohello-local-intranet-zones"></a>Hello Azure AD apparaat verificatie eindpunt toohello Lokaal Intranet zones toevoegen

tooavoid certificaat wordt gevraagd wanneer gebruikers in het register apparaten verifiëren tooAzure AD kunt u een beleid tooyour domeinapparaten tooadd Hallo URL-zone toohello Lokaal Intranet in Internet Explorer na pushen:

`https://device.login.microsoftonline.com`

## <a name="step-4-control-deployment-and-rollout"></a>Stap 4: Implementatie van het besturingselement en implementatie

Wanneer u Hallo vereiste stappen hebt voltooid, worden apparaten die lid zijn van een domein gereed tooautomatically registreren met Azure AD. Alle domein op apparaten met Windows 10 Verjaardag Update en Windows Server 2016 automatisch registreren met Azure AD op het apparaat opnieuw wordt gestart of gebruikersaanmelding. Nieuwe apparaten registreren met Azure AD wanneer Hallo-apparaat opnieuw wordt gestart nadat Hallo domain join-bewerking is voltooid.

Apparaten die eerder met de werkplek zijn toegevoegd tooAzure AD (bijvoorbeeld voor Intune) overgang te zijn'*lid van een domein, geregistreerd bij AAD*"; maar het duurt even totdat dit proces toocomplete op alle apparaten vanwege toohello normaal de stroom van de domein- en gebruikersactiviteit.

### <a name="remarks"></a>Opmerkingen

- U kunt een Group Policy object toocontrol Hallo rollout van automatische inschrijving van Windows 10 en Windows Server 2016 domein computers gebruiken.

- Windows 10 November 2015 automatisch bijwerken registers met Azure AD **alleen** als Hallo implementatie Groepsbeleid-object is ingesteld.

- toorollout hello automatische registratie van Windows downlevel-computers, u kunt een [Windows Installer-pakket](#windows-installer-packages-for-non-windows-10-computers) toocomputers die u selecteert.

- Als u push-Hallo Group Policy object tooWindows 8.1 domein apparaten, worden registratie geprobeerd; maar het wordt aangeraden dat u Hallo [Windows Installer-pakket](#windows-installer-packages-for-non-windows-10-computers) tooregister al uw Windows downlevel-apparaten. 

### <a name="create-a-group-policy-object"></a>Een groepsbeleidsobject maken 

toocontrol hello rollout van automatische registratie van de huidige Windows-computers, moet u Hallo implementeren **Domeincomputers registreren als apparaten** Group Policy object toohello apparaten gewenste tooregister. U kunt bijvoorbeeld Hallo beleid tooan organisatie-eenheid of beveiligingsgroep tooa implementeren.

**tooset hello beleid:**

1. Open **Serverbeheer**, en ga te`Tools > Group Policy Management`.
2. Ga naar toohello domeinknooppunt dat overeenkomt met toohello domein waarvoor u tooactivate automatische registratie van de huidige Windows-computers.
3. Met de rechtermuisknop op **Group Policy Objects**, en selecteer vervolgens **nieuw**.
4. Typ een naam voor uw groepsbeleidsobject. Bijvoorbeeld: *automatische registratie tooAzure AD*. Selecteer **OK**.
5. Met de rechtermuisknop op uw nieuwe groepsbeleidsobject en selecteer vervolgens **bewerken**.
6. Ga te**Computerconfiguratie** > **beleid** > **Beheersjablonen** > **Windows Onderdelen** > **apparaatregistratie**. Met de rechtermuisknop op **Domeincomputers registreren als apparaten**, en selecteer vervolgens **bewerken**.
   
   > [!NOTE]
   > Deze groepsbeleidssjabloon gewijzigd van eerdere versies van de console Groepsbeleidsbeheer Hallo. Als u een eerdere versie van het Hallo-console gebruikt, gaat u verder te`Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`. 

7. Selecteer **ingeschakeld**, en selecteer vervolgens **toepassen**.
8. Selecteer **OK**.
9. Koppeling hello Group Policy object tooa locatie van uw keuze. Bijvoorbeeld, kunt u deze koppelen tooa specifieke organisatie-eenheid. Ook kan koppelt u het tooa beveiligingsgroep met computers die automatisch wordt geregistreerd bij Azure AD. tooset dit beleid voor alle Windows 10 en Windows Server 2016 Domeincomputers in uw organisatie, koppeling Hallo Group Policy object toohello domein.

### <a name="windows-installer-packages-for-non-windows-10-computers"></a>Windows Installer-pakketten voor Windows 10-computers

tooregister domein Windows downlevel-computers in een federatieve omgeving, kunt u downloaden en installeren van deze Windows Installer-pakket (.msi) van Downloadcentrum op Hallo [Microsoft Workplace Join voor Windows 10-computers](https://www.microsoft.com/en-us/download/details.aspx?id=53554) pagina.

U kunt Hallo pakket implementeren met behulp van een software-distributiesysteem zoals System Center Configuration Manager. Hallo pakket ondersteunt Hallo standaard stille installatieopties Hello *stille* parameter. System Center Configuration Manager Current Branch biedt extra voordelen van eerdere versies, zoals Hallo mogelijkheid tootrack voltooid registraties. Zie voor meer informatie [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).

Hallo-installatieprogramma maakt een geplande taak op Hallo-systeem die wordt uitgevoerd in de context van de gebruiker Hallo. Hallo-taak wordt geactiveerd wanneer Hallo gebruiker zich aanmeldt tooWindows. Hallo taak registreert achtergrond Hallo-apparaat met Azure AD met gebruikersreferenties Hallo na verificatie met behulp van geïntegreerde Windows-verificatie. toosee hello geplande taak in het Hallo-apparaat, gaat u te**Microsoft** > **Workplace Join**, en ga toohello Task Scheduler-bibliotheek.

## <a name="step-5-verify-registered-devices"></a>Stap 5: Controleren of de geregistreerde apparaten

U kunt geslaagde geregistreerde apparaten in uw organisatie controleren met behulp van Hallo [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in Hallo [Azure Active Directory PowerShell-module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).

Hallo-uitvoer van deze cmdlet toont de apparaten die zijn geregistreerd bij Azure AD. tooget alle apparaten gebruiken Hallo **-alle** parameter en filter ze met behulp van Hallo **deviceTrustType** eigenschap. Verbonden met het domein apparaten hebben een waarde van **domein**.

## <a name="next-steps"></a>Volgende stappen

* [Automatische apparaatregistratie Veelgestelde vragen](active-directory-device-registration-faq.md)
* [Automatische registratie van domein het oplossen van problemen die lid zijn van computers tooAzure AD – Windows 10 en Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md)
* [Automatische registratie van domein het oplossen van problemen die lid zijn van computers tooAzure AD – Windows 10](active-directory-device-registration-troubleshoot-windows-legacy.md)
* [Voorwaardelijke toegang van Azure Active Directory](active-directory-conditional-access-azure-portal.md)



<!--Image references-->
[1]: ./media/active-directory-conditional-access-automatic-device-registration-setup/12.png
