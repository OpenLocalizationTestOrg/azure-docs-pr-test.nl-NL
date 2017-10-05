---
title: Het configureren van automatische registratie van Windows-domein-apparaten met Azure Active Directory | Microsoft Docs
description: Instellen van uw Windows-domein apparaten automatisch en zonder tussenkomst registreren bij Azure Active Directory.
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
ms.openlocfilehash: dccd7df6a5f85df4179c7ea7cfc476cfb57f48c0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-automatic-registration-of-windows-domain-joined-devices-with-azure-active-directory"></a>Automatische registratie van Windows-domein-apparaten met Azure Active Directory configureren

Gebruik [voorwaardelijke toegang voor Azure Active Directory op basis van apparaten](active-directory-conditional-access-azure-portal.md), uw computers moeten worden geregistreerd bij Azure Active Directory (Azure AD). U kunt een lijst met geregistreerde apparaten krijgen in uw organisatie met behulp van de [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in de [Azure Active Directory PowerShell-module](/powershell/azure/install-msonlinev1?view=azureadps-2.0). 

Dit artikel bevat de stappen voor het configureren van de automatische registratie van Windows-domein-apparaten met Azure AD in uw organisatie.


Voor meer informatie over:

- Voorwaardelijke toegang, Zie [voorwaardelijke toegang voor Azure Active Directory op basis van apparaten](active-directory-conditional-access-azure-portal.md). 
- Windows 10-apparaten in de werkplek en de uitgebreide ervaring als geregistreerd in Azure AD, Zie [Windows 10 voor ondernemingen: apparaten gebruiken voor het werk](active-directory-azureadjoin-windows10-devices-overview.md).
- Windows 10 Enterprise E3 in CSP, Zie de [Windows 10 Enterprise E3 in het overzicht van de CSP](https://docs.microsoft.com/en-us/windows/deployment/windows-10-enterprise-e3-overview).


## <a name="before-you-begin"></a>Voordat u begint

Voordat u begint met het configureren van de automatische registratie van Windows-domein-apparaten in uw omgeving, moet u dat vertrouwd raken met de ondersteunde scenario's en de beperkingen.  

In dit onderwerp gebruikt ter verbetering van de leesbaarheid van de beschrijvingen van de volgende voorwaarden: 

- **Huidige Windows-apparaten** -deze term verwijst naar domein apparaten met Windows 10 of Windows Server 2016.
- **Apparaten met Windows downlevel-** -deze term verwijst naar alle **ondersteund** domein Windows-apparaten die geen actieve Windows 10 of Windows Server 2016.  


### <a name="windows-current-devices"></a>Huidige Windows-apparaten

- Voor apparaten waarop het besturingssysteem van de Windows-bureaublad wordt uitgevoerd, wordt u aangeraden speciale Update (versie 1607) voor Windows 10 of hoger. 
- De registratie van de huidige Windows-apparaten **is** in niet-gefedereerde omgevingen zoals wachtwoord-hash-synchronisatie configuraties ondersteund.  


### <a name="windows-down-level-devices"></a>Eerdere Windows-apparaten

- De volgende Windows downlevel-apparaten worden ondersteund:
    - Windows 8.1
    - Windows 7
    - Windows Server 2012 R2
    - Windows Server 2012
    - Windows Server 2008 R2
- De registratie van apparaten met Windows downlevel- **is** in niet-gefedereerde omgevingen via naadloze eenmalige aanmelding ondersteund [Azure Active Directory naadloze eenmalige aanmelding](https://aka.ms/hybrid/sso).
- De registratie van apparaten met Windows downlevel- **is niet** ondersteund voor apparaten met behulp van zwervende profielen. Als u gebruik van zwervende profielen of instellingen, gebruikt u Windows 10.



## <a name="prerequisites"></a>Vereisten

Voordat u begint met het inschakelen van de automatische registratie van apparaten in uw organisatie lid van een domein, moet u ervoor zorgen dat u altijd een actuele versie van Azure AD connect.

Azure AD Connect:

- Houdt de koppeling tussen de computeraccount in uw on-premises Active Directory (AD) en het apparaatobject in Azure AD. 
- Andere apparaat gerelateerde functies, zoals Windows Hello voor bedrijven.



## <a name="configuration-steps"></a>Configuratiestappen

Dit onderwerp bevat de vereiste stappen voor alle standaardconfiguratie-scenario's.  
Gebruik de volgende tabel om een overzicht van de stappen die nodig voor uw scenario zijn:  



| Stappen                                      | Windows huidige en het wachtwoord-hash-synchronisatie | De huidige Windows- en Federatie | Windows downlevel- |
| :--                                        | :-:                                    | :-:                            | :-:                |
| Stap 1: Een serviceverbindingspunt configureren | ![Selecteren][1]                            | ![Selecteren][1]                    | ![Selecteren][1]        |
| Stap 2: De uitgifte van claims instellen           |                                        | ![Selecteren][1]                    | ![Selecteren][1]        |
| Stap 3: Windows 10-apparaten inschakelen      |                                        |                                | ![Selecteren][1]        |
| Stap 4: Implementatie van het besturingselement en implementatie     | ![Selecteren][1]                            | ![Selecteren][1]                    | ![Selecteren][1]        |
| Stap 5: Controleren of de geregistreerde apparaten          | ![Selecteren][1]                            | ![Selecteren][1]                    | ![Selecteren][1]        |



## <a name="step-1-configure-service-connection-point"></a>Stap 1: Een serviceverbindingspunt configureren

Het service connection point (SCP)-object wordt gebruikt door uw apparaten tijdens de registratie voor het detecteren van informatie over het Azure AD-tenant. Het SCP-object voor de automatische registratie van apparaten die lid zijn van een domein moet in uw lokale Active Directory (AD) bestaan in de configuratie van de naamgeving van de partitie van de context van de forest van de computer. Er is slechts één configuratienaamgevingscontext per forest. In een configuratie met meerdere forests met Active Directory moet het service connection point in alle forests met computers domein bestaan.

U kunt de [ **Get-ADRootDSE** ](https://technet.microsoft.com/library/ee617246.aspx) cmdlet voor het ophalen van de configuratienaamgevingscontext van het forest.  

Voor een forest met de naam van de Active Directory-domein *fabrikam.com*, is de configuratienaamgevingscontext:

`CN=Configuration,DC=fabrikam,DC=com`

Het SCP-object voor de automatische registratie van apparaten die lid zijn van een domein bevindt in uw forest zich op:  

`CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,[Your Configuration Naming Context]`

Afhankelijk van hoe u Azure AD Connect hebt geïmplementeerd, het SCP-object mogelijk al zijn geconfigureerd.
U kunt controleren of het object bestaat en ophalen van de detectie van waarden met behulp van de volgende Windows PowerShell-script: 

    $scp = New-Object System.DirectoryServices.DirectoryEntry;

    $scp.Path = "LDAP://CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,CN=Configuration,DC=fabrikam,DC=com";

    $scp.Keywords;

De **$scp. Trefwoorden** uitvoer toont de Azure AD-tenant-informatie, bijvoorbeeld:

    azureADName:microsoft.com
    azureADId:72f988bf-86f1-41af-91ab-2d7cd011db47

Als het serviceverbindingspunt niet bestaat, kunt u dit maken door het uitvoeren van de `Initialize-ADSyncDomainJoinedComputerSync` cmdlet uit op uw Azure AD Connect-server. Enterprise admin credential is vereist voor deze cmdlet uitvoeren.  
De cmdlet:

- Maakt het serviceverbindingspunt wordt gehost in Azure AD Connect is verbonden met Active Directory-forest. 
- Moet u opgeven de `AdConnectorAccount` parameter. Dit is het account dat is geconfigureerd als Active Directory connector-account in Azure AD connect. 


Het volgende script toont een voorbeeld voor het gebruik van de cmdlet. In dit script `$aadAdminCred = Get-Credential` , moet u een gebruikersnaam typt. U moet de gebruikersnaam van de in de indeling van de principal-naam (User Principal Name) gebruiker opgeven (`user@example.com`). 


    Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1";

    $aadAdminCred = Get-Credential;

    Initialize-ADSyncDomainJoinedComputerSync –AdConnectorAccount [connector account name] -AzureADCredentials $aadAdminCred;

De `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:

- Maakt gebruik van de Active Directory PowerShell-module is afhankelijk van de Active Directory Web Services uitgevoerd op een domeincontroller. Active Directory Web Services wordt ondersteund op domeincontrollers met Windows Server 2008 R2 en hoger.
- Wordt alleen ondersteund door de **MSOnline PowerShell moduleversie 1.1.166.0**. Deze module downloaden, gebruiken deze [koppeling](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).   

Gebruik het onderstaande script voor het maken van het service connection point voor domeincontrollers met Windows Server 2008 of eerdere versies.

In een configuratie met meerdere forests, moet u het volgende script voor het maken van het service connection point in elk forest waar computers bestaan:
 
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

In een federatieve Azure AD-configuratie apparaten zijn afhankelijk van de Active Directory Federation Services (AD FS) of een 3e party on-premises federation-service om te verifiëren met Azure AD. Apparaten verifiëren als u een toegangstoken registreren op basis van de Azure Active Directory Device Registration Service (DRS Azure).

Windows huidige apparaten met behulp van geïntegreerde Windows-verificatie naar een actieve WS-Trust-eindpunt (1.3 of 2005 versies verifiëren) gehost door de lokale federation-service.

> [!NOTE]
> Wanneer u AD FS, ofwel **adfs/services/trust/13/windowstransport** of **adfs/services/trust/2005/windowstransport** moet zijn ingeschakeld. Als u de webproxy verificatie gebruikt, zorg er ook voor dat dit eindpunt is gepubliceerd via de proxy. U kunt zien welke eindpunten worden ingeschakeld via de AD FS-beheerconsole onder **Service > eindpunten**.
>
>Als u geen AD FS als de lokale federation-service, volg de instructies van uw leverancier om ervoor te zorgen dat ze WS-Trust 1.3 of 2005 eindpunten en deze zijn gepubliceerd via het Metadata Exchange-bestand (MEX) ondersteunen.

De volgende claims moeten bestaan in het token dat is ontvangen door Azure DRS voor apparaatregistratie te voltooien. Azure DRS maakt een apparaatobject in Azure AD met enkele van deze informatie die vervolgens door Azure AD Connect gebruikt wordt het zojuist gemaakte apparaatobject koppelen aan de computer account on-premises.

* `http://schemas.microsoft.com/ws/2012/01/accounttype`
* `http://schemas.microsoft.com/identity/claims/onpremobjectguid`
* `http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`

Als u meer dan een geverifieerde domeinnaam hebt, moet u bieden de volgende claim voor computers:

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`

Als u al een claim onveranderbare id genoemd (bijv, alternatieve aanmeldings-ID) moet u een overeenkomende claim voor computers:

* `http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`

In de volgende secties vindt vinden u informatie over:
 
- De waarden elke claim moet hebben.
- Hoe een definitie eruit als in AD FS

De definitie helpt u om te controleren of de waarden aanwezig zijn of als u nodig hebt om ze te maken.

> [!NOTE]
> Als u AD FS niet voor de lokale federation-server gebruikt, volgt u de leverancier van uw instructies voor het maken van de juiste configuratie om deze claims te verlenen.

### <a name="issue-account-type-claim"></a>Probleem account type claim

**`http://schemas.microsoft.com/ws/2012/01/accounttype`**-Deze claim moet een waarde van bevatten **DJ**, die het apparaat als een domein gekoppelde computer identificeert. U kunt een regel voor het transformeren van uitgifte die uitziet toevoegen in AD FS:

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

### <a name="issue-objectguid-of-the-computer-account-on-premises"></a>Probleem objectGUID van de computer account on-premises

**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`**-Deze claim moet bevatten de **objectGUID** waarde van de lokale computeraccount. U kunt een regel voor het transformeren van uitgifte die uitziet toevoegen in AD FS:

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
 
### <a name="issue-objectsid-of-the-computer-account-on-premises"></a>Probleem objectSID van de computer account on-premises

**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`**-Deze claim moet bevatten de de **objectSid** waarde van de lokale computeraccount. U kunt een regel voor het transformeren van uitgifte die uitziet toevoegen in AD FS:

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

**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`**-Deze claim moet de id URI (Uniform Resource) van een van de geverifieerde domeinnamen die verbinding met de lokale federation-service (AD FS of 3e partij maken) bevatten voor het uitgeven van het token. U kunt in AD FS uitgifte transformatieregels die lijken op die hieronder in die specifieke volgorde na de bovenstaande waarden toevoegen. Houd er rekening mee dat één regel expliciet uitgeven van de regel voor gebruikers nodig is. Een eerste regel gebruiker versus computerverificatie identificeren in de onderstaande regels is toegevoegd.

    @RuleName = "Issue account type with the value User when its not a computer"
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
    
    @RuleName = "Capture UPN when AccountType is User and issue the IssuerID"
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


In de bovenstaande claim

- `$<domain>`de URL van de service AD FS
- `<verified-domain-name>`is een tijdelijke aanduiding die u wilt vervangen door een van uw geverifieerde domeinnamen in Azure AD



Zie voor meer informatie over geverifieerde domeinnamen [een aangepaste domeinnaam toevoegen aan Azure Active Directory](active-directory-add-domain.md).  
Als u een lijst van uw bedrijf geverifieerde domeinen, kunt u de [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet. 

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

### <a name="helper-script-to-create-the-ad-fs-issuance-transform-rules"></a>Help-script voor het maken van de AD FS-uitgifte transformatieregels

Het volgende script helpt u bij het maken van de uitgifte transformeren regels die hierboven worden beschreven.

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
    $rule4 = '@RuleName = "Issue account type with the value User when it is not a computer"
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
    
    @RuleName = "Capture UPN when AccountType is User and issue the IssuerID"
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

- Dit script worden de regels toegevoegd aan de bestaande regels. Het script niet twee keer uitgevoerd omdat de set regels tweemaal zou worden toegevoegd. Zorg ervoor dat er geen overeenkomende regels bestaan voor deze claims (onder de bijbehorende voorwaarden) voordat u het script opnieuw uitvoert.

- Als u meerdere geverifieerde domeinnamen (zoals weergegeven in de Azure AD-portal of via de cmdlet Get-MsolDomains) hebt, stel de waarde van **$multipleVerifiedDomainNames** in het script naar **$true**. Controleer ook of u een bestaande issuerid claim die mogelijk zijn gemaakt met Azure AD Connect of via andere middelen. Hier volgt een voorbeeld voor deze regel:


        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"]
        => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)",  "http://${domain}/adfs/services/trust/")); 

- Als u al uitgegeven een **onveranderbare id genoemd** claim voor gebruikersaccounts, stelt u de waarde van **$immutableIDAlreadyIssuedforUsers** in het script naar **$true**.

## <a name="step-3-enable-windows-down-level-devices"></a>Stap 3: Eerdere Windows-apparaten inschakelen

Als sommige van uw apparaten domein Windows downlevel-apparaten, moet u naar:

- Stel een beleid in Azure AD, zodat gebruikers kunnen apparaten registreren.
 
- Configureren van de lokale federation-service voor het verlenen van claims voor de ondersteuning van **geïntegreerde Windows-verificatie (IWA)** voor apparaatregistratie.
 
- Het verificatie-eindpunt van de Azure AD-apparaat toevoegen aan het lokale Intranet-zones certificaatmeldingen voorkomen wanneer het apparaat te verifiëren.

### <a name="set-policy-in-azure-ad-to-enable-users-to-register-devices"></a>Beleid instellen in Azure AD, zodat gebruikers kunnen apparaten registreren

Voor het registreren van eerdere Windows-apparaten, moet u ervoor zorgen dat de instelling waarmee gebruikers apparaten registreren in Azure AD is ingesteld. U kunt deze instelling onder vinden in de Azure-portal:

`Azure Active Directory > Users and groups > Device settings`
    
Het volgende beleid moet worden ingesteld op **alle**: **gebruikers hun apparaten kunnen registreren met Azure AD**

![Apparaten registreren](./media/active-directory-conditional-access-automatic-device-registration-setup/23.png)


### <a name="configure-on-premises-federation-service"></a>Configureren van de lokale federation-service 

De lokale federation-service moet ondersteuning voor het uitgeven de **authenticationmehod** en **wiaormultiauthn** claims tijdens het ontvangen van een verificatieaanvraag naar de Azure AD relying party die een parameter resouce_params met een gecodeerde waarde, zoals hieronder wordt weergegeven:

    eyJQcm9wZXJ0aWVzIjpbeyJLZXkiOiJhY3IiLCJWYWx1ZSI6IndpYW9ybXVsdGlhdXRobiJ9XX0

    which decoded is {"Properties":[{"Key":"acr","Value":"wiaormultiauthn"}]}

Wanneer een dergelijke aanvraag afkomstig is, wordt de gebruiker met behulp van geïntegreerde Windows-verificatie moet worden geverifieerd door de lokale federation-service en dit lukt, moet deze de volgende twee claims uitgeven:

    http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows
    http://schemas.microsoft.com/claims/wiaormultiauthn

In AD FS, moet u een regel voor het transformeren van uitgifte die geeft via de verificatiemethode toevoegen.  

**Deze regel toevoegen:**

1. Ga in de AD FS-beheerconsole naar `AD FS > Trust Relationships > Relying Party Trusts`.
2. Met de rechtermuisknop op het Identiteitsplatform van Microsoft Office 365 relying party trust object en selecteer vervolgens **Claimregels bewerken**.
3. Op de **uitgifte Transformatieregels** tabblad **regel toevoegen**.
4. In de **claimregel** lijst met sjablonen, selecteer **Claims verzenden met een aangepaste regel**.
5. Selecteer **volgende**.
6. In de **naam Claimregel** in het vak **Auth methode Claimregel**.
7. In de **claimregel** typt u de volgende regel:

    `c:[Type == "http://schemas.microsoft.com/claims/authnmethodsreferences"] => issue(claim = c);`

8. Typ op de federatieserver de PowerShell-opdracht hieronder na het vervangen  **\<RPObjectName\>**  met de relying party objectnaam voor uw Azure AD relying party trust-object. Dit object meestal heet **Identiteitsplatform van Microsoft Office 365**.
   
    `Set-AdfsRelyingPartyTrust -TargetName <RPObjectName> -AllowedAuthenticationClassReferences wiaormultiauthn`

### <a name="add-the-azure-ad-device-authentication-end-point-to-the-local-intranet-zones"></a>Het verificatie-eindpunt van de Azure AD-apparaat toevoegen aan de zones Lokaal Intranet

Om te voorkomen dat certificaat wordt gevraagd wanneer gebruikers in het register apparaten verifiëren met Azure AD kunt u een beleid pushen naar uw apparaten domein de volgende URL toevoegen aan de zone Lokaal Intranet in Internet Explorer:

`https://device.login.microsoftonline.com`

## <a name="step-4-control-deployment-and-rollout"></a>Stap 4: Implementatie van het besturingselement en implementatie

Wanneer u de vereiste stappen hebt voltooid, worden apparaten die lid zijn van een domein gereed voor het automatisch wordt geregistreerd bij Azure AD. Alle domein op apparaten met Windows 10 Verjaardag Update en Windows Server 2016 automatisch registreren met Azure AD op het apparaat opnieuw wordt gestart of gebruikersaanmelding. Nieuwe apparaten registreren met Azure AD wanneer het apparaat opnieuw wordt gestart nadat de domein-join-bewerking is voltooid.

Apparaten die eerder in de werkplek is gekoppeld aan de overgang naar Azure AD (bijvoorbeeld voor Intune) '*lid van een domein, geregistreerd bij AAD*"; maar het duurt enige tijd voor dit proces te voltooien op alle apparaten als gevolg van de normale stroom van de domein- en gebruikersactiviteit.

### <a name="remarks"></a>Opmerkingen

- U kunt een Group Policy object gebruiken voor het beheren van de implementatie van automatische inschrijving van Windows 10 en Windows Server 2016 domein computers.

- Windows 10 November 2015 automatisch bijwerken registers met Azure AD **alleen** als het groepsbeleidsobject van de implementatie is ingesteld.

- De automatische registratie van Windows-computers voor downlevel-implementatie, u kunt implementeren een [Windows Installer-pakket](#windows-installer-packages-for-non-windows-10-computers) op computers die u selecteert.

- Als u het groepsbeleidsobject naar domein Windows 8.1-apparaten pushen, worden registratie geprobeerd; maar het wordt aangeraden dat u de [Windows Installer-pakket](#windows-installer-packages-for-non-windows-10-computers) al uw Windows downlevel-apparaten te registreren. 

### <a name="create-a-group-policy-object"></a>Een groepsbeleidsobject maken 

Voor het beheren van de implementatie van automatische inschrijving van huidige Windows-computers, implementeert u de **Domeincomputers registreren als apparaten** groepsbeleidsobject voor de apparaten die u wilt registreren. U kunt bijvoorbeeld het beleid implementeren naar een organisatie-eenheid of aan een beveiligingsgroep.

**Het beleid instellen:**

1. Open **Serverbeheer**, en ga vervolgens naar `Tools > Group Policy Management`.
2. Ga naar het knooppunt dat overeenkomt met het domein waar u wilt activeren, automatische registratie van de huidige Windows-computers.
3. Met de rechtermuisknop op **Group Policy Objects**, en selecteer vervolgens **nieuw**.
4. Typ een naam voor uw groepsbeleidsobject. Bijvoorbeeld: *automatische registratie bij Azure AD*. Selecteer **OK**.
5. Met de rechtermuisknop op uw nieuwe groepsbeleidsobject en selecteer vervolgens **bewerken**.
6. Ga naar **Computerconfiguratie** > **beleid** > **Beheersjablonen** > **Windows-onderdelen** > **apparaatregistratie**. Met de rechtermuisknop op **Domeincomputers registreren als apparaten**, en selecteer vervolgens **bewerken**.
   
   > [!NOTE]
   > Deze groepsbeleidssjabloon gewijzigd van eerdere versies van de console Groepsbeleidsbeheer. Als u van een eerdere versie van de console gebruikmaakt, gaat u naar `Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`. 

7. Selecteer **ingeschakeld**, en selecteer vervolgens **toepassen**.
8. Selecteer **OK**.
9. Het groepsbeleidsobject koppelen naar een locatie van uw keuze. Bijvoorbeeld, kunt u deze koppelen aan een specifieke organisatie-eenheid. U kan ook deze koppelen aan een specifieke beveiligingsgroep met computers die automatisch wordt geregistreerd bij Azure AD. U dit beleid instellen voor alle Windows 10 en Windows Server 2016 Domeincomputers in uw organisatie, het groepsbeleidsobject aan het domein te koppelen.

### <a name="windows-installer-packages-for-non-windows-10-computers"></a>Windows Installer-pakketten voor Windows 10-computers

Als u wilt registreren domein Windows downlevel-computers in een federatieve omgeving, kunt u downloaden en installeren van deze Windows Installer-pakket (.msi) van Downloadcentrum op de [Microsoft Workplace Join voor Windows 10-computers](https://www.microsoft.com/en-us/download/details.aspx?id=53554) pagina.

U kunt het pakket implementeren met behulp van een software-distributiesysteem zoals System Center Configuration Manager. Het pakket ondersteunt de standard stille installatie-opties, waarbij de *stille* parameter. System Center Configuration Manager Current Branch biedt extra voordelen van eerdere versies, zoals de mogelijkheid om bij te houden van voltooide registraties. Zie voor meer informatie [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).

Het installatieprogramma maakt een geplande taak op het systeem dat wordt uitgevoerd in de context van de gebruiker. De taak wordt geactiveerd wanneer de gebruiker zich aanmeldt bij Windows. De taak wordt het apparaat achtergrond geregistreerd bij Azure AD met referenties van de gebruiker na verificatie met behulp van geïntegreerde Windows-verificatie. De geplande taak, het apparaat, Ga naar **Microsoft** > **Workplace Join**, en gaat u naar de bibliotheek voor Taakplanner.

## <a name="step-5-verify-registered-devices"></a>Stap 5: Controleren of de geregistreerde apparaten

U kunt geslaagde geregistreerde apparaten in uw organisatie controleren met behulp van de [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in de [Azure Active Directory PowerShell-module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).

De uitvoer van deze cmdlet toont de apparaten die zijn geregistreerd bij Azure AD. Als u alle apparaten, gebruikt de **-alle** parameter, en ze filteren met behulp van de **deviceTrustType** eigenschap. Verbonden met het domein apparaten hebben een waarde van **domein**.

## <a name="next-steps"></a>Volgende stappen

* [Automatische apparaatregistratie Veelgestelde vragen](active-directory-device-registration-faq.md)
* [Het oplossen van automatische registratie van domein computers toegevoegd aan Azure AD. – Windows 10 en Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md)
* [Het oplossen van automatische registratie van domein computers toegevoegd aan Azure AD. – Windows 10](active-directory-device-registration-troubleshoot-windows-legacy.md)
* [Voorwaardelijke toegang van Azure Active Directory](active-directory-conditional-access-azure-portal.md)



<!--Image references-->
[1]: ./media/active-directory-conditional-access-automatic-device-registration-setup/12.png
